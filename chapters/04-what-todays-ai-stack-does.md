# Chapter 4 — What Today's AI Stack Actually Does (and Claims)

> **[MIDTERM: VENDOR-CLAIM AUDIT]**

## 1. Overview

By the end of this chapter you will be able to take any pharma marketing-technology platform's capability deck and do something most buyers cannot: separate the part that is a genuinely deployed, working capability from the part that is marketing language wrapped around an unproven effectiveness claim. You will learn the current production inventory of commercial AI in HCP marketing — trigger-based point-of-care targeting, predictive audience modeling, Medical-Legal-Regulatory (MLR) acceleration, Next-Best-Action (NBA) recommendation, field-force LLM support, and omnichannel orchestration — and you will learn to place each capability on a three-rung maturity ladder: *deployed*, *emerging*, or *aspirational*. Most importantly, you will learn the audit move that the rest of the book depends on: for any claim, ask **what KPI does it move, what data feeds it, and what evidence supports it** — and notice when the platform that serves the ad is also the platform that measures the lift. The chapter's running thesis is blunt: in this market, most *capabilities* are real, and most *effectiveness claims* are not independently validated. Telling those two apart is the Fellow's first professional skill, and it is your midterm.

## 2. Learning Objectives

1. **(Understand)** Describe each production AI use case in pharma HCP marketing and its target KPI; rate each one *deployed*, *emerging*, or *aspirational*.
2. **(Evaluate)** Audit a vendor capability claim against the three-question rubric — *what KPI, what data, what evidence* — and detect attribution circularity and relabeled architecture buzzwords.
3. **(Analyze · Part B)** Apply the audit to a capability claim relevant to your own research thread, and render a defensible verdict.

## 3. Opening Case — "The World's First AI Operating System"

A platform deck lands in your inbox. The headline reads: *"The world's first AI-powered operating system for healthcare marketing, powered by an adaptive Mixture of Experts."* Underneath are six capability tiles — NPI audience intelligence, conversational AI, SMART-on-FHIR workflow integration, creative-experience optimization, MLR acceleration, and "federated learning across the network." A footer cites a Frost & Sullivan recognition and a "20:1 return on investment."

Your instinct is suspicion, which is correct, but suspicion is not an audit. The honest reading is more interesting than either credulity or reflexive dismissal, because the claim is *partly true*.

Take "operating system" first. Stripped of the swagger, this is a claim of **platform consolidation**: identity resolution, point-of-care ad inventory, programmatic buying, account-based marketing, co-pay programs, and analytics running on one unified data layer instead of six stitched-together vendors. That is a real, defensible architectural claim. Doceree, the platform whose language this echoes, genuinely consolidates these functions [verify — confirm current Doceree capability map against primary source]. "Operating system" is a marketing flourish over a true plumbing fact.

Now take "adaptive Mixture of Experts." A Mixture of Experts (MoE) is a real architecture — specialized sub-models plus a router that decides which to use — and we will dissect it in Chapter 7. But two things are true at once. First, the specific deployment is *not independently verified*; you have the vendor's word that an MoE is running and the vendor's word that it helps. Second, even if a genuine MoE is running, the task here is NPI-level tabular prediction, which is precisely the regime where, as Chapter 6 will show, a well-tuned gradient-boosted tree ensemble is the state of the art and an MoE is likely indistinguishable from — or worse than — that boring baseline (Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022). So the architecture word may name something real and still tell you nothing about whether the system is good.

And the "20:1 ROI"? That is a vendor-generated number measured by the vendor, with no control group and no independent audit — the kind of figure this book teaches you to label and never to repeat as fact. The Frost & Sullivan recognition is *paid* industry recognition, not independent validation.

**Verdict:** platform-consolidation claim plausible; MoE-superiority claim unproven; ROI claim un-evidenced. Every sentence on the deck can be literally accurate while the deck as a whole proves nothing about effectiveness. That coexistence — true sentences, no evidence — is the disease this chapter and the next diagnose.

## 4. Core Sections

### 4.1 The capability inventory and the deployed / emerging / aspirational ladder

