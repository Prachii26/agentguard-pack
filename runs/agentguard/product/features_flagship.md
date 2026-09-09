# Flagship features — the 20 highest-leverage

**Status: design only — no implementation exists yet (`BRIEF.md` stage line).**

**What this is**: the 20 features that carry the most weight in the product — each one named, its mechanism stated (not adjectives), the principle it maps to from `product/PRD.md` §5 (P1–P10), and the moment a user actually sees it happen.

**Why it exists**: a 50-item prioritized backlog (`product/features_prioritized.md`) makes it easy to lose the plot on which dozen features actually make AgentGuard the thing described in `strategy/positioning.md`, rather than a slower reimplementation of AutoDojo. This document is the answer to "if we only had time to build 20 things, which 20, and why would each one matter." The failure this document prevents: a roadmap where effort concentrates on the Attack stage (the fun engineering problem) while the Report stage (the actual differentiator, per `ASSUMPTIONS.md` A9) ships as an afterthought.

**How to read it**: features are ordered by loop stage (Configure → Attack → Observe → Adapt → Report), not by importance — the closing argument states explicitly why the Report-stage features, not any single Attack-stage feature, are where the product's power actually lives. A skeptic should check that no feature here is described only by an adjective (`references/quality-bar.md` property 1).

**Depends on / feeds**: expands `product/PRD.md` §6. Feeds `product/ux_spec.md` (screens for each visible moment) and, once generated, `tech/architecture/`.

---

## Configure

**1. Staging-only connection gate**
- *Mechanism*: the Configure API/CLI accepts only staging-shaped endpoint identifiers and sandbox credentials by schema — there is no field or flag that accepts a production-classified target.
- *Principle*: P10 (staging-only-by-design).
- *Visible moment*: a user who pastes a production-looking URL gets a hard validation error naming why, before any campaign can start.

**2. Defense-set selector (1–4 of the fixed four)**
- *Mechanism*: campaign configuration requires choosing which of defensive-prompting / classifier-based / rule-based tool-call validation / baseline-none to include; each selected defense spins up its own budget-matched sub-campaign.
- *Principle*: P5 (cross-defense-family comparability).
- *Visible moment*: a checklist of exactly four named defenses, not an open-ended list — the boundary from non-goal §3.2 is visible in the UI itself, not just the docs.

**3. Single attempt-budget field, applied identically per defense**
- *Mechanism*: one number (rounds per campaign) is entered once and propagated unchanged to every selected defense's sub-campaign — the system structurally cannot run defense A for more rounds than defense B in the same comparison.
- *Principle*: P1 (matched-budget).
- *Visible moment*: the budget field is disabled from per-defense override; a tooltip explains why, citing the matched-budget requirement.

**4. Reference-harness picker**
- *Mechanism*: a short, explicit list of year-one-supported agent harnesses (the frameworks the four baseline benchmarks already use) rather than a free-text "connect any agent" field.
- *Principle*: non-goal §3.4 (no cross-framework certification).
- *Visible moment*: unsupported-framework selections show "not yet supported" rather than silently failing mid-campaign.

## Attack

**5. Configurable attacker registry, AutoDojo-default**
- *Mechanism*: the red-team agent's attack-generation strategy is a pluggable configuration; year one ships exactly one, AutoDojo's black-box iterative optimizer, explicitly labeled by source.
- *Principle*: P9 (novelty is in application, not the loop); non-goal §3.7 (no proprietary-attacker claim).
- *Visible moment*: the campaign setup screen names "Attacker: AutoDojo black-box optimizer (adopted, v1)" rather than a branded, unattributed name.

**6. Feedback-only mode (default, cannot be silently disabled)**
- *Mechanism*: the attacker process receives only a pass/fail signal per round; the defense identity and configuration are withheld from its context by construction, not by convention.
- *Principle*: P2 (feedback-only-as-primary).
- *Visible moment*: the campaign's results header always states "Feedback-only" unless white-box mode was explicitly and separately opted into.

**7. White-box comparison mode, always a separate labeled column**
- *Mechanism*: an opt-in second campaign arm where the attacker is told the defense type up front; results render in a visually distinct column, never merged into the primary ASR figure.
- *Principle*: P2 (white-box is upper-bound only, never headline).
- *Visible moment*: the report never shows a single blended ASR number that mixes feedback-only and white-box rounds.

**8. Text-only injection surface generators**
- *Mechanism*: payload construction covers email, document, webpage, and calendar-invite content types only; no image or audio payload path exists in the generator.
- *Principle*: non-goal §3.3 (no multi-modal injection).
- *Visible moment*: the injection-surface selector lists exactly four content types, with no "coming soon" placeholder implying multi-modal is a checkbox away.

## Observe

**9. Per-round outcome logger**
- *Mechanism*: every round writes one row: attempt content, tool calls attempted, tool calls executed, pass/fail, and whether the legitimate benign task (if one was interleaved) still completed.
- *Principle*: P3 (utility-paired reporting), P1 (matched-budget requires auditable per-round data).
- *Visible moment*: a raw round-log table, filterable by round number, sits one click below every summary chart — nothing in the summary is un-auditable.

