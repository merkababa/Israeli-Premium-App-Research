# Identity Document Verification (IDV) Services — Comprehensive Research

**Date:** March 7, 2026
**Context:** Emuni nanny marketplace — voluntary Teudat Zehut verification for nanny "verified" badge
**Volume:** 50-500 checks/month | **Stack:** React Native (Expo SDK 55), NestJS backend

---

## 1. WHAT ARE YOU ACTUALLY PAYING FOR?

An IDV check is a multi-step pipeline. When you pay $0.80-$2.00 per verification, you're buying:

### Step 1: Document Capture
- User photographs their ID (front + back) using their phone camera
- SDK provides assisted capture: auto-framing, blur detection, glare detection, resolution checks
- Some SDKs use barcode scanning (PDF417 on back of many IDs) for faster data extraction
- The SDK rejects blurry/dark/cropped images before uploading — reducing failed checks you'd pay for

### Step 2: Data Extraction (OCR + MRZ)
- Optical Character Recognition extracts printed text: name, date of birth, ID number, nationality, expiry date
- Machine Readable Zone (MRZ) parsing for passports and some ID cards
- Barcode/QR code data extraction where available
- Some providers extract 5-15 data fields depending on plan tier

### Step 3: Document Authentication (Fake ID Detection)
- Font analysis: comparing typefaces against known government templates
- Layout verification: spacing, alignment, positioning of text and photo elements
- Security feature detection: holograms, microprint patterns, UV-reactive elements (limited on photos)
- Tamper detection: looking for pixel-level manipulation, Photoshop artifacts, spliced photos
- Template matching: comparing against a database of 12,000-14,000+ known document specimens
- Digital forgery detection: metadata analysis, compression artifact inconsistencies

### Step 4: Liveness Detection (Anti-Spoofing)
- **Passive liveness:** AI analyzes a single selfie for signs of life — skin texture, blood flow, natural lighting, 3D depth cues. No user action required.
- **Active liveness:** User must perform actions — blink, turn head, smile, read a number. More secure but higher friction.
- Both detect: printed photos held to camera, screen replays (photo of a photo on another phone), 3D masks, deepfake video injections, virtual cameras/emulators
- US-NIST / iBeta Level 2 certification is the gold standard (99.9%+ spoof rejection)

### Step 5: Face Matching (1:1 Biometric Comparison)
- Compares the live selfie against the photo extracted from the ID document
- Maps 68+ facial landmarks (eye spacing, nose bridge, jawline, etc.)
- Outputs a similarity score; provider sets threshold for pass/fail
- This is the critical link: proves the person holding the phone is the person on the document

### Step 6: Fraud Detection (Advanced — Plus/Premium tiers)
- **Deepfake detection:** AI-specific analysis for synthetic faces, face swaps, GAN-generated images
- **CrossLinks / velocity checks:** same device, IP, or face used across multiple accounts
- **Device intelligence:** emulator detection, rooted device detection, VPN/proxy flags
- **Behavioral analysis:** time to complete, interaction patterns

### Step 7: AML/Watchlist Screening (Usually a Paid Add-On)
- Checks extracted name + DOB against sanctions lists (OFAC, EU, UN)
- Politically Exposed Persons (PEP) screening
- Adverse media screening (negative news)
- Typically 1,200+ global watchlists
- **Not needed for Emuni** — nannies are not financial counterparties

### What Separates Basic from Premium Tiers?

| Feature | Basic/Essential | Plus/Premium |
|---------|----------------|--------------|
| Document OCR + authentication | Yes | Yes |
| Passive liveness | Yes | Yes |
| Face matching | Yes | Yes |
| Deepfake detection | Basic/none | Advanced |
| CrossLinks/velocity checks | No | Yes |
| Human review fallback | No | Yes (hybrid AI+human) |
| Session video recording | No | Yes |
| Risk scoring/labeling | No | Yes |
| AML screening | Add-on ($) | Add-on or included |
| Data retention | 3 months | 6-12 months |

**For Emuni's use case (voluntary nanny badge, not regulated KYC), the Essential/Basic tier is sufficient.** You need: document capture + OCR + liveness + face match. You do NOT need AML screening, CrossLinks, or human review.

---

## 2. ALL PROVIDERS — COMPREHENSIVE ANALYSIS

### 2.1 Veriff (Estonia)

**HQ:** Tallinn, Estonia | **Founded:** 2015 | **Employees:** ~600

**Pricing (Self-Serve, March 2026):**
| Plan | Per Check | Monthly Min | What You Get |
|------|-----------|-------------|--------------|
| Essential | $0.80 | $49/mo | AI-only verification, 10 data fields, iBeta liveness, 3-mo retention |
| Plus | $1.39 | $99/mo | AI + human fallback, video recording, FaceBlock, CrossLinks, 6-mo retention |
| Premium | $1.89 | $209/mo | AI + human, custom branding, CSV export, API deletion, 6-mo retention |

