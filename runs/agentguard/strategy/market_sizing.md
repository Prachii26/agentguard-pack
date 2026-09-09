# Market sizing — TAM / SAM / SOM, bottom-up with a top-down check

**What this is**: TAM, SAM, and SOM for AgentGuard, built bottom-up (units × frequency × price) with every factor sourced or explicitly tagged `(assumption)`, cross-checked against the top-down analyst numbers in `research/sources.md`.

**Why it exists**: quality-bar property 2 requires every number to be sourced or flagged, and a market-sizing document is where that discipline is tested hardest — it is the artifact most tempted to round up. The failure this document prevents: a pitch deck slide reading "$X billion market" with no visible arithmetic behind it, which is the single fastest way to lose a technical investor's trust (`references/quality-bar.md` red flag list, and `skills/startup-critic`'s "skeptical deep-tech VC" persona's signature question).

**How to read it**: start with the pricing assumption box — every number downstream inherits it, and it is the single most load-bearing `(assumption)` tag in this document. A skeptic should attack the company-count Fermi estimate in the SAM section; it is the weakest-sourced step in the chain and is labeled as such rather than hidden.

**Depends on / feeds**: built from `research/sources.md` (S76–S89) and `strategy/market_type.md`. Feeds `strategy/gtm.md`'s CAC/payback math and `financials/revenue_build.md` — the pricing assumption here is explicitly preliminary and must be revisited, with the founder notified first, before `startup-financials` finalizes it (per the run's explicit instruction).

---

## Pricing assumption (load-bearing — read this box first)

**(assumption: preliminary, not final — no AgentGuard-specific pricing test exists)**. No source in `research/sources.md` gives AgentGuard-specific or even close-analog public per-engagement pricing — every named competitor's pricing is "not public" (`research/competitors.md` teardown table). **Correction (post-critic-loop)**: an earlier draft of this box cited the LLM Penetration Testing Services market's $3.416B aggregate scale (S82) as if it were the basis for the $750/$2,500 figures — it is not; S82 gives no per-engagement price or engagement count, so no arithmetic actually connects that aggregate number to a unit price, and citing it that way borrowed a source's credibility without deriving anything from it. Removed.

What the figures below are actually grounded in: a **cost-plus Fermi estimate** of what one campaign costs to run, computed from verified LLM pricing, checked against a plausible margin for self-serve security tooling.

