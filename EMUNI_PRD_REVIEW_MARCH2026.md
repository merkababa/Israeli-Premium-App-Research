# Emuni PRD Review — March 2026

**Method:** 6 parallel review agents (Legal, Tech, Financial, Market Data, Product/UX, Growth Strategy)
**PRD Version:** 1.0 (March 7, 2026) — 1,622 lines
**Total findings:** 11 CRITICAL, 24 HIGH, 18 MEDIUM, 6 LOW

---

## EXECUTIVE SUMMARY

The PRD is strong overall — legal framework is solid, tech choices are sound, and market positioning is well-researched. However, 6 agents collectively found **11 critical issues** that should be fixed before development begins:

### Top 5 Must-Fix Items

1. **Jerusalem daycare tragedy date is WRONG** — says January 2025, should be January 2026
2. **Google Maps Distance Matrix API is LEGACY** — replaced by Routes API; $200/mo credit no longer exists
3. **50 nannies + 20 families in Month 1 while solo-building MVP is unrealistic** — most critical feasibility risk
4. **No emergency nanny replacement flow** — #1 NPS-killing scenario has no solution beyond "search again"
5. **Apple IAP 15% commission not addressed** — directly impacts subscription revenue

---

## PART 1: FACTUAL ERRORS (Must Fix)

### INCORRECT Claims

