# AI-Driven Programmatic HCP Marketing: State of the Art
### A Research Synthesis for the Pharma Digital Marketing Practitioner

---

## The Scale of the Machine

Pharma digital ad spend reached $24.8 billion in the US in 2025, up more than 13% year-over-year, and is outpacing most other industries in growth rate. The broader global healthcare advertising market hit $44.56 billion in 2025, projected to reach $67.87 billion by 2033.

Within this, point-of-care (POC) advertising crossed the $1 billion annual spend threshold in 2024 — a 171% increase from 2019 to 2023, growing at roughly 15–22% annually. The category likely underrepresents total POC ad sales because the Point of Care Marketing Association figures only include member revenues.

This is not a marginal channel. POC is the fastest-growing segment in pharma digital, growing more than four times faster than overall digital ad spend.

---

## 1. Programmatic HCP Targeting: How the Machine Works

### The NPI Identity Layer

The National Provider Identifier (NPI) is a unique 10-digit number assigned to every licensed healthcare provider in the US. It has become the foundational data primitive for deterministic HCP targeting — the equivalent of a cookie, but permanent, accurate, and tied to real prescribing behavior.

The pipeline works as follows: Pharma brands construct NPI target lists curated by specialty, geography, prescribing history, patient population characteristics, or practice setting. These lists are built from multiple data sources:

**Claims data** — the primary source, originating from insurance claims and pharmacy fills. De-identified under HIPAA safe harbor provisions, it is sold by data brokers who aggregate across payers. This is the data that tells you what a physician prescribes, in what volumes, for which diagnostic categories.

**The AMA Physician Masterfile** — crucially, the American Medical Association sells access to its physician master file containing license information for nearly every doctor in America. This is the bridge: it connects de-identified prescribing data to identifiable physician profiles, giving pharma brands a complete picture. This is not a loophole — it is the legal and commercial mechanism on which the entire HCP targeting industry rests.

**DEA registries, specialty databases, Definitive Healthcare** — demographic, affiliation, and practice context data layered onto the NPI spine.

**Behavioral data** — digital engagement signals including search behavior, journal article reads, CME completion, and website visits on endemic medical platforms.

The result is an HCP identity graph: a persistent, cross-channel profile for each physician linked to their NPI. The most sophisticated current iteration is **Bid-by-NPI**, launched in 2025 by Tap Native/eHealthcare Solutions — the first auction pricing model allowing pharma advertisers to set individual bids at the single prescriber level, aligning spend directly to predicted prescribing value.

### From Static to Dynamic

Most NPI target lists have historically been static — drawn from claims data with a notable lag time, updated no more than a few times per year. The current frontier is dynamic NPI activation: platforms that ingest real-time clinical signals to continuously refresh audience membership. OptimizeRx's Dynamic Audience Activation Platform (DAAP) is the leading example — using AI and real-world data to identify patients nearing therapy eligibility and the HCPs treating them simultaneously, triggering coordinated HCP+DTC messaging.

### The Attribution Problem

Script lift is the pharma industry's primary measurement currency: the incremental change in prescriptions for exposed vs. unexposed HCPs. Industry platforms report ranges of 4% to 44% lift depending on therapy, targeting methodology, and channel. OptimizeRx's AI-guided DAAP platform claimed 3x the return in half the time vs. traditional trigger-based targeting in a 2024 major depressive disorder campaign.

**Critical caveat**: All script lift figures in this space are vendor-generated. Attribution methodology is not independently audited. The NPI-level linkage between ad exposure and subsequent prescribing requires access to the same data infrastructure used for targeting, creating an inherent measurement circularity. There is no independent academic literature validating the attribution models used by POC platforms. This is the single most significant evidentiary gap in the field.

---

## 2. EHR-Integrated Point-of-Care Advertising: The Prescribing Moment

### How Ads Get Inside Clinical Workflows

Getting a commercial message into an EHR is technically non-trivial because major EHR vendors — Epic, Oracle Cerner — officially prohibit native commercial advertising. The commercial platforms have developed two primary workaround architectures:

**SMART on FHIR apps**: SMART (Substitutable Medical Applications and Reusable Technologies) on FHIR (Fast Healthcare Interoperability Resources) is an open standard that allows third-party applications to launch within an EHR and access patient data via standardized APIs with OAuth authentication. Originally designed for clinical decision support and patient-facing apps, it enables any approved third-party app to embed in the clinical workflow and receive real-time patient context. Doceree's **Spark** product operates exactly this way — built on SMART on FHIR standards, it operates within "approved interoperability frameworks," enabling commercial brand engagement without technically violating EHR platform policies.

