<!--
  INTRODUCTION — Chapter 0 / roadmap chapter.
  Follows the 13-element roadmap. Reader-facing: what the book argues + how it is organized.
-->

# Introduction

A vendor's deck is open on the conference-room screen, paused on the slide everyone came to see: **"44% script lift."** The brand director turns to the Fellow the lab sent over — the one who has spent the week pulling the program apart on public data — and asks the only question that matters: *"If I hand this to my data-science team on Monday, what would they actually do with it?"* The honest answer is uncomfortable. They would not know whether the 44% is the effect of the advertising or the shadow of the targeting, because the platform that served the ads also measured the lift, and it aimed those ads at the physicians already most likely to prescribe. The number is real as a difference between two groups. It is unknown as an effect of the campaign. And a budget is about to be set on it.

The gap this book fills: pharmaceutical marketing has built a fast, precise, AI-driven machine for *engaging* physicians and almost no discipline for proving that the engagement *caused* a prescription worth causing.

The central argument is testable and contestable: **the script-lift figures that drive HCP marketing budgets are associations systematically inflated toward zero risk and away from the truth — by selection, attribution circularity, missing controls, and reporting bias — and the field's most valuable AI work is not producing a better number but specifying the design that would make a number trustworthy.** If a single pre-registered, independent, controlled study showed the vendor-range lift holding up, the argument would weaken. It has not been run.

This book is written for the data-capable Fellow and the marketing-science team working alongside a martech partner — people who can read a model, join a public dataset, and are responsible for telling a brand team what the evidence does and does not support.

**What this book is.** It is a field manual for seeing the HCP-marketing machine clearly and grading its claims honestly. It gives you a shared vocabulary — NPI targeting, the identity graph, lift versus brand, uplift and incrementality, the Evidence Ladder, attribution circularity, the IP firewall — and it teaches you to use AI tools strategically: to draft, reformat, and option-generate where you can check the output, and to refuse the model exactly where the judgment is irreducibly yours. It is built around public and synthetic data, so every method in it is one you can actually run.

**What this book is not.** It is not legal or compliance counsel; it flags MLR, fair balance, the Sunshine Act, and HIPAA, then routes them to a human with authority. It is not a deep-learning course or a media-buying handbook. It assumes you can read basic statistics and write a little code — comfort with a dataframe, a regression, and the difference between a correlation and a cause — but it does not assume causal inference, which it builds from the ground up. It will not tell you whether a drug deserves to be promoted; it will tell you whether the claim that the promotion *works* is evidence or decoration.

**The concept that runs throughout** is the *evidence taxonomy*: the discipline of grading any claim on two axes at once — how strong the study design is, and how independent the source is — and taking the *minimum* of the two as the grade. The vendor's 44% sits in the weakest corner of that grid: an unadjusted exposed-versus-unexposed comparison reported by the party that profits from it. The taxonomy is what lets you say so precisely, and lets you apply the same standard to evidence you *like*. Running alongside it are two distinctions you will use on every page: **Rung-1 engagement** (did the physician notice the message) versus **the budget question** (did the message change a prescription that would not otherwise have changed), and **attribution circularity** (the platform that serves the ad also measures its effect).

**A running thread.** From the first chapter you carry one branded drug — your choice — through the whole book in a project called *One Drug, End to End*. You map its split-agency stakeholders, profile its lift-versus-brand position, grade its promotional claims, benchmark a model that targets it, and finally assemble a one-page brief recommending what a partner should test, build, or kill. The exercises build that case file chapter by chapter.

**How this book is organized.** The fourteen chapters move in four movements.

*Movement I — the machine and its anomaly (Chapters 1–3).* Chapter 1 shows you the machine nobody sees: how a commercial message rides clinical interoperability rails into the physician's chart, and why the party who pays is never in the room. Chapter 2 separates the two dependent variables every campaign actually moves — short-term lift and durable brand association. Chapter 3 builds the HCP identity graph and the deterministic NPI targeting that the whole stack hangs on.

