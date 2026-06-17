# Chapter 14 — From Prototype to Product Decision (The Fellow's Brief)
*A good "no" is as valuable as a build recommendation — and harder to write.*

A Fellow brings the lab a prototype she is proud of. It is an AI-driven content-personalization model for point-of-care messaging, and on her public-data proxy it shows a clean, statistically significant lift in engagement — opens, clicks, dwell time, the metrics the platform reports natively. The vendor deck would call this a win. She is inclined to write a BUILD brief.

The lab lead asks three questions, in order.

"Engagement, or incrementality?" The model lifts the surrogate, but there is no holdout, no credible identification. She cannot say whether it changed any prescribing. Engagement is not belief and is not scripts — that distinction was Chapter 2's whole argument. On the Evidence Ladder she is at Level 2, maybe 3: an offline result on a surrogate, not a causal readout on the outcome that matters.

"What does it touch?" The personalization fires content into the EHR sidebar — the same visual layer as drug-interaction and safety alerts. That is a compliance flag (FDA fair-balance risk if the content makes product claims; an unsettled HIPAA question about real-time clinical triggers) and a patient-welfare flag (intensifying commercial messaging in the safety-alert layer raises cognitive load at the exact moment a prescribing decision is being made).

"If we hand this to engineering and it ships, what would we be shipping?" A feature that demonstrably moves a surrogate, has no evidence it moves the real outcome, and lives in the most ethically fraught layer in the stack.

The right call is not BUILD. It is **TEST** — the engagement signal is promising enough to justify the partner running a proper holdout on proprietary data, the only thing that can produce the causal readout public data cannot, *conditioned on* clearing the fair-balance and welfare flags first. And if the partner's holdout later showed lift was engagement-only — surrogate movement with no prescribing change — and the content tripped fair-balance, the verdict would flip to KILL regardless of how good the engagement number looked.

That is the machinery this chapter produces: the brief that generates this call, and the welfare gate that can override a positive commercial result.

---

Before the mechanics, a structural fact worth holding clearly: the Fellow's job ends at the gate-1-to-gate-2 handoff.

The four-stage research-to-product pipeline maps cleanly to the Evidence Ladder. Stage 1 is open research — the Fellow's stage, public data and public methodology, topping out around Level 3. Stage 2 is proprietary replication — the *partner* re-runs the promising method on its internal data, running the prospective holdout the Fellow could only gesture at. Stage 3 is a working prototype inside the partner's environment. Stage 4 is a monitored, resourced deployment.

<!-- → [TABLE: Four-stage pipeline — columns: Stage, What happens, Who owns it, Evidence Ladder level; rows: 1 Open research / Fellow tests on public data / Fellow / L0–L3; 2 Proprietary replication / Partner runs holdout on internal data / Partner / L4; 3 Prototype / Built artifact in client context / Partner / L5; 4 Resourced feature / Monitored deployment / Partner / L6; firewall indicated between Stages 1 and 2] -->

The Chapter 14 brief is precisely the gate-1-to-gate-2 handoff document. It answers one question: does this public-data result earn the partner's data and engineering investment? The Fellow who tries to build the feature has confused the role. Over-building is scope creep the firewall forbids — and, practically, a Fellow on public data *cannot* reach Levels 4 through 6, because those require proprietary data and a live client context that exist only inside the partner's walls.

One blocker to name honestly before proceeding. The handoff mechanics here assume that a gate-2 partner exists, has agreed to receive briefs, and will act on them — and that the partner has signed off on the framing, including the framing of briefs that critique its own products. None of that is settled by this chapter. Whether proprietary replication is in scope, and who signs off on a brief's framing, is an open question, not a resolved arrangement. Read everything below as how the handoff works *if* the agreement lands where the book assumes, and treat that "if" as live. `[contested — see pantry, Risk 1]`

---

The brief reaches one of three verdicts. **TEST** means promising but not decisive — more public-data work, or hand to the partner for proprietary replication at gate 2. **BUILD** means the evidence, the magnitude, the compliance posture, the welfare gate, and the build cost are all sufficient — recommend resourcing. **KILL** means one threshold has failed — shelve the project, and write the rationale.

