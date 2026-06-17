# Chapter 7 — Mixture of Experts and Related Routing Models (and When the Word Is Marketing)

## 1. Chapter overview

A vendor deck lands on your desk. The hero slide says the platform is "powered by an adaptive Mixture of Experts." You have read Chapter 6, so you know that a tuned gradient-boosted tree ensemble is the baseline any fancier claim has to beat on tabular prescriber data. Now you need to know one thing: is "Mixture of Experts" naming a real architectural upgrade, or is it a transformer-era label glued onto ordinary model stacking?

This chapter teaches you enough genuine Mixture of Experts (MoE) to answer that question. By the end you will be able to explain what a sparse-gated MoE layer actually is — the formal routing operation, the load-balancing problem, what experts really specialize in — and trace the line of real systems from Shazeer's 2017 paper through Switch, Mixtral, and DeepSeek-V3 to the 2025 frontier of Llama 4, Qwen3, and GLM. More importantly, you will be able to name the two distinctions that genuinely separate MoE from ensemble stacking, apply six buyer-verification questions to any "MoE" platform claim, and reach a defensible verdict. The payload for pharma work is uncomfortable for the marketing slide: for tabular NPI prediction, MoE is usually *not* the right tool, and a "MoE targeting engine" is most often legitimate stacking wearing a borrowed name. The skill you are building is audit, not implementation. You are learning to detect MoE, not to build it.

## 2. Learning objectives

By the end of this chapter you will be able to:

1. **(Understand)** Explain sparse gating (Shazeer et al. 2017), top-k routing, load balancing, and expert collapse; and trace the genuine-MoE lineage Switch → Mixtral 8x7B → DeepSeek-V3 → 2025 frontier models (Llama 4, Qwen3, GLM).
2. **(Analyze)** Explain *output standardization* and *joint end-to-end training* as the real architectural differences from ensemble stacking, and describe what MoE experts actually specialize in (syntactic/computational patterns more than semantic domains).
3. **(Evaluate)** Apply the six buyer-verification questions to a "MoE" platform claim, reach a verdict, and judge when MoE is meaningful (scale, token/sequence, multi-task) versus irrelevant (tabular NPI prediction).

*Part B:* run the same teardown on a "MoE" or "AI engine" claim relevant to your own research thread.

## 3. Opening case — the "MoE targeting engine" that is XGBoost plus rules

A martech vendor pitches an HCP-targeting platform "built on an adaptive Mixture-of-Experts architecture that learns which expert to trust for each physician." It sounds like the frontier. You ask for the architecture diagram, and under a friendly NDA the data-science lead walks you through it.

Here is what is actually running. One model is an XGBoost classifier that scores each NPI's propensity to prescribe. A second, separate model predicts the optimal bid for a programmatic impression. A third is a rules engine that enforces fair-balance and suppression constraints. Their outputs feed a learned aggregator that produces the final targeting decision. The lead is proud of it, and should be: this is legitimate, effective machine learning. It ships, it works, it makes money.

But it is not a Mixture of Experts. It has none of MoE's defining properties. There is no token-level routing, because there are no tokens — the input is a physician feature vector, not a sequence. There is no sparse activation of sub-networks. There is no shared output space; the three models emit incommensurable things (a probability, a bid, a pass/fail flag) that the aggregator must translate. And there is no joint end-to-end training — the three models were trained separately, frozen, and only then combined. This is **stacking**, a paradigm you met in Chapter 6, relabeled with a name from large-language-model research.

The honest verdict — the one you can defend to a partner without burning the relationship — is precise: *this is not MoE, and it is not obviously better than a tuned ensemble.* It is not fraud. Stacking is a fine architecture, and on tabular prescriber data it may be the genuinely superior one. The problem is the label. "Mixture of Experts" implies scaling and joint-optimization capabilities the system does not have — and on tabular data, those capabilities would be irrelevant even if it did. The relabel buys marketing gloss, not performance. The rest of this chapter gives you the vocabulary to deliver that verdict every time, and to tell the rare genuine case from the common relabel.

## 4. Core sections

