# Value Proposition Canvas

**What this is**: customer jobs/pains/gains mapped against AgentGuard's pain-relievers/gain-creators/products, for the two personas who actually pay (Marcus, the beachhead engineer, and Elena/David, the enterprise red-team lead and budget holder), with the strongest mapping ranked.

**Why it exists**: `strategy/lean_canvas.md`'s UVP cell asserts a value proposition in one sentence; this document is the evidence that the mapping underneath it is real, job-by-job, not just a slogan. The failure this document prevents: a positioning statement that sounds right in isolation but doesn't actually relieve the specific pain a named persona described in `strategy/personas.md`.

**How to read it**: the ranked mapping at the end of each persona's table is the one `strategy/gtm.md`'s messaging should lead with — everything else is supporting, not primary.

**Depends on / feeds**: built from `strategy/personas.md` and `BRIEF.md`'s Solution/Mechanism. Feeds `strategy/gtm.md`'s messaging hierarchy and `product/PRD.md`'s feature prioritization.

---

## Persona 1: Marcus (beachhead — security/ML platform engineer)

### Customer profile

| Jobs | Pains | Gains |
|---|---|---|
| 1. Produce a risk assessment before each release that expands agent tool access | 1. No time or budget for an external pentest on a sprint timeline | 1. A report he can attach directly to the release risk-assessment ticket |
| 2. Choose which defense (prompting/classifier/rule-based) to deploy | 2. Existing tools (Garak, manual checklist) give "no findings" results he privately doesn't trust | 2. A number that reflects how hard an *adapting* attacker actually has to work, not a static pass/fail |
| 3. Justify the security/usability trade-off to product when a defense blocks legitimate requests | 3. No way to show product *why* a stricter defense costs real usability, so security asks get overridden | 3. A utility number alongside the attack number, so the trade-off is visible and defensible in the same conversation |

### Value map

| Pain relievers | Gain creators | Products/services |
|---|---|---|
| 1. Report ties directly into existing release risk-assessment process — no new workflow to adopt | 1. Final-window ASR + utility reported together, per defense | 1. Self-serve API/CLI campaign against staging deployment |
| 2. Matched-budget adaptive attacker replaces the "no findings" static-checklist result with an honest adapted-attacker number | 2. Adaptation curve shows *how fast* an attacker converges — a speed signal, not just a yes/no | 2. Per-defense comparison report (4 defense configurations, one run) |
| 3. Utility metric (aligned to AgentDojo's definition) gives him language product can't dismiss as "security being paranoid" | 3. Reproducible, re-runnable before every release — not a one-off engagement he has to re-justify each time | 3. Usage-based pricing matches his per-release cadence, no annual-contract approval cycle needed |

**Ranked mapping (strongest first)**: (1) the release-risk-assessment fit — this is the pain with the tightest deadline and the clearest existing process to slot into; (2) the utility-paired trade-off number — this is the pain no competitor found in research addresses (`research/competitors.md`); (3) the "no findings ≠ trustworthy" pain — real, but slower-burning and harder to quantify in a sales conversation than the first two.

## Persona 2: Elena (edge-high, user) and David (edge-high, payer)

### Customer profile

| Jobs | Pains | Gains |
|---|---|---|
| 1. (Elena) Give the board one coherent, comparable security number across dozens of agents and defenses | 1. Current vendor outputs don't share a common metric — can't be aggregated or trended | 1. One reproducible protocol, run the same way every time, across every agent in the portfolio |
| 2. (David) Produce certification-grade evidence for ISO 42001 and board/audit questions | 2. Current answer to auditors is assurance ("my team tells me it's fine"), not evidence | 2. A report format built to function as audit evidence, not just an internal security artifact |
| 3. (Both) Decide whether a new AI-security vendor is worth the switching/procurement cost given zero traction | 3. Pre-traction vendor risk — "will this company exist in two years" | 3. (Unaddressed by product alone — see Objection in `strategy/personas.md` card 4; must be handled in sales conversation, not product) |

### Value map

| Pain relievers | Gain creators | Products/services |
|---|---|---|
| 1. Same protocol run across every agent and defense in the portfolio produces one trendable metric set | 1. A number the board and an insurer can both read the same way over time | 1. Continuous/high-frequency campaign usage at edge-high scale (same self-serve unit, higher volume — `ASSUMPTIONS.md` A3) |
| 2. Report structure maps to ISO 42001's Operation/Performance Evaluation clauses (S114) | 2. Converts a compliance burden into a documented, defensible artifact | 2. Exportable comparison report suitable for audit attachment |
| 3. *(Not solved by the product)* — pre-traction risk must be addressed by transparency (open methodology, published research credibility) rather than papered over | 3. Academic/research credibility (methodology extends AgentDojo/AutoDojo's own published literature) partially substitutes for traditional vendor-maturity signals | 3. Public methodology documentation, not just an opaque report |

**Ranked mapping (strongest first)**: (1) the one-reproducible-protocol-across-portfolio pain — this is Elena's, and it's the pain no competitor in `research/competitors.md` solves (each reports differently, none is cross-defense); (2) the certification-grade-evidence pain — this is David's, and it's the pain that actually gets budget approved, since David (not Elena) signs; (3) the pre-traction trust gap — honestly, the weakest-addressed pain in this whole canvas, and the one `narrative/vc_memo.md` and `strategy/gtm.md` need to name rather than paper over.

## Recommended next 3

1. **`strategy/gtm.md`'s beachhead messaging leads with Marcus's #1 ranked pain (release-risk-assessment fit), not the adaptive-attacker technique** — consistent with `strategy/positioning.md`'s instruction to lead with the comparison, not the adversary.
2. **David's pain (#2, certification-grade evidence) should shape `product/ux_spec.md`'s report export format** — an audit-ready PDF/export is a concrete product requirement this canvas surfaces, not just a nice-to-have.
3. **The unaddressed pre-traction-trust pain (Elena/David #3) should become an explicit line in `validation/discovery_guide.md`'s interview script** — ask real prospects directly what evidence (open-source, published papers, pilot references) would overcome it, rather than assuming the academic-credibility answer above is sufficient.
