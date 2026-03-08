# Backend Stack Research: NestJS & Node.js Ecosystem (March 2026)

Research conducted: March 7, 2026
Context: Emuni Israeli nanny marketplace — REST API, PostgreSQL, real-time messaging

---

## Table of Contents

1. [NestJS Current Version](#1-nestjs-current-version)
2. [NestJS vs Alternatives](#2-nestjs-vs-alternatives-in-2026)
3. [Node.js Current LTS](#3-nodejs-current-lts-version)
4. [Bun vs Node.js](#4-bun-vs-nodejs-in-2026)
5. [Deno in 2026](#5-deno-in-2026)
6. [API Paradigm](#6-api-paradigm-rest-vs-trpc-vs-graphql)
7. [ORM/Query Builder](#7-ormquery-builder-comparison)
8. [Fastify Adapter](#8-fastify-adapter-for-nestjs)
9. [Breaking Changes & Deprecations](#9-breaking-changes--deprecations)
10. [Recommendation for Emuni](#10-recommendation-for-emuni)

---

## 1. NestJS Current Version

| Detail | Value |
|--------|-------|
| **Latest stable** | v11.1.16 |
| **Major release** | NestJS 11, released January 2025 |
| **Next major** | v12.0.0, planned ~Q3 2026 |
| **npm packages** | `@nestjs/core@11.1.16`, `@nestjs/common@11.1.11` |
| **CLI** | `@nestjs/cli` (latest 11.x) |

### What Changed Since v10

NestJS 11 is a significant upgrade from v10:

- **Express v5 is now the default HTTP adapter** (was Express v4)
- **Fastify v5 support** added
- **Built-in JSON logging** — `json: true` option for structured logging (container-friendly)
- **New ParseDatePipe** in `@nestjs/common`
- **IntrinsicException** — exceptions that skip auto-logging
- **CQRS enhancements** — request-scoped providers, strongly-typed commands/events/queries
- **Improved module resolution** — opaque key generation uses object references instead of hashing, faster startup for large apps
- **Microservice DI container** — microservice options can now come from DI

### NestJS 12 Roadmap (Q3 2026)

Announced features for v12:
- **Native ESM support** (the most requested feature)
- **Vitest + SWC** as default test runner for ESM projects
- **Standard Schema in route decorators** — use Zod, Valibot, ArkType directly (no more class-validator requirement)
- **Complete website redesign**
- **Native WebAssembly support** for compute-intensive tasks

**Implication for Emuni:** Starting on NestJS 11 now is safe. v12's ESM + Zod integration will be a natural upgrade path in ~6 months. No risk of being stranded.

Sources:
- [Announcing NestJS 11 - Trilon](https://trilon.io/blog/announcing-nestjs-11-whats-new)
- [NestJS v12 PR #16391](https://github.com/nestjs/nest/pull/16391)
- [NestJS v12 announcement on X](https://x.com/nestframework/status/2025894197044158491)
- [@nestjs/core npm](https://www.npmjs.com/package/@nestjs/core?activeTab=versions)

---

## 2. NestJS vs Alternatives in 2026

### Framework Comparison Matrix

| Framework | Best For | Performance | TypeScript | Maturity | Ecosystem |
|-----------|----------|-------------|------------|----------|-----------|
| **NestJS** | Enterprise apps, structured teams | Good (Express/Fastify adapter) | Excellent (native) | Very High | Largest |
| **Fastify** (standalone) | High-throughput APIs | Very Good | Good (native support) | High | Large |
| **Hono** | Edge/serverless, lightweight APIs | Excellent | Excellent | Medium | Growing |
| **ElysiaJS** | Bun-native apps | Excellent (Bun-only) | Excellent (Eden type safety) | Low | Small |
| **tRPC** | TS monorepos (web + backend) | Good | Best (end-to-end) | Medium | Medium |
| **Encore.ts** | Distributed systems, auto-infra | Best (Rust runtime) | Excellent | Low-Medium | Small |

### Detailed Assessment

**NestJS** remains the dominant choice for structured TypeScript backends. Its opinionated architecture (modules, providers, controllers, guards, interceptors) provides guardrails that matter for long-term maintainability. The ecosystem is unmatched — official packages for WebSockets, GraphQL, microservices, Swagger, health checks, CQRS, scheduling, etc. The learning curve is steeper than lightweight frameworks.

**Hono** (v4.12.0) is the rising star. At under 12kB with zero dependencies, it works on every runtime (Node, Bun, Deno, Cloudflare Workers, AWS Lambda). Its Zod validator middleware and RPC client provide end-to-end type safety. Ideal for edge/serverless but lacks NestJS's enterprise structure (no DI container, no module system, no guards/interceptors pattern). For a simple API it excels; for a complex app with auth, roles, real-time, scheduled jobs — you'd rebuild NestJS's patterns manually.

**ElysiaJS** is Bun-exclusive. Its "Eden" feature provides tRPC-like end-to-end type safety. Impressive performance but adopting two cutting-edge technologies (Bun + Elysia) simultaneously is risky for a production app. Small ecosystem. Not recommended for Emuni.

**Fastify** (standalone) handles 30-40% more requests/sec than Express. Built-in JSON Schema validation, structured logging, plugin architecture. Good choice if you don't need NestJS's structure. But you lose DI, decorators, guards, interceptors, and the entire NestJS ecosystem.

**tRPC** provides the best TypeScript type safety — your frontend gets auto-completed API types with zero code generation. Works with React Native (since it's just TypeScript/React). However, it's designed for TypeScript-to-TypeScript communication. If you ever need a public API or non-TS clients, you'd need a separate REST layer.

**Encore.ts** (11K+ GitHub stars) claims 9x faster than Express with a Rust-based runtime. Unique value: you declare infrastructure (DB, Pub/Sub, cron) in TypeScript and it auto-provisions. Used by Groupon in production. However, it's a vendor-coupled platform — you're locked into Encore's deployment model. Too risky for a bootstrapped startup.

### Verdict for Emuni

**NestJS remains the right choice.** Rationale:
1. Solo developer needs structure/guardrails, not micro-optimization
2. Largest ecosystem = fewer things to build from scratch
3. Official WebSocket gateway for real-time messaging
4. Official Swagger integration for API documentation
5. Official scheduling module for cron jobs (booking reminders, etc.)
6. Strong NestJS + Supabase/PostgreSQL integration patterns
7. v12 coming Q3 2026 with Zod/Standard Schema — modernizes the stack

Sources:
- [Best TypeScript Backend Frameworks 2026 - Encore](https://encore.dev/articles/best-typescript-backend-frameworks)
- [Hono vs Encore.ts 2026](https://encore.dev/articles/hono-vs-encore)
- [NestJS vs Encore.ts 2026](https://encore.dev/articles/nestjs-vs-encore)
- [Hono docs](https://hono.dev/docs/)

---

## 3. Node.js Current LTS Version

| Detail | Value |
|--------|-------|
| **Current LTS** | Node.js 24 "Krypton" |
| **Latest LTS release** | v24.14.0 (March 2026) |
| **Active LTS since** | May 6, 2025 |
| **Maintenance LTS** | October 28, 2025 |
| **End of Life** | April 30, 2028 |
| **V8 engine** | v13.6 |
| **Previous LTS** | Node.js 22 "Jod" (still supported, EOL April 2027) |
| **Current line** | Node.js 25 (odd = non-LTS, for experimentation) |

### Key Node.js 24 Features

- **Built-in fetch** (stable, no more node-fetch dependency)
- **Stable test runner** (`node:test` module)
- **Permission model** for security sandboxing
- **OpenSSL 3.5** — enforces 2048-bit minimum RSA keys
- **Undici v7** for faster HTTP
- **Float16Array**, **Error.isError**, **Global URLPattern API**
- **Faster startup** and optimized V8 execution

### Recommendation

**Use Node.js 24 LTS for Emuni.** It's the current active LTS, will be supported until April 2028, and all NestJS 11 features are compatible. Node.js 22 is still supported but enters maintenance mode and has an earlier EOL.

Sources:
- [Node.js Releases](https://nodejs.org/en/about/previous-releases)
- [Node.js 24 LTS - NodeSource](https://nodesource.com/blog/nodejs-24-becomes-lts)
- [Node.js v22 to v24 Migration](https://nodejs.org/en/blog/migrations/v22-to-v24)
- [Node.js EOL dates](https://endoflife.date/nodejs)

---

## 4. Bun vs Node.js in 2026

| Detail | Bun | Node.js |
|--------|-----|---------|
| **Latest version** | v1.3.10 (Feb 27, 2026) | v24.14.0 LTS |
| **Owner** | Anthropic (acquired Dec 2025) | OpenJS Foundation |
| **Monthly downloads** | 7.2M+ (Oct 2025) | Dominant (billions) |
| **Performance** | 2-3.5x more RPS than Node | Baseline |
| **Startup time** | Much faster | Standard |
| **npm compatibility** | Very high (improved in 1.3) | Native |
| **Production adoption** | Growing but limited | Universal |
| **NestJS support** | Unofficial, community adapters | Official, first-class |

### Anthropic Acquisition (December 2025)

Anthropic acquired Bun — their first-ever acquisition. Claude Code ships as a Bun executable. Bun powers Claude Code, which hit $1B ARR. This gives Bun significant financial backing and reduces abandonment risk. Bun remains open-source and MIT-licensed.

### Production Readiness Assessment

Bun is production-viable for many workloads in 2026:
- 157ms mean response time, 0% failure rate in benchmarks
- 30,000-50,000 RPS vs Node's 13,000-20,000
- Built-in SQLite, bundler, test runner, package manager

**However, for NestJS specifically:**
- NestJS does not officially support Bun as a runtime
- Edge incompatibilities can still arise with npm packages
- Debugging/profiling tooling is less mature
- AWS Lambda, Docker, CI/CD workflows are all optimized for Node.js

### Verdict for Emuni

**Use Node.js 24 LTS, not Bun.** Rationale:
1. NestJS officially supports Node.js, not Bun
2. Supabase client libraries are tested against Node.js
3. AWS il-central-1 Lambda/ECS runs Node.js natively
4. Solo developer cannot afford to debug runtime incompatibilities
5. Bun's advantages (startup speed, bundler) don't matter for a long-running server process
6. Revisit Bun when NestJS 12+ adds official support (if ever)

Sources:
- [Bun joins Anthropic](https://bun.com/blog/bun-joins-anthropic)
- [Anthropic acquires Bun](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone)
- [Is Bun Production-Ready in 2026?](https://dev.to/last9/is-bun-production-ready-in-2026-a-practical-assessment-181h)
- [Node vs Bun vs Deno 2026 Guide](https://javascript.plainenglish.io/node-vs-bun-vs-deno-what-actually-runs-in-production-2026-guide-a3552c18ce91)

---

## 5. Deno in 2026

| Detail | Value |
|--------|-------|
| **Latest version** | v2.7.4 (March 5, 2026) |
| **Recent major** | Deno 2.7 (Feb 25, 2026) |
| **LTS status** | LTS being discontinued after April 30, 2026 |
| **Deploy** | Deno Deploy GA (serverless) |
| **Sandbox** | Deno Sandbox for AI-generated code |

### Deno 2.7 Features

- Temporal API stabilized
- Windows ARM builds
- npm overrides in package.json
- Brotli compression streams
- Self-extracting compiled binaries
- `deno create` command
- Dozens of Node.js compatibility improvements

### Assessment

Deno has matured significantly with Deno 2.x. Its security-by-default permission model is appealing. However:

- **LTS support ends April 30, 2026** — no more LTS releases after that
- NestJS does not officially support Deno
- Ecosystem is much smaller than Node.js
- npm compatibility improved but not 100%
- Deno Deploy is serverless-only — doesn't fit Emuni's architecture

### Verdict for Emuni

**Do not use Deno.** The LTS discontinuation is a red flag for production use. Node.js remains the safe choice. Deno's niche is edge/serverless, which doesn't align with Emuni's architecture (NestJS + PostgreSQL + WebSockets).

Sources:
- [Deno 2.7 blog post](https://deno.com/blog/v2.7)
- [Deno EOL dates](https://endoflife.date/deno)
- [Deno releases](https://github.com/denoland/deno/releases)

---

## 6. API Paradigm: REST vs tRPC vs GraphQL

### Comparison for Mobile App Backend

| Paradigm | Mobile App Fit | Type Safety | Caching | Learning Curve | NestJS Support |
|----------|---------------|-------------|---------|----------------|----------------|
| **REST** | Excellent | Manual (OpenAPI) | Native HTTP caching | Low | First-class |
| **tRPC** | Good (React Native) | Best (auto) | React Query | Medium | Community adapter |
| **GraphQL** | Good | Good (codegen) | Apollo cache | High | Official module |

### REST for Mobile Apps

REST remains the most practical choice for mobile backends:
- Works with ANY client (iOS, Android, web, third-party)
- HTTP caching (CDN, ETags) works out of the box
- Swagger/OpenAPI auto-generates client SDKs
- Every developer understands REST
- NestJS has first-class REST support

### tRPC for React Native

tRPC works with React Native and provides the best TypeScript type safety — your React Native frontend gets auto-completed API types with zero code generation. However:
- Only works with TypeScript clients (no Swift/Kotlin native apps)
- If you ever build a native iOS/Android app (not React Native), you lose tRPC's benefits
- NestJS integration exists but is community-maintained, not official
- Designed for monorepos — your mobile app needs to share types with the backend

### GraphQL for Mobile Apps

GraphQL's query flexibility helps mobile apps fetch exactly what they need (reducing bandwidth). However:
- Over-engineering for a startup MVP
- N+1 query problem requires careful DataLoader implementation
- Apollo client adds complexity to the mobile app
- Higher learning curve for a solo developer

### 2026 Industry Trend

The best teams use multiple protocols for different layers. Your public API can be REST while internal services use tRPC or gRPC. However, for a solo bootstrapper building an MVP, start with one protocol.

### Verdict for Emuni

**Use REST.** Rationale:
1. Solo developer — simplest to build, debug, and document
2. React Native + REST is the most well-trodden path
3. NestJS + Swagger auto-generates OpenAPI docs
4. If you later hire native iOS/Android devs, REST just works
5. Real-time features use WebSockets (NestJS Gateway), not the API paradigm
6. tRPC could be added later for admin dashboard or internal tooling

Sources:
- [REST vs GraphQL vs tRPC 2026 Guide](https://dev.to/pockit_tools/rest-vs-graphql-vs-trpc-vs-grpc-in-2026-the-definitive-guide-to-choosing-your-api-layer-1j8m)
- [REST vs GraphQL vs tRPC - same backend comparison](https://navanathjadhav.medium.com/rest-vs-graphql-vs-trpc-i-built-three-versions-of-the-same-backend-946ddb0fc950)
- [API Design 2026: Multi-Protocol Approach](https://dev.to/dataformathub/api-design-2026-why-the-multi-protocol-approach-is-the-ultimate-guide-2h6o)

---

## 7. ORM/Query Builder Comparison

### Current State (March 2026)

| ORM | Version | Architecture | Performance | NestJS Integration | Bundle Size |
|-----|---------|-------------|-------------|-------------------|-------------|
| **Prisma** | v7.x (late 2025) | Schema-first, pure TS engine | Good (3x faster in v7) | Official recipe | ~1.6MB (was 14MB) |
| **Drizzle** | v0.45.1 | Code-first, SQL-like | Best (14x lower latency) | Community module | ~7.4KB |
| **TypeORM** | v0.3.x | Decorator-based Active Record/Data Mapper | Adequate | Official (`@nestjs/typeorm`) | Medium |
| **MikroORM** | v6.x | Data Mapper + Unit of Work | Good (batch ops) | Official recipe + `@mikro-orm/nestjs` | Medium |

### Prisma 7 (Major Update)

The biggest change in Prisma's history: **the Rust query engine has been completely removed.** Prisma 7 is now pure TypeScript:
- 90% smaller bundle (14MB -> 1.6MB)
- 3x faster query execution
- 98% fewer types to evaluate
- 70% faster type checks
- Works natively on edge runtimes (Vercel Edge, Cloudflare Workers)
- Generated code moved out of `node_modules`

This addressed Prisma's two biggest complaints: bundle size and the Rust binary dependency. Prisma 7 is a competitive option again.

### Drizzle ORM

Drizzle is the "SQL-in-TypeScript" approach — you write queries that map 1:1 to SQL. Key facts:
- Only 7.4KB minified+gzipped, zero dependencies
- Supports PostgreSQL, MySQL, SQLite, MSSQL
- Works on every runtime (Node, Bun, Deno, edge)
- 1,391 dependent npm packages
- Best raw performance of any TypeScript ORM
- Schema defined in TypeScript (not a DSL file)
- Built-in validator integration (Zod)

NestJS integration via community `nestjs-drizzle` module or manual setup. Trilon (NestJS consulting company) published an official guide: "NestJS & DrizzleORM: A Great Match."

### TypeORM

TypeORM is the "default" NestJS ORM with official `@nestjs/typeorm` module. However:
- Development has slowed significantly
- Still on v0.3.x (never reached v1.0)
- Known issues with complex relations and migrations
- Large open issue backlog
- Not recommended for new projects in 2026 by most sources

### MikroORM

MikroORM follows the Data Mapper + Unit of Work pattern (similar to Hibernate/Doctrine):
- Best for complex domain models with rich business logic
- Excellent maintenance quality (lowest issue-to-user ratio)
- Official NestJS recipe + `@mikro-orm/nestjs` v6.1.1
- Supports request context management
- Best fit for DDD-style architectures

### Head-to-Head: Prisma vs Drizzle (the 2026 choice)

| Factor | Prisma 7 | Drizzle |
|--------|----------|---------|
| **Developer velocity** | Faster (generated client, Prisma Studio) | Moderate (manual SQL-like queries) |
| **Performance** | Good (3x improvement in v7) | Best (14x lower latency than N+1 ORMs) |
| **Migrations** | Excellent (`prisma migrate`) | Good (`drizzle-kit`) |
| **Type safety** | Excellent (generated types) | Excellent (inferred from schema) |
| **Learning curve** | Lower (intuitive API) | Higher (need to know SQL) |
| **Bundle size** | 1.6MB | 7.4KB |
| **Edge/serverless** | Now works (v7) | Always worked |
| **NestJS integration** | Recipe/manual | Community module/manual |
| **Supabase** | Works via connection string | Works via connection string |
| **Community size** | Larger | Growing fast |
| **PostGIS support** | Via extension | Via community plugin |

### Verdict for Emuni

**Prisma 7 is recommended for Emuni.** Rationale:
1. **Solo developer velocity** — Prisma's auto-generated client, Prisma Studio GUI, and intuitive API let you ship faster
2. **Prisma 7 fixed the deal-breakers** — no more Rust binary, 90% smaller, 3x faster
3. **Migrations are production-grade** — `prisma migrate` handles schema evolution safely
4. **PostGIS for location** — Prisma supports raw SQL for PostGIS queries; or use Prisma + `@prisma/extension-accelerate`
5. **Prisma Studio** — visual database browser, invaluable for solo debugging
6. **Better documentation** — more tutorials, examples, and community support

If performance becomes a bottleneck at scale, Drizzle is the natural migration target (both use PostgreSQL, migration is straightforward).

Sources:
- [Prisma 7 Release](https://www.prisma.io/blog/announcing-prisma-orm-7-0-0)
- [Prisma 7 - InfoQ](https://www.infoq.com/news/2026/01/prisma-7-performance/)
- [Drizzle ORM npm](https://www.npmjs.com/package/drizzle-orm)
- [Drizzle vs Prisma 2026 - MakerKit](https://makerkit.dev/blog/tutorials/drizzle-vs-prisma)
- [NestJS & DrizzleORM - Trilon](https://trilon.io/blog/nestjs-drizzleorm-a-great-match)
- [Best ORM for NestJS 2025](https://dev.to/sasithwarnakafonseka/best-orm-for-nestjs-in-2025-drizzle-orm-vs-typeorm-vs-prisma-229c)
- [MikroORM competitive analysis](https://github.com/mikro-orm/mikro-orm/issues/7170)

---

## 8. Fastify Adapter for NestJS

### Performance Comparison

| Adapter | Requests/sec (200 concurrent) | Relative Performance |
|---------|------------------------------|---------------------|
| NestJS + Fastify v5 | ~50,000 | 3x faster |
| NestJS + Express v5 | ~17,000 | Baseline |

### Current State

NestJS 11 upgraded both adapters:
- **Express v5** is the new default (was v4)
- **Fastify v5** is fully supported via `@nestjs/platform-fastify`

### When to Use Fastify Adapter

**Advantages:**
- 3x raw throughput improvement
- Built-in JSON Schema validation
- Structured logging (pino)
- Better TypeScript support than Express
- Lower memory usage

**Disadvantages:**
- Some Express middleware won't work (must find Fastify equivalents)
- Fewer community examples/tutorials use Fastify
- Multer (file uploads) needs `@fastify/multipart` instead
- Some NestJS community packages assume Express

### Verdict for Emuni

**Use Fastify adapter.** Rationale:
1. 3x performance for free — matters when handling location queries + real-time messaging
2. NestJS 11 has first-class Fastify v5 support
3. Structured JSON logging built-in (matches NestJS 11's new JSON logging)
4. For a new project, there's no Express middleware lock-in to worry about
5. Setup is trivial: `NestFactory.create<NestFastifyApplication>(AppModule, new FastifyAdapter())`

The only caveat: if a critical NestJS community package requires Express, you'd need to check compatibility. For Emuni's needs (auth, WebSockets, Swagger, validation), all work with Fastify.

Sources:
- [NestJS Express vs Fastify 2026](https://www.index.dev/skill-vs-skill/backend-nestjs-vs-expressjs-vs-fastify)
- [Migrating NestJS Express to Fastify - PropertyGuru](https://propertyguru.tech/migrating-from-nestjs-express-to-nestjs-fastify-f94db4171fed)
- [NestJS Fastify comparison](https://medium.com/deno-the-complete-reference/nestjs-express-vs-fastify-comparison-for-hello-world-19875479e41d)
- [API with NestJS #89 - Replacing Express with Fastify](https://wanago.io/2023/01/02/api-nestjs-fastify/)

---

## 9. Breaking Changes & Deprecations

### NestJS 11 Breaking Changes (Affecting New Projects)

1. **Express v5 route syntax** — Wildcards must be named: `@Get('*splat')` instead of `@Get('*')`. Optional parameters need braces: `/:file{.:ext}`

2. **Global module middleware order** — Middleware in global modules now executes FIRST, regardless of import order. Design middleware accordingly.

3. **Lifecycle hooks order reversed** — `OnModuleDestroy`, `OnApplicationShutdown` hooks now fire in reverse order. Matters for cleanup logic.

4. **CacheModule → cache-manager v6** — Uses Keyv for unified key-value storage. If using caching, update configuration.

5. **setGlobalPrefix no longer supports RegExp** — Due to path-to-regexp upgrade. Use string prefixes only.

6. **Dynamic module deduplication changed** — If you import the same dynamic module with identical config multiple times, NestJS 11 treats them as separate instances (was deduplicated before).

### Node.js 24 Breaking Changes

1. **OpenSSL 3.5 security level 2** — RSA keys < 2048 bits are rejected. Affects legacy API integrations.
2. **Some deprecated APIs removed** — Check migration guide if upgrading from Node 22.

### Upcoming NestJS 12 Changes (Q3 2026)

These are NOT breaking yet but worth planning for:
- **Native ESM** will become the default — CommonJS will still work but ESM is the future
- **Standard Schema** will replace class-validator as the recommended validation approach
- **Vitest** will replace Jest as the default test runner for ESM projects

### Action Items for Emuni

Starting a new NestJS 11 project now, these are non-issues — they only affect migrations from older versions. Key things to do:

1. Use named wildcards in routes from day one
2. Design middleware with global-first execution in mind
3. Use Keyv-based cache configuration
4. Use string-only global prefixes
5. Target Node.js 24 LTS
6. Consider using Zod for validation (forward-compatible with NestJS 12's Standard Schema)

Sources:
- [NestJS Migration Guide](https://docs.nestjs.com/migration-guide)
- [NestJS 11 Features & Examples](https://medium.com/@atillataha/nestjs-11-new-features-and-examples-fb648ab797dc)
- [NestJS v11 setGlobalPrefix issue](https://github.com/nestjs/nest/issues/16095)

---

## 10. Recommendation for Emuni

### Final Stack Decision

| Layer | Choice | Version | Rationale |
|-------|--------|---------|-----------|
| **Runtime** | Node.js | 24 LTS (Krypton) | Official NestJS support, AWS il-central-1 native, EOL April 2028 |
| **Framework** | NestJS | 11.x | Best ecosystem, structured architecture, solo dev guardrails |
| **HTTP Adapter** | Fastify | v5 | 3x performance, structured logging, TypeScript-first |
| **API Paradigm** | REST | OpenAPI 3.1 | Universal compatibility, Swagger auto-docs, simplest for mobile |
| **ORM** | Prisma | v7.x | Fastest dev velocity, pure TS engine, Prisma Studio, great migrations |
| **Database** | PostgreSQL + PostGIS | via Supabase | Already decided in PRD |
| **Real-time** | WebSockets | NestJS Gateway | Already decided in PRD |
| **Validation** | Zod | (future-proof) | Forward-compatible with NestJS 12 Standard Schema |

### What Changed vs. Original PRD

| PRD Decision | Research Finding | Change Needed? |
|-------------|-----------------|---------------|
| NestJS | Still best choice, now v11 | Update version to 11.x |
| Node.js | v24 LTS is current | Update from unspecified to Node 24 |
| Express (implied) | Fastify adapter is 3x faster | **Switch to Fastify adapter** |
| TypeORM (common default) | Prisma 7 or Drizzle are better | **Use Prisma 7** |
| REST API | Still the right choice | No change |
| PostgreSQL + PostGIS | Still the right choice | No change |

### Risks to Monitor

1. **NestJS 12 migration (Q3 2026)** — ESM + Standard Schema changes may require code updates. Plan a half-day migration sprint.
2. **Prisma 7 is new** — Pure TS engine is a major architecture change. Watch for edge-case bugs in the first 6 months.
3. **Bun + NestJS** — If Anthropic pushes Bun adoption and NestJS adds official support, re-evaluate. Not before 2027.
4. **Hono** — If Emuni ever needs edge functions (CDN-level auth checks, geolocation), Hono is the best fit for that specific layer. Not for the main API.
