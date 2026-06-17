# Research Notes: Chapter 04 — What Today's AI Stack Actually Does (and Claims)

**[MIDTERM: VENDOR-CLAIM AUDIT]**

**Chapter one-line (TIKTOC):** Fellows learn to separate a genuinely deployed AI capability from marketing language across next-best-action, predictive audiences, trigger messaging, MLR acceleration, and omnichannel.

**Opening artifact (TIKTOC):** "the world's first AI-powered operating system for healthcare marketing, powered by an adaptive Mixture of Experts" — is it true? what would it mean? what is it actually?

**Scope of these notes:** next-best-action, predictive audiences, trigger messaging, MLR acceleration, field-force intelligence, omnichannel; the deployed / emerging / aspirational ladder; vendor-claim auditing. *(Deep MoE teardown is Ch 7; this chapter is the capability inventory + first labeling pass.)*

---

## A. Conceptual foundations

### A1. The capability inventory and the deployed / emerging / aspirational ladder
**Explanation.** The chapter's core skill: place each named AI use case on a maturity ladder and attach a target KPI. The honest current state:
- **Trigger-based POC targeting** — *deployed / mature.* ICD-10 code fires → contextual ad delivers. Industry consensus "current gold standard" in POC messaging; higher HCP engagement than non-contextual digital.
- **Predictive audience modeling (propensity)** — *deployed at scale.* Models on claims + behavioral signals identify high-potential HCPs *before* a prescribing event (OptimizeRx DAAP, Doceree intelligence layer, IQVIA OCE+).
- **MLR acceleration / content generation** — *emerging but contested.* AI flags incomplete claims/missing references, links content to pre-approved claims libraries, routes low-risk modular content, drafts reviewer summaries (Veeva PromoMats Content Agent, late 2025).
- **Next-Best-Action (NBA) / agentic field-force AI** — *deployed (task-assistive), maturing toward agentic.* Recommends which HCP, channel, message, moment. Veeva AI Agents for Vault CRM (Dec 2025); IQVIA OCE+ NBA + AI agents built with NVIDIA; Salesforce Life Sciences Cloud (LSC4CE, Sept 2025).
- **LLM-based field-force support** — *emerging.* Meeting recaps, voice account-prep, real-time personalization; deployed at scale by Veeva/Salesforce/IQVIA 2025–26.
- **Federated learning for targeting models** — *in development / aspirational at scale.* Train on distributed patient data without centralizing it (Doceree references it); maturity unclear.
**Common misconception.** "If a vendor names a capability, it's deployed and proven." The skill is sorting deployed-and-evidenced from deployed-but-unaudited from sandbox/aspirational. Most *capabilities* are real; most *effectiveness claims* are not independently validated.
**Worked example.** A platform deck listing "AI-powered NBA, MLR acceleration, federated learning, MoE routing" → trigger targeting (mature), NBA (deployed, KPI=engagement/NBRx), MLR (emerging/contested), federated learning (aspirational-at-scale), MoE (likely relabeled stacking → Ch 7).
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §4. NBA/agentic 2025–26: IQVIA field-force agentic AI (https://www.iqvia.com/blogs/2025/07/driving-field-force-excellence-in-pharma); Veeva AI Agents for Vault CRM Dec 2025 + Salesforce-Veeva split Sept 2025 (https://www.veeva.com/eu/blog/veeva-commercial-summit-europe-agentic-ai-accelerates-precision-and-productivity-for-next-generation-engagement/); NBA-in-pharma overview (IntuitionLabs, https://intuitionlabs.ai/articles/next-best-action-pharma-guide).

### A2. Next-Best-Action (NBA) — what it actually computes
**Explanation.** NBA is the current frontier of pharma *commercial* AI: an AI system recommending **which HCP to contact, through which channel, with which message, at which moment**, generated from claims + behavioral signals + calendar optimization. The field rep becomes the human delivery mechanism for an AI-orchestrated sequence. KPI: engagement / NBRx / call response.
**Common misconception.** "NBA optimizes for the patients who most need the drug." NBA optimizes for *reachable responders* — it targets engagement-likelihood, not clinical need (the Ch 8 inversion and Ch 3 susceptibility concern, surfacing again). "Agentic" in the 2025–26 wave mostly means *task-assistive* agents (faster CRM work, call-report drafting), **not** autonomous analytical decision-making.
**Worked example.** Veeva's "Agentic Call Report" surfaces treatment barriers from rep notes; IQVIA agents free reps from admin. Genuine productivity tools — but the effectiveness claim ("better engagement → more scripts") is the part needing the Ch 8 holdout.
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §3; IQVIA/Veeva 2025–26 sources above. NBA-optimizes-responders-not-need: `pantry/pharma-brand-measurement-synthesis.md` §7 (AI use-case risk table).

### A3. MLR acceleration — the most operationally mature, most contested ROI
**Explanation.** MLR (Medical, Legal, Regulatory) review historically runs 50–60 days per content piece. AI is deployed to compress it: pre-screen for incomplete claims/missing references, link to approved claims libraries, route low-risk content, draft reviewer summaries. McKinsey cites 50–65% reduction in regulatory-submission timelines at some companies. Leading pharmas (Pfizer, Novartis, Sanofi, GSK, AstraZeneca) have moved from pilots to enterprise GenAI for medical info, literature monitoring, MSL enablement. The consensus implementation pattern is **Human-in-the-Loop (HITL)**: assistive automation for quantitative checks, human judgment preserved for contextual/ethical decisions.
**Common misconception.** "AI is replacing MLR reviewers and the efficiency gains are proven." Two counter-facts sit in tension: McKinsey's 50–65% efficiency claim *and* an MIT finding that **95% of enterprise generative-AI pilots are failing.** And speed creates a new problem: promotional-material production rose **29% YoY** in the US while **77% of approved content is rarely/never used by field teams** — volume up, not necessarily value. The problem is *governance, not generation speed.*
**Worked example.** A company reports "50% faster MLR" — the audit questions: faster on which content tiers? measured how? did rejected-content rate or post-launch FDA letters change? (See the 2025 FDA enforcement wave, B below.)
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §4. MLR + pilot-failure: Vodori (https://www.vodori.com/blog/the-future-of-ai-in-medical-legal-and-regulatory-mlr-review), Indegene future-of-MLR (https://www.indegene.com/what-we-think/reports/future-of-mlr-review), pharmaphorum "AI: missing link or reason it breaks" (https://pharmaphorum.com/market-access/ai-missing-link-fixing-mlr-or-reason-it-breaks). MIT 95%-pilot-failure widely cited across these.

### A4. Omnichannel orchestration
**Explanation.** Post-COVID, only ~45% of US physicians make themselves available to pharma (Q1 2024; 30% limit to one brand). The channel mix permanently shifted: in-person reps declining, remote/virtual detailing normalized, email high-volume/low-engagement, POC/EHR fastest-growing/highest-conversion, endemic digital high-trust/moderate-scale, programmatic open-web broad-reach/low-trust. **Omnichannel orchestration** = coordinating all channels for *one* HCP so messaging is coherent not overwhelming; NBA routes engagement to each HCP's preferred/responsive channel.
**Common misconception.** "Omnichannel = being everywhere." The point is *coordination*, not ubiquity — a physician hit by a rep visit + 2 emails + banners + an EHR trigger in one week has a *fragmented* brand experience; orchestration exists to prevent that.
**Worked example.** A physician who ignores email but engages endemic content → NBA suppresses email, prioritizes a Medscape placement + a virtual detail.
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §7.

### A5. Auditing a vendor claim — "what KPI, what data, what evidence?"
**Explanation.** The chapter's named artifact (and the midterm). For any capability claim, the Fellow asks: (1) **What KPI** does it actually move (and is that lift or brand)? (2) **What data** feeds it — is it the same infrastructure that also *measures* the result (attribution circularity)? (3) **What evidence** — vendor-generated case study, or independent? (4) **Deployed / emerging / aspirational?** (5) Does a buzzword (MoE, federated learning, "operating system") name a real architecture or a relabel (→ Ch 7)?
**Common misconception.** "An impressive lift number from a named platform is evidence." All script-lift figures (4%–44%) in this space are **vendor-generated, methodologically circular** (the platform serving the ad also measures the lift) — the field's single largest evidentiary gap (developed fully in Ch 5/8). "20:1 ROI" figures are unverified.
**Worked example.** "World's first AI operating system … adaptive Mixture of Experts." Audit: "operating system" = genuine *platform consolidation* (identity + POC inventory + programmatic + ABM + co-pay + analytics on a unified layer) — a real, defensible architectural claim. "Adaptive MoE" = a real *type* of architecture (specialized models + router), but specific deployment is *not independently verified* and on tabular NPI data is likely indistinguishable from / worse than a tuned ensemble (→ Ch 6/7). Verdict: platform-consolidation claim plausible; MoE-superiority claim unproven.
**Source.** `pantry/pharma-ai-hcp-marketing-synthesis.md` §4 (AI OS framing), §8 (genuine vs. claimed); `_lib_science-calling-bullshit-*.md` (the audit posture); `_lib_ai-prediction-machines-*.md` (what AI actually does economically — prediction, not judgment).

---

## B. Domain examples and cases

- **Doceree "AI Operating System."** Genuine platform consolidation across six capabilities on a unified data layer; "intelligence layers" map to NPI audience intelligence, conversational AI, SMART-on-FHIR workflow, creative-experience optimization. Real consolidation; specific performance unaudited. Frost & Sullivan recognition is *paid* recognition, not independent validation. (Synthesis §4, §6.)
- **Veeva AI Agents for Vault CRM (Dec 2025) + Agentic Call Report.** Concrete, dated example of *task-assistive* agentic AI in production; good "deployed but task-scoped" exemplar. (Veeva 2025–26 sources.)
- **IQVIA OCE+ NBA + NVIDIA agents.** Deployed predictive-audience + NBA; dominant data position (11M+ profiles, LAAD). (Synthesis §3; IQVIA blog.)
- **Veeva Crossix.** Cited by independent analysts as the *measurement gold standard* (best privacy methodology, HCP-level attribution) — a rare "evidence quality: high(er)" entry in the platform table; useful contrast case. (Synthesis §6 table.)
- **FAILURE case — the 2025 FDA enforcement wave.** Sept 2025: 200+ enforcement letters (74 to manufacturers: 10 Warning, 64 Untitled), FDA using *its own AI surveillance* to catch exaggerated efficacy / inadequate fair-balance. Context: warning letters collapsed from 100+/yr pre-2020 to 1 in 2023, 0 in 2024; OPDP Policy Division eliminated April 2025. The failure: AI-accelerated content generation (29% YoY volume rise) meeting reinvigorated, AI-powered enforcement — the governance gap made concrete. EHR-integrated ads notably *not* targeted (regulatory vacuum persists). (Synthesis §5.)
- **FAILURE case — the MoE label.** A "MoE targeting engine" that is actually XGBoost + bid model + rules with a learned aggregator: legitimate engineering, but *not* MoE and not obviously better than a tuned ensemble. The midterm's payoff (full teardown Ch 7). (TIKTOC Ch 7; `pantry/moe-vs-ensemble-synthesis.md`.)

---

## C. Connections and dependencies

- **Prereqs:** Ch 1 (the stack/channels), Ch 2 (lift vs. brand KPIs — every audit asks "which one?"), Ch 3 (the data substrate the AI runs on).
- **Unlocks:** Ch 5 (the evidence problem — this chapter exposes the claims; Ch 5 builds the framework to rate them); Ch 6 (the ensemble baseline any AI claim must beat); Ch 7 (the deep MoE-vs-relabel teardown this chapter previews); Ch 8 (why predicting prescribers ≠ causing prescriptions); Ch 10 (LLMs for content — the MLR/fair-balance risk surfaced here).
- **Adjacent:** Ch 14 (the handoff brief is the mature form of the vendor-claim audit). The midterm artifact (vendor-claim audit) is reused as a building block in the Part B thread.

---

## D. Current state of the field

- **Settled (capabilities real).** Trigger-based POC and predictive-audience modeling are genuinely deployed at scale. CRM/NBA agentic tooling shipped across all three majors (Veeva, IQVIA, Salesforce) in 2025–26. MLR pre-screening genuinely reduces cycle time for some content tiers.
- **Contested / thin (effectiveness).** Script-lift attribution (no independent validation; circular). AI-platform ROI ("20:1") unverified. The MIT 95%-pilot-failure stat sits unreconciled beside McKinsey's 50–65% efficiency gains — both circulate with unclear methodology (**FLAG both**). Whether "MoE" platforms run genuine MoE — *mostly false in practice* (book's position; Ch 7). Whether agentic NBA improves *incremental* scripts (vs. engagement) is unmeasured without a holdout (Ch 8).
- **Last-3-years developments.** Agentic AI wave (Dec 2025 Veeva agents; Sept 2025 Salesforce LSC4CE; IQVIA+NVIDIA). Veeva-Salesforce partnership expired Sept 2025 (5-yr migration window; 115+ Vault CRM live deployments by Q3 FY2026). FDA Sept 2025 enforcement wave + AI surveillance. Healthcare-AI investment in pharma commercial projected ~$1.9B (2025) → $16B+ (2034).

---

## E. Teaching considerations

- **Where students stick.** (1) Treating "named capability" as "proven capability" — the deployed/emerging/aspirational + KPI/data/evidence rubric is the antidote and the assessable skill. (2) Being dazzled by architecture words (MoE, agentic, federated) — teach that *most capabilities are real, most effectiveness claims aren't.* (3) Missing attribution circularity — the platform that serves the ad measures the lift; this is the seed of Ch 5/8.
- **Analogies.** Vendor deck = "a menu where every dish is described by the restaurant; your job is to ask who tasted it besides the chef." Deployed/emerging/aspirational = "in production / in pilot / in the press release." "Agentic" 2025 = "a very good intern, not an autonomous analyst." AI OS = "real plumbing consolidation, not magic."
- **Exercises (match TIKTOC midterm).** The **vendor-claim audit (100 pts)**: take a real public platform claim, rate each capability deployed/emerging/aspirational, attach KPI + data source + evidence type, flag circularity and relabeled buzzwords, render a verdict. Part B: apply the audit to a claim relevant to the Fellow's own thread.

---

## F. Library files relevant (copied to `pantry/` as `_lib_*`)

- `_lib_science-calling-bullshit-the-art-of-skepticism-in-a-data-driven-world.md` — the foundational posture for the whole chapter: how to interrogate impressive-sounding data claims, spot circularity and unfalsifiable numbers; directly powers the vendor-claim-audit rubric.
- `_lib_ai-prediction-machines-the-simple-economics-of-artificial-intelligence.md` — frames what AI *actually* does (cheap prediction) vs. judgment/action; helps students separate "the model predicts X" from "the platform achieves business outcome Y," central to deployed-vs-claimed.
- `_lib_ai-gigo.md` — garbage-in/garbage-out and AI-hype discounting; supports auditing federated-learning and MLR claims against data-quality reality.

*(No pharma-AI-vendor-specific library file exists in MD; these supply the skepticism/AI-capability scaffolding. The platform-specific facts come from the web sources above + `pantry/pharma-ai-hcp-marketing-synthesis.md`.)*

---

## G. Gaps and flags

- **FLAG (must `[verify]` before publication):** McKinsey "50–65% MLR/submission timeline reduction" and MIT "95% of GenAI pilots fail" both circulate without clear methodology and are in apparent tension — present both, attribute clearly, do not treat either as settled.
- **FLAG:** All script-lift / ROI figures (4%–44%; "20:1") are vendor-generated and circular — never present as independent evidence (developed fully Ch 5).
- **FLAG:** "Frost & Sullivan recognition" and similar = paid/industry recognition, not independent validation — label as such.
- **CONTESTED (book's position):** "'MoE' platforms run genuine MoE" — mostly false in practice; reserve the full verdict for Ch 7's architectural criteria (token-level routing? shared trunk? jointly trained?). Here, just flag the claim and defer.
- **GAP:** Independent measurement of whether agentic NBA improves *incremental* prescribing (not just engagement/productivity) does not exist — the holdout question routes to Ch 8.
- **FLAG (aging risk, per TIKTOC):** specific platform/model names (Veeva AI Agents, LSC4CE, OCE+, DeepSeek/Mixtral in Ch 7) date fast — pair every named example with the stable principle it illustrates.
