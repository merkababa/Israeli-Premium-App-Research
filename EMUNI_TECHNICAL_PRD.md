# EMUNI — Technical PRD

**Version:** 1.1
**Date:** March 8, 2026
**Companion Documents:** `EMUNI_PRD.md` (v1.2), `EMUNI_ROADMAP.md` (v1.1)
**Method:** 7 parallel research agents, web-verified (no training data). 190+ web searches across all stack components.
**Status:** APPROVED — All decisions resolved. Ready for development.

---

## TABLE OF CONTENTS

1. [Stack Decision Summary](#1-stack-decision-summary)
2. [Frontend Architecture](#2-frontend-architecture)
3. [Backend Architecture](#3-backend-architecture)
4. [Database & Data Layer](#4-database--data-layer)
5. [Identity Verification](#5-identity-verification)
6. [Payment Processing](#6-payment-processing)
7. [Maps & Geolocation](#7-maps--geolocation)
8. [Push Notifications](#8-push-notifications)
9. [Real-Time Messaging](#9-real-time-messaging)
10. [Cloud Infrastructure](#10-cloud-infrastructure)
11. [DevOps & Monitoring](#11-devops--monitoring)
12. [Cost Model](#12-cost-model)
13. [PRD v1.2 Delta](#13-prd-v12-delta)
14. [Resolved Decisions](#14-resolved-decisions)

---

## 1. STACK DECISION SUMMARY

### Final Stack (Web-Verified March 2026)

| Layer | Technology | Version | Why |
|-------|-----------|---------|-----|
| **Mobile** | Expo (managed) | SDK 55 (v55.0.5) | Bundles RN 0.83, React 19.2. New Architecture mandatory. File-based routing. Zero-config builds. |
| **Navigation** | Expo Router | v7 | File-based routing, automatic deep linking, native tabs |
| **State (server)** | TanStack Query | v5 | Caching, background refetch, offline support |
| **State (client)** | Zustand | v5 | 9M+ weekly downloads, minimal boilerplate |
| **Language** | TypeScript | 5.x (strict) | Universal standard for RN + NestJS |
| **Backend** | NestJS + Fastify v5 | v11.x | Enterprise structure, DI, guards, 3x Express throughput |
| **Runtime** | Node.js | 24 LTS | Active LTS until April 2028 |
| **ORM** | Drizzle | Latest | Native PostGIS, no code gen, 7.4KB bundle, SQL-like type-safe queries |
| **Validation** | Zod | v3 | Forward-compatible with NestJS 12 Standard Schema |
| **Database** | PostgreSQL + PostGIS | PG 16+ / PostGIS 3.x | Via Supabase managed |
| **Auth/Realtime** | Supabase | Latest | Phone OTP, Realtime WebSocket, RLS |
| **ID Verification** | Didit | Free tier | 500 free/mo, $0.30/check after, Expo plugin, confirmed TZ support |
| **Maps** | Google Maps Platform | Routes API | Best Hebrew geocoding, 10K free elements/mo |
| **Payments (v1)** | Manual Bit + Morning | — | Invoicing + SHAAM in one API |
| **Payments (v2)** | PayMe | — | Only Israeli marketplace split processor |
| **Push** | Expo Notifications | (bundled) | Free, unlimited, zero setup |
| **Analytics** | PostHog | Free tier | 1M events + session replay + feature flags |
| **Errors** | PostHog (errors) | Free tier | 100K exceptions/mo, replaces Sentry |
| **Cloud** | AWS il-central-1 | — | Israeli data residency, Supabase compatibility |
| **CI/CD** | GitHub Actions | Free tier | 2,000 min/mo private repos |
| **Uptime** | UptimeRobot | Free tier | 50 monitors |

### Changes from PRD v1.1

| Component | PRD v1.1 Says | This Technical PRD Says | Reason |
|-----------|--------------|------------------------|--------|
| ID Verification | AU10TIX | **Didit** | AU10TIX enterprise-only, 2024 breach. Veriff disqualified (no TZ). Didit: 500 free/mo, $0.30/check, Expo plugin. |
| ORM | (not specified) | **Drizzle** | Native PostGIS support (decisive), no code gen, 7.4KB bundle, SQL-like type-safe queries |
| Analytics | Mixpanel | **PostHog** | 1M free events + session replay + feature flags. Mixpanel reduced free tier. |
| Errors | (not specified) | **PostHog (errors)** | 100K exceptions/mo free — replaces Sentry (5K limit). One fewer vendor. |
| State Management | (not specified) | **TanStack Query + Zustand** | 2026 consensus: separate server state (TQ) from client state (Zustand) |
| Navigation | (not specified) | **Expo Router v7** | File-based routing, automatic deep links, native tabs |
| Node.js | (not specified) | **Node.js 24 LTS** | Active LTS, supported until April 2028 |
| HTTP Adapter | Fastify (mentioned) | **Fastify v5** (confirmed) | NestJS 11 first-class support, 3x Express throughput |
| Validation | (not specified) | **Zod** | Forward-compatible with NestJS 12 Standard Schema |
| Payments v1 | Manual Bit | **Manual Bit + Morning (Green Invoice)** | Morning handles invoicing + SHAAM in one API |
| Uptime | (not specified) | **UptimeRobot** | 50 free monitors |

---

## 2. FRONTEND ARCHITECTURE

### Expo SDK 55 (February 25, 2026)

- Bundles **React Native 0.83** and **React 19.2**
- **New Architecture is mandatory** (Legacy Architecture fully removed in RN 0.82, Oct 2025)
- **Hermes V1** is the default JS engine (cannot be disabled)
- Minimum iOS: **15.1** (will bump to 16.4 in SDK 56, expected Q2 2026)
- Minimum Android: **API 24** (Android 7.0)
- Node.js: **24.x LTS** recommended

### Project Structure

```
emuni/
├── src/
│   ├── app/                    # Expo Router file-based routes
│   │   ├── (auth)/             # Auth group (login, register)
│   │   ├── (family)/           # Family tab group
│   │   │   ├── search/         # Nanny search + filters
│   │   │   ├── bookings/       # Booking list + details
│   │   │   ├── messages/       # Conversations
│   │   │   └── profile/        # Family profile + settings
│   │   ├── (nanny)/            # Nanny tab group
│   │   │   ├── requests/       # Booking requests
│   │   │   ├── bookings/       # Active bookings
│   │   │   ├── messages/       # Conversations
│   │   │   └── profile/        # Nanny profile + availability
│   │   ├── (admin)/            # Admin panel routes
│   │   └── _layout.tsx         # Root layout
│   ├── components/             # Shared UI components
│   ├── hooks/                  # Custom hooks
│   ├── services/               # API client (TanStack Query)
│   ├── stores/                 # Zustand stores
│   ├── i18n/                   # Hebrew + English translations
│   ├── utils/                  # Helpers
│   └── constants/              # Theme, config
├── app.config.ts               # Expo config
├── tsconfig.json
└── package.json
```

### RTL Configuration

```json
// app.config.ts
{
  "expo": {
    "extra": {
      "supportsRTL": true,
      "forcesRTL": true
    },
    "plugins": ["expo-localization"]
  }
}
```

- Use `paddingStart`/`paddingEnd` instead of `paddingLeft`/`paddingRight`
- `flexDirection: 'row'` automatically reverses in RTL
- **RTL does NOT work in Expo Go** — must use development builds for testing
- RN 0.79 fixed the iOS RTL restart bug — dynamic layout switching works

### State Management Architecture

```
TanStack Query v5  →  All API data (nanny search, bookings, profiles, reviews)
                       Caching, background refetch, optimistic updates

Zustand v5         →  Auth state, booking flow state, user preferences
                       Persisted to AsyncStorage where needed

useState           →  Form inputs, UI toggles, ephemeral state

React Context      →  Theme, locale (he/en), accessibility settings
```

### Key Libraries

| Library | Purpose | Version |
|---------|---------|---------|
| `expo-router` | File-based navigation | v7 (SDK 55) |
| `@tanstack/react-query` | Server state | v5 |
| `zustand` | Client state | v5 |
| `react-native-maps` | Map views | Latest (NOT `expo-maps` — still alpha) |
| `expo-notifications` | Push notifications | SDK 55 |
| `expo-localization` | i18n + RTL | SDK 55 |
| `react-native-reanimated` | Animations | v3 |
| `expo-image` | Optimized images | SDK 55 |
| `expo-secure-store` | Sensitive local storage | SDK 55 |
| `react-hook-form` | Form management | v7 |
| `zod` | Schema validation (shared with backend) | v3 |

### Why NOT These Alternatives

| Alternative | Verdict | Why Not |
|-------------|---------|---------|
| Flutter | ~46% market share but uses Dart | Switching cost too high for solo JS/TS dev. Smaller talent pool (3-4x). |
| Kotlin Multiplatform | Stable since 2023, Compose Multiplatform stable May 2025 | Requires Kotlin expertise. No file-based routing. Smaller ecosystem. |
| .NET MAUI | MAUI 9 shipping | Performance issues, thin ecosystem, smallest community. |
| Bare React Native | Still an option | No benefit over Expo for this app. Expo is the default recommendation in 2026. |

---

## 3. BACKEND ARCHITECTURE

### NestJS v11 on Node.js 24 LTS

- **NestJS 11.1.16** (stable since January 2025)
- **NestJS 12** planned Q3 2026 — native ESM, Zod/Standard Schema validation, Vitest
- **Fastify v5** adapter — 3x throughput vs Express, structured logging, better TypeScript
- **Node.js 24 "Krypton"** (v24.14.0) — Active LTS until April 2028

### Backend Project Structure

```
emuni-api/
├── src/
│   ├── app.module.ts
│   ├── main.ts                     # Fastify bootstrap
│   ├── common/
│   │   ├── guards/                 # Auth, role guards
│   │   ├── interceptors/          # Logging, transform
│   │   ├── filters/               # Exception filters
│   │   ├── decorators/            # Custom decorators
│   │   └── pipes/                 # Zod validation pipe
│   ├── modules/
│   │   ├── auth/                  # Phone OTP via Supabase
│   │   ├── families/              # Family CRUD
│   │   ├── nannies/               # Nanny CRUD + search
│   │   ├── bookings/              # Booking lifecycle
│   │   ├── reviews/               # Mutual review system
│   │   ├── messages/              # In-app messaging
│   │   ├── verification/          # Didit integration
│   │   ├── subscriptions/         # Premium/Founding tiers
│   │   ├── notifications/         # Expo push
│   │   └── admin/                 # Admin panel API
│   ├── drizzle/
│   │   ├── schema.ts              # Database schema
│   │   └── migrations/            # Migration history
│   └── shared/
│       ├── schemas/               # Zod schemas (shared with frontend)
│       └── types/                 # Shared TypeScript types
├── test/
├── tsconfig.json
└── package.json
```

### API Design

- **RESTful**, versioned: `/api/v1/`
- **JWT auth** via Supabase Auth (access token + refresh token)
- **Zod validation** on all inputs (forward-compatible with NestJS 12)
- **Drizzle ORM** for database access — native PostGIS, no code gen, 7.4KB bundle
- **Swagger/OpenAPI** auto-generated from decorators
- Rate limiting: 100 req/min general, 10 req/min search

### Why NOT These Alternatives

| Alternative | Verdict | Why Not |
|-------------|---------|---------|
| Hono | Rising star, great for edge/lightweight | Lacks NestJS's DI, guards, interceptors, official modules. Too minimal for marketplace. |
| ElysiaJS | Bun-only, very fast | Bun not officially supported by NestJS. Too risky for solo dev. |
| Encore.ts | Interesting DX | Vendor lock-in. Small community. |
| tRPC | Great type safety | Locks you to TypeScript clients. REST more practical for mobile + future web. |
| Bun runtime | 2-3.5x faster than Node, now Anthropic-backed | NestJS doesn't officially support it. Runtime incompatibility risk too high for solo dev. |
| Deno | v2.7.4 active | LTS ends April 2026. Not suitable. |

### ORM: Drizzle

**Why Drizzle over Prisma 7:**
- **Native PostGIS support** — `ST_DWithin`, `GEOGRAPHY` types without raw SQL (decisive factor; Prisma requires raw SQL for PostGIS)
- **No code generation step** — schema defined in TypeScript, no `prisma generate`
- **7.4KB bundle** — dramatically smaller than Prisma's client
- **SQL-like type-safe queries** — reads like SQL, full TypeScript inference
- Migrations via `drizzle-kit push` / `drizzle-kit generate`

### Monorepo: Turborepo + pnpm Workspaces

- **Turborepo** for task orchestration (build, lint, test) with caching
- **pnpm workspaces** for dependency management — strict, fast, disk-efficient
- Shared Zod schemas between frontend and backend in a `packages/shared` workspace
- Single CI pipeline via GitHub Actions

---

## 4. DATABASE & DATA LAYER

### Supabase (Managed)

- **Hosting region:** Frankfurt (eu-central-1) — **no Israel region available**
- Latency to Israel: ~50-80ms (acceptable for CRUD, not ideal for real-time gaming)
- **Self-hosting on AWS il-central-1** adds significant ops complexity — not recommended for solo founder
- **Decision: Use Supabase managed in Frankfurt** — legally acceptable (Israel has no data residency mandate), soften marketing to "EU-hosted" not "Israel-hosted"

### Supabase Services Used

| Service | What For | Free Tier | Pro ($25/mo) |
|---------|----------|-----------|-------------|
| **Auth** | Phone OTP, JWT | 50K MAU | 100K MAU |
| **Database** | PostgreSQL 16 + PostGIS | 500MB, 2 projects | 8GB, unlimited |
| **Realtime** | WebSocket messaging | 200 connections, 2M msgs/mo | 500 connections, 5M msgs/mo |
| **Storage** | Profile photos, ID docs | 1GB | 100GB |
| **RLS** | Row-Level Security | Included | Included |

### PostgreSQL + PostGIS

- **PostgreSQL 16+** (via Supabase)
- **PostGIS 3.x** for geospatial queries
- All locations stored as `GEOGRAPHY(POINT, 4326)` — WGS 84
- `ST_DWithin` for radius filtering (parameterized: 1/3/5/10/15km)
- Hebrew full-text search via `tsvector`

### Drizzle + Supabase

Drizzle connects to Supabase's PostgreSQL via connection string. Native PostGIS support via `ST_DWithin` and `GEOGRAPHY` types without raw SQL. Supabase RLS still applies for direct client access (Realtime subscriptions). Backend API uses Drizzle (bypasses RLS via service role key).

---

## 5. IDENTITY VERIFICATION

### Recommendation: Didit (replaces Veriff and AU10TIX)

| Criteria | Didit (Primary) | Shufti Pro (Fallback) | Veriff (Disqualified) | AU10TIX |
|----------|----------------|----------------------|----------------------|---------|
| **Pricing** | **500 free/mo, $0.30/check after** | $0.20/check | $0.80/verification, $49/mo min | Enterprise-only |
| **Self-serve** | **Yes** | Yes | Yes | No |
| **Free tier** | **500 verifications/mo** | No | 15-day trial only | No |
| **Expo/RN SDK** | **Yes (Expo plugin)** | Yes | Yes | No |
| **Israeli ID (Teudat Zehut)** | **Yes (confirmed)** | **Yes (confirmed)** | **NO — does NOT support TZ** | Yes (native) |
| **Liveness detection** | Yes | Yes | Yes | Yes |
| **Data breach history** | None known | None known | None known | **Major 2024 breach** |
| **Bootstrapper-friendly** | **Yes (best)** | Yes | Moderate | No |

### Why Didit

1. **500 free verifications/month** — covers Emuni's entire first year at launch scale
2. **$0.30/check after free tier** — cheapest per-check pricing among major providers
3. **Expo plugin available** — native integration with Expo development builds
4. **Confirmed Teudat Zehut support** — both old laminated and new biometric smart card
5. **No data breach history** — critical for a trust-based platform

### Why NOT Veriff

**Veriff was recommended in v1.0 but is now DISQUALIFIED:** research confirmed Veriff does **not** support Teudat Zehut (Israeli national ID). This is a hard blocker for an Israeli nanny platform.

### Fallback: Shufti Pro

If Didit encounters issues in production, Shufti Pro is the backup:
- $0.20/check (even cheaper per-check, but no free tier)
- Confirmed Teudat Zehut support
- RN SDK available

### Estimated Cost

| Period | Verifications | Cost |
|--------|:---:|:---:|
| Pre-launch (50 nannies) | 50 | **$0** (within free tier) |
| Year 1 (500 nannies) | ~40/mo avg | **$0/mo** (under 500/mo free tier) |
| Year 2 (2,000 nannies) | ~150/mo avg | **$0/mo** (under 500/mo free tier) |
| Overflow months | 500+ | $0.30 × overflow count |

---

## 6. PAYMENT PROCESSING

### v1: Manual Bit + Morning (Green Invoice)

| Component | Service | Cost |
|-----------|---------|------|
| Family→Nanny payment | **Bit P2P** (direct, platform not involved) | Free |
| Family→Platform subscription | **Bit transfer** to business account | Free |
| Invoicing | **Morning (Green Invoice)** | NIS 45/mo (Best plan) |
| SHAAM e-invoicing | **Morning API** (built-in) | Included |
| Admin activation | Manual (founder verifies Bit payment, activates premium) | — |

**Why Morning (Green Invoice):** 160K+ Israeli businesses use it. Single API for invoicing + SHAAM compliance. Eliminates need for separate SHAAM integration. Best plan at NIS 45/mo from Day 1.

### v2: PayMe (Month 3+)

| Component | Service | Fee |
|-----------|---------|-----|
| Subscription billing | PayMe recurring | 1.5-2.5% |
| Marketplace splits | PayMe split payments | Included |
| Nanny payouts | PayMe → bank account | Included |
| Bit as payment method | PayMe Bit integration | Included |
| SHAAM e-invoicing | PayMe or Morning | Included |

**PayMe remains the only Israeli processor with native marketplace split payments.** No alternative found. Stripe is still NOT available in Israel.

### SHAAM E-Invoicing Timeline

| Date | Threshold |
|------|-----------|
| January 1, 2026 | NIS 10,000+ (current) |
| **June 1, 2026** | **NIS 5,000+** (permanent floor) |

Emuni's NIS 49 subscriptions are well below both thresholds. SHAAM only relevant for B2B contracts.

### Apple IAP

- **15% commission** on in-app subscriptions (Small Business Program, <$1M revenue)
- NIS 49 → ~NIS 41.65 net | NIS 29 → ~NIS 24.65 net | NIS 19 → ~NIS 16.15 net
- **Apple Pay fully operational in Israel** since May 2021
- **Google Pay:** online payments yes, NFC contactless in stores NOT supported in Israel

---

## 7. MAPS & GEOLOCATION

### Google Maps Platform (Routes API)

**Pricing changed March 1, 2025:** $200/mo credit removed, replaced by per-SKU free thresholds.

| SKU | Free Threshold | Overage | Emuni Usage |
|-----|:---:|:---:|---|
| Geocoding | 10,000/mo | $5/1,000 | Address lookup on registration |
| Routes API (computeRouteMatrix) | 10,000 elements/mo | $5/1,000 | Travel time for top 5 search results |
| Maps SDK (mobile) | Unlimited | Free | Map view on nanny profiles |
| Places Autocomplete | 10,000/mo | $2.83/1,000 | Address autocomplete |

**Estimated cost at launch: $0/mo.** At 1,000 users: ~$10-25/mo. The new free thresholds are actually more generous than the old $200 credit for small apps.

### Distance Matrix API Status

- **Legacy since March 2025** — still works for existing projects, not available for new ones
- **No shutdown date** — 12 months' notice will be given
- **Use Routes API `computeRouteMatrix`** for all new development

### Maps Library

- Use **`react-native-maps`** (stable, Fabric-compatible)
- Do **NOT** use `expo-maps` — still alpha, requires iOS 18.0
- Google Maps on Android, Apple Maps on iOS (automatic via react-native-maps)

### Why NOT Alternatives

| Alternative | Why Not |
|-------------|---------|
| Mapbox | Geocoding optimized for North America/Europe, not Israeli Hebrew addresses |
| Apple MapKit | iOS-only, poor Hebrew address geocoding |
| OSM/Nominatim | Variable data quality in Israel, no SLA |

---

## 8. PUSH NOTIFICATIONS

### Expo Push Notifications (Free, Unlimited)

- **Completely free** with no monthly message limit
- Rate limit: 600 notifications/second per project, 100 per batch
- At-least-once delivery guarantee
- Handles iOS (APNs) + Android (FCM) through single API
- Zero additional setup beyond Expo SDK

### Notification Types

| Notification | Trigger | Priority |
|-------------|---------|:---:|
| Booking request received (nanny) | Family sends request | High |
| Booking accepted (family) | Nanny accepts | High |
| Booking confirmed (both) | Family confirms | High |
| New message | In-app message received | Medium |
| Booking reminder (24hr) | 24 hours before session | Medium |
| Booking reminder (2hr) | 2 hours before session | High |
| Review prompt | 1 hour after session end | Low |
| Emergency alert (admin) | Nanny presses emergency button | Critical |
| Cancellation (affected party) | Other party cancels | High |
| Emergency replacement suggestions | Nanny cancels <24hr | High |

### v2 Upgrade Path

If scheduling, analytics, or marketing segmentation needed: migrate to **OneSignal** (free tier: unlimited mobile push) or **FCM direct**. But Expo Push is sufficient for v1-v2.

---

## 9. REAL-TIME MESSAGING

### Supabase Realtime

- Client subscribes to `messages` table where `receiver_id = current_user_id`
- New messages appear instantly without polling
- Supabase RLS ensures users can only read their own messages
- Latency: <100ms

### Capacity

| Plan | Peak Connections | Messages/Month | Cost |
|------|:---:|:---:|:---:|
| Free | 200 | 2M | $0 |
| Pro | 500 | 5M | $25/mo |
| Overage | +$10/1,000 connections | +$2.50/1M messages | — |

At launch (50 nannies, 20 families): Free tier is sufficient. Move to Pro when approaching 200 concurrent connections (~Month 2-3).

### Why NOT Alternatives

| Alternative | Why Not |
|-------------|---------|
| Stream Chat | Free under $10K revenue, then **$499/mo**. Overkill for 1:1 messaging. |
| SendBird | Developer plan: 100 MAU only. Starter: **$1,199/mo**. Way too expensive. |
| Ably | 6M free msgs/mo — good but adds another vendor when Supabase Realtime is already in stack. |
| Pusher | 200 free connections — similar to Supabase free tier with more complexity. |

**Build custom 1:1 messaging on Supabase Realtime.** The messaging feature is simple (text-only, 1:1) and doesn't justify a $500+/mo chat SDK.

---

## 10. CLOUD INFRASTRUCTURE

### AWS il-central-1 (Tel Aviv)

- **3 Availability Zones**, growing service catalog
- All core services available: Lambda, RDS, S3, ECS, DynamoDB, EC2 (M7i instances added Feb 2026)
- Pricing: ~5-6% premium over Ireland, comparable to Frankfurt
- **AWS Activate Founders**: $1,000 free credits for bootstrapped founders

### Cloud Providers Comparison (Israel Regions)

| Provider | Israel Region | Since | AZs |
|----------|:---:|:---:|:---:|
| **AWS** | il-central-1 (Tel Aviv) | Aug 2023 | 3 |
| **GCP** | me-west1 (Tel Aviv) | Oct 2022 | 3 |
| **Azure** | Israel Central (Modi'in) | 2023 | 3 |

**All three** have Israel regions. AWS wins because Supabase runs exclusively on AWS — deploying backend on same cloud reduces cross-network latency.

### Architecture

```
┌─────────────────────────────────────────────────┐
│                  AWS il-central-1                 │
│                                                   │
│   ┌──────────────┐     ┌──────────────────────┐  │
│   │  ECS Fargate  │     │  Supabase (Frankfurt) │  │
│   │  NestJS API   │────▶│  PostgreSQL + PostGIS  │  │
│   │  Fastify v5   │     │  Auth (Phone OTP)      │  │
│   └──────────────┘     │  Realtime (WebSocket)   │  │
│          │              │  Storage (photos, docs)  │  │
│          │              └──────────────────────┘  │
│          │                                        │
│   ┌──────────────┐     ┌──────────────────────┐  │
│   │  CloudFront   │     │  S3                    │  │
│   │  CDN + Edge   │     │  Static assets         │  │
│   └──────────────┘     └──────────────────────┘  │
│                                                   │
└─────────────────────────────────────────────────┘

         ┌──────────────────────────┐
         │  External Services        │
         │  ├── Didit (ID verify)    │
         │  ├── Google Maps (Routes) │
         │  ├── Expo Push            │
         │  ├── PostHog (analytics   │
         │  │   + errors)            │
         │  └── Morning (invoicing)  │
         └──────────────────────────┘
```

**Note:** Supabase managed hosting is in Frankfurt (eu-central-1), adding ~50-80ms latency to Israel. This is acceptable. The NestJS backend runs on AWS il-central-1 for lowest latency to Israeli users. Supabase is accessed server-side (backend→Supabase) and client-side (Realtime WebSocket).

---

## 11. DEVOPS & MONITORING

### Zero-Cost Monitoring Stack

| Tool | Purpose | Free Tier |
|------|---------|-----------|
| **PostHog** | Product analytics, session replay, feature flags, error tracking (100K exceptions/mo) | 1M events/mo, 5K replays/mo, 1M flag requests/mo, 100K exceptions/mo |
| **UptimeRobot** | Uptime monitoring | 50 monitors, 5-min intervals |
| **AWS CloudWatch** | Infrastructure logging | Included with AWS |
| **Total** | | **$0/mo** |

**Note:** PostHog replaces Sentry — 100K free exceptions/mo vs Sentry's 5K. One fewer vendor to manage.

### Why PostHog Over Mixpanel

| Criteria | PostHog | Mixpanel |
|----------|---------|---------|
| Free events/mo | **1M** | 1M (but event-based pricing since Feb 2025) |
| Session replay | **5K/mo free** | Not included |
| Feature flags | **1M requests/mo free** | Not included |
| Error tracking | **100K exceptions/mo free** (replaces Sentry) | Not included |
| Seats | **Unlimited** | Limited |
| Self-hostable | Yes | No |

PostHog replaces 3-4 separate tools. For a solo founder, this consolidation is critical.

### CI/CD: GitHub Actions

- Free: **2,000 min/mo** for private repos (unchanged)
- January 2026: up to 39% price drop on hosted runners
- March 2026: self-hosted runners now consume free minutes (new)
- Public repos: unlimited free minutes

### Git Workflow

Solo founder — simple trunk-based development:
- `main` — production
- `feature/*` — feature branches, merged via PR
- Direct commits to `main` only for: docs, memory files, config updates

---

## 12. COST MODEL

### Monthly Infrastructure Cost

| Phase | Item | Cost/mo |
|-------|------|:---:|
| **Pre-launch** | Supabase Free | $0 |
| | AWS (minimal EC2/ECS) | ~$15-25 |
| | Google Maps | $0 |
| | Didit (50 nannies — within free tier) | $0 |
| | PostHog Free (analytics + errors) | $0 |
| | **Total** | **~$15-25/mo** |
| **Launch (Mo 0-3)** | Supabase Pro | $25 |
| | AWS ECS Fargate | ~$30-50 |
| | Google Maps | $0-10 |
| | Didit (under 500/mo free tier) | $0 |
| | Expo Push | $0 |
| | PostHog Free (analytics + errors) | $0 |
| | Morning invoicing | NIS 45 |
| | **Total** | **~$67-97/mo (~NIS 250-360)** |
| **Traction (Mo 3-6)** | Supabase Pro | $25 |
| | AWS | ~$50-100 |
| | Google Maps | $10-25 |
| | Didit (under 500/mo free tier) | $0 |
| | PayMe processing | Variable |
| | Morning invoicing | NIS 45 |
| | **Total** | **~$97-162/mo (~NIS 360-600)** |

### One-Time Costs

| Item | Cost |
|------|:---:|
| Apple Developer Program ($99/yr) | NIS 370 |
| Google Play Developer ($25 one-time) | NIS 90 |
| Domain (emuni.co.il) | ~NIS 50/yr |
| Didit pre-launch (50 nannies) | $0 (free tier) |
| **Total one-time** | **~NIS 510** |

**vs PRD v1.1 estimate of NIS 1,500-2,500:** The Technical PRD v1.1 shows significantly lower costs because Didit's free tier eliminates ID verification costs at launch scale, PostHog replaces Sentry (one fewer vendor), and the monitoring stack is $0.

---

## 13. PRD v1.2 DELTA

Items in the main PRD (v1.1 → v1.2) that need updating based on resolved technical decisions:

| PRD Section | Current (v1.1) | Should Be (v1.2) |
|-------------|---------|-----------|
| 5.1 Stack: ID Verification | AU10TIX | **Didit** (500 free/mo, $0.30/check after, Expo plugin) + **Shufti Pro** fallback. Veriff disqualified (no TZ). |
| 5.1 Stack: ORM | (not specified) | **Drizzle** (native PostGIS, no code gen, 7.4KB bundle) |
| 5.1 Stack: Analytics | Mixpanel (1M events) | **PostHog** (1M events + replay + flags + errors) |
| 5.1 Stack: Errors | (not specified) | **PostHog error tracking** (100K exceptions/mo — Sentry dropped) |
| 5.1 Stack: Payments v1 | Manual Bit invoicing | **Manual Bit + Morning (Green Invoice)** NIS 45/mo Best plan |
| 2.3 Background Verification Budget | NIS 8-15/nanny (AU10TIX) | **$0/nanny** (Didit 500 free/mo) |
| 2.3 Budget table | NIS 800-1,500 for 100 nannies | **$0 for 100 nannies** (within Didit free tier) |
| 5.1 Node.js | (not specified) | **Node.js 24 LTS** |
| 9.2 Canonical: Background check cost | NIS 8-15/nanny | **$0/nanny** (Didit free tier) |
| 9.2 Canonical: Pre-launch one-time | NIS 1,500-2,500 | **~NIS 510** (app stores NIS 460 + domain ~NIS 50) |
| 9.2 Canonical: Monthly infra | (not specified) | **~NIS 250-360/mo** at launch |

---

## 14. RESOLVED DECISIONS

All 6 open decisions from v1.0 have been resolved (March 8, 2026):

| # | Decision | Resolution | Notes |
|---|----------|-----------|-------|
| 1 | **Supabase hosting** | **RESOLVED: Managed Frankfurt** | Solo founder can't maintain self-hosted Supabase. ~50-80ms latency is acceptable. No Israel data residency mandate. |
| 2 | **ID Verification** | **RESOLVED: Didit** (primary) + **Shufti Pro** (fallback) | Veriff DISQUALIFIED — does not support Teudat Zehut. Didit: 500 free/mo, $0.30/check after, Expo plugin, confirmed TZ. Shufti Pro: $0.20/check, confirmed TZ. |
| 3 | **ORM** | **RESOLVED: Drizzle** | PostGIS support was decisive — Prisma requires raw SQL for PostGIS queries. Drizzle: native PostGIS, no code gen, 7.4KB bundle. |
| 4 | **Invoicing** | **RESOLVED: Morning Best plan (NIS 45/mo)** | From Day 1. Automates invoicing + SHAAM compliance via API. |
| 5 | **Analytics/Errors** | **RESOLVED: PostHog** (replaces Mixpanel + Sentry) | 1M events + session replay + feature flags + 100K exceptions/mo. Sentry dropped (only 5K errors/mo free). Replaces 5-7 separate tools. |
| 6 | **Monorepo** | **RESOLVED: Turborepo + pnpm workspaces** | Shared Zod schemas between frontend/backend, single CI pipeline, caching. |

---

*Research compiled from 7 parallel agents, 190+ web searches, March 7-8, 2026. All version numbers and pricing verified against live web sources. See individual research files for source URLs: `BACKEND_STACK_RESEARCH_2026.md`, `IDENTITY_VERIFICATION_SERVICES_2026.md`, `ISRAEL_PAYMENT_PROCESSING_RESEARCH_2026.md`, `CLOUD_INFRASTRUCTURE_RESEARCH_2026.md`, `EMUNI_TECH_SERVICES_RESEARCH_2026.md`, `PRISMA_VS_DRIZZLE_COMPARISON_2026.md`, `POSTHOG_VS_MIXPANEL_RESEARCH_2026.md`, `EMUNI_INVOICING_MONOREPO_RESEARCH.md`.*
