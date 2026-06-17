# Chapter 7 — Mixture of Experts and Related Routing Models (and When the Word Is Marketing)
*The architecture is real. Whether it belongs on your vendor's slide is the question.*

A vendor deck arrives. The hero slide says the platform is "powered by an adaptive Mixture of Experts." You have read Chapter 6, so you know that a tuned gradient-boosted tree ensemble is the baseline any fancier claim has to beat on tabular prescriber data. Now you need to know one thing: is "Mixture of Experts" naming a real architectural upgrade, or is it a transformer-era label glued onto ordinary model stacking?

Start with the opening case, because it is the common case.

A martech vendor pitches an HCP-targeting platform "built on an adaptive Mixture-of-Experts architecture that learns which expert to trust for each physician." You ask for the architecture diagram. Under a friendly NDA, the data-science lead walks you through it. One model is an XGBoost classifier scoring each NPI's prescribing propensity. A second, separate model predicts the optimal bid for a programmatic impression. A third is a rules engine enforcing suppression and fair-balance constraints. Their outputs feed a learned aggregator that produces the final targeting decision.

The lead is proud of this, and should be. It ships. It works. It makes money. But it is not a Mixture of Experts. There is no token-level routing, because there are no tokens — the input is a physician feature vector, not a sequence. There is no sparse activation of sub-networks. The three models emit incommensurable things: a probability, a bid, a pass/fail flag. And they were trained separately, frozen, and only then combined. This is **stacking** — a legitimate, well-understood ensemble paradigm — wearing a name borrowed from large-language-model research.

The honest verdict is not "fraud." The honest verdict is: *this is not MoE, and it is not obviously better than a tuned ensemble.* The problem is the label. "Mixture of Experts" implies capabilities the system does not have — and on tabular prescriber data, those capabilities would be irrelevant even if it had them. By the end of this chapter you will have the vocabulary to deliver that verdict every time, and to recognize the rare genuine case.

---

## What a Mixture of Experts actually is

A Mixture of Experts is not "several models in a trench coat." It is a specific neural-network layer. Given $N$ expert networks $E_1, E_2, \dots, E_N$ and a gating function $G$, the MoE output for any input $x$ is:

$$y = \sum_{i=1}^{N} G(x)_i \cdot E_i(x)$$

The gating vector is computed by routing the input through a small learned gate, keeping only its strongest entries:

$$G(x) = \text{Softmax}(\text{Top-}k(H(x))), \qquad H(x) = x \cdot W_{\text{gate}} + \epsilon$$

where $\epsilon$ is Gaussian noise added to help balance load across experts (Shazeer et al. 2017), and Top-$k$ zeros out all but the $k$ largest scores before the softmax. That zeroing is the whole trick. It makes activation **sparse**: only $k$ of the $N$ experts fire for any given input. Model capacity — the total number of parameters — can grow with the number of experts while the compute per forward pass stays roughly flat, because you only ever run $k$ of them.

![Single input x flowing into a gating network that produces a weight vector; only k of N expert boxes are highlighted (active); their outputs combine via weighted sum to produce y. Sparse activation: N experts exist, k fire. Capacity scales with N; compute scales with k.](images/07-mixture-of-experts-fig-01.png)

*Figure 7.1 — Sparse activation in a MoE layer: gating fires only k of N experts*

<!-- → [DIAGRAM: Single input x flowing into a gating network that produces a weight vector; only k of N expert boxes are highlighted (active); their outputs combine via weighted sum to produce y. Caption: "Sparse activation: N experts exist, k fire. Capacity scales with N; compute scales with k."] -->

The single most important structural fact hides in plain sight. All experts share identical input and output dimensionality. That is why the weighted sum is mathematically clean — it is a convex combination in a shared vector space. If the experts emitted different output shapes, you could not add them; you would need a translation layer first. This property — output standardization — is the crux of the entire chapter. It is exactly what the opening-case platform lacked.

