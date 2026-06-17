# Chapter 1 — The Machine Nobody Sees

## Chapter overview

By the end of this chapter you will be able to describe the full HCP (health-care professional) marketing stack — from the identity layer that names a single physician, through the programmatic impression that fires inside the electronic health record (EHR), to the attribution loop that claims credit for the result — precisely enough to critique it rather than be impressed by it. You will be able to trace a brand objective forward into a point-of-care message, and trace that message backward into the infrastructure that produced it. Most of all, you will be able to name the structural anomaly that makes pharma marketing different from every other kind of advertising: the party who pays the bill is not at the table.

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain why the split of prescriber / patient / payer / institution breaks ordinary advertising theory.
2. **(Apply)** Trace the data flow from a brand objective through NPI (National Provider Identifier) identity to a point-of-care impression.
3. **(Analyze)** Distinguish what the stack optimizes from what patient welfare would require.

## Opening case — the card in the sidebar

A family-medicine physician opens a patient's chart in Epic. The patient is a 54-year-old who quit smoking eight months ago; the chart carries the diagnosis code Z87.891, "personal history of nicotine dependence." Nothing unusual happens — except that, in the right-hand sidebar of the screen, a small card appears. It is the same size, the same color, in the same visual layer as the drug-interaction warnings and the clinical-guideline reminders the physician sees a hundred times a day. The card mentions a branded smoking-cessation drug. A few clicks later, at the e-prescribing screen, a co-pay card populates automatically: the patient's out-of-pocket cost drops to almost nothing.

The physician does not experience this as advertising. There is no banner, no "Sponsored" label that registers, no interruption that feels like a sales pitch. The card looks like part of the medical software. And in a precise technical sense, it *is* part of the medical software — it arrived through the very same plumbing that delivers safety alerts.

Here is the failure we will sit with for the rest of the chapter. Somewhere upstream, a vendor's case study says this kind of placement produced a "44% script lift." The physician cannot evaluate that claim. The patient cannot see it. The payer — the insurer who will reimburse roughly 95% of a list price the physician never saw — was never consulted, even though a clinically equivalent generic sits one formulary tier away at a fraction of the cost. A whole machine has acted, and almost none of the people it acted upon can describe how it works. That is the machine nobody sees. Your first job as a Fellow is to learn to see it.

## Core concept 1 — The structural anomaly: the party who pays is not at the table

Ordinary advertising rests on a quiet assumption so familiar we never state it: the person who *sees* the ad is the same person who *decides* to buy, *pays*, and *consumes*. When you see a sneaker ad, you choose the sneakers, hand over your money, and wear them. Your wallet disciplines your choice — if the sneakers cost too much, you walk away. That feedback loop is what economists call **consumer sovereignty**, and most of advertising theory is built on it.

Pharma breaks every link in that chain.

- The **physician decides** — writes the prescription.
- The **patient consumes** — takes the drug.
- The **payer** (a commercial insurer, an employer plan, or a government program like Medicare) **pays** — often the overwhelming majority of the cost.
- The **institution** (the health system, the formulary committee, the pharmacy benefit manager, or PBM) **constrains the menu** of what can even be chosen.

Four different parties, four different roles. The decision-maker bears almost none of the cost and experiences none of the consumption. This is a classic **principal–agent problem with split agency**: the physician is supposed to act as the patient's *agent* for the clinical decision, but the physician is also the *target* of the commercial message, and the information asymmetry between physician and patient is enormous (the framing is standard in health economics — see "Principal-agent problems in health care," *Health Policy and Planning*, Oxford Academic, 2011).

The common misconception here is that "pharma marketing is just B2B advertising aimed at doctors." It is not, and the reason matters. In normal B2B advertising the buyer still pays and still feels price. In pharma, the cost-bearer — the payer — is structurally *absent* from the message. The price sensitivity that disciplines ordinary markets has been engineered out of the loop. **The party who pays is not at the table.** Hold onto that phrase; it is the single most important idea in the chapter, and every later concept is a consequence of it.

Is this misalignment merely theoretical, or does it show up in behavior? There is at least suggestive evidence. A study of 2013 Medicare Part D prescribers found that 39.1% received gifts from industry, and that gift recipients prescribed 2.3 more claims per patient and 7.8% more branded drugs than non-recipients (Hadland et al. and related Part D analyses, summarized in PMC5656307). Note carefully what this is and is not: it is an **association**, not a clean causal estimate (a point we will take apart in Chapter 5 and again in Chapter 8). It does not prove that gifts *caused* the prescribing. But it tells us the incentive structure the anomaly predicts is at least visible in the data.