**CDS Hooks**: Clinical Decision Support Hooks is a complementary standard that fires service calls at specific points in the clinical workflow — when a patient chart is opened, when a diagnosis code is entered, when an e-prescription is initiated. This mechanism is designed for safety alerts and evidence-based guidelines; commercial platforms have adapted it to trigger branded messages at these same clinical decision moments.

The practical result: a physician enters ICD-10 code Z87.891 (personal history of nicotine dependence) and a smoking cessation drug ad appears in the sidebar. They navigate to the e-prescribing screen and a co-pay card offer populates. They open a patient's oncology chart and a targeted therapy banner loads. These are not ads in the traditional sense — they are messages delivered inside the clinical software, in the same visual context as drug interaction alerts and clinical guidelines.

### The EHR Advertising Ecosystem

**Doceree** operates 150+ direct EHR integrations including Epic and Oracle Cerner, positioning itself as the largest direct POC engagement platform by this measure. Its Spark product uses SMART on FHIR. It also operates an endemic marketplace, point-of-care network, and an ABM suite. In 2025 it expanded into **Co-Pay.com**, extending POC engagement into affordability and treatment initiation — inserting co-pay cards and patient access programs into the prescribing workflow. As of May 2026 it received Frost & Sullivan's Global Technology Innovation Leadership Recognition for AI-powered healthcare marketing.

**OptimizeRx** is the other major POC player, operating a network of 300+ EHR, ePrescribing, telehealth, and practice management contributors. Its key differentiator is DAAP (Dynamic Audience Activation Platform), which applies predictive AI to identify the right HCP at the right clinical moment rather than relying purely on real-time trigger events.

**Veradigm/Allscripts** runs its own Digital Health Media platform positioned as the first EHR marketing solution accepted into the POCMA, emphasizing HIPAA compliance and transparency.

**WebMD Ignite** operates "Ignite on FHIR" reaching patients directly in Epic's patient portal — extending the model from HCP-facing to patient-facing within the same EHR ecosystem.

### The Ethical and Regulatory Status

The AMA has formal policies on physician-industry financial relationships but has not issued a specific policy statement on EHR-integrated advertising as of mid-2026. The AMA's general patient privacy framework emphasizes that "personal health information is not always truly private" in the digital age and that social media platforms, wearable devices, and apps collect health data that "can be shared for advertising purposes."

No federal regulation specifically prohibits commercial advertising delivered via SMART on FHIR within EHR workflows. The ONC's information blocking rules govern data access and interoperability but do not address commercial advertising delivered through interoperability channels. This is a significant regulatory vacuum.

The ethical concern that has been documented: EHR-embedded ads appear in the same visual layer as CDS safety alerts. Medical informatics researchers and the AMA have noted that this proximity risks compromising clinical decision-making, increasing cognitive load, and — most significantly — exposing medical trainees to persistent brand placement at a formative stage of prescribing habit formation, before they have developed independent evidence-based practice patterns.

---

## 3. Prescribing Data Analytics: The Targeting Intelligence Layer

### Where the Data Comes From

De-identified prescribing data is legal under HIPAA's safe harbor provisions as long as 18 specific personal identifiers are removed. The major commercial sources:

**IQVIA LAAD** (Longitudinal Access and Adjudication Data) — the dominant commercial prescribing dataset, covering approximately 90% of US retail pharmacy dispensing, updated monthly. IQVIA has 11+ million HCP profiles in its OneKey directory. This is the data infrastructure underlying most HCP targeting in the industry.

**Symphony Health** (acquired by PRA Health Sciences, now ICON) — a major alternative claims data source, particularly strong in specialty pharmacy and specialty distribution channels.

**Definitive Healthcare** — HCP demographic, affiliation, and procedural data used for audience construction.

The AMA Physician Masterfile remains the critical linkage layer: it connects de-identified Rx data to identifiable physician profiles. Without it, you know that NPI 1234567890 prescribed Drug X 47 times last month; with it, you know that is Dr. Jane Smith at Massachusetts General Hospital.

### Next Best Action: AI in the Commercial Engine

The current frontier of pharma commercial AI is **Next Best Action (NBA)** — AI systems that recommend to a field rep or marketing platform which HCP to contact, through which channel, with which message, at which moment. The major platforms:

**Veeva CRM + AI Agents** (December 2025): Veeva, the dominant pharma CRM platform, released agentic AI capabilities in late 2025 adding next-best-action recommendations. In April 2024 it launched AI-powered e-detailing tools in partnership with SalesLoft.

