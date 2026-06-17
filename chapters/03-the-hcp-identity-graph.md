# Chapter 3 — The HCP Identity Graph and the Targeting Data

## Chapter overview

By the end of this chapter you will be able to trace, step by step, how a prescription written in a pharmacy becomes a targetable signal attached to a named physician — and to do it precisely enough to find where the data is biased. You will understand the one legal fact the entire targeting industry rests on (de-identified health data is no longer protected), the data brokers who aggregate prescribing behavior, the single licensing arrangement that bridges anonymous prescribing patterns to real physician identities, and the Supreme Court case that makes the whole structure constitutionally secure. You will be able to open up a physician propensity model's feature vector and classify what is inside it — clinical-need signal, susceptibility-to-influence signal, or neutral — and you will be able to name the data-lag and identity-error problems that bias both targeting *and* the attribution that claims it worked.

## Learning objectives

By the end of this chapter you should be able to:

1. **(Apply)** Trace the pipeline: pharmacy claims → HIPAA de-identification → NPI identity resolution → bid-time decision.
2. **(Analyze)** Identify the components of a physician propensity model's feature vector and assess each for appropriateness.
3. **(Evaluate)** Assess data lag and identity-resolution error as sources of targeting and measurement bias.

## Opening case — the phone book that names the prescriber

Here is a fact that surprises almost everyone the first time they meet it. The American Medical Association maintains a file — the **AMA Physician Masterfile** — that contains a record for very nearly every physician in the United States, member or not, built from the moment each one enters medical school. Name, address, education, specialty, and historically the physician's DEA license number, for more than a million physicians. And the AMA *licenses* this file, for revenue, to commercial data-mining firms.

On its own, that is just a directory. The opening case is what happens when it meets the prescribing data. De-identified pharmacy claims can tell you *what NPI 1234567890 prescribes* — but not *who* that is. The Masterfile is the bridge: license it, join it to purchased prescribing records on physician identity, and an anonymous prescribing pattern becomes "Dr. Jane Smith at Mass General, who wrote 47 statin scripts last month and switched three patients off your competitor." That join — pharmacy records plus the AMA Masterfile — *is* the foundation of NPI-level targeting.

The failure to sit with is not that this is illegal. It is neither a loophole nor a hack; it is the open, legal, commercial backbone of an entire industry — and it is, as one observer put it, "barely understood by the physicians being targeted." The doctor in the opening case has no idea that her prescribing is a licensed, joined, and bid-upon data product. That gap between how completely the system knows her and how little she knows the system is the chapter's real subject.

## Core concept 1 — HIPAA de-identification: the legal fact everything rests on

The entire targeting industry rests on one legal proposition: **de-identified health data is no longer Protected Health Information (PHI), and can be used and sold commercially.** Get the data out from under HIPAA, and the ordinary rules fall away. HIPAA provides two routes to do that.

**Safe Harbor** is the rule-based route: remove **18 specified identifiers** and the data is deemed de-identified. The list is worth knowing because its gaps are revealing — it strips names; all geographic subdivisions smaller than a state *except* 3-digit ZIP codes for areas of 20,000-plus people; all date elements finer than year for dates tied to an individual; phone, fax, and email; Social Security, medical-record, health-plan, and account numbers; certificate and license numbers; vehicle and device identifiers; URLs; IP addresses; biometric identifiers; full-face photos; and any other unique identifying code. It is simple, cheap, and conservative — and it strips a lot of detail that machine learning would want.

**Expert Determination** is the risk-based route: a qualified statistician certifies that the re-identification risk is "very small," which permits *retaining more detail* — month-level dates, finer geography — that Safe Harbor would have removed. This is better for ML and research, and claims aggregators often use it to preserve longitudinal granularity.

The misconception to dismantle: "de-identified means anonymous forever." It does not. Re-identification risk is real, especially with rich longitudinal data; Safe Harbor is a rule, not a guarantee, and Expert Determination is explicitly a *risk* judgment — "very small," not "zero." (Re-identification risk for rich de-identified claims is an active privacy-research area, not a settled question — flag it; do not claim de-identification is fully privacy-protective.) [contested — see pantry]