**Add-ons:** PEP & Sanctions +$0.64/check | Ongoing monitoring +$0.09/check | Extended retention (2yr) +$0.30/check

**Free trial:** 30 days, 100 free verifications (50 per plan), unlimited test verifications

**Israel Document Support:**
- Passport: YES
- **ID Card (Teudat Zehut): NO** (confirmed via veriff.com/supported-countries — March 2026)
- Driver's License: YES
- Residence Permit: NO

**React Native SDK:** Official SDK v11.1.0 (published Feb 2026). **Requires ejecting from Expo managed workflow.** No config plugin. Must use `npx expo prebuild` or bare workflow. iOS 15.0+, Android API 26+.

**Data Breach:** November 2025 — unauthorized access to customer ID images via Veriff's systems. 8,583 US users affected (Total Wireless customers). Images of government IDs and personal info exposed.

**Verdict for Emuni:** DISQUALIFIED. Does not support Teudat Zehut. Only Israeli passport and driver's license. Since many nannies may not have a passport (or may not want to use it for a babysitting app), this is a dealbreaker.

---

### 2.2 iDenfy (Lithuania)

**HQ:** Kaunas, Lithuania | **Founded:** 2017

**Pricing:**
- Pay-as-you-go: ~$0.55-$1.35/verification (volume-dependent)
- Only charged for successful verifications
- 14-day free trial with 10 free checks
- No published monthly minimum

**Israel Document Support:**
- Israel listed as supported country in their documentation
- Supports 3,000+ documents from 190+ countries
- Specific Teudat Zehut support: **Likely but unconfirmed** — Israel (IL) appears in their country dropdown but specific document list requires interactive lookup

**React Native SDK:** Official SDK `@idenfy/react-native-sdk` on npm (last updated May 2025). Native module — requires development build with Expo (no config plugin found).

**Data Breach:** No known incidents.

**Verdict for Emuni:** POSSIBLE. Decent pricing at low volumes. Need to confirm Teudat Zehut support directly. No Expo config plugin.

---

### 2.3 Sumsub (UK/Global)

**HQ:** London, UK (offices in Berlin, Tel Aviv, Miami, Dubai, Singapore) | **Founded:** 2015

**Pricing:**
| Plan | Per Check | Monthly Min | What You Get |
|------|-----------|-------------|--------------|
| Basic | $1.35 | $149/mo | ID verification, liveness, face match, email/phone verification |
| Compliance | $1.85 | $299/mo | + AML screening, ongoing monitoring, proof of address |
| Enterprise | Custom | Custom | Full suite including business verification |

**Free trial:** 14 days, 50 free checks

**Israel Document Support:**
- 14,000+ document types from 220+ countries
- Israel ID card: **Likely supported** — Sumsub claims broadest document coverage in industry
- Has a Tel Aviv office, suggesting strong Israel market awareness
- Specific confirmation requires checking their supported documents page or PDF

**React Native SDK:** Official `@sumsub/react-native-mobilesdk-module` v1.40.2. Requires native configuration (Kotlin 1.9.25, iOS 13+). Works with Expo development builds but no config plugin.

**Data Breach:** No major known incidents.

**Verdict for Emuni:** TOO EXPENSIVE. $149/month minimum is way too high for 50-500 checks/month. At 50 checks, effective cost = $2.98/check. Only makes sense at 110+ checks/month.

---

### 2.4 Entrust IDV (formerly Onfido) (UK)

**HQ:** London, UK | **Acquired by Entrust for $650M (April 2024)**

**Pricing:**
- Quote-based only — no self-serve pricing
- Historically expensive; optimized for 100K+ annual checks
- One reviewer mentioned $10,000 commitments
- Not startup-friendly

**Israel Document Support:** 2,500+ document types from 195+ countries. Israeli ID card likely supported but unconfirmed.

**React Native SDK:** Official `@onfido/react-native-sdk` exists on npm and GitHub.

**Data Breach:** No major known incidents for Onfido specifically.

**Verdict for Emuni:** DISQUALIFIED. No self-serve. Quote-based pricing designed for enterprise. Not viable for bootstrapped startup.

---

### 2.5 AU10TIX (Israel/Netherlands)

**HQ:** Amsterdam, Netherlands (main operations in Hod HaSharon, Israel) | **Founded:** 2002

**Pricing:**
- Quote-based only — no self-serve, no public pricing
- Annual platform minimums + prepaid bundles
- Requires sales call
- Designed for enterprise (Uber, TikTok, X are customers)

**Israel Document Support:** Being an Israeli company, Teudat Zehut is almost certainly supported, but no public confirmation found.

**React Native SDK:** No dedicated RN SDK. Offers iOS, Android, and Web SDKs. RN integration requires native bridging.

