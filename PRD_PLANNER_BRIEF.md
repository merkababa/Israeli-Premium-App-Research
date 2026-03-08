# PRD + Roadmap Planner Brief

**Purpose:** This document gives you everything you need to write the PRD and roadmap WITHOUT reading all 27 research files (~15K lines). You have ~200K tokens of context. Budget them wisely.

**Your deliverables:**
1. A complete Product Requirements Document (PRD) for "Emuni" — the Israeli nanny/babysitter marketplace
2. A phased roadmap (MVP → v2 → v3 → scale)

---

## READING PLAN (MANDATORY ORDER)

You CANNOT read all 27 files. Here is exactly what to read and when:

### Phase 1 — Read These First (core context, ~2,500 lines)

| Priority | File | Lines | Why |
|:--------:|------|------:|-----|
| **1** | `RESEARCH_INDEX.md` | 200 | Navigation + canonical data points + topic cross-reference |
| **2** | `NANNY_PLATFORM_FOUNDER_DECISIONS.md` | 608 | **THE** decision document. All 10 decisions that shape the PRD. Read the full "IF YOU ONLY READ ONE PAGE" section + Quick Decision Summary + each decision's recommendation. |
| **3** | `NANNY_PLATFORM_MASTER_RESEARCH.md` | 600 | Single source of truth for all data. Has the Executive Summary, legal framework summary, revenue model, and market sizing. |
| **4** | `NANNY_PLATFORM_MVP_SCOPE.md` | 581 | RICE-scored feature list for v1/v2/v3. This IS your feature spec. |
| **5** | `NANNY_PLATFORM_PRD_READINESS.md` | 489 | PRD structure template and open questions to address. |

### Phase 2 — Read These for Specific PRD Sections (~2,500 lines)

| Read When Writing... | File | Lines | What You Need From It |
|---------------------|------|------:|----------------------|
| Tech Architecture section | `NANNY_PLATFORM_TECH_RESEARCH.md` | 610 | Stack decisions, IS 5568 accessibility, privacy requirements |
| Matching/Booking section | `NANNY_PLATFORM_MATCHING_FLOW.md` | 943 | 4-tier booking spec, algorithm, trust tiers, cancellation policies — this is the PRODUCT SPEC |
| Growth/Launch section | `NANNY_PLATFORM_LAUNCH_GEOGRAPHY.md` | 748 | Old North TLV beachhead analysis, density math, expansion path |
| Legal/Compliance section | `NANNY_PLATFORM_BACKGROUND_CHECK_RESEARCH.md` | 520 | Background check operationalization — two-track system |
| Legal/Compliance section | `NANNY_PLATFORM_PRIVACY_AMENDMENT_13_RESEARCH.md` | 556 | Data protection compliance checklist |

### Phase 3 — Reference Only If Needed (DON'T read proactively)

| File | When You'd Need It |
|------|--------------------|
| `NANNY_PLATFORM_PAYMENT_PROCESSOR_COMPARISON.md` | Payment architecture details |
| `NANNY_PLATFORM_COST_MODEL.md` | Burn rate details, salary benchmarks |
| `NANNY_PLATFORM_MONETIZATION_STRATEGY.md` | Pricing experiment details |
| `NANNY_PLATFORM_GROWTH_STRATEGY.md` | Cold start tactics, viral mechanics |
| `NANNY_PLATFORM_FUNDING_RESEARCH.md` | IIA grant details |
| `NANNY_PLATFORM_BUSINESS_MODEL_STRATEGY.md` | Revenue model deep dive (WARNING: 1,150 lines — only read specific sections) |
| `NANNY_PLATFORM_LEGAL_FRAMEWORK.md` | Employment law details |
| `WOLT_ISRAEL_LEGAL_DEEP_DIVE.md` | Wolt case details |
| All other files | Unlikely to need |

---

## EVERYTHING YOU NEED TO KNOW (EXTRACTED)

The sections below extract the key facts from all 27 documents so you don't have to read them. Use the files above for depth.

### 1. WHAT IS EMUNI?

A **Hebrew-first mobile marketplace** connecting Israeli families with background-checked babysitters and nannies. Legally structured as a **pure marketplace** — the family is always the employer, never the platform.

