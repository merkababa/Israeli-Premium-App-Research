# Israeli Payment Processing & Fintech Landscape — March 2026

Research date: 2026-03-07

---

## 1. PayMe — Israel's Leading Marketplace Payment Processor

**Status: Active, dominant in Israeli marketplace payments.**

- **Founded**: 2014, Tel Aviv. Founder: Adam Kogan.
- **Employees**: ~60
- **Clients**: 200+ partners, 20,000+ merchants. Notable: Wolt, Shufersal, Super-Pharm, IKEA, Wix, Easy2Give.
- **What they do**: White-label embedded payments platform for banks, acquirers, marketplaces, and platforms. Full-stack financial infrastructure.

### Key Capabilities (Verified from docs.payme.io)
- **Marketplace split payments**: Supports splitting transactions between multiple sellers, with dynamic platform fees per transaction.
- **Instant payouts**: Rapid fund transfers for platform transactions.
- **Subscription/recurring billing**: Built-in.
- **Israeli direct debit (Masav)**: Supported via API.
- **Bit integration**: Supported as alternative payment method.
- **Fraud prevention**: Built-in.
- **Invoice factoring, loans, financing**: Available.
- **Closed-loop wallets**: Supported.
- **Reconciliation & payouts**: Built-in.
- **Tokenization, 3D Secure**: Supported.
- **85+ payment methods globally**.

### API Quality
- REST API with documentation at docs.payme.io (Stoplight-hosted).
- Separate Marketplace API documented at paymeapi.docs.apiary.io.
- Guides for: payment generation, Israeli direct debit, platforms & marketplaces.
- Sandbox environment available.
- Request format: GET/POST with application/x-www-form-urlencoded. Requires merchant ID, order number, amount, signature.

### Pricing
- **Not publicly listed.** Custom pricing — must contact sales.
- Expected: percentage per transaction + possible monthly fee. Industry standard for Israeli gateways is 1.2%-2.0% per transaction.

### Assessment for Emuni
PayMe is the strongest candidate for a marketplace startup. It is the processor behind Wolt Israel, which validates its marketplace split-payment capability. It handles the core need: parent pays -> platform takes fee -> nanny receives payout.

