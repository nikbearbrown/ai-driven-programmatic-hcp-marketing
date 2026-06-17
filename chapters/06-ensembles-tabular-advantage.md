# Chapter 6 — Ensembles and the Tabular-Data Advantage
*Why the boring model is hard to beat, and why that is the most useful thing you can know.*

The number came back at 0.94. I had built the unglamorous thing first — an XGBoost model scoring each physician's propensity to start prescribing a brand, trained on public data, calibrated outputs, ranked target list. Clean pipeline. Sensible features. And an AUC of 0.94, which on a real targeting problem would be extraordinary. The kind of number that makes a vendor's "AI platform" look like an expensive way to do worse.

Then I went looking for what was too good.

The failure-first instinct this book keeps returning to is not pessimism; it is the only reliable way to learn what a model is actually doing. And what this model was doing, I found, was reading a smudged copy of the answer. One of my features — a recent-fill flag — had been computed *after* the prediction timestamp. It postdated the moment at which I was supposed to be predicting. The model was not forecasting future prescribing. It was encoding a bookkeeping artifact of future prescribing.

I fixed the timestamp, cut the feature, and ran it again. The AUC dropped to 0.78.

That number is real. It is the bar a vendor's fancier claim would have to beat. The 0.94 was a hallucination the data was willing to produce because I had not yet asked it the right question. And the particular way pharma data produces this hallucination — through claims-processing lag, through features whose timestamp you think you know but do not — is the first thing to understand before anything else in this chapter makes sense.

---

An ensemble is just a collection of models whose outputs get combined. That sentence is almost insultingly simple, and it is nonetheless the key. The question worth asking is *why* combining models helps at all, because the answer — the real mathematical answer — is not "averaging smooths things out" but something more precise, and it has a hard limit that controls everything that follows.

