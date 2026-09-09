# Positioning — the two axes, the open quadrant, the statement

**What this is**: the two axes that actually divide the agent-security-evaluation market (discovered from `research/competitors.md`, not assumed), every named competitor placed on them, the quadrant nobody occupies, and the one-sentence positioning statement everything else in the pack should trace back to.

**Why it exists**: `ASSUMPTIONS.md` A9 records that AgentGuard's original wedge ("we automate the adaptive adversary") was half-wrong — three candidate replacement differentiators were considered and rejected before landing on the one this document builds around. The failure this document prevents: a pitch deck that claims differentiation on attack technique against funded competitors (Adversa AI, Straiker) who can out-resource that fight, when the real open space is somewhere else entirely.

**How to read it**: the 2×2 is the argument. A skeptic should try to place AgentGuard in the same quadrant as Adversa AI, AutoDojo, or Microsoft's AI Red Teaming Agent (the platform-bundled threat, easy to underweight because it's free rather than a funded startup) — the competitor-placement table exists specifically so that attempt fails on the record, not just in prose.

**Depends on / feeds**: built from `research/competitors.md` and `ASSUMPTIONS.md` A9. Feeds `strategy/gtm.md`, `strategy/market_sizing.md`, `narrative/one_pager.md`, and `narrative/vc_memo.md` directly — none of those should invent a different differentiation claim.

---

## The two axes

Most 2×2s in this space default to "price × quality" or "adaptive × static," and both are wrong here — the first is meaningless in a market where most pricing is "not public" (`research/competitors.md` teardown table), and the second was AgentGuard's *original* wedge, already occupied by AutoDojo and Adversa AI (`ASSUMPTIONS.md` A9). The two axes that actually separate every named entry in `research/competitors.md`'s teardown table:

- **X-axis — What's reported**: attack-success-rate-only ↔ **attack success and legitimate-task utility reported together**.
- **Y-axis — Comparison scope**: single defense / single framework, evaluated once ↔ **multiple defense families compared at matched attack budget, reproducibly**.

## Competitor placement

| Entity | ASR-only ↔ ASR + utility | Single defense ↔ cross-defense, matched-budget | Quadrant |
|---|---|---|---|
| Garak, PyRIT (raw), InjecAgent, Agent Security Bench | ASR-only | Single defense, static | Bottom-left |
| AutoDojo [S13] | ASR-only (no utility metric) | Single defense (one filter at a time), within one framework (AgentDojo) | Bottom-left, but high on a third dimension (adaptivity) not plotted here — see `research/competitors.md`'s original two-axis read for that framing |
| NIST/UK AISI human red-team exercise [S27] | ASR-only (hijack success rate) | Single model, single exercise, not repeated | Bottom-left, one-off, not a product |
| Adversa AI [S50–S52] | ASR-only in all public material found — no published utility metric | Proprietary, per-customer engagements; no published cross-defense comparison | Bottom-left today; **one business-model decision (publishing an aggregate benchmark) away from top-right** — see "The open quadrant" below |
| Straiker, Mindgard, HiddenLayer, SplxAI, Repello AI [S44–S64] | ASR-only / vulnerability-count-only in all public material found | Full-stack breadth (discover + attack + defend) but no evidence of a published matched-budget, cross-defense-family comparison | Bottom-left to bottom-center |
| **Microsoft AI Red Teaming Agent (Azure Foundry)** [S60, S61] | ASR-only (XPIA success/failure) | Runs against one customer's one deployment at a time, not a published cross-defense comparison | Bottom-left today, but **the single biggest platform-level threat to this whole quadrant** — it already owns the attacker half of AgentGuard's mechanism, bundled free into every Foundry account; a feature update, not a new product, would close the gap — see "The open quadrant" below |
| AgentDojo itself [S1] | Both ASR and utility — the only entry besides AgentGuard that reports utility | Single framework, and (per the shipped paper) single fixed attack distribution, not cross-defense at matched adaptive budget | Top-left — **closest neighbor on the reporting axis**, which is exactly why AgentGuard's utility metric is explicitly aligned to AgentDojo's definition (`BRIEF.md` Vocabulary) rather than inventing a new one |
| **AgentGuard** | **ASR + utility, reported together, per defense** | **All four defense families, matched attack budget, reproducible** | **Top-right — unoccupied** |

## The open quadrant — and why it stays open only for now

