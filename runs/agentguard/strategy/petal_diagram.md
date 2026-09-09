# Petal diagram — adjacent markets AgentGuard draws customers from

**What this is**: Blank's petal diagram — AgentGuard at the center, six adjacent markets it draws customers *from* (not a 2×2 of rivals), naming the incumbents in each petal and what those customers currently spend their budget and time on.

**Why it exists**: `strategy/positioning.md` answers "where do we sit relative to direct rivals"; this document answers the harder, more useful question Blank's Customer Development method asks instead — whose existing budget and habit does AgentGuard actually have to displace to get its first dollar. The failure this document prevents: a GTM plan that assumes a clean, uncontested new budget line exists, when every dollar AgentGuard earns in year one will visibly come out of some other line item a prospect already funds.

**How to read it**: for each petal, the "what they currently spend" column is the number `strategy/gtm.md`'s CAC-payback logic should be checked against — a channel strategy that ignores which existing budget it's displacing will overestimate how easy the sale is.

**Depends on / feeds**: built from `research/competitors.md` and `research/sources.md` (funding/market data). Feeds `strategy/channel_plan.md` and `strategy/gtm.md`.

---

```
                    Petal 2
              AI Guardrails/Runtime
              Defense Budget
              (Lakera, SentinelOne/
              Prompt Security)
                     |
  Petal 6                              Petal 3
  Internal Security          \    /    Traditional AppSec /
  Engineering Headcount        \/       Pentest Budget
  (build-vs-buy)               /\      (Bishop Fox-style
                               /  \      firms, annual
                              /    \     engagements)
                         AGENTGUARD
                              \    /
  Petal 5                      /\
  Compliance/GRC Tooling      /  \
  Budget (ISO 42001,          |    Petal 4
  EU AI Act evidence          |    Open-Source/Academic
  platforms)                  |    Tooling (Garak, PyRIT,
                     Petal 1  |    AgentDojo — time, not $)
              AI/Agent Red-Teaming
              & Pentesting Services
              (Adversa AI, Straiker,
              Mindgard, HiddenLayer)
```

## The six petals

| Petal | Incumbents | What customers there currently spend |
|---|---|---|
| **1. AI/agent red-teaming & pentesting services** | Adversa AI, Straiker ($85M raised, S63), Mindgard ($30M Series A, S44), HiddenLayer ($156M total, S46) | Proprietary per-engagement or subscription spend on adversarial testing, structurally unable to produce a published cross-defense comparison (`research/competitors.md`) — the budget already exists and is already earmarked for "someone attacks our AI," AgentGuard argues for a slice of it on the comparison framing rather than asking for a new line item. |
| **2. AI guardrails / runtime defense** | Lakera Guard, SentinelOne (Prompt Security, ~$250M acquisition, S66), NVIDIA NeMo Guardrails, Guardrails AI (now Harvey, S67) | Ongoing subscription/license spend on the *defense itself*. These customers already believe their defense works; AgentGuard's pitch is that the same budget owner needs to know, with evidence, whether it actually does — a natural upsell conversation for whoever owns this line item. |
| **3. Traditional application security / pentest budget** | Established pentest firms running annual/semi-annual engagements that increasingly include an "AI/LLM" line item as a checkbox, not a specialty | Annual contracted pentest spend, historically web/API-focused, now expanding scope. AgentGuard argues for AI-agent evaluation as a distinct, deeper line item within this existing annual budget cycle rather than a wholly new purchase decision. |
| **4. Open-source/academic tooling** | Garak (NVIDIA-backed), PyRIT (Microsoft), AgentDojo/AutoDojo (academic, free) | Not dollars — **engineering time**. Teams currently running these tools in-house pay in the hours of a security engineer (Marcus, `strategy/personas.md`) manually stitching results together. AgentGuard converts time spent into a purchased report, the classic OSS-to-paid conversion motion (same pattern as Giskard's OSS library → Hub, S54). |
| **5. Compliance/GRC tooling budget** | ISO 42001 and EU AI Act compliance-evidence platforms, broadly (no single named vendor confirmed in research as AI-agent-specific — flagged as an open space in `research/sources.md`'s regulatory section) | Emerging spend tied to certification requirements (ISO 42001, published Dec 2023, S113) and the EU AI Act's red-teaming/adversarial-testing requirements for systemic-risk models (S109). This is the newest, least-established petal — the budget line is still forming, which is both an opportunity (less entrenched competition) and a risk (less certain the budget exists yet at all). |
| **6. Internal security engineering headcount (build vs. buy)** | No external vendor — the "incumbent" is the cost of Marcus's or Elena's own team building an internal adaptive-evaluation harness themselves (a real, viable alternative, since AutoDojo is free and open-source, S13/S14) | Fully-loaded engineering time to build and maintain an internal tool. AgentGuard's argument here is time-to-value and ongoing maintenance burden, not capability — a technically sophisticated team *could* build this themselves from AutoDojo's open code, and some will; this petal's customers are the ones who decide the maintenance burden isn't worth it. |

## Recommended next 3

1. **Prioritize Petal 1 and Petal 4 for year-one GTM** — Petal 1 (red-teaming services budget) is the largest and most clearly earmarked existing spend; Petal 4 (OSS/academic tooling users) is the cheapest to reach via the channel plan already committed to (`strategy/channel_plan.md`) and matches `strategy/business_model_canvas.md`'s Channels hypothesis.
2. **Treat Petal 6 (build vs. buy) as the petal to actively address in messaging, not ignore** — AutoDojo being free and open-source means a sophisticated prospect's real alternative is "build it ourselves," and `strategy/positioning.md`'s messaging should preempt this objection directly (time-to-value, ongoing maintenance, methodology credibility) rather than assume it won't come up.
3. **Watch Petal 5 (compliance/GRC) as the highest-upside, least-proven petal** — revisit this diagram once `validation/discovery_guide.md` interviews test whether real budget exists yet for AI-agent-specific compliance evidence, since the current entry is based on regulatory-requirement citations (S109, S113) rather than confirmed spending behavior.
