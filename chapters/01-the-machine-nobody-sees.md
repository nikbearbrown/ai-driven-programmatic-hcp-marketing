# Chapter 1 — The Machine Nobody Sees
*How a physician clicks and a payer pays and neither one quite understood what happened.*

A family-medicine doctor opens a patient's chart. The patient is fifty-four. She quit smoking eight months ago. The chart carries the ICD-10 code Z87.891 — personal history of nicotine dependence — which is not a diagnosis so much as a flag: this person used to be at risk, may be at risk again, is worth watching. The physician has seen this code a thousand times. She moves toward the prescribing screen.

In the right-hand sidebar, a card appears. It is the color of a clinical reminder. It is the size of a drug-interaction warning. It names a branded smoking-cessation medication. At the e-prescribing screen, a co-pay card loads automatically; the patient's out-of-pocket cost drops to nearly zero.

The physician does not experience this as advertising. There is no banner. There is no "Sponsored" label that registers. Nothing interrupts. The card arrived through the same software plumbing that carries safety alerts, and it looks, mechanically, like medicine — because, mechanically, it arrived like medicine.

Somewhere upstream, a vendor's case study claims this kind of placement produces a "44% script lift." The physician cannot evaluate that claim. The patient cannot see it. The insurer who will reimburse 95% of a list price the physician never saw was never consulted — even though a clinically equivalent generic sits one formulary tier away at a fraction of the cost.

A whole machine has acted. Almost none of the people it acted upon can describe how it works. That is the machine nobody sees. The first job of this book is to teach you to see it.

---

## The broken loop

Start with the physics of ordinary advertising, because pharma breaks it and the break is everything.

When you see an ad for running shoes, you are the person who decides to buy them, pays for them, and wears them out. Your wallet disciplines your choice. If the shoes cost too much, you walk away. Economists call this consumer sovereignty, and most of advertising theory rests on it: the message goes to the buyer, the buyer feels the price, the market self-corrects.

Pharma severs every link in that chain.

The **physician** decides — writes the prescription. The **patient** consumes — takes the drug. The **payer** (a commercial insurer, an employer plan, Medicare, Medicaid) pays — often the overwhelming majority of the cost. And the **institution** — a health system, a pharmacy benefit manager, a formulary committee — constrains the menu of what can even be chosen.

Four parties. Four roles. The person who decides bears almost none of the cost. The person who pays had no voice in the decision. The person who consumes is downstream of both.

This is a well-described structure in health economics: a principal–agent problem with split agency. The physician is supposed to act as the patient's agent for the clinical decision. But the physician is also the *target* of the commercial message, and the information asymmetry between them — physician over patient — is enormous.

The common misreading is to call pharma marketing "B2B advertising aimed at doctors." The analogy sounds right: a professional buyer, a sophisticated product, a persuasion effort. But in real B2B, the buyer still pays. The CFO who approves the enterprise software contract feels the price. In pharma, the cost-bearer — the payer — is structurally absent from the transaction. The price sensitivity that disciplines ordinary markets has been engineered out of the room.

This is not a critique. It is a description. Understand the structure and you understand everything that follows: why the targeting works the way it does, why co-pay cards exist, why attribution claims are slippery, why nobody has funded a counter-stack. Every puzzle in this book is a consequence of the same anomaly. The party who pays is not at the table.

