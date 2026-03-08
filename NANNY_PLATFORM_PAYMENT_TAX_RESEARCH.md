# Nanny Platform Payment, Tax & Invoicing Research — Israel

**Date:** March 7, 2026
**Researcher:** Payment & Tax Research Agent
**Status:** Complete
**Context:** Supplements NANNY_PLATFORM_REVENUE_MODEL_REVISED.md

---

## 1. ISRAELI PAYMENT PROCESSORS FOR MARKETPLACES

### Processor Comparison Matrix

| Processor | Marketplace Split Payments | Bit Support | Fees (est.) | Setup | PCI Compliance | Best For |
|-----------|:-:|:-:|---|---|:-:|---|
| **PayMe** | YES — native split to multiple sellers with dynamic platform fee | YES (via Isracard) | Custom pricing (volume-based) | API + plugins (Magento, Wix, WooCommerce) | YES | **Best fit for our marketplace model** |
| **Tranzila** | Partial — certified acquirer, can process but no native marketplace split | YES (via integration) | Custom (transparent pricing, low cost reputation) | API integration | YES (Bank of Israel certified, Visa/MC intl.) | High-volume simple processing |
| **Grow (Meshulam)** | NO — standard payment gateway, no split | YES | 1.7% + NIS 1 per transaction (excl. VAT) | Wix/Duda plugins, API | YES | Small businesses, simple checkout |
| **CardCom** | Partial — invoicing + payment, no native split | Unknown | Custom pricing | API, plugins | YES | Invoice-heavy businesses |
| **Stripe** | **NOT available in Israel** — requires US LLC workaround | N/A | 2.9% + $0.30 (US pricing) | Requires US entity (LLC + EIN + US bank) | YES | Only if we have US entity |

### RECOMMENDATION: PayMe as Primary Payment Processor

PayMe is the clear winner for our marketplace model because:

1. **Native marketplace split payments** — family pays X, platform takes fee, nanny gets the rest. All automated.
2. **Dynamic fee per transaction** — we can set our service fee percentage per booking.
3. **Bit integration** built-in (via Isracard partnership).
4. **Israeli company** — understands local compliance, VAT, invoicing.
5. **Additional features:** tokenization, recurring billing (for subscriptions), 3DSecure fraud protection, BNPL options.
6. **Instant payouts** available (premium feature for nannies who want same-day payment).

**Fallback:** Tranzila as secondary processor. Bank of Israel certified acquirer with strong reputation. Could handle subscription billing while PayMe handles marketplace transactions.

**Stripe:** NOT viable as primary processor. Israel is not a supported country. Would require forming a US LLC — adds complexity, cost, and regulatory overhead. Not recommended for MVP.

---

## 2. MOBILE PAYMENTS & CONSUMER PREFERENCES IN ISRAEL

### How Israeli Families Currently Pay Babysitters (Bank of Israel Survey)

| Payment Method | % of Families |
|:---:|:---:|
| **Payment app (Bit/PayBox)** | **43%** |
| Cash | 22% |
| Bank transfer | 20% |
| Credit card | 5% |
| Other | 10% |

**Key insight:** Payment apps are already the #1 method. Our platform should make this even easier, not fight the existing behavior.

### Bit (Bank Hapoalim)

- **Market position:** Largest payment app in Israel, 2M+ users, ~80% market share in P2P transfers
- **Business integration:** API available via Allpay; Bit button on checkout pages
- **Transaction limits:** Up to NIS 5,000/transaction, NIS 20,000/month (NIS 240,000/year for business accounts)
- **Integration path:** Via PayMe (which has native Bit support via Isracard partnership)
- **Bank of Israel status:** Approved as digital wallet (2024)

### PayBox (Discount Bank)

- **Market position:** 2.5M+ users, second-largest payment app
- **Ownership:** Discount Bank (50.1%) + Shufersal (49.9%)
- **Features:** Digital wallet, holds funds outside bank accounts, 3% interest on balances
- **Marketplace feature:** Machine-learning matching for merchants to reach user groups
- **Integration:** Less documented API than Bit; primarily consumer-facing

### Apple Pay & Google Pay

- **Status in Israel:** Both available and growing
- **Integration:** Supported by Grow (Meshulam) and PayMe
- **Adoption:** Part of the contactless payment trend; Mobile POS payments projected to grow 28% annually through 2027
- **Market size:** Digital payments market projected at US$45.2B by 2027

