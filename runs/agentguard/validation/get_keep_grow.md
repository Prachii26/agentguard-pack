# Get / Keep / Grow

**What this is**: the acquisition, retention, and expansion funnel for AgentGuard's two revenue-bearing segments — beachhead (Marcus) and edge-high (Elena/David) — using the actual channels and sequencing `strategy/channel_plan.md` and `strategy/gtm.md` commit to, not a generic funnel template.

**Why it exists**: `strategy/gtm.md` commits to a 90-day sequence of actions; this document is what forces every stage of that sequence to name its own metric, current value, and lever, rather than leaving "growth" as an implied outcome of "doing marketing." The failure this document prevents: a funnel that looks complete because Get/Keep/Grow headers exist, while every cell under them is actually empty or invented.

**How to read it**: every "Current" cell below says "not yet measured" — this is the honest state, not a placeholder to be embarrassed about. A skeptic should check that no "Target" cell smuggles in a number without a citation back to `strategy/gtm.md` or `strategy/market_sizing.md`, or an explicit `(assumption)` tag where no such source exists.

**Depends on / feeds**: built from `strategy/channel_plan.md`'s channel economics and `strategy/gtm.md`'s 90-day motion and capacity budget. Feeds `validation/metrics_by_stage.md` and, once it exists, `financials/revenue_build.md`.

---

## Beachhead segment (Marcus)

Edge-low (Priya) usage feeds this funnel's Get stage as top-of-funnel volume per `strategy/gtm.md` (some fraction moves into beachhead-type roles over time or refers beachhead colleagues) rather than being tracked as its own revenue funnel — consistent with `strategy/market_sizing.md` sizing the SOM off the beachhead specifically, not edge-low.

| Stage | Metric | Current | Target | Lever |
|---|---|---|---|---|
| **Get** — channel to activation moment | Free-tier signups attributable to the OSS scanner and academic/research-credibility content (`strategy/channel_plan.md`'s two zero-marginal-cost channels) | **Not yet measured** — no product exists to generate signups | Enough signups to support 3 paid customers from 3 distinct companies by day 60, and a 9-customer floor within 12 months (`strategy/gtm.md`, `strategy/market_sizing.md` SOM low end) | Publish methodology-transparency content and make the OSS scanner discoverable via GitHub/developer search (`strategy/personas.md` Marcus's named trigger) |
| **Get** — activation moment | Signup → first free-tier campaign run (against a sample/toy target agent, `strategy/sales_roadmap.md` step 1–2) | **Not yet measured** | **(assumption: majority of signups run at least one campaign within 7 days — a standard self-serve PLG activation heuristic, not a measured or founder-set figure)** | In-product documentation walking through interpreting a first Comparison Report, removing any need for a sales touch (`strategy/sales_roadmap.md` step 2) |
| **Keep** — habit loop | Repeat-campaign rate: campaigns run per paying account per quarter | **Not yet measured** | 4 campaigns/year per paying account — one per quarterly release cycle (`strategy/market_sizing.md`'s SAM Fermi step 6, reasoned from Marcus's own persona trigger, not independently measured) | Exportable report format that plugs directly into Marcus's existing release risk-assessment ticket process (`strategy/sales_roadmap.md` step 4) — the habit is re-running before each release, not a new behavior invented from scratch |
| **Keep** — retention-predicting metric | Whether a paying account's second campaign is self-initiated (no re-engagement prompt needed) | **Not yet measured** | No number set yet — this is the metric `validation/experiment_board.md` row 5's self-serve-sufficiency logic depends on; a target should be set only once first-purchase data exists | Same as above — the release-ticket workflow fit is the retention mechanism, not a separate engagement campaign |
| **Grow** — expansion | Single-defense campaign ($750) → full 4-defense Comparison Report ($2,500) upgrade rate | **Not yet measured** | No number set yet — flagged as open, to be set once the ~17% bundle discount (`strategy/market_sizing.md`) has real upgrade data behind it | Bundle discount on the full Comparison Report, framed around the product's actual unit of value (the comparison, not one campaign — `strategy/positioning.md`) |
| **Grow** — referral loop | Referral-sourced signups, and beachhead-customer referrals opening edge-high access | **Not yet measured** — `strategy/gtm.md` states plainly this is a "speculative second-order effect," not an observed loop | No number set yet — `strategy/gtm.md`'s own honesty constraint: do not claim this compounds until day-90 data exists | First 3 paying customers used as reference points in later outreach (`strategy/gtm.md` days 61–90); referral access into edge-high orgs (`strategy/sales_roadmap.md` access map item 3) |

