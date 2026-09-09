# Personas — the full spectrum, named and quoted

**What this is**: five persona cards spanning `BRIEF.md`'s user spectrum (edge-low, beachhead core, edge-high) plus the distinct buyer/decision-maker roles that emerge once user and payer separate at the enterprise tier.

**Why it exists**: `BRIEF.md`'s Users & spectrum section names three tiers in the abstract; this document makes them concrete enough that `product/journeys/` and `strategy/gtm.md` can write against a specific person's actual words rather than a segment label. The failure this document prevents: a GTM plan that says "we'll sell to security teams," which hides the fact that nobody has named who signs (the exact failure `references/grill-question-bank.md` §2 warns about, closed properly in `validation/decision_making_unit.md` later — these cards are the raw material that artifact builds on).

**How to read it**: each card's Objection line is the one a real prospect would actually raise; a skeptic should check that every "must-have" quote sounds like something a person would say out loud, not marketing copy translated into first person.

**Depends on / feeds**: built from `BRIEF.md`'s Users & spectrum section and `research/sources.md` (S76, S83, S87 for the pain/adoption data grounding each card). Feeds `product/journeys/*.md`, `strategy/value_prop_canvas.md`, `strategy/gtm.md`, and `validation/decision_making_unit.md`.

---

## 1. Edge-low — the solo agent builder

**Priya Nair, 27, independent developer.** Building a personal-assistant agent (email drafting + calendar scheduling) as a side project she's about to open-source and add to a small SaaS waitlist.

- **Context**: No security background beyond "don't commit API keys." Ships fast, alone, nights and weekends.
- **Day-in-the-life pain moment**: She's about to give her agent write access to a user's calendar (not just read) for the first time, and a friend just sent her the EchoLeak writeup (`research/sources.md` S90) with the message "does this affect you?" She has no idea how to answer.
- **Current workaround**: Manually reads through the OWASP LLM Top 10 prompt-injection section (S118) once, writes a defensive system prompt, and ships. No testing beyond "I tried a few injection phrases myself and they didn't work."
- **Trigger to switch**: A free-tier, no-signup-friction way to get a pass/fail signal before she flips write access on — something she can run from a GitHub Action, not a sales call.
- **"Must-have" language she'd actually say**: *"I just want to know if my system prompt is actually doing anything before I give this thing access to someone's real inbox."*
- **Objection to overcome**: *"I'm not paying for a security tool for a project that has twelve users."* (Free/cheap entry tier is not optional for this persona — see `strategy/gtm.md`.)

## 2. Beachhead core — the security/ML platform engineer