The idea is not new. Jacobs, Jordan, Nowlan, and Hinton introduced Adaptive Mixtures of Local Experts in 1991 for vowel discrimination; Jordan and Jacobs extended it to hierarchical mixtures in 1994. Then it went quiet for roughly twenty-six years. The missing ingredient was scale — the architecture only demonstrates its advantage when there is enough compute to route across enough capacity. Shazeer et al. (2017), "Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer," supplied it, scaling MoE to a 137-billion-parameter LSTM by activating only the top-$k$ experts per token. Sparsity was the unlock.

---

## The two distinctions that actually separate MoE from stacking

Both MoE and ensemble stacking combine multiple components, so "it has multiple models" tells you nothing. Two things — and only two — make MoE architecturally different from stacking.

**Output standardization, which buys differentiability.** Because all experts live in the same input-output space, the combination $y = \sum G(x)_i E_i(x)$ is differentiable with respect to *both* the gating weights and the expert parameters. The whole system can be optimized end to end by a single backpropagation pass. In a stacked ensemble, the components emit incommensurable formats — a random forest gives a probability vector, a gradient-boosted tree gives a score, a logistic regression gives log-odds — and the meta-learner must first learn to translate between them. That translation is an extra source of error, and it blocks joint gradient flow entirely.

**Joint, end-to-end training, which produces co-adaptation.** In MoE the gating network and the experts train together. The router learns to send inputs to the experts that handle them well; the experts learn to handle whatever they get routed. They *co-adapt*. Specialization is therefore emergent — a consequence of routing, not something engineered in advance. In stacking, the base models are trained and frozen *before* the meta-learner ever sees them. There is no co-adaptation and no joint optimization. You are combining separately trained artifacts and hoping the combination beats the parts.

If a platform's components were trained separately and combined afterward, it is stacking. That single test resolves most "MoE" claims.

| Property | Genuine MoE | Stacked ensemble |
| --- | --- | --- |
| Output dimensionality | All experts share one input-output space | Components emit incommensurable formats (probability, score, log-odds) |
| Training regime | Gating and experts trained jointly, end to end | Base models trained and frozen before the meta-learner sees them |
| Gradient flow | Differentiable w.r.t. gating weights and expert parameters | Blocked — meta-learner must translate formats first |
| Routing mechanism | Learned, token-level, sparse top-$k$ | Learned aggregator over frozen outputs; no token-level routing |
| Specialization source | Emergent from co-adaptation of router and experts | None — separately trained artifacts combined after the fact |
| Tabular-data performance | No regime advantage; tree ensembles remain state of the art | Legitimate, well-understood; often the right tool |

*Table 7.1 — The two distinctions that matter. Everything else — number of components, presence of a meta-learner — is shared between the architectures.*

---

## The load-balancing problem: why specialization is harder than it looks

Genuine MoE has an unsolved problem at its center. Without intervention, routing **collapses**. Early in training, a few experts get most of the routing, so they receive most of the gradient, so they improve fastest, so they attract even more routing. You pay for 256 experts and end up using three. This is expert collapse.

The field has three main responses, and the progression tracks the architecture's history.

An **auxiliary load-balancing loss** — the Switch Transformer approach — penalizes imbalanced routing by adding a term to the training objective that discourages any expert from receiving too much traffic. It works, but it introduces gradient interference: set the penalty too high and model quality suffers, set it too low and collapse returns. The tuning is difficult.

**Noisy top-$k$ gating** — the $\epsilon$ term in the Shazeer formulation — adds Gaussian noise before the Top-$k$ selection, so no expert dominates on a slight early lead. It forces exploration. This was the 2017 fix, and it is still in use.

**Auxiliary-loss-free balancing via dynamic bias terms** — the DeepSeek-V3 approach — nudges overloaded experts down and underused experts up by adjusting per-expert bias terms without adding any term to the training loss. The gradient is not polluted. This is the current best practice. [verify DeepSeek-V3 technical details against primary tech report]

Hold the deep tension underneath all three. Load balancing pushes routing toward *uniform* distribution across experts. Specialization requires *non-uniform* routing — experts must see systematically different inputs to develop different capabilities. The two objectives genuinely conflict. Recent interpretability work finds that aggressive load balancing produces overlapping token distributions across experts, which reduces the specialization the architecture was built to produce. The mechanism that prevents collapse partly defeats the purpose.

