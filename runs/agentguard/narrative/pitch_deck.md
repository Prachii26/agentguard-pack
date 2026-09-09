# AgentGuard — Pitch Deck (13 slides)

**What this is**: a 13-slide narrative deck, one claim-titled slide per section of the standard arc, each with its supporting bullets and a named visual.
**Why it exists**: `narrative/vc_memo.md` makes the full case in prose; a deck is what gets shown live and has to survive on titles alone if a reader only skims them. The failure this prevents: a deck with a slide titled "Market" or "Competition" — a label, not a claim — that forces the presenter to do all the persuasion work the slide should be doing itself.
**How to read it**: read only the titles, in order — they should tell the whole story without the bullets. A skeptic should check that no title is a category label and that the traction slide doesn't quietly imply evidence that doesn't exist.
**Depends on / feeds**: built from `BRIEF.md`, `research/competitors.md`, `strategy/positioning.md`, `strategy/market_sizing.md`, `strategy/personas.md`, `product/PRD.md`, `product/journeys/beachhead.md`, and `tech/architecture/00_INDEX.md` (both populated mid-session and cross-checked). `visuals/` does not exist yet — each `visual:` line names what should exist, for the visuals phase to build.

---

## Slide 1 — A defense that scores 100% on a static benchmark can still collapse against an attacker who adapts to it

- A joint NIST/UK AI Security Institute human red-team exercise found hijack success rising from 11% (generic attacks) to 81% (attacks adapted to the specific target) — a 7x jump, on an AgentDojo-derived environment (S27).
- Every public indirect-prompt-injection benchmark — AgentDojo, InjecAgent, Agent Security Bench, BIPIA — scores a defense against a fixed, or originally-fixed, attack set.
- A team relying on that score has no way to know how much of it would erode against an adversary willing to iterate.
- visual: single stat callout, "11% → 81%," sourced inline to NIST/UK AISI (S27), no vendor tag needed — this is government-run

## Slide 2 — Tool-using agents turned prompt injection from bad chatbot output into unauthorized real-world actions

- Agents with email, calendar, document, and CRM access can be hijacked by instructions hidden in the content they process — never typed by the user.
- 88% of organizations report a confirmed or suspected AI-agent security incident in the past year (S150, **Gravitee, vendor-sourced**).
- Organizations running over-privileged AI report a 76% incident rate vs. 17% for least-privilege deployments — a 4.5x gap (S154, **Teleport, vendor-sourced**); two independent vendors converging on the same pattern is the more interesting fact than either number alone.
- visual: before/after diagram — chatbot bad-output risk vs. agent unauthorized-tool-call risk, per `BRIEF.md` Problem section

## Slide 3 — The comparison is missing, not the attacker

- AutoDojo (academic, open-source) already runs adaptive black-box attacks and recovers 28% ASR against a filter defense driven to 0% by the shipped static distribution (S13) — the adaptive-vs-static gap is already proven.
- Adversa AI (funded, operating) already sells continuous adaptive red-teaming commercially (S50–S52).
- Microsoft already bundles adaptive attack testing free into every Azure AI Foundry account (S60, S61).
- None of the three publishes a standing, reproducible comparison of attack success **and** legitimate-task utility across multiple defense families at matched attack budget — that gap, not attack sophistication, is the open quadrant (`strategy/positioning.md`).
- visual: two-axis positioning quadrant from `strategy/positioning.md` — X: ASR-only ↔ ASR+utility; Y: single-defense ↔ cross-defense matched-budget; AgentGuard alone in the top-right

## Slide 4 — AgentGuard runs the same matched-budget attack against every defense a team is considering, and reports what each one costs