**IQVIA OCE+ / Salesforce Life Sciences Cloud**: IQVIA launched OCE+ in 2024-2025 with embedded AI-powered NBA recommendations, claiming the ability to suggest optimal call timing and channel for each HCP interaction. In April 2024 IQVIA licensed OCE to Salesforce; in September 2025 Salesforce released Life Sciences Cloud for Customer Engagement (LSC4CE), its direct entry into pharma CRM leadership. All three platforms now offer agentic AI.

In practice: a rep's CRM screen shows that Dr. Martinez in cardiology has recently switched three patients off Brand X, that digital engagement with Brand Y has been trending up over the last 30 days, and that she is available for a virtual detail call on Tuesday at 2pm — all generated automatically from claims data + behavioral signals + calendar optimization. The field rep becomes a human delivery mechanism for an AI-orchestrated engagement sequence.

Healthcare AI investment in pharma commercial operations specifically is projected to grow from ~$1.9 billion in 2025 to over $16 billion by 2034.

---

## 4. AI in Pharma Commercial Operations: Genuine vs. Marketed

### What Is Actually Deployed

**Content generation and MLR acceleration** — the most operationally mature AI use case. MLR (Medical, Legal, Regulatory) review cycles historically run 50–60 days per content piece. AI is now deployed to: flag incomplete claims and missing references before human review, link generated content to pre-approved claims libraries, route low-risk modular content through accelerated approval paths, and generate automated reviewer summaries. McKinsey estimates some companies have reduced regulatory submission timelines by 50–65%. Veeva PromoMats released its Content Agent (AI agents for MLR) in late 2025.

The compliance risk counterpoint: pharma promotional material production rose 29% year-over-year in the US in 2025, while 77% of approved content is rarely or never used by field teams. Volume is rising without proportional quality improvement. An MIT analysis found 95% of generative AI pilots at companies are failing. The problem is governance, not generation speed.

**Trigger-based POC targeting** — clinically mature and widely deployed. ICD-10 code fires → ad delivers. This is the "current gold standard" in POC messaging per industry consensus.

**Predictive audience modeling** — genuinely deployed at scale. Propensity models trained on claims history and behavioral signals identify HCPs with high-potential patient populations before a prescribing event occurs, rather than reacting to it. OptimizeRx DAAP, Doceree's intelligence layer, IQVIA OCE+ all operate this way.

**LLM-based field force support** — emerging. AI-powered podcast-style meeting recaps, voice-activated account preparation, real-time engagement pattern personalization. Deployed at scale by Veeva, Salesforce, IQVIA as of 2025–2026.

**Federated learning for targeting model training** — in development for ID-based ad targeting (Doceree explicitly references this), enabling models to train on distributed patient data without centralizing sensitive information. Genuinely addresses a real privacy problem; maturity level in commercial deployment is unclear.

### What "AI Operating System" Actually Means

Doceree's positioning as "the world's first AI-powered Operating System for healthcare marketing" describes a platform architecture that consolidates:
- HCP identity resolution and targeting
- Point-of-care inventory access (direct EHR integrations)
- Programmatic marketplace (endemic + open web)
- ABM (Account-Based Marketing) for health system targeting
- Co-pay/patient access programs
- Analytics and attribution

The "operating system" framing means a unified data layer across all these capabilities rather than point solutions. The intelligence layers they describe — reading, conversational, workflow, experience — map roughly to: NPI-level audience intelligence, conversational AI for HCP interaction, workflow integration via SMART on FHIR, and experience optimization (creative analytics).

The adaptive mixture-of-experts architecture referenced in Doceree's commercial AI work refers to a machine learning approach where multiple specialized models handle different inputs and a routing mechanism selects which model(s) to apply to a given problem. In pharma commercial terms: one model handles cardiology prescribing dynamics, another handles rare disease referral patterns, another handles oncology treatment sequencing — the router selects the relevant combination for each HCP interaction. This is a real AI architecture, not marketing language, though its specific deployment details are not independently verified.

---

## 5. The Regulatory and Privacy Landscape: 2025–2026

### The FDA Enforcement Wave

In September 2025 the FDA executed an unprecedented enforcement action against pharmaceutical advertising:
- Over 200 enforcement letters issued across pharma manufacturers, telehealth companies, and compounding pharmacies
- 74 letters to pharmaceutical and biologic manufacturers (10 Warning Letters, 64 Untitled Letters)
- Enforcement used "AI and other tech-enabled tools to proactively surveil and review drug ads" — the FDA's own AI-powered surveillance
- Primary violations: exaggerated efficacy claims, failure to present risk information with adequate fair balance

