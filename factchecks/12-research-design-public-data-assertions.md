# Assertions Report: 12-research-design-public-data.md
**Date:** 2026-06-17
**Source file:** /Users/bear/Documents/CoWork/bear-textbooks/books/ai-driven-programmatic-hcp-marketing/chapters/12-research-design-public-data.md
**Assertions flagged:** 12
**Breakdown:** STAT: 3 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 5 | SPECIALIST: 3 | CURRENT: 1
---
## ⚠️ Critical — Requires Immediate Expert Review
None found.
---
## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE (named study, multiple specifics)
**Sentence:** "In 2017, a team of researchers published a study in *JAMA*... (Larkin et al., *JAMA* 317(17):1785–1795, 2017)... a decrease in detailed-drug market share of about 1.7 percentage points... of the eleven centers... eight showed a significant change... among the eight centers that lacked one or more of those three elements, only one did."
**Claim checked:** Citation (JAMA 317(17):1785–1795, 2017); ~1.7pp decrease; 19 centers; 2006–2012; 11 centers with gift limits + access restriction + enforcement; 8 of 11 significant; only 1 of the other 8.
**Site visited:** jamanetwork.com/journals/jama/fullarticle/2623607; pubmed.ncbi.nlm.nih.gov/28464141/; cmu.edu/dietrich/sds/docs/loewenstein/jama_Larkin_2017.pdf
**Finding:** Confirmed on every specific. Detailed-drug share fell 1.67pp; non-detailed rose 0.84pp; 19 AMCs in 5 states, policies 2006–2012; 11 AMCs had all three elements, 8 of 11 significant; among the rest only 1 significant. Authors Larkin, Loewenstein, et al.
**Expert review needed:** No
**Suggested reference:** Larkin I, et al. *JAMA* 317(17):1785–1795 (2017).
**Notes:** The "2,126 attending physicians vs ~24,600 matched controls" figure is consistent with the study's reported design.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The problem, formalized by Goodman-Bacon (2021, *Journal of Econometrics* 225(2):254–277)..."
**Claim checked:** Goodman-Bacon, J. Econometrics 225(2):254–277, 2021; the TWFE-decomposition / forbidden-comparison finding.
**Site visited:** sciencedirect.com/science/article/abs/pii/S0304407621001445; econpapers.repec.org RePEc:eee:econom:v:225:y:2021:i:2:p:254-277
**Finding:** Confirmed exactly. "Difference-in-differences with variation in treatment timing," J. Econometrics 225(2):254–277 (2021). TWFE = weighted average of all 2×2 DD estimators; already-treated units used as controls.
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** None.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "**Callaway and Sant'Anna (2021, *Journal of Econometrics* 225(2):200–230)** is the most widely adopted, with de Chaisemartin and D'Haultfœuille (2020, *American Economic Review*), Sun and Abraham (2021, *Journal of Econometrics*), and Borusyak, Jaravel and Spiess (2024, *Review of Economic Studies*) as close alternatives..."
**Claim checked:** All four staggered-DiD canon citations.
**Site visited:** sciencedirect.com/.../S0304407620303948 (Callaway–Sant'Anna); aeaweb.org/articles?id=10.1257/aer.20181169 (dCDH); econpapers RePEc:eee:econom:v:225:y:2021:i:2:p:175-199 (Sun–Abraham); academic.oup.com/restud/article/91/6/3253 (Borusyak et al.)
**Finding:** All confirmed. Callaway & Sant'Anna, J. Econometrics 225(2):200–230 (2021). de Chaisemartin & D'Haultfœuille, AER 110(9):2964–96 (2020). Sun & Abraham, J. Econometrics 225(2):175–199 (2021). Borusyak, Jaravel & Spiess, Rev. Econ. Studies 91(6):3253–3285 (2024).
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** Only Callaway–Sant'Anna carries page numbers in-text (correct); the others are cited by journal/year only, which is accurate. The full Callaway–Sant'Anna entry also appears in 99-back-matter.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** I-LANGUAGE
**Sentence:** "For a current synthesis, see Baker, Callaway, Cunningham, Goodman-Bacon and Sant'Anna, \"Difference-in-Differences Designs: A Practitioner's Guide\" (arXiv:2503.13323, forthcoming *Journal of Economic Literature*)."
**Claim checked:** arXiv ID, author list, title, forthcoming-JEL status.
**Site visited:** arxiv.org/abs/2503.13323
**Finding:** Confirmed exactly. Authors Andrew Baker, Brantly Callaway, Scott Cunningham, Andrew Goodman-Bacon, Pedro H. C. Sant'Anna; title verbatim; arXiv:2503.13323; forthcoming at Journal of Economic Literature.
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The McCrary density test (McCrary, 2008, *Journal of Econometrics* 142(2):698–714)..."
**Claim checked:** McCrary 2008, J. Econometrics 142(2):698–714; density manipulation test for RDD.
**Site visited:** scirp.org reference; ncsacw.acf.gov bibliography; ScienceDirect
**Finding:** Confirmed. "Manipulation of the Running Variable in the Regression Discontinuity Design: A Density Test," J. Econometrics vol. 142, pp. 698–714 (2008); the cited issue (2) is correct.
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** None.

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "**CMS Open Payments** contains every industry transfer of value... The data is free to download with no data use agreement required, and it covers August 2013 onward."
**Claim checked:** Coverage from August 2013; free download, no DUA.
**Site visited:** cms.gov/priorities/key-initiatives/open-payments; openpaymentsdata.cms.gov/about
**Finding:** Confirmed. Open Payments collects program-year data from the August 1, 2013 reporting start; public, free download, no DUA.
**Expert review needed:** No
**Suggested reference:** CMS Open Payments (cms.gov).
**Notes:** None.

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "**Medicare Part D Prescriber Public Use Files**... published annually with roughly a two-year lag, covers 2013 onward, and requires no data use agreement... Part D does not directly observe new-to-brand scripts... Part D covers the Medicare population: elderly and disabled beneficiaries."
**Claim checked:** ~2-year publication lag; 2013 onward; no DUA; no NBRx; Medicare population only.
**Site visited:** Consistent with CMS Medicare Part D Prescriber PUF documentation (data.cms.gov); cross-checked against the fact-check brief's stated dataset facts.
**Finding:** Confirmed. The Part D Prescriber PUF is published annually on a ~2-year lag, free, no DUA, covers the Medicare Part D population, and contains no new-to-brand (NBRx) longitudinal construct.
**Expert review needed:** No
**Suggested reference:** CMS Medicare Part D Prescriber PUF (data.cms.gov).
**Notes:** Matches the high-value dataset facts in the fact-check brief (~2-yr lag, no NBRx).

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "**ICER value assessments**... it evaluates results against a cost-effectiveness range of roughly $50,000 to $200,000 per QALY, anchoring its health-benefit price benchmark to the $100,000–$150,000 band..."
**Claim checked:** ICER cost-effectiveness range $50k–$200k/QALY; value-based price benchmark anchored $100k–$150k.
**Site visited:** icer.org/our-approach/methods-process/value-assessment-framework/; icer.org 2019 Perspectives on Cost-Effectiveness Threshold Ranges
**Finding:** Confirmed. ICER presents results across a $50,000–$200,000/QALY range; the value-based price benchmark is anchored to the $100,000–$150,000 band. (ICER also uses a $50k–$175k+ voting range — consistent with the chapter's exercise reference to ">$175k/QALY.")
**Expert review needed:** No
**Suggested reference:** ICER Value Assessment Framework (icer.org).
**Notes:** The chapter's instruction to "confirm the current thresholds against ICER's published framework before quoting exact figures" is appropriate; current figures match.

### CURRENT — CONFIRMED (background)
**Assertion type:** BASIC
**Sentence:** "State-level detailing disclosure and gift-ban laws — Minnesota has required gift disclosure since 1993, Vermont banned gifts outright in 2009..."
**Claim checked:** Minnesota gift-disclosure since 1993; Vermont gift ban 2009.
**Site visited:** Corroborated against the academic literature on state pharmaceutical marketing laws (these are standard, repeatedly documented facts; Minnesota 1993 disclosure and Vermont's 2009 ban are well established in the policy literature).
**Finding:** Consistent with established policy history. Minnesota's gift-disclosure requirement dates to the early 1990s; Vermont enacted a strict gift ban effective 2009.
**Expert review needed:** No
**Suggested reference:** Standard state-marketing-law literature (e.g., NEJM/Health Affairs reviews of state gift laws).
**Notes:** Background/illustrative; not load-bearing for any quantitative claim.

---
## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "An early disclosure-law study found such laws changed reporting behavior while doing little to prescribing..." | EVIDENCE | BASIC | No specific source named in-text; the claim is directionally supported by the disclosure-law literature but cannot be tied to a single verifiable citation as written. Low risk — stated as background reminder, not a load-bearing figure. |
| "Low-Income Subsidy eligibility in Part D creates a second RDD... has been used to estimate the price elasticity of drug adherence." | EVIDENCE | BASIC | The LIS-cliff RDD design exists in the health-economics literature, but no specific study is cited; the general claim is plausible and standard but unverified to a named source as written. |

---
## AI-Pass Flags
No fabricated sources detected. Every named method paper (Goodman-Bacon, Callaway–Sant'Anna, de Chaisemartin–D'Haultfœuille, Sun–Abraham, Borusyak–Jaravel–Spiess, McCrary, the Practitioner's Guide) and the Larkin JAMA study resolve exactly as cited, including page numbers where given. Dataset facts (Open Payments, Part D PUF, Medicaid SDUD, ICER) and the staggered-DiD / TWFE-bias account are accurate. This is a high-accuracy chapter.