---

## What experts actually specialize in

Here intuition fails almost everyone. The natural image — one expert handles math, another handles biology, another handles code — is largely wrong.

Interpretability work on Mixtral 8x7B finds that experts specialize in **syntactic and computational patterns — token type — far more than semantic domains.** A punctuation token routes differently from a verb regardless of the topic sentence it lives in. The routing geometry reflects surface-level token structure, not the kind of topic-level functional diversity the architecture appears to promise. More troubling: in some trained MoE models, experts converge to greater than 99 percent representational similarity. The architecture's promised functional diversity quietly becomes redundancy.

Now carry that finding to pharma. NPI prediction operates on tabular feature vectors — prescribing history, demographic signals, Open Payments data, behavioral indicators. There is no token sequence and no syntactic structure. The mechanism by which MoE experts develop specialization — routing on token type within a sequence — has no natural analogue in a physician feature vector. What would "specialization" even mean for an expert routing on NPI features? If routing on tabular data found stable, interpretable physician archetypes, that would be a genuinely new finding. But the null result is more likely: routing degenerates into the same near-redundancy the interpretability work already warns about.

![Two panels. Left: sequence input (tokens) flowing through a MoE layer — color-coded by token type showing which expert each route takes. Right: tabular NPI input (feature vector) flowing toward the same architecture — question mark over the routing, captioned "no syntactic structure to route on." MoE routing specializes on token type in sequential models. What it routes on in a feature-vector regime is an open question — and probably not 'physician archetypes.'](images/07-mixture-of-experts-fig-02.png)

*Figure 7.2 — What MoE routes on: token type versus a feature vector with no structure*

<!-- → [INFOGRAPHIC: Two panels. Left: sequence input (tokens) flowing through a MoE layer — color-coded by token type showing which expert each route takes. Right: tabular NPI input (feature vector) flowing toward the same architecture — question mark over the routing, captioned "no syntactic structure to route on." Caption: "MoE routing specializes on token type in sequential models. What it routes on in a feature-vector regime is an open question — and probably not 'physician archetypes.'"] -->

---

## The genuine MoE lineage

Model names age fast. Treat every name below as a dated example of a stable architectural idea; verify configuration details against primary tech reports before relying on them. `[verify model-config specifics — expert counts, top-k — against primary tech reports]`

**Switch Transformer** (Fedus, Zoph, Shazeer 2022): top-1 routing — one expert per token. The simplification turned out to be more stable than top-2, and it scaled toward trillion-parameter models.

**Mixtral 8x7B** (Jiang et al. 2024): 8 experts per layer, top-2 routing; roughly 47 billion total parameters but only about 13 billion active per token. Approximately Llama 2 70B quality at one-fifth the active-parameter count. The first major open-source MoE success.

**DeepSeek-V3** (2024): 671 billion total, 37 billion active — about 5.5 percent utilization. 256 fine-grained experts, 8 routed per token, auxiliary-loss-free balancing, and a shared-expert mechanism in which one or two experts are always active and carry what might be called common knowledge, with the routed experts handling the specialized work on top.

**2025 frontier** [verified via web June 2026; confirm against primary tech reports]: MoE is now standard across frontier open models. Llama 4 uses a shared-plus-one-routed architecture, sparser than DeepSeek. Qwen3 (e.g., 235B-A22B) uses no shared expert. GPT-OSS models follow a similar pattern. DeepSeek-R1-0528 keeps the 1-shared-plus-8-of-256-routed structure. Three trend lines are visible: fine-grained, high-count experts are now the norm; the shared expert is optional and the field has not settled on whether it helps; and there is no single best MoE design, only trade-offs between routing stability and specialization depth.

Every one of these systems is a large-scale sequence model. That is not an accident. It is the regime where MoE's advantages actually live.

---

## The tabular exception: the pharma payload

