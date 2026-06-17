# Chapter 11 — The External Innovation Lab Operating Model (and the IP Firewall)

> This is the operating system of Act Three. Everything you built in the
> toolkit — lift, brand, ensembles, uplift, LLM harnesses — becomes a
> *process* here: scout an idea, turn it into a falsifiable hypothesis,
> run a cheap public-data test, score the evidence, flag the compliance
> risk, and hand it off (or kill it). The chapter introduces two of the
> book's load-bearing constructs: the **Evidence Ladder (0–6)** and the
> **public-data / IP firewall**.

## 11.1 Chapter overview

By the end of this chapter you will be able to run the lab's end-to-end workflow and place any artifact on the Evidence Ladder — knowing what each level unlocks and where, on public data, you must stop. The central idea is that the lab's product is *reduced uncertainty*, not a shipped platform. The Fellow tests cheaply, on public data, which research ideas earn the partner's proprietary data and engineering investment. The boundary between what a Fellow can prove and what only the partner can prove is not a limitation to apologize for — it *is* the firewall that protects both the partner's IP and the Fellow's research independence, made operational.

## 11.2 Learning objectives

By the end of this chapter you will be able to:

1. **(Understand)** Describe the lab's role — reduce the partner's uncertainty, not own production — and the four-stage productization pipeline (open research → proprietary replication → prototype → resourced).
2. **(Apply)** Convert a research finding into a falsifiable commercial hypothesis and a low-cost test.
3. **(Evaluate)** Apply the IP firewall: public data and method in the book and repo; partner-confidential material stays in `private/`; nothing proprietary is published.
4. **(Create)** Draft the skeleton of a product-handoff brief for medical, legal, regulatory, data-science, and commercial stakeholders, naming its Evidence Ladder level.

## 11.3 Opening case: ten interesting papers — which one becomes a test?

A Fellow's first week ends with a reading list of ten genuinely interesting papers. One proposes a routing architecture for tabular data. One reports that physician brand loyalty survives three generic entries. One finds that disclosure laws change *what physicians report* but not *what they prescribe*. One claims a transformer beats gradient boosting on a healthcare benchmark. And so on — ten papers, each plausibly relevant to lift or brand.

Here is the trap the chapter exists to defuse: *interesting is not the same as testable, and testable is not the same as worth testing.* A paper at the frontier of method is worth Level 0 attention — a watch item — until someone can state the riskiest assumption it makes about the partner's commercial reality, tie that assumption to a key performance indicator (KPI), and design the cheapest test that could kill it. The Fellow who tries to "evaluate all ten" produces ten shallow summaries. The Fellow who runs the lab picks the one or two where a small public-data test could move the idea up a rung — and writes a one-page memo that *earns or refuses* engineering resources.

That memo is the artifact. Its job is a defensible go/kill, and the rest of this chapter is how you produce it.

## 11.4 Prerequisites

You should carry the full toolkit: the lift/brand split (Chapter 2), the evidence frame and association-vs-causation (Chapter 5), the ensemble baseline (Chapter 6), incrementality and holdouts (Chapter 8), and the LLM validation harness (Chapter 10). This chapter assembles them into a workflow; Chapter 12 supplies the identification strategies the higher ladder rungs require.

## 11.5 Core sections

### 11.5.1 The lab is a filter, not a factory

The lab's role, stated in the book's logline, is to *reduce the partner's uncertainty, not to own production.* This is a real operating choice, and it has a name in the management literature: **open innovation** — "a distributed innovation process based on purposively managed knowledge flows across organizational boundaries" (Bogers, Chesbrough & Moedas, *California Management Review*, 2018). The lab is specifically an *inbound* (outside-in) engine: it pulls external, **public** research into the relationship and routes the credible hypotheses outward to a commercial owner who can resource them. External sourcing is not exotic in pharma — industry summaries report that roughly 45% of large-biopharma pipelines were externally sourced around 2020 (via M&A, licensing, university partnerships; *industry-reported* [verify]), and named structures like Takeda's Center for External Innovation exist to manage exactly this flow.

The discipline this imposes: the Fellow's deliverable is a credible *test/build/kill*, not a shipped feature. Confusing the two — trying to build the platform — is how a lab loses its independence and its value.

