# Chapter 11 — The External Innovation Lab Operating Model (and the IP Firewall)
*The lab's product is reduced uncertainty, not a shipped platform.*

Ten interesting papers land in a Fellow's inbox at the end of week one. One proposes a new routing architecture for tabular data. One reports that physician brand loyalty survives three generic entries. One finds that disclosure laws change what physicians *report* but not what they *prescribe*. One claims a transformer beats gradient boosting on a healthcare benchmark. Ten papers, each plausibly relevant to lift or brand, each with a reasonable claim on the next few weeks of work.

Here is the trap this chapter exists to defuse. Interesting is not the same as testable, and testable is not the same as worth testing. The Fellow who tries to evaluate all ten produces ten shallow summaries that sit in a shared drive and change nothing. The Fellow who runs the lab picks the one or two where a small public-data test could actually move an idea forward — and writes a one-page memo that earns or refuses engineering resources.

That memo is the artifact. Its job is a defensible go or kill. The chapter is how you produce it.

---

Start with what the lab actually is, because most of the operating mistakes follow from a wrong answer to that question.

The lab's role, stated plainly, is to *reduce the partner's uncertainty, not to own production.* This is a real operational distinction, not a modesty posture. The lab is an inbound innovation engine: it pulls external, public research into a commercial relationship, tests the credible hypotheses cheaply on public data, and routes the survivors outward to a commercial owner who can resource them. The Fellow's deliverable is a credible test-build-kill, not a shipped feature.

Confusing the two — trying to build the platform — is how a lab loses its independence and its value at the same time. A lab that owns production is now accountable for production; it cannot publish critical findings about the thing it is responsible for shipping; it has traded its most important asset — the ability to say something inconvenient — for a production role that a vendor could fill more cheaply.

The management literature has a name for this structure: open innovation — "a distributed innovation process based on purposively managed knowledge flows across organizational boundaries" (Bogers, Chesbrough & Moedas, *California Management Review*, 2018). In pharma, this is not exotic. Industry-reported figures suggest roughly 45% of large-biopharma pipelines were externally sourced around 2020, through licensing, university partnerships, and M&A. `[verify this figure against primary industry sources]` Named structures — Takeda's Center for External Innovation is one example — exist to manage exactly this flow. The lab is the inbound half of that flow, specialized to commercial measurement rather than drug development.

<!-- → [DIAGRAM: Inbound innovation funnel — left side labeled "External research / public data / vendor claims," center labeled "Lab: scout → hypothesize → test → score → go/kill," right side labeled "Partner: proprietary replication → prototype → resourced product"; firewall drawn as a vertical line between lab and partner; arrows cross the firewall only via the handoff brief] -->

---

The lab runs a six-step funnel, and the steps matter more than the tools.

**Scout.** Surface signals from research, vendor claims, and the field. The ten-paper inbox is the scouting output. The scouting pass produces a watch list, not an agenda.

**Hypothesize.** For each idea that clears the watch list, name the *riskiest assumption* it makes about the partner's commercial reality, and tie that assumption to a KPI — lift or brand, from Chapter 2. The hypothesis is not "this paper is interesting"; it is "this paper rests on the assumption that X holds in our context, and if X fails, the whole idea fails." A hypothesis that cannot be killed is not a hypothesis.

**Design a cheap test.** The lean-startup vocabulary is precise here: a minimum viable experiment that produces *validated learning* — reducing uncertainty by testing the riskiest assumption against real signal, with the least effort (Ries, *The Lean Startup*). The cheap test is not a proof. It is a filter. Its job is to kill bad ideas early, before the partner has spent six engineering months on them. A cheap test that comes back negative is not a failure; it is the lab working correctly.

**Run it and score the evidence.** Execute the test on public data and grade what you got. The grading vocabulary is the Evidence Ladder, introduced in the next section.

**Gate: go or kill.** Confront the result against criteria set in advance, before you ran the test. This is Stage-Gate logic (Cooper): stages separated by gates where a cross-functional team decides go or kill against predefined criteria, so weak concepts are filtered early and only the strongest graduate to the next stage. The criteria must be written *before* the test runs. A kill criterion defined after seeing the result is not a criterion; it is rationalization.

