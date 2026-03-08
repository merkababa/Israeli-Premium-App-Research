# EMUNI PRD + Roadmap — Round 2 Review Decisions

**Date:** March 7, 2026
**Context:** Fresh-eyes review by 4 parallel agents (consistency, legal, financial, product/UX), followed by iterative founder decisions.

---

## CRITICAL CONTEXT: FOUNDER PROFILE

- Solo bootstrapper, coding everything with AI assistance
- Near-zero monthly budget (under NIS 1K/mo)
- No co-founder, not looking
- No team, no salaries

---

## DECISIONS TO APPLY

### 1. DROP TRACK A (Mandatory Sex Offense Clearance)

**What:** Remove the mandatory sex offense clearance certificate (Track A) entirely from the PRD.
**Why:** Requires "covered institution" legal status, attorney fees, and creates DPO obligation. Too complex and expensive for a solo bootstrapper.
**Impact on PRD:**
- Section 2.3: Remove Track A subsection. Keep Track B as voluntary only.
- Section 2.3 "Two-Track Background Check System" → rename to "Background Verification System"
- Remove all references to "co-signed by the platform," "covered institution," sex offense clearance forms
- Update verification status machine: remove BG_CHECK_PENDING state for Track A
- Section 3.2 (Nanny Registration): Simplify Step 7 — remove Track A consent, keep Track B as optional
- Background check budget table: remove sex offense clearance processing line
- Insurance strategy: unchanged
- Open Questions #2 (covered institution): REMOVE — no longer needed
- Risk Register R3 (background check process): rewrite — risk is now about Track B adoption rate, not legal structuring
- Risk Register R5 (child safety): update — platform does ID verification + voluntary badge, not mandatory checks

### 2. KEEP TRACK B AS VOLUNTARY BADGE ONLY

**What:** Nannies CAN voluntarily upload criminal record certificate from gov.il for a badge. 100% optional, nanny-initiated.
**Badge name change:** "מאומת רקע" (Background Verified) → "הגיש/ה אישור רקע" (Submitted Background Certificate)
**Impact on PRD:**
- Section 2.3: Update Track B description — emphasize voluntary, nanny-initiated
- Section 2.3 "Never Say" table: update badge name
- All references to "Background Verified" badge → "הגיש/ה אישור רקע"
- Feature N4: Rename to "Optional background verification badge" — simplified flow
- Admin A2: Simplify — only Track B status to manage, and only for nannies who opt in

### 3. DEFER DPO

**What:** No DPO at launch. Without Track A, platform is not processing "significant volume of especially sensitive data."
**Rationale:** Amendment 13 triggers DPO for entities whose "main activity" is processing sensitive data at "significant scale." With Track A dropped and Track B voluntary, the platform primarily does ID verification (not classified as especially sensitive). At 50 users, not "significant scale."
**Impact on PRD:**
- Section 2.4: Rewrite DPO requirement — state it's deferred, with rationale. Note: revisit at ~500-1,000 users or if Track A is ever added.
- Remove "Appoint before launch" language everywhere
- Pre-launch checklist: remove DPO line item
- Privacy compliance budget: reduce significantly (no DPO cost)
- Risk Register R4: rewrite — risk is now "operating without DPO while processing some voluntary criminal data"
- Section 7.1: remove "Appoint outsourced DPO (Amendment 13)" from pre-launch steps

### 4. SKIP ATTORNEY

**What:** No attorney engagement before launch. DIY ToS and privacy policy from templates.
**Rationale:** Without Track A, no "covered institution" confirmation needed. DIY approach for ToS/privacy using templates. Revisit when revenue exists.
**Impact on PRD:**
- Section 7.1 Company Formation: remove "Engage employment law attorney" from pre-launch
- Budget: remove attorney line item (NIS 5-10K saved)
- Open Questions: remove attorney-related items
- Risk Register: add new risk "DIY legal documents may have gaps"
- PRD Appendix canonical data: update one-time costs

