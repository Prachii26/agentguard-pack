# Go-to-market

**What this is**: channel strategy by segment, a content/credibility funnel with a speculative compounding hypothesis, a CAC hypothesis per channel with payback logic, and the 90-day motion to first customers.

**Why it exists**: every prior strategy artifact establishes *what* to say and *where* the budget sits; this is the first artifact that commits to a specific sequence of actions with numbers attached, against the team's actual capacity. The failure this document prevents: a strategy layer that's internally consistent on paper but never converts into an actual plan a 4-person, course-load-constrained team could execute — either by ignoring that nothing is built yet, or by silently assuming unlimited hours.

**How to read it**: the 90-day motion at the end is the operational core — everything above it is the argument for why that specific sequence, not a different one, is correct. Read the capacity-budget box before the 90-day motion: the motion's clock and targets are calibrated against it, not against an idealized team with unlimited hours.

**Depends on / feeds**: built from `strategy/channel_plan.md`, `strategy/petal_diagram.md`, `strategy/personas.md`, and `strategy/market_sizing.md`'s pricing assumption. Feeds `validation/mvp_definition.md` and `narrative/vc_memo.md`'s traction-plan section.

---

## Channel strategy by segment (beachhead first)

Per `strategy/market_type.md`'s re-segmented-niche framing, GTM does not lead with outbound sales or paid acquisition — the channel economics in `strategy/channel_plan.md` rule that out at this unit price. It leads with the beachhead (Marcus's persona) via the two zero-marginal-cost channels: free-tier/OSS and academic/research credibility.

1. **Beachhead (primary target)**: reached via free-tier self-serve signup, driven by methodology-transparency content and an open-source scanner component. Marcus's persona converts from "using AutoDojo/Garak manually" to "running AgentGuard's Comparison Report" once the free tier demonstrates the cross-defense comparison on a toy/sample target agent.
2. **Edge-low (funnel, not primary revenue)**: Priya's persona uses the free tier indefinitely in many cases, but some fraction moves into beachhead-type roles over time (career progression) or refers beachhead-tier colleagues — treated as a long-horizon brand-awareness input, not a revenue target for year one.
3. **Edge-high (secondary, credibility-gated)**: Elena/David/Sofia-type prospects are not reachable via cold outbound at this stage (no traction, no sales team) — they are reached only once the beachhead motion has produced enough published methodology credibility and (eventually) case evidence to be worth their attention, consistent with `strategy/personas.md` card 4's unaddressed "will this vendor exist in two years" objection.

## Capacity budget (read before the 90-day motion)

`BRIEF.md` states plainly that no implementation exists yet, and this is a 4-person team carrying a full CMPE 295A/295B course load, not a funded startup with dedicated operators. The 90-day motion below does **not** start today — it starts once a working free-tier product exists, which in this program's normal structure is the transition from 295A (design/research semester) to 295B (build/execution semester). Treating "day 1" as today, before anything is built, would be exactly the GTM-fantasy failure mode `skills/startup-critic`'s operator-founder persona exists to catch.

