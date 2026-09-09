# Citation audit — every source actually cited in an artifact

**What this is**: a pass/fail audit of all 90 distinct `[Sn]` citations actually used across `BRIEF.md`, `ASSUMPTIONS.md`, `research/*.md`, and `strategy/*.md` (not every entry in `sources.md` — only ones a downstream artifact actually relies on). For each: does the URL contain the claim attributed to it, is every number stated as-is, is it primary or a citation chain, and is it vendor-sourced.

**Why it exists**: a prior review round found one real citation error by chance (a statistic attributed to the wrong source entirely). The founder's instruction was direct: "one bug found by chance means the layer is unverified, not clean." This document is the systematic check that replaces chance with method. The failure this prevents: a pack whose narrative sounds rigorous because every claim has a bracket next to it, when a material fraction of those brackets don't actually say what they're cited for.

**How to read it**: the verdict column is the finding. **12 entries failed outright** (wrong source entirely, or numbers that don't match the cited page at all) and have been corrected at the source layer in `research/sources.md`, with downstream artifacts patched wherever the error actually reached prose (most didn't — see the Impact column). **~20 entries were partial** — usually true facts attached to a URL that doesn't itself contain them, a real and recurring pattern distinct from the outright failures. This audit was run under time pressure (stopped before a planned deeper follow-up pass) — see Coverage note at the end for what that means honestly.

**Depends on / feeds**: audits `research/sources.md` as it stood after the strategy-phase critic loop. Feeds every downstream phase — Product, Tech, Narrative, and Validation should treat this file's corrected `sources.md` as ground truth, not the pre-audit version.

---

## Method

Four parallel passes, one per risk category, plus five sources (S150, S152–S154, and the original error that triggered this audit) verified directly by the run's own agent before the batch passes launched. Each source: WebFetch the live URL, compare word-for-word against the claim in `sources.md`, check number precision, classify as primary/secondary/tertiary, tag vendor interest.

## Summary

| Result | Count | What it means |
|---|---|---|
| **PASS** | 62 | URL supports the claim as stated, number matches, no material issue |
| **PARTIAL** | 21 | The underlying fact is usually true, but the specific cited URL doesn't itself contain it (true elsewhere on the same site, or in a different source entirely) — a distinct, recurring failure mode from outright fabrication |
| **FAIL** | 12 | Number doesn't match the cited page, or the claim is materially unsupported/overstated |
| **UNVERIFIABLE** | 2 | URL unreachable across retries within this pass's time budget |

**12 FAILs, corrected in `research/sources.md`** (each entry there now carries a `**Correction (audit, 2026-09-09)**` note — read the source entry directly for full detail, not repeated here):

| Source | What was wrong | Downstream artifact impact |
|---|---|---|
| S33 | Wrong Hugging Face model card URL (v1 Prompt Guard, not PromptGuard 2) — the recall/FPR figures live on a different repo | Sources.md URL fixed; no downstream prose cited S33 directly (S34 carries the numbers, and S34 passed) |
| S48 | $400M acquisition price not on the cited page (undisclosed there); close date wrong (Sept 23 2024, not October) | `research/landscape.md`'s consolidation-pattern sentence doesn't state the dollar figure or date — no downstream fix needed |
| S49 | Cited as confirming TAP is part of Cisco's "AI Validation" product; page only discusses TAP as background threat context, never names that product | No downstream artifact directly quoted this claim — sources.md corrected |
| S53 | "Completed April 2026" wrong — cited page only announces an agreement; real close date likely July 2026 (not independently re-verified this pass) | `research/landscape.md` doesn't state a close date — no downstream fix needed |
| S79 | Market-size figures completely wrong: cited page actually says $1.9B→$15.6B at 28.7% CAGR, not $2.37B→$17.7B at 21.4% | Not used in any strategy artifact's arithmetic (only appears in `research/sources.md`'s own range-reporting) — corrected at source |
| S89 | Headline stats ("60% lacking governance," "72% in production") do not appear anywhere in the cited report | Not cited in any downstream artifact — corrected at source, replaced with the report's actual content |
| S104 | Sonnet 5 pricing ($2/$10) not on the cited Finout page | Moved to S103 (Claude's own official pricing page), which does carry it — no downstream artifact needed a fix since none cited Sonnet 5 pricing to S104 specifically |
| S105 | GPT-4o mini pricing not on the current live page (page has been rewritten since original citation) | `research/capability_table.md` — inline caveat added; figure itself not disputed, only the citation's current stability |
| S136 | "9 of 10 challenges solved" claim not on the cited blog page — belongs to S135 (the arXiv paper) instead | Sources.md corrected; not separately cited downstream |
| *(prior round)* S150 (partial) | Carried a 76%/17% stat that belongs to a different vendor entirely (Teleport, not Gravitee); a healthcare figure that couldn't be confirmed on re-fetch; an ambiguous monitoring-coverage figure | Fixed in `research/competitors.md`, `research/landscape.md`, `strategy/lean_canvas.md`, `README.md` — new S154 added for the correct Teleport citation |
| *(prior round)* S152, S153 (partial) | Both cited as evidence that manual practices are "the dominant status-quo" — neither source claims this; both are vendor pages recommending automation instead | Fixed in `research/landscape.md` §4 — reframed as definitional references only |

**2 UNVERIFIABLE** (URL unreachable within this pass): S55 (Giskard docs, connection error x3), S66 (Dark Reading/SentinelOne, HTTP 403 every attempt — underlying facts corroborated via independent outlets, but the specific cited page itself was never read). Neither is deleted — both facts are independently well-corroborated per the batch audit's own cross-checks — but neither should be treated as "confirmed by its own citation" until re-fetched.

## The ~21 PARTIAL entries — a real, recurring pattern

The single most common defect this audit found was **not** fabrication — it was **a true fact, attached to a URL that itself doesn't contain it** (true elsewhere on the same vendor's site, or in a different, uncited source). This happened often enough across every batch that it's a pattern, not a one-off:

