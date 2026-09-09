# Journey — Day in the life: Elena (user) and David (payer), one ordinary Tuesday

**Status: design only — this narrates a specification, not a recorded user session. No implementation exists yet (`BRIEF.md` stage line); nothing below has actually happened.**

**What this is**: one ordinary day, not a crisis day, across every touchpoint two people at the same company (Elena Osei, Head of AI Red Team; David Chen, her CISO and the actual budget-signer) have with AgentGuard — including the buyer's view, since user and payer separate at this tier (`strategy/personas.md` cards 3 and 4).

**Why it exists**: `product/PRD.md` names David's persona as someone who "does not use AgentGuard hands-on and will likely never open the product himself" — a claim that only means something if this document shows what his actual touchpoint looks like instead. The failure this document prevents: a product design that only ever thinks about the person who clicks "run campaign," leaving the person who signs the renewal with no designed experience at all.

**How to read it**: read top to bottom as one calendar day, 8:00am to 6:00pm. A skeptic should notice David's touchpoints are real (a notification, an export, a five-minute skim) but genuinely light — that lightness is the design intent (`strategy/value_prop_canvas.md`: "certification-grade evidence... not just an internal security artifact"), not an oversight.

**Depends on / feeds**: dramatizes `product/PRD.md` §6 (Report-stage features especially) across a compressed timeline. Feeds `product/ux_spec.md`'s notification, portfolio-dashboard, and audit-export screens.

---

## 8:14am — Elena, at her desk

The **scheduled/recurring campaign trigger** (`features_prioritized.md` #44) fired overnight on its weekly cadence across 15 agents (`journeys/edge_high.md`). Elena opens the **portfolio dashboard** (#49) with coffee in hand — this is routine Tuesday triage, not an incident response. Fourteen of fifteen agents show stable or improved final-window ASR versus last week. One — the Slack-integrated HR-assistant agent — shows a jump from 12% to 34% ASR against its deployed classifier-based defense.

## 8:22am — Elena investigates

She clicks into the HR-assistant agent's campaign. The **cross-defense comparison table** (#18) confirms the jump is isolated to the classifier-based defense; the other three defense configurations she also runs against this agent as a standing comparison are unchanged. The **defense fingerprint capture** feature (#23) shows the classifier's block pattern shifted in a way consistent with an upstream model update, not a change on her own side. The **notification/webhook on campaign completion** (#40) had already pushed this delta to her team's Slack channel at 6:03am, which is how she knew to look here first.

## 9:00am — Elena's team stand-up

She assigns a teammate to open a **shareable report link** (#34) — read-only — and send it to the HR-assistant product owner, who isn't an AgentGuard user at all. This is the third touchpoint type the product has to support today: not the configurer (Elena), not the payer (David, below), but a one-time report recipient who needs zero onboarding to understand a single page.

## 11:40am — Marcus, a different business unit, same company's broader agent portfolio (a supporting touchpoint)

Unrelated to Elena's morning, Marcus-equivalent engineers in two other business units under the same enterprise workspace run their own pre-release campaigns using the shared **campaign templates** (#45) Elena's team published org-wide. This is the same mechanism at beachhead cadence, inside the same edge-high organizational shell — the one-system claim (`BRIEF.md` Users & spectrum) made concrete within a single company, not just across the three personas.

## 1:15pm — David, in a board-prep meeting, not at his laptop

David gets a text summary from his chief of staff, not a product notification: "Elena flagged a classifier regression on the HR agent, already re-evaluating, report attached." He does not open AgentGuard. This is by design (`product/PRD.md` §4, David's row: "does not use AgentGuard hands-on").

## 2:30pm — David's actual touchpoint: an auditor's question

An external auditor, preparing the company's ISO 42001 certification review, asks David's team for evidence of adversarial robustness testing on agents handling employee data — squarely the HR-assistant agent from this morning. David's chief of staff pulls the **audit-ready report export** (#32) for that agent directly from the portfolio dashboard — mapped to ISO 42001's Operation and Performance Evaluation clauses (`research/sources.md` S113, S114) — and attaches the exported file to the audit response. David skims it for five minutes: the final-window ASR trend line, the utility number, the timestamp. He does not need to understand the adaptive-attack mechanism to use it; the export is built to stand on its own (`strategy/value_prop_canvas.md`, David's ranked pain #2).

**Written to David's touchpoint, specifically**: nothing new is generated for him — he consumes the same report Elena's team produced this morning, exported once, through the one feature (#32) his entire relationship with the product runs through.

## 3:45pm — Elena, back on the HR-assistant agent

The re-evaluation her team kicked off at 9:00am completes. **Final-window ASR** (#17) against the classifier-based defense is back down to 15% after her team temporarily tightens the classifier's threshold as a stopgap — the **re-run / re-diff** feature (#33) shows this delta directly against this morning's number, not requiring a manual comparison. She notes the classifier vendor needs a permanent fix, not just her team's workaround, and files that as a vendor-management item — outside AgentGuard's scope, but visible because of what AgentGuard measured.

## 5:10pm — Priya, unrelated, a different company entirely (a parallel touchpoint, same day)

At the same hour, on a completely unrelated account, Priya (`journeys/edge_low.md`) runs her second campaign after tightening her system prompt, using the same **configurable attacker registry** (#7) and the same **final-window ASR** computation (#17) that produced Elena's board-ready number and David's audit export. Nothing about the mechanism differs between her session and Elena's day — only the volume, the organizational scaffolding around it, and what each of them does with the number once it exists.

## 6:00pm — Close of day

Elena's durable record for the day: one flagged regression, investigated, re-evaluated, and resolved with a workaround, all timestamped and diffed against the prior week's baseline. David's durable record: one export, attached to one audit response, that he never had to interpret beyond its headline numbers. Both records come from the same four-stage loop (Configure → Attack → Observe → Adapt → Report) — the difference between Elena's day and David's day is entirely in which single screen each of them touched, not in what ran underneath it.

**What a skeptic can verify**: David's only touchpoint across the entire day is one export screen, used for five minutes, for a real external obligation (an auditor's question) — not an invented urgency, and not a claim that he uses the product "seamlessly" or "effortlessly." He uses it once, for the one job his persona card names, and the rest of his day is unaffected by AgentGuard, exactly as `product/PRD.md` §4 specifies.
