# Prisma 7 vs Drizzle ORM: Detailed Comparison (March 2026)

> Research for Emuni nanny marketplace. Backend: NestJS 11 + Fastify v5, PostgreSQL 16 via Supabase, TypeScript strict. Solo developer.

---

## 1. Prisma 7 Current State (March 2026)

### Version: 7.4.2 (latest as of March 2026)

Prisma 7 is the most significant architectural overhaul in Prisma's history. The entire Rust-based query engine has been removed and replaced with a pure TypeScript + WebAssembly runtime.

### What's New in v7

| Feature | Details |
|---------|---------|
| **Rust engine removed** | Query compiler now runs as a WASM module on the JS main thread. No more Rust binary downloads during `npm install`. |
| **Bundle size** | Reduced from ~14MB to ~1.6MB (90% smaller). 600KB gzipped. |
| **Query performance** | Up to 3.4x faster queries by eliminating cross-language JS-to-Rust serialization overhead. |
| **Type generation** | 98% fewer types to evaluate (collaboration with David Blass, creator of ArkType). 70% faster full type checks vs previous versions. |
| **prisma.config.ts** | New TypeScript-based config file replaces schema-level datasource config. Connection URLs now go here, not in schema.prisma. |
| **Generated code location** | Moved out of `node_modules` into a project directory (e.g., `src/generated/prisma`). |
| **Driver adapters mandatory** | All database connections now require a driver adapter (e.g., `@prisma/adapter-pg` for PostgreSQL). |
| **Mapped enums** | Long-requested feature: `@map` on enums now works properly. |
| **New Prisma Studio** | Rebuilt, smaller, supports relationship visualization, remote DB via `--url` flag. Currently supports Postgres, MySQL, SQLite only. |
| **TypedSQL** | Write `.sql` files with fully typed inputs/outputs, used alongside Prisma Client. |