**Data Breach:** MAJOR INCIDENT (June 2024). Admin credentials exposed online for 1+ year via infostealer malware. Researcher accessed logging platform with links to customer ID document images, names, DOB, nationality, ID numbers. Company claims "no evidence of data exposure" and said it was a legacy log system being phased out. Selected as one of the "Worst Data Breaches of 2024" by the EFF.

**Verdict for Emuni:** DISQUALIFIED. No self-serve, no public pricing, serious data breach history, no RN SDK. Enterprise-only.

---

### 2.6 Jumio (USA)

**HQ:** Palo Alto, California, USA | **Founded:** 2010

**Pricing:**
- Custom/quote-based only
- No public per-check pricing
- Described as "cost-prohibitive for startups with limited budgets"
- 1 billion+ transactions processed

**Israel Document Support:** 5,000+ ID types from 200+ countries. Israel likely supported but specific document list requires CSV download from their portal.

**React Native SDK:** Official `mobile-react` plugin on GitHub, compatible with Jumio SDK v4.15.0.

**Data Breach:** No major known incidents.

**Verdict for Emuni:** DISQUALIFIED. No self-serve, enterprise pricing, not startup-friendly.

---

### 2.7 Regula (Latvia)

**HQ:** Daugavpils, Latvia (US office in Reston, VA) | **Founded:** 2006

**Pricing:**
- License-based model (annual fixed cost)
- Not per-check pricing for most deployments
- Pricing depends on modules (Basic, VizOCR, AAC) and deployment size
- No public self-serve pricing
- On-device processing (no cloud required)

**Israel Document Support:** 15,000+ document templates from 254 countries. Hebrew script explicitly supported. Israel identity card highly likely supported.

**React Native SDK:** Official `react-native-document-reader` on GitHub. All processing done on-device (offline capable). This is unique — no data leaves the device.

**Data Breach:** No known incidents.

**Verdict for Emuni:** INTERESTING BUT COMPLEX. License-based model doesn't fit low-volume per-check use case. On-device processing is a privacy advantage but adds complexity. No self-serve.

---

### 2.8 Persona (USA)

**HQ:** San Francisco, California, USA | **Founded:** 2018

**Pricing:**
| Plan | Cost | Details |
|------|------|---------|
| Startup Program | FREE | 500 free Gov ID verifications/month for 12 months |
| After startup quota | $1.00/check | Per additional verification |
| Essential Plan | $250/mo | After startup program ends |

**Startup Program Eligibility:** <$5M funding, <50 employees, or independently owned small business. Rolling applications. Credit card required.

**Israel Document Support:** Broad coverage but specific Israeli document support unconfirmed in search results.

**React Native SDK:** Official SDK with `PersonaInquiryView` component. Integration guide available.

**DATA BREACH / SECURITY INCIDENT (February 2026):**
- Researcher found Persona's entire government dashboard codebase (53MB, 2,456 files) exposed on a public endpoint at withpersona-gov.com
- Revealed that Persona performs 269 distinct verification checks including facial recognition against watchlists, PEP screening, and surveillance capabilities
- IP addresses, browser fingerprints, device fingerprints, government ID numbers, phone numbers, names, faces, and selfie backgrounds analyzed and retained for up to THREE YEARS
- Discord cut ties with Persona after this exposure
- Persona characterized as conducting government surveillance, not just identity verification

**Verdict for Emuni:** HIGH RISK. The February 2026 exposure reveals a surveillance-oriented architecture that is deeply problematic for a consumer-trust app. 3-year data retention of biometric data. Discord dropped them. The startup program pricing is attractive (500 free/month) but the trust and privacy implications make this a liability for a nanny platform where parent trust is everything.

---

### 2.9 Shufti Pro (UK/Pakistan)

**HQ:** London, UK (founded by Pakistani entrepreneurs) | **Founded:** 2017

**Pricing:**
- **Pay-as-you-go: Starting at $0.20/verification**
- No minimum commitment
- 7-day free trial
- Monthly commitment plans also available

**Included in base price:**
- Document verification with AI authenticity checks
- Biometric liveness detection (100+ facial vectors)
- Face match (selfie vs document photo)
- Deepfake detection
- AML/sanctions screening against 1,700+ global watchlists

**Israel Document Support: CONFIRMED.**
- Teudat Zehut (Identity Card): YES
- Driver's License: YES
- Passport: YES
- Residence Permit: YES
- Voter ID: YES
- Immigration Permit: YES
- Consular ID Card: YES
- Health Insurance Card (Kupat Holim Card): YES

**React Native SDK:** Official SDK on GitHub (`shuftipro/React-Native-SDK`). Cross-platform iOS + Android.

**Certifications:** GDPR, ISO 27001:2013, CCPA, QG-GDPR certified.

**Data Breach:** No known incidents. Proactive security posture.

**Concerns:**
- Some users report occasional verification issues and deepfake detection gaps
- $0.20/check seems unusually low — need to verify what's actually included at that price point vs. upsells
- G2 rating: 4.3/5 (12 reviews) — small sample size
- Trustpilot: 4.7/5 (2,700+ reviews)

