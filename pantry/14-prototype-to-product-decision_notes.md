# Research Notes: Chapter 14 — From Prototype to Product Decision (The Fellows Brief)

**Chapter one-line (TIKTOC):** Fellows decide whether a project earns productization, proprietary-data replication, MLR review, engineering investment, partner client testing — or rejection — and write the brief that says so.

**Learning outcomes (TIKTOC):** (1, Evaluate) Apply explicit handoff criteria (evidence strength, lift/association magnitude, compliance risk, **patient-welfare gate**, build cost). (2, Create) Produce the product-handoff brief and the rejection rationale (a "no" is a result). (3, Apply) Stage a portfolio: test next / replicate on proprietary data / shelve / ship.

**Opening artifact (TIKTOC):** the terminal deliverable structure shown before any work — the brief a Fellow could hand the partner's team.

**Core content (TIKTOC):** handoff criteria; the four-stage pipeline revisited; the patient-welfare gate as a required criterion (not an appendix); writing the test/build/kill recommendation.

**Scope of these notes:** the handoff decision machinery — test/build/kill criteria, evidence thresholds, MLR/legal review, engineering estimate, client-pilot design, post-launch monitoring, the patient-welfare gate, and the four-stage research→product pipeline. This is the terminal chapter; it converts a scored Ch 13 project into a defensible product decision.

---

## A. Conceptual foundations

### A1. The four-stage research→product pipeline (from Ch 11, the decision spine)
**Explanation.** The lab's value is *reducing the partner's uncertainty*, not shipping product. The pipeline routes a finding through four gates, each a bigger resource commitment:
1. **Open research** — public-data test on public methodology (the Fellow's zone; Evidence Ladder L0–L3). The firewall holds here: nothing proprietary in book/repo.
2. **Proprietary replication** — the *partner* re-runs the promising method on its internal data (L4: prospective pilot/holdout). This is where public-data ideas earn proprietary resources; the Fellow hands off, the partner executes.
3. **Prototype** — a built artifact tested in a controlled client context (L5: client-validated incremental impact).
4. **Resourced product feature** — monitored deployment with compliance + patient-welfare checks (L6: product feature).
The Ch 14 brief is the **gate-1→gate-2 handoff document**: does this public-data result earn proprietary replication?
**Common misconception.** "The Fellow's job is to build the feature." No — the Fellow's job ends at "this earns (or doesn't earn) the partner's data and engineering." The handoff is the deliverable; over-building is scope creep that the firewall forbids.
**Source.** Four-stage pipeline + Evidence Ladder: TIKTOC Ch 11 (LO 1, the ladder table); `pantry/13-fellow-research-portfolio_notes.md` (ladder ceiling = firewall). Lab-reduces-uncertainty framing: TIKTOC logline + Part 1 thesis.

### A2. The handoff criteria (test / build / kill)
**Explanation.** The brief reaches one of three verdicts via explicit criteria:
- **Evidence strength** — the Evidence-Ladder level the project actually reached (be honest: public data tops at ~L3) and the quality of the identification (was it a credible design or association dressed up?).
- **Lift or association magnitude** — does it move the book's two dependent variables enough to matter commercially? A statistically significant but tiny effect is a kill.
- **Compliance risk** — MLR / FDA fair-balance / Sunshine Act / HIPAA-privacy exposure, flagged and routed (not adjudicated) to counsel.
- **Patient-welfare gate** (A3) — a *required* criterion, not an appendix.
- **Build cost** — the engineering/data estimate to take it to L4+; a strong-evidence/high-cost project may still be "test next" rather than "build."
**The three verdicts:** **TEST** (promising but not yet decisive → more public-data work, or hand to partner for proprietary replication at gate 2); **BUILD** (evidence + magnitude + acceptable compliance + passes welfare gate + tractable cost → recommend resourcing); **KILL** (fails a threshold → shelve, *with the rejection rationale written* — "a no is a result").
**Common misconception.** "The brief recommends building if the result is positive." No — a positive result that fails the welfare gate, or carries unacceptable compliance risk, or costs more than its value, is a kill or a test-next. The criteria are conjunctive, and welfare can veto.
**Source.** Handoff criteria: TIKTOC Ch 14 LO 1; staging (test next / replicate / shelve / ship) LO 3. Compliance flags as route-to-counsel: TIKTOC Ch 11 core content + Part 14 out-of-scope (legal authority routed, not adjudicated).

