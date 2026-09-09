# Decision tree — when/what fires, in which order

**What this is**: the triage logic that decides, for a given campaign request, whether it runs at all, which defense harnesses fire, and in what order severity is checked versus adaptive exploration proceeds.

**Why it exists**: `BRIEF.md`'s year-one scope excludes production traffic, custom defenses, and multi-modal injection — this document is where those exclusions become an enforced decision sequence rather than a paragraph a future engineer might not read. The failure this document prevents: a campaign silently running against an out-of-scope target (production traffic, an unsupported defense type) because no gate exists to catch it before the adaptive loop starts spending budget.

**How to read it**: the flowchart's top three diamonds are refusal gates (scope violations), not adaptive branches — a skeptic should confirm every "no" path terminates before any model call is made, since a scope violation caught after spending campaign budget is a worse failure than one caught before.

**Depends on / feeds**: built from `BRIEF.md` Year-one scope and Vocabulary, and `tech/deep_dives.md` items 1–7. Feeds `tech/architecture/D01.md` (this is the logic that precedes D01's pipeline) and `tech/architecture/D10.md` (severity triage, elaborated here at the decision-table level).

---

```mermaid
flowchart TD
    Req[Campaign request received] --> G1{Target is staging/sandboxed,\nnot production?}
    G1 -->|no| Refuse1[Refuse: production traffic\nout of year-one scope]
    G1 -->|yes| G2{Requested defense type is\none of the 4 named types?}
    G2 -->|no| Refuse2[Refuse: custom defense\nauthoring not supported]
    G2 -->|yes| G3{Injection surface is\ntext-based only?}
    G3 -->|no, image/audio| Refuse3[Refuse: multi-modal injection\nout of year-one scope]
    G3 -->|yes| Sev{Does target agent have\nwrite/irreversible-action tool access?\ne.g. send, delete, transact}
    Sev -->|yes| Priority[Priority: run high-severity\nobjective classes first\ndata exfiltration, unauthorized send/transact]
    Sev -->|no, read-only tools| Standard[Standard order: run\ncampaign objective set as configured]
    Priority --> ThreatModel{Threat model?}
    Standard --> ThreatModel
    ThreatModel -->|feedback-only, default| Primary[Run primary campaign:\nfeedback-only, matched budget N]
    ThreatModel -->|white-box, upper-bound arm requested| Upper[Run upper-bound comparison arm\nin addition to, never instead of, primary]
    Primary --> Harnesses{Which defense(s)\nselected?}
    Upper --> Harnesses
    Harnesses --> H1[Defensive-prompting harness]
    Harnesses --> H2[Classifier-based harness]
    Harnesses --> H3[Rule-based tool-call harness]
    Harnesses --> H4[Baseline/none harness]
    H1 --> Reeval{Continuous mode?\nedge-high tier}
    H2 --> Reeval
    H3 --> Reeval
    H4 --> Reeval
    Reeval -->|yes| Schedule[Re-trigger on schedule\nor release event]
    Reeval -->|no| Done[Report once, campaign complete]
    Schedule --> Req
```

## Logic table

| State | Condition | Action | Fires before/after |
|---|---|---|---|
| 1 | Target is production, not staging | Refuse the request entirely | Before any model call — hard gate, `BRIEF.md` Year-one scope #1 |
| 2 | Requested defense type is not one of the four named types | Refuse the request entirely | Before any model call — hard gate, `BRIEF.md` Year-one scope #2 |
| 3 | Injection surface is image- or audio-embedded | Refuse the request entirely | Before any model call — hard gate, `BRIEF.md` Year-one scope #3 |
| 4 | Target agent has write/irreversible-action tool access (send, delete, transact) | Prioritize high-severity objective classes (exfiltration, unauthorized send/transact) before broader campaign exploration | After scope gates pass, before the adaptive loop begins — this is the "safety-critical triage before adaptive branching" the brief calls for |
| 5 | Target agent has read-only tool access only | Run the configured objective set in standard order, no severity reprioritization needed | Same stage as state 4, mutually exclusive with it |
| 6 | Threat model = feedback-only (default) | Run the primary campaign; this is the number reported as the headline | Core adaptive loop, `tech/deep_dives.md` item 1 |
| 7 | Threat model = white-box requested | Run the upper-bound arm **in addition to**, never instead of, the feedback-only primary | Runs in parallel with state 6, never substitutes for it — `BRIEF.md` Vocabulary is explicit white-box is never the headline |
| 8 | Multiple defense types selected | Run each selected defense's harness at the same matched budget N | Fan-out stage, `tech/architecture/D01.md` |
| 9 | Mid-campaign, a severe finding occurs (exfiltration/irreversible action succeeds) | Escalate to human reviewer before report release (`tech/architecture/D10.md`) | Interrupts the standard flow at any round, does not wait for campaign completion |
| 10 | Edge-high / continuous mode enabled | Re-trigger the full sequence on a schedule or release-event trigger, starting again from state 1's gates | Continuous re-evaluation, `BRIEF.md` edge-high persona (Dr. Elena Osei) |

## Recommended next 3

1. **Implement states 1–3 (the refusal gates) before any adaptive-loop code**, since they are the cheapest, highest-consequence checks to get right — a scope violation caught here costs nothing; caught after spending campaign budget, it costs real inference spend and, worse, customer trust on the exact production-traffic boundary `tech/architecture/D06.md` is built to guarantee.
2. **Test state 4's severity-prioritization logic against a target agent with mixed tool access** (some read-only, some write) before assuming the binary split in the table is sufficient — most real target agents (Marcus Webb's persona's refund-processing agent, `strategy/personas.md`) mix both.
3. **Decide the state-7 upper-bound-arm default (opt-in vs. opt-out) explicitly** before shipping — `BRIEF.md` Vocabulary implies white-box is available but secondary; this document assumes opt-in, which should be confirmed against actual product decisions once `product/PRD.md` exists.