Where is MoE genuinely superior? At scale, on sequential or token-structured data, and in heterogeneous multi-task settings where different input types demand functionally different processing. Where is it not? On structured tabular prediction — which is exactly what NPI propensity scoring, behavioral targeting, and bid optimization on claims data are.

Grinsztajn, Oyallon, and Varoquaux (NeurIPS 2022) benchmarked deep-learning architectures against tree-based models across 45 tabular datasets. Tree-based models remained state of the art even before accounting for their speed and interpretability advantages. The reasons are structural: trees are natively robust to uninformative features (and real claims data is full of them), they handle the irregular target functions tabular data tends to produce, and the best-performing tabular methods are themselves ensembles of decision trees. This is the result you met in Chapter 6 as the justification for the XGBoost baseline. Here it delivers the verdict on MoE.

The gradient-boosted ensemble is not a simplified stand-in for MoE on this task. It is likely the genuinely superior architecture for this task. [contested — the magnitude of any MoE advantage in commercial structured prediction is not empirically established; see pantry] The MoE label in pharma ad-tech reflects scaling ambition, not deployment reality. The single most important sentence of the chapter: genuine MoE's advantages — sub-linear scaling, joint optimization, token-level routing — are real in the regime they were designed for and irrelevant to tabular NPI prediction. A "MoE targeting engine" is either mislabeled stacking or a scale-regime tool applied to a problem with no scale regime. Either way, your move is the same: demand the Chapter 6 baseline comparison.

---

## Six buyer questions

Return to the opening-case platform. Run the six questions that form the reusable audit instrument of this chapter.

*What are the component models?* XGBoost propensity model, a separate bid model, a rules engine. Three distinct algorithms.

*Trained jointly or independently?* Independently, then frozen. Independent.

*Shared input-output interfaces, or does the aggregator translate formats?* Outputs are a probability, a bid, and a flag. The aggregator translates. No shared output space.

*Routing: learned and jointly trained, or separately assigned?* A learned aggregator over frozen models, no token-level routing. Not joint routing.

*Does "MoE" denote a routing layer within one model, or a meta-architecture across separate models?* Across separate models. Meta-architecture — stacking.

*Performance versus a well-tuned XGBoost ensemble on the same task, on what independent benchmark?* No independent benchmark offered. Unverified.

There is also a fast three-criterion screen for when you are short on time: *token-level routing? shared trunk and output space? jointly trained?* Three "no" answers means stacking.

![Six-question audit as a vertical checklist with yes/no branches. Fast screen as a three-item inset box. The six buyer questions and the fast screen. A vendor that cannot answer questions 2, 3, and 4 transparently has answered them.](images/07-mixture-of-experts-fig-03.png)

*Figure 7.3 — The six buyer questions and the fast screen*

<!-- → [INFOGRAPHIC: Six-question audit as a vertical checklist with yes/no branches. Fast screen as a three-item inset box. Caption: "The six buyer questions and the fast screen. A vendor that cannot answer questions 2, 3, and 4 transparently has answered them."] -->

The audit does not require the platform's internals. The answers a vendor gives — or refuses to give — are themselves the evidence. Every honest answer for the opening-case platform points the same direction: stacking, not MoE, with no independent benchmark showing it beats the tuned ensemble.

The limit: the teardown tells you the label is wrong. It does not tell you the platform is bad. Stacking may be exactly right for this task. And the audit cannot, by itself, prove the ensemble is better — only a head-to-head benchmark can. The buyer questions diagnose mislabeling; they do not substitute for the empirical comparison that question six demands.

---

## What would change my mind

The chapter's position — that MoE is usually the wrong tool for NPI prediction, and usually a relabel when claimed in pharma ad-tech — inverts on evidence. A peer-reviewed benchmark showing a genuinely jointly trained, feature-routed system outperforming a well-tuned gradient-boosted ensemble on a real NPI or new-to-brand-prescription task, with better calibration and subgroup robustness and not just headline AUC, would move the verdict substantially. Equally, a vendor that answers all six buyer questions transparently and demonstrates joint training and a shared output space would earn the genuine-MoE label honestly. The position is not anti-vendor; it is falsifiable.

