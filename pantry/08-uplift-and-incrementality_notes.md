# Chapter 8 — Uplift and Incrementality: Measuring Real Lift · Research Notes

> Gathering notes only (no chapter prose). Format A–G.
> Chapter spine (HARDEST CONCEPTUAL MOMENT): move from "who will prescribe?" (propensity) to "whose
> behavior changed *because of* the intervention?" (uplift / incrementality). Treatment/control,
> holdouts, the fundamental problem of causal inference, heterogeneous effects (CATE), natural
> experiments, why vendor "lift" without a control is structurally inflated.
> Primary sources: web research (uplift/CATE methods, pharma natural experiments) +
> `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md` (potential outcomes, S/T/X/R-learners,
> causal forests, uplift curves) + `_lib_science-randomistas` (RCT logic) + both pharma syntheses
> (attribution circularity, EHR gap). Web-verified 2026-06-16.

---

## A. Conceptual foundations

**The inversion (the chapter's whole point).** A good *predictor* of prescribing is not a good
*intervention target*. Propensity answers P(prescribe | physician features). Incrementality answers
P(prescribe | treated) − P(prescribe | untreated) *for the same physician*. A physician with 95%
propensity has little room to be moved (and would likely prescribe anyway); the incremental return
lives among the *persuadable*, not the *predictable*. Targeting on propensity and measuring the
treated group's outcome therefore systematically *inflates* apparent lift — the high-propensity
targets were going to prescribe regardless. (This is the formal resolution of Ch 5's association-vs-
causation problem.)

**The fundamental problem of causal inference (Rubin potential outcomes).** For any physician we can
observe either Y(1) (prescribing if exposed) or Y(0) (if unexposed) — never both at once. The unit-
level treatment effect Y(1) − Y(0) is unobservable in principle. We recover *averages* only by making
groups comparable. [VERIFIED, _lib_causal-inference §"fundamental problem": "for any given unit we can
never observe both Y1 and Y0 at the same time… causal questions are inherently comparative."]
- **ATE** = E[Y(1) − Y(0)] (average over population).
- **CATE / uplift** = E[Y(1) − Y(0) | X = x] (conditional on physician covariates — the heterogeneous,
  individualized effect uplift modeling targets). "Uplift modeling" and "CATE estimation" are the same
  task under two vocabularies (marketing vs. econometrics). [VERIFIED via web: causalml docs;
  arxiv 2604.06123.]

**Identification: what makes a comparison causal.** Required assumptions (taught at first use):
- **Unconfoundedness / conditional exogeneity**: treatment is as-good-as-random given X. Satisfied by
  design in an RCT/holdout; *assumed* (and usually violated) in observational vendor "lift."
- **Overlap / positivity**: treated and control physicians exist across the covariate space.
- **SUTVA / no interference**: one physician's exposure doesn't change another's outcome (shaky in
  pharma — KOLs, shared practices, spillover).
A randomized **holdout** buys unconfoundedness directly: randomly withhold the intervention from a
subset of the target list; the holdout *is* the counterfactual.

**Uplift / CATE estimation families (the toolkit to name):**
- **Meta-learners** (any base learner, e.g. LightGBM/XGBoost):
  - *S-learner* — one model, treatment as a feature. Simple; can wash out a weak treatment signal.
  - *T-learner* — two separate models (treated, control); differences them. Variance issues with
    imbalanced groups.
  - *X-learner* — imputes individual effects cross-wise; strong with unequal group sizes.
  - *R-learner* — residualizes out the propensity/outcome nuisance (Robinson-style), Neyman-orthogonal.
  [VERIFIED via web: causalml docs; matheusfacure handbook ch.21; _lib_causal-inference §15.1
  "Meta-Learning Strategies for CATE Estimation."]
- **Direct / tree-based**: uplift trees, **causal forests** (GRF formulation) — split on treatment-
  effect heterogeneity, give CATE + non-parametric confidence intervals. *Caveat the chapter should
  keep* [VERIFIED, _lib_causal-inference §14.3]: causal-forest inference is theoretically valid only
  when X is low-dimensional and "in practice can be more brittle… not as assumption-lean as inference
  based on OLS." Don't oversell it.
- **Doubly-robust / DR-learner**: consistent if *either* the propensity model *or* the outcome model
  is right — the practical safety net for observational CATE.

**Evaluation (you cannot use ordinary accuracy — the label is unobservable).** Use **uplift/Qini
curves**: rank units by predicted uplift, plot cumulative incremental response of treated-minus-
control as you descend the ranking; area between the curve and the random line is the Qini coefficient.
[VERIFIED via web (matteocourthoud "Evaluating Uplift Models") + _lib_causal-inference §15.B "Appendix:
Interpretation of Uplift curves."]

---

## B. Domain examples + a failure case

**Worked examples:**
- **The honest holdout for an NBA / trigger campaign.** Randomly withhold the next-best-action message
  from X% of the target NPI list. Incremental scripts = (treated mean NBRx) − (holdout mean NBRx),
  per physician over a defined window with claims-lag accounting. The headline "lift" the platform
  reports collapses toward (often to) the holdout-corrected number — the TIKTOC opening: "a
  next-best-action lift number that evaporates against a proper holdout."
- **Persuadables vs. sure things (uplift segmentation).** Classic 2×2: persuadables (prescribe only if
  treated — the only profitable target), sure things (prescribe regardless — wasted spend), lost
  causes (won't prescribe either way), sleeping dogs / do-not-disturbs (treatment *reduces* the
  outcome). Targeting high-propensity = targeting sure things. Uplift targets persuadables.
- **Natural experiment — academic-medical-center detailing restrictions (the flagship pharma quasi-
  experiment).** [VERIFIED via web 2026-06-16] Larkin, Loewenstein et al., *JAMA* 2017
  (pubmed 28464141): difference-in-differences on 19 AMCs across 5 states that restricted rep detailing
  (2006–2012); 2,126 affected physicians vs. 24,593 matched controls; 262 drugs across 8 classes.
  Finding: modest but significant reductions in detailed-drug prescribing in 6 of 8 classes; physicians
  switched from expensive patent-protected drugs to cheaper generics; effect concentrated in AMCs with
  *enforcement teeth* (access limits + gift bans + enforcement). A clean template for Ch 12
  identification: policy change = as-good-as-random shock; neighbor/matched physicians = control.
- **Related natural experiment — opioid prescribing under AMC marketing restrictions.** [VERIFIED:
  pubmed 32479218, *Health Affairs* / related] AMC policies restricting direct-to-physician marketing
  associated with lower opioid prescribing — a patient-welfare-relevant variant.
- **Other natural-experiment shocks (TIKTOC Ch 12 menu):** state disclosure laws, formulary changes,
  loss-of-exclusivity (LOE / generic entry), payment thresholds (RDD). Each gives a credible
  counterfactual without a vendor's cooperation.

**Failure case (the discipline made vivid).** *The inflated "44% lift" with no control.* A platform
reports exposed high-decile prescribers grew NBRx 44% vs. their own prior period (or vs. unexposed
low-propensity physicians). Three compounding biases: (1) targeting-on-outcome — the exposed were the
highest-propensity targets; (2) regression to the mean + secular trend — the brand was already growing;
(3) attribution circularity — the platform that served the ad measured the lift on its own data (Ch 5).
A holdout drawn from the *same* high-propensity stratum, randomly assigned, would show the incremental
effect is a fraction of 44% — often within noise of zero. The number isn't fabricated; it's the wrong
estimand. [The 44% figure is illustrative/vendor-range; label + [verify].]

---

## C. Connections / dependencies

- **Depends on Ch 2** (lift defined: TRx/NRx/NBRx, new starts) and **Ch 5** (the evidence frame;
  association vs. causation) — TIKTOC prereq map lists Ch 8 as depending on 2 and 5.
- **Depends on Ch 6** (ensembles): uplift meta-learners *use* gradient-boosted trees as base learners,
  so the Ch 6 baseline is literally the engine inside S/T/X/R-learners. Calibration (Ch 6) matters
  doubly here.
- **Contrast with Ch 3/6/7** (propensity): the chapter's job is to break the instinct those chapters
  built — predicting a prescriber ≠ moving one.
- **Bridges to Ch 9** (brand): "lift is activation; does the intervention also build durable brand
  belief?" Uplift measures the short-run script change; brand association (Ch 9) measures the durable
  shift — different estimands, different designs.
- **Feeds Ch 11–12 directly**: holdout design = Evidence Ladder Level 4 ("prospective pilot or holdout
  study → product resourcing"); a Fellow on *public* data tops out at Level 3 (offline test beating
  baseline), because true holdouts require the partner's live targeting — *that boundary is the IP
  firewall made operational.* Natural experiments (Larkin/Loewenstein) are the Ch 12 public-data path
  to causal claims *without* a live holdout.
- **Research thread (TIKTOC Track A)**: no peer-reviewed study has evaluated EHR/point-of-care
  advertising with a randomized/pre-registered design — the incrementality gap is the lift-side
  research opening.

---

## D. Current state (settled / contested / key refs / last-3-yr)

**Settled:**
- Fundamental problem of causal inference; potential-outcomes framework (Rubin/Neyman) — foundational,
  uncontested.
- Holdout/RCT is the gold standard for incrementality; propensity ≠ incrementality.
- Meta-learner taxonomy (S/T/X/R) and causal forests are standard, implemented in mature open-source
  (EconML, causalml, grf). [VERIFIED via web.]
- AMC detailing restrictions reduced branded/detailed prescribing (Larkin *JAMA* 2017) — peer-reviewed,
  DiD, widely cited.

**Contested / active research:**
- *Which* CATE estimator wins in practice is empirical and dataset-dependent. [VERIFIED via web 2026:
  arxiv 2604.06123 "A Large-Scale Empirical Comparison of Meta-Learners and Causal Forests… in
  Marketing Uplift Modeling" — benchmarks S/T/X-learner (LightGBM) + Causal Forest (EconML) on Criteo
  Uplift v2.1, 13.98M records. No universal winner; calibration + ranking matter as much as the
  estimator.] Use as "the method choice is itself an empirical question" — not "X-learner is best."
- Causal-forest inference brittleness in high dimensions (see A caveat).
- Vendor "lift" attribution remains un-validated independently (Ch 5 carryover).

**Key references (verify before publication):**
- Larkin I, et al. "Association Between Academic Medical Center Pharmaceutical Detailing Policies and
  Physician Prescribing." *JAMA.* 2017;317(17):1785–1795. [VERIFIED exists, pubmed 28464141.]
- AMC marketing restrictions + opioid prescribing. [VERIFIED, pubmed 32479218; confirm journal/year —
  *Health Affairs* 2020 likely.]
- Künzel, Sekhon, Bickel, Yu. "Metalearners for estimating heterogeneous treatment effects." *PNAS*
  2019 (S/T/X-learner). [FLAG: not in lib; standard citation — add.]
- Wager & Athey. "Estimation and Inference of Heterogeneous Treatment Effects using Random Forests."
  *JASA* 2018 (causal forests). [FLAG: add citation.]
- Nie & Wager. "Quasi-oracle estimation of heterogeneous treatment effects" (R-learner), 2021. [FLAG.]
- Gutierrez & Gérardy, "Causal Inference and Uplift Modelling: A Review," 2017. [FLAG: add.]
- _lib_ai-applied-causal-inference-powered-by-ml-and-ai.md ch.14–15 (CATE, causal forests, uplift
  curves, meta-learners) — primary in-library grounding.

**Last-3-yr:** large-scale empirical uplift benchmarks on industrial marketing data (Criteo) maturing
(2024–2026); causal ML tooling (EconML, causalml) now production-standard. The pharma *incrementality
holdout* practice exists internally at sophisticated advertisers/measurement vendors (Veeva Crossix
positions on HCP-level attribution) but the *methods are not independently audited* (pharma-ai
synthesis §6, §8).

---

## E. Teaching considerations

- **TIKTOC flags this the hardest conceptual moment.** Teaching order that works: (1) show a lift
  number; (2) introduce a holdout and watch it shrink ("teach with a holdout that fails first" — per
  TIKTOC Hard Chapters); (3) only *then* name potential outcomes and CATE. Concept follows the felt
  surprise, not the other way round.
- **The persuadables 2×2** is the single most retainable intuition — leads with business logic, not
  math. The "sleeping dogs" quadrant (treatment backfires) is the memorable counter-intuitive case.
- **Keep the math honest but bounded** (the reader is data-capable, not a causal-inference PhD): name
  S/T/X/R-learners and causal forests and *when* each is used; do not derive Neyman orthogonality.
  Route depth to the _lib_ causal-inference text + EconML/causalml docs in Further Reading.
- **Public-data ceiling is a teaching feature, not a limitation.** The Fellow cannot run a live
  randomized holdout on a partner's targeting system on public data (Level 4) — so teach the *natural-
  experiment* substitute (Larkin/Loewenstein DiD on Open Payments + Part D) as the public-data route to
  a causal claim. This makes the IP firewall concrete and sets up Ch 12.
- **Honesty caveat to model:** even natural experiments rest on assumptions (parallel trends for DiD,
  no confounding policy co-shock). Don't present quasi-experiments as automatically clean.
- **Bridge (TIKTOC):** "lift is activation; does the intervention also build durable brand belief?" → Ch 9.
- **Assessment:** Reading Response #4; Part B — design a holdout/uplift study for the Fellow's own
  thread with a defensible incrementality readout, and critique a control-less "lift" claim.

---

## F. Library files (copied to pantry/, prefixed `_lib_`)

- `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md` — **primary**: potential outcomes &
  fundamental problem (§ early / line ~2014), CATE under conditional exogeneity (ch.14), causal forests
  + brittleness caveat (§14.3), S/T/X/R meta-learners (§15.1), uplift-curve validation (§15.B), doubly-
  robust methods. The technical spine of A and D.
- `_lib_science-randomistas-how-radical-researchers-are-changing-our-world.md` — why randomization/
  control is the gold standard; RCT culture; intuition for "the holdout is the counterfactual."
- `_lib_math-causal-inference-mit-press-essential-knowledge-series.md` — confounding, identification
  assumptions, natural experiments in accessible form.
- `_lib_science-the-book-of-why-the-new-science-of-cause-and-effect.md` — counterfactual reasoning,
  the ladder of causation; framing for the propensity-vs-causation inversion.
- `_lib_finance-advances-in-financial-machine-learning.md` — useful *honesty parallel*: López de Prado
  on backtest overfitting / leakage in finance maps onto pharma claims-lag + attribution leakage;
  ensemble + CV discipline relevant to uplift base-learner evaluation.
- (Reuse) both pharma syntheses for attribution circularity and the EHR incrementality gap.

---

## G. Gaps & flags

- [FLAG] Add canonical method citations not in-library: Künzel et al. PNAS 2019 (metalearners);
  Wager & Athey JASA 2018 (causal forests); Nie & Wager 2021 (R-learner); Gutierrez & Gérardy 2017
  (uplift review). Verify all before publication.
- [VERIFY] Larkin *JAMA* 2017 exact vol/pages (317:17:1785–1795 cited from memory); opioid-restriction
  study journal/year (Health Affairs 2020?).
- [VERIFY] Criteo Uplift v2.1 record count (13.98M) and the arxiv benchmark's specific conclusions —
  cite as "empirical comparisons find no universal best estimator," not a ranking.
- [FLAG] All vendor "lift"/"3x return"/"19–44%" figures: never present as incremental without naming
  the missing control. Cross-ref Ch 5 G.
- [GAP] No public, peer-reviewed *randomized* evaluation of EHR/POC advertising exists — the
  incrementality gap. This is the Track A research opening, not a number to fill.
- [SCOPE] Causal-inference depth: design-first, not estimator-derivation (per TIKTOC Open Q #6). Keep
  the chapter at "name the method, name its assumptions, design the test."