### 11.5.2 The workflow: scout → hypothesis → cheap test → evidence → go/kill → handoff

The lab runs an innovation funnel:

1. **Scout** — surface signals from research, vendor claims, and the field.
2. **Hypothesis** — name the *riskiest assumption* the idea makes about the partner's commercial reality and tie it to a KPI (lift or brand).
3. **Cheap test** — design the lowest-cost experiment that could falsify that assumption. This is the lean-startup move: an experiment that produces *validated learning* — reducing uncertainty by testing the assumption against real signal (Ries, *The Lean Startup*; "an MVP is that version of a new product which allows a team to collect the maximum amount of validated learning with the least effort").
4. **Evidence** — run it on public data and score what you got (Section 11.5.3).
5. **Go/kill** — confront the result against predefined criteria. This is the **Stage-Gate** logic (Cooper): stages separated by *gates* where a cross-functional team decides go or kill against criteria set in advance, so weak concepts are filtered early and only the strongest graduate.
6. **Handoff** — write the memo that places the artifact on the Evidence Ladder and recommends the next investment stage.

The whole funnel exists to make a *cheap* mistake instead of an expensive one — to kill a bad idea at Level 1 instead of after the partner has spent six engineering months on it.

### 11.5.3 The Evidence Ladder (0–6) — the lab's shared vocabulary

The Evidence Ladder is **the book's own construct.** It is not a citation to a named external scale; it is a synthesis of two well-established axes — a *maturity* axis adapted from NASA's Technology Readiness Levels (TRL 1–9, basic principles through flight-proven) and an *evidential-strength* axis adapted from the Oxford Centre for Evidence-Based Medicine Levels of Evidence (OCEBM 2011, systematic reviews of RCTs down to mechanism-based reasoning). We combine them into a single 0–6 ladder because the lab needs to talk about *both* "how mature is this idea?" and "how strong is the evidence for it?" in one breath.

| Level | Evidence | What it unlocks |
|---|---|---|
| 0 | Interesting paper or vendor claim | Watch only |
| 1 | Plausible hypothesis mapped to a KPI | Fellow brief |
| 2 | Reproducible benchmark or simulation (public data) | Internal discussion |
| 3 | Small offline test that beats the baseline | Product discovery |
| 4 | Prospective pilot or holdout study | Product resourcing |
| 5 | Client-validated incremental impact | Roadmap candidate |
| 6 | Monitored deployment with compliance + patient-welfare checks | Product feature |

Two rules make the ladder operational. First, **every handoff brief must name its artifact's level** — vague enthusiasm is not a level. Second — and this is the firewall in disguise — **a Fellow working on public data tops out around Level 3.** A small offline test that beats the baseline is the most a public dataset can buy you (the ten papers in §11.3 mostly aspire to Level 2–3). Levels 4–6 — a prospective pilot, a client-validated incremental result, a monitored deployment — require the partner's *proprietary* data and infrastructure. That boundary is not a failure of ambition. It is the firewall, made concrete: the rung where the work crosses from the Fellow's side of the wall to the partner's.

### 11.5.4 The four-stage productization pipeline

The ladder describes evidence; the pipeline describes ownership. The four stages — **open research → proprietary replication → prototype → resourced** — map cleanly onto a university technology-transfer pipeline (disclosure/evaluation → IP protection/business planning → review/decision → commercialization), with TRL supplying the graduation criteria and Stage-Gate supplying the gates.

