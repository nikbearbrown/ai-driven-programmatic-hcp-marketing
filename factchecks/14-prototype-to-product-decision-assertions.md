# Assertions Report: 14-prototype-to-product-decision.md
**Date:** 2026-06-17
**Source file:** /Users/bear/Documents/CoWork/bear-textbooks/books/ai-driven-programmatic-hcp-marketing/chapters/14-prototype-to-product-decision.md
**Assertions flagged:** 4
**Breakdown:** STAT: 0 | GUIDELINE: 1 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 1 | CURRENT: 0
---
## ⚠️ Critical — Requires Immediate Expert Review
None found.
---
## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE
**Sentence:** "The \"no\" saves engineering budget — the expected outcome given what the evidence on tree ensembles versus deep learning on medium tabular data predicts (Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022)."
**Claim checked:** Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022; tree ensembles vs deep learning on medium tabular data.
**Site visited:** arxiv.org/abs/2207.08815
**Finding:** Confirmed (see Ch13 report). NeurIPS 2022, arXiv:2207.08815; tree-based models remain SOTA on medium tabular data.
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE (named study + mechanism)
**Sentence:** "Mechanism: suppression of bioequivalent-generic substitution (Dafny, Ody & Schmitt, *AEJ: Economic Policy* 9(2):91–123, 2017)."
**Claim checked:** Dafny, Ody & Schmitt, AEJ:EP 9(2):91–123, 2017; coupon → generic-suppression mechanism.
**Site visited:** aeaweb.org/articles?id=10.1257/pol.20150588
**Finding:** Confirmed (see Ch13 report). The mechanism — coupons raise branded sales entirely by displacing bioequivalent generics — is the paper's central finding.
**Expert review needed:** No
**Suggested reference:** As cited.
**Notes:** None.

### GUIDELINE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "MLR, FDA fair-balance, Sunshine Act, HIPAA — the brief surfaces the exposure; medical, legal, and regulatory affairs make the calls." / "Coupons banned in Medicare; state-law variation on Medicaid and commercial."
**Claim checked:** The four compliance surfaces are correctly named; co-pay coupons are prohibited for Medicare beneficiaries; state variation on Medicaid/commercial.
**Site visited:** Cross-checked against Ch11 regulatory verifications (21 CFR 202.1; CMS Open Payments/Sunshine Act; HIPAA 164.514/164.508) and the Dafny–Ho–Kong (NBER w29735) design, which uses the Medicare coupon ban as its control.
**Finding:** Confirmed. Co-pay coupons are illegal for federal-program (Medicare) beneficiaries under the federal Anti-Kickback Statute; Dafny/Ho/Kong (2022) and Dafny/Ody/Schmitt (2017) both exploit this ban and cross-state legality variation. The four compliance surfaces match Ch11's verified framework.
**Expert review needed:** No
**Suggested reference:** Dafny, Ho & Kong, NBER WP 29735 (2022); CMS/OIG Anti-Kickback guidance on copay coupons.
**Notes:** The Medicare coupon ban is the identification engine in both Dafny papers — well established.

### SPECIALIST — CONFIRMED (construct framing)
**Assertion type:** BASIC
**Sentence:** "The four-stage research-to-product pipeline maps cleanly to the Evidence Ladder. Stage 1 is open research... topping out around Level 3..." (Table 14.1)
**Claim checked:** The four-stage pipeline and its Evidence-Ladder mapping (L0–L3 / L4 / L5 / L6).
**Site visited:** Cross-checked against Ch11 construct verification (TRL × OCEBM); internal consistency with Tables 11.1 and 13.1.
**Finding:** Confirmed as internally consistent. The Evidence Ladder is the book's own construct (verified in Ch11 as resting on real NASA TRL and OCEBM 2011 axes); the L0–L3 public-data ceiling and L4–L6 proprietary requirement are applied consistently across Chapters 11, 13, and 14.
**Expert review needed:** No
**Suggested reference:** Internal construct; see Ch11 (TRL/OCEBM source axes).
**Notes:** Not externally citable; correctly presented as the book's framework. No OUTDATED flag warranted.

---
## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "an unsettled HIPAA question about real-time clinical triggers" (EHR-sidebar personalization) | GUIDELINE | BASIC | A genuinely open/contested regulatory area, explicitly framed in-text as "unsettled." No definitive ruling exists to cite; correctly hedged, not a factual error. |
| "`[contested — see pantry, Risk 1]`" / "`[Risk 1]`" (partner-agreement blocker) | — | — | Internal editorial/pantry cross-reference, not an external factual claim. Out of scope. |

---
## AI-Pass Flags
No fabricated sources detected. Both external citations (Grinsztajn et al. NeurIPS 2022; Dafny–Ody–Schmitt AEJ:EP 2017) resolve and match Chapters 12–13. The compliance framing (four surfaces, Medicare coupon ban, routed-not-adjudicated posture) is accurate. The Evidence Ladder and four-stage pipeline are the book's internal constructs, applied consistently. No assertions require expert review.
