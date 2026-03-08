# Nanny Platform Matching Flow Specification

## Executive Summary

The optimal matching model is a **social-trust hybrid marketplace** that combines job posting (parent broadcasts a need) with profile search (parent browses nannies), layered on a **community trust graph** where friend recommendations and neighborhood connections determine ranking. The platform operates four distinct booking flows calibrated by urgency — from 15-minute emergency broadcasts to 48-hour recurring job postings — with **request-based matching for first-time bookings** (safety friction) and **streamlined one-tap rebooking for established relationships** (speed). Background checks are mandatory, platform-paid, and completed before any nanny appears in search. The system uses positive reinforcement (badges, visibility boosts, tiered perks) instead of penalties to maintain supply-side health, and integrates WhatsApp as the confirmed-booking communication channel. Every design decision prioritizes the Israeli cultural model: replicate the Facebook-group flow (post, get recommendations, DM), frame as community not marketplace, and respect the hamlatza (recommendation) culture that drives Israeli childcare trust.

---

## 1. The 4 Booking Flows

### 1.1 Tier 1: Emergency / Same-Day

**Trigger:** Parent needs a nanny within 0-6 hours.

**Step-by-step flow:**

1. Parent taps "I Need a Sitter Now" (prominent button on home screen)
2. Parent enters: start time, end time, number/ages of children, any special requirements (one screen, pre-filled from profile where possible)
3. System identifies up to **5 best-matched available nannies** using the matching algorithm (Section 13) — filters by: availability set to "today", distance <= 5km, children's age experience match, trust graph proximity
4. All 5 nannies receive **simultaneous push notification + SMS**: "A family in [neighborhood] needs a sitter from [time] to [time]. Tap to view."
5. Nannies have **15 minutes** to accept or decline
6. **First nanny to accept is auto-booked** (single confirmation — no parent review step for emergency)
   - Exception: If the parent has never used this nanny before, parent gets a 3-minute confirmation window with nanny's profile summary (photo, rating, trust connections). If parent doesn't respond in 3 minutes, booking auto-confirms.
7. If no nanny accepts within 15 minutes: system **expands radius to 10km** and broadcasts to the next 5 best matches. Another 15-minute window.
8. If still no match after 30 minutes total: parent receives notification "We couldn't find a sitter right now. Would you like to post this as a Short Notice request (2-4 hour window)?" with one-tap conversion.
9. Upon confirmation: both parties see booking details. WhatsApp deep link provided for coordination ("I'm on my way", "door code is...").

**Pricing:** Surge multiplier of **1.3x** the nanny's standard rate for < 2 hours notice. 1.0x for 2-6 hours notice. Nanny sees the boosted rate before accepting.

**Cancellation:** Parent cancels < 1 hour before start = 50% of booked hours paid to nanny. Nanny cancels < 1 hour = reliability score impact + parent gets priority rebooking.

---

### 1.2 Tier 2: Short Notice ("This Weekend" / 6 hours - 3 days out)

**Trigger:** Parent needs a nanny within 6 hours to 3 days.

**Step-by-step flow:**

1. Parent taps "Find a Sitter" and enters: date, start/end time, number/ages of children, requirements
2. System shows **top 5 matched nannies** ranked by matching algorithm. Parent sees: photo, first name, rating, response time badge, trust connections ("Used by 3 families you know"), hourly rate, distance
3. Parent selects **up to 3 nannies** to send request to simultaneously
4. Selected nannies receive push notification: "A family in [neighborhood] is looking for a sitter on [date] [time]. Tap to view details."
5. Nannies have **4 hours** to accept or decline
6. As each nanny accepts, parent is notified: "[Name] is available! Tap to confirm."
7. Parent reviews accepting nannies and **chooses one** (double confirmation)
   - If only 1 nanny accepts after 4 hours, parent gets a nudge: "[Name] is available. Confirm booking?" Auto-expire the request if parent doesn't confirm within 2 hours.
8. Unchosen nannies receive: "This booking has been filled. You'll be notified of new opportunities."
9. If no nanny accepts within 4 hours: system suggests 5 new matches. Parent can send a second round. If second round also fails after 4 hours, suggest posting as an Advance Booking.

**Reminders:** Nannies who haven't responded get 1 reminder at the 2-hour mark. No more than 1 reminder per request.

**Cancellation:** Parent cancels < 12 hours before = 25% fee. < 6 hours = 50% fee. Nanny cancels < 12 hours = reliability score impact.

---

### 1.3 Tier 3: Advance Booking (3+ days out)

**Trigger:** Parent is planning ahead — date night next week, travel coverage, etc.

**Step-by-step flow:**

1. Parent uses **full search/browse mode**: filters by availability, distance, rate range, experience, languages, certifications, trust connections
2. System shows results ranked by matching algorithm (Section 13), paginated, 10 per page
3. Parent browses profiles at their pace. Can "favorite" nannies for later.
4. Parent sends a **booking request to 1 specific nanny** at a time (not broadcast — this is a considered choice)
5. Request includes: date, time, number/ages of children, any special notes ("bedtime is 20:00, please read stories")
6. Nanny has **24 hours** to accept or decline
7. Reminders sent at **12 hours** and **20 hours** if no response
8. If nanny declines or request expires: parent is notified and prompted to request another nanny. System suggests the next best match.
9. Upon acceptance: double confirmation. Parent confirms the booking.
10. For **first-time bookings**: platform encourages (not requires) a video/phone call before the date. Shows prompt: "This is your first time with [Name]. Want to schedule a quick intro call?" with one-tap scheduling.

**Cancellation:** > 48 hours = no fee. 24-48 hours = 25%. 12-24 hours = 50%. < 12 hours = 75%. No-show = 100%.

---

### 1.4 Tier 4: Recurring / Ongoing Arrangement

**Trigger:** Parent needs regular childcare (e.g., Sun-Thu 14:00-18:00 after-school).

