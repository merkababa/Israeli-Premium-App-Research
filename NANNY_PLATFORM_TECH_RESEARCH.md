# Nanny Platform Technical Research

## Research Date: March 2026

---

## 1. Tech Stack Recommendation for Israeli Marketplace Startup

### 1.1 Frontend: React Native (Recommended)

**Recommendation: React Native with Expo**

| Framework | Market Share | Pros | Cons |
|-----------|-------------|------|------|
| **React Native** | ~35% cross-platform | Massive JS/TS talent pool in Israel; built-in RTL/Hebrew support via I18nManager; code sharing with web (React); Expo simplifies builds/OTA updates; 90% code shared between iOS/Android | Slightly less pixel-perfect UI than Flutter |
| **Flutter** | ~46% cross-platform | Pixel-perfect UI; hot reload; growing ecosystem; desktop support production-ready in 2026 | Dart is niche (harder to hire in Israel); smaller Israeli developer community; less mature RTL support |
| **Native (Swift + Kotlin)** | N/A | Best performance; full platform API access | 2x development cost; 2x maintenance; impractical for a startup |

**Why React Native wins for this project:**
- **Israeli talent pool**: Israel's 450,000+ developers skew heavily toward JavaScript/TypeScript. React Native developers are significantly easier to hire than Dart/Flutter developers in Tel Aviv.
- **RTL-first support**: React Native has mature RTL support via `I18nManager`. Use `start`/`end` instead of `left`/`right` in all layouts. Hebrew text rendering works natively.
- **Expo**: Expo SDK handles push notifications, OTA updates, camera (for ID verification), and location services out of the box, dramatically reducing time-to-market.
- **Web code sharing**: If a web dashboard is needed later (admin panel, nanny profile management), React code can be shared via React Native Web.

**RTL Implementation Notes:**
- Call `I18nManager.forceRTL(true)` at app initialization for Hebrew-first layout
- Use `start`/`end` properties instead of `left`/`right` in all FlexBox styles
- Icons and images do NOT auto-flip -- manually mirror directional icons (arrows, back buttons)
- Test with both Hebrew and English since the app may need bilingual support (Russian, Arabic speakers)

### 1.2 Backend: Node.js with NestJS (Recommended)

| Option | Pros | Cons |
|--------|------|------|
| **Node.js / NestJS** | Same language as frontend (TypeScript end-to-end); excellent real-time support (WebSockets, Socket.io); non-blocking I/O ideal for marketplace matching; huge Israeli developer pool; NestJS provides structure at scale | CPU-intensive tasks need worker threads |
| **Python / Django** | Great for ML/AI matching algorithms; Django REST framework mature | Two languages in stack; slower real-time; GIL limits concurrency |
| **Go** | Excellent performance; great concurrency | Smaller talent pool in Israel; less ecosystem for marketplace features |

**Why Node.js/NestJS:**
- TypeScript end-to-end (frontend + backend) means one language for the entire team
- NestJS provides enterprise-grade structure (modules, dependency injection, guards) while keeping Node.js performance
- Native WebSocket support for real-time matching notifications
- Fastify adapter available for maximum performance (2x Express throughput)
- Offload CPU-intensive matching algorithms to worker threads or Bull/BullMQ job queues

**Recommended Node.js version:** Node 24 LTS (current Active LTS as of 2026)

### 1.3 Database: PostgreSQL with PostGIS (Recommended)

| Option | Geospatial | Social Graph | ACID | Scaling |
|--------|-----------|-------------|------|---------|
| **PostgreSQL + PostGIS** | 1,000+ spatial functions; distance, radius, polygon queries | Excellent with recursive CTEs and materialized views | Full ACID | Vertical + read replicas; Supabase/Neon for managed |
| **MongoDB** | 3 geospatial functions (geoWithin, geoIntersects, nearSphere) | Document references; no joins | Eventual consistency (default) | Horizontal sharding |

**Why PostgreSQL wins decisively:**
- **Geospatial superiority**: PostGIS provides 1,000+ spatial functions vs MongoDB's 3. For a nanny platform needing distance calculations, radius searches, and neighborhood boundaries in Israeli urban areas, PostGIS is the clear winner.
- **Social trust graph**: The platform's community trust graph (friend recommendations, neighborhood connections) maps naturally to relational data with JOIN operations and recursive CTEs for graph traversal.
- **ACID compliance**: Financial transactions (booking payments, nanny payouts) require ACID guarantees.
- **Supabase integration**: Supabase provides managed PostgreSQL with real-time subscriptions, built-in auth, and row-level security -- perfect for marketplace apps.
- **Full-text search**: PostgreSQL's `tsvector` supports Hebrew full-text search natively, potentially eliminating the need for a separate search engine at MVP scale.

