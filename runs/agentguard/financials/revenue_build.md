# Revenue build — $1M → $10M → $50-100M ARR

**What this is**: the bottom-up path from first revenue to $50-100M ARR — units × conversion × price per stage, the milestone each jump depends on, and which GTM motion carries it.

**Why it exists**: `strategy/market_sizing.md` sized the SOM at $90K-$430K/year for the beachhead alone; this document is where that number becomes a staged path with named milestones, not a hockey stick with no bend.

**How to read it**: every stage's jump depends on a named, falsifiable milestone from `validation/riskiest_assumptions.md` or `validation/stage_gate.md` — a reader should be able to check that the milestone, not optimism, causes the bend.

**Depends on / feeds**: built from `financials/pricing.md`, `strategy/market_sizing.md`, `strategy/gtm.md`, `validation/stage_gate.md`. Feeds `financials/unit_economics.md` and `financials/use_of_funds.md`.

---

## Stage 1: First revenue → $1M ARR

| Driver | Value | Basis |
|---|---|---|
| Customers (beachhead) | ~100 | `(assumption)` — top of `strategy/market_sizing.md`'s SOM range (9–43) extended past year one, assuming `strategy/gtm.md`'s 90-day motion succeeds and continues at a similar pace |
| Comparison Reports/customer/year | 4 | `strategy/market_sizing.md` — per-release cadence |
| Price | $2,500/report | `financials/pricing.md` `(assumption)` |
| **Revenue** | **~$1.0M** | 100 × 4 × $2,500 |
| Milestone that causes this jump | The riskiest-assumption test returns a positive matched-budget ASR gap (`validation/riskiest_assumptions.md` #1) — without this, the product has nothing to sell | `BRIEF.md` Riskiest assumption |
| GTM motion | Self-serve, OSS/academic-credibility channel only (`strategy/channel_plan.md`) — no sales team | `ASSUMPTIONS.md` A3 |

## Stage 2: $1M → $10M ARR

| Driver | Value | Basis |
|---|---|---|
| Customers (beachhead, scaled) | ~700 | `(assumption)` — a 7x customer scale, not a price increase, consistent with the uniform-pricing model (`ASSUMPTIONS.md` A3) |
| Comparison Reports/customer/year | 5 | `(assumption)` — modest cadence increase as continuous evaluation (rather than purely per-release) becomes more common |
| Price | $2,500/report | Unchanged — `financials/pricing.md` states no pricing-power lever exists yet |
| **Revenue** | **~$8.75M**, rounding to the $10M band with a modest edge-high contribution below | 700 × 5 × $2,500 |
| Expansion layer | A small number of edge-high accounts (Elena/David-type) converting at continuous-use volume — `strategy/sales_roadmap.md`'s "weight edge-high revenue conservatively (or at zero) for year one" implies this layer only appears from Stage 2 onward, not Stage 1 | `strategy/sales_roadmap.md` |
| Milestone that causes this jump | The free-tier→paid conversion funnel (`strategy/gtm.md`) demonstrates a repeatable, non-founder-dependent motion — i.e., growth survives the capstone team's own time constraints (`strategy/gtm.md`'s capacity budget) | `strategy/business_model_canvas.md` Channels hypothesis |
| GTM motion | Still self-serve-led; first edge-high conversations begin (deferred past the 90-day window per `strategy/gtm.md`, not before) | `strategy/gtm.md` |

## Stage 3: $10M → $50-100M ARR

| Driver | Value | Basis |
|---|---|---|
| Customers | ~2,000–4,000 blended beachhead + edge-high | `(assumption)` — requires the SAM (`strategy/market_sizing.md`: ~8,595 addressable companies) to be substantially penetrated, well beyond the conservative SOM this pack sized for year one |
| Comparison Reports/customer/year | 6–8 (continuous evaluation becoming the norm, not per-release) | `(assumption)` |
| Price | $2,500/report, or a shift to a comparison-corpus-based pricing lever if `BRIEF.md`'s Moat hypothesis proves out | `financials/pricing.md`'s pricing-power argument — explicitly contingent, not assumed |
| **Revenue** | **~$50-100M**, wide range reflecting the pricing-lever uncertainty | Customers × cadence × price |
| Milestone that causes this jump | Either (a) the SAM's ~8,595-company ceiling is approached, requiring TAM expansion beyond the current "securing AI" category, or (b) the comparison-corpus moat hypothesis proves out, enabling a pricing shift — this stage genuinely depends on one of these two uncertain events, not a straight-line extrapolation | `strategy/market_sizing.md`, `BRIEF.md` Moat |
| GTM motion | Likely requires the two-motion model (`ASSUMPTIONS.md` A3 flags this as worth re-confirming) if edge-high becomes a material revenue share — self-serve alone may not carry this stage | `ASSUMPTIONS.md` A3 |

## What this table does not claim

This is not a committed forecast — `ASSUMPTIONS.md`'s Restated hard facts stand: zero traction, zero funding, zero implementation exist today. Stage 1 has not started. Every multiplier from Stage 1 onward compounds uncertainty from the stage before it, and Stage 3's range is deliberately wide (50-100M, a 2x spread) rather than a single number, because two different uncertain events could cause the jump and neither is measured yet.

## Recommended next 3

1. **Treat Stage 1's ~100-customer figure as the number to falsify first** — it is the only stage with a named, near-term, cheap test (the riskiest-assumption test plus the 90-day GTM motion), and every later stage is conditional on it.
2. **Revisit Stage 3's pricing-lever assumption only after real campaign-corpus data exists** — do not let a later financial model quietly assume the moat hypothesis proved out.
3. **Build a real conversion-funnel dashboard from day one of the free tier** (per `strategy/gtm.md`'s Recommended next 1) — this table's Stage 1→2 jump is unverifiable without it.
