# Chapter 5 — The Evidence Problem · Research Notes

> Gathering notes only (no chapter prose). Format A–G per Research Gatherer spec.
> Chapter spine: distinguish peer-reviewed evidence from vendor-generated claims; rate evidence
> quality per channel; association ≠ causation in promo analytics; the detailing literature; the
> meal/Open-Payments findings; the EHR-ad evidence gap; attribution circularity.
> Primary reuse sources: `pantry/pharma-marketing-evidence-synthesis.md` (deep on detailing/meals/
> EHR gap) and `pantry/pharma-ai-hcp-marketing-synthesis.md` (deep on attribution circularity).
> Web-verified 2026-06-16; every factual claim sourced or [FLAG]'d.

---

## A. Conceptual foundations

**The core distinction the chapter teaches: association vs. causation in promotional analytics.**
Almost every effectiveness claim in pharma HCP marketing is an *association* — exposed physicians
prescribe more than unexposed physicians — presented as if it were a *causal* claim — the exposure
*caused* the additional prescribing. The gap between the two is the entire chapter.

Four mechanisms make the association systematically *over-state* causal effect, all of which a Fellow
must be able to name:

1. **Selection / targeting on the outcome.** Platforms target high-propensity prescribers (high
   deciles, rising NBRx, on-label patient mix). Those physicians were *already* going to prescribe
   more. Measuring their post-exposure prescribing and attributing the delta to the ad confounds the
   targeting signal with the treatment effect. (This is the Ch 8 propensity-vs-incrementality
   inversion previewed here.)
