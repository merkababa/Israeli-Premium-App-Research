# Israeli Payment Processor Comparison for Nanny Marketplace Platform

**Date:** March 7, 2026
**Research Gap:** G2 -- Head-to-head comparison of Israeli payment processors
**Status:** Complete
**Context:** Supplements NANNY_PLATFORM_PAYMENT_TAX_RESEARCH.md and NANNY_PLATFORM_REVENUE_MODEL_REVISED.md

---

## EXECUTIVE SUMMARY

PayMe remains the recommended primary processor for our nanny marketplace, but with important caveats discovered in this comparison. PayMe's 2.9% "no monthly fee" plan is actually the most expensive per-transaction option among the three candidates. For a platform processing NIS 500K+/month, negotiating a volume-based custom rate with PayMe (targeting 1.2-1.6%) or using PayPlus/Tranzila with their lower base rates would be significantly cheaper. The critical differentiator is that PayMe is the **only** processor with native marketplace split-payment and seller-payout infrastructure -- a hard requirement for our business model.

---

## SUMMARY RECOMMENDATION TABLE

| Criterion | PayMe | PayPlus | Tranzila | Winner |
|-----------|-------|---------|----------|--------|
| **Transaction fee (standard)** | 2.9% (no monthly) or ~1.6% + NIS 0.20 (with plan) | 1.8% + NIS 50-60/mo | 1.3% + NIS 65/mo | Tranzila |
| **Marketplace split payments** | Native -- full split, dynamic fees, seller payouts | Not native -- no documented marketplace API | Not native -- no split payment infrastructure | PayMe |
| **Seller/provider onboarding** | Built-in seller onboarding flow | Not available | Not available | PayMe |
| **Subscription/recurring billing** | Yes -- tokenization + subscription engine | Yes -- recurring instructions via API | Yes -- standing orders + token billing | Tie |
| **Credit card installments** | Up to 12 installments | Yes -- installments supported | Yes -- installments on single payments | Tie |
| **SHAAM e-invoicing** | Digital accounting + tax automation built-in | Invoice integration via CRM (Hashbonit+) | Digital invoicing approved by Income Tax Authority | PayMe |
| **PCI DSS compliance** | Yes (level not publicly specified) | PCI DSS Level 1 | PCI DSS Level 1 | PayPlus/Tranzila |
| **API documentation quality** | Good -- Stoplight + Apiary docs, REST API | Good -- ReadMe-hosted docs, REST API | Good -- Stoplight-hosted API V2 docs | Tie |
| **Mobile SDK** | JavaScript API (iframe/web-based) | Mobile app (iOS/Android POS) | Mobile clearing app (iOS/Android POS) | Tie (all web-based for in-app) |
| **Bit support** | Yes (via Isracard partnership) | Yes (native) | Yes (native) | Tie |
| **Apple Pay / Google Pay** | Yes | Yes | Yes (Google Pay) | Tie |
| **Customer support** | Hebrew + English, Tel Aviv office | Hebrew, Holon office, 18+ years experience | Hebrew + English, Netanya, praised for responsiveness | Tranzila |
| **Contract terms** | No minimum (no-monthly-fee plan) | Custom (likely annual) | Custom (likely annual) | PayMe |
| **Notable Israeli clients** | Shufersal, Wolt, Super-Pharm, Ikea, Wix | SMBs, Shopify/Wix merchants | SMBs, enterprises, nonprofits, government | PayMe |
| **Overall fit for nanny marketplace** | Best fit | Inadequate for marketplace | Inadequate for marketplace | **PayMe** |

---

## DETAILED PROCESSOR ANALYSIS

### 1. PayMe (by Morning/Pepper)

