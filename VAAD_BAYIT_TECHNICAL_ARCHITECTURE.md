# Vaad Bayit Management Platform — Technical Architecture (MVP)

**Date: March 2026 | Budget: NIS 130K-200K | Timeline: 6-8 weeks with 2 developers**
**Revenue Model: Transaction-fee-first (1.5% on payments processed) — platform is free for buildings**

---

## Table of Contents

- [Competitive Context](#competitive-context)
- [MVP Feature Set](#mvp-feature-set)
- [Technology Stack](#technology-stack)
- [Architecture Diagram](#architecture-diagram)
- [Database Schema](#database-schema)
- [Security Considerations](#security-considerations)
- [Revenue Model & Fee Architecture](#revenue-model--fee-architecture)
- [Cost Estimates](#cost-estimates)
- [Monorepo Structure](#monorepo-structure)
- [Key Risks and Mitigations](#key-risks-and-mitigations)

---

## Competitive Context

| Competitor | Focus | Weakness / Opportunity |
|---|---|---|
| **Bllink** ([bllink.co](https://www.bllink.co/en/)) | Financial collection for buildings | Narrow — payments only, no maintenance/communication |
| **Binayati** ([binayati.com](https://www.binayati.com/)) | Full property management suite | Targets professional management companies, not volunteer vaad bayit |
| **RunMaxi** | AI-powered property management | Enterprise-oriented, overkill for 8-40 unit buildings |
| **Darimpo** | Maintenance + communication | Limited financial features |
| **vaadbayit.co.il** | Basic vaad bayit management | Dated technology stack |

**Your differentiation**: A **completely free**, self-service platform purpose-built for volunteer vaad bayit committees in small/medium buildings (8-40 units), combining payments + maintenance + communication + documents in a single modern interface with Hebrew-first UX. Revenue comes from a transparent 1.5% fee on payments processed through the platform — no subscription, no monthly fees. Buildings effectively pay NIS ~108/month (vs. Ding/OXS at NIS 200/month) while the platform appears free.

---

## MVP Feature Set

### Phase 1: Must-Have (Weeks 1-6) — 60 person-days total

| # | Feature | Description | Effort (person-days) | Priority |
|---|---------|-------------|---------------------|----------|
| 1 | **Building & Resident Onboarding** | Create building, add units, invite residents (SMS/WhatsApp link), role assignment (vaad member, treasurer, resident) | 5 | P0 |
| 2 | **Monthly Payment Collection** | Standing orders via credit card tokenization, one-time payments, Bit integration, payment reminders, receipt generation | 12 | P0 |
| 3 | **Financial Dashboard** | Income/expense tracking, balance per building, transparency reports viewable by all residents, monthly/annual summaries | 8 | P0 |
| 4 | **Maintenance Request System** | Submit request (with photo), categorize (plumbing, electrical, elevator, cleaning), track status, assign to vendor, resident can view progress | 8 | P0 |
| 5 | **Announcements & Notifications** | Committee posts announcements, push notifications to residents, email fallback, read receipts | 6 | P0 |
| 6 | **Document Storage** | Upload meeting minutes, financial reports, contracts, insurance docs; organized by category and date | 5 | P1 |
| 7 | **Expense Management** | Record expenses, attach invoices/receipts, categorize, approve workflow for committee | 6 | P1 |
| 8 | **Resident Directory** | Unit-to-resident mapping, contact info (opt-in), move-in/move-out tracking | 3 | P1 |
| 9 | **Platform Revenue Dashboard** | Internal admin: track platform fee revenue per building, payment volume analytics, fee payout reports, Meshulam settlement reconciliation | 4 | P0 |
| 10 | **Hebrew RTL & Localization** | Full RTL layout, Hebrew date formatting, shekel currency, Israeli phone validation | 3 | P0 |

**Total: 60 person-days = 2 developers x 6 weeks**

### Phase 2: v1.1 (Weeks 7-12) — Revenue Expansion

| Feature | Effort | Notes |
|---------|--------|-------|
| **Insurance referral integration** | 6 days | Partner with licensed agent; in-app quotes for bituach binyan/mashutaf. Revenue: 10-15% commission on premiums. |
| **Payment installment plans** | 4 days | Split large one-time charges (repairs, renovations) into 3-6 credit card payments via Meshulam. Increases platform payment volume. |
| Resident voting system (building decisions) | 6 days | Requires careful UX for quorum rules |
| Debt tracking & payment plans | 4 days | Sensitive — needs legal review |
| WhatsApp bot integration | 5 days | High engagement potential; payment links via WhatsApp |
| Multi-building management (for professional managers) | 5 days | Opens new market segment |

### Phase 3: v2.0 (Months 6-12) — Marketplace & Scale

| Feature | Effort | Notes |
|---------|--------|-------|
| **Service provider marketplace** | 10 days | Plumbers, electricians, cleaners pay NIS 100-200/mo for listing + leads. Requires 150+ buildings for viable density. |
| **Premium tier for property managers** | 5 days | NIS 99-199/mo for multi-building dashboard, advanced analytics, API. Additive revenue, not core model. |
| AI expense categorization (from receipt photos) | 5 days | |
| Integration with Israeli municipal systems | 8 days | |

### Phase 4: v3.0 — Future

- Predictive maintenance alerts
- Building insurance comparison marketplace
- Elevator/generator maintenance scheduling with IoT
- Solar panel group-buy coordination

---

## Technology Stack

### Frontend: Next.js 15 (Web) + Expo / React Native (Mobile)

**Decision: Turborepo monorepo with Next.js for web + Expo for iOS/Android**

| Option | Verdict | Reasoning |
|--------|---------|-----------|
| **Next.js + Expo (chosen)** | Best fit | Shared TypeScript types, business logic, and API client. Next.js for responsive web dashboard (committee members often use desktop). Expo for resident mobile app (maintenance requests, notifications). [Expo docs confirm monorepo support since SDK 52](https://docs.expo.dev/guides/monorepos/). |
| Flutter | Rejected | Dart ecosystem is smaller. No code sharing with web. Harder to hire in Israel. |
| React Native Web | Rejected | Adds complexity for the financial dashboard — Next.js SSR and built-in routing is more mature for web. |

**RTL Support**: Next.js has native `dir="rtl"` support. Tailwind CSS v4 has built-in RTL utilities (`rtl:` variant). Expo supports RTL via `I18nManager.forceRTL()`.

**UI Library**: [Shadcn/ui](https://ui.shadcn.com/) for web (with RTL patches), [NativeWind](https://www.nativewind.dev/) for cross-platform components.

### Backend: Supabase (PostgreSQL + Auth + Realtime + Edge Functions + Storage)

**Decision: Supabase as the primary backend platform**

| Option | Verdict | Reasoning |
|--------|---------|-----------|
| **Supabase (chosen)** | Best fit for MVP | Bundles Postgres, auth (100K MAU on Pro), realtime subscriptions, edge functions, file storage, and Row Level Security at [$25/month Pro plan](https://supabase.com/pricing). Direct client SDK for both Next.js and React Native. RLS eliminates separate authorization layer. |
| Node.js/Express custom | Rejected for MVP | Would require building auth, file upload, realtime, and API separately. Estimated +15 person-days. Consider for v2.0. |
| Python/Django | Rejected | Slower iteration for real-time features. No TypeScript code sharing. |

**Supabase Pro plan includes** ([verified 2026 pricing](https://uibakery.io/blog/supabase-pricing)):
- 8 GB database storage
- 100 GB file storage
- 100K monthly active users
- 5M realtime messages
- 2M edge function invocations

This is sufficient for 300 buildings x ~25 residents = ~7,500 users.

### Database: PostgreSQL (via Supabase)

**Multi-tenancy approach: Shared database, shared schema, RLS-enforced isolation**

- All buildings share one database and one set of tables
- Every table has a `building_id` column
- RLS policies ensure residents can only see their own building's data
- Most cost-effective approach for 300 buildings

### Payments: Meshulam (Grow) as Primary + Bit via PayMe

| Gateway | Verdict | Reasoning |
|---------|---------|-----------|
| **Meshulam/Grow (chosen)** | Primary | [Supports credit cards + Bit](https://apps.duda.co/apps/grow-payments) in a single integration. [Sandbox available](https://sandbox.meshulam.co.il). [API docs at doc.meshulam.co.il](https://doc.meshulam.co.il/). Supports recurring/tokenized payments. |
| Cardcom | Backup | [Good API (v11)](https://www.npmjs.com/package/@tsdiapi/cardcom) with tokenization. Consider as fallback. |
| Tranzila | Rejected | API documentation quality lower. More suited to e-commerce. |
| PayMe | Alternative | [Supports Bit natively](https://help.payme.io/hc/en-us/articles/360013964399-Alternative-Payment-Method-Bit). |

**Bit limits**: [NIS 5,000/transaction and NIS 20,000/month](https://developer.bitpay.co.il/docs). For typical vaad bayit fees (NIS 100-300/unit), adequate per resident. Credit card remains primary; Bit is convenience.

**PCI compliance**: Meshulam handles all PCI DSS via hosted payment page / tokenization. Your platform never touches raw card numbers (SAQ-A level).

**Platform fee architecture**: Meshulam processes the full payment amount. The 1.5% platform fee is calculated and tracked internally. The building receives the full amount from Meshulam; the platform invoices the building for the accumulated fee monthly (or deducts from a settlement account). See [Revenue Model & Fee Architecture](#revenue-model--fee-architecture) for details.

### Authentication: Supabase Auth

| Option | Verdict | Reasoning |
|--------|---------|-----------|
| **Supabase Auth (chosen)** | Best fit | Bundled at no extra cost. Supports phone OTP (critical for Israeli users). 100K MAU on Pro. Integrates with RLS. |
| Clerk | Rejected | [$0.02/MAU after 10K](https://clerk.com/articles/user-management-platform-comparison-react-clerk-auth0-firebase). Unnecessary vendor dependency. |
| Firebase Auth | Rejected | Split-brain architecture — auth in Firebase, data in Supabase. |
| Auth0 | Rejected | [$0.07/MAU](https://leonstaff.com/blogs/clerk-vs-auth0-identity-crisis/) — overkill enterprise pricing. |

**Auth flow**: Phone number + OTP (primary), email + password (secondary). No social login needed for this market.

### Realtime & Notifications

- **In-app**: Supabase Realtime (WebSockets, 5M messages/month on Pro)
- **Mobile push**: [Expo Push Notification service (free)](https://docs.expo.dev/push-notifications/overview/)
- **Email**: Resend ($0 for 100 emails/day, $20/month for 50K)

### File Storage

- **MVP (0-300 buildings)**: Supabase Storage (100 GB on Pro plan). Documents ~10-30 GB.
- **Scale (300+)**: Migrate to [Cloudflare R2 at $0.015/GB/month with zero egress](https://www.cloudflare.com/pg-cloudflare-r2-vs-aws-s3/).

### Hosting

| Component | Host | Cost |
|-----------|------|------|
| Next.js web app | **Vercel** | $20/month (Pro) |
| Expo mobile app | App Store / Google Play | $99/year + $25 one-time |
| Backend (DB, Auth, Storage, Realtime) | **Supabase Cloud** | $25/month (Pro) |
| Edge Functions | Supabase Edge Functions | Included in Pro |
| Email | Resend | $0-20/month |

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           CLIENT LAYER                                  │
│                                                                         │
│  ┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐  │
│  │   Next.js Web    │    │  Expo iOS App    │    │ Expo Android App │  │
│  │   (Dashboard)    │    │  (Resident App)  │    │ (Resident App)   │  │
│  │                  │    │                  │    │                  │  │
│  │  - RTL/Hebrew    │    │  - Push Notifs   │    │  - Push Notifs   │  │
│  │  - Financial     │    │  - Maintenance   │    │  - Maintenance   │  │
│  │    Reports       │    │    Requests      │    │    Requests      │  │
│  │  - Admin Panel   │    │  - Payments      │    │  - Payments      │  │
│  └────────┬─────────┘    └────────┬─────────┘    └────────┬─────────┘  │
│           │                       │                       │            │
└───────────┼───────────────────────┼───────────────────────┼────────────┘
            │                       │                       │
            └───────────────────────┼───────────────────────┘
                                    │
                          HTTPS / WSS
                                    │
┌───────────────────────────────────┼────────────────────────────────────┐
│                        SUPABASE PLATFORM                               │
│                                    │                                    │
│  ┌─────────────────────────────────▼──────────────────────────────┐    │
│  │                     Supabase API Gateway                       │    │
│  │              (PostgREST + GoTrue + Realtime)                   │    │
│  └──────┬──────────────┬──────────────┬──────────────┬────────────┘    │
│         │              │              │              │                  │
│  ┌──────▼──────┐ ┌─────▼─────┐ ┌─────▼─────┐ ┌─────▼─────┐          │
│  │  PostgreSQL │ │ Supabase  │ │ Realtime  │ │ Supabase  │          │
│  │  Database   │ │   Auth    │ │ (WebSocket│ │  Storage  │          │
│  │             │ │           │ │  Server)  │ │  (S3)     │          │
│  │ - RLS       │ │ - Phone   │ │           │ │           │          │
│  │   Policies  │ │   OTP     │ │ - Announce│ │ - Docs    │          │
│  │ - All       │ │ - Email   │ │   ments   │ │ - Photos  │          │
│  │   tables    │ │ - JWT     │ │ - Status  │ │ - Reports │          │
│  │ - Triggers  │ │ - Roles   │ │   Updates │ │ - Invoices│          │
│  └──────┬──────┘ └───────────┘ └───────────┘ └───────────┘          │
│         │                                                             │
│  ┌──────▼───────────────────────────────────────────────────────┐    │
│  │                   Supabase Edge Functions                     │    │
│  │  (Deno runtime — serverless)                                  │    │
│  │                                                               │    │
│  │  ┌─────────────┐ ┌──────────────┐ ┌───────────────────────┐  │    │
│  │  │  Payment    │ │ Notification │ │  Revenue & Reports    │  │    │
│  │  │  Webhooks   │ │   Sender     │ │                       │  │    │
│  │  │             │ │              │ │                       │  │    │
│  │  │ - Meshulam  │ │ - Expo Push  │ │ - Platform fee calc   │  │    │
│  │  │   callback  │ │ - Resend     │ │ - Monthly invoicing   │  │    │
│  │  │ - Update    │ │   email      │ │ - Financial summaries │  │    │
│  │  │   payment   │ │ - WhatsApp   │ │ - Transparency report │  │    │
│  │  │   status    │ │   pay links  │ │ - Revenue dashboard   │  │    │
│  │  └─────────────┘ └──────────────┘ └───────────────────────┘  │    │
│  └───────────────────────────────────────────────────────────────┘    │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
            │                                    │
            ▼                                    ▼
┌───────────────────────┐          ┌──────────────────────────┐
│   MESHULAM GATEWAY    │          │    EXTERNAL SERVICES     │
│                       │          │                          │
│  - Hosted Payment     │          │  - Expo Push API (Free)  │
│    Page (iframe)      │          │  - Resend Email ($0-20)  │
│  - Credit Card        │          │  - SMS Provider (OTP)    │
│    Processing         │          │                          │
│  - Bit Payments       │          └──────────────────────────┘
│  - Token Storage      │
│    (PCI compliant)    │
│  - Recurring Billing  │
│                       │
└───────────────────────┘
```

### Payment Flow (with Platform Fee Tracking)

```
Resident opens payment page (via app, WhatsApp link, or web)
         │
         ▼
┌─────────────────────┐
│ App calls Supabase   │
│ Edge Function:       │
│ "create-payment"     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐     ┌─────────────────────┐
│ Edge Function calls  │────▶│ Meshulam API:       │
│ Meshulam API to      │     │ createPaymentProcess│
│ generate payment URL │     │ Returns: paymentURL │
└──────────────────────┘     └──────────┬──────────┘
                                        │
                                        ▼
                             ┌─────────────────────┐
                             │ Resident redirected  │
                             │ to Meshulam hosted   │
                             │ payment page         │
                             │ (credit card or Bit) │
                             └──────────┬──────────┘
                                        │
                              Payment completes
                                        │
                                        ▼
┌─────────────────────┐     ┌─────────────────────┐
│ Supabase Edge        │◀───│ Meshulam webhook     │
│ Function:            │     │ POST callback with   │
│ "payment-webhook"    │     │ payment status       │
└──────────┬──────────┘     └─────────────────────┘
           │
           ▼
┌──────────────────────────────────────────┐
│ 1. Update payments table (status=done)   │
│ 2. Calculate platform fee:               │
│    fee = amount × building.fee_pct/100   │
│ 3. INSERT into platform_fees             │
│    (status='accrued')                    │
│ 4. Generate receipt for resident         │
│ 5. Send push notif + email              │
└──────────────────────────────────────────┘
```

### Monthly Fee Collection Flow (Cron — 1st of each month)

```
Cron: "generate-monthly-invoice" runs on 1st of month
         │
         ▼
┌──────────────────────────────────────┐
│ For each building with accrued fees: │
│  1. SUM(platform_fees) for month     │
│  2. CREATE platform_invoice          │
│  3. Mark fees as 'invoiced'          │
│  4. Send invoice to treasurer email  │
│  5. (Optional: auto-charge if card   │
│     on file for platform fees)       │
└──────────────────────────────────────┘
```

### Notification Flow

```
Database event (INSERT/UPDATE)
         │
         ▼
PostgreSQL Trigger → pg_notify()
         │
         ▼
Supabase Edge Function (Database Webhook)
         │
    ┌────┴─────┐
    ▼          ▼
Expo Push    Resend Email
(mobile)     (digest)
```

---

## Database Schema

```sql
-- =============================================================
-- CORE TABLES
-- =============================================================

CREATE TABLE buildings (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name            TEXT NOT NULL,                    -- "רחוב הרצל 15"
    address         TEXT NOT NULL,
    city            TEXT NOT NULL,
    total_units     INTEGER NOT NULL CHECK (total_units BETWEEN 2 AND 200),
    monthly_fee     NUMERIC(10,2) NOT NULL,           -- Default monthly fee in NIS
    bank_account    JSONB,                            -- {bank, branch, account}
    settings        JSONB DEFAULT '{}',
    platform_fee_pct NUMERIC(4,2) DEFAULT 1.50,      -- Platform fee % (default 1.5%)
    onboarding_status TEXT DEFAULT 'active'
                    CHECK (onboarding_status IN ('pending', 'active', 'suspended')),
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE units (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id) ON DELETE CASCADE,
    unit_number     TEXT NOT NULL,                    -- "4א" (supports Hebrew)
    floor           INTEGER,
    size_sqm        NUMERIC(8,2),
    monthly_fee_override NUMERIC(10,2),              -- NULL = use building default
    is_commercial   BOOLEAN DEFAULT false,
    created_at      TIMESTAMPTZ DEFAULT now(),
    UNIQUE(building_id, unit_number)
);

CREATE TABLE residents (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    auth_user_id    UUID NOT NULL REFERENCES auth.users(id),
    building_id     UUID NOT NULL REFERENCES buildings(id) ON DELETE CASCADE,
    unit_id         UUID REFERENCES units(id),
    full_name       TEXT NOT NULL,
    phone           TEXT NOT NULL,                    -- 05X-XXXXXXX
    email           TEXT,
    role            TEXT NOT NULL DEFAULT 'resident'
                    CHECK (role IN ('resident', 'committee_member', 'treasurer', 'chair')),
    is_owner        BOOLEAN DEFAULT true,
    move_in_date    DATE,
    move_out_date   DATE,
    expo_push_token TEXT,
    notification_preferences JSONB DEFAULT '{"push": true, "email": true, "sms": false}',
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

-- =============================================================
-- FINANCIAL TABLES
-- =============================================================

CREATE TABLE payments (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    unit_id         UUID NOT NULL REFERENCES units(id),
    resident_id     UUID REFERENCES residents(id),
    amount          NUMERIC(10,2) NOT NULL,
    currency        TEXT DEFAULT 'ILS',
    payment_method  TEXT NOT NULL
                    CHECK (payment_method IN ('credit_card', 'bit', 'bank_transfer', 'cash', 'check')),
    status          TEXT NOT NULL DEFAULT 'pending'
                    CHECK (status IN ('pending', 'processing', 'completed', 'failed', 'refunded')),
    period_month    INTEGER NOT NULL CHECK (period_month BETWEEN 1 AND 12),
    period_year     INTEGER NOT NULL,
    meshulam_transaction_id TEXT,
    meshulam_token  TEXT,
    receipt_url     TEXT,
    paid_at         TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now(),
    UNIQUE(unit_id, period_month, period_year)
);

CREATE TABLE standing_orders (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    unit_id         UUID NOT NULL REFERENCES units(id),
    resident_id     UUID NOT NULL REFERENCES residents(id),
    payment_method  TEXT NOT NULL CHECK (payment_method IN ('credit_card', 'bit')),
    meshulam_token  TEXT NOT NULL,
    amount          NUMERIC(10,2) NOT NULL,
    day_of_month    INTEGER DEFAULT 1 CHECK (day_of_month BETWEEN 1 AND 28),
    is_active       BOOLEAN DEFAULT true,
    last_charged_at TIMESTAMPTZ,
    next_charge_at  TIMESTAMPTZ,
    failure_count   INTEGER DEFAULT 0,
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE expenses (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    category        TEXT NOT NULL
                    CHECK (category IN (
                        'cleaning', 'elevator', 'plumbing', 'electrical',
                        'gardening', 'insurance', 'legal', 'painting',
                        'water', 'electricity_common', 'pest_control',
                        'security', 'repairs_general', 'other'
                    )),
    description     TEXT NOT NULL,
    amount          NUMERIC(10,2) NOT NULL,
    vendor_name     TEXT,
    vendor_phone    TEXT,
    invoice_url     TEXT,
    receipt_url     TEXT,
    approved_by     UUID REFERENCES residents(id),
    expense_date    DATE NOT NULL,
    status          TEXT DEFAULT 'pending'
                    CHECK (status IN ('pending', 'approved', 'rejected', 'paid')),
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

-- =============================================================
-- MAINTENANCE TABLES
-- =============================================================

CREATE TABLE maintenance_requests (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    unit_id         UUID REFERENCES units(id),        -- NULL = common area
    reported_by     UUID NOT NULL REFERENCES residents(id),
    category        TEXT NOT NULL
                    CHECK (category IN (
                        'plumbing', 'electrical', 'elevator', 'cleaning',
                        'structural', 'pest_control', 'lock_intercom',
                        'water_heater', 'roof', 'parking', 'garden', 'other'
                    )),
    title           TEXT NOT NULL,
    description     TEXT NOT NULL,
    urgency         TEXT DEFAULT 'normal'
                    CHECK (urgency IN ('low', 'normal', 'high', 'emergency')),
    status          TEXT DEFAULT 'open'
                    CHECK (status IN ('open', 'in_review', 'assigned', 'in_progress',
                                      'waiting_parts', 'completed', 'closed', 'rejected')),
    assigned_vendor TEXT,
    vendor_phone    TEXT,
    estimated_cost  NUMERIC(10,2),
    actual_cost     NUMERIC(10,2),
    resolution_notes TEXT,
    completed_at    TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE maintenance_photos (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    request_id      UUID NOT NULL REFERENCES maintenance_requests(id) ON DELETE CASCADE,
    storage_path    TEXT NOT NULL,
    uploaded_by     UUID NOT NULL REFERENCES residents(id),
    created_at      TIMESTAMPTZ DEFAULT now()
);

-- =============================================================
-- COMMUNICATION TABLES
-- =============================================================

CREATE TABLE announcements (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    author_id       UUID NOT NULL REFERENCES residents(id),
    title           TEXT NOT NULL,
    body            TEXT NOT NULL,
    priority        TEXT DEFAULT 'normal'
                    CHECK (priority IN ('low', 'normal', 'high', 'urgent')),
    attachment_urls  JSONB DEFAULT '[]',
    published_at    TIMESTAMPTZ DEFAULT now(),
    expires_at      TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE announcement_reads (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    announcement_id UUID NOT NULL REFERENCES announcements(id) ON DELETE CASCADE,
    resident_id     UUID NOT NULL REFERENCES residents(id),
    read_at         TIMESTAMPTZ DEFAULT now(),
    UNIQUE(announcement_id, resident_id)
);

-- =============================================================
-- DOCUMENT STORAGE
-- =============================================================

CREATE TABLE documents (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    category        TEXT NOT NULL
                    CHECK (category IN (
                        'meeting_minutes', 'financial_report', 'contract',
                        'insurance', 'permit', 'legal', 'other'
                    )),
    title           TEXT NOT NULL,
    description     TEXT,
    storage_path    TEXT NOT NULL,
    file_size_bytes BIGINT,
    mime_type       TEXT,
    uploaded_by     UUID NOT NULL REFERENCES residents(id),
    created_at      TIMESTAMPTZ DEFAULT now()
);

-- =============================================================
-- PLATFORM REVENUE TRACKING
-- =============================================================

-- Tracks the platform's 1.5% fee on each payment processed
CREATE TABLE platform_fees (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    payment_id      UUID NOT NULL REFERENCES payments(id),
    payment_amount  NUMERIC(10,2) NOT NULL,           -- Original payment amount
    fee_pct         NUMERIC(4,2) NOT NULL,             -- Fee % at time of payment (e.g., 1.50)
    fee_amount      NUMERIC(10,2) NOT NULL,            -- Calculated fee in NIS
    status          TEXT DEFAULT 'accrued'
                    CHECK (status IN ('accrued', 'invoiced', 'collected', 'waived')),
    invoice_id      UUID REFERENCES platform_invoices(id),
    created_at      TIMESTAMPTZ DEFAULT now()
);

-- Monthly invoice to building for accumulated platform fees
CREATE TABLE platform_invoices (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    period_month    INTEGER NOT NULL CHECK (period_month BETWEEN 1 AND 12),
    period_year     INTEGER NOT NULL,
    total_payment_volume NUMERIC(12,2) NOT NULL,       -- Total payments processed that month
    fee_pct         NUMERIC(4,2) NOT NULL,             -- Fee % applied
    total_fee       NUMERIC(10,2) NOT NULL,            -- Total fee owed
    status          TEXT DEFAULT 'draft'
                    CHECK (status IN ('draft', 'sent', 'paid', 'overdue', 'waived')),
    issued_at       TIMESTAMPTZ,
    paid_at         TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now(),
    UNIQUE(building_id, period_month, period_year)
);

-- Phase 2: Insurance referral tracking
CREATE TABLE insurance_referrals (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    partner_name    TEXT NOT NULL,                      -- Insurance agent/agency name
    policy_type     TEXT NOT NULL
                    CHECK (policy_type IN ('building', 'shared_areas', 'liability', 'earthquake')),
    annual_premium  NUMERIC(10,2),
    commission_pct  NUMERIC(4,2),                      -- Our referral commission %
    commission_amount NUMERIC(10,2),
    policy_start    DATE,
    policy_end      DATE,
    status          TEXT DEFAULT 'referred'
                    CHECK (status IN ('referred', 'quoted', 'sold', 'renewed', 'cancelled')),
    created_at      TIMESTAMPTZ DEFAULT now(),
    updated_at      TIMESTAMPTZ DEFAULT now()
);

-- =============================================================
-- ROW LEVEL SECURITY
-- =============================================================

ALTER TABLE buildings ENABLE ROW LEVEL SECURITY;
ALTER TABLE units ENABLE ROW LEVEL SECURITY;
ALTER TABLE residents ENABLE ROW LEVEL SECURITY;
ALTER TABLE payments ENABLE ROW LEVEL SECURITY;
ALTER TABLE standing_orders ENABLE ROW LEVEL SECURITY;
ALTER TABLE expenses ENABLE ROW LEVEL SECURITY;
ALTER TABLE maintenance_requests ENABLE ROW LEVEL SECURITY;
ALTER TABLE maintenance_photos ENABLE ROW LEVEL SECURITY;
ALTER TABLE announcements ENABLE ROW LEVEL SECURITY;
ALTER TABLE announcement_reads ENABLE ROW LEVEL SECURITY;
ALTER TABLE documents ENABLE ROW LEVEL SECURITY;
-- Platform revenue tables: NO RLS — accessed only by service_role (admin)
-- platform_fees, platform_invoices, insurance_referrals are internal-only

-- Residents can only see their own building's data
CREATE POLICY "residents_see_own_building" ON residents
    FOR SELECT USING (
        building_id IN (
            SELECT r.building_id FROM residents r
            WHERE r.auth_user_id = auth.uid()
        )
    );

-- Committee members can manage announcements
CREATE POLICY "committee_manage_announcements" ON announcements
    FOR ALL USING (
        building_id IN (
            SELECT r.building_id FROM residents r
            WHERE r.auth_user_id = auth.uid()
        )
    )
    WITH CHECK (
        EXISTS (
            SELECT 1 FROM residents r
            WHERE r.auth_user_id = auth.uid()
              AND r.building_id = announcements.building_id
              AND r.role IN ('committee_member', 'treasurer', 'chair')
        )
    );

-- Residents see own payments, committee sees all
CREATE POLICY "payment_visibility" ON payments
    FOR SELECT USING (
        (unit_id IN (
            SELECT r.unit_id FROM residents r WHERE r.auth_user_id = auth.uid()
        ))
        OR
        (building_id IN (
            SELECT r.building_id FROM residents r
            WHERE r.auth_user_id = auth.uid()
              AND r.role IN ('committee_member', 'treasurer', 'chair')
        ))
    );

-- =============================================================
-- INDEXES
-- =============================================================

CREATE INDEX idx_residents_building ON residents(building_id);
CREATE INDEX idx_residents_auth_user ON residents(auth_user_id);
CREATE INDEX idx_payments_building_period ON payments(building_id, period_year, period_month);
CREATE INDEX idx_payments_unit ON payments(unit_id);
CREATE INDEX idx_payments_status ON payments(status);
CREATE INDEX idx_expenses_building ON expenses(building_id);
CREATE INDEX idx_expenses_category ON expenses(building_id, category);
CREATE INDEX idx_maintenance_building ON maintenance_requests(building_id);
CREATE INDEX idx_maintenance_status ON maintenance_requests(building_id, status);
CREATE INDEX idx_announcements_building ON announcements(building_id);
CREATE INDEX idx_documents_building ON documents(building_id);
CREATE INDEX idx_standing_orders_next ON standing_orders(next_charge_at) WHERE is_active = true;

-- Platform revenue indexes
CREATE INDEX idx_platform_fees_building ON platform_fees(building_id);
CREATE INDEX idx_platform_fees_status ON platform_fees(status);
CREATE INDEX idx_platform_invoices_building ON platform_invoices(building_id);
CREATE INDEX idx_platform_invoices_status ON platform_invoices(status);
CREATE INDEX idx_platform_invoices_period ON platform_invoices(period_year, period_month);
CREATE INDEX idx_insurance_referrals_building ON insurance_referrals(building_id);
```

### Role-Permission Matrix

| Action | Resident | Committee Member | Treasurer | Chair |
|--------|----------|-----------------|-----------|-------|
| View own payments | Yes | Yes | Yes | Yes |
| View all building payments | No | Yes | Yes | Yes |
| Submit maintenance request | Yes | Yes | Yes | Yes |
| Assign vendor to request | No | Yes | Yes | Yes |
| Post announcement | No | Yes | Yes | Yes |
| Record expense | No | No | Yes | Yes |
| Approve expense | No | No | Yes | Yes |
| Upload document | No | Yes | Yes | Yes |
| Manage residents/units | No | No | No | Yes |
| Change building settings | No | No | No | Yes |
| View financial reports | Summary | Full | Full | Full |
| View platform fee invoices | No | No | Yes | Yes |

---

## Security Considerations

### PCI DSS Compliance (SAQ-A — Lowest Scope)

- Platform **never** touches, stores, or processes raw credit card numbers
- All card data flows through Meshulam's hosted payment page
- [PCI DSS v4.0.1 (mandatory since March 2025)](https://paymentnerds.com/blog/pci-dss-updates-how-to-be-pci-dss-compliant-in-2026/) requires monitoring third-party scripts on payment pages
- Use Meshulam's hosted payment page redirect (not iframe) for full isolation
- Annual SAQ-A self-assessment (no external audit required)

### Israeli Privacy Protection Law (Amendment 13)

[Amendment 13 took effect August 14, 2025](https://iapp.org/news/a/israel-marks-a-new-era-in-privacy-law-amendment-13-ushers-in-sweeping-reform/) — Israel's most significant privacy reform in 40 years.

| Requirement | Implementation |
|---|---|
| **Database registration** | Register with Israeli Privacy Protection Authority (PPA) |
| **Purpose limitation** | Collect only data necessary for building management |
| **Data minimization** | No ID numbers required for residents |
| **Security measures** | Encryption at rest (Supabase default), TLS 1.3, access logging, RLS |
| **Breach notification** | [72-hour mandatory notification to PPA](https://iapp.org/news/a/israel-enacts-landmark-data-security-notification-regulations) |
| **Data Subject Rights** | Self-service: view, export, correct, delete personal data |
| **Consent** | Explicit consent during onboarding. Separate consent for marketing. |
| **Cross-border transfer** | Use Supabase EU region (Frankfurt) — covered by EU-Israel adequacy agreement |

### Authentication & Authorization

```
Authentication (Supabase Auth):
  ├── Phone OTP (primary) — Israeli mobile numbers
  ├── Email + Password (secondary)
  └── Magic Link (email-based passwordless)

Authorization (PostgreSQL RLS):
  ├── auth.uid() → residents.auth_user_id → building_id (tenant isolation)
  ├── residents.role → CRUD permissions per table
  └── RLS policies enforce at database level (cannot be bypassed)

Sessions:
  ├── JWT tokens: 1-hour expiry
  ├── Refresh tokens: 7-day expiry
  └── Auto-refresh via Supabase client SDKs
```

### Additional Security

- **Rate limiting**: 5/min payment creation, 3/min OTP requests, 10/min file uploads
- **Input validation**: Zod schemas shared between frontend and edge functions
- **File upload security**: Allowed MIME types only (PDF, JPEG, PNG). Max 10 MB.
- **Audit logging**: All financial operations logged to immutable `audit_log` table

---

## Revenue Model & Fee Architecture

### Core Model: 1.5% Transaction Fee ("Platform is Free")

The platform charges **zero subscription fees**. Revenue comes from a transparent 1.5% fee on payments processed through the platform. This fee is borne by the building fund (not individual residents).

**Why this works:**
- **Zero adoption barrier**: "It's completely free" eliminates the #1 objection
- **Scales with value delivered**: larger buildings pay more, smaller buildings pay less
- **Undercuts all competitors**: effective cost of ~NIS 108/mo vs Ding/OXS at NIS 200/mo
- **No churn from cancellation**: there's nothing to cancel — buildings just use or don't use

### Fee Calculation Example

```
Building: 24 apartments × NIS 300/month = NIS 7,200 monthly collection
Platform fee: NIS 7,200 × 1.5% = NIS 108/month
Meshulam processing: NIS 7,200 × 1.5% + 24 × NIS 1 = NIS 132/month (paid to Meshulam)

Building's total cost: NIS 108 (platform) + NIS 132 (Meshulam) = NIS 240/month
  → Still cheaper than Ding/OXS at NIS 200/month + their own processing fees
  → Platform appears FREE to the building — processing fees are the only visible cost
```

### Fee Collection Mechanism

Two options (configurable per building):

1. **Monthly invoice** (default): Platform fees accrue throughout the month. On the 1st, an invoice is generated and sent to the treasurer. Payment due within 14 days.
2. **Auto-deduct** (opt-in): Building provides a credit card for platform fees. Charged automatically monthly. Requires separate Meshulam token for platform fee collection.

### Revenue Projections (Transaction Fee Only — Phase 1)

| Scale | Monthly Payment Volume | Platform Fee (1.5%) | Meshulam Cost | Net Revenue |
|-------|----------------------|--------------------|--------------|-|
| 50 buildings | NIS 360,000 | NIS 5,400 | ~NIS 6,600 | NIS 5,400 |
| 150 buildings | NIS 1,080,000 | NIS 16,200 | ~NIS 19,800 | NIS 16,200 |
| 300 buildings | NIS 2,160,000 | NIS 32,400 | ~NIS 39,600 | NIS 32,400 |

*Note: Meshulam costs are paid by the building as payment processing fees, not by the platform. Platform net revenue = platform fee only.*

### Phase 2-3 Revenue Stacking

| Revenue Stream | When | Est. Revenue at 300 Buildings |
|---|---|---|
| Transaction fee (1.5%) | Phase 1 (launch) | NIS 32,400/mo |
| Insurance referral commissions | Phase 2 (month 6+) | NIS 12,500-18,750/mo |
| Service provider marketplace | Phase 3 (month 12+) | NIS 10,000-20,000/mo |
| Premium tier (property managers) | Phase 3 (month 12+) | NIS 5,000-10,000/mo |
| **Combined** | **Month 18** | **NIS 60,000-80,000/mo** |

### Payment Bypass Mitigation

The biggest risk: residents pay via bank standing orders (horaot keva) instead of through the platform, generating zero revenue. Mitigation strategies built into the product:

| Strategy | Implementation | Impact |
|----------|---------------|--------|
| **One-tap payment** | Bit / Apple Pay / Google Pay via Meshulam | Easier than setting up horaot keva |
| **Auto-generated receipts** | Only platform payments get instant digital receipts | Vaad committees need receipts for accounting |
| **Payment tracking dashboard** | Real-time "who paid / who didn't" — only for platform payments | Treasure's #1 pain point solved |
| **Installment plans** | Split large charges into 3-6 credit card payments | Impossible with bank transfer |
| **Automatic late reminders** | WhatsApp + push + email reminders for unpaid residents | Only works for platform-tracked payments |
| **WhatsApp payment links** | Treasurer sends "pay now" link in building WhatsApp group | Tap → pay in 30 seconds |

---

## Cost Estimates

### Monthly Infrastructure Costs

| Service | 50 Buildings | 170 Buildings | 300 Buildings | 1,000 Buildings |
|---------|-------------|--------------|--------------|----------------|
| **Supabase Pro** | $25 | $25 | $25-50 | $75-150 |
| **Vercel Pro** | $20 | $20 | $20 | $20-50 |
| **Resend email** | $0 | $20 | $20 | $50 |
| **Expo Push** | $0 | $0 | $0 | $0 |
| **SMS (OTP)** | ~$15 | ~$50 | ~$90 | ~$300 |
| **Domain + SSL** | $15 | $15 | $15 | $15 |
| **App Store fees** | $10 | $10 | $10 | $10 |
| **Monitoring (Sentry)** | $0 | $26 | $26 | $80 |
| **TOTAL** | **~$85/mo** | **~$166/mo** | **~$206/mo** | **~$680/mo** |

### Revenue vs Cost (Transaction Fee Model)

| Scale | Tx Fee Revenue (NIS) | Insurance Rev (Phase 2) | Total Revenue | Monthly Infra (NIS) | Gross Margin |
|-------|---------------------|------------------------|--------------|---------------------|--------------|
| 50 buildings | 5,400 | — | 5,400 | ~310 | 94% |
| 150 buildings | 16,200 | — | 16,200 | ~600 | 96% |
| 300 buildings | 32,400 | 15,625 | 48,025 | ~750 | 98% |
| 1,000 buildings | 108,000 | 52,000 | 160,000 | ~2,500 | 98% |

*Revenue assumes 1.5% platform fee on average building collecting NIS 7,200/month. Insurance referral at 12.5% of NIS 5,000/year avg premium.*

### MVP Development Budget

| Category | Estimated Cost (NIS) | % |
|----------|---------------------|---|
| Developer 1 (senior, 6 weeks) | 60,000-80,000 | 46% |
| Developer 2 (mid-level, 6 weeks) | 40,000-55,000 | 31% |
| UI/UX Design (Hebrew RTL, 2 weeks) | 15,000-25,000 | 12% |
| Meshulam integration + testing | 5,000-10,000 | 5% |
| App Store setup + legal | 5,000-10,000 | 4% |
| Infrastructure (first 3 months) | 1,000-2,000 | 1% |
| **TOTAL** | **126,000-182,000** | **100%** |

---

## Monorepo Structure

```
vaad-bayit/
├── apps/
│   ├── web/                          # Next.js 15 web dashboard
│   │   ├── app/                      # App Router (RTL layout)
│   │   │   ├── [locale]/             # i18n (he, en, ru, ar)
│   │   │   ├── dashboard/
│   │   │   ├── payments/
│   │   │   ├── maintenance/
│   │   │   ├── admin/                # Internal: platform revenue, fee tracking
│   │   │   └── invoices/             # Building's platform fee invoices
│   │   ├── components/
│   │   └── next.config.ts
│   │
│   └── mobile/                       # Expo (React Native)
│       ├── app/                      # Expo Router (file-based)
│       │   ├── (tabs)/
│       │   ├── maintenance/
│       │   └── payments/
│       ├── components/
│       └── app.json
│
├── packages/
│   ├── shared/                       # Shared TypeScript code
│   │   ├── types/                    # DB types (generated from Supabase)
│   │   ├── validators/               # Zod schemas
│   │   ├── constants/                # Categories, roles, statuses
│   │   └── utils/                    # Date formatting, currency
│   │
│   ├── supabase-client/              # Typed Supabase client wrapper
│   │   ├── queries/                  # React Query hooks
│   │   └── realtime/                 # Realtime subscription hooks
│   │
│   └── ui/                           # Shared UI primitives (optional)
│
├── supabase/
│   ├── migrations/                   # SQL migrations
│   ├── functions/                    # Edge Functions (Deno)
│   │   ├── create-payment/           # Generate Meshulam payment URL
│   │   ├── payment-webhook/          # Handle Meshulam callback + calculate platform fee
│   │   ├── send-notification/        # Push + email + WhatsApp payment links
│   │   ├── charge-standing-orders/   # Cron: daily
│   │   ├── generate-monthly-invoice/ # Cron: 1st of month — invoice buildings for platform fees
│   │   ├── generate-monthly-report/  # Cron: monthly — financial transparency reports
│   │   └── platform-admin/           # Internal: revenue dashboard, fee overrides, building health
│   ├── seed.sql                      # Development seed data
│   └── config.toml
│
├── turbo.json                        # Turborepo config
├── package.json                      # Workspace root
└── .env.example
```

---

## Key Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|-----------|------------|
| **Payment bypass (horaot keva)** | **High** | **High** | Make in-app payment easier: one-tap Bit/card, auto-receipts, installments, WhatsApp pay links. See [Payment Bypass Mitigation](#payment-bypass-mitigation). |
| **Low payment adoption in early buildings** | **High** | **Medium** | Onboard buildings where treasurer is tech-forward. Offer white-glove setup. Target buildings already frustrated with cash/check collection. |
| Meshulam API limitations for recurring billing | High | Medium | Abstract payment provider behind interface. Cardcom as fallback. |
| **Platform fee collection from buildings** | **Medium** | **Medium** | Auto-deduct option with card on file. Monthly invoices with 14-day terms. Fee waiver for first month as onboarding incentive. |
| Bit transaction limits (NIS 20K/month) | Medium | Low | Bit is convenience only; credit card primary. |
| Supabase Edge Function cold starts | Low | Medium | Scheduled pings to keep warm. Payment webhooks aren't latency-sensitive. |
| Hebrew RTL bugs in third-party components | Medium | High | Budget 3 days for RTL testing. Use CSS logical properties. |
| Israeli Privacy Law compliance | High | Low | Data export/deletion from day 1. Register with PPA before launch. |
| Bllink first-mover advantage in payments | Medium | Medium | Differentiate on integrated experience (payments + maintenance + communication). We're free; they take a hidden commission. |

---

## Technology Decision Summary

| Layer | Choice | Monthly Cost (300 buildings) |
|-------|--------|-------------------------------|
| Frontend (Web) | Next.js 15 on Vercel | $20 |
| Frontend (Mobile) | Expo / React Native | $0 |
| Backend + DB + Auth + Storage | Supabase Pro (PostgreSQL) | $25-50 |
| Payments | Meshulam (credit cards + Bit) | Per-transaction (paid by buildings) |
| Push Notifications | Expo Push + Supabase Realtime | $0 |
| Email | Resend | $20 |
| SMS (Auth OTP) | Local Israeli provider or Twilio | ~$90 |
| Monorepo Tooling | Turborepo + pnpm workspaces | $0 |
| CI/CD | GitHub Actions | $0 |
| Monitoring | Sentry | $26 |
| **Total Infrastructure** | | **~$206/month** |

| Revenue Model | Source | Est. Monthly (300 buildings) |
|---|---|---|
| **Platform transaction fee (1.5%)** | Payments processed through app | NIS 32,400 |
| Insurance referral commissions | Partner with licensed agent (Phase 2) | NIS 12,500-18,750 |
| Service provider marketplace | Provider listings + leads (Phase 3) | NIS 10,000-20,000 |
| **Combined at scale** | | **NIS 55,000-71,000** |

---

*Architecture designed March 2026. Updated March 2026 to transaction-fee-first revenue model. All pricing and technology verified via web searches with cited sources.*

**Sources:**
- [Supabase Pricing](https://supabase.com/pricing) | [Supabase RLS Docs](https://supabase.com/docs/guides/database/postgres/row-level-security) | [Supabase Realtime](https://supabase.com/docs/guides/realtime)
- [Expo Monorepo Guide](https://docs.expo.dev/guides/monorepos/) | [Expo Push Notifications](https://docs.expo.dev/push-notifications/overview/) | [Expo + Supabase](https://docs.expo.dev/guides/using-supabase/)
- [Meshulam / Grow Payments](https://apps.duda.co/apps/grow-payments) | [Meshulam API](https://doc.meshulam.co.il/) | [Grow Pricing](https://grow.business/pay-as-you-grow/)
- [Bit Developer Portal](https://developer.bitpay.co.il/docs) | [Cardcom API](https://www.npmjs.com/package/@tsdiapi/cardcom)
- [Israel Privacy Law Amendment 13](https://iapp.org/news/a/israel-marks-a-new-era-in-privacy-law-amendment-13-ushers-in-sweeping-reform)
- [PCI DSS 2026](https://paymentnerds.com/blog/pci-dss-updates-how-to-be-pci-dss-compliant-in-2026/)
- [Cloudflare R2 vs S3](https://www.cloudflare.com/pg-cloudflare-r2-vs-aws-s3/)
- [Bllink Revenue Model](https://www.flashpointvc.com/post/bllink-property-management-platform-closes-a-us1-2-million-seed-round-to-support-its-growth-and-expansion)
- [PayHOA Payment Fees](https://intercom.help/payhoa/en/articles/8663819-payment-fees) | [Buildium Transaction Fees](https://www.buildium.com/blog/buildium-vs-appfolio/)
- [SaaS Freemium Conversion Benchmarks](https://firstpagesage.com/seo-blog/saas-freemium-conversion-rates/)
- [Bank of Israel Interchange Reduction](https://www.boi.org.il/en/communication-and-publications/press-releases/the-interchange-fee-will-be-reduced-by-approximately-30-percent-from-07-percent-to-05-percent-in-three-stages/)
