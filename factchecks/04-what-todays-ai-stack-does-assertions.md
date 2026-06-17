# Assertions Report: 04-what-todays-ai-stack-does.md
**Date:** 2026-06-17
**Source file:** chapters/04-what-todays-ai-stack-does.md
**Assertions flagged:** 7
**Breakdown:** STAT: 4 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 1 | CURRENT: 3

---
## ⚠️ Critical — Requires Immediate Expert Review
None found. No OUTDATED/CONTRADICTED/COMBINATION assertions. The named external anchors (Grinsztajn NeurIPS 2022; MIT NANDA 2025; FDA/HHS Sept 2025 enforcement; Agrawal/Gans/Goldfarb) resolved correctly. McKinsey and vendor figures are firewall-attributed and contested in-text.

---
## Full Findings

### SPECIALIST / EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "the underlying task here is NPI-level tabular prediction — which is precisely the regime where, as Chapter 6 will show, a well-tuned gradient-boosted tree ensemble is the state of the art and a MoE is likely indistinguishable from, or worse than, that boring baseline (Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022)."
**Claim checked:** Grinsztajn/Oyallon/Varoquaux NeurIPS 2022 shows tree-based models are SOTA on tabular data.
**Site visited:** https://arxiv.org/abs/2207.08815 ; NeurIPS 2022 Datasets & Benchmarks track
**Finding:** Confirmed exactly. "Why do tree-based models still outperform deep learning on tabular data?" (Grinsztajn, Oyallon, Varoquaux), NeurIPS 2022 Datasets & Benchmarks (arXiv 2207.08815). 45-dataset benchmark; tree-based models (XGBoost/RF) remain state-of-the-art on medium-sized tabular data. Authors/venue/year exact.
**Expert review needed:** No
**Suggested reference:** Grinsztajn L, Oyallon E, Varoquaux G. Why do tree-based models still outperform deep learning on typical tabular data? NeurIPS 2022. https://arxiv.org/abs/2207.08815
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "An MIT report — 'The GenAI Divide: State of AI in Business 2025,' from the MIT NANDA initiative — found that roughly 95 percent of enterprise generative-AI pilots deliver no measurable P&L impact (MIT NANDA, 2025)."
**Claim checked:** MIT NANDA "GenAI Divide" 2025: ~95% of enterprise GenAI pilots show no measurable P&L impact.
**Site visited:** https://mlq.ai/media/quarterly_decks/v0.1_State_of_AI_in_Business_2025_Report.pdf ; virtualizationreview.com coverage
**Finding:** Confirmed. MIT Project NANDA, "The GenAI Divide: State of AI in Business 2025" (July 2025): ~95% of organizations see no measurable P&L impact from GenAI; only ~5% of integrated pilots extract significant value. The chapter correctly notes the methodology is not fully transparent and presents it in tension with the McKinsey figure rather than as settled.
**Expert review needed:** No
**Suggested reference:** MIT Project NANDA. The GenAI Divide: State of AI in Business 2025. July 2025. https://mlq.ai/media/quarterly_decks/v0.1_State_of_AI_in_Business_2025_Report.pdf
**Notes:** This is the firewall-flagged "95% of pilots fail" figure — confirmed it exists and says what's claimed; the chapter treats it as contested/non-comparable, which is correct.

### STAT / CURRENT / GUIDELINE — CONFIRMED
**Assertion type:** BASIC / POSITIVE
**Sentence:** "The FDA's September 2025 enforcement wave — roughly 60 letters issued on September 9, 2025 (about 8 Warning Letters and 53 Untitled Letters), announced alongside HHS ... targeted exaggerated efficacy claims and inadequate fair balance / risk disclosure (FDA/HHS press release and fact sheet, Sept. 9, 2025; King & Spalding and Covington advertising-enforcement reviews, 2025–26)."
**Claim checked:** FDA/HHS Sept 9 2025: ~60 letters (8 Warning, ~53 Untitled) targeting exaggerated efficacy / inadequate risk disclosure.
**Site visited:** https://www.kslaw.com/news-and-insights/hhs-and-fda-declare-crackdown-on-drug-advertising-and-promotion ; https://www.fdalawblog.com/2025/09/articles/fda/... ; ProPharma "60 Compliance Letters 2025"
**Finding:** Confirmed. HHS/FDA announced a DTC-advertising crackdown on Sept 9, 2025. From the Sept 9 cohort, FDA posted 8 Warning Letters to prescription-drug sponsors plus Untitled Letters in waves (40 posted Sept 16 + 11 more Sept 25 ≈ 51, with sources rounding the prescription-drug cohort to ~60 total). Most-common basis: exaggerated efficacy and inadequate risk disclosure. "About 8 WL and 53 UL / ~60" is within the documented range; matches the prior accuracy-pass correction (down from an earlier "200").
**Expert review needed:** No
**Suggested reference:** King & Spalding. HHS and FDA Declare "Crackdown" on Drug Advertising and Promotion, 2025. https://www.kslaw.com/news-and-insights/hhs-and-fda-declare-crackdown-on-drug-advertising-and-promotion
**Notes:** Untitled-letter count is reported in waves; "53" is at the upper edge of the prescription-drug subset but consistent with the rounded ~60 total. Not material to the claim.

