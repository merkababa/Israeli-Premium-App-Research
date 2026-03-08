# EMUNI — Product Requirements Document

**Version:** 1.2
**Date:** March 8, 2026
**Author:** Product Team (synthesized from 27 research documents, 18+ research agents, 250+ sources)
**Status:** FINAL — Ready for Engineering & Investor Review
**Changelog:**
- v1.2 — Applied technical decision deltas: Didit IDV (replaces AU10TIX), Drizzle ORM, PostHog analytics + error tracking (replaces Mixpanel + Sentry), Morning invoicing NIS 45/mo, Turborepo + pnpm monorepo. Updated all cost estimates.
- v1.1 — Applied 59-item review fixes (11 CRITICAL, 24 HIGH, 18 MEDIUM, 6 LOW). See `EMUNI_PRD_REVIEW_MARCH2026.md` for full review.
**Companion Document:** `EMUNI_ROADMAP.md`

---

## TABLE OF CONTENTS

1. [Product Overview](#1-product-overview)
2. [Legal & Compliance Framework](#2-legal--compliance-framework)
3. [User Stories & Flows](#3-user-stories--flows)
4. [Feature Specification (MVP)](#4-feature-specification-mvp)
5. [Technical Architecture](#5-technical-architecture)
6. [Revenue Model & Pricing](#6-revenue-model--pricing)
7. [Growth & Launch Plan](#7-growth--launch-plan)
8. [Risk Register](#8-risk-register)
9. [Appendices](#9-appendices)

---

# 1. PRODUCT OVERVIEW

## 1.1 Vision & Mission

**Vision:** Every Israeli family finds trusted childcare with confidence — and every qualified caregiver builds a career with dignity.

**Mission:** Emuni is a Hebrew-first mobile marketplace that connects Israeli families with identity-verified babysitters and nannies. We replicate the power of the Israeli hamlatza (המלצה — personal recommendation) culture digitally, providing verified trust signals that make finding childcare as reliable as asking your best friend. We are a pure technology platform — never the employer, always the enabler.

## 1.2 Problem Statement

### The Trust Crisis in Israeli Childcare

Israeli parents face a broken childcare discovery system at a moment of national crisis:

**The January 2026 Jerusalem daycare tragedy** — two babies died from overcrowding and dehydration at an unlicensed daycare facility (January 19, 2026) — exposed systemic failures in Israel's childcare supervision infrastructure. The government's daycare supervision budget has **collapsed by 76%**, leaving families to fend for themselves.

There is **no standardized national system** for background-checking private nannies and babysitters. The Daycare Supervision Law (2018) covers facilities with 7+ children, but an estimated 200,000+ families who hire private in-home caregivers (derived from ~270K addressable households with children under 12 in metro areas, CBS data) have zero institutional support.

### Current Solutions and Why They Fail

| Current Solution | How It Works | Why It Fails |
|-----------------|-------------|-------------|
| **Facebook/WhatsApp groups** | Parents post "looking for babysitter" in neighborhood groups | Zero vetting, ephemeral, unstructured, impossible to search history, no accountability |
| **Helpbook.co.il** | Israel's largest babysitter job board (since 2014) | Static listings, no real-time booking, no background checks, Android-only app (Ionic, no iOS), no verification |
| **Babysitter.co.il** | Job board operating since 2002 | Dated UI, tiny scale, no vetting, no trust signals |
| **Babysits.co.il** | European marketplace with Israeli presence | 89 sitters in Tel Aviv, not Israel-optimized, optional background checks, generic |
| **Agencies** (Rockmybaby, City Sitters, Nanny Poppins) | Manual matching, phone/WhatsApp-based | Premium pricing, minimum booking requirements, not scalable, opaque processes |
| **Yad2** | Classifieds | No verification, no reviews, no childcare-specific features |
| **Word of mouth** | Ask friends and family | Limited to personal network, not scalable, excludes olim and newcomers |

**No platform in Israel offers:** real-time booking + identity verification + background certificate badges + mobile-first marketplace + Hebrew UI + community trust signals.

### The Parent Pain Point Hierarchy

Research across 250+ sources confirms the priority order:

1. **Trust** (Critical) — "Many parents end up simply not going out as couples for months" — Jerusalem Post. Parents would rather cancel plans than hire an unknown babysitter.
2. **Availability** (High) — Last-minute care is nearly impossible. Only Rockmybaby offers emergency booking at tiny scale.
3. **Cost** (Medium) — Childcare is one of the largest household expenses, consuming up to 30% of family budget in Tel Aviv. But parents will pay MORE for verified trust.

## 1.3 Target Users

### Family Persona 1: Noa & Eyal — The Dual-Income Tech Parents

| Attribute | Detail |
|-----------|--------|
| **Names** | Noa (נעה), 34, and Eyal (אייל), 36 |
| **Location** | Old North Tel Aviv (Basel Street area) |
| **Occupation** | Noa: Product Manager at a Ramat HaChayal tech company. Eyal: Software engineer at a fintech startup. |
| **Children** | Yonatan (יונתן), 4, in gan. Shira (שירה), 18 months, in mishpachton. |
| **Household income** | NIS 38,000/month combined |
| **Childcare spend** | NIS 6,500/month (mishpachton + gan + occasional babysitter) |
| **Current babysitter method** | Asks in the "Old North Moms" WhatsApp group. Has 2-3 babysitters she trusts from word-of-mouth but they're not always available. |
| **Frustrations** | (1) When her regulars are busy, she has no backup and cancels plans. (2) She once hired someone from Facebook who was unreliable — showed up 30 minutes late with no explanation. (3) She doesn't know if her babysitters have ever been background-checked. (4) Finding a new babysitter takes days of WhatsApp back-and-forth. |
| **Goals** | Find 3-4 trusted, verified babysitters she can book with confidence on short notice. Know they've been checked. Stop the WhatsApp runaround. |
| **Willingness to pay** | NIS 49/month for unlimited access to verified babysitters — "less than one hour of babysitting." |
| **Tech behavior** | iPhone user. Uses Wolt, Gett, Monday.com daily. Expects polished Hebrew UI. Will share good finds on WhatsApp immediately. |

### Family Persona 2: Sarah — The Single Anglo Mom

| Attribute | Detail |
|-----------|--------|
| **Name** | Sarah, 31 |
| **Location** | Florentin, Tel Aviv (moving from Old North due to rent) |
| **Origin** | Made aliyah from New York 3 years ago via Nefesh B'Nefesh |
| **Occupation** | Content marketing manager (remote, US company) |
| **Children** | Emma (אמה), 2.5 years old |
| **Household income** | NIS 18,000/month (USD salary, favorable exchange) |
| **Childcare spend** | NIS 3,800/month (mishpachton) + NIS 800-1,200/month on babysitters |
| **Current babysitter method** | Asks in Janglo Facebook groups and "Secret Tel Aviv." Struggles with Hebrew-only WhatsApp groups. Has one reliable babysitter found through a friend. |
| **Frustrations** | (1) Hebrew-only babysitter posts are hard to navigate. (2) As a single parent, she has no partner to stay home — she MUST find care or miss work. (3) She doesn't have the deep Israeli social network for hamlatzot. (4) She tried Babysits but there were only 3 sitters near her. |
| **Goals** | A bilingual platform where she can browse verified sitters, read reviews in English, and book quickly. Needs reliability above all. |
| **Willingness to pay** | NIS 49/month — "I paid $30/month for Care.com in New York, this is normal." |
| **Tech behavior** | iPhone. Fluent in app-based services. Active on Facebook groups, Janglo, Anglo-List. Will leave detailed English reviews. |

### Nanny Persona 1: Maya — The University Student Babysitter

| Attribute | Detail |
|-----------|--------|
| **Name** | Maya (מאיה), 22 |
| **Location** | Lives near TAU campus, serves Old North and Ramat Aviv |
| **Background** | Completed Sherut Leumi at a gan in Ramat Gan. Now studying Education at Tel Aviv University. |
| **Experience** | 3 years babysitting (during and after Sherut Leumi). Comfortable with ages 1-6. Basic first aid from Sherut Leumi training. |
| **Hourly rate** | NIS 55/hour |
| **Availability** | Sunday-Thursday evenings (after classes), Thursday nights, some Fridays |
| **Current method** | Gets babysitting jobs through WhatsApp group referrals from families she's worked with. Also posted on Helpbook once. |
| **Frustrations** | (1) Income is inconsistent — some weeks 3 bookings, some weeks zero. (2) She wants more families but doesn't know how to market herself beyond word-of-mouth. (3) She's uncomfortable sharing her phone number on Facebook groups with strangers. (4) One family paid her late (Bit transfer 2 weeks later). |
| **Goals** | Steady stream of bookings (3-4/week). Build a reputation that follows her. Feel safe knowing who she's going to. |
| **What she needs from platform** | Free to join (she can't afford fees). Easy profile setup. Ability to set her own rate and availability. Reviews she can show future families. Background check she doesn't have to pay for. |

### Nanny Persona 2: Svetlana — The Professional Career Nanny

| Attribute | Detail |
|-----------|--------|
| **Name** | Svetlana (סבטלנה), 38 |
| **Location** | Bat Yam, serves Tel Aviv and Herzliya |
| **Background** | Made aliyah from Ukraine 8 years ago. Early childhood education degree from Kyiv. Fluent in Hebrew, Russian, and basic English. |
| **Experience** | 12 years professional nanny experience (6 in Ukraine, 6 in Israel). Has worked with 2 families in Herzliya Pituach long-term. Magen David Adom first aid certified. Special needs experience (worked with an autistic child for 2 years). |
| **Hourly rate** | NIS 70/hour (premium rate justified by experience and certifications) |
| **Availability** | Full-time availability. Currently between long-term positions. Takes babysitting jobs to fill gaps. |
| **Current method** | Found previous positions through a nanny agency (Rockmybaby) and personal referrals. Dislikes the agency model — they take a cut and she has no control. |
| **Frustrations** | (1) Agencies take her rate and mark it up — families pay NIS 100/hr but she gets NIS 65. (2) She has no online presence — all her reputation is word-of-mouth. (3) Finding new families between positions takes weeks. (4) She wants to build a professional profile showcasing her certifications and experience. |
| **Goals** | Build a professional online presence. Get booked directly by families at her full rate. Showcase her special needs experience and certifications. Eventually find a new long-term position through the platform. |
| **What she needs from platform** | Professional profile with certifications displayed. Keep 100% of her rate. Be found by families looking for premium, experienced nannies. Russian language support eventually. |

## 1.4 Success Metrics & KPIs

### Product-Market Fit Metric

**North Star: 10 completed bookings per week by Week 12.**

A "completed booking" means: family sent request → nanny accepted → session happened → both parties confirmed.

### Kill Criteria

| Signal | Threshold | Timeline | Action |
|--------|-----------|----------|--------|
| **RED — Kill/Pivot** | < 5 bookings/week | By Week 20-24 | Stop development. Interview 20 churned users. Pivot or shut down. Babysitting is low-frequency (1-4x/month); solo founder with NIS 2K/mo burn can afford more time. |
| **YELLOW — Concern** | 5-10 bookings/week | Week 16 (diagnostic) | Investigate bottleneck (supply? demand? UX?). Intensive iteration. |
| **GREEN — PMF** | 10+ bookings/week | By Week 16 | Continue. Prepare for Phase 2 expansion. |

### Monthly KPI Dashboard

| Category | KPI | Month 1 | Month 3 | Month 6 | Month 12 |
|----------|-----|---------|---------|---------|----------|
| **Supply** | Verified nannies | 50 | 100 | 200 | 500 |
| **Supply** | Active nannies (1+ booking/month) | 20 | 50 | 120 | 300 |
| **Supply** | Nanny NPS | — | 40+ | 45+ | 50+ |
| **Demand** | Registered families | 20 | 200 | 500 | 2,000 |
| **Demand** | Active families (1+ booking/month) | 10 | 80 | 200 | 800 |
| **Demand** | Family NPS | — | 40+ | 45+ | 50+ |
| **Bookings** | Bookings/week | 3 | 10 | 40 | 150 |
| **Bookings** | Booking completion rate | 50%+ | 60%+ | 70%+ | 75%+ |
| **Bookings** | Repeat booking rate (30-day) | — | 30%+ | 40%+ | 50%+ |
| **Revenue** | Monthly revenue (NIS) | 0 (soft launch) | 5K | 30K | 80K |
| **Revenue** | Premium subscribers | 0 | 30 | 100 | 400 |
| **Revenue** | Premium conversion rate | — | 15%+ | 20%+ | 25%+ |
| **Retention** | Family monthly retention | — | 60%+ | 65%+ | 70%+ |
| **Retention** | Nanny monthly retention | — | 70%+ | 75%+ | 80%+ |
| **Growth** | Organic acquisition % | — | 40%+ | 50%+ | 60%+ |

---

# 2. LEGAL & COMPLIANCE FRAMEWORK

This section defines the **non-negotiable legal constraints** that shape every product decision. These are not suggestions — they are architectural requirements.

## 2.1 Pure Marketplace Architecture

Emuni is a **pure technology marketplace**. The family is ALWAYS the employer. The platform is NEVER the employer.

### The 9 Wolt Control Factors — And How Emuni Avoids Each One

The Tel Aviv Regional Labor Court (Case 35327-08-20, Judge Ariella Gilzer-Katz, August 3, 2022) ruled Wolt is the employer of all its couriers based on 9 control factors. Wolt faces millions in retroactive social benefits. The appeal is pending at the National Labor Court. Here is how Emuni structurally avoids every factor:

| # | Wolt's Fatal Mistake | Why It Triggered Classification | Emuni's Architecture |
|---|---------------------|-------------------------------|---------------------|
| 1 | **Set courier pay rates unilaterally** | Rate-setting = employer control over compensation | Nannies set their own hourly rate. Families and nannies negotiate directly. Platform never suggests, caps, or adjusts rates. |
| 2 | **App replaced employer instructions (dispatch)** | Algorithmic dispatch = giving work orders | Nannies browse requests and choose which to accept. No dispatching. No assignment. No "you must take this job." |
| 3 | **Real-time GPS supervision** | Live tracking = workplace supervision | Zero monitoring during work sessions. No GPS tracking. No check-ins. No live location sharing (optional nanny check-in is nanny-initiated, not platform-required). |
| 4 | **Required exclusive freelancer registration** | Exclusivity = economic dependence | Zero exclusivity. Nannies explicitly encouraged to work anywhere — other platforms, agencies, direct arrangements. ToS states: "You are free to provide services through any channel." |
| 5 | **Owned entire customer relationship** | Customer belongs to platform, not worker | Families and nannies exchange direct contact (phone, WhatsApp) after booking confirmation. Platform facilitates discovery; relationship belongs to both parties. |
| 6 | **Couriers couldn't negotiate rates** | No negotiation = employer dictates terms | Direct negotiation between family and nanny. Platform provides nanny's stated rate as a starting point. Families can discuss, nannies can adjust. |
| 7 | **Branded equipment/uniforms** | Branding = integration into business | No uniforms. No branded equipment. No "Emuni" t-shirts. Nannies present as independent professionals. |
| 8 | **Algorithm-driven de facto scheduling** | Algorithmic scheduling = controlling work hours | Nannies set their own availability calendar. No minimum hours. No availability requirements. No penalties for being unavailable. |
| 9 | **Couriers were core to business** | Workers integral to service delivery | Emuni is a technology/matching platform. We provide the marketplace infrastructure. The childcare service is provided by independent nannies directly to families. |

**Critical legal finding:** The Wolt court mentioned Wolt's revenue model (25% restaurant commission) only as **context**, never as a classification factor. The ruling was entirely about **control**. There is no Israeli case law where a platform's fee structure itself led to employer classification. Our fee model (subscriptions, transaction fees) is legally irrelevant to classification risk.

### Platform MUST NEVER List

The platform MUST NEVER, under any circumstances:

1. **Set, suggest, or cap nanny rates** — not even "recommended rates" or "market average" displays that could be construed as guidance
2. **Assign or dispatch nannies to families** — families choose; nannies accept or decline
3. **Create schedules or require availability** — no minimum hours, no mandatory availability windows
4. **Monitor work in real time** — no GPS tracking, no check-ins, no live session monitoring
5. **Handle nanny wages** — platform fee is separate from nanny's payment. Family pays nanny directly.
6. **Provide mandatory training** — optional resources are fine; required training programs create an employer relationship
7. **Require exclusivity** — no non-compete, no "Emuni-only" language
8. **Provide work equipment or uniforms** — no branded items for nannies
9. **Discipline nannies for work quality** — handle safety violations only; work quality feedback is through reviews, not platform action
10. **Penalize nannies for declining work** — rejection has zero negative consequences
11. **Unilaterally change compensation** — nannies control their rates at all times
12. **Require personal service** — nannies may send qualified substitutes

## 2.2 Employment Classification Safeguards

### Legal Classification Target

| Category | License Required? | Employer Obligations? | Our Target |
|----------|:-:|:-:|:-:|
| Manpower Contractor (קבלן כוח אדם) | Yes | Yes — full employer | **AVOID** |
| Private Employment Bureau (לשכת תעסוקה פרטית) | Yes | No — but can't charge job seekers | **GET LICENSE AS SAFETY NET** |
| Broker/Intermediary | Depends | No | Acceptable |
| Classifieds/Marketplace | No | No | **PRIMARY TARGET** |

**Key actions:**
- **Family = employer.** All employment obligations (Bituach Leumi registration, social benefits, pension after eligible period) are on the family. Platform provides educational tools but never assumes the employer role.
- **Employment Bureau License:** Apply proactively as a safety net. Even though a pure marketplace likely doesn't require one, the license eliminates ambiguity. Cost: estimated NIS 5,000-15,000 for application and legal counsel.
- **Fee structure is irrelevant to classification.** How we charge (subscription, transaction fee, flat fee) has ZERO impact on whether we're classified as an employer. Only the 9 control factors matter. This is confirmed by Israeli precedent: Fiverr (20% seller + 5.5% buyer fee, 14+ years, no classification), Gett (subscription + per-ride %, 10+ years, no classification), Bubble UK (25% first sit / 6% repeat, 8+ years, no classification).

### The Real Fee Constraint — Employment Service Law (1959)

| Who We Charge | Legal? | Basis |
|:---:|:---:|---|
| **Families** (any amount, any % or flat fee) | **YES** | No restriction on employer-side fees |
| **Nannies** (listing/subscription/commission) | **RISKY** | If classified as employment bureau, violates prohibition on charging job seekers. Penalty: substantial financial penalties per violation. |
| **Nannies** for "verification services" | **GRAY ZONE** | Arguable as tech service, not placement fee. Get attorney sign-off first. |

**Decision: Charge families only. All revenue streams are family-side. Nanny-side fees deferred indefinitely until attorney confirms legality.**

## 2.3 Background Check System

### Minimum Nanny Age: 18+

While Israel's Youth Labor Law (Amendment 9b) permits babysitting from age 15, Emuni requires all nannies to be **18 or older** because:
- Eliminates parental consent requirements for registration
- Eliminates Youth Labor Law hour/night restrictions we'd need to enforce in UX
- Eliminates medical exam requirements before employment
- Eliminates minor data processing complexity under the Legal Capacity and Guardianship Law
- Matches the professional industry standard (Rockmybaby Israel: 18+)
- Simplifies Amendment 13 compliance (no children's data as data subjects on the nanny side)

### Background Verification System

The 2019 Criminal Information and Rehabilitation of Offenders Law (חוק המידע הפלילי ותקנת השבים, 5779-2019) **prohibits** most employers from requesting criminal records. The platform cannot legally require background checks from nannies. However, nannies can voluntarily provide their own criminal record certificate as a trust signal.

#### Voluntary Background Certificate Badge

| Aspect | Detail |
|--------|--------|
| **Legal basis** | 2019 Criminal Information Law — nannies may voluntarily share their own certificate; platform cannot request or require it |
| **Who obtains** | The nanny, independently, via gov.il (online) or police station (in-person) |
| **What it shows** | Active criminal convictions (not expunged), pending cases. Does NOT show foreign convictions. |
| **Cost** | **FREE** for domestic use (NIS 0). NIS 35 for apostille (international use). |
| **Processing time** | 7-10 business days (online), 2-4 weeks (in-person) |
| **Platform role** | Nanny uploads the digital PDF. Platform performs visual verification. Profile receives "הגיש/ה אישור רקע" (Submitted Background Certificate) badge. |
| **Language** | Platform frames this as: "Enhance your profile with a background certificate badge. Families prefer nannies who submit certificates." — NOT as a requirement. |
| **Why voluntary** | The 2019 law makes it a criminal offense for unauthorized employers to REQUEST criminal information. The platform cannot legally require this. But nannies can voluntarily provide it. |
| **Renewal** | Badge expires after 12 months; nanny prompted to renew. |

**Expiry handling:** When a nanny's voluntary background certificate badge expires, the badge simply disappears — profile remains visible but without the badge. The nanny receives a push notification: "Your background certificate badge has expired. Upload a new certificate to restore it."

### The "Negligent Vetting Trap" — Critical Language Rules

**By conducting background checks, the platform creates a duty of care it would not otherwise have** (Civil Wrongs Ordinance, פקודת הנזיקין, Section 35). The Care.com wrongful death lawsuits were based on "negligent vetting" — NOT employer liability. Care.com's $8.5M FTC settlement (2024) was for deceptive earnings claims, inflated job listings, and dark-pattern cancellation practices — NOT safety claims.

**Protection is through precise language, not safety guarantees:**

| NEVER Say | ALWAYS Say |
|-----------|-----------|
| "Safe nanny" / "בייביסיטר בטוח/ה" | "Identity verified" / "זהות מאומתת" |
| "Verified nanny" / "בייביסיטר מאומת/ת" | "Submitted background certificate" / "הגיש/ה אישור רקע" |
| "We ensure your child's safety" | "Tools to help families make informed choices" / "כלים לעזור למשפחות לקבל החלטות מושכלות" |
| "Background-checked and safe" | "Background verification completed on [date]" |
| "Trusted caregiver" | "Completed platform verification process" |

**Additional requirements:**
- All checks described as "point-in-time" — do not guarantee future behavior
- Families must acknowledge in ToS that they are responsible for their own due diligence
- Platform provides tools and information; families make the hiring decision
- Criminal record certificates only cover offenses committed IN ISRAEL — foreign convictions are a known gap, disclosed to families
- **Foreign conviction self-attestation:** During registration, nannies are asked: "Have you ever been convicted of a crime outside of Israel?" (Yes/No self-declaration). This is NOT "requesting criminal information" under the 2019 law — it is a voluntary self-declaration. A "Yes" answer triggers manual admin review before profile goes live.

### Background Verification Budget

| Item | Cost per Nanny | For 100 Nannies |
|------|:---:|:---:|
| Criminal record certificate (nanny obtains voluntarily) | Free | Free |
| Didit ID verification (document + selfie match) | **NIS 0** (500 free/mo) | **NIS 0** (within free tier) |
| Staff time for manual review | Internal | Internal |
| **Total per nanny (ongoing)** | **NIS 0** | **NIS 0** |

**Decision: Platform pays for ID verification. Background certificates are free and nanny-initiated.** Didit provides 500 free verifications/month (document + biometric face match + liveness detection, with native Teudat Zehut support and an Expo plugin). At launch scale (50 nannies), this is entirely free. Beyond 500/month: $0.30/check. Fallback provider: Shufti Pro ($0.20/check, confirmed TZ support). "Every nanny on Emuni is identity-verified" is the #1 marketing differentiator. Nannies who also submit a voluntary background certificate get a visible badge.

### Insurance Strategy

| Phase | Coverage | Cost |
|-------|----------|------|
| **Launch (Month 0-6)** | ToS + precise language + family acknowledgment of responsibility | NIS 0 |
| **Seed Round (Month 6+)** | Add E&O (Errors & Omissions) + Cyber Liability insurance | ~NIS 15,000-30,000/year |
| **Scale (Month 12+)** | Explore group nanny liability policy | TBD |

## 2.4 Privacy Compliance (Amendment 13)

Amendment 13 to the Privacy Protection Law (effective August 14, 2025) is Israel's most significant privacy overhaul in 40+ years. The PPA is in **active enforcement mode** — the grace period ended in late 2025.

### Why Emuni is a High-Risk Data Controller

| Data Type | Classification |
|-----------|---------------|
| Criminal record certificates | **Especially Sensitive Data** |
| Location data (nanny/family addresses) | **Especially Sensitive Data** |
| Financial/payment information | **Especially Sensitive Data** |
| Background check results | **Especially Sensitive Data** |
| ID documents (Teudat Zehut scans) | Personal Data (high sensitivity) |
| Children's information (names, ages, needs) | Personal Data (heightened duty of care) |

### Mandatory Requirements

| Requirement | Implementation |
|-------------|---------------|
| **Data Protection Officer (DPO)** | **Deferred until ~500-1,000 users or if mandatory background checks (Track A) are ever added.** Amendment 13 triggers DPO for entities whose "main activity" is processing sensitive data at "significant scale." At launch with ~50 users, voluntary-only background certificates, and primarily ID verification data, the platform does not meet the threshold. Revisit when user base grows or data processing profile changes. When appointed, must be outsourced (NIS 60,000-150,000/year), report to CEO, cannot also serve as CISO. |
| **Database registration** | At launch (<10K users): not required. At 10K+ users (if classified as data broker): register with PPA. At 100K+ users with sensitive data: mandatory notification to PPA. Maintain a Database Definition Document from Day 1 regardless. |
| **Breach notification** | Notify PPA within 72 hours of any severe security incident. Prepare notification templates before launch. |
| **Explicit consent** | Separate, granular consent for EACH processing purpose: criminal record processing, location data, payment processing, profile sharing with matches. Blanket/bundled consent is prohibited for Especially Sensitive Data. |
| **Data minimization** | Store only verification results (pass/fail + date), NOT raw criminal record certificates. Collect only data necessary for matching. Delete data when no longer needed. |
| **Encryption** | AES-256 at rest (AWS RDS default). TLS 1.3 in transit. Enhanced encryption for Especially Sensitive Data. |
| **Access controls** | Row-Level Security (Supabase RLS). Role-based access. Comprehensive audit logging for all sensitive data access. |
| **Penetration testing** | Every 18 months for medium/high security databases. Budget: NIS 15,000-40,000 per test. |
| **Data subject rights** | Build mechanisms for access, correction, and deletion requests. No general "right to be forgotten" under Israeli law, but deletion required when data is inaccurate, outdated, or unnecessary. |
| **Cross-border transfers** | AWS il-central-1 (Israel) for all data. If using any non-Israeli cloud services: data processing agreements required, prohibition on onward transfer, documented risk assessment. |

### Privacy Compliance Budget (Solo Bootstrapper)

| Item | First Year | Ongoing Annual | Notes |
|------|:---:|:---:|---|
| Outsourced DPO | NIS 0 | NIS 0 | Deferred until ~500-1,000 users |
| Initial legal counsel | NIS 0 | — | DIY from templates at launch; revisit when revenue exists |
| Penetration testing | NIS 0 | NIS 15,000-40,000 | Required every 18 months; first test due ~Month 18 |
| Privacy compliance tools | NIS 0-5,000 | NIS 0-5,000 | Free/open-source tools initially |
| **TOTAL (bootstrapper)** | **NIS 0-5,000** | **NIS 15,000-45,000** |

*When DPO appointment is triggered (~500-1,000 users), add NIS 60-150K/year. When scaling post-seed, add legal counsel, pen testing, and compliance tooling per the full budget model.*

### Penalty Exposure

| Violation | Penalty |
|-----------|---------|
| Administrative fines (general) | Up to 5% of annual turnover |
| Small business annual cap | 140,000 NIS/year |
| Security violations | 80,000-320,000 NIS per violation |
| Missing required DPO | 20,000-40,000 NIS minimum |
| Statutory damages (court, per individual) | Up to 10,000 NIS (no proof of harm needed) |
| Sensitive data violations (court, per individual) | Up to 100,000 NIS (no proof of harm needed) |
| Criminal penalties | Up to 5 years imprisonment for willful infringement |

**Class action risk is the largest financial threat.** Statutory damages of NIS 10,000-100,000 per individual WITHOUT proof of harm, multiplied across a user base, dwarf any administrative fines. This makes privacy compliance a sound business decision, not just a legal obligation.

## 2.5 Accessibility (IS 5568)

**IS 5568 is MANDATORY for both public and private sector mobile applications in Israel.** Effective since October 2017.

| Requirement | Standard |
|------------|---------|
| Base compliance | WCAG 2.0 Level AA (minimum) |
| Aligned with | WCAG 2.1 guidelines |
| Applies to | Websites AND mobile applications |
| Penalty | Up to **NIS 50,000 per complaint** — complainant does NOT need to prove actual harm |
| Enforcement | Civil lawsuits, class actions by disability organizations |

### Key Implementation Requirements

1. **Screen reader compatibility** — all interactive elements must have `accessibilityLabel` in Hebrew
2. **Color contrast** — minimum 4.5:1 for normal text, 3:1 for large text
3. **Text resizing** — content readable at 200% zoom without horizontal scrolling
4. **Keyboard/gesture navigation** — all functions operable without precise gestures
5. **Alternative text** — all images (profile photos, badges, icons) must have alt text in Hebrew
6. **Focus indicators** — visible focus state on all interactive elements
7. **Error identification** — form errors clearly identified and described in text
8. **Time limits** — if booking flows have timeouts, users must be able to extend them

**Build accessible from Day 1.** Retrofitting accessibility is 5-10x more expensive than building it in. The NIS 50,000 per complaint penalty with no harm proof required makes Israel one of the most aggressive accessibility enforcement regimes globally.

## 2.6 Tax & Invoicing

| Item | Rule |
|------|------|
| **VAT** | 18% (increased from 17% on January 1, 2025). Charged on platform service fees only. |
| **SHAAM e-invoicing** | Mandatory for transactions above NIS 5,000. Deadline: June 2026. Affects B2B contracts. Individual subscription fees (NIS 49/mo) are below the threshold. |
| **Platform tax status** | Israeli Ltd. (חברה בע"מ). Issues tax invoices (חשבונית מס) for its own fees. |
| **Nanny tax status** | The nanny is the family's employee when working in the family's home. The family must register the nanny with Bituach Leumi (ביטוח לאומי) and handle tax withholding. The platform is NOT involved in this relationship. |
| **Platform fee invoicing** | v1: Manual Bit payment + Morning (Green Invoice) Best plan (NIS 45/mo) for automated tax invoices (חשבונית מס). v2: PayMe handles payment processing, SHAAM integration, and PCI compliance. |

---

# 3. USER STORIES & FLOWS

## 3.1 Family Registration & Onboarding

**As Noa (dual-income tech parent), I want to create a family profile quickly so that I can start browsing verified nannies tonight.**

### Flow: Family Sign-Up → Profile → Search

```
Step 1: Download & Open
  - App Store / Google Play → "Emuni - אמוני"
  - App opens to Hebrew welcome screen
  - "Find trusted childcare" / "מצאו טיפול בילדים מהימן"

Step 2: Phone Verification
  - Enter Israeli mobile number (05X-XXXXXXX)
  - Receive OTP via SMS (Supabase Auth)
  - Enter 6-digit code
  - No social login in v1 (simplify)

Step 3: Basic Profile
  - First name (required)
  - Last name (required)
  - Profile photo (optional but encouraged — "Nannies feel more comfortable accepting requests from families with photos")
  - Neighborhood (dropdown with autocomplete, Hebrew): e.g., "צפון הישן" (Old North)
  - Address (private, used for distance calculations only, never shown to nannies until booking confirmed)

Step 4: Family Details
  - Number of children (1-6+)
  - For each child: name (optional), age, any special needs (optional free text)
  - Languages spoken at home (multi-select: Hebrew, English, Russian, Arabic, French, Amharic, Other)
  - "What do you typically need a babysitter for?" (multi-select: Date night, Work hours, After school, Weekend, Emergency backup)

Step 5: Preferences (optional, skippable)
  - Preferred nanny experience level (any, 1+ years, 3+ years)
  - Hourly rate range (slider: NIS 30-100/hr)
  - "Do you have a nanny you'd like to invite to Emuni?" → "Bring Your Nanny" flow

Step 6: Consent & Terms
  - Privacy notice (Amendment 13 compliant, layered: short summary + link to full policy)
  - Terms of Service acknowledgment:
    * "I understand that I am the employer of any nanny I hire through Emuni"
    * "I understand that background checks are point-in-time and do not guarantee future behavior"
    * "I am responsible for my own due diligence in selecting a caregiver for my children"
  - Separate consent checkboxes for:
    * Location data processing
    * Profile sharing with potential nanny matches

Step 7: Welcome Screen
  - "Welcome to Emuni! Let's find your perfect match."
  - CTA: "Browse Nannies" → goes to search
  - Secondary: "Complete your profile later"
```

**Time to complete:** Under 3 minutes. Steps 4-5 can be skipped and completed later.

## 3.2 Nanny Registration & Verification

**As Maya (university student babysitter), I want to create a professional profile and get verified so that families can find and trust me.**

### Flow: Nanny Sign-Up → ID Check → Background Check → Profile Live

```
Step 1: Download & Phone Verification
  - Same as family flow (OTP)
  - Select "I'm a nanny/babysitter" / "אני בייביסיטר/מטפלת"

Step 2: Age Verification
  - Date of birth (must be 18+)
  - If under 18: "Emuni requires all nannies to be 18 or older.
    We'll notify you when you're eligible!" → registration blocked

Step 3: Basic Profile
  - First name, last name
  - Profile photo (REQUIRED — must be clear face photo, no sunglasses, no group)
  - Neighborhood (home base for distance calculations)
  - Phone number (already verified)

Step 4: Professional Profile
  - Bio / About me (free text, 50-500 characters, Hebrew)
  - Experience: years of babysitting/nanny experience (0-1, 1-3, 3-5, 5-10, 10+)
  - Age groups comfortable with (multi-select: Infant 0-1, Toddler 1-3, Preschool 3-6, School age 6-12, Teen 12+)
  - Languages (multi-select)
  - Certifications (multi-select: First Aid/MDA, CPR, Education degree, Special needs training, Other)
  - Hourly rate (NIS, nanny sets this — platform never suggests)
  - Additional skills (free text: cooking, homework help, music, etc.)

Step 5: Availability
  - Weekly recurring calendar (tap days/times to mark available)
  - Sunday-Saturday grid, morning/afternoon/evening blocks
  - "I'll set this later" option

Step 6: ID Verification
  - Upload photo of Teudat Zehut (front)
  - Take selfie for biometric matching
  - Didit processes: document authenticity + face match + liveness detection
  - Result: ~30 seconds

Step 7: Optional Background Certificate + Foreign Conviction Self-Attestation
  - Self-attestation: "Have you ever been convicted of a crime outside of Israel?" (Yes/No)
    * "Yes" → flagged for admin review before profile goes live
  - Optional background certificate badge:
    * "Enhance your profile! Families prefer nannies who submit a background certificate.
      Get yours free from gov.il (7-10 business days)."
    * Link to gov.il application page
    * Upload option (available now or later)
    * Profile receives "הגיש/ה אישור רקע" badge upon upload and admin verification

Step 8: Terms & Consent
  - Privacy notice (Amendment 13 compliant)
  - Service agreement (NOT employment agreement):
    * "You are an independent professional. Emuni is a technology platform."
    * "You set your own rates, availability, and work terms."
    * "You are free to provide services through any channel."
  - Separate consent for: profile sharing with families, push notifications
  - If nanny opted in to background certificate: additional consent for criminal record processing

Step 9: Verification Pending Screen
  - "Your profile is being verified! We'll notify you when you're live."
  - "Typical timeline: 1-3 business days for ID verification."
  - "While you wait, complete your profile to attract more families."
  - Profile visible to nanny but NOT to families until all checks pass

Step 10: Profile Goes Live (after all checks pass)
  - Push notification: "You're verified and live on Emuni!"
  - Profile now appears in family search results
  - Badge displayed: verification tier + date
```

### Verification Status Machine

```
pending → id_submitted → id_verified → live

At any step, can transition to:
  → rejected (failed ID verification or admin review)
  → suspended (safety report, pending investigation)

live nannies can transition to:
  → inactive (nanny pauses profile)
  → suspended (safety concern)

Optional badge states (independent of LIVE status):
  → BG_CERT_SUBMITTED (nanny uploaded voluntary background certificate)
  → BG_CERT_VERIFIED (admin verified certificate → badge displayed)
  → BG_CERT_EXPIRED (12 months elapsed → badge removed, profile stays LIVE)
```

## 3.3 Search & Discovery

**As Noa, I want to search for available babysitters near me, filtered by my needs, so that I can find the right person quickly.**

### Search Filters

| Filter | Options | Default |
|--------|---------|---------|
| Distance | 1km, 3km, 5km, 10km, 15km | 5km |
| Availability | Specific date/time, "Available this week," Day of week | None |
| Hourly rate | Slider: NIS 30-100/hr | Full range |
| Age group experience | Infant, Toddler, Preschool, School age, Teen | From family profile |
| Languages | Hebrew, English, Russian, Arabic, Amharic, French | Hebrew |
| Certificate badge | "Show only nannies with background certificate" toggle | Off (show all verified nannies) |
| Rating | 4.0+, 4.5+, 4.7+ | None |

**Free tier filters:** Distance, hourly rate (basic)
**Premium filters:** Language, experience level, schedule match, age group specialization

### Search Results Card

Each result displays:
- Profile photo
- First name + last initial (e.g., "Maya T.")
- Verification badge (blue shield)
- Star rating + number of reviews (e.g., "4.8 (12 reviews)")
- "Responds within X hours" badge (thresholds: < 1hr = "Responds quickly", 1-4hr = "Responds within a few hours", 4-12hr = "Responds within half a day"; new nannies with < 3 requests show no badge)
- Distance from family ("1.2 km away")
- Hourly rate ("NIS 55/שעה")
- Top 2 tags: "Great with toddlers" / "MDA First Aid"
- Availability indicator: green = available this week

### Search Algorithm (v1 — Distance Buckets)

For MVP with <500 nannies, use distance buckets to prevent a nearby low-rated nanny from always outranking a slightly farther high-rated nanny:

```sql
SELECT nannies.*,
  ST_Distance(nannies.location, family.location) AS distance_meters,
  CASE
    WHEN ST_DWithin(nannies.location, family.location, 2000) THEN 1  -- Near (<2km)
    WHEN ST_DWithin(nannies.location, family.location, 5000) THEN 2  -- Farther (2-5km)
    ELSE 3                                                            -- Far (5km+)
  END AS distance_bucket,
  CASE
    WHEN nannies.created_at > NOW() - INTERVAL '30 days'
     AND nannies.review_count < 3 THEN 1  -- New nanny boost
    ELSE 0
  END AS is_new_nanny
FROM nannies
WHERE ST_DWithin(nannies.location, family.location, :radius_meters)  -- parameterized: 1000/3000/5000/10000/15000
  AND nannies.status = 'live'
  AND nannies.available_on @> requested_date
ORDER BY
  distance_bucket ASC,    -- Near nannies first, but within bucket...
  rating DESC,            -- ...sort by rating (not raw distance)
  is_new_nanny DESC,      -- Boost new nannies with <3 reviews
  response_rate DESC
LIMIT 20;
```

**Empty search results state:** At launch density, 50%+ of searches outside Old North will return zero results. Empty state screen shows: (1) "No nannies available in your area yet" with illustration, (2) "Expand your search radius" button (auto-suggests next radius tier), (3) "Bring Your Nanny to Emuni" CTA — invite your existing nanny to join, (4) "Join the waitlist for [neighborhood]" — captures demand data for expansion planning, (5) "We're growing fast — check back soon!" This screen is critical for retention; a blank page = immediate uninstall.

**"New on Emuni" badge:** Nannies with <3 reviews and <30 days on platform get a "New on Emuni" badge + 30-day ranking boost within their distance bucket. This prevents cold-start disadvantage.

**v2+ matching algorithm** (when supply exceeds 500): 100-point weighted scoring — trust graph 30%, availability 20%, distance 15%, rating 15%, response rate 10%, experience 7%, profile completeness 3%.

## 3.4 Booking Flow — Advance Booking (Tier 3) ONLY

**MVP launches with Advance Booking only** (24+ hours out). Emergency, Short Notice, and Recurring booking tiers are deferred to v2/v3 because they require supply density and technical complexity that don't exist at launch.

**As Noa, I want to send a booking request to a specific nanny for next Thursday evening so that I can plan date night with confidence.**

### Step-by-Step Flow

```
Step 1: Noa browses search results, finds Maya
  - Taps Maya's card to view full profile

Step 2: Full profile view
  - Photo, bio, experience, languages, certifications
  - Verification badges and dates
  - Rating breakdown (stars + text reviews)
  - Availability calendar (visual weekly view)
  - Hourly rate: NIS 55/hr
  - "Request Booking" button

Step 3: First-time booking gate (if Noa has never booked Maya before)
  - Noa must scroll through the full profile (minimum 10 seconds)
  - Then "Request Booking" button activates

Step 4: Booking request form
  - Date: [calendar picker, must be 24+ hours out for Tier 3]
  - Start time: [time picker, 24hr format]
  - End time: [time picker]
  - Children: [pre-filled from profile — Yonatan 4, Shira 18mo]
  - Special notes: free text
    ("Shira's bedtime is 19:30, Yonatan can stay up until 20:00.
     Please read them a story. Door code: 1234#")
  - Message to nanny (REQUIRED for first-time bookings):
    ("Hi Maya! We're looking for a babysitter for Thursday date night.
     The kids are great, Shira might need a bottle around 19:00.")

Step 4b: Booking cost summary (displayed before submission)
  - "Estimated total: NIS 275 (5 hrs x NIS 55/hr)"
  - v1: informational only (family pays nanny directly)
  - v2: actual charge amount including service fee

Step 5: Free tier check
  - If Noa is on Free tier and has already used her 1 booking this month:
    → "Upgrade to Premium for unlimited bookings (NIS 49/mo)"
    → Or: "Unlock this booking for NIS 19" (per-contact purchase)
  - If Noa has bookings remaining: proceed

Step 6: Request sent
  - Maya receives push notification:
    "A family in Old North is looking for a sitter on Thursday 18:00-23:00.
     Tap to view."
  - Noa sees: "Request sent to Maya! She has 24 hours to respond."

Step 7: Maya reviews request
  - Sees: Noa's profile, children details, date/time, special notes, message
  - Sees: Noa's rating from previous nannies (if any)
  - Options: Accept / Decline / [Message to discuss]

Step 8a: Maya ACCEPTS
  - Noa receives push notification: "Maya accepted your booking!"
  - Noa confirms booking (double confirmation)
  - Both see booking confirmation screen:
    * Date, time, address (now revealed to Maya)
    * Children details
    * Special notes
    * "Open WhatsApp" button (pre-filled message:
      "Hi Maya, this is Noa from Emuni. Looking forward to Thursday!")
    * Emergency contact info exchanged
    * **Nanny safety tools:**
      - "Share my location" WhatsApp deep link (Maya can share live location with a friend/family member)
      - Emergency buttons prominently displayed: 112 (police) / 101 (Magen David Adom)
      - Optional check-in: "Let someone know you arrived safely" (nanny-initiated, NOT platform-required — avoids Wolt control factor 3)
  - First-time prompt: "This is your first time with Maya.
    We recommend a quick intro call before Thursday."

Step 8b: Maya DECLINES
  - Noa receives notification: "Maya isn't available for this date."
  - System suggests next best match: "How about Lior? She's 1.5km away,
    4.7 stars, available Thursday."
  - Noa can send request to another nanny

Step 8c: Maya doesn't respond within 24 hours
  - Request auto-expires
  - Noa notified: "Maya didn't respond in time."
  - Same suggestion flow as decline

Step 9: Reminder notifications
  - 24 hours before: Push to both — "Reminder: Booking tomorrow at 18:00"
  - 2 hours before: Push to both — "Your booking starts in 2 hours"

Step 10: Post-booking
  - 1 hour after session end time: Push to both — "How did it go?"
  - Review prompt: stars (1-5) + text (optional)
  - Reviews are BLIND — both sides submit before seeing the other's review
  - 48-hour window to submit review, then prompt expires
```

### Edge Cases

| Scenario | Handling |
|----------|---------|
| Maya proposes a different time | Maya sends in-app message: "I can't do Thursday but I'm free Friday — would that work?" Noa can accept the alternative or decline. |
| Noa wants to cancel after confirmation | > 48 hours: no consequence. < 48 hours: reliability score impact (no financial penalty in v1). |
| Maya cancels < 24 hours before | Reliability score impact. **Emergency replacement flow:** System auto-queries available nannies for the same time slot within 5km. Noa receives: "Maya cancelled. We found 3 nannies available for your time slot — tap to send a request." If no matches: "Maya cancelled. No nannies are currently available for this slot. Would you like to search with a wider radius or different time?" |
| Maya no-shows | Significant reliability score impact + account review. After 3 late cancellations in 30 days: supportive outreach + lower search ranking. |
| Noa is not home when Maya arrives | Maya marks "family no-show" after 15 minutes. Session cancelled. Noa's reliability score impacted. |
| Safety concern during session | Both parties have "Report an Issue" button → immediate flag to admin. **Emergency protocol:** (1) Nanny taps emergency button → one-tap 112 (police) / 101 (MDA). (2) Simultaneously sends silent alert to admin with nanny name, location, booking details. (3) Admin receives push + SMS within 30 seconds. (4) Booking auto-flagged as "safety incident." (5) Post-incident: admin contacts both parties within 24 hours, documents incident, determines account action (warning / suspension / ban). (6) If nanny was harmed: platform provides police report reference number and support resources. |
| Dispute (family vs nanny disagreement) | Either party taps "Report an Issue" → selects "Dispute" category → describes issue (late arrival, early departure, conduct concern). Admin reviews within 48 hours. v1: manual mediation by admin. Both parties notified of resolution. Repeat disputes by same user trigger account review. |
| Nanny changes rate between request and acceptance | Rate is **locked at request time**. The rate shown on the nanny's profile when the family sends the request is the rate for that booking. Nanny rate changes apply to future requests only. |
| Two bookings overlap for same nanny | v1: No automated conflict detection. Nanny is responsible for managing their own schedule. If a nanny accepts an overlapping booking, admin intervenes. v2: Add server-side overlap validation. |
| Family wants both parents on one account | v1: One account per family. Either parent can use it. No multi-user login. v2: Consider linked accounts if demand emerges. |
| Family doesn't pay nanny after session (v1) | Platform is NOT involved in family→nanny payments in v1. Nanny should collect payment directly (Bit/cash). ToS and nanny onboarding must state: "You are responsible for collecting payment directly from families." |
| Booking completion trigger | Booking auto-completes at `end_time + 1 hour`. Either party can manually mark complete earlier. Only bookings with status "confirmed" count toward the free tier monthly booking limit. |
| Rejected nanny re-application | Rejected nannies see: "Your profile wasn't approved at this time. Common reasons: unclear photo, incomplete profile, ID verification failed." They can fix issues and re-submit once. After 2 rejections: "Please contact support for assistance." |
| Phone number changes (account recovery) | User contacts support via email. Admin verifies identity (name, profile details, last booking). Admin updates phone number. v2: self-service phone number change with re-verification. |
| Free tier booking count | Only bookings that reach "confirmed" status count toward the 1 booking/month free tier limit. Cancelled, expired, or declined bookings do not count. |

## 3.5 Messaging (In-App Only in v1)

**As Noa, I want to message Maya before booking to ask a question, and then coordinate on WhatsApp after the booking is confirmed.**

### Pre-Booking: In-App Messaging Only

- All pre-booking communication stays in-app
- Protects privacy (no phone number exchange before commitment)
- Enables safety monitoring (scan for red flags)
- Enables response time tracking (for matching algorithm)
- Messages are text-only in v1 (no images, no voice)

### Post-Booking: WhatsApp Handoff

- After booking confirmation: both parties see each other's phone number
- "Open WhatsApp" button with pre-filled message
- Deep link: `https://wa.me/972XXXXXXXXX?text=Hi%20Maya%2C%20this%20is%20Noa%20from%20Emuni...`
- Zero WhatsApp API integration needed (just a URL)
- Why WhatsApp: 95%+ of Israeli adults use it. Israelis expect WhatsApp for coordination.
- Review and booking management stay in-app

## 3.6 Reviews & Ratings

**As Noa, I want to rate Maya after our session so that other families can benefit from my experience. As Maya, I want to rate Noa so that other nannies know she's a good family to work for.**

### Mutual Review System

- Both family and nanny rate each other after every completed session
- **Blind reviews:** both sides submit before seeing the other's review
- **Rating:** 1-5 stars
- **Text review:** optional but encouraged ("Tell other families/nannies about your experience")
- **Review window:** 48 hours after session end time
- **Reminder:** Push notification at 24 hours if no review submitted
- **Display:** Reviews visible on both family and nanny profiles
- **Free tier:** Families see star ratings. **Premium:** Families also see detailed text reviews.

### Review Guidelines

- No personal attacks or identifying information
- No contact information in review text
- Admin moderation for flagged content (manual at MVP scale)
- Reviews cannot be edited after submission (prevents retaliation)
- Reviews are permanent (no deletion except by admin for policy violations)
- **Nanny response:** Nannies may post ONE public response to any review (visible below the review). Responses are subject to the same content guidelines. This balances fairness without enabling flame wars.

## 3.7 Subscription & Payment

**As Noa, I want to understand what I get for free vs. paid, and pay easily.**

### Tier Comparison

| Feature | Free (NIS 0) | Premium (NIS 49/mo) | Founding Member (NIS 29/mo, locked forever) |
|---------|:---:|:---:|:---:|
| Browse all nanny profiles (photos, ratings, reviews) | Full | Full | Full |
| See star ratings | Yes | Yes | Yes |
| See detailed text reviews | No | **Yes** | **Yes** |
| Basic filters (location, rate) | Yes | Yes | Yes |
| Advanced filters (language, experience, schedule match) | No | **Yes** | **Yes** |
| Bookings per month | **1** | **Unlimited** | **Unlimited** |
| In-app messaging | Yes | Yes | Yes |
| Priority in nanny's booking requests (Premium requests sorted first) | No | **Yes** | **Yes** |
| Favorites list + quick rebook (pre-filled booking form for past nannies) | No | **Yes** | **Yes** |
| Founding Member badge | No | No | **Yes** |
| Priority support | No | **Yes** | **Yes** |
| Early access to new features | No | No | **Yes** |

### Per-Contact Purchase

- For non-subscribers who want to unlock a specific nanny beyond their monthly limit
- **NIS 19 per additional booking unlock**
- No commitment, pay as you go
- Designed for the Israeli preference for per-use over subscription (50-60% prefer per-use per GWI research)

### Founding Member Program

- First 200 families to subscribe
- **NIS 29/month, locked forever** (never increases)
- All Premium features + Founding Member badge + early access + input on feature roadmap
- Creates urgency and early revenue validation
- "200 spots available — 180 remaining"

### v1 Payment Collection

| What | How | When to Automate |
|------|-----|-----------------|
| Premium subscription (NIS 49/mo) | Family sends Bit payment to platform. Admin manually activates premium status. | Month 3 (PayMe integration) |
| Per-contact (NIS 19) | Family sends Bit payment. Admin unlocks booking. | Month 3 (PayMe integration) |
| Founding Member (NIS 29/mo) | Same as Premium. | Month 3 |
| Family→Nanny payment | Direct between family and nanny (Bit, cash, bank transfer). Platform NOT involved. | v2: PayMe marketplace splits |

This manual process works for the first 50 paying users. Beyond that, PayMe integration is needed.

## 3.8 Cancellation & No-Show Policy

### v1: Reliability Score Only (No Financial Penalties)

There is no payment mechanism in v1 to collect cancellation fees. Instead, cancellations affect a **reliability score** that impacts search ranking.

| Event | Reliability Score Impact | Platform Action |
|-------|:---:|---|
| Cancel > 48 hours before start | None | None |
| Cancel 24-48 hours before start | Minor decrease | None |
| Cancel < 24 hours before start | Moderate decrease | Warning notification |
| No-show | Significant decrease | Account review |
| 3 late cancellations in 30 days | Cumulative decrease | **Supportive outreach** (not punishment): "We noticed some cancellations. Can we help with scheduling?" + lower search ranking |

**Why no financial penalties for nannies:**
The Wolt lesson is clear — financial penalties destroy supply-side trust in marketplaces. Wolt's punitive approach to couriers contributed to their employer classification. We use positive reinforcement: reliable nannies get higher search ranking, better badges, and more bookings. Unreliable nannies naturally receive fewer requests.

### v2: Financial Penalties (with PayMe Integration)

When PayMe is integrated (Month 3+), add financial cancellation penalties per the Matching Flow spec:

| Timing | Family Cancellation Fee | Nanny Financial Penalty |
|--------|:---:|:---:|
| > 48 hours | 0% | None |
| 24-48 hours | 25% of booked hours | None (reliability score only) |
| 12-24 hours | 50% | None (reliability score only) |
| < 12 hours | 75% | None (reliability score only) |
| No-show | 100% | None (but account review + possible suspension) |

Family cancellation fees go to the nanny as compensation. Nannies NEVER face financial penalties — only reliability score impacts.

---

# 4. FEATURE SPECIFICATION (MVP)

## 4.1 In-Scope Features (v1)

Features are prioritized using Modified RICE scoring from the research corpus. P0 = must have for launch, P1 = should have (first 2 weeks post-launch), P2 = nice to have (month 1-2).

### Family-Side Features

| # | Feature | Priority | Description | Acceptance Criteria |
|---|---------|:---:|-------------|-------------------|
| F1 | Registration (phone + OTP) | P0 | Phone number verification via Supabase Auth | Israeli mobile numbers only. OTP delivered within 10 seconds. Account created in <30 seconds. |
| F2 | Family profile | P0 | Name, photo, neighborhood, children (names, ages, needs), languages | All fields saveable. Address geocoded via Google Maps. Children info editable. |
| F3 | Search nannies with filters | P0 | Browse verified nannies by distance, availability, rate, age experience, language | Results load in <500ms. PostGIS radius query. Pagination (10 per page). Filters persist across sessions. |
| F4 | View nanny profiles | P0 | Full profile: photo, bio, experience, rate, certifications, verification badges, reviews | All verification badges displayed with dates. Star rating + review count visible. |
| F5 | Send booking request (Advance/Tier 3) | P0 | Date, time, children details, special notes, message to nanny | Date must be 24+ hours out. Booking request persists for 24 hours. Push notification to nanny within 5 seconds. |
| F6 | Receive accept/decline notification | P0 | Push notification when nanny responds | Notification delivered within 5 seconds of nanny action. Deep link to booking details. |
| F7 | Confirm booking | P0 | Double confirmation after nanny accepts | Booking status transitions: pending → accepted → confirmed. Address revealed to nanny only after confirmation. |
| F8 | View booking details + WhatsApp link | P0 | Confirmed booking screen with all details and "Open WhatsApp" button | Pre-filled WhatsApp message. Emergency contacts visible. Special notes visible. |
| F9 | In-app messaging (pre-booking) | P0 | Text messaging with nanny before booking | Messages delivered in <2 seconds (Supabase Realtime). Text only (no images in v1). |
| F10 | Leave review after session | P0 | Stars (1-5) + optional text. Blind reviews. | Review prompt 1 hour after session end. 48-hour window. Both sides submit before seeing other's review. |
| F11 | View upcoming and past bookings | P0 | Booking history with status | Sorted by date. Status: pending, confirmed, completed, cancelled. |
| F12 | Report an issue | P0 | Simple form to flag safety or conduct concerns | Form: category (safety, conduct, no-show, other) + free text. Sent to admin immediately. |
| F13 | Freemium subscription | P1 | Free tier (1 booking/mo) + Premium (NIS 49/mo) + per-contact (NIS 19) | Free: browse + 1 booking. Premium: unlimited + advanced filters + text reviews. Manual Bit payment. |
| F14 | Push notifications | P0 | Booking requests, acceptances, reminders, new messages | Firebase Cloud Messaging via Expo. Booking reminders at 24hr and 2hr before. New message notification within 5 seconds. |
| F15 | "Bring Your Nanny" invite flow | P1 | Family invites existing nanny to join platform | SMS/WhatsApp invite link. Pre-filled referral. Nanny lands on registration with family linked. |
| F16 | Favorites list | P1 | Bookmark nannies for later | Add/remove from profile view. List accessible from home screen. |

### Nanny-Side Features

| # | Feature | Priority | Description | Acceptance Criteria |
|---|---------|:---:|-------------|-------------------|
| N1 | Registration (phone + OTP) | P0 | Same as family + age check (18+) | Under-18 blocked with friendly message. |
| N2 | Professional profile | P0 | Name, photo, bio, experience, languages, rate, certifications | All fields editable. Rate set by nanny. Photo required. |
| N3 | Upload ID for verification | P0 | Teudat Zehut photo + selfie for Didit | Upload flow with camera integration (Didit Expo plugin). Processing <30 seconds. |
| N4 | Optional background certificate badge | P0 | Voluntary criminal record certificate upload for profile badge | Upload flow for gov.il certificate. Admin visual verification. "הגיש/ה אישור רקע" badge displayed on profile. Nanny-initiated only. |
| N5 | Set weekly availability calendar | P0 | Recurring weekly schedule (day/time blocks) | Visual grid. Sunday-Saturday. Morning/afternoon/evening blocks. Saveable. |
| N6 | Receive booking request notifications | P0 | Push notification with request summary | Delivered within 5 seconds. Shows: neighborhood, children ages, date/time, rate. |
| N7 | View request details + family profile | P0 | Full request with family info before accepting | Family rating visible (if exists). Children details. Special notes. |
| N8 | Accept / Decline request | P0 | One-tap accept or decline | Accept: booking moves to "accepted, pending family confirmation." Decline: family notified, suggested alternatives. |
| N9 | View booking details + WhatsApp link | P0 | Same as family side — full details + "Open WhatsApp" | Address visible only after family confirms. |
| N10 | Leave review of family | P0 | Stars + text, blind review | Same review system as family side. |
| N11 | View upcoming and past bookings | P0 | Booking history | Same as family side. |
| N12 | In-app messaging (pre-booking) | P0 | Same messaging system as family side | Same as F9. |
| N13 | Nanny safety tools | P0 | Safety features for nannies going to unknown homes | "Share my location" WhatsApp deep link on booking confirmation. Emergency 112/101 buttons. Optional nanny-initiated check-in (NOT platform-required). |

### Admin-Side Features

| # | Feature | Priority | Description | Acceptance Criteria |
|---|---------|:---:|-------------|-------------------|
| A1 | Review and approve nanny profiles | P0 | Queue of pending profiles with all details | Approve/reject with reason. Notification to nanny on decision. |
| A2 | Manage background verification | P0 | Track voluntary background certificate submissions and ID verification results | View certificate uploads, verify authenticity, grant/revoke "הגיש/ה אישור רקע" badge. Only for nannies who opt in. |
| A3 | ID verification review | P0 | Compare ID upload vs selfie (Didit results) | View Didit confidence score. Override capability. |
| A4 | View all bookings | P0 | Sortable, filterable list of all bookings | Filter by status, date, nanny, family. |
| A5 | Handle reported issues | P0 | Queue of reports with context | Priority sorting. Response status tracking. Ability to suspend accounts. |
| A6 | Basic metrics dashboard | P1 | Signups, bookings, active users, conversion | Daily/weekly/monthly views. Export to CSV. |

## 4.2 Out-of-Scope (v2/v3)

| Feature | Reason for Deferral | Target Version |
|---------|--------------------|----|
| **Emergency / same-day booking (Tier 1)** | Requires 50+ available nannies in 5km at any time. At launch density, feature would show "no nannies available" 90% of time. Each failure destroys trust. | v2 (Month 6+) |
| **Short Notice booking (Tier 2, <24 hours)** | Multi-request logic (select 3, first-accept wins) adds significant complexity. | v1.5 (Month 2-3) |
| **Recurring booking (Tier 4)** | Different UX paradigm (job posting + applicants). Validate one-off booking first. | v2 (Month 4-6) |
| **Trust graph / community recommendations** | Worthless with <500 users. "0 friends have used this nanny" is WORSE than not showing the feature. | v2 (Month 4-6) |
| **B2B corporate portal** | No corporate client will sign until they see consumer traction. 3-6 month sales cycle. | v3 (Month 6-12) |
| **Nanny Pro tier (paid nanny subscription)** | Employment Service Law gray zone. Deferred until attorney sign-off. | v3+ (Month 9-12) |
| **AI matching algorithm** | Needs months of behavioral data. Simple sort produces identical results with <500 nannies. | v3 (Month 9-12) |
| **In-app payments / PayMe integration** | Adds 3-4 weeks development + PCI compliance. Families already pay nannies via Bit/cash. | v2 (Month 3) |
| **English UI** | Hebrew covers 90% of target. Build i18n from Day 1, ship English at Month 4-6. | v2 (Month 4-6) |
| **WhatsApp Business API deep integration** | Pre-filled links are sufficient. Full API adds complexity. | v2 (Month 6+) |
| **Insurance products** | Partnership, not tech. Requires scale. | v3 (Month 12+) |
| **Annual subscription pricing (NIS 399/year)** | Not enough data to justify annual commitment pricing. Add once monthly retention data proves value. | v2 (Month 3-6) |
| **Nanny video introduction** | Nice trust signal, not blocking transactions. | v2 |
| **Trust tiers (Verified → Established → Trusted → Premium)** | Meaningful only after nannies have booking history. | v2 (Month 3-6) |
| **Content monitoring (phone number detection)** | At 100 users, admin can review manually. Automate at scale. | v2 |
| **SMS fallback notifications** | Push is sufficient for 24-hour response windows. SMS needed only for Emergency tier. | v2 |

## 4.3 Non-Functional Requirements

| Category | Requirement | Metric |
|----------|-------------|--------|
| **Performance** | App launch (cold start) | < 2 seconds |
| **Performance** | Search results load | < 500ms |
| **Performance** | Booking confirmation | < 3 seconds |
| **Performance** | Message delivery | < 2 seconds |
| **Security** | OWASP Top 10 compliance | All 10 categories addressed |
| **Security** | PII encrypted at rest | AES-256 |
| **Security** | PII encrypted in transit | TLS 1.3 |
| **Security** | Row-Level Security on all user data | Supabase RLS policies |
| **Security** | Penetration testing | Every 18 months |
| **Availability** | Uptime SLA | 99.5% |
| **Scalability** | Concurrent users supported by Month 12 | 10,000 |
| **Accessibility** | IS 5568 compliance level | WCAG 2.1 Level AA |
| **Localization** | Primary language | Hebrew (RTL) |
| **Localization** | i18n architecture | From Day 1 (react-intl or i18n-js) |
| **Localization** | Second language | English (Month 4-6) |
| **Data residency** | All PII storage location | AWS il-central-1 (Israel) |

---

# 5. TECHNICAL ARCHITECTURE

## 5.1 Stack Overview

| Layer | Technology | Justification |
|-------|-----------|---------------|
| **Mobile** | React Native + Expo (TypeScript) | Cross-platform iOS/Android. Massive JS/TS talent pool in Israel (~450K devs). Mature RTL support via `I18nManager`. Expo simplifies builds, push notifications, OTA updates. |
| **Backend** | NestJS on Node.js (TypeScript) with Fastify adapter | TypeScript end-to-end (one language for entire team). Enterprise-grade structure. Native WebSocket support. Fastify: 2x Express throughput. |
| **Database** | PostgreSQL 16+ with PostGIS (via Supabase) | 1,000+ spatial functions for nanny search by location. ACID compliance for booking transactions. Hebrew full-text search via `tsvector`. Social trust graph via recursive CTEs. |
| **Auth/Realtime** | Supabase | Auth (phone OTP, JWT), Realtime (WebSocket subscriptions for messaging), Row-Level Security. 3-5x cheaper than Firebase for heavy read/write patterns. |
| **Cloud** | AWS il-central-1 (Tel Aviv) | Israeli data residency. 3 Availability Zones. $7.2B AWS investment in Israel. Largest service catalog. |
| **ID Verification** | Didit (primary) / Shufti Pro (fallback) | Didit: 500 free verifications/month, $0.30/check after. Native Teudat Zehut support. Biometric face matching + liveness detection. Expo plugin for seamless mobile integration. Fallback: Shufti Pro ($0.20/check, confirmed TZ support). AU10TIX was dropped due to 2024 data breach (EFF worst breach of 2024). Veriff disqualified (no Teudat Zehut support). |
| **Maps** | Google Maps Platform | Best geocoding accuracy for Israeli/Hebrew addresses. Waze data integration. Per-SKU free usage thresholds (no monthly credit since March 2025). Routes API (`computeRouteMatrix`) for travel times (Distance Matrix API is legacy). |
| **Push Notifications** | Expo Notifications | Free, bundled with Expo. Handles iOS (APNs) + Android (FCM) through single API. |
| **Monitoring** | PostHog (error tracking) + CloudWatch | PostHog error tracking: 100K exceptions/month free (20x Sentry's 5K free tier). React Native SDK. Sentry dropped — PostHog consolidates analytics + errors + session replay + feature flags in one tool. CloudWatch for infrastructure monitoring. |
| **Analytics** | PostHog | Product analytics, session replay, feature flags, error tracking — replaces 5-7 separate tools (Mixpanel, Sentry, LaunchDarkly, etc.). Free tier: 1M events/month + session replay + feature flags + 100K error exceptions/month. Single SDK integration. |
| **CI/CD** | GitHub Actions | Standard. Free for private repos (2,000 min/mo). |
| **Payments (v2)** | PayMe | Leading Israeli processor with native marketplace split payments. Target 1.5-2.5% processing fee (realistic for startup volume). Bit integration. SHAAM e-invoicing. PCI compliant. |
| **SMS (v2)** | 019/Cellact | Local Israeli provider. 4-5x cheaper than Twilio for domestic SMS. |
| **ORM** | Drizzle | Native PostGIS support (decisive for location queries). No code generation step. 7.4KB bundle size. TypeScript-first with full type inference. Replaces Prisma. |
| **Invoicing** | Morning (Green Invoice) | Best plan NIS 45/mo. Automated tax invoices (חשבונית מס) from Day 1. Israeli invoicing compliance. |
| **Monorepo** | Turborepo + pnpm workspaces | Shared types/validation between mobile + backend. Incremental builds. Zero-install CI. |

**Estimated MVP infrastructure cost: ~NIS 250-360/month** (~$70-100/month; Didit free, PostHog free, Morning NIS 45/mo included)

## 5.2 Key Database Entities

### Users

```
users
├── id: UUID (PK)
├── phone: VARCHAR(15) UNIQUE -- Israeli mobile, format: +972XXXXXXXXX
├── email: VARCHAR(255) -- optional
├── role: ENUM('family', 'nanny', 'admin')
├── first_name: VARCHAR(100)
├── last_name: VARCHAR(100)
├── profile_photo_url: TEXT
├── location: GEOGRAPHY(POINT, 4326)  -- PostGIS, stored as lat/lng
├── neighborhood: VARCHAR(100)  -- "Old North" / "צפון הישן"
├── languages: TEXT[]  -- ['he', 'en', 'ru']
├── created_at: TIMESTAMPTZ
├── updated_at: TIMESTAMPTZ
├── status: ENUM('active', 'inactive', 'suspended', 'pending_verification')
└── reliability_score: DECIMAL(3,2) DEFAULT 5.00  -- 1.00-5.00
```

### Family Profiles

```
family_profiles
├── id: UUID (PK)
├── user_id: UUID (FK → users)
├── subscription_tier: ENUM('free', 'premium', 'founding')
├── subscription_started_at: TIMESTAMPTZ
├── bookings_used_this_month: INTEGER DEFAULT 0
└── booking_reset_date: DATE
```

### Children

```
children
├── id: UUID (PK)
├── family_id: UUID (FK → family_profiles)
├── name: VARCHAR(100)  -- optional
├── birth_date: DATE  -- for age calculation
├── special_needs: TEXT  -- optional free text
└── created_at: TIMESTAMPTZ
```

### Nanny Profiles

```
nanny_profiles
├── id: UUID (PK)
├── user_id: UUID (FK → users)
├── bio: TEXT  -- 50-500 characters
├── experience_years: ENUM('0-1', '1-3', '3-5', '5-10', '10+')
├── age_groups: TEXT[]  -- ['infant', 'toddler', 'preschool', 'school_age', 'teen']
├── certifications: TEXT[]  -- ['first_aid', 'cpr', 'education_degree', 'special_needs']
├── hourly_rate: DECIMAL(6,2)  -- NIS, set by nanny
├── additional_skills: TEXT
├── verification_status: ENUM('pending', 'id_submitted', 'id_verified', 'live', 'rejected', 'suspended')
├── verified_at: TIMESTAMPTZ
├── average_rating: DECIMAL(3,2)
├── review_count: INTEGER DEFAULT 0
├── response_rate: DECIMAL(3,2)  -- % of requests responded to within window
└── response_time_median: INTEGER  -- minutes
```

### Availability

```
nanny_availability
├── id: UUID (PK)
├── nanny_id: UUID (FK → nanny_profiles)
├── day_of_week: INTEGER  -- 0=Sunday, 6=Saturday
├── start_time: TIME
├── end_time: TIME
└── is_recurring: BOOLEAN DEFAULT true
```

### Bookings

```
bookings
├── id: UUID (PK)
├── family_id: UUID (FK → family_profiles)
├── nanny_id: UUID (FK → nanny_profiles)
├── status: ENUM('pending', 'accepted', 'confirmed', 'completed', 'cancelled_by_family', 'cancelled_by_nanny', 'expired', 'no_show')
├── booking_date: DATE
├── start_time: TIMESTAMPTZ
├── end_time: TIMESTAMPTZ
├── children_ids: UUID[]  -- which children
├── special_notes: TEXT
├── initial_message: TEXT  -- family's message to nanny
├── hourly_rate: DECIMAL(6,2)  -- locked at booking time
├── cancellation_reason: TEXT
├── created_at: TIMESTAMPTZ
├── responded_at: TIMESTAMPTZ  -- when nanny accepted/declined
├── confirmed_at: TIMESTAMPTZ  -- when family confirmed
├── completed_at: TIMESTAMPTZ
└── is_first_time: BOOLEAN  -- first booking between this family and nanny
```

### Reviews

```
reviews
├── id: UUID (PK)
├── booking_id: UUID (FK → bookings)
├── reviewer_id: UUID (FK → users)  -- who wrote it
├── reviewee_id: UUID (FK → users)  -- who it's about
├── rating: INTEGER  -- 1-5
├── text: TEXT  -- optional
├── created_at: TIMESTAMPTZ
└── is_visible: BOOLEAN DEFAULT true  -- admin can hide
```

### Messages

```
messages
├── id: UUID (PK)
├── sender_id: UUID (FK → users)
├── receiver_id: UUID (FK → users)
├── booking_id: UUID (FK → bookings, nullable)  -- associated booking if any
├── content: TEXT
├── read_at: TIMESTAMPTZ
└── created_at: TIMESTAMPTZ
```

### Background Verifications

```
background_verifications
├── id: UUID (PK)
├── nanny_id: UUID (FK → nanny_profiles)
├── check_type: ENUM('criminal_record_voluntary', 'id_verification')
├── status: ENUM('pending', 'in_progress', 'passed', 'failed', 'expired')
├── initiated_at: TIMESTAMPTZ
├── completed_at: TIMESTAMPTZ
├── expires_at: TIMESTAMPTZ  -- 12 months from completion
├── result_summary: VARCHAR(50)  -- 'CLEAR' or 'FLAGGED' — NEVER store raw certificate data
├── verified_by: UUID (FK → users, admin)
└── notes: TEXT  -- admin notes only
```

### Subscriptions

```
subscriptions
├── id: UUID (PK)
├── family_id: UUID (FK → family_profiles)
├── tier: ENUM('premium', 'founding')
├── status: ENUM('active', 'cancelled', 'expired')
├── price_nis: DECIMAL(6,2)
├── started_at: TIMESTAMPTZ
├── expires_at: TIMESTAMPTZ
├── payment_method: ENUM('bit_manual', 'payme')  -- v1: bit_manual, v2: payme
└── created_at: TIMESTAMPTZ
```

## 5.3 API Design Principles

- **RESTful**, versioned: `/api/v1/`
- **JWT auth** via Supabase Auth (access token + refresh token)
- **Rate limiting**: 100 requests/minute per user, 10 requests/minute for search
- **Response format**: JSON with consistent error structure
- **Pagination**: cursor-based for lists

### Key Endpoint Map

```
AUTH
  POST   /api/v1/auth/otp/send          -- Send OTP to phone
  POST   /api/v1/auth/otp/verify         -- Verify OTP, return JWT
  POST   /api/v1/auth/refresh             -- Refresh access token

FAMILIES
  POST   /api/v1/families                 -- Create family profile
  GET    /api/v1/families/me              -- Get current family profile
  PATCH  /api/v1/families/me              -- Update profile
  POST   /api/v1/families/me/children     -- Add child
  PATCH  /api/v1/families/me/children/:id -- Update child
  DELETE /api/v1/families/me/children/:id -- Remove child

NANNIES
  POST   /api/v1/nannies                  -- Create nanny profile
  GET    /api/v1/nannies/me               -- Get current nanny profile
  PATCH  /api/v1/nannies/me               -- Update profile
  PUT    /api/v1/nannies/me/availability  -- Set availability
  GET    /api/v1/nannies/search           -- Search nannies (family-facing)
  GET    /api/v1/nannies/:id              -- Get nanny public profile

BOOKINGS
  POST   /api/v1/bookings                 -- Create booking request
  GET    /api/v1/bookings                 -- List my bookings (role-aware)
  GET    /api/v1/bookings/:id             -- Get booking details
  POST   /api/v1/bookings/:id/accept      -- Nanny accepts
  POST   /api/v1/bookings/:id/decline     -- Nanny declines
  POST   /api/v1/bookings/:id/confirm     -- Family confirms
  POST   /api/v1/bookings/:id/cancel      -- Either party cancels
  POST   /api/v1/bookings/:id/complete    -- Mark session completed

REVIEWS
  POST   /api/v1/bookings/:id/reviews     -- Submit review
  GET    /api/v1/nannies/:id/reviews      -- Get nanny's reviews
  GET    /api/v1/families/:id/reviews     -- Get family's reviews

MESSAGES
  GET    /api/v1/conversations             -- List conversations
  GET    /api/v1/conversations/:userId     -- Get messages with user
  POST   /api/v1/messages                  -- Send message
  -- Real-time: Supabase Realtime subscription on messages table

VERIFICATION (Admin)
  GET    /api/v1/admin/verifications       -- Pending verifications queue
  POST   /api/v1/admin/verifications/:id   -- Approve/reject

SUBSCRIPTIONS
  POST   /api/v1/subscriptions             -- Create subscription (manual v1)
  GET    /api/v1/subscriptions/me          -- Get current subscription
```

## 5.4 Geospatial Search

### PostGIS Implementation

- All user locations stored as `GEOGRAPHY(POINT, 4326)` — WGS 84 coordinate system
- Nanny search uses `ST_DWithin` for radius filtering (database-level, free)
- Google Maps Routes API (`computeRouteMatrix`) only for final shortlist (top 5 nannies) — actual travel time

```sql
-- Find nannies within 5km of family, sorted by distance then rating
SELECT
  np.*,
  u.first_name,
  u.profile_photo_url,
  ST_Distance(u.location, ST_SetSRID(ST_MakePoint(:lng, :lat), 4326)::geography) AS distance_meters
FROM nanny_profiles np
JOIN users u ON np.user_id = u.id
WHERE u.status = 'active'
  AND np.verification_status = 'live'
  AND ST_DWithin(
    u.location,
    ST_SetSRID(ST_MakePoint(:lng, :lat), 4326)::geography,
    5000  -- 5km radius in meters
  )
ORDER BY distance_meters ASC, np.average_rating DESC
LIMIT 20 OFFSET :offset;
```

This hybrid approach (PostGIS for radius, Google Maps for travel time on shortlist) reduces Google Maps API costs by 90%+.

## 5.5 Real-Time Messaging

- **Supabase Realtime** WebSocket subscriptions on the `messages` table
- Client subscribes to `messages` where `receiver_id = current_user_id`
- New messages appear instantly without polling
- Supabase RLS ensures users can only read their own messages
- Unread message count maintained via `read_at IS NULL` queries

## 5.6 Authentication

- **Phone number + OTP** (Israeli mobile numbers: +972 5X-XXX-XXXX)
- **Supabase Auth** handles OTP delivery, verification, JWT issuance
- **No social login in v1** — simplifies implementation, avoids privacy concerns
- **JWT tokens:** access token (1 hour), refresh token (30 days)
- **Role-based access:** family, nanny, admin — enforced at API and RLS levels

## 5.7 Data Residency

- **AWS il-central-1 (Tel Aviv)** — all infrastructure
- **3 Availability Zones** — high availability
- **PII storage strategy:** Supabase managed hosting has NO Israel region (closest: Frankfurt, eu-central-1). Options: (a) Use Supabase managed in Frankfurt — all PII in EU, compliant but not Israeli-hosted; adjust marketing to "EU-hosted" not "Israel-hosted." (b) Self-host Supabase on AWS il-central-1 — all PII in Israel, but adds significant ops complexity for solo founder. **Decision needed pre-launch (see Open Questions #5).** Israel does NOT legally mandate data residency, so Frankfurt is legally acceptable.
- **Supabase:** resolve data residency before launch — confirm managed region or self-host plan
- Israel does NOT legally mandate data residency, but hosting locally provides: lowest latency for Israeli users, simplest compliance narrative, alignment with PPA expectations
- **CDN:** CloudFront with edge location in Israel for static assets

---

# 6. REVENUE MODEL & PRICING

## 6.1 Tier Comparison Table

| Feature | Free (NIS 0) | Premium (NIS 49/mo) | Founding Member (NIS 29/mo, locked forever) |
|---------|:---:|:---:|:---:|
| Browse all nanny profiles (photos, badges, star ratings) | Yes | Yes | Yes |
| See detailed text reviews | No | **Yes** | **Yes** |
| Basic filters (location, hourly rate) | Yes | Yes | Yes |
| Advanced filters (language, experience, schedule match, age group) | No | **Yes** | **Yes** |
| Bookings per month | **1** | **Unlimited** | **Unlimited** |
| In-app messaging | Yes | Yes | Yes |
| Priority in nanny's booking requests | No | **Yes** | **Yes** |
| Favorites list + quick rebook | No | **Yes** | **Yes** |
| Priority support | No | **Yes** | **Yes** |
| Founding Member badge + early access | No | No | **Yes** |
| **Price** | **NIS 0** | **NIS 49/mo** | **NIS 29/mo (first 200 families)** |

**Why NIS 49, not NIS 69:** Israeli subscription norm is NIS 22-50/month (Spotify NIS 23.90, Netflix Standard NIS 46.90). NIS 49 is at the top of the "impulse buy" range. NIS 69 crosses into "let me think about it." Price can be raised once value is proven.

**Apple IAP impact:** Apple takes 15% commission on in-app subscriptions (Small Business Program, <$1M revenue). NIS 49 subscription yields ~NIS 41.65 net to platform. NIS 29 Founding Member yields ~NIS 24.65 net. NIS 19 per-contact yields ~NIS 16.15 net. All revenue projections in Section 6.5 account for this.

**Founding Member tier:** NIS 29/mo locked forever, first 200 families. All Premium features + badge + early access.

## 6.2 Transaction Fees (v2)

- **12-15% on booking value**, charged to families (on top of nanny's rate)
- Average booking: NIS 250-320 (4-5 hours at NIS 62-64/hr TLV average, Babysits 2026 data)
- Average platform fee per booking: NIS 30-48
- Introduced with PayMe integration at Month 3
- Families see: "Nanny rate: NIS 55/hr + Emuni service fee: 12-15%"
- Nannies receive 100% of their stated rate — fee is entirely family-side

## 6.3 B2B (v2+, Month 6)

| Package | Price | Includes |
|---------|-------|---------|
| Starter (up to 100 employees) | NIS 2,000/month | Employee access, backup care bookings/month |
| Growth (100-500 employees) | NIS 5,000/month | Unlimited access, priority matching, HR dashboard |
| Enterprise (500+) | NIS 8,000+/month | Custom, dedicated account manager, reporting |

**B2B trigger:** Start conversations at Month 3 (with traction data). Target first pilot at Month 6. Sign first contract at Month 6-9. The B2B sales cycle is 3-6 months.

**Target companies:** Monday.com, Wix, Check Point, CyberArk, Fiverr, ironSource/Unity — approach via HR/People team contacts.

**No known Israeli competitor offers Bright Horizons/Helpr-style corporate childcare benefits.** This is the single largest untapped revenue opportunity.

## 6.4 Payment Architecture

### v1 Money Flow (Month 0-3): Manual

```
FAMILY pays NANNY directly:
  └── Bit / Cash / Bank transfer (however they want)
      Platform is NOT involved in this payment.

FAMILY pays PLATFORM subscription/per-contact fee:
  └── Bit transfer to platform's business account
      └── Admin manually verifies payment
          └── Admin activates premium status / unlocks booking
              └── Morning (Green Invoice) issues tax invoice (חשבונית מס) — Best plan NIS 45/mo
```

### v2 Money Flow (Month 3+): PayMe Integration

```
FAMILY books NANNY through platform:
  │
  ├── SUBSCRIPTION FLOW:
  │   └── Family subscribes via credit card (PayMe recurring billing)
  │       └── PayMe charges NIS 49/mo + 18% VAT = NIS 57.82/mo
  │           └── Platform receives subscription revenue
  │
  ├── BOOKING FEE FLOW:
  │   └── Family books nanny → pays via PayMe
  │       └── PayMe charges: nanny rate + 12-15% service fee + 18% VAT on fee
  │           └── PayMe splits automatically:
  │               ├── Nanny receives: 100% of stated rate → bank account
  │               └── Platform receives: 12-15% service fee
  │
  └── INVOICING:
      └── PayMe handles:
          ├── SHAAM e-invoicing (for B2B transactions > NIS 5K)
          ├── Credit card installments (תשלומים)
          └── PCI DSS compliance
```

## 6.5 Financial Projections

**Revenue projections rebuilt bottom-up from actual Roadmap KPIs. Y1 based on realistic user growth targets. Y2-Y3 remain aspirational and are dependent on seed funding and team hiring.**

| Metric | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| **Total Revenue (net of Apple IAP 15%)** | **NIS 120-300K** | **NIS 2.5-3.5M** | **NIS 7.6-9.4M** |
| Family Subscriptions (net of 15% IAP) | NIS 90K (avg ~200 subs × NIS 37 blended net × 12mo) | NIS 1.0-1.4M | NIS 3.0-3.5M |
| Per-Booking Service Fee (from Month 3, net of IAP) | NIS 30K (avg ~200 bookings/mo × NIS 21 net × 8mo) | NIS 700K-1.0M | NIS 2.2-2.6M |
| B2B Corporate (from Month 8, no IAP — direct billing) | NIS 15-30K (~NIS 3.5K/mo × 4-5mo) | NIS 400K-600K | NIS 1.0-1.5M |

*Emergency Surcharge and Value-Added Services removed from Y1 — features don't launch until Month 6-9 with minimal volume. Added to Y2+ projections.*

### Bootstrapper Operating Costs

Emuni is built and operated by a solo founder with AI-assisted development. There are no team salaries. Costs reflect actual out-of-pocket expenses only.

| Financial Metric | Value |
|-----------------|-------|
| **Solo breakeven** | **Month 3-5** (revenue exceeds solo operating costs of ~NIS 2-5K/mo; Month 2 math doesn't work at early subscriber counts) |
| **Scaled breakeven** | **Month 20-26** (revenue exceeds full-team burn post-seed, ~NIS 500K/mo) |
| Pre-launch monthly burn (solo) | ~NIS 250-360/mo (infra + Morning NIS 45/mo; Didit IDV free, no Sentry) |
| Pre-launch one-time costs | ~NIS 510 (app store fees NIS 460 [Apple $99/yr + Google $25 one-time] + domain ~NIS 50). Didit free tier = no IDV cost. |
| Launch monthly burn (solo) | ~NIS 250-360/mo (infra + Morning invoicing; Didit free 500/mo, PostHog free tier) |
| Monthly burn at scale (with team) | Revisit at seed round |
| Recommended seed round | NIS 5-7M (when PMF proven, for team hiring + growth) |
| CAC (families, organic/bootstrapper) | NIS 10-30 (organic: WhatsApp virality, Facebook groups) |
| CAC (families, scaled/paid) | NIS 80-150 |
| CAC (nannies) | NIS 30-60 |
| LTV (subscription) | ~NIS 600-900 |
| LTV (subscription + transaction fees) | ~NIS 800-1,300 |
| LTV/CAC ratio (organic) | ~5-8x (healthy; based on organic CAC NIS 10-30) |
| LTV/CAC ratio (paid) | ~3-5x (based on paid CAC NIS 80-150; less efficient, use selectively) |

---

# 7. GROWTH & LAUNCH PLAN

## 7.1 Pre-Launch (Month -3 to 0)

### Company Formation
- Register Israeli Ltd. (חברה בע"מ) — in articles of incorporation, use **"development and operation of technology software for information services"** — NOT "childcare matching" or "connecting families with nannies." This avoids labor court interpreting the company purpose as operating an employment bureau.
- Apply for Employment Bureau License (safety net)
- Apply for IIA Tnufa grant (NIS 200,000, non-dilutive but has royalty repayment obligation of 3-5% of revenue; cannot cover salaries)
- DIY Terms of Service + Privacy Policy from templates (no attorney at launch; revisit when revenue exists)

### Supply Recruitment: 50 Nannies in Old North TLV

**Target density:** 50 nannies in ~2-3 km2 (Old North: Yarkon to Arlozorov, Ibn Gvirol to sea) = ~17-25/km2 = thriving marketplace density

| Channel | Target Nannies | Method |
|---------|:-:|---|
| Facebook groups (babysitter recommendation groups) | 15 | Direct outreach to group members, post "get verified for free" |
| TAU campus (3km from Old North) | 10 | Job board postings, education/psychology department, campus events |
| "Bring Your Nanny" (founding families invite their nanny) | 10 | 20 founding families × 50% conversion |
| Sherut Leumi alumni networks | 5 | Partner with amutot |
| Instagram targeted ads (TLV, women 18-30) | 5 | "Get paid more, get booked more — join Emuni free" |
| Nanny referrals (NIS 100 per verified referral) | 5 | Existing nannies invite friends |

### Founding Families: 20 Families for Soft Launch

- Founder's personal network: 10 families
- TAU parent WhatsApp groups: 5 families
- Old North mom Facebook groups: 5 families
- All 20 get Founding Member pricing (NIS 29/mo locked forever)
- Manual onboarding: meet each family, explain the platform, help create profiles

### SEO & ASO Strategy

Parents search Google for "בייביסיטר תל אביב" and "babysitter Tel Aviv." Organic discovery requires web presence from Day -3:

- **Month -3:** Launch emuni.co.il landing page with waitlist signup, neighborhood demand capture, basic SEO (Hebrew + English keywords)
- **Launch:** App Store Optimization — Hebrew keywords, screenshots, compelling description. Target: "בייביסיטר", "מטפלת", "שמרטפות", "babysitter Israel"
- **Month 3+:** Content marketing — blog posts on babysitter rates, safety tips, parenting in TLV. Target long-tail Hebrew search queries.

### Pre-Launch Checklist

- [ ] emuni.co.il landing page live with waitlist
- [ ] All 50 nannies verified (ID verification via Didit + profile approved)
- [ ] 20 founding families registered with complete profiles
- [ ] Hebrew privacy policy + ToS completed (DIY from templates)
- [ ] IS 5568 accessibility audit passed
- [ ] Database Definition Document created
- [ ] Breach response plan documented
- [ ] Crisis communications templates prepared
- [ ] Admin panel operational
- [ ] PostHog error tracking + analytics configured (replaces Sentry + Mixpanel)
- [ ] PostHog session replay + feature flags enabled
- [ ] App Store and Google Play listings ready (Hebrew, ASO-optimized)

## 7.2 Launch (Month 0-3)

### Geography: Old North TLV Only

**Why concentrated force beats broad coverage:**

| Metric | Original Plan (4 neighborhoods) | Emuni Plan (Old North only) |
|--------|:-:|:-:|
| Nannies at launch | 100 across 30 km2 | 50 in ~2-3 km2 |
| Density | 3.3/km2 (minimum viable) | **~17-25/km2 (thriving)** |
| Nearby nannies per family search | 8-12 | **20-30** |
| Time to first booking | Hours to days | **Minutes to hours** |
| Word-of-mouth concentration | Diluted | **Concentrated** |
| Operational complexity | 4 zones | **1 zone to perfect** |

### "Bring Your Nanny" Mechanic

A supply seeding mechanic (note: not a true viral loop — K-factor < 1 because invited nannies don't generate further invites; real viral loop = family→friend WhatsApp recommendations):

1. Family signs up → platform prompts: "Do you have a nanny you trust? Invite them to get verified for free!"
2. Family sends WhatsApp invite with pre-filled link
3. Nanny lands on registration with family already linked
4. Nanny gets verified → first review comes from inviting family (warm start)
5. Nanny's profile is now visible to ALL families in Old North
6. **Result:** Each successful invite adds 1 nanny + 1 family + 1 review simultaneously

**Target:** 30% of early families = 30 nanny+family pairs

### PMF Tracking

| Week | Bookings/Week Target | Cumulative Nannies | Cumulative Families |
|------|:---:|:---:|:---:|
| 1-4 | 1-3 | 50 | 40 |
| 5-8 | 3-7 | 70 | 80 |
| 9-12 | **10** (PMF threshold) | 100 | 200 |

## 7.3 Expansion Phases

### Phase 3: Traction (Month 3-6)

- **Geography:** Expand to Ramat Aviv (adjacent to Old North, family-dense, TAU proximity) then Ra'anana (Anglo community). Florentin deferred — not family-oriented per Ronkin List analysis (~7K population).
- **Product:** PayMe integration, Short Notice booking (Tier 2), English UI toggle
- **Revenue:** First Premium subscribers at scale, transaction fees begin
- **B2B:** Start conversations with 3-5 TLV tech companies
- **Target:** 200 nannies, 500 families

### Phase 4: Growth (Month 6-12)

- **Geography:** Herzliya + opportunistic Florentin (if demand signals emerge)
- **Product:** Emergency booking (if density allows), trust tiers, trust graph v1
- **Revenue:** First B2B contract signed (NIS 2K-5K/mo)
- **Funding:** Begin seed round (NIS 5-7M) with IIA matching (50-55%)
- **Target:** 500 nannies, 2,000 families

### Phase 5: Scale (Month 12-24)

- **Geography:** Multi-city — Jerusalem (Anglo neighborhoods), Modiin, Netanya, Herzliya
- **Product:** AI matching algorithm, recurring booking, B2B corporate portal
- **Revenue:** Multiple B2B contracts, approaching scaled breakeven
- **Target:** 2,000 nannies, 8,000 families
- **Solo breakeven:** Month 3-5 (revenue > solo operating costs ~NIS 2-5K/mo)
- **Scaled breakeven:** Month 20-26 (revenue > full-team burn post-seed ~NIS 500K/mo)

### Expansion Trigger Criteria

**Hard gate:** PMF must be confirmed (10+ bookings/week for 4+ consecutive weeks) before any expansion decision.

**Ideal gate (recommended):** Move to next zone when current zone hits 4 of 6 metrics for 4 consecutive weeks:

1. Booking fill rate > 65%
2. Repeat booking rate > 50%
3. NPS > 50
4. Organic acquisition > 50%
5. Nanny density > 5/km2
6. Monthly active nannies > 65%

If PMF is confirmed but the 6-metric gate isn't fully met, expansion can proceed with caution — focus on the weakest metrics in the new zone.

## 7.4 PMF Metrics & Kill Criteria

| Signal | Green (PMF) | Yellow (Concern) | Red (Kill) |
|--------|:---:|:---:|:---:|
| Bookings/week | 10+ by Week 16 | 5-10 by Week 16 | < 5 by Week 20-24 |
| Monthly family retention | 40%+ | 25-40% | < 25% |
| NPS (families) | 50+ | 30-50 | < 30 |
| Repeat booking rate (30-day) | 30%+ | 15-30% | < 15% |
| Booking completion rate | 60%+ | 40-60% | < 40% |

**If RED by Week 20-24:** Stop development. Interview 20 churned users. Determine root cause (supply? demand? UX? trust? pricing?). Pivot or shut down. Week 16 is diagnostic checkpoint, not kill trigger — babysitting frequency (1-4x/month) means slower signal than daily-use apps.

---

# 8. RISK REGISTER

| # | Risk | Likelihood | Impact | Mitigation | Owner |
|---|------|:---:|:---:|------------|-------|
| **R1** | **Cold start failure** — can't recruit 50 nannies | Medium | Critical | Founder does in-person recruitment at TAU campus, Facebook groups. NIS 100 referral bonus. "Bring Your Nanny" mechanic. ID verification free for nannies. | Founder |
| **R2** | **NIS 49/mo too low** for unit economics | Medium | High | Transaction fees (12-15%) supplement. B2B revenue stream. Can raise to NIS 69 once value proven. Breakeven may extend to Mo 24-28. | CEO / CFO |
| **R3** | **Voluntary background certificate adoption rate** too low | Medium | Medium | Only ~20-30% of nannies may submit voluntary certificates. Mitigate with: strong UX nudges, "families prefer certified nannies" messaging, badge visibility on profiles, social proof ("X nannies already certified"). ID verification (Didit) remains mandatory and is the baseline trust signal. | Founder |
| **R4** | **Operating without DPO** while processing some voluntary criminal data | Medium | Medium | DPO deferred based on Amendment 13 "significant scale" threshold analysis. At ~50 users with voluntary-only criminal certificates, not triggered. Mitigate: privacy-by-design, data minimization, store only pass/fail results. Revisit at ~500-1,000 users. | Founder |
| **R5** | **Safety incident** involving nanny or family on platform | Low | Critical | Didit ID verification (mandatory). Voluntary background certificate badge. Foreign conviction self-attestation. Nanny safety tools (location sharing, emergency buttons). Immediate suspension protocol. Precise language (never "safe"). E&O insurance at seed round. | Founder |
| **R6** | **Employer classification** (like Wolt) | Low | Critical | Pure marketplace structure. 12 MUST DOs / 12 MUST NEVERs enforced. Fee model irrelevant to classification. Employment bureau license as safety net. | Legal |
| **R7** | **Wolt appeal reversal** changes classification law | Low | High | Our structure avoids all 9 control factors regardless of ruling outcome. AG position favors case-by-case analysis, not blanket gig worker legislation. | Legal |
| **R8** | **"Emuni" domain/trademark** unavailable | Medium | Low | Backup names researched: Kena (קנא, "little nest"), Bubale (בובאלע, endearment). File trademark application immediately. | CEO |
| **R9** | **Solo founder burnout / single point of failure** | High | Critical | Solo founder handles product, development, growth, support, legal. Mitigate: AI-assisted development (Claude, Cursor), ruthless prioritization, automate everything possible, defer non-essential features. If founder becomes incapacitated, platform can run on autopilot for 2-4 weeks (automated infra, no manual processes critical). Consider first hire (part-time community manager) when revenue supports it. | Founder |
| **R10** | **WhatsApp cannibalization** — users take relationships off-platform | High | Medium | Platform value = vetting + reviews + legal tools. WhatsApp can't provide these. "Bring Your Nanny" encourages platform adoption for existing relationships. Nanny reviews only build on-platform. | Product |
| **R11** | **IS 5568 accessibility lawsuit** | Medium | High | NIS 50K per complaint, no harm proof. Build accessible from Day 1. `accessibilityLabel` on every component. Pre-launch accessibility audit. | CTO |
| **R12** | **Nanny retention** — leave after finding families | High | Medium | Trust tiers (v2), review portability, ongoing value (MDA courses, earnings tracking). Reviews only exist on-platform. | Product |
| **R13** | **Israeli parents won't pay NIS 49/mo** | Medium | Medium | Per-contact option (NIS 19) for price-sensitive users. Founding Member at NIS 29/mo. A/B test pricing in first month. | Product / CEO |
| **R14** | **SHAAM e-invoicing deadline** (June 2026) | High | Medium | B2B invoices > NIS 5K need SHAAM allocation numbers. Must integrate PayMe SHAAM API before B2B launch. Individual subscription fees below threshold. | CTO / Finance |
| **R15** | **Class action under Amendment 13** | Low | Critical | Statutory damages NIS 10K-100K per individual without proof of harm. Privacy compliance is a business investment, not just legal obligation. Store minimal data. Privacy-by-design from Day 1. DPO appointment when scale triggers requirement. | Founder |
| **R16** | **DIY legal documents may have gaps** | Medium | Medium | ToS and privacy policy built from templates without attorney review. Mitigate: use best-practice Israeli SaaS templates, study comparable platforms' terms, flag as risk. Engage attorney when first revenue exists. | Founder |
| **R17** | **Didit IDV vendor risk** (newer provider) | Low | Medium | Didit is a newer IDV provider (less track record than incumbents like AU10TIX or Onfido). AU10TIX was dropped due to 2024 data breach (EFF worst breach of 2024). Veriff disqualified (no Teudat Zehut support). Mitigate: (1) Shufti Pro as confirmed fallback ($0.20/check, TZ support). (2) Do not store raw ID images longer than necessary. (3) Monitor Didit's security posture and uptime. (4) Didit's free tier (500/mo) eliminates vendor lock-in risk — easy to switch at low volume. | Founder / CTO |
| **R18** | **Yad2 competitive entry into childcare** | Low | Critical | Yad2 has NOT entered childcare as of March 2026, but has distribution (millions of MAU) and brand recognition. If they add a childcare vertical, they can instantly commoditize the market. Mitigate: build defensible trust signals (reviews, verification, community) that Yad2 can't replicate with classifieds. | Founder |
| **R19** | **Crisis communications plan missing** | High | High | No documented plan for handling negative PR, safety incidents, or data breaches in media. Mitigate: prepare crisis comms templates before launch — press statement, user notification, social media response. Identify trusted journalist contacts. | Founder |
| **R20** | **App store rejection risk** | Medium | High | Apple is sensitive about children's data and background check claims. "Safety" messaging, children's ages stored, and background check language may trigger review pushback. Mitigate: review Apple Kids Category guidelines, avoid "safe" language in store listing, prepare appeal documentation. | Founder |
| **R21** | **Negative PR / viral safety incident** | Low | Critical | One bad experience shared on Israeli social media can go viral in hours. Mitigate: rapid response protocol (< 2 hours), designated spokesperson (founder), pre-written holding statements, proactive communication with affected parties. | Founder |
| **R22** | **iSavta pivot to childcare** | Low | Medium | iSavta has 35K+ caregivers (elderly care). If they pivot to childcare, they have immediate supply-side advantage. Mitigate: our focus on babysitting (not elderly care), Hebrew-first UX, and verified trust signals create differentiation. Monitor their product roadmap. | Founder |
| **R23** | **Regulatory change (gig economy legislation)** | Medium | Medium | Israel may pass broad gig economy legislation following Wolt ruling. Could affect platform obligations. Mitigate: pure marketplace architecture avoids all 9 control factors regardless of legislative changes. Monitor Knesset committee discussions. | Legal |

---

# 9. APPENDICES

## 9.1 Research Corpus Reference

Full research index available in `RESEARCH_INDEX.md`. The PRD is backed by 27 research documents (~15,000 lines), produced by 18+ research agents across 6 research rounds, verified by a 4-agent team with 64+ claims checked and 23 corrected.

## 9.2 Canonical Data Points

These are the final, verified numbers. If any document disagrees with these, these are authoritative.

| Data Point | Value | Source |
|-----------|-------|--------|
| Company name | **Emuni (אמוני)** | NAMING_RESEARCH |
| Subscription price | **NIS 49/mo** | FOUNDER_DECISIONS |
| Per-contact fee | **NIS 19** | FOUNDER_DECISIONS |
| Founding Member price | **NIS 29/mo (locked forever)** | FOUNDER_DECISIONS |
| Transaction fee | **12-15% on booking value** | MASTER_RESEARCH |
| VAT rate | **18%** | PAYMENT_TAX_RESEARCH |
| Y1 revenue | **NIS 120-300K** (net of Apple IAP 15%) | Rebuilt bottom-up from Roadmap KPIs |
| Y2 revenue | **NIS 2.5-3.5M** | MASTER_RESEARCH (aspirational, dependent on seed funding) |
| Y3 revenue | **NIS 7.6-9.4M** | MASTER_RESEARCH (aspirational, dependent on seed funding) |
| Solo breakeven | **Month 3-5** | Revenue > solo burn (~NIS 2-5K/mo) |
| Scaled breakeven | **Month 20-26** | Revenue > full-team burn post-seed (~NIS 500K/mo) |
| Pre-launch burn (solo bootstrapper) | **~NIS 250-360/mo** + ~NIS 510 one-time | Revised: Didit free, Morning NIS 45/mo, no Sentry |
| Launch burn (solo bootstrapper) | **~NIS 250-360/mo** | Revised: Didit free 500/mo, PostHog free tier, Morning NIS 45/mo |
| Seed round target (post-PMF) | **NIS 5-7M** | COST_MODEL (for team hiring + growth) |
| TAM | **NIS 22.8B ($6.3B)** | CUSTOMER_RESEARCH |
| SAM | **NIS 216M ($60M)** | CUSTOMER_RESEARCH |
| SOM Y3 | **NIS 23.5M ($6.5M)** | CUSTOMER_RESEARCH |
| Launch area | **Old North TLV** | LAUNCH_GEOGRAPHY |
| Target nanny density | **~17-25/km2 (50 in ~2-3 km2)** | LAUNCH_GEOGRAPHY |
| Tech stack | **React Native (Expo) + NestJS + PostgreSQL + Drizzle ORM** | TECH_RESEARCH + PRISMA_VS_DRIZZLE_COMPARISON_2026 |
| Payment processor (v2) | **PayMe (target 1.5-2.5%)** | PAYMENT_PROCESSOR_COMPARISON |
| MVP build time | **8-12 weeks** | MVP_SCOPE |
| Background check cost | **FREE (criminal cert via gov.il)** | BACKGROUND_CHECK_RESEARCH |
| ID verification cost | **NIS 0/nanny** (Didit free tier: 500/mo) | IDENTITY_VERIFICATION_SERVICES_2026 |
| Privacy compliance cost (bootstrapper) | **NIS 0-5K/yr** (DPO deferred) | Revised for solo founder model |
| Average babysitter rate (TLV) | **NIS 62-64/hr** | Babysits 2026 data |
| PMF metric | **10 bookings/week by Week 16** | MVP_SCOPE |
| Kill metric | **< 5 bookings/week by Week 20-24** | MVP_SCOPE |

## 9.3 Glossary of Hebrew Legal/Business Terms

| Hebrew Term | Transliteration | English Meaning | Context |
|-------------|----------------|-----------------|---------|
| תעודת יושר | Teudat Yosher | Certificate of Good Conduct / Criminal Record Certificate | Background check document issued by Israel Police |
| תעודת זהות | Teudat Zehut | Identity Card | Israeli national ID document |
| עוסק מורשה | Osek Murshe | Authorized Dealer | VAT-registered business (must charge and remit VAT) |
| עוסק פטור | Osek Patur | Exempt Dealer | Small business below VAT threshold (NIS 120K/yr turnover) |
| חברה בע"מ | Chevra Ba'am | Ltd. Company | Israeli limited liability company |
| שע"ם | SHAAM | Tax Authority e-invoicing system | Electronic allocation numbers for invoices > NIS 5K |
| מס הכנסה | Mas Hachnasa | Income Tax | Israeli income tax authority |
| ביטוח לאומי | Bituach Leumi | National Insurance Institute | Israeli social security — families must register nannies |
| המלצה | Hamlatza | Recommendation | Personal referral — the #1 trust signal in Israeli culture |
| גן / גנון | Gan / Ganon | Kindergarten / Daycare | Israeli early childhood education facility |
| משפחתון | Mishpachton | Family Daycare | Home-based daycare (up to 5 children) |
| שירות לאומי | Sherut Leumi | National Service | Alternative to military service — many serve in childcare settings |
| מטפלת | Metapelet | Caregiver/Nanny | Female caregiver (standard term) |
| בייביסיטר | Babysitter | Babysitter | Borrowed English term, widely used in Hebrew |
| חוק שירות התעסוקה | Chok Sherut HaHa'asakah | Employment Service Law (1959) | Prohibits charging job seekers placement fees |
| קבלן כוח אדם | Kablan Koach Adam | Manpower Contractor | Classification to avoid — creates employer obligations |
| לשכת תעסוקה פרטית | Lishkat Ha'asakah Pratit | Private Employment Bureau | License to obtain as safety net |
| פקודת הנזיקין | Pkudat HaNzikin | Civil Wrongs Ordinance | Tort law — basis for duty of care / negligent vetting claims |
| חוק הגנת הפרטיות | Chok Haganat HaPratiyut | Privacy Protection Law | Israeli privacy law, amended by Amendment 13 (2024) |
| הרשות להגנת הפרטיות | HaRashut LeHaganat HaPratiyut | Privacy Protection Authority (PPA) | Israeli data protection regulator |
| ממונה הגנת מידע | Memuneh Haganat Meida | Data Protection Officer (DPO) | Required under Amendment 13 for sensitive data processors |

## 9.4 Open Questions

These items from the research require resolution before or shortly after launch:

| # | Question | Priority | Owner | Deadline |
|---|----------|:---:|-------|----------|
| 1 | "Emuni" domain and trademark availability — confirm and register | High | CEO | Pre-launch |
| 2 | ~~RESOLVED — Track A (mandatory sex offense clearance) dropped. No covered institution status needed.~~ | — | — | — |
| 3 | ~~RESOLVED — Didit selected (500 free/mo, Expo plugin, TZ confirmed). Shufti Pro as fallback. AU10TIX dropped (2024 breach). Veriff disqualified (no TZ).~~ | — | — | — |
| 4 | WhatsApp Business API approval timeline for Israel | Medium | CTO | Month -1 |
| 5 | Supabase data residency confirmation for il-central-1 (or self-host decision) | High | CTO | Month -2 |
| 6 | IIA Tnufa grant application — current processing times | High | CEO | Immediately |
| 7 | Insurance products for childcare platforms in Israel — broker consultation | Low | CEO | Month 6 |
| 8 | User interviews — 15-20 parents + 5-10 nannies (all research is secondary) | High | Product | Month -2 |
| 9 | Rockmybaby Israel competitive intelligence — pricing, scale, operations | Medium | Product | Month -1 |
| 10 | PayMe contract negotiation — target 1.5-2.5% processing fee (realistic for startup volume) | Medium | CEO | Month 2 |
| 11 | **Data retention schedule** — define retention periods for: booking records, messages, inactive accounts, expired background check results, ID verification images. Must align with Amendment 13 data minimization. | High | Founder + DPO (when appointed) | Pre-launch |
| 12 | **Account deletion flow** — Amendment 13 requires deletion mechanisms for data subjects. Define UX flow for users who want to delete their account + what data is retained for legal obligations vs. deleted. | High | Founder | Pre-launch |
| 13 | **Disaster recovery / backup strategy** — define backup frequency, RTO/RPO targets, and failover plan for Supabase + AWS. | Medium | Founder | Pre-launch |
| 14 | **App Store review risk** — Apple is sensitive about children's data and background check claims. Prepare for potential review pushback on: children's ages stored, background check language, "safety" messaging. Review Apple's Kids Category guidelines. | High | Founder | Pre-launch |
| 15 | **Scheduling conflict detection** — v1 has no server-side overlap prevention for nanny bookings. Monitor for double-booking incidents and prioritize server-side validation if they occur. | Low | Founder | Month 1-2 |

---

*This PRD synthesizes research from 27 documents, 18+ research agents, and 250+ sources across 6 research rounds, verified by a 4-agent team. It does not constitute legal, financial, or tax advice. Consult qualified Israeli professionals for all legal, tax, privacy, and employment law matters before launch.*

*Research corpus: `RESEARCH_INDEX.md` | Roadmap: `EMUNI_ROADMAP.md` | All research files in project directory.*
