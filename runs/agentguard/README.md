# AgentGuard

An adaptive red-team/blue-team evaluation platform that runs the same budget-matched, feedback-only adaptive attack campaign against each of a target agent's candidate defenses and reports attack success and legitimate-task utility side by side — the standing, reproducible cross-defense comparison that neither the academic adaptive-attack literature (e.g. AutoDojo) nor proprietary red-teaming vendors (e.g. Adversa AI) currently publish. This originates as a CMPE 295A/295B graduate capstone project at San José State University (4-person team, two semesters); the startup framing is a positioning exercise on real research work, not a claim of an existing company. No implementation exists yet, and the venture has zero traction — no customers, revenue, funding, or pilots.

## Status

**PARTIAL — updated 2026-09-09.** **57/61 required artifacts present (93%)** per `audit/COVERAGE.md`, counted from the glob, not memory. Phases complete: **0 (Brief), 1 (Research), 2 (Strategy), 3 (Product), 4 (Tech), 5 (Narrative), 6 (Validation), 7 (Financials), 9 (Audit)**. **Phase 8 (Visuals) was explicitly skipped** — the 4 missing required rows (`visuals/visual_manifest.md`, `visuals/infographics/*.html`, `visuals/image_prompts.md`, `visuals/docimages.json`) are the entirety of the gap, not an oversight. Phase 10 (Website) follows this README's own publish.

**Disclosed gap, not hidden: no critic loop ran on phases 3–7.** Only Strategy (phase 2) completed the full three-persona adversarial critic loop. Product, Tech, Narrative, Validation, and Financials were generated under explicit deadline pressure with each phase's own internal check against `references/quality-bar.md`, plus one targeted integration check that confirmed the highest-risk failure mode — illustrative journey/demo numbers being mistaken for real campaign results — is handled correctly everywhere ("design-only, nothing has actually run" is stated explicitly at every occurrence). Beyond that specific check, these five phases have not had an adversarial pass and should not be treated as equally hardened as Strategy. `audit/COVERAGE.md` also logs one mechanical property-0 fix row (the ten architecture diagrams compress their orientation block onto one line instead of four) — cosmetic, not a content gap.

**The wedge changed since phase 1, and stayed changed.** Research found AgentGuard's original claim ("we automate the adaptive adversary") already occupied by academic prior art (AutoDojo) and a commercial vendor (Adversa AI). The founder rejected three proposed replacements and resolved it (`ASSUMPTIONS.md` A9): AgentGuard's differentiator is **the comparison, not the attacker**. Every phase since is built around this resolution.

## Start here

1. [`BRIEF.md`](BRIEF.md) — the founder brief: problem, wedge, users, business model, riskiest assumption, year-one scope, vocabulary.
2. [`narrative/one_pager.md`](narrative/one_pager.md) — the single-page version of the whole pack.
3. [`narrative/vc_memo.md`](narrative/vc_memo.md) — the full technical-investor case, including the honest risks section.

## Reading paths by audience

- **Investor**: [`narrative/one_pager.md`](narrative/one_pager.md) → [`narrative/vc_memo.md`](narrative/vc_memo.md) → [`narrative/pitch_deck.md`](narrative/pitch_deck.md) → [`financials/unit_economics.md`](financials/unit_economics.md) — the deck's own "Recommended next 3" says plainly not to present it as a funding pitch given zero traction; treat the ask as design-partner/feedback-scoped.
- **Engineer / builder**: `BRIEF.md` → `research/capability_table.md` → `tech/whitepaper.md` → `tech/deep_dives.md` → `tech/architecture/00_INDEX.md` → `product/PRD.md` → `tech/not_vaporware.md`.
- **Operator / GTM**: `strategy/market_type.md` → `strategy/positioning.md` → `strategy/gtm.md` → `financials/pricing.md` → `validation/stage_gate.md` → `validation/riskiest_assumptions.md`.
- **Researcher / skeptic**: `research/sources.md` (154 numbered citations) → `audit/CITATIONS.md` → `audit/COVERAGE.md` → `research/competitors.md` → `ASSUMPTIONS.md` A9 → `strategy/positioning.md`.

## Full artifact map

| Path | What it holds | File count | Owning skill |
|---|---|---|---|
| `BRIEF.md`, `ASSUMPTIONS.md` | Founder brief and logged assumptions (9 tracked, A9 resolved) | 2 | grill-me |
| `research/` | Landscape, competitor teardown, capability table, survey, 154-entry sources list | 5 | startup-research |
| `strategy/` | 11 artifacts — critic-loop hardened (3 rounds) | 11 | startup-strategy |
| `product/` | PRD, flagship + prioritized features, 4 journeys, UX spec | 8 | startup-product |
| `tech/` | Whitepaper (honest 3x–30x range, not a forced 10x), deep dives, 10 architecture diagrams + index, 2 technique waves (37 sourced techniques), decision tree, technique/feature matrix, not-vaporware | 17 | startup-tech |
| `narrative/` | One-pager, VC memo, 14-slide deck, future press release, founder story, mission/vision | 6 | startup-narrative |
| `validation/` | Full Blank board — 9 artifacts, every experiment "planned," none fabricated | 9 | startup-validation |
| `financials/` | Pricing (founder-signed-off, illustrative), revenue build, unit economics (margin reuses `tech/not_vaporware.md`'s cost derivation verbatim), use of funds (explicitly hypothetical, no active raise), risk matrix, comps & exits | 6 | startup-financials |
| `audit/` | Citation audit (90 sources checked, 12 corrected) + manifest coverage (this pass) | 2 | startup-audit |

Not yet generated: `visuals/` (skipped per instruction), `index.html` / site (this README's next update).

## Visual index

None rendered — visuals phase explicitly skipped this run.

## Top 5 sharpest claims

1. **The adaptive-vs-static gap is real and large where measured**: a NIST/UK AI Security Institute human red-teaming exercise found hijack success rising from 11% to 81% — a 7x jump (`research/sources.md` S27).
2. **The status quo fails at a measurable, quantified rate**: 88% of organizations report a confirmed or suspected AI-agent security incident in the past year (S150, Gravitee, vendor-sourced); orgs with over-privileged AI report a 76% incident rate vs. 17% for least-privilege deployments, a 4.5x gap (S154, Teleport, vendor-sourced) — both vendor-commissioned, read as convergent signal, not audited ground truth.
3. **The differentiation is the comparison, not the attacker**: no source found in research publishes a standing, budget-matched, utility-paired comparison across defense families (`strategy/positioning.md`).
4. **Gross margin is not the constraint on the founder-confirmed pricing** ($750 single-defense / $2,500 four-defense report, both `(assumption: illustrative, not final)`): inference cost runs ~92-99.5% margin depending on model tier — willingness-to-pay is the open question, not cost (`financials/unit_economics.md`).
5. **This is a graduate capstone with zero traction, stated plainly everywhere it matters, including in the money**: `financials/use_of_funds.md` states outright no raise is active; any paid customer is told upfront this is a research-stage engagement with no guarantee beyond the program's end (`strategy/gtm.md`).

## Completeness

**PARTIAL.** 57/61 required artifacts present. Phases 0–2 are critic-loop hardened; phases 3–7 are complete but have not had an adversarial critic pass (see Status above for the one targeted check that did run). Visuals (phase 8) was explicitly skipped. See `audit/COVERAGE.md` for the row-by-row manifest table, the property-0 mechanical check, and the priority draw order for what remains.
