# AgentGuard — Future Press Release (working backwards, dated 2033)

**What this is**: an Amazon-style working-backwards press release, written as if dated 2033, describing the outcome AgentGuard would need to achieve for its thesis to have been right — plus a "how we got here" timeline.
**Why it exists**: every other narrative artifact argues from today's evidence; this one is the only place the pack states, vividly and on the record, what winning actually looks like — so that near-term decisions can be checked against whether they move toward this outcome or away from it. The failure this prevents: a team that executes competently on individual features while losing sight of what the comparison protocol was supposed to become.
**How to read it**: this is a hypothetical, clearly dated in the future — nothing in it is a claim about the present. A skeptic should check that the "how we got here" timeline stays consistent with the resolved wedge (`ASSUMPTIONS.md` A9: the comparison, not the attacker) rather than quietly reverting to "we invented adaptive attacks," which the pack has already rejected.
**Depends on / feeds**: extrapolates from `BRIEF.md`'s 10-year vision, `strategy/positioning.md`'s open quadrant, and `strategy/market_sizing.md`'s SAM. Consumed by nobody downstream — this is a vision artifact, not an input to other files.

---

**FOR IMMEDIATE RELEASE — March 14, 2033**

## Comparison-budget testing becomes the standard release gate for tool-using AI agents; AgentGuard's protocol format is now cited more often than any single vendor's product

*SAN JOSE, CALIF.* — When a security team asks "did our agent's defense hold up," the number that now settles the question is a **final-window ASR at matched attempt budget, reported alongside utility, across every defense family under consideration** — the exact shape of report AgentGuard began publishing from a four-person graduate capstone project at San José State University in 2026. What started as a comparison protocol extending the AgentDojo and AutoDojo literature is now referenced, by name or by format, in security release checklists at companies that have never used AgentGuard's product directly — the way a "Sharpe ratio" or an "NPS score" outlived the company that popularized it.

"I don't need 'no vulnerabilities found' anymore — nobody's accepted that as an answer in years," said a hypothetical version of Marcus Webb, now a principal security engineer at a payments company, describing the kind of report a beachhead customer might attach to a release ticket in this scenario. "What I need is the comparison-budget number: how hard did it have to try, against each defense we were considering, and what did the harder one cost us in blocked legitimate work. That's the report format now — it's not even branded, it's just how you show your work."

"We stopped treating a point-in-time pentest as sufficient evidence for the board in 2029," said a hypothetical version of Dr. Elena Osei, in this scenario now a CISO herself. "What changed the conversation with our insurer wasn't a better attacker — every serious vendor has an adaptive attacker now. It was that one comparison format, run the same way every quarter, across every agent we ship, that our underwriter could actually read as a trend line instead of a one-off claim."

### The metric the world now uses

**Comparison-budget ASR** — attack success rate at a stated, matched attempt budget, reported per defense family alongside legitimate-task utility — has become the reference unit analysts and regulators cite when discussing agent-defense resilience, the way "requests per second" became a reference unit for infrastructure performance long after any one company owned the term. No single vendor owns the metric; AgentGuard is credited as the entity that made it a standing, reproducible measurement rather than a one-off research result.

### How we got here (a hypothetical timeline, consistent with the resolved wedge)

- **2026** — AgentGuard begins as a CMPE 295A/295B graduate capstone project: a comparison protocol, not a new attack technique, built by adopting AutoDojo's published adaptive-attack optimizer and AgentDojo's utility definition rather than inventing either. The riskiest assumption (adaptive beats static at matched budget) is tested and reported honestly, including whatever the result actually is.
- **2027** — The team (or a successor effort building on the published methodology, win or lose as a company) publishes the first cross-defense, utility-paired comparison results extending, not competing with, the AgentDojo/AutoDojo literature — the credibility motion `strategy/gtm.md` names as cheaper than outbound sales for a pre-traction team.
- **2028–2029** — The comparison format gets cited by at least one of the platform or vendor incumbents named in `research/competitors.md` (Microsoft's Foundry Red Teaming Agent or a commercial vendor such as Adversa AI) as a reference point in their own reporting — in this scenario, a sign the format won broader adoption than any single product line, not evidence that the originating team out-competed them on distribution.
- **2030–2031** — ISO 42001 recertification cycles and EU AI Act Article 15 disclosure practices converge on matched-budget, utility-paired comparison evidence as a common (not mandated) way to satisfy adversarial-robustness documentation expectations — regulatory language catching up to a format the market had already converged on, not the reverse.
- **2032–2033** — Comparison-budget ASR is referenced in security literature, vendor marketing, and board-level reporting widely enough that its origin as one capstone team's protocol is a historical footnote, not a current competitive claim.

### What this scenario does not claim

This is not a projection with a probability attached, and it does not assume AgentGuard-the-company survives to 2033, wins any specific competitive encounter named in `research/competitors.md`, or achieves the market share implied by `strategy/market_sizing.md`'s SAM. It states one thing plainly: **if the comparison-protocol thesis (`ASSUMPTIONS.md` A9) is right, this is the shape "right" takes** — a metric that outlives any one vendor, not a company that out-attacks Adversa AI or out-distributes Microsoft. Whether it happens depends on evidence this pack does not yet have, starting with the riskiest-assumption test that has not been run as of this writing.

## Recommended next 3

1. **Re-read this file after the riskiest-assumption test result lands** — if the test returns a null or negative gap, this entire scenario's premise (adaptive beats static, therefore a comparison protocol is worth standardizing) needs to be revisited, not quietly kept as aspirational copy.
2. **Do not quote the hypothetical customer lines above in any investor-facing document as if they were real testimonials** — they are explicitly future-hypothetical, framed in the persona voices from `strategy/personas.md`, and reusing them outside this file's clearly-dated fiction would violate `references/quality-bar.md`'s zero-traction honesty requirement.
3. **Revisit the "how we got here" timeline against `tech/deep_dives.md` and `tech/whitepaper.md` in full** — both populated mid-session; this file's timeline was checked only against `tech/architecture/00_INDEX.md`'s diagram index and `product/journeys/`'s three journey narratives under the same-day deadline, not the full technical prose.
