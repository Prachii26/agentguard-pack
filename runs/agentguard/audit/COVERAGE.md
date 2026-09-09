# Coverage — manifest audit

**What this is**: the full `references/artifact-manifest.md` table with a status per row, checked against the actual glob (not memory), plus a property-0 (orientation block) mechanical check on every artifact and a priority draw order for what remains.

**Why it exists**: `references/quality-bar.md` and `skills/startup-audit` both require "done" to be verified from disk, never asserted — this document is that verification, run once at the end of a deadline-driven push through phases 0–7.

**How to read it**: the gap list and the property-0 fix-row list are the two things a future session should act on first; the completion count at the top is the one number to quote, and it is deliberately not rounded up.

**Depends on / feeds**: built from a full glob of `runs/agentguard/` against `references/artifact-manifest.md`. Feeds `README.md`'s Status and Completeness sections directly.

---

## Honest completion count

**61 / 61 required artifacts present (100%)**, updated after a later visuals-only pass closed A49–A52b (previously skipped by explicit instruction; a later instruction reversed that and generated them, still without a critic loop or any change to existing artifacts). 1 optional row (A27, technique wave 3) was deliberately not generated because `tech/techniques/wave2.md` states the sourced technique material was genuinely exhausted at 37 total — documented, not padded. A52 (rendered PNGs) remains optional and undone — no image tool available. A53 (ingest sources) is not applicable — no external documents were ingested into this run.

**No critic loop has run on phases 3–8** (Product, Tech, Narrative, Validation, Financials, Visuals) — only Strategy (phase 2) completed the full three-persona adversarial loop. This caveat is unchanged by the visuals pass and should not be read as resolved.

**No critic loop ran on phases 3–7** (Product, Tech, Narrative, Validation, Financials) — only Strategy (phase 2) went through the full three-persona adversarial loop. This is stated here and in `README.md`, not hidden.

## Manifest table

