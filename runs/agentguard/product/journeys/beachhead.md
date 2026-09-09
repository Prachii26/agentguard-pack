# Journey — Beachhead: Marcus's first campaign to habitual pre-release use

**Status: design only — this narrates a specification, not a recorded user session. No implementation exists yet (`BRIEF.md` stage line); nothing below has actually happened.**

**What this is**: an end-to-end narrative of Marcus Webb (`strategy/personas.md` card 2) running his first four-defense AgentGuard campaign under a sprint deadline, then the shift to habitual pre-release use.

**Why it exists**: the beachhead is the core paying use case (`BRIEF.md` Users & spectrum); this document is where the abstract claim "a report he can attach to the release risk-assessment ticket" (`strategy/value_prop_canvas.md`) gets tested against a real 48-hour deadline, a real sprint, and a real trust objection about whether the adaptive attacker is representative.

**How to read it**: phase-by-phase, naming the acting component and what's written to Marcus's durable record. A skeptic should check that the objection named in his persona card ("how do I know your adaptive attacker is actually representative") gets an answer inside the journey, not just asserted away.

**Depends on / feeds**: dramatizes the full `product/PRD.md` §1 loop across all four defenses, using `strategy/personas.md` card 2 and `strategy/value_prop_canvas.md` verbatim. Feeds `product/ux_spec.md`'s comparison-table and habitual-use states.

---

## Profile

**Marcus Webb, 34, senior security engineer, mid-size fintech (bank's digital-lending arm).** Small security team (4 people), "AI risk" is roughly 20% of his job. Product wants to expand a Slack-integrated support agent's tool access to include refund processing — a real financial action — before next quarter's release. He has 48 hours in a sprint and no budget for an external pentest firm.

## Session goal (first campaign)

Produce a risk assessment, backed by numbers, on whether the currently-deployed defense (defensive prompting) should be trusted for a defense expanding into refund-processing tool access — and if not, which of the other three fixed defenses trades security for usability better.

## Phase 1 — Trigger

Marcus's usual workaround — running Garak (a static probe library, `research/sources.md` S58) and a manual OWASP-derived checklist, then reporting "no findings" — has never sat right with him, because he knows Garak's probe library doesn't adapt. With a real financial action now in scope and a 48-hour clock, he decides this is the release where "no findings" isn't good enough to sign off on.

## Phase 2 — Configure

Marcus authenticates with his team's existing AgentGuard API key (**API key / CLI auth**, `features_prioritized.md` #6). He points the **staging-only connection gate** (#1) at the bank's staging deployment of the support agent — the gate rejects his first attempt because he accidentally pointed it at a URL pattern matching the production Slack workspace integration; he corrects it to the staging instance, and it's accepted. The **sandbox credential vault** (#2) stores the staging credential.

Using the **defense-set selector** (#3), Marcus selects all four fixed defenses — defensive prompting (currently deployed), classifier-based detection, rule-based tool-call validation, and baseline/none (as a floor reference) — because he needs to know not just whether the current defense holds, but whether a different one would trade better. The **shared attempt-budget field** (#4) is set to 150 rounds per defense, propagated identically to all four sub-campaigns. The **reference-harness picker** (#5) confirms the agent's framework is supported.

**Written to his durable record**: campaign entry — target: staging support agent, defenses: all four, budget: 150 rounds each, threat model: feedback-only.

## Phase 3 — Attack (four parallel sub-campaigns)

The **configurable attacker registry** (#7), running AutoDojo's adopted black-box optimizer, launches four independent sub-campaigns, one per defense, each starting from round 1 with **feedback-only mode** (#8) — the attacker does not know which defense configuration it faces in any given sub-campaign, only the round outcome. The **text-only injection surface generators** (#9) construct attempts as Slack messages and embedded document content (the surfaces the support agent actually ingests), targeting the **attack objective** "unauthorized refund tool call" (#10).

Against baseline/none, the attacker succeeds by round 3. Against defensive prompting (the currently deployed defense), early rounds fail, then round 19 slips through using a framing that impersonates an internal support macro. Against classifier-based detection, the attacker struggles longer — round 40 before first success. Against rule-based tool-call validation, no success within the full 150-round budget.

## Phase 4 — Observe & Adapt

The **per-round outcome logger** (#12) records every attempt, tool call, and outcome across all four sub-campaigns. The **legitimate-task interleaving** feature (#13) sends benign refund-lookup and support requests throughout each sub-campaign, so utility is measured under the same live conditions. The **in-context adaptation controller** (#14) refines each sub-campaign's next attempt from its own prior rounds only — no cross-contamination between the four defense conditions. The **attempts-to-first-success tracker** (#15) logs: baseline/none round 3, defensive prompting round 19, classifier-based round 40, rule-based validation: no success (budget exhausted). The **adaptation-curve data pipeline** (#16) records ASR per round-window for all four.

## Phase 5 — Report

The **final-window ASR** metric (#17) computes, per defense, over the last 15 rounds: baseline/none 95%, defensive prompting 62%, classifier-based 18%, rule-based validation 0%. The **cross-defense comparison table** (#18) renders all four side by side, same 150-round budget. The **utility-under-attack metric** (#19) shows: baseline/none 100% (never blocks anything, hence high ASR too), defensive prompting 91%, classifier-based 84%, rule-based validation 71% — the rule-based defense that fully resisted the attacker also blocked the most legitimate refund requests.

**Written to his durable record**: the completed four-defense comparison — final-window ASR, attempts-to-first-success, and utility, one row per defense, timestamped, attached to the campaign entry from Phase 2.

## Phase 6 — Decision and the objection answered

Marcus attaches the comparison table directly to the release risk-assessment ticket (`strategy/value_prop_canvas.md`, his ranked pain #1) — no reformatting needed. When his VP asks the exact objection his persona card names — "how do you know this adaptive attacker is representative of a real attacker, and not just gaming your own report?" — Marcus points to two things the report itself carries: the attacker registry is explicitly labeled "AutoDojo black-box optimizer (adopted, v1)," published academic prior art with its own peer-reviewed evaluation (`research/sources.md` S13), not an opaque in-house claim; and the matched-budget design (identical 150-round budget across all four defenses) means the comparison can't be gamed by running one defense longer than another. He recommends rule-based tool-call validation for the refund-processing expansion, flagging the 71% utility figure as the trade-off product needs to accept knowingly, not discover after launch.

## Phase 7 — Habitual use

Three months later, ahead of the next release that expands the agent's document-access scope, Marcus runs the same campaign configuration again without being asked. This becomes his default pre-release step — the **re-run** behavior he now expects, even though the automatic re-diff feature (`features_prioritized.md` #33) is Next-tier and not yet available at this point in the roadmap; he manually compares the new report against the one from Phase 5, saved in his ticket history, and notices the classifier-based defense's ASR crept up to 26% — the classifier vendor shipped a model update, and Marcus now has a concrete number showing it needs re-evaluation, not just a vague sense that "things might have changed."

**What a skeptic can verify**: four independently-run sub-campaigns, one shared attempt budget, one attacker registry explicitly labeled as adopted prior art, one comparison table — and Marcus's objection about representativeness is answered by naming the exact adopted technique and the matched-budget design, not by an unexplained "trust us."