But here is the asymmetry that makes the whole chapter work. Trace one statin claim through the pipeline: the patient's identifiers are stripped under Safe Harbor — the *patient* is gone. But the prescriber's NPI is **not a patient identifier**, so it remains. The result: "NPI 1234567890 wrote 47 statin scripts last month" is *de-identified with respect to the patient and fully identified with respect to the physician.* Nobody in the chain — patient → payer (strips identifiers) → broker (licenses) → pharma (buys) — holds identifiable *patient* data. And nobody needs to. The physician was always the target (HHS HIPAA de-identification guidance; the 18-identifier list per HHS and secondary summaries such as Censinet and the USC IFS guide).

## Core concept 2 — The claims layer: IQVIA, Symphony, Definitive Healthcare

De-identified-patient prescribing data is sold by data brokers who aggregate it across payers and pharmacies. Three names dominate.

- **IQVIA LAAD** (Longitudinal Access and Adjudication Data) is the dominant dataset — roughly 90% of US retail pharmacy dispensing, refreshed monthly. IQVIA's OneKey directory holds 11-million-plus HCP profiles. This is the infrastructure underneath most HCP targeting. [verify the ~90% and 11M figures as current IQVIA self-descriptions]
- **Symphony Health** (now under ICON) is the major alternative, with particular strength in specialty pharmacy and distribution data.
- **Definitive Healthcare** supplies HCP demographic, affiliation, and procedural data used to construct audiences.

The misconception: "pharma sees individual patient records." No. They buy *aggregated, de-identified-patient* prescribing data, keyed to the prescriber's NPI. The patient is invisible; the physician is the unit of analysis. A propensity model trained on LAAD-style data learns from each NPI's monthly script volume by drug and class, switch and restart patterns, patient-mix proxies, and refill behavior — never from a named patient (claims-layer detail from `pharma-ai-hcp-marketing-synthesis.md` §3).

## Core concept 3 — The AMA Physician Masterfile and the identity bridge

Now we return to the opening case and make it formal, because this is the mechanism the whole chapter pivots on.

De-identified claims tell you *what* NPI X prescribes. The **AMA Physician Masterfile** tells you *who* NPI X is — name, address, education, specialty, historically DEA number — for over a million US physicians, built from medical-school entry onward and covering nearly every physician whether or not they are an AMA member. The AMA *licenses* this file to data-mining firms (historically IMS Health, Verispan, Dendrite), who **link physician identity to purchased pharmacy prescribing records** to create prescriber-level data (PLD), which is sold to drug makers. That linkage is the foundation of NPI-level targeting. The canonical model is IMS Health's: buy pharmacy Rx records, license the AMA Masterfile, join the two on physician identity (now the NPI/DEA), and sell the result (Medscape; *amednews* reporting on AMA data licensing; the AMA Physician Masterfile entry on Wikipedia).

The misconception: "there must be a loophole, or it must be illegal." Neither. It is the open, commercial, legal backbone of the industry — and it earns the AMA real money. In 2004, the AMA took in **$40.4 million from database products, roughly 15% of its consolidated revenue.** [verify — this is a 2004 figure from secondary reporting; flag as historical and confirm any current figure before stating it. The *mechanism* — AMA licenses the Masterfile to data-miners — remains current; the dollar amounts are dated.] (The AMA also runs a Physician Data Restriction Program, PDRP, that lets a physician opt out of *rep access* to their prescribing data — but note that it limits rep visibility, not the underlying data licensing.)

And the legal keystone: **Sorrell v. IMS Health (2011).** Vermont's 2007 Prescription Confidentiality Law barred selling or using prescriber-identified data for marketing without the physician's consent. The Supreme Court struck it down as a First Amendment violation: **data-mining of prescriber-identified data is constitutionally protected commercial speech.** This is *why* the targeting infrastructure is legally secure and why states cannot easily restrict it. Cite Sorrell whenever someone assumes a state could simply ban this; the Court has already said it cannot, on free-speech grounds.

(One field to flag rather than assert: the Masterfile historically included the DEA number, but AMA data products and their licensed fields may have changed. Verify current licensing terms before stating present-day practice.) [verify]

## Core concept 4 — The propensity feature vector (including Open Payments) and claims lag

We can now open the hood on the model that decides which physician gets targeted. A physician **propensity model** predicts how likely a given NPI is to prescribe — and its feature vector typically combines four kinds of signal:

- **Claims-derived:** script volume by class, switch and restart patterns, patient-mix proxies, refill behavior, loyalty decile.
- **Identity / affiliation:** specialty, practice setting, geography, health-system membership.
- **Behavioral / digital:** journal reads, CME (continuing medical education) completions, endemic-platform visits, email engagement, search.
- **CMS Open Payments history:** publicly disclosed industry payments and meals to the physician, from the Sunshine Act.

