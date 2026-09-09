# Not vaporware — stack, evaluation loop, cost model, and honest build scope

**What this is**: the concrete-enough-to-start-Monday page — real stack choices, how AgentGuard checks its own quality continuously, the cost model at current API prices, and what a four-person capstone team can actually build this quarter versus what remains genuine research risk.

**Why it exists**: `tech/whitepaper.md` and `tech/deep_dives.md` argue the mechanism; this document exists so a skeptical engineer can ask "fine, but could you actually build this by Tuesday" and get a specific, checkable answer rather than a roadmap slide. The failure this document prevents: a tech layer that reads well but evaporates the moment someone asks which model, which repo, and which week.

**How to read it**: the buildable-vs-research-risk table at the end is the one section a skeptic should read first — it is where this document is most honest about what a two-semester, four-person capstone team can and cannot realistically ship, and it should be checked against `ASSUMPTIONS.md`'s "Restated hard facts" (no implementation exists yet) before anything else here is trusted.

**Depends on / feeds**: built from `research/sources.md` S101–S106 (LLM pricing), `strategy/market_sizing.md`'s campaign-cost Fermi (reused, not recomputed), `BRIEF.md`'s Riskiest assumption, and `BRIEF.md`'s Founder edge (four-person, two-semester team). Feeds nothing further downstream yet in this run — it is the tech layer's final artifact.

---

## 1. Concrete stack choices

No implementation exists yet (`ASSUMPTIONS.md`, Restated hard facts) — everything below is a design choice, labeled as such, not a description of shipped software.

