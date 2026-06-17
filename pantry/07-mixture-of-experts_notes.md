# Chapter 7 — Mixture of Experts and Related Routing Models · Research Notes

> Gathering notes only (no chapter prose). Format A–G.
> Chapter spine: learn genuine sparse-gated MoE precisely, and learn to tell it apart from ensemble
> *stacking* sold under a transformer-era label. Sparse gating (Shazeer 2017), Switch, Mixtral 8x7B,
> DeepSeek-V3; routing, load balancing, expert collapse; output standardization + joint training as
> the *real* architectural difference; the tabular exception; the buyer verification questions.
> PRIMARY SOURCE — mostly a RESTRUCTURE of `pantry/moe-vs-ensemble-synthesis.md` §§1,2,3,5,7,8,9.
> Currency UPDATED via web 2026-06-16 (Llama 4, Qwen3, GPT-OSS, GLM-5; shared experts now optional).

---

## A. Conceptual foundations

**The formal MoE layer.** Given N expert networks E_1…E_N and a gating function G:
  y = Σ_i G(x)_i · E_i(x),  with  G(x) = Softmax(Top-k(H(x))),  H(x) = x·W_gate + ε
(ε = Gaussian noise for load balancing, Shazeer 2017). Top-k zeros all but the k largest before the
softmax → **sparse** activation. [Source: synthesis §2.] The decisive structural fact: **all E_i share
identical input AND output dimensionality**, so the weighted sum is a clean convex combination *in a
shared vector space*. If experts had different output shapes you couldn't add them — you'd need a
translation layer. This standardization is the crux of the whole chapter.

**The two things that genuinely distinguish MoE from stacking** (the chapter's load-bearing claim —
synthesis §5):
1. **Output standardization** → a mathematically clean weighted sum, *and* end-to-end
   differentiability. The combination is differentiable w.r.t. both gating weights and expert
   parameters.
2. **Joint / end-to-end training (co-adaptation)** → gating and experts train together via one
   backprop pass. The router learns to route to experts that do well; experts learn to handle what
   they're routed. Specialization is *emergent* (a consequence of routing), not engineered. In
   stacking, base models are frozen *before* the meta-learner sees them — no co-adaptation, no joint
   optimization. "You're combining separately trained artifacts and hoping the combination beats the
   parts." [Source: synthesis §5.]

**Sparsity = the 2017 unlock.** Shazeer et al., "Outrageously Large Neural Networks: The Sparsely-Gated
Mixture-of-Experts Layer," 2017 (with Hinton & Dean): scaled MoE to a 137B-param LSTM by activating
only top-k experts per token → capacity grows with total params while compute/forward-pass stays ~flat.
Origin: Jacobs, Jordan, Nowlan & Hinton 1991, "Adaptive Mixtures of Local Experts" (vowel
discrimination); Jordan & Jacobs 1994 (Hierarchical MoE). ~26-year dormancy until compute made the
advantage demonstrable. [Source: synthesis §1.]

**The load-balancing ↔ specialization tension (the central unsolved problem).** Without intervention,
routing **collapses**: a few experts get most early routing, most gradient, improve fastest, attract
more routing — "you pay for 256 experts and use 3." Fixes: (a) auxiliary load-balancing loss (Switch) —
but its interference gradients can hurt quality; (b) noisy top-k gating (Shazeer 2017); (c) **auxiliary-
loss-free balancing via dynamic bias terms** (DeepSeek) — best current practice. The deep tension:
load balancing pushes routing toward *uniform*, but specialization requires *non-uniform* routing —
the two objectives conflict, and load-balanced routing causes overlapping expert token-distributions
that *reduce* the specialization the architecture exists to produce. [Source: synthesis §2.]

**What experts actually specialize in (empirically surprising).** Not "one expert does math, one does
code." Mixtral analysis: experts specialize in **syntactic/computational patterns (token type), not
semantic domains** — a punctuation token routes differently from a verb regardless of topic. Some
experts converge to >99% similarity in some trained models (the relocated correlation problem). [Source:
synthesis §3.] *Pharma implication:* on tabular NPI vectors there is no token sequence and no
syntactic structure — so the routing-specialization mechanism has no natural analogue. "It's unclear
what 'specialization' would mean for an expert routing on NPI feature vectors." [Source: synthesis §9.]

---

## B. Domain examples + a failure case

**Genuine MoE landmarks (the dated examples — stable principle, refresh the model names):**
- **Switch Transformer** (Fedus, Zoph, Shazeer 2022): top-1 routing; simpler routing is more stable;
  scaled toward trillion-param. [synthesis §1.]
- **Mixtral 8x7B** (Mistral, 2023): 8 experts/layer, top-2 routing; ~47B total / ~13B active per token;
  ≈ Llama 2 70B quality at ~1/5 active params. First major open-source MoE success. [synthesis §1.]
- **DeepSeek-V3** (2024): 671B total / 37B active (~5.5%); **256 fine-grained experts**, 8 routed/token;
  **auxiliary-loss-free** balancing; **shared-expert** mechanism (1–2 always-active experts for
  "common knowledge"). [synthesis §1, §7.]
