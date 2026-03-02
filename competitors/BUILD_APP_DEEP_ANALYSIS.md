# Build-App (בילד אפ) — Deep Competitive Intelligence Report

**Date:** March 2, 2026
**Analyst:** Competitive Intelligence Team
**Classification:** Internal — Strategic Planning

---

## Executive Summary

- **Build-App is the B2B market leader** for professional property management companies in Israel, self-described as "the most popular system for maintenance companies in Israel." Built by A Point Systems (founded 2011), it operates as a SaaS platform with ISO 27001 certification and a 5-person support team, serving management companies that oversee hundreds of buildings.
- **They are already expanding into volunteer vaad bayit territory** — their website explicitly mentions reducing "the burden on committee members" and targets both professional companies AND volunteer committees. However, their pricing (NIS 2,500+ setup, enterprise SaaS) and complexity make them impractical for a volunteer running a single 20-unit building.
- **Low direct threat to our free-tier strategy** — Build-App's DNA is B2B enterprise sales to professional management companies. Moving downmarket to serve individual volunteer committees at free/NIS 0 would cannibalize their premium pricing and confuse their brand. The risk is indirect: if they partner with more management companies who then offer committee tools as part of their managed service.

---

## Company Profile

| Field | Detail |
|---|---|
| **Legal Name** | A Point Systems Ltd (איי פוינט מערכות בע"מ) |
| **Product Name** | Build-App (בילד אפ) |
| **Website** | [build-app.co.il](https://www.build-app.co.il/) |
| **Parent Company** | [A Point Systems](https://www.apoint.co.il/?lang=en) |
| **Founded** | 2011 (A Point Systems); Build-App is a product within the company |
| **Founder/CEO** | Daniel Cohen — experienced Access & SQL Server developer |
| **HQ Address** | Halipid 12, Petach Tikva (Build-App); Habonim 5, Ramat Gan (A Point corporate) |
| **Team Size** | 11-50 employees (ZoomInfo), 5-person technical support team (website) |
| **Revenue** | Under $5M (ZoomInfo estimate) |
| **Funding** | None publicly disclosed — appears bootstrapped |
| **Other Products** | Business-App (business ERP), School-Master (educational institutions) |
| **Tech Stack** | Access & SQL Server core, WordPress/WooCommerce website, PHP, Cloudflare CDN, SaaS cloud platform |
| **Security** | ISO 27001 certified |
| **Contact** | 077-2060010, sales@apoint.co.il |

### Key Insight: A Point is a Database Shop, Not a Startup

A Point Systems is fundamentally a Microsoft Access/SQL Server consulting firm that productized their expertise into vertical SaaS products. Daniel Cohen's background is database development, not consumer product design. This means:
- Deep strength in data management, reporting, and enterprise workflows
- Weak on UX/UI, mobile-first design, and consumer-facing experiences
- Unlikely to pivot to a consumer-grade, free, WhatsApp-native product

**Sources:**
- [A Point Systems About Page](https://www.apoint.co.il/about-a-point/?lang=en)
- [Daniel Cohen LinkedIn](https://www.linkedin.com/in/apoint/)
- [ZoomInfo Company Profile](https://www.zoominfo.com/c/a-point-systems-ltd/426560152)

---

## Product Analysis

### Core Platform Features

Build-App is a comprehensive property management platform designed as a "One Stop Shop" for building management companies. Key modules:

**1. Collection Management (Gaviah)**
- Automated billing calculations for thousands of residents
- Automatic dunning letters via email and SMS
- Credit card processing with PCI compliance
- Standing order management
- Automatic check deposit system
- Real-time payment tracking dashboard
- "Smart Collection Manager" module (valued at NIS 3,970)

**2. Maintenance Management**
- Service request handling with automated SMS to maintenance staff
- Routine and preventive maintenance scheduling
- Inspection checklists and documentation
- Supplier database management
- Real-time status updates to residents

**3. Financial Management**
- Building-level income and expense tracking
- Budget management and anomaly detection
- One-click financial report generation
- BI dashboards with smart visualizations

**4. Communication & CRM**
- Automated resident notifications (email, SMS)
- Built-in messaging system with group chat
- Digital voting/polling capabilities
- Automatic CRM documentation of all interactions
- 2,000 SMS messages included in packages

**5. Mobile Applications**
- **Resident app** (iOS: Build App, App Store ID 1605492474; Android: com.apoint.tenantapp) — for payments and service requests
- **Maintenance staff app** — field operations and work orders
- **Supplier portal** — vendor management

**6. Additional Capabilities**
- Electric vehicle charging station management (modern feature)
- Multi-building management console for companies
- Data export and reporting
- GDPR compliance features

### App Store Presence

| Platform | Rating | Reviews | Last Updated |
|---|---|---|---|
| iOS (Apple App Store) | 3.5/5 | 14 ratings | August 9, 2023 (v2.0.08) |
| Android (Google Play) | Data unavailable | — | — |

**iOS App Review Themes:**
- Positive: "Really easy to use," highly recommended by some users
- Negative: "Few bugs, some features not working," maintenance issues unresolved for nearly a year, lack of responsiveness from support
- App size: 20.4 MB, requires iOS 11.0+

### Critical Observation: Stale Mobile App

The iOS app was last updated in **August 2023** — over 2.5 years ago. This is a significant red flag indicating:
- Mobile is not a priority (web-first platform)
- The resident-facing experience is likely dated
- Bug fixes reported by users may remain unresolved
- They may be losing to competitors with better mobile experiences

**Sources:**
- [Build-App Homepage](https://www.build-app.co.il/)
- [Build-App Smart Collection Page](https://www.build-app.co.il/smartcollection-tpl/)
- [Apple App Store - Build App](https://apps.apple.com/il/app/build-app/id1605492474)
- [Google Play - Build App](https://play.google.com/store/apps/details?id=com.apoint.tenantapp)

---

## Pricing & Business Model

### Publicly Disclosed Pricing (Smart Collection Package)

Build-App does not publicly list standard SaaS pricing, but their "Smart Collection" landing page reveals a promotional offer:

| Item | "Value" | Promo Price |
|---|---|---|
| Implementation project (4 weeks) | NIS 9,970 | Included |
| Smart collection app | NIS 9,970 | Included |
| Collection manager module | NIS 3,970 | Included |
| Service management module | NIS 970 | Included |
| Financial management module | NIS 790 | Included |
| Service staff mobile app (annual) | NIS 480 | Included |
| 2,000 SMS messages | NIS 360 | Included |
| **Total "Stated Value"** | **NIS 25,130** | — |
| **Promotional Price** | — | **NIS 2,500 + VAT** |

**Terms:** 10 months of access for up to 5 buildings + 2 complimentary months (12 months total)
**Guarantee:** 30-day money-back

### Pricing Model Analysis

- **Per-company pricing**, not per-building or per-unit
- **The NIS 2,500 promo** works out to ~NIS 208/month for up to 5 buildings — roughly NIS 42/building/month at the low end
- For companies managing 50+ buildings, the per-building cost drops dramatically (likely enterprise pricing not disclosed)
- The inflated "NIS 25,130 value" marketing tactic suggests the real market rate is likely NIS 200-500/month per management company depending on building count
- No free tier exists — this is exclusively a paid B2B product

### Revenue Model

- **SaaS subscription** — recurring monthly/annual fees from management companies
- **Implementation fees** — onboarding and setup for new clients
- **SMS packages** — overage charges beyond included messages
- **No transaction fees** — they do not take a cut of resident payments (this is a key differentiator from our model)

### Comparison to Our Pricing

| Metric | Build-App | Our Platform |
|---|---|---|
| Price to vaad bayit | NIS 200+ via management company | FREE |
| Revenue model | SaaS subscription | 1.5% transaction fee |
| Setup cost | NIS 2,500+ | NIS 0 |
| Minimum commitment | 10-12 months | None |
| Target buyer | Management company CFO | Volunteer committee chair |

**Sources:**
- [Build-App Smart Collection Pricing](https://www.build-app.co.il/smartcollection-tpl/)
- [Build-App Landing Page](https://www.build-app.co.il/sp/google1/)

---

## Market Position & Partnerships

### Market Claims

Build-App consistently positions itself as:
- "The most popular system for managing shared residential buildings in Israel"
- "The leading and established platform for management and maintenance companies"
- "The leading system in Israel" for property management companies

While exact market share data is not publicly available, these claims suggest a strong #1 or #2 position in the B2B professional management software segment.

### Known Clients

| Client | Type | Source |
|---|---|---|
| Eazy House (איזי האוס) | Leading management company, Tel Aviv & center | Website testimonial |
| Denya Maintenance (דניה אחזקה) | Management company | Website testimonial |
| Cleanext (קלינקסט) | Management company | Website testimonial |
| IsraHouse | Management company | Website recommendation |
| Findon Homes | Real estate/management (A Point client since 2014) | ZoomInfo |

The website displays "logos of numerous Israeli property management companies" but does not disclose the full client list or building count.

### Batim Portal Partnership

**Batim.org.il** is a major Israeli portal for building committees (vaad bayit) and shared building residents, operated in partnership with "The Association for Building Management." It offers:
- Database of management and maintenance companies
- Curated professional directories
- Articles on shared building topics
- Free services for committees and residents

**Partnership details (announced October 2021):**
- Build-App is listed as a recommended software vendor on the Batim portal
- Management companies signing up through Batim receive a bonus package of 2,000 SMS messages (valued at NIS 500)
- Batim endorsement gives Build-App credibility and distribution among management companies seeking software solutions

**Strategic significance:**
- This is a **B2B distribution channel** — Batim connects Build-App with management companies, NOT directly with volunteer committees
- The partnership gives Build-App visibility but not direct access to the ~300,000 self-managed buildings in Israel
- For our strategy: Batim portal is a potential partner for us too, if we can offer something compelling for their audience (volunteer committees)

**Sources:**
- [Batim Portal](https://www.batim.org.il/)
- [Batim-Build-App Partnership Announcement](https://www.batim.org.il/news/%D7%A9%D7%AA%D7%A4-%D7%91%D7%99%D7%9F-%D7%91%D7%AA%D7%99%D7%9D-%D7%9C%D7%9E%D7%A2%D7%A8%D7%9B%D7%AA-%D7%A0%D7%99%D7%94%D7%95%D7%9C-%D7%95%D7%90%D7%97%D7%96%D7%A7%D7%AA-%D7%9E%D7%91%D7%A0%D7%99/)
- [Batim Article: Can Software Replace Management Companies?](https://www.batim.org.il/articles/%D7%94%D7%90%D7%9D-%D7%AA%D7%95%D7%9B%D7%A0%D7%AA-%D7%A0%D7%99%D7%94%D7%95%D7%9C-%D7%91%D7%AA%D7%99%D7%9D-%D7%99%D7%9B%D7%95%D7%9C%D7%94-%D7%9C%D7%94%D7%97%D7%9C%D7%99%D7%A3-%D7%97%D7%91%D7%A8%D7%AA/)

---

## Strengths & Weaknesses

### Strengths

1. **Market Leadership in B2B** — Established as the go-to platform for professional management companies. Industry recognition and Batim partnership reinforce credibility.

2. **Comprehensive Feature Set** — Covers the full spectrum of building management: collection, maintenance, financials, CRM, reporting, mobile apps for all stakeholders.

3. **ISO 27001 Security** — Enterprise-grade security certification is a significant trust signal for management companies handling financial data.

4. **Bootstrapped & Profitable** — No venture pressure, no burn rate problem. A Point has been in business since 2011 and appears sustainably profitable.

5. **Deep Domain Expertise** — 10+ years building property management software specifically for the Israeli market. Deep understanding of local regulations, collection practices, and building law.

6. **BI & Reporting** — Strong analytics capabilities (smart graphs, dashboards) that management companies need for multi-building oversight.

7. **Proven Collection Engine** — The "Smart Collection Manager" is battle-tested across many management companies and thousands of residents.

### Weaknesses

1. **Stale Mobile Experience** — iOS app last updated August 2023 (3.5/5 stars, only 14 ratings). Mobile is clearly an afterthought. User reviews cite bugs and unresolved issues.

2. **Legacy Technology** — Built on Microsoft Access/SQL Server foundations. While functional, this is not a modern tech stack. No evidence of API-first architecture, real-time capabilities, or modern frontend frameworks.

3. **No Consumer Brand** — Residents don't choose Build-App; their management company does. Zero brand recognition among the 300,000+ self-managed buildings.

4. **Enterprise Complexity** — The platform is designed for companies managing dozens/hundreds of buildings. A volunteer managing 1 building would be overwhelmed by the interface.

5. **No WhatsApp Integration** — No evidence of WhatsApp-based communication. Relies on SMS and email — increasingly outdated channels in Israel where WhatsApp dominance is near-universal.

6. **Small Team** — 11-50 employees (likely closer to 15-20 given sub-$5M revenue) limits their ability to develop new market segments while maintaining the core B2B product.

7. **High Barrier to Entry** — NIS 2,500+ setup, 10-month commitment, and 4-week implementation process. Impossible for a volunteer committee to adopt on a whim.

8. **No Self-Serve Onboarding** — Every client requires a demo call and implementation project. No self-service signup flow.

9. **Hebrew-Only Focus** — While appropriate for the market, the underlying technology (Access/SQL) limits internationalization potential if they ever wanted to expand.

---

## Expansion Risk Assessment

### Could Build-App Move Downmarket to Target Volunteer Vaad Bayit?

**Overall Risk: LOW-MEDIUM (25-35% probability in next 2 years)**

#### Evidence FOR Expansion (Risk Signals)

1. **Website already mentions volunteer committees** — Their marketing explicitly includes "reducing the burden on committee members" and lists vaad bayit as a target user alongside management companies. This is at least aspirational positioning.

2. **Promotional pricing exists** — The NIS 2,500/year package for up to 5 buildings suggests they have experimented with lower price points. They could theoretically create a single-building tier.

3. **Batim partnership** — Batim.org.il serves both professional companies AND volunteer committees. If Batim pushed Build-App to their volunteer audience, it could create downmarket distribution.

4. **Market size opportunity** — The ~300,000 self-managed buildings in Israel represent an enormous untapped market that any incumbent would eventually eye.

#### Evidence AGAINST Expansion (Safety Signals)

1. **DNA mismatch** — A Point is a B2B database consulting firm. Their entire sales motion (demo calls, implementation projects, account management) is built for enterprise clients, not volunteers.

2. **Cannibalization risk** — Offering a free or cheap tier for individual buildings would undermine their NIS 200+/month pricing to management companies who serve those same buildings.

3. **Product complexity** — The platform is designed for multi-building management with features like BI dashboards, supplier management, and cross-building reporting. Simplifying this for a single volunteer is a massive product effort.

4. **Support burden** — Serving 10,000 free volunteer committees requires 100x the support tickets of 100 paying management companies. Their 5-person support team cannot handle this.

5. **No self-serve capability** — They have no self-service onboarding, no freemium funnel, no consumer marketing expertise. Building this from scratch would take 12-18 months minimum.

6. **Mobile weakness** — The volunteer segment is mobile-first. Their stale iOS app (last updated 2023) and apparent lack of mobile development investment makes them uncompetitive for this audience.

7. **No transaction-fee infrastructure** — Their revenue model is SaaS subscriptions. Switching to a transaction-fee model (like ours) would require integrating payment processing at a completely different level.

### Scenario Analysis

| Scenario | Probability | Impact | Response |
|---|---|---|---|
| Build-App ignores volunteer segment | 50% | None | Continue as planned |
| Build-App creates a "lite" tier for volunteers | 20% | Medium | Beat them on UX, WhatsApp, and free pricing |
| Build-App partners with a consumer platform | 15% | Medium-High | Move fast, lock in user base before they execute |
| Build-App acquires a competitor in our space | 10% | High | Differentiate on technology and community |
| Build-App launches a free consumer product | 5% | Very High | Unlikely — would cannibalize core business |

### Timeline Assessment

Even if Build-App decided TODAY to target volunteer committees:
- Product simplification: 6-12 months
- Self-serve onboarding: 3-6 months
- Mobile app modernization: 6-12 months
- Consumer marketing: 3-6 months
- **Total: 12-18 months minimum** to be competitive in our segment

This gives us a substantial first-mover window.

---

## How to Win / Coexist

### Strategy 1: Occupy the Vacuum (Primary)

Build-App serves management **companies**. We serve volunteer **committees**. These are fundamentally different buyers:

| Dimension | Build-App's Customer | Our Customer |
|---|---|---|
| Buyer | CFO/COO of management company | Volunteer committee chair (often retired, non-technical) |
| Decision process | Formal procurement, demos, contracts | WhatsApp group discussion, 5-minute signup |
| Buildings per customer | 50-500 | 1 |
| Budget | NIS 200-500/month from business revenue | NIS 0 from personal pocket |
| Technical sophistication | High (accounting, ERP, BI) | Low (wants simplicity, WhatsApp familiarity) |
| Switching cost | High (multi-building migration, data export) | Low (can try and leave freely) |

**Action:** Position ourselves as "the platform for buildings that DON'T have a management company." This is a segment Build-App has no incentive or ability to serve at free.

### Strategy 2: WhatsApp-Native Moat

Build-App communicates via SMS and email. Israeli residents live on WhatsApp. Our WhatsApp-native architecture (pay via link, no app download) creates an experience Build-App cannot replicate without fundamental re-architecture.

**Action:** Make WhatsApp the center of every interaction. Residents should never need to download an app, create an account, or open a website. This is the opposite of Build-App's model (dedicated apps for residents, suppliers, maintenance staff).

### Strategy 3: Zero-Friction Onboarding

Build-App requires: demo call > 4-week implementation > NIS 2,500 payment > training. Our onboarding should be: WhatsApp message > 3 minutes > first payment collected.

**Action:** Invest heavily in self-serve onboarding. The volunteer committee chair should go from "I heard about this" to "collecting payments" in under 5 minutes, without talking to anyone.

### Strategy 4: Potential Partnership (Upside Play)

Build-App and our platform could be complementary:
- Management companies using Build-App manage ~30% of Israeli buildings
- The other ~70% are self-managed by volunteer committees (our market)
- If a volunteer committee grows and hires a management company, they "graduate" to Build-App
- If a management company loses a client, the building committee could "downgrade" to our free platform

**Possible partnership angles:**
1. **Referral agreement:** We refer buildings that outgrow our platform to Build-App. They refer buildings that fire their management company to us.
2. **Data migration:** Offer easy export from our platform to Build-App format, making us a feeder into their ecosystem.
3. **Co-listing on Batim:** Both platforms listed on Batim.org.il — us for volunteer committees, them for management companies.

**Action:** After reaching 500+ buildings, approach Build-App/A Point with a partnership proposal. Frame it as "we grow your pipeline by professionalizing volunteer committees who eventually need a management company."

### Strategy 5: Speed as Defense

Build-App has been around since 2011 and has ~15 years of enterprise features. We cannot out-feature them. But we can out-speed them:

1. **Launch in 6-8 weeks** (before they could even plan a downmarket move)
2. **Reach 1,000 buildings in 6 months** (network effects make switching harder)
3. **Build community lock-in** (WhatsApp groups, building-to-building referrals)
4. **Iterate weekly** on committee feedback (vs. their quarterly enterprise release cycle)

### Strategy 6: Monitor & Trigger Points

Watch for these signals that Build-App is moving into our territory:

| Signal | Monitoring Method | Response Trigger |
|---|---|---|
| New "free" or "lite" tier on their website | Monthly website check | Accelerate feature development |
| Mobile app update after 2+ year gap | App Store alerts | Assess if targeting consumers |
| New marketing targeting "vaad bayit" | Google Alerts on Hebrew terms | Counter-marketing campaign |
| Hire of consumer product/growth roles | LinkedIn monitoring | Prepare competitive positioning |
| Partnership with WhatsApp/payment provider | News monitoring | Accelerate WhatsApp feature rollout |
| Batim portal starts promoting Build-App to committees | Monthly Batim check | Approach Batim for our own partnership |

---

## Appendix: Build-App vs. Our Platform — Feature Comparison

| Feature | Build-App | Our Platform (Planned) |
|---|---|---|
| **Price** | NIS 2,500+/year | FREE (1.5% on payments) |
| **Target** | Management companies | Volunteer committees |
| **Onboarding** | 4-week implementation | 5-minute self-serve |
| **Collection** | Enterprise billing engine | WhatsApp payment links |
| **Maintenance** | Full work order system | Simple request via WhatsApp |
| **Financial Reporting** | BI dashboards, smart graphs | Simple income/expense summary |
| **Communication** | SMS + email | WhatsApp-native |
| **Mobile App** | Dedicated apps (stale, 3.5 stars) | No app needed (WhatsApp) |
| **Multi-building** | Yes (core strength) | Yes (but optimized for single) |
| **Security** | ISO 27001 | Standard SaaS security |
| **Hebrew** | Yes | Yes |
| **Self-serve** | No (requires demo/implementation) | Yes (core differentiator) |
| **EV Charging** | Yes | No (not needed for small buildings) |
| **Supplier Management** | Full module | Basic directory |
| **Credit Card Processing** | PCI-compliant, check deposit | Via Meshulam (WhatsApp link) |

---

## Key Takeaways

1. **Build-App is NOT our direct competitor** — they are a B2B enterprise platform for professional management companies. Our market is the ~70% of Israeli buildings managed by volunteer committees.

2. **Their weaknesses are our opportunities** — stale mobile apps, no WhatsApp, no self-serve, enterprise pricing. Every weakness aligns perfectly with our differentiators.

3. **Partnership > Competition** — The best outcome is coexistence where we own the volunteer segment and they own the professional segment, with a referral bridge between.

4. **Speed matters** — Their 2.5-year iOS app staleness and database-shop DNA suggest slow product iteration. We can capture the volunteer market before they even consider competing.

5. **Monitor the Batim partnership** — If Batim starts actively pushing Build-App to volunteer committees (rather than just management companies), that's our signal to act on a counter-partnership.

---

*Report compiled March 2, 2026. All sources verified at time of writing.*