**Source:** [Prisma 7 Release Announcement](https://www.prisma.io/blog/announcing-prisma-orm-7-0-0), [Prisma Architecture Shift Blog](https://www.prisma.io/blog/from-rust-to-typescript-a-new-chapter-for-prisma-orm)

### Why Remove Rust?

Counterintuitive but validated: the JavaScript-to-Rust communication layer (serialization/deserialization) was the bottleneck, not the Rust code itself. Removing the cross-language boundary eliminated that overhead entirely.

**Source:** [InfoQ: Prisma 7 Performance Gains](https://www.infoq.com/news/2026/01/prisma-7-performance/)

### Migration System

- `prisma migrate dev` generates SQL migration files in `/prisma/migrations/`, fully customizable.
- **Shadow database required** for `migrate dev` -- Prisma creates a temporary DB to diff schema changes. This requires CREATE DATABASE permissions, which can be problematic on some cloud hosts. On Supabase, you can configure a separate shadow database URL.
- `prisma db push` is available for rapid prototyping (no migration files, just pushes schema changes directly).
- **Breaking change in v7:** `migrate dev` and `db push` no longer auto-run `prisma generate`. You must run it explicitly.
- **Breaking change in v7:** Automatic seed execution after migrations has been removed.

**Source:** [Prisma Migrate Documentation](https://www.prisma.io/docs/orm/prisma-migrate/getting-started), [Shadow Database Docs](https://www.prisma.io/docs/orm/prisma-migrate/understanding-prisma-migrate/shadow-database)

### NestJS Integration

- Official community package: `nestjs-prisma` (v0.27.0, published ~Jan 2026). Provides `PrismaModule` and `PrismaService` for NestJS dependency injection.
- **Critical gotcha:** Prisma 7 defaults to ESM output, but NestJS uses CommonJS. You MUST set `moduleFormat = "cjs"` in the generator block of `schema.prisma`. Without this, NestJS will fail at runtime with module resolution errors.
- Well-documented: Prisma has an [official NestJS guide](https://www.prisma.io/docs/guides/nestjs), and NestJS docs have a [Prisma integration page](https://deepwiki.com/nestjs/docs.nestjs.com/3.3-prisma-integration).

**Source:** [NestJS + Prisma 2026 Guide](https://dev.to/manendrav/how-to-set-up-nestjs-with-prisma-and-postgresql-2026-complete-guide-2da7), [nestjs-prisma npm](https://www.npmjs.com/package/nestjs-prisma)

### Supabase Compatibility

- Works with Supabase PostgreSQL via `@prisma/adapter-pg` driver adapter.
- Connection pooling: Use the Supabase pooled connection string (Supavisor) with `?pgbouncer=true` appended. This disables prepared statements, which Supavisor in transaction mode does not support.
- Migrations: Use the direct (non-pooled) connection string for `prisma migrate dev`; use the pooled string for runtime `PrismaClient`.
- Configuration is done in `prisma.config.ts` (new in v7).

**Source:** [Prisma Supabase Docs](https://supabase.com/docs/guides/database/prisma), [Prisma Supavisor Config](https://supabase.github.io/supavisor/orms/prisma/)

### Edge Runtime Support

- Prisma 7 was designed for edge compatibility (no Rust binary = no binary dependency issues).
- **However:** Cloudflare Workers currently broken -- Prisma 7 compiles query compiler WASM at runtime, which Cloudflare blocks ("Wasm code generation disallowed by embedder"). Workaround: downgrade to Prisma 6.19 for Workers. (Not relevant for NestJS on AWS, but worth noting.)
- Vercel Edge Functions: In Preview, works with Prisma Accelerate.

**Source:** [Prisma Edge Deployment Docs](https://www.prisma.io/docs/orm/prisma-client/deployment/edge/overview), [GitHub Issue #28657](https://github.com/prisma/prisma/issues/28657)

### PostGIS / Geolocation Support

- **No native PostGIS support as of March 2026.** This is a long-standing request (GitHub issue #1798, opened 2020; issue #2789).
- Workaround: Use `$queryRaw` or `$executeRaw` for all spatial queries (ST_Distance, ST_DWithin, etc.).
- You can store geometry columns using `@db.Geometry` annotation but cannot query them through the Prisma Client API -- raw SQL only.
- Native PostGIS support is planned for 2026 but no release date confirmed.

**Source:** [GitHub Issue #1798](https://github.com/prisma/prisma/issues/1798), [GitHub Issue #25768](https://github.com/prisma/prisma/issues/25768), [PostGIS Workaround Guide](https://freddydumont.com/blog/prisma-postgis)

### Known Issues / Limitations (March 2026)

1. **Performance regression in v7.3:** Some users report 50%+ slower queries than Prisma 6 under high concurrency. The WASM query compiler runs synchronously on the JS main thread, blocking the event loop during compilation. A `compilerBuild` option was added in 7.3.0 to mitigate this.
2. **Shadow database requirement:** `prisma migrate dev` needs CREATE DATABASE permissions -- can be awkward with managed Supabase DBs.
3. **ESM/CJS friction with NestJS:** Requires explicit `moduleFormat = "cjs"` configuration.
4. **BigInt precision loss:** When using `relationJoins` with BigInt fields, JavaScript's `JSON.parse` loses precision for integers > Number.MAX_SAFE_INTEGER.
5. **No native PostGIS support:** All spatial queries must use raw SQL.

**Source:** [GitHub Issue #29099](https://github.com/prisma/prisma/issues/29099), [Prisma Limitations Docs](https://www.prisma.io/docs/orm/prisma-migrate/understanding-prisma-migrate/limitations-and-known-issues)

---

## 2. Drizzle ORM Current State (March 2026)

### Version: 0.45.1 (stable) / 1.0.0-beta.16 (beta)

Drizzle has NOT reached v1.0 stable. The v1 roadmap shows ~98% completion, but no stable release date has been announced. The current recommended version for production is 0.45.x, with v1 betas available for early adopters.

### Key Features

| Feature | Details |
|---------|---------|
| **Architecture** | Pure TypeScript, zero dependencies, no binary engines. ~7.4KB minified+gzipped. |
| **Schema definition** | Code-first: define tables in TypeScript files. No separate schema language, no code generation step. |
| **Query API** | SQL-like builder (`select().from().where()`) that maps directly to SQL constructs. Also has a "relational query" API for Prisma-like convenience. |
| **SQL control** | You see what SQL is generated. "If you know SQL, you know Drizzle." |
| **Database support** | PostgreSQL, MySQL, SQLite, plus serverless variants (Supabase, Neon, PlanetScale, Cloudflare D1, Turso). |
| **No generation step** | Types are inferred from your schema definitions at save time. No `generate` command needed. |
| **Validator consolidation** | Zod/Valibot validators moved into the main drizzle-orm package. |
| **Gel dialect** | New PostgreSQL-compatible Gel dialect added. |

**Source:** [Drizzle ORM Homepage](https://orm.drizzle.team/), [Drizzle Latest Releases](https://orm.drizzle.team/docs/latest-releases), [npm: drizzle-orm](https://www.npmjs.com/package/drizzle-orm)

### SQL-Like Syntax in Practice

Drizzle's query builder maps 1:1 to SQL. Example:

```typescript
// Drizzle -- reads like SQL
const users = await db
  .select({ id: usersTable.id, name: usersTable.name })
  .from(usersTable)
  .where(eq(usersTable.city, 'Tel Aviv'))
  .limit(10);

// vs Prisma -- abstracted API
const users = await prisma.user.findMany({
  select: { id: true, name: true },
  where: { city: 'Tel Aviv' },
  take: 10,
});
```

The Drizzle approach means less abstraction to learn, but requires SQL knowledge. The Prisma approach is more beginner-friendly but hides what SQL is actually executed.

### Migration System (drizzle-kit)

Two workflows:

1. **`drizzle-kit generate`** -- Reads your TypeScript schema, diffs against the last snapshot, generates `.sql` migration files. You then apply them with `drizzle-kit migrate` or `drizzle-orm`'s `migrate()` function. This creates a version history.

2. **`drizzle-kit push`** -- Pushes schema changes directly to the database with no migration files. Ideal for rapid prototyping. The team says "dozens of teams and solo developers successfully use it as a primary migrations flow in production."

- **No shadow database required.** Drizzle diffs against JSON snapshots stored locally, not against a temporary DB.
- Migration history tracked via JSON snapshot files and a journal.

**Source:** [drizzle-kit generate](https://orm.drizzle.team/docs/drizzle-kit-generate), [drizzle-kit push](https://orm.drizzle.team/docs/drizzle-kit-push), [drizzle-kit migrate](https://orm.drizzle.team/docs/drizzle-kit-migrate)

### NestJS Integration

- **No official NestJS module from the Drizzle team.** Integration is done via community packages or manual setup.
- Community packages: `nestjs-drizzle` (by knaadh) provides a NestJS module for Drizzle with Postgres, MySQL, SQLite drivers.
- Trilon (the NestJS consulting firm) published a guide: ["NestJS & DrizzleORM: A Great Match"](https://trilon.io/blog/nestjs-drizzleorm-a-great-match).
- Manual integration is straightforward: create a `DrizzleModule` that provides the `db` instance via NestJS dependency injection. More boilerplate than Prisma's integration, but not complex.

**Source:** [nestjs-drizzle GitHub](https://github.com/knaadh/nestjs-drizzle), [Trilon Guide](https://trilon.io/blog/nestjs-drizzleorm-a-great-match), [Wanago.io NestJS + Drizzle](https://wanago.io/2024/05/20/api-nestjs-drizzle-orm-postgresql/)

### Supabase Compatibility

- First-class Supabase support. Official tutorial on Drizzle docs and Supabase docs.
- Uses `postgres` (postgres.js) driver. Configuration: `const client = postgres(process.env.DATABASE_URL, { prepare: false })`.
- **`prepare: false` is mandatory** when using Supabase Supavisor in transaction mode (pooled connections). Prepared statements are not supported.
- RLS (Row Level Security) supported: admin client bypasses RLS; user client respects it.

**Source:** [Drizzle + Supabase Tutorial](https://orm.drizzle.team/docs/tutorials/drizzle-with-supabase), [Supabase Drizzle Docs](https://supabase.com/docs/guides/database/drizzle)

### Drizzle Studio

- Web-based GUI launched via `drizzle-kit studio`. Runs locally at `local.drizzle.studio`.
- Browse tables, execute queries, edit data, view relationships.
- Supports PostgreSQL, MySQL, SQLite.
- Also available as a Chrome extension for PlanetScale, Cloudflare D1, Vercel Postgres consoles.
- **Drizzle Studio Gateway:** Deployable Docker version for private infrastructure access.
- Less feature-rich than the new Prisma Studio, but functional for basic data browsing and editing.

**Source:** [Drizzle Studio Docs](https://orm.drizzle.team/docs/drizzle-kit-studio), [Drizzle Studio Guide](https://www.achromatic.dev/blog/drizzle-studio-complete-guide)

### PostGIS / Geolocation Support

- **Significantly better than Prisma.** Drizzle has built-in `geometry` and `point` column types for PostGIS.
- Two mapping modes: `tuple` ([x, y]) and `xy` ({ x, y }).
- Supports `ST_Distance()`, the `<->` operator, and GIST spatial indexes natively through the query builder.
- A community package `drizzle-postgis` extends support further.
- **Limitation:** Polygon types are not supported out of the box -- requires a custom column type.
- **Limitation:** No built-in command to enable the PostGIS extension -- you must enable it manually in the database.

**Source:** [Drizzle PostGIS Guide](https://orm.drizzle.team/docs/guides/postgis-geometry-point), [Drizzle PostgreSQL Extensions](https://orm.drizzle.team/docs/extensions/pg), [drizzle-postgis GitHub](https://github.com/Schmavery/drizzle-postgis)

### Known Issues / Limitations (March 2026)

1. **Still pre-v1.0:** The 0.45.x API could have breaking changes before v1 stable. Beta v1.0.0-beta.16 is available but not production-recommended by the team.
2. **Type safety gaps:** Only query *results* are typed. You CAN write invalid queries that TypeScript won't catch (e.g., selecting a column from a table not in the FROM clause). This is a fundamental API design limitation.
3. **Generated columns not supported yet.**
4. **Cloudflare D1 cascade data loss bug:** `PRAGMA foreign_keys=OFF` is ignored by D1, causing CASCADE DELETE during table recreation. (Not relevant for PostgreSQL/Supabase.)
5. **D1 parameter limit:** 100 bound parameters per query; Drizzle doesn't auto-chunk bulk inserts. (Not relevant for PostgreSQL.)
6. **Smaller ecosystem:** Fewer community plugins, generators, and Stack Overflow answers compared to Prisma.

**Source:** [Drizzle GitHub Issues](https://github.com/drizzle-team/drizzle-orm/issues), [Drizzle v1 Roadmap](https://orm.drizzle.team/roadmap), [Prisma vs Drizzle Type Safety](https://www.prisma.io/docs/orm/more/comparisons/prisma-and-drizzle)

---

## 3. Head-to-Head Comparison

### Developer Experience (DX)

| Aspect | Prisma 7 | Drizzle 0.45 |
|--------|----------|---------------|
| **Schema definition** | Separate `.prisma` file (DSL) | TypeScript files (code-first) |
| **Code generation** | Required (`prisma generate` after every schema change) | Not needed (types inferred at save) |
| **IDE autocompletion** | Excellent (generated types) | Good (inferred types, but can be slower for large schemas) |
| **Raw SQL escape hatch** | `$queryRaw`, `$executeRaw`, TypedSQL (`.sql` files with typed I/O) | `sql` template tag, or drop to raw driver |
| **Debugging SQL** | Need to enable logging to see generated SQL | SQL is visible in the query builder code |
| **Studio GUI** | New rebuilt Studio with relationship visualization | Web-based Studio + Chrome extension |
| **Migration DX** | `prisma migrate dev` (needs shadow DB) + `prisma db push` for prototyping | `drizzle-kit generate` (no shadow DB) + `drizzle-kit push` for prototyping |

**Winner: Depends on preference.** Prisma is more polished and batteries-included. Drizzle is lighter with no generation step. For a solo dev who knows SQL, the no-generation workflow is a meaningful time saver.

### Type Safety

| Aspect | Prisma 7 | Drizzle 0.45 |
|--------|----------|---------------|
| **Query inputs** | Fully typed -- invalid field names / filters caught at compile time | Partially typed -- you CAN write invalid queries that compile |
| **Query results** | Fully typed | Fully typed |
| **Type-check speed** | 70% faster than Prisma 6; few hundred type instantiations per schema | 5,000+ type instantiations per schema; can degrade as schema grows |
| **Approach** | Generated types (front-loaded work) | Inferred types (re-derived each build) |

**Winner: Prisma.** Comprehensively type-safe for both query construction and results. Drizzle's query-input type gaps are a real concern.

**Source:** [Why Prisma Checks Types Faster Than Drizzle](https://www.prisma.io/blog/why-prisma-orm-checks-types-faster-than-drizzle), [Prisma vs Drizzle Type Safety](https://www.prisma.io/docs/orm/more/comparisons/prisma-and-drizzle)

### Query Performance (Runtime)

| Metric | Prisma 7 | Drizzle 0.45 |
|--------|----------|---------------|
| **ORM overhead** | WASM query compiler on JS main thread. 3.4x faster than Prisma 5/6, but still has compilation overhead | Zero engine layer. Generates SQL strings directly. Minimal overhead. |
| **Simple queries** | ~comparable after v7 improvements | Slightly faster |
| **Complex queries** | WASM compilation can block event loop under high concurrency (reported in v7.3) | Consistent performance, no compilation step |
| **Real-world impact** | For most apps, the DB round-trip (5-50ms) dwarfs ORM overhead | Same -- ORM layer is rarely the bottleneck |

**Winner: Drizzle** for raw ORM overhead. **Negligible difference** for most real-world apps where database round-trip dominates. The Prisma v7.3 regression under high concurrency is a concern for production, but has been partially addressed with the `compilerBuild` option.

**Source:** [Drizzle Benchmarks](https://orm.drizzle.team/benchmarks), [Prisma Performance Benchmarks](https://www.prisma.io/blog/prisma-orm-without-rust-latest-performance-benchmarks), [GitHub Issue #29099](https://github.com/prisma/prisma/issues/29099)

### Bundle Size

| Metric | Prisma 7 | Drizzle 0.45 |
|--------|----------|---------------|
| **Runtime size** | ~1.6MB (600KB gzipped) | ~7.4KB (minified + gzipped) |
| **Ratio** | ~216x larger than Drizzle | ~216x smaller than Prisma |
| **Dependencies** | Driver adapter + WASM compiler | Zero dependencies |

**Winner: Drizzle** by a massive margin. For a NestJS server running on AWS (not serverless/edge), this matters less than for Lambda/edge deployments. But smaller bundles mean faster installs and less disk usage.

**Source:** [MakerKit Drizzle vs Prisma 2026](https://makerkit.dev/blog/tutorials/drizzle-vs-prisma), [DEV.to Honest Comparison](https://dev.to/pockit_tools/drizzle-orm-vs-prisma-in-2026-the-honest-comparison-nobody-is-making-3n6g)

### Learning Curve

| Persona | Prisma 7 | Drizzle 0.45 |
|---------|----------|---------------|
| **New to databases** | Gentler. Schema DSL is beginner-friendly. Studio helps visualize. | Steeper. Assumes SQL knowledge. |
| **Knows SQL** | Can feel over-abstracted. Need to learn Prisma's query API. | Natural. "If you know SQL, you know Drizzle." |
| **Knows Prisma already** | Smooth upgrade (v7 migration guide exists). | Need to learn new paradigm. |

**Winner: Prisma** for beginners. **Drizzle** for SQL-proficient developers.

### Community Size & Ecosystem

| Metric | Prisma | Drizzle |
|--------|--------|---------|
| **GitHub stars** | ~44,000-45,000 | ~32,900 |
| **npm weekly downloads** | ~5.5M-7.8M | ~5.0M |
| **First release** | 2021 (stable) | 2023 (0.x) |
| **v1.0 status** | v7.4.2 stable | v1.0.0-beta.16 (no stable v1) |
| **Meta-framework adoption** | RedwoodJS, Wasp, KeystoneJS, t3, Remix, Amplication | Growing, popular with AI coding tools and modern TS stacks |
| **Community plugins** | Large: prisma-erd-generator, prisma-zod-generator, bridg, jest-prisma, prisma-pothos-types | Smaller: drizzle-postgis, drizzle-zod, drizzle-valibot, nestjs-drizzle |
| **Stack Overflow coverage** | Extensive | Growing but smaller |

**Winner: Prisma** for ecosystem maturity and breadth. Drizzle is catching up rapidly (npm downloads are nearly equal), but the plugin ecosystem and documentation breadth are not there yet.

**Source:** [GitHub: prisma/prisma](https://github.com/prisma/prisma), [GitHub: drizzle-team/drizzle-orm](https://github.com/drizzle-team/drizzle-orm), [npm trends](https://npmtrends.com/drizzle-orm-vs-prisma)

### Documentation Quality

| Aspect | Prisma | Drizzle |
|--------|--------|---------|
| **Official docs** | Comprehensive, well-organized, extensive guides and tutorials | Good but thinner; some areas lack depth |
| **Migration guides** | Detailed v6->v7 upgrade guide | v1 beta upgrade guide exists but evolving |
| **API reference** | Complete | Complete but less polished |
| **Blog/tutorials** | Frequent blog posts, official video content | Fewer official resources; more community-driven |

**Winner: Prisma.** More thorough documentation with better organization and more tutorials.

### Migration Tooling

| Aspect | Prisma 7 | Drizzle |
|--------|----------|---------|
| **Migration file format** | SQL files (customizable) | SQL files |
| **Diff mechanism** | Shadow database (requires CREATE DB permissions) | JSON snapshot comparison (no shadow DB) |
| **Prototyping mode** | `prisma db push` | `drizzle-kit push` |
| **Migration history** | `_prisma_migrations` table in DB | JSON journal + snapshot files |
| **Custom SQL in migrations** | Yes (edit generated SQL files) | Yes (edit generated SQL files) |
| **Rollback** | Manual (no auto-rollback) | Manual (no auto-rollback) |

**Winner: Drizzle.** No shadow database requirement is a meaningful advantage, especially with managed Supabase databases where CREATE DB permissions may be restricted.

### Connection Pooling

| Aspect | Prisma 7 | Drizzle |
|--------|----------|---------|
| **Supabase Supavisor** | Supported via `?pgbouncer=true` in connection string | Supported via `{ prepare: false }` in driver config |
| **Prepared statements** | Disabled by pgbouncer flag | Disabled by prepare flag |
| **Configuration** | `prisma.config.ts` | Inline in driver instantiation |

**Winner: Tie.** Both work with Supabase's connection pooler. Both require disabling prepared statements for transaction mode.

### PostGIS Support (Critical for Emuni)

| Capability | Prisma 7 | Drizzle |
|------------|----------|---------|
| **Native geometry types** | No (use `@db.Geometry` annotation, but can't query through client API) | Yes (`geometry('point')` with `tuple` or `xy` modes) |
| **ST_Distance queries** | Raw SQL only (`$queryRaw`) | Supported in query builder + raw SQL |
| **Spatial indexes (GIST)** | Raw SQL only | Supported in schema definition |
| **Nearest-neighbor queries** | Raw SQL only | `<->` operator and `ST_Distance()` via builder |
| **PostGIS extension enable** | Manual SQL | Manual SQL |
| **Polygon support** | Raw SQL only | Custom column type required |

**Winner: Drizzle** by a significant margin. For a nanny marketplace that needs "find nannies within X km of my location," Drizzle provides native query builder support for the core spatial operations. Prisma forces you into raw SQL for every spatial query, which negates much of its type-safety advantage.

**Source:** [Drizzle PostGIS Guide](https://orm.drizzle.team/docs/guides/postgis-geometry-point), [Prisma PostGIS Issue #1798](https://github.com/prisma/prisma/issues/1798)

### Maintenance Burden for Solo Dev

| Factor | Prisma 7 | Drizzle |
|--------|----------|---------|
| **Schema changes** | Edit `.prisma` file -> run `prisma generate` -> run `prisma migrate dev` (3 steps) | Edit TypeScript schema file -> run `drizzle-kit push` or `generate` (2 steps) |
| **Dependency weight** | Heavier (WASM compiler, adapter packages) | Lighter (single package, zero deps) |
| **Upgrade friction** | v6->v7 upgrade was painful (new config file, driver adapters, ESM changes). Future major versions may be similar. | Pre-v1, so breaking changes are expected. Post-v1 should stabilize. |
| **Debugging** | Need logging to see SQL; WASM internals harder to debug | SQL is visible in code; simpler internals |
| **NestJS integration** | Well-documented, dedicated package | Manual or community package; more boilerplate |

**Winner: Mixed.** Prisma has better NestJS integration ergonomics. Drizzle has fewer moving parts and a simpler mental model. For a solo dev, fewer moving parts = fewer things to break.

---

## 4. Recommendation for Emuni

### Context Recap

- Solo bootstrapper, no team
- NestJS 11 + Fastify v5 backend
- PostgreSQL 16 via Supabase (Frankfurt region)
- TypeScript strict mode
- PostGIS needed for geolocation (find nannies near me)
- Traditional server deployment (AWS), not serverless/edge
- MVP speed is critical

### Decision Matrix

| Factor | Weight (for Emuni) | Prisma 7 | Drizzle | Winner |
|--------|-------------------|----------|---------|--------|
| **PostGIS support** | CRITICAL | Raw SQL only | Native builder support | **Drizzle** |
| **NestJS integration** | HIGH | Official package, well-documented | Community package, more boilerplate | **Prisma** |
| **Solo dev maintenance** | HIGH | More moving parts (generate step, config file, shadow DB) | Simpler (no generation, no shadow DB) | **Drizzle** |
| **Type safety** | HIGH | Full (queries + results) | Partial (results only) | **Prisma** |
| **Query performance** | MEDIUM | Good (v7 improvements), some concurrency concerns | Excellent (zero overhead) | **Drizzle** |
| **Bundle size** | LOW (not serverless) | 1.6MB | 7.4KB | **Drizzle** |
| **Ecosystem maturity** | MEDIUM | Larger, more plugins, better docs | Smaller, growing fast, still pre-v1 | **Prisma** |
| **Type-check speed** | MEDIUM | 70% faster, scales better | Slower, degrades with schema size | **Prisma** |
| **Supabase compat** | HIGH | Works (driver adapter required) | Works (simpler setup) | **Drizzle** |
| **Learning curve** | MEDIUM | Higher if you know SQL (over-abstracted) | Lower if you know SQL | **Drizzle** |

### Score: Drizzle 6, Prisma 4

### Recommendation: Drizzle ORM

**For Emuni specifically, Drizzle is the better choice.** Here's why:

1. **PostGIS is the decisive factor.** Emuni's core feature -- matching nannies to parents by proximity -- requires geolocation queries. Drizzle supports `ST_Distance()`, spatial indexes, and point types natively in the query builder. Prisma forces every spatial query into raw SQL, which eliminates its main advantage (type safety) for your most critical queries. If 30-50% of your queries need spatial operations, Prisma's type safety premium vanishes.

2. **Solo dev simplicity.** No code generation step. No shadow database. No `prisma.config.ts` + `schema.prisma` + `generated/` directory dance. Edit your TypeScript schema, run `drizzle-kit push`, done.

3. **Supabase integration is simpler.** No driver adapter boilerplate. Just `postgres(url, { prepare: false })` and you're connected.

4. **Pre-v1 risk is manageable.** Drizzle 0.45.x is used in production by many teams. The API surface is stable. The v1 beta is at beta.16, suggesting the finish line is close. For an MVP launching in mid-2026, Drizzle v1 stable should be available by then or shortly after.

### Mitigations for Drizzle's Weaknesses

- **Type safety gaps:** Mitigate with thorough integration tests. For a solo dev, the risk of writing an invalid query that compiles is real but detectable at runtime during development.
- **NestJS integration boilerplate:** Use the `nestjs-drizzle` community package or follow the Trilon guide. It's ~20 lines of module setup code, not a significant burden.
- **Smaller ecosystem:** For Emuni's needs (CRUD + spatial queries + Supabase), Drizzle's core capabilities are sufficient. You don't need the breadth of Prisma's plugin ecosystem for an MVP.
- **Documentation gaps:** Supplement with Drizzle's Discord community and the growing body of blog tutorials.

### If You Picked Prisma Instead

Prisma would work fine for Emuni. The main cost would be writing all spatial queries in raw SQL (which means you lose type safety for your most important queries), plus the extra overhead of the generation step and shadow database. If PostGIS support weren't needed, Prisma's superior type safety and NestJS integration would make it the clear winner.

---

## Sources

### Prisma 7
- [Prisma 7 Release Announcement](https://www.prisma.io/blog/announcing-prisma-orm-7-0-0)
- [Prisma Architecture Shift: Rust to TypeScript](https://www.prisma.io/blog/from-rust-to-typescript-a-new-chapter-for-prisma-orm)
- [InfoQ: Prisma 7 Performance Gains](https://www.infoq.com/news/2026/01/prisma-7-performance/)
- [Prisma Performance Benchmarks (Rust-Free)](https://www.prisma.io/blog/prisma-orm-without-rust-latest-performance-benchmarks)
- [Why Prisma Checks Types Faster Than Drizzle](https://www.prisma.io/blog/why-prisma-orm-checks-types-faster-than-drizzle)
- [Prisma 7 Upgrade Guide](https://www.prisma.io/docs/orm/more/upgrade-guides/upgrading-versions/upgrading-to-prisma-7)
- [Prisma ORM 7.2.0 Release](https://www.prisma.io/blog/announcing-prisma-orm-7-2-0)
- [Prisma NestJS Guide](https://www.prisma.io/docs/guides/nestjs)
- [Prisma + Supabase Docs](https://supabase.com/docs/guides/database/prisma)
- [Prisma Edge Deployment](https://www.prisma.io/docs/orm/prisma-client/deployment/edge/overview)
- [Prisma Shadow Database](https://www.prisma.io/docs/orm/prisma-migrate/understanding-prisma-migrate/shadow-database)
- [Prisma PostGIS Issue #1798](https://github.com/prisma/prisma/issues/1798)
- [Prisma PostGIS Issue #25768](https://github.com/prisma/prisma/issues/25768)
- [Prisma v7.3 Performance Issue #29099](https://github.com/prisma/prisma/issues/29099)
- [Prisma Cloudflare Workers Issue #28657](https://github.com/prisma/prisma/issues/28657)
- [nestjs-prisma npm](https://www.npmjs.com/package/nestjs-prisma)
- [NestJS + Prisma 2026 Setup Guide](https://dev.to/manendrav/how-to-set-up-nestjs-with-prisma-and-postgresql-2026-complete-guide-2da7)
- [Prisma Supavisor Configuration](https://supabase.github.io/supavisor/orms/prisma/)

### Drizzle ORM
- [Drizzle ORM Homepage](https://orm.drizzle.team/)
- [Drizzle Latest Releases](https://orm.drizzle.team/docs/latest-releases)
- [Drizzle v1 Roadmap](https://orm.drizzle.team/roadmap)
- [Drizzle v1 Beta.2 Release Notes](https://orm.drizzle.team/docs/latest-releases/drizzle-orm-v1beta2)
- [Drizzle + Supabase Tutorial](https://orm.drizzle.team/docs/tutorials/drizzle-with-supabase)
- [Drizzle PostGIS Geometry Point](https://orm.drizzle.team/docs/guides/postgis-geometry-point)
- [Drizzle PostgreSQL Extensions](https://orm.drizzle.team/docs/extensions/pg)
- [drizzle-kit generate](https://orm.drizzle.team/docs/drizzle-kit-generate)
- [drizzle-kit push](https://orm.drizzle.team/docs/drizzle-kit-push)
- [Drizzle Studio Docs](https://orm.drizzle.team/docs/drizzle-kit-studio)
- [Drizzle Benchmarks](https://orm.drizzle.team/benchmarks)
- [Drizzle + Supabase (Supabase Docs)](https://supabase.com/docs/guides/database/drizzle)
- [drizzle-postgis GitHub](https://github.com/Schmavery/drizzle-postgis)
- [nestjs-drizzle GitHub](https://github.com/knaadh/nestjs-drizzle)
- [Trilon: NestJS & DrizzleORM](https://trilon.io/blog/nestjs-drizzleorm-a-great-match)
- [Wanago.io: NestJS + Drizzle](https://wanago.io/2024/05/20/api-nestjs-drizzle-orm-postgresql/)

### Comparison Articles
- [MakerKit: Drizzle vs Prisma 2026](https://makerkit.dev/blog/tutorials/drizzle-vs-prisma)
- [Bytebase: Drizzle vs Prisma 2026](https://www.bytebase.com/blog/drizzle-vs-prisma/)
- [DEV.to: The Honest Comparison Nobody Is Making](https://dev.to/pockit_tools/drizzle-orm-vs-prisma-in-2026-the-honest-comparison-nobody-is-making-3n6g)
- [Better Stack: Drizzle vs Prisma](https://betterstack.com/community/guides/scaling-nodejs/drizzle-vs-prisma/)
- [Design Revision: Prisma vs Drizzle](https://designrevision.com/blog/prisma-vs-drizzle)
- [Prisma Official: Prisma vs Drizzle](https://www.prisma.io/docs/orm/more/comparisons/prisma-and-drizzle)
- [Prisma Blog: The ORM Convergence](https://www.prisma.io/blog/convergence)