- **2025 currency [VERIFIED via web 2026-06-16]:** MoE is now standard across frontier open models —
  **Llama 4** (Maverick/Scout: 1 shared + 1 routed expert, top-1 routing — sparser than DeepSeek),
  **Qwen3** (e.g. Qwen3-235B-A22B; *no* shared expert), **GPT-OSS** (20B/120B; no shared expert),
  **GLM-5**, DeepSeek-R1-0528 (1 shared + 8 of 256 routed). Key 2025 trend lines:
  (i) fine-grained experts + high expert counts are now the norm; (ii) **the shared expert is now
  *optional*** — DeepSeek & Llama 4 use it; Qwen3, OLMoE, GPT-OSS skip it; (iii) "no single best MoE
  design, only trade-offs." Sources: friendli.ai MoE-2025 comparison; Raschka LLMs-from-scratch MoE;
  Chris Hughes "Beyond Vanilla MoE" (Medium). [Treat all model names as dated examples per TIKTOC
  aging-risk: High.]

**The tabular exception (the chapter's pharma payload — synthesis §6, §9).** MoE's advantages are
concentrated at scale, in sequential/token data, and in heterogeneous multi-task settings. For
*structured tabular* prediction (NPI propensity, behavioral prediction, bid optimization on claims
data) the empirical winner is a tuned gradient-boosted tree ensemble (Grinsztajn NeurIPS 2022, Ch 6).
On this problem type, the ensemble is **not a simplified substitute for MoE — it is likely the
genuinely superior architecture.** The MoE label in pharma ad-tech reflects *scale ambition*, not
deployment reality.

**Failure case (TIKTOC opening) — the relabeled "MoE targeting engine."** A platform's "adaptive
Mixture-of-Experts" turns out to be: XGBoost (propensity) + a separate bid model + a rules engine,
combined by a learned aggregator. This is **legitimate, effective ML — and it is stacking, not MoE.**
It has none of MoE's defining properties: no token-level routing, no sparse activation, no shared
output space, no joint end-to-end training, no sub-linear compute scaling. Claiming "MoE" implies
scaling + joint-optimization capabilities the system doesn't have — and on tabular data those
properties are irrelevant anyway, so the relabel buys marketing gloss, not performance. [Source:
synthesis §8.] *Honesty balance for the partner:* the verdict is "not MoE, and not obviously better
than a tuned ensemble" — not "fraudulent." Stacking is a fine architecture; the issue is the label.

---

## C. Connections / dependencies

- **Depends on Ch 6** (TIKTOC prereq map): you cannot evaluate a routing model without the tuned-
  ensemble baseline. Buyer question #6 = "performance vs. well-tuned XGBoost on the same task."
- **Contrasts ensemble stacking (Ch 6 §stacking)** — the entire chapter is "MoE vs. relabeled
  stacking." The bias-variance-covariance "manufactured diversity" limit (Ch 6) is what MoE's
  *emergent* specialization claims to escape — and partly does, partly doesn't (>99% expert similarity).
- **Feeds Ch 13 Track C**: "algorithmic audit of public 'MoE' platform claims" and "ensemble-vs-genuine-
  MoE benchmark on NPI propensity" — the buyer questions (A/E) operationalized as a publishable
  technology-audit study (TIKTOC research finding for Ch 7).
- **Feeds Ch 4** (vendor-claim audit / midterm) and Ch 11 (Evidence Ladder) — the six buyer questions
  are an audit instrument.
- **Bridge (TIKTOC):** "architecture aside — predicting a prescriber is not changing one" → Ch 8.

---

## D. Current state (settled / contested / key refs / last-3-yr)

**Settled:**
- The formal sparse-gated MoE definition (Shazeer 2017) and the joint-training / output-standardization
  distinction from stacking — settled.
- Load-balancing ↔ specialization tension; expert-collapse risk — settled, actively researched.
- For tabular prediction, tree ensembles ≥ MoE (Grinsztajn NeurIPS 2022) — settled (Ch 6).
- MoE is now standard in frontier LLMs (2024–2025) — settled. [VERIFIED via web.]

**Contested / open (synthesis §9):**
- Is MoE's correlation/diversity advantage empirically robust? Mixed — >99% expert similarity
  documented; load balancing erodes specialization.
- Does joint training beat stacking *for tabular* at commercial scale? Less obvious; stacking is
  competitive and far simpler to build/debug/maintain.
- What does "specialization" even mean for tabular routing? Possibly nothing useful.
- Is output standardization decisive in practice? Strongest at large scale / sequence data; magnitude
  in commercial structured prediction not empirically established.

**Key references:**
- Shazeer et al. 2017 (sparsely-gated MoE); Jacobs/Jordan/Nowlan/Hinton 1991; Jordan & Jacobs 1994;
  Fedus/Zoph/Shazeer 2022 (Switch); Mixtral 8x7B (Jiang et al. 2024); DeepSeek-V3 tech report 2024.
- Grinsztajn et al. NeurIPS 2022 (tabular). 
- 2025: Llama 4, Qwen3, GPT-OSS, GLM-5 model/tech reports. [VERIFIED names via web; add formal cites.]
- (Reuse) `pantry/moe-vs-ensemble-synthesis.md` — in-pantry primary source.

**The six buyer verification questions (from synthesis §8 — the reusable artifact, verbatim intent):**
1. What are the component models (algorithms, training data)?
2. Trained jointly or independently?
3. Shared I/O interfaces, or does the aggregator translate formats?
4. Routing: learned + jointly trained, or rule-based / separately trained assignment?
5. Does "MoE" denote a meta-architecture *across separate models*, or a sub-network routing layer
   *within one model*?
6. Performance vs. a well-tuned XGBoost ensemble on the same task, on what independent benchmark?
*Three-criteria quick test (TIKTOC): token-level routing? shared trunk/output space? jointly trained?
Three "no"s = it's stacking.*

**Last-3-yr:** rapid model turnover (Mixtral→DeepSeek-V3→Llama4/Qwen3/GPT-OSS, 2023→2025); shared-
expert design went from novelty to optional; auxiliary-loss-free balancing became best practice. None
of this changes the *tabular* verdict. Aging risk: HIGH for model names — write "stable principle +
dated example."

---

## E. Teaching considerations

- **TIKTOC Hard Chapter warning:** "must stay honest without becoming an ML-theory course for a
  non-engineer-leaning reader." Strategy: teach MoE *to the depth needed to run the six buyer
  questions* — formal layer + the two real distinctions (standardization, joint training) + the
  tabular exception. Skip routing-math derivations; route depth to Further Reading.
- **Lead with the relabel failure case** (failure-first) — the reader's job is to detect, not to build,
  MoE. The chapter is an *audit* skill, not an implementation skill.
- **The single most important sentence to land:** genuine MoE's advantages (sub-linear scaling, joint
  optimization, token-level routing) are *real but irrelevant to tabular NPI prediction* — so a "MoE"
  pharma platform is either mislabeled stacking or applying a scale-regime tool to a problem that
  doesn't have that regime. Either way, demand the Ch 6 baseline comparison.
