# Chapter 14 — From Prototype to Product Decision (The Fellows Brief)

## 1. Chapter overview

This is the terminal chapter, and it produces the book's terminal deliverable: the **product-handoff brief**. By the end you will be able to take a scored portfolio project (Chapter 13) and turn it into a defensible decision — **test it, build it, or kill it** — written so a partner's product, data-science, medical, legal, regulatory, and commercial stakeholders can act on it. You will apply explicit handoff criteria (evidence strength, lift or association magnitude, compliance risk, build cost), route compliance flags to counsel rather than adjudicating them, sketch an engineering estimate, design a client-pilot and a post-launch monitoring plan for the build path, and — the chapter's moral spine — apply the **patient-welfare gate as a binding veto**: a project can be commercially excellent and still be killed because it harms patients or the health system. You will also place the project in the **four-stage research-to-product pipeline** and understand exactly where the Fellow's job ends and the partner's begins. The skill being trained is judgment under honesty: writing a *good* "no" is as assessable, and as valuable, as recommending a build.

## 2. Learning objectives

By the end of this chapter you will be able to:

1. **(Evaluate)** Apply explicit handoff criteria — evidence strength, lift/association magnitude, compliance risk, the **patient-welfare gate**, and build cost — to reach a verdict.
2. **(Create)** Produce the product-handoff brief *and* the rejection rationale, treating a "no" as a result.
3. **(Apply)** Stage a portfolio: decide what to test next, what to replicate on proprietary data, what to shelve, and what to ship.

## 3. Opening case — a prototype that lifts engagement but not incrementality, and trips a flag

A Fellow brings the lab review a prototype she is proud of. It is an AI-driven content-personalization model for point-of-care messaging, and on her public-data proxy it shows a clean, statistically significant lift in *engagement* — the surrogate metric (opens, clicks, dwell) the platform reports natively. The vendor deck would call this a win. She is inclined to write a BUILD brief.

The lab lead asks three questions, in order.

First: "Engagement, or incrementality?" The model lifts the surrogate, but she has no holdout and no credible identification — she cannot say whether it changed any *prescribing*. Engagement is not belief and is not scripts (Chapter 2). On the Evidence Ladder she is at Level 2, maybe 3: an offline result on a surrogate, not a causal readout on the outcome that matters.

Second: "What does it touch?" The personalization fires content into the EHR sidebar — the same visual layer as drug-interaction and safety alerts (`pharma-ai-hcp-marketing-synthesis.md` §2). That is a **compliance flag** (FDA fair-balance risk if the content makes claims; an unsettled HIPAA question about real-time clinical triggers) *and* a **patient-welfare flag** (intensifying commercial messaging in the safety-alert layer raises cognitive load at the prescribing moment).

Third: "If we hand this to engineering and it ships, what would we be shipping?" A feature that demonstrably moves a surrogate, has *no* evidence it moves the real outcome, and lives in the most ethically fraught layer in the stack.

What is the right call? Not BUILD. The honest verdict is **TEST** — the engagement signal is promising enough to justify the partner running a proper holdout on proprietary data (the only thing that can produce the causal readout public data cannot), *conditioned on* clearing the fair-balance and welfare flags first. And if the proprietary holdout later showed the lift was engagement-only — surrogate movement with no prescribing change — *and* the content tripped fair-balance, the verdict would flip to KILL regardless of how good the engagement number looked. This chapter is the machinery that produces that call, and makes the welfare flag able to override a positive commercial result.

## 4. Prerequisites

You should arrive able to:

- Place an artifact on the **Evidence Ladder** and explain why public data tops out around Level 3 (Chapter 11).
- Describe the **four-stage productization pipeline** and the IP firewall (Chapter 11).
- Read a **scored portfolio project** — its seven-field card, ladder level, and flags (Chapter 13).
- Distinguish **propensity from incrementality** and know why a public-data result usually can't reach Level 4 without a holdout (Chapter 8).
- Grade **evidence quality** honestly — association dressed up vs. credible identification (Chapter 5).
- Distinguish **engagement (surrogate) from lift and brand (the real dependent variables)** (Chapter 2).

## 5. The handoff decision machinery

### 5.1 The four-stage research-to-product pipeline (the decision spine)

The lab's value is *reducing the partner's uncertainty*, not shipping product. A finding moves through four gates, each a larger resource commitment, mapped to the Evidence Ladder:

