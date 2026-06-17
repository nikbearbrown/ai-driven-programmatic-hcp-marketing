# Chapter 4 — What Today's AI Stack Actually Does (and Claims)
*A capability is real. An effectiveness claim is something else. Knowing the difference is the only professional skill that survives this market.*

Here is the problem with a pharma marketing-technology deck: it is not lying to you. That is what makes it hard.

A deck lands in your inbox. The headline reads: *"The world's first AI-powered operating system for healthcare marketing, powered by an adaptive Mixture of Experts."* Underneath are six capability tiles — NPI audience intelligence, conversational AI, SMART-on-FHIR workflow integration, creative-experience optimization, MLR acceleration, and federated learning across the network. A footer cites a Frost & Sullivan recognition and a "20:1 return on investment."

Your first instinct is suspicion, which is correct. But suspicion is not an audit, and dismissal would throw away the true part along with the false. The honest reading is more interesting than either credulity or cynicism, because the claim is *partly true* — and "partly true" is precisely the condition that requires you to do the work.

Take "operating system" first. Stripped of the swagger, this is a claim of platform consolidation: identity resolution, point-of-care ad inventory, programmatic buying, account-based marketing, co-pay programs, and analytics running on one unified data layer instead of six stitched-together vendors. That is a real, defensible architectural claim. Doceree, the platform whose language this echoes, genuinely consolidates these functions. [verify — confirm current Doceree capability map against primary source] "Operating system" is a marketing flourish over a true plumbing fact.

Now take "adaptive Mixture of Experts." A Mixture of Experts is a real machine-learning architecture — specialized sub-models plus a router that decides which to activate — and we will dissect it properly in Chapter 7. Two things are true at once. First, the specific deployment is not independently verified; you have the vendor's word that a MoE is running and the vendor's word that it helps. Second, even if a genuine MoE is running, the underlying task here is NPI-level tabular prediction — which is precisely the regime where, as Chapter 6 will show, a well-tuned gradient-boosted tree ensemble is the state of the art and a MoE is likely indistinguishable from, or worse than, that boring baseline (Grinsztajn, Oyallon & Varoquaux, NeurIPS 2022). The architecture word may name something real and still tell you nothing about whether the system is any good.

And the "20:1 ROI"? A vendor-generated number, measured by the vendor, with no control group and no independent audit. The Frost & Sullivan recognition is paid industry recognition, not peer review.

Verdict before we go further: platform-consolidation claim, plausible. MoE superiority claim, unproven. ROI claim, un-evidenced. Every sentence on the deck can be literally accurate while the deck as a whole proves nothing about effectiveness. That coexistence — true sentences, no causal evidence — is the disease this chapter diagnoses.

---

## The maturity ladder

The single most useful move you can make with a capability deck is to sort each claim onto a three-rung maturity ladder and attach a KPI to each rung. Not because the ladder resolves anything, but because it forces you to ask the right prior question: is this *deployed*, or is this *described*?

**Deployed and mature.** Trigger-based point-of-care targeting. An ICD-10 diagnosis code fires inside the EHR and a contextual ad is delivered at or near the prescribing moment — the mechanism Chapter 1 traced through CDS Hooks and SMART on FHIR. This is the field's consensus current production capability, in use at scale, reliably producing higher HCP engagement than non-contextual digital placements. The capability is unambiguously real.

**Deployed at scale.** Predictive audience modeling — propensity models trained on claims data plus behavioral signals that identify high-potential HCPs before a prescribing event, so a brand can reach them early. OptimizeRx's DAAP, Doceree's intelligence layer, and IQVIA's OCE+ are production examples. [verify product names and current positioning against vendor documentation] The KPI is engagement or new-to-brand prescriptions. The modeling is genuine. Whether it *causes* incremental scripts is a separate question, and it is the question Chapter 8 is built to answer.

**Deployed but task-scoped.** Next-Best-Action recommendation — an AI system recommending which HCP, which channel, which message, at which moment, with the field rep as the human delivery mechanism for the AI-orchestrated sequence. Veeva's AI Agents for Vault CRM and IQVIA's NBA agents built with NVIDIA are concrete, dated examples from 2025. [verify] The crucial nuance: "agentic" in this wave mostly means task-assistive. Drafting call reports. Surfacing treatment barriers from rep notes. Speeding CRM work. Not autonomous analytical decision-making. A very good intern, not an autonomous analyst.