The single most useful thing you can do with a platform deck is sort its capabilities onto a maturity ladder and attach a KPI to each. Here is the honest current state of the field, rung by rung.

**Deployed and mature.** *Trigger-based point-of-care (POC) targeting* — an ICD-10 diagnosis code fires inside the electronic health record (EHR) and a contextual ad is delivered at or near the prescribing moment. This is the industry's consensus "current gold standard" in POC messaging and reliably produces higher HCP engagement than non-contextual digital. The capability is unambiguously real and in production.

**Deployed at scale.** *Predictive audience modeling* (propensity modeling) — models trained on claims data plus behavioral signals identify high-potential HCPs *before* a prescribing event, so the brand can reach them early. OptimizeRx's DAAP, Doceree's "intelligence layer," and IQVIA's OCE+ are production examples [verify product names/positioning against current vendor docs]. The KPI is engagement or new-to-brand prescriptions (NBRx). The modeling is genuine; whether it *causes* incremental scripts is a separate question (Chapter 8).

**Deployed but task-scoped (maturing toward agentic).** *Next-Best-Action (NBA)* — an AI system recommends which HCP, which channel, which message, at which moment, and the field rep becomes the human delivery mechanism for the AI-orchestrated sequence. Veeva's AI Agents for Vault CRM (announced December 2025) and IQVIA's NBA agents built with NVIDIA are concrete, dated examples [verify]. The crucial nuance is that "agentic" in the 2025–26 wave mostly means *task-assistive* — drafting call reports, surfacing barriers from rep notes, speeding CRM work — not autonomous analytical decision-making. A very good intern, not an autonomous analyst.

**Emerging but contested.** *MLR acceleration / content generation* — AI pre-screens promotional content for incomplete claims or missing references, links copy to pre-approved claims libraries, routes low-risk modular content, and drafts reviewer summaries. Veeva's PromoMats Content Agent (late 2025) is an example [verify]. We will see in §4.3 why the operational maturity is real but the ROI is genuinely contested.

**In development / aspirational at scale.** *Federated learning for targeting models* — training on distributed patient data without centralizing it. Vendors reference it; whether it is running at production scale is unclear and should be treated as aspirational until shown otherwise.

The skill is not memorizing this list — the named products will age within a year (a risk this book flags explicitly). The skill is the *sorting move*: where does each named capability sit, deployed / emerging / aspirational, and what KPI does it claim to move? **The common misconception to kill on sight: "if a vendor names a capability, it is deployed and proven."** Most capabilities in this market are real. Most effectiveness claims are not independently validated. Those are different sentences.

### 4.2 Next-Best-Action — what it actually computes

NBA is the current frontier of pharma *commercial* AI, so it deserves a precise definition. An NBA system ingests claims data, behavioral engagement signals, and calendar/territory constraints, and outputs a ranked recommendation: *this HCP, this channel, this message, this week.* The rep executes it. The target KPI is engagement, call response, or NBRx.

Here is the misconception worth dwelling on, because it recurs across the whole book: **"NBA optimizes for the patients who most need the drug."** It does not. NBA optimizes for *reachable responders* — physicians whose engagement-likelihood is highest. That is an optimization over the marketer's objective (efficient engagement), not over clinical need. This is the same inversion you will meet formally in Chapter 8 (predicting a prescriber is not changing one) and the same susceptibility concern raised in Chapter 3. The system is good at its actual job; its actual job is just not the one the brochure implies.

The 2025–26 "agentic" wave is real but should be read carefully. Veeva's "Agentic Call Report" surfaces treatment barriers from a rep's notes; IQVIA's agents free reps from administrative work. These are genuine productivity tools. But the *effectiveness* claim — "better engagement leads to more scripts" — is exactly the claim that requires a holdout to test, and no independent study supplies one (Chapter 8).

### 4.3 MLR acceleration — the most operationally mature, most contested ROI

