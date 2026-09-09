# AgentGuard — Mission, Vision, Values

**What this is**: mission (true today), vision (10 years out), and values (each a real trade-off the company would actually make), stated independently of any competitor.
**Why it exists**: `strategy/positioning.md` defines AgentGuard against Adversa AI, AutoDojo, and Microsoft — necessary for a pitch, but a definition that evaporates the moment those three entities change or disappear. This document is the one place the pack states why AgentGuard would still be worth building even if every named competitor vanished tomorrow. The failure it prevents: values that are actually virtues ("we value security," "we value transparency") that cost the company nothing to claim and reveal nothing about what it would sacrifice.
**How to read it**: read the values table first — each row names what gets deprioritized, not just what gets prioritized. A skeptic should be able to point to a real business decision (already made, in `BRIEF.md` or `product/PRD.md`) that each value actually explains.
**Depends on / feeds**: built from `BRIEF.md`'s Problem, Wedge, and Year-one scope sections and `product/PRD.md`'s Non-goals. Feeds nothing downstream — a terminal reference artifact other narrative pieces should stay consistent with, not build on.

---

## Mission (true today)

**AgentGuard tells security and ML platform teams how much protection a deployed defense actually buys their tool-using agent against an attacker willing to iterate, and what that protection costs in blocked legitimate work — reproducibly, not as a one-off engagement.**

This is true today in the sense that matters for a mission statement: it describes what the team is trying to build right now, at the capstone stage, not a future-state aspiration. It is deliberately narrower than "we secure AI agents" — AgentGuard does not ship a defense (`product/PRD.md` non-goal 5); it evaluates one.

## Vision (10 years out)

**A world where no team deploys a tool-using AI agent's defense without first knowing, from a standing and reproducible comparison, how it performs against every other defense family they were considering — the way no team ships infrastructure today without first knowing its load-testing numbers.**

Load testing is the useful analogy, not a coincidence: it became a standard release-gate practice not because one vendor won a market, but because the underlying measurement (does this hold up under realistic load, and what does it cost) became something every serious team expected to see before shipping. This vision is about the comparison-budget measurement becoming that kind of default expectation — consistent with `BRIEF.md`'s 10-year vision of the comparative evaluation protocol staying open and academically credible while a run-against-your-actual-defenses service is the paid product, and with `narrative/future_press.md`'s working-backwards scenario.

## Values (each a real trade-off)

| Value | The trade-off it actually means | Where this is already visible in the pack |
|---|---|---|
| **Report the null result.** | We will publish "the adaptive attacker did not beat the static baseline at this budget" if that is what a test shows, even though it undercuts our own founding claim — over quietly re-running the test until a more favorable number appears. | `BRIEF.md`'s Riskiest assumption section states explicitly that a null or negative gap is "a valid, reportable outcome," not a failure to hide. |
| **Adopt published technique over inventing a proprietary one.** | We will use AutoDojo's attack optimizer and AgentDojo's utility definition, attributed by name, over building an in-house "proprietary AI" story that would read better in a pitch — even when a from-scratch technique might be easier to defend as differentiated IP. | `product/PRD.md` non-goal 7 states the product will describe itself as running a "configurable attacker," never a "proprietary attack AI." |
| **Stay out of production, even when a customer asks.** | We will refuse to evaluate a target agent connected to real user data or live production tools, even if a customer would pay more for that access — over expanding scope to capture revenue a staging-only product structurally can't reach. | `BRIEF.md` Year-one scope item 1 and `product/PRD.md` §3.1 — a hard design boundary, not a "pro tier" upsell deferred to later. |
| **One system for every tier, not a bolted-on enterprise track.** | We will keep the same adaptive engine and defense set across the solo developer, the beachhead security team, and the enterprise red-team lead — over building a separate, more expensive "enterprise" feature set that might capture more revenue per deal. | `BRIEF.md` Users & spectrum and `ASSUMPTIONS.md` A3 — tiers differ in run frequency and volume only. |
| **State the moat honestly as unproven.** | We will describe our compounding-data hypothesis as untested in every downstream artifact, even in a fundraising conversation where a confident moat claim would land better — over overclaiming defensibility we can't yet back with real campaign volume. | `BRIEF.md` Moat section and `ASSUMPTIONS.md` A2 — explicit instruction that this must never be presented as an established advantage downstream. |

## Why we exist (independent of competitors)

Strip away every named competitor in `research/competitors.md` and the reason to build this doesn't disappear: a security team deploying a tool-using agent has no standing way to know, before shipping, whether the defense they picked would hold up against an adversary willing to try more than once — and no way to know what picking a stricter defense would cost them in legitimate work blocked. That gap exists independently of whether Adversa AI, AutoDojo, or Microsoft's Foundry Red Teaming Agent exist at all; it is a property of how defenses are evaluated today (against fixed attack sets, one at a time, without a paired utility number), not of who else is trying to fill it. `strategy/positioning.md` explains why AgentGuard is the one to fill it *right now, against these competitors*; this document is the answer to why the gap would still be worth closing if none of them existed.

## Recommended next 3

1. **Test the "report the null result" value against the actual riskiest-assumption test outcome** — this is the value most likely to be quietly abandoned under real pressure, and the one most worth holding the team accountable to.
2. **Revisit the "one system for every tier" value once real usage data exists** — if edge-high customers (Elena, David, Sofia's personas) turn out to need a genuinely different delivery motion, as `ASSUMPTIONS.md` A3 already flags as a live re-confirmation risk, this value should be revised openly, not silently violated.
3. **Do not let this document drift into positioning language** — if a future edit starts naming competitors to justify a value, move that content to `strategy/positioning.md` instead; this file's job is to stay true independent of them.