### RECOMMENDATION for Payment Methods

Support in order of priority:
1. **Credit/debit card** (Visa, Mastercard, Amex) — via PayMe
2. **Bit** — via PayMe's native Bit integration
3. **Apple Pay / Google Pay** — via PayMe
4. **Bank transfer** — for B2B corporate invoicing
5. **PayBox** — evaluate post-MVP based on API availability

---

## 3. ISRAELI TAX & INVOICING REQUIREMENTS

### VAT (Value Added Tax)

| Detail | Current Rule (2026) |
|--------|-------------------|
| **Standard VAT rate** | **18%** (increased from 17% on January 1, 2025) |
| **Do we charge VAT on our service fee?** | **YES** — platform service fee is a taxable service |
| **Do we charge VAT on the full booking amount?** | **NO** — only on OUR fee. The nanny's payment is between family and nanny. |
| **Is the nanny's income subject to VAT?** | Only if she is an Osek Murshe (licensed dealer). Osek Patur is VAT-exempt. |
| **Osek Patur threshold (2024-2026)** | NIS 120,000/year (~NIS 10,000/month) |

### VAT Implications for Our Platform

```
EXAMPLE TRANSACTION:
Family books nanny for 4 hours at NIS 60/hr = NIS 240
Platform service fee (10%): NIS 24
VAT on service fee (18%): NIS 4.32

Family pays: NIS 240 (to nanny) + NIS 24 + NIS 4.32 = NIS 268.32
Platform keeps: NIS 24 + NIS 4.32 = NIS 28.32 (remits NIS 4.32 to tax authority)
Nanny receives: NIS 240 (handles her own tax obligations)
```

### Tax Invoice (חשבונית מס) Requirements

**When must we issue a tax invoice?**
- For EVERY service fee we charge to families
- Must be issued at the time of or shortly after payment
- Must include: our business details, customer details, service description, amount, VAT amount, allocation number (if over threshold)

**E-Invoicing Mandate (SHAAM Platform) — CRITICAL for 2026:**

| Date | Threshold for Mandatory Allocation Number |
|------|------------------------------------------|
| 2025 | Invoices over NIS 20,000 (pre-VAT) |
| January 1, 2026 | Invoices over NIS 10,000 (pre-VAT) |
| June 1, 2026 | Invoices over NIS 5,000 (pre-VAT) |

**Impact on our platform:**
- Individual booking fees (NIS 19-29) are far below the threshold — no allocation number needed per transaction
- **Monthly subscription invoices** (NIS 69/mo) also below threshold
- **B2B corporate contracts** (NIS 2,000-8,000/mo) — WILL require allocation numbers from SHAAM
- **Integration requirement:** Our accounting/ERP system must connect to ITA's SHAAM platform via API (JSON format) for B2B invoices
- A manual web portal exists but is not suitable for volume invoicing

### Receipt vs. Invoice Requirements

| Document | When to Issue | Who Issues |
|----------|--------------|-----------|
| **Tax Invoice (חשבונית מס)** | Platform charges family a service fee | **Us** (must be Osek Murshe / Ltd.) |
| **Receipt (קבלה)** | Upon receiving payment | **Us** |
| **Combined Invoice-Receipt (חשבונית מס / קבלה)** | Can combine both in one document | **Us** — recommended for simplicity |
| **Nanny's receipt to family** | If nanny is registered self-employed | **Nanny** (her responsibility) |

### Annual Reporting

| Form | What | When |
|------|------|------|
| **Annual VAT returns** | Total VAT collected and paid | Monthly/bi-monthly filing |
| **Form 856 (טופס 856)** | Annual report of payments to service providers | By March 31 of following year |
| **Form 126** | Annual employer report (if we have employees) | By April 30 |

**Form 856 is critical:** If we facilitate payments to nannies, we may need to report total payments to each nanny on Form 856 to the tax authority. This creates tax transparency — a FEATURE we can market to families ("we help you stay compliant").

---

## 4. MONEY FLOW ARCHITECTURE

### Recommended Payment Flow

