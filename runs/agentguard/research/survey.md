# Survey — adaptive adversarial evaluation of indirect prompt injection defenses in tool-using LLM agents

**What this is**: a dated mini survey of the scientific ground AgentGuard stands on — classical foundations, taxonomy of attack/defense approaches, enabling technology, evaluation methodology, and the evidence for and against the core mechanism (adaptive attackers meaningfully outperform static ones against agent defenses).

**Why it exists**: `tech/whitepaper.md` and `product/PRD.md` will need to cite a coherent scientific account of why this mechanism should work, not just that it sounds plausible. The failure this document prevents: a whitepaper built on the assumption that adaptive-vs-agent-defense evaluation is unstudied, when a specific, checkable body of 2025–2026 literature already exists and disagrees on some particulars.

**How to read it**: §5 (evidence for/against) is the load-bearing section — it is where BRIEF.md's riskiest assumption gets its strongest indirect support and its clearest open questions. §6 (open questions) should be read alongside `ASSUMPTIONS.md` before any downstream artifact treats the mechanism as validated.

**Depends on / feeds**: synthesizes `research/sources.md`, `research/landscape.md`, and `research/capability_table.md`. Feeds `tech/whitepaper.md`, `tech/deep_dives.md`, and `product/PRD.md`'s mechanism section directly.

---

## Abstract

Tool-using LLM agents that ingest untrusted external content (email, documents, calendars, webpages) are vulnerable to indirect prompt injection: instructions embedded in that content that hijack the agent's tool calls. Four public benchmarks — AgentDojo (2024-06) [S1], InjecAgent (2024-03) [S3], Agent Security Bench (2024-10) [S5], and BIPIA (2023-12) [S6] — established static, fixed-attack-set evaluation as the field's methodological baseline, and each of the four's own authors or follow-on work explicitly notes that adaptive-attacker evaluation was left as future work or an identified gap. That gap has since been substantially, if unevenly, filled: at least four 2025–2026 papers (AutoDojo [S13], MUZZLE [S12], PI-Hunter [S15], "Adaptive Attacks Break Defenses Against Indirect Prompt Injection Attacks on LLM Agents" [S11]) and one cross-lab collaboration spanning chatbot and general LLM defenses ("The Attacker Moves Second," OpenAI/Anthropic/Google DeepMind [S9]) demonstrate that adaptive attackers reliably and substantially outperform static ones against agent and LLM defenses that report near-zero vulnerability under fixed-attack-set evaluation. This survey lays out the classical foundations, the current taxonomy of approaches, the enabling technology, and — most load-bearing for AgentGuard specifically — the evidence for and against the proposition that this gap is commercially exploitable as a continuously-available evaluation service rather than already closed by free/open-source tooling.

## 1. Classical foundations

Adversarial testing of machine learning systems predates LLMs by a decade. Szegedy et al. (2014) [S132] first showed neural image classifiers can be fooled by imperceptible input perturbations; Goodfellow et al.'s Fast Gradient Sign Method (2015) [S133] established both the canonical attack and the adversarial-training defense pattern much later work still follows. Google Brain's NIPS 2017 Adversarial Attacks and Defenses Competition [S134] was the first large-scale competitive red-team/blue-team format for adversarial ML, and MITRE ATLAS [S135, S136] — modeled on MITRE ATT&CK, now at v5.1.0 with 16 tactics and 84 techniques — is the standing industry taxonomy for cataloging adversarial-ML attacker behavior.

What is genuinely different about agentic indirect prompt injection, and worth stating precisely rather than asserting: classical adversarial ML attacks a fixed, differentiable decision boundary with a bounded perturbation budget (an epsilon-ball around a fixed input) in a single-shot query. Agentic indirect prompt injection attacks a multi-turn, tool-mediated, natural-language decision process, where the "perturbation" is unbounded text hidden in retrieved data, the attack surface includes which tools the agent can invoke and what state it can change, and success is defined by downstream *actions* (data exfiltration, unauthorized state change) rather than misclassification [S137].

The "attacker adapts to observed defense behavior" loop itself, independent of the LLM domain, is also not new: coverage-guided fuzzing (AFL/libFuzzer [S146, S147]) has mutated inputs against observed program behavior for over 15 years, and game-theoretic adaptive penetration-testing research (ADAPT [S148], co-adaptive attacker-defender learning over attack graphs [S149], finite-state-machine attacker models against moving-target defenses [S150]) has formalized attacker/defender co-adaptation for 5–10 years. AgentGuard's novelty claim, if any, has to rest on the application to the agentic indirect-injection domain specifically — not on the adaptation loop as a general concept, which is well-trodden prior art.