| # | Location | Claim | Truth | Source |
|---|----------|-------|-------|--------|
| 1 | Line 39 | "January 2025 Jerusalem daycare tragedy" | **January 2026** (Jan 19, 2026). Also: cause was overcrowding/dehydration, not "caregiver harmed children" | [Times of Israel](https://www.timesofisrael.com/2-babies-die-in-incident-at-unlicensed-jerusalem-daycare-3-caregivers-detained/) |
| 2 | Line 271 | Care.com "$8.5M FTC settlement (2024) for deceptive practices around safety claims" | Settlement was about **deceptive earnings claims, inflated job listings, and dark-pattern cancellation** — NOT safety | [FTC Press Release](https://www.ftc.gov/news-events/news/press-releases/2024/08/ftc-takes-action-against-carecom) |
| 3 | Line 963 | Google Maps "$200/mo free credit" | **No longer exists** as of March 2025. Replaced by per-SKU free usage thresholds | [Google Maps Pricing FAQ](https://developers.google.com/maps/billing-and-pricing/faq) |
| 4 | Line 963+ | "Distance Matrix API" | **Legacy since March 2025.** New projects must use **Routes API** (`computeRouteMatrix`) | [Migration Guide](https://developers.google.com/maps/documentation/routes/migrate-routes) |
| 5 | Line 48 | Helpbook has "no mobile app" | **Has an Android app** (Ionic, Google Play: `com.ionicframework.helpbookapp973405`). No iOS. | [Google Play](https://play.google.com/store/apps/details?id=com.ionicframework.helpbookapp973405) |
| 6 | Line 962 | AU10TIX headquartered in "Hod Hasharon" | **HQ is Amsterdam, Netherlands.** Israel offices exist but HQ is wrong. | [Wikipedia](https://en.wikipedia.org/wiki/AU10TIX) |
| 7 | Line 966 | Mixpanel "Free tier for <1K MTU" | **Changed Feb 2025** — now 1M monthly events (event-based, not MTU) | [Mixpanel Pricing](https://mixpanel.com/pricing/) |
| 8 | Line 1268 | "Spotify NIS 22.90, Netflix NIS 49.90" | Spotify is **NIS 23.90**; Netflix Standard is **NIS 46.90** | [Spotify IL](https://www.spotify.com/il-en/premium/) |
| 9 | Line 1275 | "Average booking at NIS 50-60/hr" | TLV average is **NIS 62-64/hr** (Babysits 2026 data) | [Babysits TLV](https://en.babysits.co.il/babysitter/tel-aviv/) |

### Claims Needing Update (Not Wrong, But Stale/Incomplete)

| # | Location | Issue | Fix |
|---|----------|-------|-----|
| 10 | Line 960 | Supabase presented as straightforward | **Supabase managed has NO Israel region.** Available: Frankfurt is closest. Self-hosting on il-central-1 adds ops complexity. |
| 11 | Lines 1240-1247 | "All PII stored in Israel" | **Contradicts Supabase managed hosting.** Either self-host (complex) or accept Frankfurt and soften claim. |
| 12 | Line 968 | PayMe is "only Israeli processor with marketplace split payments" | Likely true but unverifiable. Soften to "leading" not "only." |
| 13 | Line 1382 | "Old North is 5 km2" | Geographic analysis suggests **2-3 km2** (Yarkon to Arlozorov, Ibn Gvirol to sea). Density actually better if smaller. |
| 14 | Line 41 | "200,000+ families hire private caregivers" | **Unsourced.** Derived figure is 270K addressable households. Reframe with methodology. |
| 15 | Line 63 | "Childcare is 2nd largest household expense" | **Unverified ranking.** Food competes. Change to "one of the largest." |

---

## PART 2: MISSING ITEMS (Must Add)

### CRITICAL Gaps

| # | Gap | Impact | Recommendation |
|---|-----|--------|---------------|
| 1 | **Apple IAP 15% commission** | NIS 49 subscription yields only ~NIS 41.65 after Apple's cut. Not mentioned anywhere in PRD. | Add to Section 6 revenue model. Adjust Y1 low-end from NIS 150K to NIS 120K. |
| 2 | **AU10TIX 2024 data breach** | Admin credentials leaked for 18+ months, exposing user identity documents. EFF named it worst breach of 2024. Trust is Emuni's core value — using a provider with a major ID leak is a material risk. | Add to Risk Register. Document mitigations. Evaluate Onfido/Veriff as alternatives. |
| 3 | **Emergency nanny replacement flow** | When a nanny cancels <24 hours before, "search for another nanny" is inadequate. This is the #1 NPS-killing scenario. | Design auto-suggest available nannies for the same time slot. Even v1 should have this. |
| 4 | **Nanny-in-danger emergency protocol** | Safety is P0 but the actual flow after pressing the emergency button is ONE LINE. No notification chain, no post-incident protocol. | Specify: who gets notified, in what order, what happens to the booking, post-incident review. |
| 5 | **Dispute resolution mechanism** | No flow for "family says nanny was late, nanny disputes this." No arbitration. | Design basic dispute flow for v1, even if manual (admin reviews). |
| 6 | **Empty search results state** | 50%+ of early users will see zero nannies. No screen specified. | Design: expand radius suggestion, "Bring Your Nanny" CTA, waitlist option. |
| 7 | **SEO/ASO strategy** | Zero mention of web presence or app store optimization. Parents search Google for "babysitter Tel Aviv." | Add landing page from Month -3, basic ASO at launch, content marketing by Month 3. |

### HIGH Gaps

| # | Gap | Recommendation |
|---|-----|---------------|
| 8 | No in-app payment even in v1 — every major competitor has this | Acknowledged as intentional deferral, but document the trust/data gap this creates |
| 9 | No social/community trust network at launch | Even minimal "2 families nearby booked this nanny" counter would help |
| 10 | No interview/video call feature pre-booking | Consider at least a phone-call-through-app option |
| 11 | No "drives" / has car filter | Critical for parents needing gan pickup. Add to nanny profile |
| 12 | No tipping mechanism | Culturally expected in Israel. Simple post-booking prompt |
| 13 | No grandparent/proxy booking flow | Many Israeli grandparents book sitters |
| 14 | No au pair vs babysitter vs full-time nanny distinction | Svetlana and Maya have fundamentally different needs |
| 15 | No Shabbat/chagim handling | Push notification preferences, Shabbat availability marking |
| 16 | No re-engagement flow for registered-but-never-booked families | Push/email drip after 24/48 hours |
| 17 | No booking total cost display | Show "Total: NIS 275 (5 hrs x NIS 55)" before confirming |
| 18 | 7 risks missing from Risk Register | Crisis comms plan, regulatory change, competitive entry (Yad2/iSavta), app store rejection, data breach ops, negative PR, key person risk upgrade to CRITICAL |

---

## PART 3: INTERNAL CONTRADICTIONS (Must Fix)

| # | Severity | Issue | Sections |
|---|----------|-------|----------|
| 1 | CRITICAL | **Verification status enum mismatch.** Section 3.2: `REGISTERED -> ID_SUBMITTED -> ID_VERIFIED -> LIVE`. Section 5.2 DB enum: `pending, id_submitted, id_verified, live, rejected, suspended`. `REGISTERED` != `pending`. | 3.2 vs 5.2 |
| 2 | CRITICAL | **Search distance hardcoded.** Filters offer 1/3/5/10/15km but SQL query hardcodes `WHERE ST_DWithin(..., 5000)` (5km only). 10km and 15km filters silently broken. | 3.3 vs SQL |
| 3 | HIGH | **`fully_verified` in SQL but not in enum.** Section 5.4: `AND np.verification_status = 'fully_verified'` but enum has no `fully_verified` — should be `live`? | 5.4 vs 5.2 |
| 4 | HIGH | **Founding Member tier exists in Section 3.7 but missing from Section 6.1** revenue model table (only Free/Premium shown). | 3.7 vs 6.1 |
| 5 | HIGH | **"Priority in nanny's inbox"** is a Premium feature but no inbox exists in the feature spec. Only push notifications. | 3.7 vs 4.x |
| 6 | HIGH | **"1-tap rebook"** sold as Premium feature but no rebook flow defined anywhere. | 3.7 vs 3.x |
| 7 | MEDIUM | **"Budget range" vs "Hourly rate"** — same slider named differently in onboarding vs search. | 3.1 vs 3.3 |
| 8 | MEDIUM | **"Responds within X hours" badge** — no specification of thresholds or what new nannies show. | 3.3 |

---

## PART 4: GROWTH STRATEGY ISSUES

| # | Severity | Finding | Recommendation |
|---|----------|---------|---------------|
| 1 | **CRITICAL** | **50 nannies + 20 families in Month 1 while solo-building MVP = 5 full-time jobs in 3 months.** Development + recruitment + verification + onboarding + legal setup + accessibility audit. | Reduce to 25 nannies / 10 families, OR start recruitment 3 months before development via landing page + waitlist. |
| 2 | HIGH | **Florentin is the wrong second market.** Ronkin List: "notably not family-oriented. Families with young children typically choose other neighborhoods." Population ~7K. | Swap to: Old North -> **Ramat Aviv** -> Ra'anana. Florentin can be opportunistic. |
| 3 | HIGH | **Anglo vs Hebrew-first contradiction.** Ideal early adopters (tech-savvy, app-familiar, willing-to-pay) are disproportionately Anglos who can't use Hebrew-only v1. | Either add basic English from Day 1 (i18n is built), or explicitly defer Anglos to Month 4+. |
| 4 | HIGH | **Kill criteria too aggressive.** < 5 bookings/week by Week 16 = kill. Babysitting is low-frequency (1-4x/month, not daily). Most frameworks recommend 6-9 months. Solo founder with NIS 2K/mo burn can afford more time. | Extend: diagnostic at Week 16, kill at Week 20-24. |
| 5 | HIGH | **"Bring Your Nanny" is a seeding mechanic, not a viral loop.** The invited nanny doesn't generate further invites — loop terminates. K-factor < 1. | Keep but rename internally. Real viral loop = family recommends to friend via WhatsApp. |
| 6 | MEDIUM | **PMF = 10 bookings/week by Week 12** is reasonable but tight for babysitting frequency. | Consider extending GREEN threshold to Week 16. |
| 7 | MEDIUM | **Solo breakeven "Month 2-4"** is optimistic. Month 2 math doesn't work. | Tighten to Month 3-5. |

---

## PART 5: FINANCIAL CORRECTIONS

| # | Item | PRD Says | Should Be | Impact |
|---|------|----------|-----------|--------|
| 1 | Apple IAP commission | Not mentioned | 15% on subscriptions (Small Business Program) | ~NIS 7.35/mo lost per subscriber |
| 2 | Babysitter rates | NIS 50-60/hr | NIS 62-64/hr (TLV avg) | Bookings worth more; update calculations |
| 3 | Solo breakeven | Month 2-4 | Month 3-5 | Month 2 math doesn't work at 20 subs |
| 4 | Y1 revenue low-end | NIS 150K | NIS 120K (with IAP impact) | More conservative, more honest |
| 5 | PayMe target rate | 1.2-1.6% | 1.5-2.5% (more realistic for startup volume) | Slightly higher payment costs |
| 6 | App store fees | NIS 400 | NIS 460 (Apple $99/yr + Google $25) | Minor |
| 7 | AU10TIX per-check | NIS 4-8 | NIS 8-15 (conservative for low volume) | Budget ~NIS 750 for 50 nannies vs NIS 400 |
| 8 | LTV/CAC ratio | 5-8x | Calculation mixes organic (NIS 10-30) and paid (NIS 80-150) CAC inconsistently | Separate the calculations |
| 9 | IIA Tnufa | "non-dilutive" | Correct, but has royalty repayment (3-5% of revenue). Cannot cover salaries. | Add caveats |
| 10 | Minimum wage (memory) | NIS 34.32/hr | **NIS 35.40/hr** (effective April 2026) | Update project memory |

---

## PART 6: LEGAL VERIFICATION RESULTS

### Confirmed Correct (No Changes Needed)

| Claim | Status |
|-------|--------|
| Wolt appeal pending at National Labor Court | CORRECT (note: mediation proposed mid-2024) |
| 2019 Criminal Information Law prohibits employer requests | CORRECT |
| Employment Service Law 1959 prohibits charging job seekers | CORRECT |
| Privacy Amendment 13 effective Aug 14, 2025 + penalties | CORRECT |
| IS 5568 mandatory, NIS 50K penalty | CORRECT |
| VAT 18% from Jan 1, 2025 | CORRECT |
| SHAAM NIS 5K threshold, June 2026 deadline | CORRECT |
| Daycare Supervision Law 2018 | CORRECT |
| Company registration as "technology software" | CORRECT |
| 9 Wolt control factors and avoidance strategy | CORRECT |

### Needs Minor Update

| Claim | Issue |
|-------|-------|
| Youth Labor Law "babysitting from 15" | Age is 15 OR 16 depending on compulsory education status. Decision to use 18+ is unaffected. |
| Employment bureau license NIS 5,000-15,000 | Plausible but unverifiable. Add "estimated." |

---

## PART 7: TECH STACK VERIFICATION RESULTS

### Confirmed Correct

| Component | Status |
|-----------|--------|
| React Native + Expo | CORRECT. Expo SDK 55 ships with RN 0.83, React 19.2. New Architecture now mandatory. |
| NestJS | CORRECT. v11.1.16 (March 2026), v12 planned Q3 2026. |
| AWS il-central-1 | CORRECT. 3 AZs, growing service catalog. |
| Bit P2P payments | CORRECT. 2M+ users, ~80% market share in Israel. |
| WhatsApp Business API approach | CORRECT. Phased approach (pre-filled links first) is sound. |
| SHAAM e-invoicing requirements | CORRECT. June 2026 deadline, NIS 5K threshold. |
| GitHub Actions free tier | CORRECT. 2,000 min/mo on Free plan. |

### Needs Update

| Component | Issue | Fix |
|-----------|-------|-----|
| Google Maps Distance Matrix API | Legacy since March 2025 | Switch to Routes API |
| Google Maps $200/mo credit | No longer exists | Update pricing model |
| Supabase Israel data residency | No Israel region available | Use Frankfurt or self-host |
| AU10TIX HQ location | Amsterdam, not Hod Hasharon | Fix |
| AU10TIX security | Major 2024 data breach (18mo credential exposure) | Add to risk register |
| Mixpanel free tier | Now event-based (1M events), not MTU-based | Update |
| PayMe "only" claim | Unverifiable exclusivity | Change to "leading" |

---

## PART 8: COMPETITIVE FEATURE GAPS VS TOP PLATFORMS

| Feature | Bubble (UK) | UrbanSitter | Care.com | Emuni v1 | Gap? |
|---------|:-----------:|:-----------:|:--------:|:--------:|:----:|
| In-app payment | Yes | Yes | Yes | No (v2) | YES |
| Insurance per sit | Yes (GBP 1M) | No | No | No (Month 12) | YES |
| Social trust graph | Yes | Yes | No | No (v2) | YES |
| Video profiles/interviews | No | Yes | Yes | No | YES |
| "Drives" / car filter | No | Yes | Yes | No | YES |
| Tipping | No | Yes | No | No | YES |
| Job posting (families post, sitters apply) | No | Yes | Yes | No | MEDIUM |
| Trial/meet-and-greet booking | No | Yes | Yes | No | MEDIUM |
| Group booking | No | No | No | No | LOW |
| Nanny earnings dashboard | No | Yes | Yes | No (v2) | LOW |
| Special needs category | No | No | Yes | Partial | LOW |

---

## FULL ISSUE TRACKER

### CRITICAL (11) — Fix Before Development

| ID | Category | Issue |
|----|----------|-------|
| C1 | Factual | Jerusalem daycare date: January 2025 -> January 2026 |
| C2 | Factual | Care.com FTC settlement reason incorrect |
| C3 | Tech | Google Maps API is legacy + $200 credit gone |
| C4 | Financial | Apple IAP 15% commission not addressed |
| C5 | Growth | 50 nannies + 20 families + MVP build in Month 1 = unrealistic for solo founder |
| C6 | Product | No emergency nanny replacement flow |
| C7 | Product | Nanny-in-danger emergency protocol is one line |
| C8 | Product | Verification enum mismatch (REGISTERED vs pending) |
| C9 | Product | Search distance filter broken (hardcoded 5km vs 15km option) |
| C10 | Product | No empty search results state |
| C11 | Product | No dispute resolution mechanism |

### HIGH (24) — Should Fix Before Development

| ID | Category | Issue |
|----|----------|-------|
| H1 | Tech | Supabase has no Israel region — contradicts "all PII in Israel" |
| H2 | Tech | AU10TIX 2024 data breach not in risk register |
| H3 | Tech | AU10TIX HQ is Amsterdam, not Hod Hasharon |
| H4 | Financial | Babysitter rates: NIS 50-60 -> NIS 62-64/hr |
| H5 | Financial | Solo breakeven: Month 2-4 -> Month 3-5 |
| H6 | Financial | PayMe target rate: 1.2-1.6% -> 1.5-2.5% |
| H7 | Financial | LTV/CAC calculation mixes organic and paid CAC |
| H8 | Growth | Florentin is wrong second market — swap for Ramat Aviv |
| H9 | Growth | Anglo vs Hebrew-first contradiction |
| H10 | Growth | Kill criteria too aggressive — extend to Week 20-24 |
| H11 | Growth | SEO/ASO strategy completely missing |
| H12 | Growth | 7 risks missing from Risk Register |
| H13 | Product | `fully_verified` in SQL but not in enum |
| H14 | Product | Founding Member tier missing from revenue table |
| H15 | Product | "Priority inbox" feature sold but no inbox exists |
| H16 | Product | "1-tap rebook" feature undefined |
| H17 | Product | No social proof / neighborhood trust signal at launch |
| H18 | Product | No video/phone interview before booking |
| H19 | Product | No "drives/has car" nanny filter |
| H20 | Product | No tipping mechanism |
| H21 | Product | No grandparent/proxy booking |
| H22 | Product | No au pair vs babysitter vs full-time nanny distinction |
| H23 | Product | No Shabbat/chagim notification handling |
| H24 | Market | Helpbook "no mobile app" claim is wrong (has Android) |

### MEDIUM (18)

| ID | Category | Issue |
|----|----------|-------|
| M1 | Financial | App store fees NIS 400 -> NIS 460 |
| M2 | Financial | AU10TIX budget NIS 4-8 -> NIS 8-15 per check |
| M3 | Financial | IIA Tnufa has royalty repayment — add caveat |
| M4 | Financial | Spotify/Netflix prices slightly off |
| M5 | Tech | Mixpanel free tier is now event-based |
| M6 | Market | "200,000+ families" unsourced |
| M7 | Market | "2nd largest expense" ranking unverified |
| M8 | Market | Old North "5 km2" may be 2-3 km2 |
| M9 | Market | 270K addressable — add CBS source |
| M10 | Product | "Budget range" vs "Hourly rate" naming inconsistency |
| M11 | Product | "Responds within X hours" thresholds undefined |
| M12 | Product | No overnight booking handling |
| M13 | Product | No booking total cost display |
| M14 | Product | No family home description for nanny safety |
| M15 | Product | No "last active" indicator on profiles |
| M16 | Product | No notification management settings |
| M17 | Product | No progressive engagement (2nd-5th booking) |
| M18 | Product | No dual-role (parent who is also a babysitter) |

### LOW (6)

| ID | Category | Issue |
|----|----------|-------|
| L1 | Product | No nanny earnings dashboard (v2) |
| L2 | Product | No parent community/content (v2) |
| L3 | Product | No group booking feature |
| L4 | Product | No nanny "bring own child" field |
| L5 | Product | Data retention for deleted accounts unclear |
| L6 | Growth | "Bring Your Nanny" is seeding, not viral loop |

---

## WHAT'S CORRECT AND STRONG

The PRD gets a lot right. Worth noting:

- **Legal framework is excellent.** All 9 Wolt control factors correctly identified and avoided. Employment classification strategy is sound. "Never say safe/verified" language rules are well-designed.
- **Pure marketplace architecture is legally defensible.** No reviewer found structural legal risk.
- **Revenue model (freemium + per-contact) is well-positioned.** NIS 49/mo against NIS 62-64/hr babysitter rates is strong value proposition.
- **Tech stack choices are current and sound.** RN+Expo, NestJS, PostgreSQL+PostGIS, AWS il-central-1 all verified correct.
- **KPI framework is comprehensive.** Multi-metric PMF measurement (bookings + retention + NPS + repeat rate) is better than most early-stage PRDs.
- **Risk register exists and is structured.** 16 identified risks with mitigations — just needs 7 more.
- **Old North TLV beachhead is validated.** Family-dense, affluent, tight-knit — correct launch geography.
- **Supply-first strategy is correct** for childcare (families who see 0 nannies uninstall immediately).

---

## RECOMMENDED ACTION PLAN

### Before Development (Week 0)
1. Fix all 11 CRITICAL items
2. Resolve Supabase data residency contradiction
3. Add Apple IAP impact to revenue model
4. Add AU10TIX breach to risk register
5. Design empty state, emergency replacement, and dispute flows

### During Development (Week 1-12)
1. Fix 24 HIGH items as relevant sections are built
2. Start nanny recruitment via landing page + waitlist (parallel to dev)
3. Launch emuni.co.il landing page for SEO

### Before Launch
1. Fix remaining MEDIUM items
2. Verify Old North area size with municipal data
3. Confirm AU10TIX or switch to alternative provider

---

*Review compiled from 6 parallel agents. Total: ~380 web searches, ~270 tool calls, ~340K tokens consumed.*
