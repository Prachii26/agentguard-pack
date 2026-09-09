# Sales roadmap — organisation, influence, access maps, and process

**What this is**: Blank's Customer Validation Phase 1 toolkit applied to AgentGuard's two paying segments (beachhead and edge-high) — who sits where in the buying org, who actually sways the decision, how a stranger reaches them, and the sales process with the artifact needed at each step.

**Why it exists**: `strategy/personas.md` names individuals; this document is what turns "we'll sell to security teams" into an answer for who signs — the exact gap `references/grill-question-bank.md` §2 calls out, and the reason a GTM plan without this document hides whether anyone has actually mapped the buying committee. The failure this document prevents: a 90-day motion (`strategy/gtm.md`) that assumes Marcus alone can approve a purchase when in reality someone else has to sign off, discovered only after the sales cycle stalls.

**How to read it**: the access map is the most actionable section — it's the literal list of how a stranger (this venture, with zero traction) reaches each buyer type without an existing relationship. A skeptic should check whether the access map actually reflects the zero-traction starting point (`ASSUMPTIONS.md` Restated hard facts) rather than assuming warm intros that don't exist yet.

**Depends on / feeds**: built from `strategy/personas.md`. Feeds `strategy/gtm.md`'s 90-day motion and `validation/decision_making_unit.md` (phase 6), which formalizes user/payer/champion/saboteur roles from the maps here.

---

## Beachhead segment (Marcus's org)

### Organisation map

At a mid-size company with a small (≈4-person) security team reporting into a larger engineering org:

- **Marcus** (senior security engineer) — hands-on user, initiates evaluation, no purchase authority above a small discretionary threshold.
- **Marcus's manager** (Head of Security or VP Engineering, depending on company size) — approves spend above Marcus's discretionary threshold; at the $750–$2,500 per-transaction price point (`strategy/market_sizing.md`), this may fall entirely within Marcus's own approval authority, which is the key structural advantage of this segment's low unit price.
- **Product/Engineering lead** for the specific agent being evaluated — not a purchase approver, but the stakeholder whose release timeline creates the triggering pain moment (`strategy/personas.md`'s Marcus card).

### Influence map

- **Marcus himself** is the primary influencer — at this price point, he can plausibly be both user and approver, collapsing the traditional user/champion/economic-buyer distinction that matters more at the enterprise tier.
- **Product/Engineering lead** has secondary influence — if the release timeline pressure they create is the trigger, they indirectly drive Marcus's urgency without being part of the purchase decision itself.

### Access map

Given zero existing relationships or brand awareness (`ASSUMPTIONS.md` Restated hard facts), a stranger reaches Marcus through:

1. **The free-tier OSS scanner**, discovered via GitHub/developer search when Marcus is already looking for exactly this kind of tool (`strategy/channel_plan.md`'s primary beachhead channel).
2. **Security community spaces** (DEF CON AI Village-adjacent forums, HackAPrompt-adjacent communities, `research/sources.md` S140–S143) where security engineers like Marcus already spend time professionally.
3. **Methodology-transparency content** shared within security-engineering circles (blog posts, conference talks) that Marcus's own professional network surfaces to him.

### Sales process and artifacts needed at each step

| Step | Artifact needed |
|---|---|
| 1. Discovery (Marcus finds AgentGuard) | Free-tier product itself — no sales artifact required, the product is the pitch |
| 2. First campaign run (self-serve) | In-product documentation walking through interpreting a Comparison Report |
| 3. Decision to pay for a full Comparison Report | The free-tier result itself, demonstrating value on a sample/toy target — no separate sales deck needed at this price point |
| 4. Attach to release risk-assessment process | An exportable report format Marcus can attach directly to an internal ticket (a concrete `product/ux_spec.md` requirement, also surfaced in `strategy/value_prop_canvas.md`) |

## Edge-high segment (Elena's and David's org)

### Organisation map

At a large enterprise with a dedicated AI red-team function reporting to a CISO:

- **Elena** (Head of AI Red Team) — hands-on user, evaluates tools against her team's existing capability, no final budget authority above her team's line-item budget.
- **David** (CISO) — economic buyer; approves spend beyond Elena's discretionary authority, cares about board/audit defensibility (`strategy/personas.md` card 4) more than technical mechanism detail.
- **Procurement/vendor-risk function** — not modeled as an individual persona here, but a real gate at this company size: a new vendor (especially a pre-traction, 4-person capstone-origin one) must clear a vendor-risk review before any contract, a step the beachhead segment's low unit price largely avoids.
- **Sofia**-type buyer (agent-platform vendor's Trust & Safety lead) — a structurally similar but distinct org: Sofia likely reports to a CPO/Chief Trust Officer rather than a CISO, and her Trust & Safety function's budget is closer to a product-risk line than a pure security line item.

### Influence map

- **Elena** is the technical champion — her endorsement is necessary but not sufficient; she cannot unilaterally approve spend at this org size.
- **David** is the actual economic buyer and the person `strategy/personas.md` identifies as needing certification-grade evidence (ISO 42001-aligned reporting) more than technical depth — his sign-off is the binding constraint.
- **Procurement/vendor-risk** is a potential **saboteur** role (Blank's term, formalized in `validation/decision_making_unit.md`) — a pre-traction vendor with zero customer references is a plausible rejection point independent of product quality, and this risk should be named explicitly rather than assumed away.

### Access map

Given zero existing relationships and the credibility gap named in `strategy/personas.md` card 4:

1. **Not reachable via cold outbound at this stage** — `strategy/gtm.md`'s 90-day motion explicitly defers the first edge-high conversation to after beachhead traction exists.
2. **Reached via published research credibility** — a methodology paper, conference talk, or public comparison-report example that Elena's team (which already engages with academic security research, per her persona's PhD background) would plausibly encounter independent of any sales outreach.
3. **Reached via beachhead-customer referral** — once beachhead customers exist, a referral from a peer security engineer at another company carries more access-opening weight than any direct outreach this venture could make unassisted.

### Sales process and artifacts needed at each step

| Step | Artifact needed |
|---|---|
| 1. Elena becomes aware (via research credibility or referral) | Published methodology documentation, not a sales deck |
| 2. Elena evaluates technically | A pilot Comparison Report run against a real (staging) target agent from her org — requires a guided or semi-guided onboarding, unlike the beachhead's zero-touch motion (`strategy/business_model_canvas.md`'s Customer Relationships hypothesis explicitly tests whether this guided step is actually necessary) |
| 3. Elena champions internally to David | An audit/board-ready report export (ISO 42001-aligned format, per `strategy/value_prop_canvas.md`) Elena can hand to David directly |
| 4. David approves, procurement/vendor-risk reviews | Vendor-risk documentation this venture does not yet have (references, security posture of AgentGuard itself, business continuity assurance) — **named here as a real gap, not glossed over**: a 4-person capstone-stage venture will struggle to clear a formal enterprise vendor-risk review, and this should be treated as a genuine blocker for edge-high sales in year one, not a solvable-with-a-good-pitch problem |

## Recommended next 3

1. **Treat the edge-high procurement/vendor-risk saboteur risk as a hard constraint on year-one edge-high revenue expectations**, not a detail — `financials/revenue_build.md` should weight edge-high revenue conservatively (or at zero) for year one given this gap, consistent with `strategy/market_sizing.md`'s SOM being sized off the beachhead, not the enterprise tier.
2. **Formalize both organisation maps into `validation/decision_making_unit.md`'s user/payer/champion/saboteur framework** (phase 6) — this document supplies the raw mapping; that artifact should assign the formal DMU roles.
3. **Test the beachhead segment's "Marcus can be both user and approver" assumption directly in the first 3 paid purchases** (`strategy/gtm.md`'s day 31–60 target) — if a second approver turns out to be required even at this low price point, the sales-process artifacts above (and the zero-touch channel economics in `strategy/channel_plan.md`) both need revision.