### 4.1 What a Mixture of Experts actually is

A Mixture of Experts is not "several models in a trench coat." It is a specific neural-network layer. Given $N$ expert networks $E_1, E_2, \dots, E_N$ and a gating function $G$, the MoE output is a weighted sum:

$$y = \sum_{i=1}^{N} G(x)_i \cdot E_i(x)$$

The gating vector is computed by routing the input through a small learned gate, then keeping only its strongest entries:

$$G(x) = \text{Softmax}(\text{Top-}k(H(x))), \qquad H(x) = x \cdot W_{\text{gate}} + \epsilon$$

where $\epsilon$ is Gaussian noise added to help balance load (Shazeer et al. 2017), and Top-$k$ zeros out all but the $k$ largest gate scores before the softmax. That zeroing is the whole trick. It makes activation **sparse**: only $k$ of the $N$ experts fire for any given input. Model capacity can grow with the total number of experts while the compute per forward pass stays roughly flat, because you only ever run $k$ of them.

The single most important structural fact hides in plain sight: **all experts share identical input and output dimensionality.** That is why the weighted sum is mathematically clean — it is a convex combination *in a shared vector space*. If the experts emitted different output shapes, you could not add them; you would need a translation layer. Hold onto that. Output standardization is the crux of the entire chapter, and it is exactly what the opening-case platform lacked.

The idea is old. Jacobs, Jordan, Nowlan, and Hinton introduced "Adaptive Mixtures of Local Experts" in 1991 for vowel discrimination, and Jordan and Jacobs extended it to hierarchical mixtures in 1994. Then it went quiet for roughly twenty-six years. The missing ingredient was scale: the architecture only demonstrates its advantage when there is enough compute and enough capacity to route across. Shazeer et al. (2017), "Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer," with Hinton and Dean, supplied it — scaling MoE to a 137-billion-parameter LSTM by activating only the top-$k$ experts per token. Sparsity was the unlock.

### 4.2 The two distinctions that actually separate MoE from stacking

This is the load-bearing section. Both MoE and ensemble stacking combine multiple components, so "it has multiple models" tells you nothing. Two things, and only two, make MoE architecturally different from stacking (grounded in `pantry/moe-vs-ensemble-synthesis.md` §5).

**Distinction one: output standardization, which buys differentiability.** Because all experts live in the same input/output space, the combination $y = \sum G(x)_i E_i(x)$ is differentiable with respect to *both* the gating weights and the expert parameters. The whole system can be optimized end to end by a single backpropagation pass. In a stacked ensemble, the components emit incommensurable formats — a random forest gives a probability vector, a gradient-boosted tree gives a score, a logistic regression gives log-odds — and the meta-learner must first learn to translate between them. That translation layer is an extra source of error and opacity, and it blocks joint gradient flow.

**Distinction two: joint, end-to-end training, which produces co-adaptation.** In MoE the gating network and the experts train together. The router learns to send inputs to the experts that handle them well; the experts learn to handle whatever they get routed. They *co-adapt*. Specialization is therefore **emergent** — a consequence of routing, not something engineered in advance. In stacking, the base models are trained and frozen *before* the meta-learner ever sees them. There is no co-adaptation and no joint optimization. As the synthesis puts it, "you're combining separately trained artifacts and hoping the combination beats the parts."

If a platform's components are trained separately and combined afterward, it is stacking — no matter how sophisticated the aggregator. That single test resolves most "MoE" claims.

### 4.3 The load-balancing versus specialization tension

Genuine MoE is not free magic; it has a hard, unsolved problem at its center. Without intervention, routing **collapses**. Early in training a few experts get most of the routing, so they receive most of the gradient, so they improve fastest, so they attract even more routing. You pay for 256 experts and end up using three. This is *expert collapse*.

The field has three main fixes, and the progression is worth knowing because it shows up in vendor sophistication claims. (a) An **auxiliary load-balancing loss** (the Switch Transformer approach) penalizes imbalanced routing — but it introduces interference gradients that can hurt model quality; set the penalty too high and quality suffers, too low and collapse returns. (b) **Noisy top-$k$ gating** (the $\epsilon$ term in Shazeer 2017) forces exploration so no expert dominates on a slight early lead. (c) **Auxiliary-loss-free balancing via dynamic bias terms** (DeepSeek) nudges overloaded experts down and underused experts up without polluting the gradient — current best practice.

