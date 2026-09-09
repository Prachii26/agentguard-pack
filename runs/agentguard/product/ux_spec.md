# UX spec — 10 key screens

**Status: design only — no implementation exists yet (`BRIEF.md` stage line). This is a text specification; visual collages belong to a later visuals phase, not this document.**

**What this is**: the 10 screens that carry AgentGuard's product experience, each with its purpose, primary action, information hierarchy, empty/loading/error states, and the micro-interactions that make the mechanism (not an adjective) visible to the user.

**Why it exists**: `product/journeys/*.md` narrate what happens; this document specifies where it happens and what's on screen when it does. The failure this document prevents: a comparison report that is correct in the backend but unreadable on screen — a skeptic-facing product whose core differentiator (the cross-defense table) doesn't visually earn the trust the mechanism deserves.

**How to read it**: start with screen 4 (Cross-Defense Comparison Report) — it is the screen every persona in `strategy/personas.md` is described as needing, and the one every other screen ultimately serves. Screen 6 (Audit-Ready Export) is David's entire product relationship (`product/journeys/day_in_life.md`) — check it can stand alone, without the live product open, before treating this document as complete.

**Depends on / feeds**: specifies the visible moments named in `product/features_flagship.md` and the screens referenced by name in `product/journeys/*.md`. Feeds a not-yet-generated `visuals/` phase and `tech/architecture/` front-end scoping.

---

## 1. New Campaign — Configure

- **Purpose**: set up a campaign's target, defense set, and budget before any attack runs.
- **Primary action**: "Start campaign."
- **Information hierarchy**: (1) staging-endpoint field with inline validation, (2) defense-set checklist (exactly four named options, none addable), (3) shared attempt-budget field (single value, no per-defense override — visibly disabled from splitting), (4) reference-harness dropdown (supported frameworks only), (5) threat-model toggle (feedback-only default, white-box opt-in as a clearly secondary control).
- **States**: *Empty* — no campaigns yet, a single CTA and a link to the CLI quickstart (screen 9). *Loading* — validating the staging endpoint against the connection-gate schema. *Error* — production-shaped credential rejected, with the specific field and reason named, not a generic failure.
- **Micro-interactions**: attempting to set a different budget per defense visibly locks with a tooltip ("budget is matched across all selected defenses so the comparison stays valid — see `product/PRD.md` P1"); selecting white-box mode surfaces a one-line warning that it will render as a separate, clearly-labeled column, never blended into the headline number.

## 2. Live Campaign — Attack/Observe Progress

- **Purpose**: show a running campaign's real-time round count and interim signal without requiring a page refresh.
- **Primary action**: none required — this is a monitoring screen; secondary action is "cancel campaign."
- **Information hierarchy**: (1) round counter (e.g., "round 61 of 150") per defense sub-campaign, run in parallel, (2) interim ASR trend sparkline per defense, (3) a live feed of the most recent round's outcome (pass/fail icon, no attempt content yet — that's screen 3).
- **States**: *Empty/not started* — "waiting for the attacker registry to initialize." *Loading/running* — the default state, updating per round via the real-time progress stream feature. *Error* — a sub-campaign stalls (infra timeout, distinguished from a genuine defense block) with a retry affordance, per the error/timeout handling feature.
- **Micro-interactions**: each defense's sub-campaign progresses independently but the four progress bars are vertically aligned so a user can see at a glance if one defense is converging to success far faster than the others, before the final report even exists.

## 3. Round Detail — Attempt Content Viewer

- **Purpose**: full auditability of one specific round — the attempt content, the tool calls attempted/executed, and the outcome.
- **Primary action**: "view raw trace" (tool-call execution trace).
- **Information hierarchy**: (1) round number and defense it ran against, (2) the generated injection content, verbatim, (3) tool calls attempted vs. executed, (4) pass/fail outcome and the reason logged, (5) link to the adjacent rounds (n-1, n+1) for the cross-round strategy diff.
- **States**: *Loading* — round data still writing (for a very recent round in a still-running campaign). *Error* — round data corrupted or an infra failure invalidated the round (flagged distinctly from a genuine defense block, never silently dropped).
- **Micro-interactions**: hovering a tool call attempted-but-not-executed row highlights exactly which defense component intercepted it, when that data is available from the defense fingerprint capture.

