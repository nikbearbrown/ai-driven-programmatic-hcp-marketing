# Assertions Report: 01-the-machine-nobody-sees.md
**Date:** 2026-06-17
**Source file:** chapters/01-the-machine-nobody-sees.md
**Assertions flagged:** 7
**Breakdown:** STAT: 4 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 3 | SPECIALIST: 0 | CURRENT: 0

---
## ⚠️ Critical — Requires Immediate Expert Review
None found. No OUTDATED, CONTRADICTED, or COMBINATION-type assertions. All load-bearing empirical/citation claims resolved to primary or near-primary sources. Vendor capability figures are already attributed and contested in-text per the firewall.

---
## Full Findings

### EVIDENCE / STAT — CONFIRMED
**Assertion type:** I-LANGUAGE (reports a finding, hedged as association)
**Sentence:** "A study of 2013 Medicare Part D prescribers in the District of Columbia found that gift recipients prescribed 2.3 more claims per patient and 7.8% more branded drugs than non-recipients (Wood et al., ... *PLOS ONE* 2017; PMC5656307)."
**Claim checked:** Wood et al. 2017 reports 2.3 more claims/patient and 7.8% more branded drugs among DC gift recipients.
**Site visited:** PLOS ONE article id 10.1371/journal.pone.0186060; GW Milken press release; PMC5656307 (abstract via search index)
**Finding:** Confirmed exactly. Wood SF et al., PLOS ONE 12(10):e0186060 (2017): vs. non-recipients, gift recipients prescribed 2.3 more claims per patient, drugs costing ~$50 more per claim, and 7.8% more branded drugs. The chapter correctly frames this as association, not causation.
**Expert review needed:** No
**Suggested reference:** Wood SF, et al. Influence of pharmaceutical marketing on Medicare prescriptions in the District of Columbia. PLoS ONE. 2017;12(10):e0186060. https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0186060
**Notes:** The PMC full-text page is reCAPTCHA-gated to automated fetch; confirmed via the journal/press-release index instead.

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Dafny, Ho, and Kong (NBER working paper w29735, 2022) found that in the 12 months after a coupon was introduced, commercially insured purchases of the drug (measured in days of supply) rose by more than 20% relative to Medicare Advantage; for the multiple-sclerosis drug class they studied, they estimated that banning coupons would cut total spending by about $950 million, a 7.6% reduction in insurer costs."
**Claim checked:** Dafny/Ho/Kong w29735 (2022): >20% commercial-vs-MA quantity rise; ~$950M / 7.6% MS-class spending reduction from banning coupons.
**Site visited:** https://www.nber.org/papers/w29735 ; https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4034185
**Finding:** Confirmed. The paper reports coupon introductions increase quantity 23–25% in the commercial segment relative to Medicare Advantage (consistent with "more than 20%"). The MS-class spending/insurer-cost magnitudes are reported in the paper's counterfactual simulations. Author/venue/year exact.
**Expert review needed:** No
**Suggested reference:** Dafny L, Ho K, Kong E. How Do Copayment Coupons Affect Branded Drug Prices and Quantities Purchased? NBER Working Paper No. 29735, 2022. https://www.nber.org/papers/w29735
**Notes:** The accuracy-review log already corrected an earlier conflation; the corrected ">20%" framing matches the source. (Published version later appeared in AEJ: Economic Policy 16(3):314–46, 2024.)

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The earlier Dafny, Ody, and Schmitt study ... 2017 ... found that coupons increased branded sales by more than 60%, entirely by displacing lower-cost bioequivalent generics, raising total spending by an estimated $30–$120 million per drug."
**Claim checked:** Dafny/Ody/Schmitt 2017: 60+% branded sales increase via generic displacement, $30–120M per drug.
**Site visited:** https://www.aeaweb.org/articles?id=10.1257/pol.20150588 ; https://www.nber.org/papers/w22745
**Finding:** Confirmed exactly. AEJ: Economic Policy 9(2):91–123 (2017): coupons increase branded sales 60+%, entirely by reducing bioequivalent generic sales; total spending up $30–120M per drug over five years post-generic-entry.
**Expert review needed:** No
**Suggested reference:** Dafny L, Ody C, Schmitt M. When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization. American Economic Journal: Economic Policy. 2017;9(2):91–123. https://www.aeaweb.org/articles?id=10.1257/pol.20150588
**Notes:** None.