**Verdict for Emuni:** STRONG CONTENDER. Confirmed Teudat Zehut support, extremely low per-check price, no minimum commitment, RN SDK available. Main risk: the $0.20 price point may be a loss leader with limited features, or quality may be lower than competitors.

---

### 2.10 Didit (Spain)

**HQ:** Barcelona, Spain | **Founded:** 2021

**Pricing:**
| Feature | Free (500/mo) | Paid (per check) |
|---------|--------------|-------------------|
| ID Verification | FREE | $0.15 |
| Face Match 1:1 | FREE | $0.05 |
| Passive Liveness | FREE | $0.10 |
| IP Analysis | FREE | $0.03 |
| Active Liveness | N/A | $0.15 |
| NFC Verification | N/A | $0.15 |
| AML Screening | N/A | $0.20 |
| Age Estimation | N/A | $0.10 |
| Proof of Address | N/A | $0.20 |

**Key pricing details:**
- **500 free checks/month per feature** for core KYC (ID + liveness + face match + IP)
- Pay only for successful completed checks
- No minimums, no monthly fees, no setup fees
- Credits never expire
- A full verification (ID + passive liveness + face match) = FREE for first 500/month, then $0.30/check ($0.15 + $0.10 + $0.05)

**Israel Document Support:** 14,000+ document types from 220+ countries, Hebrew script supported. Israel likely supported but specific Teudat Zehut confirmation requires checking their interactive supported documents page.

**React Native SDK:** Official `@didit-protocol/sdk-react-native` on npm and GitHub. **HAS EXPO CONFIG PLUGIN** — add to `app.json` plugins array. Supports Expo development builds. Auto-configures Android Maven repository and iOS podspec. Requires `npx expo prebuild` (not Expo Go).

**SDK Features:** ID Verification (OCR, MRZ, barcodes), Passive & Active Liveness, 1:1 Face Match, Face Search (1:N duplicate detection).

**Data Breach:** No known incidents.

**Verdict for Emuni:** TOP CONTENDER. 500 free checks/month covers Emuni's entire early-stage volume. Expo config plugin is a massive DX advantage for solo developer. Per-check pricing after free tier is the cheapest in market. Main risk: relatively new company (2021), less proven at scale. Need to confirm Teudat Zehut support.

---

### 2.11 IDWise (UK)

**HQ:** London, UK | **Founded:** 2020

**Pricing:**
- **$1.00/verification — all-in, flat rate**
- Includes: document verification (13,000+ types), liveness detection (NIST-certified, 99.99% accuracy), face matching, unlimited retries, data extraction, dashboard, SDKs, APIs, lifetime support
- **AML add-on:** $0.25/check
- **30-day free trial**, no credit card required
- No published monthly minimum

**Israel Document Support:** 13,000+ document types from 200+ countries. Specific Teudat Zehut confirmation not found, but broad coverage suggests likely support.

**React Native SDK:** Official `idwise-react-native-sdk` on npm. Latest version v6.2.7 (released March 3, 2026 — very active development). Bridge implementation wrapping native iOS/Android SDKs.

**Data Breach:** No known incidents.

**Verdict for Emuni:** GOOD OPTION. Simple, transparent pricing. Active SDK development. $1/check is mid-range but includes everything. Need to confirm Teudat Zehut support.

---

### 2.12 ID Analyzer (Taiwan)

**HQ:** Taichung, Taiwan | **Founded:** ~2015-2018

**Pricing:**
| Plan | Monthly | API Credits/mo | Per Check |
|------|---------|---------------|-----------|
| Free | $0 | 100 | $0.00 |
| Entry | $89 | 1,000 | ~$0.089 |
| Advanced | $350 | 5,000 | ~$0.07 |
| Business | $880 | 15,000 | ~$0.059 |

Yearly plans save 25%. All plans include AML/PEP checks, biometric verification, and fake ID detection.

**Israel Document Support: CONFIRMED.**
- Identity Card (2013 biometric version): YES
- Passport: YES
- Driver's License (2018): YES

**React Native SDK:** No dedicated RN SDK. JavaScript/Node.js library (`idanalyzer` on npm) for server-side API calls. Document scanning would need to be handled client-side separately.

**Data Breach:** No known incidents.

**Verdict for Emuni:** BUDGET OPTION. Confirmed Teudat Zehut support. Cheapest per-check pricing at scale. But no mobile SDK means more integration work — you'd need to build your own document capture UI and call the API server-side. Better suited for web-based verification flows. Free tier (100/month) could work for MVP.

---

### 2.13 ComplyCube (UK)

**HQ:** London, UK | **Founded:** 2020

**Pricing:**
- Per-check: ~$0.80-$1.35 (volume-dependent, lower at higher volumes)
- Startup Program: up to $50,000 in benefits (stage-dependent)
- No setup fees, no hidden costs
- Monthly commitment model with allocated verification credits

