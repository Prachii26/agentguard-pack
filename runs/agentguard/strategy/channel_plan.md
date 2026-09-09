# Channel plan — map and economics

**What this is**: the channel map by segment plus, for each channel, the discount/margin stack from list price to net, the cost to acquire through it, the time to first revenue, and whether it's viable at AgentGuard's price point.

**Why it exists**: `strategy/petal_diagram.md` names where customers' budgets currently sit; this document computes whether reaching them through each available channel actually pencils out at the pricing `strategy/market_sizing.md` assumes. The failure this document prevents: a GTM narrative that names channels (as `strategy/lean_canvas.md`'s Channels cell does, necessarily briefly) without ever computing whether any one of them is financially viable — asserting distribution instead of planning it.

**How to read it**: the "Viable at this price point?" column is the verdict — a skeptic should check that every channel marked viable actually survives the discount/margin stack at the $750/$2,500 pricing assumption (`strategy/market_sizing.md`), not just sound plausible in prose.

**Depends on / feeds**: built from `strategy/petal_diagram.md` and `strategy/market_sizing.md`'s pricing assumption. Feeds `strategy/gtm.md`'s CAC-payback logic directly.

---

## Channel map by segment

| Segment | Primary channel | Secondary channel |
|---|---|---|
| Edge-low (Priya) | Open-source scanner / free tier, organic discovery (GitHub, dev communities) | Word of mouth from edge-low users who later move to beachhead roles |
| Beachhead (Marcus) | Academic/research credibility content (methodology posts, conference talks) driving direct self-serve signup | Security community events (DEF CON AI Village-adjacent, HackAPrompt-adjacent — `research/sources.md` S140–S143) |
| Edge-high (Elena, David, Sofia) | Direct outreach informed by published research credibility (papers, methodology transparency) | Inbound from beachhead accounts that grow into edge-high usage over time |

## Channel economics

| Channel | Discount/margin stack (list → net) | Cost to acquire | Time to first revenue | Viable at $750/$2,500 price point? |
|---|---|---|---|---|
| **Open-source scanner / free tier** | No discount on the *paid* product — the OSS tool itself is free (zero list price), monetization happens only when a user upgrades to a paid Comparison Report at full $2,500 list, net ≈ list (self-serve, no reseller cut) | Engineering time to build and maintain the OSS scanner (one-time + ongoing maintenance), no per-acquisition dollar cost — **(assumption: comparable to SplxAI's Agentic Radar and Giskard's OSS-to-Hub motion, S62/S54, not a measured AgentGuard-specific cost)** | Longest of the three — depends on organic adoption curve of the free tool before any paid conversion | **Yes** — zero marginal acquisition cost per paid conversion means the channel is viable at any positive price point above infrastructure cost; the risk is volume/speed, not unit economics |
| **Academic/research credibility content** | No discount — direct self-serve signup at full list price, net = list | Primarily founder/team time (writing, publishing, speaking) — near-zero cash cost, consistent with the capstone team's actual resources (`BRIEF.md` Founder edge) | Medium — a methodology post or conference talk can drive signups within weeks, but trust-building compounds over months | **Yes** — same zero-cash-cost structure as the OSS channel; the real cost is opportunity cost of founder time, which `strategy/business_model_canvas.md`'s Key Activities hypothesis is built to test |
| **Security community events (DEF CON AI Village, HackAPrompt-adjacent)** | No discount — direct signup, net = list | Travel/registration cost only (small, one-time per event) — no ongoing per-lead cost | Fast for the specific leads met at an event, but event cadence is infrequent (a few per year), so aggregate volume is low | **Yes for individual conversions, no as a primary scaling channel** — good for edge-high credibility-building (meeting Elena/Sofia-type prospects directly) but cannot carry SOM-floor volume alone; explicitly secondary per the channel map above |
| **Direct outbound sales (considered and rejected for year one)** | Would require a discount/negotiation stack typical of enterprise sales (10–20% off list for annual commitments) plus a commissioned sales function | High — fully-loaded SDR/AE cost, easily exceeding the $2,500 per-Comparison-Report list price on a single deal's CAC before any negotiated discount is even applied | Fast per deal once a rep is productive, but ramp time to productivity is 3–6 months typically | **No** — at this unit price ($750–$2,500 per transaction, not an annual contract), a commissioned outbound motion's CAC would exceed multiple transactions' worth of revenue before payback; this is *why* `BRIEF.md`'s Business model and `ASSUMPTIONS.md` A3 commit to self-serve-only rather than a two-motion model |

## Recommended next 3

1. **Build the OSS scanner (or an equivalent free-tier artifact) as the first channel investment**, not a "nice to have" — it's the only channel in this table with genuinely zero marginal acquisition cost per conversion, which matters most given the zero-funding starting point.
2. **Track actual conversion-to-paid rates from the free tier and academic-content channels against the SOM's 0.1%–0.5% capture-rate assumption (`strategy/market_sizing.md`)** — if real conversion undershoots that range, the channel economics in this table (viable in theory) will need re-testing before `startup-financials` trusts them.
3. **Revisit the "no" verdict on direct outbound sales once (if) an edge-high annual-contract motion is validated** — this document's rejection is specific to the current self-serve, per-transaction pricing; a future pivot to an annual enterprise contract (flagged as a live open question in `ASSUMPTIONS.md` A3) would change this channel's viability math entirely.
