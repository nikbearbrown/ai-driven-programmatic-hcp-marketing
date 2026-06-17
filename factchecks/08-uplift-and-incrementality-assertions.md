# Assertions Report: 08-uplift-and-incrementality.md
**Date:** 2026-06-17
**Source file:** chapters/08-uplift-and-incrementality.md
**Assertions flagged:** 5
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 4 | SPECIALIST: 1 | CURRENT: 0
---
## ⚠️ Critical — Requires Immediate Expert Review

> **RESOLVED 2026-06-17:** the opioid-study author attribution was corrected in the chapter prose from "Larkin et al." to "Eisenberg, Stone, Pittell & McGinty" (*Health Affairs* 2020;39(6):1002–1010). Logged here for the record.

**CONTRADICTED — citation misattribution (Larkin opioid Health Affairs 2020).**
Verbatim sentence: *"A related study found AMC marketing restrictions associated with lower opioid prescribing — a patient-welfare-relevant variant (Larkin et al., "The Impact Of Academic Medical Center Policies Restricting Direct-To-Physician Marketing On Opioid Prescribing," Health Affairs, 2020)."*
One-line finding: The paper with that exact title in Health Affairs 2020 (39(6):1002–1010, DOI 10.1377/hlthaff.2019.01289) is authored by **Eisenberg, Stone, Pittell & McGinty — not Larkin**; no Larkin-authored opioid Health Affairs 2020 paper exists. The finding itself (AMC marketing restrictions → lower opioid prescribing) is real and correctly described, but the author attribution is wrong.

---
## Full Findings

### EVIDENCE — CONFIRMED (Künzel meta-learners, PNAS 2019)
**Assertion type:** BASIC
**Sentence:** "The S-, T-, and X-learner family is formalized in Künzel, Sekhon, Bickel, and Yu, 'Metalearners for estimating heterogeneous treatment effects using machine learning' (PNAS, 2019)."
**Claim checked:** Authors, title, venue, year, X-learner formalization.
**Site visited:** https://www.pnas.org/doi/abs/10.1073/pnas.1804597116
**Finding:** Exact. Künzel, Sekhon, Bickel, Yu; PNAS 2019; DOI 10.1073/pnas.1804597116; introduces the X-learner and the meta-learner framework. 
**Expert review needed:** No
**Suggested reference:** Künzel et al., PNAS 2019, doi:10.1073/pnas.1804597116.

### EVIDENCE — CONFIRMED (Nie & Wager R-learner, Biometrika 2021)
**Assertion type:** POSITIVE
**Sentence:** "The double residualization (Neyman-orthogonal) makes it robust to misspecification in either the propensity or the outcome model ... (Nie & Wager, 'Quasi-oracle estimation of heterogeneous treatment effects,' Biometrika 108(2):299–319, 2021)."
**Claim checked:** Authors, title, volume/issue/pages, quasi-oracle/Neyman-orthogonal property.
**Site visited:** https://academic.oup.com/biomet/article-abstract/108/2/299/5911092
**Finding:** Exact. Nie & Wager, Biometrika 108(2):299–319, June 2021, DOI 10.1093/biomet/asaa076; two-step residualization with quasi-oracle property. Volume, issue, and page range all match.
**Expert review needed:** No
**Suggested reference:** Nie & Wager, Biometrika 108(2):299–319 (2021).

### EVIDENCE — CONFIRMED (Wager & Athey causal forests, JASA 2018)
**Assertion type:** POSITIVE
**Sentence:** "Causal forests — from Wager and Athey ('Estimation and Inference of Heterogeneous Treatment Effects using Random Forests,' JASA 113(523):1228–1242, 2018)."
**Claim checked:** Authors, title, volume/issue/pages, year.
**Site visited:** https://www.tandfonline.com/doi/abs/10.1080/01621459.2017.1319839
**Finding:** Exact. Wager & Athey, JASA 113(523):1228–1242, 2018, DOI 10.1080/01621459.2017.1319839; causal forest splitting on treatment-effect heterogeneity with pointwise consistency. The chapter's caveat about high-dimensional brittleness is consistent with the GRF/causal-forest literature.
**Expert review needed:** No
**Suggested reference:** Wager & Athey, JASA 113(523):1228–1242 (2018).

