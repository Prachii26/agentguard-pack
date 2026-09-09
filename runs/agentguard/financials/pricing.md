# Pricing

**What this is**: the pricing model — value metric, tiers, anchor, willingness-to-pay logic, and the pricing-power argument.

**Why it exists**: `strategy/market_sizing.md` and `strategy/gtm.md` used a placeholder pricing assumption pending founder sign-off; this document is that sign-off, made explicit and traceable. The failure this prevents: downstream financial arithmetic quietly resting on a number nobody actually decided on.

**How to read it**: every dollar figure below is founder-confirmed but still labeled `(assumption: illustrative, not final)` — this is a decision, not a measurement; no willingness-to-pay test has run.

**Depends on / feeds**: reuses `tech/not_vaporware.md` §3's cost-per-round derivation (not recomputed) and `strategy/market_sizing.md`'s SAM/SOM. Feeds `financials/revenue_build.md` and `financials/unit_economics.md` directly.

---

## Value metric: usage (per campaign), not seats

**(assumption: founder-confirmed, 2026-09-09)** — AgentGuard prices per campaign run, not per seat. Basis: `BRIEF.md`'s Business model already committed to self-serve, usage-based delivery across all three user tiers; a seat-based model would misalign price with value for a beachhead customer who runs campaigns quarterly (per-release cadence, `strategy/personas.md` Marcus) versus an edge-high customer running continuously — usage tracks actual value delivered (a comparison produced) in both cases, seats do not.

## Anchor: what budget line this replaces

Per `strategy/petal_diagram.md`, the closest existing budget lines are (1) AI/agent red-teaming service engagements (Petal 1: Adversa AI, Straiker, Mindgard — pricing "not public" per `research/competitors.md`, so no direct anchor available) and (2) engineering time currently spent running free OSS tools manually (Petal 4: Garak, PyRIT, AgentDojo/AutoDojo — `strategy/personas.md` Marcus's actual workaround). Neither anchor gives a clean comparable price point `(assumption: no competitor pricing found in research/sources.md — flagged, not invented)`.

## Competitor price table

| Competitor | Pricing model | Price | Source |
|---|---|---|---|
| Adversa AI | Not public | Not public | `research/sources.md` S50–S52 |
| Straiker | Not public | Not public | S63 |
| Mindgard | Not public | Not public | S44 |
| Giskard | OSS free / Hub subscription on request | Not public | S54 |
| SplxAI | Not public | Not public | S62 |
| Microsoft AI Red Teaming Agent | Bundled into Azure Foundry | No separate price | S60, S61 |

**No usable price anchor exists in the competitive set** — every direct competitor's pricing is undisclosed. This is itself informative: it means AgentGuard's tier design below cannot be validated against a market price and must be treated as a hypothesis, not a benchmark match.

## Tier design

**(assumption: founder-confirmed pricing, illustrative, not final — see `strategy/market_sizing.md` for the prior version this replaces)**:

| Tier | Price | What it buys |
|---|---|---|
| Free | $0 | 1 campaign/month (single defense, matched budget) — the top-of-funnel tier per `strategy/channel_plan.md` |
| Single-defense campaign | $750 `(assumption)` | One matched-budget adaptive campaign against one defense configuration |
| 4-defense Comparison Report | $2,500 `(assumption)` | All four defense families compared at matched budget in one bundled report — a ~17% discount off four standalone campaigns, pricing the bundle (the actual unit of value per `strategy/positioning.md`) below the sum of its parts |

No seat tiers, no annual contracts, no enterprise tier distinct in mechanism — `ASSUMPTIONS.md` A3 already established this uniformity; edge-high customers pay the same per-campaign price at higher volume, not a different price.

## Willingness-to-pay logic per persona

- **Priya (edge-low)**: the free tier (1 campaign/month) is designed to be sufficient for her actual need — a pre-launch pass/fail signal on a low-traffic side project (`strategy/personas.md`). She is not expected to convert to paid; she is the funnel, not the revenue.
- **Marcus (beachhead)**: per-release cadence (`strategy/gtm.md`: ~4 Comparison Reports/year) at $2,500 each ≈ $10,000/year — a plausible fraction of a security engineer's discretionary tooling budget, though untested `(assumption)`. His actual willingness-to-pay is unknown until `validation/experiment_board.md`'s pricing-page test runs.
- **Elena/David (edge-high)**: same per-campaign price, higher frequency (continuous rather than quarterly) — the willingness-to-pay question here is less "is $2,500 reasonable" and more "does a usage-based model without an annual contract clear procurement," a real open question `strategy/sales_roadmap.md` already flags as a probable blocker in year one.

## Pricing-power argument

`BRIEF.md`'s Moat section states plainly there is no moat yet. Consistent with that, this document makes **no claim that price can rise as a data moat compounds** — that would contradict `ASSUMPTIONS.md` A2's honest disclosure. The only defensible pricing-power argument available today: if the comparison-corpus hypothesis (`BRIEF.md` Moat) ever proves out, price could shift from per-campaign to per-comparison-insight (e.g., a defense-fingerprint subscription) — named here as a *future* possibility contingent on unproven data, not a current pricing lever.

## Recommended next 3

1. **Run a real willingness-to-pay test against the $750/$2,500 anchor before treating it as more than illustrative** — `strategy/business_model_canvas.md`'s Revenue Streams hypothesis test (an A/B on pricing-page framing) is the cheapest version of this.
2. **Do not add a seat-based or annual-contract tier without revisiting `ASSUMPTIONS.md` A3** — the uniform usage-based model is a deliberate, founder-confirmed choice, not a default.
3. **Revisit this document the moment any competitor discloses pricing** — the complete absence of a competitor price anchor is this document's biggest open risk, not a settled input.