Notice the deep tension underneath all three: load balancing pushes routing toward *uniform*, but specialization requires *non-uniform* routing. The two objectives genuinely conflict. Recent work finds that load-balanced routing creates overlapping token distributions across experts, which *reduces* the specialization the architecture exists to produce. This is the honest counterweight to MoE hype: the mechanism that prevents collapse partly defeats the purpose.

### 4.4 What experts actually specialize in (and why it matters for pharma)

Here intuition fails almost everyone. The natural assumption is that one expert "does math," another "does code," another "does biology." That is largely wrong. Interpretability work on Mixtral 8x7B finds that experts specialize in **syntactic and computational patterns — token type — far more than in semantic domains**. A punctuation token routes differently from a verb regardless of the topic of the sentence. Worse for the diversity story: in some trained MoE models, experts converge to greater than 99% similarity — the architecture's promised functional diversity quietly collapses into redundancy.

Now carry that to pharma. NPI prediction operates on tabular feature vectors: prescribing history, demographics, Open Payments signals, behavioral indicators. There is **no token sequence and no syntactic structure.** The very mechanism by which MoE experts specialize — routing on token type within a sequence — has no natural analogue. As the synthesis flags directly: "It's unclear what 'specialization' would mean for an expert routing on NPI feature vectors." The architecture's signature advantage is not merely unhelpful here; it may be undefined.

### 4.5 The genuine MoE lineage — dated examples, stable principle

Model names age fast, so treat every name below as a dated example of a stable idea. The TIKTOC aging-risk rating for these specifics is High; verify configurations against primary tech reports before relying on them. `[verify model-config specifics — expert counts, top-k — against primary tech reports]`

- **Switch Transformer** (Fedus, Zoph, Shazeer 2022): top-1 routing — one expert per token. Simpler routing turned out to be more stable, and it scaled toward trillion-parameter models.
- **Mixtral 8x7B** (Jiang et al. 2024): 8 experts per layer, top-2 routing; about 47B total parameters but only ~13B active per token; roughly Llama 2 70B quality at about one-fifth the active parameters. The first major open-source MoE success.
- **DeepSeek-V3** (2024): 671B total / 37B active (~5.5%); **256 fine-grained experts**, 8 routed per token; **auxiliary-loss-free** balancing; a **shared-expert** mechanism (1–2 always-active experts carrying "common knowledge").
- **2025 frontier** `[verified via web 2026-06-16; confirm against primary tech reports]`: MoE is now standard across frontier open models. **Llama 4** (Maverick/Scout: 1 shared + 1 routed expert, top-1 routing — sparser than DeepSeek); **Qwen3** (e.g. Qwen3-235B-A22B, *no* shared expert); **GPT-OSS** (20B/120B, no shared expert); **GLM-5**; DeepSeek-R1-0528 (1 shared + 8 of 256 routed). Three trend lines: fine-grained, high-count experts are now the norm; the shared expert is now *optional* (DeepSeek and Llama 4 use it, Qwen3 and GPT-OSS skip it); and there is no single best MoE design, only trade-offs.

Every one of these is a large-scale sequence model. That is not an accident — it is the regime where MoE's advantages live.

### 4.6 The tabular exception — the pharma payload

Where is MoE actually superior? At scale, in sequential/token data, and in heterogeneous multi-task settings. Where is it *not*? On structured tabular prediction — which is exactly what NPI propensity, behavioral prediction, and bid optimization on claims data are.

Grinsztajn et al. (NeurIPS 2022) benchmarked deep-learning methods against tree-based models across 45 tabular datasets and found tree-based models remain state of the art on medium-sized tabular data, even before accounting for their speed advantage. The reasons are structural: trees are natively robust to uninformative features (and real claims data is full of them), they handle the irregular target functions tabular data tends to have, and the best tabular methods are themselves ensembles of decision trees. You met this result in Chapter 6 as the reason XGBoost is your baseline. Here it delivers the verdict.