**Write the handoff.** If the test earns a go, produce the memo that places the artifact on the Evidence Ladder, routes the compliance flags, and recommends the next investment stage. If the test produces a kill, write that too — a documented kill is as valuable as a go, because it saves the partner from a mistake.

The funnel exists to make cheap mistakes instead of expensive ones.

---

The Evidence Ladder is the lab's shared vocabulary for where any artifact stands. It is not a citation to an external standard; it is this book's own construct, synthesized from two well-established axes: a maturity axis adapted from NASA's Technology Readiness Levels (TRL 1–9, basic principles through flight-proven) and an evidential-strength axis adapted from the Oxford Centre for Evidence-Based Medicine Levels of Evidence (OCEBM 2011, from systematic reviews of RCTs down to mechanism-based reasoning). Both axes matter, because the lab needs to talk about how mature an idea is *and* how strong the evidence for it is, in one breath.

<!-- → [TABLE: Evidence Ladder 0–6 — columns: Level, Evidence, What it unlocks; rows: 0 = interesting paper or vendor claim / Watch only; 1 = plausible hypothesis mapped to a KPI / Fellow brief; 2 = reproducible benchmark or simulation on public data / Internal discussion; 3 = small offline test that beats the baseline / Product discovery; 4 = prospective pilot or holdout study / Product resourcing; 5 = client-validated incremental impact / Roadmap candidate; 6 = monitored deployment with compliance and patient-welfare checks / Product feature] -->

Two rules make the ladder operational.

First: every handoff brief must name its artifact's level. Vague enthusiasm is not a level. "This is promising" is not a level. A number between zero and six is a level, and it commits to a specific evidence claim that can be checked.

Second, and this is the firewall in disguise: **a Fellow working on public data tops out around Level 3.** A small offline test that beats the baseline is approximately the most a public dataset can buy. The ten papers in the opening case mostly aspire to Level 2 or 3. Levels 4 through 6 — a prospective pilot, a client-validated incremental result, a monitored deployment — require the partner's proprietary data and infrastructure. That boundary is not a failure of ambition. It is the firewall made concrete: the rung where the work crosses from the Fellow's side of the wall to the partner's.

Understanding why this ceiling exists, rather than just accepting it, is what makes it useful. Public data cannot tell you how a message performed on a specific partner's NPI list, inside the partner's campaign window, against the partner's commercial baseline. Those are proprietary facts. The best a public-data test can do is establish whether the *method* is sound and the *signal* is present in the structure of the problem — which is exactly what earns the partner's confidence to replicate it internally.

---

The ladder describes evidence; the four-stage productization pipeline describes ownership.

**Stage 1 — open research — is the Fellow's stage.** Scan, hypothesize, test on public data, score. Tops out at Ladder Level 3. The work is publishable because it uses only public data and public methods.

**Stage 2 — proprietary replication — is the partner's stage.** The partner re-runs the method that passed Stage 1 on its own data, internally. This is where Levels 4 through 6 become reachable. It is the first stage on the partner's side of the firewall.

**Stage 3 — prototype.** A working prototype inside the partner's environment.

**Stage 4 — resourced.** A funded product effort with an owner.

The Fellow owns Stage 1 and writes the handoff that recommends whether Stage 2 should happen. The Fellow does not do Stage 2. That is the operational meaning of "test on public data, hand off for proprietary replication" — not a modest self-limitation, but the precise definition of the role.

<!-- → [DIAGRAM: Four-stage pipeline — horizontal flow: Stage 1 (Fellow) → handoff brief crossing firewall → Stage 2 (Partner internal) → Stage 3 (Partner prototype) → Stage 4 (Partner production); Evidence Ladder levels annotated under each stage: 1–3 under Stage 1, 4 under Stage 2, 5 under Stage 3, 6 under Stage 4; firewall drawn between Stage 1 and Stage 2] -->

---

The IP firewall is the defining constraint of the partner collaboration, and it is worth understanding as a structure rather than a rule.

The rule is simple: public data and public methodology only, in the book and the repo. Fellows test on public datasets — CMS Open Payments, Medicare Part D, ICER value scores, syndicated or synthetic substitutes. The partner replicates promising methods on its proprietary data internally, in Stage 2. Nothing confidential — partner internal metrics, named-vendor figures, any patent or product IP — enters the public book or repo. Sensitive working material lives in `private/` (gitignored).

