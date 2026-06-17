# Chapter 8 — Uplift and Incrementality: Measuring Real Lift
*The model that predicts everything changes nothing.*

A platform reports a triumph. Physicians who received its AI-selected next-best-action message grew their new-to-brand prescriptions by 44% over the campaign window. The deck calls this "44% script lift." The number is real in the narrow sense that the arithmetic checks out. It is also almost certainly the wrong number, and you can show why with one move: ask where the holdout is.

`[the 44% figure is illustrative of the vendor range; verify against primary sources before citing]`

Here is what the 44% actually compares. The exposed physicians were the highest-propensity targets — the platform deliberately picked the doctors most likely to prescribe. Their post-campaign NBRx is being measured against their own prior period, or against unexposed low-propensity physicians who were never comparable in the first place. Three biases compound simultaneously. The first is targeting on the outcome: the treated group was selected *because* it was going to prescribe, so its growth is partly the growth it would have shown untreated. The second is regression to the mean and secular trend: the brand was already growing, and physicians selected at a high point drift back toward their average over time. The third is attribution circularity: the platform that served the ad also measured the lift, on its own data, with no independent firewall.

Now draw a holdout. Randomly withhold the message from a fraction of that *same* high-propensity target list. Measure incremental NBRx as treated-mean minus holdout-mean. The honest number is the gap between two comparable groups — and it is typically a fraction of 44%, sometimes inside the noise of zero.

The 44% was not fabricated. It was the answer to a different question. This chapter is about asking the right one.

---

Start with the inversion, because the whole chapter lives inside it.

Propensity answers one question: how likely is this physician to prescribe, given what we know about them? Incrementality answers a different question: how much did the prescription probability change *because of what we did*? These feel related. They come apart violently at the top of the propensity scale.

A physician with 95% propensity has almost no room to be moved. She would very likely prescribe anyway. The intervention's incremental return on her is near zero even though the model is certain about her. The incremental return on any campaign lives not among the predictable but among the **persuadable** — the physicians who are genuinely on the fence, for whom the message tips something.

This is why targeting on propensity and then measuring the treated group's outcome systematically inflates apparent lift. The high-propensity targets were going to prescribe regardless of what you did. Their prescribing gets credited to the campaign. The model you built to predict them was doing its job. The mistake was using a prediction model to answer a causation question.

A great predictor can be a terrible intervention target. Keep that sentence nearby. It is the inversion this chapter is built on, and it resolves the opening case in one step.

<!-- → [DIAGRAM: Two-axis plot — x: propensity score (0 to 1), y: incremental effect (CATE); curve peaks in the middle persuadable range and is near zero at both tails; annotations at high-propensity end read "sure things — wasted spend," at low end "lost causes — wasted spend," in middle "persuadables — the only profitable target"] -->

---

The reason incrementality is hard is not statistical fussiness. It is logical, and understanding the logic matters before you trust any method that claims to solve it.

For any single physician, you could in principle observe $Y(1)$ — their prescribing if exposed — or $Y(0)$ — their prescribing if not exposed. You cannot observe both at the same time. The individual treatment effect, $Y(1) - Y(0)$, is unobservable *in principle.* Not because we lack data. Because the physician can only be in one world at once.

This is the fundamental problem of causal inference. It is not a problem that more data solves, or that a better algorithm solves. It is a structural feature of how time works. Any method that claims to estimate individual-level treatment effects is really estimating something slightly different: an average over physicians who are similar in measurable ways, in the hope that the unmeasured ways cancel out.

Because the individual effect is unrecoverable, we settle for averages over comparable groups. The **average treatment effect** is $E[Y(1) - Y(0)]$ across a population — the mean lift, if you could run the experiment on everyone. The **conditional average treatment effect**, or **CATE**, is $E[Y(1) - Y(0) \mid X = x]$ — the effect conditional on a physician's covariates. CATE is the heterogeneous, individualized quantity that uplift modeling targets: it is why two physicians with different features get different predicted lifts from the same campaign. The marketing term "uplift modeling" and the econometrics term "CATE estimation" describe the same task in two vocabularies.

<!-- → [TABLE: Terminology bridge — three columns: marketing term, econometrics term, what it means in plain language; rows: uplift model / CATE estimator / predicts the effect of treatment for a given physician; propensity score / P(treat|X) / probability of being treated; lift / ATE / average effect across the population; persuadables / high-CATE subgroup / physicians where the treatment actually moves the needle] -->

