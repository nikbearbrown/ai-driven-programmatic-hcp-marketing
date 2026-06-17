# Research Notes: Chapter 13 — The Fellow Research Portfolio (Run One)

**Chapter one-line (TIKTOC):** Fellows execute one low-cost research project on public data that tests the book's two questions — does it move lift, does it build association — and report honestly.

**Learning outcomes (TIKTOC):** (1, Create) Run a portfolio project end to end on public/synthetic data. (2, Evaluate) Score the evidence and flag compliance/ethics risk. (3, Create / Part B) Produce the result + plain-language readout for a partner decision-maker.

**Each project ships (TIKTOC):** hypothesis · public dataset (+ synthetic fallback) · **success threshold + kill criterion** · evidence-ladder level reached · compliance + patient-welfare flags · **likely partner owner** · handoff recommendation.

**Scope of these notes:** concrete, public-data-runnable Fellow projects across the four tracks — for each: the question, the public dataset, a credible identification strategy, success threshold + kill criterion, and compliance/welfare flags. Sections A and B are organized **by track** (A = the conceptual logic of each track's projects; B = the worked exemplar + failure mode per track).

**The Evidence Ladder (from Ch 11, used here):** L0 paper/claim → L1 hypothesis mapped to KPI → L2 reproducible benchmark/sim on public data → L3 small offline test beats baseline → L4 prospective pilot/holdout → L5 client-validated incremental impact → L6 monitored deployment w/ welfare checks. **A Fellow on public data tops out around L3.** L4–6 require the partner's proprietary replication (the firewall, made operational).

---

## A. Conceptual foundations — the four tracks

### Track A — Lift & attribution (owner: measurement analytics)
**The logic.** These projects attack the field's largest open methodological problem: vendor script-lift claims (4–44%) are association-grade and structurally inflated (the platform that serves the ad also measures the lift — attribution circularity). The Fellow's job is to show what a *credibly identified* lift estimate requires and to demonstrate, on public data, that naive attribution overstates effect. The dependent variable is incremental prescribing (Part D claims / SDUD units); the threat is always confounding by physician propensity (high-decile prescribers are targeted *and* respond, inflating estimates — Ch 8).
**Projects:**
- **A1. Script-lift attribution audit.** Reconstruct a vendor-style "lift" estimate (exposed-vs-unexposed comparison without a control) on Open Payments (promotion proxy) + Part D (outcome), then re-estimate with a credible design (DiD on a policy shock; matching + selection-on-observables with explicit sensitivity analysis) and quantify the gap. The deliverable is "how much of the headline lift is selection?"
- **A2. EHR/point-of-care natural experiment.** No peer-reviewed RCT exists for POC/EHR advertising (the book's single largest validation gap). On public data the Fellow can't observe EHR exposure directly, so this is *design-grade* (L2): specify the natural experiment that *would* identify POC lift (e.g., a health-system exposure on/off rollout) and run a power/simulation analysis showing the sample and design needed — the artifact a partner needs to justify a real pilot.
- **A3. Omnichannel attribution decomposition.** Using Part D + Open Payments, decompose observed prescribing change into promotion channels (meals, payments, time) with an honest accounting of what can and cannot be separated without exposure-level data; show the identification ceiling of public data.
**Source.** Attribution circularity + vendor lift ranges: `pantry/pharma-ai-hcp-marketing-synthesis.md` §1, §8; `pantry/pharma-marketing-evidence-synthesis.md` §3 (19–25% EHR lift, vendor-sourced, independent gap). Identification toolkit: `pantry/12-research-design-public-data_notes.md` A2–A5.

### Track B — Brand & physician identity (owner: brand strategy)
**The logic.** Brand equity in pharma = the physician remembering the **patient type** ("Brand X is for *this* patient"), not the name. The book's spine asks whether AI/promotion builds *durable association* vs. short-lived engagement. These projects test the qualitative industry claims (mind-share leads share; equity tracks value) with public data and dated natural experiments. The hard constraint: public data sees *behavior* (prescribing) well and *attitudes* (recall, association) poorly — survey/attitudinal data is scarce, so several B projects must proxy equity from behavioral persistence.
**Projects:**
- **B1. SOMi→SOMa predictive validity.** Test whether share-of-mind (SOMi, attitudinal) predicts later share-of-market (SOMa, behavioral) with a lag — the industry's central leading-indicator claim, asserted qualitatively but not rigorously tested on linked survey+claims data. Public-data version: where syndicated/survey mind-share is unavailable, proxy SOMi from a public attention signal (e.g., literature/CME mentions, search/journal indices) and test lagged prediction of Part D share. Honest caveat: the proxy is weak; this may top out at L2.
- **B2. Prescribing-habit durability across therapeutic classes.** Measure how persistent branded-prescribing patterns are across classes (chronic vs. acute, high-risk vs. substitutable) using Part D panels — operationalizes "habit" and shows where equity is structurally durable.
- **B3. Brand-equity vs. ICER clinical-value correlation.** Test whether brand equity / promotion intensity predicts prescribing persistence *after controlling for ICER clinical-value score*. An **uncorrelated** finding (equity sustained on low-value drugs) is a high-impact policy result. ICER value (extracted from reports) is the covariate; Part D persistence is the outcome.
- **B4. LOE persistence as a natural experiment.** Generic-entry date is exogenous and dated; estimate how much branded share persists post-LOE and whether persistence correlates with pre-LOE equity/promotion after controlling for market type and clinical value (DiD/event-study around entry). Directly operationalizes brand-measurement §4.
**Source.** Brand-formation loop, NBRx, SOV/SOM, LOE economics, "remember the patient type": `pantry/pharma-brand-measurement-synthesis.md` §1–§4, §6 (ICER value framework; "most promoted drugs less likely to be effective/affordable/novel"). SOMi→SOMa claim flagged tractable in TIKTOC Ch 2/Ch 9.

### Track C — Model architecture & segmentation (owner: data science)
**The logic.** Vendors label tabular targeting stacks "Mixture of Experts." The book's established position (from the MoE synthesis): on medium tabular data, gradient-boosted tree ensembles are state-of-the-art (Grinsztajn et al., NeurIPS 2022), and most "MoE" platforms are stacked ensembles relabeled. These projects produce *benchmark* and *audit* evidence the partner's data-science team can act on.
**Projects:**
- **C1. Ensemble-vs-genuine-MoE benchmark on NPI propensity.** Build a calibrated XGBoost/LightGBM baseline on a public NPI propensity task (constructed from Part D + Open Payments + specialty features) and compare a routed/MoE-style model. Success = a *meaningful, interpretable* gain in out-of-time validation, calibration, or subgroup robustness; kill = no lift over the tree ensemble, worse calibration, or complexity unjustified by business value. (This is the TIKTOC worked example.)
- **C2. "Natural N" physician archetypes via routing geometry.** Ask whether routing/clustering geometry reveals a stable number of physician archetypes (a "natural N" of segments) rather than an arbitrary k — segmentation grounded in structure, not convenience.
- **C3. Algorithmic audit of public "MoE" platform claims.** Apply the three architectural criteria (token-level routing? shared trunk? jointly trained?) and the six buyer questions to public vendor "MoE" descriptions and reach a verdict. A publishable technology-audit study; pure desk research → L2 (audit), no proprietary data needed.
**Source.** `pantry/moe-vs-ensemble-synthesis.md` (tabular exception §6; labeling problem §8; buyer questions; expert-collapse/specialization §3). NPI propensity as tabular: synthesis §6 + `pantry/pharma-ai-hcp-marketing-synthesis.md` §3.

### Track D — Privacy, fairness, accountability (owner: compliance + medical-commercial)
**The logic.** The adversarial track — empirically answerable fairness/welfare questions the field leaves unexamined. Two are causal/empirical; one is a framework. This is the track with the highest partner-framing tension (TIKTOC Risk 2/4): frame as collaborative de-risking, secure partner sign-off, route legal/regulatory conclusions to counsel.
**Projects:**
- **D1. Proxy-discrimination detection in rep/targeting assignment.** Test whether propensity/targeting models encode proxies for physician *susceptibility* or for protected-correlated attributes (geography, practice setting, patient demographics) rather than clinical need. Proxy discrimination = a facially-neutral feature acting as a stand-in for a protected attribute (the redlining analogy). Method: train a public-data propensity model, then test whether its scores are predicted by protected-correlated proxies after conditioning on legitimate clinical-need features; causal-graph framing for which paths are "proxy/redlining" paths. **Public-data sufficiency is a real risk (TIKTOC Risk 5)** — physician-level protected attributes are not in Part D/Open Payments, so this may rely on area-level proxies and top out at L2.
- **D2. Co-pay-coupon generic-suppression causal estimate.** Replicate/extend the Dafny–Ody–Schmitt design (cross-state/coupon-legality variation; coupons banned in Medicare) to estimate how much coupons suppress generic substitution and raise system cost. SDUD (state×quarter) + LOE dates. The cleanest causal Track-D project; directly tests the "co-pay coupons are pro-patient" contested claim (TIKTOC: nuanced).
- **D3. Accountability framework for commercial HCP-targeting AI.** A normative/structural deliverable (not an estimate): what monitoring, disclosure, auditability, and patient-welfare checks a deployed targeting system should carry. Routes to the Ch 14 patient-welfare gate.
**Source.** Proxy discrimination definition + redlining: `pantry/_lib_math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` (proxy/feedback-loop framing); algorithmic-fairness literature (proxy = descendant of protected attribute; "Unlawful Proxy Discrimination," arXiv 2404.14050). Coupon causal design: Dafny, Ody, Schmitt 2017 (`pantry/12-research-design-public-data_notes.md` B3). Welfare gap: `pantry/pharma-brand-measurement-synthesis.md` §6; `pantry/pharma-marketing-evidence-synthesis.md` §8.

---

## B. Worked exemplar + failure mode per track

### B-A. Track A exemplar — script-lift attribution audit (A1)
**Question:** how much of a vendor-style script-lift estimate is causal vs. selection?
**Dataset:** Open Payments (promotion dose per NPI) + Part D Prescriber (prescribing outcome per NPI), join on NPI; synthetic fallback = simulate exposure correlated with latent propensity.
**Identification:** estimate naive exposed-vs-unexposed lift (no control), then re-estimate via matching + Rosenbaum-style sensitivity analysis and, where a dated policy shock exists, DiD; report the gap.
**Success threshold:** demonstrably quantify the selection inflation (naive lift exceeds design-based estimate by a reportable margin with a defensible CI). **Kill:** can't construct a credible counterfactual / no identifying variation → downgrade to a design-only memo.
**Ladder level:** L2–L3. **Owner:** measurement analytics.
**Compliance/welfare flags:** none acute; the *finding* (lift is inflated) is partner-sensitive (Risk 2) — frame as de-risking the partner's own attribution claims.
**Failure mode to teach:** the Fellow reports the matched estimate as "causal" while unobserved propensity still confounds — the honest version reports residual-confounding sensitivity, not a point claim.

### B-B. Track B exemplar — brand-equity vs. ICER clinical-value (B3)
**Question:** does brand equity / promotion predict prescribing persistence after controlling for independent clinical value?
**Dataset:** ICER reports (clinical-value score, extracted + LLM-assisted with validation) + Part D (branded-share persistence) + Open Payments (promotion intensity).
**Identification:** persistence regressed on equity/promotion conditioning on ICER value + market controls; the headline is the *partial* association of equity net of value. (Associational by design — flag; LOE event-study (B4) is the stronger causal companion.)
**Success threshold:** equity predicts persistence with clinical value held constant → equity is "commercial memory, not clinical value" (high-impact). **Kill:** equity effect vanishes once value is controlled, or ICER coverage too sparse for the drug set.
**Ladder level:** L2 (associational) / L3 (with LOE event-study). **Owner:** brand strategy.
**Welfare flags:** an equity-not-value finding is a patient-welfare finding (system pays a premium for non-superior drugs) — route framing carefully.
**Failure mode:** treating ICER value as ground truth (it's contested) and ignoring that the most-promoted drugs are selected into ICER review — selection on the covariate.

### B-C. Track C exemplar — ensemble-vs-MoE benchmark (C1, the TIKTOC worked example)
**Question:** does a routed/MoE-style model beat a tuned gradient-boosting baseline on an NPI/NBRx-proxy task?
**Dataset:** constructed NPI propensity table from Part D + Open Payments + specialty/geography features; synthetic fallback = simulated NPI feature matrix.
**Identification (benchmark, not causal):** calibrated XGBoost/LightGBM baseline vs. routed model; out-of-time validation, calibration curves, subgroup robustness.
**Success threshold:** meaningful, interpretable gain in OOT validation/calibration/subgroup robustness. **Kill:** no lift over the tree ensemble, worse calibration, or complexity not justified by business value (the expected result given the tabular-data evidence).
**Ladder level:** L2–L3. **Owner:** data science. **Handoff:** only if routing yields operationalizable segment-specific gains.
**Compliance/welfare flags:** minimal (model bake-off); but a "no lift" result *protects* the partner from an unjustified architecture investment — a "no" is a result.
**Failure mode:** the Fellow over-tunes the fancy model and under-tunes the baseline (a rigged benchmark) — the honest version tunes both equally and reports calibration, not just AUC.

### B-D. Track D exemplar — co-pay-coupon generic-suppression estimate (D2)
**Question:** how much do co-pay coupons suppress generic substitution and raise system cost?
**Dataset:** Medicaid SDUD (state×quarter generic vs. branded units/spend) + LOE/generic-entry dates; coupon-legality variation (Medicare ban; state rules) as the design.
**Identification:** DiD / cross-state-legality contrast around generic entry (the Dafny–Ody–Schmitt template), heterogeneity-robust if staggered.
**Success threshold:** a credible, signed estimate of generic-substitution suppression with valid pre-trends. **Kill:** no clean legality/timing variation; pre-trends fail.
**Ladder level:** L3 (this design is well-precedented). **Owner:** compliance + medical-commercial.
**Welfare/compliance flags:** HIGH — directly tests a partner product line (co-pay programs; Doceree's Co-Pay.com); a suppression finding has clear patient-welfare and policy weight. Secure partner sign-off on framing (Risk 2/4); route any legal characterization to counsel.
**Failure mode:** ecological inference — SDUD is aggregated to NDC×state, so individual substitution is inferred, not observed; over-claiming patient-level behavior is the trap.

---

## C. Connections and dependencies

- **Prereqs:** Ch 11 (lab workflow, IP firewall, Evidence Ladder — the level a project reaches is the firewall made operational); Ch 12 (the identification strategy + dataset each project rides on); Ch 6–7 (ensemble/MoE for Track C); Ch 8 (incrementality for Track A); Ch 9 (brand-as-outcome for Track B); Ch 10 (LLM-assisted ICER extraction with validation for B3).
- **Unlocks:** Ch 14 (each project's evidence-ladder level + welfare flags feed the test/build/kill handoff brief — the terminal deliverable).
- **Adjacent / owner map (TIKTOC):** Lift/attribution → measurement analytics; Brand/identity → brand strategy; Model architecture → data science; LLM/content → content operations; NBA/journey → NBA-product; Ethics/accountability → compliance + medical-commercial.

---

## D. Current state of the field / key references

- **Track A:** no peer-reviewed RCT for POC/EHR advertising remains the field's biggest gap (synthesis §8); vendor lift 4–44% all company-reported. Veeva Crossix cited as the best independent measurement methodology (still proprietary).
- **Track B:** SOMi→SOMa leading-indicator claim untested on linked survey+claims data; "most-promoted drugs have low added clinical benefit" — 2023 study found 68% of most-advertised drugs low added benefit (`pantry/pharma-marketing-evidence-synthesis.md` §4); ICER value framework is the available independent value benchmark.
- **Track C:** Grinsztajn et al. (NeurIPS 2022) — trees SOTA on medium tabular data; DeepSeek-V3 (2024, 256 fine-grained experts) and Mixtral 8x7B as the genuine-MoE reference points; expert-similarity >99% / collapse findings (MoE synthesis §3, §6).
- **Track D:** Dafny, Ody & Schmitt 2017 (coupons +60% branded sales via generic suppression; AEJ: Policy / NBER w22745) — the canonical causal coupon result; proxy-discrimination/algorithmic-fairness literature (redlining analogy; "Unlawful Proxy Discrimination" arXiv 2404.14050, `[verify]` as a working paper); `pantry/_lib_math-weapons-of-math-destruction...` for the feedback-loop/proxy framing.
- **`[verify]`:** Grinsztajn citation details already in MoE synthesis; ICER thresholds; Dafny et al. vintage; arXiv fairness papers (working-paper status).

---

## E. Teaching considerations

- **One project, end to end, honestly.** The pedagogy is *finish a real thing and score it truthfully* — including writing the "no." The C1 worked example is the model: a tuned baseline that the fancy model fails to beat is a *successful* project (it saves the partner money).
- **Every project ships the same 7-field card** (TIKTOC): hypothesis · dataset (+synthetic fallback) · success threshold + kill criterion · ladder level · compliance+welfare flags · likely owner · handoff recommendation. Enforce this structure on Part B.
- **Kill criteria are not failure.** Frame the kill criterion as the project's honesty mechanism — pre-registering what would make you walk away. This is the antidote to the field's vendor-deck culture.
- **Track D needs scaffolding** (TIKTOC hard-chapter note): teach the de-risking framing, the route-to-counsel rule, and the public-data-sufficiency limits (Risk 5) *before* students pick D1/D2.
- **Named Fellow artifact:** a **completed portfolio project** — run, scored, ladder-leveled, flagged, with a plain-language readout for a non-technical partner decision-maker.
- **Five-part AI block:** LLM = draft analysis plan / extract ICER values; AI-validation = catch hallucinated citations and a rigged benchmark; the human judgment is "is the signal real and would the partner defend it to a regulator/audit committee."

---

## F. Library files relevant (in `pantry/` as `_lib_*`)

- `_lib_math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` — **Track D primary:** proxy discrimination, feedback loops, opacity of scoring models; the redlining analogy and "models encode bias" framing.
- `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md` — identification strategies behind every track's design (DiD for B4/D2, IV/RDD where applicable); DML for high-dimensional first stages (Track A matching/sensitivity).
- `_lib_ai-the-alignment-problem-machine-learning-and-human-values.md` — fairness/accountability conceptual grounding for D3 (the accountability framework).
- `_lib_science-randomistas-how-radical-researchers-are-changing-our-world.md` — field-experiment/natural-experiment narrative for Track A's "what a real POC pilot needs."
- (Reused syntheses, not `_lib_`:) `moe-vs-ensemble-synthesis.md` (Track C, primary), `pharma-brand-measurement-synthesis.md` (Track B, primary), `pharma-marketing-evidence-synthesis.md` (Tracks A/D), `pharma-ai-hcp-marketing-synthesis.md` (attribution circularity, platform landscape), `12-research-design-public-data_notes.md` (the design+data each project rides on).

---

## G. Gaps and flags

- **G1. Public-data sufficiency varies by track (TIKTOC Risk 5).** Tracks C3, A1, B2/B3, D2 are well-served by public data; **D1 (proxy discrimination)** and **A2 (POC lift)** lack the exposure/protected-attribute data and top out at design/simulation (L2). Be explicit in each brief about the ladder ceiling.
- **G2. Ladder ceiling = the firewall.** Public-data Fellows reach ~L3; L4–6 require the partner's proprietary replication. Don't let a Fellow over-claim a public-data project to L4+.
- **G3. NBRx is not directly in Part D** (carried from Ch 12 G2) — Track B "new starts" are proxies; label them.
- **G4. Partner-framing tension (Risk 2/4)** is sharpest for Track A (lift inflation) and Track D (proxy discrimination, coupon suppression) — these critique partner products. Required: collaborative de-risking framing + partner sign-off + counsel routing for legal characterizations. This is the open BLOCKER (TIKTOC Risk 1 / Open Question 1) for how adversarial these can be.
- **G5. Ecological/aggregation inference** in SDUD-based projects (D2) — NDC×state, not patient-level; don't over-claim individual behavior.
- **G6. ICER as covariate is contested + selection-prone** (B3) — flag QALY-method controversy and that ICER-reviewed drugs are a selected set.
- **G7. Rigged-benchmark risk** in Track C — equal tuning effort + calibration reporting (not just AUC) is the integrity check.
- **G8. `[verify]`:** Dafny et al. citation vintage/effect sizes; 68%-low-added-benefit study (2023); arXiv fairness/proxy papers (working-paper status); Grinsztajn NeurIPS 2022 details (in MoE synthesis).