### 5. REBUILD Y1 REVENUE FROM ROADMAP KPIs

**What:** Recalculate Y1 revenue bottom-up from actual user growth targets in the Roadmap.
**Financial agent's math:**
- Subscribers: avg ~200 over 12 months × NIS 44 blended (mix of NIS 49 + NIS 29 founding) × 12 = ~NIS 105K
- Per-booking fees (start Month 3): avg ~200 bookings/mo × NIS 25 avg fee × 9 months = ~NIS 45K
- B2B: 1-2 contracts from Month 8, ~NIS 3.5K/mo × 4 months = ~NIS 14-28K
- Emergency surcharge: REMOVE from Y1 (feature doesn't launch until Month 6-9, minimal volume)
- VAS: REMOVE from Y1 (no features launched)
- **Realistic Y1 total: ~NIS 150-180K** (conservative) to **~NIS 250-300K** (optimistic)
**Impact on PRD:**
- Section 6.5: Complete rewrite of Y1 revenue table
- Remove Emergency Surcharge and VAS from Y1
- Reduce B2B to NIS 15-30K
- Update total Y1 to NIS 150-300K range
- Appendix canonical data: update Y1 figure
- Note: Y2 and Y3 projections remain aspirational but should be flagged as dependent on seed funding and team hiring

### 6. TWO BREAKEVEN MILESTONES

**What:** Define two separate breakeven points.
- **Solo breakeven:** Revenue exceeds solo operating costs (~NIS 2-5K/mo) — estimated Month 2-4
- **Scaled breakeven:** Revenue exceeds full-team burn post-seed (~NIS 500-900K/mo) — estimated Month 20-26
**Impact on PRD:**
- Section 6.5: Add both breakeven milestones with clear labels
- Roadmap: Update breakeven references to distinguish solo vs scaled
- Roadmap Phase 5: Change "Breakeven at Month 20-26" to "Scaled breakeven at Month 20-26 (solo breakeven expected Month 2-4)"

### 7. FIX MONTH 24 REVENUE vs Y2 TOTAL

**What:** Roadmap says NIS 900K/mo at Month 24, but Y2 total is NIS 2.5-3.5M. If Month 24 = NIS 900K/mo, Y2 total should be ~NIS 4.8M (averaging ~NIS 400K/mo across 12 months).
**Fix:** Either reduce Month 24 target or increase Y2 total. Recommend: keep Y2 at NIS 2.5-3.5M (already aspirational) and reduce Month 24 revenue target to ~NIS 300-500K/mo to match.
**Impact on Roadmap:**
- Cumulative targets table: reduce Month 24 monthly revenue from NIS 900K+ to NIS 300-500K
- Phase 5 breakeven: adjust NIS 900K/mo reference

### 8. ADD NANNY SAFETY FEATURES TO P0

**What:** Add basic safety features for nannies going to unknown families' homes.
- "Share my location" WhatsApp deep link on booking confirmation screen
- Emergency 112 (police) / 101 (MDA) buttons prominently displayed
- Nanny-initiated check-in option (optional, not platform-required — avoids Wolt factor 3)
**Impact on PRD:**
- Section 3.4 (Booking Flow): Add safety features to Step 8a (booking confirmation screen)
- Add new feature N13: "Nanny safety tools" as P0
- Risk Register: update R5 to reflect nanny safety, not just child safety

### 9. REDUCE BOOKING MINIMUM FROM 3 DAYS TO 24 HOURS

**What:** Change Advance Booking (Tier 3) minimum lead time from 3+ days to 24+ hours.
**Why:** Israeli parents frequently need "tomorrow night" babysitting. 3-day minimum is too restrictive and makes the platform useless for the most common use case.
**Impact on PRD:**
- Section 3.4: Change "3+ days out" to "24+ hours out" everywhere
- Feature F5: Update acceptance criteria
- Section 4.2 Out-of-Scope: Update Short Notice (Tier 2) description — now covers <24 hours, not <3 days

### 10. FIX SEARCH: DISTANCE BUCKETS + REMOVE "AVAILABLE TODAY"

**What:**
- Remove "Available today" from search filters (contradicts 24-hour booking minimum). Replace with "Available this week"
- Change search algorithm from pure distance-first to distance buckets:
  - Near (<2km): sort by rating DESC
  - Farther (2-5km): sort by rating DESC
  - This prevents a 0.5km / 3-star nanny from always outranking a 2km / 5-star nanny
- Add "New on Emuni" badge + 30-day ranking boost for nannies with <3 reviews

**Impact on PRD:**
- Section 3.3 Search Filters: Replace "Available today" with "Available this week"
- Section 3.3 Search Algorithm: Rewrite SQL to use distance buckets
- Add new nanny boost logic

### 11. COMPANY REGISTRATION LANGUAGE

**What:** In articles of incorporation, use "development and operation of technology software for information services" — NOT "childcare matching" or "connecting families with nannies."
**Why:** Avoids labor court interpreting the company purpose as operating an employment bureau.
**Impact on PRD:**
- Section 7.1: Update company formation guidance with specific language recommendation

### 12. FOREIGN CONVICTION SELF-ATTESTATION

**What:** Add to nanny registration: "Have you ever been convicted of a crime outside of Israel?" (Yes/No self-declaration)
**Why:** Criminal record checks only cover Israeli offenses. Platform targets olim/immigrants. Self-attestation is NOT "requesting criminal information" under the 2019 law — it's asking for a voluntary self-declaration.
**Impact on PRD:**
- Section 3.2 Nanny Registration: Add self-attestation step
- Section 2.3: Add note about foreign conviction self-attestation as additional trust signal

### 13. KEEP FULL P0 SCOPE (NO FEATURE CUTS)

**What:** Founder decided to keep all P0 features. No deferrals of chat, AU10TIX, admin panel, or any other features.
**Note:** This is ambitious for solo dev in 8-12 weeks. PRD should note the risk.

---

## REMAINING ITEMS FROM ROUND 1 (already applied)

These were applied in the previous editing session:
- TOC anchor links fixed
- Phase numbering aligned (5 phases)
- Transaction fee standardized (12-15% range)
- Annual pricing removed from v1
- Expansion criteria (PMF = hard gate, 6 metrics = ideal)
- Founding Member counter (180 remaining)
- Edge cases added
- Open questions added
- All team/budget tables rewritten for solo bootstrapper

---

## ITEMS TO ALSO FIX (from swarm agents, not yet discussed but straightforward)

- Herzliya: should be Phase 4 or Phase 5? (PRD says Phase 4, Roadmap says Phase 5) → align to Roadmap (Phase 5)
- Florentin: add "Neve Tzedek" consistently or remove it → align to Roadmap (just "Florentin")
- Privacy compliance budget (NIS 140-395K): orphaned from team model → rewrite for bootstrapper
- COST_MODEL.md: add caveat at top that it's superseded by solo-bootstrapper model
- Risk R9 (no co-founder): rewrite for solo founder risks
- Risk R15 (class action): update given Track A removal
- Orphaned DPO references throughout PRD (multiple locations say "appoint before launch")
- CAC figures: add solo bootstrapper organic CAC (NIS 10-30) alongside scaled CAC
- Booking completion trigger: define who marks session done (auto-complete at end_time + 1hr)
- Nanny rejection flow: define what rejected nannies see and whether they can re-apply
- Account recovery: define what happens when phone number changes
- "Bring Your Nanny": confirm it stays P1 (not P0), update supply plan if needed
- Notification for new messages: add to F14 spec
- Free tier booking count: define what counts (only "confirmed" status)

---

## HOW TO APPLY

In the next session after /clear:
1. Read this file first
2. Read both EMUNI_PRD.md and EMUNI_ROADMAP.md
3. Apply all changes systematically
4. Update MEMORY.md with new decisions