## Core concept 2 — The NPI identity layer: the spine the stack hangs on

To act on a physician, you must first *name* the physician. The naming primitive is the **National Provider Identifier (NPI)** — a unique 10-digit number assigned to every licensed US provider.

Think of the NPI as the equivalent of a web cookie, but far better for the advertiser. A cookie is probabilistic, decays, gets cleared, and only loosely maps to a real person. An NPI is **permanent, accurate, and tied to real prescribing behavior**. A brand can build a target list of NPIs curated by specialty, geography, prescribing history, and patient mix, and then maintain a persistent cross-channel profile keyed to each NPI. That persistent profile is the **HCP identity graph** — the subject of Chapter 3. For now, treat it as the spine the whole stack hangs on.

The misconception to clear: "targeting doctors must rely on probabilistic matching like web ads." No. NPI gives *deterministic* identity. You are not guessing that this device probably belongs to a cardiologist in Atlanta; you know the exact prescriber. The 2025 frontier pushes this even further — **Bid-by-NPI** (offered by Tap Native / eHealthcare Solutions) is an auction model that lets an advertiser set a bid at the level of a single, named prescriber. [verify — confirm Bid-by-NPI launch and mechanics against the vendor's primary announcement]

How does a fuzzy business goal become this precise? A brand objective — say, "grow new starts among high-volume cardiologists in the Southeast" — gets compiled into an NPI list, which gets compiled into bid-time decisions about which prescriber sees which creative in which channel. The abstraction collapses, step by step, until it points at one doctor opening one chart.

## Core concept 3 — Point-of-care / EHR as a commercial channel: the mechanics

Now the harder part: how does a commercial message get *inside* the EHR at all? Epic and Oracle Cerner — the two dominant EHR vendors — officially prohibit native advertising. So platforms route around the front door by repurposing two open clinical-interoperability standards that were built for medicine, not marketing.

**SMART on FHIR** (Substitutable Medical Apps and Reusable Technologies on Fast Healthcare Interoperability Resources) is an open standard that lets an approved third-party app launch *inside* the EHR — typically embedded in Epic's Hyperspace, often inside an iframe — and receive patient, encounter, and clinician context through FHIR data resources. The handshake is authorized with **OAuth 2.0**: on launch the EHR hands the app a short-lived launch token, and after the OAuth exchange the app receives an ID token carrying SMART context claims (which patient, which encounter, which clinician). It was designed for clinical apps. Doceree's **Spark** product uses the same standard for branded engagement, described as operating "within approved interoperability frameworks" (SMART App Launch v2.2.0, HL7; Epic SMART-on-FHIR launch context documentation, 6b.health).

**CDS Hooks** (a HL7 standard, built by the same SMART Health IT team) is an event-driven HTTP API. When a clinician takes a workflow action, the EHR fires a *hook* to a registered external service, which returns "cards" that render in the EHR. The mature hook types are revealing: **`patient-view`** (the chart was opened), **`order-select`** (an order is being chosen), and **`order-sign`** (an order is about to be signed). These were built to surface safety alerts and clinical guidelines. Commercial platforms adapt the very same trigger points to fire branded messages — and a card can link out to a SMART on FHIR app (CDS Hooks specification, cds-hooks.org; HL7 CDS Hooks 2.0; Medblocks practical guide).

The misconception: "these are banner ads bolted onto the EHR." They are not bolted on. They are delivered *inside the clinical software, in the same visual layer as drug-interaction warnings and guideline alerts.* That co-location is the whole point — and, as we will see, the whole ethical problem.

Trace the opening case through the mechanics now. The physician enters ICD-10 code Z87.891 → a CDS Hooks `order-select` or `patient-view` hook fires → a smoking-cessation drug card appears in the sidebar → at the e-prescribing screen, a co-pay card populates. **The same standard that surfaces a contraindication surfaces the ad.** As one teaching analogy puts it: the same loudspeaker that announces a fire alarm has been rented out for advertising.

Several platforms now compete to own this channel. Doceree's Spark, with 150-plus direct EHR integrations, is the largest direct point-of-care engagement platform by integration count and positions itself as "an AI-powered operating system for healthcare marketing" — a phrase we will audit hard in Chapter 4. OptimizeRx's DAAP (Dynamic Audience Activation Platform) reaches a 300-plus EHR / e-prescribing / telehealth network and uses predictive AI to identify the right HCP at the right clinical moment. (OptimizeRx is publicly traded as OPRX, which gives us a little more financial transparency — though its script-lift figures remain company-reported, never independent.) WebMD Ignite's "Ignite on FHIR" extends the same model *patient-facing*, inside Epic's MyChart portal — a reminder that the channel is not HCP-only. (Platform descriptions drawn from `pharma-ai-hcp-marketing-synthesis.md`; treat all capability language as vendor self-description until independently verified.)

## Core concept 4 — Co-pay cards and the lost price signal

Return to that automatic co-pay card at the e-prescribing screen. A **co-pay card** is a manufacturer coupon that lowers the *patient's* out-of-pocket cost for a branded drug at the pharmacy counter. It is the most elegant intervention in the broken market — and the most quietly consequential.

Here is the mechanism. Because the patient now feels little or no price difference between the brand and a generic, the **price signal that would otherwise steer them (and, through them, the physician) toward the cheaper equivalent is erased.** Meanwhile the insurer still pays the higher net price. Recall the anomaly: in a normal market, the consumer's price sensitivity disciplines the choice. The co-pay card is a deliberate intervention that subsidizes the one party — the patient — whose price sensitivity could still trigger substitution. It buys off the last disciplining force in the system.

The misconception is seductive: "coupons are pro-patient — they make drugs affordable." For the individual at the counter, yes — affordability improves. But at the level of the system, coupons raise total cost and suppress generic substitution. The evidence is unusually clean for this field. Dafny, Ody, and Schmitt (NBER working paper w29735; published in *AEJ: Policy*) found that introducing a co-pay coupon increased the quantity of drugs *without* generic substitutes by 23–25% in the commercial segment relative to Medicare Advantage, where coupons are banned; that net-of-rebate prices were roughly 8% higher; and that among branded drugs with coupons, about 49% had a generic equivalent or close substitute available at lower cost (NBER w29735; NBER Digest, May 2022). A related Georgetown brief citing Dafny et al. notes coupons "boosted branded sales by over 60%" [verify — confirm this specific figure and its scope against the Georgetown brief and the underlying paper].

This is why the book's stance on co-pay coupons is **nuanced, not a verdict** [contested — see pantry]. They improve affordability for the individual *and* suppress generic substitution and raise system cost. Present both findings; do not resolve it into "good" or "bad." (Doceree's 2025 expansion into Co-Pay.com inserts these cards directly into the prescribing workflow — the co-pay mechanism and the point-of-care channel are converging. [verify — confirm the Co-Pay.com expansion against a primary source])

