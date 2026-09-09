# AgentGuard

An adaptive red-team/blue-team evaluation platform that runs the same budget-matched, feedback-only adaptive attack campaign against each of a target agent's candidate defenses and reports attack success and legitimate-task utility side by side — the standing, reproducible cross-defense comparison that neither the academic adaptive-attack literature (e.g. AutoDojo) nor proprietary red-teaming vendors (e.g. Adversa AI) currently publish. This originates as a CMPE 295A/295B graduate capstone project at San José State University (4-person team, two semesters); the startup framing is a positioning exercise on real research work, not a claim of an existing company. No implementation exists yet, and the venture has zero traction — no customers, revenue, funding, or pilots.

## Status

**PARTIAL — updated 2026-09-09.** 61 files on disk across Brief, Research, Strategy, Product, Tech, Narrative, and Validation (counted from the glob, not memory) · 0 visuals rendered. Phases complete: **0 (Brief)**, **1 (Research)**, **2 (Strategy)**, **3 (Product)**, **4 (Tech)**, **5 (Narrative)**, **6 (Validation)**. Phases 7–10 (Financials, Visuals, Audit, Website) have not started — **Financials explicitly waits on the founder's pricing sign-off**, per standing instruction. See `audit/CITATIONS.md` for the completed source-verification pass; `audit/COVERAGE.md` (the full req/opt manifest checklist) does not exist yet — it is phase 9's own deliverable, not generated early.

**Disclosed gap, not hidden**: Product, Tech, Narrative, and Validation (phases 3–6) were generated under an explicit same-day deadline and did **not** go through the three-persona critic loop that Strategy (phase 2) completed in full. Each phase's generating pass did its own internal quality check against `references/quality-bar.md` and cross-referenced sibling phases where available, and a targeted integration check confirmed the highest-risk failure mode (illustrative journey/demo numbers being mistaken for real campaign results) is handled correctly everywhere it appears — every such number carries an explicit "design-only, nothing has actually run" disclosure. But these four phases have not had an adversarial critic pass the way Strategy did, and should not be treated as equally hardened until they do.

**The wedge changed since phase 1, and stayed changed.** Research found AgentGuard's original claim ("we automate the adaptive adversary") already occupied by academic prior art (AutoDojo) and a commercial vendor (Adversa AI). The founder rejected three proposed replacements and resolved it (`ASSUMPTIONS.md` A9): AgentGuard's differentiator is **the comparison, not the attacker** — a standing, budget-matched, utility-paired comparison across defense families that no source found in research publishes. Every phase since (Strategy's positioning, Product's PRD, Tech's whitepaper, Narrative's memo and deck) is built around this resolution, not the original claim.

## Start here

1. [`BRIEF.md`](BRIEF.md) — the founder brief: problem, wedge, users, business model, riskiest assumption, year-one scope, vocabulary.
2. [`narrative/one_pager.md`](narrative/one_pager.md) — the single-page version of the whole pack.
3. [`narrative/vc_memo.md`](narrative/vc_memo.md) — the full technical-investor case, including the honest risks section.

## Reading paths by audience

- **Investor**: [`narrative/one_pager.md`](narrative/one_pager.md) → [`narrative/vc_memo.md`](narrative/vc_memo.md) → [`narrative/pitch_deck.md`](narrative/pitch_deck.md) — the deck's own "Recommended next 3" says plainly not to present it as a funding pitch given zero traction; treat the ask as design-partner/feedback-scoped.
- **Engineer / builder**: `BRIEF.md` → `research/capability_table.md` → `tech/whitepaper.md` (the mechanism-arithmetic case, built around the comparison protocol, not a claimed attack technique) → `tech/deep_dives.md` → `tech/architecture/00_INDEX.md` → `product/PRD.md` → `tech/not_vaporware.md`.
- **Operator / GTM**: `strategy/market_type.md` → `strategy/positioning.md` → `strategy/gtm.md` (90-day motion, capacity-budgeted against the actual 4-person team) → `validation/stage_gate.md` (where the company actually sits) → `validation/riskiest_assumptions.md` (what has to be true).
- **Researcher / skeptic**: `research/sources.md` (154 numbered citations) → `audit/CITATIONS.md` (the systematic verification pass — read this before trusting any number in the pack) → `research/competitors.md` → `ASSUMPTIONS.md` A9 → `strategy/positioning.md`.