Top-right — ASR-and-utility reported together, AND compared across defense families at matched budget — is occupied by no entity found in this research. Three named entities could plausibly move into it, and none is blocked by anything AgentGuard controls — this is a **window, not a moat**, consistent with `BRIEF.md`'s Moat section already naming "none yet" as a gap rather than an asset:

- **AutoDojo** is one axis-step away (adding a utility metric is a research contribution, not a structural blocker) but stays single-framework by design; it is academic prior art with no product incentive to publish a standing cross-defense comparison — a plausible-but-unincentivized move, not an impossible one.
- **Adversa AI** is one axis-step away on the reporting axis and already covers the cross-defense-scope half through its proprietary engagements. Its current business model (per-customer, confidential) doesn't produce a *published* comparison today, and publishing one would cut against the confidentiality a consulting-shaped business usually sells — but this is a business-model choice, not a technical or structural wall. **Nothing prevents Adversa AI's leadership from deciding, as a marketing move, to publish an aggregate, anonymized cross-defense benchmark tomorrow** — if they did, the gap closes quickly. Treat this as the single most important thing to monitor (see Recommended next 3), not as a settled advantage.
- **Microsoft's AI Red Teaming Agent** (`research/competitors.md`) is arguably the biggest threat of the three, and the one this document must not underweight: Microsoft already owns the attacker half of AgentGuard's mechanism (PyRIT-based, 20+ attack strategies, explicit XPIA/tool-call testing, S60/S61), bundled free into every Azure AI Foundry account — free distribution to a large share of the beachhead segment. Shipping "run this against N configured defenses, report ASR and utility side by side" as a Foundry feature update is a small increment for Microsoft, not a new product. There is no evidence in `research/sources.md` that Microsoft has done this yet, but there is nothing in this positioning that explains why they wouldn't — the honest answer is speed and focus: a small team with nothing else to build can ship and iterate on the comparison protocol faster than a feature inside a much larger platform roadmap competes for priority, which is a real but time-limited advantage, not a permanent one.

**A related risk worth naming plainly, not softening**: read uncharitably, AgentGuard's mechanism is an orchestration layer over two already-public academic components — AutoDojo's attacker (S13) and AgentDojo's utility metric (S1) — both already living in the ecosystem `BRIEF.md` cites as baseline. That's a fair "wrapper" concern (`references/quality-bar.md`'s red-flag vocabulary), and this document does not have a rebuttal beyond: nobody has actually glued these two specific open pieces together and published the resulting cross-defense results yet, and doing that well, maintained, and reproducibly is real (if not deeply defensible) work. State this honestly rather than claim a deeper moat than exists.

See `strategy/market_type.md`'s dominant-risk row, which names Adversa AI/Microsoft closing this gap as the single highest-priority competitive risk to track — not restated here to avoid repeating the same point twice in one document.

## Positioning statement

> For security and ML platform teams deploying tool-using AI agents to production, **AgentGuard is designed to be** the only adaptive evaluation platform that reports attack success and legitimate-task utility together, across every defense family a team is considering, at matched attack budget — because it runs the same feedback-only adaptive campaign against each deployed defense configuration and publishes the comparison, rather than selling a single proprietary attack engine (Adversa AI), a bundled platform feature with no published comparison (Microsoft's AI Red Teaming Agent), or a single-framework academic result with no utility metric (AutoDojo).

No campaign has been run yet (`ASSUMPTIONS.md`, Restated hard facts) — this statement describes the product's design intent, not a shipped, operating claim.

## Recommended next 3

1. **Every mention of "adaptive" in narrative artifacts must be paired with "and utility-paired, cross-defense" — never stated alone.** Stated alone, "adaptive" collapses back into AgentGuard's original, now-rejected wedge and invites direct (losing) comparison to Adversa AI and AutoDojo on their own terms.
2. **`strategy/gtm.md`'s messaging hierarchy should lead with the comparison, not the attacker** — first sentence of any sales/marketing copy names the trade-off report, not the adaptive-attack technique, which is prior art AgentGuard adopts rather than a claim to lead with.
3. **Monitor both Adversa AI's public material and Microsoft AI Red Teaming Agent's Foundry release notes on a recurring basis for a published cross-defense or utility metric** — these are the two fastest ways this positioning becomes obsolete (a marketing decision for Adversa AI, a roadmap decision for Microsoft), and either is a trigger condition that should populate `validation/pivot_log.md` if it happens.