## Core concept 5 — The closed loop, and the counter-stack that nobody funds

Put the pieces together and you have a closed feedback loop: a brand objective becomes an NPI list, the list drives a bid-time decision, the decision fires a point-of-care impression, the impression is followed by a prescription, and the prescription — observed back through claims data — is attributed to the impression and used to refine the next NPI list. The loop tightens on itself. We will spend Chapter 5 on why the *attribution* step is far weaker evidence than it looks, and Chapter 8 on what it would take to measure real causal lift. For now, notice only that the loop exists and that it optimizes for one thing: branded prescribing volume.

And now the failure that should unsettle you most. The *same* SMART on FHIR / CDS Hooks plumbing that delivers a branded ad could surface comparative-effectiveness data, generic alternatives, and the true cost-to-patient at the prescribing moment. Technically, nothing stops it. The infrastructure is neutral. **Nobody funds the counter-stack at scale.** Academic-detailing programs — efforts to give physicians unbiased, evidence-based prescribing information — exist only in fragments: the VA's academic detailing, NPS MedicineWise in Australia, the Therapeutics Initiative in British Columbia. None operates at commercial scale (see `pharma-marketing-evidence-synthesis.md` §8).

Why? Because the structure of the anomaly predicts it. The parties who would benefit from unbiased prescribing — patients and payers — are exactly the parties least organized to build and fund a counter-infrastructure. The physician's attention at the point of care is a contested space, and only one side is paying to occupy it. The machine nobody sees has no funded opponent.

## Worked example — reading a vendor product page into the stack

**Situation.** You are handed a public product page from a point-of-care platform. The headline reads, roughly: "Our AI-powered operating system reaches the right HCP at the right clinical moment, delivering 44% script lift." Your task is to map this language onto the stack and decide what each phrase actually claims.

**Analytical process (including the dead ends).**

First attempt: read it top to bottom and try to judge whether 44% is "good." Dead end — you have no baseline, no control group, and no idea what the comparison is. The number is uninterpretable on its own.