That last component is where the chapter's hardest idea lives. The misconception is the comfortable one: "propensity equals clinical need." It does not. A propensity model predicts *who will prescribe*, which **conflates clinical need with susceptibility to influence and with historical prescribing bias.** Open Payments as a feature is double-edged: it encodes a physician's *receptivity to industry* — a susceptibility proxy — not patient need.

Make it concrete. Two cardiologists have identical patient mixes. One has a long Open Payments meal history; the other has none. A propensity model may rank the meal-history physician higher — not because that physician's *patients* need the drug more, but because that physician is more *targetable*. Including Open Payments risks reinforcing influence-susceptibility as a targeting criterion. (There is independent evidence that industry payments are *associated* with costlier prescribing — see PMC5880069, linking Open Payments and Part D — but, as always, association is not causation, and it does not tell us the model is *intentionally* selecting for susceptibility.)

This is the chapter's flagged research finding, and the book's rule here is strict: **flag, don't assert.** Whether propensity feature vectors encode proxies for physician *susceptibility* rather than clinical need is **unexamined and answerable with public data** — a fairness and accountability question, not a settled claim. [the susceptibility-proxy construct is the book's position, flagged not asserted — see pantry; it is the seed for the Chapter 13 Track D proxy-discrimination study.] The general failure pattern — opaque scoring systems that entrench historical bias while acting on people who cannot inspect them — is the subject of *Weapons of Math Destruction*, and the proxy-objective framing (a model optimizing a stand-in for the goal rather than the goal itself) is the subject of *The Alignment Problem*; both are scaffolding for this question, not pharma-specific evidence for it.

