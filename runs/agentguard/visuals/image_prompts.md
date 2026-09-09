# Image prompts

**What this is**: text-to-image prompts for the 4 visuals built as HTML this pass, written so they could be rendered as PNGs later if an image tool becomes available — plus a note on which rows should *not* be converted to images even then.

**Why it exists**: `references/artifact-manifest.md` A51 requires this file regardless of whether rendering happens this session; per its own A50 guidance, image models render pictures well and text badly — writing the prompt now, honestly scoped to what a picture (not a data table) can carry, avoids the trap of prompting for something only HTML can actually deliver.

**How to read it**: two of the four rows (V01, V04) are explicitly marked "do not convert to image" — their content is exact numbers a reader must transcribe, which is precisely the case A50 reserves for HTML, not art. Only V02 and V03 have real prompts, because only those two are genuinely picture-shaped.

**Depends on / feeds**: built from `visuals/visual_manifest.md`. Nothing downstream depends on this file existing beyond the manifest's own completeness.

---

## V01 — Matched-budget cross-defense comparison table

**Do not convert to image.** The content is a 4-row × 5-column table of exact percentages and round numbers a reader must be able to transcribe and check — this is precisely the case `references/artifact-manifest.md`'s A50 rule reserves for HTML, never art. No prompt written.

## V02 — The adaptive-vs-static gap (11%→81%)

**Prompt**: *Editorial minimalism, two vertical bars of dramatically different height side by side against a plain white background, the taller bar in a single confident indigo tone, the shorter bar in a pale muted grey, generous negative space, precise geometric shapes, no letters, no words, no numbers, no labels, no watermark, no UI chrome with readable type, one clean horizontal baseline. The composition should read as "before vs. after" at a glance without any text.*

Text-free per the hero-imagery rule (`skills/startup-website`) — all numeric labels stay in the HTML overlay, not baked into the image itself, so nothing can garble.

## V03 — Positioning two-axis quadrant

**Prompt**: *A precise 2×2 grid of thin hairline dividers on white, one quadrant filled with a soft indigo tint and the other three left white, abstract geometric dots of varying sizes scattered across the quadrants suggesting a competitive landscape map, minimal and architectural, generous negative space, no letters, no words, no numbers, no labels, no watermark, no UI chrome with readable type. Editorial, precise, restrained — a diagram, not a decoration.*

Entity names and axis labels stay in the HTML overlay per the same text-free discipline.

## V04 — Pricing tiers ladder

**Do not convert to image.** The content is three exact dollar figures and their feature lists — a reader must be able to read and compare them precisely, which is exactly what image models render badly. No prompt written; the HTML tier cards are the complete, correct form for this row.

## Recommended next 3

1. **If an image tool becomes available, render V02 and V03 first** — they are the only two rows in this file with real prompts, and both are genuinely picture-shaped rather than data that needs to stay text.
2. **Do not write a prompt for V01 or V04 even under time pressure later** — both are explicitly the wrong content type for an image, not merely deprioritized.
3. **Write prompts for V07 (revenue ladder) once built as HTML** — it is chart-shaped like V02 and would benefit from the same treatment if this pack's visual layer is extended further.