*Movement II — what the AI does, and what the evidence says (Chapters 4–5).* Chapter 4 audits what today's AI stack actually does versus what it claims. Chapter 5 is the book's spine: the evidence problem, the two-axis taxonomy, and why every sentence on the vendor deck can be true while none of it is causal evidence.

*Movement III — the methods, honestly graded (Chapters 6–10).* Chapter 6 explains why gradient-boosted ensembles, not deep nets, are state of the art on tabular HCP data. Chapter 7 takes apart "Mixture of Experts" and shows when the term is architecture and when it is marketing. Chapter 8 builds uplift and incrementality — measuring real, persuadable lift. Chapter 9 makes brand association a measurable outcome. Chapter 10 puts LLMs to work on commercial research and content intelligence, with a verification harness.

*Movement IV — the lab, written down (Chapters 11–14).* Chapter 11 is the external-innovation-lab operating model and the IP firewall — the contract that makes public-data research safe for a partner. Chapter 12 covers research design and the public datasets that power it. Chapter 13 is the Fellow's four-track research portfolio, run once, where a pre-registered "no" counts as a result. Chapter 14 turns a prototype into a product decision through the Fellow's one-page brief.

**How to read it.** Read Movements I and II in order — they set the vocabulary and the standard everything else uses. After that, the method chapters (6–10) are largely self-contained; take them in the order your work needs. The lab chapters (11–14) are best read as a sequence, because they assemble into a single workflow. Every chapter closes with the same features: a *What would change my mind* section that states the falsifying evidence, a *Still puzzling* section that keeps the open questions open, and a five-part exercise block — *When to Use AI*, *When NOT to Use AI*, an LLM exercise, a CLI exercise, and an AI-validation exercise — that builds your *One Drug* case file and trains you to use AI tools where they help and refuse them where they don't.

### A note about AI

This is a book about AI-driven marketing, written in the middle of an AI wave, and it uses AI throughout — so it owes you a clear account of how. Two things are true at once, and holding both is the whole discipline.

First, the engagement that is *specific to this field*. The AI in HCP marketing is not, for the most part, exotic. It is gradient-boosted trees on tabular data, propensity and uplift models, and increasingly LLMs for research and content. The book's stance is that you should use these tools fluently and skeptically. Fluently: an LLM is excellent at reformatting a vendor page into a claims table, drafting the skeleton of an evidence map, clustering ten papers into themes, generating a first list of candidate trigger events. Skeptically: an LLM will also confidently assign a grade it has no business assigning, launder a vendor's script-lift figure into an apparent fact, fabricate a citation that reads perfectly, and relabel a result that should have killed a project as "promising." The exercises in this book are built to train the line between the two. The rule, stated once and meant everywhere: **use AI where you can independently evaluate the output, and refuse it where the judgment — the causal call, the evidence grade, the kill criterion — is the irreducible human work.** When you used a tool, you say so, and you name the one thing it could not decide for you.

Second, the *innovation-lab framing* that makes this book more than a manual. Bear Brown, LLC and Humanitarians AI together operate as an external innovation lab: we research and prototype the AI that might help a company, build the proof of concept on public or synthetic data, test whether it actually holds, and only then work alongside the company's team to implement what survives. Humanitarians AI runs 100–200 Fellows at any time across many majors, so when a project needs extra hands for a few weeks it staffs on a per-hour basis — low commitment for the company, high evidence for the decision. The safety contract is an **IP firewall**: published work uses public and synthetic data only; the partner replicates anything promising on its proprietary data, internally, on its side of the wall. A public-data test tops out at roughly Level 3 on the book's Evidence Ladder — a small offline test that beats a baseline — and the firewall is exactly the rung where the work crosses from the Fellow's side to the partner's. This is not a sidebar to the book; it is the book's method. Chapters 11 through 14 are the lab's operating model, its research design, its portfolio, and its handoff brief, written down so that running the exercises *is* a preview of working with the lab. If you finish this book having built your *One Drug* case file under the firewall, you have done, on your own drug, exactly what a Fellow does on a partner's question.