**One-liner:** "Tinder for finding trusted childcare, not dating."

### 2. THE 10 FOUNDER DECISIONS (CANONICAL)

| # | Decision | Answer | Non-Negotiable? |
|:-:|----------|--------|:---------------:|
| 1 | Name | **Emuni** (אמוני — "My Trust") | Yes |
| 2 | Co-founder | **Technical co-founder, 50/50 equity** | Yes |
| 3 | Funding | **IIA Tnufa (NIS 200K) + Angel syndicate (NIS 1-1.5M) + IIA 60% match** | Yes |
| 4 | Launch city | **Old North Tel Aviv only** (single beachhead) | Yes |
| 5 | Language | **Hebrew-first** (English at Month 4-6, i18n from Day 1) | Yes |
| 6 | Monetization | **Freemium from Day 1** — Free: browse + 1 booking/mo; Premium: NIS 49/mo; Per-contact: NIS 19 | Yes |
| 7 | Payments v1 | **No in-app payments** — families pay nannies directly (Bit/cash). Platform collects fees via manual Bit invoicing. Add PayMe at Month 3. | Yes |
| 8 | Background checks | **Platform pays** (criminal cert is FREE; budget NIS 47/nanny for admin costs) | Yes |
| 9 | Nanny Pro tier | **Deferred** — Employment Service Law gray zone. Get attorney sign-off first. | Yes |
| 10 | Emergency/B2B in MVP | **No** — both need density you don't have yet. B2B conversations at Month 3, sign at Month 6+. | Yes |
| 11 | Minimum nanny age | **18+** — Youth Labor Law allows 15, but 18+ eliminates parental consent, hour restrictions, minor data complexity. Matches Rockmybaby standard. | Yes |
| 12 | Cancellation policy (v1) | **Reliability score only** — no financial penalties (no payment mechanism in v1). Score impacts search ranking. Add financial penalties in v2 with PayMe. | Yes |
| 13 | Liability language | **Precise language + ToS, not insurance.** Never say "safe" or "verified nanny." Say "identity verified," "police clearance obtained." The "negligent vetting trap": doing background checks creates a duty of care — protect through accurate descriptions, not safety guarantees. | Yes |
| 14 | Insurance | **ToS only at launch.** Add E&O + cyber at seed round (Month 6+, ~NIS 15-30K/yr). | Yes |
| 15 | Free tier limits | **Generous free, premium = convenience.** Free: full profiles, 1 booking/mo, basic filters, messaging. Premium (NIS 49/mo): unlimited bookings, advanced filters, priority inbox, favorites, founding badge. | Yes |

### 3. LEGAL CONSTRAINTS (HARD RULES FOR PRD)

These are non-negotiable architectural constraints:

| Constraint | Rule | Consequence of Violation |
|-----------|------|------------------------|
| **Pure marketplace** | Platform NEVER controls, assigns, prices, or supervises nannies | Employer classification → millions in retroactive benefits (Wolt disaster) |
| **Family = employer** | All employment obligations (social benefits, insurance) are on the family | Platform provides info/tools but never assumes employer role |
| **No nanny fees** | Employment Service Law prohibits charging job seekers (nannies) placement fees | Substantial financial penalties per violation |
| **Family-side fees only** | Subscription, booking fees, transaction fees — all charged to families | Unrestricted under Israeli law |
| **Fee structure ≠ classification** | How you charge has ZERO impact on employer classification | Only the 9 control factors matter (Wolt ruling) |
| **Background checks** | Cannot legally REQUIRE general criminal record from nannies (2019 law). CAN require sex offense clearance for childcare roles. | Two-track system: mandatory sex offense check + voluntary criminal cert with badge |
| **Privacy (Amendment 13)** | Mandatory DPO, 72-hr breach notification, explicit consent per data type, database registration with PPA | Fines + class actions (NIS 10-100K per individual without proof of harm) |
| **IS 5568 accessibility** | Mobile app must comply with Israeli accessibility standard | NIS 50K penalty per complaint |
| **SHAAM e-invoicing** | Mandatory for transactions above NIS 5K (June 2026 deadline) | Tax authority penalties |
| **Employment bureau license** | Recommended safety net (apply proactively) | Not strictly required for pure marketplace, but adds legal protection |

