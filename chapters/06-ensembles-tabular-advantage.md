# Chapter 6 — Ensembles and the Tabular-Data Advantage

## 1. Overview

This chapter builds the baseline. By the end of it you will be able to explain the three ways multiple models get combined — bagging, boosting, and stacking — and why diversity among them is not an aesthetic preference but a mathematical necessity with a hard floor. You will be able to justify, from peer-reviewed evidence, why gradient-boosted tree ensembles (XGBoost, LightGBM, CatBoost) are the practical state of the art for medium-sized tabular data, which is exactly what NPI-level propensity prediction is. And you will learn to evaluate such a model *honestly* — calibration alongside discrimination, out-of-time validation instead of random splits, subgroup robustness — and to spot the pharma-specific landmine that makes a model look brilliant offline and collapse in production: leakage from claims-data lag. The reason this matters is strategic, not just technical. The ensemble baseline is the bar. Every fancier claim in the next chapter — "we run a Mixture of Experts," "our deep model beats your trees" — has to clear it. The emotional takeaway the chapter is built to produce: *the boring thing is hard to beat.* One honest hedge, stated up front so the book does not age badly: tabular deep learning (notably TabPFN v2, 2024/25) is genuinely narrowing the gap. Trees remain the correct *baseline*; "trees always win" is a claim with a shelf life, and we will mark it as such.

## 2. Learning Objectives

1. **(Understand)** Explain bagging, boosting, and stacking, and the bias–variance–covariance decomposition that makes ensemble diversity load-bearing.
2. **(Evaluate)** Justify gradient-boosted tree ensembles as state-of-the-art on medium tabular data (Grinsztajn et al., NeurIPS 2022), and state honestly where tabular deep learning is closing the gap.
3. **(Apply · Part B)** Specify an ensemble baseline and an honest evaluation plan for a propensity task in your own research thread — calibration, out-of-time validation, subgroup robustness, and a leakage check.

## 3. Opening Case — The Baseline That Leaks

You build the unglamorous thing first: an XGBoost model that scores each physician's propensity to start prescribing a brand, trained on public data — CMS Open Payments plus Medicare Part D prescriber records, with behavioral and demographic features. The pipeline is clean: features in, gradient-boosted trees, a calibrated probability out, a ranked target list. You run cross-validation and the AUC comes back at 0.94. You are, briefly, delighted. A 0.94 AUC on a real targeting problem would be a genuinely strong baseline — the kind of number that makes a vendor's "AI platform" look like an expensive way to do worse.

Then you check the failure-first instinct this book drills into you, and you go looking for what is too good. You find it. One of your features is a recent-fill flag that was computed *after* the prediction timestamp — it postdates the moment at which you are supposed to be predicting. The model is not predicting future prescribing; it is reading a smudged copy of the answer. This is **target leakage**, and it is the most common way a tabular model lies to its builder.

You fix it: define a strict as-of prediction timestamp and admit only features knowable *before* it. The AUC drops to 0.78. That number is real, and it is the one a vendor claim must actually beat. The dead end taught the lesson the chapter opens with: *a baseline that looks brilliant offline is, more often than not, leaking.* There is a second, subtler version of this trap that comes straight from pharma's data plumbing, and it is the reason this opening is not just a generic ML cautionary tale — we return to it in §4.4.

## 4. Core Sections

### 4.1 The three ensemble paradigms

"Ensemble" just means combining several models. There are three canonical ways to do it, and you should know each by its originating idea.

**Bagging** (Breiman, 1996): train many independent models on bootstrap samples of the data and average or vote their outputs. This primarily reduces **variance** — it averages out each model's overfitting. The **Random Forest** (Breiman, 2001) is bagging plus a twist: at each tree split, only a random subset of features is considered, which decorrelates the trees and pushes the variance down further.

**Boosting** (AdaBoost: Freund & Schapire, 1997; Gradient Boosting: Friedman, 2001): train models *sequentially*, each one correcting the errors of its predecessors. This reduces both **bias and variance** — it is more powerful than bagging, and correspondingly more sensitive to noise and outliers. **XGBoost** (Chen & Guestrin, 2016), **LightGBM**, and **CatBoost** are the dominant modern implementations, and they are the practical default for structured tabular work.

**Stacking** (Wolpert, 1992): train several diverse base models, then train a *meta-learner* on their out-of-fold predictions; the meta-learner learns which base model to trust in which region of the input space. Remember this one — it is the punchline of Chapter 7, because **what most "Mixture of Experts" pharma platforms actually run is stacking**, not MoE.