- **Keep the partner-relationship balance:** verdict is "not MoE / not obviously better than a tuned
  ensemble," not "lying." Stacking is legitimate. This protects credibility and the collaboration
  (TIKTOC Risk 2).
- **Use dated examples deliberately** and say so — model the aging-risk discipline for the reader.
- **Bridge (TIKTOC):** → Ch 8 (prediction ≠ intervention).
- **Assessment:** lab exercise — claim teardown (apply the six buyer questions to a public "MoE"
  platform claim and reach a verdict). Part B: same on a claim relevant to the Fellow's thread.

---

## F. Library files (copied to pantry/, prefixed `_lib_`)

- `_lib_ai-why-machines-learn-the-elegant-math-behind-modern-ai.md` *(in MD library; copy if used)* —
  accessible math for routing/softmax/gating if the chapter needs an intuition pump. [NOTE: not yet
  copied — flag below.]
- `_lib_finance-advances-in-financial-machine-learning.md` — ensemble/stacking discipline; useful for
  contrasting genuine joint training vs. post-hoc combination (the §5 distinction).
- `_lib_ai-prediction-machines-the-simple-economics-of-artificial-intelligence.md` — keeps the chapter
  anchored to "what decision does this architecture improve?" (prevents architecture-for-its-own-sake).
- (Reuse) `pantry/moe-vs-ensemble-synthesis.md` — the primary, very thorough in-pantry source; this
  notes file is a restructure + 2025 currency update of it.

---

## G. Gaps & flags

- [FLAG — currency, RESOLVED] Synthesis stopped at DeepSeek-V3 (2024). UPDATED 2026-06-16: Llama 4
  (shared+routed, top-1), Qwen3 (no shared expert), GPT-OSS, GLM-5; shared-expert now *optional*; fine-
  grained high-count experts the norm. Verify model-config specifics (expert counts, top-k) against
  primary tech reports in ACCURACY pass — secondary sources (friendli.ai, Raschka, Hughes) used here.
- [VERIFY] Add formal citations: Shazeer 2017 arXiv, Switch (Fedus 2022 JMLR), Mixtral (Jiang 2024
  arXiv), DeepSeek-V3 report, Llama 4 / Qwen3 / GPT-OSS reports.
- [FLAG] `_lib_ai-why-machines-learn…` referenced but NOT yet copied to pantry — copy it if the chapter
  uses it, or drop the reference.
- [GAP] No public audit exists of pharma "MoE" platform claims against the three criteria — that's the
  TIKTOC Ch 13 Track C study the chapter sets up. Don't fabricate platform internals; the buyer
  questions are the instrument precisely *because* internals are undisclosed.
- [BALANCE] Maintain "not MoE ≠ fraud" framing throughout (partner relationship, TIKTOC Risk 2).