**Step-by-step flow:**

1. Parent taps "Find Regular Help" and fills out a **job posting**: schedule (days/times), duration (ongoing / X months), number/ages of children, duties (pickup from school, homework help, cooking), rate range, requirements (first aid, car, languages)
2. Job posting is visible to all matched nannies in the area (passive — nannies browse and apply)
3. System also **pushes the job** to the top 10 best-matched nannies via notification: "A family in [neighborhood] is looking for regular help [schedule]. Tap to view."
4. Nannies have **48 hours** to apply. Application includes: available schedule confirmation, rate expectation, brief message to family
5. Parent reviews applications. Can view full profiles, reviews, trust connections.
6. Parent **shortlists 2-3 candidates** and initiates in-app messaging or schedules video/phone calls
7. Parent selects one nanny. **Both parties confirm** the arrangement.
8. A **1-2 week trial period** begins. Either party can end the arrangement during trial with no penalty.
9. After trial: recurring booking auto-creates weekly sessions. Either party can cancel individual sessions or end the arrangement with 1 week notice.

**Auto-renewal:** Recurring bookings auto-renew weekly. Parent and nanny each get a weekly summary: "Your upcoming sessions this week: [list]"

**Cancellation of individual session:** Same policy as Advance Booking. Cancellation of arrangement: 1 week notice required from either party.

---

## 2. Discovery Model

### 2.1 Dual Discovery — Post + Search

Parents have two primary paths, accessible from the home screen:

**Path A: "I Need a Sitter" (Post/Request)**
- Parent describes their need (date, time, requirements)
- System matches and sends to relevant nannies
- Nannies come to the parent
- Best for: Emergency, Same-Day, Short Notice, Recurring

**Path B: "Browse Sitters" (Search)**
- Parent browses available nanny profiles with filters
- Parent initiates contact with specific nannies
- Parent goes to the nanny
- Best for: Advance Booking, building a "My Nannies" list, discovering new nannies

### 2.2 Search Filters

| Filter | Options | Default |
|--------|---------|---------|
| Distance | 1km, 3km, 5km, 10km, 15km | 5km |
| Availability | Specific date/time, "Available today", Day of week | None |
| Hourly rate | Slider: 30-80 NIS/hr | Full range |
| Experience with ages | Infant (0-1), Toddler (1-3), Preschool (3-6), School age (6-12), Teen (12+) | From parent profile |
| Languages | Hebrew, Arabic, English, Russian, Amharic, French | Hebrew |
| Certifications | First Aid, CPR, Education degree, Special needs | None |
| Trust connections | "Known to my network", "Used by friends" | None (but results weighted by this) |
| Rating | 4.0+, 4.5+, 4.7+ | None |
| Verification level | Established, Trusted, Premium | All verified |

### 2.3 Search Results Display

Each result card shows:
- Profile photo
- First name + last initial
- Trust badge (tier icon)
- Star rating + number of reviews
- "Responds within X hours" badge
- Distance from parent
- Hourly rate
- Social connection indicator: "Used by [Name] and 2 others you know" or "New to your network"
- Top 2 tags: "Great with toddlers", "First aid certified"
- Availability indicator: green dot = available today, yellow = available this week

Results are **ranked by the matching algorithm** (Section 13), not by distance or price alone.

---

## 3. Multi-Request Logic

### 3.1 Simultaneous Request Limits

| Tier | Max simultaneous nannies contacted | Max active requests at a time |
|------|-----------------------------------|-------------------------------|
| Emergency | 5 (system-selected, broadcast) | 1 |
| Short Notice | 3 (parent-selected) | 1 |
| Advance | 1 (parent-selected) | 2 |
| Recurring | Unlimited applicants (job post) | 1 |

### 3.2 Request Lifecycle Rules

1. **One active Emergency or Short Notice request at a time.** Parent cannot spam the platform with overlapping urgent requests for the same time slot.
2. **Up to 2 active Advance requests** allowed — for different dates/times only. Not for the same slot.
3. **1 active Recurring job post** at a time.
4. When a request is filled (nanny accepts + parent confirms), all other requests for the same time slot are **auto-cancelled**.
5. When a request expires with no match, the parent is prompted to retry with adjusted parameters (wider radius, higher rate, different time).

### 3.3 Cascading Logic

For Emergency and Short Notice tiers, if initial batch yields no acceptances:

```
Round 1: Top 5 matches within 5km → wait [tier timeout]
Round 2: Next 5 matches within 10km → wait [tier timeout]
Round 3: Next 5 matches within 15km → wait [tier timeout]
Round 4: Notify parent "No sitters available. Try adjusting your request."
```

Each round only fires if the previous round produced zero acceptances. If even one nanny accepts during any round, cascading stops.

---

## 4. Response Time Windows

### 4.1 Per-Tier Windows

| Tier | Nanny response window | Auto-expiry | Reminder schedule | Escalation |
|------|----------------------|-------------|-------------------|------------|
| Emergency | 15 min | Yes, auto-expire + cascade | None (too short) | Expand radius, broadcast next batch |
| Short Notice | 4 hours | Yes, auto-expire | 1 reminder at 2hr mark | Suggest new matches to parent |
| Advance | 24 hours | Yes, auto-expire | At 12hr and 20hr | Suggest next match to parent |
| Recurring | 48 hours | Yes, close applications | At 24hr | Extend posting if < 2 applicants |

### 4.2 Parent Response Windows

After a nanny accepts, the parent must also act:

| Tier | Parent confirmation window | If parent doesn't respond |
|------|---------------------------|--------------------------|
| Emergency (first-time nanny) | 3 minutes | Auto-confirm |
| Emergency (known nanny) | Auto-confirmed | N/A |
| Short Notice | 2 hours after last acceptance | Request expires, nannies released |
| Advance | 24 hours | Request expires, nanny released |
| Recurring | 72 hours (review period) | Applicants notified posting closed |