- **Stage 1 — Open research (the Fellow's stage).** Scan, hypothesize, test on public data, score. Tops out at Ladder Level 3.
- **Stage 2 — Proprietary replication (the partner's stage).** The partner re-runs the promising public-data method on its *own* data, internally. This is where Levels 4–6 become reachable, and it is the first stage on the partner's side of the firewall.
- **Stage 3 — Prototype.** A working prototype inside the partner's environment.
- **Stage 4 — Resourced.** A funded product effort with an owner.

The Fellow owns Stage 1 and writes the handoff that recommends whether Stage 2 should happen. The Fellow does *not* do Stage 2 — that is the operational meaning of "test on public data, hand off for proprietary replication."

### 11.5.5 The public-data / IP firewall

The firewall is the defining constraint of the whole partner collaboration, present from this chapter and enforced throughout:

> **Public data and public methodology only in the book and its repo.** Fellows test on public datasets (CMS Open Payments, Medicare Part D, ICER, syndicated or synthetic substitutes). The *partner* replicates promising methods on its proprietary data *internally* (Stage 2). Nothing confidential — partner internal metrics, named-vendor figures, any patent or product IP — enters the public book or repo; sensitive working material lives in `private/` (gitignored).

The firewall protects two things at once: the partner's IP *and* the Fellow's research independence. A Fellow who never touches proprietary data can publish honest findings — including critical ones — without leaking anything confidential, and the partner can replicate internally without exposing its data. The Level-3 ceiling for public-data work *is* the firewall; the `private/` directory is its file-system enforcement.

### 11.5.6 Compliance as routing, not adjudication

Every artifact the lab produces is screened for compliance risk across four surfaces, and every flag is **routed to medical/legal/regulatory counsel** — the lab *models the flag, it does not play lawyer*:

- **MLR (Medical–Legal–Regulatory) review** — the mandatory cross-functional review of promotional and medical content: Medical (clinical accuracy, substantiation), Legal (liability, IP), Regulatory (FDA/OPDP, labeling). Triggered by essentially any externally facing promotional asset. (Vendors report ~50–60-day cycle times and "50–65% AI reduction"; both are *vendor-reported*, directional only — there is no neutral benchmark.)
- **FDA fair balance / OPDP** — under 21 CFR 202.1, product-claim promotion must present a fair balance of risk and benefit and substantiate claims. The 2025 enforcement escalation (Chapter 10, §10.5.6) raises the stakes on any generated or AI-assisted content.
- **Sunshine Act / Open Payments** — manufacturers must annually report transfers of value to covered recipients above the de minimis thresholds (cite the *current-year* inflation-adjusted CMS figures, not round baselines `[verify]`); CMS publishes the public Open Payments database annually.
- **HIPAA / privacy** — de-identification Safe Harbor (45 CFR 164.514(b)) and the marketing-authorization rules (45 CFR 164.508(a)(3)) govern any use of patient-derived data.

The routing posture matters for tone, too. A lab embedded with a named partner will sometimes produce pointed findings (the coupon and proxy-discrimination work of later chapters). The frame is **collaborative de-risking** — the lab surfaces risk *before* it becomes an enforcement letter — and the partner signs off on pointed framing. The lab is pro-evidence, not anti-partner.

### 11.5.7 The handoff-brief skeleton

The chapter's named artifact is the lab protocol — the Evidence-Ladder placement plus the handoff-brief skeleton. A minimal brief contains:

1. **The finding** (one sentence) and its source.
2. **The commercial hypothesis** — riskiest assumption, tied to a KPI (lift or brand).
3. **The cheap test** — design, public dataset, success threshold, and *kill criterion* (a "no" is a result).
4. **Result and Evidence Ladder level** — what you got, and the rung it reached.
5. **Compliance flags** — MLR / fair-balance / Sunshine / HIPAA surfaces, routed to counsel.
6. **Patient-welfare note** — who benefits and who might be harmed.
7. **Likely partner owner** — measurement analytics, brand strategy, data science, content ops, or compliance.
8. **Recommendation** — test next / replicate on proprietary data (Stage 2) / shelve / kill, and why.

## 11.6 Worked example: turning one of the ten papers into a test

**Process.** The Fellow picks the "brand loyalty survives generic entry" paper from §11.3.

1. *Scout → finding.* "Physician brand loyalty appears to persist across generic entries in some classes."
2. *Hypothesis.* Riskiest assumption for the partner: that this persistence is *brand equity*, not just inertia or clinical value. KPI: post-loss-of-exclusivity branded share decline. Tie: if equity drives persistence, high-equity brands should erode slower *after controlling for clinical value*.
3. *Cheap test.* Use loss of exclusivity as a natural experiment (Chapter 12) on Medicare Part D prescriber data, with ICER value scores as the clinical-value covariate. Success threshold: a meaningful, robust persistence effect net of value. Kill criterion: no effect once value is controlled, or no usable signal in public data.
4. *Evidence.* The test, run on public data, is a *small offline test* — Ladder **Level 3** at most. It cannot establish client-validated impact (Level 5); that needs the partner's proprietary panel.
5. *Go/kill.* Suppose the public-data test finds a modest, value-adjusted persistence signal. Recommendation: *replicate on proprietary data (Stage 2)* — the firewall hands it to the partner.

**Lesson.** One paper became a falsifiable hypothesis, a cheap public-data test, and a Ladder-placed recommendation — while the other nine stayed at Level 0 (watch). The lab's value was the *selection*, not the volume.

**Limit.** Part D does not directly observe new-to-brand prescriptions and skews to an older population (Chapter 12); the public-data result is suggestive, not definitive — which is exactly why the recommendation is "replicate," not "build."

## 11.7 Common misconceptions

- **"More interesting papers = more lab output."** Output is selected, tested hypotheses, not summaries. Nine of ten papers correctly stay at Level 0.
- **"The Evidence Ladder is a standard industry scale."** It is the *book's construct*, synthesized from TRL (maturity) and OCEBM (evidential strength). Say so when you use it.
- **"A Fellow on public data can reach Level 5."** No — public data tops out around Level 3. Levels 4–6 require the partner's proprietary replication. That ceiling is the firewall.
- **"Compliance flags mean the Fellow decides the legal question."** The Fellow *flags and routes*; counsel adjudicates. Modeling the flag is the skill; playing lawyer is the error.
- **"The firewall is just a rule about file storage."** It is a research-design and ownership boundary; `private/` is merely its enforcement.

## 11.8 Evidence check

- **Established frameworks (adapted, not novel):** TRL (NASA), OCEBM Levels of Evidence (CEBM 2011), Stage-Gate (Cooper), open innovation (Chesbrough), lean startup (Ries), tech-transfer pipelines. The **Evidence Ladder 0–6 is the book's own synthesis** of TRL and OCEBM.
- **Industry-reported (directional):** ~45% externally sourced biopharma pipeline (2020); Stage-Gate adoption rates; MLR cycle times and AI-reduction figures (all vendor/consultancy-reported, no neutral benchmark).
- **Verified compliance mechanisms:** MLR structure, 21 CFR 202.1 fair balance, Sunshine Act/Open Payments reporting, HIPAA Safe Harbor — mechanisms solid against primary HHS/FDA/CMS sources; the FDA 2025 enforcement *counts* are approximate (Chapter 10).
- **`[verify]`:** current-year Open Payments de minimis thresholds; TRL 8/9 verbatim wording.

## 11.9 Compliance and patient-welfare check

Compliance is the spine of this chapter, not an appendix: every artifact is screened across MLR, fair balance, Sunshine, and HIPAA, and every flag is **routed to counsel.** The patient-welfare note is a required field in the handoff brief — the lab asks *who benefits and who might be harmed* before recommending any idea for resources, so that welfare-relevant findings (coupon effects on generic substitution, susceptibility proxies) surface as gates rather than afterthoughts. The collaborative-de-risking frame keeps the lab pro-evidence and pro-patient without being anti-partner.

## 11.10 Exercises

1. **(Understand)** State the lab's role in one sentence, and explain why owning production would undermine it.
2. **(Apply)** Take one finding from your own thread. Write its riskiest assumption, the KPI it touches, and the cheapest test that could falsify it.
3. **(Apply+ / Evaluate)** For that test, name the highest Evidence Ladder level it can reach on public data, and say what would be required to go one rung higher — and on whose side of the firewall that work lives.
4. **(Create / Part B — produce)** Draft a one-page handoff brief skeleton for your thread, with all eight fields filled, including the Evidence Ladder level, at least one routed compliance flag, and the patient-welfare note.

## 11.11 Five-part AI exercise block

1. **When to use AI:** scouting and clustering candidate findings, drafting first-pass hypotheses, generating handoff-brief boilerplate, surfacing compliance-flag candidates for human routing.
2. **When NOT to use AI:** deciding the go/kill, setting the kill criterion, adjudicating a compliance flag, or asserting an Evidence Ladder level — these are human judgments the brief must own.
3. **LLM exercise:** give a model three findings from your reading and ask it to draft, for each, a riskiest-assumption-plus-KPI hypothesis. Keep the best; rewrite the rest.
4. **CLI / code exercise:** build a template script that emits an empty eight-field handoff-brief skeleton and validates that no field is blank and that the Evidence Ladder level is one of 0–6 before "submission."
5. **AI-validation exercise:** ask the model to assign an Evidence Ladder level to one of your artifacts. Then check it against the firewall rule — if the model put a public-data result at Level 4+, you have caught it violating the ceiling, which is the load-bearing human correction.

## 11.12 AI Use Disclosure (Part B)

Name one judgment in building your handoff brief that the AI could not make: the kill criterion, the true Evidence Ladder level given the firewall, whether a compliance flag is real, or whether the partner could defend the recommendation. Naming it earns the Part B bonus.

## 11.13 What would change my mind

If a public dataset emerged that credibly supported a prospective, client-validated incremental result without touching proprietary data, the Level-3 public-data ceiling would move up. Today no such dataset exists for HCP commercial outcomes — Levels 4–6 inherently require the partner's data — so the firewall ceiling holds.

## 11.14 Still puzzling

The firewall keeps the Fellow independent and the partner's IP safe, but it also caps how far the Fellow can prove an idea before handing it over — which means the most consequential validation always happens *out of the Fellow's sight*, on the partner's side. How does the lab maintain evidentiary discipline across that boundary, when it cannot see the Stage-2 replication? The book's answer is the handoff brief's explicit criteria and the partner's reciprocal reporting — but the asymmetry is real and unresolved.

## 11.15 Summary

You can now run the lab as a filter: scout, hypothesize, test cheaply on public data, score, gate, and hand off. You can place any artifact on the Evidence Ladder (0–6) — the book's own synthesis of TRL and OCEBM — and you know that public data tops out around Level 3, with Levels 4–6 living on the partner's side of the firewall through proprietary replication (Stage 2 of the four-stage pipeline). You can model compliance as routing, not adjudication, and draft a handoff brief that earns or refuses resources.

## 11.16 Key terms

- **Open innovation** — managed knowledge flows across organizational boundaries; the lab is the inbound engine.
- **Validated learning** — reducing uncertainty by testing an assumption against real signal (lean startup).
- **Stage-Gate** — stages separated by go/kill gates judged against predefined criteria.
- **Evidence Ladder (0–6)** — the book's construct synthesizing TRL (maturity) and OCEBM (evidential strength); names what each evidence level unlocks.
- **Four-stage productization pipeline** — open research → proprietary replication → prototype → resourced; Fellow owns Stage 1.
- **Public-data / IP firewall** — public data and method in the book/repo; partner-confidential material in `private/`; nothing proprietary published.
- **Compliance routing** — flagging MLR / fair-balance / Sunshine / HIPAA risk and routing it to counsel rather than adjudicating it.
- **Handoff brief** — the one-page memo that places an artifact on the ladder and recommends test/build/replicate/kill.

## 11.17 Bridge

The lab's higher rungs — Level 3's "beats the baseline" and Level 4's "prospective study" — only count if the test is *credibly identified*. To run those tests on public data, you need the causal-inference toolkit: natural experiments, difference-in-differences, regression discontinuity, instrumental variables, and a map of which public dataset answers which question. That is Chapter 12.

## 11.18 Further reading

- Bogers, M., Chesbrough, H., & Moedas, C. (2018). *Open Innovation: Research, Practices, and Policies.* California Management Review. The inbound/outbound framing the lab adapts.
- Cooper, R. G. *Stage-Gate Idea-to-Launch Process.* Wiley Encyclopedia of Management (2010). The go/kill gate logic.
- Ries, E. *The Lean Startup.* MVP and validated learning — the cheap-test vocabulary.
- NASA, *Technology Readiness Levels.* The maturity axis the Evidence Ladder adapts (`[verify]` TRL 8/9 wording).
- CEBM, *OCEBM Levels of Evidence (2011).* The evidential-strength axis the Evidence Ladder adapts.
- IPWatchdog, *Clean-Room Development to Prevent the Spread of "Infectious IP."* The firewall failure mode: procedures don't guarantee immunity if tainted material reaches the output.
