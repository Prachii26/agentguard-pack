# Risk matrix

**What this is**: the top risks across technology, market, regulatory, competition, cost, retention, key-person, and platform categories, with honest residual levels after mitigation.

**Why it exists**: `strategy/market_type.md` and `strategy/positioning.md` already named the dominant competitive risk in prose; this document is where every category of risk gets the same treatment in one place, so no risk hides behind being "mentioned once" in a different artifact.

**How to read it**: the Residual column is the point — a matrix where everything mitigates to "low" is fiction, per this skill's own red flag list.

**Depends on / feeds**: consolidates risks named across `BRIEF.md`, `strategy/market_type.md`, `strategy/positioning.md`, `strategy/sales_roadmap.md`, `validation/riskiest_assumptions.md`. Feeds `financials/comps_exits.md` and `narrative/vc_memo.md`'s honest-risks section.

---

| Risk | Category | Likelihood | Impact | Leading indicator | Mitigation | Residual |
|---|---|---|---|---|---|---|
| Matched-budget adaptive-vs-static ASR gap is null or negative | Technology | Medium | Fatal (`BRIEF.md` Riskiest assumption states this kills the company if false) | The two-week/$1k test result itself | None available before the test runs — this is precisely what the test exists to find out | **High** — cannot be mitigated in advance, only tested |
| Microsoft ships a comparable cross-defense, utility-paired report as a Foundry feature | Competition/Platform | Medium-High | High — collapses the open quadrant `strategy/positioning.md` identifies | Azure Foundry release notes (monitored per `strategy/positioning.md` Recommended next 3) | Speed and focus (a small team can iterate faster than a feature competes for platform roadmap priority) — a time-limited advantage, not a durable one | **High** |
| Adversa AI publishes an aggregate cross-defense benchmark as a marketing move | Competition | Medium | High — same quadrant-collapse effect | Adversa AI's public material (monitored per `strategy/positioning.md`) | None structural — `strategy/positioning.md` states plainly nothing prevents this | **High** |
| No moat exists if the comparison-corpus hypothesis doesn't compound | Technology/Market | Medium-High | Medium — the business can still function as a service without a moat, just without pricing power (`financials/pricing.md`) | Whether campaign volume produces any measurable defense-fingerprint value after real usage exists | None yet — `BRIEF.md`'s Moat section already discloses this as unproven, not mitigated | **High** |
| Inference cost rises materially (model pricing reverses trend) | Cost | Low | Low — `financials/unit_economics.md` shows margin has substantial headroom (~92-99.5%) even at frontier-tier pricing | Model API pricing pages (S101-S106) | Multiple model providers/tiers available; not locked to one vendor (`tech/not_vaporware.md` §1) | **Low** |
| Progent's or PromptGuard's self-reported defense claims don't hold under AgentGuard's own adaptive testing | Technology | High (per `research/sources.md` S9's general finding that adaptive attacks break published defenses) | Low — this is not a risk to AgentGuard, it is the product working as intended; the risk is reputational only if AgentGuard's own harness is buggy, not if the defense fails | Reproducing AutoDojo's published number as a sanity check (`tech/not_vaporware.md` §2.3) | Harness validated against a known published result before trusting novel-target output | **Low** |
| Enterprise procurement/vendor-risk review blocks edge-high sales | Market | High | Medium — `strategy/market_sizing.md`'s SOM is already sized off the beachhead, not edge-high, so this doesn't threaten Stage 1 revenue | Number of edge-high deals stalled at vendor-risk review (`strategy/sales_roadmap.md`) | None available to a pre-traction, 4-person team — `strategy/sales_roadmap.md` already recommends weighting edge-high revenue at zero in year one | **High for edge-high specifically, Low for overall Stage 1 plan** (because Stage 1 doesn't depend on edge-high) |
| Regulatory requirement for AI red-teaming (EU AI Act, ISO 42001) doesn't materialize as a buying trigger as expected | Regulatory | Medium | Medium — `research/sources.md` S109/S113/S114 document the requirement exists on paper; whether it drives actual purchasing decisions is untested | Whether discovery interviews (`validation/discovery_guide.md`) surface compliance as an actual purchase trigger vs. a nice-to-have | None — this is a market hypothesis, not something the product controls | **Medium** |
| Post-capstone continuity — team disbands or deprioritizes after CMPE 295B ends | Key-person | Medium-High | High — `strategy/gtm.md` already discloses no service guarantee beyond the program's end | Whether the team decides to continue past the capstone (an explicit, undecided fork per `strategy/gtm.md`) | Disclosed to any paying customer upfront (`strategy/gtm.md`) — honesty, not elimination, of the risk | **High** |

## Recommended next 3

1. **Track the two platform/competition risks (Microsoft, Adversa AI) as the highest-priority residual risks**, not the technology risk — the technology risk (null ASR gap) is at least testable cheaply; the competition risks are not something AgentGuard can test or control, only monitor.
2. **Do not let the "Low" residual on inference cost create false confidence about overall margin safety** — margin is dominated by the $2,500 price point holding, not by inference cost, per `financials/unit_economics.md`.
3. **Revisit the post-capstone continuity risk explicitly once CMPE 295B concludes** — this is the one risk with a known resolution date, unlike the others.
