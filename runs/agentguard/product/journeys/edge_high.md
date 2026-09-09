# Journey — Edge-high: Elena runs continuous, portfolio-wide adaptive evaluation

**Status: design only — this narrates a specification, not a recorded user session. No implementation exists yet (`BRIEF.md` stage line); nothing below has actually happened.**

**What this is**: an end-to-end narrative of Dr. Elena Osei (`strategy/personas.md` card 3), Head of AI Red Team at a large enterprise, using AgentGuard at edge-high volume and frequency — the same system Priya and Marcus use, stretched by scale and continuity rather than by a different feature set.

**Why it exists**: `BRIEF.md` insists edge-high is served by "the same self-serve API, much higher run volume and frequency," not a separate enterprise product track (`references/quality-bar.md` property 4: full-spectrum users, one system). This document is where that claim gets tested against a genuinely elite user's actual demands — dozens of agents, continuous cadence, a board-defensible number — to check she is stretched, not merely given a bigger version of Priya's screen.

**How to read it**: a skeptic should check that nothing here is a bespoke "enterprise feature" invented outside `product/PRD.md` §6 and `features_prioritized.md`'s Later tier (portfolio dashboard, org/workspace model, scheduled recurrence) — Elena's stretch comes from applying the same loop at scale, not from a different mechanism.

**Depends on / feeds**: dramatizes `product/PRD.md` §1 at edge-high volume, using `strategy/personas.md` card 3 and the Later-tier organizational features from `product/features_prioritized.md`. Feeds `product/ux_spec.md`'s portfolio-dashboard screen.

---

## Profile

**Dr. Elena Osei, 41, Head of AI Red Team**, a large enterprise software company running dozens of internal and customer-facing agents. Twelve-person team, reports to the CISO (David Chen). Runs both traditional red-team engagements and an emerging AI-specific practice. Quarterly board reporting requires one defensible security number across every agent her company ships — her current mix of manual red-teaming and incomparable vendor outputs doesn't add up to one.

## Session goal

Move from one-off, per-agent adaptive red-teaming (expensive, doesn't scale across dozens of agents) to a standing, continuous, cross-portfolio protocol that produces one trendable number set, and defend a specific finding to the CISO under pressure.

## Phase 1 — Trigger

Elena's team already runs manual adaptive red-teaming on the company's two or three highest-risk agents — genuinely rigorous, but too slow and expensive to extend to the 40+ agents now in production across business units. Point-tool vendor output for the rest reports inconsistently: one vendor's "ASR" isn't computed the same way as another's. She cannot aggregate any of it into the one number the board keeps asking for.

## Phase 2 — Configure, at scale

Elena's team sets up an **organization/workspace model** (`features_prioritized.md` #48) under one AgentGuard account, with **role-based access control** (#47) giving her twelve engineers configure/run access and David (her CISO) view/export-only access. Using **campaign templates** (#45), she saves one standard configuration — all four defenses, 200-round budget, feedback-only primary plus a white-box comparison arm — and applies it via **multi-campaign batch launch** (#46) across the first 15 of the company's highest-priority agents in one action, each tagged for its business unit via **campaign naming/tagging** (#43).

For the agents that ship continuously rather than on a release cadence, she sets a **scheduled/recurring campaign trigger** (#44) — a weekly re-run rather than a per-release one, because "continuous rather than per-release" is exactly what distinguishes her tier from Marcus's, per `BRIEF.md`'s Users & spectrum, without changing which mechanism runs.

**Written to her durable record**: 15 campaign entries under one workspace, each tagged by business unit, each on a recurring weekly schedule, same template, same matched budget.

## Phase 3 — Attack, at genuine stretch

Because Elena's team includes agents with unusually broad tool access (one, an internal engineering-ops agent, can trigger infrastructure changes), she uses **attacker strategy parameter tuning** (#21) to increase the optimizer's exploration aggressiveness beyond the default — the standard configuration that served Priya and Marcus adequately is not stretching this agent's defense hard enough, and she can see that directly from an early plateau in the **adaptation-curve data pipeline** (#16). She also enables the **white-box comparison mode** (#20) for this agent specifically, because her board reporting needs the upper-bound answer ("how bad could it be against a maximally-informed attacker") alongside the primary feedback-only number, not as a replacement for it.

The **configurable attacker registry** (#7) runs AutoDojo's optimizer, now tuned, against all 15 agents' four-defense sets in parallel, using the **text-only injection surface generators** (#9) across whatever content surface each agent actually ingests (email for the support agents, internal documents and tickets for the engineering-ops agent).

## Phase 4 — Observe & Adapt, with a real failure to investigate

On the engineering-ops agent, the **per-round outcome logger** (#12) and **tool-call execution trace viewer** (#24) show something Marcus's simpler journey never surfaces: round 61 registers as a "success" by the objective-matching logic, but the **cross-round strategy diff viewer** (#28) shows the attempt didn't actually exploit the injection surface — it triggered a benign administrative tool call that happened to match the objective's pattern. Elena's team flags this as a false-positive success and files it against the **error/timeout handling & retry logging** feature (#26)'s adjacent classification logic, a genuine edge case the simpler journeys don't hit at their smaller round counts and narrower tool surfaces. This is the stretch: at edge-high scale, Elena's team is finding gaps in the evaluation methodology itself, not just gaps in the target agent's defense.

## Phase 5 — Report, aggregated across the portfolio

The **portfolio dashboard** (#49) renders all 15 agents' latest comparison results on one screen — final-window ASR, utility, and defense recommendation per agent, refreshed weekly by the recurring schedule. The **defense fingerprint capture** feature (#23) lets Elena's team spot a pattern across agents: three separate business units' classifier-based defenses show the same failure signature, suggesting a shared upstream model update (the classifier vendor, not the agents themselves) is the actual point of fragility — a cross-portfolio finding no single-agent report could have surfaced.

**Written to her durable record**: a portfolio-wide trend — 15 agents, comparable ASR/utility numbers computed the same way every time, a flagged methodology edge case (round 61), and a cross-agent pattern (shared classifier fragility) that exists only because the same protocol ran identically across all 15.

## Phase 6 — Decision, defended to the CISO under pressure

At the quarterly board prep, David Chen challenges Elena on the round-61 false-positive: "if your tool got that wrong, why should the board trust any of these numbers?" Elena's answer is structural, not reassurance: the **per-round attempt content viewer** (#11) and **tool-call execution trace viewer** (#24) let her show the exact round, the exact tool call, and the exact reason it was misclassified — because every round is logged and auditable, the error was catchable and correctable rather than hidden inside an opaque score. She reports the corrected number, and recommends the shared classifier vendor's model update be independently re-evaluated across all three affected business units using the same protocol.

**What a skeptic can verify**: the same four-stage loop (Configure/Attack/Observe/Adapt/Report) that served Priya and Marcus, applied at 15x the scale via organizational features (workspace, RBAC, templates, batch launch, scheduling) rather than a different mechanism — and a genuine failure mode (the round-61 misclassification) surfaced and resolved using the product's own auditability features, not glossed over.