### 1.4 Real-Time: Supabase Realtime (Recommended)

| Option | Pricing | Pros | Cons |
|--------|---------|------|------|
| **Supabase Realtime** | Free tier; Pro $25/mo; Team $599/mo | Built on PostgreSQL; real-time row subscriptions; predictable pricing; open-source; self-host option | Newer than Firebase |
| **Firebase Realtime/Firestore** | Pay per read/write operation | Google ecosystem; mature; offline sync | NoSQL (loses relational benefits); unpredictable costs at scale (3-5x more than Supabase for heavy read/write); vendor lock-in |
| **Custom WebSockets (Socket.io)** | Infrastructure cost only | Full control; no vendor dependency | Must build everything; scaling complexity |

**Why Supabase:**
- **PostgreSQL-native**: Since we're already using PostgreSQL, Supabase Realtime subscribes directly to database changes -- no sync layer needed.
- **Predictable pricing**: $25/mo Pro plan vs Firebase's per-operation billing that can spike unpredictably. Case studies show Firebase costing 3-5x more than Supabase for production apps.
- **Open-source**: Can self-host if costs become an issue or if Israeli data residency becomes required.
- **Auth included**: Supabase Auth handles email/password, phone (SMS OTP), and social login -- reduces integration work.

### 1.5 Search: PostgreSQL Full-Text Search (MVP) -> Algolia (Scale)

| Option | Pricing | Hebrew Support | Complexity |
|--------|---------|---------------|-----------|
| **PostgreSQL FTS** | Included with DB | Hebrew via `tsvector` with Hunspell dictionary | Zero additional infrastructure |
| **Algolia** | Free: 10K requests + 100K records/mo; then ~$0.50/1K requests | Excellent multi-language including Hebrew | SaaS; easy to implement; expensive at scale |
| **Elasticsearch** | Self-hosted or Elastic Cloud ($95+/mo) | Hebrew via ICU plugin | Complex to operate; requires dedicated DevOps |

**Recommendation:**
- **MVP**: Use PostgreSQL full-text search with GIN indexes. For a nanny profile search (name, skills, neighborhood, languages), PostgreSQL FTS is more than adequate for the first 10,000-50,000 profiles.
- **Scale (50K+ profiles)**: Migrate to Algolia for sub-50ms search with typo tolerance, faceted filtering, and geo-search. At MVP volumes, the free tier covers needs.
- **Avoid Elasticsearch at MVP**: Operational overhead is too high for a startup. One case study showed Elasticsearch setup requiring dedicated infrastructure at $2M+ over 3 years.

### 1.6 Hosting: AWS il-central-1 (Recommended)

All three major cloud providers now have Israel regions:

| Provider | Israel Region | Status | Availability Zones | Key Advantage |
|----------|-------------|--------|-------------------|---------------|
| **AWS** | il-central-1 (Tel Aviv) | GA since Aug 2023 | 3 AZs | Largest service catalog; $7.2B investment in Israel by 2037; 99.99% uptime SLA |
| **GCP** | me-west1 (Tel Aviv) | GA since 2022 | 3 zones | Google's private fiber network; native Supabase competitor (but we're using Supabase on AWS) |
| **Azure** | Israel Central | GA since 2023 | With AZs | Best for hybrid/enterprise; Microsoft ecosystem |

**Why AWS il-central-1:**
- **Largest ecosystem**: Most services available in-region (ECS/EKS, RDS PostgreSQL, ElastiCache, S3, CloudFront, Lambda)
- **Supabase compatibility**: Supabase can be self-hosted on AWS or used as SaaS with data flowing through AWS infrastructure
- **Israeli data residency**: All three providers offer data residency in Israel, but AWS has the most mature offering with 3 AZs
- **Cost**: AWS is competitive with GCP for compute; free tier is generous for MVP (750 hrs/mo EC2, 750 hrs/mo RDS)
- **CDN**: CloudFront edge location in Israel ensures low latency for static assets and API caching

