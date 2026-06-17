# Pharma Brand Measurement: What They Actually Measure and How

This synthesis covers pharma brand measurement rather than campaign attribution. The campaign stack asks: did this exposure generate incremental scripts? The brand stack asks: is this drug becoming the default mental, clinical, and commercial choice for a category of physicians and patients?

## 1. The Pharma Brand-Measurement Stack

Pharma brand measurement works in layers. Brand equity in pharma is not just awareness. It is a durable pattern in which a physician mentally associates a drug with a patient type, clinical situation, risk profile, or treatment sequence, and then repeatedly prescribes it.

| Layer | Core question | Typical KPIs | Data sources | What it misses |
|---|---|---|---|---|
| Attitudinal / brand equity | Does the HCP know, trust, and prefer the brand? | Unaided recall, aided awareness, familiarity, favorability, message association, perceived efficacy/safety, prescribing intent, NPS-style advocacy, share of mind | Custom HCP surveys, syndicated panels, Kantar-style trackers, M3/Medscape panels, IQVIA/DRG-type trackers | Often self-reported; can overstate actual prescribing behavior |
| Behavioral prescribing | Is the HCP actually using the brand? | TRx, NRx, NBRx/NBx, new patient starts, switch-ins, restarts, add-ons, market share, specialty share | IQVIA, Symphony Health, Komodo-like claims/Rx data, internal CRM and sales data | Claims/Rx data does not fully explain clinical appropriateness |
| Prescriber quality / loyalty | Is the prescriber becoming a durable brand user? | Decile rank, writer/non-writer, loyalist vs. trialist, share of eligible patients, retention, prescribing cascade, competitive switching | Longitudinal prescription data, patient-level claims, CRM engagement history | Confounded by patient mix, formulary, access, payer restrictions |
| Investment / share of voice | Are we out-communicating competitors? | Rep call share, detail share, digital SOV, email reach, conference presence, journal SOV, scientific SOV | Veeva CRM/Pulse, media data, CRM activity, field call logs | Exposure is not the same as belief change or patient value |
| Patient journey | Are patients starting, staying, and benefiting? | New patient starts, adherence, persistence, DOT, discontinuation, abandonment, switching, co-pay usage | Claims, hub data, specialty pharmacy data, EHR, patient support programs | Commercial journeys rarely measure true outcomes deeply |
| Economic / payer value | Does the brand sustain price and access? | Net price, rebate-adjusted access, formulary tier, price premium vs. generic/biosimilar, ICER-style value benchmark, LOE erosion | Payer data, price/rebate analytics, ICER reports, CMS, IQVIA | Brand equity can preserve revenue without proving superior outcomes |

IQVIA describes NBRx as based on longitudinal linking of a patient's prescription activity over time and calls it a gold-standard input for longitudinal prescription data in sales-force management. IQVIA also says its prescription data sample covers about 93% of outpatient prescription activity before national projection, which explains why these commercial metrics dominate brand planning.

## 2. The Three Most Important Brand Metrics

### A. New-To-Brand Prescribing: NBRx / NBx

New-to-brand prescribing measures the flow of patients who are newly starting the brand, not just refilling it.

This matters because TRx can look healthy while the brand is actually aging. A mature drug may have strong refill volume but weak new starts. NBRx/NBx answers: are new treatment decisions still breaking our way?

Typical construction:

```text
NBRx = prescriptions where the patient is new to the brand
       after longitudinal lookback across prior therapies
```

Subtypes often include:

- new-to-market / therapy-naive
- switch from competitor
- restart after lapse
- add-on therapy

IQVIA's Brand Analytics fact sheet breaks treated patients and prescriptions into subcomponents such as NBRx, new to market, immediate switch, restart, different, and add-on.

Brand teams like NBRx because it is closer to the physician's current decision than TRx. Refills often reflect old decisions, formulary inertia, or patient persistence. New starts reveal whether the brand is still winning at the moment of choice.

Predictive validity is strongest when paired with persistence and access. A brand with high NBRx but high discontinuation may be generating trial without durable equity. A brand with moderate NBRx but high continuation and low switching may have stronger long-term economics.

### B. Prescriber Loyalty Deciles

Prescriber loyalty deciles measure whether physicians are occasional writers or deep brand adopters.

Typical segmentation starts with the universe of eligible prescribers in the therapeutic class:

| Segment | Meaning |
|---|---|
| Decile 10 | Highest prescribing volume or value |
| Decile 9 | Next highest prescribing volume or value |
| Decile 1 | Lowest measurable prescribing |
| Non-writers | No prescriptions |

Sophisticated teams do not stop at volume. They also measure brand share within each physician's eligible patient pool:

```text
Physician brand loyalty =
Brand X prescriptions or patients
/
All eligible category prescriptions or patients
```