MLR review — the Medical, Legal, and Regulatory gate every piece of promotional content must pass — has historically run roughly 50–60 days per piece [verify]. AI is deployed to compress it: pre-screening for incomplete claims and missing references, linking content to approved claims libraries, routing low-risk modular content, and drafting reviewer summaries. The consensus implementation pattern is **Human-in-the-Loop (HITL)**: AI does the quantitative checks, humans keep the contextual and ethical judgment.

This is where you must hold two numbers in tension and resist resolving them prematurely. McKinsey has cited a **50–65% reduction** in regulatory-submission timelines at some companies [verify — methodology unclear]. At the same time, a widely circulated MIT finding holds that **95% of enterprise generative-AI pilots are failing** [verify — methodology unclear]. Both circulate without transparent methodology, and they point in opposite directions. The honest move is to present both, attribute both, and treat neither as settled.

A third datum reframes the whole thing. Promotional-material production in the US rose **29% year over year** while **77% of approved content is rarely or never used by field teams** [verify]. Volume is up; value is not obviously up. The real problem with MLR is *governance, not generation speed* — and faster generation can make the governance problem worse, not better.

So when a company reports "50% faster MLR," the audit questions write themselves: faster on which content tiers? measured how? did the rejected-content rate or the rate of post-launch FDA letters change? That last question is not hypothetical — see §4.5's enforcement case.

### 4.4 Omnichannel orchestration

Physician access changed permanently after COVID. By early 2024, only about **45% of US physicians** made themselves available to pharma reps, and roughly 30% limited themselves to a single brand [verify]. The channel mix shifted with it: in-person reps declining, remote/virtual detailing normalized, email high-volume but low-engagement, POC/EHR the fastest-growing and highest-conversion channel, endemic digital (e.g., Medscape) high-trust but moderate-scale, and programmatic open-web broad-reach but low-trust.

**Omnichannel orchestration** is the coordination of all those channels for *one* HCP so the brand experience is coherent rather than overwhelming. NBA routes engagement to each physician's preferred and most-responsive channel. The misconception is "omnichannel means being everywhere." It does not — it means *coordination*, not ubiquity. A physician hit in one week by a rep visit, two emails, retargeting banners, and an EHR trigger has a *fragmented* brand experience; orchestration exists precisely to prevent that. Worked concretely: a physician who ignores email but engages endemic content gets email suppressed and a Medscape placement plus a virtual detail prioritized.

### 4.5 Auditing a vendor claim — "what KPI, what data, what evidence?"

This is the chapter's named artifact and your midterm. For any capability claim, run five questions:

1. **What KPI** does it actually move — and is that KPI *lift* (incremental prescribing) or *brand* (durable quality association)? (The spine of this whole book, from Chapter 2.)
2. **What data** feeds it — and critically, is it the *same* NPI-linked infrastructure that also *measures* the result? If so, you have **attribution circularity**: the party with a commercial interest in a high number is also the party producing the number. There is no firewall.
3. **What evidence** — a vendor-generated case study, or independent peer-reviewed work?
4. **Deployed, emerging, or aspirational?**
5. **Does a buzzword** — MoE, federated learning, "operating system," "agentic" — name a real architecture, or is it a relabel of something simpler? (Defer the deep MoE verdict to Chapter 7; here, just flag it.)

The misconception to break: **"an impressive lift number from a named platform is evidence."** Every script-lift figure in this space — the 4% to 44% range you will meet in Chapter 5 — is **vendor-generated and methodologically circular**, because the platform serving the ad also measures the lift. The "20:1 ROI" figures are unverified. These are claims, not evidence, and the rubric exists to make you say so out loud.

A useful frame from the economics of AI (Agrawal, Gans & Goldfarb, *Prediction Machines*): AI makes *prediction* cheap; it does not supply *judgment* or guarantee a *business outcome*. "The model predicts X" and "the platform achieves outcome Y" are different claims, and the gap between them is where the audit lives.

## 5. Worked Example — Auditing the Six-Tile Deck

Let us audit the opening deck properly, including the dead ends, because the process matters more than the verdict.

