# Pivot Log

**What this is**: a decision journal — what has already been considered and killed, on the record with dates and reasoning, plus the standing pivot-or-persevere criteria that govern what happens next as real test results come in.

**Why it exists**: `ASSUMPTIONS.md` A9 already records a real, founder-made decision to reject three candidate differentiators, but it lives inside an assumptions log, not a decision journal a future session would think to check before re-litigating the same question. The failure this document prevents: re-debating a settled decision from scratch six months from now because nobody could find where it was already made, or — the opposite failure — treating a live risk as settled because no standing trigger was ever written down.

**How to read it**: the "Already considered and killed" section is closed history — it should not be reopened without new evidence directly contradicting the reasoning given. The "Standing criteria" section is the opposite: open, numbered, and meant to be checked against real data as `validation/experiment_board.md` and `validation/riskiest_assumptions.md` produce results.

**Depends on / feeds**: pulls the already-decided history from `ASSUMPTIONS.md` A9 and `BRIEF.md`'s Wedge/Competition sections. Standing criteria are tied directly to `validation/riskiest_assumptions.md`'s ranked board and `strategy/gtm.md`'s 90-day milestones. Feeds `narrative/vc_memo.md`'s risk section, once it exists.

---

## Already considered and killed

**2026-09-09 — narrowed the original wedge claim.** The original why-now narrative implied "no one automates adaptive attacks against agents." Research found this false: AutoDojo (academic, open-source), a NIST/UK AISI human red-teaming exercise, and Adversa AI (funded commercial vendor) all already do adaptive evaluation. **Decided by**: resolved through research, confirmed by the founder (`ASSUMPTIONS.md` A1, A7, A9). **Not reopened unless**: a future research pass finds the corrected claim ("no one publishes the cross-defense, utility-paired comparison") is itself false.

**2026-09-09 — rejected "breadth across arbitrary customer-deployed defenses" as the differentiator.** Considered as a replacement wedge after the narrowing above. **Reason killed**: contradicts AgentGuard's own year-one scope, which explicitly excludes custom defense authoring (`BRIEF.md` Year-one scope, item 2). **Decided by**: founder, recorded in `ASSUMPTIONS.md` A9. **Not reopened unless**: the year-one scope itself is deliberately revised to add custom defense authoring — a separate, larger decision that would need its own record here first.

**2026-09-09 — rejected "a standalone continuously-available service" as the differentiator.** Considered as a second replacement wedge. **Reason killed**: this is Adversa AI's exact existing positioning — adopting it as AgentGuard's claimed differentiator would mean competing head-on with a funded incumbent on its own ground, not differentiating from it. **Decided by**: founder, `ASSUMPTIONS.md` A9. **Not reopened unless**: Adversa AI's positioning changes materially (tracked as a standing criterion below).

**2026-09-09 — rejected "feedback-only-as-primary framing" as the differentiator.** Considered as a third replacement wedge. **Reason killed**: this is already AutoDojo's threat model — not a novel claim, only a restatement of existing academic prior art. **Decided by**: founder, `ASSUMPTIONS.md` A9. **Not reopened unless**: a future finding shows AutoDojo has moved away from feedback-only as its primary framing.

**Resolution adopted in place of all three**: "the comparison, not the attacker" — a standing, reproducible, budget-matched, utility-paired comparison across defense families is the differentiator, because no source found in research publishes one (`ASSUMPTIONS.md` A9 Resolution; `strategy/positioning.md`). This resolution is itself tracked as an open, testable claim below, not treated as permanently settled.

## Standing pivot-or-persevere criteria

Each criterion names a real threshold and a date or milestone it's checked against — the discipline `skills/startup-validation` requires. None of these has been triggered yet; none can be, since the underlying tests (`validation/experiment_board.md`, `validation/riskiest_assumptions.md`) have not run.

1. **We pivot away from the entire wedge** if the matched-budget ASR gap (`validation/riskiest_assumptions.md` row 1) comes back null or negative across all four defense types once tested, within the 2-week/<$1k window BRIEF.md specifies for the first defense and the follow-on window for the remaining three (`validation/riskiest_assumptions.md` row 2). This is not a soft signal — `BRIEF.md` states directly that a non-positive gap means "a static benchmark would already be sufficient" and "the entire wedge collapses."
2. **We reconsider the self-serve-only, uniform-motion business model** (`ASSUMPTIONS.md` A3) if, by day 60 of the post-product 90-day motion, edge-high-profile prospects reached through the free tier demonstrate they will not transact without a guided or managed motion — i.e., if `strategy/business_model_canvas.md`'s Customer Relationships test (`validation/experiment_board.md` row 5) fails its 2-of-3 threshold.
3. **We revisit pricing** (`ASSUMPTIONS.md` A4) if the first 3 paid purchases (`strategy/gtm.md`, target: by day 60) require material discounting off $750/$2,500 list to close, or if the pricing A/B test (`validation/experiment_board.md` row 6) shows conversion stalling specifically at the price-quote step rather than earlier in the funnel.
4. **We escalate active reassessment of the comparison-protocol positioning** (not necessarily a pivot, but a forced re-evaluation) if Adversa AI publishes an aggregate cross-defense benchmark, or Microsoft ships a comparable feature in Azure AI Foundry, before AgentGuard's own day-60 milestone (`strategy/positioning.md`, `strategy/market_type.md`'s dominant-risk row; monitored via `validation/riskiest_assumptions.md` row 3).
5. **We persevere on deferring edge-high outreach past day 90** unless the beachhead's 3-customer milestone is hit meaningfully early and is referenceable (`strategy/gtm.md`, `strategy/sales_roadmap.md`) — this is a standing "do not pivot the sequencing early" guardrail as much as a trigger, protecting against the temptation to chase a bigger-looking edge-high deal before the beachhead motion is proven.
6. **We treat the "zero paid acquisition" channel strategy as failed**, and reconsider `strategy/business_model_canvas.md`'s Cost Structure hypothesis, if signups attributable to the OSS/academic channels are not on pace for the 9-customer, 12-month floor by day 90 (`validation/experiment_board.md` row 4's pass threshold).
7. **We reopen the "already considered and killed" section above** only if new evidence directly contradicts the stated reason a candidate differentiator was rejected — not on the strength of a new pitch or a new person's opinion re-raising the same option.

## Recommended next 3

1. **Check criterion 1 the moment the riskiest-assumption test (`validation/riskiest_assumptions.md` row 1) produces a result** — it is the fastest-resolving criterion on this list (2 weeks, once product exists) and the only one that can end the company outright.
2. **Add a recurring calendar checkpoint for criterion 4** (Adversa AI / Microsoft monitoring) starting now, not after product ships — it is the one criterion that can trigger before AgentGuard has done anything at all, since it depends entirely on competitors' moves.
3. **Do not let this log go stale** — per `references/quality-bar.md`'s property-8 discipline for `README.md`, a pivot log that isn't updated the moment a criterion is actually checked is worse than no log at all, because it invites false confidence that "we would have caught it."