| Stage | What happens | Who owns it | Ladder |
|---|---|---|---|
| **1. Open research** | Public-data test on public methodology. | The Fellow. | L0–L3 |
| **2. Proprietary replication** | The *partner* re-runs the promising method on its internal data (prospective pilot/holdout). | The partner. | L4 |
| **3. Prototype** | A built artifact tested in a controlled client context. | The partner. | L5 |
| **4. Resourced product feature** | Monitored deployment with compliance + welfare checks. | The partner. | L6 |

The firewall holds at Stage 1: nothing proprietary enters the book or repo. The Fellow owns Stage 1; the partner owns Stage 2 and up. **The Chapter 14 brief is precisely the gate-1→gate-2 handoff document**: does this public-data result earn proprietary replication?

The load-bearing misconception to kill: *"the Fellow's job is to build the feature."* No. The Fellow's job ends at "this earns (or does not earn) the partner's data and engineering." Over-building is scope creep the firewall forbids — and, practically, a Fellow on public data *cannot* reach Levels 4–6, because those require the proprietary data and live client context that exist only inside the partner's walls.

> **The standing blocker [contested — see pantry, Risk 1 / Open Question 1].** The handoff mechanics in this chapter *assume* a gate-2 partner exists, has agreed to receive briefs, and will act on them — and that the partner has signed off on the framing, including the framing of briefs that critique its own products. None of that is settled. Whether (and what) proprietary replication is in scope, and who signs off on a brief's framing, is an **open blocker**, not a resolved arrangement. Read everything below as "this is how the handoff works *if* the agreement lands where the book assumes," and treat that "if" as live.

### 5.2 The handoff criteria — test / build / kill

The brief reaches one of three verdicts via explicit, **conjunctive** criteria:

- **Evidence strength** — the Evidence-Ladder level actually reached (be honest: public data tops at ~L3) and the quality of the identification (a credible design, or association dressed up?).
- **Lift or association magnitude** — does it move one of the book's two dependent variables *enough to matter commercially*? A statistically significant but tiny effect is a kill.
- **Compliance risk** — MLR / FDA fair-balance / Sunshine Act / HIPAA exposure, **flagged and routed to counsel**, never adjudicated by the Fellow.
- **Patient-welfare gate** (§5.3) — a *required* criterion, not an appendix, and able to veto.
- **Build cost** — the engineering/data estimate to take it to L4+. A strong-evidence, high-cost project may still be "test next" rather than "build."

The three verdicts:

- **TEST** — promising but not decisive → more public-data work, *or* hand to the partner for proprietary replication at gate 2. ("We reduced uncertainty about *which* claim to trust without resolving it.")
- **BUILD** — evidence + magnitude + acceptable compliance + passes the welfare gate + tractable cost → recommend resourcing.
- **KILL** — fails a threshold → shelve, *with the rejection rationale written.* A "no" is a result.

The criteria are **conjunctive**, and **welfare can veto**: a positive commercial result that fails the welfare gate, or carries unacceptable compliance risk, or costs more than its value, is a KILL or a TEST-next — not a BUILD. The misconception to kill: *"the brief recommends building if the result is positive."* It does not. Positive-but-vetoed is the most important case the chapter teaches.

### 5.3 The patient-welfare gate (the chapter's moral spine)

The welfare gate asks one question: **even if this works commercially, does it harm patients or the health system?** It is a **gate** — a project can be commercially excellent and still be killed on welfare grounds. The gate operationalizes the book's central critique: the commercial stack measures *adoption* far better than it measures *welfare* (`pharma-brand-measurement-synthesis.md` §6). Concretely, the gate flags whether the project:

- suppresses clinically appropriate **generic substitution** (the coupon case);
- targets physician **susceptibility** rather than patient need (the proxy case);
- moves prescribing of **low-clinical-value** drugs (the ICER-mismatch case);
- intensifies **EHR-embedded messaging in the same layer as safety alerts** (the point-of-care case from the opener).

The discipline is pervasive by design — every chapter carries a compliance-and-welfare check (the series anatomy). Chapter 14 is where welfare stops being a check and becomes a *binding decision criterion*. A Fellow who treats the gate as boilerplate has missed the chapter. And — consistent with the route-to-counsel rule — the welfare gate flags and reasons about harm; it does not *adjudicate* legality. "This suppresses generic substitution and raises system cost with no clinical benefit" is a welfare finding the Fellow can defend; "this is illegal" is a conclusion for counsel.