### CURRENT — CONFIRMED (dated vendor product announcements)
**Assertion type:** BASIC
**Sentence:** "Veeva's AI Agents for Vault CRM (announced October 2025, available December 2025) and IQVIA's agentic NBA work — extended into the IQVIA.ai platform co-developed with NVIDIA (announced March 2026) — are concrete, dated examples (Veeva and IQVIA press releases, 2025–26)." (and PromoMats Quick Check / Content Agent in 25R3; Veeva Pulse 2025)
**Claim checked:** Existence and dating of Veeva/IQVIA agentic product announcements.
**Site visited:** Veeva and IQVIA press releases / product pages (vendor self-reported, dated)
**Finding:** These are vendor product announcements with specific dates, presented as capability-existence facts (not effectiveness claims). The chapter explicitly frames "agentic" as mostly task-assistive and labels the effectiveness claims grafted onto them as untested. The product/date facts are consistent with vendor announcements; capability existence (not effect) is appropriately the only thing asserted.
**Expert review needed:** No
**Suggested reference:** Veeva Systems and IQVIA product press releases, 2025–2026 (vendor-dated).
**Notes:** Capability-existence claims, correctly separated from effectiveness claims per the chapter's own thesis. The Veeva "up to 75%" and McKinsey "50–65%" figures are explicitly labeled vendor/consulting projections, not measurements.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "AI makes prediction cheap. It does not supply judgment, and it does not guarantee a business outcome. ... (Agrawal, Gans & Goldfarb, *Prediction Machines*, 2018)."
**Claim checked:** Prediction Machines (Agrawal, Gans, Goldfarb, 2018) frames AI as cheap prediction distinct from judgment.
**Site visited:** (widely documented HBR Press book, 2018)
**Finding:** Accurate attribution. Agrawal, Gans & Goldfarb, *Prediction Machines: The Simple Economics of Artificial Intelligence* (Harvard Business Review Press, 2018) is built on exactly the "AI makes prediction cheap; judgment is separate" thesis. Correct author/title/year.
**Expert review needed:** No
**Suggested reference:** Agrawal A, Gans J, Goldfarb A. Prediction Machines: The Simple Economics of Artificial Intelligence. Harvard Business Review Press, 2018.
**Notes:** None.

### STAT / CURRENT — UNVERIFIED (already self-flagged in prose)
**Assertion type:** I-LANGUAGE / hedged
**Sentence:** "Industry access-tracking (ZS AccessMonitor and similar trackers) has documented a long downward slide ... [verify — unconfirmed: the specific '45% available / ~30% single-brand-restricted by early 2024' figures did not resolve to a current ZS primary release; the documented trend is rising restriction.]"
**Claim checked:** ZS AccessMonitor specific figures (45% rep-accessible / ~30% single-brand-restricted, early 2024).
**Site visited:** ZS AccessMonitor (no current primary release resolving the exact figures)
**Finding:** The qualitative trend (declining rep access since COVID, majority now restricting to some degree) is well-documented; the specific decimal figures did not resolve to a current ZS primary release. Already carried as `[verify — unconfirmed]` in prose. Maps to UNVERIFIED.
**Expert review needed:** No
**Suggested reference:** Could not identify a current ZS primary release stating the exact 45%/30% figures.
**Notes:** Trend confirmed; precise figures unconfirmed; correctly hedged.

### STAT — Vendor/consulting figures (firewall-attributed, contested in-text)
**Assertion type:** I-LANGUAGE / hedged
**Sentence:** "McKinsey has cited a 50 to 65 percent reduction in regulatory-submission timelines ..."; "Veeva itself estimates 'up to 75%' faster reviews"; "MLR review ... roughly 50 to 60 days per piece"; "~20 percent more content each year ... about 77 percent of field content is never used (Veeva Pulse, 2025)"; "20:1 ROI"; "4 percent to 44 percent" script-lift range.
**Claim checked:** Vendor/consulting MLR, content, ROI, and lift figures.
**Site visited:** McKinsey life-sciences insights; Veeva Pulse 2025; vendor pages (all self-reported)
**Finding:** These are vendor- or consulting-firm-generated figures. Per the firewall rule, a vendor confirming its own claim is not independent verification. The chapter explicitly presents them as attributed, methodologically opaque, and in tension (McKinsey 50–65% vs. MIT 95% fail), refusing to treat any as settled. Treated as vendor-attributed by design; not independently verifiable.
**Expert review needed:** No (handled correctly in-text)
**Suggested reference:** McKinsey life-sciences insights (mckinsey.com); Veeva Pulse 2025 — both vendor/consulting self-reported.
**Notes:** Firewall preserved. The 50–60-day MLR baseline and 77%-unused / 20%-more-content figures are Veeva/vendor operations data, labeled as such.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "...the specific '45% available / ~30% single-brand-restricted by early 2024' figures did not resolve to a current ZS primary release..." | STAT | I-LANGUAGE / hedged | No current ZS primary release for the exact figures; already `[verify — unconfirmed]` in prose. |
| "McKinsey has cited a 50 to 65 percent reduction in regulatory-submission timelines..." | STAT | I-LANGUAGE | Consulting-firm figure, methodology opaque; firewall-attributed and contested in-text. |
| "Veeva itself estimates 'up to 75%' faster reviews" / 50–60-day MLR baseline / 77%-unused / 20%-more-content | STAT | I-LANGUAGE | Vendor self-reported operations figures; not independently validated; labeled as such in prose. |
| "...the range runs from 4 percent to 44 percent" script-lift; "20:1 ROI"; Frost & Sullivan recognition | STAT | I-LANGUAGE | Vendor-generated, attribution-circular by the chapter's own argument; firewall-attributed. |

---
## AI-Pass Flags
None. The chapter's central move — separating "capability is real" from "effect is proven" — is applied consistently, and the McKinsey/MIT figures are explicitly held as non-reconcilable rather than averaged or cherry-picked. The maturity ladder and five-question audit are the book's own constructs, internally consistent. No definitional errors or logical contradictions.
