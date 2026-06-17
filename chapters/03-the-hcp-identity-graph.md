# Chapter 3 — The HCP Identity Graph and the Targeting Data
*How a prescription written in a pharmacy becomes a bid at the moment a physician opens a browser.*

Here is a fact that stops most people cold the first time they meet it. The American Medical Association maintains a file — the **AMA Physician Masterfile** — that holds a record for very nearly every physician in the United States, member or not, assembled from the moment each one enters medical school. Name. Address. Specialty. Education. Historically, the DEA license number. Over a million physicians. And the AMA licenses this file, for revenue, to commercial data-mining firms.

Sit with that for a moment, because the surprising part is not the existence of the file. Directory services have always existed. The surprising part is what happens when that file meets the pharmacy.

---

There is a legal fact the entire HCP targeting industry rests on, and it is worth stating precisely before anything else, because once you have it, the rest of the chapter assembles itself.

HIPAA defines **Protected Health Information** as data that identifies — or could identify — a patient. The law's protections attach to PHI. Strip PHI out, and the data reverts to ordinary commercial information, buyable and sellable like any other dataset. HIPAA provides two routes to do this.

The first is **Safe Harbor**: remove 18 specified identifiers and the data is deemed de-identified by rule. The list reads like a privacy auditor's checklist — names, geographic subdivisions smaller than a state (with a carve-out for 3-digit ZIP codes covering 20,000-plus people), all date elements finer than year, phone numbers, Social Security numbers, medical-record numbers, account numbers, certificate and license numbers, device identifiers, IP addresses, biometric identifiers, full-face photographs, and any other unique code. Strip all 18, and the data is legally de-identified. No PHI. No HIPAA.

The second route is **Expert Determination**: a qualified statistician certifies that the re-identification risk is "very small," which permits retaining *more* detail — month-level dates, finer geography — that Safe Harbor would have required dropping. Better for longitudinal analysis. Claims aggregators often use it precisely because that granularity is what makes the data valuable for machine learning.

Now trace a single statin prescription through this machine. A patient fills a script at CVS. The claim flows to the payer, who strips the patient's identifiers under Safe Harbor — name gone, date-of-birth gone, address gone. What remains is: a de-identified patient record, a drug, a quantity, a date-resolved-to-year, and — here is the pivot — a **National Provider Identifier**. The NPI is a 10-digit number assigned by CMS to every prescribing physician in the country. It is not a patient identifier. It is not on the Safe Harbor list. It stays.

The result is not anonymous data. It is data that is anonymous with respect to the *patient* and fully identified with respect to the *physician*. The output of that de-identification step is: "NPI 1234567890 wrote 47 statin scripts last month." The patient is gone. The doctor is named — numerically, but named.

<!-- → [DIAGRAM: Two-column pipeline diagram — left column shows patient data being stripped at the payer step (fields crossed out: name, DOB, address); right column shows NPI persisting through every subsequent step — broker, pharma buyer, model, bid. Caption: "De-identification removes the patient and leaves the prescriber. This asymmetry is the legal foundation of NCP targeting."] -->

---

That number — NPI 1234567890 — is commercially useless on its own. You know what it prescribes. You do not know who it is. This is where the AMA Physician Masterfile enters, and where the mechanism of the entire industry becomes clear.

Data-mining firms license the Masterfile. They then perform a join: the de-identified prescribing records on one side, the Masterfile on the other, linked on physician identity (NPI, historically also DEA number). The output of that join is **prescriber-level data** — "Dr. Jane Smith at Mass General, who wrote 47 statin scripts last month and switched three patients off your competitor in Q3." That is the product. That is what pharmaceutical companies buy.

