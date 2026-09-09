# AgentGuard — Product Requirements Document

**Version 0.1 — drafted 2026-09-09 — status: DESIGN ONLY, NOTHING BUILT.** Every capability described below is a specification for what a four-person capstone team intends to build across CMPE 295A/295B, not a description of shipped software. No campaign has been run, no defense has been evaluated, and no UI exists. Treat every present-tense verb in this document ("the platform reports," "the red-team agent generates") as shorthand for "the design specifies that the platform will report" (`BRIEF.md` stage line; `ASSUMPTIONS.md` Restated hard facts).

**What this is**: the product specification for AgentGuard — the core loop in its own verbs, the non-goals that bound year one, the domain-science principles every feature must trace to, the feature set, the (unproven) data flywheel, the oversight/compliance requirements, and the success metrics, in priority order (outcome → engagement → business).

**Why it exists**: `BRIEF.md` states the wedge and the mechanism; `strategy/positioning.md` states the differentiation. Neither tells an engineer what to build first, what to explicitly refuse to build, or which feature earns its place because it serves a named principle rather than because it sounded good in a meeting. The failure this document prevents: a build that drifts toward "a better attacker" (the wedge `ASSUMPTIONS.md` A9 explicitly rejected) because that is the more fun engineering problem, while the actual differentiator — the standing, cross-defense, utility-paired comparison — never gets built because no single feature obviously owns it.

**How to read it**: start with the Non-Goals — they are as load-bearing as the goals, and a skeptic should check each Core feature set row actually cites a principle in §4, not just a phase of the loop. The Data & learning flywheel section is deliberately the least confident section in this document; read it next to see whether the honesty holds.

**Depends on / feeds**: inherits `BRIEF.md` (mechanism, year-one scope, vocabulary), `ASSUMPTIONS.md` A9 (the comparison-not-attacker wedge), `research/survey.md` (first-principles grounding), `strategy/positioning.md` and `strategy/market_type.md` (why the comparison is the differentiator), and `strategy/personas.md` + `strategy/value_prop_canvas.md` (target users). Feeds `product/features_flagship.md`, `product/features_prioritized.md`, `product/journeys/*.md`, `product/ux_spec.md`, and (downstream, not yet generated) `tech/whitepaper.md` and `tech/architecture/`.

---

## 1. Executive summary & vision

AgentGuard is a design for an evaluation platform, not a defense product. It does not protect a target agent; it tells a team how much protection their chosen defense actually buys them against an attacker willing to iterate, and what that protection costs in legitimate work blocked. The core loop, named in the domain's own verbs:

**Configure → Attack → Observe → Adapt → Report**

| Verb | What happens | System component (design) |
|---|---|---|
| **Configure** | A team points AgentGuard at a staging/sandboxed target agent, selects which of the four fixed defense configurations to evaluate (one, several, or all four), and sets an attempt budget (rounds per campaign) | Campaign configuration layer (CLI/API) |
| **Attack** | The red-team agent generates round *n*'s injection, using an adopted adaptive-attack technique (AutoDojo's black-box optimizer configuration is the year-one default — `BRIEF.md` Mechanism, `ASSUMPTIONS.md` A9) as one configurable attacker, not a proprietary invention | Red-team agent (configurable attacker) |
| **Observe** | The target agent (behind the selected defense) processes the round, and the outcome — pass/fail, tool calls made, whether the legitimate task also completed — is logged | Outcome logger, one row per round |
| **Adapt** | Feedback-only by default: the red-team agent sees only the round's pass/fail outcome (not the defense's identity or configuration) and updates its next attempt on that signal alone — the primary threat model, because that is what a real attacker facing an unknown target actually has (`BRIEF.md` Vocabulary). A white-box condition (defense type disclosed) runs in parallel only as an upper-bound comparison, never as the headline | Adaptation controller |
| **Report** | Once every configured defense has completed its own budget-matched campaign, the platform assembles the cross-defense comparison: final-window ASR, attempts-to-first-success, campaign-average ASR, utility under attack, and an adaptation curve — **per defense, side by side, at equal attempt budget** | Comparison report generator |

The loop repeats per defense configuration within one campaign set; the **Report** step, which nothing found in research publishes in this standing, reproducible, cross-defense, utility-paired form (`strategy/positioning.md`), is the product. Configure/Attack/Observe/Adapt alone reproduce what AutoDojo already does inside one framework, once, without a utility metric (`research/competitors.md`). AgentGuard's contribution is closing the loop across defense families and publishing the trade-off, not any single stage of it in isolation.

## 2. Goals