Rough capacity: 4 people, realistically ~10–15 hours/week each on this project alongside other coursework/obligations ≈ 40–60 person-hours/week, ≈ 520–780 person-hours across a 13-week (90-day) window. That capacity has to cover product engineering (red-team agent, four defense harnesses, comparison/report engine — the entire unbuilt platform per `BRIEF.md`), methodology-content writing, and any customer-facing work below. **Something is deliberately dropped, not silently assumed away**: security-community event attendance (`strategy/channel_plan.md`'s secondary channel) is explicitly deprioritized in this 90-day window in favor of shipping a working product first — it re-enters the plan only once the free-tier product is stable, not before.

**Continuity after the capstone ends — answered plainly, not left open.** `strategy/personas.md` card 4 names "will this vendor exist in two years" as an unaddressed objection; this GTM plan does not solve it, but it should not pretend the question has no answer either. The honest answer for year one: any paid customer acquired during the CMPE 295A/295B window is told upfront, in the same conversation as the pitch, that this is a research-stage engagement with no service guarantee beyond the end of the two-semester program (per `ASSUMPTIONS.md`'s Restated hard facts — zero traction, no funding, no implementation history to point to otherwise). The free tier and published methodology are designed to remain useful (self-serve, open documentation) even without ongoing maintenance, which is why the OSS/academic-credibility channel is prioritized over any commitment that implies an ongoing support relationship the team cannot yet promise to keep. This constraint should be revisited explicitly the moment the team decides whether AgentGuard continues past the capstone (a decision this document does not make).

## Content/credibility funnel (not yet a compounding loop)

1. A beachhead user runs a free-tier Comparison Report against a sample/toy target agent.
2. The report's methodology (matched-budget, utility-paired, cross-defense) is distinctive enough to be worth sharing — within a security team, or publicly as a methodology-transparency post — because it's the artifact `strategy/personas.md`'s Marcus needs to justify a security/usability trade-off decision to product, a naturally shareable output.
3. Sharing drives more free-tier signups from the same channel (academic/research credibility, security community), which drives more usage data, which *might* strengthen the (currently unproven, per `BRIEF.md`'s Moat section) comparison-corpus hypothesis — this third step is speculative and untested, not a mechanism this document can claim is working yet.

This is explicitly **not yet a compounding loop** — it compounds through content and credibility, not through the product creating value for one user by way of another user's presence (no multiplayer mechanic exists in `BRIEF.md`'s design), and step 3's corpus effect is a hypothesis, not an observed mechanism. Naming it "the acquisition loop that compounds" would overclaim what steps 1–2 (a content/credibility funnel, real but linear) actually establish — state it honestly as a funnel with a speculative second-order effect, not a proven loop.

## CAC hypothesis per channel, with payback logic

Using the `strategy/market_sizing.md` pricing assumption ($750/single-defense campaign, $2,500/full Comparison Report — preliminary, to be revisited before `startup-financials`):

| Channel | CAC hypothesis | Payback logic |
|---|---|---|
| Free-tier/OSS → paid conversion | **(assumption: $0 marginal CAC per conversion** — the channel's only cost is one-time/ongoing engineering time to build and maintain the OSS scanner, not a per-lead spend, per `strategy/channel_plan.md`) | Payback is immediate on the first paid conversion, since there is no per-customer acquisition spend to recover — the real constraint is *volume* of conversions, not payback speed |
| Academic/research credibility content | **(assumption: near-$0 marginal CAC** — founder/team time, not cash spend) | Same immediate-payback logic as above; the actual cost is opportunity cost of time not spent elsewhere, tracked via `strategy/business_model_canvas.md`'s Key Activities hypothesis test |
| Security community events | **(assumption: CAC ≈ $200–$500/event-driven lead**, based on typical small-conference travel/registration cost spread across a handful of qualified leads per event — not a measured figure) | At $750–$2,500 per transaction, a single converted lead from this channel pays back the CAC in one purchase — viable, but low-volume, consistent with `strategy/channel_plan.md`'s "secondary, not primary" verdict |

No CAC hypothesis is given for outbound/paid channels because `strategy/channel_plan.md` already rejects them as unviable at this price point for year one — repeating a rejected channel's math here would contradict that document rather than build on it.

## 90-day motion

Clock starts at the point a working free-tier product exists (see Capacity budget above) — treat "Day 1" below as that milestone, not today's date.

**Days 1–30 — Build-only phase, with an explicit go/no-go gate.**
Ship the open-source scanner / free-tier Comparison Report against a small set of reference target agents (matching `BRIEF.md`'s year-one scope: staging/sandboxed, text-only injection, the four named defense types, a small number of reference agent harnesses). No customer-facing date is committed inside this window. **Go/no-go gate at day 30**: the free tier must produce a stable, non-buggy comparison result on at least the reference target agents before day 31's activities begin — if it isn't stable, days 31–90 slip by however long it takes, rather than proceeding on an unreliable product (the exact failure mode `skills/startup-critic`'s operator persona flags when a plan has no slack for the thing that predictably eats month one of shipping security tooling).

**Days 31–60 — Publish methodology, open the funnel, first paying customers.**
Publish the methodology as a transparency post extending, not competing with, AgentDojo/AutoDojo's own literature (per `strategy/positioning.md`). Target profile matches Marcus's persona — reachable via the free-tier funnel rather than cold outbound. **Success metric: first 3 paid purchases** (Comparison Report at $2,500 list, or equivalent single-defense campaigns at $750), from 3 distinct companies, not 3 purchases from one account, since the goal is validating breadth of demand. Three by day 60 is deliberately a small, front-loaded slice of `strategy/market_sizing.md`'s 9–43-customer, 12-month SOM range — not an attempt to hit the 12-month floor in two months, which the SOM's own capture-rate assumption does not support.

**Days 61–90 — Grow toward a 9-customer year-one floor; no edge-high outreach yet.**
Continue free-tier funnel growth toward the low end of the 12-month SOM range (9 customers), using the first 3 paying customers as reference points in outreach. Per `strategy/sales_roadmap.md`'s explicit finding that edge-high procurement/vendor-risk review is a near-zero-probability close for a pre-traction, 4-person team in year one, **no edge-high conversation is scheduled inside this 90-day window** — the capacity budget above has no slack for a low-probability segment while the beachhead motion is still unproven, and `strategy/sales_roadmap.md`'s own "Recommended next 3" already calls for weighting edge-high revenue at zero in year one. Revisit edge-high outreach only after the beachhead motion is validated (see `validation/riskiest_assumptions.md`, phase 6).

## Recommended next 3

1. **Instrument free-tier → paid conversion from day one of the build-only phase** — this is the single number that validates or kills the entire channel-economics table above, and `strategy/business_model_canvas.md`'s Channels hypothesis test depends on having this data as early as possible, not just from day 31.
2. **Do not schedule any edge-high conversation before the beachhead's 3-paying-customer milestone is hit and referenceable** — consistent with `strategy/personas.md`, `strategy/channel_plan.md`, and `strategy/sales_roadmap.md`, all three of which independently conclude this segment requires credibility this venture doesn't have yet.
3. **If the content/credibility funnel's speculative corpus effect (step 3 above) shows no measurable signal by day 90**, log it explicitly in `validation/pivot_log.md` rather than continuing to describe it as compounding — consistent with `BRIEF.md`'s Moat section already stating this is unproven.

<!-- critic: unresolved (minor) — the go/no-go gate above names day 30 but does not specify what happens organizationally if the gate is missed by more than, say, 2 weeks (does the whole GTM plan shift a full semester?). Skipped this round as a genuinely minor scheduling-contingency detail better resolved once a real build timeline exists in validation/mvp_definition.md (phase 6) than guessed at here. -->