The firm that built this model at scale was IMS Health. The arrangement was simple enough: buy pharmacy Rx records from chains and pharmacies, license the AMA Masterfile, join the two, sell the result. IQVIA — IMS's successor after a series of mergers — now holds what it describes as roughly 90% of US retail pharmacy dispensing in its Longitudinal Access and Adjudication Data product, refreshed monthly, and more than 11 million HCP profiles in its OneKey directory. [verify — these are IQVIA self-descriptions; confirm current figures before citing as external validation.] Symphony Health (now under ICON) competes, with particular strength in specialty pharmacy. Definitive Healthcare supplies HCP affiliation and procedural data used to construct audience segments. Three names, essentially, for the layer that turns pharmacy claims into a targetable physician universe.

The misconception worth dissolving here: pharma does not see patient records. Not even aggregate patient records with names stripped. What pharma buys is NPI-keyed prescribing behavior — each physician, by drug and class, by volume, by switching pattern, by month. The patient is not present in the transaction at any point. The physician was always the unit of analysis, and the entire infrastructure was built to describe the physician precisely.

---

Now we can open the model that decides which physician gets a promotional impression, because the identity resolution is not the end of the pipeline — it is the input to the next step.

A **physician propensity model** predicts how likely a given NPI is to prescribe a drug in the next measurement period. Feed it enough prescribing history and you get a ranked list: highest-propensity physicians at the top, lowest at the bottom, with a targeting threshold somewhere in the middle. The question worth asking — and the one the industry rarely asks openly — is *what is actually in that model's feature vector.*

Four kinds of signal appear:

**Claims-derived features:** script volume by class, switching patterns (from competitor to brand, from brand to generic), restart rates, refill behavior, patient-mix proxies, loyalty decile. These come from the LAAD-style data.

**Identity and affiliation features:** specialty, practice setting, geography, health-system membership. These come from the Masterfile and databases like Definitive Healthcare.

**Behavioral and digital features:** journal-article reads, CME completions, endemic-platform visits (Medscape, WebMD), email open rates, search behavior. These come from digital engagement tracking.

**CMS Open Payments history:** every publicly disclosed industry payment — meals, speaker fees, consulting payments — made to this physician, drawn from the Sunshine Act database.

The first three feel intuitive. The fourth is where the chapter's central idea lives.

Open Payments data encodes not *what patients need* but *how receptive this physician has been to industry contact.* A physician who has accepted many industry meals and speaking invitations has a different Open Payments history than one who has declined all of them. If that history is a feature in the propensity model, the model is not purely predicting clinical appropriateness — it is partly predicting *targetability*, the likelihood that this physician will respond to promotional contact.

Make it concrete. Two cardiologists. Identical patient mixes — same age distribution, same comorbidity burden, same proportion of patients likely to benefit from the drug being promoted. But one has a three-year history of industry meals; the other has none. A propensity model with Open Payments as a weighted feature may rank the meal-history physician higher — not because that physician's patients are better candidates, but because that physician has historically been *more moveable by industry contact.*

<!-- → [TABLE: Side-by-side comparison of two hypothetical physicians — Physician A (high Open Payments history, same patient mix) vs. Physician B (no Open Payments history, same patient mix). Columns: specialty, patient mix proxy, Open Payments meals (last 3 years), predicted propensity score. Point: propensity diverges despite identical clinical context.] -->