## Full artifact map

| Path | What it holds | File count | Owning skill |
|---|---|---|---|
| `BRIEF.md`, `ASSUMPTIONS.md` | Founder brief and logged assumptions (9 tracked, A9 resolved) | 2 | grill-me |
| `research/` | Landscape, competitor teardown, capability table, survey, 154-entry sources list | 5 | startup-research |
| `strategy/` | Market type, positioning, market sizing, personas, lean canvas, value prop canvas, GTM, business model canvas, petal diagram, channel plan, sales roadmap — critic-loop hardened (3 rounds) | 11 | startup-strategy |
| `product/` | PRD, flagship + prioritized features, 4 journeys, UX spec | 8 | startup-product |
| `tech/` | Whitepaper (honest 3x–30x range, not a forced 10x), deep dives, 10 architecture diagrams + index, 2 technique waves (37 sourced techniques, wave 3 explicitly skipped as exhausted not padded), decision tree, technique/feature matrix, not-vaporware | 17 | startup-tech |
| `narrative/` | One-pager, VC memo, 14-slide deck, future press release, founder story, mission/vision | 6 | startup-narrative |
| `validation/` | Riskiest assumptions board, experiment board, discovery guide, get/keep/grow, stage gate, metrics by stage, pivot log, MVP definitions, decision-making unit | 9 | startup-validation |
| `audit/` | Systematic citation audit (90 sources checked, 12 corrected) | 1 | startup-audit (partial — COVERAGE.md pending) |

Not yet generated: `financials/` (waiting on founder pricing sign-off), `visuals/`, full `audit/COVERAGE.md`, `index.html`.

## Visual index

None rendered yet — visuals phase (8) has not started.

## Top 5 sharpest claims

1. **The adaptive-vs-static gap is real and large where measured**: a NIST/UK AI Security Institute human red-teaming exercise found hijack success rising from 11% (generic attacks) to 81% (adapted attacks) — a 7x jump — on the same AgentDojo-derived environment (`research/sources.md` S27).
2. **The status quo fails at a measurable, quantified rate**: 88% of organizations report a confirmed or suspected AI-agent security incident in the past year (S150, Gravitee, vendor-sourced); separately, orgs with over-privileged AI report a 76% incident rate vs. 17% for least-privilege deployments, a 4.5x gap (S154, Teleport, vendor-sourced) — both vendor-commissioned, read as convergent market signal, not audited ground truth.
3. **The differentiation is the comparison, not the attacker**: no source found in research publishes a standing, budget-matched, utility-paired comparison across defense families — AutoDojo measures ASR recovery within one framework and never reports utility; Adversa AI's engagements are proprietary and per-customer; Microsoft's AI Red Teaming Agent tests one deployment at a time (`strategy/positioning.md`).
4. **The tech layer's honest multiplier is "high single digits to low tens," not a confident 10x** — `tech/whitepaper.md` shows the arithmetic (3x–30x range, ~9.5x geometric midpoint, both bounds explicitly `(assumption)`) rather than asserting a round number.
5. **This is a graduate capstone with zero traction, stated plainly everywhere it matters** — the VC memo's risk section leads with it, the pitch deck's own recommended-next-3 says not to present it as a funding ask, and any paid customer is told upfront this is a research-stage engagement with no guarantee beyond the program's end (`strategy/gtm.md`).

## Completeness

**PARTIAL.** Phases 0 (Brief), 1 (Research), and 2 (Strategy) are complete and critic-loop hardened. Phases 3–6 (Product, Tech, Narrative, Validation) are complete but were generated in parallel under an explicit same-day deadline without the adversarial critic loop — a targeted integration check confirmed no fabricated-traction failures, but a full three-persona pass has not run on these four phases. A systematic citation audit (`audit/CITATIONS.md`) covers all 90 sources cited across every phase through Strategy; sources added or relied on more heavily by Product/Tech/Narrative/Validation have not had a second audit pass. Financials (phase 7) is explicitly blocked on the founder's pricing sign-off. Visuals, full audit coverage, and the website have not started.