**Emerging and contested.** MLR acceleration and AI-assisted content generation — AI pre-screens promotional content for incomplete claims or missing references, links copy to pre-approved claims libraries, and drafts reviewer summaries. Veeva's PromoMats Content Agent is an example. [verify] Whether this actually compresses cycle time at the claimed rate is genuinely uncertain, and we will sit with that uncertainty in the next section rather than resolve it prematurely.

**In press releases.** Federated learning for targeting models — training on distributed patient data without centralizing it. Vendors reference it. Whether it is running at production scale in this market is not demonstrated by any source independent of the vendors themselves. Treat it as aspirational until shown otherwise.

<!-- → [TABLE: Five-row maturity ladder — columns: capability, maturity rung, target KPI, evidence type available, verdict. Rows: trigger-based POC targeting, predictive audience modeling, Next-Best-Action, MLR acceleration, federated learning. Caption: "The maturity ladder applied to the current production stack. Note that 'evidence type available' is vendor-generated for every row — that is the shared vulnerability."] -->

The misconception to kill on sight: if a vendor names a capability, it is deployed and proven. Capabilities in this market are mostly real. Effectiveness claims attached to them are mostly not independently validated. Those are different sentences, and conflating them is the professional error this book exists to prevent.

---

## What Next-Best-Action actually computes

NBA deserves a precise definition because the gap between what it does and what the brochure implies is especially wide.

An NBA system ingests claims data, behavioral engagement signals, and calendar and territory constraints. It outputs a ranked recommendation: this HCP, this channel, this message, this week. The rep executes it. The target KPI is engagement, call response, or new-to-brand prescriptions.

Here is the misconception worth dwelling on, because it recurs across the whole book: **NBA optimizes for reachable responders, not for patients who most need the drug.** The system scores physicians by engagement-likelihood — who is most likely to open an email, take a call, respond to a POC card. That is an optimization over the marketer's objective function, which is efficient engagement. It is not an optimization over clinical appropriateness. A physician who is highly responsive to commercial messages and a physician who is treating the highest-burden patients are different physicians, and NBA reliably finds the former.

This inversion matters for the same reason the split-agency structure in Chapter 1 matters. The system is genuinely good at its actual job. Its actual job is just not the one the brochure implies.

The 2025–26 "agentic" framing is real but should be read carefully. When Veeva announces an "Agentic Call Report" that surfaces treatment barriers from a rep's visit notes, that is a genuine productivity tool — it saves the rep from administrative work and surfaces clinically relevant signals the brand team wants. The effectiveness claim grafted onto it — "better engagement coordination leads to more scripts" — is exactly the claim that requires a holdout group to test. No independent study supplies one.

---

## MLR acceleration — the most contested ROI in the stack

MLR review — the Medical, Legal, and Regulatory gate every piece of promotional content must pass before a rep can carry it or a platform can run it — has historically taken roughly 50 to 60 days per piece. [verify] AI is being deployed to compress that: pre-screening for incomplete claims, flagging missing references, linking copy to pre-approved claims libraries, routing low-risk modular content, and drafting reviewer summaries so the human committee can move faster.

The consensus implementation pattern is Human-in-the-Loop: AI does the quantitative checks, humans keep the contextual and ethical judgment. This is the right architecture for the task, and the operational deployment is real.

Now hold two numbers in tension and resist resolving them.

McKinsey has cited a 50 to 65 percent reduction in regulatory-submission timelines at some companies. [verify — methodology unclear] An MIT study found that 95 percent of enterprise generative-AI pilots are failing. [verify — methodology unclear] Both circulate without transparent methodology. They appear to describe different populations, different task definitions, or different stages of the same adoption curve. The honest move is to present both, attribute both, and treat neither as settled.

A third datum reframes the whole thing. Promotional-material production in the US rose 29 percent year over year while 77 percent of approved content is rarely or never used by field teams. [verify] Volume is up. Value is not obviously up. The real constraint in MLR is not speed — it is governance and relevance. If 77 percent of what clears review never gets used, faster generation makes the governance problem worse, not better. "50% faster MLR" is an answer to a question nobody asked.

