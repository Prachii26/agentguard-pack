# Wave 2 — advanced, theory-grounded techniques

**What this is**: the 2025–2026 wave of adaptive and co-adaptive red-teaming research specifically — the academic frontier AgentGuard's comparison protocol sits alongside, treated throughout as prior art or adjacent research, never as a technique AgentGuard claims to have invented or improved on.

**Why it exists**: `ASSUMPTIONS.md` A9 and `strategy/positioning.md` are explicit that AgentGuard's differentiation is the comparison protocol, not attack technique — this document exists to show the full field of adaptive-attack research AgentGuard is deliberately *not* trying to out-innovate, so the comparison-protocol claim reads as informed restraint rather than ignorance of the literature.

**How to read it**: the "Distinguishing note" column is the load-bearing one — most entries here look similar to AgentGuard's own loop at a glance, and the note states precisely how each differs (scope, target-freezing, training regime) so a skeptic can't collapse AgentGuard into "just another one of these."

**Depends on / feeds**: built from `research/sources.md` and `research/survey.md` §2 (taxonomy by adaptation mechanism and target surface). Feeds `tech/techniques/technique_feature_matrix.md` and `tech/techniques/decision_tree.md`.

---

## Cluster F — Agentic/tool-use adaptive red-teaming, closest neighbors (5 techniques)

| Technique | One-line mechanism | Evidence anchor | Distinguishing note |
|---|---|---|---|
| MUZZLE | Fully automated framework iteratively refining injection tactics based on observed browser-agent defense behavior (same-origin policy, site isolation, injection detectors) | [S12] | Scoped to web/browser agents specifically, not general tool-use — AgentGuard's target surface is broader but shallower (text-based IPI across email/documents/webpages/calendar, not browser-security-specific) |
| PI-Hunter | Agentic auditing framework, iteratively evolves test cases through feedback-driven exploration to surface latent injection vulnerabilities | [S15] | Framed as vulnerability discovery/localization, not a standing cross-defense comparison protocol — closer to a single-run audit tool than a repeatable service |
| "Adaptive Attacks Break Defenses Against IPI on LLM Agents" | Tests three defense categories (detection-based, sanitization, reasoning-modification) against LLM agents specifically, with a per-defense custom adaptive attack | [S11] | Closest academic precedent to AgentGuard's own "one attacker, multiple defense types" structure — but reports per-defense adaptive success, not a matched-budget, utility-paired, side-by-side comparison |
| PIArena | Unified benchmark/attack/defense/evaluator platform; "dynamic strategy-based attack" adaptively optimizes injected prompts based on defense feedback | [S16] | Domain coverage confirmed for QA/RAG/code-gen; agentic tool-call coverage unconfirmed from the abstract — flagged as an open question in `research/survey.md` §6.4, not resolved here |
| AdapTools | Uses commercial LLMs to score exploitability and adaptively construct injected content targeting tool-use trajectories | [S23] | Attack-construction technique only — no comparison or utility-reporting layer |

## Cluster G — Reinforcement-learning-trained and co-adaptive attackers (3 techniques)

| Technique | One-line mechanism | Evidence anchor | Distinguishing note |
|---|---|---|---|
| PISmith | RL-trained (GRPO-family) attacker in a black-box query-only setting; notes naive RL fails against strong defenses due to reward sparsity | [S18] | Offline RL-trained rather than in-context live adaptation — a meaningfully different adaptation mechanism from AgentGuard's per-campaign in-context loop; the reward-sparsity finding directly informs `tech/deep_dives.md` item 1's failure-mode note |
| AdvGRPO | Co-trained attacker/defender via RL with a curriculum from single-turn to closed-loop multi-turn attacks | [S19] | General chatbot/jailbreak scope (HarmBench), not agent tool-use IPI specifically — adjacent-domain, not directly agentic |
| Async Control | Formal alternating-round red/blue game: blue submits a monitor update, red develops an attack optimized against it, repeat | [S22] | Closest structural match anywhere in this research to a round-over-round red/blue evaluation loop — but scoped to control/monitoring measures generally, not indirect prompt injection specifically; the alternating-round *game structure* is conceptually adjacent to AgentGuard's matched-budget design even though the domain differs |

## Cluster H — Target-surface variants and skill-evolution approaches (5 techniques)

