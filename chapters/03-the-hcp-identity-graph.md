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

![Two-column pipeline: patient identifiers struck through at the payer de-identification step while the NPI persists through broker, model and bid.](images/03-the-hcp-identity-graph-fig-01.png)
*Figure 3.1 — De-identification removes the patient and leaves the prescriber*

<!-- → [DIAGRAM: Two-column pipeline diagram — left column shows patient data being stripped at the payer step (fields crossed out: name, DOB, address); right column shows NPI persisting through every subsequent step — broker, pharma buyer, model, bid. Caption: "De-identification removes the patient and leaves the prescriber. This asymmetry is the legal foundation of NCP targeting."] -->

---

That number — NPI 1234567890 — is commercially useless on its own. You know what it prescribes. You do not know who it is. This is where the AMA Physician Masterfile enters, and where the mechanism of the entire industry becomes clear.

Data-mining firms license the Masterfile. They then perform a join: the de-identified prescribing records on one side, the Masterfile on the other, linked on physician identity (NPI, historically also DEA number). The output of that join is **prescriber-level data** — "Dr. Jane Smith at Mass General, who wrote 47 statin scripts last month and switched three patients off your competitor in Q3." That is the product. That is what pharmaceutical companies buy.

The firm that built this model at scale was IMS Health. The arrangement was simple enough: buy pharmacy Rx records from chains and pharmacies, license the AMA Masterfile, join the two, sell the result. IQVIA — IMS's successor after a series of mergers — describes its US prescription datasets as covering roughly 90% or more of US retail pharmacy dispensing, refreshed frequently, and its OneKey reference directory as holding more than 25 million healthcare-professional profiles across 100-plus countries (IQVIA, "OneKey HCP Reference Data," iqvia.com). These are IQVIA self-descriptions; a vendor describing the reach of its own product is not independent validation, and the figures should be read accordingly. Symphony Health (now under ICON) competes, with particular strength in specialty pharmacy. Definitive Healthcare supplies HCP affiliation and procedural data used to construct audience segments. Three names, essentially, for the layer that turns pharmacy claims into a targetable physician universe.

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


| | Physician A | Physician B |
|---|---|---|
| Specialty | Cardiology | Cardiology |
| Patient-mix proxy (eligible for the promoted drug) | Identical — same age distribution, comorbidity burden, share of likely-to-benefit patients | Identical — same age distribution, comorbidity burden, share of likely-to-benefit patients |
| Open Payments meals (last 3 years) | Many — a three-year history of industry meals and speaking invitations | None — has declined all industry contact |
| Predicted propensity score | Higher | Lower |

*Table 3.1 — Identical clinical context, divergent propensity: when Open Payments history is a weighted feature, the model partly predicts targetability — how moveable the physician is — rather than patient need.*