So for pharma commercial ML, the gradient-boosted ensemble is **not a simplified stand-in for MoE — it is likely the genuinely superior architecture for the task** [contested — see pantry: the magnitude of any MoE advantage in commercial structured prediction is not empirically established]. The MoE label in pharma ad-tech reflects scale *ambition*, not deployment reality. This gives you the single most important sentence of the chapter: genuine MoE's advantages — sub-linear scaling, joint optimization, token-level routing — are real but irrelevant to tabular NPI prediction. So a "MoE" pharma platform is either mislabeled stacking or a scale-regime tool applied to a problem with no scale regime. Either way, your move is the same: demand the Chapter 6 baseline comparison.

## 5. Worked example — running the six buyer questions

**Process.** Return to the opening-case platform and interrogate it with the six buyer-verification questions, the reusable audit instrument of this chapter (from `pantry/moe-vs-ensemble-synthesis.md` §8).

1. *What are the component models (algorithms, training data)?* — XGBoost propensity model, a separate bid model, a rules engine. **Three distinct algorithms.**
2. *Trained jointly or independently?* — Independently, then frozen. **Independent.**
3. *Shared I/O interfaces, or does the aggregator translate formats?* — Outputs are a probability, a bid, and a flag; the aggregator translates. **No shared output space.**
4. *Routing: learned and jointly trained, or rule-based / separately trained assignment?* — A learned aggregator over frozen models; no token-level routing. **Not joint routing.**
5. *Does "MoE" denote a meta-architecture across separate models, or a sub-network routing layer within one model?* — Across separate models. **Meta-architecture, i.e. stacking.**
6. *Performance versus a well-tuned XGBoost ensemble on the same task, on what independent benchmark?* — No independent benchmark offered. **Unverified.**

There is also a fast three-criterion screen for when you are short on time: *token-level routing? shared trunk/output space? jointly trained?* Three "no"s means it is stacking.

**Lesson.** Every honest answer points the same way: this is stacking. The verdict to write is "not MoE; not shown to beat a tuned ensemble; demand a head-to-head benchmark against the Chapter 6 baseline." Note what made the audit possible — you never needed the platform's internals. The buyer questions are designed to work *because* internals are usually undisclosed; the answers a vendor gives (or refuses to give) are themselves the evidence.

**Limit.** The teardown tells you the *label* is wrong. It does not tell you the *platform* is bad. Stacking may be exactly right for this task. And the audit cannot, by itself, prove the ensemble is better — only a benchmark can. The buyer questions diagnose mislabeling; they do not substitute for the empirical comparison that question 6 demands. That comparison is a Chapter 13 study, not a conversation.

## 6. Common misconceptions

- **"It combines several models, so it's a Mixture of Experts."** Combination is not the distinction; both MoE and stacking combine. The distinctions are output standardization and joint end-to-end training.
- **"MoE is just a fancier, better ensemble — strictly an upgrade."** It is a different tool with a different sweet spot. On tabular data, tree ensembles are likely superior, not a downgrade.
- **"Each expert is a domain specialist."** Empirically, experts route on syntactic/token patterns more than semantic domains, and can converge to near-identical representations.
- **"More experts means proportionally more capability."** Without load balancing, routing collapses onto a few experts; with aggressive load balancing, specialization erodes. The relationship is fraught, not linear.
- **"If a platform says MoE, it must be running MoE."** Usually it is stacking relabeled — and on tabular pharma data, MoE's properties would be irrelevant even if present.

## 7. Evidence check and Compliance and welfare check

**Evidence check.** *Independent / settled:* the formal sparse-gated MoE definition (Shazeer 2017), the output-standardization and joint-training distinctions from stacking, the load-balancing/specialization tension, and the tabular-data result that tree ensembles lead (Grinsztajn et al., NeurIPS 2022) are settled and well sourced. *Vendor-generated:* the opening-case platform and the "powered by MoE" claim are illustrative composites of the kind of marketing language this book audits, not a named product. *Hypothetical / proposal:* a systematic public audit of pharma "MoE" platform claims against the three criteria does not yet exist — that is the Chapter 13, Track C study this chapter sets up; do not present it as completed. *Contested:* whether MoE's correlation/diversity advantage is empirically robust (>99% expert similarity is documented), and whether output standardization is decisive for commercial structured prediction, remain open `[contested — see pantry]`.