## 2. Taxonomy of current approaches

**By threat model** (the axis BRIEF.md's Vocabulary now organizes around):
- *White-box*: attacker knows the defense's identity/configuration, sometimes has gradient access (GCG [S29]).
- *Black-box, feedback-only*: attacker sees only pass/fail per attempt, no defense identity (PAIR [S30], TAP [S31], AutoDojo [S13]) — this is BRIEF.md's primary threat model.
- *Black-box, no feedback at all*: a single fixed attempt with no observed outcome to adapt on — this describes the four baseline benchmarks' static evaluation mode, and is a meaningfully weaker attacker than "feedback-only," a distinction worth being precise about in any comparison (see `capability_table.md`'s note on "black-box" terminology ambiguity, also flagged in ASSUMPTIONS.md A6).

**By adaptation mechanism**:
- *In-context, live adaptation*: an LLM proposes, observes, and refines within a single evaluation session, no training phase (PAIR, TAP, AutoDojo). This is AgentGuard's presumed design.
- *Offline RL-trained attacker*: the attacker is trained via reinforcement learning ahead of time and then deployed (PISmith [S18], AdvGRPO [S19]). Requires reward-shaping expertise and an offline training phase; PISmith notes naive RL fails against strong defenses due to reward sparsity (most attempts get blocked, yielding little training signal).
- *Skill-evolution against a frozen target*: attack capability improves round-over-round, but the target/defense does not itself respond within the same loop (RedEvoAgent [S20]) — a meaningfully weaker claim than full co-adaptation.

**By target surface**:
- Chatbot/general jailbreak (GCG, PAIR, TAP, "The Attacker Moves Second," HarmBench-scoped AdvGRPO).
- Web/browser agents specifically (MUZZLE [S12]).
- General agentic tool-use (AutoDojo, PI-Hunter, AdapTools [S23], AgentVigil [S25]).
- Computer-use/OS-level agents (SIR [S26]).
- Coding-agent harnesses with file/API access (RedEvoAgent [S20]).

AgentGuard's stated scope (BRIEF.md's year-one exclusions: text-only, staging-only, no custom defense authoring) sits in the general-agentic-tool-use bucket, alongside AutoDojo and PI-Hunter as the closest academic neighbors.

## 3. Enabling technology

See `capability_table.md` for the full table with sourced performance figures. Two points bear directly on BRIEF.md's why-now argument:

1. **Inference cost has dropped enough to make many-round adaptive campaigns routinely affordable.** GPT-4 (2023) priced at $30/$60 per million input/output tokens; GPT-4o (2024) at $5/$15 — roughly a 4x drop within a year [S101]. At the cheap tier, Gemini 2.5 Flash-Lite prices at $0.10/$0.40 [S106]. A back-of-envelope calculation using these verified numbers, not the unverified "300x" aggregator claim [S107], should anchor the whitepaper's cost argument.
2. **The defenses being tested are themselves recent and still maturing.** Classifier-based detection (Meta PromptGuard 2, 2024–2025-era [S33, S34]) and rule-based policy engines (Progent, 2025-04 [S38]) are both young enough that their self-reported robustness numbers have not, in most cases, been independently adversarially stress-tested — which is precisely the service AgentGuard proposes to provide.

## 4. Evaluation methods and benchmarks

The four baseline benchmarks differ meaningfully in scope and are not interchangeable:
- **BIPIA** (2023-12) [S6] — earliest; both black-box and white-box *defense* evaluation settings, but static attacks; explicitly "the first benchmark for indirect prompt injection."
- **InjecAgent** (2024-03) [S3] — 1,054 fixed (user task, injection task) pairs across 17 user tools and 62 attacker tools; a single fixed "enhanced setting" prefix, no per-defense adaptation.
- **AgentDojo** (2024-06) [S1] — 629 security test cases across 97 user tasks in 4 domains (Banking, Slack, Workspace, Travel); introduces the utility/ASR metric pair AgentGuard's own Vocabulary aligns with; the authors explicitly flag adaptive-attack extension as future work.
- **Agent Security Bench** (2024-10) [S5] — broadest reported scope (10 scenarios, 10 agents, 400+ tools, 27 attack/defense methods); highest reported average ASR across combinations is 84.30%, evidence that even static evaluation already finds most defenses porous.

