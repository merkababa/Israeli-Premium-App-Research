# Operationalizing Background Checks for a Nanny/Babysitter Platform in Israel (2026)

**Research Date:** March 7, 2026
**Status:** Deep-dive research to close Gap G1
**Complements:** `NANNY_PLATFORM_SAFETY_LEGAL_RESEARCH.md` (legal framework)

---

## TABLE OF CONTENTS

1. [Criminal Record Certificate (Teudat Yosher) -- Full Process](#1-criminal-record-certificate-teudat-yosher--full-process)
2. [Sex Offense Clearance Certificate -- Separate Track](#2-sex-offense-clearance-certificate--separate-track)
3. [Sex Offender Registry -- Access and Limitations](#3-sex-offender-registry--access-and-limitations)
4. [The 2019 Criminal Information Law -- What Changed for Employers](#4-the-2019-criminal-information-law--what-changed-for-employers)
5. [How Existing Israeli Childcare Organizations Handle Background Checks](#5-how-existing-israeli-childcare-organizations-handle-background-checks)
6. [Practical Operationalization for the Platform](#6-practical-operationalization-for-the-platform)
7. [Key Risks and Gaps](#7-key-risks-and-gaps)
8. [Recommended Workflow](#8-recommended-workflow)
9. [Sources](#9-sources)

---

## 1. CRIMINAL RECORD CERTIFICATE (TEUDAT YOSHER) -- FULL PROCESS

The Criminal Information Certificate (תעודת מידע פלילי), commonly called "Teudat Yosher" (תעודת יושר), is issued by the Israel Police. It is the standard criminal background document in Israel.

### 1.1 How to Obtain One

There are **two channels** for Israeli citizens:

| Channel | Details |
|---------|---------|
| **Online (gov.il)** | Israeli citizens with a gov.il account can apply through the Israel Police online service at `gov.il/he/service/request-for-criminal-information-certificate`. The certificate is generated digitally and sent to the applicant's email in both Hebrew and English. |
| **In-person** | Visit the nearest Israel Police station and fill out a dedicated request form. In Jerusalem, applicants go to Migrash Harusim. Must bring teudat zehut (ID card). |

For non-citizens/foreigners: Must obtain a police clearance from their country of citizenship, even if they never lived there. In Israel, foreigners who resided 3+ months can also obtain an Israeli certificate.

For Israelis abroad: Must apply through an Israeli embassy/consulate or via a trusted representative with notarized power of attorney.

### 1.2 Current Cost

**KEY FINDING: The basic criminal information certificate is FREE of charge for use within Israel.**

| Service | Cost |
|---------|------|
| Criminal Information Certificate (domestic use) | **FREE (NIS 0)** |
| Apostille stamp (for international use) | NIS 35 |
| Notarial translation (if needed) | Additional fee |
| Attorney-assisted service (expedited) | NIS 200-500+ (private market) |

Note: Some older sources cite NIS 45-47 or NIS 60. Based on current (2025) information from the Decker, Pex, Levi law firm and the gov.il service description, the certificate itself is free. The discrepancy may reflect fees for apostille, authentication, or attorney services bundled into the cost.

**Sources:**
- [Decker, Pex, Levi Law Firm -- Police Clearance Certificate](https://lawoffice.org.il/en/police-clearance-certificate/): "An Israeli PCC is free of charge, whether for use in Israel or when sent abroad (35 NIS for an apostille aside)."
- [Gov.il -- Criminal and Traffic Violation Record Service](https://www.gov.il/en/service/criminal-and-traffic-violation-record)

### 1.3 Processing Time

| Method | Timeframe |
|--------|-----------|
| Online (digital, sent to email) | **7-10 business days** |
| In-person at police station | **2-4 weeks** |
| Through embassy/consulate (abroad) | **Up to 1 month** |
| Attorney-assisted (expedited) | **Up to 3 days** (per attorney offices) |

### 1.4 What the Certificate Shows

**Shows:**
- Presence or absence of a criminal record
- Active criminal convictions that have NOT expired (under the statute of limitations / rehabilitation period)
- Pending cases awaiting trial (cases under "מב"ד" status)
- Court sentences received

**Does NOT show:**
- Expunged convictions (those past the rehabilitation/expiry period under the 2019 law)
- Convictions from OUTSIDE Israel (critical gap)
- Police investigations that did not lead to charges
- Administrative violations
- Offense details appear in **Hebrew only**, even on the bilingual certificate

### 1.5 Validity Period

**CONFLICTING INFORMATION -- CONTEXT-DEPENDENT:**

| Context | Stated Validity |
|---------|----------------|
| General use (Australian Embassy, NZ Embassy) | **1 year** from date of issue |
| Immigration/visa purposes (Chaim V'Chessed, NBN) | **6 months** from date of issue |
| Some Israeli attorney sources | **3 months** |
| Employer best practice | Point-in-time check; should be re-run periodically |

**Resolution:** The certificate itself does not have a legally mandated expiration date. The validity period is determined by the **requesting institution's policy**. For platform purposes, we should set our own policy (recommended: require renewal every 12 months, with the understanding that it's a point-in-time check).

### 1.6 Digital Certificate Format

Since at least 2023, the Israel Police issues **digital certificates** that are sent directly to the applicant's email. The certificate is bilingual (Hebrew and English), though conviction details are in Hebrew only. This is significant for platform operationalization -- nannies can forward the digital PDF to the platform.

---

## 2. SEX OFFENSE CLEARANCE CERTIFICATE -- SEPARATE TRACK

**This is a DIFFERENT document from the general criminal record certificate (Teudat Yosher).** This distinction is critical.

### 2.1 Legal Basis

The **Law for Prevention of Employment of Sex Offenders in Certain Institutions (5761-2001)** requires covered institutions to obtain a specific certificate from Israel Police confirming the applicant is NOT on the sex offender registry.

### 2.2 Process

| Aspect | Detail |
|--------|--------|
| **Who requests** | The **employer/institution**, NOT the individual |
| **How** | Candidate submits a dedicated form to Israel Police, co-signed by the employer |
| **What it checks** | The national sex offender registry (established by 2006 law) |
| **Who receives** | The certificate is sent **directly to the requesting employer**, not to the individual |
| **Processing time** | Several business days (routine) |
| **Scope** | Sex offenses ONLY -- not general criminal history |

### 2.3 Who Must Obtain This

The law explicitly covers:
- Kindergartens and daycare centers
- Educational institutions
- Organizations serving minors
- Community centers and recreational facilities
- **Volunteer positions** involving contact with children
- Employers providing services to children and disabled/mentally ill people

### 2.4 The Male-Only Anomaly

Multiple sources indicate that the mandatory police sex offense confirmation requirement applies to **"all male candidates"** specifically. This appears to be a legislative quirk that may have been updated, but multiple current (2024-2025) legal guides still reference this gender-specific language.

**Platform implication:** Regardless of the law's gendered language, the platform should require this check for ALL nanny/babysitter candidates of any gender.

---

## 3. SEX OFFENDER REGISTRY -- ACCESS AND LIMITATIONS

### 3.1 Registry Status

Israel has maintained a **non-public** national sex offender registry since the **Law for Community Protection from Sex Offenders (2006)**. Key facts:

| Aspect | Detail |
|--------|--------|
| **Maintained by** | Israel Police |
| **Public access** | **NO** -- registry is not searchable by the public |
| **Accessible to** | Law enforcement, prison services, authorized employers (under the 2001 law) |
| **Notification system** | Police can notify relevant institutions (schools, youth organizations) when a registered offender lives or works nearby |
| **Supervision** | The Tsur unit (prison service) supervises released offenders classified as medium+ danger level, with restrictions lasting up to 5 years |

### 3.2 Legislative Efforts for a Public Registry

Multiple Knesset members have proposed creating a public sex offender registry:

| Proposer | Proposal | Status |
|----------|----------|--------|
| MK Eli Afalo (17th Knesset) | Pedophile database + mandatory preventive medication | **Stalled in committee** |
| MK Oded Forer | Court-managed database open to public, with exceptions for treated/single offenders after 7 years | **Stalled in committee** |
| Various other MKs | Similar proposals | **All stalled** |

**As of 2026, Israel still has no public sex offender registry.** All proposals have failed, primarily due to privacy rights arguments and rehabilitation concerns.

### 3.3 Critical Limitation: No Foreign Coverage

The registry only contains offenders convicted **in Israel**. This is a well-documented gap:
- A sex offender convicted abroad who makes aliyah or enters Israel may show a completely clean record
- Child protection advocates (Jewish Community Watch, ECPAT) have repeatedly flagged this as a critical vulnerability
- No international data-sharing agreement for sex offender registries exists between Israel and other countries

### 3.4 Can the Platform Access the Registry?

**Not directly.** The platform cannot query the registry itself. The legal pathway is:

1. The platform must qualify as a "covered institution" under the 2001 law, OR
2. The platform must structure itself as the employer (or act through an employer entity), OR
3. The nanny must obtain the sex offense clearance through a different qualifying employer and share proof

**This is the single most important legal structuring question for the platform's background check process.**

---

## 4. THE 2019 CRIMINAL INFORMATION LAW -- WHAT CHANGED FOR EMPLOYERS

### 4.1 The Law

The **Criminal Information and Rehabilitation of Offenders Law (5779-2019)** came into force on **July 12, 2022** (after multiple delays). It replaced the Criminal Register and Rehabilitation of Offenders Law (5741-1981).

### 4.2 What Changed -- Critical for the Platform

| Before (1981 Law) | After (2019 Law) |
|--------------------|-------------------|
| Employers routinely asked candidates to obtain and present their criminal record | **PROHIBITED.** Employers not authorized by law cannot request criminal information in any form |
| Employers could ask candidates to sign affidavits about criminal history | **PROHIBITED.** Cannot request affidavits or written questionnaires about criminal past |
| Employers could use publicly available criminal information | **PROHIBITED.** Cannot take into account ANY public information about criminal record |
| Violation was a civil matter | **CRIMINAL SANCTIONS** for violations |

### 4.3 The Exceptions

The 2019 law preserves specific exceptions for employers who ARE authorized by law to access criminal information:

| Exception | Legal Basis |
|-----------|-------------|
| Government security employers | Specified by the law |
| Institutions working with children, disabled, or mentally ill persons | **Law for Prevention of Employment of Sex Offenders (2001)** |
| Certain regulated professions | Various sector-specific laws |

**KEY FINDING:** Employers providing services to children **remain legally required** to obtain sex offense clearance. The 2019 law did NOT remove this obligation -- it actually strengthened the dichotomy: most employers CANNOT check criminal records, but childcare employers MUST check for sex offenses.

### 4.4 Implications for the Platform

This creates a legal tension:

1. **General criminal record (Teudat Yosher):** The platform likely CANNOT require nannies to provide this, because the 2019 law prohibits employers from requesting criminal information unless specifically authorized. A platform that is not the direct employer may face even murkier legal standing.

2. **Sex offense clearance:** The platform likely CAN and arguably MUST require this, IF it qualifies as a covered institution under the 2001 law.

3. **Workaround for general criminal records:** The nanny can VOLUNTARILY provide their criminal record certificate. The law prohibits the employer from REQUESTING it, but does not prohibit the individual from voluntarily sharing it. However, relying on "voluntary" sharing as a platform requirement is legally dubious.

**LEGAL COUNSEL REQUIRED:** The exact legal structuring of whether the platform can require criminal record certificates from nannies needs to be confirmed by Israeli employment law counsel. The answer depends on:
- Whether the platform is classified as an employer, a marketplace, or an institution
- Whether the 2001 sex offender employment law's definition of "institution" covers digital matching platforms
- Whether the "voluntary" sharing pathway is legally defensible

---

## 5. HOW EXISTING ISRAELI CHILDCARE ORGANIZATIONS HANDLE BACKGROUND CHECKS

### 5.1 Licensed Daycare Centers (Maon Yom)

Under the **Daycare Supervision Law (2018)**:
- A government commissioner must run background checks on ALL daycare staff
- The commissioner updates a public list of all facilities and their license status
- This covered approximately 100,000 workers
- Implementation faced significant delays (the ministry admitted in 2019 it could not complete checks for all workers before the law took effect)
- Enforcement transferred to Education Ministry in 2022
- Operating without a license is now a criminal offense (up to 1 year imprisonment)

Budget: The Knesset allocated ILS 280 million (EUR 66 million) for implementation, mostly for supervision and enforcement.

### 5.2 Private Nanny Agencies

**Rockmybaby Israel** (international agency with Israel office):
- States all nannies and babysitters are "fully screened, interviewed and reference checked"
- Specific screening procedures not publicly disclosed
- Likely includes sex offense clearance (as a childcare institution) and reference verification

**City Sitters** (Tel Aviv-focused):
- Claims "highest standard of babysitters"
- Specific verification process not publicly documented

**Nanny Poppins Israel:**
- Operates primarily through Facebook and direct contact
- Verification process not publicly documented

**Concierge-Me:**
- Operates in Tel Aviv, Herzliya, Jerusalem
- Verification process not publicly documented

### 5.3 Digital Platforms Operating in Israel

**Babysits (babysits.co.il):**
- Requires **ID verification** for all members before messaging
- Offers optional criminal record checks via partnership with **Sterling** (international background check provider)
- Babysitters who complete a check receive a "background checked" badge
- Also screens messages automatically for fraud
- Identity verification available through email, phone, or connected social profiles

**Helpbook.co.il:**
- Israel's leading babysitter job board
- Features video profiles and recommendations
- Background check process not publicly documented

### 5.4 International Platform Precedent (Care.com)

- Requires ALL caregivers to undergo enhanced screening including criminal background check
- Profile displays a "background checked" badge
- Report details are NOT shared with families (only pass/fail badge)
- Active sitters are subject to **ongoing criminal history monitoring**
- Partnerships with background check providers (Checkr, Sterling)
- Does NOT operate in Israel specifically but sets industry standard

---

## 6. PRACTICAL OPERATIONALIZATION FOR THE PLATFORM

### 6.1 Can the Platform Require Nannies to Upload Their Criminal Record Certificate?

**Legal analysis:**

| Scenario | Can Require? | Risk Level |
|----------|-------------|------------|
| Platform structured as employer | Likely YES for sex offense cert; RISKY for general criminal cert (2019 law restricts) | Medium |
| Platform structured as marketplace | NO direct legal basis to require general criminal cert; CAN encourage voluntary submission | High |
| Platform structured as "institution" under 2001 law | YES for sex offense cert; still restricted on general criminal cert | Low-Medium |

**Practical answer:** The platform should:
1. **Require** the sex offense clearance certificate (this is legally supported and arguably mandatory)
2. **Strongly encourage** (but frame carefully) the voluntary provision of a general criminal record certificate
3. Consult legal counsel on exact language to avoid running afoul of the 2019 law

### 6.2 Can the Platform Verify the Certificate's Authenticity?

**Challenge:** There is NO Israel Police API or verification portal that allows third parties to verify a certificate's authenticity by entering a certificate number or QR code.

**Available verification methods:**

| Method | Reliability | Practicality |
|--------|-------------|-------------- |
| Visual inspection of the digital PDF (watermarks, formatting, Israel Police logos) | Low-Medium | Easy |
| Cross-check applicant details (name, ID number) against the certificate | Medium | Easy |
| Require the certificate to be dated within a specific window (e.g., last 90 days) | Medium | Easy |
| Require the sex offense certificate to be sent directly from police to platform (as the requesting "employer") | **High** | Complex (requires legal structuring) |
| Partner with Sterling or Checkr (international BG check providers with Israel capability) | **High** | Moderate cost |
| Request the digital certificate be forwarded directly from the gov.il system (check email metadata) | Medium | Technical |

### 6.3 Manual Workflow for Background Checks

**Recommended two-track process:**

#### Track 1: Sex Offense Clearance (MANDATORY)

```
1. Nanny registers on platform
2. Platform provides nanny with the sex offense clearance form
   (requires platform's signature as requesting institution)
3. Nanny submits form to Israel Police (online or in-person)
4. Israel Police sends certificate directly to platform
   (NOT to the nanny -- this is the standard process)
5. Platform reviews certificate
6. If clear --> nanny is approved for this dimension
7. If flagged --> nanny is rejected (no appeal through platform)
8. Re-check: every 12 months
```

**Prerequisite:** Platform must be legally structured as a "covered institution" under the 2001 law. This may require:
- Registering as an organization/company that provides childcare services
- Legal opinion confirming the platform qualifies
- Possibly obtaining a specific authorization from the relevant ministry

#### Track 2: General Criminal Record (VOLUNTARY/ENCOURAGED)

```
1. During onboarding, platform explains that a clean criminal
   record certificate enhances profile trust
2. Nanny obtains certificate independently via gov.il (free,
   digital, sent to their email)
3. Nanny uploads the digital PDF to the platform
4. Platform performs visual verification checks
5. Profile receives "criminal record verified" badge
6. Badge expires after 12 months; nanny prompted to renew
```

**Critical language consideration:** The platform should NOT "require" this as a condition, but should make it a practical prerequisite for receiving bookings (e.g., families can filter for verified nannies, unverified profiles are ranked lower).

### 6.4 Cost to the Platform

| Item | Cost per Nanny | Frequency |
|------|---------------|-----------|
| Sex offense clearance processing | Free (police service) | Annual |
| General criminal record certificate | Free for nanny (gov.il) | Annual |
| Sterling/Checkr partnership (if used) | ~$30-$80 per check (international benchmark) | Annual |
| Legal structuring as covered institution | One-time legal cost (NIS 5,000-20,000 estimated) | One-time |
| Staff time for manual verification | Internal cost | Ongoing |

---

## 7. KEY RISKS AND GAPS

### 7.1 No Foreign Criminal Record Coverage

The most critical gap: Israeli background checks only cover convictions in Israel. For a nanny who immigrated from Ethiopia, Russia, France, or anywhere else, their Israeli record will be clean even if they have convictions abroad.

**Mitigation options:**
- Require country-of-origin police clearance for nannies who are not native-born Israelis (adds friction and cost)
- Partner with an international background check provider (Sterling, Checkr)
- Accept the gap and disclose it to families in the terms of service

### 7.2 No Real-Time Monitoring

The certificate is a point-in-time snapshot. If a nanny is convicted of a crime after obtaining the certificate, the platform will not be notified.

**Mitigation options:**
- Require annual renewal of all certificates
- Build a system to check Hebrew-language court records (complex, possibly legally restricted)
- Partnership with providers offering ongoing monitoring (Care.com model)

### 7.3 No API for Verification

Israel Police does not provide an API for certificate verification. All verification must be manual or through third-party providers.

**Mitigation:**
- Build internal verification procedures (visual checks, metadata analysis)
- For sex offense certificates: rely on direct-from-police delivery (highest trust)
- Partner with Sterling/Checkr for automated checks

### 7.4 The 2019 Law Creates Legal Ambiguity

The platform cannot simply "require" a general criminal record certificate from nannies. The 2019 law makes it a criminal offense for unauthorized employers to request criminal information.

**Mitigation:**
- Focus mandatory requirements on the sex offense clearance (legally clear)
- Frame general criminal record as "optional verification that enhances your profile"
- Get legal opinion on exact permissible language
- Consider structuring as a regulated childcare entity to gain authorized access

### 7.5 Certificate Fraud Risk

Without an API, there is a risk of forged certificates. A bad actor could create a fake PDF.

**Mitigation:**
- For sex offense certs: insist on direct police-to-platform delivery
- For general certs: verify formatting, watermarks, and cross-reference personal details
- Partner with background check provider for independent verification
- Random audit a percentage of submitted certificates

### 7.6 Daycare vs. Private Nanny Regulatory Gap

The Daycare Supervision Law (2018) applies to facilities with 7+ children. Private nannies in family homes are in a regulatory gray zone -- there is no explicit law requiring background checks for private household nannies. The platform is stepping into this gap voluntarily, which is a competitive advantage but also means there is no regulatory framework to lean on.

---

## 8. RECOMMENDED WORKFLOW

### 8.1 MVP Phase (Launch)

**Mandatory for all nannies:**
1. Sex offense clearance certificate (platform acts as requesting institution)
2. ID verification (teudat zehut scan + selfie match)
3. At least 2 reference checks (former families or employers)
4. Self-declaration form (no criminal history, signed digitally)

**Strongly encouraged (badge-based):**
5. General criminal record certificate (voluntary upload, "verified" badge)
6. First aid certification (MDA or equivalent, "first aid certified" badge)

### 8.2 Growth Phase

7. Partner with Sterling or Checkr for automated background screening
8. Add country-of-origin police clearance requirement for non-native Israelis
9. Implement annual re-verification reminders and badge expiration
10. Explore ongoing monitoring capabilities

### 8.3 Premium Phase

11. Real-time background monitoring partnership
12. International criminal record checks for all nannies
13. Psychological assessment or interview component
14. Platform-funded background checks (absorb cost as trust investment)

---

## 9. SOURCES

### Official Government Sources
- [Gov.il -- Apply for Criminal or Traffic Offenses Information Certificate](https://www.gov.il/en/service/criminal-and-traffic-violation-record)
- [Gov.il -- Requests for Information from Israel Police](https://www.gov.il/en/pages/requests-for-information-from-the-israel-police)
- [Israel Ministry of Foreign Affairs -- Request for Authenticated Criminal Information Certificate](https://embassies.gov.il/england/en/services/israeli-citizens-foreign-citizens/request-authenticated-criminal-information-certificate)
- [Israel Ministry of Foreign Affairs -- Digital Criminal Information Certificate](https://embassies.gov.il/singapore/en/announcements/digital-criminal-information-certificate-hebrew-and-english)
- [Library of Congress -- Israel: Additional Restriction on Sex Offenders (2017)](https://www.loc.gov/item/global-legal-monitor/2017-05-16/israel-additional-restriction-on-sex-offenders/)

### Legal Analysis Sources
- [Herzog Fox & Neeman -- The Criminal Information and Rehabilitation of Offenders Law 2019](https://herzoglaw.co.il/en/news-and-insights/the-criminal-information-and-rehabilitation-of-offenders-law-2019/)
- [Decker, Pex, Levi Law Firm -- How to Issue a Police Clearance Certificate](https://lawoffice.org.il/en/police-clearance-certificate/)
- [Multiplier -- Employee Background Checks in Israel](https://www.usemultiplier.com/israel/background-checks)
- [Veremark -- Background Screening Checks in Israel](https://www.veremark.com/country/israel)
- [Ius Laboris -- Major Amendment to Privacy Law in Israel](https://iuslaboris.com/insights/major-amendment-to-privacy-law-in-israel/)
- [Lexology -- Employer's Right to Seek Criminal Information in Israel](https://www.lexology.com/library/detail.aspx?g=1feb4113-d85e-499b-a395-e530436e7890)

### Media and Investigative Sources
- [Haaretz -- Despite Law, No Time to Require Criminal Checks for Day Care Employees](https://haaretz.com/israel-news/.premium-despite-law-no-time-to-require-criminal-checks-for-israel-s-day-care-employees-1.7529006)
- [Quartz -- Israel Has a Child Safety Problem, It Just Passed a Law to Fix It](https://qz.com/1439009/israel-has-a-child-safety-problem-it-just-passed-a-law-to-fix-it)
- [Times of Israel -- Diaspora Pedophiles Increasingly Use Israel as 'a Haven'](https://www.timesofisrael.com/diaspora-pedophiles-increasingly-use-israel-as-a-haven-activists-charge/)
- [Humanium -- Exposing Pedophilia and Legal Failures in Israel](https://www.humanium.org/en/exposing-pedophilia-and-legal-failures-in-israel/)
- [CaughtDok -- Israel Does Have a Sex Offender Registry But It Is Not Public](https://www.caughtdok.org/2023/04/18/israel-does-have-a-sex-offender-registry-but-it-is-not-public/)
- [Avi Dubitzky -- Why Is There No Sex Offender Registry in Israel?](https://avihunter.com/?p=2090)

### Immigration and Olim Resources
- [Chaim V'Chessed -- Obtaining a Background Check](https://chaimvchessed.com/information/legal-financial/obtaining-a-background-check/)
- [Nefesh B'Nefesh -- Background Checks](https://www.nbn.org.il/background-checks/)
- [Canada.ca -- How to Get a Police Certificate, Israel](https://www.canada.ca/en/immigration-refugees-citizenship/services/application/medical-police/police-certificates/how/israel.html)
- [Australian Embassy -- Israel Police/Criminal Information Certificate](https://israel.embassy.gov.au/tavv/eng_visas_11.html)
- [Visit Ukraine -- How to Obtain Certificate of No Criminal Record in Israel](https://visitukraine.today/blog/6416/how-to-obtain-a-certificate-of-no-criminal-record-in-israel-instructions-and-details)

### Platform and Industry Sources
- [Babysits -- Trust & Safety](https://www.babysits.com/trust/)
- [Babysits -- Background Check Help](https://www.babysits.com/help/background-check/)
- [Care.com -- Safety Background Checks](https://www.care.com/about/safety/background-checks/)
- [Checkr -- Israel Background Screening](https://help.checkr.com/s/article/7891551152535-Israel-Background-Screening)

### Israeli Childcare Law and Policy
- [Van Leer Foundation -- Israel's Lawmakers Take Responsibility for Supervising Childcare Providers](https://vanleerfoundation.org/news/israels-lawmakers-take-responsibility-for-supervising-childcare-providers/)
- [Springer -- Reforming Inspection of Childcare Provision: Lessons from Israel](https://link.springer.com/article/10.1007/s13158-024-00390-5)
- [Taub Center -- Early Childhood Education and Care in Israel: An Overview](https://www.taubcenter.org.il/wp-content/uploads/2023/12/Early-Childhood-2023-ENG-1.pdf)
- [Anglo-List -- Safety and Security in Israel's Daycare, Kindergartens and Preschools](https://anglo-list.com/israel-daycare-safety-security/)

---

## SUMMARY OF KEY FINDINGS

| Question | Answer |
|----------|--------|
| How does someone obtain a criminal record certificate? | Online via gov.il (digital, sent to email) or in-person at police station |
| What is the current cost? | **FREE** for domestic use; NIS 35 for apostille |
| How long does it take? | 7-10 business days (online); 2-4 weeks (in-person) |
| What does it show? | Active convictions and pending cases; does NOT show expired/expunged convictions or foreign convictions |
| Validity period? | No legal expiration; receiving institution sets policy (typically 6-12 months) |
| Can the platform check the sex offender registry? | Only through the formal sex offense clearance process (requires legal structuring as a covered institution) |
| Is there a public sex offender registry? | **NO.** Registry is non-public. No Knesset proposal has succeeded. |
| Can the platform require nannies to upload criminal records? | **Legally complex.** The 2019 law prohibits unauthorized employers from requesting criminal info. Sex offense clearance is the exception for childcare institutions. |
| Can the platform verify certificate authenticity? | No API exists. Verification is manual. Best approach: receive sex offense cert directly from police. |
| What is the recommended workflow? | Two-track: mandatory sex offense clearance + voluntary general criminal record with badge system |

---

**NEXT STEPS:**
1. Engage Israeli employment lawyer to confirm platform's legal standing under the 2001 sex offender employment law
2. Determine exact legal structure needed to qualify as a "covered institution"
3. Evaluate Sterling/Checkr partnership for automated screening
4. Design the onboarding flow with background check integration
5. Draft terms of service language that properly addresses the 2019 law restrictions