### STAT / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Point-of-care spending crossed $1 billion in annual spend in 2024, according to the Point of Care Marketing Association (POCMA); spending among reporting POCMA members grew roughly 171% from 2019 to 2023, reaching about $803 million (a compound annual growth rate near 22%) ..."
**Claim checked:** POCMA: >$1B POC revenue in 2024; 171% growth 2019→2023 reaching ~$803M.
**Site visited:** https://pocmarketing.org/resources-insights/point-of-care-revenue-surpassed-1-billion-in-2024-whats-driving-the-surge ; PR Newswire 302423737
**Finding:** Confirmed. POCMA: member revenue exceeded $1B in 2024; POC spending among reporting members grew 171% from 2019 to 2023, reaching ~$803M. The chapter correctly flags this as an industry-association figure, not an independent analyst finding.
**Expert review needed:** No
**Suggested reference:** Point of Care Marketing Association. Point of Care Revenue Surpassed $1 Billion in 2024. pocmarketing.org, 2024–2025. https://pocmarketing.org/resources-insights/point-of-care-revenue-surpassed-1-billion-in-2024-whats-driving-the-surge
**Notes:** Self-flagged as association framing; firewall-appropriate.

### EVIDENCE — CONFIRMED (mechanism / standards)
**Assertion type:** BASIC
**Sentence:** "CDS Hooks is an event-driven HTTP API: when a clinician opens a chart, selects an order, or signs a prescription, the EHR fires an HTTP request to a registered external service. ... `patient-view` ... `order-select` ... `order-sign`." (and the parallel SMART on FHIR / OAuth 2.0 description)
**Claim checked:** CDS Hooks and SMART on FHIR are real HL7 interoperability standards with the described hook types and OAuth 2.0 launch.
**Site visited:** cds-hooks.org / HL7 CDS Hooks 2.0; HL7 SMART App Launch v2.2.0 (standards-level, widely documented)
**Finding:** These are accurately described, well-established HL7 standards (CDS Hooks 2.0; SMART App Launch). The hook types (patient-view, order-select, order-sign) and the OAuth 2.0 token exchange are correct. This is standard textbook mechanism, not a contested claim.
**Expert review needed:** No
**Suggested reference:** HL7. CDS Hooks specification 2.0. https://cds-hooks.org/ ; HL7. SMART App Launch v2.2.0. http://hl7.org/fhir/smart-app-launch/
**Notes:** Vendor product mappings (Doceree Spark) are vendor self-reported and labeled as such in-text.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Doceree expanded into co-pay card delivery by launching co-pay.com in July 2025 ... (Doceree, PR Newswire, July 22, 2025)."
**Claim checked:** Doceree launched co-pay.com in July 2025.
**Site visited:** Doceree / PR Newswire (vendor announcement, dated)
**Finding:** Consistent with the vendor's own dated press release. This is a vendor announcement of its own product launch (a corporate fact, not an effectiveness claim) and is appropriately attributed. Confirmed as a dated vendor announcement.
**Expert review needed:** No
**Suggested reference:** Doceree. Press release on co-pay.com launch, PR Newswire, July 22, 2025.
**Notes:** Corporate-fact claim; not an effectiveness claim, so no causal verification needed.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "Somewhere upstream, a vendor's case study claims this kind of placement produces a '44% script lift.'" and the closing teardown's 44% | STAT | I-LANGUAGE (illustrative) | Vendor-attributed figure within the 4–44% firewall range; explicitly framed in-text as a claim to be flagged `[verify]`, never as independent evidence. No independent peer-reviewed validation exists. Treated as vendor-attributed by design. |

Note: vendor reach/integration counts (Doceree 150+ EHR integrations; OptimizeRx "300+ EHR systems / 2M+ physicians"; WebMD Ignite) are explicitly labeled vendor self-reported in-text ("a vendor confirming its own reach figure is not independent verification"). Not separately flagged — the chapter already discloses them as un-independently-verified.

---
## AI-Pass Flags
None. The chapter's empirical claims resolve to primary sources; the causal-vs-association distinction is applied consistently (e.g., the Wood study is explicitly held as association). No internal contradictions or definitional errors found. The "44% lift" is consistently treated as an unproven vendor claim throughout, including in the teardown section — the chapter's own thesis.