---

Averaging only recovers a causal effect when the groups being compared are genuinely comparable. Three assumptions do that work, and each deserves to be understood at first use rather than memorized as a checklist.

**Unconfoundedness** — also called conditional exogeneity — means treatment is as-good-as-random given the covariates. A randomized holdout satisfies this by design: you flipped a coin, so there is no systematic difference between treated and held-out physicians beyond what the coin decided. Observational vendor "lift" merely *assumes* unconfoundedness — it assumes the exposed and unexposed groups are comparable after you condition on whatever features the model observed. That assumption is almost always violated in a targeting context, because targeting is the opposite of random. The platform selected the exposed group precisely because they were different from the unexposed group.

**Overlap**, or positivity, requires that treated and control physicians both exist across the covariate space. If every high-decile physician is treated and every low-decile physician is not, there is no overlap — nothing to compare at the top of the distribution where the action is. Without overlap, any estimated effect is extrapolated, not observed.

**SUTVA**, the stable unit treatment value assumption, says one physician's exposure does not change another's outcome. This is shaky in pharma. Key opinion leaders, shared practices, and referral networks all create spillover: a message that activates a high-volume prescriber at an academic medical center may diffuse through residents, fellows, and community physicians who share the workflow. Spillover inflates lift estimates in the treated cluster and deflates lift estimates in adjacent controls. It is the assumption that matters most in real pharma networks and gets stressed least in vendor methodology decks.

A **randomized holdout** is the cleanest instrument because it buys unconfoundedness directly. Randomly withhold the intervention from a subset of the target list; the holdout *is* the counterfactual. Every other method in this chapter is either an approximation to the holdout or a way to extract causal signal when a holdout is not available. None is as decisive as that single design move.

---

When you cannot randomize at will — or when you want to estimate heterogeneous effects from data you already have — you reach for CATE estimators. Know them and their failure modes; the derivations matter less than the intuition.

**Meta-learners** wrap any base learner — typically a gradient-boosted tree, which means the Chapter 6 baseline is literally the engine running inside them — and use that learner to estimate treatment effects.

The **S-learner** fits one model with treatment as a feature. Simple and often badly behaved: if the treatment signal is weak, a regularized base learner may shrink the treatment coefficient toward zero and miss the effect entirely.

The **T-learner** fits two separate models — one on the treated group, one on the control group — then differences their predictions. This works cleanly when groups are balanced. With imbalanced treatment assignment (which is typical in pharma targeting), the two models train on unequal sample sizes and the variance in the difference can overwhelm the signal.

The **X-learner** handles imbalance by cross-imputing: it estimates what each treated physician *would have* done in the control condition using the control model, and vice versa, then averages the imputed individual effects. It is stronger than the T-learner specifically when group sizes are unequal — which is almost always.

The **R-learner** takes a different route: it residualizes out the propensity and the baseline outcome using auxiliary nuisance models, then regresses the residualized outcome on the residualized treatment. The double residualization (Neyman-orthogonal) makes it robust to misspecification in either the propensity or the outcome model — and that robustness is worth the added complexity. [Nie & Wager, 2021 — verify cite]

**Causal forests** — from Wager and Athey [JASA 2018 — verify cite] — take a tree-based approach that splits on treatment-effect heterogeneity directly rather than outcome heterogeneity. They produce a CATE estimate with non-parametric confidence intervals at each leaf. One honest caveat to carry with them: causal-forest inference is theoretically valid mainly in low-dimensional settings and "can be more brittle... not as assumption-lean as inference based on OLS" in high dimensions. Do not oversell causal forests as assumption-free. They are not.

**Doubly-robust methods**, including the DR-learner, are consistent if *either* the propensity model or the outcome model is correctly specified — a practical safety net for observational CATE when you are not confident in either model alone.

Which estimator wins on your data is empirical, dataset-dependent, and not answerable in advance. A large benchmark on industrial marketing data compared S/T/X-learners and causal forests and found no universal winner; calibration and ranking quality matter as much as the estimator family. `[verify the Criteo Uplift v2.1 benchmark conclusions against the primary arXiv source]` Treat "which CATE estimator is best" as a question you test, not a setting you assume.

