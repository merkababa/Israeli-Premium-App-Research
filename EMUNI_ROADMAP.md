# EMUNI — Product Roadmap

**Version:** 1.1
**Date:** March 7, 2026
**Companion Document:** `EMUNI_PRD.md` (v1.1)
**Status:** FINAL — Aligned with PRD v1.1 (post-review fixes applied)
**Changelog:** v1.1 — Aligned with PRD review fixes: geography (Florentin→Ramat Aviv), kill criteria (Week 16→20-24), financials (IAP, AU10TIX costs), SEO/ASO, emergency flows.

---

## ROADMAP OVERVIEW

```
MONTH -6 to -3    PREPARATION (SOLO)
                   ├── Company formation, IIA Tnufa application
                   ├── DIY ToS + privacy policy from templates
                   ├── Launch emuni.co.il landing page + waitlist (SEO)
                   └── Begin nanny outreach (warm leads)

MONTH -3 to 0     PRE-LAUNCH (SOLO, AI-ASSISTED DEV)
                   ├── MVP development (8-12 weeks, solo + AI)
                   ├── Supply recruitment (50 nannies in Old North)
                   ├── ID verification for all 50 (AU10TIX)
                   ├── Founding family onboarding (20 families)
                   └── IS 5568 accessibility audit

MONTH 0-3         MVP LAUNCH — "Does It Work?"
                   ├── Public launch in Old North TLV
                   ├── PMF tracking → 10 bookings/week by Week 16
                   ├── Manual payments (Bit invoicing)
                   └── Diagnostic at Week 16, kill decision at Week 20-24

MONTH 3-6         TRACTION — "Is It Worth Paying For?"
                   ├── PayMe integration (automated payments)
                   ├── English UI toggle
                   ├── Expand to Ramat Aviv + Ra'anana
                   ├── Short Notice booking (Tier 2)
                   └── First B2B pilot conversations

MONTH 6-12        GROWTH — "Can It Scale?"
                   ├── Herzliya expansion + opportunistic Florentin
                   ├── B2B corporate portal + first contract
                   ├── Trust graph v1
                   ├── Emergency booking (if density allows)
                   ├── Seed round (NIS 5-7M + IIA match)
                   └── Target: 500 nannies, 2,000 families

MONTH 12-24       SCALE — "Israel's Childcare Platform"
                   ├── Multi-city (Jerusalem, Modiin, Netanya)
                   ├── AI matching algorithm
                   ├── Insurance products
                   ├── Solo breakeven Month 3-5, Scaled breakeven Month 20-26
                   └── Target: 2,000 nannies, 8,000 families
```

---

## PHASE 1: PRE-LAUNCH (Month -3 to 0)

### Goals
- Build and test the MVP
- Recruit and verify 50 nannies in Old North TLV
- Onboard 20 founding families
- Complete all legal and compliance prerequisites

### Features

**P0 — Must ship:**
- Family registration + profile (phone OTP, children, neighborhood)
- Nanny registration + profile (bio, experience, rate, availability, certifications)
- Nanny verification flow (ID upload → AU10TIX → optional background certificate upload → admin approval)
- Search/browse nannies (PostGIS radius, parameterized filters: distance 1/3/5/10/15km, rate, availability, age group)
- **Empty search results state** (expand radius, "Bring Your Nanny" CTA, waitlist capture)
- Advance Booking flow (Tier 3 only, 24+ hours out — request → accept/decline → confirm)
- **Booking cost summary display** ("Estimated total: NIS 275 (5 hrs x NIS 55/hr)")
- **Emergency nanny replacement flow** (auto-suggest available nannies when a nanny cancels <24hr)
- Nanny safety tools (WhatsApp location sharing, emergency 112/101 buttons, emergency alert to admin, optional check-in)
- **Dispute resolution** (report issue → dispute category → admin review within 48hr)
- In-app messaging (Supabase Realtime, pre-booking only)
- WhatsApp handoff post-booking (deep link with pre-filled message)
- Push notifications (Expo Notifications — booking requests, acceptances, reminders)
- Basic reviews (1-5 stars + text, blind, mutual)
- Hebrew RTL UI (i18n architecture from Day 1)
- Basic admin panel (approve profiles, manage background checks, view bookings, handle reports)
- IS 5568 accessibility compliance