| Layer | Choice | Basis |
|---|---|---|
| Attacker model (feedback-only exploration rounds) | Claude Haiku 4.5 ($1 in / $5 out per million tokens) or Gemini 2.5 Flash-Lite ($0.10 in / $0.40 out) as the cost-sensitive default | `research/sources.md` S103, S106 — cheapest documented frontier-family tiers found in this research |
| Attacker model (white-box upper-bound arm, higher-fidelity rounds) | Claude Opus 5 ($5 in / $25 out) | S103 — frontier-tier accuracy where the upper-bound comparison specifically needs it |
| Target agent model | Customer-specified — AgentGuard evaluates the customer's own deployed model choice, never substitutes its own | `BRIEF.md` Business model: the target agent is the customer's, AgentGuard evaluates it in staging |
| Judge/scoring model | Frontier tier (Claude Opus 5 or GPT-5.6, $5/$30 [S102]) for ASR and utility scoring accuracy | Scoring errors propagate into every downstream comparison — this is not the place to cost-optimize |
| Attack-generation environment | AgentDojo [S1], adapted for the feedback-only harness | Named, open, cited as baseline throughout `BRIEF.md`; not reinvented |
| Adaptive attacker | AutoDojo's black-box iterative optimizer [S13], adopted as the primary attacker configuration | `ASSUMPTIONS.md` A9 — explicitly adopted, not built from scratch |
| Round orchestration | PyRIT's orchestrator pattern [S59] reused for scheduling/retry/logging plumbing only | `tech/deep_dives.md` item 8 |
| Reference classifier defense | Meta PromptGuard 2 (86M) [S33, S34] | Best-documented open classifier found; pluggable, not hard-coded (`tech/techniques/technique_feature_matrix.md`'s recommendation) |
| Reference rule-based defense | Progent policy language [S38] | Best-documented open rule-based engine found, with the explicit caveat that its 0%-ASR claim is self-reported (`capability_table.md`) |
| Delivery | Self-serve CLI + API | `BRIEF.md` Business model, uniform across all three user tiers |

## 2. The evaluation loop — how AgentGuard measures its own quality continuously

This is the same design as `tech/architecture/D08.md`, restated here as a standing commitment rather than a diagram detail, because it is the direct operational form of `BRIEF.md`'s Riskiest Assumption test:

1. **The riskiest-assumption test is not a one-time gate — it is a recurring self-check.** `BRIEF.md`'s matched-budget design (N adaptive rounds vs. N random static draws, same target/defense/budget, ASR gap reported either way, including a null result) is re-run on a fixed reference target agent on a recurring cadence, not only once before launch.
2. **A null or shrinking gap is a first-class, actionable signal, not a discarded result.** `research/survey.md` §6.2 already flags that the adaptive advantage may be *shrinking* against frontier models (the agentic TAP-vs-GPT-5 result, ~5% ASR [S32]) — the self-eval loop exists specifically to catch this drift on AgentGuard's own reference target before it silently erodes every customer's Comparison Report's credibility.
3. **No named external benchmark exists yet for "is AgentGuard's own comparison accurate."** This is a genuine gap, stated honestly: unlike a model-eval product that can cite MMLU or HumanEval, there is no standing third-party benchmark for "does this adaptive-red-team-comparison tool produce a trustworthy comparison." The closest available proxy is reproducing AutoDojo's own published number (28% ASR recovery / 64% on action-open tasks [S13]) on the same defense configuration as a sanity check before trusting AgentGuard's own re-implementation on novel targets (`tech/deep_dives.md`'s Recommended next #2).
4. **Model-version drift is monitored, not assumed static.** Attacker, target, and judge models all change versions over the life of the product; `tech/architecture/D08.md`'s drift monitor exists because a version change on any of the three could shift results without a code change on AgentGuard's side.

## 3. Cost model at current API prices (reused from `strategy/market_sizing.md`, not recomputed)

`strategy/market_sizing.md`'s campaign-cost Fermi already computed this and should not be recomputed here — restated for this document's completeness only:

- **~50 rounds per defense**, attacker context growing roughly linearly from ~500 to ~25,000 tokens (averaging ~12,750 tokens/round) → **~637,500 tokens per campaign** for the attacker side alone.
- **Cheap tier (Claude Haiku 4.5, $1/$5 per million tokens [S103])**: **≈$0.64–$3.19** for the attacker side alone; **≈$3–$10** per single-defense campaign after tripling for target-agent calls, defense-classifier calls, and retries; **≈$12–$40 per full 4-defense Comparison Report**.
- **Frontier tier (Claude Opus 5, $5/$25 [S103])**: **≈$10–$48** per single-defense campaign; **≈$38–$190 per 4-defense Comparison Report**.
- Against the placeholder pricing in `strategy/market_sizing.md` ($750/single-defense campaign, $2,500/bundled report — explicitly `(assumption: preliminary, not final)`), gross margin on inference cost alone is comfortably above 90% under either tier. **This is not a claim that $750/$2,500 is the right price** — `strategy/market_sizing.md` is explicit that whether the market will pay that is unresolved, only that inference cost is not the constraint.

## 4. Buildable this quarter vs. genuine research risk — honest for a 4-person, two-semester capstone team

`BRIEF.md`'s Founder edge is explicit: four people, CMPE 295A/295B, two semesters, research access and rigor as the edge — not a funded engineering team. This table is calibrated to that reality, not to a Series A startup's headcount.

| Component | Buildable this quarter (real engineering, known techniques) | Genuine research risk (uncertain, could fail, needs its own validation) |
|---|---|---|
| Feedback-only round loop (item 1) | **Yes** — wiring AutoDojo's open-source code [S14] to a target agent and logging rounds is integration work, not invention | Whether the loop reproduces AutoDojo's own published numbers on a first attempt is not guaranteed — budget time for debugging against research-grade code, not production-grade code |
| Defensive-prompting harness (item 4) | **Yes** — a prompt template plus the same round loop | — |
| Classifier-based harness (item 5) | **Yes** — wrapping PromptGuard 2 [S33] as an inline filter is a known integration pattern | Whether PromptGuard 2 holds up under AgentGuard's own adaptive pressure is exactly what the product measures — a genuinely open question, not an engineering risk |
| Rule-based harness (item 6) | **Partially** — wrapping Progent [S38] if its policy language is usable off-the-shelf; **research risk if it requires non-trivial policy authoring per target agent** | Progent's own ASR-to-0% claim is self-reported and unverified [S38, capability_table.md] — building the harness is buildable, but trusting Progent's baseline claim without adaptive testing is not |
| Utility metric (item 3) | **Yes** — AgentDojo's definition is published and precise [S1] | Whether AgentGuard's own campaign cases (not AgentDojo's fixed 629-case suite) produce numbers meaningfully comparable to AgentDojo's published baselines is an open bridging-methodology question (`tech/deep_dives.md` item 3) |
| Matched-budget aggregator/report (item 7) | **Partially** — the budget-enforcement and report-formatting logic is buildable; the schema (D04) is straightforward | **This is the component `strategy/positioning.md` names as AgentGuard's actual contribution** — getting the comparison semantics right (what counts as "matched," how partial campaigns are handled) is real design work a four-person team can do, but it is the one piece with no existing reference implementation to copy |
| White-box upper-bound arm (item 2) | **No — deliberately deprioritized**, per `tech/deep_dives.md`'s own Recommended next #3: build items 1, 3–7 solid first | Lower research risk than it looks (GCG/TAP are well-documented [S29, S31]), but low priority — not the headline mechanism |
| The riskiest-assumption test itself | **Yes, this is the two-week/$1k test `BRIEF.md` already specifies** | The test's *outcome* is the actual research risk — a null or negative gap is explicitly a valid result that would mean the wedge does not hold at that budget, and the team must be prepared to report that honestly rather than route around it |
| Continuous/standing corpus (F10, `technique_feature_matrix.md`) | **No — not this quarter.** Requires a working single-campaign pipeline first, plus unresolved cross-tenant data governance questions (`tech/architecture/D09.md`) | Whether an accumulating comparison corpus produces any real defensibility is `BRIEF.md`'s own named moat hypothesis, explicitly unproven (`ASSUMPTIONS.md` A2) — not a build task, a business hypothesis that can't be tested before real usage exists |

**Compression note, stated plainly**: this table reflects a hard-deadline pass, not a full engineering sprint-planning exercise — actual sprint sizing (story points, exact week numbers against CMPE 295A/295B's calendar) is deferred to a project-management artifact this pack does not generate, not silently assumed away here.

## Recommended next 3

1. **Run the riskiest-assumption test in Weeks 1–2, using only the buildable-this-quarter components (items 1, 3, 4)** — this validates the core mechanism before any team time is spent on the harder rule-based harness (item 6) or the aggregator (item 7), and a null/negative result here should stop further build work, per `BRIEF.md`'s own instruction that this kills the company if false.
2. **Build the aggregator (item 7) against stub harnesses immediately after**, per `tech/deep_dives.md`'s Recommended next #1 — it is the one component with no reference implementation to copy, so it needs the most iteration time, not the least.
3. **Defer the white-box arm (item 2) and the continuous/standing-corpus feature (F10) past this quarter entirely** — both are explicitly lower-priority per the deep-dives and matrix documents, and a four-person team attempting all ten `tech/deep_dives.md` items simultaneously this quarter would not finish any of them well.
