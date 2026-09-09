# Customer Discovery Guide

**What this is**: the interview kit — screening criteria per persona, a shared past-behavior question set, a solution-interview script, and a synthesis template — for running real discovery conversations against AgentGuard's five personas.

**Why it exists**: `strategy/personas.md` builds five detailed cards from research and reasoning, not from a single conversation with a real prospect; this document is what turns those cards into an actual interview protocol someone can run this week. The failure this document prevents: a "discovery guide" whose questions secretly pitch the product ("would you use a tool that…") and comes back with polite agreement instead of evidence — the exact red flag `skills/startup-validation`'s own contract names.

**How to read it**: the question set is the load-bearing section — every question asks what the interviewee *actually did*, never what they'd hypothetically do. A skeptic should read each question and try to answer it with an opinion instead of a fact; if that's possible, the question is broken and needs to be rewritten before use.

**Depends on / feeds**: screening criteria drawn directly from `strategy/personas.md`'s five cards. Feeds `validation/experiment_board.md` row 3 (Value Propositions test), `validation/riskiest_assumptions.md` row 3/9, and `validation/mvp_definition.md`'s earlyvangelist definition.

---

## Screening criteria per persona

No interview should be scheduled with someone who doesn't clear their persona's screen — an unscreened interview produces noise, not signal.

| Persona | Screening criteria (must clear before scheduling) |
|---|---|
| **1. Priya — edge-low, solo agent builder** | Currently building or has shipped an agent with real tool access (email, calendar, or similar) that other people will use, even at small scale; has personally made at least one deliberate decision about how to defend it (a system prompt, a manual test pass) without a security background. |
| **2. Marcus — beachhead, security/ML platform engineer** | Holds a security- or ML-platform-titled role; their company runs at least one tool-using agent in production with real data or tool access; has personally run some form of adversarial testing (Garak, PyRIT, a manual OWASP LLM Top 10 checklist, or equivalent) against an agent within the past 6 months. |
| **3. Elena — edge-high, AI red-team lead** | Leads or is a senior member of a dedicated AI/ML red-team function; reports up to a CISO or equivalent; has personally run or commissioned more than one AI red-team engagement (internal or vendor). |
| **4. David — edge-high, budget-holding payer (CISO)** | Holds budget authority for security-tooling spend above a team's discretionary threshold; has personally been asked a board-, audit-, or compliance-related question about AI/agent security within the past 12 months. |
| **5. Sofia — edge-high, agent-platform Trust & Safety lead** | Works Trust & Safety or platform-security at a company whose product is agent infrastructure sold to other companies (not an internal-only deployment); has personally handled a prospective customer's security questionnaire within the past 6 months. |

Interviews with anyone who fails their persona's screen should still be logged (a failed screen is itself data about how common the target profile actually is) but not counted toward any pass/fail threshold in `validation/experiment_board.md`.

## Problem-interview questions (10–15, past-behavior only — Mom Test discipline)

Every question below asks about a specific past instance, decision, or artifact — never "would you," "do you think," or "how do you feel about." Ask for the *last* time, a *specific* tool, a *specific* person who signed off — specificity is what makes an answer checkable.

