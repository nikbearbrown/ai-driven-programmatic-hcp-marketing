# Assertions Report: 06-ensembles-tabular-advantage.md
**Date:** 2026-06-17
**Source file:** chapters/06-ensembles-tabular-advantage.md
**Assertions flagged:** 4
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 3 | SPECIALIST: 1 | CURRENT: 0
---
## ⚠️ Critical — Requires Immediate Expert Review
None found.
---
## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Léo Grinsztajn, Edouard Oyallon, and Gaël Varoquaux published 'Why do tree-based models still outperform deep learning on typical tabular data?' at NeurIPS 2022 — the Datasets and Benchmarks track (arXiv 2207.08815) ... They tested deep-learning methods against tree-based methods across 45 tabular datasets. The finding: tree-based models remain state-of-the-art on medium-sized tabular data — around 10,000 samples."
**Claim checked:** Title, authors, arXiv ID, 45 datasets, ~10K-sample finding, tree-based SOTA.
**Site visited:** https://arxiv.org/abs/2207.08815
**Finding:** Exact match. Authors Grinsztajn, Oyallon, Varoquaux; arXiv 2207.08815 (submitted 18 Jul 2022); abstract states 45 datasets, "tree-based models remain state-of-the-art on medium-sized data (~10K samples) even without accounting for their superior speed." Widely documented as NeurIPS 2022 Datasets & Benchmarks track.
**Expert review needed:** No
**Suggested reference:** Grinsztajn, Oyallon & Varoquaux, arXiv:2207.08815 (NeurIPS 2022 Datasets & Benchmarks).
**Notes:** The chapter's three "mechanisms" map onto the paper's three challenges with minor paraphrase: (1) robust to uninformative features [exact], (2) chapter frames as "biased toward smooth functions / irregular targets" — the paper lists "preserve orientation of data" and "easily learn irregular functions" separately; the chapter's framing is an accurate gloss of the irregular-function challenge. (3) "best tabular methods are ensembles of decision trees" is consistent with the paper. No correction needed.

### EVIDENCE — CONFIRMED (mechanism implementations)
**Assertion type:** BASIC
**Sentence:** "the dominant modern implementations — XGBoost (Chen and Guestrin, 2016), LightGBM, CatBoost — are all gradient-boosted decision tree systems."
**Claim checked:** XGBoost attribution Chen & Guestrin 2016.
**Site visited:** Cross-checked against widely documented record (KDD 2016, "XGBoost: A Scalable Tree Boosting System").
**Finding:** Correct. XGBoost = Chen & Guestrin, KDD 2016. AdaBoost (Freund & Schapire 1997), Gradient Boosting (Friedman 2001), Bagging/Random Forest (Breiman 1996/2001), Stacking (Wolpert 1992) are all standard, correctly attributed dates — these are AI-ONLY canonical attributions verified against general knowledge; no contradiction.
**Expert review needed:** No
**Suggested reference:** Chen & Guestrin, KDD 2016.
**Notes:** Originating-idea attributions in Table 6.1 are all standard and correct.

### SPECIALIST — CONFIRMED (carried from Ch7/9 method-citation pass)
**Assertion type:** BASIC
**Sentence:** Bias-variance-covariance decomposition and the covariance floor (Eq. line 24).
**Claim checked:** Whether the three-term ensemble error decomposition (bias² + variance/N + (1−1/N)·covar) is a real, standard result.
**Site visited:** Standard ensemble-learning theory (Ueda & Nakano 1996 bias-variance-covariance; Brown et al. 2005 "Managing diversity in regression ensembles").
**Finding:** The decomposition is a real, well-established result in ensemble theory. The chapter presents it as approximate and pedagogical, which is appropriate. No fabrication.
**Expert review needed:** No
**Suggested reference:** Ueda & Nakano (1996); Brown, Wyatt, Harris & Yao, JMLR 2005.
**Notes:** AI-ONLY mechanism; included here because it is load-bearing for the chapter's argument. Verified as genuine.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
| --- | --- | --- | --- |
| "newer tabular deep-learning methods — FT-Transformer, SAINT, and particularly TabPFN and its successor TabPFN v2 — have been reported to narrow the gap ... [verify — unconfirmed: the precise 2026 standing of TabPFN-class results ...]" | CURRENT | I-LANGUAGE | Chapter explicitly hedges this as an active, contested frontier; the precise 2026 competitive standing is not a settled, citable result. Correctly left flagged. The named methods (FT-Transformer, SAINT, TabPFN, TabPFN v2) are all real architectures. |

---
## AI-Pass Flags
No logical or definitional issues found. The bias-variance-covariance argument, the discrimination/calibration distinction, the claims-lag illusion, and the out-of-time/subgroup evaluation framing are internally consistent and technically sound. The AUC narrative (0.94 leakage → 0.78) is a presented worked example, appropriately framed as the author's case rather than a cited statistic.
