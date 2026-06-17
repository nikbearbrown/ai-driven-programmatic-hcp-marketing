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

![Three-panel diagram of the bias-variance-covariance decomposition. Panel 1: a single model's error as bias-squared plus variance. Panel 2: a ten-model ensemble where the variance term shrinks and a covariance term appears. Panel 3: the covariance floor as N approaches infinity, where ensemble error settles at bias-squared plus covariance.](images/06-ensembles-tabular-advantage-fig-01.png)
*Figure 6.1 — Adding models reduces variance but cannot reduce correlated error*

<!-- → [DIAGRAM: Three-panel figure showing bias-variance-covariance decomposition. Panel 1: single model error as bias² + variance. Panel 2: 10-model ensemble — variance term shrinks, covariance term appears and grows. Panel 3: the covariance floor: as N → ∞, ensemble error approaches bias² + covar. Caption: "Adding models reduces variance but cannot reduce correlated error. Diversity is what moves the floor."] -->

---

There are three canonical ways to manufacture that diversity, and you should know them by their originating idea rather than their names.

The first is **bagging** — Leo Breiman, 1996. Train many independent models on bootstrap samples of the data (random draws with replacement) and average their outputs. The independence is the point: each model sees a slightly different dataset, learns slightly different patterns, makes slightly different errors. Averaging washes the differences out in a direction that reduces variance. The **Random Forest** (Breiman again, 2001) pushes this further: at each split in each tree, only a random subset of features is considered. This decorrelates the trees even more aggressively than the bootstrap alone. Random Forests are still competitive on many problems and are often the right first thing to try.

The second is **boosting**. Rather than training models independently and averaging, train them *sequentially*, each one correcting the errors of its predecessors. The first model fits the data; the second fits the residuals of the first; the third fits the residuals of the second. Freund and Schapire's AdaBoost (1997) formalized this for classification. Friedman's Gradient Boosting (2001) generalized it to arbitrary loss functions by framing each sequential model as a gradient descent step in function space. The dominant modern implementations — **XGBoost** (Chen and Guestrin, 2016), **LightGBM**, **CatBoost** — are all gradient-boosted decision tree systems, and they are the practical default for structured tabular work. Boosting reduces both bias and variance, which makes it more powerful than bagging. It is correspondingly more sensitive to noise and outliers, and requires more care in tuning.

The third is **stacking** — David Wolpert, 1992. Train several diverse base models. Then train a *meta-learner* on their out-of-fold predictions: the meta-learner learns which base model to trust in which region of the input space, and combines them accordingly. Remember stacking's definition precisely, because it is the punchline of Chapter 7: **most pharma platforms that describe themselves as running "Mixture of Experts" are actually running stacking**. The terms have been relabeled; the machinery has not changed. Knowing what stacking actually is lets you ask the right question about whether what a vendor is selling is genuinely different.

| Paradigm | Originating idea | Primary error component reduced | Canonical modern implementation | Key weakness |
|---|---|---|---|---|
| Bagging | Parallel, independent models on bootstrap samples, then averaged (Breiman, 1996) | Variance | Random Forest (Breiman, 2001) | Correlated errors if features overlap; cannot beat the covariance floor |
| Boosting | Sequential, corrective — each model fits the residuals of its predecessors (Freund & Schapire 1997; Friedman 2001) | Bias and variance | XGBoost / LightGBM / CatBoost | Sensitive to noise and outliers; needs careful tuning |
| Stacking | Meta-learner trained on base models' out-of-fold predictions (Wolpert, 1992) | Both, via learned combination | Any diverse ensemble + meta-learner | Requires strict out-of-fold discipline to avoid leakage; often relabeled "Mixture of Experts" |

*Table 6.1 — Three ways to manufacture ensemble diversity. Stacking is the one to hold precisely: most pharma platforms describing a "Mixture of Experts" are running stacking under a relabeled name.*

---

So why does this matter for the specific problem of predicting which physician will prescribe a drug?

There is a rigorous answer to this question. Léo Grinsztajn, Edouard Oyallon, and Gaël Varoquaux published "Why do tree-based models still outperform deep learning on typical tabular data?" at NeurIPS 2022 — the Datasets and Benchmarks track (arXiv 2207.08815), where the standard of evidence is precisely the kind of broad, comparative evaluation the question requires. They tested deep-learning methods against tree-based methods across 45 tabular datasets. The finding: **tree-based models remain state-of-the-art on medium-sized tabular data** — around 10,000 samples — and that holds even setting aside trees' substantial speed advantage.

The paper identifies three mechanisms, and each one maps onto the pharma problem directly.

First: trees are natively robust to uninformative features. A split on a useless feature will be selected away from by the tree's information criterion; the feature simply goes unused. Neural networks must *learn* to ignore uninformative inputs, which takes capacity and training examples. An NPI feature vector is full of weakly informative signals — Open Payments meal counts from three years ago, engagement rates on specific journal articles, geography proxies — and trees shrug them off while networks waste capacity on them.

Second: neural networks are biased toward smooth functions. The gradient descent process that trains them nudges outputs toward continuity; the inductive bias is toward interpolating gradually across the input space. Tabular relationships are often jagged: a threshold effect at a particular prescribing decile, a discontinuity at a payment cutoff, a specialty boundary that creates a hard categorical jump. Decision tree splits represent those discontinuities natively. Neural networks must approximate them with many parameters.

Third — and the paper states this directly — the best tabular methods are themselves ensemble methods, with a decision tree as the weak learner. The paper's own conclusion: the best methods on tabular data are ensemble methods.

The pharma relevance is not a loose analogy. NPI-level propensity prediction is a structured tabular problem: physician features, prescribing history, Open-Payments history, demographics, behavioral engagement signals. This is exactly the regime the Grinsztajn result covers. The gradient-boosted tree ensemble is not a stand-in for something better that you will swap in later. On this problem, it may be the best architecture available — which makes "we use a fancier model" a claim that owes you a benchmark, not the benefit of the doubt.

One hedge, stated explicitly because otherwise this chapter ages badly: newer tabular deep-learning methods — FT-Transformer, SAINT, and particularly TabPFN and its successor TabPFN v2 — have been reported to narrow the gap on some benchmarks, especially on small-sample problems and where large-scale pre-training transfers well. [verify — unconfirmed: the precise 2026 standing of TabPFN-class results against tuned tree baselines across benchmarks; treat as an active, contested frontier rather than a settled result.] The Grinsztajn result remains the right anchor for medium tabular data, but it is no longer unchallenged across the entire landscape. The honest framing is not "trees are unbeatable" but "trees are the correct default and baseline; tabular deep learning is an active, not-yet-default frontier." That framing is robust to the next few years of results — even if a deep tabular model eventually wins on your specific problem, you would only know that by beating the tuned tree baseline you built first.

![Bar chart qualitatively reproducing the structure of Grinsztajn et al. 2022 Figure 1: tree-based methods clustered at the top of average normalized performance across 45 tabular datasets, deep-learning methods scattered lower.](images/06-ensembles-tabular-advantage-fig-02.png)
*Figure 6.2 — Tree-based vs. deep-learning methods on medium tabular data (qualitative reproduction of Grinsztajn et al., NeurIPS 2022, arXiv 2207.08815; bar heights are illustrative, not exact published values)*

<!-- → [CHART: Bar chart reproducing the qualitative structure of Grinsztajn et al. 2022 Figure 1 — tree-based vs. deep-learning methods ranked by average normalized performance across 45 tabular datasets. Trees clustered at the top; DL methods scattered lower. Caption: "On medium tabular data, gradient-boosted trees consistently outperform deep-learning architectures. This is the benchmark any 'AI platform' claim must beat. Source: Grinsztajn et al., NeurIPS 2022. [verify figure representation against paper before publication.]"] -->

---

Now for how to evaluate the model honestly — which is a separate question from how to build it, and the one that most often gets skipped.

A propensity score feeds a spend decision. It gets used as a quantity: this physician gets a $40 CPM impression because her score is 0.8; that physician gets nothing because his score is 0.3. For a quantity to be useful, it needs to mean what it says. This is the difference between **discrimination** and **calibration**, and it is the difference that most model-evaluation practice ignores.

Discrimination — measured by AUC or AUPRC — answers: can the model rank prescribers above non-prescribers? Can it tell the top decile from the bottom? This is necessary but not sufficient. A model can rank perfectly and still be completely miscalibrated: every score 0.05 too high, every confidence interval in the wrong direction. AUC would not catch it. A reliability curve would.

**Calibration** asks whether predicted probabilities match observed rates. Plot your bins: the group of physicians you scored between 0.7 and 0.8 — what fraction of them actually prescribed? If the answer is 0.6, your model is overconfident and every bid decision built on it is systematically wrong. The Brier score captures this in a single number. Calibration is not a detail. For spend decisions it is co-equal with discrimination, and for the uplift estimation of Chapter 8 it is load-bearing — CATE estimates use propensity scores as base learners, so miscalibration propagates directly into causal estimates.

**Out-of-time validation** means splitting by time, not by randomly shuffled rows. Pharma data drifts. Prescribing patterns shift with trial publications, label changes, competitor entries. Random cross-validation leaks the future into the training fold and makes your model look more stable than it is. Train on earlier periods. Test on later ones. Any lift in performance you see on a random split that disappears on a time split is a signal the model has memorized temporal regularities it will not have at deployment.

**Subgroup robustness** means evaluating by specialty, decile, and geography separately — not just on the aggregate. A model that is strong on average can be useless on the one segment the campaign actually targets. In my worked example, the aggregate AUC after fixing the leakage was 0.78 and looked defensible. Breaking it out by decile revealed the model was near-useless on low-decile physicians — the exact group a growth campaign cares about most. Aggregate AUC had hidden a segment failure.

![Four-quadrant evaluation checklist. Discrimination (AUC, AUPRC — can it rank?), Calibration (reliability curve, Brier score — does the probability mean what it says?), Temporal validation (out-of-time split — does it hold when the future is actually the future?), and Subgroup robustness (by specialty, decile, geography — where does it fail?), each with a one-line failure mode if skipped.](images/06-ensembles-tabular-advantage-fig-03.png)
*Figure 6.3 — The four-quadrant evaluation checklist for an honest baseline*

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

---

## Prompts

### Figure 6.1 — Adding models reduces variance but cannot reduce correlated error

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a three-panel stacked-bar diagram of the bias-variance-covariance decomposition of ensemble error. Panel 1 (single model): two stacked segments, bias² and variance. Panel 2 (10-model ensemble): bias² unchanged, variance segment shrunk to ~1/10, a new covariance segment appearing. Panel 3 (N → ∞): bias² plus covariance only, variance gone — annotate the covariance floor with a horizontal reference line. Shared zero-baseline y-axis for total error across panels so heights are comparable. Use ink for bias², gray for variance, red for covariance (the load-bearing term). Label each segment with its name. Interactive: hovering a segment shows its formula contribution. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

### Figure 6.2 — Tree-based vs. deep-learning methods on medium tabular data

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a horizontal bar chart, one bar per method, ranked by average normalized performance across 45 tabular datasets — a qualitative reproduction of Grinsztajn et al. 2022 Figure 1, not exact values. Sort descending so tree-based methods (GBT, Random Forest, XGBoost) cluster at the top and deep-learning methods (FT-Transformer, ResNet, MLP, SAINT) fall lower. Zero-baseline x-axis. Color tree methods in red (the one data series of interest), deep-learning methods in ink/gray. Title and caption must state this is a qualitative reproduction and `[verify]` against the paper; never present the bar heights as exact published values. Interactive: hovering a bar shows method family and approximate rank. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

### Figure 6.3 — The four-quadrant evaluation checklist for an honest baseline

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a 2×2 grid of equal quadrants: Discrimination (AUC, AUPRC — "can it rank?"), Calibration (reliability curve, Brier score — "does the probability mean what it says?"), Temporal validation (out-of-time split — "does it hold when the future is the future?"), Subgroup robustness (by specialty, decile, geography — "where does it fail?"). Each quadrant shows its metrics and a one-line failure mode if skipped. No axes; this is a layout infographic. Use ink boxes with a thin red accent on the most-skipped quadrant (calibration). Interactive: clicking a quadrant reveals its failure-mode detail. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

---

## Chapter 6 Exercises: Ensembles and the Tabular-Data Advantage

**Project:** One Drug, End to End
**This chapter adds:** A calibrated, leakage-checked propensity baseline for your drug's prescribers, built from public data — the honest AUC that every later claim in the series must beat.

Throughout the series we carry one branded drug end to end. The worked example is **Jardiance (empagliflozin)**, a branded SGLT2 inhibitor in a crowded class — branded competitors (Farxiga, Invokana) alongside cheaper generic alternatives (metformin, sulfonylureas). Every prompt is written for Jardiance and copy-pastes as-is; adaptation notes tell you how to swap in your own drug. This chapter lays the first stone: the propensity baseline.

### Exercise 1 — When to Use AI

You have a public Open Payments and Medicare Part D extract and a target: score each prescriber's propensity to start Jardiance. Hand the AI the mechanical scaffolding.

1. Ask an LLM to draft the join logic that links Open Payments records to Part D prescribing by NPI, plus a stratified out-of-time split harness (train on earlier quarters, test on later ones). *Why AI works here:* code generation against a stated schema — a task type where the output is deterministic and runnable.
2. Have it generate the reliability-curve and per-decile subgroup evaluation plots from your scored predictions. *Why AI works here:* boilerplate visualization from a fixed dataframe — mechanical transformation, not judgment.

**The tell:** you can independently evaluate the output — run the code, read the AUC, eyeball the calibration plot. The result is checkable against ground truth you hold.

### Exercise 2 — When NOT to Use AI

1. Do not let the AI decide your as-of timestamp or clear your Jardiance feature list of leakage on its own. Whether a "recent-fill flag" postdates the prediction point depends on the claims-lag behavior of your specific Part D source — facts not in the model's training data. *Why AI fails here:* ground-truth — the model cannot know your data plumbing, so it will build a beautiful, leaking pipeline (the 0.94-that-should-be-0.78 trap from the opening case).
2. Do not let the AI declare your propensity scores "calibrated." It will read a Brier score back to you as a verdict rather than running the held-out-time reliability check that earns the word. *Why AI fails here:* calibration — co-equal with discrimination for spend decisions and load-bearing for Chapter 8's CATE base learners, and not certifiable from fluent output.

**The tell:** if the AI's claim ("no leakage," "well calibrated") is your *reason* to believe, you have failed; if it is a *tool* whose output you then verify against a time split, you are fine. **Series connection:** this is a **T6** judgment — miscalibration masquerading as accuracy. A propensity score that *looks* accurate but is silently miscalibrated corrupts every downstream uplift and brand estimate in the series. The human owns the leakage and calibration calls.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** an ensemble-baseline memo for Jardiance propensity — target definition, as-of timestamp, feature set with a per-feature leakage check, ensemble and tuning choice, and the four-quadrant evaluation plan.

**Tool:** Claude, run as a **Claude Project**. Persistent drug-context helps because every chapter in this series adds to the same Jardiance case — a Project keeps the drug, class, competitors, and data sources resident so you never re-paste them, and so Chapter 8's uplift work inherits this chapter's baseline definition.

**The Prompt:**

```
You are helping me build the propensity-baseline memo for a running case study on
one branded drug carried end to end. The drug is Jardiance (empagliflozin), a
branded SGLT2 inhibitor for type 2 diabetes. Its class has branded competitors
(Farxiga, Invokana) and cheaper generic alternatives (metformin, sulfonylureas).
Data is PUBLIC ONLY: CMS Open Payments and Medicare Part D Prescriber data, joined
by NPI. No proprietary or patient-level data.

Target: predict whether a prescriber will be a new-to-Jardiance starter in the
quarter following an as-of date of January 1.

Produce a draft memo with these sections, and for the leakage check, ASK ME the
questions you need rather than assuming:

1. Target definition (new-to-brand starter, stated precisely).
2. As-of timestamp and why it matters given claims-processing lag.
3. Candidate feature set from public data (prior Jardiance and class volume,
   Open Payments meal/speaker counts, specialty, geography, trend features),
   and for EACH feature, the one question you'd need answered to rule out that it
   postdates the as-of date.
4. Ensemble choice (default to a gradient-boosted tree ensemble) and why trees are
   the correct baseline on this tabular problem — reference the Grinsztajn et al.
   (NeurIPS 2022) result and its scope conditions.
5. The four-quadrant evaluation plan: discrimination, calibration, out-of-time
   validation, subgroup robustness by specialty and decile.

Flag any claim about competitor pricing or class effects as [verify]. Do not
assign a final calibration verdict — describe the check I must run myself.

ADAPTATION: to use your own drug, replace Jardiance with your branded drug, its
class, its branded competitors, and its generic alternatives, and keep everything
else. To run in ChatGPT or Gemini, paste the drug context at the top of each
session since they lack a persistent Project.
```

**What this produces:** a structured baseline memo with a feature-by-feature leakage interrogation — the exact artifact Chapter 7's vendor audit and Chapter 8's uplift work build on.

**How to adapt:** swap the drug block for your own brand; in ChatGPT/Gemini re-paste the drug context each session; in a Claude Project, save the drug block as Project knowledge so it persists.

**Connection to previous chapters:** the memo operationalizes the vendor-claim skepticism from Chapters 1 and 5 — instead of grading someone's number, you build the honest one.

**Preview of next chapter:** this baseline AUC is literally the bar a vendor's "Mixture of Experts" claim must clear in Chapter 7's sixth buyer question.

### Exercise 4 — CLI Exercise

**What you're building:** a concrete measurement of the claims-lag illusion in your own extract — the date distribution between service date and recorded date.

**Tool:** Claude Code (or Cowork) — it can read your local CSVs, run shell tooling, and write a short script in one loop. **Skill level:** beginner-to-intermediate (comfortable running a notebook or `awk`).

**Setup:**
- [ ] A public Part D extract (or a synthetic claims file) with a service-date and a recorded/adjudicated-date column in your working directory.
- [ ] `csvkit` or Python+pandas available.
- [ ] A scratch folder for outputs; nothing else writable.

**The Task:**

```
Read ONLY the claims CSV in ./data/ (do not modify it). Compute the distribution
of (recorded_date - service_date) in days. Then, assuming a hypothetical Jardiance
marketing-exposure window of the most recent 90 days, COUNT how many records fall
inside a naive "post-exposure" outcome window but have a SERVICE date that predates
the exposure window start — i.e., scripts that look like responses but were written
before the contact.

Write the day-lag histogram and the contaminated-record count to
./outputs/claims-lag-report.txt. Do not write anywhere else. Do not alter the
source CSV. Stop when the report file exists, then print its contents so I can
verify the numbers myself.
```

**Expected output:** a histogram of recording lag plus a single count of fills that would inflate naive Jardiance "lift" purely through bookkeeping.

**What to inspect:** is the contaminated-record count non-trivial? Does the lag distribution have a long tail past 90 days? Confirm the source CSV's modification time is unchanged.

**If it goes wrong:** if Claude Code edits the source CSV (failure), recover from your untouched copy and re-run with the read-only scope restated; if it invents a lag column that does not exist, point it at the real column names and re-run.

**CLAUDE.md note:** add `Treat all files in ./data/ as read-only source data; write only to ./outputs/.`

### Exercise 5 — AI Validation Exercise

**What you're validating:** the evaluation report the AI produced for your Jardiance baseline (from Ex3/Ex4) — specifically whether its "calibrated, leakage-free, validated" framing survives scrutiny.

**Validation type:** correctness-and-calibration audit of a generated analytic artifact. **Risk level:** high — because a miscalibrated propensity score silently corrupts the entire downstream series (uplift in Ch8, brand work in Ch9), and the failure is invisible in fluent output.

**Setup:** use your Ex3 memo and Ex4 report. If you need a specific failure to practice on, have the AI generate a deliberately flawed evaluation that reports AUC from a *random* (not time) split and calls the model "well calibrated" on the strength of a single Brier number.

**The Validation Task:**

```
Validation Checklist — Chapter 6 (Jardiance propensity baseline)

Mark each Pass / Fail / Cannot-determine:
- Correctness: Is the reported AUC computed on an out-of-TIME split, not a random
  shuffle?
- Completeness: Are all four evaluation quadrants present (discrimination,
  calibration, out-of-time, subgroup)?
- Scope: Does every feature use only public, pre-as-of-date data?
- Calibration criterion: Is there a reliability curve on a HELD-OUT TIME split, not
  just a Brier scalar?
- Subgroup criterion: Is performance broken out by decile, exposing any low-decile
  failure the aggregate hides?
- Failure-mode check: Look specifically for miscalibration-masquerading-as-accuracy
  — a fluent "well-calibrated" claim backed only by a single number — and for any
  missing ground truth (a claim of "no leakage" with no stated as-of check).
```

**What to do with findings:** all Pass — the baseline is defensible and becomes the series anchor. One Fail — fix that layer (re-run the time split, add the decile breakout) and re-validate. Multiple Fails — discard the AI's verdict, rebuild the evaluation yourself, and treat the original report as a fluency-trap exhibit.

**AI Use Disclosure prompt:** *Write two sentences naming exactly what the AI did and the one judgment it could not make. Example: "I used Claude to draft the join logic and the four-quadrant evaluation harness for the Jardiance baseline; I decided which features leak and whether the scores were truly calibrated, because that requires the claims-lag knowledge of my specific Part D source and a held-out-time reliability check the model cannot certify."* (Mandatory.)

**Series connection:** the failure mode here is **miscalibration-masquerading-as-accuracy** at tier **T6** — the same class of silent error that, uncaught, propagates into every downstream chapter of the One Drug case.