## 4. Cross-Defense Comparison Report (the core screen)

- **Purpose**: the single screen that is the product — attack success and utility, per defense, side by side, at matched attempt budget.
- **Primary action**: "export report" (routes to screen 6) or "share link" (read-only).
- **Information hierarchy**: (1) final-window ASR as the largest figure on the screen, one column per defense, (2) attempts-to-first-success directly beside it, (3) campaign-average ASR, visually smaller, labeled "secondary," (4) utility-under-attack and benign block rate columns, never blank, (5) the attempt budget stated once, prominently, as the condition every column shares. White-box-mode results, if run, appear in a visually separated section below the primary feedback-only table, never merged into it.
- **States**: *Loading* — campaign still running, table shows partial/interim data with a clear "provisional — campaign in progress" banner. *Empty* — no defenses selected produced a completed sub-campaign yet. *Error* — one sub-campaign failed to complete; that defense's column shows "incomplete," never a fabricated or interpolated number.
- **Micro-interactions**: clicking any cell drills into that defense's adaptation curve (screen 5); a "vs. last run" delta badge appears next to each metric once a prior campaign on the same target-defense pair exists (re-run/re-diff).

## 5. Adaptation Curve Chart

- **Purpose**: visualize how fast each defense's resistance converged or held, round over round.
- **Primary action**: toggle which defenses' curves are overlaid.
- **Information hierarchy**: (1) ASR (y-axis) vs. round number (x-axis), one line per defense, (2) a marked point on each curve at its attempts-to-first-success round, (3) the shared attempt-budget boundary marked as the x-axis maximum for every line, so no curve visually implies it ran longer than another.
- **States**: *Loading* — curve draws incrementally as a live campaign progresses (fed by screen 2's data). *Empty* — fewer than ~5 rounds completed, insufficient to render a meaningful curve; shows a "collecting data" placeholder rather than a misleadingly smooth line.
- **Micro-interactions**: hovering any point on a curve shows that round's outcome and links directly to screen 3's detail view for that exact round.

## 6. Audit-Ready Report Export

- **Purpose**: produce a standalone document (David's entire touchpoint, `product/journeys/day_in_life.md`) that functions as evidence without the live product open.
- **Primary action**: "generate export" (PDF and structured-data format options).
- **Information hierarchy**: (1) the same comparison table as screen 4, reproduced verbatim, (2) an explicit methodology section naming the attacker registry version and threat model used, (3) a mapping table showing which ISO 42001 Operation/Performance-Evaluation clause each section addresses (`research/sources.md` S113, S114), (4) a generation timestamp and a non-expiring reference ID.
- **States**: *Loading* — export rendering (may take longer than a page load for large portfolios; shows a progress indicator, not a spinner with no context). *Error* — underlying campaign data incomplete; export is blocked with a named reason rather than silently producing a partial document. *Empty* — not applicable; this screen is only reachable from a completed report.
- **Micro-interactions**: a visible "not a compliance certification — one input to your compliance process" disclaimer is permanently rendered on the export itself, not just in help text, consistent with `product/PRD.md` §8's requirement not to overclaim regulatory coverage.

## 7. Portfolio Dashboard (edge-high)

- **Purpose**: one screen showing every agent's latest comparison result across an organization (Elena's board-reporting job, `strategy/personas.md` card 3).
- **Primary action**: drill into any agent's individual comparison report (screen 4).
- **Information hierarchy**: (1) a sortable grid, one row per agent, columns for final-window ASR (best/worst defense), utility, and last-run timestamp, (2) a change indicator (up/down arrow) versus the prior scheduled run, (3) a cross-portfolio pattern callout when the same anomaly (e.g., a shared classifier fragility) appears across multiple agents.
- **States**: *Empty* — new organization, no agents configured yet, CTA to screen 1. *Loading* — a scheduled batch of recurring campaigns still running; affected rows show "updating" rather than stale data silently. *Error* — an agent's scheduled campaign failed to trigger; flagged distinctly from "no regression found."
- **Micro-interactions**: rows with a newly-crossed ASR threshold (a configurable alert line) visually pin to the top of the grid, matching the notification that would already have fired via webhook.

## 8. Campaign History & Re-run Diff

- **Purpose**: compare a new campaign against the most recent prior run on the same target-defense pair.
- **Primary action**: "re-run with same configuration."
- **Information hierarchy**: (1) a timeline of prior campaigns for this target, (2) the delta view — metric-by-metric change since the last run, (3) the full configuration used (budget, defense set, attacker registry version) for each historical entry, so a metric change can be checked against whether the configuration itself changed.
- **States**: *Empty* — first campaign ever run on this target; no diff possible, shown plainly rather than defaulted to a misleading zero-delta. *Loading* — new run in progress, diff pending. *Error* — a historical campaign's data was deleted or is inaccessible (access-control boundary); shown as "unavailable," not silently skipped.
- **Micro-interactions**: hovering a delta value shows the two absolute numbers it was computed from, so a user never has to trust a percentage change without seeing its source values.

## 9. Onboarding / CLI Quickstart (edge-low entry point)

- **Purpose**: get a first-time, no-sales-call user (Priya) from signup to a running campaign in one sitting.
- **Primary action**: "copy CLI install command."
- **Information hierarchy**: (1) a three-step visual (install → configure staging target → run), (2) the free-tier cap stated plainly up front (no surprise billing), (3) a link to the exact GitHub Action template for CI-triggered campaigns.
- **States**: *Empty* — default state for a brand-new account. *Loading* — CLI reports back "campaign accepted" once the staging connection gate validates. *Error* — the connection gate's rejection reason surfaces inline in the terminal output, mirrored on this screen for users who check back in a browser.
- **Micro-interactions**: the free-tier cap counter updates live as example commands are copied and run, so a user never discovers the cap only after hitting it mid-campaign.

## 10. Organization & Access Control

- **Purpose**: manage who can configure/run campaigns versus who can only view/export reports, within one workspace (Elena vs. David, `product/journeys/day_in_life.md`).
- **Primary action**: "invite member" with role assignment.
- **Information hierarchy**: (1) member list with role (admin/configure vs. view/export-only), (2) which agents/campaigns each role can see, scoped by the campaign-log access-control boundary (raw attack payloads restricted separately from summary reports), (3) billing/usage-meter summary, visible only to admin roles.
- **States**: *Empty* — single-member workspace (the common case for Priya and early Marcus-tier teams), settings screen shows only self, invite CTA prominent. *Loading* — role change propagating. *Error* — attempting to grant raw-attack-log access to a view-only role is blocked with an explicit explanation, not a silent failure, consistent with the campaign-log access-control oversight requirement (`product/PRD.md` §8.6).
- **Micro-interactions**: a role badge next to each member's name is visible everywhere else in the product (comparison report, export screen) so it's always clear whose view is being rendered — Elena's configure view never silently renders David's export-only view or vice versa.

---

## Recommended next 3

1. **Build screen 4 (Cross-Defense Comparison Report) and screen 1 (Configure) first** — they are the two screens every Now-tier feature (`product/features_prioritized.md`) exists to support, and the two every journey in `product/journeys/` actually depends on.
2. **Treat screen 6's disclaimer language (ISO 42001 mapping, "not a compliance certification") as a fixed requirement, not a placeholder to soften later** — it is the exact honesty boundary `product/PRD.md` §8 sets, and it is the only thing standing between a legitimate audit-evidence claim and an overclaim a real auditor would catch.
3. **Defer screens 7–10 (portfolio, history/diff, onboarding polish, org/access control) to the Next/Later feature tiers they depend on** (`product/features_prioritized.md`) — do not front-load edge-high screen complexity into the first build pass, which targets the beachhead comparison-report screen above all else.