Context: warning letters had collapsed from 100+ annually pre-2020 to 1 in 2023 and 0 in 2024. The 2025 wave was characterized as reversing "decades-long lax enforcement." OPDP's Policy Division was eliminated in April 2025 and senior leaders departed, meaning enforcement is intensifying simultaneously with declining advisory capacity — a difficult regulatory environment.

Critically, the 2025 enforcement primarily targeted DTC content. The enforcement wave has extended to HCP websites, corporate web pages, influencer content, earned media, and patient testimonials — but EHR-integrated advertising remains in a regulatory gray zone with no specific OPDP guidance.

### The HIPAA Architecture of HCP Targeting

De-identified prescribing data is legal to use for commercial purposes under HIPAA safe harbor. The process: insurance claims travel from patient to payer, payer strips identifying information per HIPAA de-identification standards, data is licensed to brokers, brokers sell to pharma brands for targeting. Nobody in that chain possesses identifiable patient data.

The AMA Physician Masterfile bridges this to physician identity. Pharma companies know that NPI X prescribed Drug Y 47 times — and the AMA file tells them NPI X is Dr. Jane Smith. This is legal, widespread, and barely understood by the physicians being targeted.

The contested edge: real-time EHR-triggered advertising uses ICD-10 codes and lab values from active patient charts to select which ad to serve. The ad server does not receive PHI — it receives a contextual signal (patient has this diagnosis, physician is in cardiology). Whether this constitutes use of PHI in marketing is legally unsettled. Platforms uniformly assert HIPAA compliance; independent legal analysis of the precise data flows is limited.

### International Comparison

The US approach to EHR-integrated advertising is unique globally:

| Jurisdiction | EHR-Integrated Commercial Advertising | DTC Advertising |
|---|---|---|
| United States | Permitted via SMART on FHIR / interoperability frameworks; no specific prohibition | Permitted (unique among developed nations) |
| European Union | Commercial advertising within clinical software is effectively prohibited; GDPR would severely constrain the data flows required | Prohibited |
| Canada | Clinical decision systems insulated from commercial promotion; Health Canada does not regulate EHR advertising but practice is not established | Prohibited |
| Australia | TGA restricts physician-directed promotion; EHR-embedded ads not an established practice | Prohibited |

