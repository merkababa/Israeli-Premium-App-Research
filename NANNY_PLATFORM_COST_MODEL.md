# Nanny Platform Cost Model, Burn Rate & Funding Requirements

> **IMPORTANT:** This cost model assumes a 7.5 FTE team with salaries totaling ~NIS 329-855K/mo. It is **superseded by the solo-bootstrapper operating model** defined in `EMUNI_PRD.md` and `EMUNI_ROADMAP.md`. The solo founder model has near-zero monthly burn (~NIS 500-1K/mo pre-seed). This document is retained for reference when planning post-seed team hiring.

**Research Date:** March 7, 2026
**Purpose:** Realistic cost modeling for Israeli nanny matching platform startup
**Currency:** All figures in NIS unless noted. Exchange rate: 1 USD = ~3.6 NIS

---

## TABLE OF CONTENTS

1. [Team Costs (Israeli Salaries 2025-2026)](#1-team-costs)
2. [Infrastructure Costs](#2-infrastructure-costs)
3. [Background Check & Verification Costs](#3-background-check--verification-costs)
4. [Marketing & Customer Acquisition Costs](#4-marketing--customer-acquisition-costs)
5. [Other Operational Costs](#5-other-operational-costs)
6. [Full Cost Model: Monthly Burn by Stage](#6-full-cost-model-monthly-burn-by-stage)
7. [Funding Requirements & Seed Round Recommendation](#7-funding-requirements--seed-round-recommendation)
8. [Israeli Startup Funding Landscape 2025-2026](#8-israeli-startup-funding-landscape)

---

## 1. TEAM COSTS

### 1.1 Israeli Hi-Tech Salary Benchmarks (2025-2026)

Salaries below reflect **total employer cost** (gross salary + Bituach Leumi employer contribution ~7.6% + pension/severance ~8.33% + health tax). Employer cost is typically 120-125% of gross salary.

| Role | Monthly Gross (NIS) | Monthly Employer Cost (NIS) | Annual Employer Cost (NIS) | Source |
|------|--------------------:|---------------------------:|---------------------------:|--------|
| **Full-Stack Developer (Mid)** | 28,000-38,000 | 34,000-46,000 | 408,000-552,000 | Glassdoor, PayScale |
| **Full-Stack Developer (Senior)** | 38,000-50,000 | 46,000-61,000 | 552,000-732,000 | Levels.fyi |
| **Mobile Developer (React Native)** | 30,000-42,000 | 36,000-51,000 | 432,000-612,000 | Glassdoor |
| **UI/UX Designer (Mid)** | 22,000-32,000 | 27,000-39,000 | 324,000-468,000 | Glassdoor, PayScale |
| **Product Manager** | 30,000-45,000 | 36,000-55,000 | 432,000-660,000 | Levels.fyi, ERI |
| **Marketing Manager** | 20,000-30,000 | 24,000-36,000 | 288,000-432,000 | Glassdoor |
| **Customer Support / Trust & Safety** | 12,000-18,000 | 14,500-22,000 | 174,000-264,000 | Market rate |
| **Community Manager** | 14,000-20,000 | 17,000-24,000 | 204,000-288,000 | Market rate |

### 1.2 Freelancer/Contractor Alternative Rates

For early-stage cost reduction, freelancers avoid employer tax burden (~20% savings) but lose IP assignment protections.

| Role | Hourly Rate (NIS) | Monthly (Full-Time Equiv.) | Notes |
|------|------------------:|---------------------------:|-------|
| Full-Stack Developer | 200-350 | 34,000-60,000 | No employer taxes but higher gross |
| Mobile Developer | 220-380 | 37,000-65,000 | React Native specialists command premium |
| UI/UX Designer | 150-280 | 25,000-48,000 | Can hire part-time (50-80 hrs/month) |
| DevOps/Cloud | 250-400 | 42,000-68,000 | Usually part-time/consulting |
| QA Engineer | 120-200 | 20,000-34,000 | Can outsource or automate initially |

### 1.3 Minimum Team for MVP Launch (Pre-Revenue)

| Role | FTE | Monthly Cost (NIS) | Notes |
|------|----:|-------------------:|-------|
| CTO/Lead Developer (Co-founder) | 1.0 | 20,000 | Below market, equity-compensated |
| Full-Stack Developer | 1.0 | 38,000 | Employee, mid-level |
| Mobile Developer (React Native) | 0.5 | 19,000 | Part-time contractor |
| UI/UX Designer | 0.3 | 10,000 | Freelancer, 50-60 hrs/month |
| CEO/Product (Co-founder) | 1.0 | 15,000 | Below market, equity-compensated |
| **TOTAL** | **3.8** | **102,000** | |

### 1.4 Team at Launch + 6 Months (Post-Launch Scaling)

| Role | FTE | Monthly Cost (NIS) | Notes |
|------|----:|-------------------:|-------|
| CTO/Lead Developer | 1.0 | 30,000 | Salary increase after funding |
| Full-Stack Developer | 2.0 | 80,000 | 2 mid-senior developers |
| Mobile Developer | 1.0 | 40,000 | Full-time employee |
| UI/UX Designer | 0.5 | 15,000 | Part-time, growing to full-time |
| CEO/Product Manager | 1.0 | 25,000 | Post-funding salary |
| Marketing Manager | 1.0 | 26,000 | |
| Community/CS Manager | 1.0 | 18,000 | Trust & safety + customer support |
| **TOTAL** | **7.5** | **234,000** | |

### 1.5 Team at Scale (Month 18-24, ~5,000+ Users)

| Role | FTE | Monthly Cost (NIS) | Notes |
|------|----:|-------------------:|-------|
| CTO | 1.0 | 42,000 | |
| Full-Stack Developers | 3.0 | 126,000 | |
| Mobile Developer | 1.0 | 44,000 | |
| DevOps/SRE | 0.5 | 25,000 | Part-time or shared |
| QA Engineer | 1.0 | 25,000 | |
| UI/UX Designer | 1.0 | 32,000 | Full-time |
| CEO | 1.0 | 35,000 | |
| VP Product | 1.0 | 40,000 | |
| Marketing Manager | 1.0 | 30,000 | |
| Content/SEO Specialist | 1.0 | 20,000 | |
| Community Manager | 1.0 | 20,000 | |
| Customer Support | 2.0 | 32,000 | Trust & safety team |
| B2B Sales | 1.0 | 28,000 | + commission |
| **TOTAL** | **15.5** | **499,000** | |

---

## 2. INFRASTRUCTURE COSTS

### 2.1 Cloud Hosting (AWS Israel Region — il-central-1)

AWS opened the Tel Aviv region (il-central-1) in August 2023 with 3 Availability Zones. Pricing is approximately **5-6% higher than EU (Ireland)** region, with **4x higher data transfer costs** to other regions.

**Recommendation:** Start on AWS Israel for data residency compliance (Israeli privacy law), then consider EU region for non-sensitive workloads to save on costs.

| Stage | Monthly AWS Cost (USD) | Monthly (NIS) | What's Included |
|-------|----------------------:|--------------:|-----------------|
| **Pre-Launch/MVP** | $200-400 | 720-1,440 | 1-2 EC2 t3.medium, RDS t3.micro, S3, basic networking |
| **Launch (0-1K users)** | $500-1,000 | 1,800-3,600 | 2 EC2 t3.large, RDS t3.small, ElastiCache, S3+CloudFront |
| **Growth (1K-5K users)** | $1,200-2,500 | 4,320-9,000 | Auto-scaling group, RDS t3.medium multi-AZ, ElastiCache, heavier S3 |
| **Scale (5K-20K users)** | $3,000-6,000 | 10,800-21,600 | Multiple services, reserved instances, higher storage |

**Alternative:** GCP and Azure also have Israel regions. GCP may be 5-10% cheaper for compute but AWS has the broadest service catalog in the Israel region.

### 2.2 Third-Party Services

| Service | Provider | Monthly Cost (NIS) | Notes |
|---------|----------|-------------------:|-------|
| **Push Notifications** | Firebase (Google) | 0 (free tier) | Free for up to 500K notifications/day |
| **SMS (OTP/Alerts)** | Twilio / Sinch | 400-2,000 | Twilio: $0.2575/SMS. Hebrew = 70 chars/segment. Budget: 200-500 SMS/month initially |
| **Email Service** | SendGrid / Mailgun | 0-200 | Free tier covers 100/day. Growth: $20-50/mo |
| **CDN (Images/Video)** | CloudFront (AWS) | 100-500 | Profile photos, video intros. Scales with usage |
| **Monitoring** | Datadog / New Relic | 0-500 | Free tiers available. $20-50/mo for small teams |
| **Analytics** | Mixpanel / Amplitude | 0-400 | Free tiers cover early stage. Growth plans ~$100/mo |
| **Error Tracking** | Sentry | 0-100 | Free tier: 5K events/mo. Team plan: $26/mo |
| **Chat/Messaging** | Stream / SendBird | 0-1,500 | Stream: free up to 5K MAU. Growth: $399/mo |
| **Search** | Algolia / Meilisearch | 0-500 | Algolia free: 10K searches/mo. Self-hosted Meili: $0 |

### 2.3 Infrastructure Cost Summary by Stage

| Stage | Cloud | Third-Party Services | **Total Infra/Month (NIS)** |
|-------|------:|---------------------:|----------------------------:|
| **Pre-Launch** | 1,000 | 500 | **1,500** |
| **Launch (Month 1-6)** | 2,500 | 2,500 | **5,000** |
| **Growth (Month 6-12)** | 6,000 | 5,000 | **11,000** |
| **Scale (Month 12-24)** | 15,000 | 10,000 | **25,000** |

---

## 3. BACKGROUND CHECK & VERIFICATION COSTS

### 3.1 Israel Police Criminal Record Check (תעודת יושר)

| Item | Cost | Process | Timeline |
|------|-----:|---------|----------|
| **Criminal Information Certificate** | NIS 45-47 per check | Online via Israel Police website or in-person at station | 10 business days (online), same day (in-person) |
| **Certificate Validity** | — | Valid for 3 months | Must be renewed |
| **Who Can Request** | — | The individual themselves (or via power of attorney) | Platform CANNOT request on behalf of nanny |

**Key Constraint:** The platform cannot directly pull criminal records. The nanny must request their own certificate and upload it. The platform verifies the document's authenticity.

**Cost to Platform:** NIS 0 per check (nanny obtains their own certificate). The platform may choose to **reimburse** nannies for the NIS 47 fee as a goodwill/onboarding incentive.

**If Platform Reimburses:** Budget NIS 47 x number of new nannies per month.

### 3.2 Sex Offender Registry Check

Israel maintains a sex offender registry under the Sex Offenders Supervision Law (2006). Access is restricted to authorized bodies (police, certain government agencies). A platform likely cannot access this directly.

**Practical approach:** The criminal record certificate (תעודת יושר) will indicate if there are sex-related offenses. The platform should require this certificate and verify it covers this category.

**Cost:** Included in the NIS 47 criminal record check.

### 3.3 ID Verification (Digital)

| Provider | Per-Check Cost (est.) | Notes |
|----------|----------------------:|-------|
| **Au10tix** (Israeli company, Bnei Brak) | $1.50-3.00 (NIS 5.40-10.80) | Custom pricing. Israeli company — potential partnership. Supports Israeli ID (Teudat Zehut) |
| **Persona** | $1.00-3.00 (NIS 3.60-10.80) | Supports 200+ countries. Good for Israel + foreign workers |
| **Jumio** | $2.00-5.00 (NIS 7.20-18.00) | Enterprise-grade. Volume discounts available |
| **Regula** | $0.50-2.00 (NIS 1.80-7.20) | On-premise option. Lower cost but less feature-rich |

**Recommendation:** Au10tix — Israeli company, supports Teudat Zehut natively, potential for partnership/discount as a local startup.

### 3.4 Verification Volume & Cost Projections

| Stage | New Nannies/Month | Criminal Record Reimbursement | ID Verification (Au10tix) | **Total/Month (NIS)** |
|-------|------------------:|------------------------------:|--------------------------:|----------------------:|
| **Pre-Launch (Seeding)** | 50 | 2,350 | 400 | **2,750** |
| **Launch (Month 1-6)** | 100 | 4,700 | 800 | **5,500** |
| **Growth (Month 6-12)** | 200 | 9,400 | 1,600 | **11,000** |
| **Scale (Month 12-24)** | 400 | 18,800 | 3,200 | **22,000** |

**Note:** Criminal record certificates expire every 3 months. For ongoing nannies, re-verification costs apply quarterly. At 2,000 active nannies: NIS 94,000/quarter = NIS 31,333/month in re-verification.

---

## 4. MARKETING & CUSTOMER ACQUISITION COSTS

### 4.1 Digital Advertising Costs in Israel

#### Facebook / Instagram Ads (Meta)

| Metric | Israel Estimate | Global Benchmark | Source |
|--------|---------------:|------------------:|--------|
| **CPM (Cost per 1,000 impressions)** | $8-15 (NIS 29-54) | $7.47 global avg | Lebesgue, SuperAds |
| **CPC (Cost per click)** | $0.80-2.50 (NIS 2.90-9.00) | $1.72 global avg | Meta benchmarks |
| **CPI (Cost per install)** | $2.50-6.00 (NIS 9-22) | $1.75-4.50 EMEA | BusinessOfApps |

Israel is a Tier 1.5 market — more expensive than Eastern Europe, cheaper than US/UK. Parent demographic (women 25-45) is a competitive audience segment.

#### Google Ads (Search)

| Metric | Israel Estimate | Notes |
|--------|---------------:|-------|
| **Average CPC** | NIS 2-10 | Israel CPC ~55% less than US avg |
| **"שמרטפית" (babysitter)** | NIS 3-8 (est.) | Moderate competition, local keyword |
| **"טיפול בילדים" (childcare)** | NIS 4-12 (est.) | Higher competition |
| **"מטפלת לילדים" (nanny)** | NIS 3-10 (est.) | Moderate competition |

**Note:** Hebrew keywords have lower competition than English equivalents. Exact CPCs require Google Keyword Planner verification.

### 4.2 Influencer Marketing Costs (Israeli Mom Influencers)

| Tier | Followers | Cost per Post (NIS) | Cost per Story (NIS) | Notes |
|------|----------:|--------------------:|---------------------:|-------|
| **Nano** | 1K-10K | 500-1,500 | 200-500 | Highly engaged, local communities |
| **Micro** | 10K-50K | 1,500-5,000 | 500-2,000 | Best ROI for niche parenting content |
| **Mid** | 50K-200K | 5,000-15,000 | 2,000-5,000 | Broader reach, lower engagement rate |
| **Macro** | 200K+ | 15,000-50,000 | 5,000-15,000 | Celebrity moms, high awareness |

**Recommended approach:** Focus on 10-15 micro-influencers (10K-50K followers) in the Israeli parenting niche at NIS 2,000-4,000 per campaign. Monthly budget: NIS 10,000-20,000.

### 4.3 Referral Program Costs

| Mechanism | Cost per Acquisition (NIS) | Notes |
|-----------|---------------------------:|-------|
| **Family refers family** | 50-100 (credit/discount) | "Give NIS 50, get NIS 50" model |
| **Nanny refers nanny** | 25-50 (cash bonus) | Lower cost, high trust signal |
| **Family refers nanny** | 30-60 (credit) | Cross-side referral, valuable |

**Projected cost:** At 20% of new users from referrals — NIS 3,000-8,000/month initially.

### 4.4 SEO / Content Marketing

| Activity | Monthly Cost (NIS) | Notes |
|----------|-------------------:|-------|
| **Hebrew content writer (freelance)** | 3,000-6,000 | 4-8 articles/month on parenting, childcare, legal guides |
| **SEO tools (Ahrefs/SEMrush)** | 400-800 | One subscription for keyword research + tracking |
| **Video content (short-form)** | 2,000-5,000 | Parent testimonials, nanny profiles, TikTok/Reels |

### 4.5 CAC Benchmarks & Projections

| Channel | Estimated CAC (NIS) | % of Acquisitions | Notes |
|---------|--------------------:|------------------:|-------|
| **Organic / SEO** | 10-30 | 15% | Low cost but slow ramp |
| **Referrals** | 50-80 | 20% | High quality, medium cost |
| **Facebook/Instagram** | 80-150 | 35% | Primary paid channel |
| **Google Ads** | 100-200 | 15% | High intent, higher cost |
| **Influencer** | 60-120 | 10% | Hard to track precisely |
| **PR / Partnerships** | 20-50 | 5% | Unpredictable, high impact when it works |
| **Blended CAC** | **70-120** | **100%** | |

**Global benchmarks:** Consumer marketplace startups average $29-50 CAC (NIS 105-180). Our blended target of NIS 70-120 assumes strong organic/referral channels in a small, networked market (Israel).

### 4.6 Marketing Budget by Stage

| Stage | Monthly Budget (NIS) | Primary Channels |
|-------|---------------------:|------------------|
| **Pre-Launch** | 10,000-15,000 | Influencer seeding, Facebook community groups, WhatsApp |
| **Launch (Month 1-6)** | 25,000-40,000 | Facebook/Instagram ads, Google Ads, influencer, referral program |
| **Growth (Month 6-12)** | 50,000-80,000 | All channels, increased paid spend, B2B outreach |
| **Scale (Month 12-24)** | 80,000-150,000 | Full-funnel, brand campaigns, B2B sales, partnerships |

---

## 5. OTHER OPERATIONAL COSTS

### 5.1 Legal

| Item | Cost (NIS) | Frequency | Notes |
|------|----------:|-----------:|-------|
| **Company registration (Ltd.)** | 2,200-2,650 | One-time | Gov fee. Online: NIS 2,176; paper: NIS 2,645 |
| **Attorney — incorporation** | 5,000-15,000 | One-time | Articles of association, founder agreements |
| **Employment bureau license** | 2,000-5,000 (est.) | One-time + renewal | Based on Employment Service Law. ~3 months process |
| **Attorney retainer** | 3,000-8,000 | Monthly | Ongoing legal counsel, employment law, privacy |
| **Privacy registration (GDPR-like)** | 1,000-3,000 | One-time | Register database with Privacy Protection Authority |
| **Terms of Service / Privacy Policy** | 5,000-15,000 | One-time | Drafting by tech-specialized attorney |

**Attorney hourly rates in Israel:** NIS 300-800/hour. Startup-focused firms may offer packages.

**First-year legal budget:** NIS 60,000-120,000 (one-time setup + retainer).

### 5.2 Insurance

| Type | Annual Premium (NIS) | Coverage | Notes |
|------|---------------------:|----------|-------|
| **General Liability** | 5,000-15,000 | NIS 2-5M per occurrence | Basic business insurance |
| **E&O (Professional Liability)** | 8,000-20,000 | NIS 2-5M per occurrence | Critical for matching platform |
| **Cyber Insurance** | 5,000-15,000 | Data breach, cyber incidents | Required for PII handling |
| **Directors & Officers** | 5,000-12,000 | Personal liability protection | VCs may require this |
| **TOTAL** | **23,000-62,000** | | ~NIS 2,000-5,200/month |

### 5.3 Office / Co-Working

| Option | Monthly Cost (NIS) | Notes |
|--------|-------------------:|-------|
| **Fully remote** | 0 | Lowest cost; common for early-stage Israeli startups |
| **Hot desks (co-working)** | 800-1,200 per person | WeWork, Mindspace, local spaces |
| **Dedicated desks** | 1,200-2,000 per person | Reserved workspace, lockable storage |
| **Private office (4-6 people)** | 8,000-15,000 | Small team room in Tel Aviv co-working |
| **Private office (10+ people)** | 20,000-40,000 | Larger space, Tel Aviv center |

**Recommendation:** Start remote (NIS 0), transition to hot desks at 5+ team members (NIS 5,000-8,000/month), then private office at 10+ team (NIS 20,000+/month).

### 5.4 Payment Processing

| Provider | Transaction Fee | Monthly Fee | Notes |
|----------|---------------:|------------:|-------|
| **Stripe** | 2.9% + $0.30 ($1.04 NIS) | None | **NOT available for Israeli merchant accounts** — requires US LLC workaround. Use PayMe or PayPlus instead. |
| **PayPlus (Israeli)** | 2.3-2.8% + NIS 0.50 | NIS 0-200 | Israeli provider, supports Bit/PayBox |
| **Tranzila (Israeli)** | 2.0-2.5% + NIS 0.30 | NIS 100-300 | Popular Israeli payment gateway |
| **PayMe (Israeli)** | 2.5-3.0% | NIS 0-100 | Simple setup, mobile-first |

**Projected processing costs (based on revenue model):**
- Month 6: NIS 200K monthly transactions → NIS 5,000-6,000 in fees
- Month 12: NIS 500K monthly transactions → NIS 12,500-15,000 in fees
- Month 24: NIS 1.5M monthly transactions → NIS 37,500-45,000 in fees

### 5.5 Accounting & Bookkeeping

| Service | Monthly Cost (NIS) | Notes |
|---------|-------------------:|-------|
| **Bookkeeper (external)** | 2,000-4,000 | Monthly books, VAT filing, payroll |
| **Annual audit** | 10,000-25,000 | Required for Ltd. (spread monthly: NIS 800-2,100) |
| **Accounting software** | 200-500 | Rivhit, Hashavshevet, or similar Israeli accounting software |

---

## 6. FULL COST MODEL: MONTHLY BURN BY STAGE

### 6.1 Pre-Launch (Month -6 to 0)

Building MVP, seeding supply side, no revenue.

| Category | Monthly Cost (NIS) |
|----------|-------------------:|
| Team (3.8 FTE) | 102,000 |
| Infrastructure | 1,500 |
| Background checks (seeding nannies) | 2,750 |
| Marketing (pre-launch) | 12,000 |
| Legal (setup amortized) | 8,000 |
| Insurance | 2,000 |
| Office (remote) | 0 |
| Accounting | 2,500 |
| Misc / contingency (10%) | 13,000 |
| **MONTHLY BURN** | **143,750** |
| **Pre-Launch Phase Total (6 months)** | **862,500** |

### 6.2 Launch (Month 1-6)

Live product, first users, initial revenue trickle.

| Category | Monthly Cost (NIS) |
|----------|-------------------:|
| Team (7.5 FTE) | 234,000 |
| Infrastructure | 5,000 |
| Background checks | 5,500 |
| Marketing | 35,000 |
| Legal (retainer) | 5,000 |
| Insurance | 3,000 |
| Office (hot desks, 5 people) | 6,000 |
| Payment processing | 3,000 |
| Accounting | 3,000 |
| Misc / contingency (10%) | 30,000 |
| **MONTHLY BURN** | **329,500** |
| **Launch Phase Total (6 months)** | **1,977,000** |

### 6.3 Growth (Month 6-12)

Scaling users, growing revenue, still burning cash.

| Category | Monthly Cost (NIS) |
|----------|-------------------:|
| Team (10 FTE) | 340,000 |
| Infrastructure | 11,000 |
| Background checks (incl. re-verification) | 20,000 |
| Marketing | 65,000 |
| Legal (retainer) | 6,000 |
| Insurance | 4,000 |
| Office (dedicated desks, 8 people) | 12,000 |
| Payment processing | 10,000 |
| Accounting | 3,500 |
| Misc / contingency (10%) | 47,000 |
| **MONTHLY BURN** | **518,500** |
| **Growth Phase Total (6 months)** | **3,111,000** |

### 6.4 Scale (Month 12-24)

Larger team, aggressive marketing, approaching breakeven.

| Category | Monthly Cost (NIS) |
|----------|-------------------:|
| Team (15.5 FTE) | 499,000 |
| Infrastructure | 25,000 |
| Background checks (incl. re-verification) | 45,000 |
| Marketing | 120,000 |
| Legal (retainer + IP/compliance) | 8,000 |
| Insurance | 5,000 |
| Office (private, 12 people) | 25,000 |
| Payment processing | 30,000 |
| Accounting | 4,000 |
| B2B sales commissions | 15,000 |
| Misc / contingency (10%) | 77,600 |
| **MONTHLY BURN** | **853,600** |
| **Scale Phase Total (12 months)** | **10,243,200** |

### 6.5 Burn Rate Summary

| Phase | Duration | Monthly Burn (NIS) | Monthly Burn (USD) | Phase Total (NIS) |
|-------|----------|-------------------:|-------------------:|------------------:|
| Pre-Launch | 6 months | 143,750 | ~$39,900 | 862,500 |
| Launch | 6 months | 329,500 | ~$91,500 | 1,977,000 |
| Growth | 6 months | 518,500 | ~$144,000 | 3,111,000 |
| Scale | 12 months | 853,600 | ~$237,100 | 10,243,200 |
| **TOTAL (30 months to breakeven)** | | | | **16,193,700** |
| **TOTAL (USD)** | | | | **~$4,498,250** |

---

## 7. FUNDING REQUIREMENTS & SEED ROUND RECOMMENDATION

### 7.1 Revenue vs. Burn — Path to Breakeven

Using conservative revenue projections from NANNY_PLATFORM_REVENUE_MODEL_REVISED.md:

| Month | Monthly Revenue (NIS) | Monthly Burn (NIS) | Net Burn (NIS) | Cumulative Cash Needed (NIS) |
|-------|----------------------:|-------------------:|---------------:|-----------------------------:|
| Month 1 | 15,000 | 329,500 | -314,500 | 1,177,000 |
| Month 3 | 45,000 | 329,500 | -284,500 | 1,754,000 |
| Month 6 | 120,000 | 329,500 | -209,500 | 2,589,000 |
| Month 9 | 250,000 | 518,500 | -268,500 | 3,794,000 |
| Month 12 | 450,000 | 518,500 | -68,500 | 5,398,000 |
| Month 15 | 600,000 | 853,600 | -253,600 | 7,267,000 |
| Month 18 | 800,000 | 853,600 | -53,600 | 8,781,000 |
| Month 20 | 900,000 | 853,600 | +46,400 | 9,316,000 |
| Month 24 | 1,200,000 | 853,600 | +346,400 | 8,929,000 |

**Conservative breakeven:** Month 20 (when monthly revenue exceeds monthly burn)
**Maximum cumulative cash needed:** ~NIS 9.3M (~$2.6M) at Month 20

### 7.2 Funding Strategy Recommendation

| Round | Timing | Amount (NIS) | Amount (USD) | Purpose |
|-------|--------|-------------:|-------------:|---------|
| **Pre-Seed** | Month -6 | 1,500,000-2,000,000 | $415K-$555K | MVP build, initial team, legal setup, supply seeding |
| **Seed** | Month 3-6 | 5,500,000-7,500,000 | $1.5M-$2.1M | Growth team, marketing, 18-month runway to breakeven |
| **Innovation Authority Grant** | Month 0-3 | 750,000-2,500,000 | $208K-$694K | Non-dilutive, matches 50-60% of investment round |
| **TOTAL FUNDING NEEDED** | | **7,750,000-12,000,000** | **$2.15M-$3.33M** | |

### 7.3 Recommended Seed Round Size

**NIS 7,000,000 (~$1.95M) — target raise**

This provides:
- 18-22 months of runway at average burn rate
- Buffer for slower-than-expected growth (30% contingency built into burn)
- Enough to reach breakeven without needing a bridge round
- Aligned with Israeli seed round market (average seed: $4.2M; our raise is below average, appropriate for consumer marketplace)

**Dilution budget:** 15-25% equity for seed round (standard Israeli market).

### 7.4 Runway Analysis

| Scenario | Monthly Burn (avg) | Funding (NIS 7M) Lasts | Breakeven Month |
|----------|-------------------:|-----------------------:|----------------:|
| **Conservative** | 450,000 | 15.5 months | Month 20-24 |
| **Moderate** | 380,000 | 18.4 months | Month 16-20 |
| **Aggressive (faster revenue)** | 350,000 | 20 months | Month 12-16 |

**Key risk:** If revenue ramps slower than projected, the company may need a bridge round of NIS 2-3M around Month 15-18. The Innovation Authority grant can serve as this bridge.

---

## 8. ISRAELI STARTUP FUNDING LANDSCAPE 2025-2026

### 8.1 Market Context

- Israeli startups raised **$15.6B in 2025**, a major recovery driven by AI
- Pre-seed and seed rounds raised **$607M in H1 2025**, up 50% vs H2 2024
- Average seed round size: **$4.2M** (up from $3.1M in 2023)
- Median deal size reached a record **$10M** (skewed by larger rounds)
- ~5% of seed transactions are "mega-seeds" ($20M+) — not relevant for our category
- Fewer total deals, larger average size — VCs are more selective

### 8.2 Active Israeli VCs for Consumer/Marketplace Seed

| Fund | Focus | Seed Size | Notable Investments | Relevance |
|------|-------|----------|--------------------:|-----------|
| **Aleph** | Early-stage, $850M+ AUM | $2-8M | Lemonade, Melio, HoneyBook | Consumer marketplace experience |
| **TLV Partners** | Early-stage Israeli | $2-5M | monday.com (early), Pigment | Tech-first platforms |
| **Entree Capital** | Seed-Series A | $1-5M | Cato Networks, Stash | Consumer tech friendly |
| **Pitango** | Multi-stage | $3-10M | Outbrain, CyberArk | Larger seed rounds |
| **Viola Ventures** | Early-stage | $2-8M | ironSource, Payoneer | Consumer/marketplace |
| **lool Ventures** | Pre-seed/seed | $0.5-2M | Verbit, GlassesUSA | Smaller checks, hands-on |
| **Magma VC** | Seed | $1-4M | Resident, via | Consumer-friendly |
| **iAngels** | Syndicate/crowd | $0.5-2M | Various | Good for smaller rounds |

### 8.3 Israel Innovation Authority (IIA) Grants

**Highly relevant and recommended.**

| Program | Stage | Grant Amount | Grant % | Key Conditions |
|---------|-------|------------:|--------:|----------------|
| **Startup Fund — Pre-Seed** | Pre-Seed | Up to NIS 1.5M | 60% of round | Non-dilutive, no equity taken |
| **Startup Fund — Seed** | Seed | Up to NIS 5M | 50% of round | Non-dilutive, no equity taken |
| **Startup Fund — Round A** | Series A | Up to NIS 15M | 30% of round | Non-dilutive, no equity taken |

**Bonus:** +10% grant for underrepresented founders (women, Arab, Ultra-Orthodox) or periphery-based companies. A female founder would receive up to NIS 1.65M at pre-seed or NIS 5.5M at seed.

**Process:** Application undergoes due diligence by IIA technology experts. Approval provides risk mitigation signal for private investors.

**Strategic recommendation:** Apply for IIA pre-seed grant simultaneously with raising private capital. The grant can cover 50-60% of the pre-seed, reducing dilution significantly.

### 8.4 Other Funding Options

| Source | Amount | Notes |
|--------|-------:|-------|
| **Angel investors** | NIS 180K-720K ($50K-$200K each) | Israeli angel networks: iAngels, OurCrowd, Angels of TA |
| **Accelerators** | NIS 360K-720K ($100K-$200K) + services | Techstars TLV, MassChallenge Israel, 8200 EISP |
| **Crowdfunding** | Variable | PipelBiz (Israeli equity crowdfunding platform) |
| **Revenue-based financing** | Variable | Clearco, Pipe — once revenue is established |

---

## 9. KEY RISKS AND COST SENSITIVITIES

### 9.1 Biggest Cost Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| **Slower user growth** | Extends time to breakeven by 6-12 months, requiring bridge funding | Conservative marketing spend, focus on organic/referral channels |
| **Developer salary inflation** | Israeli dev salaries rising 5-10%/year | Lock in salaries with equity packages, consider remote/hybrid with non-TLV devs |
| **Background check costs at scale** | Re-verification every 3 months creates recurring burden | Negotiate volume pricing with Au10tix; explore if certificate validity can be extended |
| **Marketing CAC higher than projected** | Could double if paid channels underperform | Heavy investment in community/organic channels; WhatsApp group strategy is near-zero CAC |
| **Regulatory changes** | New Employment Service Law interpretation could restrict business model | Employment bureau license as insurance; ongoing legal counsel |

### 9.2 Cost Optimization Levers

1. **Remote-first team** — saves NIS 6,000-25,000/month in office costs
2. **IIA grant** — can fund 50-60% of pre-seed, reducing dilution and cash needs
3. **Hire outside Tel Aviv** — developers in Haifa, Beer Sheva, or remote are 15-25% cheaper
4. **Part-time/contractor model early** — use freelancers until product-market fit is validated
5. **Nannies self-serve background checks** — platform provides guidance but nanny handles the process and cost
6. **Open-source tools** — Meilisearch instead of Algolia, self-hosted analytics, Firebase for push notifications

---

## 10. EXECUTIVE SUMMARY

### The Numbers

| Metric | Value |
|--------|------:|
| **MVP team cost** | NIS 102,000/month (~$28K) |
| **Launch team cost** | NIS 234,000/month (~$65K) |
| **Scale team cost** | NIS 499,000/month (~$139K) |
| **Total funding needed (to breakeven)** | NIS 7-12M (~$2-3.3M) |
| **Recommended seed round** | NIS 7M (~$1.95M) |
| **Conservative breakeven** | Month 20-24 |
| **Blended CAC** | NIS 70-120 (~$19-33) |
| **Maximum monthly burn** | NIS 853,600 (~$237K) at scale |

### The Strategy

1. **Pre-Seed (NIS 1.5-2M):** Founders + IIA grant. Build MVP with 3.8-person team over 6 months.
2. **Seed (NIS 5.5-7.5M):** Raise from Israeli VC (Aleph, TLV Partners, Entree, or Magma). Scale team to 7-10. Aggressive user acquisition.
3. **IIA Grant:** Apply simultaneously — non-dilutive NIS 750K-2.5M that extends runway by 3-6 months.
4. **Breakeven target:** Month 20 at NIS 900K/month revenue, achievable with 5,000 paying families + 10 B2B contracts.

### Key Insight

The nanny platform has a **capital-efficient profile** compared to typical Israeli startups. The average Israeli seed round is $4.2M — our recommended raise of ~$2M is deliberately below this because:
- Consumer marketplace in a small market (Israel only initially)
- Low infrastructure costs (no hardware, no inventory)
- Strong organic acquisition potential (parenting is a viral topic)
- IIA grant can cover 50-60% of pre-seed costs

The biggest variable is **time to critical mass** — if the platform takes 6+ months longer than projected to reach 2,000+ active families, a bridge round will be necessary.

---

## SOURCES

### Israeli Salary Data
- [Glassdoor — Software Developer Salaries, Tel Aviv](https://www.glassdoor.com/Salaries/tel-aviv-yafo-israel-software-developer-salary-SRCH_IL.0,20_IM1002_KO21,39.htm)
- [Levels.fyi — Software Engineer Salaries, Israel](https://www.levels.fyi/t/software-engineer/locations/israel)
- [PayScale — Full Stack Developer, Israel](https://www.payscale.com/research/IL/Job=Full_Stack_Software_Developer/Salary)
- [ERI SalaryExpert — Full Stack Developer, Israel](https://www.salaryexpert.com/salary/job/full-stack-developer/israel)
- [Levels.fyi — Product Manager, Israel](https://www.levels.fyi/t/product-manager/locations/israel)
- [Glassdoor — UX Designer, Tel Aviv](https://www.glassdoor.com/Salaries/tel-aviv-yafo-israel-ux-designer-salary-SRCH_IL.0,20_IM1002_KO21,32.htm)

### Infrastructure & Cloud
- [AWS Israel (Tel Aviv) Region](https://aws.amazon.com/local/israel/)
- [DoiT — AWS Israel Region Price Comparison](https://www.doit.com/blog/aws-region-in-tel-aviv-israel-price-comparison-versus-other-regions/)
- [Sent.dm — Israel SMS Pricing 2025](https://www.sent.dm/resources/israel-sms-pricing)
- [Twilio — SMS Pricing Israel](https://www.twilio.com/en-us/sms/pricing/il)

### Background Checks
- [תעודת יושר — עלות ותהליך](https://www.haimlaw.com/%D7%AA%D7%A2%D7%95%D7%93%D7%AA-%D7%99%D7%95%D7%A9%D7%A8/)
- [Gov.il — Requests for Information from Israel Police](https://www.gov.il/en/pages/requests-for-information-from-the-israel-police)
- [Au10tix — Identity Verification](https://www.au10tix.com/)
- [Checkr — Israel Background Screening](https://help.checkr.com/s/article/7891551152535-Israel-Background-Screening)

### Marketing & CAC
- [Lebesgue — Facebook Ads CPM by Country 2026](https://lebesgue.io/facebook-ads/facebook-cpm-by-country)
- [AdAmigo — Meta Ads CPM/CPC by Country 2026](https://www.adamigo.ai/blog/meta-ads-cpm-cpc-benchmarks-by-country-2026)
- [DanGil — Google Ads in Israel](https://dangil.tech/advertising-on-google-ads-in-israel-2023/)
- [First Page Sage — Average CAC for Startups 2026](https://firstpagesage.com/reports/average-cac-for-startups-benchmarks/)
- [Business of Apps — User Acquisition Costs 2025](https://www.businessofapps.com/marketplace/user-acquisition/research/user-acquisition-costs/)

### Funding & VCs
- [Calcalist — Israel's Mega-Seed Era: 10 Biggest Seed Rounds 2025](https://www.calcalistech.com/ctechnews/article/b16iahzeze)
- [Calcalist — Israeli Startups Raised $15.6B in 2025](https://www.calcalistech.com/ctechnews/article/b1o113p8mbx)
- [Startup Nation Central — Israeli Tech Funding 2025](https://startupnationcentral.org/hub/blog/israeli-tech-funding-2025/)
- [Israel Innovation Authority — Startup Fund](https://innovationisrael.org.il/en/programs/startup-fund/)
- [SeedTable — 25 Best Active Seed Investors in Israel 2025](https://www.seedtable.com/seed-investors-israel)
- [Shizune — Top 50 Consumer VC Funds in Israel](https://shizune.co/investors/consumer-vc-funds-israel)

### Legal & Insurance
- [PZ Law — How Much Do Israel's Lawyers Charge](https://pz-law.co.il/en/blog-en/how-much-do-israeli-lawyers-charge/)
- [Aharoni Law — Registering a Corporation in Israel](https://aharonilaw.com/blog/registering-a-corporation-in-israel/)
- [WHINS — Tech E&O and Cyber Insurance for Startups 2025](https://www.whins.com/tech-eo-and-cyber-insurance-for-startups-2025-guide-to-protection-compliance/)
- [Vouch — Startup Insurance Costs](https://www.vouch.us/insurance101/start-up-insurance-costs-how-much-to-pay)

### Office Space
- [Native Israel — Office Space Tel Aviv 2025](https://www.nativeisrael.com/blog/office-space-tel-aviv)
- [Native Israel — Coworking Space Tel Aviv 2025](https://www.nativeisrael.com/blog/coworking-space-tel-aviv)

*This document provides cost estimates based on publicly available data and market research. Actual costs may vary. All figures should be validated with quotes from specific vendors before inclusion in a business plan or investor deck.*