**Israel Document Support:** 13,000+ document types from 237 countries. Specific Teudat Zehut support not confirmed but very likely given coverage breadth.

**React Native SDK:** Official `@complycube/react-native` SDK on npm and GitHub. Integration guide available.

**Data Breach:** No known incidents.

**Verdict for Emuni:** POSSIBLE but pricing is mid-range. Startup program could offset costs. Need to confirm Teudat Zehut and get actual pricing quote.

---

### 2.14 Ondato (Lithuania)

**HQ:** Vilnius, Lithuania | **Founded:** 2018

**Pricing:**
- Per-check: EUR 0.50-1.40 (volume-dependent)
- At low volumes (50-500/month): likely EUR 1.00-1.40/check
- Noted as "a bit high for small businesses"

**Israel Document Support:** 190+ countries. Specific Teudat Zehut support unconfirmed.

**React Native SDK:** Official SDK on GitHub (`ondato/ondato-sdk-react-native`).

**Data Breach:** No known incidents.

**Verdict for Emuni:** TOO EXPENSIVE at low volumes. EUR 1.40/check at startup volume. Not competitive.

---

### 2.15 HyperVerge (India/USA)

**HQ:** Palo Alto, USA / Bengaluru, India | **Founded:** 2014

**Pricing:** Custom/volume-based. No public per-check pricing. Contact required.

**Israel Document Support:** 200+ countries. Specific support unconfirmed.

**React Native SDK:** `react-native-hyperkyc-sdk` on npm.

**Data Breach:** No known incidents.

**Verdict for Emuni:** UNCLEAR PRICING. Not startup-friendly without transparent pricing.

---

### 2.16 Microblink (Croatia/USA)

**HQ:** New York, USA / Zagreb, Croatia | **Founded:** 2013

**Pricing:** Custom/license-based. No public per-check pricing. Free developer trial available.

**Israel Document Support: CONFIRMED.** Israel ID card (front + back) listed in supported documents.

**React Native SDK:** Official `blinkid-react-native` v7.2.0 (updated Feb 2026). Active development. Primarily a document scanning/OCR tool — liveness and face matching require partner integration (e.g., iProov).

**Data Breach:** No known incidents.

**Verdict for Emuni:** SPECIALIZED. Microblink is primarily a document scanning engine, not a full IDV pipeline. You'd need to add liveness and face matching separately. Adds complexity.

---

### 2.17 Innovatrics (Slovakia)

**HQ:** Bratislava, Slovakia | **Founded:** 2004

**Pricing:** Pay-per-transaction, no entry fees, no long-term contracts. Specific pricing not public.

**React Native SDK:** DOT SDK React Native samples on GitHub.

**Data Breach:** No known incidents.

**Verdict for Emuni:** POSSIBLE but pricing opaque. Need to contact for quote.

---

### 2.18 Vouched (USA)

**HQ:** Seattle, Washington, USA | **Founded:** 2018

**Pricing:** $2/verification flat fee option mentioned. Free developer onboarding. Custom pricing otherwise.

**React Native SDK:** Not confirmed in research.

**Data Breach:** No known incidents.

**Verdict for Emuni:** $2/check is expensive. Not competitive.

---

### 2.19 Passbase / Parallel Markets

**Status:** Passbase was acquired by Parallel Markets in March 2023. No longer operates as an independent IDV service. Not viable.

---

## 3. TEUDAT ZEHUT SUPPORT SUMMARY

| Provider | Teudat Zehut | Passport | Driver's License | Source |
|----------|-------------|----------|-----------------|--------|
| **Shufti Pro** | CONFIRMED | CONFIRMED | CONFIRMED | shuftipro.com/supported-documents |
| **ID Analyzer** | CONFIRMED | CONFIRMED | CONFIRMED | idanalyzer.com/solutions/supported-documents/il |
| **Microblink** | CONFIRMED | Likely | Likely | microblink.com blog (document list) |
| Veriff | **NO** | YES | YES | veriff.com/supported-countries (fetched March 2026) |
| iDenfy | Likely (IL in country list) | Likely | Likely | documentation.idenfy.com — needs interactive check |
| Sumsub | Likely (14K+ docs, TLV office) | Likely | Likely | sumsub.com — needs PDF download |
| Didit | Likely (14K+ docs, Hebrew support) | Likely | Likely | didit.me — needs interactive check |
| IDWise | Likely (13K+ docs) | Likely | Likely | idwise.com — needs confirmation |
| ComplyCube | Likely (13K+ docs, 237 countries) | Likely | Likely | complycube.com — needs confirmation |
| Regula | Likely (15K+ docs, Hebrew support) | Likely | Likely | regulaforensics.com — needs confirmation |
| AU10TIX | Very likely (Israeli company) | Very likely | Very likely | No self-serve — cannot verify |
| Entrust/Onfido | Likely | Likely | Likely | No self-serve — cannot verify |
| Jumio | Likely (5K+ docs) | Likely | Likely | No self-serve — cannot verify |
| Persona | Likely | Likely | Likely | No public doc list found |