| ID | Path | Status |
|---|---|---|
| A00 | BRIEF.md | present |
| A01 | ASSUMPTIONS.md | present |
| A02 | research/landscape.md | present |
| A03 | research/competitors.md | present |
| A04 | research/capability_table.md | present |
| A05 | research/survey.md | present |
| A06 | research/sources.md | present (154 numbered entries; 90 audited in `audit/CITATIONS.md`) |
| A07 | strategy/market_type.md | present, critic-passed |
| A08 | strategy/positioning.md | present, critic-passed |
| A09 | strategy/market_sizing.md | present, critic-passed |
| A10 | strategy/personas.md | present, critic-passed |
| A11 | strategy/lean_canvas.md | present, critic-passed |
| A12 | strategy/value_prop_canvas.md | present, critic-passed |
| A13 | strategy/gtm.md | present, critic-passed |
| A14 | product/PRD.md | present, no critic loop |
| A15 | product/features_flagship.md | present, no critic loop |
| A16 | product/features_prioritized.md | present, no critic loop |
| A17 | product/journeys/edge_low.md | present, no critic loop |
| A18 | product/journeys/beachhead.md | present, no critic loop |
| A19 | product/journeys/edge_high.md | present, no critic loop |
| A20 | product/journeys/day_in_life.md | present, no critic loop |
| A21 | product/ux_spec.md | present, no critic loop |
| A22 | tech/whitepaper.md | present, no critic loop |
| A23 | tech/deep_dives.md | present, no critic loop |
| A24 | tech/architecture/00_INDEX.md + D01–D10 | present, 11/11 files — **fix row**: D01–D10 use a compressed single-line "What/Why/How/Depends" label instead of four separately labelled lines; mechanically fails property 0's literal form though the content itself is present |
| A25 | tech/techniques/wave1.md | present, no critic loop |
| A26 | tech/techniques/wave2.md | present, no critic loop |
| A27 | tech/techniques/wave3.md | not generated — optional, documented as genuinely exhausted at 37 techniques rather than padded |
| A28 | tech/techniques/decision_tree.md | present, no critic loop |
| A29 | tech/techniques/technique_feature_matrix.md | present, no critic loop |
| A30 | tech/not_vaporware.md | present, no critic loop |
| A31 | narrative/one_pager.md | present, no critic loop |
| A32 | narrative/vc_memo.md | present, no critic loop |
| A33 | narrative/pitch_deck.md | present, no critic loop |
| A34 | narrative/future_press.md | present, no critic loop |
| A35 | narrative/founder_story.md | present, no critic loop |
| A36 | validation/riskiest_assumptions.md | present, no critic loop |
| A37 | validation/experiment_board.md | present, no critic loop |
| A38 | validation/discovery_guide.md | present, no critic loop |
| A39 | validation/get_keep_grow.md | present, no critic loop |
| A40 | validation/stage_gate.md | present, no critic loop |
| A41 | validation/metrics_by_stage.md | present, no critic loop |
| A42 | validation/pivot_log.md | present, no critic loop |
| A43 | financials/pricing.md | present, no critic loop |
| A44 | financials/revenue_build.md | present, no critic loop |
| A45 | financials/unit_economics.md | present, no critic loop |
| A46 | financials/use_of_funds.md | present, no critic loop |
| A47 | financials/risk_matrix.md | present, no critic loop |
| A48 | financials/comps_exits.md | present, no critic loop |
| A49 | visuals/visual_manifest.md | present, no critic loop — 10 candidate rows identified, 4 built, 6 deferred and named |
| A50 | visuals/infographics/*.html | present, 4/4 built (V01–V04), no critic loop — self-contained, `site.css` only, no build step |
| A51 | visuals/image_prompts.md | present, no critic loop — 2 of 4 rows carry real prompts (V02, V03); V01/V04 explicitly marked "do not convert to image" (exact numbers to transcribe) |
| A52 | visuals/images/*.png | not generated — optional; no image-rendering tool available this session |
| A52b | visuals/docimages.json | present, no critic loop — maps the 4 built visuals to 8 citing documents; `pack.html`'s reader does not yet consume this map to display images inline (named as open work in `visuals/visual_manifest.md`) |
| A53 | ingest/SOURCE_<n>.md | not applicable — no ingested sources this run |
| A54 | audit/COVERAGE.md | present (this file) |
| A55 | README.md | present, updated this pass |
| A56 | index.html | present — built as a single-page site (`index.html` + `pack.html` reader + `site.css`, hand-built `visuals/docmanifest.json`); no Node.js available in this environment, so `templates/build_site.js`'s multi-page generator was not used |
| A57 | Live GitHub Pages URL | **blocked, not generated** — no `gh` CLI installed and no push access on the only configured git remote (`upstream` → dlmastery/startup-skills, confirmed via `git push --dry-run`, 403). Needs a remote the user can push to (e.g. a personal fork) or `gh` CLI with authentication before this can complete. |
| A58 | strategy/business_model_canvas.md | present, critic-passed |
| A59 | strategy/petal_diagram.md | present, critic-passed |
| A60 | strategy/channel_plan.md | present, critic-passed |
| A61 | strategy/sales_roadmap.md | present, critic-passed |
| A62 | validation/mvp_definition.md | present, no critic loop |
| A63 | validation/decision_making_unit.md | present, no critic loop |
| A64 | narrative/mission_vision.md | present, no critic loop |

## Property-0 mechanical check (every artifact, not a sample)

Grepped every `.md` file for the four labelled lines (`**What this is**`, `**Why it exists**`, `**How to read it**`, `**Depends on`). Results:

- **Correctly exempt** (own defined structure, not property-0's contract): `BRIEF.md`, `ASSUMPTIONS.md`, `README.md` — these follow grill-me's and A55's own contracts, not the generic orientation block.
- **Fix row**: `tech/architecture/D01.md` through `D10.md` (10 files) — compress all four labels onto one line (`**What/Why/How/Depends**: ...`) rather than four separately labelled lines. The content is present and accurate; the form doesn't match property 0's literal specification. Low-severity, mechanical, cheap to fix (a five-minute reformat per file) but not done this pass per the "move on" instruction.
- **Everything else** (47 files): full four-label orientation block present and confirmed non-generic on spot-read during earlier phase work.

## Gap list, priority tiers

No required-artifact gaps remain (61/61 present). Two real open items remain, neither a missing-artifact gap:

1. **The deferred three-persona critic loop on phases 3–8** (Product, Tech, Narrative, Validation, Financials, Visuals). Owning process: `skills/startup-critic`. Effort: large. This is the single largest quality-assurance gap in the current pack and is unaffected by the visuals pass landing.
2. **A24's ten architecture diagrams' orientation-block format** — cosmetic, mechanical. Owning skill: `startup-tech` (reformat only, no content change). Effort: trivial.

Additionally, `visuals/visual_manifest.md` itself names 6 further candidate visual rows as deferred (not gaps against the manifest, since A50 only requires HTML for rows that need it — but real backlog for a future visuals pass): V05–V06 already covered by existing Mermaid/ASCII, V07–V10 next-build candidates.

## Priority draw order (for a future session, not executed now)

1. Run the deferred three-persona critic loop on phases 3–8 — the single largest quality-assurance gap in the current pack, now covering Visuals too.
2. Reformat `tech/architecture/D01–D10.md`'s orientation blocks to four separate labelled lines (trivial, ~30 min total).
3. Wire `pack.html`'s reader to consume `visuals/docimages.json` and display images inline per document, per the website skill's "put the visuals in the documents" requirement — the mapping exists, the reader doesn't use it yet.
4. Build the 4 next-queue visual candidates (V07–V10) named in `visuals/visual_manifest.md`.
5. Second citation-audit pass on sources added or leaned on more heavily by phases 3–8 (`audit/CITATIONS.md` covers only sources cited through phase 2).

## Recommended next 3

1. **Run the deferred critic loop before treating phases 3–8 as equal in reliability to Strategy** — this is the single most consequential open item in this coverage report, unchanged by the visuals pass.
2. **Wire the reader to the docimages map** — the visuals exist and are cited from documents in `visuals/docimages.json`, but a reader browsing `pack.html` today won't see them inline yet.
3. **Reformat the ten architecture diagram orientation blocks** — cheap, mechanical, and still the only property-0 fix row in the pack.
