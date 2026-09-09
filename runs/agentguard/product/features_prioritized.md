# Features — prioritized (50), Now / Next / Later

**Status: design only — no implementation exists yet (`BRIEF.md` stage line).**

**What this is**: all 50 features in strict priority order, grouped into Now (MVP — enough to run the riskiest-assumption test and deliver Marcus's core comparison report), Next (rounds out the four-defense, dual-threat-model product and self-serve business mechanics), and Later (portfolio-scale features for the edge-high tier). Each row: number, feature, mechanism, user value, dependency, effort (S/M/L).

**Why it exists**: `product/features_flagship.md` argues *which* 20 features matter most; this document forces the sequencing question — what gets built in what order so a four-person, two-semester team ships something real rather than 50 half-finished features. The failure this document prevents: a prioritization that is secretly chronological (build whatever's easiest next) rather than tied to what actually proves the riskiest assumption and serves the beachhead persona first (`references/quality-bar.md` red flag: "prioritization that's secretly chronological").

**How to read it**: Now is scoped tightly to what the riskiest-assumption test (`BRIEF.md`) and Marcus's core job (`strategy/value_prop_canvas.md`) require — a skeptic should check that every Now-tier item is traceable to one of those two things, not to "seemed important." Depends-on columns should form a DAG with no forward references from Now into Next/Later.

**Depends on / feeds**: expands `product/PRD.md` §6 and `product/features_flagship.md`. Feeds the not-yet-generated `tech/architecture/` build sequencing directly.

---

## Now (19 items) — proves the riskiest assumption, delivers the beachhead's core report

| # | Feature | Mechanism | User value | Depends on | Effort |
|---|---|---|---|---|---|
| 1 | Staging-only connection gate | Configure API/CLI accepts only staging-shaped endpoints/credentials by schema; production-shaped inputs are rejected | Removes the trust barrier to first adoption for every persona | — | S |
| 2 | Sandbox credential vault | Encrypted storage for the staging credentials the connection gate (1) accepts, scoped per campaign | Makes (1) safe to actually use, not just enforce at the API boundary | 1 | M |
| 3 | Defense-set selector (1–4) | Campaign config requires choosing among the four fixed defenses; each spins up its own sub-campaign | Structurally enforces the cross-defense scope non-goal boundary in the UI itself | — | S |
| 4 | Shared attempt-budget field | One budget value propagates unchanged to every selected defense's sub-campaign, no per-defense override | Makes every comparison matched-budget by construction, not by discipline | 3 | S |
| 5 | Reference-harness picker | Explicit list of year-one-supported agent harnesses, no free-text "any agent" field | Sets expectations correctly before a campaign is configured, avoiding mid-run failures | — | S |
| 6 | API key / CLI auth | Self-serve key issuance, no sales call required to start | Priya's stated trigger to switch: "something I can run from a GitHub Action" | — | S |
| 7 | Configurable attacker registry (AutoDojo default) | Attack-generation strategy is a pluggable module; year one ships AutoDojo's black-box optimizer as the sole default, explicitly labeled by source | The engine that actually runs the campaign; labeling honesty avoids the proprietary-attacker overclaim | 1, 2 | L |
| 8 | Feedback-only mode (default) | Attacker process receives only round pass/fail; defense identity withheld from its context by construction | Makes the primary threat model (real-attacker-realistic) the default, not an option a user has to know to choose | 7 | M |
| 9 | Text-only injection surface generators | Payload construction for email, document, webpage, calendar-invite content types | Covers the year-one attack surface BRIEF.md scopes in | 7 | M |
| 10 | Attack objective library | Named objective types (data exfiltration, unauthorized send, unintended tool call) the attacker targets per round | Makes campaign results interpretable ("what was it trying to do") rather than an opaque pass/fail | 7 | M |
| 11 | Per-round attempt content viewer | Every generated injection attempt is stored and viewable, not just its outcome | Auditability — a skeptic can inspect what was actually tried, not just trust a summary number | 7 | S |
| 12 | Per-round outcome logger | Every round writes one row: attempt, tool calls attempted/executed, pass/fail, benign-task completion flag | The raw data every downstream metric (ASR, utility, adaptation curve) is computed from | 7, 9 | M |
| 13 | Legitimate-task interleaving | Benign task requests interleaved with injection attempts against the same active defense in the same campaign | Makes utility measurable under the same conditions the attack was measured under, not a separate disconnected test | 12 | M |
| 14 | In-context adaptation controller | Attacker updates its next-round strategy from prior rounds' logged outcomes within the live session, no offline training step | The mechanism that makes this an *adaptive* evaluation rather than a single static attempt repeated | 8, 12 | L |
| 15 | Attempts-to-first-success tracker | Round index of first successful injection recorded per campaign per defense | The practicality signal BRIEF.md's Vocabulary names as a required metric alongside ASR | 12, 14 | S |
| 16 | Adaptation-curve data pipeline | ASR computed per round-window across the campaign, stored as a time series | The data behind the adaptation-curve chart and the final-window ASR computation | 12, 14 | M |
| 17 | Final-window ASR (headline) | ASR computed over the last *k* rounds rather than averaged across the whole campaign | The headline number every persona's report reads first | 16 | S |
| 18 | Cross-defense comparison table | One table: rows = defenses, columns = final-window ASR / attempts-to-first-success / utility, at matched budget | The screen that is the actual product — every persona's stated trigger-to-switch points here | 3, 4, 15, 17 | M |
| 19 | Utility-under-attack metric | Fraction of interleaved benign tasks completed correctly while the defense is active and an injection is present, using AgentDojo's utility definition | The number that makes the security/usability trade-off visible, which no competitor found in research reports at this scope | 13 | M |

## Next (23 items) — rounds out the four-defense, dual-threat-model product and self-serve mechanics

| # | Feature | Mechanism | User value | Depends on | Effort |
|---|---|---|---|---|---|
| 20 | White-box comparison mode | Opt-in second campaign arm where the attacker is told the defense type up front; rendered in a separate labeled column | Answers "how much better could a privileged attacker do" without contaminating the headline feedback-only number | 8, 18 | M |
| 21 | Attacker strategy parameter tuning | Advanced config exposing optimizer parameters (exploration rate, temperature) for power users | Serves Elena's edge-high need to stress the attacker harder than the default | 7 | S |
| 22 | Injection content-type weighting | Bias the generator toward one content surface type (e.g., email-only) for a focused campaign | Lets a team test the specific surface their agent actually exposes | 9 | S |
| 23 | Defense fingerprint capture | Behavioral signature of how a defense responded under pressure (block patterns, latency, refusal phrasing) logged per campaign | Evidence trail for *how* a defense failed, not just that it did — supports the self-reported-robustness-collapses principle | 12 | M |
| 24 | Tool-call execution trace viewer | Full trace of tool calls attempted/executed per round, viewable per attempt | Debug-depth auditability for a security engineer who needs to verify a specific claimed success | 12 | M |
| 25 | Real-time campaign progress stream | Live round-count and interim-metric updates as a campaign runs | Removes the "is this stuck" uncertainty on long campaigns | 12 | S |
| 26 | Error/timeout handling & retry logging | Distinguishes attacker/infra failure from a genuine defense block in the round log | Prevents an infra hiccup from silently corrupting an ASR number | 12 | M |
| 27 | Early-stopping detector | Flags when a campaign's ASR has plateaued well before budget exhaustion | Cost control — avoids spending the full attempt budget once the adaptation curve has clearly flattened | 16 | M |
| 28 | Cross-round strategy diff viewer | Shows what changed between round *n* and round *n+1*'s attempt content | Makes the "adapt" stage legible to a skeptic, not just its outcome | 11, 14 | M |
| 29 | Campaign-average ASR (secondary) | ASR across the whole campaign including early exploration rounds, displayed smaller than final-window ASR | The secondary metric BRIEF.md's Vocabulary specifies, kept clearly subordinate to the headline | 16, 17 | S |
| 30 | Benign block rate metric | Percentage of legitimate requests outright blocked, reported distinct from utility | Utility can hide a defense that never blocks but still degrades quality; block rate is the narrower, complementary number | 13 | S |
| 31 | Adaptation-curve chart (report) | The round-over-round ASR time series (16) rendered as an overlaid line chart, one line per defense | Visual answer to "how fast did each defense's resistance collapse" | 16, 18 | M |
| 32 | Audit-ready report export | Comparison report exports to a structured, ISO 42001 Operation/Performance-Evaluation-clause-mapped PDF/data format | David's persona's entire job — evidence he can hand an auditor without opening the product | 18, 19, 30 | L |
| 33 | Re-run / re-diff against history | New campaign on the same target-defense pair auto-diffs against the most recent prior run | Reproducibility principle made visible — "vs. last run" delta, not just a fresh number each time | 18 | M |
| 34 | Shareable report link | Read-only, revocable link to a comparison report | Sofia's persona's trigger to switch — something excerptable into her own trust-center docs | 18 | S |
| 35 | CSV/JSON raw-data export | Per-round and summary data downloadable in structured form | Lets a team compute their own downstream metrics rather than trusting only the rendered report | 12, 18 | S |
| 36 | Campaign cost/spend summary | Token/inference cost per campaign, broken out per defense sub-campaign | Answers the "is this affordable" question directly, grounded in the same cost data as BRIEF.md's why-now argument | 12 | S |
| 37 | Usage-based billing meter | Meters completed campaigns for pay-per-run billing | The mechanism the self-serve, usage-based business model (`ASSUMPTIONS.md` A3) actually runs on | 18 | M |
| 38 | Free/low-cost entry tier gating | Capped free campaigns per month before billing (37) applies | Priya's explicit objection — "I'm not paying for a security tool for a project with twelve users" | 37 | M |
| 39 | GitHub Action / CI integration | Pre-built CI step that triggers a campaign and returns pass/fail as a build gate | Priya's exact stated trigger to switch, in her exact workflow | 6, 18 | M |
| 40 | Notification/webhook on campaign completion | Push notification/webhook when a campaign finishes, with a summary payload | Removes the need to poll a long-running campaign | 18 | S |
| 41 | Consent/disclosure gate before evaluating a third-party defense | Explicit consent step before a campaign targets a defense built by a third party (e.g., a commercial classifier) | Oversight requirement — avoids publishing or exposing results about a vendor's product without acknowledgment | 3 | S |
| 42 | Campaign log access-control | Restricts raw attack-payload log visibility separately from the summary report, even within one organization | The attack log is itself a usable attack toolkit against the customer's own defense if leaked — access must be narrower than report access | 11, 12 | M |

## Later (9 items) — portfolio-scale features for the edge-high tier

| # | Feature | Mechanism | User value | Depends on | Effort |
|---|---|---|---|---|---|
| 43 | Campaign naming/tagging | Free-text labels and tags on campaigns | Organizes growing campaign history as volume increases | 18 | S |
| 44 | Scheduled/recurring campaign trigger | Cron-style recurring campaign launch, not just manual/CI-triggered | Elena's persona's need — continuous rather than per-release evaluation | 39 | M |
| 45 | Campaign templates | Save a full configuration (defense set, budget, harness) for reuse | Reduces reconfiguration overhead for teams running the same shape of campaign repeatedly | 3, 4, 5 | S |
| 46 | Multi-campaign batch launch | Launch the same configuration across multiple target agents in one action | Serves an org with many agents wanting one comparison sweep, not one agent at a time | 45 | M |
| 47 | Role-based access control | Admin vs. viewer roles within an organization/workspace | Separates Elena's (configure/run) access from David's (view/export only) access | 2, 18 | M |
| 48 | Organization/workspace model | Multiple agents and defenses tracked under one org, with shared billing and access control | The container the portfolio dashboard (49) and RBAC (47) need to exist | 37, 47 | L |
| 49 | Portfolio dashboard | One screen showing every agent's latest comparison result across an org | Elena's stated job — "one coherent, comparable security number across dozens of agents," her board-reporting need | 48 | L |
| 50 | Methodology documentation page, versioned per attacker-registry release | Public-facing page documenting exactly which attacker configuration, threat model, and metric definitions produced a given report, versioned | Academic-credibility trust substitute for traditional vendor-maturity signals (`strategy/value_prop_canvas.md`, Elena/David pain #3) | 7, 32 | M |

---

## Scope-compression note (honesty requirement per the assignment's instructions)

This list reaches 50 real, non-duplicate features without padding — the domain (campaign configuration, a four-stage attack loop, a five-metric report, and the self-serve business mechanics layered on top) genuinely supports that count. Where it is thinner than it might look: several Later-tier items (43, 45) are close variants of convenience/organization features rather than new capability, and are labeled S effort accordingly rather than dressed up as larger work. If forced to cut to a true minimum-viable slice, the Now tier's 19 items (not the full 50) is the actual MVP — everything in Next and Later is sequenced after a working single-defense-then-four-defense comparison loop exists and Marcus's core report has been validated with a real (even if internal/simulated) run.

Total rows across all three tiers: 19 (Now) + 23 (Next) + 8 (Later) = 50.