The second limit on this whole apparatus is **claims lag.** Claims data arrives with a notable delay — historically, target lists refreshed only a few times a year — so any "static" propensity model is always somewhat stale. (Garbage-in reasoning applies: a model fed months-old prescribing reality cannot be more current than its inputs.) The frontier response is *dynamic NPI activation*, ingesting real-time clinical signals (OptimizeRx's DAAP) to reduce dependence on lagged claims (feature-vector and claims-lag detail from `pharma-ai-hcp-marketing-synthesis.md` §1, §3).

## Core concept 5 — Where the graph gets activated: CRM, endemic media, EHR triggers

The identity graph is not inert data sitting in a warehouse; it is continuously *activated* across channels, and the same NPI profile drives all of them:

- **CRM** systems (Veeva, IQVIA OCE+, Salesforce Life Sciences Cloud) feed sales reps next-best-action recommendations.
- **Endemic media** (Medscape / WebMD, medical journals) target by NPI inside trusted clinical environments.
- **EHR triggers** (CDS Hooks / SMART on FHIR, from Chapter 1) fire on real-time clinical events.

**Omnichannel orchestration** coordinates these so one physician is not blitzed incoherently across all three at once. The misconception is to imagine "the data" and "the targeting" as separate steps. They are one loop: the graph is continuously refreshed by engagement signals fed *back* from every channel — CRM call logs, click data, EHR-trigger responses — and those signals become new features. The graph that targets Dr. Martinez today is built partly from how Dr. Martinez responded to being targeted yesterday.

A worked instance: Dr. Martinez switched three patients off Brand X (a claims signal) + Brand Y digital engagement is trending up (a behavioral signal) + she has an open Tuesday at 2 p.m. (a calendar signal) → the CRM surfaces a next-best-action call recommendation to the rep. Three signal types, one profile, one activation (synthesis §3, §7).

## Worked example — classifying a feature vector

**Situation.** You are handed the feature list for a physician propensity model and asked to assess whether the model is targeting *clinical need* or *susceptibility to influence*. The features: (1) specialty, (2) monthly script volume in-class, (3) switch-from-competitor rate, (4) number of industry meals in the last 12 months (Open Payments), (5) email open rate to brand communications, (6) patient-mix proxy for the eligible condition, (7) loyalty decile.

**Analytical process (including the dead ends).**

First instinct: call any feature about prescribing "clinical-need" and any feature about engagement "susceptibility." Dead end — script volume (feature 2) is *behavioral*, not need; a high-volume prescriber may be high-volume because of habit, not because their patients are sicker. The clinical/behavioral line does not fall where it first appears to.

Second pass: classify each feature against the question "does this measure what the *patient* needs, or how *targetable the physician* is?"
- Specialty (1) and patient-mix proxy (6): closest to **clinical need / eligibility** — they describe the population the physician sees.
- Script volume (2), switch rate (3), loyalty decile (7): **behavioral / neutral-to-targeting** — they describe prescribing behavior, which blends need and habit, and (recall Chapter 2) ranking on these inflates lift estimates.
- Industry meals (4) and email open rate (5): **susceptibility-to-influence proxies** — they measure receptivity to industry, not patient need.

Third step: notice the consequence. If features 4 and 5 carry meaningful weight, the model is partly selecting physicians *because they are influenceable*, and the targeting will concentrate promotion on the most-influenceable physicians regardless of patient benefit — a potential proxy-discrimination failure mode.

**Resolution.** You report that the vector mixes need-proxies (1, 6) with behavioral signals (2, 3, 7) and at least two explicit susceptibility proxies (4, 5), and you flag — without asserting — that the model may be encoding influence-susceptibility. You recommend the publicly-testable check: does the model's targeting correlate with Open Payments history *after* controlling for patient-mix? (A Chapter 13 Track D analysis.)

**The lesson (one sentence).** A propensity feature vector silently encodes *who is influenceable*, not *whose patients need the drug* — and only by classifying each feature can you see it.

**The limit (where it fails).** This classification identifies *suspect* features; it does not *prove* the model discriminates by susceptibility, because feature inclusion is not the same as feature influence, and a feature can be present but down-weighted to near-zero. Proving it requires the actual model weights or a public-data behavioral test — which is exactly why the susceptibility question is flagged as open, not asserted as fact.

## Common misconceptions

**"De-identified means the patient is anonymous, so there's no privacy issue."** Plausible, because the patient's name really is stripped. It fails on two counts: re-identification risk for rich longitudinal data is non-zero (Expert Determination certifies "very small," not "zero"), and — more to the point — the *physician* is fully identified throughout. The opening case works precisely because the prescriber, not the patient, is the unit being named.

**"NPI targeting must be a legal gray area or a loophole."** Plausible, because it feels like it shouldn't be allowed. It fails because the AMA Masterfile licensing is open and commercial and Sorrell v. IMS Health makes prescriber data-mining constitutionally protected speech. There is no loophole to close; the structure is legally secure by design.

**"Propensity equals clinical need — the model targets the doctors whose patients need the drug."** Plausible, because propensity sounds like "appropriateness." It fails because propensity predicts *who will prescribe*, conflating need with habit and with susceptibility to influence; the Open Payments and engagement features in the worked example measure targetability, not patient benefit.

## Evidence check

- **Independent (governmental / peer-reviewed):** HIPAA de-identification rules and the 18-identifier list (HHS); Sorrell v. IMS Health (2011, Supreme Court) — binding precedent; the *association* between Open Payments and costlier prescribing (PMC5880069) — independent but correlational.
- **Vendor-generated:** IQVIA's LAAD "~90% coverage," OneKey "11M+ profiles," "gold-standard" positioning; OptimizeRx DAAP capability claims. Cite as product self-description, not validation.
- **Historical / secondary:** the AMA "$40.4M / ~15% of revenue from database products" figure (2004, secondary reporting) — flagged `[verify]` as historical; the DEA-number-in-Masterfile detail — historically documented, current licensing fields `[verify]`.
- **Hypothetical:** the Dr. Martinez and feature-classification scenarios are illustrative composites.
- **Contested:** **re-identification risk** of rich de-identified claims [contested — see pantry] — an active research area, not settled; whether real-time EHR clinical-context triggers cross into PHI-in-marketing — legally unsettled (overlaps Chapter 1).
- **`[verify]` flags:** IQVIA coverage/profile figures; the AMA revenue figure; current Masterfile licensed fields (incl. DEA).

The flagged research finding: **whether propensity models encode susceptibility proxies (not just clinical need) is unexamined and publicly testable** [the susceptibility-proxy construct is flagged, not asserted]. Present it as the open Chapter 13 Track D question; do not state it as a finding.

## Compliance & patient-welfare check

**Privacy / HIPAA.** This is the most privacy-laden chapter in Act One. The data flow is legally grounded in de-identification, but two things must be flagged to counsel rather than adjudicated here: (1) re-identification risk for rich longitudinal de-identified claims is real and unsettled; (2) whether EHR real-time clinical-context triggers ever cause PHI to leave the EHR is contested — platforms assert it does not, independent analysis of the exact trigger-to-ad-server data flow is limited. Route both to counsel.

**MLR / FDA fair balance.** Targeting and identity resolution are upstream of content, so they do not themselves trigger MLR — but a targeting model that concentrates messaging on the most-influenceable physicians raises a fair-balance question one level up: are the physicians most often shown promotional content the ones least likely to discount it? That is a flag for medical and compliance, not a legal verdict.

**Patient-welfare note.** The welfare risk here is **proxy discrimination**: if propensity features (Open Payments history, historical prescribing) encode susceptibility rather than patient need, the model reinforces existing prescribing bias and may concentrate promotion on the most-influenceable physicians regardless of patient benefit. The welfare question for a Fellow: *does the targeting model select physicians because their patients are likely to benefit, or because the physicians are likely to be moved?* The chapter's honest answer is that we do not yet know — and that the question is answerable on public data, which is the point.

## Exercises

1. **(Apply)** Trace the full pipeline in writing, naming the legal or technical mechanism at each arrow: pharmacy claim → HIPAA de-identification → NPI identity resolution (via the AMA Masterfile join) → bid-time targeting decision. At the de-identification step, state which party strips identifiers and which identifier is *not* stripped, and why that matters.

2. **(Analyze)** Given a list of propensity-model feature components (use the seven from the worked example, or build your own from the chapter), classify each as **clinical-need / eligibility**, **behavioral / neutral**, or **susceptibility-to-influence**, and justify each classification in one sentence. Mark which classifications you are *confident* in and which are genuinely ambiguous.

3. **(Evaluate — produces an artifact)** Write a one-page memo assessing how claims lag and identity-resolution error bias *both* targeting *and* attribution. Be specific: give one concrete example of how a six-month claims lag could make a targeting list wrong, and one example of how the same lag could make a measured "lift" look bigger or smaller than it truly was. This memo is your identity-graph artifact and connects forward to Chapter 8's attribution problems.

## Five-part AI exercise block

**When to use AI.** Use an LLM to summarize the 18 HIPAA Safe Harbor identifiers, to draft a first-pass classification of feature-vector components, or to explain the Sorrell holding in plain language. These are well-documented facts the model can retrieve and structure, and you can check them against the cited primary sources.

**When NOT to use AI.** Do not use an LLM to *adjudicate* whether a specific data flow is HIPAA-compliant, whether a model is unlawfully discriminatory, or whether a given de-identification scheme has acceptable re-identification risk. These are legal and statistical judgments that require counsel and a privacy expert; a fluent model answer here can create false legal confidence.

**LLM exercise (copy-paste prompt):**
> "Here is the feature list for a physician propensity model: [PASTE LIST]. Classify each feature as (a) clinical-need / patient-eligibility, (b) behavioral / neutral-to-targeting, or (c) susceptibility-to-influence proxy. For each, give a one-sentence justification and a confidence level (high/medium/low). Then list which features, if heavily weighted, would make this model select physicians for *targetability* rather than *patient need*. Do not assert that the model is discriminatory — only identify which features raise the question."

**CLI exercise.** Download a slice of the public CMS Open Payments dataset and a slice of Medicare Part D Prescriber data from the command line. For a single specialty in one state, count physicians who appear in Open Payments versus those who do not, and compute each group's average claims for one branded drug. Write one sentence on what this *association* does and does not show (recall: it cannot establish that payments *caused* the prescribing).

**AI Validation exercise.** Ask an LLM "is prescriber-level data-mining legal in the US, and why?" Check its answer against the chapter: did it cite Sorrell v. IMS Health and the First Amendment / commercial-speech holding, or did it vaguely say "it depends" or invent a statute? Write one sentence correcting any hallucinated citation, and note that this is exactly the kind of legal claim you must verify against the primary source rather than trust.

## AI Use Disclosure

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to draft the feature-vector classification and summarize the HIPAA identifiers; I decided myself which features are genuine susceptibility proxies and flagged that the model's actual discrimination is an open empirical question, because the AI was willing to assert a fairness verdict the public data does not yet support."*

## What would change my mind

The central claims of this chapter are that the targeting infrastructure is legally secure (via de-identification, the AMA Masterfile join, and Sorrell) and that propensity feature vectors plausibly encode susceptibility-to-influence rather than pure clinical need. A change in law or precedent — a successful narrowing of Sorrell, a new federal privacy statute covering de-identified health data, or an enforcement action treating EHR clinical-context triggers as PHI-in-marketing — would revise the "legally secure" claim. On the susceptibility question, a rigorous public-data study showing that propensity-driven targeting tracks *patient-mix and clinical eligibility* and is *uncorrelated* with Open Payments history after controlling for need would substantially weaken the susceptibility-proxy concern and move it from "open question worth testing" toward "probably not the dominant signal."

## Still puzzling

- Does PHI ever actually leave the EHR in a real-time clinical-context trigger, or do the platforms' assurances hold under independent technical audit? No current, independent analysis of the exact trigger-to-ad-server data flow exists.
- How large is the real re-identification risk for the richest longitudinal de-identified claims — and at what point does "very small" stop being an acceptable standard for data that names every physician and follows millions of patients for years?
- If a propensity model *does* select for susceptibility, is that a fairness problem to physicians, a welfare problem to patients, or both — and who would have standing to object, given that no one in the data chain holds identifiable patient data and the physician's data-mining is constitutionally protected? (Seeds Chapter 11's accountability framework and Chapter 13 Track D.)