So when you reach a chapter that uses an LLM to draft a card or a CLI agent to grep a corpus, read it as the lab working in the open: the machine does the cheap, checkable work, and a human holds the load-bearing judgment. That division is the answer to the brand director's Monday question — and it is the answer this book exists to teach.

## The Innovation Lab — the project portfolio

This is the lab in one page. Bear Brown, LLC and Humanitarians AI run an external innovation lab for companies: we research and prototype the AI that might help a partner, prove it out on public and synthetic data, and then work alongside the partner's own team to implement whatever survives. What follows is the candidate-project menu — detailed enough that a Fellow can pick one up and start, and concrete enough that a partner can see exactly which questions are worth funding. The operating discipline is the same for every project. Fellows work only on **public data** (CMS Open Payments, Medicare Part D, Medicaid drug-utilization data, ICER value reports) and on **synthetic stand-ins**; the partner reproduces anything promising on its own proprietary data, behind an **IP firewall**, so nothing confidential ever enters a public book or repository. Every project is graded on an **Evidence Ladder** from 0 to 6 — public data realistically reaches about Level 3, an honest offline test that beats a baseline, and the higher rungs need the partner's private data. Every project writes its **kill criterion before it sees the result**, so a disappointing finding is a result, not an embarrassment to be spun. The lab's product is not a literature review and not a relabeled vendor number; it is *reduced uncertainty about where the partner should spend real data and engineering.* One blocker sits over all of it — **Risk 1**: partner data access, how the collaboration is framed, and consent ethics — and until it is settled, the proprietary and adversarial work waits.

The portfolio runs in two streams. A **breadth portfolio** spans the whole marketing stack — measurement, brand, model architecture, and ethics — thirteen projects, each testing one falsifiable claim on public data and naming the proprietary work that would settle the strong version. A **depth practicum** takes a single dataset — rep-visit telemetry — and builds it end to end into a deployable causal model. (Each stream is also a hands-on book in this series, so a Fellow can work it cover to cover.)

### Breadth portfolio — the marketing stack (thirteen projects)

**Track A — Lift and attribution** asks whether the "script-lift" numbers that set budgets are real effects or artifacts.

- **A1 — Script-lift attribution audit.** Rebuild a vendor-style lift number from public data, then re-estimate it with an honest design, to show how much of the headline was just the targeting picking physicians who would have prescribed anyway.
- **A2 — EHR-lift design memo.** Write the experiment that *would* prove point-of-care advertising works, with a power analysis — and admit that on public data this is a design, not a result. Saying so plainly is the contribution.
- **A3 — Channel decomposition.** Split an observed change in prescribing across promotion channels, honest about what cannot be separated without knowing who was actually exposed.

**Track B — Brand and physician identity** asks whether promotion builds something durable or rents short-term attention.

- **B1 — Share-of-mind → share-of-market.** Test the industry's belief that mindshare today predicts market share later — never rigorously checked on linked data. An open question, not a fact.
- **B2 — Prescribing-habit persistence.** Measure how sticky prescribing is across drug classes, to find where brand loyalty is structurally real.
- **B3 — Brand equity vs. clinical value.** The uncomfortable test: does brand equity predict prescribing *after* you control for the drug's independent clinical value? An equity-not-value finding is a patient-welfare result.
- **B4 — Loss-of-exclusivity event study.** Use the date a generic enters as a natural shock to see how much branded share survives, and whether the survivors were the strong brands. The causal companion to B3.

**Track C — Model architecture and segmentation** checks the engineering claims behind the targeting.

