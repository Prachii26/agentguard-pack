# Architecture index — ten diagrams, AgentGuard's own nouns

**What this is**: the index and reading order for the ten architecture diagrams (`D01.md`–`D10.md`), each a titled Mermaid diagram with a caption naming what a reviewer should notice.

**Why it exists**: `tech/deep_dives.md` describes the mechanisms in prose; a reviewer who wants to check whether the system actually holds together as an architecture, not a list of algorithms, needs the shape drawn out. The failure this document prevents: architecture diagrams that are boxes labeled "AI" (`skills/startup-tech/SKILL.md`'s own red-flag list) — every diagram below traces to a named component in `tech/deep_dives.md`, not an invented box.

**How to read it**: read D02 (the adaptive round loop) and D04 (the schema) first — they are the two diagrams a skeptic would draw themselves to check whether AgentGuard's claimed mechanism is internally consistent. D01 and D03 show how the pieces assemble around that loop; D05–D10 show the operational concerns (cost, security, integrations, observability, scale, escalation) that separate a working system from a research script.

**Depends on / feeds**: built from `tech/deep_dives.md` items 1–8 and `BRIEF.md`'s Mechanism section. Feeds `product/ux_spec.md` (not yet generated) and any future engineering handoff.

---

| # | Title | Traces to (`deep_dives.md` item) | What a reviewer should notice |
|---|---|---|---|
| D01 | Campaign-to-Comparison-Report pipeline | Items 1, 4–7 | The four defense harnesses run structurally identically, converging on one aggregator — the matched-budget guarantee is a pipeline property, not an afterthought. |
| D02 | Feedback-only round loop | Item 1 | The attacker observes pass/fail only, never defense identity — the diagram makes the information boundary explicit, the exact thing `BRIEF.md`'s feedback-only definition depends on. |
| D03 | Red-team / target / defense / judge orchestration | Items 1, 7, 8 | The orchestrator (PyRIT-pattern) is plumbing, not an attack strategy — a reviewer checking for overclaiming should confirm the orchestrator box has no attack-generation logic of its own. |
| D04 | Campaign & Comparison Report schema | Item 7 | Utility score lives on the ROUND entity, not bolted onto the report after the fact — utility-pairing is a schema-level decision, not a reporting afterthought. |
| D05 | Model routing & cost control | Items 1, 2 | Cheap-tier and frontier-tier models are routed by role, not uniformly — this is where `tech/not_vaporware.md`'s cost model becomes an architectural constraint, not just an estimate. |
| D06 | Staging-only isolation boundary | `BRIEF.md` Year-one scope #1 | Production is drawn as explicitly unreachable, not merely "not currently used" — the diagram should make a skeptic's "what if this touches real user data" objection visibly false by construction. |
| D07 | Environment and release-pipeline integrations | Items 1, 7 | AgentGuard sits on top of AgentDojo and AutoDojo, not beside or instead of them — the diagram is honest about which components are adopted, matching `ASSUMPTIONS.md` A9. |
| D08 | AgentGuard's own quality loop | `BRIEF.md` Riskiest assumption, `tech/not_vaporware.md` | AgentGuard re-runs its own riskiest-assumption test as a standing self-check, not a one-time validation — a reviewer should notice this loop never terminates. |
| D09 | Multi-tenant scalability | Item 7, 8 | Tenant isolation is enforced at the log layer, not just at the queue layer — relevant because campaign logs are the raw material for any future comparison-corpus moat hypothesis (`BRIEF.md` Moat), which must not leak across customers. |
| D10 | Critical-finding and false-block escalation | `BRIEF.md` Year-one scope, `strategy/personas.md` persona 3 (Elena Osei) | Escalation triggers on severity (irreversible actions, exfiltration), not on every failed round — a reviewer should check this doesn't silently suppress ordinary findings by routing everything through a human bottleneck. |

## Recommended next 3

1. **Build D02 and D04 first as executable stubs** (a mocked round loop writing to the real schema) before any of the other eight — every other diagram assumes these two are correct.
2. **Treat D06 as a security-review gate, not just a diagram** — before any staging integration ships, confirm the actual code path matches the boundary drawn here, not just the intent.
3. **Revisit D09 once `BRIEF.md`'s Moat hypothesis (accumulating comparison corpus) is tested against real usage** — if that hypothesis firms up, D09's per-tenant isolation design has direct bearing on what a cross-customer corpus could and could not ethically aggregate.