### 4. REVENUE MODEL

```
Revenue Streams:
├── Family Premium subscription: NIS 49/mo (Free tier: browse + 1 booking/mo)
├── Per-contact fee: NIS 19 (for non-subscribers)
├── Transaction fee: 12-15% on booking value (charged to families)
├── B2B corporate contracts: NIS 2K-8K/mo (Month 6+)
└── Value-added services (v2+): featured profiles, background check reports

Canonical Projections:
├── Y1: NIS 640K-820K
├── Y2: NIS 2.5-3.5M
├── Y3: NIS 7.6-9.4M
└── Breakeven: Month 20-26

Unit Economics:
├── CAC: NIS 80-150 (families), NIS 30-60 (nannies)
├── LTV: ~NIS 600-900 (subscription) + ~NIS 200-400 (transaction fees)
├── LTV/CAC: ~5-8x (healthy)
└── Monthly burn: NIS 143K (pre-launch) → NIS 329K (at launch)
```

### 5. MVP SCOPE (v1)

**Build time:** 8-12 weeks (with technical co-founder)

**IN MVP (v1):**
- Family registration + profile (name, location, children ages, needs)
- Nanny registration + profile (experience, availability, rate, languages, certifications)
- Nanny verification: ID check + sex offense clearance (mandatory) + criminal cert (voluntary, badge)
- Search/browse nannies by location (PostGIS), availability, rate, language
- Advance booking request (Tier 3 only — no emergency, no instant)
- In-app messaging (family ↔ nanny)
- Review/rating system (post-booking, family rates nanny AND nanny rates family)
- Free tier: browse + 1 booking/month
- Premium tier: NIS 49/mo (unlimited bookings, priority support, advanced filters)
- Per-contact purchase: NIS 19
- Manual payment collection (Bit invoicing for first 50 users)
- Push notifications
- Hebrew UI (i18n-ready)
- Basic admin dashboard
- IS 5568 accessibility compliance

**NOT IN MVP:**
- In-app payments / PayMe integration (v2, Month 3)
- Emergency/same-day booking (v2, needs density)
- Trust graph / community recommendations (v2)
- B2B corporate portal (v2, Month 6+)
- Nanny Pro tier (deferred, needs legal sign-off)
- English UI (Month 4-6)
- WhatsApp deep integration (v2)
- AI matching algorithm (v3)
- Insurance products (v3)
- Multi-city expansion (v2+)

### 6. TECH STACK

| Layer | Technology | Why |
|-------|-----------|-----|
| Mobile | **React Native + Expo** | Cross-platform, large talent pool in Israel |
| Backend | **NestJS (Node.js/TypeScript)** | Type safety, structured, scalable |
| Database | **PostgreSQL + PostGIS** | Geospatial queries for nanny search by location |
| Auth/Realtime | **Supabase** | Auth, realtime subscriptions, Row Level Security |
| Cloud | **AWS (il-central-1)** | Israeli data residency for Amendment 13 compliance |
| ID verification | **AU10TIX** | Israeli company, government ID verification |
| Messaging | **In-app (Supabase Realtime)** | v1 messaging; WhatsApp integration in v2 |
| Payments (v2) | **PayMe** | Only Israeli processor with marketplace split payments |
| Monitoring | **Sentry + Mixpanel** | Error tracking + product analytics |
| CI/CD | **GitHub Actions** | Standard |

### 7. MARKET DATA

| Metric | Value |
|--------|-------|
| TAM | NIS 22.8B ($6.3B) — 850K families |
| SAM | NIS 216M ($60M) — 270K urban digital families |
| SOM Y3 | NIS 23.5M ($6.5M) — 28K paying users |
| Dominant incumbent | **None** — fragmented Facebook groups, Yad2, small agencies |
| Closest digital competitor | **Helpbook** (job board, not marketplace) |
| Only tech marketplace | **Babysits** (generic European, no Israeli adaptation) |
| Failed Israeli predecessor | **Babysitting/ExitValley** (2016-2018, ~34K users, appears dead) |
| Market trigger | Jan 2025 Jerusalem daycare tragedy + gov supervision budget collapsed 76% |
| Average babysitter rate (TLV) | NIS 50-80/hr (Babysits data: NIS 63.95/hr avg) |