### 4.3 "Responds Within" Badge

Every nanny profile displays a response time badge calculated from rolling 30-day data:

- "Typically responds within **minutes**" (median < 30 min)
- "Typically responds within **1 hour**" (median 30 min - 1 hr)
- "Typically responds within **a few hours**" (median 1-4 hr)
- "Typically responds within **a day**" (median 4-24 hr)
- No badge shown if insufficient data (< 5 responses)

---

## 5. First-Time vs. Repeat Booking

### 5.1 First-Time Booking Flow

When a parent has **never booked** a specific nanny before:

1. **Full profile review required** — parent must scroll through entire profile (background check status, reviews, certifications, "about me") before the "Request" button becomes active. Minimum 10 seconds on profile page.
2. **Booking request must include a message** — even a brief one ("Hi, looking for help Thursday evening"). This establishes human connection.
3. **After nanny accepts:** platform shows a prompt: "This is your first time with [Name]. We recommend a quick intro call before your booking." One-tap call scheduling or WhatsApp link.
4. **First booking confirmation screen** shows a safety checklist:
   - "Background check: Passed [date]"
   - "Identity verified: Yes"
   - "Reviews: [count] from [count] families"
   - "Connected to you through: [Name] (or 'New to your network')"
5. **"First Time" badge** visible to the nanny so they can prepare (arrive a few minutes early for introductions, expect to be shown around the house).
6. **Post-booking:** Both sides prompted to leave a review within 48 hours. Higher urgency prompt than for repeat bookings.

### 5.2 Repeat Booking Flow

When a parent has **previously completed at least 1 booking** with a nanny:

1. **"My Nannies" list** — parent sees all nannies they've used before, with last booking date, rating they gave, and current availability status.
2. **One-tap request** — parent taps a nanny, selects date/time, sends. No message required. No profile review gate.
3. **For Emergency tier with a known nanny:** nanny accepts = auto-confirmed. No parent confirmation step. Target: booking completed in under 60 seconds.
4. **Quick re-book:** After a completed session, the confirmation screen includes "Book [Name] again?" with suggested next dates based on pattern (e.g., if parent books every Thursday, suggest next Thursday).

### 5.3 "Favorite" vs. "My Nannies"

- **Favorites:** Nannies the parent has bookmarked but never booked. Still requires first-time flow.
- **My Nannies:** Nannies the parent has completed at least 1 booking with. Unlocks repeat booking flow.

---

## 6. Trust and Safety Integration

### 6.1 Pre-Listing Safety Gate (Before Nanny Appears in Search)

Every nanny must complete ALL of the following before their profile appears in any search result:

| Check | Method | Timeline | Renewal |
|-------|--------|----------|---------|
| Identity verification | Government ID (Teudat Zehut) + selfie match via Persona or equivalent | 1-3 days | Once |
| Criminal background check | Israel Police records check | 5-10 days | Annual |
| Sex offender registry | Cross-reference with national registry | Included in background check | Annual |
| Profile review | Manual review by Trust & Safety team | 1-2 days | On profile changes |
| Profile photo | Must be a clear face photo (no sunglasses, no group) | At signup | On change |

**Cost:** Platform pays for all checks. This is a cost of doing business — Care.com's mistake of charging nannies led to low verification rates and safety incidents.

**Status for nanny during checks:** "Your profile is being verified. We'll notify you when you're live (typically 5-10 business days)." Nanny can complete their profile, set rates, write bio — but is invisible to parents.

### 6.2 Trust Tiers

| Tier | Requirements | Visible Badge | Perks |
|------|-------------|---------------|-------|
| **Verified** | Background check passed, ID verified, < 3 reviews | Blue shield | Can receive requests |
| **Established** | 3+ completed bookings, 4.0+ avg rating, 80%+ response rate | Silver shield | Higher search ranking |
| **Trusted** | 10+ completed bookings, 4.5+ avg rating, 90%+ response rate, 6+ months active | Gold shield | Featured in search, priority notifications for premium jobs |
| **Premium** | 25+ completed bookings, 4.7+ avg rating, 95%+ response rate, First Aid certified, 12+ months active | Purple shield | Top of search, "Platform Recommended" label, eligible for recurring/VIP families |

### 6.3 Safety Touchpoints in the Booking Flow

```
[Nanny signs up]
    |-- Identity verification (Teudat Zehut + selfie)
    |-- Background check initiated
    |-- Profile manual review
    |-- [BLOCKED until all pass]
    v
[Nanny visible in search]
    |
[Parent finds nanny]
    |-- Background check status visible on profile
    |-- Trust tier badge visible
    |-- Social connections visible ("used by 3 families you know")
    |-- Reviews visible
    |
[Parent sends request]
    |-- First-time: full profile scroll required
    |-- First-time: message required
    |
[Nanny accepts]
    |-- First-time: intro call prompt
    |-- Safety checklist shown to parent
    |-- Emergency contacts exchanged
    |
[Session starts]
    |-- Optional location sharing (nanny check-in)
    |-- Session timer active
    |-- Emergency button available (calls parent, then 112/101)
    |
[Session ends]
    |-- Both sides prompted for review (blind, 48hr window)
    |-- Payment processed
    |-- Safety concern? "Report an issue" link
```

### 6.4 Content Monitoring

- All in-app messages scanned for: phone numbers before booking (prevent off-platform), inappropriate content, spam patterns
- Nanny profiles scanned for: misleading claims, copied text, inappropriate photos
- Reviews moderated for: personal attacks, irrelevant content, fake patterns (multiple 5-star reviews from new accounts)

---

## 7. Social Trust Layer

### 7.1 How the Trust Graph Works

The trust graph is the platform's **primary differentiator** — it replicates the Israeli hamlatza culture digitally.

**Data sources for the trust graph:**

