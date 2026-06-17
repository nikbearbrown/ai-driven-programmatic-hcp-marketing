# Research Notes: Chapter 01 — The Machine Nobody Sees

**Chapter one-line (TIKTOC):** Fellows learn to describe the full HCP marketing stack — identity graph → programmatic impression → attribution — precisely enough to critique, and to name the structural anomaly that the payer is not at the table.

**Opening artifact (TIKTOC):** a real point-of-care / CDS Hooks co-pay message firing inside the EHR, worked backward to the infrastructure that produced it.

**Scope of these notes:** the pharma HCP marketing stack; the prescriber/patient/payer split; point-of-care / EHR / CDS Hooks / SMART-on-FHIR as a commercial channel; co-pay cards and the lost price signal.

---

## A. Conceptual foundations

### A1. The prescriber/patient/payer/institution split (the "structural anomaly")
**Explanation.** Ordinary advertising assumes the person who *sees* the ad, *decides* to buy, *pays*, and *consumes* are the same person. Pharma breaks every link: the **physician decides** (writes the script), the **patient consumes** (takes the drug), the **payer/PBM pays** (insurer, employer, government), and the **institution** (health system, formulary committee) constrains the menu. Advertising theory built on consumer sovereignty does not apply, because the decision-maker bears almost none of the cost and experiences none of the consumption. This is a textbook **principal–agent problem with split agency**: the physician is the patient's agent for the *clinical* decision but is the target of the *commercial* message, and information asymmetry is large.
**Common misconception.** "Pharma marketing is just B2B advertising aimed at doctors." It is not — the cost-bearer (payer) is structurally absent from the message, so the price-sensitivity that disciplines normal markets is missing. The anomaly the chapter names: **the party who pays is not at the table.**
**Worked example.** A point-of-care ad for a branded drug fires when a physician opens an eligible patient's chart. The physician chooses it; the patient takes it; the insurer pays ~95% of a list price the physician never sees; a clinically equivalent generic at 1/10 the cost sits one formulary tier away, unadvertised. Every incentive in the message points away from the cheaper equivalent.
**Source.** Principal–agent framing in pharma: *Health Policy and Planning*, "Principal-agent problems in health care" (Oxford Academic, https://academic.oup.com/heapol/article/26/suppl_1/i53/558693). Stakeholder-misalignment evidence: Medicare Part D gift study — 39.1% of 2013 Part D prescribers received gifts; recipients prescribed 2.3 more claims/patient and 7.8% more branded drugs (PMC5656307, https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5656307/). Also `pantry/pharma-marketing-evidence-synthesis.md` §6 (stakeholder map).

### A2. The NPI identity layer as the foundational data primitive
**Explanation.** The National Provider Identifier (NPI) is a unique 10-digit number assigned to every US licensed provider. In HCP marketing it functions as the equivalent of a cookie — except it is **permanent, accurate, and tied to real prescribing behavior**. Pharma builds NPI target lists curated by specialty, geography, prescribing history, and patient mix; the persistent cross-channel profile keyed to each NPI is the **HCP identity graph**. (Detailed in Ch 3; introduced here as the spine the whole stack hangs on.)
**Common misconception.** "Targeting doctors must rely on probabilistic matching like web ads." No — NPI gives *deterministic* identity. The 2025 frontier is **Bid-by-NPI** (Tap Native / eHealthcare Solutions), an auction model letting advertisers set a bid at the single-prescriber level.
**Worked example.** A brand objective ("grow new starts among high-volume cardiologists in the Southeast") becomes an NPI list, which becomes bid-time decisions on which prescriber sees which creative in which channel.
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §1 (NPI identity layer; Bid-by-NPI).

### A3. Point-of-care / EHR as a commercial channel — the mechanics
**Explanation.** Getting a commercial message *inside* the EHR is non-trivial because Epic and Oracle Cerner officially prohibit native advertising. Platforms route around this with two open clinical-interoperability standards repurposed commercially:
- **SMART on FHIR** (Substitutable Medical Apps & Reusable Technologies on Fast Healthcare Interoperability Resources): an open standard letting an approved third-party app launch inside the EHR (e.g., embedded in Epic's Hyperspace, often in an iframe) and receive patient/encounter/clinician context via FHIR resources, authorized with **OAuth 2.0**. EHR-launch hands the app a short-lived launch token; after the OAuth handshake the ID token carries SMART context claims (patient, encounter, fhirUser). Designed for clinical apps; Doceree's **Spark** uses it for branded engagement "within approved interoperability frameworks."
- **CDS Hooks** (HL7 standard, built by the SMART Health IT team): an event-driven HTTP API. When a clinician performs a workflow action, the EHR fires a *hook* to a registered external service, which returns "cards" rendered in the EHR. Mature hook types: **`patient-view`** (chart opened), **`order-select`** (an order is chosen), **`order-sign`** (about to sign/submit). Built for safety alerts and guidelines; commercial platforms adapt the same trigger points to fire branded messages — and a card can link out to a SMART on FHIR app.
**Common misconception.** "These are banner ads bolted onto the EHR." They are messages delivered *inside the clinical software, in the same visual layer as drug-interaction warnings and guideline alerts* — which is exactly the ethical problem (A4 below).
**Worked example.** Physician enters ICD-10 Z87.891 (history of nicotine dependence) → CDS Hooks `order-select`/`patient-view` fires → smoking-cessation drug card appears in the sidebar → at the e-prescribing screen a co-pay card populates. The same standard that surfaces a contraindication surfaces the ad.
**Source.** CDS Hooks spec & hook types: cds-hooks.org (https://cds-hooks.org/), HL7 CDS Hooks 2.0 (https://cds-hooks.hl7.org/2.0/), Medblocks practical guide (https://medblocks.com/blog/hl7-cds-hooks-a-practical-guide). SMART App Launch v2.2.0 (https://build.fhir.org/ig/HL7/smart-app-launch/app-launch.html); Epic SMART-on-FHIR launch context (6B, https://6b.health/insight/how-to-register-authenticate-launch-apps-with-epics-fhir-apis/). Doceree Spark / EHR ecosystem: `pantry/pharma-ai-hcp-marketing-synthesis.md` §2.

### A4. Co-pay cards and the lost price signal
**Explanation.** A co-pay card (manufacturer coupon) lowers the *patient's* out-of-pocket cost for a branded drug at the pharmacy counter. Because the patient now feels little or no price difference between brand and generic, the **price signal that would otherwise steer them (and the physician) toward the cheaper equivalent is erased** — while the insurer still pays the higher net price. This is a deliberate intervention in the broken principal–agent market (A1): the manufacturer subsidizes the one party (patient) whose price sensitivity could trigger substitution.
**Common misconception.** "Coupons are pro-patient — they make drugs affordable." Affordability for the individual at the counter, yes; but they raise *system* cost and suppress generic substitution. The book's stance (TIKTOC contested-claims table): **nuanced** — improve affordability but can suppress generic substitution.
**Worked example / numbers.** NBER (Dafny, Ody, Schmitt): coupon introductions increased quantity of drugs *without generic substitutes* by 23–25% in the commercial segment vs. Medicare Advantage (where coupons are banned); net-of-rebate prices were ~8% higher; among branded drugs with coupons, ~49% had a generic equivalent or close substitute available at lower cost.
**Source.** NBER w29735 / AEJ: Policy (https://www.nber.org/papers/w29735); NBER Digest summary (https://www.nber.org/digest/202205/copayment-coupons-and-pricing-prescription-drugs). Coupon-accumulator landscape: KFF (https://www.kff.org/health-costs/copay-adjustment-programs-what-are-they-and-what-do-they-mean-for-consumers/). Also `pantry/pharma-brand-measurement-synthesis.md` §4 (Georgetown brief citing Dafny et al., "boosted branded sales by over 60%"). Doceree's 2025 Co-Pay.com expansion inserts co-pay cards into the prescribing workflow: `pantry/pharma-ai-hcp-marketing-synthesis.md` §2.

---

## B. Domain examples and cases

- **Doceree Spark (SMART on FHIR) + 150+ direct EHR integrations.** Largest direct POC-engagement platform by integration count; positions as "AI-powered operating system for healthcare marketing." 2025 expansion into Co-Pay.com brings co-pay cards into the prescribing moment. (`pantry/pharma-ai-hcp-marketing-synthesis.md` §2, §6.)
- **OptimizeRx DAAP (Dynamic Audience Activation Platform).** 300+ EHR/ePrescribing/telehealth network; predictive AI to identify the right HCP at the right clinical moment rather than pure real-time triggers. Publicly traded (OPRX) → some financial transparency, but script-lift figures still company-reported. (`pantry/pharma-ai-hcp-marketing-synthesis.md` §2.)
- **WebMD Ignite "Ignite on FHIR."** Extends the same model patient-facing inside Epic's MyChart patient portal — shows the channel is not HCP-only. (Synthesis §2.)
- **The ICD-10 trigger walkthrough.** Z87.891 → sidebar smoking-cessation ad; e-prescribing screen → co-pay card; oncology chart → targeted-therapy banner. The literal "machine nobody sees." (Synthesis §2.)
- **FAILURE / counter-case — the market failure of the missing counter-infrastructure.** The *same* SMART on FHIR / CDS Hooks plumbing could surface comparative-effectiveness data, generic alternatives, and cost-to-patient at the prescribing moment. Nobody funds that at scale. Academic-detailing analogues exist only in fragments (VA academic detailing, NPS MedicineWise [AU], Therapeutics Initiative [BC]) — none at commercial scale. The "failure" is structural: the parties who benefit from unbiased prescribing (patients, payers) are the least organized to fund the counter-stack. (`pantry/pharma-marketing-evidence-synthesis.md` §8; synthesis §8.)

---

## C. Connections and dependencies

- **Prereqs:** none (Week 1, the pebble-in-the-pond opener). Assumes only general AI literacy and Python — pharma stack is *taught here*.
- **Unlocks:** Ch 2 (the stack optimizes *something* — lift or brand?); Ch 3 (the NPI identity graph introduced here is built in detail there); Ch 4 (what the AI layer does on top of this substrate); Ch 5 (the EHR-ad evidence gap named here becomes the evidence problem).
- **Adjacent:** Ch 8 (POC natural-experiment for incrementality), Ch 12 (POC as a public-data identification target). The co-pay/price-signal material recurs in Ch 13 Track D (coupon generic-suppression causal estimate).

---

## D. Current state of the field

- **Settled.** SMART on FHIR + CDS Hooks are real, documented open standards; their commercial repurposing is real and growing. NPI-level deterministic targeting beats specialty-level. Co-pay coupons raise branded volume and suppress generic substitution (NBER, dose-response). The prescriber/patient/payer split is well-described economics.
- **Contested / thin.** Whether EHR-integrated advertising produces *clinically appropriate or inappropriate* prescribing change — **no peer-reviewed study exists**. This is the single largest open validation gap (the chapter's "research finding for Fellows"). Whether real-time clinical-context triggers constitute "use of PHI in marketing" is legally unsettled; platforms uniformly assert HIPAA compliance, independent legal analysis is limited.
- **Last-3-years developments.** POC crossed $1B annual spend in 2024 (171% growth 2019→2023; ~15–22%/yr — fastest-growing pharma-digital segment, >4× overall digital growth; figures from Point of Care Marketing Association, likely an undercount). Bid-by-NPI launched 2025. Doceree Co-Pay.com 2025. FDA's Sept 2025 enforcement wave (200+ letters) used AI surveillance but **targeted DTC/web, not EHR ads** — EHR advertising remains a regulatory vacuum (no specific OPDP guidance; ONC info-blocking rules don't cover commercial ads). US is globally unique: EU GDPR/ePrivacy would prohibit the required data flows. (`pantry/pharma-ai-hcp-marketing-synthesis.md` §5.) **FLAG: verify the POC spend/growth numbers against POCMA primary source before publication** — TIKTOC explicitly tags this.

---

## E. Teaching considerations

- **Where students stick.** (1) They default to consumer-advertising intuitions; the prescriber/patient/payer split has to be made viscerally concrete before anything else lands. (2) They assume EHR ads are crude banners; showing the actual CDS Hooks card-in-the-sidebar (same layer as a drug-interaction alert) is the "click" moment. (3) They think co-pay cards are unambiguously good — the NBER numbers flip that.
- **Analogies.** The split market = "a restaurant where the chef orders your meal, you eat it, and your insurance company gets the bill — and the menu is written by the people selling the most expensive dish." CDS Hooks = "the same loudspeaker that announces a fire alarm is rented out for ads." Lost price signal = "a coupon that makes the brand feel free to you while quietly billing your insurer full price."
- **Exercise (matches TIKTOC LLM exercise).** Give students a public Doceree/OptimizeRx product page; have them map every phrase onto stack layers (identity → trigger/impression → attribution) and flag which claims are mechanism vs. effectiveness. Apply-level: trace one brand objective → NPI list → POC impression → attribution loop, and mark where the payer would have intervened in a normal market.

---

## F. Library files relevant (copied to `pantry/` as `_lib_*`)

- `_lib_business-data-ism-the-revolution-transforming-decision-making-consumer-behavior-and-al.md` — background on data-driven targeting infrastructure and the "everything is a data primitive" worldview; context for the NPI-as-cookie framing.
- `_lib_math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` — the general critique of opaque scoring systems acting on people who can't see them; thematic match for "the machine nobody sees" (the targeted physician barely understands the targeting).

*(Note: the shared MD library has essentially no pharma-HCP-marketing-specific files — confirmed by full grep for Doceree/POC/co-pay/Sunshine/NPI/SMART-on-FHIR; the relevant pharma-specific material lives in the existing `pantry/` syntheses and the web sources cited above.)*

---

## G. Gaps and flags

- **FLAG (TIKTOC-mandated):** POC channel-growth figures ($1B+, 171%, 15–22%/yr, "4× faster than digital") are industry/POCMA-sourced — verify against the primary POCMA release and an independent analyst before publication.
- **FLAG:** "EHR/point-of-care advertising is the fastest-growing channel with the thinnest independent evidence" is the chapter's headline research finding — the evidence-thinness half is well-supported (no peer-reviewed clinical-impact study); the growth-ranking half needs the verification above.
- **GAP:** No independent legal adjudication of whether SMART-on-FHIR/CDS-Hooks commercial triggers constitute PHI-in-marketing under HIPAA. Platforms assert compliance; route to counsel, do not adjudicate (book's stance).
- **GAP:** AMA has no specific policy statement on EHR-integrated advertising as of mid-2026 — so there is no authoritative professional-body position to cite for/against; note the silence rather than inventing one.
- **CONTESTED (book's position):** Co-pay coupons pro-patient = nuanced (affordability vs. generic suppression / system cost). Present both NBER findings; don't resolve it as purely good or purely bad.