Whether this actually describes how real propensity models are weighted is, honestly, an open empirical question. Including a feature is not the same as weighting it heavily. But the question is answerable on public data — Open Payments is public, Medicare Part D prescribing is public — and the fact that it has not been systematically examined is itself worth noting. [The susceptibility-proxy construct is the book's position, flagged not asserted — see pantry; it is the seed for the Chapter 13 Track D proxy-discrimination study.]

---

There is a second limit on this whole apparatus, and it operates not at the feature level but at the data layer underneath everything.

Claims data is stale. Not catastrophically — LAAD refreshes monthly — but in a domain where a physician might switch prescribing patterns in response to a conference, a new trial publication, or a single conversation with a colleague, monthly can mean you are targeting against a reality that no longer exists. A physician who was a high-volume prescriber of Brand X in Q1, switched patients off in Q2 after a safety signal, and has been declining since March may still appear near the top of a Q2 targeting list built from Q1 claims.

The effect on measurement compounds this. If the targeting list is built from stale claims, and the attribution model is measuring change in claims after targeting, then the lag in both the input signal and the outcome signal means any measured "lift" — the increase in prescribing attributed to the campaign — is partly an artifact of claims-processing timing. A physician already trending upward before the campaign looks like a responder. A physician already trending down looks like a non-responder. Neither assignment reflects what the campaign actually did. (This is the chapter's first clean handoff to the attribution problems of Chapter 8.)

The industry's frontier response to claims lag is **dynamic NPI activation**: ingesting real-time clinical signals — EHR-derived, from platforms like OptimizeRx's DAAP — to identify physicians at the moment of actual clinical relevance rather than on a monthly refresh cycle. Instead of "this physician was a high-volume prescriber last month," the trigger becomes "this physician just opened a chart for a patient with the eligible diagnosis." That is a meaningfully different signal. It is also, as Chapter 1 discussed, the point where the question of whether PHI is leaving the EHR becomes live again.

<!-- → [DIAGRAM: Timeline diagram showing claims-data lag: prescription written (Day 0) → pharmacy adjudication (Day 1-3) → payer processing (Day 7-14) → broker aggregation (Day 14-30) → model refresh (monthly) → targeting list deployed. Contrast with a parallel "real-time EHR trigger" track showing Day 0 → bid. Caption: "The gap between event and targeting signal is where targeting error lives."] -->

---

The identity graph does not sit dormant between targeting campaigns. It is continuously activated across every channel through which a pharmaceutical company reaches physicians, and the same NPI profile drives all of them simultaneously.

CRM systems — Veeva, IQVIA OCE+, Salesforce Life Sciences Cloud — surface next-best-action recommendations to sales representatives. Endemic media platforms — Medscape, WebMD, specialty journals — serve targeted display advertising inside environments physicians associate with clinical information. EHR-integrated platforms fire promotions at the moment of clinical decision, triggered by diagnosis codes and prescribing context. The coordination of all three is what vendors call **omnichannel orchestration**: one physician, across every touchpoint, from a unified profile.

The feature worth understanding here is not the sophistication of any individual channel but the feedback structure of the system as a whole. Every engagement signal — whether a rep's call got answered, whether a Medscape banner got clicked, whether an EHR prompt was dismissed — flows back into the profile. The propensity model that targets Dr. Martinez today is partly built from how Dr. Martinez responded to being targeted last month. This is not a static dataset that gets queried. It is a continuously updating portrait, enriched by its own use.

<!-- → [DIAGRAM: Circular feedback loop — NPI profile at center, with spokes to: CRM (rep call logs), endemic media (click data), EHR triggers (prompt responses). Each spoke has a return arrow labeled "engagement signal → model feature update." Caption: "The graph is enriched by targeting. Each campaign refines the model that drives the next one."] -->

A worked instance: Dr. Martinez switched three patients off Brand X last quarter (a claims signal). Brand Y digital engagement is trending upward for her specialty (a behavioral signal). Her calendar shows an opening Tuesday at 2 p.m. (a CRM scheduling signal). The system surfaces a next-best-action recommendation to the rep: call Tuesday, focus on the switch narrative. Three signal types, one profile, one activation decision.

---

The legal structure holding all of this in place was tested and confirmed by the Supreme Court in 2011. Vermont passed the Prescription Confidentiality Law in 2007, which barred selling or using prescriber-identified data for marketing without the physician's consent. It was a direct attempt to restrict the machinery this chapter describes. IMS Health challenged it. The Supreme Court struck the law down in *Sorrell v. IMS Health* as a violation of the First Amendment: data-mining of prescriber-identified data is constitutionally protected commercial speech.

This is worth sitting with, because it forecloses a response that otherwise seems obvious. The targeting infrastructure is not a gray area waiting for legislative correction. States cannot simply pass laws restricting prescriber data-mining; the Court has already said they cannot, on free-speech grounds. The legal foundation is not a loophole or an oversight. It was examined, challenged, and upheld at the highest level. A new federal privacy statute covering de-identified health data, or a successful narrowing of *Sorrell*, would change this picture — but neither exists as of this writing.

The AMA's role in this structure earned it real money. In 2004, database products generated approximately $40.4 million in revenue, roughly 15% of the AMA's consolidated total. [verify — 2004 figure from secondary reporting; flag as historical; confirm any current figure before stating it.] The AMA also operates a Physician Data Restriction Program that lets physicians opt out of *sales-rep access* to their prescribing data — but the program limits rep visibility, not the underlying data licensing. The prescribing data continues to flow.

---

What this chapter has built is a complete causal chain from a single prescription to a bid-time targeting decision. Every link in that chain is legal, disclosed in some form, and commercially mature. The patient's privacy is formally protected at the de-identification step. The physician's privacy was litigated to the Supreme Court and found not to be protected, at least from commercial data-mining.

The gap between how completely the system knows a physician and how little the physician knows about the system is not a malfunction. It is a design feature of a decades-old commercial infrastructure that has been optimized, legally insulated, and technically refined across multiple generations of data technology.

What the system does not know — what it cannot know without being asked and then checked — is whether it is targeting physicians because their patients will benefit or because the physicians are moveable. The propensity model optimizes for predicted prescribing. Whether predicted prescribing tracks patient need or tracks susceptibility to influence is a question the model itself cannot answer. It is the question Chapter 13 will test on public data.

**Five-part AI exercise block**

**When to use AI.** Use an LLM to summarize the 18 HIPAA Safe Harbor identifiers, to draft a first-pass classification of feature-vector components, or to explain the *Sorrell* holding in plain language. These are well-documented facts the model can retrieve and structure, and you can verify them against the cited primary sources.

**When NOT to use AI.** Do not use an LLM to adjudicate whether a specific data flow is HIPAA-compliant, whether a model is unlawfully discriminatory, or whether a given de-identification scheme has acceptable re-identification risk. These are legal and statistical judgments that require counsel and a privacy expert; a fluent model answer here can produce false legal confidence.

**LLM exercise (copy-paste prompt):**
> "Here is the feature list for a physician propensity model: [PASTE LIST]. Classify each feature as (a) clinical-need / patient-eligibility, (b) behavioral / neutral-to-targeting, or (c) susceptibility-to-influence proxy. For each, give a one-sentence justification and a confidence level (high/medium/low). Then list which features, if heavily weighted, would make this model select physicians for *targetability* rather than *patient need*. Do not assert that the model is discriminatory — only identify which features raise the question."

**CLI exercise.** Download a slice of the public CMS Open Payments dataset and a slice of Medicare Part D Prescriber data from the command line. For a single specialty in one state, count physicians who appear in Open Payments versus those who do not, and compute each group's average claims for one branded drug. Write one sentence on what this *association* does and does not show — recall that it cannot establish that payments caused the prescribing.

**AI Validation exercise.** Ask an LLM "is prescriber-level data-mining legal in the US, and why?" Check its answer against the chapter: did it cite *Sorrell v. IMS Health* and the First Amendment / commercial-speech holding, or did it vaguely say "it depends" or invent a statute? Write one sentence correcting any hallucinated citation, and note that this is exactly the kind of legal claim you must verify against the primary source rather than trust.

## AI Use Disclosure

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to draft the feature-vector classification and summarize the HIPAA identifiers; I decided myself which features are genuine susceptibility proxies and flagged that the model's actual discrimination is an open empirical question, because the AI was willing to assert a fairness verdict the public data does not yet support."*

## What Would Change My Mind

The central claims of this chapter are that the targeting infrastructure is legally secure — via de-identification, the AMA Masterfile join, and *Sorrell* — and that propensity feature vectors plausibly encode susceptibility-to-influence rather than pure clinical need. A change in law or precedent — a successful narrowing of *Sorrell*, a new federal privacy statute covering de-identified health data, or an enforcement action treating EHR clinical-context triggers as PHI-in-marketing — would revise the "legally secure" claim. On the susceptibility question, a rigorous public-data study showing that propensity-driven targeting tracks patient-mix and clinical eligibility and is uncorrelated with Open Payments history after controlling for need would substantially weaken the susceptibility-proxy concern and move it from "open question worth testing" toward "probably not the dominant signal."

## Still Puzzling

- Does PHI ever actually leave the EHR in a real-time clinical-context trigger, or do the platforms' assurances hold under independent technical audit? No current, independent analysis of the exact trigger-to-ad-server data flow exists.
- How large is the real re-identification risk for the richest longitudinal de-identified claims — and at what point does "very small" stop being an acceptable standard for data that names every physician and follows millions of patients for years?
- If a propensity model does select for susceptibility, is that a fairness problem to physicians, a welfare problem to patients, or both — and who would have standing to object, given that no one in the data chain holds identifiable patient data and the physician's data-mining is constitutionally protected?

---

## Exercises

**Warm-up**

1. *(Recall — low difficulty) What this tests: whether you can name the legal mechanism that permits commercial use of prescribing data.* State the two HIPAA de-identification routes in your own words. For each, give one reason a claims aggregator might prefer it over the other.

2. *(Recall — low difficulty) What this tests: whether you can trace the identity-resolution step.* In two sentences, explain why de-identified pharmacy claims alone cannot support physician-level targeting, and what the AMA Physician Masterfile join adds.

3. *(Recall — low difficulty) What this tests: whether you can identify the legal keystone.* What did the Supreme Court hold in *Sorrell v. IMS Health* (2011), and what does that holding foreclose that might otherwise seem like an obvious legislative remedy?

**Application**

4. *(Apply — medium difficulty) What this tests: feature classification under the clinical-need vs. susceptibility-to-influence framework.* You are handed a propensity model's feature list: specialty, monthly script volume in-class, switch-from-competitor rate, number of industry meals in the last 12 months (Open Payments), email open rate to brand communications, patient-mix proxy for the eligible condition, loyalty decile. Classify each feature as clinical-need/eligibility, behavioral/neutral, or susceptibility-to-influence proxy. For each, justify your classification in one sentence and indicate your confidence level.

5. *(Apply — medium difficulty) What this tests: reasoning about claims lag as a source of targeting error.* A campaign targeting list is built in June from April claims data. A physician who was a high-volume prescriber in Q1 switched patients off the brand in May after a safety communication. Explain in concrete terms: (a) why this physician may still appear near the top of the June targeting list, and (b) how the same lag would affect measured "lift" if the attribution model compares July claims to the April baseline.

6. *(Apply — medium difficulty) What this tests: understanding the feedback structure of the identity graph.* Describe in three or four sentences how a physician's response to being targeted — answering or declining a rep call, clicking or ignoring a Medscape banner — flows back into the propensity model and affects future targeting. Why does this feedback structure make the graph a different kind of object than a static database?

**Synthesis**

7. *(Synthesis — high difficulty) What this tests: integrating the legal, commercial, and ethical layers.* Write a one-page memo to a compliance officer explaining why the NPI-level targeting pipeline is legally secure, which elements of it are most likely to attract future regulatory scrutiny, and what a physician who objected to being targeted could and could not do about it under current law. Cite *Sorrell* and the HIPAA de-identification framework in your answer.

8. *(Synthesis — high difficulty) What this tests: connecting targeting bias to attribution error.* Explain why a propensity model that weights susceptibility-to-influence features (Open Payments history, email engagement) would systematically distort the attribution metrics used to evaluate campaign performance. What kind of physician population would appear to "respond" to the campaign, and what would that response actually measure?

**Challenge**

9. *(Challenge — open-ended) What this tests: designing a public-data audit.* Using only CMS Open Payments data and Medicare Part D prescribing data (both publicly available), design a study that would test whether propensity-driven targeting correlates with physician susceptibility to industry contact after controlling for patient mix and specialty. State your hypothesis, your independent and dependent variables, your proposed control variables, and one major confound you cannot eliminate with this data.
