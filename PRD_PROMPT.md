# PRD Writing Prompt for Opus 4.6

Copy everything below the line into a fresh Claude Opus 4.6 session (claude.ai, API, or Claude Code agent).

---

## PROMPT START

You are a senior product manager writing a production-grade PRD and roadmap for "Emuni" — an Israeli nanny/babysitter marketplace. You have access to 27 research documents (~15,000 lines) that represent months of validated research. Your job is to synthesize them into a single, actionable PRD that an engineering team can build from.

### YOUR DELIVERABLES

Write TWO documents in a SINGLE output:

**Document 1: EMUNI_PRD.md** — A complete Product Requirements Document
**Document 2: EMUNI_ROADMAP.md** — A phased roadmap with milestones, dependencies, and success criteria

### CONTEXT MANAGEMENT (CRITICAL)

You have ~200K tokens. The research corpus is ~60K tokens. You CANNOT read everything. Follow this exact reading sequence:

**Step 1 — Read the planner brief FIRST (this is your bible):**
```
Read: PRD_PLANNER_BRIEF.md
```
This file contains: reading plan, all 15 founder decisions, legal constraints, revenue model, MVP scope, tech stack, market data, growth strategy, risks, compliance checklist, and the PRD structure template. It extracts the key facts from all 27 documents so you don't have to read most of them.

**Step 2 — Read these 5 files in order (Phase 1 — core context):**
```
1. RESEARCH_INDEX.md — navigation + canonical data points
2. NANNY_PLATFORM_FOUNDER_DECISIONS.md — the 15 decisions that shape everything
3. NANNY_PLATFORM_MASTER_RESEARCH.md — single source of truth
4. NANNY_PLATFORM_MVP_SCOPE.md — RICE-scored feature list (v1/v2/v3)
5. NANNY_PLATFORM_PRD_READINESS.md — PRD structure + open questions
```

**Step 3 — Read these ONLY when writing the specific section that needs them:**
```
- Tech section → NANNY_PLATFORM_TECH_RESEARCH.md
- Booking/matching section → NANNY_PLATFORM_MATCHING_FLOW.md (WARNING: 943 lines — read only Tier 3 / Advance Booking sections for MVP)
- Launch/growth section → NANNY_PLATFORM_LAUNCH_GEOGRAPHY.md
- Background checks section → NANNY_PLATFORM_BACKGROUND_CHECK_RESEARCH.md
- Privacy/compliance section → NANNY_PLATFORM_PRIVACY_AMENDMENT_13_RESEARCH.md
```

**Step 4 — DO NOT read these unless you hit a specific unanswered question:**
```
All other files — trust the extracted data in PRD_PLANNER_BRIEF.md
```

### PRD STRUCTURE

Write the PRD with these exact sections. Each section has specific instructions.