### 4.2 Why diversity is mathematically load-bearing

Diversity among ensemble members is not a stylistic choice; it is forced by the error math. Ensemble error decomposes as:

> error = bias² + (1/N)·var + (1 − 1/N)·covar

where N is the ensemble size, *var* is the average individual-model variance, and *covar* is the average pairwise covariance between model errors. Watch what happens as you add members. As N grows, the variance term (1/N)·var shrinks toward zero — more models wash out individual noise. But the covariance term (1 − 1/N)·covar grows toward *covar* and **sets a floor**. If your models are perfectly correlated, their covariance equals their variance, and adding more of them buys you nothing. The benefit of a bigger ensemble is bounded by how *independent* its members are.

That is why diversity is load-bearing rather than decorative. But here is the catch that Chapter 7 turns on: ensemble diversity is **manufactured**, not emergent. You generate it with different seeds, different data subsets, different feature sets, different algorithms — all variations on the *same data distribution*. Models trained on the same data learn the same regularities and share the same blind spots; they make correlated errors on the same hard cases no matter how different the algorithms look. This manufactured-diversity limit is precisely what Chapter 7's MoE claims to escape through routing-induced (*emergent*) specialization. Note the tension now; do not resolve it here.

### 4.3 Why trees dominate tabular data — the state-of-the-art claim

Here is the evidence that makes the ensemble baseline more than a placeholder. Grinsztajn, Oyallon, and Varoquaux, in "Why do tree-based models still outperform deep learning on typical tabular data?" (**NeurIPS 2022**, Datasets & Benchmarks track), benchmarked deep-learning methods against tree-based methods across **45 tabular datasets**. The finding: **tree-based models remain state-of-the-art on medium-sized tabular data (around 10,000 samples)** — and that holds even when you set aside trees' large speed advantage.

The paper identifies three reasons, and each maps onto pharma data:

1. **Trees are natively robust to uninformative features.** Real tabular data is full of irrelevant columns; tree splits simply never select them, while neural nets must learn to ignore them. NPI feature vectors are full of weakly informative signals — trees shrug them off.
2. **Neural nets struggle with irregular, non-smooth target functions.** Tabular relationships are often jagged (a threshold effect at a particular decile, a discontinuity at a payment cutoff); tree splits represent those natively, while neural nets bias toward smooth functions.
3. **The best tabular methods are themselves ensemble methods, with a decision tree as the weak learner.** The paper's own conclusion: "the best methods on tabular data… are ensemble methods."

The pharma relevance is direct. NPI-level propensity is a *structured tabular* problem — physician features, prescribing history, Open-Payments history, demographics, behavioral signals. This is exactly the regime where gradient-boosted trees beat neural architectures, **including MoE**. So the ensemble baseline is not a stand-in for something better that you will swap in later. On this problem, it may *be* the best architecture available — which is what makes "we use a fancier model" a claim that owes you a benchmark, not the benefit of the doubt.

### 4.4 Honest evaluation — and the claims-lag landmine

A propensity score is not a classroom accuracy number; it feeds a spend decision. So evaluate it the way the decision requires.

- **Discrimination** (AUC / AUPRC): can the model rank prescribers above non-prescribers? Necessary but *not sufficient* — a model can rank well and still be miscalibrated.
- **Calibration**: do predicted probabilities match observed rates? Check with reliability curves and the Brier score. This is load-bearing for two reasons: downstream bid and spend decisions use the probability as a *quantity* (a 0.8 had better mean 80%), and the uplift meta-learners of Chapter 8 use these scores as base learners, so miscalibration propagates into your causal estimates.
- **Out-of-time validation**: split by *time*, not by random rows. Pharma data drifts; random cross-validation leaks the future into the training fold and flatters the model. Train on earlier periods, test on later ones.
- **Subgroup robustness**: evaluate by specialty, decile, and geography. A model strong on average can be useless on the one segment the campaign actually targets.

Now the pharma-specific landmine, which the opening case previewed. **Claims data arrives with a lag — weeks to months — and is revised after the fact.** That produces two distinct failures:

1. **Target leakage** (the opening case): a feature that encodes the outcome because it postdates the prediction point — a recent-fill flag, a "treated" indicator. Spectacular offline AUC, production collapse. The fix is a strict as-of timestamp and features knowable only *before* it.
2. **The claims-lag illusion of lift**: because fills are *recorded* late, a physician's "post-exposure" prescribing window can include scripts that were actually *written before* exposure but recorded after. The apparent response is inflated by a bookkeeping artifact. This is not only a modeling bug — it feeds directly into the Chapter 5 attribution problem and the Chapter 8 incrementality problem. A "lift" can be partly an accounting lag.