![Four-node diagram of prescriber, patient, payer and institution, with the payer's payment arrow having no return arrow to the decision node.](images/01-the-machine-nobody-sees-fig-01.png)
*Figure 1.1 — The split-agency structure that breaks consumer sovereignty*

<!-- → [DIAGRAM: Four-node diagram of prescriber / patient / payer / institution — arrows showing decision flow, payment flow, and consumption flow. Key annotation: the payer's payment arrow has no return arrow to the decision node. Caption: "The split-agency structure that breaks consumer sovereignty. The physician decides; the payer pays; neither has complete information about the other's constraints."] -->

Is this anomaly merely theoretical? Not quite. A study of 2013 Medicare Part D prescribers found that physicians who received industry gifts prescribed 2.3 more claims per patient and 7.8% more branded drugs than non-recipients (analysis of Part D data, PMC5656307). Read that carefully: it is an association, not a causal estimate. We do not know how much of the difference is the gift changing behavior versus industry targeting physicians already inclined toward branded drugs. We will take that puzzle apart in Chapter 5. For now, the anomaly predicts that the incentive structure is visible in behavior — and the data is at least consistent with the prediction.

---

## The spine: NPI and the identity graph

To act on a physician, you must first name her. The naming primitive is the **National Provider Identifier** — a unique 10-digit number assigned to every licensed US healthcare provider. Think of it as a cookie, except permanent, accurate, and tied to real prescribing behavior.

A web cookie is probabilistic. It decays. It gets cleared. It loosely maps to a device that loosely maps to a person. An NPI is *deterministic*. You are not guessing that this IP address probably belongs to a cardiologist in Atlanta. You know the exact prescriber — her specialty, her geography, her prescribing history, the diagnostic mix of her patient panel.


| Property | Web cookie | NPI |
|---|---|---|
| Durability | Decays; cleared by users, expires, blocked by browsers | Permanent — assigned for the provider's professional lifetime |
| Accuracy | Probabilistic; loosely maps device → person | Deterministic; a single named, licensed provider |
| Link to behavior | Inferred from browsing signals | Directly joined to real prescribing records (claims data) |
| Regulatory status | Governed by consumer-privacy and consent regimes | Federal billing identifier; not a HIPAA patient identifier, so it survives de-identification |
| Targeting precision | Audience segments, lookalikes, fuzzy match | Down to a single named prescriber (bid-by-NPI) |

*Table 1.1 — Why NPI-based targeting is categorically different from web advertising: the identity is permanent and directly linked to prescribing data.*


A brand can build a target list of NPIs curated by specialty, geographic market, prescribing history, and patient mix. Against each NPI it can maintain a persistent cross-channel profile: what messages this physician has seen, through which channels, and what prescribing followed. That persistent profile is the HCP identity graph — the subject of Chapter 3. For now, treat it as the spine the whole stack hangs on.

How does a fuzzy business goal become this precise? A brand objective — say, "grow new starts among high-volume cardiologists in the Southeast" — gets compiled into an NPI list. That list drives bid-time decisions at the impression layer: which prescriber sees which creative in which channel. At the frontier, this precision extends to individual auctions. Bid-by-NPI — offered by at least one point-of-care platform — lets a brand set a specific bid for a single, named prescriber. [verify — confirm Bid-by-NPI mechanics against the vendor's primary announcement before publication] The abstraction collapses, step by step, until it points at one doctor opening one chart.

The misconception worth clearing: "targeting doctors must rely on probabilistic matching, like web advertising." No. NPI gives identity without inference. The architecture is not more sophisticated web advertising. It is a different kind of infrastructure built on a different kind of identity — one that was designed by the federal government to track providers for billing, and that the commercial layer has inherited as a targeting primitive.

---

## How the message gets inside the chart

Now the harder question: how does a commercial card get *inside* the EHR at all?

Epic and Oracle Cerner — the two dominant systems — officially prohibit native advertising. So platforms route around the front door by repurposing two open standards that were built for medicine, not marketing.

The first is **CDS Hooks**. CDS stands for Clinical Decision Support — the system of alerts and reminders that fires when a physician takes a clinical action. CDS Hooks is an event-driven HTTP API: when a clinician opens a chart, selects an order, or signs a prescription, the EHR fires an HTTP request to a registered external service. The service returns a "card" that renders inside the EHR. The mature hook types tell you exactly what clinical events are available as triggers: `patient-view` (the chart was opened), `order-select` (an order is being chosen), `order-sign` (an order is about to be signed). These hooks were built to surface contraindication alerts and clinical guidelines. Commercial platforms subscribe to the same triggers to surface branded messages (CDS Hooks specification, cds-hooks.org; HL7 CDS Hooks 2.0).

The second standard is **SMART on FHIR**. SMART stands for Substitutable Medical Apps and Reusable Technologies; FHIR is Fast Healthcare Interoperability Resources. Together they define a protocol by which an approved third-party app can launch *inside* the EHR — embedded in Epic's Hyperspace, typically inside an iframe — and receive patient, encounter, and clinician context through standardized FHIR data resources. The authentication handshake uses OAuth 2.0: on launch, the EHR passes a short-lived token, and after the exchange the app receives context claims identifying which patient, which encounter, which clinician. It was designed so that a clinical decision-support app built by one vendor could run inside any EHR that supports the standard. Doceree's Spark product uses the identical protocol for branded engagement (SMART App Launch v2.2.0, HL7; Epic SMART on FHIR documentation).

![Two sequence diagrams: a CDS Hooks card flow and a SMART on FHIR app launch, both ending in a commercial card rendered inside the EHR.](images/01-the-machine-nobody-sees-fig-02.png)
*Figure 1.2 — The two clinical interoperability rails commercial messages ride*

<!-- → [DIAGRAM: Sequence diagram showing the CDS Hooks trigger flow — physician action → EHR fires hook → external service receives hook → returns card → card renders in EHR sidebar. Second sequence shows SMART on FHIR app launch. Caption: "The two clinical interoperability rails commercial messages ride. Both were designed for safety alerts; both are now available to commercial messages delivered through approved app channels."] -->

The mechanism is important to hold precisely, because the common misconception misses it entirely: "EHR ads are banner ads bolted onto the software." They are not bolted on. They are delivered *through the clinical interoperability layer*, in the same visual tier as drug-interaction warnings and guideline alerts. The card in the opening case looked like a clinical reminder because it arrived through the same plumbing as a clinical reminder. The same loudspeaker that announces a fire alarm has been rented for advertising.

Trace the opening case through this now. The physician enters ICD-10 Z87.891 → a `patient-view` or `order-select` hook fires → a commercial service returns a smoking-cessation drug card → the card renders in the sidebar → at the e-prescribing screen, a co-pay assistance card loads through the same channel. Each step is a standard clinical workflow event. The commercial layer is riding the interoperability rails the healthcare system built for itself.

Several platforms now compete for this channel. Doceree's Spark — with more than 150 direct EHR integrations — is the largest single direct point-of-care engagement platform by integration count; the company describes itself as "an AI-powered operating system for healthcare marketing," a phrase we will audit in Chapter 4. OptimizeRx's DAAP (Dynamic Audience Activation Platform) reaches a network of over 300 EHR, e-prescribing, and telehealth systems and uses predictive modeling to identify a clinical moment. WebMD Ignite's "Ignite on FHIR" extends the same model to the patient-facing side — inside Epic's MyChart portal. (All capability descriptions are vendor self-reported; treat them accordingly. [verify platform reach figures against primary sources before publication])

Point-of-care spending reportedly crossed $1 billion in annual spend in 2024, with growth of roughly 171% from 2019 to 2023, described by the Point of Care Marketing Association as growing more than four times faster than overall pharma digital spend. [verify these figures against the primary POCMA release and an independent analyst source before publication]

---

## The co-pay card and the lost price signal

Return to the automatic co-pay card that loads at the prescribing screen.

A **co-pay card** is a manufacturer coupon. It lowers the patient's out-of-pocket cost at the pharmacy counter — sometimes to nearly zero for a branded drug that lists at several hundred dollars per month. The mechanism sounds simple and pro-patient. The effect is subtler.

Here is the way to think about it. In the normal market for a branded drug, there is one remaining actor who might exercise price sensitivity: the patient, who sees a co-pay that is higher for the brand than for a generic. That difference — even a modest one — can steer a patient (and through conversation, the prescriber) toward the cheaper equivalent. The co-pay card removes that signal. The patient's out-of-pocket cost converges to zero regardless of whether she takes the brand or the generic. The last disciplining force in the system has been bought off.

Meanwhile the payer — the insurer — still absorbs the full difference in net price. The party who pays is not at the table, and the party who was at the table (the patient, at the pharmacy counter) has been neutralized.

The empirical evidence here is unusually clean by the standards of this field. Dafny, Ody, and Schmitt (NBER working paper w29735, published in *American Economic Journal: Policy*) compared prescribing in the commercial segment — where co-pay coupons are permitted — against Medicare Advantage, where coupons are federally banned. Using that variation as a quasi-experiment, they estimated that introducing a coupon increased the quantity of drugs without generic substitutes by 23–25% in the commercial segment, that net-of-rebate prices were roughly 8% higher, and that approximately 49% of branded drugs with coupons had a generic equivalent or close substitute available at lower cost. [verify the Georgetown "boosted branded sales by over 60%" figure against the original brief and the underlying paper before citation]

![Bar chart comparing the estimated coupon effect on branded-drug volume: a 23 to 25 percent increase in the commercial segment versus a zero baseline in Medicare Advantage where coupons are banned.](images/01-the-machine-nobody-sees-fig-03.png)
*Figure 1.3 — The natural experiment: the estimated coupon effect on branded-drug volume*

<!-- → [CHART: Bar chart showing estimated prescribing-volume effect of co-pay coupon introduction, commercial vs. Medicare Advantage segment, from Dafny et al. Caption: "The natural experiment: commercial insurers allow coupons; Medicare Advantage does not. The gap isolates the coupon's effect on branded-drug volume."] -->

This is the book's stance, stated plainly: co-pay cards improve affordability for the individual patient at the counter *and* suppress generic substitution and raise total system cost. Both are true. The opening case's automatic co-pay card is this mechanism executing in real time — at the very moment the physician is deciding, before the patient has seen any price at all. Doceree expanded into co-pay card delivery through its Co-Pay.com product in 2025, inserting the coupon mechanism directly into the prescribing workflow. [verify the Co-Pay.com expansion and launch date against a primary source]

---

## The closed loop, and the counter-stack nobody built

Put the pieces together. A brand objective becomes an NPI list. The list drives a bid-time decision. The decision fires a point-of-care impression through CDS Hooks or SMART on FHIR. The impression is followed by a prescription. The prescription — observed through claims data — is attributed to the impression and used to tighten the next NPI list. The loop closes. It optimizes for one output: branded prescribing volume.

Chapter 5 will take apart why the attribution step is far weaker causal evidence than it looks. Chapter 8 will describe what it would take to measure real lift. For now, notice only that the loop is complete and self-reinforcing, and that it has no funded counterweight.

Here is the thing that should unsettle you most. The same SMART on FHIR and CDS Hooks plumbing that delivers a branded ad could, at the moment of prescribing, surface comparative-effectiveness data. It could display the generic alternative and its price. It could show the patient's actual formulary tier. Technically, nothing prevents it. The infrastructure is neutral. **Nobody funds the counter-stack at scale.**

Academic detailing programs — efforts to give physicians unbiased, evidence-based prescribing guidance — exist in fragments: the VA's academic detailing service, NPS MedicineWise in Australia, the Therapeutics Initiative in British Columbia. None operates at commercial scale. None occupies the point-of-care channel at the density that commercial platforms do.

Why? Because the structure of the anomaly predicts it. The parties who would most benefit from unbiased prescribing information are patients and payers. They are exactly the parties least organized to build and fund a clinical information infrastructure. The physician's attention at the moment of prescribing is a contested space, and only one side is paying to occupy it.

![Mirror diagram with the funded commercial closed loop on the left and an unfunded counter-stack of comparative effectiveness, generic alternatives, formulary and patient-cost data on the right.](images/01-the-machine-nobody-sees-fig-04.png)
*Figure 1.4 — The same infrastructure could run both systems; only one is funded*

<!-- → [DIAGRAM: Mirror diagram — left side shows the commercial closed loop (NPI targeting → impression → prescription → attribution → refined targeting); right side shows the counter-stack that could exist but doesn't (comparative effectiveness → generic alternatives → formulary data → patient cost → prescribing decision). Caption: "The same infrastructure could run both systems. Only one is funded."] -->

---

## Reading a vendor page into the stack

One concrete exercise before the chapter closes.

You are given a public product page from a point-of-care platform. The headline reads, roughly: "Our AI-powered operating system reaches the right HCP at the right clinical moment, delivering 44% script lift." Your task is to map this language onto the stack and decide what each phrase actually claims.

First attempt: read it top to bottom and evaluate whether 44% is a good number. Dead end. You have no baseline, no control group, no denominator. The number is uninterpretable on its own.

Second attempt: separate **mechanism claims** from **effectiveness claims**. "Reaches the right HCP" is an identity-layer claim — NPI targeting, plausibly true in the narrow sense that they can construct and activate an NPI list. "At the right clinical moment" is a trigger claim — CDS Hooks firing on a clinical event, also plausibly true. "44% script lift" is an effectiveness claim, and it is the only one that requires causal evidence. The first two describe what the machine does. The third claims what the machine achieves.

Third: ask the three questions that apply to every vendor claim in this book — *what KPI, what data, what evidence?* The KPI is script lift. The data is almost certainly the platform's own observed prescribing among exposed physicians. The evidence for causation is, on the page, nothing. No control group. No holdout. No independent replication. The platform that served the ad also measured the lift. This is attribution circularity, and we will name it formally in Chapter 5.

The conclusion: mechanism claims are credible; the effectiveness claim is unverified — a vendor assertion, to be flagged `[verify]`, never presented as independent evidence.

But notice the limit. This teardown tells you the claim is *unproven*, not that it is *false*. The intervention might genuinely work. Establishing that requires a control group and a causal design, which a product page will never contain. Disbelief is as lazy as belief. The Fellow's job is to specify the test, not to assume the answer.

---

## What would change my mind

The central claim of this chapter is that point-of-care EHR advertising is a fast-growing, structurally under-disciplined channel whose clinical effectiveness is unvalidated by independent evidence. Two things would substantially revise it.

A single well-designed, pre-registered, independent study showing that EHR-integrated messaging produces *clinically appropriate* prescribing change — more correct first-line choices, better guideline adherence, no increase in low-value branded volume — would shift the framing from "a machine optimizing volume with no funded counterweight" to "a contested channel with at least some pro-patient evidence." Conversely, if the POCMA growth figures fail verification and the channel turns out to be a smaller, slower-growing slice of total pharma spend, the "fastest-growing" half of the headline claim should be dropped entirely.

## Still puzzling

If the same plumbing could deliver comparative-effectiveness and cost data at the point of prescribing, what exact funding or policy mechanism would make a counter-stack viable — and why has no payer, who would directly benefit, built one?

Does real-time clinical-context triggering legally cross into "PHI used for marketing"? Platforms assert HIPAA compliance universally; no independent court has resolved the question. The issue seeds Chapter 3's privacy material.

The Part D gifts study shows an association. How much of the prescribing difference is the gift changing behavior versus industry selecting physicians already inclined toward branded drugs? This is the propensity-versus-incrementality puzzle that Chapter 8 is built to resolve.

---

## Exercises

**Warm-up**

1. *(Recall — tests the split-agency structure)* Name the four parties in the pharma transaction — prescriber, patient, payer, institution — and state, in one sentence each, what role each plays. Which one is absent from the commercial message? *What this tests: whether you can describe the structural anomaly without recourse to jargon.*

2. *(Recall — tests NPI as identity primitive)* Explain the difference between NPI-based targeting and cookie-based web advertising. Why is one deterministic and the other probabilistic? *What this tests: whether you understand why HCP targeting is categorically different from consumer digital advertising.*

3. *(Recall — tests the clinical rails)* Name the two interoperability standards commercial platforms use to deliver messages inside the EHR. For each, describe the clinical purpose it was designed for and the commercial use it has been adapted to. *What this tests: whether you can explain the mechanism without collapsing it to "EHR banner ads."*

**Application**

4. *(Apply — traces the stack)* Take this brand objective: "Increase new starts of Brand X among endocrinologists in the Midwest who have not prescribed the drug in the past six months." Trace it forward through every layer of the stack — NPI list construction, bid-time decision, point-of-care impression trigger, co-pay delivery, attribution. At each step, mark where a fully functioning market would have had a payer intervene. *What this tests: whether you can operationalize an abstract business objective into the concrete mechanics of the stack.*

5. *(Apply — vendor-claim audit)* Find a public product page from any point-of-care or NPI-targeting platform. Build a two-column table: each distinct claim on the left, its classification (mechanism or effectiveness) on the right. Flag every effectiveness claim that lacks a stated control group. *What this tests: whether you can separate what the machine does from what it claims to achieve.*

6. *(Apply — co-pay card mechanism)* Explain, in plain language a payer's CFO would follow, why a co-pay card that helps a patient afford a branded drug can simultaneously raise the payer's total drug spend. Use the Dafny et al. quasi-experimental design to support the claim. *What this tests: whether you can hold the individual-level and system-level effects simultaneously without resolving the tension prematurely.*

**Synthesis**

7. *(Synthesize — NPI + point-of-care + attribution)* The same physician receives: (a) a Doceree card inside her EHR when she opens a relevant chart, (b) a banner ad on a medical news site she reads at lunch, and (c) a rep visit the following week. Three months later the platform reports a 44% script lift. Describe, precisely, what the attribution model would have to assume to assign that lift to the EHR card rather than to the rep visit. What would a clean causal design require instead? *What this tests: whether you can connect the stack's mechanics to the attribution-circularity problem.*

8. *(Synthesize — the counter-stack)* The chapter argues that the same CDS Hooks / SMART on FHIR infrastructure could deliver comparative-effectiveness and cost data to prescribers. Identify the three most plausible obstacles — not technical ones, but structural, financial, and regulatory — that explain why no payer has built this at scale. For each obstacle, state what would have to change for it to be overcome. *What this tests: whether you can reason from the split-agency structure to its downstream consequences.*

**Challenge**

9. *(Challenge — causal design)* Design a study that would produce credible causal evidence that point-of-care EHR advertising increases *clinically appropriate* (not merely branded) prescribing. Specify: the comparison group, the outcome measure, the randomization unit, and the primary threat to validity you would have to address. You do not need to solve the threat — just name it and explain why it is the hardest one. *What this tests: whether you can specify the evidence standard the field currently lacks.*

---

## Prompts

### Figure 1.1 — The split-agency structure that breaks consumer sovereignty

Build a four-node systems diagram as a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN, inline CSS and inline JS. Four labeled boxes: PHYSICIAN (decides), PATIENT (consumes), PAYER (pays), INSTITUTION (constrains the menu) arranged in a 2x2 grid. Draw three directed flows with arrowheads — a decision flow physician→patient, a constraint flow institution→physician, a payment flow payer→institution — plus one *missing* return edge from payer back to the physician/decision node, rendered as a dashed grey broken line labeled "no voice in the decision." Highlight the physician node in red as the contested decision point; all other boxes use ink/grey borders. No chart axes. Place each flow label off the arrow centerline. Add hover tooltips per node describing its role. viewBox 700x420, zero baseline not applicable. Structural, not decorative.

### Figure 1.2 — The two clinical interoperability rails commercial messages ride

Build two stacked horizontal sequence diagrams in one self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Top lane "CDS Hooks": four boxes left-to-right — Physician opens chart → EHR fires hook (patient-view) → External service returns card → Card renders in sidebar — joined by right-pointing arrows. Bottom lane "SMART on FHIR": App launch → OAuth 2.0 token exchange → FHIR context (patient/encounter/clinician) → Branded panel renders in iframe. Final box in each lane highlighted red. Render hook names in monospace. Below both lanes, one full-width callout box on a light fill noting both ride the same visual tier as drug-interaction warnings. Hover tooltips per step. viewBox 700x480. Structural sequence, not aesthetic.

### Figure 1.3 — The natural experiment: the estimated coupon effect on branded-drug volume

Build a vertical bar chart, single self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Two categories on x-axis: "Commercial (coupons permitted)" and "Medicare Advantage (coupons banned)". Y-axis = estimated change in branded quantity, percent, zero baseline, domain 0–30%. Commercial bar at ~24% (label "+23–25%") drawn in red; Medicare Advantage shown as a near-zero baseline marker in grey labeled "0% (banned)". Dashed gridlines at 10/20/30. Value labels above bars. Margins top48 right40 bottom56 left64. ALL-CAPS source line attributing Dafny, Ody & Schmitt NBER w29735. Hover tooltips. Caption must hedge the figure as an estimate, not established fact. viewBox 700x420.

### Figure 1.4 — The same infrastructure could run both systems; only one is funded

Build a mirrored two-column flow diagram, single self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Left column "The commercial closed loop — funded": four stacked boxes NPI targeting → Point-of-care impression → Prescription → Attribution, joined by downward arrows, with a left-side feedback arrow from Attribution back up to NPI targeting labeled "refines next NPI list." Left boxes red-bordered. Right column "The counter-stack — could exist, unfunded": Comparative effectiveness → Generic alternatives + formulary tier → Patient cost shown → Prescribing decision, grey-bordered, downward arrows, no feedback loop. Dashed vertical divider between columns. Hover tooltips per node. viewBox 700x480. Structural mirror layout, not decorative.

---

## Chapter 1 Exercises: The Machine Nobody Sees

**Project:** One Drug, End to End
**This chapter adds:** Choose the one branded drug you will carry through the whole book, then map its split-agency stakeholders and the point-of-care surface where its promotion would land.

### Exercise 1 — When to Use AI

**The judgment:** Three tasks in this chapter where AI assistance earns its place.

- *Parsing a vendor product page into a claims table* (mechanism vs. effectiveness, KPI, evidence required). **Why AI works here:** reformatting — you are restructuring text you can read into a grid you can check line by line.
- *Drafting the four-party split-agency map for your chosen drug* (who decides, consumes, pays, constrains). **Why AI works here:** drafting — the structure is known and you supply the drug-specific facts, then verify each role.
- *Generating candidate point-of-care surfaces* where a card for your drug might fire (CDS Hooks trigger types, SMART-on-FHIR launch points). **Why AI works here:** option-generation — you want a broad first list of plausible trigger events, which you then prune against the chapter's three mature hook types.

**The tell:** You are using AI appropriately when you can independently evaluate the output — when you could have written the claims table yourself, just slower.

### Exercise 2 — When NOT to Use AI

**The judgment:** Three tasks here that need your judgment, not the model's fluency.

- *Deciding whether the vendor's script-lift number is credible.* **Why AI fails here:** missing ground truth — there is no control group on the page, and the model will treat a confidently stated number as a fact rather than an un-evidenced assertion.
- *Concluding whether your drug's promotion is clinically appropriate.* **Why AI fails here:** values judgment — appropriateness depends on patient welfare and formulary alternatives the model cannot weigh, and it has no stake in getting it right.
- *Asserting whether real-time EHR triggering legally crosses into PHI-used-for-marketing.* **Why AI fails here:** hallucination risk — no court has resolved this, so the model will invent a confident legal answer with no primary source behind it.

**The tell:** You've crossed the line when AI output is your *reason* for a conclusion rather than a tool for reaching one.
**Series connection:** This trains **T4 Metacognitive** judgment — knowing what you cannot know from a marketing artifact, and refusing to let fluent prose substitute for a counterfactual you never observed.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** A split-agency stakeholder map plus a point-of-care surface inventory for your chosen drug — the foundation document the rest of the project builds on.
**Tool:** Claude. Recommend a **Claude Project** here — persistent drug context (the drug name, class, and competitor set) will be reused in every later chapter, so storing it once in the Project saves you re-pasting it nine times.

**The Prompt:**

```
You are helping me build a teaching case study for a course on AI-driven HCP
marketing. The worked-example drug is a branded SGLT2 inhibitor used for type 2
diabetes, in a class that contains both branded competitors and a generic
substitute (an older non-SGLT2 oral antidiabetic).

Do two things, using only the structure I give you. Use public, general
clinical and market knowledge; do not invent specific statistics, do not state
any effectiveness or lift number, and label anything you are unsure of with
"[verify]".

1. SPLIT-AGENCY MAP. Produce a four-row table for this drug:
   - PRESCRIBER (decides): which specialties write it and why
   - PATIENT (consumes): the patient archetype it targets
   - PAYER (pays): commercial plan / Medicare Part D / Medicaid considerations
   - INSTITUTION (constrains): formulary tier, step therapy, prior auth likely
   For each row, add one column: "where price sensitivity has been engineered
   out of this party's decision." Mark the party absent from the commercial
   message.

2. POINT-OF-CARE SURFACE INVENTORY. List the plausible EHR trigger points where
   a branded card for this drug could fire, mapped to the three mature CDS Hooks
   types (patient-view, order-select, order-sign) and to a SMART-on-FHIR launch.
   For each, give the clinical event that would trigger it and one sentence on
   why a brand team would want that moment. Do NOT assert any of these is
   actually deployed for this drug — only that the mechanism exists.

Output both as markdown tables. End with a one-line note on which single fact in
this map I should verify against a primary source before using it.
```

**What this produces:** A two-table case-study foundation — the split-agency map and the POC trigger inventory — for your drug.
**How to adapt this prompt:** *For your own drug:* replace the first paragraph with your drug, its class, and whether a generic/branded competitor exists; keep everything else. *For ChatGPT/Gemini:* paste the same prompt as a single message; those tools have no persistent Project, so re-paste the drug paragraph each session. *For a Claude Project:* put the drug-identity paragraph in the Project's system/custom-instructions field and send only instructions 1 and 2 as the message.
**Connection to previous chapters:** This is Chapter 1 — it starts the thread. **Preview of next chapter:** In Chapter 2 you will profile this same drug's lift-vs-equity position using TRx/NBRx/loyalty deciles.

### Exercise 4 — CLI Exercise

**What you're building this chapter:** A verified local note confirming that the three mature CDS Hooks types are real clinical-workflow events your drug's promotion could ride. · **Tool:** Claude Code (single-file fetch + grep, no multi-file orchestration needed). · **Skill level:** Beginner.

**Setup:**
1. Create a project folder `one-drug/` with an empty `ch01-poc-rails.md` you will fill.
2. Claude Code installed and authenticated.
3. Add a CLAUDE.md rule: "Never fabricate spec contents — only quote text actually fetched from the source URL."

**The Task:**

```
In the folder one-drug/, do the following and nothing else:

1. Fetch the public CDS Hooks specification homepage (https://cds-hooks.org/)
   into a local file cdshooks.html. If the fetch fails, stop and tell me — do
   not guess the contents.
2. Search cdshooks.html for the three hook types: patient-view, order-select,
   order-sign. For each one found, quote the surrounding sentence.
3. Write ch01-poc-rails.md with: one short paragraph per hook type confirming it
   is a clinical-workflow event, each quoting the fetched text, and a final
   one-line statement of which hook would most plausibly carry a card for a
   branded SGLT2 inhibitor (an order-select on starting an oral antidiabetic).

Do not modify cdshooks.html. Do not create any other files. Stop after writing
ch01-poc-rails.md and show me the file.
```

**Expected output:** `cdshooks.html` (raw, untouched) plus `ch01-poc-rails.md` with three quoted confirmations and one drug-specific line.
**What to inspect:** That each paragraph quotes text that actually appears in the fetched HTML — not a paraphrase the model produced from memory.
**If it goes wrong:** Most likely failure is the model "confirming" a hook type that the page does not literally contain (the site structure changed). Recovery: open `cdshooks.html` yourself, grep for the term, and if it is genuinely absent, have the model mark it `[verify]` rather than asserting it — do not just re-run.
**CLAUDE.md / AGENTS.md note:** Add the standing rule "All spec/standard claims must quote fetched source text, never model recall."

### Exercise 5 — AI Validation Exercise

**What you're validating:** The split-agency map and POC inventory your Exercise 3 prompt produced. · **Validation type:** Structured-data + Factual. · **Risk level:** Med — this map seeds every later chapter, so an error here propagates.

**Setup:** Use your Exercise 3 output as the artifact.

**The Validation Task:**

```
Validation Checklist — Chapter 1 (Split-Agency Map + POC Inventory)

For each item mark Pass / Fail / Cannot-determine and add one line of evidence:

- Correctness: Are the four parties correctly assigned roles (decides /
  consumes / pays / constrains) for THIS drug?
- Completeness: Is the absent-from-the-message party identified, and is the
  "price sensitivity engineered out" column filled for every row?
- Scope: Did it stay within mechanism/stakeholder mapping, or did it sneak in an
  effectiveness or lift claim it was told to avoid?
- Chapter-specific 1: Are the POC triggers mapped to the THREE mature hook types
  (patient-view, order-select, order-sign) and not to invented hook names?
- Chapter-specific 2: Is every POC row framed as "the mechanism exists," not
  "this is deployed for this drug"?
- Failure-mode check (fluent-but-wrong + vendor-claim laundering): Did the model
  restate any vendor capability ("AI-powered operating system," a script-lift
  figure) as an established fact rather than a labeled claim? Flag any number
  presented without [verify].
```

**What to do with your findings:** Pass → use it as your project foundation. One fail → revise the prompt and re-run that section. Multiple fails or several Cannot-determines → build the map yourself from the chapter text; this is a "When NOT to Use AI" moment, because a contaminated foundation corrupts nine chapters.
**AI Use Disclosure prompt (mandatory):** Write two sentences — what the AI produced (e.g., "the model drafted the four-party map and POC trigger list") and how you used it, plus one thing it could not determine that needed your judgment (e.g., "whether the order-select trigger is actually live for this drug, which the model could not know and I marked [verify]").
**Series connection:** Trains detection of **vendor-claim laundering** under **T4 Metacognitive** judgment — catching the moment an unproven marketing assertion gets quietly upgraded to fact.