**Marcus Webb, 34, senior security engineer, mid-size fintech (a bank's digital-lending arm) with a Slack-integrated support agent that has document and CRM access.**

- **Context**: Reports into a small security team (4 people) supporting a much larger engineering org. Owns "AI risk" as roughly 20% of his job, alongside application security and vendor risk.
- **Day-in-the-life pain moment**: Product wants to expand the support agent's tool access to include refund processing — a real financial action, not just a lookup — before next quarter's release. Marcus has 48 hours in a sprint to produce a risk assessment and no budget for an external pentest firm on this timeline.
- **Current workaround**: Runs the agent through Garak (S58) and a manually-written checklist derived from the OWASP LLM Top 10 (S118), reports "no findings" to his VP, and privately doesn't trust the result because he knows Garak's probe library is static.
- **Trigger to switch**: A report he can attach to the release risk-assessment ticket that shows, with numbers, how the specific defense they've deployed (defensive prompting, in this case) holds up against an attacker that adapts — and what it costs in blocked legitimate refund requests, so he isn't the one who has to guess at the trade-off.
- **"Must-have" language he'd actually say**: *"I don't need 'no vulnerabilities found' — I need to know how hard someone would have to try, and what it costs us if we make it harder to break."*
- **Objection to overcome**: *"How do I know your adaptive attacker is actually representative of a real attacker, and not just gaming your own report?"* (Answered by the matched-budget test design and the published methodology in `tech/whitepaper.md` — never by an opaque, unexplained "trust us" claim, consistent with `references/quality-bar.md` property 1.)

## 3. Edge-high — the enterprise AI red-team lead

**Dr. Elena Osei, 41, Head of AI Red Team, a large enterprise software company running dozens of internal and customer-facing agents.**

- **Context**: PhD in security, built her team from two people to twelve over three years, reports to the CISO. Runs both traditional red-team engagements and an emerging AI-specific practice.
- **Day-in-the-life pain moment**: Quarterly board reporting requires a defensible answer to "are our AI agents secure," and her current answer — a mix of manual red-teaming and vendor tool output that doesn't share a common metric — doesn't add up to one coherent number she can defend to the board or to the company's cyber-insurance underwriter.
- **Current workaround**: A mix of an internal team running manual adaptive red-teaming (expensive, slow, doesn't scale across the dozens of agents her company runs) and point-tool output from two or three vendors that can't be compared to each other because each reports differently.
- **Trigger to switch**: A standing, reproducible protocol her team can run continuously across every agent and every defense configuration in the company's portfolio, producing one comparable number set the board and the insurer can both read — not a one-off engagement.
- **"Must-have" language she'd actually say**: *"I don't want another point-in-time pentest report. I want a number I can trend over time, across every agent we ship, that means the same thing every time it's computed."*
- **Objection to overcome**: *"We already have Adversa AI / an internal red team — why would we add a third source of truth?"* (Answered by AgentGuard's cross-defense, utility-paired, reproducible framing — see `strategy/positioning.md` — not by claiming to replace her team.)

## 4. Buyer/decision-maker (payer ≠ user) — the enterprise budget holder

**David Chen, 46, CISO, same enterprise company as Elena Osei — Elena's manager and the actual signer for any new security-tooling spend above her discretionary budget.**

- **Context**: Owns the security budget and the board relationship; does not use AgentGuard hands-on and will likely never open the product himself. Evaluates purchases by risk-reduction-per-dollar and by how a tool affects his own reporting obligations (SOC2, the emerging ISO 42001 certification his company is pursuing — `research/sources.md` S113).
- **Day-in-the-life pain moment**: An auditor or board member asks a direct question about AI agent security posture that David cannot currently answer with evidence, only assurance ("my team tells me it's fine") — and he knows that answer doesn't hold up under ISO 42001's certification-grade-evidence requirement (S114).
- **Current workaround**: Relies on Elena's team's internal reporting and whatever narrative the existing vendor relationships provide, none of which is framed as audit-ready evidence.
- **Trigger to switch**: A report format that functions as certification-grade evidence (per ISO 42001's Operation/Performance Evaluation clauses, S114) — not just a security artifact but a compliance one, reusable across audits.
- **"Must-have" language he'd actually say**: *"If I can't hand this to an auditor and have it hold up, it's not solving my problem — it's solving Elena's."*
- **Objection to overcome**: *"Is this vendor going to exist in two years?"* (A real objection for a 4-person capstone-stage venture with zero traction — `ASSUMPTIONS.md` Restated hard facts — that `narrative/vc_memo.md` and `financials/risk_matrix.md` must not dodge.)

## 5. Edge-high (alternate buyer type) — the agent-platform vendor's trust & safety lead

**Sofia Ramirez, 38, Head of Trust & Safety at an agent-platform vendor (a company that sells agent infrastructure/orchestration to other companies, per `BRIEF.md`'s edge-high definition).**

- **Context**: Her company's product *is* the target agent other companies build on — she's not just securing one internal deployment, she's responsible for the security posture every downstream customer inherits.
- **Day-in-the-life pain moment**: A prospective enterprise customer's security questionnaire asks for evidence of adversarial testing against indirect prompt injection specifically, citing the current OWASP LLM Top 10 ranking (S118) — and her company's existing results (an internal AgentDojo run using its shipped, fixed attack distribution, not a custom adaptive one) don't answer the "have you tested against an adaptive attacker" follow-up question the more sophisticated prospects are starting to ask.
- **Current workaround**: Points to the fixed-attack-distribution AgentDojo/InjecAgent scores in the company's trust-center documentation and hopes the prospect doesn't ask the adaptive-attacker follow-up.
- **Trigger to switch**: A comparison report she can publish (or excerpt) in her own trust-center documentation, showing her platform's default defenses hold up across an adaptive, matched-budget, utility-aware evaluation — turning a vendor risk into a sales asset for her own company.
- **"Must-have" language she'd actually say**: *"I need something I can put in front of our biggest prospects' security teams that isn't just our own homework marked by us."*
- **Objection to overcome**: *"Will running this against our production platform create a new disclosure liability if the results are bad?"* (Directly addressed by `BRIEF.md`'s year-one scope — staging/sandboxed evaluation only, never production traffic — which should be foregrounded in any pitch to this persona specifically.)

## Recommended next 3

1. **Write `product/journeys/beachhead.md` and `product/journeys/edge_high.md` as Marcus's and Elena's actual first-session experiences**, quoting their pain moments above rather than inventing new ones.
2. **Use Priya's and David's objections verbatim as the two hardest lines in `narrative/vc_memo.md`'s risk section** — "won't pay" (edge-low) and "won't trust a pre-traction vendor" (enterprise buyer) are the two objections most likely to actually kill a deal, and a memo that doesn't name them isn't credible.
3. **Confirm Sofia's persona (agent-platform vendor as a customer, not just a competitor via Microsoft/Cisco-style bundling) doesn't contradict `research/competitors.md`'s finding that Microsoft bundles this capability into Azure Foundry** — Sofia's company is a plausible customer only if it does *not* already get "good enough" coverage for free from its own cloud/model provider; validate this distinction explicitly in `validation/discovery_guide.md`.
