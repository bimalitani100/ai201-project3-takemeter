> **How to use this file.** This is a starting scaffold, not a finished plan. The assignment expects you to design your own structure, so reorganize freely and make it yours. Sections tagged **DRAFT** are written from our planning conversation — read them critically, put them in your own words, and adjust anything you disagree with. Replace every **[FILL IN]** with your real decision. Disclose this AI assistance in your README's AI usage section (Claude drafted the structure and the collection/metrics sections; you reviewed and edited them).

# TakeMeter — Planning

## 1. Community

**DRAFT — confirm in your own words.** I chose **r/nba**. The discourse varies enormously in quality: the same thread can hold a rigorous tactical breakdown, a confident evidence-free hot take, and a pure emotional reaction, which means there is a real, learnable distinction to classify. The late-June timing helps — the draft and the start of free agency flood the sub with debate, giving varied, high-volume data to sample from.

> **Note to self:** r/nba is the community the assignment uses for its *worked example* (analysis / hot_take / reaction). That's convenient but it cuts both ways — the grader has seen that example too. Treat the labels in §2 as a hypothesis to test against real posts, and make sure my headline edge case in §3 is a **real comment I found**, not the doc's LeBron example.

**[FILL IN]** Add 1–2 sentences on why r/nba fits *you* specifically and what makes its discourse worth classifying.

## 2. Labels (working hypothesis — confirm or revise after reading 30–40 real comments)

- **analysis** — a structured argument backed by specific, verifiable evidence (stats, tactical detail, historical comparison) that actually reasons toward the claim.
- **hot_take** — a bold, confident claim asserted with no real support, or propped up by a single cherry-picked/decorative stat that sounds like evidence but isn't doing the reasoning.
- **reaction** — an immediate emotional response to a specific moment, with little to no argument.

(Out-of-scope material is handled by the inclusion rule in §3.)

**[FILL IN]** After your read: (a) state whether the three-label cut held up or how you revised it, and (b) add **2 real example comments per label** pulled from your collection.

## 3. Hard edge cases + inclusion rule

**Inclusion rule (DRAFT).** TakeMeter classifies *takes*. Comments that are pure jokes, one-line banter, restatements of news, or genuine information-seeking questions are **out of scope** and are not collected. Scoping the task this way is what keeps the three labels exhaustive over the data that remains — it's the honest answer to the "what did you do with posts that don't fit" question.

**Candidate hard seam (DRAFT).** The **reaction ↔ hot_take** boundary: an in-the-moment emotional comment that *also* asserts a general claim (e.g., raging at a front office while implying the front office is bad). Proposed decision rule: strip the emotional framing; if a standalone, portable claim survives → **hot_take**; if only momentary venting remains → **reaction**.

**[FILL IN]** Document **at least 3 real comments** that gave you genuine pause: what each said, which two labels it sat between, and what you decided. One of these becomes your headline edge case.

## 4. Data collection plan

**DRAFT — confirm targets.** Source: public **r/nba comments** (not submission titles — titles are mostly news/highlights; the takes live in the comments). Threads to sample:
- Mock-draft / draft megathreads and prospect-debate posts → analysis + hot_take (sort by **Top** for substantive comments).
- The live draft thread → reactions (sort by **New** for raw in-the-moment posts).
- One serious effort/analysis post.

Target: **≥200 collected comments** after applying the inclusion rule. Balance: aim for **≥20% per label**, with **no label above 70%**. If a label is underrepresented after 200, pull more from threads that skew toward it (e.g., game/draft threads for reactions). Collection is manual, straight into the CSV.

**[FILL IN]** Your per-label goal and what you'll do if balance is off.

## 5. Evaluation metrics

**DRAFT — restate in your own words.** Accuracy alone is not enough: the classes may be imbalanced (so a majority-class predictor can score deceptively well), and the failure that actually matters is *which boundary* the model misses. So the metric set is:
- **Overall accuracy** for both models (the headline comparison number).
- **Per-class precision / recall / F1**, with **F1 as the headline per-class metric**, to see whether each distinction is being learned.
- A **confusion matrix** to expose directional errors (e.g., true `analysis` predicted as `hot_take`), which tells you exactly which seam the model hasn't learned.

**[FILL IN]** Explain why these are the right metrics for *this specific* subjective-discourse task.

## 6. Definition of success

**[FILL IN — your call, and be specific.]** What per-class F1 / accuracy would make this genuinely useful as a community tool, and what would you accept as "good enough" to deploy? Give a concrete threshold, not "it works well." A reasonable way to anchor it on a hard 3-class subjective task: meaningfully beat the zero-shot baseline *and* have no class with F1 near zero — but you set the bar and justify it.

## AI Tool Plan

The assignment names three places AI tools help here:
- **Label stress-testing** — *Done.* See Appendix A: Claude generated 6 boundary comments; I labeled them against my definitions and tightened the definitions where they didn't resolve cleanly.
- **Annotation assistance** — **[FILL IN]** Will you pre-label a batch with an LLM and then review every label yourself? If yes, name the tool and how you'll track which rows were pre-labeled (for disclosure).
- **Failure analysis** — **[FILL IN]** Plan to paste your wrong predictions into an LLM to surface patterns, then verify each pattern yourself by re-reading the examples.

---

## Appendix A — Label stress-test (AI-assisted, 2026-06-22)

Claude generated the following 6 synthetic boundary comments to test my label definitions before annotating. I labeled each against my definitions; where my call and the intended boundary disagreed, I tightened the relevant definition above.

> **Disclosure:** these are synthetic, generated for stress-testing only. They are **NOT** part of the 200-example dataset.

1. *"Spurs are gonna regret not moving this pick. Wemby needs a vet PG right now, not another teenager — the win-now window is open and they're acting like it's a rebuild."* — tests **analysis vs hot_take**: argument-shaped but no verifiable evidence → **hot_take**.
2. *"Peterson is a fraud, dude put up 18 a game against literal high schoolers and now he's a top-3 lock? Soft schedule inflation, look it up."* — tests **analysis vs hot_take** (the single-stat decoy): one cherry-picked, dismissive stat → **hot_take**.
3. *"ARE YOU KIDDING ME this front office could not hit water falling out of a boat, fire all of them"* — tests **reaction vs hot_take**: strip framing → a portable claim ("this FO is bad") survives → **hot_take** (this seam is a strong candidate for the real edge case).
4. *"Spurs draft strategy: collect Frenchmen like they're Pokémon"* — tests **skip vs take**: mostly a joke → **skip** under my inclusion rule.
5. *"How is anyone mocking him to the lottery when he can't create his own shot??"* — tests **skip vs take**: rhetorical question carrying a claim → **in**, as a **hot_take** (decide and apply consistently for all such questions).
6. *"rewatched a bunch of his tape and honestly Wemby's passing out of doubles got so much better late in the year — he was hitting the weakside cutter consistently the last 20 games, that's the real leap."* — tests **analysis vs reaction**: casual tone, but a specific verifiable observation → **analysis** (judge content, not vibe).

**[FILL IN]** Note any definition you tightened as a result, and re-run this test against your *final* labels after the real read.
