# Conversation Summary
## Pharma Marketing AI + MoE vs. Ensemble Learning
### June 16, 2026

---

## Part 1: Origin — Graham Wilkinson and Doceree

The conversation began with an email from Graham Wilkinson, former KINESSO colleague, now Chief Innovation Officer at Doceree (150 John F. Kennedy Pkwy, Short Hills NJ). Graham suggested "interesting territories to explore."

Research established what Doceree is: a HIPAA-certified programmatic advertising platform for pharma/life sciences brands targeting healthcare professionals (HCPs). Core product is a DSP/SSP/Ad Server/DMP stack with 150+ direct EHR integrations including Epic and Oracle Cerner. Spark product uses SMART on FHIR for in-workflow delivery. Co-Pay.com (2025) extends into patient affordability programs. Frost & Sullivan 2026 Global Technology Innovation Leadership Recognition (noted: paid-for recognition). Founded 2020, Short Hills NJ.

Decision reached: Graham's "interesting territories" likely refers to AI education/literacy for HCPs or content/curriculum partnership. Worth a conversation to clarify.

---

## Part 2: Research Infrastructure Built

### Documents Produced

**pharma-marketing-evidence-synthesis.md** — Independent evidence on traditional pharma marketing effectiveness. Eight sections covering detailing, meals/gifts, speaker fees, branded vs. generic steering, DTC advertising, information quality/publication bias, stakeholder benefit analysis, regulatory landscape.

**pharma-ai-hcp-marketing-research-prompt.md** — Deep research prompt with seven threads covering programmatic HCP targeting, EHR integration, prescribing data analytics, pharma-specific AI, omnichannel, regulatory/privacy, and emerging terrain.

**pharma-ai-hcp-marketing-synthesis.md** — Full research synthesis run independently from web sources. Eight sections covering market scale, NPI targeting architecture, EHR integration mechanics, prescribing data analytics, AI capabilities inventory, regulatory landscape 2025-2026, platform landscape comparison, evidence quality assessment.

**moe-vs-ensemble-research-prompt.md** — Deep research prompt with eight threads covering MoE theoretical foundations, ensemble learning theory, central architectural distinctions, modern MoE in LLMs, ensemble methods in practice, decision framework, commercial AI labeling problem, and the correlation question.

**moe-vs-ensemble-synthesis.md** — Full research synthesis on MoE vs. ensemble learning run independently from web sources.

### Three External Documents Reviewed

1. **Pharma Marketing Effectiveness (evidence synthesis)** — Serious peer-reviewed literature synthesis. Added specific odds ratios (rosuvastatin OR 1.18, nebivolol OR 1.70, olmesartan OR 1.52, desvenlafaxine OR 2.18 from a single meal under $20), Johns Hopkins Medicare estimate ($1.7B excess spending from brand-over-generic requests in one year, patients paying $270M more than necessary), and the antidiabetic prescribing working paper (~$30 increased drug cost per marketing dollar received).

2. **AI-Driven Programmatic HCP Marketing (technical architecture)** — Most technically precise document. Provided full data flow diagram, CDS Hooks JSON payload showing exactly how a co-pay card fires when a physician prescribes metformin, MoE vs. ensemble distinction with correct mathematical treatment, platform landscape comparison table, regulatory risk matrix. Named Doceree specifically and described Spark accurately.