### A3. The patient-welfare gate (the chapter's moral spine)
**Explanation.** The welfare gate asks: even if this works commercially, does it harm patients or the health system? It is a **gate** (per Open Question 3, the author's recommendation), meaning a project can be commercially excellent and still be killed on welfare grounds. The gate operationalizes the book's central critique — the commercial stack measures adoption far better than welfare (brand-measurement §6). Concretely, the gate flags: does the project suppress clinically-appropriate generic substitution (coupon work)? does it target physician *susceptibility* rather than patient need (proxy work)? does it move prescribing of low-clinical-value drugs (ICER mismatch)? does it intensify EHR-embedded messaging in the same layer as safety alerts?
**Common misconception.** "Ethics is the final-chapter wrap-up." No — the book makes the compliance+welfare check pervasive (every chapter, Part 9 anatomy item 9); Ch 14 makes welfare a *binding decision criterion*. A Fellow who treats it as boilerplate has missed the chapter.
**Worked example.** A Track-D coupon project shows a coupon program lifts branded share (commercial win) by suppressing generic substitution (welfare loss → higher system cost, no clinical benefit). Welfare gate → KILL or escalate, regardless of the commercial lift.
**Source.** Patient-welfare gate as required criterion: TIKTOC Ch 14 LO 1 + core content; Open Question 3 (recommend: gate). Welfare-measurement gap: `pantry/pharma-brand-measurement-synthesis.md` §6; `pantry/pharma-marketing-evidence-synthesis.md` §8 (the structural market failure).

### A4. MLR / legal review and the engineering estimate
**Explanation.** Two practical gates a buildable project must pass:
- **MLR (Medical/Legal/Regulatory) + legal review** — pharma content/claims run through MLR (historically 50–60 days/piece; AI is compressing this). Any Fellow recommendation that would generate HCP-facing claims or content must flag MLR load and FDA fair-balance risk (the 2025 FDA enforcement wave makes this live). The Fellow *flags and routes*; counsel/medical-affairs adjudicates.
- **Engineering/data estimate** — a rough order-of-magnitude of what gate-2/3 costs: data access (proprietary replication), model/infra build, monitoring. The estimate turns "good idea" into "good idea worth $X" — the input the partner's resourcing decision actually needs.
**Common misconception.** "Compliance is someone else's problem after handoff." No — an un-flagged compliance landmine discovered at gate 3 is far costlier; the brief's job is to surface it at gate 1.
**Source.** MLR cycle times + AI acceleration + 2025 FDA enforcement: `pantry/pharma-ai-hcp-marketing-synthesis.md` §4 (MLR), §5 (FDA enforcement wave). Compliance-flag discipline: TIKTOC Part 9 anatomy item 9.

### A5. Client-pilot design and post-launch monitoring (gates 3–4)
**Explanation.** For BUILD recommendations, the brief sketches (it doesn't run — that's the partner's) the **client-pilot** (a prospective holdout/RCT-style test on the partner's client data — the L4→L5 step that finally gets a *causal* readout the public-data work couldn't) and the **post-launch monitoring** plan (L6): ongoing effectiveness tracking, compliance audit, and a **standing patient-welfare check** so the welfare gate doesn't end at launch. Monitoring is where the accountability-framework work (Track D3) lands operationally.
**Common misconception.** "Once it ships, the research is done." No — L6 is *monitored* deployment; the welfare and compliance checks are continuous. A shipped feature with no monitoring plan fails the brief.
**Source.** Ladder L4–L6 (TIKTOC Ch 11 table); accountability framework → monitoring (`pantry/13-fellow-research-portfolio_notes.md` Track D3); holdout as the causal gold standard (Ch 8).

---

## B. Domain examples and the failure case

- **BUILD example (Track C "no-lift protects the partner" inverted).** A B-track LOE-persistence finding (B4) shows brand equity meaningfully slows post-LOE erosion *and* aligns with clinical value (ICER) → commercial value, passes welfare gate (not value-divorced), tractable replication cost → **TEST→BUILD**: hand to brand strategy for proprietary replication (gate 2).
- **TEST example.** A Track-A attribution audit (A1) credibly shows vendor lift is inflated but the public-data design can't pin the true effect (L2–L3) → **TEST**: recommend the partner run the proper holdout on proprietary data (gate 2) — the Fellow has reduced uncertainty about *which* claim to trust without resolving it.
- **KILL example (welfare veto).** Track-D coupon project (D2): commercially positive (coupons lift branded share) but the lift *is* generic suppression with no clinical benefit → **welfare gate KILL**, with a written rejection rationale that is itself a publishable/partner-valuable result.
- **KILL example (magnitude).** Track-C MoE benchmark (C1): routed model statistically beats XGBoost by a hair, worse calibration, large infra cost → **KILL** on magnitude + cost; the "no" saves the engineering budget (the TIKTOC worked example's expected outcome).
- **FAILURE CASE — the brief that recommends BUILD on L2 association + ignores welfare.** A Fellow excited by a positive associational result writes a confident BUILD brief, omits the patient-welfare gate, and under-states MLR risk. At gate 3 the partner discovers the "lift" was selection (no causal basis), the content trips fair-balance, and the feature suppresses substitution. The brief failed precisely on the chapter's load-bearing items: honest ladder level, the welfare gate as a *gate*, and compliance flagged *early*. (This is the anti-pattern the final AI Use Disclosure's higher bar targets — naming the judgments AI couldn't make: true evidence status, real-vs-noise signal, partner-defensibility.)

---

## C. Connections and dependencies

- **Prereqs:** Ch 11 (the lab model, four-stage pipeline, Evidence Ladder, IP firewall); Ch 13 (the scored project being handed off — its ladder level + flags are the brief's inputs); Ch 8 (why the public-data result usually can't reach L4 without a holdout); Ch 5 (evidence quality — the brief's honesty about evidence grade).
- **Unlocks:** terminal — this is the book's final deliverable (the product-handoff brief, 200 pts). Closes the three-act arc (System → Toolkit → Lab).
- **Adjacent:** every Track's welfare/compliance flags (Ch 13) feed the gate; the accountability framework (D3) becomes the monitoring plan (A5).

---

## D. Current state of the field / key references

- **MLR acceleration is real but governance-limited:** McKinsey estimates 50–65% submission-timeline reduction from AI MLR tools (methodology unspecified), yet promotional volume rose 29% YoY in 2025 with 77% of approved content rarely used, and an MIT analysis found 95% of generative-AI pilots failing — "the problem is governance, not generation speed" (`pantry/pharma-ai-hcp-marketing-synthesis.md` §4). The brief should be skeptical of "AI makes MLR free."
- **FDA enforcement is live again:** the Sept 2025 wave (200+ letters, AI-powered ad surveillance) reversed a decade of lax enforcement; fair-balance/efficacy-exaggeration are the top violations — directly relevant to any content-generating BUILD recommendation (`synthesis` §5). EHR-integrated advertising remains a regulatory gray zone (no specific OPDP guidance) — a flag, not a green light.
- **Welfare gate has policy backing:** ICER value framework + the "most-promoted drugs have low added benefit" findings give the welfare gate empirical teeth (`pantry/pharma-brand-measurement-synthesis.md` §6; `pharma-marketing-evidence-synthesis.md` §4).
- **`[verify]`:** McKinsey 50–65% figure (methodology); MIT 95%-pilot-failure stat; current FDA/OPDP guidance status on EHR advertising; MLR cycle-time numbers (drift).

---

## E. Teaching considerations

- **Show the deliverable first** (TIKTOC opener): the brief structure on the page before any work, so students reverse-engineer toward it. The brief = verdict (test/build/kill) + evidence grade (ladder level) + magnitude + compliance flags (routed) + welfare-gate result + engineering estimate + recommended next gate.
- **A "no" is a graded result.** The rejection rationale is assessable and valuable; teach students to write a *good* kill (what would change the verdict, what the partner just avoided spending). Counters vendor-deck optimism culture.
- **The welfare gate is a veto, not a checkbox.** Run a case where commercial and welfare verdicts diverge (coupon project) and make students hold the kill. This is the chapter's hardest teaching moment.
- **Higher-bar AI Use Disclosure (TIKTOC):** name three judgments across the project that required human expertise no AI could supply — true evidence status, real-vs-noise signal, partner-defensibility. This is the capstone of the book's AI-honesty thread.
- **Named Fellow artifact:** the **product-handoff brief + rejection rationale** (the terminal deliverable). Series anatomy items 8/9/10/13/18 enforced.
- **Decision-tree teaching aid:** ladder level <L3 or association-only → TEST (or hand to gate 2); L3 + meaningful magnitude + passes welfare + acceptable compliance + tractable cost → BUILD; fails welfare OR fails magnitude OR unacceptable compliance → KILL (with rationale).

---

## F. Library files relevant (in `pantry/` as `_lib_*`)

- `_lib_ai-the-alignment-problem-machine-learning-and-human-values.md` — values/accountability grounding for the patient-welfare gate and the monitoring plan (A3, A5).
- `_lib_math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` — the "deployed model needs monitoring/accountability" argument (post-launch welfare check, A5; Track D handoffs).
- `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md` — the holdout/prospective-pilot (L4) design the BUILD path's client pilot requires (A5).
- `_lib_science-calling-bullshit-the-art-of-skepticism-in-a-data-driven-world.md` — skeptical-reading discipline for grading evidence honestly (the brief's evidence-strength criterion; the failure-case anti-pattern).
- (Reused syntheses, not `_lib_`:) `pharma-ai-hcp-marketing-synthesis.md` (MLR §4, FDA enforcement §5), `pharma-brand-measurement-synthesis.md` (welfare gap §6), `pharma-marketing-evidence-synthesis.md` (market failure §8), `13-fellow-research-portfolio_notes.md` (the project inputs + ladder ceiling), `12-research-design-public-data_notes.md` (why public data tops at L3).

---

## G. Gaps and flags

- **G1. The BLOCKER lives here too (TIKTOC Risk 1 / Open Question 1).** Whether/what proprietary replication (gate 2) is in scope, and who signs off on the brief's framing, is *unresolved with the partner*. Ch 14's handoff mechanics assume a gate-2 partner exists and will act — confirm before drafting the chapter as operational fact.
- **G2. Patient-welfare gate vs. capstone (Open Question 3).** TIKTOC recommends gate; if the partner/author lands on capstone instead, A3 and the decision tree change materially. Flag as a design decision, not settled.
- **G3. Adversarial-tone tension (Risk 2/4).** The KILL-on-welfare path (coupon, proxy) critiques partner products at the moment of a *resource decision* — the most sensitive point. The brief must be collaborative-de-risking in framing, route legal characterization to counsel, and may need partner sign-off on the kill rationale.
- **G4. Engineering estimates are out of the Fellow's expertise** (Learner Profile: not MLOps engineers). The brief should give an order-of-magnitude + the questions for the partner's engineers, not a precise estimate it can't defend.
- **G5. Compliance is flagged, never adjudicated** (Part 14 out-of-scope). Any brief that *concludes* on legal/regulatory permissibility has overstepped; the discipline is route-to-counsel.
- **G6. `[verify]`:** McKinsey MLR 50–65%; MIT 95% pilot-failure; current OPDP guidance on EHR advertising; MLR cycle-time figures.
