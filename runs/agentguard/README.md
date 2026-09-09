# AgentGuard

An adaptive red-team/blue-team evaluation platform that runs the same budget-matched, feedback-only adaptive attack campaign against each of a target agent's candidate defenses and reports attack success and legitimate-task utility side by side — the standing, reproducible cross-defense comparison that neither the academic adaptive-attack literature (e.g. AutoDojo) nor proprietary red-teaming vendors (e.g. Adversa AI) currently publish. This originates as a CMPE 295A/295B graduate capstone project at San José State University (4-person team, two semesters); the startup framing is a positioning exercise on real research work, not a claim of an existing company. No implementation exists yet, and the venture has zero traction — no customers, revenue, funding, or pilots.

## Status

**PARTIAL — generated 2026-09-09.** 19/61 required artifacts (counted from the glob, not memory) · 0 visuals rendered. Phases complete: **0 (Brief)**, **1 (Research)**, **2 (Strategy)**. Phases 3–10 (Product, Tech, Narrative, Validation, Financials, Visuals, Audit, Website) have not started. See `audit/COVERAGE.md` for the row-by-row gap list once it exists — it does not exist yet at this stage of the run.

**The wedge changed since phase 1.** Research found AgentGuard's original claim ("we automate the adaptive adversary") already occupied by academic prior art (AutoDojo) and a commercial vendor (Adversa AI). The founder rejected three proposed replacements and resolved it (`ASSUMPTIONS.md` A9): AgentGuard's differentiator is **the comparison, not the attacker** — a standing, budget-matched, utility-paired comparison across defense families that no source found in research publishes. `strategy/positioning.md` and `BRIEF.md`'s Wedge/Mechanism/Moat/Competition sections are built around this resolution.

## Start here

1. [`BRIEF.md`](BRIEF.md) — the founder brief: problem, wedge, users, business model, riskiest assumption, year-one scope, vocabulary.
2. [`strategy/positioning.md`](strategy/positioning.md) — the two axes, the open quadrant, and why it stays open only as a window, not a moat.
3. [`strategy/market_type.md`](strategy/market_type.md) — the re-segmented-niche declaration every other strategy artifact inherits.

## Reading paths by audience

- **Investor** (once `narrative/` exists): one-pager → VC memo → pitch deck. Not yet generated.
- **Engineer / builder**: `BRIEF.md` → `research/capability_table.md` (enabling tech, what's proven vs. not) → `research/survey.md` (scientific grounding, evidence for/against the core mechanism).
- **Operator / GTM**: `strategy/market_type.md` → `strategy/positioning.md` → `strategy/gtm.md` (90-day motion, capacity-budgeted against the actual 4-person team) → `strategy/channel_plan.md` (per-channel economics).
- **Researcher / skeptic**: `research/sources.md` (150 cited facts, numbered) → `research/competitors.md` (the corrected competitive teardown) → `ASSUMPTIONS.md` A9 (the differentiation resolution) → `strategy/positioning.md` (how A9 became a strategy).

## Full artifact map

| Path | What it holds | File count | Owning skill |
|---|---|---|---|
| `BRIEF.md`, `ASSUMPTIONS.md` | Founder brief and logged assumptions (9 logged, 3 still open) | 2 | grill-me |
| `research/` | Landscape, competitor teardown, capability table, survey, 150-entry sources list | 5 | startup-research |
| `strategy/` | Market type, positioning, market sizing, personas, lean canvas, value prop canvas, GTM, business model canvas, petal diagram, channel plan, sales roadmap | 11 | startup-strategy |

All other manifest directories (`product/`, `tech/`, `narrative/`, `validation/`, `financials/`, `visuals/`, `audit/`) do not exist yet.

## Visual index

None rendered yet — visuals phase (8) has not started.

## Top 5 sharpest claims

1. **The adaptive-vs-static gap is real and large where measured**: a NIST/UK AI Security Institute human red-teaming exercise found hijack success rising from 11% (generic attacks) to 81% (adapted attacks) — a 7x jump — on the same AgentDojo-derived environment (`research/sources.md` S27).
2. **The status quo fails at a measurable, quantified rate**: 88% of organizations report a confirmed or suspected AI-agent security incident in the past year; orgs without least-privilege enforcement report a 76% incident rate vs. 17% for those that enforce it (`research/sources.md` S150).
3. **The differentiation is the comparison, not the attacker**: no source found in research publishes a standing, budget-matched, utility-paired comparison across defense families — AutoDojo measures ASR recovery within one framework and never reports utility; Adversa AI's engagements are proprietary and per-customer; Microsoft's AI Red Teaming Agent tests one deployment at a time (`strategy/positioning.md`).
4. **The riskiest assumption has a specific, cheap, two-week test**: a matched-budget comparison (N adaptive rounds vs. N random static draws, same target/defense/budget) that reports the ASR gap either way, including a null result (`BRIEF.md`, Riskiest assumption).
5. **This is a graduate capstone with zero traction, stated plainly, including what that means for continuity**: no customers, revenue, funding, or pilots exist; any paid customer acquired during the capstone window is told upfront this is a research-stage engagement with no service guarantee beyond the program's end (`strategy/gtm.md`).

## Completeness

**PARTIAL.** Phases 0 (Brief), 1 (Research), and 2 (Strategy) are complete — Strategy's 11 artifacts passed a three-persona critic loop (skeptical VC, domain PhD, operator-founder) across up to three revision rounds, surfacing and fixing a real citation-integrity error (two statistics were miscited to the wrong sources and have been corrected at the source layer, not just patched downstream) plus several major planning gaps (GTM timeline ignoring that nothing is built yet, no team capacity budget, no campaign-cost check on pricing, no post-capstone continuity answer). Phases 3 through 10 have not started. No `audit/COVERAGE.md` exists yet — it is generated in phase 9.
