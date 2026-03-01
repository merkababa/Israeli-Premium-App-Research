# Vaad Bayit Management Platform — Technical Architecture (MVP)

**Date: March 2026 | Budget: NIS 130K-200K | Timeline: 6-8 weeks with 2 developers**

---

## Table of Contents

- [Competitive Context](#competitive-context)
- [MVP Feature Set](#mvp-feature-set)
- [Technology Stack](#technology-stack)
- [Architecture Diagram](#architecture-diagram)
- [Database Schema](#database-schema)
- [Security Considerations](#security-considerations)
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

**Your differentiation**: An integrated, affordable, self-service platform purpose-built for volunteer vaad bayit committees in small/medium buildings (8-40 units), combining payments + maintenance + communication + documents in a single modern interface with Hebrew-first UX.

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
| 9 | **Admin Panel & Billing** | SaaS admin: building subscription management, usage analytics, billing | 4 | P0 |
| 10 | **Hebrew RTL & Localization** | Full RTL layout, Hebrew date formatting, shekel currency, Israeli phone validation | 3 | P0 |

**Total: 60 person-days = 2 developers x 6 weeks**

### Phase 2: v1.1 (Weeks 7-10) — Deferred

| Feature | Effort | Notes |
|---------|--------|-------|
| Resident voting system (building decisions) | 6 days | Requires careful UX for quorum rules |
| Vendor marketplace (find plumbers, electricians) | 8 days | Requires vendor onboarding — chicken-and-egg problem |
| Debt tracking & payment plans | 4 days | Sensitive — needs legal review |
| Multi-building management (for professional managers) | 5 days | Opens new market segment |
| WhatsApp bot integration | 5 days | High engagement potential |

### Phase 3: v2.0 — Future

- AI expense categorization (from receipt photos)
- Predictive maintenance alerts
- Building insurance comparison tool
- Integration with Israeli municipal systems
- Elevator/generator maintenance scheduling with IoT

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
│  │  │  Payment    │ │ Notification │ │  Report Generation    │  │    │
│  │  │  Webhooks   │ │   Sender     │ │  (Monthly PDF)        │  │    │
│  │  │             │ │              │ │                       │  │    │
│  │  │ - Meshulam  │ │ - Expo Push  │ │ - Financial summaries │  │    │
│  │  │   callback  │ │ - Resend     │ │ - Payment status      │  │    │
│  │  │ - Update    │ │   email      │ │ - Transparency report │  │    │
│  │  │   payment   │ │ - SMS via    │ │                       │  │    │
│  │  │   status    │ │   provider   │ │                       │  │    │
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

### Payment Flow

```
Resident opens payment page
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
┌─────────────────────┐
│ Update payments      │
│ table → Generate     │
│ receipt → Send push  │
│ notif + email        │
└─────────────────────┘
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
    subscription_plan TEXT DEFAULT 'trial',
    subscription_status TEXT DEFAULT 'active',
    trial_ends_at   TIMESTAMPTZ,
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
-- SaaS ADMIN
-- =============================================================

CREATE TABLE building_subscriptions (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id     UUID NOT NULL REFERENCES buildings(id),
    plan            TEXT NOT NULL CHECK (plan IN ('trial', 'basic', 'premium')),
    price_monthly   NUMERIC(10,2) NOT NULL,
    started_at      TIMESTAMPTZ DEFAULT now(),
    current_period_start TIMESTAMPTZ,
    current_period_end   TIMESTAMPTZ,
    status          TEXT DEFAULT 'active'
                    CHECK (status IN ('active', 'past_due', 'cancelled', 'trial')),
    meshulam_subscription_id TEXT,
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

### Revenue vs Cost

| Scale | Monthly Revenue (NIS) | Monthly Infra (NIS) | Gross Margin |
|-------|----------------------|---------------------|--------------|
| 50 buildings | ~5,000 | ~310 | 94% |
| 170 buildings | ~20,400 | ~600 | 97% |
| 300 buildings | ~39,000 | ~750 | 98% |
| 1,000 buildings | ~130,000 | ~2,500 | 98% |

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
│   │   │   └── admin/
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
│   │   ├── create-payment/
│   │   ├── payment-webhook/
│   │   ├── send-notification/
│   │   ├── charge-standing-orders/   # Cron: daily
│   │   └── generate-monthly-report/  # Cron: monthly
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
| Meshulam API limitations for recurring billing | High | Medium | Abstract payment provider behind interface. Cardcom as fallback. |
| Bit transaction limits (NIS 20K/month) | Medium | Low | Bit is convenience only; credit card primary. |
| Supabase Edge Function cold starts | Low | Medium | Scheduled pings to keep warm. Payment webhooks aren't latency-sensitive. |
| Hebrew RTL bugs in third-party components | Medium | High | Budget 3 days for RTL testing. Use CSS logical properties. |
| Israeli Privacy Law compliance | High | Low | Data export/deletion from day 1. Register with PPA before launch. |
| Bllink first-mover advantage in payments | Medium | Medium | Differentiate on integrated experience (payments + maintenance + communication). |

---

## Technology Decision Summary

| Layer | Choice | Monthly Cost (300 buildings) |
|-------|--------|-------------------------------|
| Frontend (Web) | Next.js 15 on Vercel | $20 |
| Frontend (Mobile) | Expo / React Native | $0 |
| Backend + DB + Auth + Storage | Supabase Pro (PostgreSQL) | $25-50 |
| Payments | Meshulam (credit cards + Bit) | Per-transaction only |
| Push Notifications | Expo Push + Supabase Realtime | $0 |
| Email | Resend | $20 |
| SMS (Auth OTP) | Local Israeli provider or Twilio | ~$90 |
| Monorepo Tooling | Turborepo + pnpm workspaces | $0 |
| CI/CD | GitHub Actions | $0 |
| Monitoring | Sentry | $26 |
| **Total Infrastructure** | | **~$206/month** |

---

*Architecture designed March 2026. All pricing and technology verified via web searches with cited sources.*

**Sources:**
- [Supabase Pricing](https://supabase.com/pricing) | [Supabase RLS Docs](https://supabase.com/docs/guides/database/postgres/row-level-security) | [Supabase Realtime](https://supabase.com/docs/guides/realtime)
- [Expo Monorepo Guide](https://docs.expo.dev/guides/monorepos/) | [Expo Push Notifications](https://docs.expo.dev/push-notifications/overview/) | [Expo + Supabase](https://docs.expo.dev/guides/using-supabase/)
- [Meshulam / Grow Payments](https://apps.duda.co/apps/grow-payments) | [Meshulam API](https://doc.meshulam.co.il/)
- [Bit Developer Portal](https://developer.bitpay.co.il/docs) | [Cardcom API](https://www.npmjs.com/package/@tsdiapi/cardcom)
- [Israel Privacy Law Amendment 13](https://iapp.org/news/a/israel-marks-a-new-era-in-privacy-law-amendment-13-ushers-in-sweeping-reform)
- [PCI DSS 2026](https://paymentnerds.com/blog/pci-dss-updates-how-to-be-pci-dss-compliant-in-2026/)
- [Cloudflare R2 vs S3](https://www.cloudflare.com/pg-cloudflare-r2-vs-aws-s3/)