**The deck:** "AI-powered NBA, MLR acceleration, federated learning, MoE routing, conversational AI, SMART-on-FHIR workflow — 20:1 ROI, Frost & Sullivan recognized."

**First pass (the dead end).** My initial instinct was to reject the whole deck as hype because of the "20:1 ROI" and the MoE buzzword. That was wrong, and it is worth seeing why: reflexive dismissal would have thrown away the *true* part of the claim (genuine platform consolidation; genuinely deployed trigger targeting) along with the unproven part. A blanket "it's all marketing" verdict is as useless to a product team as blanket credulity. The Fellow's value is precision, not cynicism.

**Second pass (the rubric, tile by tile):**

| Capability | Maturity | KPI | Data / circularity | Evidence | Verdict |
|---|---|---|---|---|---|
| Trigger / SMART-on-FHIR targeting | Deployed/mature | Engagement | Vendor-served, vendor-measured (circular) | Vendor case studies | Real capability; effect size unproven |
| Predictive audience (NBA) | Deployed at scale | Engagement / NBRx | Same NPI infra serves + measures | Vendor | Real; *incremental* effect untested (Ch 8) |
| MLR acceleration | Emerging/contested | Cycle time | Internal ops data | Conflicting (McKinsey vs. MIT) | Speed plausible; value-add contested |
| Federated learning | Aspirational at scale | — | — | None shown | Treat as aspirational |
| "Adaptive MoE routing" | Architecture claim | (implied accuracy) | — | None independent | Possibly real architecture; superiority unproven (Ch 7) |
| Conversational AI | Emerging | Engagement | — | Vendor | Real capability; effect unproven |

**The lesson.** A single deck contains capabilities at every rung of the ladder, and the honest verdict is heterogeneous: *test it / watch it / believe it / route it to Chapter 7*. The "20:1 ROI" and the Frost & Sullivan badge get labeled and set aside — one is an un-controlled vendor number, the other is paid recognition.

**The limit.** This audit tells you what is *plausible* and what is *unproven*. It cannot tell you what is *true* — that would require the control group and the independent measurement that Chapters 5, 6, and 8 build toward. The audit is the entry ticket to the evidence problem, not its resolution.

## 6. Common Misconceptions

- **"If a vendor names a capability, it is deployed and proven."** Most capabilities here are genuinely deployed. The effectiveness claims attached to them are mostly un-validated. Separate the two.
- **"NBA targets the patients who most need the drug."** NBA targets reachable responders — engagement-likelihood, not clinical need.
- **"Agentic AI" means autonomous analytical decision-making.** In the 2025–26 wave it mostly means task-assistive automation (call reports, CRM work). A good intern, not an autonomous analyst.
- **"An impressive lift number from a named platform is evidence."** It is a vendor-generated, structurally circular claim until an independent party with no commercial stake measures it.
- **"Omnichannel means being everywhere."** It means coordination for a single HCP, not ubiquity.
- **"A recognized architecture word (MoE, federated learning) means the system is better."** The word can name a real thing and still tell you nothing about performance on the task at hand.

## 7. Evidence Check & Compliance and Patient-Welfare Check

**Evidence check — what here is independent vs. vendor-generated vs. contested:**
- *Independent / settled:* the existence of these capabilities (trigger targeting, predictive audiences, NBA tooling) is well-documented; the post-COVID access shift is broadly reported. The *economics-of-AI* framing (prediction ≠ judgment) is from a peer-reviewed-adjacent book (Agrawal/Gans/Goldfarb).
- *Vendor-generated (label, never cite as evidence):* all script-lift figures (4–44%), the "20:1 ROI," Frost & Sullivan recognition (paid), and any platform performance claim.
- *Contested (present both, settle neither):* McKinsey's 50–65% MLR/submission-timeline reduction vs. MIT's "95% of GenAI pilots fail" — both circulate without transparent methodology. The 29%-YoY content-volume rise and 77%-unused-content figures are reported but `[verify]`.
- *Deferred:* whether any "MoE" platform runs genuine MoE — the book's position is "mostly false in practice," but the verdict belongs to Chapter 7's architectural criteria.