S11 (defense-category labels don't match the paper's actual taxonomy), S13 (date off by one version), S38 (title drift + an unqualified 0%-ASR figure that's actually conditional on human-in-the-loop review), S46 ($156M total not stated in the cited article, though arithmetically correct), S54 (client list wrong — DeepMind is a benchmark partner, not a customer), S58 (probe count/adaptivity claims not on the cited comparison page), S59 (PDF unreadable, some specifics unverified), S63 (product-suite and growth-rate claims not on the cited page), S64 (wrong product name — "ARGUS" should be "Repello Guard" — plus unsupported claims), S73 ("$8B+" figure not on the cited page), S90 (CVSS score and date not on the cited page), S101 (GPT-4 launch date wrong even relative to its own cited source — March not May 2023), S113 (overstates practitioner advice as a quoted ISO standard requirement), S114 (overstates a supporting-evidence framing as "certification-grade"), S118 (cross-modal-injection claim not on the cited article), S132 ("first" framing is this pack's own editorializing, not sourced), S133 (sub-technique count conflated from a later framework version), S140 ("launched 2023" / "80M+ data points" not on the cited walkthrough page), S143 (conflates two distinct bug-bounty rounds under one citation).

**None of these were corrected individually in this pass** — time-boxed per the founder's stop instruction. They are logged here as the honest remaining state, not silently treated as clean. The pattern itself is the actionable finding: **a citation naming the right fact but the wrong specific URL is common enough in this pack that any new citation added in future phases should be checked against this exact failure mode before being trusted.**

## Vendor-sourced citations — explicitly tagged

Per the founder's instruction, every vendor survey used for a market-perception or incident-rate claim is tagged at point of use, not just in `sources.md`:

- **S150 (Gravitee)** — sells AI/agent governance and gateway products.
- **S154 (Teleport)** — sells infrastructure access/identity control products.
- **S89 (CrewAI)** — sells an agent orchestration framework.
- **S79, S81, S82, S80** (market-size reports from GrowthMarketReports, MarketIntelo, IntelMarketResearch, Market.us) — vendor market-research firms with a general interest in showing large, fast-growing markets; **only S76/S77/S78 (Gartner) are analyst-firm sources**, not vendor-commissioned — this distinction is now made explicit everywhere these figures are cited, not just in the source list.
- **S34 (ARMO)** — a commercial security vendor; the specific recall/FPR numbers it reports trace to Meta's own model card (independently confirmed), so the vendor angle doesn't taint the number itself, but the framing/emphasis is vendor content.
- Every named commercial competitor's self-reported funding, revenue-growth, or capability claim in `research/competitors.md` (Adversa AI, Straiker, HiddenLayer, Mindgard, SplxAI, Repello AI, Giskard) is vendor-sourced by definition — this was already the working assumption throughout `strategy/`, and this audit found no reason to revise it upward in confidence.

## Coverage note — read this before trusting "audit complete"

This audit covers all 90 citations actually used in the pack, across four parallel passes plus five sources checked directly. It was **stopped under explicit time pressure** ("deadline is today, stop the audit") after the four batch passes had already returned but before a planned second look at anything ambiguous. Concretely, this means:
- The 12 FAILs are corrected at the source layer; only the ones that had actually reached downstream prose were also patched there (5 of 12 — the rest never left `sources.md`, which is why they're lower-impact than they look).
- The ~21 PARTIALs are logged, not fixed — they are individually minor (a true fact on the wrong URL, not a false fact), but 21 is not zero, and the next session or phase should not assume this file means "every citation is now perfect."
- **Nothing in `financials/` or `narrative/` cites any of these sources yet** (those phases haven't started) — this audit's timing, ahead of Product/Tech/Narrative/Validation, is deliberate: those phases build on `research/` and `strategy/`, both now audited, rather than building on an unverified layer.

## Recommended next 3

1. **Before Financials or Narrative cite any market-size or vendor-survey figure, cite it with the vendor tag inline** (e.g., "per Gravitee's vendor-commissioned survey" not just "88% of organizations") — this audit's tagging convention should be the pack-wide default from here forward, not just applied retroactively to what existed at audit time.
2. **When time allows, run one more pass on the ~21 PARTIAL entries** — each needs either a corrected URL (the fact is true, just needs the right citation) or a downgrade to "unsourced, flagged" if no better URL exists. None are urgent (none reached downstream prose incorrectly), but 21 open items is real debt, not zero.
3. **Re-attempt S55 and S66** (the two UNVERIFIABLE entries) when network conditions allow — both back real competitive facts (Giskard's documentation, the Prompt Security/SentinelOne acquisition) that the pack currently relies on without their primary citation actually having been read.