Start from the error of a single model. It decomposes into two parts: **bias** (how far off the model is on average, from being systematically wrong) and **variance** (how much the model's outputs fluctuate across different training sets, from being unstably right). These trade off. A simple model — a shallow tree, a linear regression — is biased but stable. A complex model — a deep tree, an overparameterized network — is less biased but bounces around wildly across training runs.

Now take *N* models and average them. The bias of the average equals the average bias — you cannot remove systematic errors by averaging. But the variance term drops: it scales as *1/N* times the average individual variance. More models, lower variance. This is why averaging helps.

But here is the catch that the textbook often glosses past. The full formula for ensemble error includes a third term: **covariance** — the degree to which the models make correlated errors. The complete decomposition is:

$$\text{ensemble error} \approx \text{bias}^2 + \frac{1}{N}\cdot\text{var} + \left(1 - \frac{1}{N}\right)\cdot\text{covar}$$

As N grows large, the variance term shrinks toward zero. But the covariance term grows toward *covar* and **sets a floor**. If your models make perfectly correlated errors — if they all fail on the same cases in the same direction — then combining them buys you nothing. The floor on ensemble error is determined entirely by how *independent* the members are from each other.

This is why diversity among ensemble members is not an aesthetic preference. It is mathematically load-bearing. And it is also where the uncomfortable truth lives: ensemble diversity is **manufactured**, not emergent. You generate it with different random seeds, different bootstrap samples, different feature subsets, different algorithms — but all of these are variations on the same underlying data distribution. Models trained on the same data share the same blind spots. They will make correlated errors on the hard cases regardless of how different the algorithms look. The covariance floor is real, and manufactured diversity cannot eliminate it.

Hold that thought. Chapter 7 is going to make a specific claim — that Mixture of Experts systems escape this floor through *routing-induced* specialization. That claim deserves to be examined with exactly this math in hand. But the resolution is not this chapter's problem. The floor is.

<!-- → [DIAGRAM: Three-panel figure showing bias-variance-covariance decomposition. Panel 1: single model error as bias² + variance. Panel 2: 10-model ensemble — variance term shrinks, covariance term appears and grows. Panel 3: the covariance floor: as N → ∞, ensemble error approaches bias² + covar. Caption: "Adding models reduces variance but cannot reduce correlated error. Diversity is what moves the floor."] -->

---

There are three canonical ways to manufacture that diversity, and you should know them by their originating idea rather than their names.

The first is **bagging** — Leo Breiman, 1996. Train many independent models on bootstrap samples of the data (random draws with replacement) and average their outputs. The independence is the point: each model sees a slightly different dataset, learns slightly different patterns, makes slightly different errors. Averaging washes the differences out in a direction that reduces variance. The **Random Forest** (Breiman again, 2001) pushes this further: at each split in each tree, only a random subset of features is considered. This decorrelates the trees even more aggressively than the bootstrap alone. Random Forests are still competitive on many problems and are often the right first thing to try.

The second is **boosting**. Rather than training models independently and averaging, train them *sequentially*, each one correcting the errors of its predecessors. The first model fits the data; the second fits the residuals of the first; the third fits the residuals of the second. Freund and Schapire's AdaBoost (1997) formalized this for classification. Friedman's Gradient Boosting (2001) generalized it to arbitrary loss functions by framing each sequential model as a gradient descent step in function space. The dominant modern implementations — **XGBoost** (Chen and Guestrin, 2016), **LightGBM**, **CatBoost** — are all gradient-boosted decision tree systems, and they are the practical default for structured tabular work. Boosting reduces both bias and variance, which makes it more powerful than bagging. It is correspondingly more sensitive to noise and outliers, and requires more care in tuning.

The third is **stacking** — David Wolpert, 1992. Train several diverse base models. Then train a *meta-learner* on their out-of-fold predictions: the meta-learner learns which base model to trust in which region of the input space, and combines them accordingly. Remember stacking's definition precisely, because it is the punchline of Chapter 7: **most pharma platforms that describe themselves as running "Mixture of Experts" are actually running stacking**. The terms have been relabeled; the machinery has not changed. Knowing what stacking actually is lets you ask the right question about whether what a vendor is selling is genuinely different.

<!-- → [TABLE: Three-column comparison of bagging, boosting, and stacking. Columns: paradigm, originating idea, primary error component reduced, canonical modern implementation, key weakness. Rows: Bagging (parallel, independent; variance; Random Forest; correlated errors if features overlap), Boosting (sequential, corrective; bias + variance; XGBoost/LightGBM/CatBoost; sensitive to noise), Stacking (meta-learner on base models; both via learned combination; any diverse ensemble + meta-learner; requires careful out-of-fold discipline to avoid leakage).] -->

---

So why does this matter for the specific problem of predicting which physician will prescribe a drug?

There is a rigorous answer to this question. Léo Grinsztajn, Edouard Oyallon, and Gaël Varoquaux published "Why do tree-based models still outperform deep learning on typical tabular data?" at NeurIPS 2022 — the Datasets and Benchmarks track, where the standard of evidence is precisely the kind of broad, comparative evaluation the question requires. They tested deep-learning methods against tree-based methods across 45 tabular datasets. The finding: **tree-based models remain state-of-the-art on medium-sized tabular data** — around 10,000 samples — and that holds even setting aside trees' substantial speed advantage.

The paper identifies three mechanisms, and each one maps onto the pharma problem directly.

First: trees are natively robust to uninformative features. A split on a useless feature will be selected away from by the tree's information criterion; the feature simply goes unused. Neural networks must *learn* to ignore uninformative inputs, which takes capacity and training examples. An NPI feature vector is full of weakly informative signals — Open Payments meal counts from three years ago, engagement rates on specific journal articles, geography proxies — and trees shrug them off while networks waste capacity on them.

Second: neural networks are biased toward smooth functions. The gradient descent process that trains them nudges outputs toward continuity; the inductive bias is toward interpolating gradually across the input space. Tabular relationships are often jagged: a threshold effect at a particular prescribing decile, a discontinuity at a payment cutoff, a specialty boundary that creates a hard categorical jump. Decision tree splits represent those discontinuities natively. Neural networks must approximate them with many parameters.

Third — and the paper states this directly — the best tabular methods are themselves ensemble methods, with a decision tree as the weak learner. The paper's own conclusion: the best methods on tabular data are ensemble methods.

The pharma relevance is not a loose analogy. NPI-level propensity prediction is a structured tabular problem: physician features, prescribing history, Open-Payments history, demographics, behavioral engagement signals. This is exactly the regime the Grinsztajn result covers. The gradient-boosted tree ensemble is not a stand-in for something better that you will swap in later. On this problem, it may be the best architecture available — which makes "we use a fancier model" a claim that owes you a benchmark, not the benefit of the doubt.

One hedge, stated explicitly because otherwise this chapter ages badly: newer tabular deep-learning methods — FT-Transformer, SAINT, and particularly **TabPFN and TabPFN v2 (2024/25)** — are narrowing the gap on some benchmarks, especially on small-sample problems and where large-scale pre-training transfers well. [verify 2026 state of these results.] The Grinsztajn result remains the right anchor for medium tabular data, but it is no longer unchallenged across the entire landscape. The honest framing is not "trees are unbeatable" but "trees are the correct default and baseline; tabular deep learning is an active, not-yet-default frontier." That framing is robust to the next few years of results — even if a deep tabular model eventually wins on your specific problem, you would only know that by beating the tuned tree baseline you built first.

<!-- → [CHART: Bar chart reproducing the qualitative structure of Grinsztajn et al. 2022 Figure 1 — tree-based vs. deep-learning methods ranked by average normalized performance across 45 tabular datasets. Trees clustered at the top; DL methods scattered lower. Caption: "On medium tabular data, gradient-boosted trees consistently outperform deep-learning architectures. This is the benchmark any 'AI platform' claim must beat. Source: Grinsztajn et al., NeurIPS 2022. [verify figure representation against paper before publication.]"] -->

---

Now for how to evaluate the model honestly — which is a separate question from how to build it, and the one that most often gets skipped.

A propensity score feeds a spend decision. It gets used as a quantity: this physician gets a $40 CPM impression because her score is 0.8; that physician gets nothing because his score is 0.3. For a quantity to be useful, it needs to mean what it says. This is the difference between **discrimination** and **calibration**, and it is the difference that most model-evaluation practice ignores.

Discrimination — measured by AUC or AUPRC — answers: can the model rank prescribers above non-prescribers? Can it tell the top decile from the bottom? This is necessary but not sufficient. A model can rank perfectly and still be completely miscalibrated: every score 0.05 too high, every confidence interval in the wrong direction. AUC would not catch it. A reliability curve would.

**Calibration** asks whether predicted probabilities match observed rates. Plot your bins: the group of physicians you scored between 0.7 and 0.8 — what fraction of them actually prescribed? If the answer is 0.6, your model is overconfident and every bid decision built on it is systematically wrong. The Brier score captures this in a single number. Calibration is not a detail. For spend decisions it is co-equal with discrimination, and for the uplift estimation of Chapter 8 it is load-bearing — CATE estimates use propensity scores as base learners, so miscalibration propagates directly into causal estimates.

**Out-of-time validation** means splitting by time, not by randomly shuffled rows. Pharma data drifts. Prescribing patterns shift with trial publications, label changes, competitor entries. Random cross-validation leaks the future into the training fold and makes your model look more stable than it is. Train on earlier periods. Test on later ones. Any lift in performance you see on a random split that disappears on a time split is a signal the model has memorized temporal regularities it will not have at deployment.

**Subgroup robustness** means evaluating by specialty, decile, and geography separately — not just on the aggregate. A model that is strong on average can be useless on the one segment the campaign actually targets. In my worked example, the aggregate AUC after fixing the leakage was 0.78 and looked defensible. Breaking it out by decile revealed the model was near-useless on low-decile physicians — the exact group a growth campaign cares about most. Aggregate AUC had hidden a segment failure.

<!-- → [INFOGRAPHIC: Four-quadrant evaluation checklist. Quadrant 1: Discrimination (AUC, AUPRC — "can it rank?"). Quadrant 2: Calibration (reliability curve, Brier score — "does the probability mean what it says?"). Quadrant 3: Temporal validation (out-of-time split — "does it hold when the future is actually the future?"). Quadrant 4: Subgroup robustness (by specialty, decile, geography — "where does it fail?"). Each quadrant includes a one-line failure mode if skipped. Caption: "A model that passes all four is the baseline. A model that passes only the first is the most common mistake."] -->

---

Now back to the pharma-specific landmine that the opening case previewed, because there is a second version of the leakage problem that is subtler and more dangerous.

The first version is the one I hit: a feature that postdates the prediction point. Fix the as-of timestamp, remove the offending feature, done. But the second version is not about features at all. It is about *when fills are recorded* relative to when they were written.

Claims data arrives with a lag. A prescription written in March may not appear in adjudicated claims until April or May, after processing delays at the pharmacy, the payer, and the data broker. When you build a "post-exposure" outcome window — prescribing in the 90 days after a marketing contact — some of those fills were actually written *before* the contact but recorded after it. The apparent response is inflated by a bookkeeping artifact. The physician looks like a responder because the data processing calendar aligned in a way that had nothing to do with your intervention.

This is the **claims-lag illusion of lift**, and it feeds directly into the attribution problem of Chapter 8. A model trained to predict propensity on stale claims, evaluated on an outcome window contaminated by late-recorded fills, will systematically overstate both its targeting accuracy and the lift it is credited with producing. The fix — strict as-of timestamps, careful outcome-window construction that excludes fills with service dates predating exposure — requires knowing about the data plumbing. An AI assistant will happily build you a beautiful, self-consistent pipeline that nonetheless leaks in this way, because the lag behavior of your specific claims source is not in its training data.

---

What you have by the end of this chapter is the baseline: a tuned, calibrated, leakage-checked, out-of-time-validated, subgroup-audited gradient-boosted tree ensemble at some honest AUC — 0.78, in my case. Not 0.94. 0.78, with a documented weakness on low deciles and a recorded as-of timestamp that a vendor's analyst could check.

That number is the bar. Every claim in Chapter 7 — "we run a Mixture of Experts," "our deep model beats trees," "our routing architecture unlocks specialist knowledge the ensemble misses" — has to clear it. Not on some internal holdout set with a different data distribution, not on a random split that leaks temporal regularities, not on aggregate AUC that hides a segment failure. On the same task, evaluated the same way.

The boring thing is hard to beat. Building it correctly is the proof.

**Five-part AI exercise block**

**When to use AI here.** Use an LLM or CLI assistant to scaffold the pipeline — generate the join logic for Open Payments and Part D data, draft the cross-validation harness, produce the calibration curve and subgroup evaluation plots. It is a fast, competent pair programmer for boilerplate.

**When NOT to use AI here.** Do not let an AI decide your as-of timestamp or vet your features for leakage on its own. Whether a feature postdates the prediction point depends on pharma data-plumbing facts — claims lag, revision cycles, broker processing delays — that the model does not know about your specific source. Leakage detection is the human judgment this chapter trains. An LLM will happily build you a beautiful, leaking pipeline.

**LLM exercise (copy-paste prompt):**
> "Here is my feature list and my prediction timestamp for an NPI-propensity model on Medicare Part D and Open Payments data. For each feature, ask me the questions you'd need answered to determine whether it could leak the outcome — do not assume, ask. Then propose a calibration and out-of-time validation plan based on my answers."

**CLI exercise.** With a public extract loaded, use command-line tooling to compute the date distribution of your claims records (`csvstat` or `awk` on the fill-date column) and show yourself the lag between service date and recorded date. Then count how many "post-exposure" records have service dates that predate a hypothetical exposure window. This makes the claims-lag illusion concrete with real numbers rather than an abstraction.

**AI validation.** Have the AI generate the full evaluation report, then audit it: re-run the calibration on a held-out *time* split yourself, confirm the AUC was not computed on a random split, and confirm no feature in the final model postdates the as-of timestamp. Record any leakage the AI's pipeline introduced.

## AI Use Disclosure

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to scaffold the pipeline and draft the evaluation harness; I decided which features leak given the claims-lag behavior of my specific data source, because that is pharma data-plumbing knowledge the model does not have."*

## What Would Change My Mind

I would retire "gradient-boosted trees are the correct baseline for NPI propensity" if an independent, reproducible benchmark — on a public NPI-propensity task, with calibration and out-of-time validation, not just headline accuracy — showed a tabular deep-learning model consistently and meaningfully beating a well-tuned tree ensemble, with the gain surviving subgroup and out-of-time scrutiny. TabPFN v2's trajectory makes this a live possibility. Until that benchmark exists on this specific task, the trees stay the baseline — and even after it exists, you would only have learned it by building the baseline first.

## Still Puzzling

- If tree ensembles are state of the art on tabular data, why do so many pharma platforms reach for deep-learning and Mixture of Experts framing? Is it performance, or is it the funding and prestige those words attract?
- The covariance floor bounds ensemble benefit from manufactured diversity. Routing-induced specialization claims to break it. On tabular data with no token sequence, what is the natural unit for routing to specialize over?
- Calibration matters for spend decisions and for uplift estimation — but how miscalibrated can a propensity model be before it corrupts the Chapter 8 CATE estimates that use it as a base learner?

---

## Exercises

**Warm-up**

1. *(Recall — low difficulty) What this tests: whether you can state the three paradigms and their error targets.* Define bagging, boosting, and stacking in one sentence each, and state which component of the bias-variance-covariance error decomposition each primarily reduces. Then explain, using the covariance floor, why an ensemble of ten identical models trained on the same data is no better than one.

2. *(Recall — low difficulty) What this tests: whether you can state the Grinsztajn result and its scope conditions.* Summarize the Grinsztajn et al. (NeurIPS 2022) finding in two sentences: what was tested, what was found, and what the authors themselves concluded about the nature of the winning methods. Then name one condition under which the result is actively contested.

3. *(Recall — low difficulty) What this tests: whether you can distinguish discrimination from calibration.* Define AUC and Brier score in your own words, and explain in one sentence why a model can achieve high AUC while being severely miscalibrated. Give a concrete example of a spend-decision context where miscalibration causes a worse outcome than low AUC would.

**Application**

4. *(Apply — medium difficulty) What this tests: leakage detection on a realistic feature list.* Given a public Open Payments and Part D extract with a prediction timestamp of January 1, classify each of the following features as legitimate or leaking, and justify in one sentence: (a) specialty as of last year, (b) total meals received in the prior 12 months, (c) a recent-fill flag computed on February adjudicated data, (d) prescribing volume in Q3 of the prior year, (e) a trend feature computed as Q4-minus-Q3 volume from the prior year's adjudicated claims. Then explain in your own words how the claims-lag illusion of lift differs from straightforward target leakage.

5. *(Apply — medium difficulty) What this tests: designing a time-respecting evaluation plan.* You have 36 months of NPI-level prescribing data. Specify an out-of-time validation design — training period, validation period, test period, and the rationale for the boundary choices. Then identify one subgroup breakdown you would run and explain what a failure in that subgroup would tell you about the model's deployment risk.

6. *(Apply — medium difficulty) What this tests: translating the covariance floor into a practical diagnostic.* You train five XGBoost models with different random seeds on the same data. Their pairwise error correlations are all above 0.92. What does this tell you about the expected benefit of the ensemble relative to a single model, and what would you change to push the correlation down?

**Synthesis**

7. *(Synthesis — high difficulty) What this tests: integrating the baseline specification and evaluation plan into a defensible memo.* Write the ensemble-baseline memo for a propensity task: the target definition, the as-of timestamp, the feature set (with a leakage check for each feature), the chosen ensemble and tuning approach, and the honest evaluation plan including calibration, out-of-time split, and subgroup breakdown. Write it so it serves as the explicit bar that any vendor's "AI platform" or "Mixture of Experts" claim must beat in Chapter 7.

8. *(Synthesis — high difficulty) What this tests: connecting propensity calibration to downstream causal estimation.* Chapter 8 will use propensity scores as base learners in CATE estimation. Explain in three to four sentences how systematic miscalibration in the propensity model — specifically, overconfident scores in the high-propensity decile — would propagate into the causal estimates. What direction would the bias run, and what evaluation step in this chapter would catch it?

**Challenge**

9. *(Challenge — open-ended) What this tests: critical evaluation of a vendor benchmark.* A pharma platform vendor publishes a white paper claiming their deep-learning model achieves AUC 0.91 on NPI propensity prediction versus 0.83 for "standard gradient boosting." Write the three questions you would ask to evaluate the claim — including questions about the split strategy, the feature set, calibration reporting, and whether the comparison baseline was tuned — and state precisely what evidence would justify abandoning the tree baseline in favor of the vendor's model.