Second attempt: separate **mechanism claims** from **effectiveness claims**. "Reaches the right HCP" is an identity-layer mechanism claim — it is describing NPI targeting, and it is probably true in the narrow sense that they can target by NPI. "At the right clinical moment" is a trigger/impression mechanism claim — it is describing CDS Hooks firing on a clinical event, also plausibly true. "44% script lift" is an *effectiveness* claim, and it is the only one that requires causal evidence. The first two describe what the machine does; the third claims what the machine *achieves*.

Third step: ask the three questions you will use on every vendor claim for the rest of the book — *what KPI, what data, what evidence?* The KPI is script lift. The data is, almost certainly, the platform's own observed prescribing among exposed physicians. The evidence for *causation* is — on the page — nothing. There is no control group, no holdout, no independent replication. The platform that served the ad also measured the lift. This is **attribution circularity**, and we will name it formally in Chapter 5.

**Resolution.** You conclude that the mechanism claims are credible and the effectiveness claim is unverified — a vendor assertion, to be flagged `[verify]`, never cited as independent evidence. You can describe exactly where in a normal market the payer would have intervened (at the price the physician never saw) and note that the loop has no such intervention.

**The lesson (one sentence).** Most of what a vendor page tells you is true about *mechanism* and unproven about *effect* — and the entire value of a Fellow is keeping those two straight.

**The limit (where it fails).** This teardown tells you the claim is *unproven*; it does not tell you the claim is *false*. The intervention might genuinely work. Establishing that requires a control group and a causal design (Chapter 8), which a product page will never contain. Disbelief is as lazy as belief; the Fellow's job is to specify the test, not to assume the answer.

## Common misconceptions

**"Pharma marketing is just B2B advertising aimed at doctors."** Plausible, because the message is indeed aimed at a professional buyer. It fails because in real B2B the buyer still pays and feels price; here the payer is absent and price sensitivity has been engineered out. Tie it back to the opening case: the physician chose the branded drug with no exposure to the $X-versus-generic difference the insurer will absorb.

**"EHR ads are crude banners bolted onto the software."** Plausible, because we associate "ad" with "banner." It fails because the message rides the *clinical* interoperability standards (CDS Hooks, SMART on FHIR) and renders in the same visual layer as safety alerts. The card in the opening case looked like medicine because, mechanically, it arrived like medicine.

**"Co-pay coupons are unambiguously good for patients."** Plausible, because they obviously lower the price at the counter. It fails at the system level: the NBER evidence shows they raise net prices ~8% and suppress generic substitution, often for drugs with a cheaper equivalent one tier away. The opening case's automatic co-pay card is exactly this mechanism in action.

## Evidence check

- **Independent (peer-reviewed / governmental):** the principal–agent framing (*Health Policy and Planning*); the Part D gifts–prescribing *association* (PMC5656307) — independent but correlational, not causal; the co-pay coupon effects (Dafny et al., NBER w29735 / *AEJ: Policy*) — strong, quasi-experimental, the most solid causal evidence in the chapter. The CDS Hooks and SMART on FHIR standards themselves are documented open specifications (HL7, cds-hooks.org).
- **Vendor-generated:** all platform capability and script-lift language (Doceree, OptimizeRx, WebMD Ignite). The "44% lift" figure is a vendor claim, attribution-circular, flagged `[verify]`, and never to be presented as independent evidence.
- **Hypothetical:** the specific opening-case scenario (the smoking-cessation card) is an illustrative composite built from documented mechanisms, not a recorded event.
- **Contested:** whether co-pay coupons are net pro-patient [contested — see pantry]; whether EHR-integrated advertising produces *clinically appropriate or inappropriate* prescribing change — **no peer-reviewed study exists**, the largest open validation gap in this chapter.
- **`[verify]` flags:** point-of-care channel-growth figures (below); Bid-by-NPI mechanics; the Georgetown "60%" figure; the Doceree Co-Pay.com expansion.

One flagged claim deserves its own line. The chapter's headline research finding — *EHR/point-of-care advertising is the fastest-growing pharma channel with the thinnest independent evidence* — has two halves. The evidence-thinness half is well supported (there is no peer-reviewed study of clinical-impact). The growth-ranking half rests on industry figures: point-of-care reportedly crossed $1B in annual spend in 2024, with ~171% growth from 2019 to 2023 and ~15–22%/year, described as growing more than four times faster than overall pharma digital. **These figures come from the Point of Care Marketing Association (POCMA) and must be verified against the primary release and an independent analyst before publication** [verify].

