# Accuracy Review Log — AI-Driven Programmatic HCP Marketing

Run: 2026-06-17 · method: domain-expert web verification of every `[verify]` tag and load-bearing empirical/citation/legal claim, chapter by chapter. Rule enforced: **never fabricate a citation, statistic, author, date, or source** — confirmed claims are resolved with a real source, unconfirmable claims are kept honestly flagged, no invented replacements.

## Outcome
- `[verify]` tags in chapters: **89 → 52**. Of the 52 remaining: 11 are honest `[verify — unconfirmed: …]` hedges (load-bearing assertion softened), the rest are (a) pedagogical `[verify]` instructions inside the running-project exercise/prompt blocks (intentional — they tell students to flag their own work) and (b) firewall-attributed vendor figures kept as contested by design.
- Fabrications introduced: **0**. Fabrications found in existing text: 0 (no invented sources); several misattributions and imprecise figures were corrected.

## Substantive corrections (caught and fixed against primary sources)
- **Ch1 — co-pay coupon study.** The text conflated two papers. Corrected: Dafny, Ho & Kong (2022, NBER w29735) — commercial branded purchases rose **>20%** vs. Medicare Advantage; the 60%/generic-displacement and per-drug-cost findings belong to Dafny, Ody & Schmitt, *AEJ: Economic Policy* (2017, w22745). Removed an unsupported "net-of-rebate ~8% higher" claim. **Figure 1.3 SVG + PNG updated to match (>20%, corrected author line).**
- **Ch1 — Part D gifts study** corrected to Wood et al., *PLOS ONE* 2017 (DC-specific).
- **Ch1 — FDA enforcement** corrected from "200 letters" to ~60 (Sept 9 2025, HHS/FDA).
- **Ch2 — "68% low added benefit"** corrected to top-selling (not most-advertised) drugs, *JAMA* 2023; BMJ most-promoted-drugs finding resolved (Greenway & Ross 2017).
- **Ch3 — IQVIA OneKey** corrected (25M+ HCPs, not 11M); **AMA Masterfile** revenue figures corrected to the sourced Public Citizen 2012 numbers.
- **Ch5 — antidepressant publication-bias** corrected to Turner et al., *NEJM* 2008 (precise framing; effect inflated ~⅓, not "half").
- **Ch9 — QALY/value figure** misattribution fixed: Wouters → **Bloudek et al., *Value in Health* 2021**.
- **Ch10 — citation/fabrication anchors** verified exactly: *Mata v. Avianca* (2023); Chelli et al. *JMIR* 2024; Linardon et al. *JMIR Mental Health* 2025; Zheng et al. (LLM-as-judge) NeurIPS 2023.
- **Ch12 — Larkin 2017 (JAMA)** mischaracterization corrected (all-three-policies-with-enforcement vs. missing-one; −1.7pp detailed-drug share); **ICER thresholds** corrected to the actual VAF range; staggered-DiD canon citations completed (Callaway–Sant'Anna, Goodman-Bacon, Sun–Abraham, de Chaisemartin–D'Haultfœuille, McCrary).
- **Ch6–8** — method citations verified exactly (Grinsztajn NeurIPS 2022; Shazeer 2017 / Switch / Mixtral / DeepSeek-V3 specifics; Künzel 2019, Nie–Wager 2021, Wager–Athey 2018; Larkin JAMA 2017).

## Kept honestly flagged (unconfirmable; not asserted as fact)
IQVIA 93% NBRx coverage (Ch2); ZS 45%/30% 2024 physician-access figures (Ch4); Ritchie 31% meta-analysis figure (Ch5); TabPFN 2026 standing (Ch6); 2025-frontier model configs (Ch7); per-estimator uplift rankings (Ch8); several IAT effect-size decimals / brand-IAT gap (Ch9); secondary fabrication-rate figures + a few arXiv IDs (Ch10); MLR cycle-time vendor figures (Ch11).

## Firewall preserved
Vendor ROI/lift figures (4–44%, 20:1), "AI reduces MLR 50–65%", MIT "95% of pilots fail", and similar remain **attributed and contested** — a vendor confirming its own claim is not independent verification, and the log notes that distinction where relevant. The Evidence Ladder (0–6) is the book's own TRL×OCEBM construct (both underlying frameworks verified real).
