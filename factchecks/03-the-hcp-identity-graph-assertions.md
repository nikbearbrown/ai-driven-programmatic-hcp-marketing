# Assertions Report: 03-the-hcp-identity-graph.md
**Date:** 2026-06-17
**Source file:** chapters/03-the-hcp-identity-graph.md
**Assertions flagged:** 5
**Breakdown:** STAT: 2 | GUIDELINE: 1 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 1 | CURRENT: 0

---
## ⚠️ Critical — Requires Immediate Expert Review
None found. No OUTDATED/CONTRADICTED/COMBINATION assertions. The two legal/empirical keystones (HIPAA Safe Harbor / Sorrell v. IMS Health; Public Citizen $42M) resolved to authoritative sources.

### EVIDENCE / GUIDELINE — CONFIRMED
**Assertion type:** BASIC / POSITIVE
**Sentence:** "The legal structure holding all of this in place was tested and confirmed by the Supreme Court in 2011. Vermont passed the Prescription Confidentiality Law in 2007 ... The Supreme Court struck the law down in *Sorrell v. IMS Health* as a violation of the First Amendment: data-mining of prescriber-identified data is constitutionally protected commercial speech."
**Claim checked:** Sorrell v. IMS Health (2011) struck down Vermont's 2007 prescriber-data law on First Amendment grounds.
**Site visited:** https://supreme.justia.com/cases/federal/us/564/552 ; https://en.wikipedia.org/wiki/Sorrell_v._IMS_Health_Inc.
**Finding:** Confirmed exactly. Sorrell v. IMS Health Inc., 564 U.S. 552 (2011), decided June 23/27, 2011 (6–3, Kennedy). Struck down Vermont's 2007 Prescription Confidentiality Law restricting sale/use of prescriber-identified data for marketing, applying heightened First Amendment scrutiny. The chapter's holding and consequence ("states cannot simply pass laws restricting prescriber data-mining") are accurate.
**Expert review needed:** No
**Suggested reference:** Sorrell v. IMS Health Inc., 564 U.S. 552 (2011). https://supreme.justia.com/cases/federal/us/564/552
**Notes:** HIPAA Safe Harbor (45 CFR §164.514(b)(2)) 18-identifier list and Expert Determination route are accurately described standard regulatory text.

---
## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE (reports a finding)
**Sentence:** "According to a Public Citizen analysis, in 2011 the Masterfile and other 'database products' were the AMA's single most profitable products apart from investments, generating about $42 million — roughly 26% of net revenue before expenses that year ... (Public Citizen Health Research Group, *Health Letter*, Nov. 2012)."
**Claim checked:** Public Citizen Nov 2012: AMA Masterfile/database products ~$42M, ~26% of net revenue in 2011.
**Site visited:** https://www.citizen.org/wp-content/uploads/hl_201211.pdf
**Finding:** Confirmed exactly. Public Citizen Health Letter, Nov 2012 (Sidney M. Wolfe, ed.): in 2011 the Masterfile and other database products were the AMA's single most profitable products apart from investments, raking in $42 million and accounting for 26% of net revenue. Matches the prior accuracy-pass correction.
**Expert review needed:** No
**Suggested reference:** Public Citizen Health Research Group. Health Letter, November 2012. https://www.citizen.org/wp-content/uploads/hl_201211.pdf
**Notes:** None.

### STAT / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "IQVIA ... describes its US prescription datasets as covering roughly 90% or more of US retail pharmacy dispensing ... and its OneKey reference directory as holding more than 25 million healthcare-professional profiles across 100-plus countries (IQVIA, 'OneKey HCP Reference Data,' iqvia.com)."
**Claim checked:** IQVIA OneKey: 25M+ HCP profiles across 100+ countries; ~90%+ retail dispensing coverage.
**Site visited:** https://www.iqvia.com/solutions/commercialization/data-and-information-management/onekey/onekey-hcp-reference-data ; https://www.onekeydata.com/onekey/healthcare-professionals-data
**Finding:** Confirmed (vendor self-description, correctly attributed). OneKey covers 25M+ HCPs and 6M+ HCOs across 118 countries (so "100-plus" is accurate and conservative). The chapter explicitly notes these are IQVIA self-descriptions and "not independent validation." Matches the prior accuracy-pass correction (25M+, not 11M).
**Expert review needed:** No
**Suggested reference:** IQVIA. OneKey HCP Reference Data. https://www.iqvia.com/solutions/commercialization/data-and-information-management/onekey/onekey-hcp-reference-data
**Notes:** Vendor figure, appropriately labeled; the count itself is confirmed against the vendor page.

### EVIDENCE — CONFIRMED (corporate / lineage fact)
**Assertion type:** BASIC
**Sentence:** "The firm that built this model at scale was IMS Health. ... IQVIA — IMS's successor after a series of mergers ... Symphony Health (now under ICON) competes ... Definitive Healthcare supplies HCP affiliation and procedural data ..."
**Claim checked:** IMS Health → IQVIA lineage; Symphony Health under ICON; Definitive Healthcare role.
**Site visited:** (corporate-history, widely documented; cross-checked against IQVIA/Sorrell coverage)
**Finding:** Accurate. IMS Health is the historical builder; IQVIA is its successor (IMS Health + Quintiles merger, 2016). Symphony Health is owned by ICON plc. Definitive Healthcare supplies HCP/HCO affiliation and procedural data. These are standard, uncontested corporate-history facts.
**Expert review needed:** No
**Suggested reference:** IQVIA corporate history (IMS Health/Quintiles merger, 2016); standard industry references.
**Notes:** Name-list with functional claims; all roles accurate.

### EVIDENCE — UNVERIFIED / open by design
**Assertion type:** I-LANGUAGE / hedged
**Sentence:** "Whether this actually describes how real propensity models are weighted is, honestly, an open empirical question. ... [The susceptibility-proxy construct is the book's position, flagged not asserted — see pantry ...]"
**Claim checked:** Whether real propensity models heavily weight Open Payments / susceptibility features.
**Site visited:** (n/a — claim of an untested open question)
**Finding:** This is the book's own labeled hypothesis (the susceptibility-proxy construct), explicitly presented as an open empirical question testable on public data, not asserted as fact. Maps to UNVERIFIED by design; correctly hedged.
**Expert review needed:** No
**Suggested reference:** Could not identify a published study testing propensity-model feature weighting on Open Payments data (the chapter's point).
**Notes:** Honest open-question framing; not an error.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "Whether this actually describes how real propensity models are weighted is, honestly, an open empirical question." | EVIDENCE | I-LANGUAGE / hedged | The book's own susceptibility-proxy hypothesis, explicitly flagged not asserted; no public study tests it. |

---
## AI-Pass Flags
None. The de-identification mechanism, the Masterfile join, the Sorrell holding, and the feedback-loop description are internally consistent and consistent with the verified sources. The claims-lag and attribution-distortion reasoning is logically sound. No definitional errors.