## Compliance & patient-welfare check

**MLR / FDA fair balance.** Any branded point-of-care message is promotional content subject to Medical-Legal-Regulatory (MLR) review and the FDA's fair-balance requirements (benefits and risks presented with comparable prominence). A card rendered in a cramped EHR sidebar raises an obvious fair-balance question: is there room for risk information at the same prominence as the benefit message? Flag it; route the regulatory judgment to counsel.

**Privacy / HIPAA.** Whether real-time clinical-context triggers constitute "use of PHI (protected health information) in marketing" is **legally unsettled.** Platforms uniformly assert HIPAA compliance and that no PHI leaves the EHR; independent legal analysis is limited. The book's stance: route this to counsel, do not adjudicate it here. Notably, the FDA's September 2025 enforcement wave (200-plus letters, AI-assisted surveillance) targeted DTC and web advertising, **not** EHR ads — point-of-care remains a regulatory near-vacuum (no specific OPDP guidance; ONC information-blocking rules do not cover commercial ads). [verify the enforcement-wave specifics] The US is globally unusual here: EU GDPR / ePrivacy rules would likely prohibit the underlying data flows.

**Patient-welfare note.** The welfare risk is not that point-of-care messaging is inherently harmful — sometimes the messaged drug is the right one. The risk is *asymmetry*: the same infrastructure that could surface a cheaper, equally effective generic at the decision moment surfaces only the paid message, and the patient and payer have no representation in that moment. The welfare question for every Fellow project is the one this chapter ends on: *what would patient welfare require here that the stack does not optimize for?*

## Exercises

1. **(Understand)** In your own words, explain the prescriber/patient/payer/institution split to someone who has only ever seen consumer advertising. Then name the one feature of the split that most breaks ordinary advertising theory, and say why.

2. **(Apply)** Take a single brand objective — for example, "increase new starts of Brand X among rheumatologists in three target states" — and trace it forward through the stack: brand objective → NPI list → bid-time decision → point-of-care impression → attribution. At each step, mark where, in a *normal* market, the payer's price sensitivity would have intervened.

3. **(Analyze — produces an artifact)** Find a *public* product page from a point-of-care or NPI-targeting platform (Doceree, OptimizeRx, or similar). Build a two-column table: every phrase on the page in the left column; in the right column, label each as a **mechanism claim** (identity / trigger / impression / attribution) or an **effectiveness claim**, and flag every effectiveness claim that lacks a control group. This table is your first "vendor-claim audit" artifact and feeds directly into Chapter 4.

## Five-part AI exercise block

**When to use AI.** Use an LLM to accelerate the *mechanical mapping* in this chapter — parsing a long vendor product page into stack layers, drafting a first-pass classification of mechanism-versus-effectiveness claims, or summarizing the CDS Hooks specification's hook types. These are fluent-text tasks where a wrong draft is cheap to catch.

**When NOT to use AI.** Do not use an LLM to *judge whether a script-lift claim is causally valid*, to *characterize HIPAA or FDA compliance*, or to *decide whether a co-pay coupon is pro-patient*. These require domain judgment, legal grounding, and an evidence standard the model does not hold; a fluent answer here is a confident wrong answer.

**LLM exercise (copy-paste prompt):**
> "Here is the text of a point-of-care pharma marketing platform's product page: [PASTE]. For each distinct claim, output a row with: (1) the exact phrase, (2) whether it is a *mechanism* claim (identity / trigger / impression / attribution) or an *effectiveness* claim, (3) what KPI it implies, and (4) what evidence would be required to verify it. Do not assess whether the claims are true — only classify them. Flag any effectiveness claim that does not mention a control group or holdout."

**CLI exercise.** Using the command line, download the public CDS Hooks specification page and the hook-type list (e.g., `curl -s https://cds-hooks.org/ -o cdshooks.html`). Then `grep` for the three mature hook types (`patient-view`, `order-select`, `order-sign`) and confirm, in your own one-paragraph note, that each is a clinical-workflow event a commercial platform could subscribe to.

**AI Validation exercise.** Take the LLM's classification table from the LLM exercise above. Independently re-classify three rows yourself, then check: did the model mislabel any *effectiveness* claim as a *mechanism* claim (a common and consequential error, because it launders an unproven result into a description of how the machine works)? Write one sentence on any disagreement and which of you was right.

## AI Use Disclosure

