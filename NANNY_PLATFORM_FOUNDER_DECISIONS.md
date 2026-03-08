# Nanny Platform: 10 Founder Decisions -- Ranked Recommendations

**Date:** March 7, 2026
**Prepared by:** Chief Advisor (Synthesis of 5 research agents + 16 prior research documents)
**Purpose:** Give the founder a single document with clear, graded recommendations for every pre-PRD decision
**How to use:** Read the Quick Decision Summary first. Then dive into any decision that needs debate.

---

## IF YOU ONLY READ ONE PAGE

You are building a **Hebrew-first trust marketplace** for Israeli families and nannies. Here is what to do:

1. **Name it Emuni** -- Hebrew for "my trust." The name IS your value proposition.
2. **Find a technical co-founder (50/50).** Israeli VCs won't fund a non-technical solo founder building a marketplace. You save NIS 744K/year vs hiring.
3. **Use the IIA-Anchored Angel Round.** Apply for Tnufa (NIS 200K, free money) immediately. Close an angel syndicate (NIS 1-1.5M) in parallel. IIA matches 60-66%. Total pre-seed: NIS 2-3.15M at only 10-12% dilution.
4. **Launch in Old North Tel Aviv only.** 50 nannies in 5 km2 = 10/km2 = thriving density. The original 4-neighborhood plan spreads 100 nannies across 30 km2 = barely viable 3.3/km2.
5. **Hebrew first, English at Month 4-6.** Build i18n from Day 1 but ship Hebrew only. Anglos in TLV manage. English unlocks Ra'anana expansion.
6. **Charge from Day 1 (freemium).** Free tier: browse + 1 booking/month. Premium: NIS 49/mo. Per-contact: NIS 19. Validates willingness to pay immediately. Avoids the "free anchor" trap that causes 80% churn.
7. **No in-app payments in v1.** Families pay nannies directly (Bit/cash). Collect platform subscription/per-contact fees via manual Bit invoicing for first 50 users. Integrate PayPlus at Month 3.
8. **Platform pays for background checks.** NIS 47/nanny is your cheapest trust investment. Eliminates supply-side friction. Budget NIS 4,700 for first 100 nannies.
9. **Defer Nanny Pro tier.** Employment Service Law gray zone. Get attorney sign-off before charging nannies anything.
10. **No emergency booking, no B2B in v1.** Both need density/traction you don't have yet. Start B2B conversations at Month 3, sign first contract Month 6+.

**Total cost to implement all decisions above:** NIS 2-3M pre-seed gets you to Month 6 with a launched, revenue-generating MVP in Old North TLV, positioned for a NIS 5-7M seed round with IIA matching.

---

## QUICK DECISION SUMMARY

| # | Decision | Our #1 Pick | Grade | Key Reason | Decide Before |
|:-:|----------|-------------|:-----:|------------|:-------------:|
| 1 | Company name | **Emuni** (My Trust) | A | Name = value prop. Hebrew root, global sound. Follows Taboola/Tipalti pattern. | PRD |
| 2 | Co-founder? | **Technical co-founder, 50/50** | A | 21/25 score. Saves NIS 744K/yr. VCs require it. Faster MVP (4-6 mo). | Immediately |
| 3 | Funding strategy | **IIA-Anchored Angel Round** | A | NIS 9.7-14.2M total, only 25-32% dilution. NIS 3.7-5.7M is free (IIA). | Immediately |
| 4 | Launch geography | **Old North TLV single beachhead** | A+ | 9.40/10 score. 50 nannies in 5 km2 = thriving 10/km2 density. | PRD |
| 5 | Language strategy | **Hebrew-first, English Month 4-6** | A | Build i18n Day 1, ship Hebrew only. 90% of target market is Hebrew-proficient. | PRD |
| 6 | Monetization timing | **Freemium from Day 1 (NIS 49/mo)** | A | 20/25 score. Revenue validation from week 1. No free-to-paid transition shock. | PRD |
| 7 | In-app payments | **No (families pay nannies directly)** | A | Saves 3-4 weeks dev. No PCI compliance. Add PayMe/PayPlus in v2. | PRD |
| 8 | Background check cost | **Platform pays (NIS 47/nanny)** | A- | Removes #1 supply-side friction. NIS 4,700 for 100 nannies. Cheapest trust signal. | PRD |
| 9 | Nanny Pro tier | **Defer (get attorney sign-off)** | B+ | Employment Service Law prohibits charging job seekers. Gray zone. Don't risk it pre-launch. | Post-attorney |
| 10 | Emergency booking / B2B in MVP | **No / Start conversations only** | A | Emergency needs 50+ available nannies in 5km. B2B needs traction data. | PRD |

---

## DECISION DEPENDENCIES MAP

Decisions are not independent. Here is what affects what:

```
FUNDING (#3) ──────> CO-FOUNDER (#2)
  IIA grant timeline     If bootstrap: solo is possible but painful
  affects when you       If raise: VCs strongly prefer co-founding teams
  can hire               IIA-Anchored Angel strategy assumes co-founder

CO-FOUNDER (#2) ───> LAUNCH SPEED (#4)
  With co-founder:       With CTO: MVP in 4-6 months, launch Month 0
  4-6 mo to MVP          Without: 6-8+ months, launch delays everything

NAME (#1) ─────────> LAUNCH GEOGRAPHY (#4)
  Hebrew name (Emuni)    Reinforces Hebrew-first TLV launch
  English name           Would suggest Anglo beachhead (not recommended)

GEOGRAPHY (#4) ────> LANGUAGE (#5)
  TLV Old North          Hebrew-first is correct
  Ra'anana beachhead     Would require English-first (not recommended)

MONETIZATION (#6) ─> PAYMENTS (#7)
  Freemium Day 1         Needs some payment mechanism (manual Bit OK for MVP)
  Free MVP               No payment infrastructure needed at all

BACKGROUND CHECKS (#8) ─> MONETIZATION (#6)
  Platform pays          Cost absorbed; nanny onboarding is frictionless
  Nanny pays             Creates supply-side friction; fewer nannies sign up

NANNY PRO (#9) ────> LEGAL RISK
  Defer                  Zero legal risk
  Launch                 Employment Service Law exposure; needs attorney

EMERGENCY BOOKING (#10) ─> GEOGRAPHY (#4)
  Needs density          Minimum 50 available nannies in 5km radius
  Old North only         Could work in Phase 2 (Month 6+) once density exists
```

**The critical chain:** Funding -> Co-founder -> Launch speed -> Everything else. Decisions #2 and #3 must be made first because they determine the timeline for everything downstream.

---

## DECISION #1: COMPANY NAME

### Context
The platform's core differentiator is TRUST -- verified background checks, community recommendations (hamlatzot), and safety. The name must signal trust in Hebrew culture while being pronounceable globally for future expansion.

### 5 Options Ranked

| Rank | Name | Hebrew | Meaning | Overall Grade |
|:----:|------|--------|---------|:------------:|
| **A** | **Emuni** | אמוני | "My trust" -- from root א-מ-ן (emun) | **A** |
| B | Kena | קנא | "Little nest" -- from ken (קן) | A- |
| C | Bubale | בובאלע | Yiddish/Hebrew endearment "darling" | A- |
| D | Shimri | שמרי | "Guard for me" -- imperative command | A- |
| E | Sitra | -- | Invented. Echoes "sitter" + Hebrew "seter" (shelter) | B+ |

### Detailed Grading

| Criterion (Weight) | Emuni | Kena | Bubale | Shimri | Sitra |
|---------------------|:-----:|:----:|:------:|:------:|:-----:|
| Memorability (25%) | A | A | A | B+ | B+ |
| Hebrew market fit (25%) | A | A | A+ | A | B+ |
| Domain availability (15%) | A | B+ | A | A | A |
| Scalability (20%) | A | B+ | B | B | A |
| Trust signal (15%) | A+ | A | A- | A | B+ |

### OUR RECOMMENDATION: Emuni

**Why Emuni wins:**
- The platform's entire value proposition is TRUST. The name IS the value proposition -- no explanation needed.
- 2 syllables, musical (eh-MOO-nee), works in Hebrew and English naturally
- Follows the proven Taboola/Tipalti pattern: Hebrew root word that sounds like a plausible global tech brand
- Most scalable: "trust" applies to any care vertical (senior care, tutoring, pet care, B2B)
- Passes the WhatsApp test: "מצאתי בייביסיטר מעולה באמוני"

**Risk:** "Emuna" has some religious connotations (faith in God). The possessive form "Emuni" (my trust) is more secular/personal, mitigating this. Verify with secular focus group.

**What changes if other options are chosen:**
- Kena: Stronger global play. Weaker trust signal. Logo becomes nest/bird. Need tagline to explain trust.
- Bubale: Strongest Israeli cultural play. Risk for B2B ("Bubale Corporate Childcare Benefits" may feel too playful for HR directors). 3 syllables.
- Shimri: Action-oriented. Feels like a feature, not a brand. May limit positioning beyond childcare.
- Sitra: Most "tech startup" feeling. Loses Israeli authenticity advantage. Sounds like any Silicon Valley app.

---

## DECISION #2: CO-FOUNDER STRATEGY

### Context
The founder is non-technical, building a technically complex platform (React Native + NestJS + PostGIS + real-time + AU10TIX + WhatsApp API + Hebrew RTL + IS 5568 accessibility). Israeli VCs strongly prefer complementary founding teams.

### 5 Options Ranked

| Rank | Option | Score | Overall Grade |
|:----:|--------|:-----:|:------------:|
| **A** | **Technical co-founder, equal partner (50/50 or 55/45)** | **21/25** | **A** |
| B | Accelerator path (8200 EISP / Techstars TLV) to find co-founder | 18/25 | B+ |
| C | Technical co-founder, minority stake (20-30%) | 16/25 | B |
| D | Solo founder + hire dev team | 11/25 | C+ |
| E | Business co-founder + outsource dev | 9/25 | C- |

### Detailed Grading

| Criterion | A: CTO 50/50 | B: Accelerator | C: CTO 20-30% | D: Solo+Hire | E: BizCo+Agency |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Speed to market | A- (4-6 mo) | C (9-12 mo) | B (6-8 mo) | B (6-8 mo) | B (6-8 mo) |
| 12-month cost | A- (NIS 996K) | A (NIS 500-700K) | B (NIS 1.1M) | C (NIS 1.74M) | B- (NIS 1.14M) |
| VC fundability | A+ | A- | A- | C | F |
| Team strength | A+ | A- | B | C | D |
| Risk level | B (co-founder conflict) | B (acceptance risk) | B (commitment) | C (single point) | D (no IP control) |

