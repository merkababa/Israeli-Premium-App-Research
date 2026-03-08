# Nanny Platform MVP Scope & Feature Prioritization

**Date:** March 7, 2026
**Research Agent:** MVP Scope Researcher
**Sources:** Web research on 12+ marketplace startups, 6 prioritization frameworks, Israeli startup ecosystem analysis
**Companion Documents:** `NANNY_PLATFORM_MASTER_RESEARCH.md`, `NANNY_PLATFORM_MATCHING_FLOW.md`

---

## EXECUTIVE SUMMARY

The single most important lesson from every successful marketplace MVP: **launch with the minimum features that enable ONE complete transaction between two sides, then learn.** UrbanSitter launched with just social discovery (no payments). Airbnb launched with photos of one apartment. Uber launched as a text-to-hail-a-black-car service for the founders' friends. Bubble UK launched with friend-pooled babysitters and one-tap booking.

**Our MVP scope recommendation:** Launch with Advance Booking (Tier 3) only, basic reviews (no trust graph), manual background checks, no in-app payment, WhatsApp handoff post-match, and a laser focus on Tel Aviv tech moms. Target: 100 families + 100 nannies in 90 days.

**Estimated MVP build time:** 8-12 weeks for a focused team.

---

## PART 1: HOW MARKETPLACE STARTUPS SCOPED THEIR MVPs

### 1.1 Childcare/Care Marketplace MVPs

| Platform | Year | MVP Features | What They Added LATER | Key Lesson |
|----------|------|-------------|----------------------|------------|
| **Care.com** | 2007 | Job board for 4 care categories (child, senior, pet, tutoring). Profiles + search. No payments. No background checks. | Housekeeping (2008), background checks (optional/paid), subscriptions, B2B (Care@Work), mobile app | Started broad (4 categories) but simple. Background checks were NOT in MVP -- this later caused the $8.5M FTC disaster. |
| **UrbanSitter** | 2010 | Facebook Connect integration showing which babysitters your friends used. Built on Drupal CMS + LAMP stack. Discovery only -- no payments. | Payments, mobile app, subscription model, booking management, background checks | **Social trust was the ONLY v1 feature.** Everything else came later. Validates our trust graph concept but proves you can launch without it being fully built. |
| **Sittercity** | 2001 | Simple web directory of babysitters in Boston. Profiles + contact info. No payments. No background checks. | National expansion (2004), background checks (paid add-on), subscription model, acquired by Bright Horizons (2020) | Started hyperlocal (Boston only). Proved a directory alone has value. |
| **Bubble UK** | 2016 | Friend-pooled babysitter booking. Social layer + one-tap payment. MVP built by outsourced dev house (founders are non-technical). | Express Book (on-demand), expanded trust signals, corporate partnerships | Non-technical founders validated with outsourced MVP. Social trust + payment = their core from day 1. |
| **Helpr** | 2016 | Started as a babysitting agency (2007), pivoted to B2B app in 2016. First app: book vetted sitters through employer benefit. | "My Choice" (use your own friends/family as subsidized caregivers), 150+ country expansion, adult care | **B2B-first model works.** Started as agency, evolved to tech platform. Agency-to-platform is a valid path. |

### 1.2 Non-Childcare Marketplace MVPs (Lessons That Transfer)

| Platform | MVP | What They Deferred | Transferable Lesson |
|----------|-----|-------------------|---------------------|
| **Airbnb** (2007) | Photos of founders' apartment on a simple website. 1 listing, 1 location, 1 use case (conference attendees). | Multi-city, professional photos, payments, ratings, mobile app, Experiences | **Start with ONE use case in ONE location.** Don't build for scale before you have 10 users. |
| **Uber** (2009) | Text your address to founders, they call a black car driver. Credit card on file charged via PayPal. Founders' friends only. | Driver tracking, fare estimates, multiple car types, surge pricing, driver ratings | **Manual operations first.** Founders literally called drivers. Automate after you validate demand. |
| **Gett** (2011) | Hebrew-only beta in Tel Aviv. Find nearest licensed taxi, reduce wait to <10 min. Basic app, licensed taxis only. | London/Moscow expansion, corporate accounts (became their real business), self-driving partnerships | **Israeli MVP = Tel Aviv only, Hebrew only.** B2B became their real revenue (mirrors our strategy). |
| **Wolt** (2018 Israel) | Self-pickup ordering from 26 restaurants in Tel Aviv. NOT delivery first -- pickup was "easiest way to get running." | Delivery, grocery, pharmacy, 2500+ businesses, Wolt Market | **Launch with the EASIEST version of your service.** Wolt didn't even do delivery in their Israel MVP. |
| **Monday.com** (2014) | "daPulse" -- task assignments, one-click updates, email sending. Enterprise project management. Narrow feature set. | Gantt charts, automations, integrations, CRM, rebrand to Monday.com | **Nail one workflow before expanding.** They didn't try to be "everything" on day 1. |

### 1.3 Universal MVP Patterns from Marketplace Research