**Sources:**
- [PayMe Homepage](https://payme.io/)
- [PayMe Products](https://payme.io/products/)
- [PayMe Marketplace API Docs](https://paymeapi.docs.apiary.io/)
- [PayMe Docs & API (Stoplight)](https://docs.payme.io/)
- [Platforms and Marketplaces Guide](https://docs.payme.io/docs/payments/1840bzrqlh9vn-platforms-and-marketplaces)
- [Israeli Direct Debit Guide](https://docs.payme.io/docs/guides/0g211e0luaj6r-israeli-direct-debit)
- [Bit Integration](https://help.payme.io/hc/en-us/articles/360013964399-Alternative-Payment-Method-Bit)

---

## 2. Bit (by Bank Hapoalim) — Israel's Dominant P2P App

**Status: Active, dominant P2P payment app in Israel. Now has business/merchant capabilities and developer API.**

- **Launched**: 2017 by Bank Hapoalim.
- **Category**: P2P money transfers, now expanding to merchant payments.
- **Market position**: #1 P2P payment app in Israel.

### Key Facts (2025-2026)
- **Annual receiving limit (individuals)**: NIS 100,000/year (raised from NIS 50,000 in January 2025).
- **Annual receiving limit (business)**: NIS 240,000/year.
- **Merchant fees**: 0.6% on money received above NIS 25,000/month. Charged on the 5th of the following month.
- **"Pockets" feature**: Separate balances for business income vs personal — useful for nannies organizing earnings.
- **Bank of Israel approval**: Approved as a digital wallet (not just P2P transfer).

### Developer API
- **Developer Portal**: developer.bitpay.co.il/docs
- API documentation, sandbox environment available.
- Website integration possible via API.
- **However**: Bit's API is primarily for merchants accepting Bit as a payment method, NOT for marketplace split payments. You cannot programmatically split a Bit payment between platform and provider.

### Bit via Payment Gateways
- **PayMe**: Supports Bit as an alternative payment method.
- **Allpay**: Bit payments at 1.45% (same rate as credit cards, no additional fee).
- **Grow/Meshulam**: Supports Bit payments.
- **Tranzila**: Supports Bit.
- **iCredit**: Supports Bit.
- **Morning (Green Invoice)**: Supports Bit payments.

### Assessment for Emuni
Bit is essential for the Israeli market — it's how most young Israelis transfer money. For v1 (manual Bit invoicing), parents can pay nannies directly via Bit. For v2 (automated payments), integrate Bit as a payment method through PayMe or another gateway, where the parent pays via Bit and the platform handles the split.

**Sources:**
- [Bit Wikipedia](https://en.wikipedia.org/wiki/Bit_(payment_application))
- [Bit Developer Portal](https://developer.bitpay.co.il/docs)
- [Bit Google Play](https://play.google.com/store/apps/details?id=com.bnhp.payments.paymentsapp)
- [Bit Merchant Fees — Globes](https://en.globes.co.il/en/article-hapoalim-reveals-bit-app-charges-from-january-1001494038)
- [Allpay Bit Pricing](https://www.allpay.co.il/en/news/allpay-pricing-bit)

---

## 3. Stripe in Israel

**Status: NOT officially available in Israel as of March 2026.**

- Israel is NOT among the 46 countries where Stripe is supported.
- Stripe does support ILS (Israeli New Shekel) as a currency for international transactions.
- Stripe opened sales/support operations in Israel in early 2022 and recruited local talent, but never launched merchant account support.
- **No announced timeline** for official Israel launch.

### Workaround
Israeli businesses can use Stripe by:
1. Forming a US-based LLC.
2. Obtaining an EIN (Employer Identification Number).
3. Opening a US bank account.
4. Running Stripe through the US entity.

This is common for Israeli SaaS companies selling globally, but impractical for a domestic marketplace collecting NIS payments from Israeli parents.

### Cross-Border Payouts Update (January 2026)
Stripe added Global Payouts support for 15 new countries in January 2026, but Israel was not among them.

### Assessment for Emuni
**Not viable.** Stripe cannot be used for domestic Israeli marketplace payments without a US entity workaround that adds complexity and currency conversion costs. Use PayMe or a local gateway instead.

**Sources:**
- [Stripe Global Availability](https://stripe.com/global)
- [How to Accept Payments in Israel — Stripe](https://stripe.com/resources/more/payments-in-israel)
- [Stripe Supported Countries 2026](https://redstagfulfillment.com/how-many-countries-does-stripe-operate-in/)
- [Stripe Israel Cross-Border Payouts Changelog](https://docs.stripe.com/changelog/clover/2026-01-28/cross-border-payouts-new-countries)

---

## 4. PayPal Israel

**Status: Active in Israel but limited for domestic marketplace use.**

- PayPal is available for Israeli businesses and consumers.
- Supports: invoicing, subscriptions, payment processing.
- **Seller Protection**: Updated January 2025 to include Guest Checkout transactions.
- **Acquisition**: PayPal acquired Israeli AI company Cymbio (Tel Aviv) in early 2026 for agentic commerce capabilities. Deal expected to close H1 2026.

### Limitations for Israeli Marketplace
- PayPal fees are high for domestic transactions (typically 2.9% + fixed fee + currency conversion if applicable).
- No native ILS-to-ILS P2P transfer — always involves PayPal's intermediation.
- No native Bit integration.
- No Israeli invoice generation (SHAAM compliance).
- PayPal Connect (for marketplaces) is designed for cross-border, not domestic Israeli use.

### Assessment for Emuni
**Not recommended for primary payment processing.** PayPal is too expensive for domestic NIS transactions and lacks Israeli-specific features (Bit, installments, SHAAM invoicing). Could be offered as a secondary payment method for English-speaking users.

**Sources:**
- [PayPal Israel](https://www.paypal.com/il/home)
- [PayPal Policy Updates Israel](https://www.paypal.com/il/legalhub/upcoming-policies-full)
- [PayPal Cymbio Acquisition](https://www.paymentsdive.com/news/paypal-buys-israeli-ai-firm/810244/)
- [PayPal Israel Usage Stats](https://storeleads.app/reports/technology/PayPal/country/IL)

---

## 5. Rapyd — Israeli-Founded Global Payments

**Status: Licensed in Israel (July 2025), expanding domestic capabilities.**

- **Founded**: Tel Aviv (now HQ in London).
- **Funding**: $1B+ total. Acquired PayU.
- **Israel Payment License**: Granted July 2025 by Israel Securities Authority, along with Revolut, Airwallex, and Mesh Payments.

### Licensed Capabilities in Israel
- Transfer and convert currency.
- Offer interest on deposited funds.
- Settle digital wallets.
- Accept bank transfers and bank redirects.

### What Rapyd Does NOT Yet Offer in Israel
- No evidence of domestic credit card acquiring in Israel.
- No Israeli installments (tashlumim) support.
- No Bit integration documented.
- No SHAAM e-invoicing integration.
- Primarily focused on cross-border payments and fintech infrastructure.

### Assessment for Emuni
**Not suitable for v1.** Rapyd is building toward domestic Israeli capabilities but is not yet a viable alternative to PayMe/Tranzila/CardCom for a local marketplace. Worth monitoring for future marketplace payment orchestration, but too early and enterprise-focused for a bootstrapped startup.

**Sources:**
- [Rapyd Israel Country Data](https://www.rapyd.net/network/country/israel/)
- [Israel Payment Licenses — Digital Banker](https://thedigitalbanker.com/revolut-rapyd-airwallex-and-mesh-granted-payments-licences-in-israel/)
- [Rapyd License — Calcalist](https://www.calcalistech.com/ctechnews/article/rk633zrlxx)

---

## 6. Traditional Israeli Payment Gateways

### 6a. Tranzila

**Status: Active. Bank of Israel licensed acquirer (since 2017). One of Israel's oldest gateways (founded 1996).**

- **Location**: Netanya, Israel.
- **Revenue**: ~$6.1M (2025).
- **Certifications**: PCI DSS Level 1, Visa International, MasterCard International certified acquirer.

**Features:**
- Credit card processing (e-commerce + POS).
- Digital green invoicing module (approved by Income Tax Authority).
- Subscription/recurring billing (standing orders).
- Token-based billing (no card storage needed).
- 3D Secure authentication.
- **Payment methods**: Apple Pay, Google Pay, PayPal, Bit, Masav (bank direct debit).
- API v2 available with iframe integration.

**Pricing**: Not publicly listed. Historically competitive — known for transparent pricing and low fees.

**Assessment**: Solid, established gateway with Israeli invoicing. Lacks marketplace split-payment capability out of the box. Better suited for single-merchant e-commerce than multi-party marketplaces.

**Sources:**
- [Tranzila English](https://www.tranzila.com/english.html)
- [Tranzila API v2 Docs](https://docs.tranzila.com/docs/payments-billing/c7do32dbrot42-tranzila-api-v2)
- [Bank of Israel Acquirer License](https://blogs.timesofisrael.com/bank-of-israel-approves-tranzila-as-fourth-credit-card-processor/)

### 6b. CardCom

**Status: Active. Bank of Israel permanent acquirer license holder.**

- **Founded**: 1994. One of the oldest Israeli payment companies.
- **License**: Permanent merchant acquirer license from Bank of Israel.

**Features:**
- Credit card processing (online + digital).
- **Integrated invoice and receipt generation** compliant with Israeli tax law (unique strength).
- Tokenization.
- Recurring billing.
- REST API v11.
- Low Profile payments (redirect-based).
- Automatic tax invoice/receipt creation per Israeli law.

**Pricing**: Free for basic plugin integrations. Transaction fees — must contact for rates.

**Assessment**: Strong for Israeli tax compliance (auto-generates invoices/receipts). API is older but functional. Like Tranzila, better for single-merchant use than marketplace splits.

**Sources:**
- [CardCom Payment Gateway](https://agentskills.co.il/en/skills/tax-and-finance/cardcom-payment-gateway)
- [Bank of Israel CardCom License](https://kamakama.gov.il/en/communication-and-publications/press-releases/c18-07-23/)

### 6c. iCredit (by Rivhit)

**Status: Active. Part of the Rivhit business management ecosystem.**

- Provides online credit card processing for businesses and websites.
- **PCI DSS Level 1** (Service Provider level).
- Supports all Israeli credit card types + multiple currencies.

**Features:**
- Online invoicing modules.
- Tokenization (secure card storage).
- Bit payments.
- PayPal integration.
- 3DS verification.
- Integration with Rivhit business management software.
- API for developer integration.
- POS terminal support.
- Wix integration available.

**Pricing**: Not publicly listed. Part of Rivhit's broader business management pricing.

**Assessment**: Best suited for small businesses already using Rivhit's accounting/invoicing software. Not designed for marketplace split payments.

**Sources:**
- [iCredit Homepage](https://www.icredit.co.il/)
- [iCredit Developer Solutions](https://www.icredit.co.il/%D7%A1%D7%9C%D7%99%D7%A7%D7%AA-%D7%90%D7%A9%D7%A8%D7%90%D7%99-%D7%9C%D7%9E%D7%A4%D7%AA%D7%97%D7%99%D7%9D/)
- [iCredit on Wix](https://support.wix.com/en/article/connecting-icredit-as-a-payment-provider)

---

## 7. Apple Pay & Google Pay in Israel

### Apple Pay
- **Launched in Israel**: May 2021.
- **Status**: Fully operational for contactless in-store and online payments.
- **Supported by**: All major Israeli banks and credit card companies (Visa, Mastercard, Amex).
- **iPhone market share in Israel**: ~30% at launch, likely higher now.
- **Adoption**: No Israel-specific statistics available, but globally Apple Pay has 744M+ users.

### Google Pay
- **Launched in Israel**: Late 2021 / early 2022.
- **Status**: Available for online payments. **NFC contactless payments in physical stores are NOT supported in Israel** — this is a significant limitation.
- **Supported banks**: Bank Leumi, Bank Yahav, Cal, Israel Discount Bank, Max, Mizrahi Tefahot, Pepper, First International Bank, Bank Hapoalim (Mastercard only), Bank Massad, Union Bank, Premium Express, Isracard.
- **Cards**: Visa, Mastercard, Amex.

### Assessment for Emuni
- Apple Pay should be supported as a payment method (via PayMe, Tranzila, Grow, or Allpay — all support it).
- Google Pay is useful for online checkout but not for in-person payments.
- Both are "nice to have" payment methods, not primary. Bit and credit cards dominate Israeli payments.

**Sources:**
- [Google Pay Israel Supported Methods](https://support.google.com/wallet/answer/12059326?hl=en&co=GENIE.CountryCode%3DIL)
- [Google Pay Israel Launch](https://thepaypers.com/payments/news/google-pay-launches-in-israel)
- [Google Pay Israel — NFCW](https://www.nfcw.com/whats-new-in-payments/google-pay-goes-live-in-israel/)
- [Apple Pay Supported Countries 2026](https://worldpopulationreview.com/country-rankings/apple-pay-supported-countries)

---

## 8. SHAAM E-Invoicing — June 2026 Deadline

### Timeline (Confirmed)
| Date | Threshold | Scope |
|------|-----------|-------|
| January 2024 | NIS 25,000+ | Phase 1 — large invoices |
| January 2025 | NIS 20,000+ | Phase 2 |
| **January 2026** | **NIS 10,000+** | **Phase 3 — CURRENT** |
| **June 1, 2026** | **NIS 5,000+** | **Phase 4 — permanent floor** |

NIS 5,000 is the final threshold. No further reductions are scheduled.

### How It Works
- **Clearance model**: Suppliers submit invoice data to the SHAAM central platform (ITA — Israel Tax Authority) for validation before issuing to the buyer.
- **Allocation number**: ITA returns an approval stamp (allocation number) upon successful validation.
- **Format**: JSON via REST API, per ITA API specifications.
- **API Spec Version**: v2.0 (released late 2024). Added new JSON fields, updated web services, and two new document types:
  - Agent Tax Invoice (חשבונית מס סוכן)
  - Journal Command (פקודת יומן)
- **Manual option**: Web portal available for manual submission (small businesses).

### API Integration Providers
| Provider | Notes |
|----------|-------|
| **Pagero** | Enterprise-grade, intermediary software for SHAAM |
| **Flick Network** | Pre-clearance integration, automatic SHAAM submission |
| **DDD Invoices** | Trusted SHAAM integration provider |
| **Sovos** | Global e-invoicing, supports Israel |
| **ClearTax** | SHAAM-compliant solutions |
| **Morning (Green Invoice)** | Israeli invoicing platform with built-in SHAAM compliance |
| **CardCom** | Built-in Israeli tax invoice generation |
| **Tranzila** | Digital green invoicing module (Income Tax Authority approved) |

### Assessment for Emuni
- For Emuni's NIS 49/mo subscriptions — these are below NIS 5,000, so SHAAM clearance is NOT required per-invoice.
- For nanny payments that could accumulate above NIS 5,000/invoice — SHAAM compliance will be needed by June 2026.
- **Recommendation**: Use a payment processor with built-in Israeli invoicing (PayMe, Morning/Green Invoice, or CardCom) to handle SHAAM compliance automatically rather than building a custom ITA API integration.

**Sources:**
- [E-Invoicing in Israel — DDD Invoices](https://dddinvoices.com/learn/e-invoicing-israel)
- [Israel E-Invoicing Briefing — VATupdate](https://www.vatupdate.com/2026/01/27/briefing-document-podcast-e-invoicing-and-e-reporting-in-israel/)
- [E-Invoicing Israel — Avalara](https://www.avalara.com/us/en/vatlive/country-guides/africa-and-middle-east/israel/e-invoicing-in-israel.html)
- [Israel Invoice API v2.0 Spec (PDF)](https://www.gov.il/BlobFolder/generalpage/israel-invoice-160723/he/vat_software-houses-180724-en.pdf)
- [SHAAM FAQ — Gov.il](https://www.gov.il/en/pages/faq_israel_invoice)
- [E-Invoicing Israel — Flick Network](https://www.flick.network/en-il/e-invoicing-in-israel)

---

## 9. Best Payment Processor for Emuni (Israeli Nanny Marketplace)

### Requirements Checklist

| Requirement | PayMe | Grow/Meshulam | Allpay | Tranzila | CardCom | iCredit |
|-------------|-------|---------------|--------|----------|---------|---------|
| Marketplace split payments | YES | No | No | No | No | No |
| Subscription billing | YES | YES | YES | YES | YES | YES |
| Bit integration | YES | YES | YES | YES | No* | YES |
| Apple Pay | YES | YES | YES | YES | ? | ? |
| Credit card installments | YES | YES (up to 12) | YES (up to 12) | YES | YES | YES |
| Israeli invoice/receipt | YES | YES | ? | YES | YES | YES |
| SHAAM compliance | Likely | Likely | ? | YES | YES | ? |
| Payout to providers | YES | No | No | No | No | No |
| API quality | Good (Stoplight) | Good (readme.io) | Good | Adequate | Older | Adequate |
| Fraud prevention | YES | ? | ? | 3DS | 3DS | 3DS |

*CardCom Bit support not confirmed in search results.

### Recommendation: PayMe (Primary) + Morning/Green Invoice (Invoicing)

**PayMe** is the only Israeli processor that natively supports marketplace split payments with dynamic platform fees and provider payouts. This is the core capability Emuni needs.

**Backup Architecture (if PayMe pricing is too high for v1)**:
1. Use **Grow/Meshulam** or **Allpay** as the payment gateway (accept credit cards + Bit from parents).
2. Handle split logic in your own backend (calculate platform fee, queue nanny payouts).
3. Use **Masav (Israeli direct debit)** or manual bank transfers for nanny payouts.
4. Use **Morning (Green Invoice)** for automated Israeli invoice generation and SHAAM compliance.

This backup approach is more complex but avoids PayMe's likely premium pricing for marketplace features.

### Pricing Comparison (Where Available)

| Processor | Pricing Model |
|-----------|--------------|
| **PayMe** | Custom (contact sales). Expected: 1.5-2.5% + per-transaction fee |
| **Grow/Meshulam** | Pay-per-use: 1.7% + NIS 1/tx OR Monthly: NIS 59/mo + 1.5%/tx |
| **Allpay** | 1.45% per transaction (credit cards, Bit, Apple Pay). No monthly fee mentioned |
| **Tranzila** | Custom (contact sales). Known for competitive/transparent pricing |
| **CardCom** | Custom (contact sales) |
| **iCredit** | Part of Rivhit ecosystem pricing |

---

## 10. Credit Card Installments (תשלומים)

### How Tashlumim Work in Israel
- A uniquely Israeli feature: buyers split a purchase into 2-12 equal monthly installments.
- **Interest-free** in most cases (merchant absorbs the cost).
- Only available with Israeli-issued credit cards.
- The full amount is reserved against the buyer's credit limit.
- Merchant receives the full amount upfront (or on accelerated schedule) from the credit card company; the buyer pays the card company in installments.

### Processor Support

| Processor | Installments Support | Max Installments |
|-----------|---------------------|-----------------|
| **PayMe** | YES | Not specified (standard: up to 12) |
| **Grow/Meshulam** | YES | Up to 12 |
| **Allpay** | YES | Up to 12 |
| **Tranzila** | YES | Not specified |
| **CardCom** | YES | Not specified |
| **iCredit** | YES | Not specified |
| **Bit** | NO (P2P, no installments) | N/A |
| **PayPal** | NO (not Israeli installments) | N/A |
| **Stripe** | N/A (not available in Israel) | N/A |

### Assessment for Emuni
- For NIS 49/mo subscriptions: installments are irrelevant (too small).
- For per-contact fees (NIS 19): too small for installments.
- **Where installments matter**: If Emuni ever introduces larger packages (e.g., NIS 200+ annual plans or booking deposits), installments become important. All major Israeli gateways support them.

**Sources:**
- [Tashlumim Explained — Kosher Frugal](https://www.kosherfrugal.com/2021/10/credit-cards-in-israel-including-what.html)
- [Allpay Pricing](https://www.allpay.co.il/en/pricing)
- [Grow/Meshulam Developer Docs](https://grow-il.readme.io/)
- [Tashlumim Guide — Janglo](https://www.janglo.net/item/fcl8cQiXO9Q)

---

## Bonus: New Entrants to Watch

### Revolut (Licensed July 2025)
- Payment license in Israel. Can transfer/convert currency, hold funds, settle digital wallets.
- Seeking lean banking license for deposits and credit.
- Operating in Israel since 2023.
- **Not yet viable for merchant acquiring/marketplace payments.**

### Airwallex (Licensed July 2025)
- Payment license in Israel. Can collect, hold, and pay in ILS using local rails.
- Multi-currency accounts (ILS + 30 global currencies).
- 315% revenue surge reported.
- **Potentially useful for cross-border payouts** (e.g., if Emuni expands to serve foreign au pairs), but not for domestic marketplace payments yet.

### Mesh Payments (Licensed July 2025)
- Payment license in Israel alongside the above.
- Focused on corporate expense management, not consumer marketplace payments.

### Morning (Green Invoice / חשבונית ירוקה)
- **160,000+ Israeli businesses** use it for invoicing.
- Full API for developers (greeninvoice.co.il/api-docs).
- Now offers payment initiation through banking connections.
- Supports: credit cards, Bit, Google Pay, Apple Pay via clearing connections.
- **Best-in-class for Israeli invoicing and SHAAM compliance.**
- Could serve as Emuni's invoicing layer even if PayMe handles payments.

**Sources:**
- [Revolut/Airwallex/Rapyd/Mesh Licenses — Calcalist](https://www.calcalistech.com/ctechnews/article/rk633zrlxx)
- [Airwallex Israel License](https://www.airwallex.com/newsroom/airwallex-secures-payment-service-license-in-israel-enabling-global-payment-solutions)
- [Morning API Docs](https://www.greeninvoice.co.il/api-docs/)
- [Morning Startup Nation Finder](https://finder.startupnationcentral.org/company_page/morning-by-green-invoice)

---

## Summary: Decision Matrix for Emuni

### v1 (MVP — Manual/Semi-Automated)
- **Payment**: Parents pay nannies directly via **Bit** (P2P). Emuni is not in the payment flow.
- **Subscription**: Collect NIS 49/mo premium fees via **Grow/Meshulam** (cheapest: 1.7% + NIS 1) or **Allpay** (1.45%).
- **Invoicing**: Use **Morning (Green Invoice)** API to auto-generate receipts for subscription payments.
- **Cost**: ~NIS 0.85-1.85 per subscription transaction. Negligible.

### v2 (Automated Marketplace Payments)
- **Payment processing**: **PayMe** — marketplace split payments (parent pays, platform takes fee, nanny receives payout).
- **Bit as payment method**: Via PayMe's Bit integration.
- **Invoicing**: PayMe's built-in invoicing OR Morning API.
- **SHAAM compliance**: Via PayMe or Morning.
- **Installments**: Via PayMe (if needed for larger packages).

### v3 (Scale)
- Monitor **Rapyd**, **Airwallex**, and **Revolut** for potentially better marketplace payment orchestration as they build out Israeli domestic capabilities.
- Consider **Stripe** if/when it launches in Israel (would be ideal for marketplace payments via Stripe Connect, but no timeline exists).

---

*This research is based on web searches conducted on 2026-03-07. Pricing and capabilities should be verified directly with providers before making purchasing decisions.*