### OUR RECOMMENDATION: Option A -- Technical Co-Founder (50/50)

**Why this wins by a wide margin:**
1. **Israeli VCs require it.** Solo non-technical founders get 14.7% of VC capital vs 85.3% for teams. In an ecosystem where 70% of capital goes to AI/cyber, a consumer marketplace founder needs every advantage.
2. **NIS 744K/year savings.** Co-founder at NIS 20K/mo + 1 dev = NIS 996K/year vs solo with hired team at NIS 1.74M/year.
3. **Faster MVP.** Motivated co-founder codes from Day 1. 4-6 months vs 6-8+ months.
4. **Attracts better engineers.** Engineers want to work for technical leaders, not business founders managing contractors.
5. **50/50 splits are the new norm.** 45.9% of two-person teams chose 50/50 in 2024 (up from 31.5% in 2015).

**Fallback if no co-founder found in 2-3 months:**
Apply to 8200 EISP (free, 0% equity, 14K alumni network) + Techstars TLV + MassChallenge Israel. Engage a fractional CTO (NIS 15-25K/month) to start building while searching.

**Co-founder must-haves:** Can personally write production React Native + NestJS code (test this). Willing to go full-time. 4-year vesting with 1-year cliff (always, even for best friends).

**What changes in other docs if other options are chosen:**
- Option B (Accelerator): Add 3-6 months to timeline. PRD delayed. Potentially better funding terms (accelerator signal).
- Option C (20-30% CTO): Higher salary cost (NIS 30K/mo). May feel undervalued, retention risk.
- Option D (Solo+Hire): Cost Model changes: NIS 1.74M/year. Funding strategy changes: need larger pre-seed. VC pitch weakened.
- Option E (Outsource): Do not do this. VC fundraising becomes nearly impossible.

---

## DECISION #3: FUNDING STRATEGY

### Context
NIS 143K/mo pre-launch burn. NIS 7M total to breakeven (Month 20). NIS 329K/mo at launch. The platform cannot bootstrap to breakeven -- external capital is required.

### 5 Options Ranked

| Rank | Strategy | Total Capital (NIS) | Total Dilution | Overall Grade |
|:----:|----------|:-------------------:|:--------------:|:------------:|
| **A** | **IIA-Anchored Angel Round (Hybrid A+B)** | **9.7M-14.2M** | **25-32%** | **A** |
| B | VC-Fast Path (Pre-seed VC -> Seed) | 9.5M-13.5M | 27-43% | B+ |
| C | Grant-First Path (Tnufa -> Angels -> IIA -> Seed) | 9.5M-13.5M | 25-40% | B+ |
| D | Accelerator Path (Techstars/8200 -> Pre-seed -> Seed) | 7.5M-11.8M | 25-45% | B |
| E | Bootstrap (personal funds -> revenue -> raise later) | 3.7M-6.2M | 10-20% | C+ |

### Detailed Grading

| Criterion (Weight) | A: IIA-Angel | B: VC-Fast | C: Grant-First | D: Accelerator | E: Bootstrap |
|---------------------|:---:|:---:|:---:|:---:|:---:|
| Speed (20%) | B+ | A- | C+ | C | B |
| Dilution (25%) | A | B- | A | B- | A+ |
| Validation signal (20%) | A | A- | A- | A | C |
| Network access (15%) | B+ | A- | B | A | D |
| Risk (20%) | A- | B+ | B+ | B | C- |

### OUR RECOMMENDATION: Option A -- IIA-Anchored Angel Round

**Execution plan:**

| Step | Timing | Action | Capital (NIS) | Dilution |
|------|--------|--------|:------------:|:--------:|
| 1 | Month -8 | Apply for IIA Tnufa grant | 200,000 | 0% |
| 2 | Month -7 to -5 | Build pitch deck. Start angel conversations. | -- | -- |
| 3 | Month -5 | Tnufa approved. Use as validation signal. | (received) | -- |
| 4 | Month -5 to -3 | Close angel syndicate NIS 1-1.5M. Apply for IIA Pre-Seed (60-66% match). | 2,000,000-3,150,000 | 10-12% |
| 5 | Month -3 to 0 | Build MVP with full team. | -- | -- |
| 6 | Month 0 | Launch MVP in Old North TLV | -- | -- |
| 7 | Month 6-9 | Seed round NIS 5-7M VC + IIA Seed match (50-55%). | 7,500,000-10,850,000 | 15-20% |
| **TOTAL** | | | **9,700,000-14,200,000** | **25-32%** |

**Why this wins:**
- NIS 3.7-5.7M is IIA non-dilutive grants (free money)
- Female founder bonus: +10% on all IIA grants -- could add NIS 500K-1M+ across stages
- Each stage validates the next: Tnufa -> angels -> IIA match -> traction -> VC seed
- 68-75% founder equity retained through seed stage

**Best VC targets for seed:** lool Ventures (right pre-seed check size), Entree Capital (consumer-friendly), Aleph (consumer marketplace track record with Lemonade, Melio).

**Critical prerequisite:** Must have an Israeli registered company (Ltd.) for IIA grants.

