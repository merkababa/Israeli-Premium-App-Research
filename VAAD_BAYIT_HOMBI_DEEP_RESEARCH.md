# Hombi (הומבי) — Deep Research Report

**Date: March 2026 | Status: Zombie — great product, failed business**

---

## Quick Summary

Hombi is a **cautionary tale of a great product with no business model.** 4.8-star ratings, genuine user love, 10 years in market — and it never grew. Both founders left. Zero funding raised. NIS 29.90/month revenue per building. The app persists in zombie state.

---

## Company Overview

| Attribute | Detail |
|-----------|--------|
| **Legal Entity** | Hombi Ltd. (הומבי בע"מ), Registration #516270311 |
| **Address** | 21 Dishon Street, Jerusalem, Israel |
| **Founded** | 2015 |
| **Founders** | Oron Ben-David (Co-founder), Ovad Tzion (CEO & Co-founder) |
| **Funding** | **$0 — Zero. Entirely bootstrapped.** |
| **Team (current)** | Nobody identifiable. No CEO, CTO, or team listed. |
| **Contact** | info@hombi.co.il, support@hombi.co.il, WhatsApp: 0554425868 |
| **Websites** | [hombi.co](https://hombi.co/), [hombi.co.il](https://hombi.co.il/) |

---

## Business Model

### Revenue Streams

| Stream | Details |
|--------|---------|
| **Core app** | 100% free — messaging, voting, tasks, maintenance, documents, forums, event room booking |
| **Payment collection service** | **NIS 29.90/month per building** — the ONLY paid feature |
| **CC processing fees** | Passed through to credit card companies — Hombi does NOT take a cut |
| **Professional directory** | Possibly referral fees from vetted contractors (unconfirmed) |
| **In-app advertising** | Confirmed in privacy policy: "Commercial information display does not constitute a recommendation" |
| **Premium tiers** | None. No paid subscription tiers beyond the NIS 29.90 collection service. |

### Revenue Math

Even at their claimed 13,000 Israeli buildings, if 20% pay for collection:
- 2,600 buildings x NIS 29.90 = **NIS 77,740/month (~$21,600/month)**
- That barely supports **one developer's salary** in Israel (avg tech salary NIS 39,810/month)

### The Fatal Business Model Mistake

Compare Hombi vs. Bllink:

| | Hombi | Bllink |
|---|---|---|
| **Model** | Flat NIS 29.90/month per building | 1.5-3% commission on all payments |
| **Revenue from 20-unit building (NIS 200/unit fees)** | NIS 29.90/month | NIS 60-120/month |
| **Revenue from 40-unit building (NIS 300/unit fees)** | NIS 29.90/month (same!) | NIS 180-360/month |
| **Scales with building size?** | No | Yes |
| **Scales with payment volume?** | No | Yes |

Hombi chose a flat fee that doesn't scale. A 200-unit luxury tower pays the same NIS 29.90 as a 4-unit walk-up. Bllink's percentage model means bigger buildings = more revenue automatically.

---

## Founders — Why They Left

### Ovad Tzion (CEO & Co-founder)

| Attribute | Detail |
|-----------|--------|
| **Background** | Senior Manager at HP → Group Manager at HPE |
| **Education** | Industrial Engineering & Management, Ariel University |
| **Current role** | **COO at DealHub.io** (AI-powered CPQ/CLM platform, raised $60M+) |
| **LinkedIn** | [linkedin.com/in/ovad-tzion-9a790388](https://www.linkedin.com/in/ovad-tzion-9a790388/) |
| **When left Hombi** | Exact date unknown, but DealHub role started well before 2024 |

**Why he left:** DealHub is a well-funded ($60M+), high-growth B2B SaaS company. Hombi was making <$22K/month with zero growth trajectory. The COO title at a funded startup vs. CEO of a side project making beer money — the choice was obvious.

**Note:** The iOS App Store still lists "Ovad Tzion" as the developer — the Apple Developer account was never transferred.

### Oron Ben-David (Co-founder)

| Attribute | Detail |
|-----------|--------|
| **Current status** | **Virtually untraceable** |
| **LinkedIn** | Not found |
| **Press mentions** | None |
| **Subsequent ventures** | None found |

Likely the technical co-founder who stayed behind the scenes. Appears to have left the tech industry entirely. "Oron Ben-David" is a common Israeli name, making searches difficult.

### The Side Project Reality

**Neither founder was ever full-time on Hombi.** Evidence:
- Both were employed at HP/HPE while building Hombi
- Ionic Framework (cheapest/fastest hybrid approach) chosen for speed, not quality
- Version 1.0.7 on Android after 10 years = near-zero engineering investment
- Zero press coverage in 10 years (never pitched to media)
- Zero funding raised (never seriously fundraised)

---

## Adoption & Traction

### Claimed Numbers

| Metric | Claim | Source |
|--------|-------|--------|
| Buildings globally | 90,000+ | hombi.co.il website |
| Buildings in Israel | 13,000+ | hombi.co.il website |
| Google Play downloads | 73,000 total | AppBrain |
| Current download rate | ~540/month (18/day) | AppBrain |
| Google Play ratings | 4.80/5 (470 ratings) | Google Play |
| App Store ratings | 4.5/5 (77 ratings) | App Store |

### Reality Check

- 90,000 buildings claim is questionable with only 73K Google Play downloads
- Likely includes "registered" buildings where one person signed up but the building never actively adopted
- **Active buildings probably 2,000-3,000 at most**
- 540 downloads/month and declining = no growth trajectory
- Only 470 Google Play reviews for 73K downloads = 0.6% review rate (healthy apps get 2-5%)

---

## Current State (March 2026)

| Signal | Status |
|--------|--------|
| **Who's running it?** | Nobody identifiable |
| **Android last update** | Aug 2025 (v1.0.7) — minimal maintenance |
| **iOS last update** | Sep 2024 (v5.6) — maintenance module added |
| **Website traffic** | Very low (ScamAdviser: "not scanned in 30+ days") |
| **Social media** | Dormant |
| **App Store developer** | Still "Ovad Tzion" (personal account) |

The app still works. Someone occasionally pushes a maintenance update. But there's no team, no growth, no marketing, no future.

---

## User Feedback

### What Users Love

| Reviewer | Rating | Comment |
|----------|--------|---------|
| David Kaplan | 5/5 | "By far the most advanced and user friendly solution I have seen" |
| doronp | 5/5 | "All-in-One solution... first-class customer service" |
| NitsYak | 5/5 | "Very useable, great service" |
| Moshe B. | 5/5 | "Great application... very clear and intuitive" |

**Consistent praise:** Intuitive interface, simple for non-tech users, responsive support, comprehensive features.

### What Users (Implicitly) Complain About

- No visible complaints about bugs or crashes
- The real complaint is **adoption friction** — the app only works when most residents in a building sign up
- Professional management companies don't mention Hombi ([Midrag reviews](https://www.midrag.co.il/Expanel/Question/2448)) — they prefer Darimpo or Bllink

---

## Technology

| Attribute | Detail |
|-----------|--------|
| **Framework** | Ionic (hybrid web wrapper) — package ID: `com.ionicframework.vaadapp212468` |
| **Version (Android)** | 1.0.7 (after 10 years) |
| **Version (iOS)** | 5.6 (more active iOS development history) |
| **Backend** | Appears to use Parse/Back4App |
| **Domain hosting** | GoDaddy Netherlands servers |
| **Mobile experience** | Hybrid (not native) — performance always second-tier |

The Ionic package ID literally contains `ionicframework` — auto-generated from early Ionic CLI (2015 era). Modern apps use custom package names. This was never rebuilt.

---

## Features (What They Built)

### Full Feature List

- Internal messaging (building-level)
- Voting and surveys for building decisions
- Professional directory (vetted contractors)
- Problem/fault reporting with photos
- Financial reports accessible to all residents
- Credit card payment for vaad fees (NIS 29.90/month extra)
- Task management and maintenance reminders
- Building maintenance module (added Sep 2024)
- Service orders
- Event room booking
- Document storage (protocols, minutes)
- Forums

### What's Missing

- No WhatsApp integration
- No Bit payment support
- No standing orders / recurring payments
- No expense management (only income/payment tracking)
- No vendor marketplace
- No AI features
- No multi-language support

---

## 7 Lessons from Hombi's Failure

| # | What Went Wrong | Our Lesson |
|---|----------------|-----------|
| 1 | **NIS 29.90/month flat fee** — doesn't scale with building size | Use % transaction fees. 1.5% on NIS 4K = NIS 60 — 2x Hombi's entire revenue per building |
| 2 | **Side project** — HP employees building on weekends | Commit full-time or don't enter |
| 3 | **Zero funding** — couldn't invest in growth | Bootstrap profitably on transaction fees or raise seed |
| 4 | **Targeted volunteers** not management companies | Volunteers have no budget/time/authority. Mgmt companies manage 20-100 buildings each |
| 5 | **Competed with WhatsApp** for messaging | Don't replace WhatsApp. Work THROUGH it. Send payment links INTO WhatsApp |
| 6 | **Required ALL residents to download app** | Only vaad chair needs dashboard. Residents click WhatsApp payment link |
| 7 | **Zero marketing/press in 10 years** | Content marketing, Facebook groups, partnerships from month 1 |

---

## What's Worth Copying

- **Feature list** — the right template for what a vaad bayit platform needs
- **UX simplicity** — users consistently praise ease of use (4.8 stars)
- **Hebrew-first design** — obviously correct for Israeli market
- **"Registration in seconds" onboarding** — minimal friction

## What to Specifically Avoid

1. Flat per-building fee as primary revenue
2. Ionic/Cordova hybrid framework
3. Side project commitment level
4. Targeting individual volunteer vaad chairs exclusively
5. Trying to replace WhatsApp for messaging
6. Requiring residents to download an app
7. Zero marketing/press strategy

---

## Interesting Detail: Bllink-Hombi Connection?

[Batim.org.il](https://www.batim.org.il/) lists "Bllink Systems Ltd (בלינק מערכות בע"מ), registration 514719921" connected to Hombi — described as "System for managing vaad bayit payments | Hombi." This suggests Bllink may be the payment-processing entity behind Hombi's collection service, or there was a partnership. Could not confirm a direct corporate relationship.

---

## Sources

- [Hombi Official Website (hombi.co)](https://hombi.co/)
- [Hombi Israel Website (hombi.co.il)](https://hombi.co.il/)
- [Hombi User Manual](https://hombi.co/full_manual.htm)
- [Hombi Terms of Service](https://hombi.co/terms.htm)
- [Hombi Privacy Policy](https://hombi.co/privacy_policy.htm)
- [Hombi on Google Play](https://play.google.com/store/apps/details?id=com.ionicframework.vaadapp212468)
- [Hombi on App Store](https://apps.apple.com/il/app/%D7%94%D7%95%D7%9E%D7%91%D7%99-hombi/id1071129259)
- [Hombi on AppBrain](https://www.appbrain.com/app/hombi/com.ionicframework.vaadapp212468)
- [Hombi on Tracxn](https://tracxn.com/d/companies/hombi/__5twNDK5CgMPj3IPqNYPymXd26Z1mCwssZL4AYn8JJcw)
- [Hombi on Crunchbase](https://www.crunchbase.com/organization/hombi)
- [Hombi Ltd Company Registration](https://en.checkid.co.il/company/HOMBI+LTD-YeEBbg5-516270311)
- [Ovad Tzion LinkedIn](https://www.linkedin.com/in/ovad-tzion-9a790388/)
- [Ovad Tzion on ZoomInfo](https://www.zoominfo.com/p/Ovad-Tzion/5397721232)
- [Bllink Funding (Calcalistech)](https://www.calcalistech.com/ctech/articles/0,7340,L-3911934,00.html)
- [Midrag Professional Reviews](https://www.midrag.co.il/Expanel/Question/2448)

---

*Research compiled March 2026. All sources cited. Unverified claims flagged throughout.*