**Estimated Monthly Hosting Cost (MVP):**
- EC2 (t3.medium): ~$30/mo
- RDS PostgreSQL (db.t3.micro): ~$15/mo
- S3 + CloudFront: ~$5/mo
- ElastiCache (Redis, t3.micro): ~$12/mo
- **Total: ~$62/mo** (before free tier credits)

### 1.7 CI/CD, Monitoring, Error Tracking

| Category | Tool | Pricing | Why |
|----------|------|---------|-----|
| **CI/CD** | GitHub Actions | Free for public repos; 2,000 min/mo free for private | Industry standard; integrates with PR workflow |
| **Error Tracking** | Sentry | Free tier; Team $26/mo; Business $80/mo | Developer-first; real-time error tracking; React Native SDK; straightforward pricing |
| **APM/Monitoring** | Datadog (later) or AWS CloudWatch (MVP) | CloudWatch: included with AWS; Datadog: free trial then paid | CloudWatch for MVP; Datadog when you need full observability |
| **Uptime Monitoring** | Better Uptime / UptimeRobot | Free tier available | Simple, effective |
| **Analytics** | Mixpanel or Amplitude | Free tier for <1K MTU | Product analytics for marketplace metrics |

**MVP Stack:** GitHub Actions + Sentry (free) + CloudWatch + Mixpanel (free)

### 1.8 Complete Recommended Stack Summary

```
Frontend:     React Native + Expo (TypeScript)
Backend:      Node.js + NestJS (TypeScript) on Fastify
Database:     PostgreSQL 16+ with PostGIS (via Supabase or AWS RDS)
Real-time:    Supabase Realtime (WebSocket subscriptions)
Cache:        Redis (ElastiCache)
Search:       PostgreSQL FTS (MVP) -> Algolia (scale)
Auth:         Supabase Auth (email, phone OTP, social)
Storage:      S3 (profile photos, documents)
CDN:          CloudFront
Hosting:      AWS il-central-1
CI/CD:        GitHub Actions
Monitoring:   Sentry + CloudWatch
Analytics:    Mixpanel
```

**Estimated MVP Infrastructure Cost: $100-150/month**

---

## 2. Background Check Integration in Israel

### 2.1 Israel Police Criminal Record Check

**There is NO public API for Israel Police criminal records.**

The process is entirely manual:
1. Individual goes to nearest police station
2. Fills out a dedicated request form (bring Teudat Zehut / ID)
3. Police processes the request
4. Certificate of Good Conduct (Teudat Yosher / תעודת יושר) is issued
5. **Timeline: 2-4 weeks** for standard processing

**Key legal context:**
- Under Israeli law, employers are generally **restricted** from performing criminal background checks on prospective employees
- **Exception**: The law for prevention of employment of sex offenders in institutions working with children **requires** employers to obtain a confirmation certificate from Israel Police
- This exception is directly applicable to a nanny/childcare platform

**Implication for the platform:**
- Cannot automate police checks via API
- Must require nannies to upload their Certificate of Good Conduct (Teudat Yosher)
- Platform can verify the document's authenticity via AU10TIX document verification
- Consider partnering with a physical verification service to streamline the process

### 2.2 Sex Offender Registry

**Israel's sex offender registry is NOT public.** Only Israel Police and prison services can access it.