3. **AI-Driven Programmatic HCP Marketing (executive synthesis)** — Most intellectually honest of the three. Added: FTC antitrust challenge to IQVIA's acquisition of DeepIntent's parent (strongest independent validation of market importance), GoodRx FTC enforcement precedent (first Health Breach Notification Rule action, health-data-to-advertising pipelines as enforcement priority), Sorrell v. IMS Health Supreme Court ruling (why states can't restrict NPI targeting data — First Amendment protection), ONC governance vacuum framing (standards opened the door, institutions decide what walks through it).

---

## Part 3: The Pharma Marketing Evidence — Key Findings

### Traditional Marketing (Evidence Quality: High)

- 36-study systematic review: 89 of 101 analyses positive for association between payments and prescribing of paying company's drug
- Single sponsored meal under $20 associated with significantly higher prescribing across four drug classes; dose-response pattern confirmed
- Massachusetts disclosure law led to prescribing declines in several drug classes relative to neighboring states
- Academic medical center detailing restrictions produced statistically significant prescribing reductions
- Specialists are not immune: cardiology, oncology, rheumatology all show marketing influence
- KOL payments influence not just paid physician but colleagues in referral/information network
- Disclosure alone is insufficient; access restrictions are more effective

### Digital/EHR Marketing (Evidence Quality: Low-Medium)

- POC advertising crossed $1B annual spend in 2024; 171% growth 2019-2023; 15-22% annual growth
- All script lift figures (19-44%) are vendor-generated with no independent academic validation — the single most significant evidentiary gap in the field
- SMART on FHIR designed for clinical benefit, repurposed for commercial advertising
- AMA Resident and Fellow Section formally opposed pharma ads in EHR systems at teaching institutions
- FDA 2025 enforcement wave: 200+ enforcement letters, AI-powered surveillance — but EHR-integrated advertising remains in a specific regulatory vacuum

---

## Part 4: The Political Economy Analysis

This was the most analytically novel part of the conversation. Several interlocking observations developed:

### The Structural Anomaly

In normal markets the person seeing the ad is the person paying for the product. In pharma:
- The person seeing the ad (physician) does not pay for the product
- The person paying for the product (patient/insurer) does not see the ad
- The physician makes the purchase decision but bears none of the cost consequences
- The patient bears all cost consequences but makes none of the decisions

**"The person paying for it is not at the table."** — identified as the sharpest summary of the entire system.

### The Lunch Table Analysis

Parties at the table: the rep (paid to be there), the physician (enjoys it), the pharma brand (interests represented). Not at the table: the patient, the insurer, the employer, the taxpayer — all of whom pay. The people funding the lunch are the only parties with no representation, no knowledge it's happening, and no mechanism to object.

### The Rep Dynamic

- Physical attractiveness is a documented selection criterion for pharma reps (Journal of Health Economics 2011)
- Mechanism is halo effect (credibility/trustworthiness transfer), not primarily sexual attraction
- Historical profile: four-year degree often not in science, athletic/cheerleading background overrepresented, high social fluency
- The rep is a rational labor market actor: accurately identified that social skills and appearance command a premium in this specific market that other markets don't price comparably
- "Not many girls grow up thinking I'd like to have lunch for a living" — acknowledged as accurate and unsentimental; reps who are self-aware about the transaction are making financially sophisticated decisions
- The physician is the one being manipulated, not the rep

### The Asymmetric Information Problem

The rep has CRM data showing prescription volume by physician updated monthly from IQVIA/Symphony Health claims data. Before a visit they see how many scripts Dr. Smith wrote last month. After a visit they see if the number moved. The physician has no idea the score is being kept. Regional managers review "call effectiveness" — correlation between rep activity and prescribing trends. Physicians who respond get more attention, better samples, more invitations, more speaker fee opportunities. The system learns which physicians are influenceable and concentrates resources accordingly.

**Complete asymmetry**: rep knows the score, physician doesn't know the game is being played.

### The Co-Pay Coupon Mechanism

Eliminates the one patient price-signal moment (pharmacy counter) where the patient might ask about generics. Patient pays $0 and feels grateful. Physician feels helpful. Insurer/employer absorbs the full branded cost. The person paying is not at the table but now can't even see the bill.

### The Black Box Persona Modeling Problem

This was the most novel analytical contribution of the conversation. The question raised: can persona models be built identifying physician susceptibility profiles?

The answer: yes, and this is what AI targeting systems are built to do, though the industry doesn't describe it in those terms.

**The data exists for physician persona construction:**
- Open Payments data (public): which physicians accept meals, from whom, how much
- NPI-level prescribing response data: whether prescribing shifted after payment activity
- CRM relationship history: which rep has the relationship
- Behavioral signals: digital engagement, journal reads, CME completion

**The rep-characteristic proxy problem:**

Computer vision can extract estimated age, gender, ethnicity, and attractiveness ratings from photos automatically. Pharma companies have complete HR records on reps including photos. CRM data links each rep to each physician relationship. Connecting these datasets would give:
- Rep demographic profile (age, gender, ethnicity, appearance proxied from photo)
- Physician prescribing response correlated to that rep's profile
- A predictive model for which rep characteristics drive prescribing response for which physician segment

Nobody has to write "assign attractive young women to male cardiologists." The model learns it and outputs rep assignment recommendations without any discriminatory variable being explicitly named.

**The black box architecture:**

The model doesn't need labels. Train on historical pairings where prescribing increased. The model learns the pattern. The output is just: "assign rep ID 4471 to physician NPI 1234567890." The reason is buried in 50 million parameters.

**Layers of deniability:** pharma brand → platform → data broker → CRM vendor. Nobody is responsible. Everyone is technically accurate. The discrimination is distributed across four commercial relationships with no single point of accountability.

**Three victims:**
1. The rep — sorted by physical characteristics for territory assignment through "neutral optimization"; less conventionally attractive reps get worse territories, managed out, with no named cause
2. The physician — profiled for psychological susceptibility without consent or knowledge; matched to the relationship stimulus most likely to produce desired prescribing behavior
3. The patient — receives a prescription shaped not by clinical evidence but by a targeting model that identified their doctor as susceptible to a specific relationship stimulus

**Current regulatory gap:** FDA OPDP regulates ad content. Sunshine Act requires disclosure of payments. HIPAA governs patient data. Nobody regulates targeting model architecture, proxy discrimination in commercial AI, or exploitation of physician psychological susceptibility.

The EU AI Act would potentially require high-risk AI systems in healthcare to be transparent, auditable, and non-discriminatory. No US equivalent applied to commercial healthcare AI.

**Identified as a real gap nobody has formally named yet.**

---

## Part 5: MoE vs. Ensemble Learning — The Technical Deep Dive

This emerged from examining Doceree's claim to use "adaptive mixture of experts" architecture. The conversation developed into a technically substantial treatment of what MoE actually is vs. what commercial platforms implement.

### The Core Distinction Established

**Genuine sparse MoE:**
- Token-level routing within a single forward pass
- All experts share identical input/output dimensionality (standardized output space)
- Joint end-to-end training — experts and gating network co-adapt through shared backpropagation
- Sparse activation: top-k experts per token (k=1 or 2 out of potentially 256)
- Sub-linear compute scaling: large parameter capacity at small active compute footprint
- Emergent specialization through routing-induced differential exposure during training

**What commercial pharma ad-tech platforms actually run:**
- Multiple separate ML models (propensity scoring, bid optimization, compliance checking)
- Rule-based or learned aggregation combining heterogeneous outputs
- No joint training, no co-adaptation
- Heterogeneous output spaces requiring engineered reconciliation
- A linear meta-learner combining the outputs
- This is ensemble learning with model stacking — a legitimate effective approach, not MoE

### The Output Standardization Insight

Identified as the clearest statement of what MoE architecturally buys: all experts share identical input/output dimensionality, making the weighted combination $y = \sum G(x)_i E_i(x)$ a clean weighted sum in a shared vector space. This is mathematically possible only because outputs are commensurable. In ensemble methods, outputs are often heterogeneous (probability vector, score, log-odds) requiring a separate reconciliation layer that introduces information loss and prevents end-to-end joint optimization.

### The Correlation Problem

**Ensemble perspective:** Models trained on the same data learn the same structural regularities, share the same blind spots, make correlated errors on the same hard cases. No algorithmic diversity removes shared data biases.

**MoE perspective:** Routing-induced specialization creates functional diversity. But joint training through shared backpropagation and shared loss function creates its own correlation. Load balancing — required to prevent expert collapse — actively works against specialization by encouraging uniform routing, driving experts toward similar representations.

Empirical finding: expert similarity scores exceeding 99% across diverse inputs documented in some trained MoE models. MoE doesn't solve the correlation problem — it relocates it from "same training data" to "same training objective plus load balancing pressures."

### What MoE Experts Actually Specialize In

This is empirically surprising: not semantic domains (math, code, biology) but syntactic and computational patterns. Token routing correlates with token type more than domain. A punctuation token gets routed differently from a verb regardless of what the text is about. Expert similarity scores above 99% documented. Domain specialization exists but is partial and inconsistent.

The mechanism: the gating network learns what minimizes loss. Token type and syntactic role predict accuracy more reliably than semantic domain from a single token's hidden state. The specialization is structural, not semantic.

DeepSeek-V3's approach (256 fine-grained experts rather than 8) forces deeper specialization by making each expert small enough to require narrow focus. Whether this fully solves representational redundancy is an open research question.

### The Load Balancing Problem

Without intervention, routing collapses to 1-2 experts that receive most gradient and improve fastest. Solutions:

- **Auxiliary loss** (Switch Transformer): penalizes routing imbalance but introduces interference gradients; tradeoff between load balance and model quality
- **Noisy top-k gating** (Shazeer 2017): Gaussian noise added to routing scores, forcing exploration
- **Auxiliary-loss-free balancing** (DeepSeek): dynamic bias term added to routing scores, updated outside backpropagation via sign gradient descent; achieves better load balance and better model quality than auxiliary loss approaches

### The Tabular Data Exception

Grinsztajn et al. (NeurIPS 2022): tree-based models remain state-of-the-art on medium-sized tabular data even without accounting for superior speed. The best methods on tabular data share two attributes: they are ensemble methods (bagging or boosting), and the weak learner is a decision tree.

**Critical implication for pharma targeting:** NPI propensity scoring is exactly this problem type — structured tabular prediction. Ensemble methods are not a degraded substitute for MoE in this domain. They are likely the genuinely superior architecture. The MoE terminology in commercial vendor marketing reflects scale ambitions more than current deployment reality.

### Modern MoE Landscape

| Model | Total Params | Active Per Token | Key Innovation |
|---|---|---|---|
| Mixtral 8x7B | 46.7B | 12.9B | Standard sparse MoE, mainstream open-source |
| DeepSeek-V3 | 671B | 37B | 256 fine-grained experts, auxiliary-loss-free balancing, shared expert isolation |
| Switch Transformer | 1.6T | Variable | Top-1 routing, first trillion-parameter MoE |
| GPT-4 (rumored) | ~1.8T | ~280B | Unconfirmed architecture |

### Novel Methodological Contribution: Finding Natural N

This was the most original research contribution developed in the conversation — not in existing literature.

**The proposal:** Use routing geometry metrics as the primary criterion for N selection in MoE hyperparameter optimization rather than validation loss alone.

**The pipeline:**
1. Train MoE models with varying N on representative data sample
2. Measure not just validation loss but: expert utilization rate, routing entropy, inter-expert representational similarity (cosine similarity between expert weight matrices), routing stability
3. Plot these against N — find the elbow where adding experts stops producing meaningfully distinct routing behavior
4. The inflection point in inter-expert similarity is the empirical estimate of natural N

**Why practically tractable:** Small datasets mean fast epochs. N is discrete with a narrow interesting range (2-64). Runs are independent and embarrassingly parallel. Full sweep from N=2 to N=64 with 3 seeds each can complete in hours on a single GPU machine. The routing geometry metrics stabilize before full convergence, enabling early stopping.

**The deeper insight:** The natural N from routing geometry is equivalent to asking how many meaningfully distinct subpopulations the data contains. For physician behavioral prediction: how many genuinely distinct prescriber archetypes exist in the data. If the answer is 6, that's domain knowledge independent of the hyperparameter value — a finding that transfers to downstream analysis.

### Novel Methodological Contribution: Semantic Mapping of Expert Clusters

**Once natural N is found, map the clusters to human-interpretable descriptions:**

- **Feature importance per expert** — SHAP values showing which features most predict routing to each expert
- **Prototype identification** — records with highest routing weight for each expert; most archetypal members
- **Contrastive analysis** — feature distributions of Expert A vs. Expert B inputs; what distinguishes them
- **LLM augmentation** — describe prototypes and feature importance to an LLM for semantic characterization; not to generate findings but to articulate patterns in human language
- **External validation** — check whether discovered segments correspond to known typologies (e.g., existing physician archetype literature); temporal replication across years; cross-dataset replication across therapeutic areas

**The full pipeline:**
1. Structural discovery — hyperparameter search with routing geometry finds natural N
2. Semantic mapping — feature importance, prototypes, contrastive analysis characterize each cluster
3. Validation — external knowledge, expert review, temporal and cross-dataset replication confirm clusters are real

**Why this is novel:** The pieces exist separately in different literatures. The end-to-end methodology assembled as a principled approach to interpretable subpopulation discovery using supervised MoE as the computational engine does not exist in published form. It would make a practical methodology paper — not a fundamental theoretical advance but the kind of contribution that gets adopted because it solves a real problem with a feasible compute profile.

---

## Part 6: Documents Produced

All files in `/mnt/user-data/outputs/`:

1. `pharma-ai-hcp-marketing-research-prompt.md` — Seven-thread deep research prompt for pharma digital marketing
2. `pharma-ai-hcp-marketing-synthesis.md` — Full research synthesis, eight sections
3. `moe-vs-ensemble-research-prompt.md` — Eight-thread deep research prompt for MoE vs. ensemble
4. `moe-vs-ensemble-synthesis.md` — Full research synthesis, nine sections, grounded in current sources

---

## Part 7: Key Takeaways for Graham Conversation

1. **Doceree's technical claims are partially inflated**: "Adaptive mixture of experts" describes ensemble learning with a meta-learner, not genuine sparse MoE architecture. This is effective commercial ML but not the architectural claim the terminology implies.

2. **The script lift attribution problem**: Every platform claims 19-44% script lift. None is independently verified. If Doceree's value proposition rests on that number, understanding the attribution methodology is the right question.

3. **EHR-integrated advertising is in a regulatory vacuum**: FDA's 2025 enforcement wave hasn't touched it. The SMART on FHIR channel that Spark uses was designed for clinical benefit. There is no specific prohibition on commercial use. This is simultaneously an opportunity and a liability.

4. **The market failure framing**: The same SMART on FHIR infrastructure that delivers Doceree's branded co-pay cards could deliver generic substitution prompts and comparative effectiveness data. Nobody funds the latter because there's no commercial return. This is the most interesting conversation to have with Graham if he's open to it — whether the infrastructure he's building could be redirected toward something patient-centered.

5. **The black box persona problem**: The AI targeting layer is specifically optimizable toward physician psychological susceptibility profiles using legally obtained data with no named discriminatory variable. Nobody in the industry is asking publicly what the targeting models have learned about physician susceptibility. This is the next paper someone needs to write.

---

## Part 8: Open Threads / Pending

- Meeting with Graham Wilkinson — background research complete; decision on whether Humanitarians AI / Northeastern collaboration is appropriate given commercial model
- The novel N-finding + semantic mapping methodology — potential paper contribution
- The physician susceptibility persona paper — nobody has named this formally yet; the black box encoding of psychological susceptibility profiles in commercial AI targeting is an unaddressed gap across all three reviewed documents