Whether this actually describes how real propensity models are weighted is, honestly, an open empirical question. Including a feature is not the same as weighting it heavily. But the question is answerable on public data — Open Payments is public, Medicare Part D prescribing is public — and the fact that it has not been systematically examined is itself worth noting. [The susceptibility-proxy construct is the book's position, flagged not asserted — see pantry; it is the seed for the Chapter 13 Track D proxy-discrimination study.]

---

There is a second limit on this whole apparatus, and it operates not at the feature level but at the data layer underneath everything.

Claims data is stale. Not catastrophically — LAAD refreshes monthly — but in a domain where a physician might switch prescribing patterns in response to a conference, a new trial publication, or a single conversation with a colleague, monthly can mean you are targeting against a reality that no longer exists. A physician who was a high-volume prescriber of Brand X in Q1, switched patients off in Q2 after a safety signal, and has been declining since March may still appear near the top of a Q2 targeting list built from Q1 claims.

The effect on measurement compounds this. If the targeting list is built from stale claims, and the attribution model is measuring change in claims after targeting, then the lag in both the input signal and the outcome signal means any measured "lift" — the increase in prescribing attributed to the campaign — is partly an artifact of claims-processing timing. A physician already trending upward before the campaign looks like a responder. A physician already trending down looks like a non-responder. Neither assignment reflects what the campaign actually did. (This is the chapter's first clean handoff to the attribution problems of Chapter 8.)

The industry's frontier response to claims lag is **dynamic NPI activation**: ingesting real-time clinical signals — EHR-derived, from platforms like OptimizeRx's DAAP — to identify physicians at the moment of actual clinical relevance rather than on a monthly refresh cycle. Instead of "this physician was a high-volume prescriber last month," the trigger becomes "this physician just opened a chart for a patient with the eligible diagnosis." That is a meaningfully different signal. It is also, as Chapter 1 discussed, the point where the question of whether PHI is leaving the EHR becomes live again.

![Two parallel timelines: a multi-week claims-data lag from prescription to deployed targeting list, contrasted with a same-day real-time EHR trigger that goes straight from chart-open to bid.](images/03-the-hcp-identity-graph-fig-02.png)
*Figure 3.2 — The gap between event and targeting signal is where targeting error lives*

<!-- → [DIAGRAM: Timeline diagram showing claims-data lag: prescription written (Day 0) → pharmacy adjudication (Day 1-3) → payer processing (Day 7-14) → broker aggregation (Day 14-30) → model refresh (monthly) → targeting list deployed. Contrast with a parallel "real-time EHR trigger" track showing Day 0 → bid. Caption: "The gap between event and targeting signal is where targeting error lives."] -->

---

The identity graph does not sit dormant between targeting campaigns. It is continuously activated across every channel through which a pharmaceutical company reaches physicians, and the same NPI profile drives all of them simultaneously.

CRM systems — Veeva, IQVIA OCE+, Salesforce Life Sciences Cloud — surface next-best-action recommendations to sales representatives. Endemic media platforms — Medscape, WebMD, specialty journals — serve targeted display advertising inside environments physicians associate with clinical information. EHR-integrated platforms fire promotions at the moment of clinical decision, triggered by diagnosis codes and prescribing context. The coordination of all three is what vendors call **omnichannel orchestration**: one physician, across every touchpoint, from a unified profile.

The feature worth understanding here is not the sophistication of any individual channel but the feedback structure of the system as a whole. Every engagement signal — whether a rep's call got answered, whether a Medscape banner got clicked, whether an EHR prompt was dismissed — flows back into the profile. The propensity model that targets Dr. Martinez today is partly built from how Dr. Martinez responded to being targeted last month. This is not a static dataset that gets queried. It is a continuously updating portrait, enriched by its own use.

![A circular feedback loop with an NPI profile at the center and spokes to CRM rep-call logs, endemic-media click data and EHR prompt responses, each returning an engagement signal that updates the model.](images/03-the-hcp-identity-graph-fig-03.png)
*Figure 3.3 — The graph is enriched by targeting; each campaign refines the next*

<!-- → [DIAGRAM: Circular feedback loop — NPI profile at center, with spokes to: CRM (rep call logs), endemic media (click data), EHR triggers (prompt responses). Each spoke has a return arrow labeled "engagement signal → model feature update." Caption: "The graph is enriched by targeting. Each campaign refines the model that drives the next one."] -->

A worked instance: Dr. Martinez switched three patients off Brand X last quarter (a claims signal). Brand Y digital engagement is trending upward for her specialty (a behavioral signal). Her calendar shows an opening Tuesday at 2 p.m. (a CRM scheduling signal). The system surfaces a next-best-action recommendation to the rep: call Tuesday, focus on the switch narrative. Three signal types, one profile, one activation decision.

---

The legal structure holding all of this in place was tested and confirmed by the Supreme Court in 2011. Vermont passed the Prescription Confidentiality Law in 2007, which barred selling or using prescriber-identified data for marketing without the physician's consent. It was a direct attempt to restrict the machinery this chapter describes. IMS Health challenged it. The Supreme Court struck the law down in *Sorrell v. IMS Health* as a violation of the First Amendment: data-mining of prescriber-identified data is constitutionally protected commercial speech.

This is worth sitting with, because it forecloses a response that otherwise seems obvious. The targeting infrastructure is not a gray area waiting for legislative correction. States cannot simply pass laws restricting prescriber data-mining; the Court has already said they cannot, on free-speech grounds. The legal foundation is not a loophole or an oversight. It was examined, challenged, and upheld at the highest level. A new federal privacy statute covering de-identified health data, or a successful narrowing of *Sorrell*, would change this picture — but neither exists as of this writing.

The AMA's role in this structure earned it real money. According to a Public Citizen analysis, in 2011 the Masterfile and other "database products" were the AMA's single most profitable products apart from investments, generating about $42 million — roughly 26% of net revenue before expenses that year, considerably more than membership dues (Public Citizen Health Research Group, *Health Letter*, Nov. 2012). The AMA also operates a Physician Data Restriction Program that lets physicians opt out of *sales-rep access* to their prescribing data — but the program limits rep visibility, not the underlying data licensing. The prescribing data continues to flow.

---

What this chapter has built is a complete causal chain from a single prescription to a bid-time targeting decision. Every link in that chain is legal, disclosed in some form, and commercially mature. The patient's privacy is formally protected at the de-identification step. The physician's privacy was litigated to the Supreme Court and found not to be protected, at least from commercial data-mining.

The gap between how completely the system knows a physician and how little the physician knows about the system is not a malfunction. It is a design feature of a decades-old commercial infrastructure that has been optimized, legally insulated, and technically refined across multiple generations of data technology.

What the system does not know — what it cannot know without being asked and then checked — is whether it is targeting physicians because their patients will benefit or because the physicians are moveable. The propensity model optimizes for predicted prescribing. Whether predicted prescribing tracks patient need or tracks susceptibility to influence is a question the model itself cannot answer. It is the question Chapter 13 will test on public data.

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

---

## Prompts

### Figure 3.1 — De-identification removes the patient and leaves the prescriber

Build a two-column pipeline diagram as a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN, inline CSS and inline JS. Five vertically stacked stages on the left margin (Pharmacy, Payer / Safe Harbor, Broker, Model, Bid). For each stage draw two boxes side by side: a left "patient identifiers" box and a right "NPI" box. In the patient column, show "name · DOB · address present" at the pharmacy, then struck-through (line-through) at the payer step, then "— patient gone —" thereafter. In the NPI column, show "NPI 1234567890" persisting unchanged, with red borders, resolving to "Dr. Jane Smith named" at the model step (note the AMA Masterfile join at the broker step) and an impression at the bid step. Draw downward arrows linking the NPI boxes to show persistence. Patient column ink/grey, NPI column red highlight. Hover tooltips per stage. viewBox 700x480. Structural, not aesthetic.

### Figure 3.2 — The gap between event and targeting signal is where targeting error lives

Build two parallel horizontal timelines as a single self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Top track "Claims-data lag — the standard monthly cycle": five nodes along an arrowed baseline labeled Day 0 (Rx written), Day 1–3 (pharmacy adjudication), Day 7–14 (payer processing), Day 14–30 (broker aggregation), monthly (model refresh → list deployed, highlighted red). Bottom track "Real-time EHR trigger — dynamic NPI activation": two nodes, Day 0 (chart opened) and Day 0 (bid fired, highlighted red), on a much shorter arrowed baseline. Day labels in monospace above each node, event labels below. Below both, a light-fill callout box noting the gap is where targeting error lives (stale lists, distorted lift). Hover tooltips per node. viewBox 700x420. Structural timeline, not decorative.

### Figure 3.3 — The graph is enriched by targeting; each campaign refines the next

Build a radial feedback diagram as a single self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Center: a red-bordered circle labeled "NPI profile / one physician". Three spoke boxes positioned around it: CRM (rep call logs) top, Endemic media (click data — Medscape, WebMD) lower-left, EHR triggers (prompt responses) lower-right. For each spoke draw a pair of parallel arrows — one outbound (profile → channel, the activation) and one return (channel → profile, the engagement signal), offset so they do not overlap. Add one label "engagement signal → feature update". Center red; spokes grey-bordered. Keep labels off the arrow centerlines. Hover tooltips per node. viewBox 700x420. Structural circular layout, not aesthetic.

---

## Chapter 3 Exercises: The HCP Identity Graph

**Project:** One Drug, End to End
**This chapter adds:** Assemble a synthetic/public prescriber identity graph for your drug and write out its propensity feature vector — then flag which features predict patient need versus targetability.

### Exercise 1 — When to Use AI

**The judgment:** Three chapter tasks where AI assistance is appropriate.

- *Summarizing the 18 HIPAA Safe Harbor identifiers and the two de-identification routes.* **Why AI works here:** summarizing — these are well-documented facts you can verify against the primary HIPAA text.
- *Drafting a first-pass classification of a propensity feature vector* (clinical-need / behavioral-neutral / susceptibility-proxy). **Why AI works here:** pattern-spotting — sorting features into known buckets, which you then confirm feature by feature.
- *Explaining the* Sorrell v. IMS Health *holding in plain language.* **Why AI works here:** summarizing — a documented Supreme Court holding you can check against the opinion.

**The tell:** You are using AI appropriately when you can independently evaluate the output — when you can check each classified feature against the chapter's framework yourself.

### Exercise 2 — When NOT to Use AI

**The judgment:** Three tasks here that require human judgment.

- *Adjudicating whether a specific data flow for your drug is HIPAA-compliant.* **Why AI fails here:** hallucination risk + values judgment — this needs counsel; a fluent model answer produces false legal confidence.
- *Concluding that your drug's propensity model is unlawfully discriminatory.* **Why AI fails here:** missing ground truth — whether susceptibility features are heavily weighted is an open empirical question, not a fact the model can retrieve.
- *Certifying that a de-identification scheme's re-identification risk is "very small."* **Why AI fails here:** calibration gap — this is an Expert Determination a qualified statistician makes, and the model cannot quantify the risk.

**The tell:** You've crossed the line when AI output is your *reason* for a conclusion rather than a tool for reaching one.
**Series connection:** This trains **T4 Metacognitive** judgment — separating what is publicly documented (retrievable) from legal and statistical determinations that require credentialed human authority.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** A synthetic prescriber identity graph for your drug — a small set of synthetic NPI profiles plus a documented propensity feature vector with each feature classified by what it actually predicts.
**Tool:** Claude. Recommend a **Claude Project** — the firewall discipline (synthetic-only profiles, no real prescribers) is a standing rule best stored once in Project instructions so it governs every generation.

**The Prompt:**

```
We are continuing a teaching case study for a branded SGLT2 inhibitor (type 2
diabetes; class has branded competitors and a generic substitute). From earlier
chapters we have its prescriber set (primary care + endocrinology) and its
loyalty-decile/brand-share reasoning.

IMPORTANT FIREWALL: Use ONLY synthetic, invented prescribers. Do NOT name, infer,
or reconstruct any real physician. Do NOT use real NPI numbers — use obviously
fake placeholders like NPI-SYNTH-001. This is public/synthetic data only.

Do three things:

1. SYNTHETIC IDENTITY GRAPH. Create 5 synthetic prescriber profiles relevant to
   this drug. For each: specialty, practice setting, geography (state only),
   synthetic claims-derived signals (script volume tier, switch pattern, loyalty
   decile, brand share), and synthetic engagement signals (email open tier, CME
   completions). Label clearly as synthetic.

2. PROPENSITY FEATURE VECTOR. List the feature vector a propensity model for THIS
   drug would plausibly use, grouped as: (a) claims-derived, (b) identity/
   affiliation, (c) behavioral/digital, (d) Open Payments history.

3. FEATURE CLASSIFICATION. Classify each feature as: clinical-need/eligibility,
   behavioral/neutral-to-targeting, or susceptibility-to-influence proxy. Give a
   one-sentence justification and a confidence (high/med/low). Then list which
   features, if heavily weighted, would make the model select for TARGETABILITY
   rather than PATIENT NEED. Do NOT assert the model IS discriminatory — only
   identify which features raise the question.

Output markdown tables. End with one line naming the public datasets (Open
Payments, Medicare Part D) that could later be used to TEST the susceptibility
question.
```

**What this produces:** A synthetic identity graph (5 fake profiles) plus a classified propensity feature vector for your drug.
**How to adapt this prompt:** *For your own drug:* swap the drug/class line and your prescriber set; keep the firewall paragraph verbatim. *For ChatGPT/Gemini:* paste in one message and re-state the synthetic-only firewall at the top. *For a Claude Project:* put the firewall rule and drug identity in the Project system prompt; send the three numbered tasks as the message.
**Connection to previous chapters:** The loyalty deciles and brand share from Chapter 2 become features in the vector here. **Preview of next chapter:** In Chapter 4 you will inventory and classify the actual AI-stack tools a brand team would run against this graph.

### Exercise 4 — CLI Exercise

**What you're building this chapter:** A reproducible public-data association check — for one specialty in one state, do Open-Payments-present prescribers prescribe your drug differently than absent ones. · **Tool:** Claude Code (joins two public files). · **Skill level:** Intermediate/Advanced.

**Setup:**
1. Download a slice of CMS Open Payments and a slice of Medicare Part D Prescriber data into `one-drug/data/`.
2. Claude Code installed; Python/pandas or DuckDB available.
3. Add a CLAUDE.md rule: "Report associations only; never write 'caused' in output; print the join key and matched-row count."

**The Task:**

```
In one-drug/, using the Open Payments and Part D slices in one-drug/data/, do
only this:

1. Restrict to ONE specialty in ONE state (pick endocrinology in a state present
   in both files; state your choice).
2. Split prescribers into those who appear in Open Payments (any payment) vs.
   those who do not.
3. For your SGLT2 brand (from DRUG.txt), compute each group's average claim count.
4. Write ch03-openpayments-assoc.md with the two group averages, the join key
   used, the matched-row count, and a one-sentence statement of what this
   ASSOCIATION does and does NOT show (it cannot establish that payments caused
   prescribing).

Safety: read-only on the data files; create only the script and the markdown.
Verification: print how many prescribers fell into each group; if either group
is under 10, say so and label the result unreliable rather than reporting it as
meaningful. Stop after writing the markdown.
```

**Expected output:** A join script and `ch03-openpayments-assoc.md` with the two averages, group sizes, join key, and the association-not-causation caveat.
**What to inspect:** Group sizes — a tiny group makes the average meaningless; the caveat must be present and the word "caused" absent.
**If it goes wrong:** Most likely failure is a bad join (NPI formatted as int in one file, string in the other) producing zero matches that the model then narrates around. Recovery: normalize the NPI key type on both sides and re-join — don't accept averages computed over an empty join.
**CLAUDE.md / AGENTS.md note:** Add "Public-data findings are associations; never write causal language; always report group sizes."

### Exercise 5 — AI Validation Exercise

**What you're validating:** The propensity feature classification from Exercise 3 (which features predict need vs. targetability). · **Validation type:** Reasoning + Factual. · **Risk level:** High — mislabeling a susceptibility proxy as clinical-need launders a fairness question into a description of "patient need," exactly the move the chapter warns against.

**Setup:** Use your Exercise 3 output as the artifact.

**The Validation Task:**

```
Validation Checklist — Chapter 3 (Propensity Feature Classification)

Mark each Pass / Fail / Cannot-determine with one line of evidence:

- Correctness: Is Open Payments history classified as a susceptibility-to-
  influence proxy, not as clinical need?
- Completeness: Is every feature classified AND given a confidence level?
- Scope: Are all profiles synthetic (fake NPIs, no real physicians)? Any real
  NPI = automatic Fail.
- Chapter-specific 1: Does it identify which heavily-weighted features would make
  the model select for targetability rather than patient need?
- Chapter-specific 2: Does it correctly treat the "is this model discriminatory"
  question as OPEN and testable, not as a settled verdict?
- Failure-mode check (fluent-but-wrong + ecological inference / missing ground
  truth): Did it slide a susceptibility proxy into "clinical need," or claim the
  model's real weighting is known when it is not? Flag any feature whose
  classification it states with unwarranted confidence.
```

**What to do with your findings:** Pass → use the classified vector. One fail → revise that feature's label and re-run. Multiple/uncertain → reclassify the features yourself against the chapter's three-category framework; this is a "When NOT to Use AI" moment, because the need-vs-targetability call is the chapter's central human judgment.
**AI Use Disclosure prompt (mandatory):** Two sentences — what the AI produced (e.g., "drafted the synthetic profiles and feature classification") and how you used it, plus one thing it couldn't determine (e.g., "whether Open Payments is actually heavily weighted in real models, which is an open question I flagged for public-data testing rather than asserting").
**Series connection:** Trains detection of **ecological inference / missing-ground-truth** errors under **T4 Metacognitive** judgment — refusing to convert an untested feature weight into a claim about patient need.
