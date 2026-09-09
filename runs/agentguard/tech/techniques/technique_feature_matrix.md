# Technique × feature matrix

**What this is**: every technique named in `tech/techniques/wave1.md` and `wave2.md`, mapped to the flagship mechanism features from `BRIEF.md`'s Mechanism section (`product/features_flagship.md` does not exist yet at time of writing — this matrix uses the feature names BRIEF.md's Mechanism paragraph names directly, per the fallback the owning skill's contract allows).

**Why it exists**: `skills/startup-tech/SKILL.md`'s own red-flag list names "a matrix where every technique powers every feature" as a specific failure mode. This document exists to force the opposite — an honest accounting of which techniques are actually load-bearing for a shipped feature, which are evidentiary/lineage-only, and which features are powered by AgentGuard's own engineering rather than any adopted technique.

**How to read it**: the two "flagged" sections at the bottom are the point of the document, not an afterthought — a skeptic should read those before the matrix itself, since they are where the honest findings live.

**Depends on / feeds**: built from `tech/techniques/wave1.md`, `wave2.md`, and `BRIEF.md`'s Mechanism paragraph. Feeds `product/features_flagship.md` once it exists (this matrix should be re-validated against it, not silently left stale).

---

## Feature legend (from `BRIEF.md` Mechanism)

| Code | Feature |
|---|---|
| F1 | Feedback-only adaptive campaign engine (core round loop) |
| F2 | White-box upper-bound comparison mode |
| F3 | Defensive-prompting defense harness |
| F4 | Classifier-based detection defense harness |
| F5 | Rule-based tool-call validation defense harness |
| F6 | Baseline/none defense harness |
| F7 | Matched-budget cross-defense comparison report (aggregator) |
| F8 | Utility-under-attack measurement |
| F9 | Adaptation curve / defense fingerprint logging |
| F10 | Continuous, reproducible re-run (standing campaign corpus) |

## Matrix

`X` = directly powers/implements. `i` = informs the design (evidence or reference architecture), not directly implemented. Blank = no relationship claimed.