- No public database, no API, no web portal for queries
- Unlike the US (Megan's Law), Israel does not make this data available to the public or employers
- The 2006 Community Protection from Sex Offenders Law enables risk assessment and supervisory measures but does not create public access
- Advocacy groups have pushed for a public registry but no legislation has passed

**Implication for the platform:**
- Cannot directly query the sex offender registry
- Must rely on the Certificate of Good Conduct from Israel Police, which includes information about sexual offenses
- The police certificate requirement under the childcare institution law is the platform's primary legal mechanism

### 2.3 AU10TIX (Israeli Company) -- ID Verification

**AU10TIX is the recommended identity verification provider.**

| Feature | Details |
|---------|---------|
| **Company** | Israeli company (Hod Hasharon), founded 2002 |
| **Pricing** | Starting from $1.00/verification; enterprise pricing based on volume |
| **Integration** | Single API; SDKs for iOS/Android/Web; integration in hours, not days |
| **Capabilities** | ID document verification, biometric face matching, liveness detection, address verification |
| **Israeli ID Support** | Native support for Teudat Zehut (Israeli ID), Israeli driver's license, Israeli passport |
| **Recent milestone** | Selected by Microsoft as premier IDV issuer on Microsoft Entra platform (Dec 2025) |
| **Compliance** | SOC 2, ISO 27001, GDPR compliant |

**Why AU10TIX for this platform:**
- Israeli company = understands Israeli ID documents natively
- Can verify the authenticity of uploaded Teudat Yosher (police clearance certificate)
- Biometric liveness detection prevents fake profile photos
- Single API reduces integration complexity
- Volume-based pricing favorable for marketplace scale

### 2.4 Alternative ID Verification Providers

| Provider | Israel Coverage | Pricing | Notes |
|----------|----------------|---------|-------|
| **Checkr** | International checks in 200+ countries including Israel | $29.99-$79.99/check (US pricing; Israel varies) | US-focused; limited Israeli document expertise |
| **Veremark** | Israel background screening available | Starting $15/mo platform fee + per-check costs | UK-based; covers employment, education, criminal |
| **KYC Israel** | Israel-specific | Custom pricing | Israeli firm; corporate KYC focus, not consumer/childcare |
| **Persona** | Available internationally | Custom pricing | Strong developer experience but less Israeli document expertise than AU10TIX |

### 2.5 Recommended Background Check Flow

```
Step 1: ID Verification (Automated - AU10TIX)
  - Nanny uploads Teudat Zehut photo
  - AU10TIX verifies document authenticity + biometric face match
  - Timeline: ~30 seconds
  - Cost: ~$1-2/verification

Step 2: Police Clearance (Manual - Nanny responsibility)
  - Nanny obtains Certificate of Good Conduct from police station
  - Uploads certificate to platform
  - AU10TIX verifies document authenticity
  - Timeline: 2-4 weeks (one-time)

Step 3: Reference Check (Semi-automated)
  - Nanny provides 2-3 references
  - Platform sends automated reference request forms
  - References complete online questionnaire
  - Timeline: 3-7 days

Step 4: Profile Activation
  - All checks passed -> profile goes live
  - Badge displayed: "Background Verified" with verification date
  - Annual renewal of police clearance required
```

**Total estimated cost per nanny verification: $3-10** (AU10TIX ID + document verification)

---

## 3. WhatsApp Business API

### 3.1 Current Pricing Model (Post-July 2025)

WhatsApp shifted from conversation-based to **per-message pricing** effective July 1, 2025.

| Message Category | Description | Approximate Cost (USD) | Free? |
|-----------------|-------------|----------------------|-------|
| **Marketing** | Promotions, offers, re-engagement | $0.025 - $0.1365/msg | No |
| **Utility** | Booking confirmations, updates, receipts | $0.004 - $0.0456/msg | Free within active service window |
| **Authentication** | OTP codes, login verification | $0.004 - $0.0456/msg | No |
| **Service** | Customer-initiated responses within 24 hours | Free | Yes |

**Key cost optimization:**
- Utility template messages sent **within an active customer service window are FREE**
- Volume-based discounts kick in automatically for utility and authentication messages as monthly volume increases
- Service messages (responding to user-initiated conversations) are always free

**Israel-specific rates:** Not publicly listed in search results. Must check [Meta's official pricing page](https://business.whatsapp.com/products/platform-pricing) and select Israel. Rates vary by country.

### 3.2 BSP Comparison (Who to Integrate Through)

| Provider | Monthly Fee | Per-Message Markup | Pros | Cons |
|----------|------------|-------------------|------|------|
| **WhatsApp Cloud API (Meta Direct)** | Free | Meta's rates only | No middleman; lowest cost; full control | Must handle infrastructure, template approvals, monitoring yourself |
| **360dialog** | $49/mo (basic), $99/mo (premium) | Meta's rates only (no markup) | Low cost BSP; developer-focused; Germany-based | Minimal tooling; bare API |
| **Twilio** | Pay-as-you-go | $0.005/msg platform fee + Meta rates | Multichannel (SMS + WhatsApp + Voice); global scale; excellent docs | Most expensive option; adds up |

**Recommendation for MVP: WhatsApp Cloud API (Meta Direct)**
- Zero monthly fee
- No per-message markup
- Suitable for a dev team that can handle the integration directly
- Migrate to a BSP only if operational overhead becomes too high

**Recommendation for Scale: 360dialog**
- $49/mo is negligible at scale
- No per-message markup (unlike Twilio's $0.005/msg)
- Better reliability and support than managing Cloud API yourself

### 3.3 Approval Process and Timeline

1. **Create a Meta Business Account** (if not already existing)
2. **Verify the business** with Meta (business documents, website, etc.)
3. **Apply for WhatsApp Business API access** through Meta Business Manager
4. **Submit message templates** for approval (must be pre-approved before sending)
5. **Timeline: 1-4 weeks** for full approval and go-live

**Hebrew template message requirements:**
- Templates must be submitted in Hebrew with English translation
- Templates must clearly state the business purpose
- No promotional content in utility templates
- Variable placeholders must be clearly marked: `{{1}}`, `{{2}}`, etc.
- Example booking confirmation: `שלום {{1}}, ההזמנה שלך עם {{2}} אושרה ל-{{3}} בשעה {{4}}. לביטול, השיבו "בטל".`

### 3.4 Platform Use Cases for WhatsApp

| Use Case | Message Type | Cost |
|----------|-------------|------|
| Booking confirmation | Utility | Free (within service window) or ~$0.01-0.04/msg |
| Nanny arrival reminder | Utility | Free (within service window) or ~$0.01-0.04/msg |
| New booking request notification | Utility | ~$0.01-0.04/msg |
| Pre-filled WhatsApp links (wa.me) | N/A | Free (just a link) |
| Marketing re-engagement | Marketing | ~$0.03-0.14/msg |
| OTP verification | Authentication | ~$0.01-0.04/msg |

**Pre-filled WhatsApp links:** Yes, `wa.me/<phone_number>?text=<pre-filled_message>` is fully supported and free. Useful for "Message this nanny" buttons that open WhatsApp with a pre-written intro.

### 3.5 Rate Limits

- New accounts: 250 business-initiated messages/24 hours
- After quality verification: 1,000/24 hours
- Scaled accounts: 10,000 -> 100,000 -> unlimited (based on quality score)
- No limit on replies to customer-initiated messages

---

## 4. Israeli Accessibility Law (IS 5568)

### 4.1 Legal Requirements

**IS 5568 is MANDATORY for both public and private sector digital services in Israel.** Took effect October 2017.

| Requirement | Standard |
|------------|----------|
| **Base compliance** | WCAG 2.0 Level AA (minimum) |
| **Aligned with** | WCAG 2.1 guidelines |
| **Applies to** | Websites AND mobile applications |
| **Sectors** | Both public and private sector |
| **Enforcement** | Civil lawsuits; class actions by disability organizations |

### 4.2 Key Requirements for the Nanny Platform

1. **Screen reader compatibility**: All interactive elements must have accessible labels (Hebrew)
2. **Color contrast**: Minimum 4.5:1 contrast ratio for normal text, 3:1 for large text
3. **Text resizing**: Content must be readable at 200% zoom without horizontal scrolling
4. **Keyboard/gesture navigation**: All functions must be operable without precise gestures
5. **Alternative text**: All images (profile photos, badges, icons) must have alt text in Hebrew
6. **Focus indicators**: Visible focus state on all interactive elements
7. **Error identification**: Form errors must be clearly identified and described in text
8. **Time limits**: If booking flows have timeouts, users must be able to extend them

### 4.3 Penalties for Non-Compliance

| Penalty Type | Amount/Impact |
|-------------|--------------|
| **Statutory damages** | Up to **50,000 NIS** (~$14,000 USD) per complaint |
| **Proof required** | Complainant does NOT need to prove actual harm -- only that the site/app is non-compliant |
| **Class actions** | Disability organizations can file class action lawsuits |
| **Reputational** | Court decisions are public; bad press in Israeli media |

**Important:** The 50,000 NIS statutory damages per complaint with no requirement to prove harm makes Israel one of the most aggressive accessibility enforcement regimes globally. A single advocacy group filing multiple complaints could be extremely costly.

### 4.4 RTL-First Design Requirements

- All layouts must default to RTL (right-to-left)
- Navigation flows from right to left
- Back buttons point right (not left)
- Progress indicators fill from right to left
- Lists and cards align to the right
- Numbers remain LTR within RTL text
- Mixed Hebrew/English content must handle bidirectional text correctly

### 4.5 Testing Tools for Hebrew Accessibility

| Tool | Platform | Notes |
|------|----------|-------|
| **React Native Accessibility Inspector** | iOS/Android | Built-in; test VoiceOver (iOS) and TalkBack (Android) |
| **Axe by Deque** | Web/Mobile | Automated accessibility testing; supports WCAG 2.1 |
| **accessiBe** | Web overlay | Israeli company; automated compliance layer (controversial -- not a substitute for proper implementation) |
| **EqualWeb** | Web overlay | Israeli company; automated compliance |
| **Manual testing with VoiceOver/TalkBack** | iOS/Android | Required -- no automated tool catches everything |

**Recommendation:** Build accessibility into the component library from day one. Retrofitting accessibility is 5-10x more expensive than building it in. Use `accessibilityLabel` on every React Native component.

---

## 5. Push Notification Infrastructure

### 5.1 Push Notification Providers

| Provider | Pricing | Pros | Cons |
|----------|---------|------|------|
| **Expo Notifications** | Free (bundled with Expo) | Zero-config with Expo; handles iOS + Android; token management built-in | Expo-dependent; less customizable |
| **Firebase Cloud Messaging (FCM)** | Free (unlimited) | Free forever; reliable; Google infrastructure | No SMS/email fallback; no analytics beyond basic delivery |
| **OneSignal** | Free: unlimited mobile push; Paid: $0.01-0.02/active user | Omnichannel (push + SMS + email + in-app); audience segmentation; A/B testing | Paid features add up; another vendor dependency |

**Recommendation for MVP: Expo Notifications**
- Since we're using Expo for React Native, Expo Push Notifications are included free
- Handles push token management, sending, and delivery tracking
- Supports iOS (APNs) and Android (FCM) through a single API
- Can migrate to OneSignal later if advanced segmentation is needed

### 5.2 SMS Fallback Providers in Israel

| Provider | Price per SMS (Israel) | Notes |
|----------|----------------------|-------|
| **Twilio** | $0.167 - $0.258/msg | Global leader; reliable; well-documented API |
| **Vonage (Nexmo)** | ~$0.15-0.20/msg | Good Israel coverage; competitive pricing |
| **019 SMS (Cellact)** | ~0.10-0.15 NIS/msg (~$0.03-0.04) | Local Israeli provider; cheapest; Hebrew-native |
| **Infobip** | ~$0.15-0.20/msg | Enterprise-grade; good Israel delivery rates |

**Key insight:** Israeli local SMS providers (019/Cellact) are **4-5x cheaper** than international providers (Twilio, Vonage) for domestic Israeli SMS. For a platform operating exclusively in Israel, a local provider makes more financial sense.

**Recommendation:**
- **Push notifications (primary)**: Expo Notifications (free)
- **SMS fallback**: Local Israeli provider (019/Cellact) for cost efficiency
- **WhatsApp (secondary)**: WhatsApp Business API for booking confirmations (cheaper than SMS)

### 5.3 Delivery Rates in Israel

| Channel | Delivery Rate | Engagement Rate | Cost |
|---------|--------------|----------------|------|
| **Push notification** | 85-95% (when app installed) | 5-15% open rate | Free |
| **WhatsApp** | 95-99% | 70-80% open rate | $0.01-0.04/msg |
| **SMS** | 95-99% | 30-40% open rate | $0.03-0.25/msg |

**WhatsApp is the optimal channel for Israel** -- near-universal adoption (95%+ of Israeli adults use WhatsApp), highest engagement rates, and cheaper than SMS for transactional messages.

---

## 6. Geolocation and Mapping

### 6.1 Mapping Provider Comparison

| Provider | Israel Coverage | Hebrew Support | Pricing | Notes |
|----------|----------------|---------------|---------|-------|
| **Google Maps** | Excellent | Full Hebrew geocoding, street names, POIs | $200/mo free credit; then $5-7/1K requests | Industry standard; best accuracy in Israel |
| **Waze** | Excellent (Israeli-made) | Native Hebrew | No public developer API | Community-driven data; owned by Google; no API for third-party apps |
| **OpenStreetMap** | Good | Hebrew labels available | Free (open data) | Requires self-hosting tile server; less accurate than Google in Israel |
| **Mapbox** | Good | Hebrew support | $0-5/1K requests; generous free tier | Good alternative to Google; cheaper at scale |

**Recommendation: Google Maps Platform**

- Best geocoding accuracy for Israeli addresses (handles Hebrew street names, apartment numbers, and building naming conventions)
- Waze's community data feeds into Google Maps, so Google Maps inherits Waze's superior Israeli mapping data
- $200/mo free credit covers ~28,000-40,000 API calls/month (more than enough for MVP)
- Distance Matrix API for calculating nanny-to-family travel times with Israeli traffic data

### 6.2 Israeli Address Format Handling

Israeli addresses have unique challenges:
- Street names are in Hebrew (רחוב הרצל) but may have English transliterations
- Building numbers can include letter suffixes (12א, 12ב)
- Many residential areas use apartment-in-building format: דירה 5, קומה 3
- Kibbutzim and moshavim may not have standard street addresses
- New neighborhoods may not be in mapping databases yet

**Google Maps Geocoding handles all of these** with native Hebrew support. Input `הרצל 12, תל אביב` and get accurate lat/lng coordinates.

### 6.3 Distance Calculation for Israeli Urban Areas

- **Google Maps Distance Matrix API**: Accounts for real roads, one-way streets, and Israeli traffic patterns
- **PostGIS ST_Distance**: Calculates straight-line (haversine) distance -- suitable for initial radius filtering (much cheaper than API calls)
- **Recommended approach**:
  1. Use PostGIS `ST_DWithin` for initial radius filter (e.g., all nannies within 5km) -- free, database-level
  2. Use Google Maps Distance Matrix only for the final shortlist (e.g., top 5 nannies) to get actual travel times -- costs $5/1K requests

This hybrid approach reduces Google Maps API costs by 90%+ compared to querying the API for every search.

### 6.4 Geocoding Hebrew Addresses

```
// Google Maps Geocoding API example
GET https://maps.googleapis.com/maps/api/geocode/json
  ?address=הרצל+12,+תל+אביב
  &language=he
  &region=il
  &key=YOUR_API_KEY

// Returns accurate lat/lng for Hebrew address input
```

- Set `language=he` and `region=il` for optimal Hebrew geocoding
- Google Maps handles mixed Hebrew/English input (common in Israel)
- Reverse geocoding (lat/lng -> address) also returns Hebrew addresses

---

## 7. Data Storage and Privacy

### 7.1 Data Residency Requirements

**Israel does NOT mandate that personal data must be stored within Israel.**

Key rules:
- Personal data may be transferred out of Israel only to countries that ensure a level of protection **not lower** than Israeli law
- Israel has an **EU adequacy decision** -- data can flow freely between Israel and the EU
- Countries with adequate protection include: EU/EEA, UK, US (with appropriate safeguards), Canada, Australia, Japan, and others recognized by the PPA
- **Bottom line**: Hosting on AWS il-central-1 (Israel) is optimal for latency but not legally required. EU hosting (Frankfurt, Ireland) is also compliant.

**Recommendation:** Host in AWS il-central-1 for lowest latency to Israeli users AND to simplify compliance messaging ("Your data stays in Israel").

### 7.2 Privacy Protection Authority (PPA) Registration

Under Amendment 13 (effective August 14, 2025), database registration requirements have been **significantly narrowed**:

| Scenario | Registration Required? |
|----------|----------------------|
| Standard app database | **No** (registration requirement removed for most cases) |
| Database with sensitive data on 100K+ individuals | **Notification** to PPA required (not full registration) |
| Public bodies | **Yes**, full registration |
| Direct marketing databases (10K+ individuals) | **Yes**, full registration |

**For the nanny platform:**
- At MVP scale (<100K users): No registration required
- At scale (100K+ users with sensitive data like background checks): Must notify PPA of database existence, DPO identity, and contact information
- If the platform does direct marketing: Registration required once the database exceeds 10K individuals

### 7.3 Amendment 13 Key Compliance Requirements

Amendment 13 is Israel's most significant privacy law reform, effective August 2025. It closely aligns with GDPR.

| Requirement | Details |
|------------|---------|
| **Consent** | Must be explicit, documented, and granular. Blanket consent no longer acceptable. |
| **Privacy notices** | Must explain: what is collected, why, risks, who it's shared with |
| **Data Protection Officer** | Required if processing sensitive data at scale or engaging in systematic monitoring |
| **Data security** | Encryption, access controls, regular security audits required |
| **Breach notification** | Must notify PPA and affected individuals of data breaches |
| **Data subject rights** | Right to access, correction, deletion, data portability |
| **Data minimization** | Collect only what is necessary for the stated purpose |

**Enforcement powers:**
- PPA can conduct administrative inquiries and appoint inspectors
- Binding orders and database suspension
- Publish violators' names for up to 4 years
- Administrative fines reaching **millions of shekels** (500,000+ USD / 460,000+ EUR)
- Criminal prosecution possible

### 7.4 Data Retention Policies

No specific retention period mandated by Israeli law, but Amendment 13 requires:
- Data must be deleted when no longer necessary for its original purpose
- Users can request deletion (right to erasure)
- Financial records: Keep for 7 years (Israeli tax law -- Mas Hachnasa)
- Background check documents: Keep for duration of nanny's active status + 1 year after deactivation
- Chat/message history: Consider 1-year retention with user ability to delete

### 7.5 Recommended Privacy Architecture

```
Data Classification:
  - PUBLIC: Nanny profiles (name, photo, general area, ratings)
  - SENSITIVE: Background check documents, ID verification results
  - CRITICAL: Payment data (handled by payment processor, NOT stored)
  - PERSONAL: Home addresses, phone numbers, children's information

Security Measures:
  - Encryption at rest: AES-256 (AWS RDS default)
  - Encryption in transit: TLS 1.3
  - Row-level security: Supabase RLS policies
  - Access logging: All access to sensitive data logged
  - Data masking: Phone numbers partially masked in UI
  - Children's data: Extra consent required; never shared publicly
```

---

## 8. Cost Summary and Stack Comparison

### 8.1 Monthly Infrastructure Cost Estimates

| Component | MVP (0-1K users) | Growth (1K-10K users) | Scale (10K-50K users) |
|-----------|------------------|----------------------|---------------------|
| AWS Hosting (EC2, RDS, S3) | $62/mo | $200-400/mo | $800-1,500/mo |
| Supabase | Free | $25/mo (Pro) | $599/mo (Team) |
| Google Maps | Free ($200 credit) | $50-100/mo | $200-500/mo |
| Sentry | Free | $26/mo (Team) | $80/mo (Business) |
| WhatsApp API | Free (service msgs) | $50-100/mo | $200-500/mo |
| SMS (backup) | $10/mo | $30-50/mo | $100-200/mo |
| AU10TIX (verification) | $50/mo (~50 checks) | $200/mo | $500-1,000/mo |
| Algolia (if needed) | Free | Free-$50/mo | $200-500/mo |
| Expo/Push | Free | Free | Free |
| **Total** | **~$125/mo** | **~$600-1,000/mo** | **~$2,500-4,800/mo** |

### 8.2 Key Technical Risks

| Risk | Severity | Mitigation |
|------|----------|-----------|
| No police check API (manual process) | HIGH | Build smooth upload flow; partner with verification service; clear onboarding messaging |
| Sex offender registry not public | HIGH | Rely on police clearance certificate which covers sex offenses; annual renewal |
| WhatsApp API rate limits (250/day initially) | MEDIUM | Request quality tier upgrade early; use push notifications as primary channel |
| Amendment 13 compliance complexity | MEDIUM | Appoint DPO early; build privacy-by-design; use Supabase RLS |
| IS 5568 accessibility lawsuits | MEDIUM | Build accessibility from day 1; budget for accessibility audit before launch |
| Hebrew full-text search accuracy | LOW | PostgreSQL handles Hebrew adequately; upgrade to Algolia if needed |

---

## 9. Key Decision Matrix

| Decision | Recommendation | Confidence | Alternatives |
|----------|---------------|------------|-------------|
| Mobile framework | React Native + Expo | HIGH | Flutter (if team prefers Dart) |
| Backend | Node.js + NestJS | HIGH | Go (if performance-critical) |
| Database | PostgreSQL + PostGIS | VERY HIGH | None -- PostgreSQL is clearly superior for this use case |
| Real-time | Supabase Realtime | HIGH | Firebase (if team has experience) |
| Hosting region | AWS il-central-1 | HIGH | GCP me-west1 (equally valid) |
| ID verification | AU10TIX | HIGH | Persona (if US expansion planned) |
| Background checks | Manual upload + AU10TIX doc verify | VERY HIGH | No automated alternative exists in Israel |
| Messaging | WhatsApp Cloud API (MVP) | HIGH | 360dialog (at scale) |
| Push notifications | Expo Notifications | HIGH | OneSignal (if advanced segmentation needed) |
| Maps | Google Maps Platform | VERY HIGH | Mapbox (cheaper at scale) |
| Search | PostgreSQL FTS (MVP) | HIGH | Algolia (at scale) |
| Privacy compliance | Amendment 13 / GDPR-aligned | MANDATORY | No alternative -- legal requirement |
| Accessibility | IS 5568 / WCAG 2.1 AA | MANDATORY | No alternative -- legal requirement |