**CRITICAL FINDING:** Veriff — the provider previously recommended in the Technical PRD — does NOT support Israeli identity cards. It only supports Israeli passports and driver's licenses. This is a showstopper for Emuni's use case where nannies verify their identity with their Teudat Zehut.

---

## 4. REACT NATIVE / EXPO COMPATIBILITY

| Provider | Official RN SDK | Expo Config Plugin | Expo Compatibility | Notes |
|----------|----------------|-------------------|-------------------|-------|
| **Didit** | YES (`@didit-protocol/sdk-react-native`) | **YES** | Dev build (not Expo Go) | Best Expo integration. Auto-configures Android + iOS. |
| Veriff | YES (`@veriff/react-native-sdk` v11.1.0) | NO | Must eject/prebuild | Veriff docs explicitly say "eject from Expo" |
| iDenfy | YES (`@idenfy/react-native-sdk`) | NO | Dev build likely works | Last updated May 2025 |
| Sumsub | YES (`@sumsub/react-native-mobilesdk-module` v1.40.2) | NO | Dev build likely works | Requires Kotlin 1.9.25, iOS 13+ |
| IDWise | YES (`idwise-react-native-sdk` v6.2.7) | NO | Dev build likely works | Very active — updated March 3, 2026 |
| Shufti Pro | YES (GitHub: `shuftipro/React-Native-SDK`) | NO | Dev build likely works | Cross-platform iOS + Android |
| ComplyCube | YES (`@complycube/react-native`) | NO | Dev build likely works | Official SDK on npm |
| Ondato | YES (GitHub: `ondato/ondato-sdk-react-native`) | NO | Dev build likely works | |
| Persona | YES (official React Native SDK) | NO | Dev build likely works | |
| Jumio | YES (`mobile-react` on GitHub) | NO | Dev build likely works | |
| Regula | YES (`react-native-document-reader`) | NO | Dev build likely works | On-device processing (offline) |
| Microblink | YES (`blinkid-react-native` v7.2.0) | NO | Dev build likely works | |
| ID Analyzer | NO (server-side JS only) | N/A | N/A | No mobile SDK; API-only |
| AU10TIX | NO (native iOS/Android only) | N/A | Requires native bridge | No RN wrapper |
| HyperVerge | YES (`react-native-hyperkyc-sdk`) | NO | Dev build likely works | |

**Key insight:** ALL IDV SDKs require native modules (camera access, NFC, biometric processing). None work with Expo Go. All require either `npx expo prebuild` or a development build. **Only Didit provides an Expo config plugin** that automates the native setup, which is a significant DX advantage for a solo developer.

---

## 5. MASTER COMPARISON TABLE

| Provider | Per Check | Monthly Min | Free Trial | Israel ID Card | Teudat Zehut | RN SDK | Expo Plugin | Liveness | Face Match | AML | Self-Serve | HQ | Data Breach |
|----------|-----------|-------------|------------|---------------|--------------|--------|-------------|----------|------------|-----|------------|-----|-------------|
| **Didit** | **FREE (500/mo) then $0.30** | **$0** | 500 free/mo forever | Likely | Likely (unconfirmed) | YES | **YES** | YES (passive) | YES | $0.20 add-on | YES | Barcelona, Spain | None known |
| **Shufti Pro** | **$0.20** | **$0** | 7-day trial | **CONFIRMED** | **CONFIRMED** | YES | No | YES | YES | Included | YES | London, UK | None known |
| ID Analyzer | **$0.089** (Entry plan) | $89/mo | 100 free/mo | **CONFIRMED** | **CONFIRMED** | NO (API only) | N/A | YES | YES | Included | YES | Taichung, Taiwan | None known |
| iDenfy | $0.55-$1.35 | Not published | 14-day, 10 checks | Likely | Likely | YES | No | YES | YES | Available | YES | Kaunas, Lithuania | None known |
| Veriff | $0.80 | $49/mo | 30-day, 100 checks | **NO** | **NO** | YES | No | YES | YES | $0.64 add-on | YES | Tallinn, Estonia | Nov 2025 (8.5K records) |
| IDWise | $1.00 | Not published | 30-day, no CC | Likely | Likely | YES | No | YES (NIST) | YES | $0.25 add-on | YES | London, UK | None known |
| ComplyCube | $0.80-$1.35 | Not published | Startup program | Likely | Likely | YES | No | YES | YES | Available | YES | London, UK | None known |
| Sumsub | $1.35 | $149/mo | 14-day, 50 checks | Likely | Likely | YES | No | YES | YES | $1.85 plan | YES | London, UK | None known |
| Persona | FREE (500/mo x12) then $1.00 | $250/mo after | Startup program | Likely | Likely | YES | No | YES | YES | Included in some | YES | San Francisco, USA | Feb 2026 (code exposure + surveillance) |
| Ondato | EUR 0.50-1.40 | Not published | Not found | Likely | Likely | YES | No | YES | YES | Available | YES | Vilnius, Lithuania | None known |
| Regula | License-based | Annual license | Not found | Very likely | Very likely | YES | No | YES | YES | No | NO | Daugavpils, Latvia | None known |
| Microblink | Custom | Custom | Free dev trial | CONFIRMED | CONFIRMED | YES | No | Via partner | Via partner | No | NO | New York/Zagreb | None known |
| AU10TIX | Custom | Custom | Not found | Very likely | Very likely | NO | No | YES | YES | YES | NO | Amsterdam, NL | June 2024 (MAJOR) |
| Jumio | Custom | Custom | Not found | Likely | Likely | YES | No | YES | YES | YES | NO | Palo Alto, USA | None known |
| Entrust/Onfido | Custom | Custom | Not found | Likely | Likely | YES | No | YES | YES | YES | NO | London, UK | None known |
| HyperVerge | Custom | Custom | Not found | Likely | Likely | YES | No | YES | YES | Available | NO | Palo Alto/Bengaluru | None known |