1. Produce, per campaign, a reproducible, budget-matched, cross-defense comparison of attack success and legitimate-task utility that a security engineer can attach to a release risk-assessment ticket without further interpretation (Marcus's job, `strategy/value_prop_canvas.md`).
2. Make the feedback-only threat model the default and the headline, with white-box as a clearly-labeled upper-bound condition only (`BRIEF.md` Vocabulary; resolved in `ASSUMPTIONS.md`, Decisions settled this correction round).
3. Report utility alongside attack success in every output, so the security/usability trade-off is visible rather than asserted (`strategy/value_prop_canvas.md`, Marcus's job #3).
4. Ship a report format that functions as audit-adjacent evidence for ISO 42001's Operation/Performance Evaluation clauses (`research/sources.md` S113, S114) and EU AI Act Article 15's adversarial-robustness documentation expectation (S108, S109) — without claiming SOC 2 coverage, which no source in this research confirms exists for this category (S "UNFINDABLE" note, `research/sources.md`).
5. Serve edge-low through edge-high on one system, differing only in run frequency and volume, never a separate "enterprise" feature track (`BRIEF.md` Users & spectrum; `ASSUMPTIONS.md` A3).

## 3. Non-goals — year-one scope, stated as real renunciations

These are not "not yet" placeholders to be apologized for; they are deliberate boundaries that make the product buildable by a four-person team in two semesters and reduce first-adoption trust risk. Carried verbatim in intent from `BRIEF.md`'s Year-one scope section:

1. **No production traffic, ever.** AgentGuard evaluates staging/sandboxed target agent deployments only. It will not be built with a code path that accepts a production credential or touches an agent connected to real user data or live production tools. This is not a rate-limited or permissioned "pro" feature deferred to year two — it is a design boundary, because it is what makes the product safe for a stranger (Priya, Sofia) to try without a security review of AgentGuard itself first.
2. **No custom defense authoring.** The platform ships with exactly four defense configurations — defensive prompting, classifier-based detection, rule-based tool-call validation, baseline/none — well-instrumented and comparable to each other. It will not expose an SDK or config surface for a customer to plug in an arbitrary fifth defense in year one. This renounces breadth (any customer's exact production defense stack) in favor of depth (four defenses measured rigorously and comparably) — the same choice `ASSUMPTIONS.md` A9 already made when it rejected "breadth across arbitrary customer-deployed defenses" as a candidate differentiator.
3. **No multi-modal injection.** Attacks are text-only — email, documents, webpages, calendar invites. Image-embedded and audio-embedded injection (OWASP's 2026 edition names cross-modal injection as an emerging category, `research/sources.md` S118) are explicitly out of scope, not because they are unimportant but because they are a distinct, harder research problem that would dilute focus on the comparison protocol this product exists to prove.
4. **No cross-agent-framework certification.** AgentGuard targets a small number of reference agent harnesses deeply (the frameworks the four baseline benchmarks already use, per `research/survey.md` §4) rather than claiming broad compatibility across every agent framework on the market. It will not market a "works with any agent" claim in year one.
5. **Not a runtime defense or firewall product.** AgentGuard evaluates defenses; it does not ship one. A customer who wants AgentGuard to block an attack in production is asking for a different product — this is stated explicitly so sales conversations do not quietly redefine the product under deadline pressure.
6. **Not a claim to replace an internal red-team function.** Per Elena's objection (`strategy/personas.md` card 3), AgentGuard is positioned as a second, comparable, reproducible source of signal alongside an internal red team or an existing vendor engagement — not a replacement for either. The product will not market itself as "you no longer need a red team."
7. **No proprietary attack-generation claim.** The red-team agent's adaptive-attack technique is adopted from published prior art (AutoDojo's black-box optimizer, `research/sources.md` S13) as one configurable attacker. The product will describe itself as running a "configurable attacker," never a "proprietary attack AI" — this is a non-goal at the level of marketing language, not just engineering, because overclaiming here is the single fastest way to lose credibility with the exact skeptical, research-literate buyer (Marcus, Elena) this product needs (`ASSUMPTIONS.md` A9).

## 4. Target users & personas

Full spectrum, one adaptive system — the loop in §1 and the defense set in §3.2 are identical for every tier below; only run frequency and volume differ (`BRIEF.md` Users & spectrum; `ASSUMPTIONS.md` A3). No stigmatized "starter" vs. "enterprise" feature split exists in this design. Personas are inherited verbatim from `strategy/personas.md`, not reinvented:

| Persona | Tier | Core job AgentGuard serves | Primary artifact they touch |
|---|---|---|---|
| **Priya Nair**, 27, solo developer | Edge-low | A free-tier, no-signup-friction pass/fail signal before flipping on write access to a user's calendar | A single-defense campaign run from a GitHub Action |
| **Marcus Webb**, 34, security engineer, fintech | Beachhead | A report attachable to a release risk-assessment ticket before expanding agent tool scope | The per-release, four-defense comparison report |
| **Dr. Elena Osei**, 41, Head of AI Red Team, enterprise | Edge-high (user) | One reproducible protocol run continuously across every agent and defense in a large portfolio | The trended, cross-agent comparison history |
| **David Chen**, 46, CISO (Elena's manager, payer) | Edge-high (buyer, ≠ user) | Certification-grade evidence for ISO 42001 and board/auditor questions, without opening the product himself | The audit-ready report export |
| **Sofia Ramirez**, 38, Head of Trust & Safety, agent-platform vendor | Edge-high (alternate buyer) | A comparison report she can excerpt into her own trust-center documentation for prospects | The publishable/excerptable comparison report |

## 5. First-principles grounding (non-negotiable)

Every major feature in §6 maps to at least one principle below. Each is cited to `research/survey.md` or the research artifact that established it; none is asserted without a source or an explicit `(assumption: basis)` tag.

1. **Matched-budget principle.** An ASR comparison between an adaptive attacker and any baseline (a static attack set, or another defense) is only meaningful at equal total attempt budget — an adaptive arm run for more attempts than its comparison wins on volume alone and proves nothing about adaptation itself (`BRIEF.md` Riskiest assumption; `ASSUMPTIONS.md`, Decisions settled this correction round). This is the single most load-bearing principle in the product — it governs how campaigns are configured, not just how results are reported.
2. **Feedback-only-as-primary-threat-model principle.** The attacker that matters most to measure against is the one with the least privileged information — pass/fail per round, no defense identity — because that is what a real-world attacker facing an unknown target actually has (`research/survey.md` §2, taxonomy by threat model). White-box is a valid upper-bound condition but must never be the headline result.
3. **Utility-paired-reporting principle.** ASR alone cannot show the security/usability trade-off a defense creates: a defense can suppress attacks while also degrading legitimate task completion, and a report that omits utility hides exactly the number a product team needs to push back on an over-strict defense (`research/capability_table.md`, AgentDojo utility metric row; `BRIEF.md` Vocabulary, "utility" entry).
4. **Final-window-ASR-as-headline principle.** Early-round exploration failures are the expected shape of adaptation, not a defect to average into a lower campaign-wide number — final-window ASR (the last *k* rounds, where the attacker has converged) answers "does the attacker get there," which is the question that matters for a deployment decision (`ASSUMPTIONS.md`, Decisions settled this correction round; `BRIEF.md` Vocabulary).
5. **Cross-defense-family-comparability principle.** A comparison confined to one defense, or to variations of the same defense type, cannot answer "which defense family should we deploy" — the question every persona in §4 actually has. This is the principle that makes the Report stage (not any single Attack-stage improvement) the product (`strategy/positioning.md`, two axes).
6. **Self-reported-robustness-does-not-survive-adaptive-pressure principle.** Published defenses that report near-zero vulnerability under static evaluation have been shown, repeatedly, to collapse under genuine adaptive pressure — 12 of 12 recently published defenses broken, most to >90% ASR, in a joint OpenAI/Anthropic/Google DeepMind study (`research/sources.md` S9); Progent's and PromptGuard 2's self-reported robustness numbers are explicitly flagged in `research/capability_table.md` as unverified under adaptive pressure for exactly this reason. This is the principle that justifies the product's existence at all: a defense's own claimed number is not sufficient evidence.
7. **In-context live adaptation over offline-trained attacker principle.** The red-team agent adapts within a session, with no training phase, rather than being pre-trained via reinforcement learning against a fixed defense distribution (`research/landscape.md` §5; `research/survey.md` §2). This is a deliberate architecture choice, not merely "we didn't get to RL yet": live adaptation can run against a brand-new customer defense configuration immediately, with no retraining cycle, which is a real speed-to-value property, not an adjective.
8. **Reproducibility-over-one-off-engagement principle.** The protocol must run the same way every time it is invoked, producing a comparable number across runs and across time — not a bespoke engagement whose methodology varies by customer, the way Adversa AI's proprietary, per-customer engagements do (`research/competitors.md`; Elena's "must-have" quote, `strategy/personas.md` card 3).
9. **Novelty-is-in-the-application-and-comparison, not-the-loop principle.** The "attacker adapts to observed defense behavior" loop is 15+ years old in coverage-guided fuzzing and 5–10 years old in game-theoretic adaptive penetration-testing research (`research/survey.md` §1, citing S144–S149); AgentGuard's design must not claim novelty for the adaptation loop itself, only for its disciplined application to agentic indirect injection and the cross-defense comparison it produces. This principle directly bounds the marketing language non-goal in §3.7.
10. **Staging-only-by-design principle.** Trust in a pre-traction, zero-credibility vendor (`strategy/personas.md` card 4, David's objection) is easiest to earn by removing the worst-case failure mode entirely: the product cannot leak or damage production data because it structurally never touches it (`BRIEF.md` Year-one scope item 1). This is a design principle, not just a scope limitation — it shapes the Configure stage's connection model directly (§6).

## 6. Core feature set (superset), organized by phase of the core loop

Each feature is tagged with the principle(s) it maps to (§5, by number). This is the organizing table; `product/features_flagship.md` expands the top 20 with mechanism and visible product moment, and `product/features_prioritized.md` sequences all 50 into Now/Next/Later.

### Configure
- Staging-only connection model — no production credential type accepted (P10)
- Defense-set selector — choose 1–4 of the fixed defense configurations per campaign (P5)
- Attempt-budget field, enforced identically across every defense in the set (P1)
- Reference-harness picker, scoped to the small number of year-one-supported agent harnesses (non-goal §3.4)

### Attack
- Configurable attacker registry — AutoDojo's optimizer as the year-one default configuration, explicitly labeled as adopted prior art, not proprietary (P9, non-goal §3.7)
- Feedback-only mode (default) — attacker receives pass/fail only (P2)
- White-box mode (opt-in comparison condition, always rendered as a separate labeled column, never merged into the headline) (P2)
- Text-only injection surface: email, document, webpage, calendar invite payload generators (non-goal §3.3)

### Observe
- Per-round outcome logger (pass/fail, tool calls attempted/executed, legitimate-task completion flag) (P3, P1)
- Defense fingerprint capture — the behavioral signature of how each defense responded under pressure, logged per campaign (P6)

### Adapt
- Round-over-round adaptation controller, in-context, no offline training phase (P7)
- Attempts-to-first-success tracker (P4)
- Adaptation-curve data pipeline (ASR per round, per defense) (P4, P5)

### Report
- Final-window ASR computation (last *k* rounds, configurable *k*) as the headline metric (P4)
- Campaign-average ASR, reported as secondary, never headline (P4)
- Utility-under-attack metric, aligned to AgentDojo's definition (P3)
- Benign block rate, reported distinct from utility (P3)
- Cross-defense comparison table — all configured defenses, same attempt budget, one screen (P5, P1)
- Adaptation-curve chart, per defense, overlaid for comparison (P5)
- Audit-ready export (PDF/structured data) mapped to ISO 42001's Operation/Performance Evaluation clauses (P6, Goal 4)
- Re-run / re-diff against a prior campaign on the same agent (P8)

## 7. Data & learning flywheel

Stated as plainly as `BRIEF.md`'s own Moat section states it: **this is a hypothesis, not a working system.** The mechanism that would eventually compound, if it compounds at all: every completed campaign adds one more budget-matched, cross-defense, utility-paired result to an accumulating corpus — over time, a semi-public answer to "how much attack resistance does defense type X actually buy, and what does it cost in blocked legitimate work, at adaptive-attacker budget Y" that no single-framework academic paper or proprietary per-customer engagement currently produces (`BRIEF.md` Moat; `ASSUMPTIONS.md` A2).

What the design commits to now, without overclaiming a working flywheel:
- **What the system would remember per target/defense pair**: round-level outcomes, the defense fingerprint, and the final comparison metrics, retained so a re-run can be diffed against history (§6, Report).
- **What it does not yet claim**: that accumulated campaigns improve the red-team agent's attack quality against future targets (a genuine network effect), that a cross-customer aggregate benchmark exists or is safe to publish without customer consent, or that any volume of runs has been produced to test whether compounding value is real. Zero campaigns have been run as of this document's drafting (`ASSUMPTIONS.md`, Restated hard facts).
- **Action for every downstream artifact** (already stated in `ASSUMPTIONS.md` A2 and repeated here because the PRD is where an engineer might otherwise start building "flywheel features" prematurely): do not build cross-customer aggregation, benchmark publication, or attacker-quality-improves-with-volume claims into year-one scope. These are hypotheses to test after real campaign volume exists, not features to ship now.

## 8. Oversight, safety, privacy, and compliance requirements

1. **Staging/sandboxed scope enforcement is a hard requirement, not a policy note.** The Configure stage (§6) must structurally reject production-shaped credentials or endpoints — this is the single clearest trust-barrier removal available to a pre-traction vendor (non-goal §3.1; Sofia's objection, `strategy/personas.md` card 5).
2. **ISO/IEC 42001 alignment.** ISO 42001 (published 2023-12-18, the first certifiable international AI management system standard) requires AI systems to be "robust against adversarial attacks" and treats red-team-style evidence as certification-grade under its Operation and Performance Evaluation clauses (`research/sources.md` S113, S114). The Report stage's audit-ready export (§6) is designed against this clause structure specifically, not as a generic PDF.
3. **EU AI Act Article 15 alignment.** High-risk AI systems must demonstrate resilience against exploitation of vulnerabilities, and general-purpose AI models with systemic risk face a mandatory adversarial-testing ("red teaming") disclosure requirement (`research/sources.md` S108, S109). AgentGuard's reproducible, exportable methodology is designed to serve as one input to that disclosure, not as legal compliance certification itself — the product does not claim to make a customer EU AI Act compliant, only to produce evidence a compliance function can use.
4. **NIST AI RMF alignment.** NIST AI 600-1 (the Generative AI Profile, July 2024) recommends AI red-teaming as part of the Measure function of the NIST AI Risk Management Framework (`research/sources.md` S111, S112) — AgentGuard's campaign outputs are designed to slot into that function's evidence trail.
5. **No SOC 2 claim.** No source found in this research confirms SOC 2 has an AI-red-teaming-specific Trust Services Criterion as of this writing (`research/sources.md`, flagged UNFINDABLE). The product must not claim SOC 2 relevance in marketing or in the report export until this is independently re-verified.
6. **Malicious-payload handling.** Because the Attack stage generates and logs real injection payloads (text-only, per non-goal §3.3), the design must treat the campaign log itself as sensitive artifact storage — access-controlled, not casually exportable in full alongside the summary report, since a leaked attack log is itself a usable attack toolkit against the customer's own defense.
7. **Defense-vendor and target-agent-owner disclosure.** Because campaigns may probe defenses built by third parties (e.g., Meta's PromptGuard 2, `research/sources.md` S33) even when run by AgentGuard's own customer, the design should not publish or aggregate results in any customer-identifying or defense-vendor-identifying form without explicit consent — directly gating the data-flywheel hypothesis in §7.

## 9. Success metrics

Outcome first, then engagement, then business — never the reverse, because a business metric with no outcome evidence behind it is exactly the "vanity metric" trap a pre-traction, zero-customer product must avoid (`ASSUMPTIONS.md`, Restated hard facts).

### Outcome metrics (the real "did it work" measure)
1. **Matched-budget ASR gap delivered per campaign** — every completed campaign produces a reportable ASR gap between defenses at equal attempt budget, including a null or negative result where that is what the data shows (`BRIEF.md` Riskiest assumption — "a null or negative gap is a valid, reportable outcome, not a failure of the product").
2. **Utility delta reported alongside every ASR result** — 100% of campaign reports include utility-under-attack, not just ASR, for every defense evaluated (Goal 3).
3. **Cross-defense comparisons completed, not single-defense runs** — the fraction of campaigns that evaluate more than one defense family in the same run, since a single-defense run does not exercise the product's actual differentiator (§1, Report stage).

### Engagement metrics
4. **Campaigns run** per user per month, by tier (edge-low/beachhead/edge-high) — volume/frequency is the only dimension that is expected to differ across tiers (`BRIEF.md` Users & spectrum).
5. **Repeat-run rate before release** — the fraction of beachhead users who re-run a campaign on the same agent before a subsequent release, the specific behavior Marcus's persona describes as the trigger to switch (`strategy/personas.md` card 2).
6. **Report re-export / re-share rate** — audit-export downloads per campaign, a proxy for whether David's persona's job (certification-grade evidence) is actually being served (`strategy/value_prop_canvas.md`).

### Business metrics
7. **Self-serve campaign-run revenue** (`assumption: exact pricing and unit economics are explicitly deferred to the startup-financials phase per `ASSUMPTIONS.md` A4 — no figures are invented here`).
8. **Tier mix over time** (edge-low free/low-cost usage vs. beachhead paid vs. edge-high high-volume) as a leading indicator of which persona the product is actually reaching, independent of revenue totals, which are not yet forecastable given zero traction (`ASSUMPTIONS.md`, Restated hard facts).

---

**Scope-compression note (quality-bar honesty requirement)**: this PRD compresses the Core feature set (§6) to the organizing list that `features_flagship.md` and `features_prioritized.md` expand in full detail, rather than repeating all 50 features' mechanism/principle/effort detail inline here — that detail lives in the two dedicated files so this document stays a specification, not a duplicate feature database.
