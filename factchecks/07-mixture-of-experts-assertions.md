# Assertions Report: 07-mixture-of-experts.md
**Date:** 2026-06-17
**Source file:** chapters/07-mixture-of-experts.md
**Assertions flagged:** 7
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 5 | CURRENT: 0
---
## ⚠️ Critical — Requires Immediate Expert Review
None found.
---
## Full Findings

### SPECIALIST — CONFIRMED (Shazeer 2017 sparse MoE)
**Assertion type:** BASIC
**Sentence:** "Shazeer et al. (2017), 'Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer,' ... scaling MoE to a 137-billion-parameter LSTM by activating only the top-k experts per token."
**Claim checked:** Title, author, year, 137B parameters, LSTM, sparsely-gated top-k.
**Site visited:** https://arxiv.org/abs/1701.06538
**Finding:** Exact. Shazeer, Mirhoseini, Maziarz, Davis, Le, Hinton, Dean (2017); abstract states MoE "with up to 137 billion parameters ... applied convolutionally between stacked LSTM layers." The noisy top-k gating with Gaussian noise (the ε term in the chapter's gating equation) is from this paper. arXiv 1701.06538.
**Expert review needed:** No
**Suggested reference:** Shazeer et al., arXiv:1701.06538 (2017).
**Notes:** Gating formula and noisy top-k attribution are accurate.

### SPECIALIST — CONFIRMED (Jacobs/Jordan/Nowlan/Hinton 1991 origin)
**Assertion type:** BASIC
**Sentence:** "Jacobs, Jordan, Nowlan, and Hinton introduced Adaptive Mixtures of Local Experts in 1991 for vowel discrimination; Jordan and Jacobs extended it to hierarchical mixtures in 1994."
**Claim checked:** 1991 origin, authors, vowel-discrimination task, 1994 hierarchical extension.
**Site visited:** https://direct.mit.edu/neco/article/3/1/79 (Neural Computation 3(1):79–87, 1991)
**Finding:** Exact. Jacobs, Jordan, Nowlan & Hinton, "Adaptive Mixtures of Local Experts," Neural Computation 3(1):79–87, 1991; the paper demonstrates dividing a vowel-discrimination task into subtasks. Jordan & Jacobs hierarchical mixtures of experts (Neural Computation 1994) is a real, well-documented follow-up.
**Expert review needed:** No
**Suggested reference:** Jacobs, Jordan, Nowlan & Hinton, Neural Computation 3(1):79–87 (1991).

### SPECIALIST — CONFIRMED (Switch Transformer)
**Assertion type:** POSITIVE
**Sentence:** "Switch Transformer (Fedus, Zoph, Shazeer, JMLR 2022; arXiv 2101.03961): top-1 routing — one expert per token ... it scaled toward trillion-parameter models."
**Claim checked:** Authors, venue, arXiv ID, top-1 routing, trillion-parameter scaling.
**Site visited:** https://arxiv.org/abs/2101.03961
**Finding:** Exact. Fedus, Zoph, Shazeer; comment field reads "JMLR"; abstract describes simplified routing and pre-training "up to trillion parameter models." Switch uses top-1 (single expert) routing. arXiv 2101.03961.
**Expert review needed:** No
**Suggested reference:** Fedus, Zoph & Shazeer, arXiv:2101.03961 (JMLR).

### SPECIALIST — CONFIRMED (Mixtral 8x7B)
**Assertion type:** POSITIVE
**Sentence:** "Mixtral 8x7B (Jiang et al. 2024; arXiv 2401.04088): 8 experts per layer, top-2 routing; roughly 47 billion total parameters but only about 13 billion active per token ... matching or outperforming Llama 2 70B and GPT-3.5."
**Claim checked:** Authors, arXiv ID, 8 experts, top-2, 47B total / 13B active, Llama 2 70B / GPT-3.5 comparison.
**Site visited:** https://arxiv.org/abs/2401.04088
**Finding:** Exact. First author Albert Q. Jiang; abstract: "8 feedforward blocks (i.e. experts) ... router network selects two experts ... 47B parameters, but only uses 13B active parameters ... outperforms or matches Llama 2 70B and GPT-3.5 across all evaluated benchmarks." arXiv 2401.04088.
**Expert review needed:** No
**Suggested reference:** Jiang et al., arXiv:2401.04088 (2024).

### SPECIALIST — CONFIRMED (DeepSeek-V3)
**Assertion type:** POSITIVE
**Sentence:** "DeepSeek-V3 (DeepSeek-AI 2024; arXiv 2412.19437): 671 billion total, 37 billion active — about 5.5 percent utilization. 256 routed experts, 8 activated per token, auxiliary-loss-free balancing, and a shared-expert mechanism."
**Claim checked:** arXiv ID, 671B total / 37B active, ~5.5% utilization, auxiliary-loss-free load balancing, shared-expert.
**Site visited:** https://arxiv.org/abs/2412.19437
**Finding:** Confirmed. Abstract: "671B total parameters with 37B activated for each token ... pioneers an auxiliary-loss-free strategy for load balancing." 37/671 = 5.5% ✓. The "256 routed / 8 activated / shared expert" configuration is the DeepSeekMoE architecture detailed in the technical report body (consistent with V2/DeepSeekMoE). DeepSeek-AI 2024, arXiv 2412.19437.
**Expert review needed:** No
**Suggested reference:** DeepSeek-AI, DeepSeek-V3 Technical Report, arXiv:2412.19437 (2024).
**Notes:** Auxiliary-loss-free dynamic-bias load-balancing claim (line 73) is directly supported by the abstract.

### EVIDENCE — CONFIRMED (Grinsztajn tabular result, restated)
**Assertion type:** POSITIVE
**Sentence:** "Grinsztajn, Oyallon, and Varoquaux (NeurIPS 2022; arXiv 2207.08815) benchmarked deep-learning architectures against tree-based models across 45 tabular datasets. Tree-based models remained state of the art."
**Claim checked:** Same paper as Ch6.
**Site visited:** https://arxiv.org/abs/2207.08815
**Finding:** Confirmed (see Ch6 report). Exact restatement.
**Expert review needed:** No
**Suggested reference:** Grinsztajn et al., arXiv:2207.08815.

### EVIDENCE — UNVERIFIED (Mixtral interpretability / >99% expert similarity)
**Assertion type:** EMPHATIC
**Sentence:** "Interpretability work on Mixtral 8x7B finds that experts specialize in syntactic and computational patterns — token type — far more than semantic domains ... in some trained MoE models, experts converge to greater than 99 percent representational similarity."
**Claim checked:** Whether the token-type-not-semantic-domain finding and the >99% similarity figure are from real interpretability literature.
**Site visited:** Attempted general search; the Mixtral paper itself (2401.04088) reports the syntactic/token-position routing observation in its routing-analysis section, supporting the token-type claim. The specific ">99% representational similarity" figure was not pinned to a single primary source in this pass.
**Finding:** The token-type-over-semantic-domain finding is consistent with the Mixtral paper's own routing analysis (routing correlates with token id / syntax, not topic). The >99% expert-similarity claim is a real strand of MoE interpretability/redundancy literature but the exact figure is not anchored to a confirmed primary source here.
**Expert review needed:** Yes — confirm the >99% similarity figure against a named interpretability paper before relying on the precise number.
**Suggested reference:** Mixtral routing analysis (arXiv:2401.04088, §on routing); pantry note recommended for the >99% figure.
**Notes:** Chapter presents these as interpretability findings without a precise inline citation; the directional claim is sound, the exact decimal is the soft spot.

---
## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
| --- | --- | --- | --- |
| "The 2025 frontier [verify — model-specific configurations below ...]: MoE is now standard across frontier open models ... fine-grained-expert pattern ..." | CURRENT | BASIC | Chapter explicitly flags 2025-frontier model configs as recent/fast-moving and unconfirmed by design. Correctly left flagged. |
| ">99 percent representational similarity" (expert convergence) | EVIDENCE | EMPHATIC | Real literature strand; exact figure not anchored to a confirmed primary source this pass (see Full Findings). |
| "[contested — the magnitude of any MoE advantage in commercial structured prediction is not empirically established; see pantry]" | EVIDENCE | I-LANGUAGE | Author-flagged as contested/open; not a citable empirical result. Correctly hedged. |

---
## AI-Pass Flags
The two structural distinctions (output standardization → differentiability; joint end-to-end training → co-adaptation), the stacking-vs-MoE table, the load-balancing/specialization tension, and the six buyer questions are internally consistent and technically accurate. The central thesis — that "MoE" on tabular prescriber data is usually relabeled stacking and offers no regime advantage — is argued correctly from the verified Grinsztajn result. No definitional errors. The opening-case vendor teardown is a presented scenario, appropriately framed.