**Worked welfare-veto.** A Track-D coupon project (D2) shows a co-pay program lifts branded share — a commercial win — by suppressing generic substitution, which is a welfare loss (higher system cost, no clinical benefit; Dafny, Ody & Schmitt 2017 [verify]). The welfare gate → **KILL or escalate**, regardless of the commercial lift. The kill rationale is itself a partner-valuable result: it tells the partner what it just avoided defending.

### 5.4 MLR / legal review and the engineering estimate

Two practical gates a buildable project must pass:

- **MLR (Medical/Legal/Regulatory) + legal review.** Pharma content and claims run through MLR — historically ~50–60 days per piece [vendor-reported; verify], with AI now compressing this (McKinsey estimates 50–65% timeline reduction, methodology unspecified [verify]). Be skeptical of "AI makes MLR free": promotional volume rose ~29% year-over-year in 2025 while ~77% of approved content is rarely used, and an MIT analysis found ~95% of generative-AI pilots failing — "the problem is governance, not generation speed" [verify] (`pharma-ai-hcp-marketing-synthesis.md` §4). Any recommendation that would generate HCP-facing claims must flag MLR load and fair-balance risk — and the September 2025 FDA enforcement wave (200+ letters, AI-powered ad surveillance, fair-balance and efficacy-exaggeration the top violations [verify counts]) makes this live (§5). EHR-integrated advertising remains a regulatory gray zone with no specific OPDP guidance — a flag, not a green light. The Fellow *flags and routes*; counsel and medical affairs adjudicate.
- **Engineering / data estimate.** A rough order-of-magnitude of what gate-2/3 costs: data access for proprietary replication, model and infrastructure build, monitoring. The estimate turns "good idea" into "good idea worth roughly $X" — the input the partner's resourcing decision actually needs. Because Fellows are not MLOps engineers, the brief gives an *order of magnitude plus the questions for the partner's engineers*, not a precise number it cannot defend.

The misconception to kill: *"compliance is someone else's problem after handoff."* An un-flagged compliance landmine discovered at gate 3 is far costlier than one surfaced at gate 1. The brief's job is to surface it early.

### 5.5 Client-pilot design and post-launch monitoring (gates 3–4)