The criteria are conjunctive, and this matters: a project must pass all of them to reach BUILD. Failing any one produces a TEST or a KILL.

**Evidence strength** is the Evidence Ladder level the artifact actually reached, graded honestly. Public data tops at roughly Level 3. The grade includes the quality of the identification — a credible design, or association dressed up as causation (Chapter 5)?

**Lift or association magnitude** asks whether the effect is large enough to matter commercially. A statistically significant but economically trivial result is a kill. Significance is not size.

**Compliance risk** is flagged and routed to counsel, never adjudicated by the Fellow. MLR, FDA fair-balance, Sunshine Act, HIPAA — the brief surfaces the exposure; medical, legal, and regulatory affairs make the calls. An un-flagged compliance landmine discovered at gate 3 is far costlier than one surfaced at gate 1.

**Patient-welfare gate** is the subject of the next section. It is a required criterion, not an appendix, and it can veto.

**Build cost** is an order-of-magnitude engineering estimate — data access for proprietary replication, model and infrastructure build, monitoring. A strong-evidence, high-cost project may still be TEST rather than BUILD. The Fellow gives an order of magnitude plus the questions for the partner's engineers, not a precise number that cannot be defended.

<!-- → [DIAGRAM: Decision tree — root: scored project; first branch: evidence strength ≥ L3? No → TEST or KILL; Yes → second branch: magnitude commercially meaningful? No → KILL; Yes → third branch: compliance risk manageable? No → TEST (flag first); Yes → fourth branch: welfare gate passed? No → KILL or escalate; Yes → fifth branch: build cost tractable? No → TEST; Yes → BUILD; welfare gate shown in red to signal veto power] -->

---

The patient-welfare gate is the chapter's moral spine, and it needs to be understood as a gate rather than a gesture.

The gate asks one question: even if this works commercially, does it harm patients or the health system? The entire commercial measurement stack, as this book has documented from Chapter 2 forward, measures adoption far better than it measures welfare. A feature that lifts NBRx is not, without additional evidence, a feature that helps patients. The gate is what operationalizes that critique at the moment of a resource decision.

Four patterns trigger the gate. The first is suppression of clinically appropriate generic substitution — the coupon case, where a co-pay assistance program lifts branded share by making the branded drug cheaper to the patient but not to the system, substituting for a bioequivalent generic and raising costs without clinical benefit. The second is targeting physician susceptibility rather than patient need — the proxy case, where a personalization model optimizes on commercial responsiveness and ends up targeting physicians whose prescribing is most moveable rather than most appropriate. The third is moving prescribing of low-clinical-value drugs — the ICER-mismatch case, where the drug being promoted scores poorly on added benefit relative to available alternatives. The fourth is intensifying EHR-embedded messaging in the safety-alert layer — the opening case of this chapter.

The welfare gate is a *decision*, not a footnote. A project can be commercially excellent and still be killed on welfare grounds, and the chapter is designed so that the Fellow can hold that kill. What the Fellow cannot do is adjudicate legality. "This suppresses generic substitution and raises system cost with no clinical benefit" is a welfare finding the Fellow can defend. "This is illegal" is a conclusion for counsel.

The most important case the chapter teaches is positive-but-vetoed. A co-pay program that lifts branded share by suppressing generic substitution is a commercial win and a welfare kill. Writing the rationale for that kill — including what the partner just avoided defending to a regulator or audit committee — is the deliverable. The rejection rationale is not a consolation prize. It is what the lab produces when it works correctly.

---

For a BUILD recommendation, the brief sketches two additional things it does not run — those belong to the partner.

The **client pilot** is a prospective holdout on the partner's client data, the L4-to-L5 step that finally produces the causal readout public-data work could only approximate. This is the randomized holdout design from Chapter 8, run at scale with live clinical data: treated physicians versus a randomly held-out group from the same target list, measured on the real dependent variable over a defined window with claims-lag accounting.