The methodological gap all four share — noted explicitly by AutoDojo's own framing [S13] — is that a fixed distribution of attacks cannot bound how a defense performs against an adversary that iterates specifically against that defense's observed behavior. NIST's CAISI group demonstrated the size of that gap directly: hijack success rose from 11% (generic/static attacks) to 81% (adapted attacks) on an AgentDojo fork, a 7x difference [S27].

## 5. Evidence for and against the core mechanism

**For** (adaptive attackers meaningfully outperform static ones against agent/LLM defenses):
- NIST CAISI: 11% → 81% hijack success, static vs. adapted, same AgentDojo-derived environment [S27].
- AutoDojo: 0% → 28% ASR (64% on "action-open" tasks) against a filter defense that fully blocked static attacks [S13].
- "The Attacker Moves Second": adaptive attacks broke 12 recently published defenses (most to >90% ASR) that reported near-zero vulnerability under static evaluation, corroborated by a 500-participant human red-team competition reaching 100% success against every defense tested [S9].
- Agent Security Bench's own static-evaluation baseline already finds an 84.30% average ASR across combinations [S5] — even before introducing adaptation, published defenses are not robust; adaptation research finds the residual robustness collapses further.

**Against / complicating** (reasons the gap may be narrower, more contested, or already closing than a simple "adaptive wins" headline suggests):
- All of the strongest "for" evidence above is either (a) not agent-tool-use-specific (S9's 12 defenses are drawn from the general LLM-jailbreak/prompt-injection literature, not confirmed to include agent-tool-call defenses specifically) or (b) free and open-source already (NIST CAISI, AutoDojo) — meaning a well-resourced buyer has a credible zero-cost substitute for the *finding*, if not the *service*.
- The agentic adaptation of TAP specifically found GPT-5 far more resistant (~5% ASR, 30% S@N) than the original 2023 chatbot-jailbreak TAP numbers (>80% on GPT-4-class models) [S32] — meaning frontier-model resistance to at least one well-known adaptive technique has measurably improved, and the size of the "adaptive advantage" may already be shrinking against the newest models even as it's demonstrated against older ones.
- PIArena's "dynamic strategy-based attack" [S16] and RedEvoAgent's skill-evolution [S20] both claim adaptation but with weaker or differently-scoped mechanisms (unconfirmed agentic coverage; frozen-target evolution respectively) — not every "adaptive" claim in the literature means the same thing, and BRIEF.md's own matched-budget test design exists precisely to produce a clean, comparable number rather than relying on any one paper's framing.

**Net read**: the core mechanism is well-supported at the general level and increasingly well-supported at the agent-tool-use level specifically, but the size of the effect for AgentGuard's exact three defense types (defensive prompting, classifier-based, rule-based tool-call validation), under feedback-only threat model, at matched budget, has not been directly measured by any source found in this research. That is exactly the gap BRIEF.md's riskiest-assumption test is designed to close — this survey provides strong prior evidence the test is likely to succeed, not proof that it will.

## 6. Risks and open questions

1. **Is the effect agent-tool-use-specific or borrowed from chatbot-jailbreak literature?** The strongest single result (S9) is not confirmed to test agent tool-call defenses. Resolve before citing it as direct agent-domain evidence rather than adjacent-domain evidence.
2. **Does the adaptive advantage hold against the newest frontier models, or is it shrinking?** The GPT-5-vs-TAP result [S32] suggests newer models may already be harder to break adaptively than the literature's headline numbers (largely measured against GPT-4-class models) imply.
3. **Is "feedback-only" the standard term, or should AgentGuard adopt the literature's "black-box" language?** (ASSUMPTIONS.md A6 already flags this — unresolved here.)
4. **Does PIArena's agentic tool-call coverage exist?** Unconfirmed from the abstract; a real gap in this survey's own coverage, flagged for a follow-up full-text read.
5. **What exactly does Adversa AI's "adapts mid-run" mean mechanically?** Unverified vendor marketing language remains the single largest unresolved question standing between this survey and a confident competitive-differentiation claim (see `competitors.md`).

## Recommended next 3

1. **Cite S9, S13, and S27 as the three-source evidentiary core of `tech/whitepaper.md`'s mechanism argument** — they are the best-supported, most-independently-corroborated findings in this survey.
2. **Explicitly caveat any adaptive-vs-static claim in downstream artifacts with the agent-tool-use-specificity question (§6.1)** until AgentGuard's own matched-budget test produces a directly agent-domain number.
3. **Resolve the "feedback-only" vs. "black-box" terminology question (§6.3) before `tech/whitepaper.md` is drafted** — inventing new vocabulary where the field already has a term invites exactly the "ignorant of prior art" read ASSUMPTIONS.md A6 warns against.