---

## 6. RECOMMENDATIONS FOR EMUNI

### Tier 1: Best Options (Investigate First)

#### 1. Didit — BEST OVERALL FOR EMUNI
- **Why:** 500 free checks/month covers entire early-stage volume. $0.30/check after free tier (cheapest in market for full ID+liveness+face match). Only provider with Expo config plugin. No minimums. Pay only for successful checks.
- **Risk:** New company (2021). Teudat Zehut support needs confirmation before committing.
- **Action:** Contact Didit to confirm Israel identity card (Teudat Zehut, 2013 biometric version) support. If confirmed, this is the clear winner.
- **Monthly cost at 50 checks:** $0 (within free tier)
- **Monthly cost at 500 checks:** $0 (within free tier)
- **Monthly cost at 1,000 checks:** $150 ($0.30 x 500 paid checks)

#### 2. Shufti Pro — BEST CONFIRMED OPTION
- **Why:** CONFIRMED Teudat Zehut support. $0.20/check is extraordinarily cheap. No minimums. Includes liveness + face match + AML. RN SDK available.
- **Risk:** $0.20/check may be a promotional/introductory price. Company is smaller/less established. No Expo config plugin (but dev build should work). Quality of liveness/deepfake detection may be lower at this price point.
- **Action:** Sign up for 7-day trial. Test with actual Teudat Zehut document. Evaluate accuracy and UX.
- **Monthly cost at 50 checks:** $10
- **Monthly cost at 500 checks:** $100

### Tier 2: Fallback Options

#### 3. IDWise — SIMPLE AND TRANSPARENT
- **Why:** $1/check all-in. NIST-certified liveness. Active RN SDK development. 30-day free trial with no credit card.
- **Risk:** $1/check is 5x Shufti Pro. Teudat Zehut support unconfirmed.
- **Monthly cost at 50 checks:** $50
- **Monthly cost at 500 checks:** $500

#### 4. ID Analyzer — CHEAPEST PER-CHECK (API-ONLY)
- **Why:** CONFIRMED Teudat Zehut support. $0.089/check at Entry tier. Free tier (100/month).
- **Risk:** No mobile SDK. You'd need to build document capture UI yourself and call API server-side. Significantly more development work for a solo developer.
- **Monthly cost at 50 checks:** $0 (free tier) or $89 (Entry plan)

#### 5. iDenfy — MID-RANGE ESTABLISHED
- **Why:** $0.55/check at best volume pricing. Established provider. RN SDK. Hybrid AI+human model.
- **Risk:** Price is higher than Didit/Shufti. Teudat Zehut unconfirmed. No Expo config plugin.
- **Monthly cost at 500 checks:** $275

### NOT Recommended

| Provider | Why Not |
|----------|---------|
| **Veriff** | Does NOT support Teudat Zehut. Data breach Nov 2025. $49/mo minimum. |
| **Persona** | Feb 2026 surveillance exposure. 3-year data retention. Discord dropped them. |
| **AU10TIX** | Major data breach 2024. No self-serve. No RN SDK. Enterprise-only. |
| **Sumsub** | $149/mo minimum is too high. $1.35/check. |
| **Entrust/Onfido** | Enterprise-only. No self-serve. |
| **Jumio** | Enterprise-only. No public pricing. |
| **Regula** | License-based, not per-check. No self-serve. |

---

## 7. RECOMMENDED DECISION SEQUENCE

