# Chapter 11 — The External Innovation Lab Operating Model (and the IP Firewall)
*The lab's product is reduced uncertainty, not a shipped platform.*

Ten interesting papers land in a Fellow's inbox at the end of week one. One proposes a new routing architecture for tabular data. One reports that physician brand loyalty survives three generic entries. One finds that disclosure laws change what physicians *report* but not what they *prescribe*. One claims a transformer beats gradient boosting on a healthcare benchmark. Ten papers, each plausibly relevant to lift or brand, each with a reasonable claim on the next few weeks of work.

Here is the trap this chapter exists to defuse. Interesting is not the same as testable, and testable is not the same as worth testing. The Fellow who tries to evaluate all ten produces ten shallow summaries that sit in a shared drive and change nothing. The Fellow who runs the lab picks the one or two where a small public-data test could actually move an idea forward — and writes a one-page memo that earns or refuses engineering resources.

That memo is the artifact. Its job is a defensible go or kill. The chapter is how you produce it.

---

Start with what the lab actually is, because most of the operating mistakes follow from a wrong answer to that question.

The lab's role, stated plainly, is to *reduce the partner's uncertainty, not to own production.* This is a real operational distinction, not a modesty posture. The lab is an inbound innovation engine: it pulls external, public research into a commercial relationship, tests the credible hypotheses cheaply on public data, and routes the survivors outward to a commercial owner who can resource them. The Fellow's deliverable is a credible test-build-kill, not a shipped feature.

Confusing the two — trying to build the platform — is how a lab loses its independence and its value at the same time. A lab that owns production is now accountable for production; it cannot publish critical findings about the thing it is responsible for shipping; it has traded its most important asset — the ability to say something inconvenient — for a production role that a vendor could fill more cheaply.

The management literature has a name for this structure: open innovation — "a distributed innovation process based on purposively managed knowledge flows across organizational boundaries, using pecuniary and non-pecuniary mechanisms in line with the organization's business model" (Bogers, Chesbrough & Moedas, *California Management Review* 60(2):5–16, 2018). In pharma, this is not exotic. McKinsey estimates that roughly 45% of the pipeline assets of the top-20 biopharma companies (by R&D budget) were externally sourced around 2020, through licensing, collaborations, university partnerships, and M&A (McKinsey & Company, "Innovation sourcing in biopharma"). Named structures — Takeda's Center for External Innovation, established as part of its 2015–2016 R&D restructuring, is one example — exist to manage exactly this flow. The lab is the inbound half of that flow, specialized to commercial measurement rather than drug development.