That creates more useful segments:

| Segment | Pattern | Commercial interpretation |
|---|---|---|
| Non-writer | Knows category, never uses brand | Awareness/access/clinical objection problem |
| Trialist | One or few starts, no repeat pattern | Need experience reinforcement |
| Occasional writer | Uses brand for narrow patient type | Opportunity to expand patient archetype |
| Loyalist | High share of eligible patients | Protect and deepen |
| Advocate/KOL | Prescribes and influences peers | Medical/scientific leverage, but compliance-sensitive |

A decile 10 physician with low brand share may be more valuable than a decile 5 physician with high brand share, because the upside is bigger. This is where brand measurement becomes political economy: the brand is trying to convert physician habit, not merely generate one prescription.

### C. Share of Voice / Detail Share

Share of voice measures the brand's share of promotional presence in a defined market.

Typical formula:

```text
Brand SOV =
Brand promotional contacts or spend
/
Total promotional contacts or spend in category
```

In pharma, SOV can include rep calls, details, speaker programs, emails, digital ads, journal ads, congress presence, and scientific share of voice in medical affairs contexts. Veeva's HCP 360 reporting is built from aggregated CRM activity and field engagement data across Veeva CRM instances, showing why CRM-derived engagement has become a major source for field SOV and channel-coordination metrics.

The FMCG rule of thumb is: if SOV exceeds SOM, the brand tends to grow; if SOV trails SOM, the brand tends to shrink. In pharma, that logic applies only partially. Pharma has extra gates: FDA label, clinical guidelines, payer access, prior authorization, safety concerns, and institutional pathways. SOV is a leading indicator, not a law.

## 3. How Physician Brand Identity Forms

The core brand-formation loop looks like this:

```text
Clinical evidence / label
        ↓
KOL interpretation + guideline discussion
        ↓
Rep/detailing + medical education + congress presence
        ↓
HCP mental association:
"Brand X is for this kind of patient"
        ↓
First patient trial
        ↓
Observed outcome / tolerability / access experience
        ↓
Repeat prescribing or abandonment
        ↓
Habit, loyalty, advocacy, or switching
```

There is independent evidence that marketing affects prescribing, but the evidence is stronger for association and behavioral influence than for clean causal proof of brand identity. A systematic review in *Annals of Internal Medicine* found that industry payments were associated with increased prescribing of the paying company's drug, increased prescribing costs, and increased branded prescribing. A *JAMA Internal Medicine* study found industry payments associated with higher rates of brand-name statin prescribing.

The best way to think about durability:

| Stage | Formation mechanism | Metric |
|---|---|---|
| Launch / early adoption | KOLs, clinical data, rep education, payer access | Awareness, trial, NBRx, early adopter penetration |
| Growth | Repeated successful patient starts | NBRx share, physician conversion, repeat prescribing |
| Maturity | Habit and patient archetype ownership | Loyalty deciles, retention, share of eligible patients |
| Competitive pressure | Defense against new entrants | Switch-out rate, message association, SOV vs. competitor |
| LOE / generic entry | Brand equity fights economic substitution | Residual branded share, price premium, loyalist retention |

The key commercial insight: pharma brand equity becomes strongest when the physician does not merely remember the brand, but remembers the patient type.

## 4. Brand Equity Economics: Price Premium, LOE, and Generic Erosion

Pharma brand equity has an economic expression: the ability to sustain volume, net price, access, or patient demand against alternatives.

At loss of exclusivity, the normal small-molecule pattern is steep erosion because generic substitution changes the economics. IQVIA's LOE research compares brand prices before exclusivity loss with generic prices after entry, reflecting the standard industry view that LOE fundamentally changes the price structure. Academic work on generic entry finds that higher pre-entry sales and shorter exclusivity attract more generic entry, increasing competitive pressure.

Brand equity can still matter after LOE in some cases:

| Market type | Brand equity persistence |
|---|---|
| Small molecule, easy substitution | Usually weak; payer/pharmacy substitution dominates |
| Specialty drug | Stronger; physician comfort and patient support matter |
| Biologic / biosimilar | Stronger than simple generics; interchangeability, device, immunogenicity perception, and institutional protocols matter |
| High-risk therapy area | Stronger; physicians may resist switching stable patients |
| Strong patient support / hub model | Stronger; brand is partly service infrastructure |

Co-pay cards complicate the economics. The independent literature shows they can improve affordability and adherence in some contexts, but they can also reduce generic substitution and raise system costs. A Georgetown policy brief summarizes evidence from Dafny, Ody, and Schmitt that coupons boosted branded sales by over 60% by reducing generic use at treatment initiation.

This is the central tension: brand equity can look commercially successful while being socially inefficient if it preserves use of a higher-priced brand where a clinically equivalent lower-cost option exists.