The **post-launch monitoring plan** is the standing welfare check that does not end at launch. A shipped feature with no monitoring plan fails the brief. Level 6 is monitored deployment — continuous effectiveness tracking, compliance audit, and ongoing patient-welfare checking so that a harm pattern that emerges after deployment is caught. The monitoring plan names the outcomes tracked, the frequency, the ownership, and the threshold for escalation or shutdown.

The misconception to kill: once it ships, the research is done. It is not. The welfare gate does not issue a one-time clearance. It issues a requirement for continuous monitoring, because the harms the gate exists to prevent can emerge gradually, or in subpopulations, or only after the feature has been running long enough for its effects to accumulate.

---

Here is the full brief for two projects — one kill on commercial grounds, one on welfare grounds — as a Fellow would hand them to a partner team.

---

> **PRODUCT-HANDOFF BRIEF**
> **Project:** C1 — Ensemble vs. routed ("MoE") model on NPI propensity
> **Verdict: KILL (architecture investment)**
>
> **Question.** Does a routed/mixture-of-experts model meaningfully beat a tuned gradient-boosting baseline on the partner's core NPI-propensity task?
>
> **Evidence strength.** Evidence Ladder L3 — a small offline benchmark, not a causal readout. Appropriate for an architecture decision. Both models tuned with equal, logged effort; evaluated on out-of-time validation, calibration (Brier score and reliability diagram), and subgroup robustness — not AUC alone.
>
> **Magnitude.** The tuned LightGBM baseline matched the routed model on AUC and beat it on calibration; subgroup robustness was equivalent. No operational gain from routing.
>
> **Compliance flags (routed, not adjudicated).** None material — internal model bake-off, no HCP-facing content. No MLR action required at this stage.
>
> **Patient-welfare gate.** Pass. A "no lift" finding protects indirectly: it avoids committing resources to a less-interpretable system with no measured benefit.
>
> **Build cost.** The routed architecture would add substantial training and inference complexity and reduce interpretability, for no measured gain. Cost clearly exceeds value.
>
> **Recommendation.** Kill the routed-architecture investment; keep the tuned ensemble. Do not advance to gate 2. The "no" saves engineering budget — the expected outcome given what the evidence on tree ensembles versus deep learning on medium tabular data predicts (Grinsztajn et al., NeurIPS 2022 `[verify]`).
>
> **What would change the verdict.** A future task with genuine sequence or multi-task structure where routing's design advantages apply, and an equally tuned benchmark showing a meaningful, calibration-confirmed gain.

---

> **PRODUCT-HANDOFF BRIEF**
> **Project:** D2 — Co-pay coupon generic-suppression estimate
> **Verdict: KILL (welfare gate), with escalation**
>
> **Evidence strength.** L3; heterogeneity-robust difference-in-differences on coupon-legality variation, valid pre-trends. *Note: stated at the state-quarter level — individual substitution is inferred, not directly observed. Ecological-inference flag stands.*
>
> **Magnitude.** Commercially positive — the coupon program lifts branded share. Mechanism: suppression of bioequivalent-generic substitution (Dafny, Ody & Schmitt 2017 `[verify]`).
>
> **Compliance flags (routed).** Coupons banned in Medicare; state-law variation on Medicaid and commercial. Route any legality characterization to counsel — not adjudicated here.
>
> **Patient-welfare gate.** Fail. The commercial lift *is* generic suppression — higher system cost, no clinical benefit. The welfare gate vetoes.
>
> **Recommendation.** Kill as a product to optimize. Escalate the finding to compliance and medical-commercial as a risk the partner should know it carries. The rejection rationale is the deliverable: it tells the partner what it just avoided defending to a regulator or audit committee. Framing requires partner sign-off given the standing partner-agreement blocker. `[Risk 1]`
>
> **What would change the verdict.** Evidence that the branded drug produces clinically meaningful benefit above the generic comparator — in which case the welfare analysis changes materially, and the brief would route to ICER for a value assessment before reconsidering.

---

Two features of both briefs are worth naming explicitly. The verdict is the first line, not the last. And the "what would change the verdict" field is not a hedge — it is the scientific commitment that keeps the kill from being arbitrary. A brief without that field is opinion, not analysis.

---