## Still puzzling

What would specialization mean for experts routing on NPI feature vectors, where there is no sequence and no syntactic structure? If fine-grained experts on tabular data discovered stable, interpretable physician archetypes via routing geometry, that would be a genuinely new finding — and there is at least a theoretical argument that the routing pressure in joint training could discover such archetypes where hand-crafted segmentation fails. Whether routing on tabular data degenerates into the near-redundancy the greater-than-99-percent similarity result warns about, or whether it finds something real, is open.

---

## Exercises

**Warm-up**

1. *(Recall — tests the formal definition)* Write the MoE output equation in your own notation and explain, in plain language, what Top-$k$ does and why sparsity is the architecture's key property. *What this tests: whether you understand the mechanism, not just the name.*

2. *(Recall — tests the two distinctions)* Name the two structural properties that separate genuine MoE from stacked ensembles. For each, state in one sentence what capability it enables that stacking lacks. *What this tests: whether you can state the distinctions precisely rather than gesturing at "multiple models."*

3. *(Recall — tests the load-balancing tension)* Explain the expert-collapse problem and describe one mechanism the field uses to counter it. Then state, in one sentence, how that counter-mechanism creates a tension with the goal of specialization. *What this tests: whether you understand that MoE's central problem is unsolved, not engineered away.*

**Application**

4. *(Apply — runs the six questions)* Find a real, public vendor description of an "AI-powered" or "MoE" HCP-targeting platform. Run all six buyer-verification questions, marking each answer as confirmed, denied, or undisclosed. Write a two-sentence verdict in the register: "not MoE / not obviously better than a tuned ensemble — demand a benchmark" or "genuine MoE — verify the benchmark." *What this tests: whether you can operationalize the audit on actual vendor material.*

5. *(Apply — the tabular exception)* Explain, to a data-science lead who is proud of their stacked ensemble, why a well-tuned gradient-boosted model is likely the right baseline — not a downgrade — for an NPI propensity task. Your explanation should reference the Grinsztajn et al. result and the specific properties of tabular prescriber data that favor tree-based methods. *What this tests: whether you can make the tabular-exception argument without dismissing the vendor's work.*

6. *(Apply — the fast screen)* Apply the three-criterion fast screen (token-level routing? shared output space? jointly trained?) to the opening-case platform. State your verdict for each criterion and give the overall result. Then explain why two "yes" answers and one "no" would not be enough to call the system genuine MoE. *What this tests: whether you understand the fast screen as a sufficient condition for "not MoE," not a scoring rubric.*

**Synthesis**

7. *(Synthesize — MoE + evidence framework)* Connect the MoE audit to Chapter 4's five-question rubric. A vendor claims "our MoE engine delivers 22% script lift." Map this single claim onto both frameworks: the six buyer questions (is it genuine MoE?) and the five-question rubric (is the lift claim evidenced?). Write a unified one-paragraph verdict that addresses both the architecture label and the effectiveness claim. *What this tests: whether you can apply two audit frameworks simultaneously without conflating them.*

8. *(Synthesize — compliance consequence)* The chapter notes that a genuine MoE routing model is harder to explain to an MLR reviewer than an interpretable tree ensemble. Build the argument: what specifically would a reviewer need to understand about a MoE targeting decision to certify that it does not violate fair-balance or suppression rules, and why is that harder to produce for a MoE than for a tree? *What this tests: whether you can connect architectural opacity to a specific compliance cost.*

**Challenge**

9. *(Challenge — design a benchmark)* Design a study that would produce credible evidence that a genuine MoE system outperforms a tuned XGBoost ensemble on an NPI propensity task. Specify: the dataset, the evaluation metrics (and why headline AUC is insufficient), the randomization or holdout structure, and the primary threat to validity you would need to address. You do not need to run it — specify it precisely enough that a data-science team could. *What this tests: whether you can articulate the evidence standard the market currently lacks and understand why producing it is hard.*

---

## Prompts