The structure behind the rule is why it works. The firewall protects two things simultaneously: the partner's IP *and* the Fellow's research independence. A Fellow who never touches proprietary data can publish honest findings — including critical ones — without leaking anything confidential. The partner can replicate internally without exposing its data. The Level-3 ceiling for public-data work is the firewall expressed in evidence terms; the `private/` directory is its file-system enforcement.

The failure mode to know: the firewall fails not when someone moves a file to the wrong directory, but when tainted material — a partner's internal metric, a vendor's unpublished number — reaches the output, even through an intermediary. The "clean room" principle from IP law is the model: procedures do not guarantee immunity if contaminated material reaches the final work product. The test is not whether the file was in the right folder; it is whether any partner-confidential fact could be inferred from what was published.

---

Every artifact the lab produces is screened for compliance risk across four surfaces. The lab models the flags; counsel adjudicates them. That distinction is the entire compliance posture.

**MLR review** — Medical-Legal-Regulatory — is the mandatory cross-functional review of promotional and medical content. Medical checks clinical accuracy and substantiation. Legal checks liability and IP. Regulatory checks FDA and OPDP requirements. Virtually any externally facing promotional asset triggers MLR. Vendors report cycle times of fifty to sixty days and claim AI-assisted review reduces that by fifty to sixty-five percent — both figures are vendor-reported with no neutral benchmark `[verify]`. Flag the trigger; route to counsel for the timeline.

**FDA fair balance** — under 21 CFR 202.1, product-claim promotion must present a fair balance of risk and benefit and substantiate all claims. The 2025 enforcement escalation raised the stakes on AI-generated and AI-assisted content. Any generated output that touches product claims needs this flag attached before the brief crosses the firewall.

**Sunshine Act and Open Payments** — manufacturers must annually report transfers of value to covered recipients above the de minimis thresholds, with CMS publishing the Open Payments database for public use. `[verify current-year inflation-adjusted thresholds from CMS before citing specific dollar amounts]` The public Open Payments data is also a primary research dataset for this book, so it sits on both sides of the compliance line: research input and reportable mechanism.

**HIPAA** — the de-identification Safe Harbor under 45 CFR 164.514(b) and the marketing-authorization rules under 45 CFR 164.508(a)(3) govern any use of patient-derived data. The Fellow working on NPI-level claims data is working on de-identified patient data; any design that would re-identify patients, link patient records across datasets without authorization, or use protected health information for commercial targeting needs this flag before the test runs, not after.

The frame is collaborative de-risking: the lab surfaces risk before it becomes an enforcement letter. The lab is pro-evidence, not anti-partner — and the compliance routing is what makes pointed findings publishable without exposing anyone.

---

The handoff brief is the chapter's named artifact. It is one page, eight fields, and its job is a defensible recommendation.

The eight fields are: the finding and its source; the commercial hypothesis with the riskiest assumption tied to a KPI; the cheap test with design, dataset, success threshold, and kill criterion; the result and its Evidence Ladder level; compliance flags routed to counsel; a patient-welfare note naming who benefits and who might be harmed; the likely partner owner — measurement analytics, brand strategy, data science, content ops, or compliance; and the recommendation — test next, replicate on proprietary data (Stage 2), shelve, or kill, and why.

Two fields carry most of the weight. The kill criterion must be written before the test runs — the moment you define it after seeing the result, the brief is no longer a scientific document. And the patient-welfare note is not optional — it is a required field because the lab asks who benefits and who might be harmed before recommending any idea for resources, so that welfare-relevant findings surface as gates rather than afterthoughts.

---

Here is how the funnel works on one of the ten papers.

The Fellow picks the "brand loyalty survives generic entry" paper. The finding is that physician brand loyalty appears to persist across generic entries in some drug classes. The riskiest assumption for the partner is that this persistence reflects *brand equity* rather than inertia or clinical value. The KPI is post-loss-of-exclusivity branded market share decline. The hypothesis becomes: if equity drives persistence, high-equity brands should erode slower *after controlling for clinical value*.