### 8. GROWTH STRATEGY SUMMARY

```
Phase 0 (Pre-launch, Month -3 to 0):
├── Recruit 50 nannies in Old North TLV (10/km2 density target)
├── In-person onboarding: campus job fairs, nanny Facebook groups, referrals
├── Background checks for all 50
├── Soft-launch with 20 founding families (personal network)
└── Manual everything (Bit invoicing, WhatsApp coordination)

Phase 1 (Launch, Month 0-3):
├── Open to all families in Old North TLV
├── "Bring Your Nanny" mechanic: families invite their existing nanny to join
├── PMF metric: 10 bookings/week by week 12
├── Target: 100 nannies, 200 families
└── Begin B2B conversations with 3-5 TLV tech companies

Phase 2 (Traction, Month 3-6):
├── Integrate PayMe for in-app payments
├── Add English UI
├── Expand to Florentin/Neve Tzedek
├── Emergency booking (if density sufficient)
├── Target: 200 nannies, 500 families
└── Sign first B2B contract

Phase 3 (Growth, Month 6-12):
├── Expand to Ra'anana (Anglo community)
├── B2B corporate portal
├── WhatsApp deep integration
├── Trust graph / community recommendations
├── Target: 500 nannies, 2,000 families
└── Begin seed round (NIS 5-7M)

Phase 4 (Scale, Month 12-24):
├── Multi-city (Herzliya, Netanya, Jerusalem)
├── AI matching
├── Insurance products
├── Target: 2,000 nannies, 8,000 families
└── Breakeven at Month 20-26
```

### 9. KEY RISKS FOR PRD