The US regulatory environment enables practices that would be illegal under EU GDPR (specifically: using real-time clinical data to select commercial messages, even through intermediaries, under the ePrivacy Directive and GDPR's legitimate interest requirements).

---

## 6. The Platform Landscape: What Doceree Competes Against

| Platform | Primary Position | Differentiator | Evidence Quality |
|---|---|---|---|
| **Doceree** | Full POC operating system; direct EHR integrations | 150+ direct EHR integrations; SMART on FHIR via Spark; AI OS positioning | All figures vendor-generated; Frost & Sullivan recognition (paid for) |
| **OptimizeRx** | POC network + AI audience platform | DAAP (AI-guided predictive targeting); 300+ EHR/ePrescribing network; publicly traded (OPRX) | Script lift figures are company-reported; no independent audit; public company so some financial transparency |
| **Veeva Crossix** | Privacy-first omnichannel measurement | HCP-level attribution; ties media exposure to Rx outcomes; built on pharma CRM ecosystem | Best privacy methodology in the category; cited as measurement gold standard by independent analysts |
| **PulsePoint** | Health-focused programmatic DSP | Real-time health signals + open web DSP delivery across HCP and patient audiences | Standard programmatic metrics; limited HCP-specific attribution |
| **IQVIA** | Data infrastructure + commercial platform | Largest HCP data asset (11M+ profiles, LAAD); OCE+/NBA; Salesforce partnership | Dominant data position; commercial platform effectiveness less independently verified |
| **Medscape/WebMD Ignite** | Endemic HCP media + FHIR patient engagement | Largest HCP audience in endemic environment; Ignite on FHIR for patient portals | Survey data (61% of HCPs trust ads more in endemic environments — vendor-cited, source unclear) |

The category crossed $1 billion in annual POC spend in 2024 with 16% YoY growth. OptimizeRx publicly describes itself as having been "pioneers in EHR advertising ushering in AI-based omnichannel transformation."

---

## 7. The Omnichannel Stack: Field + Digital Integration

### Channel Mix Post-COVID

In Q1 2024, only 45% of US physicians made themselves available to pharma companies, with 30% limiting access to just one brand. The channel balance has permanently shifted:

- In-person rep visits: declining; still highest perceived impact per interaction but access severely constrained
- Remote detailing / virtual visits: normalized post-COVID; all major CRM platforms now offer integrated video detailing
- Email / approved email: high volume, low engagement
- POC / EHR-integrated: fastest growing, highest conversion per impression
- Endemic digital (medical journals, Medscape, etc.): high trust, moderate scale
- Programmatic open web: broad reach, lower HCP trust

The omnichannel orchestration challenge: coordinating all of these channels for a single HCP so messaging is coherent rather than overwhelming. A physician who receives a rep visit, two email sequences, programmatic banner ads, and an EHR-triggered ad in the same week has a fragmented brand experience. NBA systems specifically address this by routing engagement to the appropriate channel for each HCP based on their demonstrated preferences and responsiveness patterns.

### Medical Science Liaisons (MSLs)

MSLs are the nominally non-promotional scientific counterparts to sales reps, responsible for peer-level scientific exchange with KOLs and medical affairs. AI is being deployed for MSL support: AI-powered account preparation, real-time clinical literature synthesis, meeting recap generation. The distinction between MSL (scientific exchange) and sales (commercial promotion) is regulatory and ethical; AI that blurs this distinction by feeding the same commercial data intelligence into both functions represents an emerging compliance question not yet formally addressed by FDA.

---

## 8. What the Evidence Actually Shows (vs. What Is Claimed)

### Genuine Consensus
- NPI-level targeting is more efficient than specialty-level targeting — deterministic matching improves reach precision meaningfully
- Trigger-based POC messages (ICD-10 fired) achieve higher HCP engagement rates than non-contextual digital advertising
- AI-powered MLR pre-screening reduces review cycle times (McKinsey 50–65% reduction figure widely cited though methodology unspecified)
- Omnichannel approaches outperform single-channel in HCP engagement metrics per vendor-reported figures

### Genuinely Thin or Contested
- **Script lift attribution**: No independent academic validation of the causal attribution models used to claim 25–44% script lifts. All figures are vendor-generated and methodologically circular
- **EHR-integrated ad clinical impact**: The most invasive targeting modality has the weakest independent evidence base. No peer-reviewed study has assessed whether EHR-embedded advertising produces clinically appropriate or inappropriate prescribing changes
- **AI platform ROI**: The "20:1 ROI" figures cited by platforms are not independently verified. The 95% AI pilot failure rate (MIT) sits alongside McKinsey's 50–65% efficiency gains — both circulate without clear methodology
- **Long-term clinical outcomes**: Whether reduced prescribing costs from generic promotion produce mortality or morbidity improvements is unstudied in this context
- **Privacy risk of SMART on FHIR commercial use**: The legal analysis of whether real-time clinical context triggers constitute PHI use in marketing has not been formally adjudicated

### The Market Failure That Underlies All of This

The infrastructure being described — NPI identity graphs, real-time EHR integration, AI audience modeling, omnichannel orchestration — is funded entirely by pharma commercial interest. There is no equivalent infrastructure investment in genuinely unbiased AI-powered clinical decision support. The Veterans Affairs academic detailing program, NPS MedicineWise in Australia, the Therapeutics Initiative in British Columbia exist as fragments of what a patient-centered alternative could look like. None operates at the scale or with the investment level of the commercial stack.

The market failure is structural: the parties who benefit most from unbiased prescribing — patients and payers — are the least organized to fund the counter-infrastructure. The same SMART on FHIR standard that enables Doceree's Spark could, in principle, deliver comparative effectiveness data and generic substitution prompts at the same prescribing moment. Nobody is paying for that at scale.

---

## Key Takeaways for the Practitioner

1. **Point-of-care is the fastest-growing and highest-conversion channel in pharma digital** — $1B+ annual spend, 15–22% growth, migrating from endemic to EHR-embedded

2. **The SMART on FHIR interoperability framework is the technical unlock** — designed for clinical benefit, now the commercial entry point for EHR advertising; Doceree's Spark is the leading implementation

3. **NPI-level identity resolution is the foundational data primitive** — the AMA Physician Masterfile is the bridge between de-identified Rx data and physician identity; Bid-by-NPI is the 2025 frontier

4. **AI in pharma commercial is maturing fastest in three areas**: trigger-based POC targeting (mature), predictive audience modeling (scaling), MLR/content automation (emerging but contested)

5. **The regulatory environment is in flux** — FDA's 2025 enforcement wave used its own AI surveillance; EHR-integrated advertising remains in a specific regulatory vacuum; international markets prohibit most of what US platforms do routinely

6. **All script lift data is vendor-generated** — there is no independent academic validation of the causal attribution models. This is the most significant evidentiary gap in the entire field

7. **The "AI OS" framing** (Doceree, others) describes genuine platform consolidation — multiple data and activation capabilities on a unified layer — but the specific performance claims remain unaudited
