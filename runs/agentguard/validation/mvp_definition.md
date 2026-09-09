# MVP Definition

**What this is**: AgentGuard's two MVPs, kept deliberately distinct — a low-fidelity artifact that tests whether the *problem* is real, and a high-fidelity one that tests whether the *solution* is bought — plus the earlyvangelist definition that says who is qualified to test either one.

**Why it exists**: `strategy/gtm.md`'s 90-day motion describes what gets built and shipped, but treats "the product" as one thing; Blank's method insists on separating the problem-test MVP from the solution-test MVP because conflating them is how teams build months of software before learning the underlying pain isn't what they thought. The failure this document prevents: skipping straight to the high-fidelity build (which `strategy/gtm.md` already schedules for days 1–30) without ever running the cheaper, faster low-fidelity test that could kill the wedge for a fraction of the cost.

**How to read it**: the low-fidelity MVP is not a smaller version of the high-fidelity one — it deliberately is not software at all. A skeptic should check that the falsifying result for each MVP is a real, statable outcome, not a rephrased description of what the MVP does.

**Depends on / feeds**: the low-fidelity MVP operationalizes `validation/riskiest_assumptions.md` row 1 into something a person can actually run; the high-fidelity MVP is `strategy/gtm.md`'s days-1–30 free-tier build, described here from the validation angle rather than the build-schedule angle. The earlyvangelist definition draws directly from `strategy/personas.md`'s Marcus card. Feeds `validation/stage_gate.md`'s exit criteria and `validation/discovery_guide.md`'s screening use.

---

## Low-fidelity MVP — tests whether the problem is real

**What it is**: a manual, by-hand matched-budget comparison, run by a team member (not software) against one design partner's staging target agent. A person plays the red-team agent role — writing and iterating injection attempts using AutoDojo's published technique as a manual protocol rather than automated code — for N rounds (proposed default N≈50, per `validation/experiment_board.md` row 1, unconfirmed) against one defense (defensive prompting), while a second person separately draws N attacks with replacement from InjecAgent's published static set against the same target/defense pair. Results (pass/fail per round, and a rough utility check — did the legitimate task still complete) are tallied by hand and reported as an ASR gap.

**What it does**: answers the single question `BRIEF.md` says the entire wedge depends on — is there a materially higher ASR from adapting than from static draws, at equal budget, on a real (if small) target agent — using the cheapest possible version of the test, with no software built.

**What it deliberately omits**: automation of the attacker or the scoring; a user interface of any kind; more than one defense type; self-serve signup; billing; the actual Comparison Report format; any claim that this represents a repeatable *product* — it is a research exercise wearing the shape of the eventual product, nothing more.

**The question it answers**: is the riskiest assumption (`validation/riskiest_assumptions.md` row 1) worth automating at all?

**The falsifying result**: the ASR gap comes back null or negative, and/or the design partner — after seeing the by-hand report — says it tells them nothing their existing Garak/manual-checklist workaround (`strategy/personas.md`'s Marcus card) doesn't already tell them. Either outcome is a valid, reportable result per `BRIEF.md`'s own instruction, not a failed exercise.

## High-fidelity MVP — tests whether the solution is bought

**What it is**: the actual self-serve free tier described in `strategy/gtm.md`'s days 1–30 build phase — an open-source scanner / free-tier Comparison Report, automated, running against a small set of reference target agents, covering all four named defense types (defensive prompting, classifier-based, rule-based tool-call validation, baseline/none), matching `BRIEF.md`'s year-one scope exactly (staging/sandboxed only, text-based injection only, no custom defense authoring, a small number of reference agent harnesses — not broad framework compatibility).

**What it does**: lets a stranger, with zero prior relationship to this venture, discover the tool via GitHub/developer search or methodology content, run a campaign unassisted, interpret the result, and — for the first 3 target customers — decide to pay $750–$2,500 for a full report (`strategy/gtm.md` days 31–60).

**What it deliberately omits**: production traffic access (`BRIEF.md` Year-one scope item 1); custom defense authoring (item 2); multi-modal injection surfaces (item 3); cross-agent-framework certification (item 4); any account-manager or guided-onboarding motion (`strategy/sales_roadmap.md`'s beachhead sales process names none as needed at this price point); edge-high-specific features (deferred past day 90 per `strategy/gtm.md`).

**The question it answers**: will a stranger, with no relationship and no sales touch, actually pay for this — validating the entire self-serve, zero-cash-acquisition business model (`ASSUMPTIONS.md` A3, `strategy/business_model_canvas.md`'s Channels and Customer Relationships hypotheses), not just the underlying attack-technique claim the low-fidelity MVP tests.

**The falsifying result**: fewer than 3 distinct paying companies by day 60 (`strategy/gtm.md`'s own stated success metric), or free-tier users demonstrably cannot interpret a Comparison Report unassisted (surfaced via `strategy/business_model_canvas.md`'s Customer Relationships test).

## Earlyvangelist definition

Per Blank's method, an earlyvangelist is not just an interested prospect — they have already, independently, done things that prove the pain is real and urgent enough to have acted on before AgentGuard existed. Tied directly to Marcus's actual documented behavior in `strategy/personas.md`, a person counts as an earlyvangelist only if they have **already**:

1. **Deployed a tool-using agent with real tool or data access** in a production or near-production environment — not a demo or a personal side project (Marcus's Slack-integrated support agent with document and CRM access).
2. **Already run some form of adversarial or security testing against it manually** — Garak, PyRIT, or a hand-written OWASP LLM Top 10 checklist — meaning they are already spending real time on this problem, not needing to be convinced the problem exists.
3. **Already privately distrusts their own "no findings" result** — has already, unprompted, articulated doubt that a static test's clean result actually means the defense is safe (Marcus's persona: "privately doesn't trust the result because he knows Garak's probe library is static").
4. **Already has a recurring, dated trigger event on a real calendar** — a release that expands tool or data access — not a hypothetical future concern (Marcus's 48-hour sprint deadline before a refund-processing tool-access expansion).
5. **Already has budget authority, or a manager who will approve, at the $750–$2,500 price point without a new procurement process** — i.e., is already structurally capable of paying without waiting for a process AgentGuard cannot yet clear (`strategy/sales_roadmap.md`'s structural note that this price point may fall entirely within Marcus's own discretionary authority).

A person who clears `validation/discovery_guide.md`'s Marcus screening criteria but fails any one of these five is a legitimate discovery-interview candidate, not yet an earlyvangelist — the distinction matters because `validation/experiment_board.md`'s design-partner test (feeding the low-fidelity MVP above) should be run with an earlyvangelist specifically, not any screened interviewee.

## Recommended next 3

1. **Run the low-fidelity MVP before the high-fidelity one, even though `strategy/gtm.md`'s build schedule starts with the automated free tier** — it answers the more fundamental question (`validation/riskiest_assumptions.md` row 1) for a fraction of the cost and time, and a null/negative result there should stop or redirect the days-1–30 build before more engineering time is spent.
2. **Recruit the low-fidelity MVP's design partner from the earlyvangelist definition above, not from a general discovery-interview pool** — a non-earlyvangelist design partner risks a false-negative falsifying result (disinterest caused by not having the underlying pain yet, not by the product failing to solve it).
3. **Do not let the high-fidelity MVP's scope creep past `BRIEF.md`'s Year-one scope exclusions during the days-1–30 build** — every omission listed above is a deliberate decision already made upstream; re-litigating them mid-build (e.g., "let's just add one custom defense type") would be exactly the scope-creep failure a stage-gated MVP definition exists to prevent.