<!-- → [TABLE: CATE estimator comparison — rows: S-learner, T-learner, X-learner, R-learner, causal forest, DR-learner; columns: key idea, when it works best, when it breaks, one-line failure mode] -->

---

Now the evaluation problem, which is harder than the estimation problem.

You cannot score an uplift model with ordinary accuracy, because the thing you are predicting — the individual treatment effect — is never observed. You cannot check whether your predicted CATE for physician A was right, because you can only observe one of her two potential outcomes. If you treated her, you see $Y(1)$ but not $Y(0)$. If you didn't, you see $Y(0)$ but not $Y(1)$. The individual label is always missing.

The standard solution is the **uplift curve** and its summary statistic, the **Qini coefficient**. Rank physicians by predicted uplift from highest to lowest. As you descend the ranking, plot the cumulative incremental response: treated-minus-control outcome, accumulated as you go down the list. A model that correctly identifies the persuadables concentrates incremental response at the top — the curve bows upward above the random-targeting diagonal. The Qini coefficient is the area between the model curve and the diagonal; more area means better uplift targeting.

The intuition to hold: a useful uplift model lets you spend on the persuadables and skip the sure things. If a model cannot concentrate incremental response at the top of its ranking, it has not learned to distinguish persuadables from sure things, and it will not improve on random targeting even if its propensity predictions are excellent.

<!-- → [CHART: Uplift/Qini curve — x-axis: fraction of population targeted (0–1), y-axis: cumulative incremental response; three curves: perfect model (steep rise then flat), actual model (intermediate bow), random targeting (diagonal); shaded area between actual and diagonal labeled "Qini coefficient"; annotation: "sure things live below the knee; persuadables live above it"] -->

---

If you remember one picture from this chapter, make it this one.

Cross two binary questions: does this physician prescribe if treated? Does this physician prescribe if untreated? Four groups fall out.

**Persuadables** prescribe only if treated. They are the only group where the intervention produces a net gain. Every campaign dollar should be fighting its way toward them.

**Sure things** prescribe regardless of treatment. Treating them is wasted spend — and crediting their scripts to the campaign is precisely how a 44% figure gets built from a campaign that may have done nothing incremental at all.

**Lost causes** won't prescribe either way. Also wasted spend, for different reasons.

**Sleeping dogs** — sometimes called do-not-disturbs — are the counter-intuitive quadrant: treatment actively *reduces* the outcome. The message backfires. This happens in pharma contexts: a co-pay card for a drug a physician already resists prescribing on grounds of clinical inappropriateness may harden the resistance. A message that arrives in a crowded EHR workflow at the wrong moment may generate negative associations rather than positive ones. The sleeping-dog quadrant is a warning that uplift is directional, and that intervention can be harmful.

Targeting on high propensity targets the sure things. Uplift targeting targets the persuadables. That reframing is the chapter's entire argument in business language.

<!-- → [DIAGRAM: Persuadables 2x2 — axes: "prescribes if treated" (yes/no) and "prescribes if untreated" (yes/no); four quadrants labeled persuadables, sure things, lost causes, sleeping dogs; arrows from "propensity targeting" pointing to sure-things quadrant; arrows from "uplift targeting" pointing to persuadables quadrant] -->

---

A Fellow working with public data cannot run a live randomized holdout on a vendor's targeting system — that requires live infrastructure and a commercial partnership. But causal claims are still reachable through **natural experiments**, where a policy change acts as an as-good-as-random shock to exposure.

The flagship pharma example is academic medical center detailing restrictions. Larkin and colleagues [*JAMA* 2017 — verify 317(17):1785–1795] ran a difference-in-differences study on 19 AMCs across five states that restricted sales-rep detailing between 2006 and 2012 — 2,126 affected physicians against 24,593 matched controls, across 262 drugs in 8 classes. Restricting detailing produced modest but significant reductions in detailed-drug prescribing in 6 of 8 classes, with physicians shifting from expensive patent-protected drugs toward cheaper generics. The effect concentrated in AMCs whose policies had enforcement teeth. A related study found AMC marketing restrictions associated with lower opioid prescribing — a patient-welfare-relevant variant. `[verify journal and year of the opioid study]`