```
EMUNI_PRD.md
============

1. PRODUCT OVERVIEW
   1.1 Vision & Mission
       - Vision: One sentence. What does the world look like if Emuni succeeds?
       - Mission: What Emuni does, for whom, and how it's different.
   1.2 Problem Statement
       - The trust crisis in Israeli childcare (cite: Jerusalem daycare tragedy Jan 2025, gov supervision budget -76%)
       - Current solutions and why they fail (Facebook groups = zero vetting, agencies = expensive + not scalable, Yad2 = classifieds)
       - The parent pain point hierarchy: trust > availability > cost
   1.3 Target Users
       - Write 2 family personas (dual-income TLV parents, single parent) with demographics, goals, frustrations
       - Write 2 nanny personas (university student babysitter, professional career nanny) with demographics, goals, frustrations
       - Include Hebrew names for authenticity (e.g., "Noa, 34, product manager in Ramat HaChayal")
   1.4 Success Metrics & KPIs
       - Define PMF metric: 10 bookings/week by week 12
       - Define kill criteria: if <5 bookings/week by week 16, pivot or shut down
       - Monthly KPIs table: supply (nannies), demand (families), bookings, revenue, NPS, retention

2. LEGAL & COMPLIANCE FRAMEWORK
   2.1 Pure Marketplace Architecture
       - List the 9 Wolt control factors and how Emuni avoids EACH one
       - Include a "Platform MUST NEVER" list (set rates, assign nannies, supervise work, require exclusivity, etc.)
   2.2 Employment Classification Safeguards
       - Family = employer. Platform = technology/matching service.
       - Revenue model (fees, commissions) does NOT affect classification — only control factors matter
       - Employment bureau license: apply proactively as safety net
   2.3 Background Check System
       - Minimum nanny age: 18+ (Youth Labor Law allows 15, but 18+ eliminates parental consent, hour restrictions, minor data issues. Matches Rockmybaby standard.)
       - Two-track system:
         Track A (MANDATORY): Sex offense clearance certificate — platform requests as "covered institution"
         Track B (VOLUNTARY + BADGE): General criminal record cert — nanny uploads, gets "Verified" badge. Platform CANNOT legally require this (2019 Criminal Information Law).
       - Criminal cert is FREE via gov.il. Processing: 7-10 business days online.
       - Platform must engage employment counsel to confirm "covered institution" status
       - THE "NEGLIGENT VETTING TRAP": By conducting background checks, the platform creates a duty of care it wouldn't otherwise have (Civil Wrongs Ordinance, Section 35). Care.com wrongful death lawsuits were based on "negligent vetting" not employer liability. Protection = precise language:
         * NEVER say "safe," "verified nanny," or "we ensure safety"
         * DO say "identity verified," "police clearance certificate obtained," "tools to help families make informed choices"
         * State checks are point-in-time and do not guarantee future behavior
         * Require families to acknowledge responsibility for own due diligence
       - Insurance: ToS + language only at launch. Add E&O + cyber at seed round (Month 6+, ~NIS 15-30K/yr)
   2.4 Privacy Compliance (Amendment 13)
       - Mandatory DPO (outsourced OK, NIS 60-150K/yr)
       - Database registration with PPA before launch
       - 72-hour breach notification
       - Explicit, granular consent per data type (separate for criminal checks, location, payments)
       - AWS il-central-1 for data residency
       - Pen test every 18 months
       - Budget: NIS 140-395K first year
   2.5 Accessibility (IS 5568)
       - Mobile app must comply. NIS 50K penalty per complaint.
       - Build accessible from Day 1 — retrofitting is 5x more expensive
   2.6 Tax & Invoicing
       - VAT: 18%
       - SHAAM e-invoicing mandatory for transactions >NIS 5K (June 2026 deadline)
       - Nanny is a freelancer (עצמאי) — responsible for own tax reporting
       - Platform issues tax invoices for its own fees only

3. USER STORIES & FLOWS
   Write detailed user stories in the format:
   "As a [persona], I want to [action] so that [outcome]"

   Cover these flows with step-by-step descriptions:
   3.1 Family Registration & Onboarding (sign up → profile → search)
   3.2 Nanny Registration & Verification (sign up → ID check → background check → profile live)
   3.3 Search & Discovery (filters: location, availability, rate, language, age group, verified badge)
   3.4 Booking Flow — Advance Booking / Tier 3 ONLY
       - Family sends booking request (date, time, duration, children details, special needs)
       - Nanny receives notification, reviews family profile + reviews
       - Nanny accepts/declines/proposes alternative
       - Both parties confirm → booking confirmed
       - Reminder notifications (24hr, 2hr before)
       - Post-booking: both rate each other
   3.5 Messaging (in-app only in v1, WhatsApp integration deferred)
   3.6 Reviews & Ratings (mutual: family rates nanny AND nanny rates family)
   3.7 Subscription & Payment
       - Free tier: browse all profiles fully (photos, ratings, reviews), basic filters (location, rate), 1 booking/month, in-app messaging
       - Premium (NIS 49/mo): unlimited bookings, advanced filters (language, experience, schedule match), priority in nanny's inbox, favorites list + 1-tap rebook, Founding Member badge, priority support
       - Founding Member (NIS 29/mo, locked forever, first 200 families): all Premium features + early access
       - Per-contact: NIS 19 (for non-subscribers who want to unlock a specific nanny's contact)
       - v1: manual Bit invoicing. v2: PayMe integration.
   3.8 Cancellation & No-Show Policy
       - v1: Reliability score only (no financial penalties — no payment mechanism)
       - Late cancel (<24hrs): reliability score impact
       - No-show: significant score impact + account review
       - 3 late cancellations in 30 days: supportive outreach + lower search ranking (NOT punishment)
       - No financial penalties for nannies (Wolt lesson: financial penalties destroy supply-side trust)
       - v2 (with PayMe): add financial penalties per MATCHING_FLOW spec (25-100% based on timing)

4. FEATURE SPECIFICATION (MVP)
   4.1 In-Scope Features
       - Create a detailed feature table with columns: Feature | Priority (P0/P1/P2) | Description | Acceptance Criteria
       - P0 = must have for launch, P1 = should have, P2 = nice to have
       - Use the RICE scores from MVP_SCOPE.md to inform prioritization
   4.2 Out-of-Scope (v2/v3)
       - List every deferred feature with the reason for deferral and target version
       - Include: emergency booking, trust graph, B2B portal, nanny Pro tier, AI matching, insurance, WhatsApp deep integration
   4.3 Non-Functional Requirements
       - Performance: app launch <2s, search results <500ms, booking confirmation <3s
       - Security: OWASP Top 10 compliance, encrypted PII at rest + in transit, RLS on all user data
       - Availability: 99.5% uptime SLA
       - Scalability: architecture must support 10K concurrent users by Month 12
       - Accessibility: IS 5568 Level AA equivalent
       - Localization: Hebrew RTL first, i18n architecture from Day 1, English at Month 4-6

5. TECHNICAL ARCHITECTURE
   5.1 Stack Overview (table: layer → technology → justification)
   5.2 Key Database Entities
       - Users (families + nannies), Profiles, Children, Bookings, Reviews, Messages, Subscriptions, BackgroundChecks, Payments
       - For each: list key fields, relationships, and any PostGIS columns
   5.3 API Design Principles
       - RESTful, versioned (/api/v1/), JWT auth, rate limiting
       - Key endpoints list (don't write full API docs, just the endpoint map)
   5.4 Geospatial Search
       - PostGIS for nanny search by location
       - Radius search from family's address
       - Sort by distance + availability + rating
   5.5 Real-time Messaging
       - Supabase Realtime for in-app messaging
       - Push notifications (Firebase Cloud Messaging)
   5.6 Authentication
       - Phone number + OTP (Israeli mobile numbers)
       - Supabase Auth
       - No social login in v1 (simplify)
   5.7 Data Residency
       - AWS il-central-1 (Israel region)
       - All PII stored in Israel (Amendment 13 compliance)
       - Supabase self-hosted or confirm data residency

6. REVENUE MODEL & PRICING
   6.1 Tier Comparison Table
       | Feature | Free | Premium (NIS 49/mo) |
       - Include all differences
   6.2 Transaction Fees (v2)
       - 12-15% on booking value, charged to families
       - Average booking: NIS 200-300
   6.3 B2B (v2+, Month 6)
       - Corporate childcare benefits: NIS 2K-8K/mo per contract
       - Define the hook: what data/traction triggers B2B sales outreach
   6.4 Payment Architecture
       - v1: manual Bit invoicing (first 50 users)
       - v2: PayMe integration (marketplace splits, recurring billing, SHAAM compliance)
       - Include money flow diagram (text-based)
   6.5 Financial Projections
       - Y1: NIS 640K-820K | Y2: NIS 2.5-3.5M | Y3: NIS 7.6-9.4M
       - Breakeven: Month 20-26
       - DO NOT recalculate — use these canonical verified numbers

7. GROWTH & LAUNCH PLAN
   7.1 Pre-Launch (Month -3 to 0)
       - Supply recruitment plan: how to get 50 nannies in Old North TLV
       - Founder-led: campus visits, Facebook groups, nanny referral bonus (NIS 100)
       - Background check all 50 before launch
       - Soft-launch with 20 founding families
   7.2 Launch (Month 0-3)
       - Old North TLV only
       - "Bring Your Nanny" mechanic explained
       - PMF tracking: 10 bookings/week by week 12
   7.3 Expansion Phases
       - Phase 2 (Mo 3-6): Florentin/Neve Tzedek, English UI, PayMe
       - Phase 3 (Mo 6-12): Ra'anana, B2B, WhatsApp, trust graph
       - Phase 4 (Mo 12-24): Multi-city, AI matching, breakeven
   7.4 PMF Metrics & Kill Criteria
       - Green: 10+ bookings/week, 40%+ monthly retention, NPS 50+
       - Yellow: 5-10 bookings/week, 25-40% retention
       - Red/Kill: <5 bookings/week by week 16

8. ROADMAP
   This section becomes EMUNI_ROADMAP.md — write it as a standalone document.

9. RISK REGISTER
   - Table: Risk | Likelihood | Impact | Mitigation | Owner
   - Cover: legal, market, technical, operational, financial risks
   - Include the specific risks from PRD_PLANNER_BRIEF.md Section 9

10. APPENDICES
    10.1 Research Corpus Reference (link to RESEARCH_INDEX.md)
    10.2 Canonical Data Points (copy the table from RESEARCH_INDEX.md)
    10.3 Glossary of Hebrew Legal/Business Terms
         - Include: teudat yosher, osek murshe, osek patur, SHAAM, mas hachnasa, bituach leumi, etc.
    10.4 Open Questions (from PRD_READINESS.md)
```