## Chapter summary

You can now trace a prescription from the pharmacy counter to a bid-time targeting decision, naming the legal mechanism at every step: de-identification removes the patient but never the prescriber, the AMA Masterfile join restores the prescriber's identity, and Sorrell v. IMS Health makes the whole structure constitutionally secure. You can name the claims brokers (IQVIA, Symphony, Definitive Healthcare) and the dominant LAAD dataset, and you understand that pharma sees de-identified-patient, NPI-keyed data, never named patients. You can open a propensity model's feature vector and classify its components into clinical-need, behavioral, and susceptibility-to-influence signals — and you can flag, without overclaiming, the open question of whether such models encode susceptibility proxies. And you can explain how claims lag and identity-resolution error bias both targeting and attribution, setting up the causal problems of Chapter 8.

## Key terms

- **De-identification (Safe Harbor / Expert Determination):** the two HIPAA routes to strip data of PHI status; Safe Harbor removes 18 identifiers, Expert Determination certifies "very small" re-identification risk while keeping more detail.
- **NPI identity resolution:** joining de-identified prescribing records to a named physician — the step that makes targeting deterministic.
- **AMA Physician Masterfile:** the AMA's near-complete physician directory, licensed commercially; the bridge from anonymous prescribing patterns to physician identity.
- **Sorrell v. IMS Health (2011):** the Supreme Court ruling that prescriber data-mining is constitutionally protected commercial speech; the legal keystone.
- **Claims data (LAAD):** de-identified-patient, NPI-keyed prescribing data sold by brokers; IQVIA's LAAD is dominant.
- **Propensity model / feature vector:** a model predicting which NPI will prescribe, built from claims, identity, behavioral, and Open Payments signals.
- **Open Payments (Sunshine Act):** public data on industry payments to physicians — both a propensity feature and a Fellow's public-data audit tool.
- **Susceptibility proxy:** a feature that encodes a physician's receptivity to influence rather than patient need; flagged, not asserted, as a possible targeting criterion.
- **Claims lag:** the delay between a prescription and its appearance in claims data, which staleness biases both targeting and attribution.

