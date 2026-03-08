# Emuni Tech Services Research — Maps, Push Notifications, Real-time (March 2026)

> Research date: March 7, 2026. All data verified via web search, not training data.

---

## Table of Contents

1. [Maps & Geolocation](#1-maps--geolocation)
   - [1.1 Google Maps Platform — New Pricing Model](#11-google-maps-platform--new-pricing-model)
   - [1.2 Google Maps Routes API](#12-google-maps-routes-api)
   - [1.3 Mapbox](#13-mapbox)
   - [1.4 Apple MapKit](#14-apple-mapkit)
   - [1.5 OpenStreetMap / Nominatim](#15-openstreetmap--nominatim)
   - [1.6 Best Maps Solution for Emuni](#16-best-maps-solution-for-emuni)
2. [Push Notifications](#2-push-notifications)
   - [2.1 Expo Push Notification Service](#21-expo-push-notification-service)
   - [2.2 Firebase Cloud Messaging (FCM)](#22-firebase-cloud-messaging-fcm)
   - [2.3 OneSignal](#23-onesignal)
   - [2.4 Expo vs FCM — Recommendation for Emuni](#24-expo-vs-fcm--recommendation-for-emuni)
3. [Real-time / WebSocket / Chat](#3-real-time--websocket--chat)
   - [3.1 Supabase Realtime](#31-supabase-realtime)
   - [3.2 Ably, Pusher, Socket.io](#32-ably-pusher-socketio)
   - [3.3 Stream Chat / SendBird](#33-stream-chat--sendbird)
   - [3.4 Recommendation for Emuni](#34-recommendation-for-emuni)
4. [Summary Decision Matrix](#4-summary-decision-matrix)

---

## 1. Maps & Geolocation

### 1.1 Google Maps Platform — New Pricing Model

**Major change: The $200/month free credit was REMOVED on March 1, 2025.**

It was replaced with per-SKU free usage thresholds organized into three tiers:

| Tier | Free Calls/SKU/Month | Example SKUs |
|------|---------------------|--------------|
| **Essentials** | 10,000 | Dynamic Maps, Geocoding, Compute Routes Essentials, Compute Route Matrix Essentials |
| **Pro** | 5,000 | Address Validation, Nearby Search, Compute Routes Pro (traffic-aware), Compute Route Matrix Pro |
| **Enterprise** | 1,000 | Route Optimization, Photorealistic 3D Tiles, Compute Routes Enterprise (two-wheel routing) |

**What this means for Emuni:** Instead of a single $200 credit, you now get up to $3,250/month worth of free usage distributed across all SKUs. For a small app doing geocoding + distance calculations, this is actually **more generous** than before.

**Volume discounts:** Now scale to 5,000,000+ monthly billable events (up from 100,000+ pre-March 2025).

**Geocoding pricing (Essentials):**

| Monthly Volume | Cost per 1,000 Requests |
|----------------|------------------------|
| 0–10,000 | **FREE** |
| 10,001–100,000 | $5.00 |
| 100,001–500,000 | Volume discount (decreasing) |
| 5,000,000+ | $0.38 |

Sources:
- [Google Maps Platform Pricing Overview](https://developers.google.com/maps/billing-and-pricing/overview)
- [March 2025 Changes](https://developers.google.com/maps/billing-and-pricing/march-2025)
- [Core Services Pricing List](https://developers.google.com/maps/billing-and-pricing/pricing)
- [Changes FAQ](https://developers.google.com/maps/billing-and-pricing/faq)

---

### 1.2 Google Maps Routes API

**Distance Matrix API status: LEGACY (not deprecated, not dead).**

As of March 1, 2025, the Distance Matrix API was moved to **Legacy** status. Key facts:
- It still works for existing projects.
- It is **not available** for new Cloud projects.
- No hard shutdown date — Google will provide **12 months' notice** before decommissioning.
- It will **not** receive new features.
- Legacy services only get volume discounts up to 100,000 events (vs. 5M for Routes API).

**Recommended replacement: Routes API `computeRouteMatrix`**

#### Routes API Pricing

| SKU | Trigger | Free/Month | Cost per 1,000 (0-100K) | Cost per 1,000 (5M+) |
|-----|---------|-----------|-------------------------|----------------------|
| **Compute Routes Essentials** | Basic features, ≤10 waypoints | 10,000 | $5.00 | $0.38 |
| **Compute Routes Pro** | `TRAFFIC_AWARE` or `TRAFFIC_AWARE_OPTIMAL` | 5,000 | $10.00 | $0.75 |
| **Compute Routes Enterprise** | Two-wheel routing | 1,000 | $15.00 | $1.14 |
| **Compute Route Matrix Essentials** | Basic features | 10,000 elements | $5.00 | $0.38 |
| **Compute Route Matrix Pro** | Traffic-aware routing | 5,000 elements | $10.00 | $0.75 |
| **Compute Route Matrix Enterprise** | Two-wheel routing | 1,000 elements | $15.00 | $1.14 |

**Emuni impact:** For simple distance/duration calculations between parent and nanny (no traffic modeling), use **Essentials** tier = $5/1,000 elements with 10,000 free/month. At launch scale (~50 nannies, ~100 parents), Emuni will stay comfortably within the free tier.

**Max elements per request:** 625 (25 origins x 25 destinations).

Sources:
- [Routes API Usage and Billing](https://developers.google.com/maps/documentation/routes/usage-and-billing)
- [Migration Guide from Distance Matrix](https://developers.google.com/maps/documentation/routes/migrate-routes)
- [Legacy Products and Features](https://developers.google.com/maps/legacy)

---

### 1.3 Mapbox

**Current state (2025-2026):** Active, well-maintained alternative to Google Maps.

#### Pricing Overview

| Product | Free Tier | Paid Rate |
|---------|-----------|-----------|
| **Maps SDK (Mobile)** | 25,000 MAU | Usage-based after |
| **Maps GL JS (Web)** | 50,000 map loads/month | Usage-based after |
| **Temporary Geocoding** | 100,000 requests/month | $0.75/1,000 (100K-500K), down to $0.45/1,000 (1M-5M) |
| **Permanent Geocoding** | No free tier | Starts at $5/1,000 |
| **Search Box (Autofill)** | 500 sessions/month | Per-session billing |
| **Navigation SDK** | 100 MAU + 1,000 trips | Usage-based after |

#### Israel/Hebrew Support Assessment

- Mapbox supports Hebrew language in geocoding.
- Data sources: merges OSM with commercial and other open data.
- **Accuracy caveat:** Mapbox delivers "optimal result quality primarily across North American and European regions." Israel is not in that top tier.
- No Israel-specific test results found. **Must test with real Hebrew addresses before committing.**
- Mapbox expanded geocoding coverage in 2024-2025 (53 new countries added, 375M+ addresses), but Israel was not specifically highlighted.

#### Pros vs Google for Emuni
- Cheaper for maps rendering (25K free MAU vs Google's per-load billing)
- Better for custom map styling
- **Worse** for Hebrew address geocoding accuracy (Google wins for Israel)
- No Waze integration (Google owns Waze)

Sources:
- [Mapbox Pricing](https://www.mapbox.com/pricing)
- [Mapbox Geocoding 2024 Highlights](https://www.mapbox.com/blog/geocoding-2024-in-review-expanding-coverage-and-accuracy)
- [Mapbox vs Google Maps 2026](https://radar.com/blog/mapbox-vs-google-maps-api)

---

### 1.4 Apple MapKit

**Pricing:** Extremely generous for Apple Developer Program members ($99/year).

| Service | Free Allowance |
|---------|---------------|
| Maps Server API | 25,000 requests/day (~750K/month) |
| MapKit JS (web) | 250,000 map initializations/day + 25,000 service calls/day |
| MapKit (native iOS/macOS) | Free for apps earning <$10K net monthly revenue |

**Cross-platform relevance for Emuni (React Native + Expo):**
- `react-native-maps` uses Apple Maps on iOS by default — this is already free.
- The Maps Server API (REST-based) could theoretically be used for server-side geocoding from NestJS, but this is **not its intended use case** and Hebrew address coverage is inferior to Google.
- **Not a primary option** for a cross-platform app where you need consistent geocoding on both platforms.

Sources:
- [Apple Maps Developer Page](https://developer.apple.com/maps/)
- [Apple Maps Server API Docs](https://developer.apple.com/documentation/applemapsserverapi)

---

### 1.5 OpenStreetMap / Nominatim

**Viable for Israeli geocoding? Partially, with significant caveats.**

#### Capabilities
- Nominatim supports all countries and languages, including Hebrew.
- Free, open-source, self-hostable.
- OSM Israel data is actively maintained (last update: Feb 28, 2026).

#### Limitations
- **Accuracy is highly heterogeneous** — varies widely by area, even within the same city.
- Synthetic address generation can be "inaccurate or misleading."
- Urban areas (like TLV) are better covered than suburbs/rural.
- OSM data quality in Israel is specifically noted as politically contested and variable.
- **No SLA**, no support, no guaranteed uptime for the public Nominatim instance.
- Public API has strict rate limits (1 request/second).

#### Self-hosting option
- Can be self-hosted using Docker, but requires maintaining the server, data updates, and ops.
- Not practical for a solo bootstrapper.

**Verdict: NOT recommended as primary geocoder for Emuni.** Could serve as a free fallback or for non-critical lookups, but Google's Geocoding API with 10,000 free requests/month is the safer bet for Hebrew addresses in production.

Sources:
- [Nominatim](https://nominatim.org/)
- [OpenStreetMap Israel Wiki](https://wiki.openstreetmap.org/wiki/Israel)

---

### 1.6 Best Maps Solution for Emuni

**Recommendation: Google Maps Platform (Geocoding + Routes API Essentials)**

| Factor | Google Maps | Mapbox | OSM/Nominatim |
|--------|------------|--------|---------------|
| Hebrew address accuracy | Best (owns Waze data) | Good, not top-tier for Israel | Variable |
| RTL text support | Native | Supported | Basic |
| Free tier for Emuni scale | 10K geocoding + 10K route matrix = sufficient | 100K temporary geocoding = generous | Unlimited (self-host) or 1 req/sec (public) |
| Monthly cost at launch | $0 (within free tiers) | $0 (within free tiers) | $0 |
| React Native integration | `react-native-maps` (mature) | `rnmapbox/maps` (mature) | Requires manual integration |
| Waze traffic data | Yes (same company) | No | No |
| Expo compatibility | Full (`expo-maps` alpha or `react-native-maps`) | Full (`rnmapbox/maps`) | Manual |

**Specific plan for Emuni:**
1. **Map display:** `react-native-maps` with Google Maps on Android, Apple Maps on iOS (both free).
2. **Geocoding (address -> coordinates):** Google Geocoding API Essentials — 10,000 free/month, $5/1,000 after. Sufficient for launch.
3. **Distance calculation:** Google Routes API `computeRouteMatrix` Essentials — 10,000 free elements/month, $5/1,000 after. For 50 nannies x 100 parents = 5,000 elements, stays within free tier.
4. **Do NOT use:** Distance Matrix API (Legacy, will eventually be shut down).
5. **Do NOT use:** `expo-maps` (still alpha as of March 2026, requires iOS 18.0 minimum).

**Estimated monthly cost at launch: $0**
**Estimated monthly cost at 1,000 users: ~$5-25/month**

---

## 2. Push Notifications

### 2.1 Expo Push Notification Service

**Current state: Free, unlimited, production-ready.**

| Feature | Detail |
|---------|--------|
| **Cost** | **$0 — completely free, no paid tiers** |
| **Monthly message limit** | None |
| **Rate limit** | 600 notifications/second per project |
| **Batch limit** | 100 notifications per API request |
| **Delivery guarantee** | At-least-once delivery to APNs/FCM |
| **Token expiration** | ExpoPushTokens never expire (may change on reinstall) |
| **Data storage** | Messages held only in memory/queues, not databases |
| **Dependency** | Routes through FCM (Android) and APNs (iOS) under the hood |

**Limitations:**
- Tied to Expo ecosystem — works only with Expo-built apps
- No delivery analytics dashboard
- No message scheduling
- No rich segmentation or targeting
- Server-side rate limiting required (600/sec cap)
- Occasional duplicate or missed deliveries (rare)

Sources:
- [Expo Push Notifications FAQ](https://docs.expo.dev/push-notifications/faq/)
- [Expo Push Notifications Overview](https://docs.expo.dev/push-notifications/overview/)
- [EAS Pricing](https://expo.dev/pricing)

---

### 2.2 Firebase Cloud Messaging (FCM)

**Current state: Free, unlimited, no changes announced for 2025-2026.**

| Feature | Detail |
|---------|--------|
| **Cost** | **$0 — completely free, unlimited messages** |
| **Monthly message limit** | Unlimited |
| **Platform support** | Android, iOS (via APNs), Web |
| **Targeting** | Device-level, app version, user segments, topics |
| **Analytics** | Built-in with Firebase Analytics |
| **Scheduling** | Supported |
| **Rich notifications** | Supported (images, actions, etc.) |

**Important notes:**
- FCM itself is free, but adjacent Firebase services (Firestore, Cloud Functions) have their own pricing.
- FCM is the underlying transport that Expo Push uses on Android.
- Direct FCM integration gives more control but requires more setup.

Sources:
- [Firebase Pricing](https://firebase.google.com/pricing)
- [FCM vs Firebase Comparison 2026](https://ably.com/compare/fcm-vs-firebase)

---

### 2.3 OneSignal

**Current state: Freemium with generous free tier.**

| Plan | Cost | Mobile Push | Email | SMS |
|------|------|-------------|-------|-----|
| **Free** | $0 | Unlimited mobile push subscribers + sends | 10,000 emails/month | Free trial |
| **Growth** | $19/month + usage | $0.012/MAU | $0.0005/email | $0.015/SMS |
| **Professional** | Annual contract | Custom | Custom | Custom |

**Free plan limitations:**
- 10,000 web push subscribers max
- 1 active In-App Message
- 10 segments, limited data tags
- No Journeys automation

**Why you might want OneSignal:**
- Dashboard for marketing/segmentation
- A/B testing on notifications
- Multi-channel (push + email + SMS)

**Why you probably don't need it for Emuni v1:**
- Adds complexity and a vendor dependency
- Expo Push + FCM covers all v1 needs for free
- Marketing automation is a post-PMF concern

Sources:
- [OneSignal Pricing](https://onesignal.com/pricing)
- [Understanding OneSignal Pricing](https://onesignal.com/blog/understanding-onesignals-pricing/)

---

### 2.4 Expo vs FCM — Recommendation for Emuni

**Recommendation: Expo Push Notification Service for v1.**

| Factor | Expo Push | FCM Direct | OneSignal |
|--------|-----------|------------|-----------|
| Cost | Free | Free | Free (limited) |
| Setup complexity | Minimal (built into Expo) | Moderate (Firebase config) | Moderate (SDK + dashboard) |
| Expo compatibility | Native | Requires `react-native-firebase` | Requires OneSignal SDK |
| Analytics | None | Firebase Analytics | Built-in dashboard |
| Segmentation | None (DIY) | Topics + conditions | GUI-based segments |
| Scheduling | None (DIY on server) | Built-in | Built-in |
| Production reliability | Good | Excellent | Excellent |

**Migration path:**
1. **v1 (Launch):** Expo Push — zero setup, free, works out of the box.
2. **v2 (Growth):** If you need scheduling, analytics, or segmentation, either:
   - Add FCM direct via `react-native-firebase` for more control, OR
   - Add OneSignal for marketing automation.
3. Both can coexist with Expo's notification handling library (`expo-notifications`).

---

## 3. Real-time / WebSocket / Chat

### 3.1 Supabase Realtime

**Current state: Production-ready for moderate-scale chat, already in Emuni's tech stack.**

#### Capabilities
Three core features over WebSocket:
1. **Broadcast** — ephemeral pub/sub messaging (chat messages)
2. **Presence** — online/offline status tracking
3. **Postgres Changes** — listen to database INSERT/UPDATE/DELETE in real-time

#### Pricing by Plan

| Feature | Free | Pro ($25/mo) | Team ($599/mo) |
|---------|------|-------------|----------------|
| **Realtime Messages** | 2 million/month | 5 million/month | 5 million/month |
| **Peak Connections** | 200 | 500 | 500 |
| **Message Overage** | N/A (hard limit) | $2.50 per 1M | $2.50 per 1M |
| **Connection Overage** | N/A (hard limit) | $10 per 1,000 | $10 per 1,000 |

#### Performance Benchmarks
- Latency: typically <100ms for message delivery
- 200-500 concurrent users in production chat: solid performance
- 10,000+ concurrent WebSocket connections: works without issues
- 100K+ concurrent: requires architecture planning (read replicas, connection pooling)

#### Limitations
- **No delivery guarantee** — the server does not guarantee every message reaches every client.
- Broadcast partitions retained for **3 days** only.
- Default limits: 100 channels/tenant, 200 users/channel, 100 events/second.
- Database bottleneck can limit message throughput.
- Free plan: projects **auto-pause after 7 days of inactivity** (not suitable for production).

#### Chat Viability for Emuni
- At launch scale (50 nannies, ~100 parents): **200 peak connections and 2M messages/month is more than sufficient** on the Free plan.
- But Free plan auto-pauses — **must use Pro ($25/mo) for production**.
- On Pro: 500 peak connections and 5M messages/month. At 500 users exchanging ~100 messages/day = 1.5M messages/month. Well within limits.

Sources:
- [Supabase Realtime Pricing](https://supabase.com/docs/guides/realtime/pricing)
- [Supabase Realtime Limits](https://supabase.com/docs/guides/realtime/limits)
- [Supabase Pricing](https://supabase.com/pricing)
- [Supabase Review 2026](https://hackceleration.com/supabase-review/)

---

### 3.2 Ably, Pusher, Socket.io

#### Ably

| Feature | Free | Standard | Pro |
|---------|------|----------|-----|
| **Messages** | 6 million/month | Usage-based | Usage-based |
| **Pricing** | $0 | $2.50/million messages | Volume discounts down to $0.50/million |
| **Channels** | Included | $1.00/million channel-minutes | Volume discounts |

**Strengths:** Globally distributed, low-latency, delivery guarantees, 6M free messages.
**Weakness:** Another vendor to manage, no database integration.

#### Pusher Channels

| Plan | Concurrent Connections | Messages/Day | Monthly Cost |
|------|----------------------|--------------|-------------|
| **Sandbox (Free)** | 200 | 200,000 | $0 |
| **Startup** | 500 | 1,000,000 | Paid |
| **Pro** | 2,000 | 4,000,000 | Paid |
| **Business** | 5,000 | 10,000,000 | Paid |

**Strengths:** Simple API, good docs, established.
**Weakness:** Daily message limits (not monthly), no database integration.

#### Socket.io

- Open-source library, not a managed service.
- Requires self-hosting and managing WebSocket infrastructure.
- No built-in persistence, presence, or auth.
- **Not recommended** for a solo bootstrapper — too much ops overhead.

#### Should Emuni Use Any of These?

**No.** Supabase Realtime is already in the tech stack (Supabase is the chosen database). Adding Ably or Pusher would mean:
- An additional vendor and billing account
- Duplicating infrastructure (Supabase already has WebSockets)
- More complexity for no clear benefit at Emuni's scale

The only reason to add a dedicated realtime service would be if Supabase Realtime proves unreliable at scale (10K+ concurrent users), which is a post-seed-funding problem.

Sources:
- [Ably Pricing](https://ably.com/pricing)
- [Ably Free Package](https://ably.com/docs/platform/pricing/free)
- [Pusher Channels Pricing](https://pusher.com/channels/pricing/)
- [Socket.IO vs Supabase 2026](https://ably.com/compare/socketio-vs-supabase)
- [Pusher vs Supabase 2026](https://ably.com/compare/pusher-vs-supabase)

---

### 3.3 Stream Chat / SendBird

Both are **managed chat SDKs** — pre-built UI components, message history, threads, reactions, typing indicators, read receipts, moderation, etc.

#### Stream Chat

| Plan | MAU | Monthly Cost | Key Features |
|------|-----|-------------|-------------|
| **Maker (Free)** | No limit stated | $0 (if <5 team members AND <$10K/mo revenue) | Full API access, $100/mo credit |
| **Startup** | 10,000 | ~$499/month | Full features |
| **Elevate** | 25,000 | ~$1,299/month | Full features |
| **Enterprise** | 100,000+ | Custom | SLA, dedicated support |

**Storage overage:** Media transfer ~$0.12/GB, storage ~$0.05/GB.
**React Native SDK:** Official, maintained, customizable UI components.
**AI integration:** Built-in support for OpenAI, Claude, Gemini chatbots.
**Performance:** Scales to 5M concurrent users, API response avg 9ms.

#### SendBird

| Plan | MAU | Monthly Cost |
|------|-----|-------------|
| **Developer (Free)** | 100 MAU (after 30-day trial) | $0 |
| **Starter (25K MAU)** | 25,000 | ~$1,199/month |
| **Pro** | Custom | Custom |
| **Enterprise** | Custom | Custom |

**Overage:** $0.010-$0.012/user depending on tier.
**Key concern:** Widely reported as expensive and less transparent. Extra charges for file storage and traffic.

#### Should Emuni Use Stream or SendBird?

**Not for v1. Build custom chat on Supabase Realtime.**

Reasoning:
1. **Cost:** Stream's Maker plan is free but only if revenue < $10K/month. Once Emuni monetizes, you're looking at $499+/month — that's 20x the Supabase Pro cost.
2. **SendBird:** Developer plan is only 100 MAU — useless. Starter at $1,199/month is absurd for a bootstrapped launch.
3. **Emuni's chat needs are simple:** Parent sends message to nanny, nanny replies. No group chat, no threads, no reactions needed at v1.
4. **Supabase Realtime + custom UI** is sufficient for 1:1 messaging. You already have the database, auth, and WebSocket infrastructure.
5. **Migration option:** If chat becomes a core differentiator and you need rich features (typing indicators, read receipts, message search), migrate to Stream at that point.

Sources:
- [Stream Chat Pricing](https://getstream.io/chat/pricing/)
- [Stream Chat React Native SDK](https://getstream.io/chat/sdk/react-native/)
- [SendBird Pricing](https://sendbird.com/pricing/chat)
- [SendBird Pricing Breakdown 2025](https://www.cometchat.com/blog/sendbird-pricing-plans-review)
- [SendBird vs Stream 2026](https://ably.com/compare/sendbird-vs-stream)

---

### 3.4 Recommendation for Emuni

**Build custom chat on Supabase Realtime. Here's the architecture:**

```
Parent App  <-- WebSocket -->  Supabase Realtime (Broadcast)
                                      |
                                      v
                              Supabase PostgreSQL
                              (messages table with RLS)
                                      |
                                      v
Nanny App   <-- WebSocket -->  Supabase Realtime (Postgres Changes)
```

**Implementation plan:**
1. `messages` table in PostgreSQL with `sender_id`, `recipient_id`, `booking_id`, `content`, `created_at`
2. Row Level Security: users can only read messages where they are sender or recipient
3. Supabase Realtime `Postgres Changes` to push new messages to connected clients
4. `Broadcast` channel for typing indicators (optional, v2)
5. `Presence` for online/offline status (optional, v2)
6. Push notification via Expo Push when recipient is offline

**Cost at launch: $25/month (Supabase Pro, which you need anyway for production).**

---

## 4. Summary Decision Matrix

| Service | Chosen Solution | Monthly Cost (Launch) | Monthly Cost (1K Users) | Migration Trigger |
|---------|----------------|----------------------|------------------------|-------------------|
| **Map Display** | `react-native-maps` (Google Maps Android, Apple Maps iOS) | $0 | $0 | N/A |
| **Geocoding** | Google Geocoding API (Essentials) | $0 (within 10K free) | ~$5-10 | 10K+ geocode requests/month |
| **Distance Calc** | Google Routes API `computeRouteMatrix` (Essentials) | $0 (within 10K free) | ~$5-15 | Complex routing needs |
| **Push Notifications** | Expo Push Notification Service | $0 | $0 | Need scheduling/analytics -> add FCM or OneSignal |
| **Real-time Chat** | Supabase Realtime (already in stack) | $25 (Supabase Pro) | $25 (within 5M messages) | >500 concurrent users -> upgrade plan |
| **Chat UI** | Custom (built on Supabase) | $0 (dev time) | $0 | Need rich features -> migrate to Stream Chat |

### Total Infrastructure Cost at Launch: ~$25/month (Supabase Pro only)

### Key PRD Updates Needed

1. **Replace all "Distance Matrix API" references with "Routes API `computeRouteMatrix`"** — Distance Matrix is Legacy since March 2025, not available for new projects.
2. **Remove $200/month Google Maps credit assumption** — replaced with per-SKU free thresholds (actually more generous for small apps).
3. **Add Google Maps pricing tier classification** — Emuni should use Essentials tier only (no traffic-aware routing needed at v1).
4. **Confirm push notification strategy** — Expo Push is free and sufficient for v1. No need for FCM direct or OneSignal at launch.
5. **Add Supabase Realtime limits to architecture section** — Free plan: 200 connections, 2M messages. Pro plan: 500 connections, 5M messages.
6. **Do NOT adopt `expo-maps`** — still alpha as of March 2026, requires iOS 18.0 minimum. Use `react-native-maps` instead.

---

*Last updated: March 7, 2026*