```
BOOKING FLOW:

1. Family books nanny via app
2. Family's payment method is charged: Nanny Rate + Service Fee + VAT on fee
   (e.g., NIS 240 + NIS 24 + NIS 4.32 = NIS 268.32)

3. PayMe splits the transaction:
   a. Platform account receives: NIS 28.32 (service fee + VAT)
   b. Nanny's designated account receives: NIS 240

4. Platform issues חשבונית מס/קבלה to family for NIS 28.32

5. Nanny receives funds according to payout schedule

PAYOUT OPTIONS FOR NANNIES:
- Standard: Weekly payout (like Wolt couriers)
- Fast: Next business day (like Gett drivers)
- Instant: Same-day (premium — small fee, like Fiverr Early Payout)
```

### Escrow & Fund Holding

**Can we hold funds?**

Under the Regulation of Payment Services and Payment Initiation Law (2023):
- If our average monthly volume is **under NIS 5 million** → **EXEMPT from licensing**
- Above NIS 5M monthly → need payment services license from Israel Securities Authority (ISA)
- Customer funds must be **segregated** from company assets (even if exempt)

**For MVP:** We likely won't need a license. At projected Year 1 volumes (~NIS 1M/year = ~NIS 83K/month), we are far below the NIS 5M monthly threshold. However:
- Use PayMe's split payment to avoid holding funds ourselves
- PayMe holds and distributes — they already have the license
- We never touch the nanny's money directly

**Post-scale consideration:** If/when we exceed NIS 5M/month in transaction volume, we'll need to either:
1. Obtain our own payment services license from ISA
2. Continue using PayMe (or similar licensed processor) as the fund holder

### Refund Handling

| Scenario | Refund Policy | Who Bears Cost |
|----------|---------------|---------------|
| Family cancels >24h before | Full refund of service fee | Platform |
| Family cancels 2-24h before | 50% refund of service fee | Split |
| Family cancels <2h before | No refund; nanny gets cancellation fee | Family pays |
| Nanny cancels | Full refund + priority rebooking | Platform (penalize nanny) |
| Service quality dispute | Case-by-case review | Platform (escrow release delay) |

### Money Flow Comparison: How Other Israeli Platforms Do It

| Platform | Model | Payout Timing | Fee Structure |
|----------|-------|--------------|---------------|
| **Fiverr** | Buyer pays Fiverr → Fiverr holds 14 days → releases 80% to seller | 14 days (7 for top sellers) | 20% from sellers + 5.5% from buyers |
| **Gett** | Rider pays via app → Gett takes commission → driver gets rest | Next business day | Commission per ride |
| **Wolt** | Customer pays Wolt → Wolt pays restaurant/courier | Weekly (couriers), 6-30 days (restaurants) | Commission % from restaurants |
| **Midrag** | Rating platform — does not process payments | N/A | Lead generation model |

---

## 5. ISRAELI FINTECH REGULATIONS

### Do We Need a Payment Services License?

**Short answer: Probably NOT for MVP, but monitor closely.**

Under the Regulation of Payment Services and Payment Initiation Law (5783-2023):