1. **Phone contacts** (with permission): "5 people in your contacts use this app" — identifies potential connections
2. **Explicit connections:** Parents can connect with other parents they know (like Facebook friends but childcare-specific)
3. **Community groups:** Parents join their neighborhood, school, or gan group. All members of a group can see which nannies other members have used.
4. **Booking history:** When Parent A books Nanny X and leaves a positive review, Parent B (who is connected to Parent A) sees "Recommended by [Parent A]" on Nanny X's profile.
5. **Vouching:** Parents can explicitly "vouch" for a nanny — a stronger signal than a review. Vouch = "I trust this person with my children." Limited to 5 vouches per parent (keeps it meaningful).

### 7.2 Trust Graph Display

On a nanny's profile, the parent sees (in priority order):

1. **Direct connection:** "You've booked [Name] before" (if repeat)
2. **Friend's nanny:** "[Friend Name] has used [Name] 8 times" (strongest social signal)
3. **Community connection:** "Used by 4 families in [Neighborhood Group]"
4. **Extended network:** "Used by 12 families in your extended network"
5. **No connection:** "New to your network" (no social signal — parent relies on reviews and verification)

### 7.3 Trust Graph Impact on Matching

Social proximity is a **major factor** in the matching algorithm (Section 13). A nanny with a "friend's nanny" connection will rank significantly higher than a stranger with the same rating and distance.

### 7.4 Community Groups

- Parents join groups based on: neighborhood (auto-suggested from address), school/gan (searchable), or custom (e.g., "English-speaking parents in Ra'anana")
- Groups are **private** — membership requires approval from a group admin
- Within a group, parents can see: which nannies other members have used, aggregate ratings from group members, and a "group favorites" list of top-rated nannies
- Groups serve as the **digital equivalent of the WhatsApp neighborhood group** — but with structured data instead of chat noise

---

## 8. Notification Strategy

### 8.1 Notification Channels by Tier

| Tier | Primary channel | Secondary channel | Tertiary |
|------|----------------|-------------------|----------|
| Emergency | Push notification | SMS (simultaneous) | - |
| Short Notice | Push notification | SMS (after 1hr no response) | - |
| Advance | Push notification | - | Email digest (daily) |
| Recurring | Push notification | - | Email digest (daily) |

### 8.2 Notification Caps

| Rule | Limit |
|------|-------|
| Max push notifications per nanny per day | 3 |
| Max push notifications per parent per day | 5 |
| Quiet hours (no notifications) | 22:00 - 07:00 local time |
| Max reminders per request | 2 |
| Max SMS per nanny per day | 2 (emergency + 1 follow-up) |

### 8.3 Notification Types and Timing

**For Nannies:**

| Event | Channel | When |
|-------|---------|------|
| New matching request | Push + SMS (emergency) or Push (other) | Immediately |
| Reminder: unanswered request | Push | Per tier schedule |
| Booking confirmed | Push | Immediately |
| Booking cancelled by parent | Push + SMS | Immediately |
| Session reminder | Push | 2 hours before start AND 30 minutes before |
| Payment received | Push | When processed |
| New review received | Push | When submitted |
| Weekly summary | Email | Sunday 09:00 |

**For Parents:**

| Event | Channel | When |
|-------|---------|------|
| Nanny accepted your request | Push | Immediately |
| Request expired (no match) | Push | At expiry |
| Session reminder | Push | 2 hours before start |
| Nanny is on the way | Push | When nanny marks "heading out" |
| Session completed — leave review | Push | 1 hour after session end |
| Review reminder | Push | 24 hours after session (if no review yet) |
| Favorite nanny has new availability | Push | Daily at 10:00 (batched) |
| Pre-holiday nudge | Push | 7 days before major chag |

### 8.4 Smart Notification Routing

- Do NOT send job notifications to nannies who are: currently in a session, marked as unavailable for that time, outside the distance radius, at their daily notification cap
- Batch non-urgent notifications (new reviews, availability updates) into a daily digest at 10:00
- If a nanny has consistently ignored a certain type of request (e.g., always declines evening jobs), reduce those notifications over time (ML-based relevance filtering)

---

## 9. Cancellation and No-Show Policy

### 9.1 Parent Cancellation

| Timing | Fee (% of booked hours) | Where fee goes |
|--------|------------------------|----------------|
| > 48 hours before start | 0% | - |
| 24-48 hours | 15% | To nanny |
| 12-24 hours | 25% | To nanny |
| 6-12 hours | 50% | To nanny |
| < 6 hours | 75% | To nanny |
| No-show (parent not home) | 100% | To nanny |

### 9.2 Nanny Cancellation

| Timing | Financial penalty | Platform consequence |
|--------|------------------|---------------------|
| > 48 hours before start | None | None |
| 24-48 hours | None | Minor reliability score impact |
| 12-24 hours | None | Moderate reliability score impact |
| < 12 hours | None | Significant reliability score impact |
| < 2 hours | None | Major reliability score impact + manual review if pattern |
| No-show | None (but platform may suspend after investigation) | Severe reliability impact + account review |

**No financial penalties for nannies.** The Wolt/Deliveroo lesson is clear: financial penalties destroy supply-side trust in gig marketplaces. Instead, reliability score impacts affect search ranking and eligibility for premium tiers. Chronic unreliability (3+ late cancellations in 30 days) triggers a supportive outreach message, not punishment.

### 9.3 Emergency Replacement

When a nanny cancels < 6 hours before start:

1. Parent receives immediate notification: "[Name] cancelled. We're searching for a replacement."
2. System auto-triggers an **Emergency tier request** using parent's original booking details
3. If parent has other nannies in "My Nannies" list, they are contacted first
4. Parent can also cancel the replacement search if they've made other arrangements

### 9.4 Dispute Resolution

- Either party can "Report an Issue" within 72 hours of session end
- Issues handled by Trust & Safety team within 24 hours (target)
- For payment disputes: platform holds funds for 72 hours after session before releasing to nanny (allows dispute window)
- Mediation before any account action — both sides heard

