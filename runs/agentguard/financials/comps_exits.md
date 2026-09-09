# Comparables and exit landscape

**What this is**: comparable companies (sourced), realistic acquirer profiles, IPO-path conditions, and the sober case for standalone viability.

**Why it exists**: `research/landscape.md` §5 already documented that the AI-agent-security category has consolidated five named vendors into incumbents within ~18 months of raising — this document turns that observation into the actual comps and exit analysis a financial reader needs.

**How to read it**: the comps table is not a list of winners only — it includes the acquisition prices where disclosed and the pattern (fast absorption, not independent scaling) plainly, per this skill's own red flag against comps sections that list only winners.

**Depends on / feeds**: built entirely from `research/sources.md` and `research/competitors.md` — no new figures invented here. Feeds `narrative/vc_memo.md`'s "why this can win" section.

---

## Comparable companies (sourced)

| Company | Stage/outcome | Amount | Source |
|---|---|---|---|
| Robust Intelligence | Acquired by Cisco | ~$400M (reported elsewhere; undisclosed on the primary press release — `audit/CITATIONS.md`) | `research/sources.md` S48 |
| Prompt Security | Acquired by SentinelOne | ~$250M (estimated) | S66 |
| CalypsoAI | Acquired by F5 | $180M | S53 |
| Guardrails AI | Acquired by Harvey | Undisclosed | S67 |
| Promptfoo | Acquired by OpenAI | Undisclosed ($23M+ raised pre-acquisition) | S56, S57 |
| Protect AI | Acquired by Palo Alto Networks | Reportedly $500M+ | S127 |
| HiddenLayer | Independent, Series B | $156M total raised | S46, S47 |
| Straiker | Independent, Series A | $85M total raised, $64M Series A | S63 |
| Mindgard | Independent, Series A | $30M | S44 |
| Adversa AI | Independent, funding not public | Not public | S50-S52 |
| SplxAI | Independent, seed | $7M | S62 |
| Giskard | Independent, small | ~$2-2.7M | S54 |
| Repello AI | Independent, seed | $1.2M | S64 |

## What the market rewarded and punished

**Rewarded**: fast, credible technical demonstration (Robust Intelligence's Tree-of-Attacks-with-Pruning red-teaming, S49) combined with enterprise distribution fit — every disclosed acquisition above was by a company (Cisco, SentinelOne, F5, Palo Alto Networks) with existing enterprise security distribution the target lacked. **Punished (implicitly)**: none of the independent, still-standalone companies in this list (HiddenLayer, Straiker, Mindgard, Adversa AI) have disclosed revenue multiples or exit outcomes yet — the category is too young for a "punished" comp, which is itself informative: there is no visible failure case in this specific niche yet, only fast consolidation of the ones that got real technical/market traction.

## The dominant pattern: fast absorption, not independent scaling

Five of the most relevant named companies in this exact space were acquired within roughly 18 months of raising meaningful funding (`research/landscape.md` §5). This is the single most important comp-set fact for AgentGuard's own exit thinking: **the modal outcome in this category so far is acquisition by a platform incumbent, not an independent path to IPO scale.**

## Realistic acquirer profiles and why each would pay

| Acquirer profile | Why they'd pay | Precedent |
|---|---|---|
| A cloud/platform incumbent (Microsoft, Google, AWS) | To close the exact gap `strategy/positioning.md` identifies — Microsoft already owns the attacker half of the mechanism via its AI Red Teaming Agent; acquiring AgentGuard's comparison-protocol methodology would be cheaper than building cross-defense comparison in-house and validating it publicly | Robust Intelligence→Cisco, Protect AI→Palo Alto Networks, Promptfoo→OpenAI |
| An established security vendor without agent-native coverage | To buy agent-tool-use-injection credibility they lack — per `research/competitors.md`, HiddenLayer was independently noted to have "limited agentic/MCP coverage" relative to dedicated agent-security vendors | Cisco/Robust Intelligence (same pattern, prior wave) |
| A compliance/GRC platform | To add AI-agent-specific adversarial evidence generation to an existing audit/compliance product line, per `strategy/petal_diagram.md`'s Petal 5 | No direct precedent in this exact niche yet — the newest, least-proven acquirer thesis |

## IPO-path conditions

Given the comp set's pattern, an independent path to IPO scale would require AgentGuard to be a clear exception to the category's own consolidation trend — specifically: (1) the comparison-corpus moat hypothesis (`BRIEF.md` Moat) proving out with real defensibility, not just data volume, and (2) reaching `financials/revenue_build.md`'s Stage 3 ($50-100M ARR) without being acquired first, which no comparable company in this exact space has yet done. **This is a low-probability path per the comp set, stated honestly, not talked around.**

## Why this can be a standalone generational company — after the sober comps, not instead of them

The comps above argue for acquisition, not independence, as the modal outcome. The honest case for standalone viability rests on one thing the comps don't have: AgentGuard's wedge is a **published, reproducible methodology** (the comparison protocol), not a proprietary attack engine a platform incumbent could replicate as a feature update alone — replicating the *credibility* of a standing, cited, third-party-checkable comparison standard is harder than replicating the underlying attack technique, which is already open-source (AutoDojo). If AgentGuard becomes the reference standard the way a benchmark paper becomes the reference standard — cited, trusted, hard to displace once entrenched — that is a path an acquisition-hungry incumbent cannot simply out-build. This is a real but unproven argument, resting entirely on `BRIEF.md`'s Moat hypothesis actually holding, which `ASSUMPTIONS.md` A2 already states is unconfirmed.

## Recommended next 3

1. **Do not present the comps table as evidence that AgentGuard will follow the same path** — it is evidence about the category's dynamics, not a prediction about this specific company.
2. **Track whether any comp company discloses a revenue multiple or a failed/down-round outcome** — this comp set currently has no visible failure case, which is a data gap, not proof the category is safe.
3. **Revisit the standalone-viability argument only after the comparison-corpus hypothesis has real data behind it** — until then, the acquisition-path comps are the more defensible read of this company's likely outcome.