| Risk | Likelihood | Impact | Mitigation |
|------|:----------:|:------:|------------|
| Cold start failure (can't recruit 50 nannies) | MEDIUM | CRITICAL | Founder does in-person recruitment. Pay NIS 100 referral bonus. |
| NIS 49/mo too low for unit economics | MEDIUM | HIGH | Transaction fees supplement. Breakeven may extend to Mo 24-28. |
| Background check process harder than expected | HIGH | HIGH | Engage Israeli employment counsel pre-launch. May need "covered institution" status. |
| Privacy compliance delays launch | MEDIUM | MEDIUM | Budget NIS 140-395K. Appoint outsourced DPO. Register database with PPA. |
| Wolt appeal reversal changes classification law | LOW | HIGH | Our marketplace structure avoids all 9 control factors regardless. |
| "Emuni" domain/trademark unavailable | MEDIUM | LOW | Backup names: Kena, Bubale (from NAMING_RESEARCH) |
| No technical co-founder found | MEDIUM | HIGH | Outsource MVP (NIS 300-500K) but delays timeline by 2-3 months |

### 10. PAYMENT ARCHITECTURE (MVP → v2)

```
MVP (Month 0-3):
├── Family subscribes via: manual Bit payment to platform
├── Family pays nanny: directly (Bit/cash) — platform NOT involved
├── Platform collects: subscription (NIS 49/mo) + per-contact (NIS 19)
└── Platform invoices: manually via Bit, with tax invoice

v2 (Month 3+, PayMe integration):
├── Family subscribes via: credit card (PayMe recurring billing)
├── Family books nanny: pays via PayMe (platform takes 12-15% fee, nanny gets rest)
├── Platform collects: subscription + transaction fee (automatic split)
├── PayMe handles: SHAAM e-invoicing, credit card installments, PCI compliance
└── Nanny receives: automatic payout to bank account via PayMe marketplace splits
```

### 11. COMPLIANCE CHECKLIST (PRE-LAUNCH)

1. [ ] Register company (Israeli Ltd / חברה בע"מ)
2. [ ] Apply for Employment Bureau License (safety net)
3. [ ] Apply for IIA Tnufa grant (NIS 200K)
4. [ ] Engage employment law attorney (covered institution status, background checks)
5. [ ] Appoint outsourced DPO (Amendment 13)
6. [ ] Register database with PPA
7. [ ] Prepare privacy policy + terms of service (Hebrew)
8. [ ] Set up SHAAM e-invoicing (before NIS 5K threshold)
9. [ ] IS 5568 accessibility audit
10. [ ] Penetration test (mandatory every 18 months under Amendment 13)
11. [ ] Set up data breach response plan (72-hr notification)

---

## PRD STRUCTURE RECOMMENDATION

Based on PRD_READINESS.md analysis, write the PRD in these sections:

```
1. Product Overview
   1.1 Vision & Mission
   1.2 Problem Statement
   1.3 Target Users (families + nannies personas)
   1.4 Success Metrics / KPIs

2. Legal & Compliance Framework
   2.1 Pure Marketplace Architecture (non-negotiable rules)
   2.2 Employment Classification Safeguards
   2.3 Background Check System (two-track)
   2.4 Privacy Compliance (Amendment 13)
   2.5 Accessibility (IS 5568)
   2.6 Tax & Invoicing (SHAAM)

3. User Stories & Flows
   3.1 Family Registration & Onboarding
   3.2 Nanny Registration & Verification
   3.3 Search & Discovery
   3.4 Booking Flow (Advance Booking / Tier 3)
   3.5 Messaging
   3.6 Reviews & Ratings
   3.7 Subscription & Payment

4. Feature Specification (MVP)
   4.1 In-Scope Features (RICE-scored from MVP_SCOPE)
   4.2 Out-of-Scope (deferred to v2/v3)
   4.3 Non-Functional Requirements (performance, security, accessibility)

5. Technical Architecture
   5.1 Stack Overview
   5.2 Database Schema (key entities)
   5.3 API Design Principles
   5.4 Geospatial Search (PostGIS)
   5.5 Real-time Messaging (Supabase)
   5.6 Authentication & Authorization
   5.7 Data Residency (AWS il-central-1)

6. Revenue Model & Pricing
   6.1 Free vs Premium Tiers
   6.2 Transaction Fees
   6.3 B2B (deferred, but define the hook)
   6.4 Payment Architecture (MVP manual → v2 PayMe)

7. Growth & Launch Plan
   7.1 Pre-Launch (supply recruitment)
   7.2 Launch (Old North TLV)
   7.3 Phase 2-4 Expansion
   7.4 PMF Metrics & Kill Criteria

8. Roadmap
   8.1 MVP (Month 0-3) — feature list + milestones
   8.2 v2 (Month 3-6) — payments, English, expansion
   8.3 v3 (Month 6-12) — B2B, WhatsApp, trust graph
   8.4 Scale (Month 12-24) — multi-city, AI, insurance

9. Risk Register
   9.1 Legal Risks
   9.2 Market Risks
   9.3 Technical Risks
   9.4 Operational Risks

10. Appendices
    10.1 Research Document Index (link to RESEARCH_INDEX.md)
    10.2 Canonical Data Points
    10.3 Glossary (Hebrew legal/business terms)
```

---

## CONTEXT BUDGET GUIDE

Your ~200K token window ≈ ~5,000-6,000 lines of markdown you can read. Budget:

| Activity | Estimated Tokens | Lines |
|----------|:----------------:|:-----:|
| This brief (PRD_PLANNER_BRIEF.md) | ~8K | 350 |
| Phase 1 reads (5 files) | ~40K | 2,500 |
| Phase 2 reads (5 files, as needed) | ~40K | 2,500 |
| Your own reasoning | ~40K | — |
| PRD output | ~50K | ~2,000 |
| Roadmap output | ~15K | ~500 |
| **Buffer** | **~7K** | — |
| **Total** | **~200K** | — |

**Rules:**
- Read Phase 1 files FIRST (all 5, in order)
- Read Phase 2 files ONLY when writing the specific section that needs them
- NEVER read Phase 3 files unless you hit a specific question this brief doesn't answer
- Trust the canonical data points in RESEARCH_INDEX.md — don't re-verify
- If you run low on context, the MATCHING_FLOW (943 lines) is the biggest Phase 2 file — read only the sections relevant to MVP (Tier 3 Advance Booking)

---

*This brief was created March 7, 2026 after completing all audit corrections and gap-fill research across 27 documents. All data points are verified and internally consistent.*