## 5. Pharma vs. FMCG Brand Measurement

Pharma resembles Coca-Cola or Calvin Klein in one big way: brands compete for mental availability, salience, associations, and repeat behavior. But pharma diverges sharply because the buyer, consumer, payer, and decision-maker are split.

| Dimension | FMCG | Pharma |
|---|---|---|
| User | Consumer | Patient |
| Decision-maker | Consumer | Physician, payer, institution, patient |
| Payer | Consumer | Insurer, PBM, patient, employer, government |
| Brand funnel | Awareness -> consideration -> purchase -> loyalty | Awareness -> clinical belief -> trial -> prescribing habit -> patient persistence |
| Promotion | Broad persuasion | Regulated, label-constrained, evidence-framed |
| Switching | Often easy | Constrained by safety, formulary, adherence, substitution laws |
| Brand equity | Emotional + functional | Clinical + economic + institutional + emotional |
| Outcome metric | Sales, share, loyalty | Prescriptions, starts, persistence, outcomes, access |

Ehrenberg-Bass ideas apply best to mental availability, reach, and salience. They apply less well to clinical markets where prescribing is shaped by evidence hierarchy, guidelines, access restrictions, risk tolerance, and institutional pathways.

The pharma version of "brand X person" is not "I wear Calvin Klein." It is:

> For this patient profile, in this disease state, after this prior therapy, Brand X is my default.

That is much more constrained, but also much more valuable.

## 6. The Measurement Gap

The biggest flaw in pharma brand measurement is that the commercial stack is very good at measuring adoption, but much weaker at measuring patient welfare.

Traditional brand KPIs answer:

- Did physicians know it?
- Did physicians believe it?
- Did physicians prescribe it?
- Did patients start it?
- Did patients stay on it?
- Did the brand retain share and price?

A patient-centered brand stack would ask:

- Did the right patients receive it?
- Did outcomes improve versus alternatives?
- Were adverse events reduced?
- Did adherence improve because the therapy was clinically better or merely subsidized?
- Did total cost of care improve?
- Did equity/access improve?
- Was the brand's higher price justified by incremental benefit?

This gap is not theoretical. ICER's value framework explicitly aims to evaluate health interventions through rigorous, transparent evidence reports to support a more sustainable, high-value health system. Meanwhile, studies of heavily promoted drugs have questioned whether promotion aligns with therapeutic value. A BMJ-linked analysis argued that the most promoted drugs were less likely than top-selling or top-prescribed drugs to be effective, safe, affordable, novel, or genuine therapeutic advances.

That is the hard critique: brand equity is often optimized as commercial memory, not clinical value.

## 7. AI and Programmatic Targeting: What It Optimizes

AI in pharma commercial teams usually plugs into the behavioral and investment layers first:

| AI use case | Optimized KPI | Risk |
|---|---|---|
| Next-best-action | Engagement, NBRx, call response | Optimizes reachable/responders, not necessarily highest clinical need |
| HCP segmentation | Decile movement, loyalty, switch risk | Can reinforce historical prescribing bias |
| Trigger-based targeting | New diagnosis, competitor switch, formulary change | May over-prioritize commercial events |
| Message personalization | Email opens, rep effectiveness, content engagement | Engagement becomes surrogate for clinical belief |
| Media mix modeling | Budget allocation, SOV, incremental scripts | Hard to connect to patient outcomes |
| KOL mapping | Influence, peer network diffusion | Compliance and conflict-of-interest concerns |
| Patient journey analytics | Starts, adherence, persistence | Confounds affordability, access, and true therapeutic fit |

The targeting stack sees some brand KPIs well: NBRx, decile movement, switch-ins, retention, SOV, and engagement frequency. It sees other KPIs poorly: real-world outcomes, clinical appropriateness, patient quality of life, adverse-event burden, and total cost of care.

That is where the next generation of measurement should go: connect commercial brand metrics to patient-centered outcomes, not just to scripts.

## Bottom Line

Pharma brand measurement is a longitudinal belief-and-behavior system. Campaign attribution measures short-term lift. Brand measurement tracks whether a drug becomes the physician's default choice for a patient archetype, whether that choice persists, whether it survives competition and LOE, and whether it supports a price premium.

The strongest commercial KPIs are:

- NBRx / new patient starts: is the brand winning current treatment decisions?
- Prescriber loyalty / decile movement: are physicians becoming durable brand users?
- Share of voice / detail share: is the brand maintaining enough presence to shape mental availability?

The weakest part of the system is not measurement sophistication. Pharma measures commercial behavior extremely well. The weakness is alignment: the dominant KPIs measure brand adoption and revenue durability far better than they measure whether the brand improves patient welfare compared with alternatives.