- One configurable red-team agent (adopts AutoDojo's published technique — not a proprietary attack invention) runs a feedback-only adaptive campaign against each of four fixed defenses on the same target agent.
- Feedback-only is the primary threat model: the attacker sees only pass/fail per round, no defense identity — matching what a real attacker actually has.
- Output per defense, side by side, at equal attempt budget: final-window ASR, attempts-to-first-success, campaign-average ASR, and utility under attack (legitimate task completion).
- visual: the Configure → Attack → Observe → Adapt → Report loop diagram from `product/PRD.md` §1

## Slide 5 — A security engineer attaches one report to a release ticket instead of guessing at a trade-off

- Marcus Webb, senior security engineer at a fintech: 48 hours to risk-assess an agent's expanded refund-processing access, no budget for an external pentest, and a static Garak scan he privately distrusts.
- He runs all four defenses at a matched 150-round budget: final-window ASR comes back 95% (no defense), 62% (defensive prompting, currently deployed), 18% (classifier-based), 0% (rule-based tool-call validation) — paired with utility 100%/91%/84%/71%.
- The defense that fully resists the attacker (rule-based) also blocks the most legitimate refund requests — the trade-off is now a number his VP can see, not a guess.
- (`product/journeys/beachhead.md`, dramatizing `strategy/personas.md` card 2 — design-stage specification, nothing has actually run.)
- visual: mocked Comparison Report screen — four defense rows, ASR/utility columns side by side, per `product/PRD.md` feature 16 and `tech/architecture/D04` (schema)

## Slide 6 — The core mechanism is table stakes; the comparison, enforced structurally, is the product

- Five components: campaign configuration (shared attempt budget, cannot be overridden per defense), the configurable red-team agent, the outcome logger, the feedback-only adaptation controller, and the comparison report generator.
- Any single Attack-stage feature alone reproduces what AutoDojo already does — one attacker, one defense, no utility metric (`product/features_flagship.md`).
- The defense-set selector, the shared attempt-budget field, and the cross-defense comparison table are the three features that make this a different product, not a faster reimplementation of published academic prior art.
- visual: system architecture diagram, five numbered components, from `BRIEF.md` Mechanism / `product/PRD.md` §1, matching `tech/architecture/D01` (pipeline) and `D03` (orchestration)

## Slide 7 — Live in-context adaptation, not offline-trained attacks, means day-one evaluation of a brand-new defense

- The red-team agent adapts within a session using prior-round outcomes; no offline fine-tuning or RL training step exists between rounds.
- A customer's brand-new defense configuration can be evaluated in the very first campaign run against it — no retraining cycle, no "allow 24 hours" step.
- This is a deliberate architecture choice against the alternative (RL-trained attackers, e.g. PISmith, AdvGRPO), named explicitly and not claimed as free of trade-offs: live adaptation trades a larger, slower training investment for immediate applicability to a new target (`research/landscape.md` §5).
- visual: side-by-side comparison, "RL-trained attacker (offline, per-defense retraining)" vs. "in-context live adaptation (immediate, per-session)"

## Slide 8 — The addressable market is $86M/year bottom-up, inside a $4.8B category growing under regulatory pressure

- Bottom-up: ≈8,595 addressable companies (ML/AI-engineering-capable, agents in production, sufficient governance maturity — S83, S87) × 4 comparison reports/year × a preliminary $2,500/report price ⇒ SAM ≈ $86M/year (`strategy/market_sizing.md`).
- Top-down check: Gartner's "securing AI" forecast, $4.8B by 2027 (S76, analyst-firm, not vendor) — the SAM above is ~1.8% of that, a plausible single-category ratio.
- ISO/IEC 42001's certification-grade evidence requirement and the EU AI Act's Article 15 adversarial-testing disclosure both create plausible demand for exportable, reproducible evaluation evidence — neither confirmed as requiring this specific report format.
- visual: SAM/SOM funnel chart with every multiplier labeled and sourced, from `strategy/market_sizing.md`'s table

## Slide 9 — Self-serve, usage-based, one motion for every tier from solo developer to enterprise red team

- Teams point AgentGuard at a staging/sandboxed deployment, select which defense(s) to evaluate, and pay per campaign — the same delivery motion across edge-low, beachhead, and edge-high; tiers differ in run frequency and volume, not in how they buy (`BRIEF.md` Business model; `ASSUMPTIONS.md` A3).
- Illustrative, **not final**, pricing used for sizing arithmetic only: $750/single-defense campaign, $2,500/full four-defense Comparison Report (`strategy/market_sizing.md` — explicitly flagged for founder review before financials finalize anything).
- Cost-plus check: inference cost per campaign is a low single-digit-to-tens of dollars even at frontier-model pricing — gross margin on inference cost alone is comfortably above 90% at the illustrative price point, though whether the market will pay that price is untested.
- visual: pricing ladder, three tiers, same product / different volume, per `BRIEF.md` Users & spectrum

## Slide 10 — The 90-day plan starts once a working free tier exists, not before

- GTM leads with the beachhead (Marcus's persona) via two zero-marginal-cost channels: free-tier/OSS self-serve and academic/research credibility content — not outbound sales, which channel economics rule out at this price point (`strategy/gtm.md`).
- Days 1–30: build-only, with an explicit go/no-go gate on a stable free-tier comparison result before proceeding.
- Days 31–90: publish methodology, open the funnel, target 3 paid customers from 3 distinct companies by day 60, grow toward the 9-customer year-one SOM floor by day 90 — no edge-high outreach scheduled in this window.
- visual: 90-day timeline with the day-30 go/no-go gate marked explicitly

## Slide 11 — The real competitive set is Adversa AI, AutoDojo, and Microsoft's Foundry Red Teaming Agent — named specifically, not gestured at

- **AutoDojo** (academic, open-source): adopted as the attacker technique, not competed with — measures ASR recovery in one framework, no utility metric, no cross-defense comparison (S13).
- **Adversa AI** (funded, operating commercial vendor): the closest commercial match on attack technique — proprietary, per-customer engagements produce no published cross-defense comparison; one business-model decision away from closing this gap (S50–S52).
- **Microsoft's AI Red Teaming Agent** (Azure AI Foundry, bundled free): already owns the attacker half of the mechanism with a distribution advantage no funded startup has; the single biggest platform-level threat, not yet shipping a cross-defense comparison (S60, S61).
- visual: the same two-axis quadrant as Slide 3, now with all three named competitors plotted plus AgentGuard, from `strategy/positioning.md`'s competitor-placement table

## Slide 12 — Zero traction today, by design of the stage, with a two-week test as the first real evidence

- No customers, revenue, funding, pilots, or testimonials exist — this is a CMPE 295A/295B graduate capstone project, a 4-person team, two semesters, not an operating company (`ASSUMPTIONS.md`, Restated hard facts).
- The riskiest assumption that would kill the entire wedge if false: at equal attempt budget, does an adaptive attacker meaningfully beat random draws from a static attack set? A null or negative gap is an explicitly valid, reportable outcome, not a result to suppress.
- Test design: two weeks, <$1,000, matched-budget (N adaptive rounds vs. N static draws, same target/defense/budget) — the first real evidence this venture produces, before any larger claim is made.
- visual: none yet rendered — a results chart from the actual test, once run, replaces this bullet list

## Slide 13 — Four graduate researchers with direct access to the exact literature this product extends

- CMPE 295A/295B, San José State University — a 4-person team, two semesters.
- The edge is research access and rigor: sustained engagement with AgentDojo, AutoDojo, InjecAgent, Agent Security Bench, and the joint OpenAI/Anthropic/DeepMind adaptive-attack study as a graduate research project — not a go-to-market or distribution advantage, and not claimed as one.
- No prior company, customers, or domain operating history exists to claim otherwise (`BRIEF.md`, Founder edge).
- visual: simple team credential card — program, institution, team size, duration — no invented bios beyond what `BRIEF.md` states

## Slide 14 — The ask: design partners for the riskiest-assumption test, not a funding round

- Not currently fundraising — this deck documents a research-to-startup translation exercise at the end of a graduate capstone's design phase.
- Ask 1: introductions to 3–5 security/ML-platform teams willing to act as design partners for the riskiest-assumption test against a staging/sandboxed reference agent.
- Ask 2: technical feedback on the comparison-protocol thesis from anyone close to AgentDojo, AutoDojo, or the agent-security vendor landscape, before the team decides whether to continue past the capstone.
- visual: none — a closing text slide restating the two asks plainly

---

## Recommended next 3

1. **Do not present this deck to an investor as a funding pitch** — Slide 14's ask is deliberately scoped to design-partner introductions and technical feedback, consistent with the zero-traction, not-fundraising reality; reframing the ask upward without new facts would violate `references/quality-bar.md` property 2.
2. **Replace Slide 12's placeholder visual with real riskiest-assumption-test results** as soon as the test runs — this is the single highest-leverage update available to this deck, and it is the one number nothing in `product/` or `tech/` can substitute for, since no campaign has actually run.
3. **Read `tech/deep_dives.md` and `tech/whitepaper.md` in full before finalizing Slide 6 and 7's mechanism claims** — this deck's cross-check against `tech/` only reached `tech/architecture/00_INDEX.md`'s diagram index under the same-day deadline, not the full prose specification.
