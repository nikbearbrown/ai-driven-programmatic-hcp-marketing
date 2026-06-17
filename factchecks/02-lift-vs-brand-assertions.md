# Assertions Report: 02-lift-vs-brand.md
**Date:** 2026-06-17
**Source file:** chapters/02-lift-vs-brand.md
**Assertions flagged:** 4
**Breakdown:** STAT: 3 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 0 | CURRENT: 0

---
## ⚠️ Critical — Requires Immediate Expert Review
None found. No OUTDATED/CONTRADICTED/COMBINATION assertions. The two named external studies (BMJ Greenway & Ross; JAMA Johns Hopkins) resolved to real, correctly-attributed sources.

---
## Full Findings

### EVIDENCE / STAT — CONFIRMED
**Assertion type:** I-LANGUAGE (reports a finding)
**Sentence:** "A *BMJ* analysis by Greenway and Ross found that the most-promoted drugs were less likely than top-selling or top-prescribed drugs to be effective, safe, affordable, novel, or genuine advances, and that generic equivalents were available for 63% of the most-promoted drugs (Greenway & Ross, *BMJ* 2017;357:j1855)."
**Claim checked:** Greenway & Ross BMJ 2017: most-promoted drugs less likely effective/safe/affordable/novel; generic equivalents for 63%.
**Site visited:** https://pubmed.ncbi.nlm.nih.gov/28465309/ ; https://www.tctmd.com/news/drugs-most-heavily-promoted-pharma-dont-necessarily-offer-best-health-value
**Finding:** The study is confirmed real and correctly attributed (Greenway T, Ross JS. "US drug marketing: how does promotion correspond with health value?" BMJ 2017;357:j1855; PubMed 28465309). The directional finding — top-promoted drugs less likely than top-selling/top-prescribed to be effective, safe, affordable, novel, or genuine advances — is confirmed in the abstract and coverage. The specific "63% have generic equivalents" sub-figure did not surface in available search snippets but is consistent with the paper's framing and was resolved in the prior accuracy pass; the load-bearing directional claim is CONFIRMED.
**Expert review needed:** No
**Suggested reference:** Greenway T, Ross JS. US drug marketing: how does promotion correspond with health value? BMJ. 2017;357:j1855. https://pubmed.ncbi.nlm.nih.gov/28465309/
**Notes:** Direction fully confirmed; the 63% decimal is the only sub-figure not independently re-surfaced this pass (carried from prior accuracy pass).

### EVIDENCE / STAT — CONFIRMED
**Assertion type:** I-LANGUAGE (reports a finding)
**Sentence:** "A separate 2023 study from Johns Hopkins, published in *JAMA*, found that 68% of the 135 top-selling US prescription drugs in 2020 were rated as offering low added clinical benefit, and that consumer-advertising spend skewed toward those low-benefit drugs (Johns Hopkins Bloomberg School of Public Health, *JAMA*, Feb. 7, 2023)."
**Claim checked:** JAMA Feb 7 2023 (Johns Hopkins): 68% of 135 top-selling 2020 drugs = low added benefit; DTC spend skews to low-benefit drugs.
**Site visited:** https://publichealth.jhu.edu/2023/spending-on-consumer-advertising-for-top-selling-prescription-drugs-in-us-favors-those-with-low-added-benefit ; https://pubmed.ncbi.nlm.nih.gov/36749334/
**Finding:** Confirmed exactly. 68% (92 of 135) of top-selling 2020 drugs rated low added benefit; the share of promotional spend on consumer advertising was on average 14.3 percentage points higher for low-added-benefit drugs. Published in JAMA online Feb 7, 2023. The chapter correctly attributes "top-selling" (not "most-advertised"), matching the prior accuracy-pass correction.
**Expert review needed:** No
**Suggested reference:** Cliff BQ, et al. Association Between Drug Characteristics and Manufacturer Spending on Direct-to-Consumer Advertising. JAMA. 2023;329(5). https://pubmed.ncbi.nlm.nih.gov/36749334/
**Notes:** None.

### STAT — UNVERIFIED (already self-flagged in prose)
**Assertion type:** I-LANGUAGE / hedged
**Sentence:** "The major claims-data vendors — IQVIA foremost among them — describe their prescription datasets as covering roughly 90% or more of US retail dispensing before projection adjustments ... [verify — unconfirmed: a specific '93% NBRx coverage' self-description did not resolve to a current IQVIA primary source; the ~90% retail-dispensing figure is the verifiable adjacent claim.]"
**Claim checked:** IQVIA self-described ~93% NBRx coverage / ~90%+ retail dispensing.
**Site visited:** IQVIA OneKey / data product pages (vendor self-description)
**Finding:** The ~90%+ retail-dispensing characterization is a standard IQVIA self-description (vendor positioning, not independent validation). The specific "93% NBRx coverage" figure does not resolve to a current IQVIA primary source. The chapter already carries the honest `[verify — unconfirmed]` hedge. Maps to UNVERIFIED, as instructed.
**Expert review needed:** No (already hedged correctly)
**Suggested reference:** Could not identify an independent (non-vendor) source for the coverage percentages.
**Notes:** Vendor self-description; a vendor confirming its own coverage figure is not independent verification.

### EVIDENCE — UNVERIFIED (already self-flagged in prose)
**Assertion type:** I-LANGUAGE / hedged
**Sentence:** "The SOMi → SOMa leading-indicator claim ... as of this writing, it is not rigorously tested on linked survey-plus-claims data. [verify; treat as a vendor hypothesis, not an established finding]"
**Claim checked:** Whether share-of-mind-intent predicts share-of-market-actual with a lag is empirically established.
**Site visited:** (n/a — claim is that no published test exists)
**Finding:** This is a claim of absence — that no rigorous linked-data test exists — presented honestly as a vendor hypothesis, not a finding. Consistent with the chapter's own framing and the accuracy log. Maps to UNVERIFIED by design (the assertion is precisely that it is unverified).
**Expert review needed:** No
**Suggested reference:** Could not identify a published test on linked survey-plus-claims data (the chapter's point).
**Notes:** Correctly hedged; this is the book's own open-research-question framing.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "...describe their prescription datasets as covering roughly 90% or more ... a specific '93% NBRx coverage' self-description did not resolve to a current IQVIA primary source..." | STAT | I-LANGUAGE / hedged | Vendor self-description; 93% NBRx figure unresolvable to a primary source; already `[verify — unconfirmed]` in prose. |
| "The statement that 'higher brand equity is predictive of market-share growth' appears in vendor materials with no published test attached." (SOMi→SOMa) | EVIDENCE | I-LANGUAGE / hedged | Claim of absence; no published linked-data test; already `[verify]` in prose. |

---
## AI-Pass Flags
None. Metric definitions (TRx/NRx/NBRx, SOV/SOM, loyalty deciles) are standard and internally consistent. The chapter applies its own evidentiary standard consistently — explicitly refusing to let "brand equity" smuggle in a causal claim ("[contested — see pantry]"), which is intellectually honest, not an error. No definitional or logical inconsistencies found.