The capstone AI disclosure for this chapter carries a higher bar. Three judgments require human expertise no AI can supply.

The first is true evidence status — what level the work actually reached, and what it cannot claim. An LLM will accept a before/after comparison as Level 4 if you describe it confidently. The ladder level is a claim about the world, not about the text.

The second is real-versus-noise signal — whether the effect is real or an artifact of selection, a benchmarked metric that was chosen post-hoc, or a surrogate that never connected to the outcome that matters. An LLM cannot tell the difference between a result and a result-shaped number.

The third is partner-defensibility — whether the partner could defend the recommendation to a regulator or an audit committee. This is a judgment about the partner's specific situation, the current regulatory environment, and the framing choices that change what a recommendation means when it leaves the Fellow's hands. It cannot be delegated.

---

**Five-Part AI Exercise Block**

**When to use AI here.** Drafting the brief's structure, turning a scored card into prose, drafting the client-pilot and monitoring sketch, generating the "what would change my mind" section. AI is useful for format and for surfacing criteria you might forget to address.

**When NOT to use AI here.** The verdict, the welfare gate judgment, the evidence level, and the partner-defensibility call. These are the human judgments the entire book has been building toward. An LLM that defaults to BUILD on a positive result, or treats the welfare gate as a checkbox rather than a veto, has made the most important error in the chapter.

**LLM exercise (copy-paste prompt):**
> "Here is a scored project: [PASTE CARD]. Write a product-handoff brief recommending build, test, or kill. Apply the patient-welfare gate as a binding veto criterion, not a checkbox."

Audit the output against three questions: Did it default to BUILD on a positive result? Did it apply the welfare gate as a veto or a footnote? Did it adjudicate compliance instead of routing it? Rewrite every place it overstepped, and note the specific judgment the model got wrong.

**CLI exercise.** Use a script to assemble the brief from your Chapter 13 artifacts — pulling the scored card, the calibration plots, and the kill-criterion result into a single rendered document. The verdict must be computed from your stated criteria (so the logic is auditable) rather than asserted. If the kill criterion was met before the brief runs, the script should output KILL automatically; the human's job is to write the rationale, not to decide the verdict again.

**AI validation exercise.** Run the brief through the Chapter 10 validation harness at a higher bar: every cited figure resolves and is correctly labeled vendor-sourced, independent, or contested; no causal claim exceeds the ladder level; the welfare gate is applied as a binding criterion; no legal conclusion is adjudicated. Document the one judgment the AI got fluently wrong — the place where it produced a confident, well-formatted, incorrect call.

**AI Use Disclosure**

*Write three sentences — one per judgment — naming what required human expertise the AI could not supply across the whole project: (1) the true evidence status of your result; (2) whether the effect is real or an artifact; (3) whether the partner could defend your recommendation to a regulator. These are the three places the book has been preparing you to stand, and they are the three places AI cannot stand for you.*

---

**What Would Change My Mind**

I would revise the claim that public-data work cannot reach Level 4 if a public dataset emerged with credible exposure-level and protected-attribute data that supported a prospective causal readout — that dataset does not exist today. I would revise the welfare gate as a binding veto if evidence showed that it systematically kills projects that, in proprietary replication, turn out welfare-neutral — the gate's design assumes that the cost of a false BUILD (a harmful shipped feature) exceeds the cost of a false KILL (a shelved good idea), and that assumption is itself contestable and should be tested empirically rather than accepted as given. I would revise the entire handoff architecture if the partner agreement did not materialize — in which case the honest response is to report that the lab's core mechanism is blocked, not to pretend the handoff is operational.

**Still Puzzling**

- The welfare gate trades a false BUILD against a false KILL. Who decides the exchange rate, on what authority, when the Fellow is told to route policy conclusions to counsel? Is the gate a judgment the Fellow makes or a flag the Fellow raises — and if it is a flag, who holds the veto?
- The brief's most commercially inconvenient outputs — "the lift is inflated," "the coupon suppresses generics," "the routed model loses" — are exactly the ones that critique the partner at the moment of a resource decision. "Collaborative de-risking" is a stable framing when the kills are small. Does it hold when a kill costs the partner a product line?
- Post-launch monitoring is required by the brief. But the Fellow cannot see Stage 2 onward. Who runs the standing welfare check after handoff, against what criteria, and with what obligation to report back?

