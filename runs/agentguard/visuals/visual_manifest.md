# Visual manifest

**What this is**: every visual candidate identified across the pack, its Form classification (HTML vs. image, per `references/artifact-manifest.md`'s A50 rule), and its status — built or deferred.

**Why it exists**: `references/quality-bar.md` property 0 requires every substantive artifact to carry illustration where one earns its place; this document is the single place that classification and build status is tracked, so the pack's visual coverage can be checked mechanically rather than assumed.

**How to read it**: the Status column is the point. 4 of 10 identified candidates are built this pass, chosen for decision-relevance (the mechanism, the core evidence stat, the positioning argument, the pricing) rather than breadth-for-its-own-sake — per explicit instruction, fewer good visuals beat a padded manifest.

**Depends on / feeds**: built from a fresh read of `BRIEF.md`, `research/sources.md`, `strategy/positioning.md`, and `financials/pricing.md`. Feeds `visuals/docimages.json` and `README.md`'s Visual index.

---

## Target count and constraint

**No image-rendering tool is available this session** (A52 explicitly skipped). Every visual below is therefore HTML regardless of its "natural" A50 classification — a chart-shaped row that would normally wait for a PNG is built as an HTML infographic instead, because HTML is the only rendering path this session actually has. This is stated once here rather than repeated per row.

**10 candidates identified, 4 built, 6 deferred** (2 already covered by an existing Mermaid/ASCII diagram in their source document, 4 flagged as the next-build queue).

## Manifest

| ID | Row | Form (A50 classification) | Source document(s) | Status |
|---|---|---|---|---|
| V01 | Matched-budget cross-defense comparison table | Needs HTML — a table whose exact numbers must be transcribable | `product/journeys/beachhead.md`, `BRIEF.md` Wedge & Mechanism, `strategy/positioning.md` | **Built** — `visuals/infographics/V01_matched_budget_comparison.html` |
| V02 | The adaptive-vs-static gap (11%→81%) | Chart-shaped (would not need HTML with an image tool available); built as HTML here for lack of one | `research/sources.md` S27 | **Built** — `visuals/infographics/V02_adaptive_gap.html` |
| V03 | Positioning two-axis quadrant | Chart-shaped, but carries many named entities whose labels must be exactly transcribable — needs HTML on that basis independent of the no-image-tool constraint | `strategy/positioning.md` | **Built** — `visuals/infographics/V03_positioning_quadrant.html` |
| V04 | Pricing tiers ladder | Chart-shaped; built as HTML here for lack of an image tool | `financials/pricing.md` | **Built** — `visuals/infographics/V04_pricing_tiers.html` |
| V05 | Configure → Attack → Observe → Adapt → Report core loop | Does not need HTML — `tech/architecture/D01.md` already ships this as a live Mermaid diagram; an HTML poster would duplicate it | `product/PRD.md` §1, `tech/architecture/D01.md` | Not built — already covered by an existing Mermaid diagram, per the manifest's own rule against duplicating one |
| V06 | Petal diagram, adjacent markets | Does not need HTML — `strategy/petal_diagram.md` already ships an ASCII diagram inline | `strategy/petal_diagram.md` | Not built — already covered |
| V07 | Revenue build stages ($1M → $10M → $50-100M) | Chart-shaped (a ladder/funnel) | `financials/revenue_build.md` | Deferred — next-build queue |
| V08 | Technique waves poster (37 named techniques) | Needs HTML — a poster enumerating many named items | `tech/techniques/wave1.md`, `wave2.md` | Deferred — next-build queue, likely the highest-value of the four deferred rows given the sheer count of named items a reader currently has to read as prose |
| V09 | Risk matrix heat table | Needs HTML — a table with many cells | `financials/risk_matrix.md` | Deferred — next-build queue |
| V10 | Persona spectrum card wall (5 personas) | Needs HTML — a card wall carrying prose per panel | `strategy/personas.md` | Deferred — next-build queue |

## Recommended next 3

1. **Build V08 (technique waves poster) next** — 37 named techniques currently live only as prose tables; a poster is the highest-leverage remaining row for a skimming reader.
2. **Wire `pack.html`'s reader to actually display these 4 images inline per document**, per the website skill's "put the visuals in the documents" requirement — `visuals/docimages.json` already has the mapping; the reader does not yet consume it (out of scope for this pass, which was visuals-only with no changes to existing files beyond what this phase itself creates).
3. **Revisit V05/V06's "does not need HTML" call if either source diagram is ever simplified or removed** — the exemption is conditional on the Mermaid/ASCII diagram continuing to exist, not a permanent classification.