The template generalizes. The policy change is the shock; neighboring or matched physicians are the control. State disclosure laws, formulary changes, loss of exclusivity, and payment thresholds all supply credible counterfactuals without a vendor's cooperation. The public-data route to causal claims runs through these shocks, and Chapter 12 develops their identifying assumptions in detail.

The honesty caveat, modeled explicitly: natural experiments are not automatically clean. Difference-in-differences rests on a parallel-trends assumption — that treated and control physicians were on the same trajectory before the policy change — and any co-occurring shock can confound the estimate. Quasi-experiments buy you a counterfactual. They do not buy you certainty. They buy you a *defensible argument* that the groups were comparable before the shock, which you must make in plain language and subject to scrutiny.

---

Here is what the opening case would look like with the right design.

Take the next-best-action campaign and design the readout it should have had. From the high-propensity target NPI list, randomly withhold the message from 15% of physicians before the campaign launches — this is the holdout, drawn from the same propensity stratum. Define a single primary outcome: incremental NBRx over a fixed window, with claims-lag accounting so you are not measuring scripts the pipeline hasn't reported yet. Compute incremental scripts as treated-mean NBRx minus holdout-mean NBRx, per physician, over that window. Fit an X-learner with a gradient-boosted base on the treated and held-out data. Plot the Qini curve to see which physicians carried the incremental response.

The headline collapses toward the holdout-corrected number, because the holdout strips out the three compounding biases from the opening case: it is drawn from the same propensity stratum, so targeting-on-outcome is gone; it experiences the same secular trend as the treated group, so trend confound is gone; and it is a randomized comparison rather than a self-referential platform baseline, so circularity is gone. The Qini curve then identifies where the campaign's real value was concentrated — in a persuadable minority — which is useful information for the next campaign's targeting.

The limits worth naming. SUTVA can fail if treated and held-out physicians share a practice and talk. The window choice trades claims-lag bias against secular-trend bias. The holdout costs the brand the scripts it forgoes among true persuadables in the held-out group. A holdout is the gold standard, not a free lunch. And on public data you cannot run one at all — which is why the natural-experiment route exists, and why the absence of a peer-reviewed randomized evaluation of EHR advertising is the chapter's standing open question.

---

**Five-Part AI Exercise Block**