**Compliance and welfare check.** Architecture choice is not compliance-neutral. A genuinely opaque routing model makes MLR review and fair-balance auditing harder than an interpretable tree ensemble — routing is difficult to explain to a reviewer who must certify why a given physician received a given message. The interpretability cost is itself a compliance cost, and a reason the "simpler" ensemble can be the more *defensible* choice in a regulated channel. The welfare check here is indirect but real: chasing an architecture for its prestige rather than its fit can degrade explainability without improving targeting, and an unexplainable targeting decision is harder to challenge when it serves a commercial event rather than a patient need.

## 8. Exercises

1. **(Understand)** In your own words, explain why the weighted sum $y = \sum G(x)_i E_i(x)$ is "clean" in a genuine MoE layer but requires a translation layer in a stacked ensemble. Name the one structural property that makes the difference.
2. **(Apply)** Take a public vendor description of an "AI-powered" or "MoE" HCP-targeting platform. Run all six buyer-verification questions against it, marking each answer as confirmed, denied, or undisclosed, and write a two-sentence verdict in the "not MoE / not obviously better than a tuned ensemble — demand a benchmark" register.
3. **(Apply+ / Part B)** For your own research thread, find one architecture or "engine" claim and apply the fast three-criterion screen (token-level routing? shared output space? jointly trained?). State what additional evidence — and specifically what baseline comparison — you would need before believing the claim.
4. **(Produce)** Draft a one-page **MoE-claim teardown memo** a Fellow could hand to a partner's data-science lead: the claim as stated, the six answers, the verdict, and the single benchmark you are requesting. Keep the framing collaborative — diagnose the label, not the team.

## 9. Five-part AI block

**When to use AI here.** Use an LLM to *restate* an unfamiliar architecture in plain language, to generate first-draft answers to the six buyer questions from a vendor's public text, and to surface the primary citations (Shazeer 2017, Switch, Mixtral, DeepSeek-V3) you should then read yourself.

**When NOT to use AI here.** Do not let an LLM reach the verdict. It will happily call a stacked system "MoE" if the marketing copy does, and it will confidently misstate expert counts and routing schemes — exactly the High-aging-risk details you must verify against tech reports. The label call is a human judgment.

**LLM exercise.** Paste a vendor's public architecture paragraph and prompt: "Answer these six questions about this system using only what the text states; mark anything not stated as 'undisclosed' and do not infer." Then check whether it respected the "undisclosed" instruction or quietly filled gaps.

**CLI exercise.** Using a notebook, train a tuned gradient-boosted baseline (XGBoost or LightGBM) on a public tabular prescriber-style dataset and record its calibrated performance. This is the number any "MoE" claim must beat — the literal artifact behind buyer question 6.

**AI validation.** For three model facts an LLM gives you about MoE systems (e.g., DeepSeek-V3 expert count, Mixtral routing, whether Qwen3 uses a shared expert), locate the primary tech report and confirm or correct each. Log every correction. This trains the verify-not-trust reflex the chapter depends on.

## 10. AI Use Disclosure

If you used an LLM in this chapter's exercises, disclose where, and name one judgment the AI could not make: most pointedly, *whether the claim is genuine MoE or relabeled stacking, and whether the architecture is even the right tool for tabular NPI prediction.* That verdict requires reading primary sources and demanding a baseline benchmark — a human call the model cannot certify.

## 11. What would change my mind

The chapter's position is that MoE is usually the wrong tool for NPI prediction and usually a relabel when claimed in pharma ad-tech. Evidence that would move me: a peer-reviewed or rigorously documented benchmark showing a genuinely jointly-trained, token-or-feature-routed MoE beating a well-tuned gradient-boosted ensemble on a real NPI/NBRx task — with better calibration and subgroup robustness, not just headline AUC. Equally, a vendor that answers all six buyer questions transparently and demonstrates token-level routing, a shared trunk, and joint training would earn the genuine-MoE label honestly. The position is evidence-based, not anti-vendor; it inverts on evidence.

