# AgentGuard — Founder Brief

one-line: An adaptive red-team/blue-team evaluation platform that runs the same budget-matched, feedback-only adaptive attack campaign against each of a target agent's candidate defenses and reports attack success and legitimate-task utility side by side — the standing, reproducible cross-defense comparison that neither the academic adaptive-attack literature (e.g. AutoDojo) nor proprietary red-teaming vendors (e.g. Adversa AI) currently publish, so security teams learn not just whether a defense holds against an adapting attacker, but what it costs them to deploy it.

domain: AI security / agentic-AI evaluation infrastructure
stage: idea — graduate capstone, no implementation exists yet

## Problem

Tool-using AI agents that read email, documents, calendars, and webpages are vulnerable to **indirect prompt injection**: malicious instructions hidden inside the content the agent is asked to process, which can hijack the agent into taking unauthorized actions (exfiltrating data, sending messages, executing unintended tool calls) without the user ever typing an adversarial prompt themselves.

The public benchmarks that exist to measure this — AgentDojo, InjecAgent, Agent Security Bench, BIPIA — evaluate a defense against a **fixed, published set of known attacks**. A defense that scores well against last year's static attack set can still be broken by an attacker that adapts in real time to *that specific defense*, and a team relying on a static benchmark score has no way to know how much of that score would erode against such an adversary. The failure this document exists to prevent: a security/ML platform team ships an agent behind a defense that looks solid on a static leaderboard, and the leaderboard score turns out to say nothing about resilience against an adversary willing to iterate.

## Users & spectrum

User ≠ payer here is mostly collapsed — the security/ML platform engineer who runs the evaluation is also who provisions and pays for it (self-serve, usage-based; see Business model).

- **edge-low**: a solo developer shipping a single agent feature (e.g., an email-drafting assistant with calendar access), no dedicated security staff, wants a fast automated pass/fail signal before launch.
- **beachhead**: a security/ML platform team at a company running tool-using agents in production (agent with email + calendar + document access), running an adaptive evaluation campaign before each release that expands tool scope or data access.
- **edge-high**: an enterprise AI red-team function, or an agent-platform vendor itself, running continuous adaptive evaluation as part of a formal security program — same self-serve API, much higher run volume and frequency (continuous rather than per-release).

One system serves all three: the adaptive engine and defense set are identical: what differs is run frequency and volume, not a separate "enterprise" product track.

## Why now

*(verified in research — see research/sources.md S1–S8, S101–S107; ASSUMPTIONS.md A1 resolved)*

1. Tool-using / agentic LLM deployments moved from demo to production across 2024–2026, expanding the real attack surface from chatbots (bad output) to agents (unauthorized actions with real consequences).
2. Indirect prompt injection is now a named, documented threat class with four public benchmarks: BIPIA (Dec 2023, the first of the four [S6]), InjecAgent (Mar 2024 [S3]), AgentDojo (Jun 2024 [S1]), Agent Security Bench (Oct 2024 [S5]). InjecAgent and Agent Security Bench are genuinely fixed-attack-set benchmarks by design. **AgentDojo is not** — it is an extensible environment explicitly built to host adaptive attacks and defenses; what is fixed is the *attack distribution it originally shipped with*, not the framework itself [S1, S13]. **Important correction from research**: the "no one automates adaptive attacks against agents" framing this pack originally implied is false. Academic prior art (AutoDojo, MUZZLE, "The Attacker Moves Second," and others — research/landscape.md §1), a U.S. government human-red-teaming exercise (NIST CAISI, Jan 2025 [S27]), and a funded commercial vendor (Adversa AI [S50]) all already do adaptive evaluation against agent/LLM defenses. See research/competitors.md and the Competition section below for the corrected differentiation claim.
3. LLM inference cost dropped roughly 4x at the frontier tier in one year (GPT-4, 2023: $30/$60 per million tokens → GPT-4o, 2024: $5/$15 [S101]) and cheap-tier options now run as low as $0.10/$0.40 per million tokens [S106] — cheap enough to make many-round adaptive campaigns routinely affordable, supporting the riskiest-assumption test's <$1k budget.

## Wedge & 10-year vision