For a BUILD recommendation, the brief *sketches* (it does not run — that is the partner's) two things:

- **The client pilot** — a prospective holdout / RCT-style test on the partner's client data. This is the L4→L5 step that finally produces a *causal* readout the public-data work could not (Chapter 8): the holdout is the gold standard the Fellow could only gesture at on public data.
- **The post-launch monitoring plan** (L6) — ongoing effectiveness tracking, compliance audit, and a **standing patient-welfare check** so the welfare gate does not end at launch. This is where the accountability-framework work (Track D3, Chapter 13) lands operationally.

The misconception to kill: *"once it ships, the research is done."* L6 is *monitored* deployment; the welfare and compliance checks are continuous. A shipped feature with no monitoring plan fails the brief.

## 6. Worked example — a full handoff / kill memo

Below is the terminal deliverable applied to the Chapter 13 worked project (the C1 MoE-vs-ensemble benchmark, whose kill criterion was met) and, for contrast, a welfare-veto kill. This is the structure a Fellow could hand the partner's team.

> **PRODUCT-HANDOFF BRIEF**
> **Project:** C1 — Ensemble vs. routed ("MoE") model on NPI propensity
> **Prepared by:** [Fellow] · **Date:** [date] · **Distribution:** data science (owner), product, MLR (flag only)
>
> **Verdict: KILL (architecture investment).**
>
> **1. Question.** Does a routed/MoE-style model meaningfully beat a tuned gradient-boosting baseline on the partner's core NPI-propensity task?
>
> **2. Evidence strength.** Evidence-Ladder **L3** (small offline test). Benchmark, not causal — appropriate for an architecture decision. Both models tuned with equal, logged effort; evaluated on out-of-time validation, calibration (Brier + reliability), and subgroup robustness — not AUC alone.
>
> **3. Magnitude.** The tuned LightGBM baseline matched the routed model on AUC and **beat** it on calibration; subgroup robustness equivalent. No operational gain from routing.
>
> **4. Compliance flags (routed, not adjudicated).** None material — internal model bake-off, no HCP-facing content. → no MLR action required at this stage.
>
> **5. Patient-welfare gate.** PASS (no welfare exposure). Note: a "no lift" finding *protects* patients indirectly by not committing resources to an unjustified, less-interpretable system.
>
> **6. Build cost.** The routed architecture would add substantial training and inference complexity and reduce interpretability, for no measured gain. Cost clearly exceeds value.
>
> **7. Recommendation & staging.** **KILL the routed-architecture investment; keep the tuned ensemble.** Do *not* advance to gate 2. The "no" saves the engineering budget — the expected outcome given the tabular-data evidence (Grinsztajn et al., NeurIPS 2022 [verify]).
>
> **8. What would change the verdict.** A future task with genuine sequence/multi-task structure (not tabular NPI prediction) where routing's advantages apply, *and* an equally tuned benchmark showing a meaningful, calibration-confirmed gain.

> **PRODUCT-HANDOFF BRIEF (welfare veto)**
> **Project:** D2 — Co-pay-coupon generic-suppression estimate
> **Verdict: KILL (welfare gate), with escalation.**
>
> **Evidence strength.** L3; heterogeneity-robust DiD on coupon-legality variation, valid pre-trends. *Stated at the state-quarter level — individual substitution is inferred, not observed (ecological-inference flag).*
> **Magnitude.** Commercially positive — the coupon program lifts branded share. *Mechanism: suppression of bioequivalent-generic substitution.*
> **Compliance flags (routed).** Coupons banned in Medicare; state-law variation; route any legality characterization to counsel.
> **Patient-welfare gate.** **FAIL.** The commercial lift *is* generic suppression — higher system cost, no clinical benefit. This is the worked welfare veto.
> **Recommendation.** **KILL** as a product to optimize; **escalate** the finding to compliance + medical-commercial as a risk the partner should know it carries. The rejection rationale is the deliverable: it tells the partner what it just avoided defending to a regulator or audit committee. *(Framing requires partner sign-off — Risk 2/4 — and is subject to the standing blocker, Risk 1.)*

Notice the load-bearing features: the verdict is on the first line; the evidence level is honest; the welfare gate is a *decision*, not a footnote; compliance is flagged and routed, not adjudicated; and the kill carries a written rationale plus "what would change the verdict." A brief without those is incomplete.

## 7. Common misconceptions

- **"The brief recommends BUILD if the result is positive."** No — criteria are conjunctive and welfare can veto. Positive-but-vetoed (the coupon case) is a KILL.
- **"Ethics is the final-chapter wrap-up."** No — the welfare check is pervasive (every chapter); Chapter 14 makes it a *binding* criterion that can override commercial success.
- **"The Fellow builds the feature."** No — the Fellow's job ends at the gate-1→gate-2 handoff. The partner replicates, prototypes, and ships.
- **"Compliance is someone else's problem after handoff."** No — an un-flagged landmine found at gate 3 is far costlier. Flag early; route, don't adjudicate.
- **"Once it ships, the research is done."** No — L6 is *monitored* deployment with a standing welfare check. No monitoring plan → the brief fails.
- **"A KILL wasted the cycle."** No — a good "no" (what would change the verdict, what the partner just avoided spending) is an assessable, valuable result and the antidote to vendor-deck optimism.

## 8. Evidence check

- **Independent / established:** Holdout/RCT designs are the causal gold standard (Chapter 8). Tree ensembles SOTA on medium tabular data (Grinsztajn et al., NeurIPS 2022 [verify]). The "most-promoted drugs often have low added benefit" finding gives the welfare gate empirical teeth (`pharma-marketing-evidence-synthesis.md` §4 [verify the 68% figure]).
- **Vendor-generated (treat as claims):** MLR cycle-time figures (~50–60 days) and the McKinsey 50–65% AI-reduction estimate (methodology unspecified) are vendor/consultancy-reported [verify]. All script-lift numbers remain vendor-sourced.
- **Contested / drifting:** The MIT "95% of GenAI pilots fail" stat circulates without clear methodology [verify]; FDA 2025 enforcement counts vary by source (use the *trend*, attribute specific counts to a dated source) [verify]; current OPDP guidance on EHR advertising is absent (a gray zone, not a settled permission).
- **Hypothetical / design-grade:** Any BUILD path's *causal* claim is a gate-2 prediction (the partner's holdout), not something the public-data brief established.

## 9. Compliance + patient-welfare check

- **MLR / FDA fair balance:** Any BUILD that would generate HCP-facing content inherits MLR load and fair-balance risk (heightened by the 2025 enforcement wave). The brief flags it and routes to MLR/counsel; it does not pre-clear content.
- **Sunshine Act / HIPAA:** Sunshine exposure arises only if a built feature involves transfers of value; HIPAA exposure arises around real-time clinical triggers (the EHR gray zone). Flag at the gate, route to counsel.
- **Patient-welfare gate:** The binding criterion of this chapter. Run the four flags (generic suppression, susceptibility targeting, low-value prescribing, safety-alert-layer intensification) on every BUILD candidate. A failed gate vetoes the build. A shipped feature must carry a *standing* welfare check (post-launch monitoring), not a one-time clearance.
- **Route, never adjudicate:** A brief that *concludes* on legal or regulatory permissibility has overstepped (the firewall and the out-of-scope rule). The discipline is route-to-counsel.

