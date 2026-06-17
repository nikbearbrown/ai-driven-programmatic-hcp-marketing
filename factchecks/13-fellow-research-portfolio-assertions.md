# Assertions Report: 13-fellow-research-portfolio.md
**Date:** 2026-06-17
**Source file:** /Users/bear/Documents/CoWork/bear-textbooks/books/ai-driven-programmatic-hcp-marketing/chapters/13-fellow-research-portfolio.md
**Assertions flagged:** 5
**Breakdown:** STAT: 1 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 3 | SPECIALIST: 1 | CURRENT: 0
---
## ⚠️ Critical — Requires Immediate Expert Review
None found.
---
## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE (named study + quantitative claim)
**Sentence:** "...the Dafny–Ody–Schmitt template (Dafny, Ody & Schmitt, \"When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization,\" *American Economic Journal: Economic Policy* 9(2):91–123, 2017; NBER WP w22745), which found that coupons raise branded sales by more than 60 percent, entirely by displacing bioequivalent generics..."
**Claim checked:** Citation (AEJ:EP 9(2):91–123, 2017; NBER w22745); the ">60%" branded-sales claim and the "entirely by displacing bioequivalent generics" mechanism.
**Site visited:** aeaweb.org/articles?id=10.1257/pol.20150588; nber.org/papers/w22745; hbs.edu/ris/Publication%20Files/DafnyOdySchmitt_CopayCoupons...pdf
**Finding:** Confirmed exactly. AEJ: Economic Policy vol. 9, issue 2, May 2017; NBER WP 22745. The paper finds coupons "increase branded sales by 60+ percent, entirely by reducing the sales of bioequivalent generics."
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** Full entry also appears in 99-back-matter and resolves. The "more than 60 percent" wording matches the paper's "60+ percent."

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "...gradient-boosted tree ensembles are state of the art (Grinsztajn, Oyallon & Varoquaux, \"Why do tree-based models still outperform deep learning on tabular data?\", NeurIPS 2022)..."
**Claim checked:** Citation (Grinsztajn, Oyallon, Varoquaux; NeurIPS 2022); the finding that tree-based models remain SOTA on medium tabular data.
**Site visited:** arxiv.org/abs/2207.08815; semanticscholar.org
**Finding:** Confirmed. NeurIPS 2022 Datasets and Benchmarks Track, arXiv:2207.08815. The paper finds tree-based models remain state-of-the-art on medium-sized (~10K-sample) tabular data.
**Expert review needed:** No
**Suggested reference:** Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022 (arXiv:2207.08815).
**Notes:** Title rendered correctly. Full entry appears in 99-back-matter with the arXiv ID.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "...a heterogeneity-robust difference-in-differences (Callaway & Sant'Anna 2021, *Journal of Econometrics* 225(2):200–230)." (appears in projects A1 and D2)
**Claim checked:** Callaway & Sant'Anna 2021, J. Econometrics 225(2):200–230.
**Site visited:** sciencedirect.com/science/article/abs/pii/S0304407620303948
**Finding:** Confirmed exactly (see Ch12 report for full detail).
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** Cited consistently with Ch12.

### STAT — CONFIRMED (construct + dataset facts)
**Assertion type:** BASIC
**Sentence:** "Medicaid SDUD is aggregated to NDC × state × quarter — it does not observe individual patients or individual substitution decisions." and "Public data tops out around Level 3."
**Claim checked:** Medicaid SDUD aggregation level (NDC × state × quarter, no patient/physician identity); the Level-3 ceiling as the book's own construct.
**Site visited:** medicaid.gov State Drug Utilization Data documentation (cross-checked against fact-check brief dataset facts).
**Finding:** Confirmed. Medicaid SDUD is aggregated outpatient drug utilization by NDC, state, and quarter; no individual-patient or physician identity. The Evidence Ladder Level-3 ceiling is the book's internal construct (see Ch11 report) and is correctly described, not externally citable.
**Expert review needed:** No
**Suggested reference:** Medicaid State Drug Utilization Data (medicaid.gov).
**Notes:** None.

### EVIDENCE — CONFIRMED (claim correctly framed as open question)
**Assertion type:** I-LANGUAGE
**Sentence:** "ICER's QALY methodology is contested — disability and equity critiques, industry pushback — and drugs that reach ICER review are a selected set." / "B1 tests whether share-of-mind predicts later share-of-market with a lag... asserted qualitatively but never rigorously tested... this is an open research question, not an established fact."
**Claim checked:** That QALY methodology is genuinely contested, and that the listed leading-indicator claims are framed as open questions rather than established facts.
**Site visited:** General health-economics literature on QALY/disability critiques (well-documented; e.g., disability-rights and equity critiques of QALY are widely published).
**Finding:** Confirmed as appropriately hedged. The QALY-contestation claim is accurate and well-supported in the literature. The B1/B3 leading-indicator claims are explicitly flagged in-text as open research questions, which is the correct epistemic status.
**Expert review needed:** No
**Suggested reference:** Standard QALY-critique literature (ICER framework + disability/equity critiques).
**Notes:** Good practice — speculative claims are self-flagged as untested.

---
## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "industry script-lift figures (4 to 44 percent) are all vendor-generated, structurally inflated by attribution circularity..." | STAT | EMPHATIC | The 4–44% range is explicitly attributed to vendor decks and the book's entire thesis treats it as an un-refereed vendor claim (the back-matter states vendor figures are "self-reported, un-refereed, and flagged [verify]"). No neutral source exists or is claimed; correctly framed as vendor-sourced. |
| "[contested — see pantry, Risk 1]" (Track D adversarial-scope blocker) | — | — | Internal editorial/pantry cross-reference, not an external factual claim. Out of scope for external verification. |

---
## AI-Pass Flags
No fabricated sources detected. All three external citations (Dafny–Ody–Schmitt, Grinsztajn et al., Callaway–Sant'Anna) resolve exactly, including the quantitative ">60%" coupon finding. The 4–44% lift range is correctly and repeatedly framed as an un-refereed vendor claim, consistent with the book's thesis. Dataset facts are accurate. No assertions require expert review.