### ROADMAP STRUCTURE (EMUNI_ROADMAP.md)

```
EMUNI_ROADMAP.md
================

For each phase, include:
- Phase name + timeline
- Goals (what success looks like)
- Features (bulleted, with P0/P1/P2 tags)
- Dependencies (what must be true before this phase starts)
- Team requirements (who you need)
- Key milestones with dates
- Success criteria (measurable)
- Budget estimate

Phases:
1. PRE-LAUNCH (Month -3 to 0)
   - Company formation, IIA application, co-founder search
   - MVP development (8-12 weeks)
   - Supply recruitment (50 nannies)
   - Background checks
   - Soft launch (20 families)

2. MVP LAUNCH (Month 0-3)
   - Public launch in Old North TLV
   - PMF tracking
   - Manual payments (Bit)
   - Target: 100 nannies, 200 families, 10 bookings/week

3. TRACTION (Month 3-6)
   - PayMe integration
   - English UI
   - Geographic expansion (Florentin)
   - Emergency booking (if density allows)
   - First B2B contract
   - Target: 200 nannies, 500 families

4. GROWTH (Month 6-12)
   - Ra'anana expansion
   - B2B corporate portal
   - WhatsApp integration
   - Trust graph / community recommendations
   - Seed round (NIS 5-7M)
   - Target: 500 nannies, 2,000 families

5. SCALE (Month 12-24)
   - Multi-city (Herzliya, Netanya, Jerusalem)
   - AI matching algorithm
   - Insurance products
   - Breakeven at Month 20-26
   - Target: 2,000 nannies, 8,000 families

Include a visual timeline (text-based Gantt chart or milestone diagram).
Include a dependency graph showing what blocks what.
```