**Wedge (revised after research — see ASSUMPTIONS.md A9)**: the differentiator is **the comparison, not the attacker**. A red-team agent — reusing established adaptive-attack techniques (e.g. AutoDojo's black-box iterative optimizer [S13]) as one configurable attacker rather than inventing attack generation from scratch — runs the *same budget-matched adaptive campaign* against each of four blue-team defense configurations (defensive prompting / classifier-based detection / rule-based tool-call validation / baseline-none) on the same target agent, observing only per-round pass/fail outcome — **feedback-only**, the primary threat model, since that is what a real attacker facing an unknown target actually gets — with a **white-box** condition (defense type told up front) alongside as an upper-bound comparison. See Vocabulary for both terms. No benchmark or vendor found in research publishes this standing, reproducible, cross-defense, utility-paired comparison: AutoDojo measures ASR recovery within one framework and does not measure utility; NIST CAISI's result is a one-off human-red-teaming exercise on one model; Adversa AI's engagements are proprietary and per-customer, producing no publishable comparative science across defense families.

Output per campaign, reported **per defense, side by side, at equal attempt budget**: **final-window ASR** (headline — ASR over the last *k* rounds, where the adaptive attacker has converged), **attempts-to-first-success**, campaign-average ASR (secondary), **utility** — legitimate task completion under attack, aligned with AgentDojo's definition — and an adaptation curve plotting ASR round over round. Campaign ASR is not directly comparable to a static benchmark's single-shot ASR; see Vocabulary "attack success rate (ASR)" for the bridge.

**10-year vision**: a dual model. The comparative evaluation protocol stays open and academically credible — publishing budget-matched, utility-paired, cross-defense results the way AutoDojo/AgentDojo publish single-framework results, cited as extending that literature, not competing with it. The continuously-updated, run-against-your-actual-deployed-defenses *service* is the paid product: the thing a team runs because no academic paper or proprietary vendor engagement can tell them, reproducibly, how their specific defense stack trades security for usability against an adapting attacker.

## Mechanism & moat

**Mechanism**: red-team agent (configurable attacker — adopts prior-art adaptive-attack techniques such as AutoDojo's optimizer as one pluggable configuration, not a proprietary attack-generation invention — feedback-only by default, white-box as an upper-bound comparison) → run under a matched attempt budget against each of four blue-team defense configurations on the same target agent → outcome logged per round per defense → cross-defense comparison report (final-window ASR, attempts-to-first-success, campaign-average ASR, utility under attack, benign block rate, adaptation curve — all reported per defense, side by side, at equal budget, reproducibly).

**Moat**: none yet — named as a gap, not invented. The mechanism that *would* eventually compound: an accumulating, reproducible corpus of budget-matched, cross-defense, utility-paired comparison results — a public or semi-public answer to "how much attack resistance does defense type X actually buy you, and what does it cost in blocked legitimate work, at adaptive-attacker budget Y" — that no single-framework academic paper or proprietary per-customer vendor engagement currently produces. This is a hypothesis about a comparative-science network effect, unproven until real evaluation campaigns exist. Do not present it as an established advantage anywhere downstream.

## Competition & failed alternatives (as stated by founder)

AgentDojo, InjecAgent, Agent Security Bench, and BIPIA are real, public benchmarks — our baseline and ground truth, not our competition. InjecAgent and Agent Security Bench are genuinely fixed-attack-set by design. AgentDojo is not a static benchmark itself — it is an extensible environment explicitly built to host adaptive attacks [S1]; what is fixed is the attack distribution it originally shipped with.

**Full competitive teardown — see research/competitors.md.** Three names matter, and none of them is treated as a competitor on the *attack technique* — each is treated as prior art or a differently-shaped rival on the *comparison*:
- **AutoDojo** (academic, open-source [S13]) already runs adaptive black-box attacks inside the AgentDojo environment and beats the shipped static distribution's ASR. AgentGuard adopts this as one attacker configuration rather than competing with it on technique — AgentGuard's claim is the cross-defense, utility-paired comparison AutoDojo doesn't publish.
- **NIST CAISI**, with the UK AI Security Institute, ran a human red-teaming exercise (Jan 2025 [S27]) finding an even larger static-to-adapted gap (11%→81%) on one model — further evidence for the thesis, not a competing automated product; it's a one-off exercise, not a standing reproducible protocol.
- **Adversa AI** [S50] is a real, funded commercial vendor whose marketing explicitly claims mid-run adaptation to observed defenses — the closest commercial competitor found, and its existence/positioning is confirmed (not a rumor); what's unverified is only whether its internal mechanism matches AgentGuard's exact loop. Its engagements are proprietary and per-customer, producing no publishable cross-defense comparison.

The differentiation this brief defends: a **standing, budget-matched, utility-aware comparison protocol across defense families**, reproducible and reported side by side — not the adaptive-attack technique itself, which existing prior art already supplies and which AgentGuard adopts rather than reinvents.

## Business model

Self-serve API/CLI, usage-based: teams point AgentGuard at a staging/sandboxed deployment of their target agent, select which defense configuration is active, and pay per evaluation campaign run. Same delivery motion across all three user tiers (edge-low through edge-high) — they differ in run frequency and volume, not in how they buy. Exact pricing figures and unit economics are **not set in this brief** — deferred to the startup-financials phase per explicit instruction, and will be flagged as assumptions there before being written.

## Founder edge

Four-person graduate capstone team, CMPE 295A/295B, San José State University, two-semester project. The edge is research access and rigor — direct engagement with the named public benchmarks as a graduate research project — not a go-to-market or distribution advantage. No prior company, customers, or domain operating history to claim.

## Riskiest assumption

**"At equal attempt budget, an adversary that adapts round-over-round against per-round feedback achieves materially higher attack success than random draws from a fixed, published attack set (InjecAgent-style) on the same target and defense."** If the gap at equal budget is not clearly positive, the entire wedge collapses — a static benchmark would already be sufficient at that budget, and there is no reason to automate an adaptive adversary at all.

Kills company if false: **yes**.

Two-week, <$1k test, **matched-budget design** (not adaptive-N vs. static-1 — that would let the adaptive arm win on volume alone and prove nothing): run the red-team agent, feedback-only, for N rounds against a single defense (defensive prompting only) on an open-source reference agent harness. Separately, draw N attacks with replacement from InjecAgent's published static attack set against the same target/defense pair — same total attempt budget as the adaptive arm. Report the ASR gap between the two arms at equal N. **A null or negative gap is a valid, reportable outcome**: it would mean a static benchmark is already sufficient at that attempt budget and the adaptive wedge does not hold for this defense — we report it either way, not only if it confirms the hypothesis. At current low-cost frontier-model API pricing, N rounds per arm is affordable well inside a $1k budget within two weeks.

## Year-one scope — deliberately NOT doing

1. **No production traffic access** — evaluates staging/sandboxed agent deployments only; never touches an agent connected to real user data or live production tools. Removes the trust barrier to first adoption.
2. **No custom defense authoring** — ships with the four named defense types (defensive prompting, classifier-based detection, rule-based tool-call validation, baseline/none) as fixed, well-instrumented options; does not yet let customers plug in arbitrary custom defenses.
3. **No multi-modal injection surfaces** — covers text-based indirect injection (email, documents, webpages, calendar invites) only; image-embedded or audio-embedded injection vectors are a distinct, harder research problem, out of scope for year one.
4. **No cross-agent-framework certification** — targets a small number of reference agent harnesses/frameworks deeply, rather than claiming broad compatibility across every agent framework on the market.

## Vocabulary

- **target agent** — the tool-using AI agent under evaluation.
- **injection / indirect prompt injection** — a malicious instruction embedded in content the target agent ingests (email, document, calendar invite, webpage) rather than typed directly by a user.
- **red-team agent** — the automated attacker that generates and evolves injections.
- **blue-team layer / defense** — the guardrail mechanism under test: defensive prompting, classifier-based detection, rule-based tool-call validation, or baseline/none.
- **round** — one attack attempt plus its observed outcome; the unit of adaptation within a campaign.
- **campaign** — a full multi-round adaptive run of the red-team agent against one target agent + one defense configuration.
- **feedback-only (threat model)** — the red-team agent does not know which defense type is deployed or how it is configured; it observes only each round's pass/fail outcome and adapts on that signal alone. This is the **primary** threat model, because it is what a real-world attacker facing an unknown target actually has access to.
- **white-box (threat model)** — the red-team agent is told the defense type (and optionally its configuration) up front. Used only as an **upper-bound comparison condition** — how much better a privileged attacker could do — never as the primary evaluation mode or headline result.
- **attack success rate (ASR)** — the percentage of rounds where an injection achieves its objective (e.g., an unauthorized tool call executed). Reported three ways per campaign: **final-window ASR** (headline — ASR over the last *k* rounds, so early exploration failures don't drag down the number that actually answers "does the attacker get there"), **attempts-to-first-success** (rounds elapsed before the first successful injection — a practicality/speed signal), and **campaign-average ASR** (secondary — ASR across the whole campaign, early rounds included). Campaign ASR in any of these three forms is **not directly comparable** to a static benchmark's published single-shot ASR — a multi-round campaign and a single fixed attempt aren't the same measurement. The bridge to a literature-comparable number is the matched-budget test under Riskiest assumption: N adaptive rounds vs. N random draws from a static attack set, same target, same defense, same total attempts, reported as an ASR gap at equal N.
- **utility (task completion under attack)** — whether the target agent still completes the legitimate task a benign user asked for while a defense is active and an injection attempt is present in the content it processes, aligned with AgentDojo's utility definition (exact wording to be confirmed against the AgentDojo paper in startup-research). Distinct from benign block rate: a request that is never outright blocked can still fail utility if the defense degrades how the agent completes it. Reporting utility alongside ASR is what makes the security/usability trade-off visible — ASR and benign block rate alone cannot show it.
- **benign block rate / false-block rate** — the percentage of legitimate, non-malicious requests a defense outright refuses or blocks. Narrower than utility (above): a request can go unblocked and still fail utility.
- **adaptation curve** — ASR plotted round-over-round within a campaign, showing whether and how fast the red-team agent improves against a specific defense.
- **defense fingerprint** — the behavioral signature of how a given defense responds under adaptive pressure, logged per campaign.