## Edge-high segment (Elena, David, Sofia)

`strategy/gtm.md` schedules **zero edge-high conversations inside the 90-day window** — this funnel's early stages are therefore deliberately unpopulated by design, not by oversight, and no numeric target is invented for any stage that the plan itself defers.

| Stage | Metric | Current | Target | Lever |
|---|---|---|---|---|
| **Get** — channel to activation moment | Edge-high-profile inbound attributable to published methodology/research credibility or beachhead-customer referral (`strategy/sales_roadmap.md` access map — cold outbound explicitly ruled out at this stage) | **Not yet measured — no edge-high outreach has begun, by design** | **No number set for year one.** `strategy/gtm.md` explicitly defers this segment past day 90; the honest target is "any qualifying inbound signal," not a count | Publish research credibility (papers, methodology talks) that Elena's team would plausibly encounter independent of any sales outreach (`strategy/sales_roadmap.md` step 1) |
| **Get** — activation moment | Guided/semi-guided pilot Comparison Report run against a real staging target agent (`strategy/sales_roadmap.md` step 2) | **Not yet measured** | No number set — this stage's entire shape (guided vs. self-serve) is itself the open hypothesis in `validation/experiment_board.md` row 5 | Semi-guided onboarding, distinct from the beachhead's zero-touch motion |
| **Keep** — habit loop | Campaign frequency per edge-high account (continuous/high-frequency usage vs. the beachhead's per-release cadence, per Elena's persona) | **Not yet measured** | No number set for year one | A standing, reproducible protocol producing one trendable metric set across every agent in the portfolio (Elena's stated trigger, `strategy/personas.md`) |
| **Keep** — retention-predicting metric | Report reuse in recurring board/audit cycles (David's ISO 42001-aligned evidence need) | **Not yet measured** | No number set for year one | Audit-ready export format mapped to ISO 42001's Operation/Performance Evaluation clauses (`strategy/value_prop_canvas.md`) |
| **Grow** — expansion | Agents-under-evaluation per account (portfolio-wide rollout vs. a single pilot agent) | **Not yet measured** | No number set — `strategy/sales_roadmap.md`'s own Recommended next 3 instructs weighting edge-high revenue conservatively or at zero for year one | Elena's team expanding usage once the pilot proves the protocol works across one agent |
| **Grow** — referral loop | CISO-network referrals (David-to-David) once audit-grade credibility is established | **Not yet measured** | No number set for year one | Reference use of any edge-high pilot, once one exists, plus the procurement/vendor-risk saboteur (`strategy/sales_roadmap.md`) being cleared at least once |

## Recommended next 3

1. **Instrument the beachhead funnel's Get and Keep stages from the day the free tier ships**, not from day 31 — `strategy/gtm.md`'s own Recommended next 3 already makes this point for conversion specifically; this funnel shows it applies to every stage, not just the paid-conversion step.
2. **Do not backfill any edge-high "Target" cell with an invented number before day 90** — every blank target above is blank because `strategy/gtm.md` deliberately schedules no edge-high motion in this window; filling them in now would misrepresent a sequencing decision as a forecasting gap.
3. **Revisit the beachhead Grow stage's referral-loop targets the moment `validation/experiment_board.md` row 4 (channel test) produces its first 90-day data point** — `strategy/gtm.md` calls this loop "speculative," and this funnel should stop calling it speculative only once real referral-attributable signups exist, not before.