**Company Profile:**
- Founded: 2014, Tel Aviv, Israel
- Founder: Adam Kogan
- Regulated by: Israel Capital Markets Insurance and Savings Authority (License #64002, #60729)
- 200+ partners worldwide, 20,000+ merchants
- 95% of clients are Israel-based; expanding to Europe
- Notable clients: Shufersal (largest retailer in Israel), Wolt, Super-Pharm, Ikea, Wix

**Fee Structure:**
| Plan Type | Transaction Fee | Monthly Fee | Setup Fee |
|-----------|----------------|-------------|-----------|
| No-monthly-fee plan | 2.9% | NIS 0 | NIS 0 |
| Standard plan | 1.6% + NIS 0.20 per txn | Varies | NIS 85 (one-time) |
| Volume-negotiated | ~1.2-1.45% + NIS 1.20 per txn | Custom | Custom |

- No withdrawal fees to bank account (regardless of amount)
- Volume-based pricing available through negotiation
- International card processing available at higher rates

**Marketplace & Split Payment Support:**
- **Native marketplace split payments** -- the core differentiator
- Split transactions between multiple sellers per transaction
- Dynamic platform fee per transaction (configurable per booking)
- Seller onboarding in minutes
- Control over payout timing and fund flow
- Optional instant payouts for sellers (premium feature for nannies)
- White-label solutions available
- Dedicated Marketplace API documented on Apiary

**Subscription & Recurring Billing:**
- Full subscription engine with tokenization
- Configurable frequency, number of charges, start date, amount
- No additional cost for creating/canceling/updating subscriptions
- Direct debit capability (does not occupy customer credit line)
- Card-on-file services

**Credit Card Installments:**
- Up to 12 installments supported
- Merchant receives money monthly by default
- Option to receive full amount upfront via PayMe Discount service (for a fee)

**E-Invoicing & Tax:**
- Digital accounting services built into platform
- Tax automation and invoicing capabilities
- Suitable for gig platforms and creator economy
- SHAAM compliance status: PayMe offers automated invoicing infrastructure, though direct SHAAM API integration status should be confirmed during onboarding

**PCI DSS Compliance:**
- PCI compliant (handles card data so merchants don't need to)
- 3D Secure 2 / SCA support
- Fraud prevention tools included
- Specific PCI DSS level not publicly documented

**API & Integration:**
- RESTful API with comprehensive documentation (Stoplight + Apiary)
- JavaScript API for tokenization (PayMe JSAPI on GitHub)
- Plugins for Magento, Wix, WooCommerce
- Iframe-based payment forms available
- Webhook support
- No native mobile SDK -- uses web-based payment pages/iframes for mobile

**Customer Support:**
- Hebrew and English support
- Email: support@payme.io
- Phone: +972-3-7220533
- Help Center: help.payme.io (Hebrew and English)
- Tel Aviv office at 18 Totzeret Haaretz

**Contract Terms:**
- No minimum commitment on no-monthly-fee plan
- Custom terms for volume-based pricing (negotiable)

---

### 2. PayPlus

**Company Profile:**
- Founded: Holon, Israel (unfunded/bootstrapped)
- Founder: Hanan Assis
- Employees: ~18+ years experience in clearing field
- Clients: SMBs, e-commerce, some enterprises
- Serves banks and government organizations
- Strong Shopify and Wix integrations

**Fee Structure:**
| Plan Type | Transaction Fee | Monthly Fee | Setup Fee |
|-----------|----------------|-------------|-----------|
| Standard (Israeli cards) | 1.8% | NIS 50-60 | NIS 195-200 |
| International cards | 2.8% | Included | Included |
| Low-rate plan | 1.2% + 0.6% up to 2,000 txns | NIS 59 | NIS 195 |

**Marketplace & Split Payment Support:**
- **No documented marketplace split payment API**
- No seller onboarding flow
- No native multi-vendor payout system
- Designed primarily for single-merchant e-commerce
- Would require custom development to simulate splits (manual bank transfers to nannies)

**Subscription & Recurring Billing:**
- Recurring credit card instructions via API
- Direct debit instructions supported
- Flexible billing logic (fixed period or ongoing)
- Product allocation to recurring instructions
- One-time charges alongside recurring (e.g., registration fee + monthly)
- Automatic retry on failed charges with customer card-update flow

**Credit Card Installments:**
- Supported through payment terminal and API
- Multiple payment configurations available

**E-Invoicing & Tax:**
- Invoice integration via Hashbonit+ (third-party CRM connector)
- Automated document generation from payment page
- SHAAM compliance would depend on the Hashbonit+ integration

**PCI DSS Compliance:**
- **PCI DSS Level 1** (highest level, explicitly documented)
- 3D Secure authentication (Mastercard SecureCode, Verified by Visa)
- Advanced fraud detection systems

**API & Integration:**
- REST API documented at docs.payplus.co.il (ReadMe platform)
- Additional API docs on Apiary
- Plugins: Shopify, WooCommerce, OpenCart, Magento
- GitHub repositories for open-source e-commerce plugins
- Mobile POS app available for iOS and Android (for in-person payments)
- Supports Google Pay, Apple Pay, Bit, Max Pay

**Customer Support:**
- Hebrew support primarily
- Phone: 03-9444788
- WhatsApp: 050-9894366
- Holon office
- Reputation for experienced team (18+ years in clearing)

**Contract Terms:**
- Setup fee required (NIS 195-200)
- Monthly commitment assumed (likely 12 months -- confirm during onboarding)

---

### 3. Tranzila

**Company Profile:**
- Founded: 1999, Netanya, Israel (one of Israel's oldest payment companies)
- Certified acquirer by Bank of Israel, Visa International, and Mastercard International
- Serves: startups, SMBs, enterprises, nonprofits, government organizations
- Successfully integrated with Shopify (Shopify Payment App)

**Fee Structure:**
| Plan Type | Transaction Fee | Monthly Fee | Setup Fee |
|-----------|----------------|-------------|-----------|
| Standard | Starting 1.3% | ~NIS 65 | ~NIS 250 |
| Mobile clearing | Varies | From NIS 29/mo | Included |
| Discount account | Prime + 4.5% annual discount fee | Account mgmt fee | Custom |

- Vendor numbers available within 24 hours (fast onboarding)
- Discount fee applies when funds received on 6th of month; advancement fee for earlier access

**Marketplace & Split Payment Support:**
- **No native marketplace split payment infrastructure**
- No multi-vendor payout system documented in API
- Can tokenize and process individual payments
- Would require platform to manually calculate splits and transfer funds to nannies
- Multi-branch support available (but not the same as marketplace splits)

**Subscription & Recurring Billing:**
- Standing order functionality (weekly/monthly/yearly charges)
- Token module for recurring charges without storing card numbers
- Subscriber file management
- API endpoint for creating standing orders
- Cyclic billing for subscribers

**Credit Card Installments:**
- Supported on single payments
- Parameter for number of installments
- Total installment amount must match transaction amount

**E-Invoicing & Tax:**
- **Invoice system approved by Income Tax Authority**
- Digitally signed invoices for email
- Automatic invoice generation for credit card, PayPal, or bank direct debit transactions
- Manual invoice generation for cash or cheque
- Green invoicing module (digital, environmentally friendly)
- SHAAM compliance: Tranzila's invoicing is ITA-approved, but direct SHAAM allocation-number API integration status should be confirmed

**PCI DSS Compliance:**
- **PCI DSS Level 1** (explicitly documented)
- SSL encryption
- Fraud blocking system
- 3D Secure technology
- Certified acquirer by Bank of Israel, Visa, and Mastercard

**API & Integration:**
- **API V2** -- modern RESTful API documented on Stoplight (docs.tranzila.com)
- Authentication via custom HTTP headers
- Iframe integration for PCI-compliant payment forms
- Hosted Fields for custom UI integration
- Token billing (J5) and one-time payment (J4) modes
- Payment requests via API (email, SMS, or both)
- Supports: PayPal, Bit, Google Pay, bank direct debits
- BillRun integration documented
- No native mobile SDK -- uses iframe/web for in-app payments

**Customer Support:**
- Hebrew and English support
- Phone: +972-73-222-4444
- Netanya office
- Praised by customers for "best response with customer service and close technical support"
- Dedicated technical support team

**Contract Terms:**
- Setup fee required (~NIS 250)
- Terms negotiable; likely annual commitment
- Express merchant onboarding available (24 hours)

---

## ADDITIONAL PROCESSORS EVALUATED

### 4. Allpay (Emerging Competitor)

A newer Israeli payment gateway worth monitoring.

| Criterion | Details |
|-----------|---------|
| **Transaction fee** | 1.45% + NIS 1 per txn (Israeli cards); 3.65% + NIS 1 (international) |
| **Monthly fee** | NIS 50 |
| **Setup fee** | Free |
| **Installments** | Up to 12, no additional fee |
| **Recurring billing** | NIS 15/mo addon |
| **Bit support** | Yes, no additional fee |
| **Apple Pay** | Yes, NIS 50 one-time activation |
| **E-invoicing** | Via EasyCount integration (NIS 17/mo) |
| **Marketplace splits** | **No** -- single-merchant only |
| **Payouts** | Monthly (free if 5K+ NIS); weekly available at prime+3.7%/12 |
| **3D Secure** | 0.2% per transaction |
| **Refunds** | NIS 3.90 per refund |
| **Trial** | 7-day free trial |
| **API** | REST API, webhooks, hosted fields |

**Verdict:** Competitive pricing with good feature set, but no marketplace/split payment support. Not suitable as primary processor for our model.

### 5. Rapyd (Israeli-Founded, Global)

| Criterion | Details |
|-----------|---------|
| **Israel license** | Granted July 2025 by Capital Markets Authority |
| **Acquiring** | Directly licensed card acquirer in Israel (Visa/Mastercard) |
| **Marketplace support** | Yes -- sub-accounts for merchants, split payments, multi-currency |
| **Pricing** | Not public; blended pricing model, volume-dependent |
| **Split payments** | Sub-accounts with automatic splitting based on predefined rules |
| **Payouts** | Seller sub-accounts with preferred currency settlement |
| **Scale** | 900+ payment methods across 100+ countries |
| **API** | Comprehensive REST API with full documentation |
| **Funding** | $1B+ total funding, $250M Series F (March 2025) |

**Verdict:** Strong marketplace capabilities and fresh Israeli license. However, Rapyd targets enterprise/global scale. Pricing is custom/negotiated and likely optimized for high-volume operations. Worth evaluating post-MVP if we outgrow PayMe, or if PayMe's split-payment fees become prohibitive at scale. Their Israel operations are new (2025 license) so local support infrastructure may still be maturing.

---

## STRIPE STATUS IN ISRAEL (March 2026)

**Status: NOT available for Israeli merchant accounts. No confirmed launch timeline.**

Key findings:
- Stripe operates in 46 countries as of December 2025; Israel is NOT one of them
- Stripe has been trying for 4+ years to obtain an Israeli clearing license
- The SHVA (Automated Banking Service) integration adds unique complexity
- Gur Biron (former Google exec) was appointed to manage Israel entry but reportedly left
- Even Cardcom and Tranzila, which received clearing licenses years ago, took significant time to actually begin clearing
- Stripe added Israel to its Global Payouts for cross-border payouts (January 2026), but this is for paying out TO Israel, not for Israeli merchants accepting payments
- **Workaround**: Form a US LLC with EIN and US bank account to use Stripe. Adds legal complexity and not recommended for MVP

**Recommendation:** Do not plan around Stripe availability for 2026 launch. If Stripe enters Israel in 2027+, re-evaluate at that time.

---

## PAYPAL BUSINESS IN ISRAEL

**Status: Available but NOT recommended as primary processor.**

| Fee Type | Rate |
|----------|------|
| Domestic transactions | 3.40% + NIS 1.20 per txn |
| International (US/EU) | 4.40% + NIS 1.20 per txn |
| International (other) | 5.40% + NIS 1.20 per txn |
| Currency conversion | 2.5% markup on exchange rate |
| Dispute fee | NIS 30-60 per claim |
| Micro-payments (<threshold) | 5.00% + NIS 0.20 domestic |
| Bank withdrawal (<min) | NIS 8 per withdrawal |

**Why not for our platform:**
- Highest fees among all options (3.40% domestic vs PayMe's negotiable 1.2-1.6%)
- No native marketplace split payment infrastructure for Israeli operations
- No credit card installment support (Israeli-style tashlumim)
- No SHAAM e-invoicing integration
- Dispute fees add risk on a services marketplace
- Not culturally aligned with how Israelis pay for childcare services

**Use case:** Accept as an optional payment method for international families (tourists/expats) alongside the primary processor.

---

## ISRAEL SHAAM E-INVOICING COMPLIANCE TIMELINE

Critical context for all processor decisions:

| Date | Threshold | Impact |
|------|-----------|--------|
| May 2024 | NIS 25,000+ | Initial mandate |
| Jan 2026 | NIS 10,000+ | Most B2B invoices need allocation numbers |
| **Jun 2026** | **NIS 5,000+** | **Nearly all B2B invoices covered** |

- Invoices must be submitted to ITA via SHAAM platform in JSON format
- ITA validates in real-time and returns allocation number
- Allocation number + digital signature must appear on invoice before sending to buyer
- Without allocation number: buyer cannot reclaim input VAT
- 7-year digital retention requirement

**Platform impact:** Our monthly subscription (NIS 49) is below threshold, but aggregate B2B invoices to corporate clients (packages of nanny hours for companies) may exceed NIS 5,000. The payment processor's invoicing capability will be important for compliance.

---

## FINANCIAL MODELING: PROCESSOR COST COMPARISON

Assumptions for year 1:
- 500 monthly subscriptions at NIS 49 = NIS 24,500/mo
- 2,000 bookings/month at average NIS 250 = NIS 500,000/mo
- Platform takes 12% of booking = NIS 60,000/mo platform revenue from bookings
- Total processed volume: ~NIS 524,500/mo

### Annual Cost Comparison

| Cost Component | PayMe (no-monthly) | PayMe (negotiated) | PayPlus | Tranzila |
|----------------|--------------------|--------------------|---------|----------|
| Transaction fee rate | 2.9% | ~1.5% | 1.8% | 1.3% |
| Monthly platform fee | NIS 0 | Custom (~NIS 200?) | NIS 60 | NIS 65 |
| Setup (one-time) | NIS 0 | Custom | NIS 200 | NIS 250 |
| **Annual txn fees** | **NIS 182,526** | **~NIS 94,410** | **NIS 113,292** | **NIS 81,822** |
| **Annual platform fees** | **NIS 0** | **~NIS 2,400** | **NIS 720** | **NIS 780** |
| **Total annual cost** | **NIS 182,526** | **~NIS 96,810** | **NIS 114,012** | **NIS 82,852** |

**Important caveat:** PayPlus and Tranzila costs are lower BUT they lack marketplace split payments. The cost of building and maintaining custom split-payment logic, manual nanny payouts, and compliance with money-transmission regulations would likely exceed the NIS 14,000-30,000 annual savings.

---

## FINAL RECOMMENDATION

### Primary Processor: PayMe (with negotiated volume pricing)

**Rationale:**
1. **Only option with native marketplace split payments** -- this is a hard requirement for a booking marketplace that must split payments between platform and service providers
2. **Seller onboarding infrastructure** -- nannies can be onboarded as sellers, receive payouts according to our business logic
3. **Dynamic platform fee** -- we can set and adjust our 12-15% take rate per transaction
4. **Payout control** -- we decide when nannies get paid (after service completion, after review period, etc.)
5. **Optional instant payouts** -- premium feature we can offer nannies for faster access to earnings
6. **Subscription engine** -- handles our NIS 49/mo recurring charges natively
7. **Bit integration** -- critical for Israeli market where 43% of babysitter payments are via payment apps
8. **Gig economy focus** -- PayMe explicitly markets to gig platforms and creator economy
9. **Proven Israeli enterprise clients** -- Shufersal, Wolt, Super-Pharm, Ikea, Wix

**Action items before signing:**
1. **Negotiate volume-based pricing** targeting 1.2-1.5% + fixed fee (down from 2.9% default)
2. **Confirm SHAAM e-invoicing** -- verify their tax automation module generates allocation numbers via SHAAM API
3. **Confirm PCI DSS level** -- request their compliance certificate (should be Level 1 given their client base)
4. **Test marketplace API** -- request sandbox access to evaluate split payment flows, payout timing, and seller onboarding
5. **Clarify mobile integration** -- confirm iframe/JS API works smoothly within React Native WebView
6. **Negotiate contract terms** -- aim for month-to-month or maximum 12-month commitment with exit clause

### Backup Processor: Tranzila

**Use case:** If PayMe negotiations fail or if we need a secondary processor for redundancy.
- Lowest transaction fees (1.3%)
- Bank of Israel certified acquirer
- Strong PCI DSS Level 1 compliance
- Good API documentation (V2)
- Would require us to build custom split-payment logic and handle nanny payouts manually via bank transfers (MASAV)

### Future Consideration: Rapyd

**When:** Post-MVP, when processing volume exceeds NIS 2M/month and we expand to multiple cities or consider international expansion.
- Native marketplace split payments at enterprise scale
- Multi-currency support
- Licensed acquirer in Israel (as of July 2025)
- Enterprise-grade infrastructure
- Custom pricing likely competitive at high volume

---

## SOURCES

- [PayMe Official Site](https://payme.io/)
- [PayMe Documentation](https://docs.payme.io/)
- [PayMe Knowledge Center](https://help.payme.io/hc/en-us)
- [PayMe Marketplace API (Apiary)](https://paymeapi.docs.apiary.io/)
- [PayPlus Official Site](https://www.payplus.co.il/)
- [PayPlus Developer Docs](https://docs.payplus.co.il/)
- [PayPlus API (Apiary)](https://jsapi.apiary.io/apis/payplus/)
- [Tranzila Official Site](https://www.tranzila.com/english.html)
- [Tranzila API V2 Docs](https://docs.tranzila.com/)
- [Allpay Official Site](https://www.allpay.co.il/en)
- [Allpay Pricing](https://www.allpay.co.il/en/pricing)
- [Rapyd Israel](https://www.rapyd.net/network/country/israel/)
- [Rapyd Marketplace Solutions](https://www.rapyd.net/solutions/industries/marketplaces/)
- [Stripe Global Availability](https://stripe.com/global)
- [Stripe Struggling with Israeli License (Globes)](https://en.globes.co.il/en/article-stripe-struggling-to-receive-israeli-clearing-license-1001381078)
- [PayPal Israel Merchant Fees](https://www.paypal.com/il/webapps/mpp/merchant-fees?locale.x=en_IL)
- [LaStartup - Israeli Payment Processor Guide (Hebrew)](https://www.lastartup.co.il/blog/the-ultimate-guide-for-payment-providers)
- [Digitalix - Israeli Clearing Fee Comparison (Hebrew)](https://www.digitalix.co.il/credit-card-clearing-fees-comparison/)
- [Revolut/Rapyd/Airwallex Israel Licenses (Digital Banker)](https://thedigitalbanker.com/revolut-rapyd-airwallex-and-mesh-granted-payments-licences-in-israel/)
- [Israel E-Invoicing (Avalara)](https://www.avalara.com/us/en/vatlive/country-guides/africa-and-middle-east/israel/e-invoicing-in-israel.html)
- [Israel SHAAM E-Invoicing (VATupdate)](https://www.vatupdate.com/2026/01/27/briefing-document-podcast-e-invoicing-and-e-reporting-in-israel/)