- **C1 — Ensemble vs. routed model.** The worked example: a plain, well-tuned model against a fancy "Mixture-of-Experts" one on the same targeting task, judged on calibration, not just accuracy. In a worked benchmark the plain model wins — and the "no" saves a build nobody needed.
- **C2 — Physician archetypes.** Ask whether physician "segments" are a real structure in the data or a round number chosen to fit a slide.
- **C3 — Vendor "MoE" audit.** A desk review of vendor "Mixture-of-Experts" claims against a short list of what genuine MoE actually requires.

**Track D — Privacy, fairness, and accountability** is the adversarial track, and the one that most needs partner sign-off.

- **D1 — Proxy-discrimination test.** Check whether targeting models quietly key on physician "susceptibility" or protected-group proxies instead of clinical need.
- **D2 — Co-pay-coupon generic suppression.** Measure how much co-pay coupons suppress cheaper generics and raise system cost — a well-precedented public-data design that tests a partner product line, so framing must be cleared first.
- **D3 — Accountability framework.** Write the rules a deployed targeting system should live under: what it monitors, what it discloses, what can be audited.

### Depth practicum — rep-visit telemetry, built into a causal model

Three runnable studies, plus the machinery that ties them together.

- **Project 1 — Staggered difference-in-differences.** Reps are trained in waves, so the rollout calendar is a natural experiment; use it to measure what a *message* actually causes a physician to prescribe. The most feasible and highest-value study.
- **Project 2 — Meals causal forest.** Use public Open Payments data to estimate how promotional meals affect prescribing for different kinds of physicians, separating genuine education from simple reciprocity. The one study you can run today, end to end, on public data alone.
- **Project 3 — Slide-sequence Double Machine Learning.** Ask whether the *order* of slides changes prescribing — and learn the hardest lesson in the set: the engagement signals you would naively control for are *caused* by the message, so conditioning on them quietly breaks the estimate.

And the architecture around the studies:

- **The Causal Interview Bot.** Let a rep talk like a rep while the system listens like a causal scientist, turning the rep's knowledge of *why* a physician behaves a certain way into a structured prior — necessary because the data alone can never decide the direction of certain arrows.
- **Persuadables, not sure-things.** Flip targeting from "who is most likely to prescribe" (often people who would anyway) to "who would a message actually move."
- **Consent, compliance, and the handoff.** Handle the ethics and the law — opt-out quietly biases the sample, only the educational pathway is legally drivable, regulatory questions go to counsel — and end with the deliverable that matters: a working model on synthetic/public data plus a brief telling the partner exactly what to build behind the firewall.

### Where to start

For a first cohort that needs a fast, defensible win: **C1** is the cleanest starter — self-contained, public data, an honest "no" that saves an engineering decision. The **meals causal forest** is the only fully-public *causal* result in the whole portfolio — a real heterogeneous-effect estimate on Open Payments. **A1** strikes at the field's central inflated claim while framing it as de-risking the partner's own numbers. And **D2** is well-precedented but should wait for Risk-1 sign-off. Everything above Level 3 — the strong causal versions, the deployed model — is the partner's to build; the portfolio's highest-value output, where the real uncertainty lives above the public-data ceiling, is *telling the partner exactly what proprietary work to fund.*

Return to that conference room. The Fellow does not say the 44% is a lie; disbelief is as lazy as belief. The Fellow says: *here is what the number is (a difference between selected groups), here is what it is not (a causal effect), here is the holdout study that would settle it, and here is the honest evidence level I can reach on public data.* That is the deliverable. Now go build it for your own drug — start with Chapter 1, and don't let a fluent sentence stand in for a counterfactual you never observed.

**Tags:** HCP marketing · pharmaceutical marketing · programmatic advertising · point-of-care · NPI targeting · next-best-action · causal inference · uplift modeling · incrementality · attribution · evidence grading · gradient boosting · mixture of experts · LLMs · computational skepticism · external innovation lab · IP firewall · Humanitarians AI · Irreducibly Human