1. **Every successful marketplace launched with ~20% of their current features**
2. **Social trust OR verified quality -- not both at launch** (UrbanSitter had social, no verification. Care.com had profiles, no verification. Bubble had social + payment.)
3. **Payment integration is NOT required for v1** (UrbanSitter, Care.com, Sittercity all launched without it)
4. **Background checks were NOT in any childcare MVP** -- but this created massive problems later (Care.com's $8.5M FTC settlement). For a post-2020 launch, background checks are now table stakes.
5. **Geographic focus: ONE city, ONE neighborhood** -- every single marketplace started hyperlocal
6. **Manual operations replace automation** -- Uber's founders called drivers, Zappos bought shoes at retail stores, Airbnb took listing photos themselves

---

## PART 2: MVP FEATURE PRIORITIZATION FRAMEWORK

### 2.1 Framework: Combined MoSCoW + Modified RICE

We use **MoSCoW** for categorical prioritization (Must/Should/Could/Won't) and **Modified RICE** for scoring within categories.

**Modified RICE Score = (Reach x Impact x Confidence) / Effort**

| Factor | Scale | Description |
|--------|-------|-------------|
| **Reach** | 1-5 | How many of our first 200 users (100 families + 100 nannies) will use this feature? 1=<10%, 5=90%+ |
| **Impact** | 1-5 | How much does this feature affect whether a user completes a transaction? 1=nice, 5=impossible without it |
| **Confidence** | 0.5-1.0 | How confident are we this is the right solution? 0.5=guess, 1.0=validated |
| **Effort** | 1-10 | Person-weeks to build. 1=trivial, 10=months |

### 2.2 Feature Scoring — All Features from Matching Flow Spec

#### MUST HAVE (v1 MVP) — Without these, no transaction happens

| Feature | R | I | C | E | RICE | Rationale |
|---------|---|---|---|---|------|-----------|
| **Nanny profile creation (Stage 1+2)** | 5 | 5 | 1.0 | 3 | 8.3 | No profiles = no marketplace |
| **Parent registration + family profile** | 5 | 5 | 1.0 | 2 | 12.5 | Must know who is booking |
| **Basic search with filters** (distance, availability, rate, age experience) | 5 | 5 | 1.0 | 4 | 6.3 | Discovery is the core product |
| **Advance Booking flow (Tier 3)** — single request to 1 nanny, 24hr response | 4 | 5 | 1.0 | 4 | 5.0 | The simplest complete booking flow |
| **In-app messaging (pre-booking)** | 5 | 4 | 1.0 | 3 | 6.7 | Families need to communicate before committing |
| **WhatsApp handoff post-booking** (deep link with pre-filled message) | 5 | 4 | 1.0 | 1 | 20.0 | Highest RICE score. Dead simple. Israelis expect this. |
| **Background check verification** (manual process, not automated) | 5 | 5 | 0.9 | 3 | 7.5 | Non-negotiable for childcare. Manual = slower but viable for 100 nannies. |
| **ID verification** (Teudat Zehut upload + manual review) | 5 | 5 | 0.9 | 2 | 11.3 | Safety gate before going live |
| **Sex offender registry check** (manual via Israel Police) | 5 | 5 | 0.9 | 2 | 11.3 | Legal requirement for childcare |
| **Basic nanny availability calendar** (weekly recurring blocks) | 5 | 4 | 1.0 | 3 | 6.7 | Prevents wasted requests |
| **Push notifications** (booking requests, acceptances, reminders) | 5 | 4 | 1.0 | 2 | 10.0 | Nannies MUST know when a request arrives |
| **Basic reviews** (star rating + text, blind, post-session) | 4 | 4 | 1.0 | 3 | 5.3 | Trust building from day 1 |
| **Hebrew RTL UI** | 5 | 5 | 1.0 | 3 | 8.3 | Non-negotiable for Israeli market |
| **Basic admin panel** (approve profiles, manage reports, view activity) | 1 | 5 | 1.0 | 4 | 1.3 | Low reach (only admins) but critical for operations |

#### SHOULD HAVE (v1 stretch goals or early v2)

| Feature | R | I | C | E | RICE | Rationale |
|---------|---|---|---|---|------|-----------|
| **"My Nannies" list** (previous bookings) | 3 | 4 | 1.0 | 1 | 12.0 | High RICE, simple to build. Enables repeat bookings. |
| **Favorites/bookmarking** | 3 | 3 | 1.0 | 1 | 9.0 | Low effort, improves UX |
| **Parent rating of nannies visible to other parents** | 3 | 4 | 0.8 | 2 | 4.8 | Reviews need volume to be useful -- won't have this at launch |
| **Nanny rating of families** (two-sided reviews) | 3 | 3 | 0.8 | 2 | 3.6 | Important for nanny retention but can launch without |
| **Short Notice booking (Tier 2)** — request to 3 nannies, 4hr window | 3 | 4 | 0.9 | 4 | 2.7 | More complex multi-request logic. Add once Tier 3 is proven. |
| **Basic earning summary for nannies** | 4 | 3 | 1.0 | 2 | 6.0 | Nanny engagement feature |
| **Email notifications** (daily digest) | 3 | 2 | 1.0 | 1 | 6.0 | Low effort supplement to push |
| **English language option** | 2 | 3 | 1.0 | 3 | 2.0 | Olim segment is #2 priority but small at launch |
| **Profile completeness indicator for nannies** | 4 | 2 | 0.8 | 1 | 6.4 | Nudges better profiles, cheap to build |
| **Cancellation policy display** | 4 | 3 | 1.0 | 1 | 12.0 | Simple text, sets expectations |

#### COULD HAVE (v2 — months 3-6)

| Feature | R | I | C | E | RICE | Rationale |
|---------|---|---|---|---|------|-----------|
| **Emergency booking (Tier 1)** — broadcast to 5, 15-min window | 2 | 4 | 0.7 | 6 | 0.9 | Complex real-time system. Needs critical mass of supply to work. |
| **Recurring booking (Tier 4)** — job post + applicants | 2 | 4 | 0.8 | 5 | 1.3 | Different UX paradigm. Validate demand for regular care first. |
| **Social trust graph** — phone contacts, connections, vouching | 3 | 4 | 0.7 | 7 | 1.2 | Our key differentiator BUT needs network density. Useless with 100 users. |
| **Community groups** (neighborhood, school, gan) | 2 | 3 | 0.6 | 5 | 0.7 | Needs community scale. Build when you have 500+ parents per neighborhood. |
| **Trust tiers** (Verified -> Established -> Trusted -> Premium) | 3 | 3 | 0.8 | 3 | 2.4 | Meaningful only after nannies have booking history |
| **Automated background check integration** | 3 | 4 | 0.7 | 6 | 1.4 | Automate once manual process is bottleneck (100+ nanny signups/week) |
| **Surge pricing for emergency** (1.3x multiplier) | 1 | 2 | 0.6 | 3 | 0.4 | Needs Emergency tier first |
| **In-app payment processing** | 4 | 3 | 0.7 | 7 | 1.2 | Families can pay nannies directly (cash/Bit/PayBox). Platform fee via subscription or separate charge. |
| **Family subscription tier** (NIS 69/mo Premium) | 3 | 3 | 0.7 | 4 | 1.6 | Monetization v2. Start free, add paid once value is proven. |
| **Per-booking platform fee** (NIS 25) | 3 | 3 | 0.7 | 3 | 2.1 | Simpler monetization than subscription. Can test with manual invoicing first. |
| **SMS fallback notifications** | 3 | 3 | 0.8 | 2 | 3.6 | Useful for emergency tier reliability |
| **Nanny dashboard** (stats, tier progress, earnings breakdown) | 4 | 2 | 0.8 | 4 | 1.6 | Retention feature, not acquisition feature |
| **Content monitoring** (phone number detection in messages) | 3 | 3 | 0.7 | 4 | 1.6 | Prevent off-platform booking. Not critical at 100 users (you know everyone). |
| **First-time booking safety checklist** | 4 | 3 | 0.9 | 2 | 5.4 | Good UX but not blocking transactions |
| **Video introduction for nannies** | 2 | 2 | 0.6 | 3 | 0.8 | Nice trust signal, low priority |

#### WON'T HAVE (v3+ — months 6-12+)

| Feature | Reason to Defer |
|---------|----------------|
| **Full matching algorithm** (100-point scoring, 7 weighted factors) | Overkill with <500 nannies. Simple distance + availability + rating sort is sufficient for MVP. |
| **ML-based notification relevance filtering** | Needs months of behavioral data. Ship basic notification caps first. |
| **Cascading broadcast logic** (expand radius after timeout) | Needs Emergency tier + significant supply density |
| **"Suggest Different Time" counter-proposals** | Nice UX, not essential. Nannies can message alternatives. |
| **Emergency replacement auto-trigger** | Complex system, rare scenario at MVP scale |
| **Israeli calendar integration** (Hebrew dates, Shabbat times, chag awareness) | Can handle manually via push campaigns for first year |
| **Arabic language support** | Target segment is v3+ |
| **Special needs matching vertical** | Premium feature requiring specialized supply |
| **B2B corporate dashboard** | B2B revenue is Year 1+ goal, not MVP |
| **Nanny share matching** | Needs community density |
| **Subsidy navigator tool** | Growth tool, not core product |
| **Employment law toolkit** (Bituach Leumi templates) | Value-add, not core |
| **Insurance marketplace** | Partnership, not tech |
| **Anti-gaming rules** (fake review detection, connection fraud) | Premature optimization at 200 users |
| **"Available Now" toggle** | Needs Emergency tier |
| **Rate range negotiation** (nanny sets 40-55 range) | Start with fixed rate. Add ranges later. |
| **Auto-block calendar on booking** | Can be manual at low volume |
| **Notification quiet hours (22:00-07:00)** | Nice but not blocking |
| **Pre-holiday surge prompts** | Marketing, not product |

---

## PART 3: v1 MVP SCOPE — WHAT TO BUILD FIRST

### 3.1 The One-Sentence MVP

**"A Hebrew mobile app where Tel Aviv parents search verified babysitters by location and availability, send a booking request, and coordinate via WhatsApp."**

### 3.2 Which Booking Tier to Launch With

**Answer: Tier 3 (Advance Booking) ONLY.**

| Tier | MVP? | Why |
|------|------|-----|
| **Tier 1: Emergency** | NO | Requires critical mass of available supply, real-time broadcast system, cascading logic, SMS integration. Technically complex, operationally demanding. Dead on arrival with 100 nannies. |
| **Tier 2: Short Notice** | NO | Multi-request logic (select 3, first-accept wins) adds significant complexity. Add in v1.5 once single-request flow is proven. |
| **Tier 3: Advance Booking** | **YES** | Parent browses, selects 1 nanny, sends request, nanny has 24hr to respond. Simplest flow. Validates core matching. |
| **Tier 4: Recurring** | NO | Job-post paradigm with multiple applicants is a different product. Validate one-off booking first. |

### 3.3 Trust & Safety Scope for MVP

| Component | MVP Approach | Why Not Full Version |
|-----------|-------------|---------------------|
| **Background checks** | **Manual.** Nanny uploads Teudat Zehut. Team manually initiates Israel Police check. Results entered manually into admin panel. | Automated integration with Israel Police takes months to establish + legal agreements. Manual works for first 100-200 nannies. |
| **Sex offender check** | **Manual.** Included in background check process. | Same as above. |
| **ID verification** | **Semi-manual.** Nanny uploads ID photo + selfie. Team manually compares. | Full Persona/Onfido integration is v2. Manual comparison is reliable at low volume. |
| **Reviews** | **Basic.** Star rating (1-5) + text. Blind (both sides submit before seeing the other). Post-session prompt. | No trust tiers, no vouching, no social proof. Build review volume first. |
| **Trust graph** | **NONE in v1.** | The trust graph is our long-term differentiator but is worthless with <500 users. Social connections need density. Launch with reviews + verification badges only. |
| **Content monitoring** | **Manual.** Admin reviews flagged messages. | Automated phone-number detection and spam filtering is v2. At 100 users, you can review manually. |

### 3.4 Payment Scope for MVP

**Answer: NO in-app payment for v1.**

| Option | Recommendation | Rationale |
|--------|---------------|-----------|
| In-app payment processing | **DEFER** | Payment integration (Stripe/Tranzila/PayPlus) adds 3-4 weeks of development, PCI compliance burden, refund logic, and the legal complexity of holding funds. At 100 users, families can pay nannies directly. |
| How families pay nannies | **Direct payment** — cash, Bit, PayBox, bank transfer | This is how 90%+ of Israeli babysitter payments already work. Don't fix what isn't broken at MVP scale. |
| Platform revenue | **Free for MVP.** No subscription, no booking fee. | Validate matching before monetization. Care.com, UrbanSitter, and Sittercity all launched free. Charge once you've proven value. |
| When to add payment | **v2 (month 3-6)** when you need to: (a) charge a platform fee, or (b) implement cancellation fees | Payment is a monetization feature, not a matching feature. |

### 3.5 Notification Scope for MVP

| Channel | MVP? | Implementation |
|---------|------|---------------|
| **Push notifications** | YES | Firebase Cloud Messaging. Booking requests, acceptances, reminders. |
| **SMS** | NO | Only needed for Emergency tier (not in MVP). Push is sufficient for 24hr response windows. |
| **Email** | MINIMAL | Registration confirmation, booking confirmation receipts. No daily digests. |
| **WhatsApp** | YES (post-booking) | Simple deep link: `https://wa.me/{phone}?text={prefilled}`. Zero API integration needed. |

### 3.6 Complete v1 Feature List

**Parent Side:**
1. Registration (email + phone verification)
2. Family profile (children count, ages, neighborhood, languages)
3. Search nannies (filters: distance, availability, rate, age experience, languages)
4. View nanny profiles (photo, bio, experience, rate, reviews, verification badge)
5. Send booking request (date, time, number of kids, special notes)
6. Receive nanny acceptance/decline notification
7. Confirm booking
8. View booking details + WhatsApp link to nanny
9. Leave review after session (stars + text)
10. View upcoming and past bookings
11. In-app messaging with nanny (pre-booking)
12. Report an issue (simple form to admin)

**Nanny Side:**
1. Registration (email + phone verification)
2. Profile creation (name, photo, bio, experience, languages, rate, availability)
3. Upload ID for verification
4. Background check consent + document upload
5. Set weekly availability calendar
6. Receive booking request notifications (push)
7. View request details (neighborhood, children, time, earnings)
8. Accept / Decline request
9. View booking details + WhatsApp link to parent
10. Leave review of family after session
11. View upcoming and past bookings
12. In-app messaging with parent (pre-booking)

**Admin Side:**
1. Review and approve nanny profiles
2. Manage background check status (initiate, track, record results)
3. ID verification (compare upload vs selfie)
4. View all bookings
5. Handle reported issues
6. Basic metrics (signups, bookings, active users)

### 3.7 What Is Explicitly NOT in v1

| Excluded Feature | Why | When to Add |
|-----------------|-----|-------------|
| Emergency / Same-Day booking | Needs supply density | v2 (month 4-6) |
| Short Notice booking | Multi-request complexity | v1.5 (month 2-3) |
| Recurring booking | Different product paradigm | v2 (month 4-6) |
| Social trust graph | Needs network density | v2 (month 4-6) |
| Community groups | Needs user volume | v3 (month 8-12) |
| Trust tiers (badges) | Needs booking history | v2 (month 3-6) |
| In-app payments | Adds complexity, not needed | v2 (month 3-6) |
| Subscription / fees | Validate value first | v2 (month 4-6) |
| Automated background checks | Manual works at scale <200 | v2 (month 4-6) |
| B2B corporate module | Revenue stream for later | v3 (month 6-12) |
| Arabic / English UI | Target segment is Hebrew first | v2-v3 |
| Matching algorithm (weighted scoring) | Simple sort is fine for <500 nannies | v2 (month 4-6) |
| Surge pricing | Needs emergency tier | v3 |
| Cancellation fees | Needs payment integration | v2 |
| Nanny video intro | Nice-to-have | v2 |
| ML-based notification filtering | Needs data | v3+ |

---

## PART 4: v2 SCOPE — MONTHS 3-6

### 4.1 v2 Goal
**From "it works" to "it's worth paying for."** Introduce monetization, second booking tier, trust signals, and payment infrastructure.

### 4.2 v2 Feature Set

**Booking & Matching:**
- Short Notice booking (Tier 2) -- multi-request to 3 nannies, 4hr window
- "My Nannies" list with one-tap rebooking
- Matching algorithm v1 (distance + availability + rating + response rate weighted scoring)
- Nanny counter-proposal ("Suggest Different Time")
- First-time booking safety checklist display

**Trust & Safety:**
- Trust tiers (Verified -> Established -> Trusted) based on booking count + rating
- Social trust graph v1 -- phone contact matching ("5 people in your contacts use this app")
- Automated ID verification (Persona or equivalent integration)
- Semi-automated background check pipeline (API integration with provider)
- Content monitoring -- automated phone number detection in pre-booking messages
- Two-sided review display (nannies can see parent ratings before accepting)

**Monetization:**
- Per-booking platform fee (NIS 19-29 charged to family)
- OR Family subscription (NIS 69/mo for unlimited messaging + priority features)
- A/B test both models to see which converts better
- Payment integration (Israeli processor: Tranzila, PayPlus, or cardcom)
- Platform fee charged at booking confirmation, nanny paid directly by family

**Nanny Experience:**
- Nanny dashboard (earnings summary, response rate, rating, tier progress)
- Profile completeness scoring with nudges
- Video introduction upload

**Platform:**
- English language option (for olim segment)
- SMS notifications for Short Notice tier
- Notification caps (max 3/day for nannies)
- Cancellation policy enforcement (with payment integration)
- Analytics dashboard for admins (cohort retention, booking completion rate, supply/demand ratio by neighborhood)

### 4.3 v2 Key Decisions to Make Based on v1 Data

| Decision | Data Needed from v1 |
|----------|---------------------|
| Subscription vs. per-booking fee | Which do users prefer? What's the price elasticity? |
| Add Emergency booking? | Do enough nannies keep "Available Now" status? What % of requests are same-day? |
| Trust graph worth building? | How often do users ask "who else has used this nanny"? Do friends refer friends? |
| Expand to Jerusalem? | Is Tel Aviv supply/demand balanced? Unit economics proven? |

---

## PART 5: v3 SCOPE — MONTHS 6-12

### 5.1 v3 Goal
**From "a Tel Aviv babysitter app" to "Israel's childcare platform."** Geographic expansion, B2B revenue, advanced trust, full booking tiers.

### 5.2 v3 Feature Set

**Booking & Matching:**
- Emergency booking (Tier 1) -- real-time broadcast, 15-min window, cascading radius
- Recurring booking (Tier 4) -- job posting with applicant management
- Full matching algorithm (100-point scoring with all 7 factors)
- Emergency replacement auto-trigger when nanny cancels <6hr
- Smart notification routing (ML-based relevance, quiet hours, batching)

**Trust & Social:**
- Full social trust graph -- explicit connections, community groups, vouching
- Community groups (neighborhood, school, gan)
- "Premium" trust tier (25+ bookings, first aid certified)
- Vouching system (limited to 5 vouches per parent)
- Anti-gaming (fake review detection, connection fraud prevention)

**B2B Corporate:**
- Corporate employer onboarding portal
- Employee benefit dashboard
- HR admin panel (usage reports, budget management)
- Corporate booking tier with employer subsidy
- 3-5 pilot corporate clients (target: Check Point, Monday.com, Wix, CyberArk, Fiverr)

**Growth & Expansion:**
- Jerusalem and Haifa launch
- Arabic language support
- Special needs matching vertical
- Israeli calendar integration (Hebrew dates, Shabbat, chag awareness, school schedule)
- Pre-holiday surge prompts and seasonal push campaigns
- "Subsidy navigator" -- help eligible families find unclaimed government childcare subsidies
- Employment law toolkit (Bituach Leumi templates, payslip generator)

**Advanced Platform:**
- Insurance partnership integration
- Nanny share matching
- Advanced admin analytics (LTV, CAC, marketplace liquidity, supply/demand heatmaps)
- Rate range negotiation (nanny sets range, family sees it)
- "Available Now" toggle for nannies

---

## PART 6: WHAT NOT TO BUILD (Validated Learning First)

### 6.1 Features That Need Scale to Work

These features are mathematically useless below certain thresholds. Building them early wastes engineering time and creates empty-room experiences that hurt trust.

| Feature | Minimum Scale Required | Why |
|---------|----------------------|-----|
| **Social trust graph** | 500+ parents per neighborhood | With 100 total users, the probability of two connected parents is near zero. "0 friends have used this nanny" is WORSE than not showing the feature at all. |
| **Emergency booking (15-min broadcast)** | 50+ available nannies in a 5km radius at any given time | If only 3 nannies are available and none respond in 15 min, the feature fails 100% of the time. Each failure destroys trust. |
| **Community groups** | 50+ parents per group | Empty groups are worse than no groups. Wait until organic demand emerges. |
| **ML-based notification filtering** | 10,000+ data points (requests, responses, bookings) | ML needs data volume. Simple rules work better with small datasets. |
| **Matching algorithm (7-factor weighted scoring)** | 500+ nannies | With 100 nannies, simple distance + availability sort produces identical results to a complex algorithm. |
| **Anti-gaming / fraud detection** | 1,000+ reviews | Gaming is a scale problem. At 100 users, you know everyone personally. |
| **Surge pricing** | Consistent supply/demand imbalance data | Pricing optimization needs volume data to calibrate. |

### 6.2 Features That Need User Interview Validation First

**Do NOT build these until you've talked to 20+ users who explicitly ask for them:**

| Feature | Assumption to Validate | How to Validate |
|---------|----------------------|-----------------|
| **Nanny video introductions** | "Parents want to 'meet' nannies before booking" | Ask 20 parents: would a video change your booking decision? Or do reviews and verification suffice? |
| **In-app payment** | "Parents want to pay through the app" | Ask 20 parents: how do you pay your babysitter today? Would you switch? Or is Bit/cash fine? |
| **Nanny share (split babysitter between families)** | "Parents want to share nanny costs" | Is this a real need or a VC fantasy? Interview parents of toddlers in same building. |
| **First aid certification as a filter** | "Parents prioritize first aid certification" | How many parents actually ask for this vs. assume it's nice-to-have? |
| **Recurring booking with trial period** | "Parents want to formalize ongoing arrangements through the app" | Or do they just want to find a nanny once and then arrange directly via WhatsApp forever? |
| **Subscription vs. per-booking fee** | "Parents prefer predictable subscription" | Price sensitivity testing: NIS 69/mo vs. NIS 25/booking. Which converts better? |

### 6.3 The "Do Things That Don't Scale" List

Following Paul Graham's principle, these are things to do MANUALLY in v1 that you'll automate later:

| Manual v1 Process | Automated v2+ Version |
|-------------------|----------------------|
| Admin team manually reviews ID photos vs selfies | Persona / Onfido automated facial comparison |
| Admin team initiates Israel Police background checks by email/form | API integration with background check provider |
| Admin team manually approves nanny profiles after review | Automated approval with ML-flagged edge cases for human review |
| Founders personally onboard first 50 nannies (meet in person, help with profile) | Self-service onboarding with in-app guidance |
| Founders personally match difficult cases ("I need a Russian-speaking sitter in Bat Yam tonight") | Matching algorithm + emergency broadcast |
| Support via WhatsApp group with founders | In-app support chat + help center |
| Marketing via personal WhatsApp messages to parent groups | Paid acquisition + referral system |
| Track bookings and metrics in Google Sheets | Admin analytics dashboard |
| Manually send review reminders | Automated post-session review prompts |
| Manually invoice platform fee (when monetizing) | Integrated payment processing |

---

## PART 7: ISRAELI STARTUP MVP LESSONS

### 7.1 How Israeli Startups Scoped MVPs

| Startup | MVP Approach | Key Lesson for Us |
|---------|-------------|-------------------|
| **Gett** (2011) | Tel Aviv-only beta, Hebrew-only, licensed taxis only. Later pivoted hard into B2B corporate transportation -- which became their real business. Acquired by Goldcar in 2024 for $175M (down from $1.5B peak valuation). | **Start B2C to validate, but plan for B2B.** Gett's B2C was the wedge; B2B corporate was the real revenue. Our trajectory should mirror this: B2C nanny matching to validate -> B2B corporate childcare benefit as the growth engine. |
| **Wolt Israel** (2018) | Launched with self-pickup from 26 restaurants in Tel Aviv. NOT delivery. Pickup was "easiest way to get running." Added delivery later. | **Launch with the SIMPLEST version.** If Wolt could skip delivery (their core product!), we can skip Emergency booking, in-app payments, and the trust graph. |
| **Monday.com** (2014) | "daPulse" launched with task assignments + one-click updates. Nothing more. No Gantt charts, no automations, no integrations. | **Nail ONE workflow.** Our one workflow: parent searches -> finds nanny -> sends request -> nanny accepts -> they connect on WhatsApp. That's it. |
| **Fiverr** (2010) | Everything costs $5. ONE price point. Freelancers create "gigs" (fixed-scope services). Dead simple. Later added tiers, packages, Pro, Business. | **Simplify to the point of absurdity.** One booking tier. One search flow. One way to connect. Complexity is for later. |
| **Wix** (2006) | Free website builder. One template category. Basic drag-and-drop. No e-commerce, no SEO tools, no custom domains initially. | **Free-to-use MVP.** Don't charge until you've proven the product works. Wix was free for years before monetizing aggressively. |

### 7.2 Israeli Market-Specific MVP Considerations

| Factor | Implication for MVP |
|--------|-------------------|
| **Small country, dense networks** | Word-of-mouth spreads fast in Israel. 10 happy users in Ramat Aviv = 50 referrals. Invest in onboarding quality over quantity. |
| **WhatsApp is king** | Don't fight it. WhatsApp is the post-booking channel. Your app is the pre-booking channel (discovery, verification, reviews). Draw the line clearly. |
| **Hebrew UX is non-negotiable** | No Israeli consumer app has succeeded in English-only. Full RTL, Hebrew copy, NIS currency, DD/MM/YYYY, 24-hour time. |
| **Israelis are blunt reviewers** | Reviews will be honest and detailed. This is an ASSET. Lean into it -- Israeli reviews will be more useful than polite American ones. |
| **Thursday night = date night** | Your biggest demand spike will be Thursday 18:00-22:00. Optimize notifications and supply for this. |
| **Post-army/sherut leumi = supply goldmine** | 50K+ young adults finish service each year. Many babysit. Target with university job boards, post-service Facebook groups, and word of mouth. |
| **Chutzpah = fast feedback** | Israeli users will tell you what's wrong immediately. Your first 100 users are a built-in user research panel. Embrace the bluntness. |
| **Trust through people, not brands** | Israelis trust hamlatza (personal recommendation) over brand marketing. This validates our eventual trust graph -- but at MVP, the "hamlatza" is you (the founders) personally recommending nannies. |

---

## PART 8: MVP SUCCESS METRICS & MILESTONES

### 8.1 North Star Metric

**Completed bookings per week.** Not signups, not searches, not messages -- completed bookings where a family and nanny actually met.

### 8.2 MVP Milestones (First 90 Days)

| Milestone | Target | Timeframe | How to Measure |
|-----------|--------|-----------|----------------|
| Nannies onboarded | 100 verified | Week 1-6 | Admin panel count |
| Families registered | 100 | Week 4-8 | Registration count |
| First booking completed | 1 | Week 5-6 | Manual tracking |
| Bookings per week | 10 | Week 8-10 | Database query |
| Booking completion rate | >60% (requests that result in completed sessions) | Week 8-12 | requests -> acceptances -> completions |
| Repeat booking rate | >30% (families who book again within 30 days) | Week 10-14 | Cohort analysis |
| NPS (families) | >40 | Week 10-12 | Survey |
| NPS (nannies) | >40 | Week 10-12 | Survey |
| Supply liquidity | >70% of requests get at least 1 acceptance within 24hr | Week 8-12 | Database query |

### 8.3 Kill Criteria

**If by week 12, you don't have 10 bookings/week with a >50% completion rate, STOP and pivot.** Either:
- The value proposition is wrong (parents don't want this)
- The geography is wrong (Tel Aviv isn't the right beachhead)
- The supply is wrong (can't attract quality nannies)
- The UX is wrong (flow is too complex)

Before pivoting the business, interview 20 churned users to understand WHY.

---

## PART 9: MVP DEVELOPMENT APPROACH

### 9.1 Recommended Build Strategy

| Approach | Recommendation | Rationale |
|----------|---------------|-----------|
| **Native vs Cross-platform** | Cross-platform (React Native or Flutter) | Ship to iOS + Android simultaneously. Israeli market is ~50/50. |
| **Build vs Buy** | Build core, buy infrastructure | Use Firebase (auth, push, hosting), Cloudinary (images), SendGrid (email). Build matching, profiles, booking logic. |
| **Mobile-first vs Web** | Mobile-first with basic web | 80%+ of target users will discover and use on mobile. Admin panel is web-only. |
| **Team size** | 2-3 developers + 1 designer + founders | Lean. Founders handle ops, marketing, manual processes. |
| **Timeline** | 8-12 weeks to v1 launch | Assuming full-time team, clear spec. |

### 9.2 Technical MVP Shortcuts

| Shortcut | Details |
|----------|---------|
| **No matching algorithm** | Sort by distance, then by rating. WHERE distance < 5km AND available = true ORDER BY distance, rating DESC. That's your v1 "algorithm." |
| **No payment system** | Families pay nannies directly. Platform is free. When you monetize, start with manual invoicing (Google Forms + bank transfer). |
| **No real-time features** | No live location tracking, no real-time chat (polling-based messaging is fine), no live notifications dashboard. |
| **Admin panel = basic CRUD** | Don't build a beautiful admin dashboard. A table of users, a table of bookings, approve/reject buttons. That's it. |
| **Background checks = Google Form** | Nanny fills out consent form -> admin downloads it -> admin emails Israel Police -> admin updates status in admin panel. |

---

## PART 10: ROADMAP SUMMARY

```
MONTH 0-2: BUILD MVP
  - Core app: profiles, search, advance booking, messaging, push notifications
  - Hebrew RTL UI
  - Manual background checks, ID verification
  - WhatsApp deep link post-booking
  - Basic reviews (stars + text)
  - Admin panel (approve profiles, manage checks, view bookings)

MONTH 2-3: SOFT LAUNCH (Tel Aviv)
  - Recruit 100 nannies (manual onboarding, in-person where possible)
  - Invite 100 families (founder network, WhatsApp groups, university parents)
  - Everything free
  - Founders do support via WhatsApp
  - Track: bookings/week, completion rate, repeat rate, NPS

MONTH 3-4: LEARN & ITERATE (v1.5)
  - Add Short Notice booking (Tier 2) if demand exists
  - Add "My Nannies" list + repeat booking
  - Add favorites
  - Fix top 10 UX issues from user feedback
  - Grow to 250 nannies, 300 families

MONTH 4-6: MONETIZE (v2)
  - Introduce platform fee (test subscription vs per-booking)
  - Add payment integration (Israeli processor)
  - Trust tiers (Verified -> Established -> Trusted)
  - Social trust graph v1 (phone contacts)
  - Semi-automated background checks
  - English language option
  - Nanny dashboard
  - Expand to Herzliya, Ra'anana (adjacent Tel Aviv suburbs)

MONTH 6-9: SCALE (v2.5)
  - Emergency booking (Tier 1)
  - Recurring booking (Tier 4)
  - Full matching algorithm
  - Community groups
  - First B2B corporate pilot (1-2 tech companies)
  - Jerusalem launch
  - SMS fallback notifications

MONTH 9-12: PLATFORM (v3)
  - B2B corporate module (HR dashboard, usage reports)
  - Arabic language support
  - Special needs vertical
  - Israeli calendar integration
  - Nanny share matching
  - Advanced analytics
  - Insurance partnership
  - Target: 2,000 nannies, 5,000 families, 500 bookings/week, 3-5 B2B contracts
```

---

## APPENDIX: SOURCES

**Marketplace MVP Research:**
- [Care.com at 10: Where We've Been](https://www.care.com/c/carecom-at-10-where-weve-been-and-where-w/)
- [Care.com Wikipedia](https://en.wikipedia.org/wiki/Care.com,_Inc.)
- [UrbanSitter Startup Story - Jungleworks](https://jungleworks.com/how-urbansitter-helps-find-reliable-babysitters-online-startup-stories-16/)
- [UrbanSitter CEO Interview - Paste Magazine](https://www.pastemagazine.com/business/lynn-perkins/an-interview-with-lynn-perkins-ceo-of-urbansitter)
- [How We Launched Bubble - Start Up Donut](https://www.startupdonut.co.uk/set-up-a-business/starting-an-online-business/how-we-launched-our-babysitting-app-bubble)
- [Bubble Childcare App - Maddyness UK](https://www.maddyness.com/uk/2025/03/04/meet-bubble-the-childcare-app-loved-by-parents/)
- [Airbnb MVP - Fueled](https://fueled.com/blog/airbnb-mvp/)
- [Uber MVP - Dittofi](https://www.dittofi.com/learn/uber-mvp)
- [Flashback to Uber's MVP - Dogantech](https://www.dogantech.co.uk/blog/flashback-to-ubers-mvp)
- [Sittercity Raises $22.6M - TechCrunch](https://techcrunch.com/2011/04/27/sittercity-raises-22-6-million-to-connect-families-with-caregivers/)

**Israeli Startups:**
- [Gett Wikipedia](https://en.wikipedia.org/wiki/Gett)
- [Gett's Bumpy Ride - Calcalist](https://www.calcalistech.com/ctechnews/article/z7e247fjo)
- [Wolt CEO Message - 10 Years](https://life.wolt.com/en/isr/moments/10-years/ceo-message)
- [Wolt Comes to Tel Aviv - Calcalist](https://www.calcalistech.com/ctech/articles/0,7340,L-3747159,00.html)
- [Monday.com Founder Story - Frederick.ai](https://www.frederick.ai/blog/roy-mann-monday-com)
- [Monday.com IPO - Insight Partners](https://www.insightpartners.com/ideas/scaleup-milestone-series-monday-coms-ipo/)
- [Israel Tech Hub - Startup Nation Central](https://startupnationcentral.org/hub/blog/israel-tech-hub-explained/)
- [Israeli Startup Culture - Square Peg](https://www.squarepeg.vc/blog/what-makes-israels-startup-culture-world-class)

**MVP & Marketplace Strategy:**
- [Minimum Viable Platform - Sharetribe](https://www.sharetribe.com/academy/how-to-build-a-minimum-viable-platform/)
- [19 Marketplace Tactics - NFX](https://www.nfx.com/post/19-marketplace-tactics-for-overcoming-the-chicken-or-egg-problem)
- [Do Things That Don't Scale - Paul Graham](https://www.paulgraham.com/ds.html)
- [Feature Prioritization Frameworks - Plane](https://plane.so/blog/feature-prioritization-frameworks-rice-moscow-and-kano-explained)
- [RICE vs MoSCoW - Ramen Club](https://www.ramenclub.so/blog/rice-moscow-methods-prioritization-framework)
- [Helpr Corporate Childcare - Employee Benefit News](https://www.benefitnews.com/news/helpr-offers-employees-new-in-app-feature-for-backup-child-care)
- [Helpr About](https://www.hellohelpr.com/about-helpr)
- [Marketplace MVP 2026 - Roobykon](https://roobykon.com/blog/posts/how-to-build-an-online-marketplace-mvp-in-2026)

---

*This document defines MVP scope based on research from 12+ marketplace startups, Israeli startup ecosystem analysis, and rigorous RICE scoring of all features from the matching flow specification. It does not constitute product or business advice.*