![Inbound innovation funnel showing external research and public data flowing into the lab, which scouts, hypothesizes, tests, scores, and decides go or kill; a vertical dashed IP firewall separates the lab from the partner, with a single handoff brief arrow crossing it into the partner's proprietary replication, prototype, and resourced-product stages.](../images/11-innovation-lab-operating-model-fig-01.png)

*Figure 11.1 — The inbound innovation funnel and the IP firewall*

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

| Level | Evidence | What it unlocks |
| --- | --- | --- |
| 0 | Interesting paper or vendor claim | Watch only |
| 1 | Plausible hypothesis mapped to a KPI | Fellow brief |
| 2 | Reproducible benchmark or simulation on public data | Internal discussion |
| 3 | Small offline test that beats the baseline | Product discovery |
| 4 | Prospective pilot or holdout study | Product resourcing |
| 5 | Client-validated incremental impact | Roadmap candidate |
| 6 | Monitored deployment with compliance and patient-welfare checks | Product feature |

*Table 11.1 — The Evidence Ladder (this book's own construct). Levels 0–3 are reachable on public data; Levels 4–6 require the partner's proprietary data and infrastructure.*

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

![Four-stage productization pipeline running left to right: Stage 1 (Fellow, open research on public data, Evidence Ladder Levels 1 to 3), a handoff brief crossing a vertical dashed IP firewall, then Stage 2 (Partner internal proprietary replication, Level 4), Stage 3 (Partner prototype, Level 5), and Stage 4 (Partner production, Level 6). The firewall sits between Stage 1 and Stage 2.](../images/11-innovation-lab-operating-model-fig-02.png)

*Figure 11.2 — The four-stage productization pipeline*

<!-- → [DIAGRAM: Four-stage pipeline — horizontal flow: Stage 1 (Fellow) → handoff brief crossing firewall → Stage 2 (Partner internal) → Stage 3 (Partner prototype) → Stage 4 (Partner production); Evidence Ladder levels annotated under each stage: 1–3 under Stage 1, 4 under Stage 2, 5 under Stage 3, 6 under Stage 4; firewall drawn between Stage 1 and Stage 2] -->

---

The IP firewall is the defining constraint of the partner collaboration, and it is worth understanding as a structure rather than a rule.

The rule is simple: public data and public methodology only, in the book and the repo. Fellows test on public datasets — CMS Open Payments, Medicare Part D, ICER value scores, syndicated or synthetic substitutes. The partner replicates promising methods on its proprietary data internally, in Stage 2. Nothing confidential — partner internal metrics, named-vendor figures, any patent or product IP — enters the public book or repo. Sensitive working material lives in `private/` (gitignored).

The structure behind the rule is why it works. The firewall protects two things simultaneously: the partner's IP *and* the Fellow's research independence. A Fellow who never touches proprietary data can publish honest findings — including critical ones — without leaking anything confidential. The partner can replicate internally without exposing its data. The Level-3 ceiling for public-data work is the firewall expressed in evidence terms; the `private/` directory is its file-system enforcement.

The failure mode to know: the firewall fails not when someone moves a file to the wrong directory, but when tainted material — a partner's internal metric, a vendor's unpublished number — reaches the output, even through an intermediary. The "clean room" principle from IP law is the model: procedures do not guarantee immunity if contaminated material reaches the final work product. The test is not whether the file was in the right folder; it is whether any partner-confidential fact could be inferred from what was published.

---

Every artifact the lab produces is screened for compliance risk across four surfaces. The lab models the flags; counsel adjudicates them. That distinction is the entire compliance posture.

**MLR review** — Medical-Legal-Regulatory — is the mandatory cross-functional review of promotional and medical content. Medical checks clinical accuracy and substantiation. Legal checks liability and IP. Regulatory checks FDA and OPDP requirements. Virtually any externally facing promotional asset triggers MLR. Vendors report MLR cycle times on the order of weeks to a couple of months and claim AI-assisted review compresses them substantially — but these figures are vendor-reported, vary widely by asset and organization, and have no neutral published benchmark, so treat any specific number as a vendor claim rather than an established fact. `[verify — unconfirmed: searched for neutral/peer-reviewed MLR cycle-time and AI-reduction benchmarks; only vendor-sourced figures found]` Flag the trigger; route to counsel for the timeline.

**FDA fair balance** — under 21 CFR 202.1, product-claim promotion must present a fair balance of risk and benefit and substantiate all claims. The 2025 enforcement escalation raised the stakes on AI-generated and AI-assisted content. Any generated output that touches product claims needs this flag attached before the brief crosses the firewall.

**Sunshine Act and Open Payments** — under the Physician Payments Sunshine Act (enacted 2010, reporting effective August 2013), applicable manufacturers and GPOs must annually report transfers of value to covered recipients above the de minimis thresholds, with CMS publishing the Open Payments database for public use. The thresholds are inflation-adjusted each year — for context, the 2025 values are roughly $13.46 per single payment and about $134.54 in aggregate — so confirm the current-year figures with CMS before citing any specific dollar amount in a brief. The public Open Payments data is also a primary research dataset for this book, so it sits on both sides of the compliance line: research input and reportable mechanism.

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

---

## Prompts

### Figure 11.1 — The inbound innovation funnel and the IP firewall

Generate a horizontal left-to-right process diagram (not a chart; no quantitative axes, so zero-baseline is n/a). Data shape: three primary nodes in sequence — "External" (research, public data, vendor claims), "Lab" (containing the ordered steps scout, hypothesize, test, score, and a terminal go/kill decision), and "Partner" (proprietary replication, prototype, resourced product) — plus one vertical firewall divider positioned between the Lab and Partner nodes, and two arrow edges (External→Lab, and Lab→Partner labeled "handoff brief"). Marks: rectangles for nodes (rx=0, no rounding), straight line segments for edges, a vertical dashed line for the firewall, text for labels. Channels: horizontal position encodes pipeline order; stroke color distinguishes the Lab (red accent, load-bearing) from neutral nodes; the dashed style encodes the firewall boundary. Sort: fixed pipeline order, no data-driven sorting. Annotations: firewall label "IP FIREWALL"; under-node side labels "public data · Levels 0–3" and "proprietary · Levels 4–6"; the single crossing arrow labeled "handoff brief"; a two-line caption. Deliverable: a single self-contained HTML file with inline CSS, D3 7.9.0 loaded from cdnjs, color via CSS variables, ResizeObserver redraw, and accessible title/desc.

### Figure 11.2 — The four-stage productization pipeline

Generate a horizontal left-to-right stage diagram (not a chart; zero-baseline n/a). Data shape: four ordered stage nodes — Stage 1 (Fellow, open research), Stage 2 (partner replication), Stage 3 (partner prototype), Stage 4 (partner production) — each carrying an Evidence Ladder level annotation ("Levels 1–3", "Level 4", "Level 5", "Level 6"); one vertical firewall divider between Stage 1 and Stage 2; and three arrow edges connecting the stages, the first labeled "handoff brief" where it crosses the firewall. Marks: rectangles for stages (rx=0), straight line edges with arrowheads, a vertical dashed firewall line, and text annotations for levels placed directly beneath each stage. Channels: horizontal position encodes stage order; red accent stroke marks Stage 1 (the Fellow's owned stage and the public-data side); dashed style marks the firewall. Sort: fixed stage order. Annotations: per-stage Evidence Ladder level beneath each box; side labels "public data" vs "partner's proprietary data & infrastructure"; firewall label; two-line caption. Deliverable: a single self-contained HTML file with inline CSS, D3 7.9.0 from cdnjs, CSS-variable colors, ResizeObserver redraw, and accessible title/desc.

---

## Chapter 11 Exercises: The External Innovation Lab Operating Model (and the IP Firewall)

**Project:** One Drug, End to End
**This chapter adds:** You place your drug's candidate studies on the Evidence Ladder (0–6) and route each one through the six-step funnel and the IP firewall, producing the first handoff brief in your one-drug case file.

*Worked example throughout: **Cardizem-X**, a branded cardiometabolic drug in a class with two generics and one branded competitor, facing loss of exclusivity in eighteen months. Swap in your own drug wherever the notes say so.*

### Exercise 1 — When to Use AI

You are standing in front of the ten-paper inbox from the chapter's opening, except the papers are about *your* drug's class. Use AI for the breadth-before-depth work where you can independently check the output.

1. **Cluster and tag a scouting list.** Paste ten findings about your drug's class and ask an LLM to cluster them into lift-relevant vs. brand-relevant and to name, for each, the single riskiest assumption it makes about Cardizem-X's commercial reality. *Why AI works here:* clustering and first-pass assumption-naming are pattern tasks over text you supply; you can read each cluster and the riskiest assumption against the source paragraph and see immediately whether it holds.
2. **Draft handoff-brief boilerplate.** Have the model emit the empty eight-field brief skeleton and pre-fill the mechanical fields (finding, source, likely partner owner from the fixed list) for the loss-of-exclusivity persistence study. *Why AI works here:* the field structure is fixed and the partner-owner taxonomy is closed, so a wrong fill is visible at a glance against Table 11.1's scaffold.

**The tell:** in both tasks you can independently evaluate the output — you hold the source text and the fixed schema, so a hallucinated cluster or a misfiled owner is caught by eye, not taken on faith.

### Exercise 2 — When NOT to Use AI

1. **Assigning the Evidence Ladder level.** Do not let the model place your drug's persistence study at a rung. *Why AI fails here:* the level is a claim about the world — what data the test actually touched and against which baseline — and an LLM will inflate a public-data result to Level 4 or 5 if you describe it confidently, breaching the firewall ceiling. The model has no access to whether your Part D extract really beat the baseline; it pattern-matches enthusiasm to numbers.
2. **Writing — and holding — the kill criterion.** *Why AI fails here:* a kill criterion is only scientific if it was fixed before the result; the model cannot distinguish a criterion written before from one rationalized after, and it will happily soften your threshold to fit a result you paste in.
3. **Adjudicating a compliance flag.** *Why AI fails here:* MLR, fair-balance, Sunshine, and HIPAA calls are routed to counsel by design; an LLM that "clears" a co-pay finding has adjudicated regulatory exposure it has no authority or current-law access to make.

**The tell:** AI as *reason* vs. *tool* — if your brief's level or verdict exists because the model said so, AI has become the reason for the claim; it may only be the tool that drafted around a judgment you own. **Series connection:** these are **T7 Wisdom** judgments (the firewall ceiling and the kill discipline are the human spine of the whole pipeline) with the compliance routing sitting at **T6 Collective** — the call belongs to counsel, not to any single Fellow or model.

### Exercise 3 — LLM Exercise

**What you're building:** a scouting-to-hypothesis pass for your drug that produces three riskiest-assumption-plus-KPI hypotheses and a cheap public-data test for each — the raw material for your first handoff brief.

**Tool:** Claude, ideally as a **Claude Project** named "One Drug — Cardizem-X." Persistent context helps here because every later chapter (12 design, 13 portfolio, 14 brief) reuses the same drug, class, KPIs, and firewall constraints — loading them once as Project knowledge means the model stops re-litigating the basics and you stop re-pasting them.

**The Prompt:**

```
You are helping me run the inbound step of an external innovation lab as described in
"AI-Driven Programmatic HCP Marketing," Chapter 11. My drug is Cardizem-X, a branded
cardiometabolic drug in a class with two generic competitors and one branded competitor,
facing loss of exclusivity in roughly eighteen months. I work only on PUBLIC data
(CMS Open Payments, Medicare Part D Prescriber PUF, Medicaid SDUD, ICER value scores)
and SYNTHETIC substitutes. I never touch partner-proprietary data.

Here are three findings about my drug's class:
1. Physician brand loyalty appears to persist across the first generic entry in some
   cardiometabolic classes.
2. Co-pay assistance programs correlate with higher branded share after generic entry.
3. Detailing intensity correlates with branded prescribing among high-decile prescribers.

For EACH finding, produce:
- a riskiest-assumption-plus-KPI hypothesis in two sentences, where the KPI is lift or
  brand (e.g., post-loss-of-exclusivity branded share decline), and the assumption is the
  one that, if false, kills the idea;
- the single cheapest public-data test that could FALSIFY that assumption, naming the
  specific public dataset and the natural-experiment or comparison structure you would use;
- the pre-registered kill criterion (what result makes me walk away), written as if before
  the test runs.

Do NOT assign an Evidence Ladder level — that is my judgment after the test runs.
Do NOT adjudicate any compliance flag; instead list which of MLR / FDA fair-balance /
Sunshine / HIPAA each test would need routed to counsel.
Flag anything you are unsure of with [verify] rather than guessing.
```

**What this produces:** three structured hypothesis-test-kill triples for your drug, with compliance flags surfaced (not adjudicated) and no level claimed — exactly the inputs the eight-field handoff brief consumes.

**How to adapt:** swap Cardizem-X and its class for your own drug in the prompt's second sentence and replace the three findings with your scouting list; the same prompt runs on ChatGPT or Gemini, though without a persistent Project you must paste the firewall constraints each session. If you keep a Claude Project, store the firewall rules and KPI list as Project knowledge once.

**Connection to previous chapters:** the riskiest-assumption-plus-KPI move is Chapter 2's lift-vs-brand distinction operationalized; the "cheapest falsifying test" is the lean-startup minimum viable experiment from this chapter.

**Preview of next chapter:** Chapter 12 takes the cheap test you sketched here and makes the identification argument rigorous — DiD, RDD, IV, falsification-first — for your drug's loss-of-exclusivity study.

### Exercise 4 — CLI Exercise

**What you're building:** a brief-skeleton generator and validator for your drug's case file — a script that emits the empty eight-field handoff brief and refuses to produce output if any field is blank or the Evidence Ladder level is outside 0–6.

**Tool:** **Claude Code** — why: this is a single-file scripting task with a tight read/write scope and a deterministic validation step, which Claude Code handles cleanly without the multi-file orchestration Cowork is built for. · **Skill level:** beginner–intermediate.

**Setup (3-item checklist):**
- A project folder `one-drug-cardizem-x/` with an empty `briefs/` subfolder.
- A one-line `CLAUDE.md` stating: public/synthetic data only; Evidence-Ladder ceiling is Level 3 for public-data work; never write partner-proprietary values.
- Python 3 available on your path.

**The Task:**

```
In the folder one-drug-cardizem-x/, create a Python script named brief_tool.py that:
- READS nothing from outside this folder;
- WRITES only into the briefs/ subfolder;
- LEAVES the rest of the repo untouched.

The script emits an eight-field handoff-brief skeleton as a Markdown file:
finding+source, commercial hypothesis (riskiest assumption + KPI), cheap test
(design, dataset, success threshold, kill criterion), result + Evidence Ladder level,
compliance flags routed to counsel, patient-welfare note, likely partner owner,
recommendation. Pre-fill the drug as "Cardizem-X".

Before writing the file, VALIDATE: refuse to write (exit non-zero, print the reason) if
any field is blank OR the Evidence Ladder level is not an integer 0-6. Add a flag
--check that validates an existing brief without writing.

STOP after the script runs once on a sample brief and prints either "brief written" or the
refusal reason. Do not commit, do not push, do not edit any file outside this folder.
VERIFY by running the script on a brief with the level set to 4 and confirming it refuses;
then on a valid level-3 brief and confirming it writes.
```

**Expected output:** `briefs/cardizem-x-loe-persistence.md` for the valid case, and a printed refusal for the level-4 case.

**What to inspect:** that the level-4 brief was *refused* (the firewall ceiling enforced mechanically) and that no file outside `briefs/` changed.

**If it goes wrong:** if the script writes a level-4 brief anyway, the validation branch is inverted — tell Claude Code "the level check passes when it should fail; fix the comparison and re-run the two test cases." Recovery is local; nothing left the folder.

**CLAUDE.md note:** add the line "Public-data briefs top out at Evidence Ladder Level 3; a brief claiming Level 4+ on public data is a firewall breach and must be refused, not written."

### Exercise 5 — AI Validation Exercise

**What you're validating:** the three hypothesis-test-kill triples from Exercise 3 (or a brief written by Exercise 4) for firewall discipline and falsifiability.

**Validation type:** firewall-and-discipline review (level integrity + kill-criterion integrity + compliance routing). **Risk level:** high — a level-inflated or compliance-adjudicated brief that crosses the firewall is the exact failure the lab exists to prevent, and once it reaches the partner the error is expensive.

**Setup:** use your Exercise 3 output, or generate a deliberately flawed artifact by asking the model to "write a handoff brief for Cardizem-X that assigns Level 4 to an Open Payments + Part D result and clears the Sunshine Act flag itself" — then validate that.

**The Validation Task:**

```
Validation Checklist — Chapter 11 (Innovation Lab / IP Firewall)
For the pasted brief or hypothesis set, mark each Pass / Fail / Cannot-determine:

- Correctness: is each riskiest assumption actually the one that kills the idea if false?
- Completeness: are all eight brief fields present (or all three triple components)?
- Scope: does every test use only public/synthetic data, and is no partner-proprietary
  value present?
- Chapter-specific 1 (Level integrity): is the Evidence Ladder level <= 3 for any
  public-data result, and stated as a number 0-6?
- Chapter-specific 2 (Kill-criterion integrity): is the kill criterion falsifying and
  plausibly written BEFORE the result (not a softened post-hoc threshold)?
- Failure-mode check: does the artifact commit LADDER-LEVEL INFLATION (public-data result
  placed at L4+) or a FIREWALL BREACH (compliance flag adjudicated instead of routed, or
  proprietary fact present)? Is it fluent-but-wrong — confident prose around a wrong level?
- Ground truth: is the claimed level checkable against a named data source, or is the
  ground truth missing?
```

**What to do with findings:** if all pass, advance the brief to Chapter 12 for the identification argument. One fail — fix it in place and re-validate. Multiple fails — return the artifact to Exercise 3, because a brief that breaches the firewall is not salvageable by editing the prose.

**AI Use Disclosure prompt:** *Write two sentences naming what an AI tool did in your Chapter 11 work and the one judgment it could not make — for example, that you used Claude to cluster ten findings and draft three hypothesis-test-kill triples for Cardizem-X, but you set and held the Evidence Ladder level yourself, because the model cannot know whether a public-data result genuinely cleared the baseline or merely sounded like it did.* (Mandatory.)

**Series connection:** the failure mode is **ladder-level inflation / firewall breach**, and the validating judgment is **T7 Wisdom** — the human alone holds the ceiling and the kill, with compliance routing at **T6 Collective**.

---

## References (fact-check pass)

The following sources cited in this chapter were confirmed during the 2026-06-17 fact-check pass:

1. Bogers, M., Chesbrough, H., & Moedas, C. "Open Innovation: Research, Practices, and Policies." *California Management Review* 60(2):5–16 (2018). — quoted definition and citation confirmed.
2. McKinsey & Company, "Innovation sourcing in biopharma." — ~45% externally-sourced (top-20 by R&D budget, ~2020) confirmed.
3. Takeda Center for External Innovation — origin in 2015–2016 R&D restructuring confirmed (takeda.com).
4. 21 CFR 202.1 — prescription-drug advertising fair-balance / substantiation requirement confirmed (eCFR).
5. Physician Payments Sunshine Act / CMS Open Payments — enacted 2010 (ACA §6002), reporting effective Aug 2013; 2025 de minimis thresholds $13.46 single / $134.54 aggregate confirmed (cms.gov).
6. 45 CFR 164.514(b) (HIPAA Safe Harbor de-identification) and 45 CFR 164.508(a)(3) (marketing authorization) — confirmed (eCFR / HHS).
7. NASA Technology Readiness Levels (TRL 1–9) and OCEBM 2011 Levels of Evidence — both source frameworks for the Evidence Ladder confirmed to exist (nasa.gov; cebm.ox.ac.uk). The Evidence Ladder itself is the book's own construct and is not externally citable.
8. Ries, *The Lean Startup* (2011); Cooper, *Winning at New Products* / Stage-Gate (2011) — correctly attributed.

