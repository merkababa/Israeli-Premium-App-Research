# Emuni Nanny Platform — Complete Research Index

**Last Updated:** March 7, 2026
**Total Documents:** 27 (22 research + 1 audit + 4 gap-fill research)
**Total Lines:** ~15,331
**Audit Score:** 82/100 pre-corrections → ~90+/100 post-corrections
**Status:** PRD-READY (all corrections propagated, all critical gaps filled)

---

## HOW TO USE THIS INDEX

- **Starting from scratch?** Read MASTER_RESEARCH first, then FOUNDER_DECISIONS
- **Writing the PRD?** Read PRD_PLANNER_BRIEF.md for a guided reading plan
- **Looking for a specific topic?** Use the Topic Cross-Reference below
- **Checking data accuracy?** VERIFICATION_LOG has the audit trail; FINAL_AUDIT has the quality grades

---

## DOCUMENT MAP BY LAYER

```
LAYER 4 — META (read first)
├── RESEARCH_INDEX.md .................. This file — navigation guide
├── NANNY_PLATFORM_FINAL_AUDIT.md ..... Quality audit, all errors, grades
└── NANNY_PLATFORM_VERIFICATION_LOG.md  64+ verified claims, corrections

LAYER 3 — SYNTHESIS (canonical source of truth)
├── NANNY_PLATFORM_MASTER_RESEARCH.md . Single source of truth for all data
├── NANNY_PLATFORM_FOUNDER_DECISIONS.md 10 canonical decisions (pricing, geography, etc.)
└── NANNY_PLATFORM_PRD_READINESS.md ... PRD structure, open questions

LAYER 2 — DOMAIN RESEARCH (deep dives)
├── Legal cluster
│   ├── NANNY_PLATFORM_LEGAL_FRAMEWORK.md ........ Employment law, classification
│   ├── WOLT_ISRAEL_LEGAL_DEEP_DIVE.md ........... Wolt case, 9 control factors
│   ├── NANNY_PLATFORM_SAFETY_LEGAL_RESEARCH.md .. Child protection, Care.com
│   ├── NANNY_PLATFORM_BACKGROUND_CHECK_RESEARCH.md [NEW] Operationalizing checks
│   ├── NANNY_PLATFORM_PRIVACY_AMENDMENT_13_RESEARCH.md [NEW] Data protection
│   └── NANNY_PLATFORM_COMPETITOR_LEGAL_UPDATE_2026.md [NEW] Wolt appeal status
│
├── Financial cluster
│   ├── NANNY_PLATFORM_BUSINESS_MODEL_STRATEGY.md  Revenue models, B2B, projections
│   ├── NANNY_PLATFORM_REVENUE_MODEL_REVISED.md .. Corrected revenue, fee legality
│   ├── NANNY_PLATFORM_COST_MODEL.md ............. Burn rate, salaries, funding
│   ├── NANNY_PLATFORM_MONETIZATION_STRATEGY.md .. When/how to charge, freemium
│   ├── NANNY_PLATFORM_FUNDING_RESEARCH.md ....... IIA grants, VC, angels
│   ├── NANNY_PLATFORM_PAYMENT_TAX_RESEARCH.md ... PayMe, VAT, SHAAM, tax
│   └── NANNY_PLATFORM_PAYMENT_PROCESSOR_COMPARISON.md [NEW] PayMe vs PayPlus vs Tranzila
│
├── Market cluster
│   ├── CUSTOMER_RESEARCH_NANNY_BABYSITTER.md .... Pain points, sizing, segments
│   ├── NANNY_PLATFORM_GLOBAL_LANDSCAPE.md ....... 10+ global platforms analyzed
│   └── NANNY_PLATFORM_COMPETITOR_LEGAL_UPDATE_2026.md [NEW] 2026 competitor scan
│
└── Strategy/Product cluster
    ├── NANNY_PLATFORM_MVP_SCOPE.md .............. RICE scoring, v1/v2/v3
    ├── NANNY_PLATFORM_MATCHING_FLOW.md .......... 4-tier booking, algorithm, UX
    ├── NANNY_PLATFORM_TECH_RESEARCH.md .......... Stack, AU10TIX, WhatsApp, IS 5568
    ├── NANNY_PLATFORM_GROWTH_STRATEGY.md ........ Cold start, first 200, viral
    ├── NANNY_PLATFORM_LAUNCH_GEOGRAPHY.md ....... Old North TLV beachhead
    ├── NANNY_PLATFORM_NAMING_RESEARCH.md ........ "Emuni" recommendation
    └── NANNY_PLATFORM_COFOUNDER_RESEARCH.md ..... CTO search, equity splits
```