**Campaign-cost Fermi** (order-of-magnitude, not a measured figure — arithmetic shown so it can be checked, not just asserted): assume a feedback-only adaptive campaign runs ~50 rounds against one defense (a reasoned mid-point — `BRIEF.md`'s riskiest-assumption test does not fix an exact N). Each round involves an attacker-model call and a target-agent-model call; because the attacker's context accumulates prior-round history, average context length grows across the campaign rather than staying flat — assume it grows roughly linearly from ~500 to ~25,000 tokens, averaging ~12,750 tokens/round (the arithmetic mean of the start and end). That's **50 × 12,750 ≈ 637,500 tokens** per campaign for the attacker side alone.

Using Claude Haiku 4.5 ($1 input / $5 output per million tokens, `research/sources.md` S103): at the cheap bound (treat all 637,500 tokens as input) that's 637,500 × $1/1,000,000 ≈ **$0.64**; at the expensive bound (treat all tokens as output) that's 637,500 × $5/1,000,000 ≈ **$3.19**. Call it **≈$1–$3** for the attacker side. Tripling to cover the target agent's own calls, defense-classifier calls, and retries: **≈$3–$10 in inference cost per single-defense campaign**, **≈$12–$40 for a full 4-defense Comparison Report**.

At frontier-tier pricing throughout instead (Claude Opus 5, $5 input / $25 output per million tokens, S103): cheap bound 637,500 × $5/1,000,000 ≈ $3.19, expensive bound 637,500 × $25/1,000,000 ≈ $15.94, tripled — lands at roughly **$10–$48 per single-defense campaign, ≈$38–$190 per 4-defense report**, three-to-five times the cheap-tier estimate but still one to two orders of magnitude below the $750/$2,500 price point.

Against a $750 single-campaign / $2,500 bundled-report price, this implies gross margin on inference cost alone is comfortably above 90% under either the cheap-tier or frontier-tier assumption — the risk this pricing box needs to track is not inference cost, it's whether $750/$2,500 is a price the market will actually pay, which no source or Fermi estimate can answer; that is a real open question, not a solved one.

For the arithmetic below only, this document uses:
- **$750 per single-defense adaptive campaign** (one attacker configuration run against one defense configuration to a matched budget).
- **$2,500 per full Comparison Report** (all four defense families — defensive prompting, classifier-based, rule-based, baseline — compared at matched budget in one bundled report; ~17% bundle discount off four standalone campaigns, reflecting the product's actual unit of value per `strategy/positioning.md` being the *comparison*, not the individual campaign).

These figures are **placeholders for sizing arithmetic only**, grounded in the cost-plus Fermi above, not in any market-comparable price point (none was found) or any willingness-to-pay data (none exists yet). Per the founder's explicit instruction, they will be surfaced again, explicitly, before `startup-financials` sets anything closer to final.

## TAM — top-down (sourced)

**$4.8B by 2027**, growing to **~$7.7B by 2028** — Gartner's "securing AI" market forecast, the narrowest analyst-firm (not vendor-report) category found that plausibly contains AgentGuard's product (`research/sources.md` S76). This is **not** the same as Gartner's much larger "AI-amplified security" figure ($204B by 2030, S78) — that category is traditional security tools *using* AI, not tools that secure AI systems, and citing it here would be the exact "1% of a $100B market" red flag `skills/startup-strategy`'s contract warns against. Within the 2027 "securing AI" figure, "AI application security" is the largest named sub-segment at ~$851M (S77) — the closest single line item to where an agent-security evaluation product's spend would be categorized.

Vendor market-research estimates for adjacent, differently-defined categories range widely ($0.9B–$5.66B for 2025/2026 depending on whether "LLM security platforms," "LLMs in cybersecurity," or "AI security platform (LLM & agent security)" is the definition used — S79–S81) — reported here as a range, not resolved to one number, because the definitions genuinely differ and none is an analyst-firm figure with Gartner's credibility.

## SAM — bottom-up (Fermi, every step tagged)

| Step | Value | Source / basis |
|---|---|---|
| 1. Companies with a dedicated ML/AI engineering function globally | **~50,000** | **(assumption: order-of-magnitude Fermi estimate — no primary source found for this exact count; used only as a Fermi base, not presented as sourced fact)** |
| 2. × share reporting agents in production (not just piloting) | **57.3%** | LangChain "State of Agent Engineering 2025," 1,300+ practitioners surveyed (`research/sources.md` S83) |
| 3. = companies with agents in production | **≈ 28,650** | Step 1 × Step 2 (arithmetic on an assumption-tagged base — treat the resulting count as directional, not precise) |
| 4. × share with governance/evaluation maturity sufficient to buy dedicated tooling (not just ad hoc prompting) | **~30%** | McKinsey "State of AI Trust in 2026," ~500 orgs surveyed: only ~30% reach maturity level 3+ on governance dimensions (`research/sources.md` S87) — used here as a proxy for "sophisticated enough to procure a dedicated evaluation tool" **(assumption: proxy, not a direct measurement of buying intent for this specific product)** |
| 5. = addressable companies (SAM company count) | **≈ 8,595** | Step 3 × Step 4 |
| 6. × campaigns (Comparison Reports) per company per year | **4** | **(assumption: one comparison run per quarterly release cycle — a reasoned default tied to `BRIEF.md`'s beachhead persona, "running an adaptive evaluation campaign before each release that expands tool scope or data access," not a measured cadence)** |
| 7. × price per Comparison Report | **$2,500** | Pricing assumption box above |
| **SAM** | **≈ $85.95M/year** | Step 5 × Step 6 × Step 7 |

**Sanity check against TAM**: $86M is ~1.8% of the $4.8B 2027 "securing AI" TAM (S76) — a plausible SAM-to-TAM ratio for a single product category within a multi-category market (not the red-flagged "1% of $100B" pattern, because the TAM itself is the correctly-scoped narrow category, not an inflated adjacent one).

## SOM — the beachhead, sized separately

`BRIEF.md`'s beachhead persona is a security/ML platform team at a company already running tool-using agents in production — not the edge-low solo developer (too small a contract to sustain a business) and not yet the edge-high enterprise red-team/platform-vendor tier (longest sales cycle, requires the credibility this venture doesn't have yet — see `strategy/market_type.md`'s sales-cycle consequence).

| Step | Value | Basis |
|---|---|---|
| Addressable beachhead companies | **≈ 8,595** (same SAM company count — the beachhead persona *is* the SAM's core, per `BRIEF.md`) | From SAM table above |
| × realistic year-1/2 capture rate for a pre-product, capstone-stage venture with zero traction, no sales team, self-serve-only motion | **0.1%–0.5%** | **(assumption: standard early-stage PLG capture-rate range for a self-serve security tool with no outbound sales function — not a measured figure; deliberately conservative given the explicit zero-traction starting point in `ASSUMPTIONS.md`)** |
| = customers captured | **9–43 companies** | Addressable × capture rate |
| × Comparison Reports/year × price | **4 × $2,500 = $10,000/customer/year** | From SAM table |
| **SOM (annual, steady-state at capture)** | **≈ $90,000–$430,000/year** | Customers × annual spend |

This is a small number by design — it reflects a pre-revenue, pre-product, zero-traction starting point (`ASSUMPTIONS.md` Restated hard facts), not a ceiling on the opportunity. `financials/revenue_build.md` should treat this SOM range as a year-1/2 floor to build a ramp from, not a target to hit immediately.

## Recommended next 3

1. **Revisit the two pricing figures explicitly with the founder before `startup-financials`** — flagged twice now (here and in `BRIEF.md`'s Business model section) because it is the single most load-bearing assumption in this entire document, and every downstream dollar figure inherits it directly.
2. **Test the SAM's weakest link (Step 1's ~50,000 company-count Fermi base) against a real data source** if one becomes available (e.g., a paid market-research report, a survey AgentGuard runs itself) — this is the step furthest from a citable primary source in the whole calculation.
3. **Track actual capture rate against the 0.1%–0.5% SOM assumption once real usage exists**, and correct this document rather than let it go stale — a market-sizing doc that's never revisited after first contact with real customers is exactly the kind of artifact `references/quality-bar.md` warns reads as unowned.
