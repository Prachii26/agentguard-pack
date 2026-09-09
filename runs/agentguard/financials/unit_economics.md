# Unit economics

**What this is**: per-unit P&L for one Comparison Report — CAC by channel, gross margin (inference cost included), payback period, LTV, and what happens to margin as model prices fall.

**Why it exists**: `references/quality-bar.md` and this skill's own contract require the AI-compute cost line to be mandatory, not asserted away — this document is where AgentGuard's per-unit economics get tested against real inference pricing rather than a comfortable guess.

**How to read it**: the gross margin section reuses `tech/not_vaporware.md` §3's cost derivation verbatim (per the founder's explicit instruction not to recompute it) — a skeptic should check that the campaign-cost numbers here match that document exactly, not a rounded-off variant.

**Depends on / feeds**: reuses `tech/not_vaporware.md` §3 and `financials/pricing.md`. Feeds `financials/use_of_funds.md` and `financials/comps_exits.md`.

---

## Per-unit P&L: one 4-defense Comparison Report

| Line | Value | Basis |
|---|---|---|
| Price | $2,500 | `financials/pricing.md` `(assumption: illustrative, not final)` |
| Inference cost (cheap tier: Claude Haiku 4.5) | $12–$40 | `tech/not_vaporware.md` §3, reused verbatim — 50 rounds/defense, ~637,500 tokens/campaign attacker-side, tripled for target/classifier/retries, ×4 defenses |
| Inference cost (frontier tier: Claude Opus 5) | $38–$190 | `tech/not_vaporware.md` §3, reused verbatim |
| **Gross margin (cheap tier)** | **~98.4%–99.5%** | ($2,500 − $12) / $2,500 = 99.5%; ($2,500 − $40) / $2,500 = 98.4% |
| **Gross margin (frontier tier)** | **~92.4%–98.5%** | ($2,500 − $38) / $2,500 = 98.5%; ($2,500 − $190) / $2,500 = 92.4% |
| **Blended assumption for planning** | **~95%** | `(assumption: midpoint, not a measured blend — actual model mix across attacker/target/judge roles per tier is unmeasured)` |

Inference cost is **not the constraint on this pricing** at either tier — `tech/not_vaporware.md` already states this explicitly, and this document does not relitigate it. The open question is willingness-to-pay (`financials/pricing.md`), not margin.

## CAC by channel

| Channel | CAC hypothesis | Basis |
|---|---|---|
| Free-tier/OSS → paid conversion | ~$0 marginal CAC per conversion | `strategy/channel_plan.md` — one-time/ongoing engineering cost, not a per-lead spend |
| Academic/research credibility content | ~$0 marginal CAC | `strategy/channel_plan.md` — founder/team time, not cash |
| Security community events | ~$200–$500/event-driven lead | `strategy/channel_plan.md` `(assumption)` |
| Outbound/paid | Not modeled — `strategy/channel_plan.md` rejected this channel as unviable at this price point for year one | `strategy/channel_plan.md` |

**Blended CAC for planning: ~$0–$50/customer `(assumption)`** — dominated by the two near-zero-CAC channels per `strategy/gtm.md`'s actual 90-day motion, which does not budget for paid acquisition.

## Payback period

At ~$0–$50 blended CAC and a $2,500 average report price with ~95% gross margin (~$2,375 contribution per report), **payback occurs on the first unit sold** for the two dominant channels — this is a direct consequence of the near-zero-CAC channel mix, not a sign of unusually strong economics; a business with paid CAC would show a materially different (worse) payback period, and this document does not claim the near-zero-CAC assumption will hold at scale.

## LTV under stated retention

`(assumption: no retention data exists — nothing has shipped)`. Illustrative only, using `financials/revenue_build.md`'s Stage 1 assumption of 4 reports/customer/year:

- If a beachhead customer retains for **2 years** at 4 reports/year × $2,500 × ~95% margin ≈ **$19,000 lifetime contribution**.
- Against a blended CAC of ~$0–$50, illustrative LTV:CAC is extremely favorable — but this ratio is an artifact of the near-zero-CAC assumption, not evidence of a strong business; `validation/riskiest_assumptions.md` should be read alongside this number, not this number alone.

## The cost-curve argument: margin as model prices fall

`research/sources.md` S101–S106 already document a ~4-6x frontier-tier price drop and up to ~100x cheap-tier drop over 2023-2026. Applying the same trend forward: if inference cost halves again, cheap-tier campaign cost moves from $12-40 to roughly $6-20 per report — gross margin moves from ~98.4-99.5% to ~99.2-99.8%, a small absolute improvement because margin is already close to its ceiling. **The cost-curve argument does not meaningfully improve this business's economics** — margin is already dominated by the $2,500 price point, not by inference cost, at either today's prices or a plausible future price. This is the honest conclusion, not the one that makes the best slide.

## Recommended next 3

1. **Do not use the LTV:CAC ratio above as a pitch number without the caveat that CAC is near-zero by channel-mix assumption, not by unusual product strength** — `skills/startup-critic`'s VC persona would flag this immediately.
2. **Measure real inference cost against real campaigns as soon as the riskiest-assumption test runs** — this document's cheap/frontier-tier range is a Fermi estimate, not a measurement, and should be replaced with real data at the first opportunity.
3. **Revisit CAC once any paid channel is tested** — the current near-$0 blended CAC assumes `strategy/gtm.md`'s channel mix holds exactly as planned; any deviation toward paid acquisition changes every number in this document.