**When to use AI here.** Use an LLM to scaffold an analysis plan — which estimator, which assumption checks — to draft code for a holdout computation or a Qini curve, and to explain an unfamiliar estimator (say, the R-learner's residualization) in plain language before you read the primary paper.

**When NOT to use AI here.** Do not let an LLM certify that an effect is causal. It will accept a before/after comparison as evidence if you phrase it confidently, and it cannot judge whether parallel trends hold in your data or whether a co-occurring policy change confounds your natural experiment. Identification is a human argument about the world, not a property of the code.

**LLM exercise (copy-paste prompt):**
> "Here is a 'lift' claim: [PASTE CLAIM]. List every reason this number might overstate the causal effect — name targeting-on-outcome, regression to the mean, attribution circularity, and absence of a control if they apply. Then state the minimal design that would make it credible."

Check whether the model named all three compounding biases from the opening case, or stopped at a generic "needs more data."

**CLI exercise.** On a public dataset with a treatment indicator and an outcome, compute: (a) naive before/after lift for the treated group; (b) holdout-corrected incremental effect as treated-mean minus control-mean. Report both numbers side by side. The gap between them is the chapter in one table. Note what fraction of the naive lift the holdout-corrected number represents.

**AI validation.** Ask an LLM to estimate a treatment effect from observational data. Then independently check whether the unconfoundedness assumption it relied on is plausible given how treatment was assigned in that dataset. Log where the model assumed randomness the data did not have, and note whether it flagged the assumption or silently incorporated it.

**AI Use Disclosure**

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to draft the code for the Qini curve computation and to scaffold the natural-experiment design; I determined myself whether the parallel-trends assumption was defensible in my data, because the model cannot reason about whether a co-occurring policy change confounded my estimate."*

---

**What Would Change My Mind**

The chapter's position is that propensity-based lift is structurally inflated and that incrementality requires a control. A pre-registered randomized holdout — or a well-identified natural experiment with a defensible parallel-trends argument — showing a meaningful incremental effect that survives claims-lag accounting and subgroup checks would move a specific channel from "unknown" toward "evidenced." The position is not "all lift claims are false." It is "a lift claim without a counterfactual is unproven." Show the counterfactual, and the verdict flips on evidence. One such study on EHR advertising, run by an independent party, would substantially change the chapter's treatment of that channel.

**Still Puzzling**

- No peer-reviewed, randomized evaluation of EHR/point-of-care advertising exists. We genuinely do not know the true incremental effect of a co-pay message firing inside the clinical workflow. Until that study is run and published, the fastest-growing channel in pharma marketing rests on the thinnest causal evidence.
- The persuadables quadrant is theoretically clean. In practice, how do you find persuadables without first running the experiment that reveals them? The answer involves iterative holdout design and Bayesian updating across campaigns, and the industry is early in working it out.
- SUTVA fails in any network with spillover. In pharma, key opinion leader networks are precisely the mechanism of diffusion that makes marketing work — which means the assumption that validates the holdout may be violated at exactly the points where the effect is largest.

---

## Exercises

**Warm-up**

1. *(Factual recall — the inversion)* Explain, in two sentences, why targeting the highest-propensity physicians and measuring their post-campaign outcomes overstates incremental lift. Name the specific quadrant of the persuadables 2×2 that "wasted spend that looks like success" comes from.
   *What this tests: whether you can state the propensity-vs-incrementality inversion in plain language.*

2. *(Factual recall — identification assumptions)* Name the three assumptions required for a comparison to recover a causal effect. For each, state in one sentence whether a randomized holdout satisfies it by design or merely assumes it.
   *What this tests: the logical structure of causal identification, not memorized labels.*

3. *(Factual recall — evaluation)* Why can't you score an uplift model with ordinary accuracy? What does the Qini coefficient measure, and what does a higher Qini value tell you about a model's practical usefulness?
   *What this tests: the fundamental evaluation problem in uplift and the intuition behind the Qini curve.*

**Application**

4. *(Apply — critique a claim)* A vendor reports that physicians who received a co-pay assistance message wrote 31% more new-to-brand prescriptions than physicians who did not. Write a critique that names the three compounding biases from this chapter and states the single design change that would fix the estimate.
   *What this tests: applying the opening-case analysis to a new claim.*

5. *(Apply — estimator selection)* A brand team ran a campaign where 90% of high-propensity physicians were treated and 10% were held out. They want to estimate CATE using the holdout data. Which meta-learner is most appropriate given the imbalanced group sizes, and why? Name one alternative and its failure mode in this setting.
   *What this tests: applying the estimator taxonomy to a realistic data condition.*

6. *(Apply — natural experiment design)* A state passes a law restricting pharmaceutical sales-rep visits to academic medical centers, effective on a known date. Sketch a difference-in-differences design using this as a natural experiment: name the treated group, the control group, the identifying assumption, and the single biggest threat to that assumption.
   *What this tests: translating the natural-experiment concept into a concrete design with named assumptions.*

**Synthesis**

7. *(Synthesize — persuadables and Qini)* A campaign ran with a randomized holdout. The uplift model's Qini curve shows that the top 20% of predicted-uplift physicians account for 80% of the measured incremental response. The remaining 80% of targeted physicians are in the persuadables-or-worse range. What does this tell you about the campaign's efficiency, and what would you recommend for the next targeting pass?
   *What this tests: reading a Qini result as a business input, connecting uplift measurement back to targeting decisions.*

8. *(Synthesize — design for your thread)* For your research thread from Chapter 2, design either a randomized holdout (if a live system is in scope) or a natural-experiment study (on public data) with: the primary incrementality outcome, the comparison group, the identifying assumption you are relying on, and the threat to that assumption you most worry about.
   *What this tests: integration across Chapter 2 (dependent variable) and Chapter 8 (identification) — the Part B checkpoint for this unit.*

**Challenge**

9. *(Open-ended — SUTVA and networks)* The chapter notes that SUTVA fails when physician networks create spillover. Propose a study design — using public data or a realistic hypothetical — that would (a) estimate how much spillover exists in a specific pharma marketing context and (b) correct the holdout-based incremental estimate for spillover contamination. Name the data you would need and the assumption your correction relies on.
   *What this tests: pushing past the standard holdout design to a harder real-world problem, and identifying the assumption that the fix introduces.*