### EVIDENCE — CONFIRMED (Larkin detailing restrictions, JAMA 2017)
**Assertion type:** POSITIVE
**Sentence:** "Larkin and colleagues (JAMA 2017;317(17):1785–1795) ran a difference-in-differences study on 19 AMCs across five states that restricted sales-rep detailing between 2006 and 2012 — 2,126 affected physicians against 24,593 matched controls, across 262 drugs in 8 classes. Restricting detailing produced modest but significant reductions in detailed-drug prescribing in 6 of 8 classes."
**Claim checked:** Authors, venue, vol/issue/pages, 19 AMCs/5 states, DiD, 6 of 8 classes, shift toward generics.
**Site visited:** https://jamanetwork.com/journals/jama/fullarticle/2623607 ; https://pubmed.ncbi.nlm.nih.gov/28464141/
**Finding:** Confirmed. Larkin et al., JAMA 2017;317(17):1785–1795; 19 AMCs in 5 states (CA, IL, MA, PA, NY); difference-in-differences vs matched controls; reductions in detailed-drug prescribing in 6 of 8 classes; −1.67pp detailed-drug market share / +0.84pp non-detailed. Sample-size and drug-count specifics (2,126 / 24,593 / 262 drugs) are consistent with the published study.
**Expert review needed:** No
**Suggested reference:** Larkin, Ang, Steinhart et al., JAMA 2017;317(17):1785–1795.

### EVIDENCE — CONTRADICTED (opioid study author)
**Assertion type:** POSITIVE
**Sentence:** "A related study found AMC marketing restrictions associated with lower opioid prescribing ... (Larkin et al., 'The Impact Of Academic Medical Center Policies Restricting Direct-To-Physician Marketing On Opioid Prescribing,' Health Affairs, 2020)."
**Claim checked:** Author attribution and existence of the cited paper.
**Site visited:** https://www.healthaffairs.org/doi/abs/10.1377/hlthaff.2019.01289 ; https://pubmed.ncbi.nlm.nih.gov/32479218/
**Finding:** The paper with that exact title (Health Affairs 2020;39(6):1002–1010, DOI 10.1377/hlthaff.2019.01289) is authored by **Matthew D. Eisenberg, Elizabeth M. Stone, Harlan Pittell, Emma E. McGinty** (Johns Hopkins). It used DiD on Medicare Part D across 85 AMCs (2013–16); sales-rep bans → 4.7% reduction in opioid volume, all four restriction policies → 8.8% reduction. The underlying finding the chapter describes is accurate; the **author attribution to "Larkin et al." is incorrect.**
**Expert review needed:** Yes — correct the author to Eisenberg et al. (or remove the author tag and keep the title + Health Affairs 2020).
**Suggested reference:** Eisenberg, Stone, Pittell & McGinty, Health Affairs 2020;39(6):1002–1010, doi:10.1377/hlthaff.2019.01289.
**Notes:** This is a misattribution, not a fabrication — the paper is real and the result is correctly summarized. Flag inserted at the sentence.

### SPECIALIST — CONFIRMED (potential-outcomes / SUTVA / unconfoundedness framework)
**Assertion type:** BASIC
**Sentence:** Fundamental problem of causal inference; unconfoundedness, overlap/positivity, SUTVA; ATE vs CATE definitions.
**Site visited:** Standard causal-inference canon (Rubin potential outcomes; Imbens & Rubin).
**Finding:** All definitions correct and standard. AI-ONLY canonical material; no contradiction.
**Expert review needed:** No

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
| --- | --- | --- | --- |
| "Empirical comparisons of meta-learners and causal forests ... (for example, on the public Criteo uplift dataset) report no universal winner ... [verify — unconfirmed: the precise per-estimator Qini rankings vary by study ...]" | EVIDENCE | BASIC | Author-flagged; the "no universal winner" conclusion is robust and well-supported, the precise per-estimator leaderboard is configuration-dependent and correctly left unasserted. Criteo uplift dataset is real. |
| "Physicians who received its AI-selected next-best-action message grew their new-to-brand prescriptions by 44% ... [the 44% figure is illustrative of the vendor range; verify against primary sources before citing]" | STAT | EMPHATIC | Author-flagged as an illustrative vendor-range figure, firewall-attributed by design. Correctly not asserted as fact. |

---
## AI-Pass Flags
The propensity-vs-incrementality inversion, the persuadables 2×2 (persuadables / sure things / lost causes / sleeping dogs), the Qini/uplift-curve evaluation logic, and the natural-experiment / DiD parallel-trends framing are internally consistent and technically sound. The terminology bridge table (uplift = CATE, lift = ATE) is accurate. Only issue is the Larkin/Eisenberg opioid misattribution flagged above.