| Technique | F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | F10 |
|---|---|---|---|---|---|---|---|---|---|---|
| AutoDojo optimizer [S13] | **X** | | | | | | | | | |
| AgentDojo environment + utility metric [S1] | X | | | | | | | **X** | | |
| PAIR [S30] | i | | | | | | | | | |
| TAP [S31] | i | **X** | | | | | | | | |
| GCG [S29] | | X | | | | | | | | |
| Agentic GCG/TAP adaptation study [S32] | | X | | | | | | | | |
| PyRIT orchestrator pattern [S59] | | | | | | | X | | X | |
| Defensive prompting (pattern) [S1,S5,S6] | | | **X** | | | | | | | |
| Meta PromptGuard 2 [S33,S34] | | | | **X** | | | | | | |
| LlamaFirewall [S35] | | | | i | | | | | | |
| PromptShield [S36] | | | | i | | | | | | |
| CourtGuard [S37] | | | | i | | | | | | |
| Progent [S38] | | | | | **X** | | | | | |
| MiniScope [S39] | | | | | i | | | | | |
| Policy-as-Prompt [S40] | | | | | i | | | | | |
| Prompt Flow Integrity [S41] | | | | | i | | | | | |
| MUZZLE [S12] | i | | | | | | | | | |
| PI-Hunter [S15] | i | | | | | | | | | |
| "Adaptive Attacks Break Defenses" [S11] | i | | | | | | | | | |
| PIArena [S16] | i | | | | | | | | | |
| AdapTools [S23] | i | | | | | | | | | |
| PISmith [S18] | i | | | | | | | | | |
| AdvGRPO [S19] | i | | | | | | | | | |
| Async Control [S22] | | | | | | | i | | | |
| RedEvoAgent [S20] | i | | | | | | | | | |
| EVA [S24] | i | | | | | | | | | |
| AgentVigil [S25] | i | | | | | | | | | |
| SIR [S26] | i | | | | | | | | | |
| AutoRedTeamer [S21] | i | | | | | | i | | | |
| "The Attacker Moves Second" [S9] | i | | | | | | | | | |
| NIST CAISI/UK AISI exercise [S27,S28] | i | | | | | | | | | |
| MITRE ATLAS taxonomy [S135,S136] | | | | | | | | | i | |
| Classical foundations (Szegedy [S132], FGSM [S133], NIPS'17 [S134]) | | | | | | | | | | |
| Baseline benchmarks (BIPIA [S6], InjecAgent [S3], ASB [S5]) | | | | | | | | | | |

## Flagged: orphan techniques (power no shipped feature directly)

These are named, cited, and genuinely relevant to the field AgentGuard operates in — but honestly, none of them is implemented by AgentGuard's own code, only referenced as evidence or intellectual lineage:

- **Classical foundations** (Szegedy et al. [S132], FGSM [S133], NIPS 2017 competition [S134]) — establish that adversarial ML predates LLMs; zero direct implementation relationship to any feature. Kept in `wave1.md` for scientific grounding (`references/quality-bar.md` property 1's "evidence behind the mechanism" bar), not because they power a feature.
- **Baseline benchmarks** (BIPIA [S6], InjecAgent [S3], Agent Security Bench [S5]) — these are ground truth AgentGuard evaluates *against* (InjecAgent specifically as the static-arm comparator in `BRIEF.md`'s riskiest-assumption test), not technology AgentGuard's product features run on.
- **The nine `i`-only Wave 2 agentic/co-adaptive techniques** (MUZZLE, PI-Hunter, "Adaptive Attacks Break Defenses," PIArena, AdapTools, PISmith, AdvGRPO, RedEvoAgent, EVA, AgentVigil, SIR, AutoRedTeamer) — every one of these is prior art or an adjacent research direction that informs how F1 might evolve, but **none is adopted as the implemented attacker** — only AutoDojo [S13] holds that role, per `ASSUMPTIONS.md` A9. Listing this many orphans in Wave 2 is a deliberate honesty signal, not an oversight: it demonstrates AgentGuard's team read the field broadly and chose not to over-claim breadth it doesn't implement.
- **"The Attacker Moves Second" [S9] and the NIST CAISI exercise [S27, S28]** — the two strongest evidentiary sources for the whitepaper's core thesis, and neither is a technique AgentGuard runs; both are findings AgentGuard's own riskiest-assumption test exists to re-verify directly rather than cite as a substitute for AgentGuard's own measurement.

## Flagged: unsupported features (no technique from the literature powers them)

- **F6 — Baseline/none defense harness**: no technique powers this by design. It is the trivial control condition (the target agent with no defense active) that every comparison needs as a reference point — there is no "technique" for absence of a defense, and this is stated here so the blank row isn't mistaken for a gap.
- **F10 — Continuous, reproducible re-run (standing campaign corpus)**: no attack or defense technique from either wave powers this. It is powered entirely by AgentGuard's own scheduling/orchestration engineering (`tech/deep_dives.md` items 7–8, `tech/architecture/D08.md` and `D09.md`) — the aggregation and repeatability layer `strategy/positioning.md` names as AgentGuard's one genuine contribution. This is the single most important row in this matrix: the feature with no adopted-technique support is the feature the whitepaper's entire argument rests on, and that is not a coincidence — it is the honest shape of what "the comparison, not the attacker" actually means at the technique level.

## Recommended next 3

1. **Re-run this matrix against `product/features_flagship.md` the moment it exists**, since it was built from `BRIEF.md`'s Mechanism paragraph as an explicit fallback — a stale matrix that doesn't reflect the real flagship feature list is worse than no matrix.
2. **Treat F10's zero-technique row as the one line to quote in any pitch material that risks the "wrapper" objection** — it is the clearest, most checkable evidence that AgentGuard's differentiation is engineering/protocol work, not a borrowed algorithm, stated in the driest possible form (a matrix cell, not a slogan).
3. **Prune the classifier and rule-based "reference, not integrated" (`i`) rows (LlamaFirewall, PromptShield, CourtGuard, MiniScope, Policy-as-Prompt, Prompt Flow Integrity) to a single default choice per harness before `product/PRD.md` is written**, so the matrix's honest "reference only" flags don't quietly become five unbuilt integrations by default.
