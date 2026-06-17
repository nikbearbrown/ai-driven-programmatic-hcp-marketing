# Chapter 6 — Ensembles and the Tabular-Data Advantage · Research Notes

> Gathering notes only (no chapter prose). Format A–G.
> Chapter spine: gradient-boosted tree ensembles are the practical baseline for NPI propensity and
> structured commercial prediction — *the baseline any fancier "AI platform"/"MoE" claim must beat.*
> Bagging/boosting/stacking; XGBoost/LightGBM/CatBoost; why trees are SOTA on medium tabular data
> (Grinsztajn et al., NeurIPS 2022); propensity scoring, calibration, leakage, claims-lag traps.
> PRIMARY SOURCE — this is mostly a RESTRUCTURE of `pantry/moe-vs-ensemble-synthesis.md` §§4,6,8
> into notes format + pharma-specific traps. Currency verified 2026-06-16.

---

## A. Conceptual foundations

**The three ensemble paradigms (the vocabulary):**
- **Bagging** (Breiman 1996): train many independent models on bootstrap samples; average/vote.
  Reduces **variance**. Random Forest = bagging + random feature subsets per split (extra
  decorrelation). [Source: synthesis §4.]
- **Boosting** (AdaBoost: Freund & Schapire 1997; Gradient Boosting: Friedman 2001): train models
  *sequentially*, each correcting the prior's errors. Reduces **bias and variance**; more powerful but
  more sensitive to noise/outliers. **XGBoost, LightGBM, CatBoost** are the dominant modern
  implementations — the practical default for tabular work. [Source: synthesis §4.]
- **Stacking** (Wolpert 1992): train diverse base models, then a meta-learner on their out-of-fold
  predictions; the meta-learner learns which base model to trust where. *Important for Ch 7:* this is
  what most "MoE" pharma platforms actually are. [Source: synthesis §4, §8.]

**Why diversity is mathematically load-bearing (the bias–variance–covariance floor).** Ensemble error
decomposes as bias² + (1/N)·var + (1 − 1/N)·covar. As N→∞ the variance term vanishes but the
**covariance term sets a floor**: perfectly correlated models gain nothing from more members. So
diversity is not aesthetic — it is the only lever once N is large. [Source: synthesis §4.]
*The catch:* ensemble diversity is **manufactured** (different seeds/data/features/algorithms) on the
*same data distribution* — models learn the same regularities and share blind spots. This is the exact
limitation Ch 7's MoE claims to escape via *emergent* (routing-induced) specialization. Foreshadow,
don't resolve, here.

**Why trees dominate tabular data — the SOTA claim.** Grinsztajn, Oyallon & Varoquaux, "Why do
tree-based models still outperform deep learning on typical tabular data?" **NeurIPS 2022**: benchmark
of deep-learning vs. tree methods across **45 tabular datasets**; **tree-based models remain SOTA on
medium-sized tabular data (~10K samples)** even ignoring their speed advantage. Three identified
reasons [Source: synthesis §6 — quotes the paper]:
1. Trees are **natively robust to uninformative features** (real tabular data is full of them).
2. Neural nets struggle to fit the **irregular / non-smooth target functions** tabular data often has;
   tree splits handle them natively.
3. The best tabular methods **are ensemble methods, and the weak learner is a decision tree.** Paper's
   own conclusion: "the best methods on tabular data… are ensemble methods."
**Pharma relevance:** NPI-level propensity is a *structured tabular* problem — physician features,
prescribing history, Open-Payments history, demographics, behavioral signals. This is precisely the
regime where gradient-boosted trees beat neural architectures (including MoE). So the ensemble baseline
isn't a placeholder for something better — on this problem it may *be* the best architecture.
[Source: synthesis §6.]

---

## B. Domain examples + a failure case

