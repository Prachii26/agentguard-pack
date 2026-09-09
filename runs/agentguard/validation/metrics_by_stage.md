# Metrics by Stage

**What this is**: the 3–5 metrics that actually matter at each of Blank's four stages (Discovery, Validation, Creation, Building), paired with the vanity metrics to deliberately ignore at that same stage and the reason each one misleads.

**Why it exists**: `validation/stage_gate.md` names the gate between stages; this document names what to actually watch *while inside* a stage, which is a different and equally common failure point — a team can clear a real gate and then keep tracking the wrong numbers once inside the next stage. The failure this document prevents: mistaking attention (traffic, followers, press) for evidence (a completed transaction, a decisive test result), stage after stage.

**How to read it**: read the "why it's vanity here" reasons, not just the list — the same metric (e.g., total signups) is a real leading indicator at one stage and a vanity trap at another, and the reasoning column is what keeps this document from being a static list copied across stages.

**Depends on / feeds**: built from `validation/stage_gate.md`'s placement, `validation/riskiest_assumptions.md`, `validation/get_keep_grow.md`, and `BRIEF.md`'s Moat section (the unproven corpus hypothesis tracked honestly in the Building row). Feeds `validation/pivot_log.md` and, once they exist, `financials/` and `narrative/vc_memo.md`'s traction section.

---

## Discovery (AgentGuard's current stage — see `validation/stage_gate.md`)

| Metric that matters | Why |
|---|---|
| Discovery interviews completed, against `validation/discovery_guide.md`'s screening criteria | The only way to know if the persona cards in `strategy/personas.md` describe real people, not well-reasoned fiction |
| The riskiest-assumption ASR gap (`validation/riskiest_assumptions.md` row 1) — reported whichever way it lands | The single number `BRIEF.md` says decides whether the wedge exists at all |
| Fraction of `strategy/business_model_canvas.md`'s 9 hypothesis tests run, and their pass/fail count | Tracks whether the plan's load-bearing assumptions are being tested in sequence, not just documented |
| Fraction of discovery interviewees clearing the earlyvangelist definition (`validation/mvp_definition.md`) | Distinguishes a real early adopter from a polite conversation |
| A real design-partner commitment secured (a scheduled "run it against our staging agent," not a stated interest) | The behavioral-commitment threshold Mom Test discipline treats as the only trustworthy signal at this stage |