2. **Attribution circularity (the structural fraud risk).** The platform that *serves* the ad also
   *measures* the lift, using the same NPI-linked data infrastructure for both. Targeting and
   measurement are not independent. There is no firewall between the party with a commercial interest
   in a high number and the party producing the number. (Source: pharma-ai synthesis §1 "Attribution
   Problem" — "inherent measurement circularity… no independent academic literature validating the
   attribution models.")
3. **Absence of a control / counterfactual.** "Lift" without a randomized or quasi-randomized holdout
   is a before/after or exposed/unexposed comparison, not an estimate of the counterfactual (what the
   same physicians would have prescribed *un*exposed). See Ch 8.
4. **Publication / reporting asymmetry.** Vendor case studies report wins; nobody publishes the
   campaign that did nothing. The industry-trial literature shows the same disease at the source of
   the evidence base (selective outcome reporting, ghostwriting — see B failure case).

**Evidence-quality taxonomy (the gradeable artifact for this chapter).** A defensible per-channel
rating needs a ladder. Two compatible scaffolds:
- *Study-design strength* (descending causal credibility): RCT / pre-registered experiment >
  natural experiment with credible identification (DiD, RDD, IV) > matched observational/propensity
  > unadjusted exposed-vs-unexposed > vendor case study / testimonial.
- *Source independence*: independent peer-reviewed > government/nonprofit > industry-funded but
  peer-reviewed > vendor white paper / case study (un-refereed, commercial interest).
A claim's grade is roughly the *minimum* of its design strength and its source independence. The
19–44% EHR script-lift claims score low on **both** axes — unadjusted exposed-vs-unexposed design,
vendor-produced — which is the chapter's punchline.

---

## B. Domain examples + a failure case

**Worked examples (the channels, ranked by independent evidence quality):**

- **Detailing (sales-rep visits) — STRONG independent evidence it works.** Oldest, most-studied
  tactic. Systematic reviews find physicians who receive industry information, rep contact, or free
  samples increase prescribing of the paying company's drugs. The canonical *Annals of Internal
  Medicine* finding: physicians' belief that accepting payments won't affect their practice is not
  well-founded — measurable prescribing changes despite self-reported immunity (the third-person
  effect: everyone thinks they're immune; the data says no one is). (Source: evidence synthesis §1.)
- **Meals / gifts — STRONG, dose-response.** *JAMA Internal Medicine*, 20 June 2016 (DeJong et al.):
  linked CMS Open Payments to Medicare Part D prescribing for the most-prescribed branded drug in
  four classes — rosuvastatin (Crestor), nebivolol (Bystolic), olmesartan (Benicar), desvenlafaxine
  (Pristiq). n = 279,669 physicians; 63,524 relevant meal payments (Aug–Dec 2013). Finding: receipt
  of even a **single** industry-sponsored meal (mean value < $20) was associated with higher rates of
  prescribing the promoted brand; prescribing rate rose with the number/value of meals (dose-
  response). [VERIFIED via web 2026-06-16: jamanetwork.com 2528290; pubmed 27322350.] *Important
  honesty caveat: this is observational/association — physicians who take meals may differ from those
  who don't. The dose-response and single-meal threshold strengthen but do not prove causation.*
- **Academic detailing (the counter-model) — STRONG RCT evidence it works.** Unbiased educational
  outreach from non-commercial teams, same high-touch format, opposite agenda. [VERIFIED 2026-06-16]:
  recent systematic review (*JAMA Network Open*, 2024/2025; PMC12543401 / jamanetworkopen 2828799) of
  118 randomized + non-randomized studies; among 36 lowest-risk-of-bias studies, 25 (69%) showed
  significant improvement in ≥1 prescribing behavior, median absolute change 4.0% in the intended
  direction. The older 2007 Cochrane meta-analysis (69 RCTs) found median absolute change ~5.6%.
  Teaching value: same channel, rigorous evidence, *opposite funder incentive* — isolates that the
  format is a vehicle, the agenda is the variable. Chronically underfunded vs. commercial detailing
  (VA program is the main scaled example).
- **Safety-information exception (detailing can inform, not just persuade).** A study of Crestor (a
  statin contraindicated in elderly/Asian patients) found detailing *reduced* prescribing to
  contraindicated patients — evidence the informative function is real, but bundled in the same visit
  as the persuasive function. Pharma funds detailing to raise scripts; the safety benefit is real but
  incidental. (Source: evidence synthesis §1.)
- **EHR / point-of-care advertising — the EVIDENCE GAP (the chapter's center of gravity).** The
  fastest-growing channel with the thinnest independent evidence. Vendor-reported script lifts span
  4%–44% depending on therapy/channel; OptimizeRx reports 19–25% from NPI-level analysis; a vendor
  breakdown cites ~11.9% (informational messages, 8 programs) and ~11.5% (brand + savings offer,
  27 programs). [VERIFIED 2026-06-16 — but note: *the web search for "independent peer-reviewed
  evidence" returned almost exclusively vendor marketing pages (OptimizeRx, PulsePoint, WebMD Ignite,
  ConnectiveRx), which is itself the finding.*] **No independent, peer-reviewed study validates the
  causal attribution behind these numbers, and no peer-reviewed study has assessed whether EHR-
  embedded ads produce clinically appropriate vs. inappropriate prescribing.** This is the single
  largest open validation gap in the field (sources: both syntheses; evidence synthesis "Evidence
  Quality Notes"; pharma-ai synthesis §8 "Genuinely Thin or Contested").

**Failure case (the discipline made vivid — the corruption of the evidence base at its source).**
*GlaxoSmithKline Study 329 (paroxetine/Paxil in adolescents).* The published report claimed
paroxetine was "generally effective" for adolescent depression; the conclusion resulted from post-hoc
outcome switching (the pre-specified primary outcomes were negative). The drug was ineffective and
carried suicidality risk in the studied population. The paper was not corrected/retracted for years;
prescribing continued in the interim. Lesson for the Fellow: the problem is not only vendor case
studies — the *peer-reviewed literature itself* is contaminated where industry controls trial design,
analysis, and publication. (Source: evidence synthesis §5.) Reinforcing datum [VERIFIED 2026-06-16,
_lib_science-fictions]: in the antidepressant literature, 98% of positive trials were published vs.
48% of negative ones; correcting for publication bias + outcome switching collapsed an apparent
2-to-1 efficacy signal — "the drugs still work, but perhaps half as well as you believed." Only ~31%
of medical meta-analyses even check for publication bias.

---

## C. Connections / dependencies

- **Depends on Ch 2** (lift vs. brand): you cannot rate a claim's evidence until you know which
  dependent variable it asserts to move. "44% lift" is a lift claim; it needs a control. A brand-
  association claim needs a different instrument (Ch 9).
- **Depends on Ch 3–4** (identity graph + the AI stack): attribution circularity is only legible once
  the Fellow understands that the *same* NPI-linked claims infrastructure powers both targeting and
  measurement.
- **Sets up Ch 6–8 directly.** Ch 6 (ensembles) and Ch 7 (MoE) answer "is the model real?"; Ch 8
  (uplift/incrementality) answers "is the *lift* real?" — the formal resolution of the association-vs-
  causation problem opened here. Ch 5 is where the Fellow first feels the need for a control group.
- **Feeds Ch 11–12** (the Evidence Ladder + identification strategies): the per-channel evidence
  taxonomy here is the conceptual seed of the lab's Evidence Ladder (Level 0 "interesting claim" →
  Level 5 "client-validated incremental impact"). The detailing-restriction natural experiment
  (see Ch 8 notes) is a Ch 12 identification template.
- **Cross-cuts the whole book's thesis**: "pharma built the most sophisticated targeting
  infrastructure in any regulated industry while leaving almost none of its effectiveness claims
  independently validated." Ch 5 is where that thesis is proven on the evidence base itself.

---

## D. Current state (settled / contested / key refs / last-3-yr)

**Settled (strong consensus, multiple systematic reviews):**
- Detailing changes prescribing toward the promoted drug; physicians under-perceive their own
  susceptibility.
- Meals/gifts associate with branded prescribing, dose-response (JAMA Intern Med 2016).
- Academic detailing improves evidence-based prescribing (Cochrane 2007; JAMA Netw Open 2024/25).
- Disclosure alone (Sunshine Act, 2010) did **not** change physician COI behavior — necessary, not
  sufficient. (Source: evidence synthesis §1.)
- Generic bioequivalence: FDA review of >2,000 pharmacokinetic trials found no significant branded-
  vs-generic difference — so branded preference is largely marketing-driven, not clinical. (Source:
  evidence synthesis §7.) [VERIFY the exact trial count before publication.]

**Contested / thin (the open gaps — the Fellow's opportunity):**
- **EHR/POC script-lift attribution**: vendor-generated, methodologically circular, no independent
  validation. *Largest open methodological problem in the field.*
- **Clinical appropriateness of EHR-driven prescribing changes**: unstudied independently.
- **Whether the 19–44% range reflects real incremental scripts or targeting/selection**: untested
  with a control.

**Key references (verify exact wording/numbers in ACCURACY-REVIEW pass):**
- DeJong C, et al. "Pharmaceutical Industry–Sponsored Meals and Physician Prescribing Patterns for
  Medicare Beneficiaries." *JAMA Intern Med.* 2016;176(8):1114–1122. [VERIFIED exists.]
- Academic detailing systematic review, *JAMA Netw Open* 2024/25 (118 studies; 69%/4.0% among
  lowest-bias). [VERIFIED exists; confirm authors + exact year.]
- O'Brien MA, et al. Cochrane review of educational outreach visits, 2007 (69 RCTs; ~5.6% median).
  [VERIFY exact figure.]
- *Annals of Internal Medicine* systematic review on industry payments + self-assessment gap.
  [FLAG: synthesis cites it without a year/author — locate the specific citation before use.]
- GSK Study 329 reanalysis: Le Noury J, et al. *BMJ* 2015 (RIAT restoration). [FLAG: synthesis
  references the case, not this citation — add it.]
- All EHR script-lift figures: OptimizeRx / Doceree / vendor case studies — label as vendor-sourced,
  un-refereed, in every use.

**Last-3-year movement:** academic-detailing evidence refreshed (2024/25 review); FDA 2025 enforcement
wave (200+ letters) targeted DTC content but **left EHR-integrated advertising in a regulatory gray
zone** — the evidence gap and the regulatory gap coincide (pharma-ai synthesis §5). [VERIFIED
qualitatively via web.]

---

## E. Teaching considerations

- **Opening (from TIKTOC):** a vendor case study claiming 44% script lift where *every sentence is
  literally true and none of it is causal evidence.* Teach by annotating each sentence: "true —
  exposed group prescribed more"; "true — and they were the highest-decile targets"; "true — measured
  by the platform that served the ad." The Fellow learns to see truth and non-evidence coexist.
  *Numbers must be labeled illustrative + [verify].*
- **The hard inversion to pre-load for Ch 8:** students conflate "the ad was followed by more scripts"
  with "the ad caused more scripts." Use the targeting-on-outcome mechanism (A.1) as the wedge.
- **The "every sentence true" move is the most transferable skill** — it generalizes to any vendor
  deck. Make the per-channel evidence-rating taxonomy (A) the gradeable artifact.
- **Honesty trap to avoid:** the *meals* evidence is association too. Don't let the chapter present the
  industry's evidence as junk and the critical evidence as gospel — the meal study is observational;
  its strength is dose-response + single-meal threshold + N, not a randomized design. Model the same
  skepticism on both sides. This protects the book's credibility (and its partner relationship).
- **Bridge (TIKTOC):** "Act Two builds the toolkit, starting with the baseline that usually wins" → Ch 6.
- **Assessment alignment:** Reading Response #3 + Evidence-map & dataset checkpoint (100 pts). Part B:
  the Fellow writes the evidence map for their own thread and picks the public dataset here.

---

## F. Library files (copied to pantry/, prefixed `_lib_`)

- `_lib_science-science-fictions-how-fraud-bias-negligence-and-hype-undermine-the-search-for.md` —
  **directly load-bearing for B/D**: publication bias, outcome switching, the antidepressant 98%/48%
  publication asymmetry, only 31% of meta-analyses check for publication bias. Use for the
  "evidence base is contaminated at the source" argument.
- `_lib_science-randomistas-how-radical-researchers-are-changing-our-world.md` — RCT culture / why a
  control is the gold standard; supports the evidence-design ladder (A) and bridges to Ch 8.
- `_lib_math-causal-inference-mit-press-essential-knowledge-series.md` — association vs. causation
  fundamentals, confounding; the formal backbone of A.
- `_lib_science-the-book-of-why-the-new-science-of-cause-and-effect.md` — Pearl on why correlation is
  not causation; intuition pumps for the chapter's central distinction.
- `_lib_science-calling-bullshit-the-art-of-skepticism-in-a-data-driven-world.md` (pre-existing) —
  spotting misleading data claims; useful for the vendor-deck teardown exercise.
- (Reuse) `pantry/pharma-marketing-evidence-synthesis.md`, `pantry/pharma-ai-hcp-marketing-synthesis.md`.

---

## G. Gaps & flags

- [FLAG] **EHR script-lift effect sizes (4–44%, 19–25%, 11.9%/11.5%) are ALL vendor-sourced.** Never
  present without the "vendor-generated, un-refereed, methodologically circular" label. The web search
  for independent evidence returned only vendor pages — corroborates the gap; do not mistake vendor
  pages for validation.
- [VERIFY] Exact citation, year, and authors for: the *Annals of Internal Medicine* payments/self-
  assessment review; the Crestor-contraindication detailing study; the FDA bioequivalence trial count
  (>2,000); GSK Study 329 reanalysis (likely Le Noury *BMJ* 2015).
- [VERIFY] Academic-detailing review exact year (2024 vs 2025) and authors; Cochrane 5.6% figure.
- [FLAG — honesty] The meals study is observational; state the limitation explicitly so the chapter
  doesn't apply a double standard.
- [GAP] No independent estimate of EHR-ad *causal* lift exists to cite as a counter-number — the
  chapter can only point at the absence. This absence is the Ch 8 / Ch 13 Track A research opening
  (randomized/pre-registered EHR-exposure study), not something to fill with a substitute figure.
- [SCOPE] Keep DTC evidence (over-/under-use, opioid demand-pull, 68%-of-most-advertised-drugs-low-
  added-benefit) as *context*, not the chapter's spine — this book is HCP-facing (TIKTOC Out of Scope).