**Worked example (the chapter's opening, per TIKTOC):** an XGBoost NPI-propensity model as the
"unglamorous baseline that beats most 'AI platform' claims." Pipeline: claims + Open-Payments + behavioral
features → gradient-boosted trees → calibrated propensity score → ranked target list. The Fellow builds
this on public data (Open Payments + Medicare Part D) and uses it as the bar every vendor claim and
every "MoE" upgrade (Ch 7) must clear.

**Honest evaluation (the gradeable craft):**
- **Discrimination**: AUC/AUPRC — but AUC alone is insufficient for a *targeting/budgeting* decision.
- **Calibration**: do predicted probabilities match observed rates? (Reliability curves, Brier score.)
  Load-bearing because downstream bid/spend decisions use the probability as a *quantity*, and because
  uplift meta-learners (Ch 8) use these as base learners — miscalibration propagates.
- **Out-of-time validation**: split by time, not random rows — pharma data has temporal drift; random
  CV leaks the future.
- **Subgroup robustness**: by specialty/decile/geography — a model strong on average can be useless on
  the segment that matters.

**Failure case — the leakage / claims-lag trap (the pharma-specific landmine).** Claims data arrives
with a lag (weeks to months) and is revised. Two failure modes:
1. **Target leakage**: a feature that encodes the outcome (e.g., a recent-fill flag that postdates the
   prediction point, or a "treated" indicator). The model posts a spectacular offline AUC and collapses
   in production. The fix: define a strict as-of prediction timestamp and only use features knowable
   *before* it.
2. **Claims-lag illusion of lift**: because fills are recorded late, a physician's "post-exposure"
   prescribing may include scripts written *before* exposure but recorded after — inflating apparent
   response. This directly feeds the Ch 5 attribution problem and the Ch 8 incrementality problem.
This is the failure-first opening discipline the book requires: a baseline that looks brilliant offline
and is actually leaking.

---

## C. Connections / dependencies

- **Depends on Ch 5** (the evidence frame) — TIKTOC prereq map: Ch 6 depends on Ch 5. The baseline is
  the operationalization of "what would a credible claim have to beat?"
- **Required by Ch 7**: you cannot judge whether "MoE" is a real upgrade without the tuned-ensemble
  baseline to compare against. Ch 7's buyer question #6 is literally "what is the performance
  difference vs. a well-tuned XGBoost ensemble on the same task?"
- **Required by Ch 8**: uplift meta-learners (S/T/X/R-learners) use gradient-boosted trees as their
  base learners; calibration here is the prerequisite for honest CATE there.
- **Connects to Ch 3** (the propensity feature vector) — the substrate this chapter models.
- **Feeds Ch 13 Track C** (ensemble-vs-genuine-MoE benchmark on NPI propensity) — the worked portfolio
  example in TIKTOC Week 13 *is* this baseline vs. a routed model.

---

## D. Current state (settled / contested / key refs / last-3-yr)

**Settled:**
- Gradient-boosted trees (XGBoost/LightGBM/CatBoost) are the practical SOTA for medium tabular data
  (Grinsztajn NeurIPS 2022) — strong, recent, peer-reviewed consensus.
- Bias–variance–covariance decomposition; diversity floor — textbook-settled.
- Bagging/boosting/stacking definitions and originating papers — settled.

**Contested / evolving:**
- *Deep learning is catching up on tabular*: newer tabular DL (FT-Transformer, TabPFN / TabPFN v2,
  SAINT) narrows the gap on some benchmarks, especially small-N or where pretraining helps. [VERIFY
  2026 state before publication — TabPFN v2 (2024/25) is the live challenger to the "trees always win"
  claim.] The honest framing: trees remain the *default and the baseline*; DL tabular is an active
  frontier, not yet a reason to skip the ensemble baseline. [FLAG — synthesis predates the strongest
  TabPFN results; add a hedge.]
- Whether stacking ≈ MoE for tabular (the Ch 7 question) — synthesis argues stacking is competitive and
  far simpler to build/debug/maintain at commercial scale.

**Key references:**
- Grinsztajn, Oyallon, Varoquaux. "Why do tree-based models still outperform deep learning on typical
  tabular data?" NeurIPS 2022 (Datasets & Benchmarks). [VERIFIED via synthesis; confirm exact title.]
- Breiman 1996 (bagging) & 2001 (random forests); Freund & Schapire 1997 (AdaBoost); Friedman 2001
  (gradient boosting); Wolpert 1992 (stacking); Chen & Guestrin 2016 (XGBoost). [Standard; add full
  cites.]
- (Reuse) `pantry/moe-vs-ensemble-synthesis.md` §§4, 6, 8 — the in-pantry primary source.

**Last-3-yr:** XGBoost/LightGBM/CatBoost remain industry default; the live development is tabular DL
(TabPFN v2, 2024/25) — track for the aging-risk review, but it does not change the chapter's "build the
ensemble baseline first" thesis.

---

## E. Teaching considerations

- **Frame the whole chapter as building a *baseline*, not a model** — the rhetorical move that makes
  Ch 7's MoE skepticism land. The Fellow's emotional takeaway: "the boring thing is hard to beat."
- **Lead with the leakage/claims-lag failure** (failure-first per book template) — it's the most
  transferable practitioner lesson and it threads into Ch 5/8.
- **Calibration deserves equal billing with AUC** — non-obvious to a reader trained on classification
  accuracy; it's what makes the score usable for spend decisions and for Ch 8 uplift.
- **Keep math bounded**: the bias–variance–covariance formula is worth showing (it justifies diversity);
  do not derive boosting's functional-gradient view. Reader is data-capable, not an ML theorist.
- **Honesty hedge to include:** acknowledge tabular DL is improving (TabPFN) so the book doesn't overstate
  "trees always win" and age badly — the claim is "trees are the right *baseline*," which is robust.
- **Bridge (TIKTOC):** "vendors say 'MoE' — real upgrade or relabel?" → Ch 7.
- **Assessment:** lab exercise — build/eval a baseline on public data (Open Payments + Part D). Part B:
  specify an ensemble baseline + honest evaluation for the Fellow's own propensity task.

---

## F. Library files (copied to pantry/, prefixed `_lib_`)

- `_lib_finance-advances-in-financial-machine-learning.md` — **most relevant**: López de Prado on
  ensemble methods, bagging/boosting in finance, and especially **leakage, cross-validation under
  temporal structure, and backtest overfitting** — maps directly onto the pharma claims-lag/leakage
  failure case (B) and out-of-time validation (B). 15 ensemble hits.
- `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md` — uses gradient boosting + random/causal
  forests as ML engines for nuisance estimation; bridges Ch 6 ensembles → Ch 8 meta-learners (86
  ensemble/boosting hits).
- `_lib_ai-prediction-machines-the-simple-economics-of-artificial-intelligence.md` — the
  prediction-vs-decision distinction (Agrawal/Gans/Goldfarb): a good *prediction* (propensity) is not a
  good *decision* (incrementality) — frames why a strong baseline still isn't an intervention (sets up
  Ch 8).
- (Reuse) `pantry/moe-vs-ensemble-synthesis.md` — the primary in-pantry source for this chapter.

---

## G. Gaps & flags

- [FLAG/VERIFY] **Tabular DL currency**: synthesis predates the strongest TabPFN v2 (2024/25) results.
  Add a hedge so "trees are SOTA" doesn't age into a falsehood — reframe as "trees are the correct
  baseline; tabular DL is an active, not-yet-default frontier." Verify the 2026 state in ACCURACY pass.
- [VERIFY] Grinsztajn et al. exact title/venue wording ("…typical tabular data," NeurIPS 2022 D&B
  track) and the "~10K samples / 45 datasets" figures against the paper.
- [VERIFY] Add full primary citations for Breiman, Friedman, Freund-Schapire, Wolpert, Chen-Guestrin —
  synthesis names them but without years in all cases.
- [GAP] No pharma-specific *public* benchmark of XGBoost-vs-MoE on NPI propensity exists — that's
  exactly TIKTOC Track C (Ch 13). The chapter exposes the gap; the lab fills it.
- [NOTE] Calibration + leakage are under-covered in the synthesis (which is MoE-vs-ensemble-focused) —
  these are *added* here as pharma-practitioner content, grounded in _lib_advances-in-financial-ML.