## 10. Exercises

1. **(Understand)** Write the decision tree the brief implements: starting from a scored project, what sequence of criteria (ladder level, magnitude, welfare gate, compliance, cost) leads to TEST vs. BUILD vs. KILL? Show explicitly where the welfare gate can override a positive commercial result.

2. **(Evaluate)** Take the opening-case prototype (engagement lift, no incrementality, EHR-layer flag). Write the *one-paragraph* verdict with its reasoning, then state the single piece of evidence that would flip it from TEST to BUILD and the single piece that would flip it to KILL.

3. **(Apply+)** You are handed a project that is commercially strong, L3, low build cost — *and* fails the welfare gate (it moves prescribing of a low-ICER-value drug). Write the **KILL rationale** as a partner would need to read it: what the partner avoided, what would change the verdict, and how to frame it given the standing partner-sign-off blocker (Risk 1/2/4). Hold the kill — do not soften it into a BUILD.

4. **(Create / Part B — produce: the product-handoff brief).** Take your Chapter 13 scored project and produce the **full product-handoff brief** — the book's terminal deliverable. It must contain: the one-line verdict (test/build/kill); evidence strength (honest ladder level); magnitude; compliance flags (routed); the patient-welfare gate result; an order-of-magnitude engineering estimate plus the questions for the partner's engineers; the recommended next gate; and — if BUILD — a one-paragraph client-pilot and post-launch monitoring sketch; or — if KILL — a written rejection rationale with "what would change the verdict." A defensible KILL earns full marks.

## 11. Five-part AI exercise block

**When to use AI.** Use an LLM to draft the brief's structure, turn a scored card into prose, draft the client-pilot and monitoring sketch, and generate the "what would change my mind" section. AI is good at format and at surfacing criteria you might forget to address.

**When NOT to use AI.** Do not let an LLM decide the *verdict*, judge whether the welfare gate is failed, decide whether the evidence truly reaches the ladder level claimed, or assert that a finding is partner-defensible. These are the human judgments the entire book has been building toward.

**LLM exercise.** Prompt: *"Here is a scored project [paste card]. Write a product-handoff brief recommending build/test/kill."* Then audit the output: did it default to BUILD on a positive result? Did it apply the welfare gate as a *veto* or treat it as a checkbox? Did it adjudicate compliance instead of routing it? Rewrite every place it overstepped.

**CLI exercise.** Use a coding agent to assemble the brief from your Chapter 13 artifacts: pull the scored card, the calibration plots, and the kill-criterion result into a single rendered brief, with the verdict computed *from your stated criteria* (so the logic is auditable) rather than asserted.

**AI validation.** Run the brief through the Chapter 10 validation harness at a *higher bar*: every cited figure resolves and is correctly labeled vendor/independent/contested; no causal claim exceeds the ladder level; the welfare gate is applied as a binding criterion; no legal conclusion is adjudicated. Document the one judgment the AI got fluently wrong.

## 12. AI Use Disclosure

This is the capstone disclosure, and it carries a **higher bar**: name **three** judgments across the whole project that required human expertise no AI could supply —

1. **True evidence status** — what level the work *actually* reached, and what it cannot claim.
2. **Real-vs-noise signal** — whether the effect is real or an artifact (selection, a rigged benchmark, a surrogate).
3. **Partner-defensibility** — whether the partner could defend the recommendation to a regulator or an audit committee.

The disclosure is the final beat of the book's AI-honesty thread: AI drafted and scaffolded; you supplied the judgments that decide whether anyone should spend money on this.

## 13. What would change my mind

I would revise the claim that **public-data work cannot reach Level 4** if a public dataset emerged with credible exposure-level and protected-attribute data (it does not exist today). I would revise the stance that **the patient-welfare gate must be a binding veto** if evidence showed that a binding gate systematically killed projects that, in proprietary replication, turned out welfare-neutral — i.e., if the gate were producing false KILLs at the public-data stage; the gate's design assumes the cost of a false BUILD (a harmful shipped feature) exceeds the cost of a false KILL (a shelved good idea), and that assumption is itself contestable. And I would revise the entire handoff architecture if the partner agreement (Risk 1) landed such that **gate 2 does not exist or critical briefs cannot be delivered** — in which case the honest response is to report that the lab's core mechanism is blocked, not to pretend the handoff is operational.

