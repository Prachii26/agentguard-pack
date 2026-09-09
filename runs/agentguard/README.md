# AgentGuard

An adaptive red-team/blue-team evaluation platform that automates an adversary who evolves indirect-prompt-injection attacks round over round against a target agent's deployed defense — primarily from per-round pass/fail feedback alone, the way a real attacker would experience it — so security and ML platform teams learn whether their guardrails hold against an *adapting* attacker, not just the fixed attack sets in AgentDojo, InjecAgent, Agent Security Bench, or BIPIA. This originates as a CMPE 295A/295B graduate capstone project at San José State University (4-person team, two semesters); the startup framing is a positioning exercise on real research work, not a claim of an existing company. No implementation exists yet, and the venture has zero traction — no customers, revenue, funding, or pilots.

## Status

**PARTIAL — generated 2026-09-09.** 7/61 required artifacts (counted from the glob, not memory) · 0 visuals rendered. Phases complete: **0 (Brief)**, **1 (Research)**. Phases 2–10 (Strategy, Product, Tech, Narrative, Validation, Financials, Visuals, Audit, Website) have not started. See `audit/COVERAGE.md` for the row-by-row gap list once it exists — it does not exist yet at this stage of the run.

**Open, founder-facing decision blocking phase 2**: research surfaced that AgentGuard's original wedge claim ("we automate the adaptive adversary; existing benchmarks are static") is only half-defensible — it correctly distinguishes AgentGuard from the four named academic baselines, but not from several 2025–2026 academic papers and one commercial vendor (Adversa AI) that already do something close to adaptive attack evolution against agent defenses. See `ASSUMPTIONS.md` A9 and `research/competitors.md` for the full finding and three candidate narrower differentiators. Strategy work should not proceed until this is resolved.

## Start here

1. [`BRIEF.md`](BRIEF.md) — the founder brief: problem, wedge, users, business model, riskiest assumption, year-one scope, vocabulary. The single source of truth every other artifact reads.
2. [`ASSUMPTIONS.md`](ASSUMPTIONS.md) — every choice made without founder confirmation, including the A9 open question above.
3. [`research/competitors.md`](research/competitors.md) — the competitive teardown that most changes how the pitch should be framed; read this before reading anything that assumes the original wedge framing is still accurate as first written.

## Reading paths by audience

- **Investor** (once narrative/ exists): one-pager → VC memo → pitch deck. Not yet generated.
- **Engineer / builder**: `BRIEF.md` → `research/capability_table.md` (enabling tech, what's proven vs. not) → `research/survey.md` (scientific grounding, evidence for/against the core mechanism).
- **Operator / GTM**: `BRIEF.md` (Business model, Year-one scope) → `research/competitors.md` (positioning read, two-axis white-space analysis).
- **Researcher / skeptic**: `research/sources.md` (every cited fact, numbered) → `research/landscape.md` §1 (the direct-approaches teardown, where the uncomfortable finding lives) → `ASSUMPTIONS.md` A9.

## Full artifact map

| Path | What it holds | File count | Owning skill |
|---|---|---|---|
| `BRIEF.md`, `ASSUMPTIONS.md` | Founder brief and logged assumptions | 2 | grill-me |
| `research/` | Landscape, competitor teardown, capability table, survey, sources | 5 | startup-research |

All other manifest directories (`strategy/`, `product/`, `tech/`, `narrative/`, `validation/`, `financials/`, `visuals/`, `audit/`) do not exist yet.

## Visual index

None rendered yet — visuals phase (8) has not started.

## Top 5 sharpest claims

1. **The adaptive-vs-static gap is real and large where measured**: a U.S. government-backed fork of AgentDojo found hijack success rising from 11% (generic attacks) to 81% (adapted attacks) — a 7x jump — on the same environment (`research/sources.md` S27).
2. **The status quo fails at a measurable, quantified rate**: 88% of organizations report a confirmed or suspected AI-agent security incident in the past year; orgs without least-privilege enforcement report a 76% incident rate vs. 17% for those that enforce it (`research/sources.md` S76).
3. **The original differentiation claim needs narrowing**: at least four 2025–2026 papers and one funded commercial vendor already attempt adaptive attack evolution against agent defenses — AgentGuard's defensible edge, if any, is standalone productized delivery and breadth across arbitrary customer defenses, not the underlying idea (`research/competitors.md`).
4. **The riskiest assumption has a specific, cheap, two-week test**: a matched-budget comparison (N adaptive rounds vs. N random static draws, same target/defense/budget) that reports the ASR gap either way, including a null result (`BRIEF.md`, Riskiest assumption).
5. **This is a graduate capstone with zero traction, stated plainly**: no customers, revenue, funding, or pilots exist, and none are invented anywhere in this pack (`ASSUMPTIONS.md`, Restated hard facts).

## Completeness

**PARTIAL.** Phases 0 (Brief) and 1 (Research) are complete and reviewed for citation currency; phases 2 through 10 have not started, and a founder decision on the differentiation question (`ASSUMPTIONS.md` A9) is needed before strategy work begins. No `audit/COVERAGE.md` exists yet — it is generated in phase 9.