**What changes if other options are chosen:**
- Option B (VC-Fast): Faster by 2-3 months. Miss NIS 1.5-1.65M free IIA pre-seed money. Higher dilution (27-43%).
- Option C (Grant-First): Slowest path (12-18 months to seed). Best dilution. Risk: competitors emerge while waiting.
- Option D (Accelerator): 3-6 month program delay. 5% equity to Techstars (expensive). Best for network.
- Option E (Bootstrap): NIS 143K/mo burn is unsustainable on personal funds. Would require extreme cuts to NIS 40-60K/mo. Not recommended.

---

## DECISION #4: LAUNCH GEOGRAPHY

### Context
Original plan: 4 Tel Aviv neighborhoods with 100 nannies across 30 km2 (3.3/km2 -- barely viable). Research shows a tighter focus achieves marketplace liquidity faster.

### 5 Options Ranked

| Rank | Strategy | Score | Overall Grade |
|:----:|----------|:-----:|:------------:|
| **A** | **Old North TLV single beachhead (50 nannies, 5 km2)** | **9.40/10** | **A+** |
| B | 4 TLV neighborhoods simultaneous (original plan) | 7.40/10 | B+ |
| C | Ra'anana Anglo beachhead (English-first) | 6.60/10 | B |
| D | Jerusalem Anglo neighborhoods (Baka/Katamon) | 6.50/10 | B- |
| E | Modiin young families (zero competition) | 5.70/10 | C+ |

### Detailed Grading

| Criterion (Weight) | A: Old North | B: 4 TLV | C: Ra'anana | D: Jerusalem | E: Modiin |
|---------------------|:---:|:---:|:---:|:---:|:---:|
| Nanny supply (25%) | A (TAU 3km) | A- (thin spread) | C+ (no university) | B (Hebrew U) | D (no pipeline) |
| Family demand (25%) | A+ (10/km2) | B+ (3.3/km2) | B+ (Anglo families) | B+ (Anglo families) | B+ (young families) |
| Competitive vacuum (20%) | A (no platform) | B+ (some agencies) | A (zero) | A- (Janglo only) | A+ (zero) |
| Expansion potential (15%) | A (adjacent TLV) | A (Gush Dan) | C+ (Anglo ceiling) | B (fragmented) | C (isolated) |
| Operational ease (15%) | A+ (1 zone) | B- (4 zones) | B+ (small city) | C+ (scattered) | C (remote) |

### OUR RECOMMENDATION: Option A -- Old North TLV Single Beachhead

**Why concentrated force beats broad coverage:**

| Metric | Original (4 neighborhoods) | Recommended (Old North only) |
|--------|:-:|:-:|
| Nannies at launch | 100 across 30 km2 | 50 in 5 km2 |
| Density | 3.3/km2 (minimum viable) | **10/km2 (thriving)** |
| Nearby nannies per family | 8-12 | **20-30** |
| Time to first booking | Hours to days | **Minutes to hours** |
| Word-of-mouth concentration | Diluted | **Concentrated** |
| Operational complexity | 4 zones | **1 zone to perfect** |

**Expansion sequence (data-driven triggers):**
1. Month 0-3: Old North TLV (50 nannies) -- DOMINATE
2. Month 2-4: + Ramat Aviv + Lev Ha'Ir (100 nannies total)
3. Month 4-6: + Herzliya Pituach (130 total, English UI launches)
4. Month 6-9: + Ra'anana/Kfar Saba (170 total, Anglo activation)
5. Month 9-12: + Jerusalem Anglo neighborhoods (230 total)
6. Month 12-18: + Modiin + Netanya (310 total, Russian UI)
7. Month 18-24: + Haifa + Beer Sheva (430 total)
8. Year 2+: National (630+ total, Arabic UI)

**Expansion trigger:** Move to next zone ONLY when current zone hits 4 of 6 PMF metrics for 4 consecutive weeks (>65% booking fill rate, >50% repeat, >50 NPS, >50% organic acquisition, >5 nannies/km2, >65% monthly active nannies).