The cheap test: use loss of exclusivity as a natural experiment — the identification strategy Chapter 12 develops — on Medicare Part D prescriber data, with ICER value scores as the clinical-value covariate. Success threshold: a meaningful persistence effect that survives the value control. Kill criterion: no effect once value is controlled, or no usable signal in the public data.

The test runs. It finds a modest, value-adjusted persistence signal. The Evidence Ladder placement: Level 3 at most — a small offline test that beat the null, on public data, against a baseline. It cannot establish client-validated impact; that needs the partner's proprietary panel. Recommendation: replicate on proprietary data, Stage 2. The firewall hands it to the partner.

Nine of the ten papers correctly stayed at Level 0, watched but not tested. The lab's value was the selection, not the volume.

A dead end worth naming. The first instinct was to model persistence directly from Part D claims, treating high-prescription-continuity after LOE as the equity signal. Dead end: Part D does not directly observe new-to-brand prescriptions, skews heavily to an older population, and cannot cleanly separate inertia from equity without the clinical-value covariate. That limitation is exactly why the recommendation is "replicate," not "build" — the public-data result is suggestive enough to earn Stage 2, but specific enough in its limits that the partner knows what it is buying.

---

The still-puzzling question the chapter cannot close: the firewall keeps the Fellow independent and the partner's IP safe, but it also caps how far the Fellow can prove an idea before handing it over. The most consequential validation always happens out of the Fellow's sight, on the partner's side. The Stage-2 replication could confirm the finding, weaken it, or overturn it — and the Fellow has no direct access to that result. The handoff brief's explicit criteria and the partner's reciprocal reporting are the intended checks. The asymmetry is real and unresolved. A lab that cannot see its own results from Stage 2 onward is operating on a kind of scientific faith in the firewall it created.

---

**Five-Part AI Exercise Block**

**When to use AI here.** Scouting and clustering candidate findings, drafting first-pass hypotheses, generating handoff-brief boilerplate, surfacing compliance-flag candidates for human routing. AI is a fast first-pass clerk for the parts of the funnel that benefit from breadth before depth.

**When NOT to use AI here.** Deciding the go or kill, setting the kill criterion, adjudicating a compliance flag, or asserting an Evidence Ladder level. These are human judgments the brief must own. An LLM that assigns a public-data result to Level 4 or 5 has violated the firewall ceiling — and catching that violation is exactly the load-bearing human correction in this workflow.

**LLM exercise (copy-paste prompt):**
> "Here are three findings from recent research: [PASTE THREE]. For each, draft a riskiest-assumption-plus-KPI hypothesis in two sentences. Then suggest the cheapest test that could falsify the assumption, naming the public dataset you would use. Do not assign an Evidence Ladder level — that comes after the test runs."

Keep the best hypothesis from the model's output. Rewrite the rest yourself, noting where the model missed the riskiest assumption and substituted a safer one.

**CLI exercise.** Build a template script that emits an empty eight-field handoff-brief skeleton as a text file and validates, before "submission," that no field is blank and that the Evidence Ladder level is a number between 0 and 6. Run it on your own thread's brief. If any field is blank or the level is out of range, the script should refuse to produce the output file.

**AI validation exercise.** Ask an LLM to assign an Evidence Ladder level to one of your artifacts, given its data source and test design. Check the answer against the firewall rule: if the model placed a public-data result at Level 4 or above, you have caught a specific, correctable error — document it and note what the correct level is and why the ceiling holds.

**AI Use Disclosure**

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to draft first-pass hypotheses for three of the ten papers and to generate handoff-brief boilerplate; I determined myself whether the kill criterion was genuinely falsifying or had been weakened after seeing the preliminary results, because the model cannot distinguish a criterion written before from one rationalized after."*

---

**What Would Change My Mind**

If a public dataset emerged that credibly supported a prospective, client-validated incremental result — Level 4 or above — without touching proprietary data, the Level-3 public-data ceiling would move up. Today no such dataset exists for HCP commercial outcomes; Levels 4 through 6 inherently require the partner's data and operational infrastructure, which is why the firewall ceiling holds. A change in what public data makes available — a large, prospective, openly published HCP-level prescribing panel with treatment assignment recorded — would change the ceiling, but that is a dataset that does not exist.