This is why the chapter leads with failure: the most transferable practitioner lesson here is not "boosting beats bagging," it is "your offline number is probably leaking, and in pharma the leak often comes from the calendar."

### 4.5 The honest hedge — tabular deep learning is catching up

If this chapter only said "trees always win," it would age into a falsehood, so here is the calibrated version. Newer tabular deep-learning methods — FT-Transformer, SAINT, and especially **TabPFN and TabPFN v2 (2024/25)** — narrow the gap on some benchmarks, particularly on small-sample problems and where large-scale pre-training transfers well [verify the 2026 state of these results in the accuracy pass]. The Grinsztajn result remains the right anchor for *medium* tabular data, but it is no longer unchallenged across the board.

The honest framing is therefore not "trees are unbeatable" but "trees are the correct *default and baseline*; tabular DL is an active, not-yet-default frontier." That distinction is robust to the next few years of results: even if a deep tabular model eventually wins on your problem, you would only know it *by beating the tuned tree baseline you built first.* The baseline keeps its job either way. (This is a tracked aging-risk item for the book's annual review.)

## 5. Worked Example — Building the Baseline That Survives

**Task.** Build an NPI-propensity baseline on public data that a vendor's "AI platform" claim would have to beat — and make it honest.

**Step 1 — assemble the substrate.** Join CMS Open Payments (payment/meal history per physician) to Medicare Part D prescriber data (prescribing volumes), keyed on NPI, with specialty and geography as features. The target: did the physician start (or increase) prescribing the brand in the next period?

**Step 2 — set the as-of timestamp first.** Before touching a model, fix the prediction point and admit only features knowable before it. This is the single most important step and the one most often skipped.

**Step 3 — fit and tune the ensemble.** Calibrated XGBoost (or LightGBM), tuned with time-respecting cross-validation.

**Step 4 — evaluate the way the decision requires.** AUC *and* a reliability curve *and* Brier score; out-of-time test split; subgroup breakdown by specialty and decile.

**The dead end (worth keeping).** My first version scored 0.94 and I nearly shipped it as the baseline. The recent-fill feature was leaking. After fixing the as-of timestamp the model came back at 0.78. A second, subtler problem surfaced in the out-of-time split: the high decile subgroup looked fine, but the model was near-useless on low-decile physicians — the exact segment a "growth" campaign cares about. Average AUC had hidden a segment failure.

**The lesson.** The deliverable is not "a model with 0.94 AUC." It is "a *calibrated, time-validated, leakage-checked, subgroup-audited* model at 0.78 AUC, with a documented weakness on low deciles" — a baseline you can defend and a bar a fancier claim must clear.

**The limit.** This baseline tells you *who is likely to prescribe.* It does **not** tell you *whom an intervention would change* — propensity is not incrementality. A perfect propensity model is still not an intervention, which is exactly the inversion Chapter 8 forces. As *Prediction Machines* puts it, a good prediction is not a good decision; the baseline is the prediction, not the decision.

## 6. Common Misconceptions

- **"A high offline AUC means a good model."** Usually it means leakage. Check the as-of timestamp before you celebrate.
- **"Calibration is a detail; AUC is what matters."** For a spend decision and for downstream uplift estimation, calibration is co-equal with discrimination.
- **"Random cross-validation is fine."** Not on time-structured pharma data — it leaks the future. Split by time.
- **"More models in the ensemble always helps."** Only if they are diverse; the covariance floor bounds the benefit of correlated members.
- **"Deep learning must beat trees on tabular data because it's newer."** On medium tabular data, trees are the documented state of the art (Grinsztajn 2022); tabular DL is closing the gap but is not the default.
- **"A strong propensity model is a strong intervention."** Propensity ≠ incrementality (Chapter 8).

## 7. Evidence Check & Compliance and Patient-Welfare Check

**Evidence check:**
- *Settled, peer-reviewed:* gradient-boosted trees as state of the art for medium tabular data (Grinsztajn et al., NeurIPS 2022); the bias–variance–covariance decomposition (textbook); the originating papers for bagging/boosting/stacking (Breiman, Friedman, Freund & Schapire, Wolpert, Chen & Guestrin).
- *Contested / evolving:* whether tabular deep learning (TabPFN v2, 2024/25) now matches or beats trees on some problems — narrowing but not settled; flagged for the aging review. `[verify 2026 state.]`
- *Hypothetical / illustrative:* the 0.94→0.78 AUC figures in the opening and worked example are illustrative of the leakage failure mode, not measurements of a specific dataset.
- *Gap:* no pharma-specific *public* benchmark of XGBoost-vs-MoE on NPI propensity exists — that is exactly the Chapter 13 Track C study. This chapter exposes the gap; the lab fills it.

**Compliance and patient-welfare check:** a propensity model's *features* carry the welfare risk. If the model encodes proxies for physician *susceptibility* (responsiveness to promotion) rather than patient *clinical need*, then optimizing the score optimizes influence-ability, not appropriate care — the susceptibility concern from Chapter 3, surfacing in the feature vector itself. The subgroup audit (§4.4) is therefore not only a modeling check but a fairness check: a model that performs differently across specialties or geographies can systematically steer promotion toward or away from groups in ways that warrant a flag to medical and compliance review. And calibration has a welfare dimension — an over-confident propensity score translates directly into over-spend on physicians the model merely *guessed* were high-potential. None of this is adjudicated here; it is flagged and routed.

## 8. Exercises

1. **(Understand)** Define bagging, boosting, and stacking in one sentence each, and state which error component each primarily reduces. Then explain, using the bias–variance–covariance formula, why an ensemble of ten identical models is no better than one.
2. **(Apply+)** Given a public Open Payments + Part D extract, write the *as-of timestamp rule* you would enforce and list five features that would be legitimate before that timestamp and two that would constitute target leakage. Explain the claims-lag illusion of lift in your own words.
3. **(Apply+ · Produce · Part B)** Specify the **ensemble-baseline memo** for a propensity task in your own thread: the target definition, the as-of timestamp, the feature set, the chosen ensemble, and the *honest evaluation plan* (AUC + calibration + out-of-time split + subgroup breakdown + leakage check). Write it so it serves as the bar any "AI platform"/"MoE" claim in Chapter 7 must beat.
4. **(Evaluate)** A vendor claims their deep-learning targeting model "outperforms gradient boosting." Write the three questions you would ask to evaluate the claim, including the one about an independent benchmark on the same task — and state what result would actually justify abandoning the tree baseline.

## 9. The Five-Part AI Block

**When to use AI here.** Use an LLM/CLI assistant to scaffold the pipeline — generate the join logic for Open Payments + Part D, draft the cross-validation harness, and produce the calibration and subgroup-evaluation plots. It is a fast, competent pair-programmer for boilerplate.

**When NOT to use AI here.** Do not let an AI decide your *as-of timestamp* or vet your features for leakage on its own. Whether a feature postdates the prediction point depends on pharma data-plumbing facts (claims lag, revisions) the model does not know about your specific source. Leakage detection is the human judgment this chapter trains; an LLM will happily build you a beautiful, leaking pipeline.

**LLM exercise.** Prompt: *"Here is my feature list and my prediction timestamp for an NPI-propensity model on Medicare Part D + Open Payments. For each feature, ask me the questions you'd need answered to determine whether it could leak the outcome — do not assume, ask. Then propose a calibration and out-of-time validation plan."* You answer the leakage questions from domain knowledge; the AI drafts the eval plan.

**CLI exercise.** With a public extract loaded, use command-line tooling to compute the date distribution of your claims records (`csvstat`/`awk` on the fill-date column) and *show yourself* the lag between service date and recorded date. Then count how many "post-exposure" records have service dates that predate a hypothetical exposure window. This makes the claims-lag illusion concrete with real numbers.

**AI validation.** Have the AI generate the evaluation report, then validate it: re-run the calibration on a held-out *time* split yourself, confirm the AUC was not computed on a random split, and confirm no feature in the final model postdates the as-of timestamp. Record any leakage the AI's pipeline introduced.

## 10. AI Use Disclosure

An LLM assisted in structuring the ensemble taxonomy and drafting the worked-example pipeline steps; all evaluation choices, the leakage/claims-lag framing, and the TabPFN hedge were set against the synthesis and library sources and verified by hand. The judgment an AI could not supply: **deciding which features leak given the specific claims-lag behavior of the data source, and deciding that a leakage-free 0.78 is the real baseline rather than the leaking 0.94.** That call requires pharma data-plumbing knowledge the model does not have about your source. (Part B standard: name the one leakage decision you made that the AI could not.)

## 11. What Would Change My Mind

I would retire "gradient-boosted trees are the correct baseline for NPI propensity" if an independent, reproducible benchmark — on a public NPI-propensity task, with calibration and out-of-time validation, not just headline accuracy — showed a tabular deep-learning model (or a genuine MoE) *consistently and meaningfully* beating a well-tuned tree ensemble, with the gain surviving subgroup and out-of-time scrutiny. TabPFN v2's trajectory makes this a live possibility, not a rhetorical one. Until that benchmark exists, the trees stay the baseline — and even after it exists, you would only have learned it by building the baseline first.

## 12. Still Puzzling

- If tree ensembles are state of the art on tabular data, why do so many pharma platforms reach for deep-learning and "MoE" framing — is it performance, or is it the funding and prestige that attach to those words?
- The covariance floor bounds ensemble benefit; routing-induced specialization (Chapter 7) claims to break it. On *tabular* data with no token sequence, is there any natural unit for routing to specialize over?
- Calibration matters for spend and for uplift — but how miscalibrated can a propensity model be before it corrupts the Chapter 8 CATE estimates that use it as a base learner?

## 13. Summary

You can now name the three ensemble paradigms and explain, via the bias–variance–covariance floor, why manufactured diversity has a hard limit — the limit Chapter 7's MoE claims to escape. You can justify gradient-boosted trees as the documented state of the art for medium tabular data, which is what NPI propensity is, while stating honestly that tabular deep learning is narrowing the gap. You can evaluate a model the way a spend decision requires — calibration and out-of-time validation and subgroup robustness, not AUC alone — and you can detect the pharma-specific leakage that makes a model look brilliant offline and fail in production. Most of all, you have the baseline: the unglamorous, calibrated, leakage-checked tree ensemble that every fancier claim in the next chapter must beat. The boring thing is hard to beat — and proving that is the whole point.

## 14. Key Terms

- **Bagging:** train independent models on bootstrap samples and average/vote; reduces variance (Random Forest is the canonical case).
- **Boosting:** train models sequentially, each correcting prior errors; reduces bias and variance (XGBoost, LightGBM, CatBoost).
- **Stacking:** train a meta-learner on base models' out-of-fold predictions; what most "MoE" platforms actually run (Chapter 7).
- **Bias–variance–covariance decomposition:** the error formula whose covariance term sets a floor, making diversity load-bearing.
- **Manufactured vs. emergent diversity:** ensemble diversity is engineered on one data distribution (shared blind spots); MoE claims routing-induced emergent diversity.
- **Calibration:** agreement between predicted probabilities and observed rates; required when the probability feeds a spend decision or a CATE estimate.
- **Out-of-time validation:** splitting by time, not random rows, to avoid leaking the future on drifting pharma data.
- **Target leakage:** a feature that encodes the outcome (often by postdating the prediction point); the leading cause of too-good offline numbers.
- **Claims-lag illusion of lift:** late-recorded fills inflating apparent post-exposure response — a bookkeeping artifact feeding the attribution and incrementality problems.

## 15. Bridge

You now hold the baseline: a tuned, honestly evaluated tree ensemble that is genuinely hard to beat on tabular NPI prediction. So when the next vendor says the upgrade is a "Mixture of Experts," you have the one thing needed to judge it — a bar. The next chapter takes MoE apart precisely, shows you what most pharma "MoE" claims actually are (you already know: stacking), and gives you the buyer's questions to tell a real routing model from a transformer-era relabel.

## 16. Further Reading

- Grinsztajn, L., Oyallon, E., & Varoquaux, G. "Why do tree-based models still outperform deep learning on typical tabular data?" *NeurIPS 2022* (Datasets & Benchmarks Track). The anchor evidence — 45 datasets, trees state-of-the-art on medium tabular data, and the three reasons why. [verify exact title/venue wording.]
- Chen, T., & Guestrin, C. "XGBoost: A Scalable Tree Boosting System." *KDD 2016.* The implementation that made gradient boosting the practical default; read for the engineering that matters at commercial scale.
- López de Prado, M. *Advances in Financial Machine Learning* (2018). The best practitioner treatment of leakage, cross-validation under temporal structure, and backtest overfitting — maps directly onto the pharma claims-lag failure case and out-of-time validation.
- Agrawal, A., Gans, J., & Goldfarb, A. *Prediction Machines* (2018). The prediction-vs-decision distinction — why a strong propensity model is still not an intervention. Sets up Chapter 8.
- TabPFN v2 and tabular-DL benchmark literature (2024/25). Track the live challenger to the "trees win" claim; read alongside Grinsztajn to calibrate the §4.5 hedge. [verify current results in the accuracy pass before citing specifics.]

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