## 14. Still puzzling

- The welfare gate trades a false BUILD against a false KILL — but who decides the exchange rate, and on what authority, when the Fellow is explicitly told to route policy conclusions to counsel? Is the gate a *judgment* the Fellow makes or a *flag* the Fellow raises?
- Open Question 3 is not settled: is patient welfare a per-project *gate* (the book's recommendation, adopted here) or a capstone *appendix*? If the partner lands on capstone, the decision tree in this chapter changes materially.
- The brief's most valuable outputs (lift is inflated; the coupon suppresses generics; the routed model loses) are exactly the ones that critique the partner at the moment of a resource decision. Is "collaborative de-risking" a stable framing for that, or does it break the first time a kill costs the partner a product line?

## 15. Summary

You can now convert a scored portfolio project into a product-handoff brief — the book's terminal deliverable — and reach a defensible test/build/kill verdict. You can apply the conjunctive handoff criteria (evidence strength, magnitude, compliance, welfare, cost), place the project in the four-stage pipeline, and locate the gate-1→gate-2 handoff that is the brief's job. You can flag and route compliance (MLR, fair balance, Sunshine, HIPAA) without adjudicating it, sketch an engineering estimate honestly, and design a client pilot and a standing post-launch monitoring plan. Above all, you can apply the **patient-welfare gate as a binding veto** — holding a KILL on a commercially strong project that harms patients — and write a *good* "no," because a defensible rejection reduces the partner's uncertainty as much as any build. And you can name, honestly, where the whole handoff rests on an unresolved partner agreement (Risk 1) rather than pretending the mechanism is settled.

## 16. Key terms

- **Product-handoff brief:** the terminal deliverable — verdict + evidence grade + magnitude + routed compliance flags + welfare-gate result + engineering estimate + next gate.
- **Test / build / kill:** the three verdicts; a "no" is a result.
- **Patient-welfare gate:** the binding criterion that can veto a commercially positive project on patient/system-harm grounds.
- **Four-stage pipeline:** open research → proprietary replication → prototype → resourced feature; the Fellow owns Stage 1.
- **Gate-1→gate-2 handoff:** the question the brief answers — does this public-data result earn proprietary replication?
- **Route-to-counsel:** the discipline of flagging compliance risk without adjudicating legality.
- **Client pilot:** the partner's prospective holdout (L4→L5) that finally yields a causal readout.
- **Post-launch monitoring:** continuous effectiveness, compliance, and welfare checking of a shipped feature (L6).

## 17. Bridge

This closes the three-act arc: the System (what the commercial machine optimizes), the Toolkit (how to test it honestly), and the Lab (how to run a research thread and hand the result to a partner as a defensible decision). The Fellow you are now is the one the book set out to make on page one — not someone who can be impressed by a "44% lift" claim, but the honest filter between research hype and committed partner resources, holding a binding patient-welfare gate even when the commercial number says go. The back matter carries the standing open questions forward: the partner agreement (Risk 1) that this chapter's handoff mechanics depend on remains unresolved, and the welfare-gate-vs-capstone decision (Open Question 3) is a design choice this book recommends but does not impose. The work the lab exists to do is now yours to run.

## 18. Further reading

- Cooper, Stage-Gate process (Wiley Encyclopedia of Management). — The go/kill scaffold the four-stage pipeline adapts. [verify]
- Ries, *The Lean Startup.* — Validated learning and the cheap-test logic behind "reduce uncertainty before committing resources."
- O'Neil, *Weapons of Math Destruction.* — The "deployed model needs monitoring and accountability" argument behind the post-launch welfare check (`pantry/_lib_math-weapons-of-math-destruction...`).
- Christian, *The Alignment Problem.* — Values and accountability grounding for the patient-welfare gate and monitoring plan (`pantry/_lib_ai-the-alignment-problem...`).
- Bergstrom & West, *Calling Bullshit.* — Skeptical-reading discipline for grading evidence honestly (the brief's evidence-strength criterion and the failure-case anti-pattern).
- `pantry/pharma-ai-hcp-marketing-synthesis.md` (§§4–5) and `pantry/pharma-brand-measurement-synthesis.md` (§6). — MLR/FDA-enforcement state and the welfare-measurement gap that gives the gate its teeth. [verify the specific MLR, enforcement, and pilot-failure figures]

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