### QUALITY REQUIREMENTS

1. **Be specific, not generic.** Every claim must reference Israeli context. Don't write "conduct background checks" — write "request sex offense clearance certificate via Israel Police as a covered institution under the 2001 law."

2. **Be actionable.** An engineer reading Section 4 should know exactly what to build. A founder reading Section 7 should know exactly what to do next Monday.

3. **Use Hebrew terms where appropriate** with English translations. This is an Israeli product — the PRD should feel Israeli.

4. **Include edge cases.** What happens when a nanny cancels 1 hour before? What happens when a family disputes a charge? What if a nanny's background check reveals a record?

5. **Numbers must match the canonical data.** Use ONLY the verified figures from the research. Do not invent or recalculate projections.

6. **Write for two audiences:** (a) the technical co-founder who will build the MVP, and (b) potential investors who may read this during due diligence.

7. **Target length:** PRD should be 2,000-3,000 lines. Roadmap should be 400-600 lines. Do not be brief — this is the single document the team will build from.

### WORKING DIRECTORY

All files are in: `C:\Users\t2tec\projects\Israeli-Premium-App-Research\`

Write your output to:
- `C:\Users\t2tec\projects\Israeli-Premium-App-Research\EMUNI_PRD.md`
- `C:\Users\t2tec\projects\Israeli-Premium-App-Research\EMUNI_ROADMAP.md`

## PROMPT END