---

## ALL 27 DOCUMENTS — SUMMARY TABLE

| # | Document | Lines | Grade | Key Takeaway |
|:-:|----------|------:|:-----:|--------------|
| 1 | **MASTER_RESEARCH** | 600 | 82 | Single source of truth. NIS 22.8B TAM, NIS 49/mo subscription, hybrid revenue, pure marketplace structure. |
| 2 | **FOUNDER_DECISIONS** | 608 | 85 | 10 canonical decisions. Emuni name, NIS 49/mo, Old North TLV, Hebrew-first, freemium Day 1, no in-app payments v1. |
| 3 | **PRD_READINESS** | 489 | 80 | PRD structure template, open questions list, readiness assessment: GO. |
| 4 | **LEGAL_FRAMEWORK** | 540 | 79 | Israeli employment law. Family = employer. Platform = marketplace. Fee structure irrelevant to classification. Employment bureau license recommended. |
| 5 | **WOLT_DEEP_DIVE** | 563 | 86 | Wolt case 35327-08-20. 9 control factors that caused employer classification. Tax fraud (NIS 33.5M). Appeal pending — AG favors case-by-case analysis. |
| 6 | **SAFETY_LEGAL_RESEARCH** | 628 | 80 | Child protection laws, background check requirements, mandatory reporting, Care.com failures. |
| 7 | **BACKGROUND_CHECK_RESEARCH** | 520 | NEW | Criminal cert is FREE. 2019 law: illegal to require general criminal checks. Sex offense clearance IS mandatory for childcare. Two-track system needed. Must qualify as "covered institution." |
| 8 | **PRIVACY_AMENDMENT_13** | 556 | NEW | Amendment 13 live since Aug 2025. No small biz exemption. Mandatory DPO, 72-hr breach notification. Compliance cost NIS 140-395K/yr. PPA actively enforcing. |
| 9 | **COMPETITOR_LEGAL_UPDATE** | 243 | NEW | No new Israeli nanny platform in 2025-2026. Window wide open. Wolt appeal unresolved; AG position favorable. No gig worker legislation enacted. |
| 10 | **BUSINESS_MODEL_STRATEGY** | 1,150 | 65→80 | Revenue models comparison. Rewritten with corrected projections (Y3: NIS 7.6-9.4M). Sensitivity analysis added. Free + NIS 49 Premium. |
| 11 | **REVENUE_MODEL_REVISED** | 259 | 72→85 | Corrected revenue model. Israeli precedents (Fiverr, Midrag, Gett). Fee legality confirmed. Y1: NIS 640-820K. Breakeven Mo 20-26. |
| 12 | **COST_MODEL** | 628 | 88 | Pre-launch burn: NIS 143K/mo. Launch burn: NIS 329K/mo. NIS 7M seed recommended. Stripe NOT available — use PayMe/PayPlus. |
| 13 | **MONETIZATION_STRATEGY** | 461 | 84 | Freemium from Day 1. Free tier: browse + 1 booking/mo. Premium: NIS 49/mo. Per-contact: NIS 19. Israeli WTP analysis. VAT 18%. |
| 14 | **FUNDING_RESEARCH** | 537 | 90 | IIA Tnufa: NIS 200K (free). Pre-seed: up to NIS 1.5M (IIA matches 60%). Angels: NIS 1-1.5M. Total: NIS 2-3.15M at 10-12% dilution. |
| 15 | **PAYMENT_TAX_RESEARCH** | 454 | 92 | PayMe recommended. VAT 18%. SHAAM e-invoicing mandatory (NIS 5K threshold, June 2026 deadline). Stripe NOT in Israel. |
| 16 | **PAYMENT_PROCESSOR_COMPARISON** | 454 | NEW | PayMe confirmed — only Israeli processor with marketplace split payments. Negotiate to 1.2-1.6%. Tranzila cheapest but no splits. PayPlus mid-range. |
| 17 | **CUSTOMER_RESEARCH** | 556 | 88 | Parent pain points: trust (#1), availability (#2), cost (#3). 270K urban families addressable. Dual-income trend driving demand. |
| 18 | **GLOBAL_LANDSCAPE** | 1,010 | 78 | 10+ platforms: Care.com ($500M+), UrbanSitter ($49.52M, acquired Kinside), Bubble, Helpr, Sittercity. Failures analyzed. |
| 19 | **MVP_SCOPE** | 581 | 86 | RICE-scored features. MVP = Advance Booking only (Tier 3). No emergency booking, no trust graph, no B2B. 8-12 week build. |
| 20 | **MATCHING_FLOW** | 943 | 85 | 4-tier booking system. Matching algorithm spec. Trust tiers (New→Verified→Trusted→Elite). WhatsApp post-booking. Cancellation policy. |
| 21 | **TECH_RESEARCH** | 610 | 83 | React Native + Expo, NestJS, PostgreSQL + PostGIS, Supabase, AWS il-central-1. AU10TIX for ID verification. No Police API. IS 5568 mandatory. |
| 22 | **GROWTH_STRATEGY** | 635 | 78 | Supply-first cold start. "Bring Your Nanny" viral mechanic. Anglo community beachhead. PMF = 10 bookings/week by week 12. **Superseded: Old North only (not 4 neighborhoods).** |
| 23 | **LAUNCH_GEOGRAPHY** | 748 | 84 | Old North TLV = single beachhead. 50 nannies in 5 km2 = 10/km2 density. Supersedes 4-neighborhood plan. Expansion path: Florentin → Ra'anana. |
| 24 | **NAMING_RESEARCH** | 460 | 80 | "Emuni" (My Trust) recommended. Hebrew root א-מ-ן. Global pronunciation works. Domain availability needs confirmation. |
| 25 | **COFOUNDER_RESEARCH** | 486 | 82 | Technical co-founder recommended (50/50). Saves NIS 744K/yr. Israeli VCs require founding team. CTO profile: React Native + Node.js. |
| 26 | **VERIFICATION_LOG** | 287 | 95 | 64+ claims verified, 23 corrected, 16 unverifiable flagged, 9 contradictions resolved. Corrections now propagated to all source docs. |
| 27 | **FINAL_AUDIT** | 325 | 95 | 4-auditor quality review. Weighted avg 82/100. All errors cataloged. Correction checklist (now completed). |

---

## TOPIC CROSS-REFERENCE

Use this to find exactly where a topic is covered:

### Legal & Compliance
| Topic | Primary Document | Also In |
|-------|-----------------|---------|
| Employment classification risk | LEGAL_FRAMEWORK | WOLT_DEEP_DIVE, REVENUE_MODEL_REVISED |
| Wolt case (9 control factors) | WOLT_DEEP_DIVE | MASTER_RESEARCH, LEGAL_FRAMEWORK |
| Wolt appeal status (2026) | COMPETITOR_LEGAL_UPDATE | — |
| Employment Service Law (nanny fees) | LEGAL_FRAMEWORK | REVENUE_MODEL_REVISED, FOUNDER_DECISIONS |
| Background checks (how to) | BACKGROUND_CHECK_RESEARCH | SAFETY_LEGAL_RESEARCH |
| Criminal record certificate | BACKGROUND_CHECK_RESEARCH | COST_MODEL |
| Sex offender registry | BACKGROUND_CHECK_RESEARCH | SAFETY_LEGAL_RESEARCH |
| Privacy / Amendment 13 | PRIVACY_AMENDMENT_13 | TECH_RESEARCH |
| IS 5568 accessibility | TECH_RESEARCH | — |
| Child protection / mandatory reporting | SAFETY_LEGAL_RESEARCH | — |
| Care.com failures | SAFETY_LEGAL_RESEARCH | GLOBAL_LANDSCAPE |
| Employment bureau license | LEGAL_FRAMEWORK | REVENUE_MODEL_REVISED |

### Financial
| Topic | Primary Document | Also In |
|-------|-----------------|---------|
| Revenue projections (canonical) | MASTER_RESEARCH | REVENUE_MODEL_REVISED, BUSINESS_MODEL_STRATEGY |
| Pricing decision (NIS 49/mo) | FOUNDER_DECISIONS | MONETIZATION_STRATEGY |
| Unit economics | BUSINESS_MODEL_STRATEGY | COST_MODEL |
| Burn rate / runway | COST_MODEL | — |
| Funding strategy (IIA + angels) | FUNDING_RESEARCH | FOUNDER_DECISIONS, COST_MODEL |
| Payment processors | PAYMENT_PROCESSOR_COMPARISON | PAYMENT_TAX_RESEARCH |
| VAT / tax / SHAAM | PAYMENT_TAX_RESEARCH | MONETIZATION_STRATEGY |
| B2B corporate revenue | BUSINESS_MODEL_STRATEGY | REVENUE_MODEL_REVISED |

### Product & Technology
| Topic | Primary Document | Also In |
|-------|-----------------|---------|
| MVP feature scope (v1/v2/v3) | MVP_SCOPE | FOUNDER_DECISIONS |
| Matching algorithm | MATCHING_FLOW | — |
| Booking system (4 tiers) | MATCHING_FLOW | MVP_SCOPE |
| Tech stack | TECH_RESEARCH | — |
| WhatsApp integration | TECH_RESEARCH | MATCHING_FLOW |
| ID verification (AU10TIX) | TECH_RESEARCH | — |

### Market & Growth
| Topic | Primary Document | Also In |
|-------|-----------------|---------|
| Market sizing (TAM/SAM/SOM) | CUSTOMER_RESEARCH | MASTER_RESEARCH |
| Parent pain points | CUSTOMER_RESEARCH | — |
| Israeli competitors (2026) | COMPETITOR_LEGAL_UPDATE | GLOBAL_LANDSCAPE |
| Global competitors | GLOBAL_LANDSCAPE | BUSINESS_MODEL_STRATEGY |
| Cold start / supply-first | GROWTH_STRATEGY | LAUNCH_GEOGRAPHY |
| Launch geography | LAUNCH_GEOGRAPHY | FOUNDER_DECISIONS |
| Viral mechanics | GROWTH_STRATEGY | — |
| PMF metrics | GROWTH_STRATEGY | MVP_SCOPE |

### Founder / Strategy
| Topic | Primary Document | Also In |
|-------|-----------------|---------|
| All 10 founder decisions | FOUNDER_DECISIONS | — |
| Company name ("Emuni") | NAMING_RESEARCH | FOUNDER_DECISIONS |
| Co-founder strategy | COFOUNDER_RESEARCH | FOUNDER_DECISIONS |
| Monetization timing | MONETIZATION_STRATEGY | FOUNDER_DECISIONS |

---

## CANONICAL DATA POINTS (SINGLE SOURCE OF TRUTH)

These are the final, verified numbers. If any document disagrees, it is wrong.

| Data Point | Value | Source |
|-----------|-------|--------|
| Subscription price | **NIS 49/mo** | FOUNDER_DECISIONS |
| Per-contact fee | **NIS 19** | FOUNDER_DECISIONS |
| Transaction fee | **12-15% on booking value** | MASTER_RESEARCH |
| VAT rate | **18%** | PAYMENT_TAX_RESEARCH |
| Y1 revenue | **NIS 640K-820K** | MASTER_RESEARCH (verified) |
| Y2 revenue | **NIS 2.5-3.5M** | MASTER_RESEARCH (verified) |
| Y3 revenue | **NIS 7.6-9.4M** | MASTER_RESEARCH (verified) |
| Breakeven | **Month 20-26** | MASTER_RESEARCH (verified) |
| Pre-launch burn | **NIS 143K/mo** | COST_MODEL |
| Launch burn | **NIS 329K/mo** | COST_MODEL |
| Seed round target | **NIS 7M** | COST_MODEL |
| TAM | **NIS 22.8B** | CUSTOMER_RESEARCH |
| SAM | **NIS 216M** | CUSTOMER_RESEARCH |
| SOM Y3 | **NIS 23.5M** | CUSTOMER_RESEARCH |
| Launch area | **Old North TLV** | LAUNCH_GEOGRAPHY |
| Target nanny density | **10/km2 (50 in 5 km2)** | LAUNCH_GEOGRAPHY |
| Tech stack | **React Native + NestJS + PostgreSQL** | TECH_RESEARCH |
| Payment processor | **PayMe (negotiate 1.2-1.6%)** | PAYMENT_PROCESSOR_COMPARISON |
| MVP build time | **8-12 weeks** | MVP_SCOPE |
| Background check cost | **FREE (criminal cert)** | BACKGROUND_CHECK_RESEARCH |
| Privacy compliance cost | **NIS 140-395K/yr** | PRIVACY_AMENDMENT_13 |
| Company name | **Emuni (אמוני)** | NAMING_RESEARCH |

---

## RESEARCH TIMELINE

| Round | Date | Agents | Documents Produced |
|-------|------|:------:|-------------------|
| 1 | Mar 7, 2026 | 6 | LEGAL_FRAMEWORK, WOLT_DEEP_DIVE, CUSTOMER_RESEARCH, SAFETY_LEGAL, GLOBAL_LANDSCAPE, BUSINESS_MODEL_STRATEGY |
| 2 | Mar 7, 2026 | 7 | REVENUE_MODEL_REVISED |
| 3 | Mar 7, 2026 | 1 | MATCHING_FLOW |
| 4 | Mar 7, 2026 | 4 | VERIFICATION_LOG |
| 5 | Mar 7, 2026 | 5 | MVP_SCOPE, PAYMENT_TAX, COST_MODEL, GROWTH_STRATEGY, TECH_RESEARCH |
| 6 | Mar 7, 2026 | 5 | MONETIZATION_STRATEGY, NAMING, LAUNCH_GEOGRAPHY, FOUNDER_DECISIONS, COFOUNDER_RESEARCH |
| Synthesis | Mar 7, 2026 | 2 | MASTER_RESEARCH, PRD_READINESS |
| Audit | Mar 7, 2026 | 5 | FINAL_AUDIT, corrections propagated to all source docs |
| Gap Fill | Mar 7, 2026 | 7 | BACKGROUND_CHECK, PAYMENT_PROCESSOR_COMPARISON, COMPETITOR_LEGAL_UPDATE, PRIVACY_AMENDMENT_13 |

---

## KNOWN REMAINING GAPS (P2 — Nice to Have)

These were not critical enough to block PRD but should be addressed eventually:

1. **Domain/trademark availability** for "Emuni" — not confirmed
2. **WhatsApp Business API** costs and approval process for Israel
3. **Insurance products** for childcare platforms in Israel
4. **IIA application** current processing times
5. **User interviews** — all research is secondary (surveys, CBS data); zero primary interviews
6. **AU10TIX** API documentation / technical feasibility spike
7. **Rockmybaby Israel** deep competitive intelligence

---

*This index was generated after completing all audit corrections and gap-fill research. All 27 documents are internally consistent as of March 7, 2026.*
