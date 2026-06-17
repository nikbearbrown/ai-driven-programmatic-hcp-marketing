# Research Notes: Chapter 03 — The HCP Identity Graph and the Targeting Data

**Chapter one-line (TIKTOC):** Fellows learn how prescribing data is legally obtained and resolved to NPI identity, what the feature vector actually contains, and where it is biased.

**Opening artifact (TIKTOC):** the AMA Physician Masterfile — the bridge from de-identified claims to physician identity, and why its existence is the legal foundation of NPI targeting.

**Scope of these notes:** NPI identity; claims data (IQVIA/Symphony); AMA Physician Masterfile; HIPAA safe-harbor de-identification; CRM / endemic media / EHR triggers; the propensity feature vector (incl. Open Payments); claims lag; bias/privacy.

---

## A. Conceptual foundations

### A1. HIPAA de-identification — Safe Harbor vs. Expert Determination
**Explanation.** The entire targeting industry rests on one legal fact: **de-identified** health data is no longer PHI and can be used/sold commercially. HIPAA provides two routes:
- **Safe Harbor** (rule-based): remove **18 specified identifiers** (names; all geographic subdivisions smaller than a state *except* 3-digit ZIPs with ≥20,000 people; all date elements finer than year for dates tied to an individual; phone/fax; email; SSN; medical record / health-plan / account numbers; certificate/license numbers; vehicle and device identifiers/serials; URLs; IP addresses; biometric identifiers; full-face photos; and any other unique identifying code). Simple, cheap, conservative — but strips detail.
- **Expert Determination** (risk-based): a qualified statistician certifies the re-identification risk is "very small," allowing *retention of more detail* (e.g., month-level dates, sub-state geography) — better for ML/research. Claims aggregators often use this to keep longitudinal granularity.
**Common misconception.** "De-identified = anonymous forever." Re-identification risk is real, especially with rich longitudinal data; Safe Harbor is a rule, not a guarantee, and Expert Determination is an explicit *risk* judgment ("very small," not "zero"). The data flow: patient → payer (strips identifiers per HIPAA) → broker licenses → pharma buys. Nobody in that chain holds identifiable *patient* data — but the *physician* is fully identifiable (A3).
**Worked example.** Pharmacy claim for a statin: patient identifiers stripped under Safe Harbor; the *prescriber's* NPI remains (an NPI is not a patient identifier). Result: "NPI 1234567890 wrote 47 statin scripts last month" is de-identified-patient but fully-identified-physician.
**Source.** HHS HIPAA de-identification guidance, summarized: Censinet Safe Harbor vs. Expert Determination (https://censinet.com/perspectives/safe-harbor-vs-expert-determination-phi); 18-identifier list (https://www.walturn.com/insights/the-18-hipaa-identifiers-and-how-to-de-identify-them); USC IFS de-identification guide (https://ifs.sc.edu/resources/documents/USC_IFS_PHIDataDeIdentification_18_REV22.pdf). Data flow also in `pantry/pharma-ai-hcp-marketing-synthesis.md` §5.

### A2. The claims layer — IQVIA / Symphony / Definitive Healthcare
**Explanation.** De-identified-patient prescribing data is sold by data brokers who aggregate across payers/pharmacies.
- **IQVIA LAAD** (Longitudinal Access and Adjudication Data): the dominant dataset, ~90% of US retail pharmacy dispensing, monthly; IQVIA's OneKey directory holds 11M+ HCP profiles. The infrastructure under most HCP targeting.
- **Symphony Health** (now under ICON): major alternative, strong in specialty pharmacy/distribution.
- **Definitive Healthcare:** HCP demographic, affiliation, procedural data for audience construction.
**Common misconception.** "Pharma sees individual patient records." No — they buy *aggregated, de-identified-patient* prescribing data keyed to prescriber NPI. The patient is invisible; the physician is the unit of analysis.
**Worked example.** A propensity model trains on LAAD-style features: each NPI's monthly script volume by drug/class, switch patterns, patient-mix proxies, refill behavior.
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §3.

### A3. The AMA Physician Masterfile — the identity bridge (chapter opener)
**Explanation.** This is the load-bearing legal/commercial mechanism the whole chapter pivots on. De-identified claims tell you *what NPI X prescribes*; the **AMA Physician Masterfile** tells you *who NPI X is* — name, address, education, specialty, and historically **DEA license number** — for ~1M+ US physicians (the file covers nearly every physician, member or not, built from medical-school entry onward). The AMA *licenses* this data to data-mining firms (historically IMS Health, Verispan, Dendrite), who **link physician identity to purchased pharmacy prescribing records** to create prescriber-level data (PLD) sold to drugmakers. This linkage *is* the foundation of NPI-level targeting.
**Common misconception.** "There must be a loophole or it's illegal." It is neither a loophole nor illegal — it is the open, commercial, legal backbone of the industry. (It is, however, "barely understood by the physicians being targeted.") The AMA earns substantial revenue from it: in 2004 the AMA took in **$40.4M from database products (~15% of consolidated revenue)**.
**Worked example.** IMS Health's founding model (per the historical record): buy pharmacy Rx records + license AMA Masterfile + join the two → prescriber-level data. The join key is physician identity (now NPI/DEA).
**Legal foundation — Sorrell v. IMS Health (2011).** Vermont's 2007 Prescription Confidentiality Law barred selling/using prescriber-identified data for marketing without physician consent. The Supreme Court struck it down as a First Amendment violation — **data-mining of prescriber-identified data is constitutionally protected commercial speech.** This is *why* the targeting infrastructure is legally secure; cite it as the precedent.
**Source.** AMA Masterfile + IMS linkage + revenue: Medscape (https://www.medscape.com/viewarticle/559704), Wikipedia AMA Physician Masterfile (https://en.wikipedia.org/wiki/AMA_Physician_Masterfile), AMA data licensing reporting (amednews, https://amednews.com/article/20060522/profession/305229971/1/). The AMA's physician-data-privacy / opt-out (PDRP) program: AMA (https://www.ama-assn.org/topics/ama-physician-professional-data). Sorrell v. IMS Health: https://en.wikipedia.org/wiki/Sorrell_v._IMS_Health_Inc. Also `pantry/pharma-ai-hcp-marketing-synthesis.md` §1, §3, §5.

### A4. The propensity feature vector (incl. Open Payments) and claims lag
**Explanation.** The feature vector behind a physician propensity model typically combines: **claims-derived** features (script volume by class, switch/restart patterns, patient-mix proxies, refill behavior, decile), **identity/affiliation** features (specialty, practice setting, geography, health-system), **behavioral/digital** signals (journal reads, CME completion, endemic-platform visits, email engagement, search), and — notably — **CMS Open Payments** history (publicly disclosed industry payments/meals to the physician, from the Sunshine Act). **Claims lag** is the central data-quality limit: claims data arrives with a notable delay (historically lists refreshed only a few times/year), so a "static" propensity model is always somewhat stale; the frontier is *dynamic NPI activation* ingesting real-time clinical signals (OptimizeRx DAAP).
**Common misconception.** "Propensity = clinical need." A propensity model predicts *who will prescribe*, which conflates clinical need with **susceptibility to influence** and historical prescribing bias. Open Payments as a feature is double-edged: it encodes a physician's *receptivity to industry* (a susceptibility proxy), not patient need. TIKTOC's flagged research finding: whether propensity models encode proxies for physician *susceptibility* (not just clinical need) is **unexamined and answerable with public data** — a fairness/accountability question (Ch 13 Track D).
**Worked example.** Two cardiologists with identical patient mix; one has a long Open Payments meal history. A propensity model may rank the second higher — not because patients need the drug more, but because that physician is more *targetable*. Including Open Payments risks reinforcing influence-susceptibility as a targeting criterion.
**Source.** Feature vector + claims lag + DAAP: `pantry/pharma-ai-hcp-marketing-synthesis.md` §1, §3. Open Payments–prescribing association: PMC5880069 (industry payments ↔ costlier prescribing, Open Payments + Part D, https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5880069/). Bias-reinforcement framing: `_lib_math-weapons-of-math-destruction-*.md`, `_lib_ai-the-alignment-problem-*.md`.

### A5. CRM / endemic media / EHR triggers — where the graph gets *activated*
**Explanation.** The identity graph is not static data — it is *activated* across channels: **CRM** (Veeva / IQVIA OCE+ / Salesforce LSC4CE) feeds reps NBA recommendations; **endemic media** (Medscape/WebMD, journals) targets by NPI in trusted clinical environments; **EHR triggers** (CDS Hooks / SMART on FHIR, Ch 1) fire on real-time clinical events. The same NPI profile drives all three; **omnichannel orchestration** coordinates them so one physician isn't blitzed incoherently.
**Common misconception.** "The data and the targeting are separate steps." They're one loop — the graph is continuously refreshed by engagement signals fed back from every channel (CRM logs, click data, EHR triggers), which become new features.
**Worked example.** Dr. Martinez switched 3 patients off Brand X (claims signal) + Brand Y digital engagement trending up (behavioral signal) + available Tuesday 2pm (calendar) → CRM surfaces an NBA call recommendation. (Synthesis §3.)
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §3, §7; CRM/NBA detail also Ch 4 notes.

---

## B. Domain examples and cases

- **IMS Health's prescriber-level-data model.** The canonical join: pharmacy Rx records + AMA Masterfile → PLD. Shows the literal mechanism of the identity bridge. (Medscape; amednews.)
- **Sorrell v. IMS Health (2011).** The legal keystone — prescriber data-mining is protected speech; explains why states *cannot* easily restrict it. (Wikipedia/SCOTUS.)
- **CMS Open Payments (Sunshine Act).** A *public* dataset of industry→physician payments — simultaneously a propensity feature *and* the Fellow's public-data tool for auditing the targeting industry (Ch 12/13). Dual role is pedagogically rich.
- **OptimizeRx DAAP dynamic activation.** Static-claims → real-time-signal upgrade; addresses the claims-lag problem. (Synthesis §1.)
- **FAILURE / fairness case — proxy discrimination in targeting.** If propensity features (Open Payments history, historical prescribing) encode susceptibility rather than patient need, the model *reinforces existing prescribing bias* and may concentrate promotion on the most-influenceable physicians regardless of patient benefit — an algorithmic-fairness failure mode, empirically testable on public data (Ch 13 Track D: proxy-discrimination detection in rep assignment). Analogous failure patterns documented in `_lib_math-weapons-of-math-destruction-*.md` (opaque scores that entrench bias) and `_lib_ai-the-alignment-problem-*.md` (proxy objectives).

---

## C. Connections and dependencies

- **Prereqs:** Ch 1 (NPI as the data primitive; the stack), Ch 2 (the metrics a model would predict — NBRx, deciles).
- **Unlocks:** Ch 4 (the AI stack operates *on top of* this substrate); Ch 6 (the propensity model is a tabular ensemble problem — this chapter defines its feature vector); Ch 7 (whether "MoE" segmentation beats an ensemble on this exact data); Ch 8 (propensity ≠ incrementality — the feature vector predicts *who will*, not *whom you changed*); Ch 12–13 (Open Payments / Part D as public data; Track D fairness).
- **Adjacent:** Ch 11 (privacy/HIPAA flags routed to counsel); Ch 1 (claims data + co-pay).

---

## D. Current state of the field

- **Settled.** HIPAA Safe Harbor (18 identifiers) and Expert Determination are well-defined legal routes. The claims → de-identification → AMA-Masterfile → NPI-resolution → bid-time pipeline is established and legal. Sorrell v. IMS Health is binding precedent. Industry payments are *associated* with costlier/branded prescribing (Open Payments + Part D studies).
- **Contested / open.** (1) **Susceptibility-proxy question** — whether propensity feature vectors encode influence-susceptibility rather than clinical need is *unexamined*; the book's stance is "flag, don't assert," and it's answerable with public data (TIKTOC contested-claims table; Ch 13 Track D). (2) **Re-identification risk** of rich de-identified claims is an active privacy-research area, not settled. (3) Whether real-time EHR clinical-context triggers cross into PHI-in-marketing is legally unsettled (Ch 1 overlap).
- **Last-3-years developments.** Bid-by-NPI (2025) — single-prescriber auction pricing. Dynamic NPI activation (DAAP) reducing claims-lag dependence. Veeva/IQVIA/Salesforce CRM consolidation (2024–2026) tightening the graph→activation loop. AMA's Physician Data Restriction Program (PDRP) lets physicians opt out of rep *access* to their prescribing data — but it limits rep visibility, not the underlying data licensing.

---

## E. Teaching considerations

- **Where students stick.** (1) Believing de-identified = anonymous patient = no privacy issue — clarify that the *physician* is fully identified and that re-id risk for patients is non-zero. (2) Missing the AMA Masterfile's role — without it, claims data is just numbered NPIs; *it is the bridge*, and that's the chapter's whole point. (3) Conflating propensity with need — set up the Ch 8 inversion here by stressing the feature vector predicts behavior, not benefit.
- **Analogies.** De-identification = "the pharmacy erases the patient's name but leaves the doctor's signature." AMA Masterfile = "the phone book that turns an anonymous prescribing pattern into Dr. Jane Smith at Mass General." Open Payments as a feature = "using a doctor's history of accepting lunches to predict whether they'll accept your pitch."
- **Exercises (match TIKTOC).** Apply: trace the full pipeline (pharmacy claims → HIPAA de-id → NPI resolution → bid-time decision). Analyze: given a list of feature-vector components, classify each as clinical-need vs. susceptibility vs. neutral and justify. Evaluate: assess how claims lag and identity-resolution error bias both targeting *and* attribution. Lab exercise (TIKTOC): inspect a public CMS Open Payments + Part D extract.

---

## F. Library files relevant (copied to `pantry/` as `_lib_*`)

- `_lib_math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` — the canonical treatment of opaque scoring models that entrench historical bias and act on people who can't inspect them; directly supports the proxy-discrimination / susceptibility-feature analysis.
- `_lib_ai-the-alignment-problem-machine-learning-and-human-values.md` — proxy-objective and fairness framing; supports the "model optimizes targetability, not patient need" argument and the Ch 13 Track D fairness thread.
- `_lib_ai-gigo.md` — data-quality / "garbage-in" reasoning; supports the claims-lag and identity-resolution-error bias discussion.

*(No pharma-identity-specific file exists in the MD library; these provide the bias/privacy/data-quality scaffolding. The pharma-specific mechanics come from the web sources above + `pantry/pharma-ai-hcp-marketing-synthesis.md`.)*

---

## G. Gaps and flags

- **FLAG (TIKTOC research finding):** "Do propensity models encode susceptibility proxies (not just clinical need)?" is *unexamined* — present as an open, publicly-testable question (Ch 13 Track D), not an assertion. The book's rule: flag, don't assert.
- **FLAG:** AMA "$40.4M / ~15% revenue from database products" is a 2004 figure from secondary reporting — flag as historical and `[verify]` for any current figure; the *mechanism* (AMA licenses Masterfile to data-miners) remains current but the dollar amounts are dated.
- **FLAG:** "DEA number in the Masterfile" is historically documented; verify current licensing terms, since AMA data products and what fields are licensed may have changed — `[verify]` before stating current practice.
- **GAP:** Independent, current analysis of the *exact* data flow from EHR clinical-context trigger to ad-server (does PHI ever leave the EHR?) is limited; platforms assert it does not. Route legal characterization to counsel.
- **CONTESTED:** Re-identification risk of de-identified claims — flag as an active research question; do not state that de-identification is fully privacy-protective.