**P1 — Ship within first 2 weeks:**
- Freemium tiers (Free: 1 booking/mo, Premium: NIS 49/mo, manual Bit payment)
- Per-contact purchase (NIS 19, manual Bit)
- "Bring Your Nanny" invite flow
- Favorites/bookmarking
- Cancellation policy display (reliability score only, no financial penalties)

### Dependencies
- [ ] Israeli Ltd. registered (articles: "development and operation of technology software for information services")
- [ ] Employment bureau license application filed
- [ ] AU10TIX contract signed and API integrated (note: evaluate Onfido/Veriff as alternatives due to AU10TIX 2024 data breach — see PRD Risk R17)
- [ ] Privacy policy + ToS drafted (DIY from templates)
- [ ] Database Definition Document created
- [ ] Breach response plan documented
- [ ] Crisis communications templates prepared
- [ ] emuni.co.il landing page live with waitlist + SEO
- [ ] App Store + Google Play accounts set up (ASO-optimized Hebrew listings)
- [ ] AWS il-central-1 infrastructure provisioned
- [ ] Supabase hosting decision resolved (managed Frankfurt vs self-host il-central-1 — see PRD Open Question #5)

*DPO deferred until ~500-1,000 users. Attorney engagement deferred until revenue exists.*

### Team
Solo founder — building everything with AI-assisted development (Claude, Cursor). No salaries. No co-founder.

### Key Milestones

| Milestone | Target Date | Success Criteria |
|-----------|:-----------:|------------------|
| MVP code complete | Month -1 | All P0 features functional in staging |
| IS 5568 accessibility audit passed | Month -1 | WCAG 2.1 AA compliance confirmed |
| 50 nannies verified and live | Month 0 (launch day) | All with ID verification (AU10TIX). Voluntary background certificate badges encouraged. |
| 20 founding families registered | Month 0 | Complete profiles, Founding Member subscription active |
| App Store + Google Play approved | Month 0 | Hebrew listings live |
| Soft launch begins | Month 0 | First real bookings |

### Budget Estimate (Solo Bootstrapper)

| Item | Cost (NIS) |
|------|:---:|
| AWS infrastructure (3 months) | 1,500 |
| AU10TIX verification (50 nannies @ NIS 8-15 each) | 400-750 |
| DIY privacy policy + ToS (templates) | 0 |
| Nanny referral bonuses (10 x NIS 100) | 1,000 |
| App Store fees (Apple $99/yr + Google $25) | 460 |
| Misc (domains, tools, subscriptions) | 2,000 |
| **Total Pre-Launch** | **~NIS 5,400-5,700** |

*No attorney fees at launch. DPO deferred until ~500-1,000 users. Engage attorney when revenue exists.*

---

## PHASE 2: MVP LAUNCH (Month 0-3)

### Goals
- Validate product-market fit: 10 bookings/week by Week 16
- Grow to 100 nannies, 200 families
- Validate willingness to pay (first Premium subscribers)
- Collect enough data to inform v2 decisions

### Features (Post-Launch Iterations)

**Month 0-1:**
- Bug fixes from soft launch feedback
- UX improvements based on first 20 families' feedback
- Performance optimization (search <500ms target)
- Founding Member enrollment (200 spots at NIS 29/mo)

**Month 1-2:**
- "My Nannies" list (previous bookings) — RICE score 12.0, low effort
- Cancellation policy display on booking screen
- Profile completeness indicator for nannies (nudge better profiles)
- Email notifications (booking confirmations, weekly digest)

**Month 2-3:**
- Nanny earnings summary (total bookings, total hours, monthly view)
- Basic nanny-of-the-month highlighting (manual, admin-selected)
- Prepare PayMe integration (contract negotiation, API spike)
- Begin Short Notice booking (Tier 2) development

### Dependencies
- PMF tracking infrastructure operational (Mixpanel events firing correctly)
- Customer support process defined (founder WhatsApp for first 100 users)
- Manual Bit invoicing workflow documented and tested

### Team
Solo founder — product, development, growth, support, nanny recruitment, PMF tracking. All roles.

### Key Milestones

| Milestone | Target Date | Success Criteria |
|-----------|:-----------:|------------------|
| First completed booking | Week 1-2 | Real family + real nanny + real session |
| 50 families registered | Week 4 | With complete profiles |
| 5 bookings/week | Week 6-8 | Consistent for 2 consecutive weeks |
| First 10 Premium subscribers | Week 8 | Manual Bit payment confirmed |
| **10 bookings/week** | **Week 16** | **PMF threshold — GREEN signal** |
| 100 nannies verified | Week 10-12 | Across Old North + adjacent areas |
| Diagnostic checkpoint | Week 16 | If < 5 bookings/week → investigate bottleneck |
| Kill/continue decision | Week 20-24 | If still < 5 bookings/week → interview 20 churned users, pivot or shut down |

### Success Criteria (End of Phase 2)

| Metric | Target |
|--------|--------|
| Verified nannies | 100 |
| Registered families | 200 |
| Bookings/week | 10+ |
| Booking completion rate | 60%+ |
| Repeat booking rate (30-day) | 30%+ |
| NPS (families) | 40+ |
| NPS (nannies) | 40+ |
| Premium subscribers | 30+ |
| Monthly revenue | NIS 5,000+ |

### Budget Estimate (Solo Bootstrapper)

| Item | Monthly (NIS) | 3-Month Total |
|------|:---:|:---:|
| AWS infrastructure | 500 | 1,500 |
| Google Maps API (Routes API, per-SKU free thresholds) | 0-200 | 0-600 |
| AU10TIX (50 new nannies @ NIS 8-15) | ~130-250 | 400-750 |
| Marketing (organic + small Instagram spend) | 500-1,000 | 1,500-3,000 |
| Misc | 500 | 1,500 |
| **Monthly burn** | **~NIS 1,600-2,500** | **~NIS 5,000-7,400** |

---

## PHASE 3: TRACTION (Month 3-6)

### Goals
- Integrate automated payments (PayMe)
- Launch English UI for Anglo community
- Expand geography to Ramat Aviv and Ra'anana (Florentin deferred — not family-oriented)
- Add Short Notice booking (Tier 2)
- Begin B2B pilot conversations
- Target: 200 nannies, 500 families

### Features

**P0 — Must ship:**
- **PayMe integration** — automated subscription billing (NIS 49/mo), transaction fees (12-15%), marketplace split payments (nanny receives rate, platform receives fee)
- **Short Notice booking (Tier 2)** — request to up to 3 nannies, 4-hour response window
- **English UI toggle** — leveraging i18n architecture built on Day 1
- **Trust tiers v1** — Verified (blue), Established (silver, 3+ bookings), Trusted (gold, 10+ bookings)
- **Cancellation financial penalties** (via PayMe) — family cancellation fees per tier schedule
- **Enhanced admin analytics** — cohort retention, booking completion rate, supply/demand ratio by neighborhood

**P1 — Should ship:**
- Automated ID verification (AU10TIX API fully automated, no manual review)
- Nanny dashboard (earnings summary, response rate, rating, tier progress)
- Two-sided review display (nannies see family ratings before accepting)
- Content monitoring — automated phone number detection in pre-booking messages
- Video introduction upload for nannies
- Notification caps (max 3/day for nannies)

### Dependencies
- Phase 2 PMF confirmed — **hard gate:** 10+ bookings/week for 4+ consecutive weeks. **Ideal gate:** 4 of 6 expansion metrics met (see PRD Section 7.3)
- PayMe contract signed (target: 1.5-2.5% processing fee, realistic for startup volume)
- SHAAM e-invoicing API integrated (for future B2B invoices > NIS 5K)
- English translations complete (UI strings + key content)
- 50+ nannies in expansion neighborhoods before opening to families there

### Team
Solo founder. Consider first hire (community manager or part-time dev) if revenue supports it.

### Key Milestones

| Milestone | Target Date | Success Criteria |
|-----------|:-----------:|------------------|
| PayMe live in production | Month 3.5 | First automated subscription charge processed |
| English UI live | Month 4 | Full app usable in English |
| Ramat Aviv / Ra'anana expansion | Month 4 | 30+ nannies in each new area |
| Short Notice booking live | Month 4.5 | Tier 2 functional with multi-request logic |
| First B2B pilot conversation | Month 4 | Meeting with HR at 3+ tech companies |
| 200 nannies verified | Month 5 | Across all active areas |
| 500 families registered | Month 6 | |
| 40 bookings/week | Month 6 | |

### Budget Estimate (Solo Bootstrapper)

| Item | Monthly (NIS) |
|------|:---:|
| AWS infrastructure | 1,500-3,000 |
| PayMe processing costs | 1,000-2,000 |
| Google Maps API | 500-2,000 |
| Marketing | 2,000-5,000 |
| Misc | 1,000 |
| **Monthly burn** | **~NIS 6,000-13,000** |
| **Phase 3 total (3 months)** | **~NIS 18,000-39,000** |

*DPO appointment may become necessary during this phase if user count approaches 500-1,000. Budget ~NIS 5-12K/mo outsourced if triggered.*

---

## PHASE 4: GROWTH (Month 6-12)

### Goals
- Expand to Herzliya + opportunistic Florentin (if demand signals)
- Sign first B2B corporate contract
- Launch trust graph and emergency booking
- Begin seed round fundraising (NIS 5-7M + IIA match)
- Target: 500 nannies, 2,000 families

### Features

**P0 — Must ship:**
- **Herzliya geographic expansion** (requires 50+ nannies pre-recruited) + opportunistic Florentin if waitlist demand exists
- **B2B corporate portal v1** — employer onboarding, employee benefit dashboard, usage reporting
- **Emergency booking (Tier 1)** — broadcast to 5 available nannies, 15-min window, cascading radius (only if density > 50 available nannies in 5km)
- **Social trust graph v1** — phone contact matching ("5 people in your contacts use this app"), booking history connections
- **Recurring booking (Tier 4)** — job posting with applicant management, trial period

**P1 — Should ship:**
- WhatsApp Business API integration (booking confirmations, reminders via WhatsApp)
- SMS fallback notifications (for Emergency tier reliability)
- Community groups (neighborhood-based, auto-suggested from address)
- Full matching algorithm (100-point scoring: trust 30%, availability 20%, distance 15%, rating 15%, response 10%, experience 7%, profile 3%)
- Vouching system (parents vouch for nannies, limited to 5 vouches per parent)
- Israeli calendar integration (Hebrew dates, Shabbat times, chag awareness)

### Dependencies
- Phase 3 success metrics met (200+ nannies, 500+ families, 40+ bookings/week)
- Seed round fundraising initiated (pitch deck, investor meetings)
- IIA Pre-Seed/Seed grant applications filed
- Anglo community partnerships established (Janglo, Nefesh B'Nefesh, ESRA) — now relevant from Phase 3 (Ra'anana)
- B2B pilot data available (from Month 3-6 conversations)

### Team
Solo founder until seed round closes. Post-seed hiring plan: CTO, mobile dev, community manager (3-4 FTE). Exact team depends on seed round size and timing.

### Key Milestones

| Milestone | Target Date | Success Criteria |
|-----------|:-----------:|------------------|
| Herzliya launch | Month 7 | 50+ nannies, English UI live |
| First B2B contract signed | Month 8 | NIS 2K-5K/mo recurring |
| Trust graph v1 live | Month 8 | Phone contact matching functional |
| Emergency booking live | Month 9 | Only in zones with 50+ available nannies |
| Seed round term sheet | Month 9-10 | NIS 5-7M at pre-money valuation |
| 500 nannies | Month 10 | Across all active areas |
| 2,000 families | Month 12 | |
| 150 bookings/week | Month 12 | |

### Budget Estimate

**Pre-seed (solo):** ~NIS 10-20K/mo (infra, marketing, DPO, legal retainer)
**Post-seed (with team):** Revisit based on seed round size. COST_MODEL.md has a full-team model at ~NIS 441K/mo for reference.

| **Phase 4 total estimate** | **NIS 60-120K (solo) to NIS 2,650K (full team post-seed)** |
|---|---|

---

## PHASE 5: SCALE (Month 12-24)

### Goals
- Expand to multiple cities (Jerusalem, Modiin, Netanya, Herzliya)
- AI-powered matching algorithm
- Insurance products
- Russian language support (for Haifa/Netanya expansion)
- Solo breakeven expected Month 3-5; scaled breakeven at Month 20-26
- Target: 2,000 nannies, 8,000 families

### Features

- **Multi-city expansion** — Jerusalem (Anglo neighborhoods: Baka, Katamon, Rehavia), Modiin, Netanya
- **AI matching algorithm** — ML-based relevance scoring trained on booking completion data, response patterns, and user preferences
- **Insurance marketplace** — partnership with Israeli insurance provider for nanny liability coverage
- **Russian UI** — for Haifa/Netanya expansion (1.3M Russian speakers in Israel)
- **Special needs matching vertical** — dedicated filters, certified nanny tags, specialized profiles
- **Advanced B2B** — multiple corporate contracts, employer subsidy flow, HR reporting
- **Nanny share matching** — families in same building/street share a nanny
- **Employment law toolkit** — Bituach Leumi registration guide, payslip templates (lead magnet + value-add)
- **Subsidy navigator** — help eligible families find unclaimed government childcare subsidies
- **Anti-gaming** — fake review detection, connection fraud prevention
- **Arabic UI exploration** — research and planning for Arabic language support (Year 2+)

### Team
Post-seed: scale to ~8-15 FTE based on traction and funding. Exact roles TBD based on what's working.

### Key Milestones

| Milestone | Target Date | Success Criteria |
|-----------|:-----------:|------------------|
| Jerusalem launch | Month 14 | 100+ nannies in Anglo neighborhoods |
| 5+ B2B corporate contracts | Month 15 | NIS 20K+/mo B2B revenue |
| AI matching v1 live | Month 16 | Measurable improvement in booking completion rate |
| Russian UI live | Month 18 | For Haifa/Netanya launch |
| 1,000 nannies | Month 18 | Across all cities |
| 5,000 families | Month 18 | |
| **Scaled breakeven** | **Month 20-26** | **Monthly revenue > monthly burn (~NIS 500K/mo)** |
| 2,000 nannies | Month 24 | National presence |
| 8,000 families | Month 24 | |

### Budget Estimate
Depends entirely on seed round outcome. COST_MODEL.md has a full-scale model for reference (note: that model assumes 7.5 FTE which may be aspirational). Actual spend will be data-driven based on what Phase 4 reveals.

| **Phase 5 monthly burn (full team)** | **~NIS 300-500K/mo** |
|---|---|

---

## VISUAL TIMELINE

```
2026
────────────────────────────────────────────────────────────────────────

Q2 (Apr-Jun)                    Q3 (Jul-Sep)
├── Mo -3: Landing page + MVP   ├── Mo 0: PUBLIC LAUNCH (Old North TLV)
├── Mo -2: Nanny Recruitment    ├── Mo 1: Bug fixes, iteration
├── Mo -1: Testing, Audit       ├── Mo 2: My Nannies, profiles
└── Mo 0: Soft Launch (20 fam)  └── Mo 3: PayMe integration begins
         ▲                               ▲
    50 nannies verified            PMF tracking (target: Wk 16)

Q4 (Oct-Dec)
├── Mo 3: PayMe LIVE
├── Mo 4: English UI, Ramat Aviv + Ra'anana expansion
├── Mo 5: Short Notice booking, 200 nannies
└── Mo 6: First B2B conversations, Herzliya prep
         ▲
    500 families, 40 bookings/week

2027
────────────────────────────────────────────────────────────────────────

Q1 (Jan-Mar)                    Q2 (Apr-Jun)
├── Mo 7: Herzliya launch      ├── Mo 10: Seed round closes
├── Mo 8: B2B portal, trust     ├── Mo 11: Multi-city prep
│         graph, 1st B2B $$$    ├── Mo 12: Jerusalem launch
└── Mo 9: Emergency booking     └──────────────────────────────
         ▲                               ▲
    Seed round term sheet          500 nannies, 2,000 families

Q3-Q4 (Jul-Dec)
├── Mo 13-15: Modiin, Netanya expansion
├── Mo 16: AI matching v1
├── Mo 18: Russian UI, Haifa prep
├── Mo 20-26: ████ SCALED BREAKEVEN ████
└── Mo 24: 2,000 nannies, 8,000 families
         ▲
    NIS 300-500K/mo revenue = self-sustaining (solo breakeven at Mo 3-5)
```

---

## DEPENDENCY GRAPH

```
LEGAL FOUNDATION
├── Company registration ──────────────┐
├── Employment bureau license ─────────┤
└── Privacy policy + ToS (DIY) ────────┘
                                       │
                                       ▼
                              MVP DEVELOPMENT (8-12 weeks)
                              ├── React Native + Expo (mobile)
                              ├── NestJS (backend)
                              ├── PostgreSQL + PostGIS (database)
                              ├── Supabase (auth, realtime, RLS)
                              ├── AU10TIX integration (ID verify)
                              ├── Hebrew RTL UI
                              └── IS 5568 accessibility
                                       │
                                       ▼
                              SUPPLY RECRUITMENT (50 nannies)
                              ├── Depends on: AU10TIX integration
                              ├── ID verification + profile review
                              └── Must complete BEFORE family launch
                                       │
                                       ▼
                              MVP LAUNCH (Old North TLV)
                              ├── 50 verified nannies
                              ├── 20 founding families
                              └── Manual payments (Bit)
                                       │
                    ┌──────────────────┤
                    ▼                  ▼
              PMF VALIDATION     PAYME CONTRACT
              (10 bookings/week   (negotiate terms)
               by Week 16)             │
                    │                  │
                    ▼                  ▼
              EXPANSION DECISION  PAYME INTEGRATION
              (Green = expand,    (automated payments)
               Red = pivot/kill)       │
                    │                  │
                    └────────┬─────────┘
                             ▼
                    GEOGRAPHIC EXPANSION
                    ├── Ramat Aviv + Ra'anana (Month 3-6)
                    │   └── Requires: 50+ nannies per area + English UI for Ra'anana
                    ├── Herzliya + opportunistic Florentin (Month 6-9)
                    │   └── Requires: proven expansion playbook
                    ├── Jerusalem (Month 12-14)
                    │   └── Requires: seed funding + English UI
                    └── Multi-city (Month 14-24)
                        └── Requires: seed funding + proven playbook
                             │
                             ▼
                    B2B REVENUE
                    ├── Conversations (Month 3-4)
                    │   └── Requires: consumer traction data
                    ├── Pilot (Month 6-8)
                    │   └── Requires: PayMe + basic reporting
                    ├── First contract (Month 8-9)
                    │   └── Requires: B2B portal v1
                    └── Scale (Month 12+)
                        └── Requires: seed funding + dedicated sales

                    SEED ROUND (Month 6-10)
                    ├── Requires: PMF demonstrated
                    ├── Requires: 200+ nannies, 500+ families
                    ├── IIA matching (50-55% non-dilutive)
                    └── Target: NIS 5-7M total
```

---

## FUNDING TIMELINE

| Step | Timing | Action | Capital (NIS) | Dilution |
|------|--------|--------|:---:|:---:|
| 1 | Month -6 | Apply for IIA Tnufa grant (non-dilutive, but 3-5% royalty on revenue; cannot cover salaries) | 200,000 | 0% |
| 2 | Month -3 to 0 | **Build MVP solo** (AI-assisted, near-zero cost) | ~10-15K out of pocket | 0% |
| 3 | Month 0 | Launch MVP in Old North TLV | — | — |
| 4 | Month 3-6 | Prove PMF. Start angel conversations with traction data. | — | — |
| 5 | Month 6-9 | Seed round NIS 5-7M VC + IIA Seed match (50-55%) | 7,500,000-10,850,000 | 15-20% |
| **TOTAL** | | | **NIS 7.7-11.1M** | **15-20%** |

**Key insight:** Bootstrapping to PMF before raising = stronger negotiating position, less dilution. IIA grants are non-dilutive (free money). Female founder bonus: +10% on all IIA grants.

**Best VC targets for seed:** lool Ventures, Entree Capital, Aleph (consumer marketplace track record with Lemonade, Melio).

---

## CUMULATIVE TARGETS

| Metric | Month 3 | Month 6 | Month 12 | Month 24 |
|--------|:---:|:---:|:---:|:---:|
| Verified nannies | 100 | 200 | 500 | 2,000 |
| Registered families | 200 | 500 | 2,000 | 8,000 |
| Bookings/week | 10 | 40 | 150 | 500+ |
| Premium subscribers | 30 | 100 | 400 | 1,600 |
| B2B contracts | 0 | 0-1 | 3-5 | 15-20 |
| Monthly revenue (NIS) | 5K | 30K | 80K | 300-500K |
| Areas active | 1 (Old North) | 3 (+ Ramat Aviv, Ra'anana) | 5 (+ Herzliya, Jerusalem) | 8-10 |
| Languages | Hebrew | Hebrew + English | +English | +Russian |
| Team | Solo | Solo (consider 1st hire) | Solo → post-seed team | 8-15 FTE |
| Monthly burn (NIS) | ~2K | ~6-13K | 10-20K (solo) / 441K (post-seed) | 500-855K |

---

## CRITICAL DECISIONS CALENDAR

| When | Decision | Data Needed | Options |
|------|----------|------------|---------|
| Week 16 | **Diagnostic checkpoint** | Bookings/week, completion rate, NPS | Green (10+ bookings) → continue + expand. Yellow (5-10) → iterate intensively. Red (<5) → investigate bottleneck, prepare for kill decision. |
| Week 20-24 | **Kill / Pivot decision** | Same + trend direction | If still Red (<5 bookings/week) → interview 20 churned users. Pivot or shut down. |
| Month 3 | **Subscription vs Per-Booking pricing** | Conversion data from manual Bit payments | A/B test NIS 49/mo subscription vs NIS 19-25/booking via PayMe |
| Month 4 | **Expand geography?** | PMF metrics in Old North for 4+ consecutive weeks | Yes → Ramat Aviv + Ra'anana. No → stay concentrated. |
| Month 6 | **Add Emergency booking?** | Supply density in active zones | Only if 50+ available nannies in 5km at any given time |
| Month 6 | **Begin seed fundraising?** | 200+ nannies, 500+ families, 40+ bookings/week, first revenue | Yes → pitch deck + investor meetings. No → extend pre-seed runway. |
| Month 9 | **B2B portal investment?** | At least 3 warm B2B leads, 1 pilot contract | Yes → build B2B dashboard. No → continue manual B2B. |
| Month 12 | **Multi-city expansion?** | Old North + expansion areas all at PMF. Seed round closed. | Yes → Jerusalem + Modiin. No → deepen existing markets. |
| Month 18 | **Russian UI?** | Haifa/Netanya expansion on roadmap, Russian-speaking demand signal | Yes → Russian translation + community. No → defer. |

---

## RISK-ADJUSTED SCENARIOS

### Optimistic Scenario (everything goes right)
- MVP built solo in 8 weeks
- 50 nannies verified by Month -1
- PMF (10 bookings/week) achieved by Week 10
- Seed round (NIS 7M) closed by Month 7
- Solo breakeven at Month 3
- Scaled breakeven at Month 18
- Year 3 revenue: NIS 9.4M (high end)

### Base Scenario (plan of record)
- MVP built solo in 10-12 weeks
- 50 nannies verified by Month 0
- PMF achieved by Week 16
- Seed round closed by Month 9
- Solo breakeven at Month 4-5
- Scaled breakeven at Month 22
- Year 3 revenue: NIS 8.0M (midpoint)

### Pessimistic Scenario (significant headwinds)
- MVP takes 16+ weeks solo (scope creep, technical blockers)
- Only 30 nannies at launch (below density threshold)
- PMF achieved by Week 22 (delayed)
- Seed round closes at Month 12 (smaller: NIS 4M)
- Solo breakeven at Month 6-7
- Scaled breakeven at Month 28
- Year 3 revenue: NIS 5.0M (lower bound)

### Kill Scenario
- < 5 bookings/week by Week 20-24 despite iteration
- Nanny retention < 30% monthly
- Family NPS < 20
- **Action:** Interview 20 churned users. If structural problem (market doesn't want this) → shut down. If execution problem → pivot approach.

---

*This roadmap is a living document. Update at each phase transition based on actual data. Every expansion decision should be data-driven, not calendar-driven. Move to the next phase ONLY when current phase success criteria are met.*

*Companion document: `EMUNI_PRD.md` | Research corpus: `RESEARCH_INDEX.md`*