```
1. Contact Didit -> "Do you support Israeli Teudat Zehut (biometric ID card, 2013 version)?"
   |-- YES -> Use Didit. 500 free/month. Expo config plugin. Done.
   |-- NO or unclear ->
   v
2. Sign up for Shufti Pro 7-day trial -> Test with real Teudat Zehut
   |-- Works well, good UX -> Use Shufti Pro. $0.20/check. Done.
   |-- Poor quality / issues ->
   v
3. Contact IDWise -> Confirm Teudat Zehut support
   |-- YES -> Use IDWise. $1/check all-in. Simple. Done.
   |-- NO ->
   v
4. Contact iDenfy -> Confirm Teudat Zehut support
   |-- YES -> Use iDenfy. $0.55/check. Done.
   |-- NO ->
   v
5. Use ID Analyzer API ($0.089/check) + build custom capture UI
   (confirmed Teudat Zehut support, but more dev work)
```

---

## 8. CRITICAL UPDATE TO TECHNICAL PRD

The Technical PRD (EMUNI_TECHNICAL_PRD.md) currently recommends **Veriff at $0.80/check**. This must be updated:

**Problem:** Veriff does NOT support Israeli identity cards (Teudat Zehut). It only supports Israeli passports and driver's licenses. For a nanny verification flow where the primary document is the Teudat Zehut, Veriff is not viable.

**Required change:** Replace Veriff with the winner from the decision sequence above. Update cost projections accordingly (likely cheaper: $0-$0.20/check instead of $0.80/check).

**Cost impact:** Significant savings. At 500 checks/month:
- Veriff: $400/month ($0.80 x 500)
- Didit: $0/month (within free tier)
- Shufti Pro: $100/month ($0.20 x 500)
- IDWise: $500/month ($1.00 x 500)

---

## Sources

- [Veriff Self-Serve Plans](https://www.veriff.com/plans/self-serve)
- [Veriff Supported Countries](https://www.veriff.com/supported-countries)
- [Veriff React Native SDK](https://devdocs.veriff.com/docs/react-native-sdk-guide)
- [Veriff Data Breach — Total Wireless](https://www.teiss.co.uk/news/data-security-incident-at-veriff-impacted-total-wireless-customers-mvno-says-16945)
- [iDenfy Pricing](https://www.idenfy.com/pricing-plans-v3/)
- [iDenfy React Native SDK](https://github.com/idenfy/ReactNativeSDK)
- [iDenfy Supported Documents](https://www.idenfy.com/supported-documents/)
- [Sumsub Pricing](https://sumsub.com/pricing/)
- [Sumsub React Native Module](https://docs.sumsub.com/docs/react-native-module)
- [Sumsub Supported Documents](https://sumsub.com/supported-documents/)
- [Entrust/Onfido Acquisition](https://techcrunch.com/2024/02/06/confirmed-entrust-is-buying-ai-based-id-verification-startup-onfido-sources-say-for-more-than-400m/)
- [AU10TIX Data Breach (EFF)](https://www.eff.org/deeplinks/2024/06/hack-age-verification-company-shows-privacy-danger-social-media-laws)
- [Jumio React Native Plugin](https://github.com/Jumio/mobile-react)
- [Regula React Native SDK](https://github.com/regulaforensics/react-native-document-reader)
- [Persona Startup Program](https://help.withpersona.com/articles/1XNnqukfZY9VamF2e7jkuJ/)
- [Persona Security Exposure (Malwarebytes)](https://www.malwarebytes.com/blog/news/2026/02/age-verification-vendor-persona-left-frontend-exposed)
- [Persona Security Exposure (Fortune)](https://fortune.com/2026/02/24/discord-peter-thiel-backed-persona-identity-verification-breach/)
- [Shufti Pro Supported Documents](https://shuftipro.com/supported-documents/)
- [Shufti Pro React Native SDK](https://github.com/shuftipro/React-Native-SDK)
- [Didit Pricing](https://didit.me/pricing/)
- [Didit React Native SDK (GitHub)](https://github.com/didit-protocol/sdk-react-native)
- [Didit Supported Documents](https://docs.didit.me/reference/supported-documents-id-verification)
- [IDWise Pricing](https://www.idwise.com/pricing/)
- [IDWise React Native SDK](https://www.npmjs.com/package/idwise-react-native-sdk)
- [ID Analyzer Pricing](https://www.idanalyzer.com/pricing.html)
- [ID Analyzer Israel Documents](https://www.idanalyzer.com/solutions/supported-documents/il.html)
- [ComplyCube Pricing](https://www.complycube.com/en/pricing/)
- [ComplyCube React Native SDK](https://github.com/complycube/complycube-react-native-sdk)
- [Ondato Pricing](https://ondato.com/identity-verification-pricing/)
- [Microblink BlinkID React Native](https://github.com/BlinkID/blinkid-react-native)
- [IDV Pricing Comparison (Trust Swiftly)](https://trustswiftly.com/blog/identity-verification-pricing-comparison-and-alternatives/)
- [Best IDV Providers 2026 (Ondato)](https://ondato.com/blog/best-identity-verification-software/)