| Technique | One-line mechanism | Evidence anchor | Distinguishing note |
|---|---|---|---|
| RedEvoAgent | Experience-driven skill evolution against real tool-use harnesses (Claude Code/Codex-style environments); attack capability improves round-over-round | [S20] | Targets a **frozen** target agent — the defense does not itself respond within the loop, a meaningfully weaker claim than full co-adaptation; explicitly named in `research/survey.md` §2 as a weaker adaptation category than AgentGuard's design |
| EVA | Closed-loop optimization red-teaming for GUI agents via evolving adversarial cues | [S24] | GUI-agent target surface, not general tool-use/IPI |
| AgentVigil | Generic black-box iterative-fuzzing red-teaming for indirect prompt injection against LLM agents | [S25] | Fuzzing-based exploration strategy, general agentic scope — a candidate alternative attack-generation strategy, not adopted as primary (AutoDojo remains primary per `ASSUMPTIONS.md` A9) |
| SIR | Self-improving red-teaming for computer-use agents, adaptive IPI at the OS/computer-use level | [S26] | OS/computer-use target surface, out of AgentGuard's year-one scope (text-based IPI in email/documents/webpages/calendar only) |
| AutoRedTeamer | Dual-agent (evaluator + strategy proposer) "lifelong," continuously-updating red-team framing | [S21] | Full text not confirmed in this research pass, flagged for follow-up read — the "lifelong/continuous" framing is conceptually close to AgentGuard's edge-high continuous-run tier, but the paper's actual mechanism is not independently verified here |

## Cluster I — Cross-lab and government-scale validation of the core thesis (3 techniques/findings)

| Technique/finding | One-line mechanism | Evidence anchor | Distinguishing note |
|---|---|---|---|
| "The Attacker Moves Second" | Cross-lab (OpenAI/Anthropic/Google DeepMind) methodology; adaptive attacks broke 12 published defenses, most to >90% ASR; corroborated by a 500-participant human red-team competition reaching 100% success against every tested defense | [S9, S10] | The single strongest validation of the core "adaptive beats static" thesis found in this research — but not confirmed agent-tool-use-specific (drawn from general LLM-jailbreak/prompt-injection literature); `research/survey.md` §6.1 flags this explicitly as an open question, not resolved by this wave |
| NIST CAISI / UK AISI human red-teaming exercise | Human red-teamers crafted target-optimized attacks against one model on an AgentDojo-derived environment, compared to generic/static baseline; 11%→81% hijack success (7x) | [S27, S28] | Human-executed, not automated — a single exercise, not a repeatable protocol; evidence for the thesis, explicitly not a competing product (`ASSUMPTIONS.md` A9) |
| Agentic GCG/TAP adaptation study | Adapts GCG and TAP into AgentDojo's agentic setting; GPT-5 shows only ~5% ASR/30% S@N against TAP, far below original chatbot-jailbreak numbers | [S32] | The one finding in this wave that argues the adaptive advantage may be *shrinking* against the newest frontier models — `tech/whitepaper.md` §4 cites this as an honest limit, not omitted |

**Cluster totals**: 5 + 3 + 5 + 3 = **16 techniques/findings**, genuinely sourced. Combined with Wave 1's 21, this pack documents **37 real, cited techniques** across both waves — stopped short of the 50-per-wave ceiling `skills/startup-tech/SKILL.md` allows, because the field of directly relevant, independently sourced adaptive-attack and agent-defense research surfaced in `research/sources.md` is genuinely exhausted at this count, not because of a time constraint. Padding further would mean re-listing Wave 1 entries under new headings or including techniques with no real bearing on AgentGuard's mechanism — both are exactly what `skills/startup-tech/SKILL.md`'s red-flag list warns against.

**Wave 3 — skipped, stated honestly**: this pack does not include a `wave3.md`. A genuine frontier/cross-domain wave (per the skill's own definition — "frontier AI-native and cross-domain imports") would need to draw on techniques meaningfully distinct from Waves 1–2's adversarial-ML and agentic-redteaming material — e.g., techniques imported from an unrelated domain (game theory, control theory, biosecurity red-teaming) with a real, sourced connection to AgentGuard's mechanism. `research/sources.md` does contain adjacent material (Async Control's game-theoretic framing, Cluster G above, is the closest candidate) but not enough independently-sourced cross-domain material to justify a third wave without padding. Per `skills/startup-tech/SKILL.md`'s own instruction ("wave3.md is optional... include it only if you have genuine frontier/cross-domain material, otherwise skip and say so"), this wave is skipped rather than padded.

## Recommended next 3

1. **Re-verify AutoRedTeamer's [S21] actual mechanism against its full text** — it is the one entry in this wave flagged as unconfirmed from an abstract-only read, and its "lifelong/continuous" framing is close enough to AgentGuard's edge-high tier that a wrong reading here would be an embarrassing miss in front of a technical reviewer.
2. **Track the agentic GCG/TAP adaptation study's finding [S32]** (shrinking adaptive advantage against frontier models) as a standing risk in `tech/architecture/D08.md`'s self-eval loop, not just a footnote here — if the effect keeps shrinking, it changes §2 of `tech/whitepaper.md`'s confidence bands materially.
3. **Resolve PIArena's agentic tool-call coverage [S16]** before citing it as a direct competitor-technique comparison anywhere downstream — `research/survey.md` §6.4 already flags this as an open research-coverage gap, not a settled fact.