**What changes in other docs if other options are chosen:**
- Option B (4 TLV): Growth Strategy needs 100 nannies before launch (vs 50). Longer pre-launch. Higher burn.
- Option C (Ra'anana): Language strategy flips to English-first. Name should be English-friendly (Kena or Sitra over Emuni). Smaller ceiling. Nanny supply crisis.
- Option D (Jerusalem): Fragmented geography. Lower rates (NIS 40-50/hr vs 58-64). Shabbat operational constraints. Need English UI from Day 1.
- Option E (Modiin): No nanny supply pipeline. Car-dependent. Geographic isolation. Cold start nightmare.

---

## DECISION #5: LANGUAGE STRATEGY

### Context
Israel: 9.5M people. Hebrew 90%+ of Jewish Israelis. 300K-400K Anglos. 1.3M Russian speakers. 2M Arabic speakers. The platform must eventually serve all -- but not simultaneously.

### 5 Options Ranked

| Rank | Strategy | Overall Grade |
|:----:|----------|:------------:|
| **A** | **Hebrew-only MVP, English Month 4-6 (build i18n from Day 1)** | **A** |
| B | Hebrew + English simultaneous from Day 1 | B+ |
| C | English-first (Anglo beachhead) | B- |
| D | Hebrew + English + Russian from Day 1 | C |
| E | English-only (global approach) | D |

### Detailed Grading

| Criterion | A: Hebrew-first | B: Bilingual Day 1 | C: English-first | D: Trilingual | E: English-only |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Speed to market | A (fastest) | B (doubles UI testing) | B+ | C (3x UI work) | B+ |
| Market coverage | A (90% of target) | A+ (95%) | C (5-8% of Israel) | A+ | D (5%) |
| Brand positioning | A (Israeli product) | A- | C ("Anglo app" trap) | A- | F (foreign import) |
| Dev complexity | A (single locale) | B- (2 locales) | B+ | C- (3 locales) | A |
| Expansion readiness | A (i18n ready) | A- (already bilingual) | B- (must add Hebrew) | A | D |

### OUR RECOMMENDATION: Option A -- Hebrew-first, English at Month 4-6

**Key principle:** Build the i18n code infrastructure from Day 1 (react-intl or i18n-js). Ship Hebrew-only. This is a code architecture decision (cheap, 1-2 days), not a content/translation decision (expensive, weeks).

**Language sequencing:**

| Language | Timeline | Trigger | Market Unlocked | Effort |
|----------|----------|---------|-----------------|--------|
| Hebrew | Day 1 | MVP launch | Tel Aviv, all Jewish Israeli families | Full build |
| English | Month 4-6 | Ra'anana expansion prep | 300K-400K Anglos nationwide | UI toggle + content |
| Russian | Month 12+ | Haifa/Netanya expansion | 1.3M Russian speakers | UI + content + community |
| Arabic | Year 2+ | National expansion | 2M Arabic speakers | Full cultural adaptation |

**Anglo strategy (parallel, not primary):**
- Month 0-3: English blog content, Janglo listings, NBN partnership conversations. Anglos in TLV can use Hebrew app (most are bilingual enough).
- Month 4-6: English UI toggle launches. Anglo community fully activated for Ra'anana expansion.

**What changes if other options are chosen:**
- Option B (Bilingual Day 1): Add 2-3 weeks to MVP build. Better Anglo adoption from Day 1. Reasonable tradeoff if co-founder is Anglo.
- Option C (English-first): Name should change to Kena or Sitra. Geography should change to Ra'anana. Entire brand positioning shifts. Not recommended.
- Option D (Trilingual): Only viable with a large team. 3x QA effort. Premature for MVP.

---

## DECISION #6: MONETIZATION TIMING AND MODEL

### Context
Existing plan: launch free, add fees at Month 4-6. Research shows this is risky. The "free anchor" trap causes up to 80% user churn when switching from free to paid. Israeli consumers are 2.5x more price-sensitive than global average.

### 5 Options Ranked

| Rank | Strategy | Score | Overall Grade |
|:----:|----------|:-----:|:------------:|
| **A** | **Freemium from Day 1 (Free tier + NIS 49/mo Premium + NIS 19/contact)** | **20/25** | **A** |
| B | Free C2C forever, monetize only B2B corporate | 16/25 | B |
| C | Free MVP, per-booking fee at Month 4 (NIS 19-25) | 15/25 | B- |
| D | Free MVP, subscription at Month 4 (NIS 69/mo) | 15/25 | B- |
| E | Pay What You Want for 6 months | 14/25 | C |

### Detailed Grading

| Criterion | A: Freemium D1 | B: B2B Only | C: Fee M4 | D: Sub M4 | E: PWYW |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Revenue validation speed | A+ | D | D | D | B- |
| Cold start impact | A- (free tier useful) | A+ (free forever) | A+ (free first) | A+ (free first) | A- |
| User retention | A (no transition) | A+ | C (80% churn risk) | C (price shock) | B- |
| LTV potential | A | B | B | A- | C |
| Operational simplicity | B (payment from D1) | C (B2B sales) | A- | B | C |

### OUR RECOMMENDATION: Option A -- Freemium from Day 1

**The model:**

```
FREE TIER (from Day 1):
  - Browse all nanny profiles (full info, verification badges)
  - See star ratings (not detailed text reviews)
  - Send 1 booking request per month
  - Advance Booking only

PREMIUM (NIS 49/month or NIS 399/year):
  - Unlimited booking requests
  - Detailed reviews and text feedback visible
  - Priority notification to nannies
  - "My Nannies" favorites list with one-tap rebooking
  - Founding Member badge (first 200 families)

PER-CONTACT (non-subscribers):
  - NIS 19 per additional contact exchange
  - No commitment, pay as you go

FOUNDING MEMBER (first 200 families):
  - NIS 29/mo locked forever
  - Status badge + input on feature roadmap
```

**Why NIS 49, not NIS 69:**
Israeli subscription norm: NIS 22-50/month (Spotify NIS 22.90, Netflix NIS 49.90). NIS 49 is at the top of "impulse buy" range. NIS 69 crosses into "let me think about it." You can always raise to NIS 69 once value is demonstrated.

**Why Israelis need a per-contact option:** Israelis are 50-60% less likely to prefer membership over per-use payment (GWI research). Always offer per-booking alongside subscription.

**Payment infrastructure for MVP:** Manual Bit/PayBox invoicing for first 50 paying users (zero dev cost). Integrate PayPlus/Tranzila at Month 3. No Stripe (not available in Israel).

**What changes in other docs if other options are chosen:**
- Option B (B2B Only): Revenue projections zero for months 1-6. Need 6+ months of pure burn. Seed round must be larger. High risk.
- Option C/D (Free then charge): MVP Scope removes payment infrastructure. Add "monetization switch" as v2 feature. Risk: 80% churn at transition.
- Option E (PWYW): Unreliable data. Israeli consumers find it confusing. Average PWYW payment is $0.92 globally.

---

## DECISION #7: IN-APP PAYMENTS FOR MVP

### Context
Families currently pay babysitters: 43% payment apps (Bit/PayBox), 22% cash, 20% bank transfer. The question is whether the platform should process nanny wages through in-app payments, or only collect platform fees.

### 5 Options Ranked

| Rank | Strategy | Overall Grade |
|:----:|----------|:------------:|
| **A** | **No in-app wage payments. Platform fees via manual Bit, then PayPlus at Month 3.** | **A** |
| B | No in-app payments at all (fully free MVP, no platform fees) | B- |
| C | Full in-app payments from Day 1 (PayMe marketplace split) | C+ |
| D | In-app for platform fees only, not nanny wages (PayPlus) | B+ |
| E | Nanny wage escrow with platform fee deducted | C |

### Detailed Grading

| Criterion | A: Manual Bit | B: No payments | C: Full PayMe | D: Fees only | E: Escrow |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Dev speed | A+ (0 dev) | A+ (0 dev) | C (3-4 weeks) | B (2 weeks) | D (complex) |
| Revenue validation | A (manual OK) | F (no revenue) | A | A | A |
| Legal simplicity | A (no PCI) | A+ | B (PCI, license) | B+ | C (payment license?) |
| User experience | B (manual step) | A | A+ (seamless) | B+ | B |
| Scalability | C (manual limit) | -- | A+ | A | A |

### OUR RECOMMENDATION: Option A -- Manual Bit for platform fees, no in-app wage payments

**How it works:**
1. Families browse, match, book on the platform (free or premium)
2. Family pays nanny directly (Bit, cash, bank transfer -- however they want)
3. Platform subscription/per-contact fees collected via Bit link or PayBox invoice
4. Admin manually activates premium status after payment confirmation
5. At Month 3 (~50 paying users): integrate PayPlus for automated subscription billing

**Why this is correct for MVP:**
- Saves 3-4 weeks of development (no payment integration)
- No PCI compliance burden
- No payment license concerns (exempt under NIS 5M/month threshold, but why add complexity?)
- Families already pay babysitters via Bit (43%) -- no behavior change needed
- Manual invoicing works fine for <50 paying users
- The platform's value is MATCHING and TRUST, not payment processing

**What changes if other options are chosen:**
- Option C (Full PayMe): Add 3-4 weeks to MVP timeline. Add PCI compliance. Adds NIS 2,500+/mo infrastructure cost. Better long-term but premature for MVP with 100 users.
- Option D (PayPlus for fees): Good middle ground. Add 2 weeks to MVP. Consider this if co-founder joins quickly and timeline has slack.

---

## DECISION #8: WHO PAYS FOR BACKGROUND CHECKS

### Context
Background checks cost NIS 47/nanny (police clearance certificate) + NIS 5-11 for AU10TIX ID verification. No Israel Police API exists -- process is manual. Checks take 2-4 weeks.

### 5 Options Ranked

| Rank | Strategy | Overall Grade |
|:----:|----------|:------------:|
| **A** | **Platform pays for all checks (absorb as CAC)** | **A-** |
| B | Platform pays, recoup from first booking fee | B+ |
| C | Nanny pays (NIS 47), platform reimburses after 3 completed bookings | B |
| D | Nanny pays (NIS 47), no reimbursement | C+ |
| E | Split cost (nanny pays police cert, platform pays AU10TIX) | B- |

### Detailed Grading

| Criterion | A: Platform pays | B: Recoup | C: Reimburse | D: Nanny pays | E: Split |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Supply-side friction | A+ (zero) | A- (free upfront) | B (NIS 47 barrier) | C (NIS 47 barrier) | B- |
| Cost to platform | B- (NIS 5,800 for 100) | A (recovered) | A- (delayed cost) | A+ (free) | B+ |
| Trust signal | A+ (we invest in safety) | A | B+ | B (safety = afterthought) | B |
| Nanny quality | A (no self-selection) | A | B+ (committed nannies) | B+ (committed) | B |
| Marketing value | A+ ("free verification") | A | B | C | B- |

### OUR RECOMMENDATION: Option A -- Platform pays for all checks

**The math:** 100 nannies x NIS 58 (NIS 47 police cert + NIS 11 AU10TIX) = **NIS 5,800 total.** This is your cheapest, highest-ROI investment. Compare to:
- One Instagram ad campaign: NIS 5,000-15,000
- One influencer partnership: NIS 3,000-10,000
- One booth at a parenting expo: NIS 2,000-5,000

**Marketing angle:** "Every nanny on Emuni is background-checked for free. We pay for verification because your child's safety isn't a premium feature." This is the single strongest differentiator vs every competitor (Care.com made background checks a paid add-on and got an $8.5M FTC settlement).

**Budget:** NIS 5,800 for first 100 nannies. At scale (1,000 nannies): NIS 58,000 -- still less than one month's salary for a junior developer.

**What changes if other options are chosen:**
- Option D (Nanny pays): Fewer nannies sign up (supply friction). Weaker trust positioning. Saves NIS 5,800 but loses the #1 marketing differentiator.

---

## DECISION #9: NANNY PRO TIER

### Context
The research identified a potential "Nanny Pro" subscription (NIS 29/mo) offering featured profiles, priority placement, and analytics. However, the Employment Service Law (1959) prohibits charging job seekers placement fees. Penalty: substantial financial penalties per violation.

### 5 Options Ranked

| Rank | Strategy | Overall Grade |
|:----:|----------|:------------:|
| **A** | **Defer entirely until attorney sign-off** | **B+** |
| B | Launch as "technology service" (not placement fee) with attorney pre-approval | B+ |
| C | Launch at low price (NIS 19/mo) to test demand, get attorney sign-off in parallel | C+ |
| D | Launch immediately, standard NIS 29/mo | C- |
| E | Never charge nannies anything | B |

### Detailed Grading

| Criterion | A: Defer | B: Attorney first | C: Test quietly | D: Launch now | E: Never charge |
|-----------|:---:|:---:|:---:|:---:|:---:|
| Legal risk | A+ (zero) | A- (pre-approved) | C (gray zone) | D (unvetted) | A+ (zero) |
| Revenue potential | C (delayed) | A- | B | B+ | F (zero) |
| Nanny goodwill | A (free platform) | B | B- | C (fee resistance) | A+ |
| Speed | A (no work) | B- (attorney time) | B | A | A |
| Competitive positioning | A ("100% free for nannies") | B | B- | B- | A |

### OUR RECOMMENDATION: Option A -- Defer

**Why:** The legal risk is real and the reward is tiny at MVP scale. NIS 29/mo x 100 nannies = NIS 2,900/month -- negligible revenue. Meanwhile, one violation of the Employment Service Law creates massive legal and reputational risk. The "100% free for nannies" positioning is a stronger competitive differentiator anyway.

**When to revisit:** After (1) attorney explicitly confirms the legal structure, (2) 500+ active nannies on the platform, and (3) data shows nannies would pay for premium features. Estimated: Month 9-12 at earliest.

**What changes if other options are chosen:**
- Option B (Attorney first): Need NIS 5-10K attorney consultation. Adds 4-6 weeks. If approved, small revenue upside.
- Option E (Never charge): Simplest. Loses a potential revenue stream but maintains strongest competitive positioning.

---

## DECISION #10: EMERGENCY BOOKING AND B2B IN MVP

### Context
Emergency booking (0-6 hour) requires high supply density -- minimum 50 available nannies within 5km at any given moment. B2B corporate contracts require traction data, case studies, and an HR dashboard.

### 5 Options Ranked

| Rank | Strategy | Overall Grade |
|:----:|----------|:------------:|
| **A** | **No emergency booking, no B2B in v1. Start B2B conversations at Month 3.** | **A** |
| B | No emergency, B2B pilot conversations from Day 1 (no product features) | A- |
| C | Emergency booking as premium-only feature | C+ |
| D | B2B module in MVP (HR dashboard, employee access) | C |
| E | Both emergency and B2B in MVP | D |

### Detailed Grading

| Criterion | A: Neither | B: B2B convos | C: Emergency | D: B2B module | E: Both |
|-----------|:---:|:---:|:---:|:---:|:---:|
| MVP build speed | A+ | A+ | C (2 weeks add) | C- (3-4 weeks) | D (5-6 weeks) |
| Focus | A+ (one thing) | A (minimal distraction) | B (divided focus) | B- (two products) | C (scattered) |
| Revenue impact (M1-6) | B (consumer only) | B+ (pipeline building) | B- (no supply density) | C (6-month B2B cycle) | C- |
| User experience | A (simple) | A | B- (empty results likely) | B | C |
| Future readiness | A (clean foundation) | A+ (warm leads) | B+ (feature built) | B+ (module built) | B |

### OUR RECOMMENDATION: Option A (leaning toward B)

**Emergency booking:** Mathematically impossible with 50 nannies. If 50 nannies are registered, maybe 20 are available on a given day, maybe 5 within 5km of a requesting family. That's not enough for reliable same-day matching. Emergency booking with empty results destroys trust. Add in v2-v3 (Month 6+) when supply density reaches 50+ available nannies in the launch zone.

**B2B:** Start informal conversations at Month 3 (after launch, with real data to show). Target first pilots at Month 6. Sign first contracts at Month 6-9. The B2B sales cycle is 3-6 months -- starting conversations early loses nothing and builds pipeline.

**Immediate B2B target list:** Monday.com, Wix, Check Point, CyberArk, Fiverr, ironSource/Unity. Approach via: HR/People team contacts, Israeli tech HR Facebook groups, corporate wellness events.

**What changes if other options are chosen:**
- Option C (Emergency): Add 2 weeks to MVP build. Feature will show "no nannies available" 90% of the time at launch density. Negative user experience.
- Option D (B2B module): Add 3-4 weeks to MVP. No corporate client will sign until they see consumer traction. Wasted development.

---

## APPENDIX: CHANGES REQUIRED IN EXISTING DOCUMENTS

If the founder adopts all 10 recommendations above, the following documents need updates:

| Document | Changes Needed |
|----------|----------------|
| `NANNY_PLATFORM_PRD_READINESS.md` | Update Open Questions section to mark all 10 as DECIDED. Update pricing from NIS 69 to NIS 49. |
| `NANNY_PLATFORM_MASTER_RESEARCH.md` | Update pricing tiers (NIS 49 not NIS 69). Update launch geography (Old North only, not 4 neighborhoods). |
| `NANNY_PLATFORM_GROWTH_STRATEGY.md` | Revise from 4-neighborhood to single-beachhead model. Update nanny target from 100 to 50 at launch. |
| `NANNY_PLATFORM_MVP_SCOPE.md` | Change from "free MVP" to "freemium MVP." Add manual Bit payment flow. Remove "monetize at Month 4" language. |
| `NANNY_PLATFORM_COST_MODEL.md` | Add NIS 5,800 for background checks to pre-launch costs. Add co-founder at NIS 20K/mo salary. Revise team composition. |
| `NANNY_PLATFORM_REVENUE_MODEL_REVISED.md` | Add Day 1 freemium projections. Adjust subscription price to NIS 49. Add Founding Member tier (NIS 29/mo). |
| `NANNY_PLATFORM_MATCHING_FLOW.md` | Remove Emergency and Short Notice tiers from v1 spec. Advance Booking only. |

---

## ADDITIONAL DECISIONS (Post-Audit Round)

### DECISION #11: MINIMUM NANNY AGE — 18+

**Decision:** Platform requires all nannies/babysitters to be 18 or older.

**Why:** While Israeli Youth Labor Law permits work from age 15 (babysitting explicitly covered by Amendment 9b), allowing 16-17 year olds would require: parental consent for registration, Youth Labor Law hour/night restrictions enforced in UX, medical exam before employment, and minor data processing under the Capacity Law. The professional standard (Rockmybaby: 18+) and liability simplification make 18+ the clear choice.

### DECISION #12: CANCELLATION POLICY (V1) — RELIABILITY SCORE ONLY

**Decision:** No financial penalties in v1 (no payment mechanism anyway). Cancellations affect reliability score only.

- Late cancel (<24hrs): reliability score impact
- No-show: significant score impact + account review
- After 3 late cancellations in 30 days: supportive outreach, lower search ranking
- Financial penalties added in v2 when PayMe is integrated, per MATCHING_FLOW spec

### DECISION #14: INSURANCE — ToS + LANGUAGE AT LAUNCH, E&O AT SEED ROUND

**Decision:** No insurance at launch. Protect via precise language and ToS. Add E&O + cyber at seed round (Month 6+, ~NIS 15-30K/yr).

- Launch (Month 0-6): ToS + precise language + family acknowledgment. Cost: NIS 0.
- Seed round (Month 6+): Add E&O + cyber liability insurance. Cost: ~NIS 15-30K/year.
- Scale (Month 12+): Explore group nanny liability policy. Cost: TBD.

### DECISION #15: FREE TIER LIMITS — GENEROUS FREE, PREMIUM = CONVENIENCE

**Decision:** Free tier shows everything, limits bookings. Premium unlocks volume + convenience.

**Free tier:**
- Browse all nanny profiles fully (photos, ratings, reviews)
- Basic filters (location, hourly rate)
- 1 booking per month
- In-app messaging

**Premium (NIS 49/mo):**
- Unlimited bookings
- Advanced filters (language, experience level, schedule match, age group specialization)
- Priority placement in nanny's inbox
- Favorites list + 1-tap re-booking
- Founding Member badge (first 200 families)
- Priority support

**Founding Member (NIS 29/mo, locked forever, first 200 families):**
- All Premium features
- Founding Member badge
- Early access to new features

### DECISION #13: PLATFORM LIABILITY LANGUAGE — PRECISE, NOT INSURANCE

**Decision:** Protect through precise language and ToS, not insurance at launch. Add E&O at seed round.

**Key insight:** By conducting background checks, the platform creates a duty of care (Civil Wrongs Ordinance, Section 35). The Care.com wrongful death lawsuits were based on "negligent vetting" — not employer liability. Protection is language precision:
- Say "identity verified" not "verified nanny"
- Say "police clearance certificate obtained" not "background-checked and safe"
- Say "tools to help families make informed choices" not "we ensure your child's safety"
- Require families to acknowledge responsibility for their own due diligence
- Get E&O + cyber insurance at seed round (Month 6+, ~NIS 15-30K/year)

---

## SOURCES

This document synthesizes findings from 5 dedicated research agents and 16 prior research documents:

**New Research (Round 6):**
1. `NANNY_PLATFORM_NAMING_RESEARCH.md` -- 25+ Israeli/global companies analyzed, 5 naming directions, 20 candidate names
2. `NANNY_PLATFORM_COFOUNDER_RESEARCH.md` -- Solo vs co-founder data, Israeli VC expectations, equity benchmarks, 5 co-founder finding channels
3. `NANNY_PLATFORM_FUNDING_RESEARCH.md` -- IIA grants (Tnufa/Pre-Seed/Seed), 8 Israeli VCs profiled, angel networks, accelerators, 5 funding strategies
4. `NANNY_PLATFORM_LAUNCH_GEOGRAPHY.md` -- 5 cities analyzed, 4 TLV neighborhoods scored, Anglo community data, concentric expansion model
5. `NANNY_PLATFORM_MONETIZATION_STRATEGY.md` -- 10 marketplace monetization timelines, Israeli WTP benchmarks, freemium conversion data, pricing experiments

**Prior Research (Rounds 1-5):**
6-16. See `NANNY_PLATFORM_PRD_READINESS.md` for complete index of all 16 research documents.

---

*This document provides strategic recommendations synthesized from 21 research documents, 23+ research agents, and 300+ sources. It does not constitute legal, financial, or tax advice. Consult qualified Israeli professionals before making final decisions.*