---

## 10. Israeli Market Adaptations

### 10.1 WhatsApp Integration

WhatsApp is not optional — it is the backbone of Israeli communication.

**Integration points:**

| Stage | WhatsApp role |
|-------|--------------|
| Pre-booking | NOT used. All communication stays in-app to protect privacy and enable monitoring. |
| Booking confirmed | WhatsApp deep link provided: "Chat with [Name] on WhatsApp" for coordination (directions, door code, "running 5 min late") |
| Session day | WhatsApp for real-time coordination |
| Post-session | Review and payment stay in-app |

**Implementation:** After booking confirmation, both parties receive each other's WhatsApp-linked phone number. The app provides a "Open WhatsApp" button that creates a pre-filled message: "Hi [Name], I'm [Parent Name] from [App Name]. Looking forward to [date]!"

**Why not replace in-app messaging entirely:** Privacy (don't share numbers before commitment), safety (monitor pre-booking communication for red flags), data (track response times and engagement for matching algorithm).

### 10.2 Hebrew and RTL UX

- Full RTL layout: navigation, buttons, swipe directions, progress bars all mirrored
- Hebrew as default language. Full Arabic and English language options.
- Font size 10% larger than standard for Hebrew (no uppercase for emphasis)
- Bidirectional text support for mixed Hebrew/English content (common in Israeli tech UX)
- Date format: DD/MM/YYYY. Time format: 24-hour (14:00, not 2:00 PM).
- Currency: NIS displayed as "X per hour" (not "ILS" — Israelis say "shekel")
- Day names in Hebrew. Week starts Sunday.

### 10.3 Cultural UX Adaptations

| Israeli behavior | Platform adaptation |
|-----------------|---------------------|
| Hamlatza (recommendation) culture | Trust graph is the #1 ranking signal. "Recommended by [Name]" is the most prominent element on nanny cards. |
| "I want to see all options" | Show 3-5 curated matches but always provide a "See more" button. Never hide options. |
| Negotiation culture | Nannies set rate ranges (e.g., "40-55 NIS/hr") not fixed prices. Parents can see the range and discuss. |
| Direct communication | Clear yes/no flows. No ambiguous states. "Available" or "Not available." "Accepted" or "Declined." |
| Thursday night = going out night | Thursday afternoon push to parents: "Planning Thursday night? Book your sitter now." |
| Erev chag surge | 7 days before major holidays: "Chag is coming! Your favorites are filling up — book now." |
| Sunday = start of work week | Sunday morning is peak search time. Ensure system capacity and fast response. |
| Community framing | Never say "marketplace" or "platform" in user-facing copy. Say "your neighborhood's babysitter network" or "your family's sitter circle." |
| Military/sherut leumi as trust signal | Optional profile field: "Completed military service / national service." Visible as a badge, not a filter. |

### 10.4 Israeli Calendar Integration

- Support Hebrew calendar dates alongside Gregorian
- Pre-built awareness of: Shabbat times (auto-adjust availability), chag dates (surge prep), school vacation schedule (Pesach, summer, Sukkot — extended childcare needs), chol hamoed (intermediate days)
- "Erev chag mode": 7 days before a major chag, the home screen shows a banner prompting advance booking

---

## 11. Nanny-Side Experience

### 11.1 Profile Setup

Nannies complete their profile in stages (progressive, not overwhelming):

**Stage 1 (Required before verification):**
- Full name, phone, address (for distance calculation — not shown to parents)
- Government ID upload (Teudat Zehut)
- Selfie for ID verification
- Profile photo (clear face)
- Date of birth (must be 18+)

**Stage 2 (Required before going live):**
- "About Me" text (minimum 50 characters)
- Experience: years, age groups, special skills
- Languages spoken
- Hourly rate range
- General availability (weekday mornings, evenings, weekends — broad strokes)

**Stage 3 (Optional, boosts ranking):**
- Video introduction (30-60 seconds)
- Certifications upload (First Aid, CPR, education degree)
- References from previous families (platform contacts them)
- "Why I love working with kids" prompt

### 11.2 Availability Management

- **Weekly availability calendar:** Nanny sets recurring available blocks (e.g., Sun-Thu 14:00-20:00, Fri 10:00-14:00)
- **Override for specific dates:** Mark specific dates as unavailable (vacation, exams) or add extra availability
- **"Available Now" toggle:** One-tap to indicate availability for same-day emergency requests. Auto-expires after 8 hours or end of day.
- **Auto-block:** When a booking is confirmed, that time slot is automatically blocked in the calendar. No double-booking possible.

### 11.3 Request Management

**Nanny's home screen shows:**
- Active requests awaiting response (with countdown timer)
- Upcoming confirmed bookings (chronological)
- Earnings summary (this week / this month)

**For each incoming request, nanny sees:**
- Family's neighborhood (not exact address until confirmed)
- Number and ages of children
- Date, start time, end time
- Any special requirements
- Parent's rating (from other nannies — two-sided reviews)
- Earnings for this session (hours x rate, including any surge multiplier)
- Trust connection: "You've worked with this family before" or "This family is in your neighborhood"

**One-tap actions:** "Accept" / "Decline" / "Suggest Different Time"

"Suggest Different Time" lets the nanny counter-propose without declining. Parent gets notification: "[Name] can't do 14:00-18:00 but is available 15:00-19:00. Accept alternative?"

### 11.4 Nanny Dashboard

- **Earnings:** Weekly/monthly breakdown, pending payments, payment history
- **Stats:** Response rate, reliability score, average rating (all shown positively — "You respond to 92% of requests!" not "You ignored 8%")
- **Reviews:** All reviews received, with option to respond to each
- **Calendar:** Visual weekly/monthly view of bookings and availability
- **Tier progress:** "You're 3 bookings away from Trusted status!" with progress bar

---

## 12. Matching Algorithm

### 12.1 Scoring Model

Each potential nanny match is scored on a 0-100 scale. The score determines ranking in search results and priority in broadcast notifications.

**Scoring weights:**

| Factor | Weight | Calculation |
|--------|--------|-------------|
| **Social trust proximity** | 30% | Direct connection (used before) = 30. Friend's nanny = 25. Community connection = 15. Extended network = 8. No connection = 0. |
| **Availability match** | 20% | Exact match with requested time = 20. Partial overlap >= 75% = 15. "Available Now" toggle on = 18 (for emergency). No availability data = 0. |
| **Distance** | 15% | < 1km = 15. 1-3km = 12. 3-5km = 9. 5-10km = 5. 10-15km = 2. > 15km = 0. |
| **Rating and reviews** | 15% | (avg_rating / 5.0) * review_count_factor * 15. review_count_factor = min(review_count / 10, 1.0). A 4.8 with 20 reviews scores higher than 5.0 with 1 review. |
| **Response reliability** | 10% | (response_rate * 0.5 + on_time_rate * 0.3 + low_cancellation * 0.2) * 10 |
| **Experience match** | 7% | Nanny's experience with the specific age group of parent's children. Exact match = 7. Adjacent age group = 4. No data = 2. |
| **Profile completeness** | 3% | Video intro = +1. Certifications = +1. References verified = +1. |

### 12.2 Scoring Adjustments

| Condition | Adjustment |
|-----------|------------|
| Nanny is in parent's "Favorites" list | +15 bonus |
| Nanny has been booked by parent before | +20 bonus |
| Parent explicitly vouched for this nanny | +25 bonus |
| Nanny's trust tier is Premium | +5 bonus |
| Nanny has not worked in 30+ days | -5 (may be inactive) |
| Nanny has 2+ cancellations in last 30 days | -10 |
| Request is for age group nanny has never worked with | -5 |

### 12.3 Anti-Gaming Rules

- Nannies cannot see their own score or the scoring formula
- Score is recalculated on each request (not cached) to reflect latest data
- Fake review detection: flag accounts that only review one nanny, or reviews submitted without a completed booking
- Social connection fraud: connections must be mutual (both parties confirm) to count toward trust score

### 12.4 Cold Start (New Nannies)

New nannies with no reviews or connections start with a **base score of 35** (out of 100). To prevent new nannies from being permanently buried:

- **New nanny boost:** For the first 30 days, new nannies get a +10 bonus to their score (decays linearly: +10 on day 1, +0 on day 30)
- **"New in Your Area" section:** A dedicated section on the search page showing recently verified nannies nearby. Parents who book a new nanny get a small incentive (e.g., "Book a new sitter and get 10% off your first session")
- **Social bootstrap:** If a new nanny is vouched for by an existing parent user before they even get their first booking, they start with the social trust score instead of 0

---

## 13. Flow Diagrams

### 13.1 Emergency / Same-Day Flow

```
PARENT                          PLATFORM                         NANNY
  |                                |                               |
  |-- "I Need a Sitter Now" ----->|                               |
  |   (time, kids, requirements)  |                               |
  |                                |-- Score & rank top 5 -------->|
  |                                |   (within 5km, available)     |
  |                                |                               |
  |                                |-- Push + SMS to 5 nannies --->|
  |                                |   "Family needs sitter now"   |
  |                                |                               |
  |                                |          15 MIN WINDOW        |
  |                                |                               |
  |                                |<--- Nanny A: Accept ----------|
  |                                |                               |
  |   [If first-time nanny:]      |                               |
  |<-- "Nanny A accepted.         |                               |
  |    Confirm?" (3 min window)   |                               |
  |-- Confirm ------------------>|                               |
  |                                |                               |
  |   [If known nanny:]           |                               |
  |<-- "Booked! [Name] is        |-- "You're booked!" ---------->|
  |    confirmed." (auto)         |   (address, details)          |
  |                                |                               |
  |                                |-- Cancel other 4 requests --->|
  |                                |   "This booking was filled"   |
  |                                |                               |
  |<-- WhatsApp link for [Name] --|-- WhatsApp link for parent -->|
  |                                |                               |
  |              ... SESSION ...   |                               |
  |                                |                               |
  |<-- "How was [Name]?" ---------|-- "How was this family?" ---->|
  |    (blind review, 48hr)       |   (blind review, 48hr)        |


  IF NO RESPONSE IN 15 MIN:

  |                                |-- Expand to 10km ------------>|
  |                                |-- Push + SMS next 5 --------->|
  |                                |        15 MIN WINDOW          |
  |                                |                               |

  IF STILL NO RESPONSE (30 MIN TOTAL):

  |<-- "No sitters available.     |                               |
  |    Convert to Short Notice?"  |                               |
```

### 13.2 Short Notice Flow

```
PARENT                          PLATFORM                         NANNY
  |                                |                               |
  |-- "Find a Sitter" ----------->|                               |
  |   (date, time, requirements)  |                               |
  |                                |-- Show top 5 matches -------->|
  |<-- Display 5 nanny cards -----|                               |
  |                                |                               |
  |-- Select 3 nannies ---------->|                               |
  |   "Send request"              |                               |
  |                                |-- Push to 3 nannies --------->|
  |                                |   "Family looking for sitter" |
  |                                |                               |
  |                                |          4 HOUR WINDOW        |
  |                                |                               |
  |                                |<--- Nanny B: Accept ----------|
  |<-- "[Name B] is available!" --|                               |
  |                                |                               |
  |                                |     [2hr mark: remind others] |
  |                                |                               |
  |                                |<--- Nanny C: Accept ----------|
  |<-- "[Name C] is also          |                               |
  |     available!"               |                               |
  |                                |                               |
  |-- Choose Nanny B ------------>|                               |
  |                                |-- "You're booked!" --------->| (to B)
  |                                |-- "Booking filled" ---------->| (to C)
  |                                |-- Auto-cancel Nanny A's req ->|
  |                                |                               |
  |<-- Booking confirmed          |                               |
  |    + WhatsApp link            |                               |
```

### 13.3 Advance Booking Flow

```
PARENT                          PLATFORM                         NANNY
  |                                |                               |
  |-- Browse/Search sitters ----->|                               |
  |   (filters: date, distance,  |                               |
  |    rate, age group, etc.)     |                               |
  |                                |                               |
  |<-- Search results (ranked) ---|                               |
  |                                |                               |
  |-- View [Name]'s full profile ->|                               |
  |   (scroll through: bio,       |                               |
  |    reviews, certifications,   |                               |
  |    background check, trust)   |                               |
  |                                |                               |
  |-- "Request Booking" --------->|                               |
  |   + message to nanny          |                               |
  |                                |-- Push notification --------->|
  |                                |   "New booking request"       |
  |                                |                               |
  |                                |         24 HOUR WINDOW        |
  |                                |    [Reminders: 12hr, 20hr]    |
  |                                |                               |
  |                                |<--- Nanny: Accept ------------|
  |<-- "[Name] accepted!          |                               |
  |     Confirm booking?"         |                               |
  |                                |                               |
  |   [First-time? Prompt for     |                               |
  |    intro video/phone call]    |                               |
  |                                |                               |
  |-- Confirm ------------------>|                               |
  |                                |-- "Booking confirmed!" ----->|
  |<-- Confirmation + details ----|                               |
  |    + WhatsApp link            |                               |
```

### 13.4 Recurring Arrangement Flow

```
PARENT                          PLATFORM                         NANNY
  |                                |                               |
  |-- "Find Regular Help" ------->|                               |
  |   (schedule, duties, rate     |                               |
  |    range, requirements)       |                               |
  |                                |-- Create job posting -------->|
  |                                |   (visible in nanny's feed)   |
  |                                |                               |
  |                                |-- Push to top 10 matches ---->|
  |                                |   "A family needs regular     |
  |                                |    help — matches your        |
  |                                |    availability"              |
  |                                |                               |
  |                                |         48 HOUR WINDOW        |
  |                                |    [Reminder at 24hr]         |
  |                                |                               |
  |                                |<--- Nanny D: Apply -----------|
  |                                |     (schedule, rate, message) |
  |                                |<--- Nanny E: Apply -----------|
  |                                |<--- Nanny F: Apply -----------|
  |                                |                               |
  |<-- "3 nannies applied!" ------|                               |
  |                                |                               |
  |-- Review applications ------->|                               |
  |-- Message Nanny D & E ------->|<-------- in-app chat -------->|
  |-- Schedule call with D ------>|                               |
  |                                |                               |
  |-- Select Nanny D ------------>|                               |
  |                                |-- "You got the job!" -------->| (D)
  |                                |-- "Family chose another       | (E, F)
  |                                |    nanny for this role"       |
  |                                |                               |
  |   TRIAL PERIOD (1-2 WEEKS)    |                               |
  |                                |                               |
  |-- Confirm ongoing? --------->|                               |
  |-- YES ----------------------->|                               |
  |                                |-- Create recurring sessions ->|
  |                                |   (auto-generated weekly)     |
  |<-- Weekly schedule confirmed --|-- Weekly schedule confirmed ->|
```

### 13.5 Nanny Onboarding Flow

```
NEW NANNY
  |
  |-- Download app, sign up (phone number + OTP)
  |
  |-- Stage 1: Identity
  |   |-- Enter full name, DOB, address
  |   |-- Upload Teudat Zehut (front + back)
  |   |-- Take selfie for ID match
  |   |-- Upload profile photo
  |
  |-- [Background check initiated — 5-10 business days]
  |-- [Profile reviewed by Trust & Safety — 1-2 days]
  |
  |-- Stage 2: Profile (can complete while waiting)
  |   |-- Write "About Me"
  |   |-- Select experience (age groups, years)
  |   |-- Set languages
  |   |-- Set hourly rate range
  |   |-- Set weekly availability
  |
  |-- [All checks pass]
  |
  |-- PROFILE GOES LIVE
  |   |-- "You're verified! Families can now find you."
  |   |-- 30-day new nanny boost active
  |
  |-- Stage 3: Optional enhancements
  |   |-- Record video introduction
  |   |-- Upload certifications
  |   |-- Add references
  |
  |-- [First request received]
  |   |-- Accept/Decline
  |   |-- Complete first booking
  |   |-- Receive first review
  |   |-- Progress toward "Established" tier
```

---

## 14. What We Chose NOT to Do (and Why)

### 14.1 No Fully Managed Matching (Poppy Model)

**What it is:** Platform assigns a nanny to the family with no parent choice.

**Why we rejected it:** Poppy (Y Combinator W16) tried this exact model and shut down in December 2018 after burning through $2M+. The managed curation layer made unit economics impossible. Parents wanted $20/hr sitters but personalized matching required expensive human operations. Israeli parents particularly want to choose — "I want to see all options and decide myself."

### 14.2 No Pure On-Demand / Uber Model

**What it is:** Parent taps a button, nearest available nanny is auto-dispatched.

**Why we rejected it:** Nanno tried this ("The Uber for childcare") and was acquired in 2022 after failing to scale. Childcare is not a commodity — parents won't accept "any available" nanny the way they accept any available taxi. Trust must be established before booking, especially for first-time matches. We use on-demand elements only for Emergency tier with known nannies.

### 14.3 No Financial Penalties for Nannies

**What it is:** Charging nannies for declining requests, late cancellations, or low acceptance rates.

**Why we rejected it:** Wolt couriers struck in Kazakhstan over commission cuts. Deliveroo riders protested unfair account deactivation. In a childcare marketplace where supply is already the harder side to grow, financial penalties would destroy trust and drive nannies to competitors or back to Facebook groups. We use positive reinforcement exclusively: badges, visibility boosts, tiered perks.

### 14.4 No Paywall for Parents to Contact Nannies

**What it is:** Requiring a paid subscription before parents can message nannies (Care.com model at $39-78/month).

**Why we rejected it:** Care.com is heavily criticized for this. Parents pay monthly but may not find a match. For the Israeli market, where Facebook groups and WhatsApp are free alternatives, a paywall would prevent adoption. Revenue comes from transaction fees, not access fees.

### 14.5 No Unverified Nanny Profiles in Search

**What it is:** Showing nanny profiles before background checks complete (with a "pending" badge).

**Why we rejected it:** Care.com's biggest safety scandal: unvetted caregivers on the platform led to child injuries and deaths, an $8.5M FTC settlement, and a separate $480K settlement. Our platform pays for background checks and completes them before any nanny appears in search. "Pending" nannies are invisible. This is non-negotiable.

### 14.6 No Algorithmic "Recommendations"

**What it is:** Telling parents "We recommend [Name]" or "Our top pick for you."

**Why we rejected it:** Courts are increasingly holding platforms liable when algorithms actively recommend services. If our AI recommends a specific nanny and something goes wrong, liability is higher than if the parent selected independently. We show "matches based on your preferences" — sorted results, not recommendations. The parent always makes the choice.

### 14.7 No Unlimited Multi-Requesting

**What it is:** Letting parents contact 10+ nannies simultaneously for a single booking.

**Why we rejected it:** Marketplace theory (Paradox of Choice) shows that more than 5-7 options causes decision paralysis. Additionally, mass-contacting degrades supply-side experience — nannies receive too many low-intent requests, become fatigued, and stop responding. We cap at 5 (emergency broadcast) or 3 (parent-selected short notice).

### 14.8 No In-App Chat Replacement for WhatsApp

**What it is:** Building a full messaging platform and discouraging WhatsApp use.

**Why we rejected it:** WhatsApp has 99% penetration in Israel. Fighting WhatsApp is fighting user behavior. Instead, we use in-app messaging for pre-booking communication (where we need monitoring and data) and hand off to WhatsApp for confirmed bookings (where parents and nannies expect it). The platform provides the match; WhatsApp provides the relationship.

### 14.9 No Auction / Bidding Model

**What it is:** Nannies compete on price to win a booking (race to the bottom).

**Why we rejected it:** Price competition drives quality providers away. Israeli parents making childcare decisions are not optimizing for cheapest — they're optimizing for trust. Nannies set their own rate ranges, and pricing is transparent. No bidding, no reverse auction.

### 14.10 No Automated Reviews

**What it is:** Auto-generating reviews or ratings based on booking completion data alone.

**Why we rejected it:** Authentic human reviews are the trust currency. Auto-generated "stars" have no credibility. We prompt both parties for reviews but never fabricate or auto-fill them. A nanny with 5 genuine reviews is more trustworthy than one with 50 auto-generated ones.

---

## Appendix A: Key Numbers Reference

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Max nannies in emergency broadcast | 5 | Balance speed vs. flooding |
| Max nannies parent can select (short notice) | 3 | Paradox of choice: 3-5 optimal |
| Max active emergency/short notice requests | 1 | Prevent spam |
| Max active advance requests | 2 | Allow planning flexibility for different dates |
| Emergency response window | 15 min | Israeli same-day expectation: 15-30 min |
| Short notice response window | 4 hours | 2-4 hour range from research |
| Advance response window | 24 hours | Airbnb standard, proven |
| Recurring application window | 48 hours | Job-posting model needs time |
| Parent confirmation (emergency, first-time) | 3 min | Fast but allows profile glance |
| Parent confirmation (short notice) | 2 hours | Time to choose from acceptors |
| Quiet hours | 22:00-07:00 | Research: up to 40% better open rates |
| Max push notifications/nanny/day | 3 | Industry best practice |
| Max push notifications/parent/day | 5 | Slightly higher (booking confirmations count) |
| Emergency surge multiplier | 1.3x | Meaningful incentive, not exploitative |
| Background check renewal | Annual | UrbanSitter standard |
| New nanny score boost duration | 30 days | Enough for first few bookings |
| New nanny score boost value | +10 (decaying) | Prevents permanent burial |
| Blind review window | 48 hours | Airbnb model |
| Payment hold before release | 72 hours | Dispute window |
| Default search radius | 5 km | Urban Israeli density |
| Max search radius (emergency cascade) | 15 km | Practical commute limit |
| Minimum profile view time (first-time) | 10 seconds | Prevents rushing past safety info |
| Trial period (recurring) | 1-2 weeks | Enough for mutual evaluation |
| Cancellation dispute window | 72 hours | Standard |
| Vouches per parent (max) | 5 | Keeps vouches meaningful |

## Appendix B: Glossary

| Term | Meaning |
|------|---------|
| Hamlatza | Hebrew for "recommendation" — the cultural foundation of trust in Israeli childcare |
| Trust graph | The network of connections between parents, showing which nannies are known/vouched by friends |
| Broadcast | Sending a request to multiple nannies simultaneously |
| Cascade | Expanding the search radius and pool after initial broadcast yields no response |
| Single confirmation | Nanny accepts = booking confirmed (no parent step needed) |
| Double confirmation | Nanny accepts, then parent confirms from among acceptors |
| Surge multiplier | Rate increase for last-minute emergency bookings |
| Cold start | The challenge of ranking new nannies who have no reviews or connections |
| Trust tier | Verification level (Verified, Established, Trusted, Premium) based on track record |
| Quiet hours | Period when no notifications are sent (22:00-07:00) |
| My Nannies | Parent's list of nannies they've completed at least 1 booking with |
| Favorites | Parent's list of bookmarked nannies they haven't booked yet |
