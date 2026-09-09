# Stage Gate

**What this is**: where AgentGuard sits today on Steve Blank's Discovery → Validation → Creation → Building path, the evidence for that placement, and the numbered, evidence-backed exit criteria required to pass into Validation.

**Why it exists**: `strategy/gtm.md` and `strategy/market_sizing.md` both describe a future sequence of milestones (3 customers, 9 customers), but neither states, in one place, what stage the company is actually in *today* and what specifically has to be true to leave it. The failure this document prevents: a pack that talks fluently about day-60 and day-90 milestones while quietly implying the company is closer to Validation than it is — the exact gap between planning language and actual evidence that makes a plan read as aspirational rather than honest.

**How to read it**: the Evidence column under "Where AgentGuard sits today" is the check — every claim there should trace to `ASSUMPTIONS.md` or `BRIEF.md` directly, not to an inference. A skeptic should treat any exit criterion without a number as not yet a real gate.

**Depends on / feeds**: built from `BRIEF.md`'s stage line ("idea — graduate capstone, no implementation exists yet"), `ASSUMPTIONS.md`'s Restated hard facts, and `strategy/gtm.md`'s 90-day motion (day-30 build gate, day-60 3-customer milestone, day-90 9-customer floor target — `strategy/market_sizing.md`'s 12-month SOM low end). Feeds `validation/metrics_by_stage.md` and `validation/pivot_log.md`.

---

## Where AgentGuard sits today: **Discovery**

| Evidence | Source |
|---|---|
| Stage stated directly as "idea — graduate capstone, no implementation exists yet" | `BRIEF.md` |
| Zero traction: no customers, revenue, funding, pilots, testimonials, or logos exist anywhere in the pack | `ASSUMPTIONS.md`, Restated hard facts |
| No implementation exists — everything in `product/` and `tech/` (where they exist) describes a design, not shipped software | `ASSUMPTIONS.md`, Restated hard facts |
| Zero discovery interviews have been conducted — `validation/discovery_guide.md` is a newly written protocol, not yet run against a single real prospect | This phase's own output |
| The riskiest assumption (`validation/riskiest_assumptions.md` row 1) — the test the entire wedge depends on — has not been run | `validation/riskiest_assumptions.md` |
| No `strategy/gtm.md` clock has started — the 90-day motion explicitly does not begin until a working free-tier product exists, which has not happened | `strategy/gtm.md`, Capacity budget section |

This is squarely Blank's Customer Discovery stage: the company has a stated problem hypothesis and a stated solution hypothesis, has not yet gotten either in front of a real customer, and has not yet built anything a customer could use.

## Numbered exit criteria to reach Validation

Each criterion below is a real gate — a number, not a description of effort — and each is drawn from a milestone `strategy/gtm.md` or `strategy/business_model_canvas.md` already commits to, not invented for this document.

1. **The free-tier product ships and clears `strategy/gtm.md`'s day-30 go/no-go gate**: a stable, non-buggy Comparison Report result on at least the reference target agents named in `BRIEF.md`'s year-one scope. Until this is true, no later criterion can be honestly attempted.
2. **The riskiest-assumption matched-budget test (`validation/riskiest_assumptions.md` row 1) runs to completion and reports an ASR gap** — positive, null, or negative. The gate is that the *decisive test ran and was reported honestly*, per `BRIEF.md`'s own instruction to report a null result rather than only a confirming one; the gate is not conditional on the result being positive.
3. **`strategy/business_model_canvas.md`'s Value Propositions test completes**: ≥10 discovery interviews run (`validation/discovery_guide.md`), with a majority of interviewees' first follow-up question targeting the comparison report rather than the attack technique (`validation/experiment_board.md` row 3's declared threshold: ≥6 of 10).
4. **First 3 paid purchases, from 3 distinct companies**, by day 60 of the post-product 90-day motion (`strategy/gtm.md`'s explicit success metric — a Comparison Report at $2,500 list, or equivalent single-defense campaigns at $750, from 3 distinct companies, not 3 purchases from one account).
5. **The 9-customer, 12-month SOM floor is reached** (`strategy/market_sizing.md`'s low end) via the free-tier/academic channels alone, with $0 spent on paid acquisition — validating `strategy/business_model_canvas.md`'s Channels hypothesis rather than assuming it.
6. **Actual free-tier → paid conversion rate is measured and compared against the 0.1%–0.5% SOM capture-rate assumption** (`strategy/market_sizing.md`) — real data replacing the current Fermi estimate, whichever direction it lands.

All six criteria are currently unmet — none can be, since criterion 1 (product exists) has not happened yet. Criteria 2–6 are sequenced after criterion 1 by design, not by neglect: `strategy/gtm.md`'s own capacity-budget section states the 90-day clock does not start until the free tier exists.

## Recommended next 3

1. **Treat criterion 1 (day-30 build gate) as the single blocking dependency for this entire document** — nothing else on this gate list can move until it clears, and `strategy/gtm.md`'s own unresolved-critic note (no specified fallback if the gate slips by more than ~2 weeks) means this stage-gate document should be revisited the moment that slippage question gets answered.
2. **Run criterion 2 (riskiest-assumption test) as early as possible relative to criterion 1**, not after it — the matched-budget test can in principle run against an open-source reference agent harness independent of AgentGuard's own product being built, so it should not wait for the full free-tier product if a lower-fidelity version can answer it sooner (see `validation/mvp_definition.md`'s low-fidelity MVP).
3. **Do not backdate this document's "Discovery" placement once product work starts** — a team mid-build on criterion 1 is still in Discovery until criterion 1 actually clears; this stage gate should be re-run (not silently assumed passed) the moment there's a real claim to test it against.