**10. Defense fingerprint capture**
- *Mechanism*: the behavioral signature of how a given defense responded under pressure (block patterns, latency, refusal phrasing) is logged per campaign as a structured record, not just a pass/fail count.
- *Principle*: P6 (self-reported robustness doesn't survive adaptive pressure — the fingerprint is the evidence trail that shows *how* it collapsed, not just *that* it did).
- *Visible moment*: a "defense fingerprint" panel per defense, showing the shape of its failures, not just a final number.

**11. Legitimate-task interleaving**
- *Mechanism*: benign, non-malicious task requests are interleaved with injection attempts during the same campaign, against the same active defense, so utility can be measured under the same conditions the attack was measured under (not a separate, disconnected utility test run).
- *Principle*: P3 (utility-paired reporting).
- *Visible moment*: the round log shows both attack rounds and benign-task rounds in one continuous timeline.

## Adapt

**12. In-context adaptation controller (no training phase)**
- *Mechanism*: the attacker updates its next-round strategy from within the live campaign session using prior rounds' observed outcomes — no offline fine-tuning or RL training step exists between rounds.
- *Principle*: P7 (in-context adaptation over offline-trained attacker).
- *Visible moment*: a new customer's brand-new defense configuration can be evaluated in the very first campaign run against it — no "please allow 24 hours to train" step anywhere in the flow.

**13. Attempts-to-first-success tracker**
- *Mechanism*: the round index of the first successful injection is recorded per campaign per defense as a distinct metric from the ASR figures.
- *Principle*: P4 (final-window ASR as headline, alongside practicality signals).
- *Visible moment*: a single number, "first success at round 7," displayed next to (not folded into) the ASR headline.

**14. Adaptation-curve data pipeline**
- *Mechanism*: ASR is computed per round-window across the campaign and stored as a time series, not just a final scalar.
- *Principle*: P4, P5.
- *Visible moment*: a line chart, ASR vs. round number, one line per defense, overlaid.

## Report

**15. Final-window ASR as the headline metric**
- *Mechanism*: ASR is computed over the last *k* rounds (configurable, sensible default) rather than averaged across the whole campaign, so early exploration failures don't drag down the number that answers "does the attacker get there."
- *Principle*: P4 (final-window-ASR-as-headline).
- *Visible moment*: the largest number on the report screen is final-window ASR; campaign-average ASR appears smaller, clearly labeled "secondary."

**16. Cross-defense comparison table**
- *Mechanism*: one table, rows = defenses, columns = final-window ASR / attempts-to-first-success / campaign-average ASR / utility / benign block rate, all computed at the same attempt budget.
- *Principle*: P5 (cross-defense comparability), P1 (matched-budget).
- *Visible moment*: this is the single screen every persona in `strategy/personas.md` is described as needing — Marcus attaches it to a ticket, Elena trends it, David exports it.

**17. Utility-under-attack metric, AgentDojo-aligned**
- *Mechanism*: computed as the fraction of interleaved benign tasks the target agent still completes correctly while the defense is active and an injection is present, using AgentDojo's published utility definition rather than an invented one.
- *Principle*: P3 (utility-paired reporting).
- *Visible moment*: every row of the comparison table (feature 16) has a utility column that is never blank.

**18. Adaptation-curve chart in the report**
- *Mechanism*: the time series from feature 14 is rendered as an overlay chart on the final report, one curve per defense, at matched round count.
- *Principle*: P4, P5.
- *Visible moment*: a visual answer to "how fast did the attacker converge against each defense," not just the final number.

**19. Audit-ready report export**
- *Mechanism*: the comparison report (feature 16 + 17 + 18) exports to a structured, ISO 42001 Operation/Performance-Evaluation-clause-mapped PDF/data format, addressed and citable without needing the live product open.
- *Principle*: Goal 4 (`PRD.md` §2), P6.
- *Visible moment*: David's persona (`strategy/personas.md` card 4) can hand this file to an auditor and never open AgentGuard himself.

**20. Re-run / re-diff against campaign history**
- *Mechanism*: a new campaign against the same target-agent-plus-defense pair is automatically diffed against the most recent prior run on that pair, surfacing what changed (ASR up/down, utility up/down) rather than requiring manual comparison.
- *Principle*: P8 (reproducibility over one-off engagement).
- *Visible moment*: a "vs. last run" delta badge next to each metric in the comparison table, present from the second campaign onward.

---

## Why the power is the closed comparison loop, not any single feature

Any one of features 5–14 (Attack/Observe/Adapt) reproduces, at best, what AutoDojo already does — a single adaptive attacker against a single deployed defense, inside one framework, without a utility metric (`research/competitors.md`). None of them, alone, is defensible; all of them together are still just a faster reimplementation of published academic prior art. The features that make AgentGuard a different thing than AutoDojo, Adversa AI, or Microsoft's bundled Foundry Red Teaming Agent are features 2, 3, and 16 specifically: the defense-set selector, the shared attempt-budget field, and the cross-defense comparison table. Remove any one of the Attack-stage features and the product gets weaker at attacking; remove feature 16 and the product stops being AgentGuard — it becomes an attack tool with a results page, which is a crowded, well-funded category AgentGuard has already declined to compete in on those terms (`strategy/market_type.md`, dominant risk). The closing argument is the same one `strategy/positioning.md` makes about the business as a whole: the mechanism is table stakes, adopted rather than invented; the comparison, enforced structurally (features 2, 3) and surfaced clearly (feature 16), is the product.
