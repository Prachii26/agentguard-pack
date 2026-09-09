# Journey — Edge-low: Priya ships her first write-access agent feature

**Status: design only — this narrates a specification, not a recorded user session. No implementation exists yet (`BRIEF.md` stage line); nothing below has actually happened.**

**What this is**: an end-to-end, phase-by-phase narrative of Priya Nair (`strategy/personas.md` card 1) running her first AgentGuard campaign, from the trigger moment to the decision it enables.

**Why it exists**: `product/PRD.md` §3 names "no production traffic, ever" and a free/low-cost entry tier as non-negotiable for the edge-low persona; this document is where that abstraction gets tested against one concrete session. The failure this document prevents: a product that is only usable by a team with a procurement process, silently excluding the exact persona `references/quality-bar.md` property 4 requires this product serve with dignity, not a stripped-down "starter" tier.

**How to read it**: every beat names the system component acting and what gets written to Priya's durable record (the comparison report). A skeptic should be able to list, in order, which components fired — Configure gate, attacker registry, outcome logger, comparison table — without inferring anything not stated.

**Depends on / feeds**: dramatizes `product/PRD.md` §1 (core loop) and §6 (Configure/Attack/Observe/Report features), using `strategy/personas.md` card 1 verbatim. Feeds `product/ux_spec.md`'s empty/first-run states.

---

## Profile

**Priya Nair, 27, independent developer.** Building a personal-assistant agent (email drafting + calendar scheduling) as a side project about to gain write access to a user's calendar for the first time. No security background beyond "don't commit API keys." Solo, nights and weekends.

## Session goal

Get a pass/fail signal on whether her defensive system prompt actually holds up before she flips on calendar write access — without a sales call, without paying for a tool built for a twelve-person security team.

## Phase 1 — Trigger

A friend sends Priya the EchoLeak writeup (`research/sources.md` S90) with "does this affect you?" She doesn't know. Her current practice — reading the OWASP LLM Top 10 once, writing a defensive system prompt, trying a few injection phrases herself — has never been tested against anything that adapts. She searches for a way to get a real signal from a GitHub Action, finds AgentGuard's self-serve CLI.

## Phase 2 — Configure

Priya installs the CLI and runs `agentguard init`. **The API key / CLI auth feature** (`features_prioritized.md` #6) issues her a key with no sales conversation. **The staging-only connection gate** (#1) inspects the endpoint she provides — her agent's local sandbox deployment, not the real user-facing instance — and accepts it; had she pointed it at anything resembling a production credential, the gate would have rejected it before any campaign could start. **The free/low-cost entry-tier gate** (#38) recognizes her account as under the monthly cap and does not prompt for billing.

She selects **defensive prompting** as her one defense — the only one she's actually deployed — via the **defense-set selector** (#3). She sets an attempt budget of 40 rounds via the **shared attempt-budget field** (#4), the default the CLI suggests for a quick pre-launch check. She picks her agent's framework from the **reference-harness picker** (#5); it's on the supported list.

**Written to her durable record**: a new campaign entry — target: her sandbox agent, defense: defensive prompting, budget: 40 rounds, threat model: feedback-only (default, unselected).

## Phase 3 — Attack

The **configurable attacker registry** (#7), running AutoDojo's black-box optimizer as the year-one default, begins round 1. **Feedback-only mode** (#8) means the attacker knows nothing about Priya's specific system prompt — only that it will get a pass/fail signal. It generates its first injection attempt using the **text-only injection surface generators** (#9), embedded in a fake calendar invite (the surface Priya's agent actually processes), targeting the **attack objective** "unauthorized calendar write" (#10).

Round 1 fails — the defensive prompt catches the naive attempt. The **per-round outcome logger** (#12) writes: round 1, attempt content stored via the **per-round attempt content viewer** (#11), tool call attempted (calendar write), tool call executed: no, pass/fail: block.

## Phase 4 — Observe & Adapt (rounds 2–40)

The **in-context adaptation controller** (#14) reads round 1's outcome and refines the next attempt — no training phase, no delay, it happens live within the same session. Rounds 2 through 11 fail the same way. At round 12, the attacker finds a phrasing that slips past the prompt — a calendar-invite body that frames the malicious instruction as a "system note" the agent's prompt hadn't anticipated. The **legitimate-task interleaving** feature (#13) has also been sending Priya's agent ordinary, benign calendar requests throughout — those keep succeeding, which matters for the utility number in Phase 5.

The **attempts-to-first-success tracker** (#15) logs round 12 as the first success. The **adaptation-curve data pipeline** (#16) has been recording ASR per round-window the entire time; by round 30, roughly a third of attempts are succeeding — the defense hasn't collapsed, but it isn't holding either.

## Phase 5 — Report

At round 40, the campaign completes. The **final-window ASR** feature (#17) computes ASR over the last 10 rounds: 30%. Because Priya only selected one defense, the **cross-defense comparison table** (#18) renders with a single row rather than four — still useful, but visibly smaller than the multi-defense report a beachhead team would see. The **utility-under-attack metric** (#19) shows 100% — her benign calendar requests never failed, meaning the defensive prompt's problem is that it's too permissive, not that it's breaking her product.

**Written to her durable record**: the completed campaign — final-window ASR 30%, attempts-to-first-success round 12, utility 100%, one defense evaluated, timestamped.

## Phase 6 — Decision

Priya reads the number and does not flip on write access yet. She tightens her system prompt to explicitly reject "system note"-framed instructions inside calendar-invite bodies and re-runs the same campaign — the **re-run / re-diff** feature (Next tier, `features_prioritized.md` #33) is not yet built in her version of the product at this stage of the roadmap, so she manually compares the new final-window ASR (11%, after the fix) against her saved first report. She judges 11% low enough, for a twelve-user side project, to ship — a decision she can now defend with a number instead of "I tried a few things myself."

**What a skeptic can verify**: every phase names its acting component (gate, registry, controller, logger, tracker, pipeline) in the order it fired, and the only thing written to Priya's durable record is what the logged rounds and computed metrics actually produced — no invented traction, no claim that AgentGuard "knows" her agent is safe, only a measured, dated number she chose to act on.