### Figure 7.1 — Sparse activation in a MoE layer

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 from the cdnjs CDN) rendering a left-to-right process diagram of one Mixture-of-Experts layer. Marks: one input node `x` → a `gating network` box → a fan of dashed hairline arrows to a vertical column of eight stacked expert boxes, of which exactly two are highlighted (filled ink) as active and connected by solid arrows; the two active experts converge into a `weighted sum` node → output `y`. Below, a magnitude band of two horizontal bars sharing a zero baseline: a long red bar "capacity scales with N (total parameters)" and a short ink bar "compute scales with k (active per pass)". Channels: fill encodes active vs inactive; bar length encodes magnitude. No sorting; bars zero-based. Annotate that eight experts and top-2 are an illustrative count, not a claimed configuration. viewBox 700×420. Deliverable: one HTML file, inline CSS, var(--color-*) tokens, light/dark theming, accessible title/desc, hover/focus tooltips.

### Figure 7.2 — What MoE routes on: token type versus a feature vector

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 CDN) rendering a two-panel contrast diagram. Left panel: a short token sequence (verb, punctuation, noun) → a `gate` → distinct solid routes to two color-distinct expert boxes, labeling this routing on token type. Right panel: a tabular NPI feature vector (Rx, geo, pay, spec cells in one row) → a `gate` → a red "?" mark over a dashed route into two dashed "expert ?" boxes, labeling "no syntactic structure to route on". Channels: solid vs dashed strokes encode established vs uncertain routing; color separates the two sequence experts. No axes. Annotate that "physician archetypes" via routing is an open question, probably near-redundancy, and token labels are illustrative. viewBox 700×420. Deliverable: one HTML file, inline CSS, var(--color-*), light/dark theming, accessible title/desc, hover/focus tooltips.

### Figure 7.3 — The six buyer questions and the fast screen

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 CDN) rendering a vertical six-row checklist plus a boxed inset. Each row pairs an audit question (left cell) with the opening-case platform's answer (right cell); rows for questions 2, 3, and 4 are outlined red to mark the answers that point to stacking. Below the checklist a verdict line reads "stacking, not MoE — and no benchmark," with a note that the label is wrong but platform quality is a separate question. The inset box lists the three-criterion fast screen (token-level routing? shared trunk and output space? jointly trained?) and the rule "three no answers → stacking". Channels: red outline encodes the disqualifying answers. No sorting beyond question order; no axes. viewBox 700×480. Deliverable: one HTML file, inline CSS, var(--color-*), light/dark theming, accessible title/desc, hover/focus tooltips.

---

## Chapter 7 Exercises: Mixture of Experts and Related Routing Models

**Project:** One Drug, End to End
**This chapter adds:** A six-buyer-question verdict on whether a vendor's "Mixture of Experts" engine would actually improve targeting for your drug — or is stacking in a transformer-era costume.

We continue with **Jardiance (empagliflozin)** — branded SGLT2 inhibitor, branded rivals Farxiga and Invokana, generic alternatives metformin and sulfonylureas. In Chapter 6 you built the calibrated propensity baseline. Now a vendor wants to sell you an "adaptive MoE targeting engine" for Jardiance. This chapter's piece: run the audit and deliver the verdict.

### Exercise 1 — When to Use AI

1. Paste a vendor's public "MoE-powered" platform description and ask the LLM to extract, verbatim, what the text states for each of the six buyer questions — component models, joint vs. independent training, shared output space, routing mechanism, what "MoE" denotes, and any independent benchmark — marking anything not stated as "undisclosed." *Why AI works here:* structured extraction from a fixed text — a task type where the source is in front of you and the output is checkable line by line.
2. Ask the LLM to explain the math of sparse top-k gating in plain language before you read Shazeer et al. *Why AI works here:* concept exposition of a well-documented, stable idea — verifiable against the primary paper.

**The tell:** you can independently evaluate the output — every extracted answer is checkable against the vendor's exact words, and every concept against the primary source.

### Exercise 2 — When NOT to Use AI