---

## Exercises

**Warm-up**

1. *(Factual recall — the decision structure)* State the three verdicts the brief can reach and the conditions under which each is appropriate. Then explain in one sentence why the criteria are conjunctive rather than weighted — why a single failed criterion produces a non-BUILD result regardless of how strong the others are.
   *What this tests: the logical structure of the decision, not just the vocabulary.*

2. *(Factual recall — the welfare gate)* Name the four patterns that trigger the patient-welfare gate. For each, write one sentence explaining the mechanism of harm — why the commercial metric goes up while patient or system welfare goes down.
   *What this tests: understanding the gate's content, not just its existence as a criterion.*

3. *(Factual recall — pipeline and ownership)* State which stages of the four-stage pipeline the Fellow owns and which the partner owns. Explain in one sentence why the Fellow cannot reach Level 4 on public data, and what specifically the partner brings to Stage 2 that public data cannot supply.
   *What this tests: the ownership boundary and the Evidence Ladder ceiling, understood as a structural fact rather than a rule.*

**Application**

4. *(Apply — opening case verdict)* Take the opening case prototype — engagement lift, no incrementality, EHR-layer flags. Write the one-paragraph verdict with its reasoning. Then state the single piece of evidence that would flip it from TEST to BUILD, and the single piece that would flip it to KILL.
   *What this tests: applying the full decision machinery to a case the chapter introduced but did not close.*

5. *(Apply — welfare veto)* A project shows commercially strong results at L3, low build cost, no compliance flags — and fails the welfare gate because it moves prescribing of a drug with low ICER added-benefit scores. Write the KILL rationale as a partner would need to read it: what the partner avoided, what would change the verdict, and how to frame it given that the partner must sign off on the framing. Hold the kill — do not soften it into a TEST.
   *What this tests: writing a defensible rejection against commercial pressure, including the framing constraint.*

6. *(Apply — engineering estimate)* A BUILD candidate requires proprietary data access, a model retrained on the partner's NPI panel, and a 90-day holdout. You are not an MLOps engineer. Write the order-of-magnitude engineering estimate the brief requires — what you can say with confidence, and the three questions you would ask the partner's engineers to sharpen it.
   *What this tests: producing an honest estimate that acknowledges limits rather than a false precision.*

**Synthesis**

7. *(Synthesize — the monitoring plan)* A BUILD brief has been approved and the feature is moving to gate 3. Sketch the post-launch monitoring plan: what outcomes are tracked, at what frequency, by whom, and what threshold triggers escalation or shutdown. Include at least one welfare outcome alongside the commercial outcomes, and name the party responsible for the welfare check after the Fellow's involvement ends.
   *What this tests: designing the L6 accountability structure, connecting the welfare gate at decision time to the standing welfare check after deployment.*

8. *(Synthesize — full brief)* Take your Chapter 13 scored project and produce the full product-handoff brief with all required fields: one-line verdict; evidence strength with honest ladder level; magnitude; compliance flags routed to counsel; patient-welfare gate result; order-of-magnitude engineering estimate with partner questions; recommended next gate; and — if BUILD — a one-paragraph client-pilot and post-launch monitoring sketch, or — if KILL — a written rejection rationale with "what would change the verdict." A defensible kill earns full marks.
   *What this tests: the terminal deliverable of the book — the Fellow's brief as a complete, honest, actionable document.*

**Challenge**

9. *(Open-ended — the exchange rate problem)* The welfare gate assumes that the cost of a false BUILD — a harmful shipped feature — exceeds the cost of a false KILL — a shelved good idea. Construct the strongest possible argument that this assumption is wrong in a specific commercial context, then construct the counterargument. On what empirical question does the exchange rate actually depend, and what data would you need to set it on something other than assumption?
   *What this tests: holding the welfare gate's design as a testable assumption rather than a moral given, and identifying the evidence that would adjudicate it.*
