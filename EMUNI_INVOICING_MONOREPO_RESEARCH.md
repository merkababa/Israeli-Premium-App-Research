# Emuni Research: Invoicing (Morning/Green Invoice) & Monorepo Strategy

**Date:** March 7, 2026
**Status:** Research complete — pending founder decisions

---

## TABLE OF CONTENTS

1. [TOPIC 1: Morning (Green Invoice) vs Manual Invoicing](#topic-1-morning-green-invoice-vs-manual-invoicing)
   - 1.1 What is Morning (Green Invoice)?
   - 1.2 SHAAM and the Allocation Number System
   - 1.3 Manual Invoicing Alternative
   - 1.4 Other Israeli Invoicing Services
   - 1.5 Recommendation
2. [TOPIC 2: Monorepo (Turborepo) vs Polyrepo](#topic-2-monorepo-turborepo-vs-polyrepo)
   - 2.1 Turborepo Current State (March 2026)
   - 2.2 Alternative Monorepo Tools
   - 2.3 Monorepo Benefits for NestJS + Expo
   - 2.4 Monorepo Drawbacks and Pitfalls
   - 2.5 Polyrepo Benefits/Drawbacks
   - 2.6 Recommendation

---

# TOPIC 1: Morning (Green Invoice) vs Manual Invoicing

## 1.1 What is Morning (Green Invoice)?

**Morning** (formerly Green Invoice / חשבונית ירוקה) is Israel's leading digital invoicing and business management SaaS platform, used by **160,000+ businesses**. It was bootstrapped for a decade without outside investors, then acquired by Italian fintech giant TeamSystem for **$150 million** in 2025.

**What it does:**
- Digital invoice, receipt, and quote generation (all Israeli-compliant document types)
- Client and expense management
- Automatic bimonthly VAT reports for accountants
- Bank account integration (Israeli banks)
- Online payment acceptance (credit cards, Bit, digital wallets)
- **Automatic SHAAM allocation number retrieval** (mandatory from Jan 2026)
- Webhooks and API for programmatic invoice creation

**API Capabilities:**
- REST API at `https://api.greeninvoice.co.il/api/v1`
- Authentication via `api_key_id` + `api_key_secret` (sandbox + production environments)
- Create/manage documents programmatically (invoices, receipts, tax invoice-receipts)
- Supported document types include `TAX_INVOICE_RECEIPT` and others
- Enumerations for: `Currency`, `DocumentLanguage`, `DocumentType`, `PaymentCardType`, `PaymentDealType`, `PaymentType`, `IncomeVatType`
- Webhook support for payment events
- Make.com integration for no-code automation
- Community SDKs: Python ([yanivps/green-invoice](https://github.com/yanivps/green-invoice)), PHP ([MordiSacks/greeninvoice](https://github.com/MordiSacks/greeninvoice), [bariew/greeninvoice](https://github.com/bariew/greeninvoice))
- No official Node.js/TypeScript SDK found — you would call the REST API directly or build a thin wrapper

**API documentation:** [greeninvoice.docs.apiary.io](https://greeninvoice.docs.apiary.io/) (mostly in Hebrew)

**Limitation:** API access requires the **Best plan or higher** (not available on Basic).

### Pricing (March 2026, excl. VAT)

| Plan | Monthly (annual) | Monthly (monthly) | Documents/mo | API | Businesses | Overage |
|------|------------------|--------------------|-------------|-----|------------|---------|
| **Basic** | NIS 29 | NIS 29 | 20 | No | 1 | NIS 1.00/doc |
| **Best** (recommended) | NIS 45 | NIS 54 | 50 | Yes | 2 | NIS 1.00/doc |
| **Extra** | NIS 74 | NIS 89 | 200 | Yes | 3 | NIS 0.50/doc |
| **Prime** | NIS 129 | NIS 155 | 500 | Yes | 5 | NIS 0.15/doc |

**Free trial available** for all plans.

**For Emuni:** The **Best** plan at NIS 45/mo (annual) or NIS 54/mo (monthly) is the minimum for API access. At launch with ~50 transactions/month, this is within the 50-document limit.

Sources:
- [Morning pricing page](https://www.greeninvoice.co.il/pricing/)
- [Morning API docs (Apiary)](https://greeninvoice.docs.apiary.io/)
- [Unofficial API notes](https://github.com/danielrosehill/Green-Invoice-API-My-Notes)
- [Python SDK](https://github.com/yanivps/green-invoice)
- [TeamSystem acquisition — Calcalist](https://www.calcalistech.com/ctechnews/article/s1sss8hb1e)

---

## 1.2 SHAAM and the Allocation Number System

### What is SHAAM?

**SHAAM** (ש.א.מ — שידור אימות מקוון) is the Israel Tax Authority's (ITA) **Continuous Transaction Controls (CTC) clearance platform**. It validates B2B invoices in real time and issues a unique **allocation number** (מספר הקצאה) that proves the invoice was approved by the ITA.

### Why it matters

**Without an allocation number, the buyer cannot deduct input VAT.** This means your B2B customers will refuse invoices that should have an allocation number but don't — it directly costs them 18% of the invoice amount.

### Threshold Timeline

| Date | Threshold (excl. VAT) | Status |
|------|----------------------|--------|
| May 2024 | NIS 25,000 | Active |
| Jan 1, 2025 | NIS 25,000 (confirmed) | Active |
| **Jan 1, 2026** | **NIS 10,000** | **Now active** |
| **Jun 1, 2026** | **NIS 5,000** | **Upcoming — final threshold** |

After June 1, 2026, **any B2B invoice above NIS 5,000 (before VAT) requires an allocation number**.

### Scope: B2B Only

- **B2B transactions**: Mandatory (between VAT-registered businesses above threshold)
- **B2C transactions**: NOT mandatory (consumers cannot deduct VAT anyway)
- **B2G transactions**: NOT mandatory
- **Voluntary**: Any business can obtain allocation numbers for any invoice, any amount, any customer type — it is optional for sub-threshold and non-B2B transactions

### How it works

1. Supplier submits invoice data in JSON format to ITA via SHAAM API
2. ITA validates in real time
3. ITA returns a unique allocation number
4. Supplier records the allocation number on the tax invoice
5. Only then can the buyer claim VAT deduction

### Impact on Emuni

**At launch, Emuni's invoices to parents are B2C** — parents are consumers, not VAT-registered businesses. The SHAAM allocation number is NOT mandatory for B2C invoices. However:

- If Emuni ever invoices businesses (corporate accounts, daycare centers), SHAAM becomes mandatory above NIS 5,000
- Morning (Green Invoice) **handles allocation numbers automatically** — when you create an invoice above the threshold, it obtains the number from SHAAM before issuing
- This is a major reason to use Morning rather than manual invoicing: **SHAAM compliance is built-in**

Sources:
- [Avalara — E-invoicing in Israel](https://www.avalara.com/us/en/vatlive/country-guides/africa-and-middle-east/israel/e-invoicing-in-israel.html)
- [EDICOM — Israel CTC clearance model](https://edicomgroup.com/blog/israel-electronic-invoice-clearance-model)
- [VATupdate — Israel e-invoicing lower thresholds 2026](https://www.vatupdate.com/2025/12/14/israel-expands-mandatory-e-invoicing-lower-thresholds-and-new-vat-compliance-rules-for-2026/)
- [Flick — E-invoicing in Israel guide](https://www.flick.network/en-il/e-invoicing-in-israel)
- [Gov.il — Israel Invoices FAQ](https://www.gov.il/en/pages/faq_israel_invoice)
- [KPMG — Israel e-invoicing expansion](https://kpmg.com/us/en/taxnewsflash/news/2025/12/tnf-israel-expansion-of-mandatory-e-invoicing-model.html)

---

## 1.3 Manual Invoicing Alternative

### What "manual invoicing" means in Israel

In Israel, you have two legal options for issuing invoices:

1. **Pre-printed customized invoice booklets** (פנקסי חשבוניות) — physical receipt/invoice books purchased from authorized printers
2. **Tax Authority-approved online software** — any approved digital system (Morning, iCount, EZcount, YPAY, etc.)

### Mandatory fields on Israeli tax invoices

Per Israeli VAT invoice rules, every tax invoice must include:

| Field | Required |
|-------|----------|
| Supplier name (including trading name) and address | Yes |
| Customer name and address | Yes |
| Supplier's VAT number | Yes |
| The words "Tax Invoice" (חשבונית מס) and "Authorized Entrepreneur" (עוסק מורשה) | Yes |
| Invoice date | Yes |
| The word "Original" (מקור) on the original copy only | Yes |
| Description of goods/services (including quantities/weights) | Yes |
| Taxable amount, VAT amount (18%), gross total | Yes |
| Foreign currency conversion rate (if not NIS) | Yes |
| **Allocation number** (for B2B above threshold) | From June 2026 |

Invoices must be issued **within 14 days** of the taxable supply or cash settlement.

### Can you do it with Excel/receipt books?

**Technically yes, but increasingly impractical:**

- Physical receipt books are still legal for small businesses
- You could use Excel to track transactions and issue numbered invoices
- **But:** from June 2026, any B2B invoice above NIS 5,000 needs a SHAAM allocation number, which requires connecting to the ITA's API — you cannot do this from Excel or a receipt book
- For pure B2C (like Emuni's parent invoices), manual invoicing remains legal but time-consuming

### Time cost estimate

| Volume | Manual (Excel + receipt book) | Morning (Best plan) |
|--------|-------------------------------|---------------------|
| 10 transactions/mo | ~1-2 hours/mo | ~10 min/mo (automated) |
| 50 transactions/mo | ~5-8 hours/mo | ~30 min/mo |
| 200 transactions/mo | ~15-25 hours/mo (unsustainable) | ~1-2 hours/mo |
| 500 transactions/mo | Impossible manually | ~2-3 hours/mo |

Manual invoicing also requires:
- Maintaining a revenue accounting book (ספר הכנסות)
- Maintaining an external documents book
- Maintaining a receipts and payments book
- Filing bimonthly VAT returns (form 874) — Morning generates these automatically

### Osek Patur vs Osek Murshe

| | Osek Patur (exempt) | Osek Murshe (authorized) |
|--|---------------------|--------------------------|
| Threshold | Under NIS 120,000/year (2024-2026) | Above NIS 120,000/year or excluded professions |
| VAT | Exempt — do NOT charge VAT | Must charge 18% VAT |
| Invoices | Issue receipts (קבלות) | Issue tax invoices (חשבוניות מס) |
| VAT returns | Annual turnover declaration in January | Bimonthly VAT returns |
| VAT recovery | Cannot recover input VAT | Can recover input VAT on expenses |
| Invoice method | Receipt books or approved software | Pre-printed booklets or approved software |

**For Emuni:** If Year 1 revenue is NIS 120-300K (per existing projections), you will be an **Osek Murshe** and must charge 18% VAT on all invoices. Morning handles this automatically.

Sources:
- [Avalara — Israeli VAT invoice rules](https://www.avalara.com/vatlive/en/country-guides/africa-and-middle-east/israel/israeli-vat-invoice-rules.html)
- [Dray & Dray — Osek Patur Guide](https://cpa-dray.com/en/blog/osek-patur-guide/)
- [Dray & Dray — Osek Murshe Guide](https://www.cpa-dray.com/en/blog/the-osek-murshe-guide/)
- [Deel — Sole Proprietorship Israel](https://www.deel.com/blog/sole-proprietorship-israel/)

---

## 1.4 Other Israeli Invoicing Services

### Comparison Table

| Service | Free Tier | API | API Minimum Plan | Monthly Cost (lowest with API) | SHAAM Support | Notes |
|---------|-----------|-----|-----------------|-------------------------------|---------------|-------|
| **Morning (Green Invoice)** | Free trial only | Yes | Best (NIS 45-54/mo) | NIS 45/mo (annual) | Yes, automatic | Market leader. 160K+ businesses. Best ecosystem. |
| **iCount** | 45-day trial | Yes (higher plans) | Unknown | Pay-per-document model | Likely yes | Second largest. Per-document pricing may be cheaper at very low volume. |
| **EZcount (Hyp)** | 30-day trial | Yes (referenced) | Unknown | Unknown | Likely yes | 150K monthly invoices on platform. Acquired by Max. |
| **YPAY** | Yes (free forever) | Yes | NIS 50/mo add-on | NIS 50/mo (API only) | Unknown | Free invoicing + paid API. Smaller platform. |
| **Rivhit** | Unknown | Yes | Unknown | Unknown | Likely yes | More enterprise-focused. API docs at [rivhit-api.readme.io](https://rivhit-api.readme.io/docs/general). |

### YPAY — The Free Alternative

YPAY ([ypay.co.il](https://ypay.co.il/)) offers a notable free tier:

**Free features:**
- Invoice and receipt generation (no stated limit found)
- Customer management
- Digital signature
- Report generation
- Tax authority reports
- Email support

**Paid add-ons:**
- API access: NIS 50/mo
- Accounting management: NIS 100-2,200/mo
- Salary slips: NIS 50/slip
- Tax file opening: NIS 500 (one-time)

**For Emuni:** YPAY's free tier could work for manual invoice generation at launch, but if you need API access it costs NIS 50/mo — essentially the same as Morning's Best plan (NIS 45/mo annual) which includes much more functionality.

Sources:
- [YPAY official site](https://ypay.co.il/)
- [iCount pricing](https://www.icount.net/plans/)
- [iCount API](https://www.icount.net/features/api/)
- [Rivhit API docs](https://rivhit-api.readme.io/docs/general)
- [EZcount (Hyp) official site](https://www.ezcount.co.il)

---

## 1.5 Invoicing Recommendation

### Decision Matrix

| Scenario | Recommendation | Cost |
|----------|---------------|------|
| **Pre-launch (0 revenue)** | Don't pay for anything yet. Use nothing or YPAY free. | NIS 0/mo |
| **Soft launch (1-10 transactions/mo)** | YPAY free tier for manual invoicing, or Morning Basic (NIS 29/mo) if you want digital from Day 1 | NIS 0-29/mo |
| **Launch (10-50 transactions/mo)** | **Morning Best plan** — API access, automatic SHAAM, payment integration | NIS 45/mo (annual) |
| **Growth (50-200 transactions/mo)** | Morning Extra | NIS 74/mo (annual) |
| **Scale (200+ transactions/mo)** | Morning Prime | NIS 129/mo (annual) |

### Final Recommendation

**Start with Morning Best (NIS 45/mo annual billing) from the moment you have paying users.**

Rationale:
1. **SHAAM compliance is automatic** — Morning handles allocation numbers. This is mandatory from June 2026 for B2B invoices over NIS 5,000. Even though Emuni starts B2C, you may have B2B clients eventually, and Morning just handles it.
2. **API access included** — you can automate invoice creation from your NestJS backend when a booking is completed, eliminating manual work entirely.
3. **Bimonthly VAT reports generated automatically** — as an Osek Murshe, you must file these. Morning does it for you.
4. **NIS 45/mo is trivial** — at your projected NIS 260-370/mo infrastructure cost, adding NIS 45 (making it ~NIS 305-415/mo) is a rounding error compared to the hours saved.
5. **No Node.js SDK, but REST API is straightforward** — a thin wrapper around the REST API is ~50 lines of TypeScript.
6. **Can start manual and switch later?** Yes, but the switch cost is near-zero and manual invoicing at 50 transactions/month will eat 5-8 hours. Not worth it for a solo developer.

### Updated Cost Model

| Item | Previous Estimate | Updated |
|------|-------------------|---------|
| Monthly infrastructure | NIS 260-370/mo | NIS 305-415/mo (+NIS 45 Morning) |
| Pre-launch one-time | ~NIS 660 | ~NIS 660 (no change — Morning is post-launch) |

---

# TOPIC 2: Monorepo (Turborepo) vs Polyrepo

## 2.1 Turborepo Current State (March 2026)

### Latest Version

**Turborepo 2.8.13** (released ~March 5, 2026). Major release: **Turborepo 2.8** (January 23, 2026).

Turborepo is maintained by Vercel, written in Rust, and optimized for JavaScript/TypeScript monorepos.

### Key Features in Turborepo 2.8

| Feature | Description | Relevance for Solo Dev |
|---------|-------------|----------------------|
| **Git worktree support** | Cache shared across Git worktrees automatically | Useful if running AI coding agents in parallel branches |
| **Task descriptions** | `description` field in `turbo.json` for documenting tasks | Good for self-documentation and AI agent integration |
| **`turbo docs` command** | Search Turborepo docs from terminal | Helpful when stuck |
| **Agent Skill** | `npx skills add vercel/turborepo` for AI agents | Direct Turborepo expertise in Claude/Copilot |
| **AI-enabled docs** | Markdown routes for agent consumption | Better AI assistance |
| **Affected packages** (2.1+) | Run tasks only for changed packages since a baseline | Saves CI minutes — critical for free tier |
| **Remote caching** | Free via GitHub Actions cache setup | No extra cost |
| **Composable config** (2.7) | Extend turbo.json per-workspace | Cleaner config for NestJS vs Expo different needs |

### Setup Complexity

**Minimal.** One developer reported having Turborepo working in **15 minutes** vs 4 hours for Nx. Config is ~20 lines in `turbo.json`. Turborepo doesn't force project restructuring — it runs scripts defined in your `package.json`.

Upgrade path: `npx @turbo/codemod migrate` or start fresh with `npx create-turbo@latest`.

### CI/CD Impact (GitHub Actions)

- **Free tier: 2,000 min/mo** on GitHub Actions
- Turborepo caching reduces CI time dramatically: initial build ~30s, cached rebuild ~0.2s
- **Affected-only execution** is the biggest lever: running 4 packages instead of 45 beats any caching
- Remote caching via GitHub Actions cache: **free, no extra infrastructure**
- Reports of **70-85% faster build times** vs non-cached monorepo CI

Sources:
- [Turborepo 2.8 blog post](https://turborepo.dev/blog/2-8)
- [Turborepo official docs](https://turborepo.dev/docs)
- [Turborepo GitHub Actions guide](https://turborepo.dev/docs/guides/ci-vendors/github-actions)
- [turbo npm package](https://www.npmjs.com/package/turbo)
- [Turborepo GitHub releases](https://github.com/vercel/turborepo/releases)

---

## 2.2 Alternative Monorepo Tools

### Comparison Table (March 2026)

| Tool | Latest Version | Setup Time | Config Complexity | Caching | Best For |
|------|---------------|------------|-------------------|---------|----------|
| **Turborepo** | 2.8.13 | ~15 min | ~20 lines | Local + remote (free) | Solo devs, small teams, simplicity |
| **Nx** | 22.x | ~1-4 hours | ~200+ lines | Local + Nx Cloud (free tier) | Large teams, enterprise governance, code generation |
| **pnpm workspaces** | 9.x | ~5 min | ~5 lines | None built-in | Minimal setup, just shared deps |
| **npm workspaces** | Built into npm | ~5 min | ~5 lines | None built-in | Absolute minimum, no extra tools |
| **Lerna** | 8.x | ~30 min | Moderate | Via Nx (Lerna is now Nx-powered) | Legacy projects |

### Nx vs Turborepo — The Key Comparison

| Dimension | Turborepo | Nx |
|-----------|-----------|------|
| **Performance (small repo, <10 packages)** | 2.8s build | 8.3s build (3x slower) |
| **Performance (large repo, 50+ packages)** | Good | 7x better than Turbo |
| **Config** | ~20 lines | ~200+ lines |
| **Code generators** | None | Yes (scaffolding, migrations) |
| **Dependency graph visualization** | Basic | Advanced (interactive UI) |
| **Framework plugins** | None needed | NestJS, React Native, Expo plugins |
| **AI features (2026)** | Agent Skill, AI docs | "Build Intelligence Platform" |
| **Learning curve** | Minimal | Significant |
| **Opinionated?** | No — just runs your scripts | Yes — has opinions about project structure |

**Verdict for Emuni (solo dev, 2-3 packages):** Turborepo wins. Nx's advantages (code gen, governance, graph visualization) matter for large teams with 50+ packages. For a solo developer with NestJS backend + Expo mobile + shared types, Turborepo's simplicity is the right tradeoff.

### pnpm Workspaces — The Simpler Option

pnpm workspaces alone provide:
- Shared dependencies via global store
- Package linking (import from `@emuni/shared` in both apps)
- Script execution across workspaces (`pnpm -r run build`)

What pnpm workspaces do NOT provide:
- Task caching (rebuilds everything every time)
- Affected-only execution
- Parallel task orchestration with dependency awareness
- Remote caching for CI

**Can you use pnpm workspaces without Turborepo?** Yes. At 2-3 packages, the caching benefit is small. But Turborepo adds ~15 minutes of setup for significant CI time savings and better DX. The combination of **pnpm workspaces + Turborepo** is the standard recommendation.

Sources:
- [Dev.to — Turborepo vs Nx vs Lerna 2026](https://dev.to/dataformathub/turborepo-nx-and-lerna-the-truth-about-monorepo-tooling-in-2026-71)
- [Dev.to — Why I chose Turborepo over Nx](https://dev.to/saswatapal/why-i-chose-turborepo-over-nx-monorepo-performance-without-the-complexity-1afp)
- [Nx vs Turborepo for startups](https://nextbuild.co/blog/nx-vs-turborepo-monorepo-startups)
- [Nx 21.2 release (NestJS 11 support)](https://nx.dev/blog/nx-21-2-release)
- [pnpm workspaces docs](https://pnpm.io/workspaces)

---

## 2.3 Monorepo Benefits for NestJS + Expo

### Shared Zod Schemas — The Killer Feature

The #1 benefit for Emuni is **sharing Zod validation schemas** between NestJS backend and Expo frontend. This eliminates the entire class of "frontend sends X but backend expects Y" bugs.

**How it works in a monorepo:**

```
emuni/
  apps/
    api/          # NestJS 11 backend
    mobile/       # Expo SDK 55 (React Native)
  packages/
    shared/       # Zod schemas, TypeScript types, constants
      src/
        schemas/
          booking.ts    # BookingSchema + inferred types
          user.ts       # UserSchema + inferred types
          payment.ts    # PaymentSchema + inferred types
        constants/
          regions.ts
          pricing.ts
  turbo.json
  pnpm-workspace.yaml
```

The `packages/shared` package contains **only pure TypeScript + Zod** — no NestJS decorators, no React components, no platform-specific code. This keeps it 100% reusable.

```typescript
// packages/shared/src/schemas/booking.ts
import { z } from 'zod';

export const CreateBookingSchema = z.object({
  nannyId: z.string().uuid(),
  date: z.string().datetime(),
  startTime: z.string(),
  endTime: z.string(),
  childrenCount: z.number().int().min(1).max(6),
});

export type CreateBookingInput = z.infer<typeof CreateBookingSchema>;
// ^ This exact type is used in BOTH NestJS DTOs and React Native forms
```

Both apps import from `@emuni/shared`:
- **NestJS**: Uses schemas with `nestjs-zod` for automatic request validation
- **Expo**: Uses schemas with React Hook Form + Zod resolver for form validation

**Result: validation logic is written ONCE and enforced identically on both sides.**

### Other Monorepo Benefits

| Benefit | Impact for Solo Dev |
|---------|-------------------|
| **Shared TypeScript types** | API response types match frontend expectations — zero drift |
| **Atomic commits** | Change API + mobile + shared types in one commit |
| **Single CI pipeline** | One GitHub Actions workflow, not three |
| **Unified dependency management** | One place to update Zod, TypeScript, etc. |
| **Easier refactoring** | Rename a field and TypeScript catches every usage across all apps |
| **Single `git clone`** | New machine setup = one clone, one `pnpm install` |

Sources:
- [Dev.to — Sharing types between React + NestJS in pnpm monorepo](https://dev.to/lico/step-by-step-guide-sharing-types-and-values-between-react-esm-and-nestjs-cjs-in-a-pnpm-monorepo-2o2j)
- [Compiledbox — Share types across Next.js & NestJS with Zod](https://compiledbox.com/blog/share-types-across-nextjs-nestjs-with-zod)
- [Michael Guay — Type-safe full-stack with Zod](https://michaelguay.dev/type-safe-full-stack-development-shared-types-between-tanstack-router-and-nestjs-with-zod/)

---

## 2.4 Monorepo Drawbacks and Pitfalls

### Expo-Specific Pitfalls

| Issue | Severity | Mitigation |
|-------|----------|------------|
| **Duplicate React Native versions** | Critical — causes runtime crashes | pnpm `overrides` in root `package.json` to force single version |
| **Metro bundler module resolution** | Medium — historically painful | **SDK 52+ auto-configures Metro for monorepos**. SDK 55 adds automatic autolinking. Much less painful than 2023-2024. |
| **Hoisting issues** | Medium | Set `node-linker=hoisted` in `.npmrc` for Expo compatibility |
| **EAS Build uploads entire monorepo** | Low — slower builds | Use `EXPO_MONOREPO_ROOT` env var. Turborepo caching helps locally. |
| **Duplicate Turbo/Expo module versions** | Medium | Enforce single versions via pnpm overrides |

**Critical improvement:** Since **Expo SDK 52** (and Emuni targets SDK 55), Metro is auto-configured for monorepos. The historically painful manual Metro configuration is no longer needed if you use `expo/metro-config`. This removes the biggest pain point.

### General Monorepo Drawbacks

| Drawback | Impact for Solo Dev |
|----------|-------------------|
| **Initial setup complexity** | ~15-30 min with Turborepo (one-time cost) |
| **Larger git clone** | Negligible for 2-3 packages |
| **Mental overhead** | Low — you wrote all the code, you know where everything is |
| **CI builds entire repo** | Mitigated by Turborepo affected-only execution |
| **Tight coupling risk** | Mitigated by keeping shared package pure (no platform deps) |

### Proven Templates

Multiple production-ready Turborepo + NestJS + Expo templates exist:

1. **[barisgit/nextjs-nestjs-expo-template](https://github.com/barisgit/nextjs-nestjs-expo-template)** — Full-stack type-safe monorepo with NestJS, Expo, tRPC, typed WebSockets
2. **[ax-at/expo-nextjs-nestjs-trpc-turborepo](https://github.com/ax-at/expo-nextjs-nestjs-trpc-turborepo)** — Expo + NestJS + tRPC in Turborepo
3. **[Marknjo/create-turbo-with-expo](https://github.com/Marknjo/create-turbo-with-expo)** — Turbo Monorepo starter with Expo + NestJS
4. **[byCedric/expo-monorepo-example](https://github.com/byCedric/expo-monorepo-example)** — Cedric's canonical pnpm + Expo monorepo example (Expo team member)

Sources:
- [Expo monorepo guide](https://docs.expo.dev/guides/monorepos/)
- [Medium — React Native monorepo with Turbo + pnpm](https://medium.com/code-sense/how-i-finally-got-a-react-native-monorepo-working-with-turbo-pnpm-and-an-expo-shell-after-c8afd85522ea)
- [NestJS monorepo issue with pnpm](https://github.com/nestjs/nest/issues/13463)

---

## 2.5 Polyrepo Benefits/Drawbacks

### Polyrepo for Emuni would mean:

```
emuni-api/         # Separate repo — NestJS backend
emuni-mobile/      # Separate repo — Expo app
emuni-shared/      # Separate repo — shared types (published to npm?)
```

### Benefits

| Benefit | Relevance to Solo Dev |
|---------|----------------------|
| Simpler git history per repo | Marginal — you're the only committer |
| Independent deployments | Already achievable in monorepo with Turborepo |
| Smaller clone size per repo | Negligible for small projects |
| No monorepo tooling to learn | Saves ~15-30 min setup |

### Drawbacks

| Drawback | Severity for Solo Dev |
|----------|----------------------|
| **Type duplication / drift** | HIGH — must manually sync types between repos. This is the #1 source of bugs in polyrepo full-stack projects. |
| **No atomic commits** | HIGH — "change API field name" requires 3 separate PRs across 3 repos. Easy to forget one. |
| **Shared package distribution** | HIGH — must publish `emuni-shared` to npm (or private registry) and version it. Adds friction to every schema change. |
| **Multiple CI pipelines** | Medium — 3 separate GitHub Actions configs to maintain |
| **Dependency version drift** | Medium — Zod v3.24 in api, v3.23 in mobile = subtle bugs |
| **3 separate `git clone`** + `npm install` | Low — minor inconvenience |

### The "shared types" problem in polyrepo

Without a monorepo, sharing Zod schemas requires one of:
1. **npm package** — publish `@emuni/shared` to npm, version it, update in both consumers on every change
2. **Git submodule** — universally hated, fragile, confusing
3. **Copy-paste** — guaranteed drift
4. **tRPC** — generates types from API, but adds complexity and doesn't cover all use cases

All of these add friction that a monorepo eliminates entirely.

---

## 2.6 Monorepo Recommendation

### Verdict: Monorepo with Turborepo + pnpm workspaces

**Yes, a monorepo is worth the setup overhead for a solo developer building NestJS + Expo.**

The decision is clear for three reasons:

1. **Shared Zod schemas** are the single highest-leverage productivity tool for a solo full-stack developer. Eliminating type drift between frontend and backend prevents an entire category of bugs. This alone justifies the monorepo.

2. **Setup cost is minimal.** With Turborepo 2.8 and Expo SDK 55, the historically painful Metro configuration issues are resolved. Setup takes ~15-30 minutes using an existing template as reference.

3. **CI savings compound.** Turborepo's caching and affected-only execution reduce GitHub Actions minutes, which matters on the free tier (2,000 min/mo).

### Recommended Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| **Package manager** | pnpm | Fastest installs, best monorepo support, strict dependency resolution |
| **Monorepo orchestrator** | Turborepo 2.8 | Minimal config, free caching, Expo-compatible |
| **NOT Nx** | — | Overkill for 2-3 packages. Adds complexity without proportional benefit for solo dev. |
| **NOT plain pnpm workspaces** | — | Missing caching, affected-only execution, task orchestration. Turborepo adds these for ~15 min of setup. |

### Recommended Structure

```
emuni/
  apps/
    api/                  # NestJS 11 + Fastify
      package.json
      src/
      tsconfig.json
    mobile/               # Expo SDK 55 (React Native)
      package.json
      app/                # Expo Router v7
      tsconfig.json
  packages/
    shared/               # Pure TypeScript + Zod
      package.json        # name: "@emuni/shared"
      src/
        schemas/          # Zod schemas (booking, user, payment, etc.)
        types/            # Additional TypeScript types
        constants/        # Shared constants (regions, pricing tiers)
      tsconfig.json
    eslint-config/        # Shared ESLint config (optional)
    tsconfig/             # Shared tsconfig bases (optional)
  turbo.json
  pnpm-workspace.yaml
  package.json            # Root — workspace config, shared devDeps
  .npmrc                  # node-linker=hoisted (for Expo)
```

### Key Configuration Files

**pnpm-workspace.yaml:**
```yaml
packages:
  - "apps/*"
  - "packages/*"
```

**turbo.json (minimal):**
```json
{
  "$schema": "https://turborepo.dev/schema.json",
  "tasks": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    },
    "dev": {
      "cache": false,
      "persistent": true
    },
    "lint": {},
    "typecheck": {
      "dependsOn": ["^build"]
    },
    "test": {}
  }
}
```

### What NOT to do

1. **Do NOT put React Native components in the shared package** — keep it pure TypeScript + Zod. Platform-specific code stays in `apps/`.
2. **Do NOT skip `node-linker=hoisted`** in `.npmrc` — Expo requires hoisted dependencies.
3. **Do NOT use Yarn** — pnpm is the recommended package manager for Turborepo + Expo monorepos.
4. **Do NOT over-engineer the shared package** — start with just Zod schemas. Add more only when you need it.

Sources:
- [Expo monorepo documentation](https://docs.expo.dev/guides/monorepos/)
- [Turborepo structuring a repository](https://turborepo.dev/docs/crafting-your-repository/structuring-a-repository)
- [Simform — monorepo vs polyrepo](https://www.simform.com/blog/monorepo-vs-polyrepo/)
- [Graphite — monorepo vs polyrepo pros/cons](https://graphite.com/guides/monorepo-vs-polyrepo-pros-cons-tools)

---

# SUMMARY OF DECISIONS NEEDED

| # | Decision | Recommended | Alternative | Impact |
|---|----------|-------------|-------------|--------|
| 1 | **Invoicing provider** | Morning Best (NIS 45/mo annual) | YPAY free (manual) or Morning Basic (NIS 29/mo, no API) | Start from first paying user |
| 2 | **Monorepo vs polyrepo** | Monorepo | Polyrepo (3 repos) | Architecture — decide before writing code |
| 3 | **Monorepo tool** | Turborepo + pnpm | Nx, or plain pnpm workspaces | Decide with #2 |
| 4 | **Business registration type** | Osek Murshe (if revenue > NIS 120K) | Osek Patur (if revenue < NIS 120K) | Affects invoicing, VAT, reporting |

---

# APPENDIX: Updated Infrastructure Cost Model

| Item | Monthly Cost | Notes |
|------|-------------|-------|
| Supabase (free tier) | NIS 0 | Up to 500MB DB, 50K auth users |
| Veriff (per-check) | ~NIS 3/check | ~$0.80/check |
| Sentry (free tier) | NIS 0 | 5K errors/mo |
| UptimeRobot (free) | NIS 0 | 50 monitors |
| PostHog (free tier) | NIS 0 | 1M events/mo |
| GitHub Actions (free) | NIS 0 | 2,000 min/mo |
| Expo Notifications | NIS 0 | Free, unlimited |
| AWS il-central-1 (API server) | NIS 260-370 | EC2/ECS + networking |
| **Morning Best** | **NIS 45** | **NEW: invoicing + SHAAM** |
| **TOTAL** | **NIS 305-415/mo** | **+ ~NIS 3 per Veriff check** |