1. Do not let the LLM render the verdict — "this is genuine MoE" or "this is stacking" — as your conclusion. That verdict turns on architectural facts (was it jointly trained? is there a shared output space?) the public text usually omits, and on whether MoE's advantages even apply to tabular Jardiance prediction. *Why AI fails here:* hallucination — the model will fill the "undisclosed" gaps with plausible inference, manufacturing an architecture the vendor never described.
2. Do not let the LLM certify the vendor's benchmark claim ("22% better than gradient boosting"). Whether that beats *your* Chapter 6 Jardiance baseline requires a head-to-head on the same task with the same split discipline. *Why AI fails here:* ground-truth — there is no benchmark in the text for the model to verify against, so any endorsement is fabricated.

**The tell:** if the LLM's "it's stacking" is your *reason*, you have laundered an inference into a fact; if it is a *tool* output you then confirm against the vendor's actual disclosures and your own baseline, you are fine. **Series connection:** this is a **T5** judgment — MoE-relabel laundering. A vendor relabels stacking as MoE; an uncritical AI relabels the AI's guess as the architecture. Both launder. The human owns the architecture call and the benchmark demand.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** a filled six-buyer-question audit plus a two-sentence verdict on a real vendor's "MoE" targeting claim for a Jardiance-style brand.

**Tool:** Claude, run as a **Claude Project**. Persistent drug-context helps because the verdict references your Chapter 6 Jardiance baseline as the bar the vendor must beat — keeping the baseline definition resident in the Project means the audit stays anchored to the same case rather than a generic one.

**The Prompt:**

```
You are auditing a vendor's AI targeting claim for a running case study on one
branded drug carried end to end: Jardiance (empagliflozin), a branded SGLT2
inhibitor with branded competitors (Farxiga, Invokana) and generic alternatives
(metformin, sulfonylureas). In Chapter 6 of this case I built a calibrated,
out-of-time-validated gradient-boosted tree baseline for Jardiance propensity on
public Open Payments + Part D data. That baseline AUC is the bar.

Here is the vendor's public description of an "adaptive Mixture-of-Experts" HCP
targeting engine: [PASTE VENDOR TEXT]

Using ONLY what the text states, answer the six buyer questions. Write "undisclosed"
for anything not stated — do not infer:
1. What are the component models or algorithms?
2. Were they trained jointly or independently?
3. Do they share an input-output interface, or does an aggregator translate formats?
4. Is routing learned jointly with the models, or assigned separately?
5. Does "MoE" describe a routing layer within ONE model, or a meta-architecture
   across SEPARATE models?
6. What independent benchmark compares performance against a tuned gradient-boosted
   ensemble on the SAME task?

Then run the three-criterion fast screen (token-level routing? shared trunk and
output space? jointly trained?). Then write a two-sentence verdict in one of two
registers: "not MoE / not obviously better than a tuned ensemble — demand a
benchmark against my Chapter 6 Jardiance baseline" OR "genuine MoE — verify the
benchmark." Flag every claim of effectiveness as [verify].

ADAPTATION: replace Jardiance and its class with your own drug; the six questions
and the screen are drug-agnostic. In ChatGPT or Gemini, paste your Chapter 6
baseline summary at the top so the verdict stays anchored.
```

**What this produces:** a completed audit instrument with a defensible verdict that names exactly which disclosures are missing — the artifact you hand a procurement committee.

**How to adapt:** swap the drug and paste your own vendor text; in ChatGPT/Gemini, re-supply the Chapter 6 baseline each session; in a Claude Project, store the baseline summary as Project knowledge.

**Connection to previous chapters:** the verdict's teeth come from Chapter 6 — without your honest baseline AUC, buyer question six has no bar to point at, and the vendor's number floats free exactly as the Chapter 1 and 5 vendor claims did.

**Preview of next chapter:** even a genuine MoE that ranks Jardiance prescribers well still answers a *prediction* question; Chapter 8 shows why ranking the likely is the wrong target and uplift is the right one.

### Exercise 4 — CLI Exercise

**What you're building:** the literal artifact behind buyer question six — a tuned, calibrated gradient-boosted baseline on a Jardiance-shaped tabular dataset, with the AUC and Brier score any "MoE" claim must beat.