**Vanity metrics to ignore, and why**: website/landing-page traffic (no product exists yet to convert visitors to; traffic without a next action measures nothing); social-media followers or impressions (`BRIEF.md`'s zero-traction stage makes any following purely speculative interest); "sounds interesting" responses without a scheduled next step (the classic Mom Test vanity signal — polite agreement costs the responder nothing); press or conference mentions before any product exists (credibility with no artifact behind it).

## Validation

| Metric that matters | Why |
|---|---|
| Free-tier signups and activation rate (`validation/get_keep_grow.md`'s Get stage) | The first real measurement replacing this stage's entirely unmeasured current state |
| Free-tier → paid conversion rate, against the 0.1%–0.5% SOM capture-rate assumption (`strategy/market_sizing.md`) | Directly tests the single most load-bearing number in the market-sizing chain |
| Paid customer count against the 3-by-day-60 and 9-by-12-months milestones (`strategy/gtm.md`) | The actual gate criteria this stage exists to clear (`validation/stage_gate.md`) |
| CAC per channel, against the near-$0 hypothesis for OSS/academic channels (`strategy/channel_plan.md`) | Tests whether the entire zero-cash-burn GTM plan is real or optimistic |
| Actual campaign cost, against the $3–$48 cost-plus Fermi estimate (`strategy/market_sizing.md`) | Confirms whether gross margin holds at real usage, not just on paper |

**Vanity metrics to ignore, and why**: total signups without a conversion-tracking link to a paid transaction (interest without payment says nothing about willingness to pay — `validation/riskiest_assumptions.md` row 4); GitHub stars on the OSS scanner alone (a proxy for developer curiosity, not for paid-conversion likelihood); total pageviews on methodology posts (readership is not the same as the credibility effect `strategy/gtm.md`'s funnel claims); "interested" inbound emails with no scheduled paid transaction (same trap as Discovery's "sounds interesting," recurring at a later stage).

## Creation

| Metric that matters | Why |
|---|---|
| Repeat-purchase / re-run rate, against the 4-campaigns/year-per-account assumption (`strategy/market_sizing.md` SAM step 6) | Tests whether the habit loop (`validation/get_keep_grow.md` Keep stage) actually forms, or whether accounts churn after one purchase |
| Expansion rate: single-defense campaign → full 4-defense bundle upgrade | Tests the bundle-discount pricing logic (`strategy/market_sizing.md`) against real behavior |
| Referral-sourced signups, beachhead → edge-high specifically (`strategy/sales_roadmap.md` access map item 3) | The only currently-plausible access path into edge-high; if this doesn't produce signal, edge-high stays effectively unreachable |
| First edge-high pipeline opened, post-beachhead-traction | Tests whether `strategy/gtm.md`'s deferral strategy (no edge-high before beachhead proof) actually pays off once attempted |
| Net revenue retention once repeat customers exist | The first real signal on whether the business compounds or requires constant new-logo acquisition |

**Vanity metrics to ignore, and why**: restating the $4.8B TAM or $86M SAM (`strategy/market_sizing.md`) as if quoting them again were progress (market size doesn't change because a slide repeats it); aggregate press or analyst mentions of the AI-agent-security *category* rather than of AgentGuard specifically (category momentum isn't company momentum); raw campaign-run count without a paid/repeat distinction (a spike in free-tier toy-agent runs looks identical to real usage growth unless separated out).

## Building

| Metric that matters | Why |
|---|---|
| Gross margin actuals at real volume, against the $750/$2,500 price and the cost-plus Fermi | Confirms the unit economics `strategy/market_sizing.md` assumed on paper still hold once volume, not just one campaign, is real |
| Edge-high vendor-risk-review pass rate | Directly tests `strategy/sales_roadmap.md`'s named procurement/vendor-risk saboteur — the honest measure of whether edge-high is actually reachable, not just theoretically reachable |
| Revenue or campaigns per person (team-scaling efficiency) | Tests `ASSUMPTIONS.md` A2's implicit claim that this scales with usage, not headcount — the same logic `strategy/business_model_canvas.md`'s Key Resources hypothesis tests earlier |
| Net revenue retention / expansion revenue from existing accounts | The clearest signal of whether Grow-stage mechanics (`validation/get_keep_grow.md`) are working at scale, not just in the first few accounts |
| Size and reuse rate of the accumulating cross-defense comparison corpus | `BRIEF.md`'s Moat section names this as the only candidate defensibility mechanism and states plainly it is "unproven until real evaluation campaigns exist" — tracked here as a hypothesis metric to watch, explicitly not as evidence of a moat that exists |

**Vanity metrics to ignore, and why**: total funding raised without a matching efficiency metric attached (capital raised measures access to capital, not business quality); headcount growth alone (`ASSUMPTIONS.md` A2's moat hypothesis specifically depends on usage volume compounding, not team size); number of defense types "supported" with no usage data behind them (a capability claim with zero real campaigns run against it is a feature list, not traction).

## Recommended next 3

1. **Do not start tracking any Validation-stage metric before `validation/stage_gate.md`'s criterion 1 (product ships) clears** — tracking free-tier conversion against a product that doesn't exist yet produces zeros that look like data but aren't.
2. **Flag the Building-stage moat-corpus metric explicitly every time it's reported**, per `BRIEF.md`'s own instruction — this is the one metric on this entire document most likely to be quietly upgraded from "hypothesis being watched" to "proof of a moat" without a deliberate decision to do so, and that upgrade should never happen silently.
3. **Revisit this document once `validation/experiment_board.md`'s first few rows actually produce results** — several "why it matters" reasons above are themselves forward-looking judgments (e.g., which vanity traps will actually tempt this specific team); the real test of this document is whether it still reads as correct after the first real numbers come in.