## Bridge question

Given this substrate — a deterministically identified physician described by a rich, somewhat-stale, possibly-biased feature vector — what does today's AI stack actually *do* on top of it, and how much of what vendors claim is real? Chapter 4 audits the capabilities and the language.

## Further reading

- **Sorrell v. IMS Health, Inc. (2011).** Read the holding in full — it is the legal foundation of the entire targeting industry and the reason states cannot easily restrict prescriber data-mining.
- **HHS, "Guidance Regarding Methods for De-identification of Protected Health Information."** The primary source for Safe Harbor and Expert Determination; read it for what the 18 identifiers do and do not cover, especially the geography and date carve-outs.
- **PMC5880069** (industry payments and costlier prescribing, linking Open Payments and Part D). Read it as the strongest *independent* (but correlational) evidence on the payments–prescribing link; note what it cannot establish.
- **Cathy O'Neil, *Weapons of Math Destruction*.** Scaffolding, not pharma evidence — the canonical account of opaque scoring models that entrench bias while acting on people who cannot inspect them; directly relevant to the susceptibility-proxy question.
- **Brian Christian, *The Alignment Problem*.** Scaffolding for the proxy-objective framing — why optimizing a stand-in (predicted prescribing) for the real goal (patient benefit) can quietly drift from what we actually want; supports the "model optimizes targetability, not patient need" argument.