**Compliance and patient-welfare check:** MLR acceleration sits directly on the FDA fair-balance and promotional-claims fault line. The September 2025 FDA enforcement wave (§4.5's case) is a live reminder that AI-accelerated content generation, if ungoverned, scales the *risk* of exaggerated efficacy and inadequate fair balance as fast as it scales output — and the FDA is now using its own AI surveillance to catch it [verify the enforcement-wave specifics against primary FDA sources]. EHR-integrated advertising remains in a regulatory gray zone, which is a patient-welfare concern, not a compliance comfort: ads delivered in the same interface layer as drug-interaction warnings borrow the clinical authority of a safety alert. Any capability that "optimizes engagement" must be checked against the question of whether it optimizes *appropriate* prescribing — a gate no current vendor metric answers.

## 8. Exercises

1. **(Understand)** List the six capabilities in §4.1 and assign each a maturity rung and a KPI from memory, then check yourself against the chapter. Where you disagree with the chapter's rung, write one sentence defending your choice.
2. **(Apply+)** Take a real, public pharma-platform capability page (e.g., a vendor's "AI" product page). For each capability claimed, fill in the five-question rubric from §4.5 in a table, flag any attribution circularity, and flag any relabeled architecture buzzword. Render a one-line verdict per capability.
3. **(Apply+ · Produce · Part B)** Build your **vendor-claim audit artifact** for a capability claim relevant to your own research thread: the filled rubric table, the circularity flag, the maturity rung, and a defensible test/watch/route verdict — written so a product manager could act on it. This is the reusable form of the midterm.
4. **(Analyze)** Find a vendor "ROI" or "lift" number in public material. Write the three audit questions you would have to answer to convert it from a claim into evidence, and name the specific independent party who would have to measure it.

## 9. The Five-Part AI Block

**When to use AI here.** Use an LLM to *triage* a long platform deck or capability page — extracting every distinct claim, normalizing vendor jargon, and drafting a first-pass rubric table you then correct. AI is good at the high-recall extraction step.

**When NOT to use AI here.** Do not let an LLM render the *verdict*. Whether a number is circular, whether a buzzword is load-bearing, and whether a capability is genuinely deployed are judgment calls that require domain knowledge and an adversarial stance the model does not reliably hold. The model will fluently rationalize a vendor's framing if you let it.

**LLM exercise.** Paste a public vendor capability page and prompt: *"Extract every distinct capability claim and every effectiveness/ROI claim as separate rows. For each, label: claimed KPI, whether the claim is about a capability or an outcome, and whether any number cited is independently sourced or vendor-sourced. Do not assess whether the claims are true — only categorize them. Flag any architecture buzzwords (MoE, federated learning, agentic, operating system)."* Then you do the verdict pass by hand.

**CLI exercise.** Save three vendor pages as text. Use a command-line tool (e.g., `grep -i -E "lift|roi|x return|increase|%"`) to extract every quantified claim across all three files at once, then `wc -l` the result. The point: see how many quantified effectiveness claims a market makes, and how few carry an independent citation.

**AI validation.** For every claim the LLM categorized as "independently sourced," verify the source yourself — open it, confirm the number exists, and confirm the measuring party is not the selling party. Record how many "independent" labels survived. In this market, expect attrition.

## 10. AI Use Disclosure

Drafting this chapter, an LLM was used to help organize the capability inventory and draft the worked-example table structure; all maturity ratings, the attribution-circularity framing, and every verdict were set against the research notes and synthesis files and checked by hand. The judgment an AI could not make here: **which effectiveness claims are genuinely un-validated rather than merely un-cited**, and whether a named architecture is load-bearing or decorative — both require domain knowledge and an adversarial reading the model does not supply on its own. (Part B disclosure standard: name one judgment in your own audit that the AI could not have made.)

## 11. What Would Change My Mind

I would revise the chapter's "most effectiveness claims are un-validated" thesis if an *independent* party — academic, regulatory, or a third-party auditor with no commercial stake and no data dependency on the platform — published a pre-registered, controlled evaluation of an EHR/POC or NBA capability and found the vendor's effect size held up. One credible independent replication of a script-lift number would move the EHR-ad capability from "real capability, unproven effect" toward "real and evidenced." None exists today; the absence is the point, and it is falsifiable.

## 12. Still Puzzling

- If MLR acceleration genuinely cuts cycle time, why does 77% of approved content go unused — is the bottleneck never speed, always relevance? If so, what is the AI actually buying?
- The MIT "95% of pilots fail" and McKinsey "50–65% faster" figures cannot both describe the same reality cleanly. Which subset of work does each describe, and can anyone produce the methodology?
- "Agentic" tooling is task-assistive today. What is the first NBA decision a Fellow would trust an agent to make *autonomously*, and what evidence would that require?

## 13. Summary

You can now inventory the production AI stack in pharma HCP marketing and sort each capability onto the deployed/emerging/aspirational ladder with a KPI attached. You can run the five-question audit — KPI, data, evidence, maturity, buzzword — on any capability claim, and you can spot attribution circularity (the platform that serves the ad measures the lift) and relabeled architecture words. Most importantly, you have internalized the chapter's discipline: in this market, capabilities are mostly real and effectiveness claims are mostly un-validated, and your professional value is the precision to say which is which — without collapsing into either credulity or blanket cynicism. That precision is your midterm artifact, the vendor-claim audit, and the seed of every later brief.

## 14. Key Terms

- **Next-Best-Action (NBA):** an AI recommendation of which HCP, channel, message, and moment to engage; optimizes reachable-responder engagement, not clinical need.
- **MLR (Medical-Legal-Regulatory) review:** the mandatory compliance gate for promotional content; the target of "acceleration" claims.
- **Trigger-based POC targeting:** delivering a contextual ad when a diagnosis/event code fires in the EHR at or near the prescribing moment.
- **Propensity / predictive audience modeling:** scoring HCPs by likelihood to prescribe, to target them before a prescribing event.
- **Attribution circularity:** the structural conflict in which the platform that serves an ad also measures its lift, with no independent firewall.
- **Omnichannel orchestration:** coordinating all channels for one HCP for coherence — coordination, not ubiquity.
- **Deployed / emerging / aspirational:** the maturity ladder — in production / in pilot / in the press release.
- **Human-in-the-Loop (HITL):** the consensus MLR pattern where AI does quantitative checks and humans keep contextual/ethical judgment.

## 15. Bridge

You can now name and rate every claim a platform makes. But naming a claim is not grading its evidence. The next chapter builds the framework that lets you say *how good* the evidence behind a claim actually is — and it opens with a vendor case study claiming 44% script lift in which every single sentence is true and none of it is causal evidence.

## 16. Further Reading

- Bergstrom, C. T., & West, J. D. *Calling Bullshit: The Art of Skepticism in a Data-Driven World* (2020). The foundational posture for this chapter — how to interrogate impressive-sounding data claims, spot circularity, and recognize unfalsifiable numbers. Directly powers the audit rubric.
- Agrawal, A., Gans, J., & Goldfarb, A. *Prediction Machines: The Simple Economics of Artificial Intelligence* (2018). Frames what AI actually does economically — makes prediction cheap — and why "the model predicts X" is not "the platform achieves outcome Y." Central to the deployed-vs-claimed distinction.
- Grinsztajn, L., Oyallon, E., & Varoquaux, G. "Why do tree-based models still outperform deep learning on typical tabular data?" *NeurIPS 2022* (Datasets & Benchmarks Track). The empirical reason an "MoE" claim on tabular NPI data should not impress you on its own; developed in Chapter 6.
- Veeva and IQVIA 2025–26 commercial-AI announcements (primary vendor sources). Read as dated *capability* evidence, not effectiveness evidence — and pair every named product with the stable principle it illustrates, because the names age fast. [verify links current at time of use]
- FDA Office of Prescription Drug Promotion (OPDP) enforcement materials, 2025 wave. Primary-source context for the compliance check; confirm letter counts and dates against FDA.gov before citing. [verify]

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