**Tool:** Claude Code (or Cowork) — it can scaffold the notebook, train the model, and emit the metrics in one loop. **Skill level:** intermediate (comfortable with a Python ML notebook).

**Setup:**
- [ ] A public tabular dataset shaped like prescriber data (rows = entities, columns = behavioral + demographic features, binary target) — or your Chapter 6 Jardiance extract.
- [ ] `xgboost` or `lightgbm` plus `scikit-learn` installed.
- [ ] An `./outputs/` folder; the source data read-only.

**The Task:**

```
Read ONLY the dataset in ./data/ (do not modify it). Train a tuned gradient-boosted
tree baseline (XGBoost or LightGBM) on a binary target, using an out-of-time or
grouped split, NOT a random shuffle. Calibrate the probabilities (isotonic or
Platt) on a held-out fold. Report AUC and Brier score.

Write the metrics and the split description to ./outputs/moe-baseline-bar.txt.
This number is the bar any vendor "MoE" claim must beat. Do not write anywhere
else. Stop when the file exists, then print it so I can verify the numbers.
```

**Expected output:** a single text file stating the baseline AUC, Brier score, and the split used — the empirical answer to "better than what?"

**What to inspect:** is the split out-of-time, not random? Is the Brier score reported alongside AUC (calibration, not just ranking)? Is the source data untouched?

**If it goes wrong:** if Claude Code uses a random split (failure), restate the out-of-time requirement and re-run; if it reports AUC without calibration, ask it to add the isotonic step and the Brier score.

**CLAUDE.md note:** add `Baselines must use an out-of-time split and report a calibration metric (Brier), never AUC alone.`

### Exercise 5 — AI Validation Exercise

**What you're validating:** the AI's six-question audit output from Ex3 — specifically whether it honored "undisclosed" or quietly inferred an architecture, and whether its verdict is laundered guesswork.

**Validation type:** inference-discipline audit of a generated classification. **Risk level:** high — because a false "genuine MoE" verdict justifies real spend on an engine that may be no better than your Chapter 6 baseline, and the error hides inside a fluent, confident teardown.

**Setup:** use your Ex3 audit. If you want a specific failure to practice on, ask the AI to audit a deliberately vague vendor blurb and watch whether it invents answers for the undisclosed questions.

**The Validation Task:**

```
Validation Checklist — Chapter 7 (Jardiance MoE vendor audit)

Mark each Pass / Fail / Cannot-determine:
- Correctness: Does each of the six answers cite only words actually in the vendor
  text?
- Completeness: Are all six buyer questions AND the three-criterion fast screen
  answered?
- Scope: Are genuinely unstated items marked "undisclosed" rather than inferred?
- MoE-vs-stacking criterion: Does the verdict rest on the two real distinctions
  (shared output space, joint end-to-end training), not just "it has multiple
  models"?
- Benchmark criterion: Does the verdict explicitly demand a head-to-head against
  my Chapter 6 Jardiance baseline?
- Failure-mode check: Look specifically for MoE-relabel laundering — the AI
  treating an inferred architecture as disclosed fact (fluent-but-wrong) — and for
  missing ground truth (a benchmark endorsed with no benchmark in the text).
```

**What to do with findings:** all Pass — the verdict is sound; forward it with the benchmark demand attached. One Fail — correct the inferred answer to "undisclosed" and re-issue. Multiple Fails — discard the AI verdict and re-run the audit yourself from the vendor text, treating the original as a laundering exhibit.

**AI Use Disclosure prompt:** *Write two sentences naming exactly what the AI did and the one judgment it could not make. Example: "I used Claude to extract the vendor's stated answers to the six buyer questions for the Jardiance MoE pitch; I decided whether it was genuine MoE or relabeled stacking, and whether it could beat my baseline, because both require the two architectural distinctions and a benchmark the public text never supplied."* (Mandatory.)

**Series connection:** the failure mode is **MoE-relabel laundering** at tier **T5** — relabeling that survives only because no one demanded the baseline comparison the rest of the series is built to provide.