## 12. Still puzzling

What would "specialization" even mean for experts routing on NPI feature vectors, where there is no sequence and no syntactic structure? If fine-grained experts on tabular data discovered stable, interpretable physician archetypes via routing geometry, that would be a genuinely new finding — and the "natural N archetypes" idea (Chapter 13, Track C) is exactly that gamble. It is open whether the gamble pays, or whether routing on tabular data degenerates into the redundancy the >99%-similarity result warns about.

## 13. Summary

You can now state what a sparse-gated MoE layer is, why sparsity was the 2017 unlock, and how the architecture has evolved from Switch through Mixtral and DeepSeek-V3 to the 2025 frontier. You can name the two distinctions that genuinely separate MoE from stacking — output standardization (which buys differentiability) and joint end-to-end training (which buys emergent co-adaptation) — and you know what experts really specialize in. Most usefully, you can run the six buyer-verification questions, deliver the honest "not MoE / not obviously better than a tuned ensemble" verdict, and recognize that on tabular NPI prediction the ensemble baseline is the architecture to beat. Architecture, though, is a sideshow next to the next question. Predicting which physician will prescribe is not the same as changing whether they do.

## 14. Key terms

- **Mixture of Experts (MoE):** a neural-network layer that routes each input to a sparse subset of expert sub-networks and combines their outputs as a weighted sum in a shared vector space.
- **Sparse gating / top-$k$ routing:** activating only the $k$ highest-scored experts per input, so capacity grows without proportional compute.
- **Output standardization:** all experts sharing identical input/output dimensionality, which makes the weighted sum clean and the system differentiable end to end.
- **Joint (end-to-end) training:** training gating and experts together in one backpropagation pass, producing emergent specialization through co-adaptation.
- **Expert collapse / load balancing:** the failure where routing concentrates on a few experts, and the counter-measures (auxiliary loss, noisy gating, auxiliary-loss-free bias) that fight it at some cost to specialization.
- **Stacking:** combining separately trained, frozen models with a meta-learner — legitimate ML, but not MoE.
- **The tabular exception:** the empirical finding that tree ensembles, not deep or routed architectures, lead on structured tabular prediction.

## 15. Bridge

Suppose the architecture is genuine and the baseline is beaten. You now have a model that predicts, with real accuracy, which physician will prescribe. Does that tell you which physician your campaign *changed*? It does not. A perfect predictor of prescribing can be a useless intervention target — because the physicians easiest to predict are often the ones who would have prescribed anyway. The next chapter is the hardest inversion in the book: from "who will prescribe?" to "whose behavior changed *because of* what we did?" We will teach it the way it has to be learned — with a holdout that makes a proud lift number shrink.

## 16. Further reading

- Shazeer, N., et al. (2017). *Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer.* The modern MoE foundation — sparsity, noisy top-$k$ gating, the 137B LSTM. `[verify arXiv id]`
- Fedus, W., Zoph, B., & Shazeer, N. (2022). *Switch Transformers.* Top-1 routing and the case that simpler routing scales more stably. `[verify JMLR cite]`
- Jiang, A., et al. (2024). *Mixtral of Experts.* The first major open-source MoE success; 8 experts, top-2. `[verify arXiv id]`
- DeepSeek-AI (2024). *DeepSeek-V3 Technical Report.* Fine-grained experts, auxiliary-loss-free balancing, shared experts — current best practice. `[verify cite]`
- Grinsztajn, L., Oyallon, E., & Varoquaux, G. (2022). *Why do tree-based models still outperform deep learning on tabular data?* NeurIPS 2022. The empirical anchor for the tabular exception — read alongside Chapter 6.
- `pantry/moe-vs-ensemble-synthesis.md` — the in-pantry primary synthesis this chapter restructures, including the full six buyer questions and the open-questions section.

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