| Exemption Category | Threshold | Our Status |
|-------------------|-----------|-----------|
| Monthly transaction volume | Under NIS 5M/month | **EXEMPT** (Year 1 est. ~NIS 83K/month) |
| Payment account balances | Under NIS 1,500/unidentified, NIS 3,000/identified | **EXEMPT** (we don't hold balances) |
| Core business is NOT payments | Payment is incidental to service | **LIKELY EXEMPT** (we are a matching platform) |

**Key strategy: Don't hold funds.** By using PayMe's split payment, we route money through a licensed payment processor. We never hold nanny funds. This keeps us in the "incidental payment services" category.

### Anti-Money Laundering (AML) Requirements

Even without a license, if we process payments we should implement:

| Requirement | What It Means | When Required |
|-------------|--------------|---------------|
| **KYC (Know Your Customer)** | Verify identity of families and nannies | From Day 1 (also needed for background checks) |
| **Transaction monitoring** | Flag unusual patterns | When volume justifies |
| **Suspicious Activity Reports** | Report to IMPA if suspicious | Mandatory if we are classified as payment company |
| **Record keeping** | Keep transaction records 7 years | From Day 1 |

**The November 2024 AML Order** for payment companies requires:
- Appointed corporate compliance officer
- Customer identification and ongoing due diligence
- Business-wide risk assessments
- Reporting to IMPA (Israel Money Laundering and Terror Financing Prohibition Authority)

**For MVP:** Our KYC for background checks (ID verification for nannies, basic family verification) satisfies most AML identity requirements. We should implement basic transaction monitoring from launch.

### Bank of Israel Regulations

- Bank of Israel expanded access to payment systems beyond banks to licensed fintech companies (2024-2025)
- Tranzila was approved as the fourth credit card processor by Bank of Israel
- New "identification code" system increases competition in payment market
- Payment systems now open to: payment service providers, licensed financial asset providers, licensed credit/deposit providers

---

## 6. THE NANNY TAX SITUATION — CRITICAL PLATFORM DECISION

### The Core Question: Is the Nanny Self-Employed or an Employee?

**Answer: The FAMILY is the employer. The nanny is their employee.**

This is the established legal position in Israel:

| Scenario | Classification | Implications |
|----------|---------------|-------------|
| Nanny works at family's home | **Family's employee** | Family must register with Bituach Leumi, pay social contributions |
| Nanny watches child at her own home | **Self-employed** | She handles her own tax/Bituach Leumi |
| Nanny found through our platform, works at family's home | **Family's employee** (not ours) | Our platform is a matching service only |

### Family's Legal Obligations as Employer (even for a few hours/week)

| Obligation | Details | Deadline |
|-----------|---------|----------|
| **Bituach Leumi registration** | Register as employer, report employee (form BL/1) | Within 2 weeks of employment start |
| **Monthly Bituach Leumi payments** | Social security + health insurance contributions | Monthly |
| **Pension contributions** | Mandatory since 2008: 6.5% to pension fund + 8.33% to severance fund | Monthly |
| **Minimum wage** | NIS 32.31/hour (NIS 5,880.02/month) as of 2025 | Per pay period |
| **Travel reimbursement** | Bus fare to/from work (daily or monthly pass — whichever is cheaper) | Monthly |
| **Sick days** | No pay Day 1; 50% Days 2-3; 100% from Day 4 | As needed |
| **Vacation days** | Pro-rated based on employment scope | Annually |
| **Form 101 (Tofes 101)** | Employee tax declaration form | Annually (start of year) |
| **Payslip** | Detailed record of hours, gross, deductions, net pay | By 9th of following month |

**The painful truth:** Most Israeli families who hire babysitters do NOT comply with these requirements. They pay cash or Bit with no documentation. This is technically illegal.

### Platform Opportunity: Compliance-as-a-Feature

This is a massive value proposition for our platform:

```
WHAT WE CAN OFFER FAMILIES:

1. "Employment Law Toolkit" (part of Premium subscription):
   - Auto-generated payslip templates
   - Bituach Leumi registration guide (step-by-step)
   - Pension contribution calculator
   - Annual summary for tax reporting
   - Form 101 template

2. "Tax-Smart Payments":
   - All payments documented and traceable
   - Annual summary report (useful for Form 856)
   - Helps families stay legal without the headache
   - "Your babysitter payments, fully compliant"

3. Future feature: "Employer-in-a-Box"
   - Partner with payroll service (like CWS Israel or Deel)
   - Automate Bituach Leumi payments
   - Auto-generate payslips
   - Handle pension contributions
   - NIS 49-99/month premium add-on
```

### Nanny's Tax Registration Options

| Status | When Applicable | VAT | Income Tax | Bituach Leumi |
|--------|----------------|:---:|:---:|:---:|
| **Employee of family** (most common) | Works at family's home | No VAT (employee) | Withheld by employer | Paid by employer |
| **Osek Patur** (self-employed, VAT-exempt) | Works at her own home, or multiple freelance gigs, earns under NIS 120K/year | Exempt | Self-reported | Self-paid |
| **Osek Murshe** (self-employed, licensed) | Earns over NIS 120K/year | Must charge 18% VAT | Self-reported | Self-paid |

**Important restriction:** Some professions requiring licensing cannot register as Osek Patur. Babysitting/nanny work is NOT a licensed profession, so Osek Patur is available for self-employed nannies under the threshold.

### What We Should Recommend to Families

```
OUR PLATFORM GUIDANCE:

"When you hire a nanny through [Platform Name], you are the employer.
Israeli law requires you to:
1. Register with Bituach Leumi as a household employer
2. Pay social security contributions monthly
3. Provide a payslip each month
4. Contribute to your nanny's pension

We make this easy with our Employment Law Toolkit (included in Premium).
Your nanny keeps 100% of her stated rate — we charge YOU a service fee."
```

---

## 7. RECOMMENDED PAYMENT ARCHITECTURE — SUMMARY

### Tech Stack for Payments

| Component | Recommended Solution | Why |
|-----------|---------------------|-----|
| **Primary payment processor** | PayMe | Native marketplace split, Bit support, Israeli company |
| **Subscription billing** | PayMe recurring billing OR in-app purchase (iOS/Android) | Tokenization, auto-renewal |
| **B2B invoicing** | Custom + SHAAM API integration | Mandatory for invoices over NIS 5K (from June 2026) |
| **Invoicing/receipts** | Automated via PayMe or integration with Israeli accounting software (e.g., Hashavshevet, Invoice4U, Rivhit) | Must issue חשבונית מס/קבלה |
| **Payout to nannies** | PayMe split payment → nanny's bank/Bit | Weekly standard, instant available |
| **Fraud prevention** | PayMe 3DSecure + platform-level monitoring | Required for card-not-present transactions |

### Regulatory Compliance Checklist

- [ ] Register as Israeli Ltd. (חברה בע"מ) — Osek Murshe
- [ ] Open business bank account
- [ ] Register for VAT (mandatory for Ltd.)
- [ ] Integrate with PayMe for marketplace payments
- [ ] Set up automated invoicing (חשבונית מס/קבלה) for every service fee
- [ ] Implement SHAAM API integration for B2B invoices (before June 2026)
- [ ] Implement basic KYC/AML (identity verification for all users)
- [ ] Segregate customer funds from company accounts
- [ ] Appoint compliance officer (when required by scale)
- [ ] Set up transaction monitoring
- [ ] File monthly/bi-monthly VAT returns
- [ ] File Form 856 annually (payments to service providers)
- [ ] Monitor monthly transaction volume vs. NIS 5M license threshold

### Cost Estimates for Payment Infrastructure

| Item | Estimated Cost | Frequency |
|------|---------------|-----------|
| PayMe setup/integration | NIS 0-5,000 | One-time |
| PayMe transaction fees | ~1.5-2.5% per transaction | Per transaction |
| Accounting software license | NIS 100-300/month | Monthly |
| SHAAM API integration (dev) | NIS 5,000-15,000 | One-time |
| Legal consultation (payment compliance) | NIS 5,000-10,000 | One-time |
| Ongoing compliance/audit | NIS 2,000-5,000/year | Annual |

---

## 8. KEY RISKS & MITIGATION

| Risk | Severity | Mitigation |
|------|:--------:|-----------|
| Classified as payment company (need license) | HIGH | Use PayMe split — never hold funds ourselves |
| VAT miscalculation / non-compliance | MEDIUM | Automated invoicing from Day 1; hire Israeli accountant |
| Nanny classified as OUR employee | HIGH | Clear ToS: family is employer; no dispatch/pricing control |
| AML violation | HIGH | KYC from Day 1 (background checks double as AML); transaction monitoring |
| E-invoicing non-compliance (SHAAM) | MEDIUM | Integrate SHAAM API before June 2026 for B2B; individual fees under threshold |
| Family non-compliance with Bituach Leumi | LOW (their risk) | Provide tools/guidance; not our legal obligation |
| PayMe service disruption | LOW | Have Tranzila as backup processor |

---

## SOURCES

### Payment Processors
- [PayMe — Marketplace Payment Platform](https://payme.io/)
- [PayMe Marketplace API Documentation](https://paymeapi.docs.apiary.io/)
- [Tranzila — Credit Card Processing](https://www.tranzila.com/english.html)
- [Grow by Meshulam — Wix Integration](https://support.wix.com/en/article/connecting-grow-by-meshulam-as-a-payment-provider)
- [CardCom — Payment Gateway](https://www.ampeco.com/ev-charging-apps-marketplace/cardcom/)
- [Stripe — Payments in Israel](https://stripe.com/resources/more/payments-in-israel)
- [Stripe Global Availability](https://stripe.com/global)

### Bit & Mobile Payments
- [Bit — Wikipedia](https://en.wikipedia.org/wiki/Bit_(payment_application))
- [Bit for Business — Allpay](https://www.allpay.co.il/en/news/bit-button-on-checkout-page)
- [Bit via PayMe Integration](https://help.payme.io/hc/en-us/articles/360013964399-Alternative-Payment-Method-Bit)
- [PayBox — Wikipedia](https://en.wikipedia.org/wiki/PayBox)
- [Bank of Israel Payment Preferences Survey](https://www.boi.org.il/en/communication-and-publications/press-releases/ahead-of-the-payments-conference-the-bank-of-israel-conducted-a-survey-intended-to-show-the-public-s-payment-preferences/)

### Tax & Invoicing
- [Israel VAT Stays at 18% for 2026](https://www.vatupdate.com/2025/12/10/israel-approves-2026-budget-vat-stays-at-18-expands-exemptions-eases-bank-entry-rules/)
- [Israel E-Invoicing — Avalara](https://www.avalara.com/us/en/vatlive/country-guides/africa-and-middle-east/israel/e-invoicing-in-israel.html)
- [KPMG — Israel E-Invoicing Expansion](https://kpmg.com/us/en/taxnewsflash/news/2025/12/tnf-israel-expansion-of-mandatory-e-invoicing-model.html)
- [Israel E-Invoicing CTC Model — EDICOM](https://edicomgroup.com/blog/israel-electronic-invoice-clearance-model)
- [Osek Patur Guide — Dray & Dray CPAs](https://cpa-dray.com/en/blog/osek-patur-guide/)
- [Freelancer Tax Compliance Israel 2026 — CWS Israel](https://www.cwsisrael.com/freelancer-tax-compliance-in-israel-2026/)

### Employment & Bituach Leumi
- [Registering Childcare Provider — Nefesh B'Nefesh](https://www.nbn.org.il/life-in-israel/community-and-housing/setting-up-your-home-in-israel-community-and-housing/registering-a-childcare-provider-or-housekeeper/)
- [Domestic Workers NII Payments — VOLEH](https://voleh.org/domestic-workers-nii-payments-benefits/)
- [Domestic Workers Pension — VOLEH](https://voleh.org/domestic-workers-intro-pension-fund/)
- [Hiring Help in Israel — Rifka Lebowitz](https://rifkalebowitz.com/courses/israeli-domestic-employer-guide/)
- [Rockmybaby Israel — Family FAQs](https://www.rockmybaby.co.il/pages/families-faqs-for-clients)
- [Employer Responsibilities Israel — CWS](https://www.cwsisrael.com/employer-responsibilities-in-israel-a-comprehensive-guide/)

### Fintech Regulation
- [Regulated Payment Services Israel 2025 — Barnea Law](https://barlaw.co.il/regulated-payment-services-and-financial-services-in-israel-summary-and-outlook-for-2025/)
- [Payment Services Law — Gornitzky](https://www.gornitzky.com/new-regulation-in-israel-payment-services-and-payment-initiation-law/)
- [Payment Licensing Reform — Regulazia](https://regulazia.co.il/en/articles/payment-licensing-reform-in-israel/)
- [AML Regulations Israel — Sumsub](https://sumsub.com/blog/aml-kyc-israel/)
- [AML Directives for Payment Companies — S. Horowitz](https://s-horowitz.com/new-directives-for-payment-companies-in-israel-to-implement-aml-obligations-using-online-identification-technology/)

### Platform Payment Models
- [Fiverr Payment Methods](https://help.fiverr.com/hc/en-us/articles/37332701180945-Payment-methods)
- [How to Get Paid on Fiverr — Wise](https://wise.com/us/blog/how-to-get-paid-on-fiverr)
- [Wolt Merchant Fees Explained](https://explore.wolt.com/en/isr/merchant/learning-center/wolt-merchant-fees-and-commissions)
- [Wolt Courier FAQ Israel](https://explore.wolt.com/en/isr/couriers/faq)
- [Gett — How It Works — Ridester](https://www.ridester.com/gett/)
- [Bubble Forum — Israel Marketplace Split Payments](https://forum.bubble.io/t/how-to-implement-split-payments-between-multiple-recipients-without-passing-through-platform-s-bank-account-israel-based-marketplace/375376)

*This document is based on web research conducted March 7, 2026. It does not constitute legal, tax, or financial advice. Consult a qualified Israeli attorney and CPA before implementation.*