**Still Puzzling**

- The firewall is structurally sound, but the Fellow never sees the Stage-2 replication. How does the lab maintain evidentiary discipline across that boundary — how does it know whether its Level-3 results survive the partner's proprietary test, and whether the failures are being reported honestly?
- The go/kill gate requires predefined criteria, but the riskiest assumption is often only visible *after* the preliminary results arrive. How do you write a kill criterion before you know what the test will show — and how do you distinguish genuine pre-registration from motivated post-hoc revision?
- The compliance routing posture is collaborative de-risking, not adversarial oversight. But some findings — that a targeting approach produces proxy discrimination, or that a coupon program substitutes expensive drugs for cheaper effective ones — are genuinely inconvenient. How does the lab publish those findings while maintaining a productive partner relationship, when the partner who signs off on the pointed framing has an interest in the finding being softer?

---

## Exercises

**Warm-up**

1. *(Factual recall — the lab's role)* State the lab's role in one sentence. Then explain, in one sentence, why owning production would undermine it.
   *What this tests: whether you hold the lab's fundamental identity distinct from a product team's.*

2. *(Factual recall — the Evidence Ladder)* The Evidence Ladder is described as the book's own construct, synthesized from two external frameworks. Name both source frameworks, what axis each contributes, and why both axes are needed rather than just one.
   *What this tests: understanding the ladder's architecture, not just memorizing its rungs.*

3. *(Factual recall — the firewall ceiling)* State the highest Evidence Ladder level a Fellow working on public data can typically reach, and explain in one sentence why Levels 4 through 6 require the partner's involvement.
   *What this tests: understanding the firewall as an evidence constraint, not just a data-storage rule.*

**Application**

4. *(Apply — hypothesis construction)* Take one finding from your research thread. Write its riskiest assumption — the assumption that, if false, kills the whole idea — tied to a specific KPI from Chapter 2. Then write the kill criterion you would set before running the test.
   *What this tests: distinguishing a falsifiable hypothesis from an interesting observation, and pre-committing to a kill criterion.*

5. *(Apply — Evidence Ladder placement)* A Fellow runs a difference-in-differences analysis on Medicare Part D data using a state formulary change as a natural experiment. The analysis finds a meaningful effect that beats the baseline. What Evidence Ladder level does this reach, and what would be required to move it one rung higher — and on whose side of the firewall does that next rung live?
   *What this tests: applying the ladder to a realistic public-data result and tracing the ownership boundary.*

6. *(Apply — compliance routing)* A handoff brief recommends expanding a co-pay assistance program shown to increase branded prescribing. List the compliance surfaces that need flags, name which one you would route first and why, and write one sentence on the patient-welfare note for this artifact.
   *What this tests: modeling compliance as routing across four surfaces and connecting it to the patient-welfare field.*

**Synthesis**

7. *(Synthesize — the funnel on one paper)* Walk one paper from your reading list through all six steps of the funnel: scout → hypothesis → cheap test → evidence → go/kill → handoff recommendation. The output is a one-paragraph brief for each step. For the go/kill step, commit to a recommendation — go, kill, or replicate — and defend it in one sentence.
   *What this tests: integrating the full funnel workflow on a real input, with a committed recommendation rather than a hedge.*

8. *(Synthesize — draft the handoff brief)* Draft a full one-page handoff brief for your research thread with all eight fields filled: finding, commercial hypothesis, cheap test, result and Ladder level, compliance flags routed to counsel, patient-welfare note, likely partner owner, and recommendation. The Evidence Ladder level must be defensible against the firewall ceiling.
   *What this tests: producing the chapter's named artifact at full specification — the Part B graded checkpoint.*

**Challenge**

9. *(Open-ended — the asymmetry problem)* The lab cannot see its own results from Stage 2 onward. Propose a mechanism — a reporting structure, a pre-registered protocol, or a contractual arrangement — that would give the lab meaningful evidentiary discipline across the firewall without violating the IP boundary or compromising the partner's operational confidentiality. Name the assumption your mechanism relies on and the way it could still fail.
   *What this tests: thinking structurally about the firewall's unresolved asymmetry, not just accepting it as a given.*