<!-- → [CHART: Two-bar chart per year, 2020–2024 — left bar: total promotional materials submitted for MLR review; right bar: materials actively used by field teams. Caption: "If the 77%-unused figure is accurate, speed is not the binding constraint. The chart makes the governance problem visible as the gap between bars."] -->

So when a company reports faster MLR review times, the audit questions write themselves: faster on which content tiers? Measured how? Did the rejected-content rate change? Did the rate of post-launch FDA enforcement letters change? That last question matters. The FDA's September 2025 enforcement wave — more than 200 letters, AI-assisted surveillance — targeted exaggerated efficacy claims and inadequate fair balance. [verify enforcement specifics against primary FDA sources] AI-accelerated content generation, if ungoverned, scales the production of problematic content as fast as it scales the production of clean content. The FDA is now using AI to catch what AI is generating.

---

## Omnichannel — coordination, not ubiquity

Physician access changed permanently after COVID. By early 2024, roughly 45 percent of US physicians made themselves available to pharma reps, and approximately 30 percent limited access to a single brand. [verify] The channel mix shifted accordingly: in-person reps declining, remote detailing normalized, email high-volume but low-engagement, EHR point-of-care the fastest-growing and highest-conversion channel, endemic digital (Medscape, Doceree's physician network) high-trust but moderate-scale, programmatic open web broad-reach but low-conversion.

Omnichannel orchestration is the coordination of all those channels for a single HCP so the brand experience is coherent rather than overwhelming. NBA decides which channel each physician is most responsive to, suppresses channels where they are not, and sequences messages so the rep call and the EHR trigger and the email reinforce each other rather than firing simultaneously and competing for the physician's attention.

The misconception is that omnichannel means being everywhere. It does not. It means coordination. A physician hit in one week by a rep visit, two emails, retargeting banners, and an EHR trigger has a fragmented brand experience, not an omnichannel one. Orchestration exists precisely to prevent that. In practice: a physician who ignores email but engages endemic content gets email suppressed and a Medscape placement plus a virtual detail prioritized. The system is adjusting in real time to revealed preference — which is genuinely useful, and which is still optimizing for the marketer's objective, not the patient's.

<!-- → [DIAGRAM: Single HCP at the center; radiating lines to six channels (in-person rep, virtual detail, email, EHR/POC card, endemic digital, programmatic). Two versions side by side: left labeled "fragmented" (all channels firing same week); right labeled "orchestrated" (two channels active, four suppressed based on engagement history). Caption: "Omnichannel is a sequencing and suppression problem, not a reach problem."] -->

---

## The audit: five questions for any claim

This is the chapter's named artifact and the structure the rest of the book uses. For any capability claim, run five questions in order.

**One: what KPI does it actually move?** Is the claimed outcome *lift* — incremental prescribing above what would have happened without the intervention — or *engagement* — a physician opened an email, clicked a card, took a meeting? These are very different. Engagement is a leading indicator at best. Lift requires a counterfactual (Chapter 5). Many claims measure the former and imply the latter.

**Two: what data feeds it, and who measures the result?** This is where attribution circularity lives. If the platform that serves the ad is also the platform that observes the prescribing and reports the lift, there is no independent firewall. The party with a commercial interest in a high number is producing the number. Every script-lift figure in this market — the range runs from 4 percent to 44 percent — is vendor-generated in exactly this way. This does not make the numbers false. It makes them uninformative about causal effect.

**Three: what evidence?** A vendor case study is not peer-reviewed evidence. An industry-association recognition is not independent validation. A randomized holdout, pre-registered, measured by a party with no stake in the outcome — that is evidence.

**Four: deployed, emerging, or aspirational?**

**Five: does a buzzword name a real architecture, or is it a relabel?** "Mixture of Experts" may name a real system. It does not tell you whether that system outperforms a gradient-boosted tree on tabular NPI data. "Federated learning" may describe real infrastructure. It does not tell you whether the resulting model is better than a centrally trained one. "Agentic" may describe real task automation. It does not tell you whether the tasks being automated are the binding constraint on commercial effectiveness.

<!-- → [INFOGRAPHIC: Five-question audit rubric as a vertical flowchart — each question in a box, with branch paths for "answered clearly" vs. "not answered / circular" — converging at a bottom verdict: test it / watch it / believe it / route to Chapter 7. Caption: "Run this rubric on every vendor claim before citing any number."] -->

A useful economic frame: AI makes prediction cheap. It does not supply judgment, and it does not guarantee a business outcome. "The model predicts X" and "the platform achieves outcome Y" are different claims. The gap between them is where the audit lives (Agrawal, Gans & Goldfarb, *Prediction Machines*, 2018).

---

## The deck, audited tile by tile

Return to the opening deck. The first pass — dismissing the whole thing as hype — was the wrong move, and it is worth seeing why. Blanket cynicism would have discarded the true part (genuine platform consolidation, genuinely deployed trigger targeting) along with the unproven part. The Fellow's value is precision, not attitude.

The second pass runs the rubric on each tile.

Trigger and SMART-on-FHIR targeting: deployed and mature. KPI is engagement at the point of care. Data is vendor-served and vendor-measured — attribution circular. Evidence is vendor case studies. Verdict: real capability; effect size unproven.

Predictive audience and NBA: deployed at scale. KPI is engagement and new-to-brand scripts. Same NPI infrastructure serves and measures. Evidence is vendor-generated. Verdict: real capability; incremental effect untested (Chapter 8).

MLR acceleration: emerging and contested. KPI is cycle time. Data is internal operations data. Evidence conflicts — McKinsey vs. MIT, neither methodology transparent. Verdict: speed plausible; value-add genuinely uncertain.

Federated learning: aspirational at scale. No KPI demonstrated. No independent evidence. Verdict: treat as aspirational.

"Adaptive MoE routing": architecture claim. Implies accuracy improvement. No independent evidence. Verdict: possibly a real architecture; superiority on this task unproven (Chapter 7).

Conversational AI: emerging. KPI is engagement. Evidence is vendor-only. Verdict: real capability; effect unproven.

The 20:1 ROI: labeled and set aside. Un-controlled vendor number. The Frost & Sullivan badge: labeled and set aside. Paid recognition.

The lesson is that a single deck contains capabilities at every rung of the ladder, and the honest verdict is heterogeneous. The audit does not collapse to a single score. It produces a capability-by-capability map that a product team can actually use — which is what a vendor scorecard cannot do and which is why the audit is the Fellow's first artifact.

The limit: this audit tells you what is plausible and what is unproven. It cannot tell you what is true. That requires the control group and the independent measurement that Chapters 5, 6, and 8 build toward. The audit is the entry ticket to the evidence problem, not its resolution.

---

## What would change my mind

The chapter's central thesis — that most effectiveness claims in this market are not independently validated — would require revision if an independent party, academic or regulatory, with no data dependency on the platform, published a pre-registered controlled evaluation of an EHR or NBA capability and found the vendor's effect size held up. One credible independent replication of a script-lift figure in a peer-reviewed venue would move the whole category from "real capability, unproven effect" toward "real and evidenced." None exists today. The absence is the point, and it is falsifiable.

## Still puzzling

If MLR acceleration genuinely cuts cycle time, why does 77 percent of approved content go unused — is the bottleneck never speed, always relevance? If so, what is the AI actually buying the brand?

The MIT "95% of pilots fail" and McKinsey "50–65% faster" figures cannot both describe the same reality cleanly. Which subset of work does each describe, and can anyone produce the methodology?

"Agentic" tooling is task-assistive today. What is the first NBA decision a Fellow would trust an agent to make autonomously, and what evidence would that trust require?

---

**LLM exercise (copy-paste prompt):**

> "Here is the text of a pharma marketing-platform capability page: [PASTE]. Extract every distinct capability claim and every effectiveness or ROI claim as separate rows. For each row: (1) state the claimed KPI, (2) label the claim as a capability claim or an outcome claim, (3) flag whether any number cited is independently sourced or vendor-sourced, (4) flag any architecture buzzwords (MoE, federated learning, agentic, operating system). Do not assess whether the claims are true — only categorize them."

Then run the verdict pass yourself. The model will extract faithfully; the maturity rating and the circularity flag require your judgment.

**CLI exercise.** Save three vendor capability pages as plain text. Run:

```bash
grep -i -E "lift|roi|x return|increase|%" vendor1.txt vendor2.txt vendor3.txt | wc -l
```

Count how many quantified effectiveness claims the market makes across three pages. Then grep for citations with `grep -i "doi\|pubmed\|ncbi\|journal"` and count how many carry an independent source. Record the ratio.

**AI Validation exercise.** For every claim your LLM categorized as "independently sourced," open the source yourself. Confirm the number exists. Confirm the measuring party is not the selling party. Record how many "independent" labels survive the check. In this market, expect significant attrition.

**AI Use Disclosure**

*Write two sentences naming exactly what an AI tool did in your work for this chapter and what judgment you supplied that the AI could not. For the Part B standard: name one judgment in your own vendor audit that the AI could not have made.*

---

## Exercises

**Warm-up**

1. *(Recall — tests the maturity ladder)* List the five capability types from the chapter and assign each a maturity rung (deployed / emerging / aspirational) and a target KPI from memory, then check yourself. Where you disagree with the chapter's placement, write one sentence defending your choice. *What this tests: whether you can sort capabilities without collapsing them into a single verdict.*

2. *(Recall — tests attribution circularity)* Define attribution circularity in one sentence. Then name the specific structural feature of the pharma marketing stack — described in Chapter 1 — that makes circularity the default rather than the exception. *What this tests: whether you can connect the audit rubric to the split-agency anomaly.*

3. *(Recall — tests the NBA inversion)* What does Next-Best-Action actually optimize for, and why is that different from what the brochure implies it optimizes for? *What this tests: whether you can state the inversion precisely without dismissing the system as useless.*

**Application**

4. *(Apply — runs the five-question rubric)* Find a real, public pharma-platform capability page. For each capability claimed, fill in the five-question rubric in a table: KPI, data source, evidence type, maturity rung, buzzword flag. Add a one-line verdict per row. *What this tests: whether you can operationalize the rubric on actual vendor material.*

5. *(Apply — MLR acceleration)* A brand reports "50% faster MLR review" after deploying AI-assisted content pre-screening. Write the three follow-up questions you would need answered before citing that figure, and name the specific independent party who would have to measure each answer. *What this tests: whether you can generate the audit questions a vendor result demands rather than accepting it as stated.*

6. *(Apply — omnichannel)* Describe the difference between a fragmented multi-channel campaign and a genuinely orchestrated omnichannel campaign for a single HCP. Give a concrete example of each using at least three channels. *What this tests: whether you understand orchestration as a sequencing and suppression problem rather than a reach problem.*

**Synthesis**

7. *(Synthesize — capabilities + evidence)* A product manager asks you to evaluate two vendor pitches: Vendor A claims "deployed NBA with 18% engagement lift, Frost & Sullivan recognized." Vendor B claims "emerging predictive-audience modeling, no lift figures yet, methodology available on request." Write a one-page evaluation memo recommending which vendor to run a pilot with and why. Your memo must use the maturity ladder, the five-question rubric, and the attribution-circularity frame. *What this tests: whether you can synthesize the chapter's tools into a decision-relevant output.*

8. *(Synthesize — the stack end to end)* Connect the capability inventory in this chapter to the split-agency structure in Chapter 1. For each capability (POC targeting, NBA, MLR acceleration, omnichannel), state which party in the prescriber/patient/payer/institution split benefits, which party bears the cost or risk, and whether the capability narrows or widens the gap between commercial optimization and patient welfare. *What this tests: whether you can trace commercial AI capabilities back to the structural anomaly the book opened with.*

**Challenge**

9. *(Challenge — design an independent evaluation)* Design a study that would produce credible causal evidence that NBA-coordinated omnichannel engagement increases *clinically appropriate* prescribing — not just branded prescribing volume. Specify the comparison group, the outcome measure, the randomization unit, the measurement party, and the primary threat to validity. You do not need to solve the threat — name it and explain why it is the hardest one. *What this tests: whether you can specify the evidence standard the market currently lacks and articulate why producing it is genuinely hard.*