*Write two sentences naming exactly what an AI tool did in your work for this chapter and what judgment you supplied that the AI could not. For example: "I used an LLM to parse the vendor page into a claims table; I independently determined which effectiveness claims lacked any control group, because the model accepted the vendor's framing as fact."*

## What would change my mind

The central claim of this chapter is that point-of-care / EHR advertising is a fast-growing, structurally under-disciplined channel whose effectiveness is unvalidated. A single well-designed, independent, randomized or pre-registered study showing that EHR-integrated messaging produces *clinically appropriate* prescribing change — more correct first-line choices, better adherence, no increase in low-value branded volume — would substantially revise the chapter's framing from "a machine optimizing branded volume with no funded counterweight" to "a contested channel with at least some pro-patient evidence." Conversely, if the POCMA growth figures fail verification and the channel turns out to be a small, slow-growing slice of spend, the "fastest-growing" half of the headline finding should be dropped entirely.

## Still puzzling

- If the same plumbing could deliver comparative-effectiveness and cost data at the point of care, what *exact* funding or policy mechanism would make a counter-stack viable — and why has no payer, who would directly benefit, built one?
- Does real-time clinical-context triggering legally cross into "PHI used for marketing"? The platforms say no; no independent court has said yes; the question is genuinely open (and seeds Chapter 3's privacy material).
- The Part D gifts study shows an association, not causation. How much of the prescribing difference is the gift changing behavior, versus industry targeting physicians who were already inclined to prescribe branded? (This is the propensity-versus-incrementality puzzle that Chapter 8 is built to resolve.)

## Chapter summary

You can now describe the HCP marketing stack end to end — identity graph, programmatic point-of-care impression, attribution loop — and you can name its defining anomaly: the payer is not at the table, so the price discipline of ordinary markets is absent. You can trace a brand objective down to a single named prescriber via the NPI, and you can explain how commercial messages ride the clinical interoperability standards (CDS Hooks, SMART on FHIR) into the same visual layer as safety alerts. You can describe the lost price signal that co-pay cards create and hold the nuanced, evidence-based view of it. And you can do the one thing that distinguishes a Fellow from an audience: separate a vendor's true mechanism claims from its unproven effectiveness claims, and say precisely what evidence the latter would require.

## Key terms

- **NPI (National Provider Identifier):** a permanent, unique 10-digit number for every US provider; the deterministic identity primitive of HCP targeting.
- **HCP identity graph:** the persistent, cross-channel profile keyed to each NPI (built in detail in Chapter 3).
- **CDS Hooks:** an HL7 event-driven standard that fires "cards" into the EHR on clinical workflow events; built for safety alerts, repurposed for ads.
- **SMART on FHIR:** an open standard letting an approved app launch inside the EHR and receive patient/encounter context; the other rail commercial messages ride.
- **Principal–agent problem (split agency):** the structural situation where the physician decides, the patient consumes, the payer pays, and the institution constrains — breaking consumer sovereignty.
- **Co-pay card:** a manufacturer coupon lowering the patient's out-of-pocket cost, which erases the price signal that would steer toward a generic.
- **Attribution circularity:** the structural problem that the platform serving the ad also measures the "lift" it claims (developed in Chapter 5).
- **Point-of-care (POC) marketing:** branded messaging delivered inside the clinical workflow at or near the moment of prescribing.

## Bridge question

The stack optimizes *something* — but is it incremental prescribing (**lift**) or durable physician belief (**brand**)? Chapter 2 splits the two dependent variables that everything in this book routes through.

## Further reading

- **Dafny, Ody & Schmitt, "When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization"** (NBER w29735; *AEJ: Policy*). The cleanest causal evidence in the chapter; read it for the quasi-experimental design (commercial vs. Medicare Advantage, where coupons are banned) as much as for the findings.
- **CDS Hooks specification** (cds-hooks.org; HL7 CDS Hooks 2.0). The primary source for the mechanism — read the hook-type definitions and notice that every commercial trigger point was designed for clinical safety.
- **SMART App Launch v2.2.0** (HL7, build.fhir.org/ig/HL7/smart-app-launch). The other rail; read the launch-context section to understand exactly what patient/encounter data an embedded app receives.
- **"Principal-agent problems in health care"** (*Health Policy and Planning*, Oxford Academic, 2011). The economic framing for the structural anomaly; short and foundational.
- **Sorrell v. IMS Health (2011)** — read the holding now and in full in Chapter 3. It is the legal reason the targeting infrastructure is secure: prescriber data-mining is constitutionally protected commercial speech.
