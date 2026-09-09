# Wave 1 — established techniques

**What this is**: the established, already-published domain-science techniques AgentGuard's mechanism is built from or evaluates against — foundational adversarial-ML methods, the black-box adaptive-attack family AgentGuard adopts, and the four named defense types under test.

**Why it exists**: `references/quality-bar.md` property 1 bans adjective-only claims; this document is where every "adaptive," "classifier-based," or "rule-based" label in `BRIEF.md` gets tied to a real, named, cited technique. The failure this document prevents: a technique list padded with duplicates or vague restatements to hit a round number, which `skills/startup-tech/SKILL.md`'s own red-flag list calls out directly.

**How to read it**: techniques are clustered by sub-discipline with counts; the "Adopted by AgentGuard" column is the one a skeptic should check first — most of this wave is evaluated-against (a defense AgentGuard tests) or foundational-to (a method AgentGuard's own attacker descends from), not directly run by AgentGuard's own code, and that distinction is stated explicitly per row rather than blurred.

**Depends on / feeds**: built from `research/sources.md` and `research/survey.md` §§1–4. Feeds `tech/techniques/technique_feature_matrix.md` and `tech/techniques/decision_tree.md`.

---

## Cluster A — Classical adversarial-ML foundations (4 techniques)

| Technique | One-line mechanism | Evidence anchor | Adopted by AgentGuard? |
|---|---|---|---|
| Imperceptible-perturbation adversarial examples | Small, bounded input perturbations fool a fixed classifier at inference time | Szegedy et al. 2014 [S132] | No — intellectual lineage only; agentic IPI's "perturbation" is unbounded natural-language text, not an epsilon-ball (`research/survey.md` §1) |
| Fast Gradient Sign Method (FGSM) | Single-step gradient-based perturbation, established both the canonical attack and the adversarial-training defense pattern | Goodfellow et al. 2015 [S133] | No — lineage only |
| Competitive red/blue adversarial-ML format | Large-scale competitive attack/defense evaluation as a methodological pattern | NIPS 2017 Adversarial Attacks and Defenses Competition [S134] | Conceptually — AgentGuard's cross-defense comparison is a structured descendant of this competitive-evaluation pattern, not a direct reuse |
| MITRE ATLAS taxonomy | Standing industry taxonomy (16 tactics, 84 techniques, 56 sub-techniques, 32 mitigations) for cataloging adversarial-ML attacker behavior, modeled on ATT&CK | ATLAS v5.1.0 [S135, S136] | Reference framework only — a candidate taxonomy to map AgentGuard's own attack/defense catalog onto, not yet adopted (`capability_table.md` gap note) |

## Cluster B — Foundational black-box/white-box jailbreak methods, chatbot-level ancestry (4 techniques)

| Technique | One-line mechanism | Evidence anchor | Adopted by AgentGuard? |
|---|---|---|---|
| GCG (gradient-based universal suffix search) | White-box, gradient access, finds a transferable adversarial suffix | Zou et al. 2023 [S29] | Yes — as one white-box upper-bound attack strategy (`tech/deep_dives.md` item 2), adapted to agentic settings per [S32] |
| PAIR | Black-box, LLM-vs-LLM iterative refinement via chat history, typically <20 queries to converge | Chao et al. 2023 [S30] | Indirectly — establishes the in-context, live-adaptation pattern AutoDojo (Cluster D) and AgentGuard's own loop follow |
| TAP (Tree of Attacks with Pruning) | Black-box tree-search multi-round refinement with pruning, >80% jailbreak success on GPT-4-class chatbot models originally | Mehrotra et al. 2023 [S31] | Yes — as the preferred white-box-upper-bound strategy under realistic compute budgets, per its agentic adaptation [S32] (`tech/deep_dives.md` item 2) |
| GCG/TAP agentic adaptation study | Adapts both GCG and TAP into the AgentDojo agentic setting; finds TAP substantially outperforms GCG under realistic compute; GPT-5 shows only ~5% ASR against TAP | [S32] | Yes — directly informs item 2's design choice and its honest failure-mode caveat |

## Cluster C — Baseline evaluation benchmarks (the ground truth AgentGuard tests against) (4 techniques)

| Technique | One-line mechanism | Evidence anchor | Adopted by AgentGuard? |
|---|---|---|---|
| BIPIA | Static attacks, both black-box and white-box *defense* evaluation settings; first IPI benchmark | [S6] | No — baseline/ground-truth benchmark, not a component AgentGuard runs |
| InjecAgent | 1,054 fixed (user task, injection task) pairs, one fixed "enhanced setting" prefix, no per-defense adaptation | [S3] | No — used as the static-arm attack source in `BRIEF.md`'s riskiest-assumption test specifically, otherwise baseline/ground-truth only |
| AgentDojo (environment + shipped distribution) | Extensible dynamic environment; 629 security test cases, 97 user tasks, 4 domains; introduces the utility/ASR metric pair; originally-shipped attack distribution is fixed, framework is not | [S1] | Yes — the environment AgentGuard's own harness is built inside/adapted from, and the source of the utility metric definition (`tech/deep_dives.md` item 3) |
| Agent Security Bench (ASB) | Broadest reported scope (10 scenarios, 10 agents, 400+ tools, 27 attack/defense methods); 84.30% highest average ASR across combinations | [S5] | No — baseline/ground-truth; its high average-ASR finding is cited as evidence that even static evaluation already finds most defenses porous (`tech/whitepaper.md` §1, friction 1) |

## Cluster D — The adopted adaptive attacker (2 techniques)

| Technique | One-line mechanism | Evidence anchor | Adopted by AgentGuard? |
|---|---|---|---|
| AutoDojo's black-box iterative optimizer | LLM-driven iterative black-box attack optimization against one deployed defense, run inside AgentDojo; recovers 28% ASR (64% on "action-open" tasks) against a defense that drove static ASR to 0% | [S13, S14] | **Yes — the primary adopted attacker configuration** (`tech/deep_dives.md` item 1). This is the one technique this whole pack is explicit is adopted, not invented (`ASSUMPTIONS.md` A9) |
| PyRIT orchestrator pattern | Orchestrator-managed dynamic multi-turn attack strategies (e.g., Crescendo-style escalation), released by Microsoft AI Red Team | [S59] | Yes — for round scheduling, retry/backoff, and logging plumbing only (`tech/deep_dives.md` item 8), explicitly not for its attack strategies |

## Cluster E — Named defenses under test (7 techniques)

| Technique | One-line mechanism | Evidence anchor | Adopted by AgentGuard? |
|---|---|---|---|
| Defensive prompting | System-prompt instruction pattern warning the model against injected instructions; no dedicated product, evaluated as a baseline inside AgentDojo/ASB/BIPIA | [S1, S5, S6] | Tested, not adopted as an attacker technique — AgentGuard's first defense harness (`tech/deep_dives.md` item 4) |
| Meta PromptGuard 2 (86M/22M) | Open classifier for injection/jailbreak detection; 97.5% recall at 1% FPR (86M), 88.7% (22M), self-reported, static evaluation | [S33, S34] | Tested — reference classifier for AgentGuard's classifier-based harness (`tech/deep_dives.md` item 5) |
| LlamaFirewall | Three-layer guardrail (PromptGuard 2 + chain-of-thought alignment auditor + static-analysis code shield), stated in production use at Meta | [S35] | Reference architecture for classifier-harness design, not directly wrapped |
| PromptShield | Deployability/low-false-positive-rate-focused classifier detector | [S36] | Candidate alternative classifier for the harness, not the default |
| CourtGuard | Local, multiagent prompt-injection classifier | [S37] | Candidate alternative classifier, not the default |
| Progent | Programmable privilege-control policy language, LLM-assisted policy generation, gates tool calls at execution time; self-reports ASR reduced to 0% with preserved utility | [S38] | Tested — reference policy engine for AgentGuard's rule-based harness (`tech/deep_dives.md` item 6) |
| MiniScope / Policy-as-Prompt / Prompt Flow Integrity | Least-privilege authorization frameworks and systems-level data/control-flow isolation for tool-calling agents | [S39, S40, S41] | Reference architectures for the rule-based harness's design space, not directly wrapped in year one |

**Cluster totals**: 4 + 4 + 4 + 2 + 7 = **21 techniques**, genuinely sourced from `research/sources.md`. This wave stops at 21, not 50 — the field's established, citable techniques directly relevant to AgentGuard's mechanism (foundational adversarial ML, chatbot-jailbreak ancestry, the four baseline benchmarks, the one adopted attacker, and the named defense types) are exhausted at this count; padding further would mean listing techniques with no real bearing on AgentGuard's design, which `skills/startup-tech/SKILL.md`'s own red-flag list warns against directly.

## Recommended next 3

1. **Confirm Cluster E's classifier alternatives (LlamaFirewall, PromptShield, CourtGuard) against real deployments before committing to PromptGuard 2 as the sole reference classifier** — the harness should be pluggable, not hard-coded to one model, since customers deploy their own classifier choice in practice.
2. **Map Cluster E's rule-based alternatives (MiniScope, Policy-as-Prompt, Prompt Flow Integrity) against Progent specifically to confirm Progent remains the best-documented reference** before building the rule-based harness — `capability_table.md` already flags Progent's numbers as self-reported and unverified.
3. **Revisit MITRE ATLAS (Cluster A) as an actual taxonomy mapping, not just a reference**, once AgentGuard's own attack/defense catalog stabilizes — an ATLAS-mapped catalog would strengthen `tech/whitepaper.md`'s credibility with enterprise buyers already familiar with ATT&CK-style frameworks (relevant to Dr. Elena Osei's persona, `strategy/personas.md`).