1. Walk me through the last time you (or your team) evaluated whether an AI agent's defenses would hold up to misuse — what did you actually do, step by step?
2. What tool or process did you use for that evaluation? Who set it up, and roughly how long did it take?
3. What was the last specific incident, near-miss, or "does this affect us" moment that made you look into this? What actually happened?
4. The last time a release or change expanded what an agent could do (new tool access, new data source), walk me through the actual timeline in the run-up to shipping it.
5. The last time you got a "no findings" or "passed" result from a security test on an AI agent, what did you do with that result — who did you show it to, and what happened next?
6. Tell me about the last time you had to explain to someone outside security (product, engineering, a board member) why a defense mechanism was blocking something it shouldn't have. What did that conversation actually look like?
7. What's the last tool — open-source or commercial — you evaluated or adopted for this kind of testing? What made you pick it, and what did you do when it didn't fully answer your question?
8. Have you ever paid for, or requested budget for, a red-team or pentest engagement that specifically covered an AI/agent component? Walk me through that approval process — who signed off, how long did it take?
9. What's the last time you had to produce evidence of AI security posture for an auditor, a customer's security questionnaire, or a board update? What did you actually submit?
10. When was the last time you seriously considered building something like this in-house instead of buying it? What happened to that effort?
11. Who else, if anyone, was actually involved the last time you made a decision about which AI security tool or vendor to use? Walk me through who had to sign off.
12. What's the last AI-security-related tool or report you shared with a colleague — and why did you share that specific one?
13. Tell me about a time an AI security tool or test gave you a result you didn't trust. What made you distrust it, and what did you actually do about it?

## Solution-interview script

Run only after the problem interview above establishes the person clears their screen and has a real, current version of the pain. The solution interview shows AgentGuard's actual mechanism — this is where showing a concept is appropriate — but stays disciplined about what it asks for: reactions to something specific, and a real next-step commitment, never a hypothetical opinion ("would you use this?" is explicitly out of bounds here too).

1. Show a sample Comparison Report output (final-window ASR, utility under attack, adaptation curve, reported per defense side by side) against a sample/toy target agent.
2. Ask: **"What's the first thing you look at on this?"** — observed behavior in the moment, not a stated preference.
3. Ask: **"Is there anything here you don't trust, or would want to verify yourself, before you'd attach this to a real release ticket?"** — surfaces real objections against a concrete artifact, not abstract skepticism.
4. Ask: **"How does this compare to the last report you actually used for this purpose?"** — anchors the reaction to their own remembered artifact from the problem interview, not a generic comparison.
5. Close with a real commitment ask, not a hypothetical: **"Would you be willing to run this against a staging copy of [their actual agent] this week?"** or **"Can I follow up once the free tier ships and send you the link directly?"** A yes here is behavioral evidence (a scheduled action); a polite "sounds interesting" with no commitment is treated as a no.

## Synthesis template

Fill this in per interview, then roll up across all interviews for a persona before treating any `validation/experiment_board.md` row as having a result.

| Field | What goes here |
|---|---|
| **Interviewee / persona / date** | Name (or anonymized ID), which of the five personas they match, interview date |
| **Screen result** | Cleared / did not clear — and why |
| **Top pains named** | In their own words, ranked by which one they spent the most time describing |
| **Current workaround** | The specific tool/process/checklist named in answer to Q1–Q2, Q7, Q10 |
| **Trigger event** | The specific incident or timeline named in answer to Q3–Q4 |
| **Must-have language** | Any verbatim quote that sounds like something they'd actually say out loud (cross-check against `strategy/personas.md`'s existing quotes — confirm or revise, don't just accept) |
| **Surprise findings** | Anything that contradicts an assumption in `strategy/personas.md`, `strategy/sales_roadmap.md`, or `validation/riskiest_assumptions.md` — these are the most valuable rows in this whole template |
| **Solution-interview commitment (if run)** | Specific next action agreed to, or "no commitment obtained" |

## Recommended next 3

1. **Screen and schedule Marcus-persona interviews first** — `strategy/business_model_canvas.md`'s Value Propositions test (row 3, `validation/experiment_board.md`) is the single most load-bearing of the nine BMC tests, and Marcus is the beachhead the whole 90-day motion depends on.
2. **Log every "surprise findings" entry directly into `validation/pivot_log.md`'s open-criteria section as it's found**, not just in this document's synthesis rows — a surprise that contradicts a standing pivot trigger should be visible where pivot decisions actually get made.
3. **Do not run any solution interview before at least 3 problem interviews per persona are complete** — showing the mechanism too early risks anchoring the interviewee's language to AgentGuard's own framing instead of their real, pre-existing vocabulary, which is exactly what Q12's "must-have language" column is trying to capture uncontaminated.
