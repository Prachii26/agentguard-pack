# AgentGuard — One-Pager

**What this is**: a single-page investor/partner summary of AgentGuard — problem, mechanism, market, and ask — compressed to what a reader decides from in two minutes.
**Why it exists**: every other artifact in this pack argues one piece of the case at length; nothing forces the whole argument onto one page a skeptical reader can act on cold. The failure this prevents: a reader who has to open five files to learn this is a zero-traction capstone project, which reads as concealment rather than honesty.
**How to read it**: top to bottom is the pitch order. A skeptic should go straight to Traction/Evidence — that line is the one most one-pagers fudge, and this one states the truth plainly.
**Depends on / feeds**: built from `BRIEF.md`, `research/competitors.md`, `strategy/positioning.md`, `strategy/market_sizing.md`. Feeds nothing downstream — this is a terminal artifact for external readers.

---

**AgentGuard** — An adaptive red-team/blue-team evaluation platform that runs the same budget-matched, feedback-only adaptive attack campaign against each of a target agent's candidate defenses and reports attack success and legitimate-task utility side by side — the standing, reproducible cross-defense comparison that neither the academic adaptive-attack literature (e.g. AutoDojo) nor proprietary red-teaming vendors (e.g. Adversa AI) currently publish, so security teams learn not just whether a defense holds against an adapting attacker, but what it costs them to deploy it.

## Problem

Tool-using agents (email, calendar, document, CRM access) are vulnerable to indirect prompt injection — malicious instructions hidden in content the agent processes, hijacking it into unauthorized actions the user never typed. Public benchmarks (AgentDojo, InjecAgent, Agent Security Bench, BIPIA) score defenses against fixed or originally-fixed attack sets. That score says nothing about resilience against an adversary willing to iterate: a joint NIST/UK AI Security Institute human red-team exercise on an AgentDojo-derived environment found hijack success rising from **11% against generic attacks to 81% against attacks adapted to the specific target — a 7x jump** (`research/sources.md` S27, government-run, not vendor-sourced). Separately, two independent vendors converge on the same pattern from the deployment side: 88% of organizations report a confirmed or suspected AI-agent security incident in the past year (S150, **Gravitee, vendor-sourced**), and organizations running over-privileged AI report a 76% incident rate vs. 17% for least-privilege deployments (S154, **Teleport, vendor-sourced**).

## Solution mechanism

A configurable red-team agent (adopts AutoDojo's published black-box adaptive-attack technique as one attacker configuration, not a proprietary invention — S13) runs a matched-attempt-budget campaign, feedback-only (pass/fail per round, no defense identity disclosed — the primary threat model, because that is what a real attacker actually has), against each of four fixed blue-team defenses — defensive prompting, classifier-based detection, rule-based tool-call validation, baseline/none — on the same target agent. The output nothing else publishes: final-window ASR, attempts-to-first-success, campaign-average ASR, and legitimate-task **utility under attack**, all reported **per defense, side by side, at equal budget**. The differentiator is the comparison, not the attacker (`ASSUMPTIONS.md` A9) — AutoDojo measures ASR recovery in one framework with no utility metric; Adversa AI's engagements are proprietary and per-customer; Microsoft's Azure AI Foundry Red Teaming Agent tests one deployment at a time. None publishes this standing, cross-defense, utility-paired result.

## Why now

LLM inference cost dropped ~4x at the frontier tier in one year (GPT-4 → GPT-4o, S101) with cheap-tier options as low as $0.10/$0.40 per million tokens (S106) — cheap enough to make many-round adaptive campaigns routinely affordable. Tool-using agent deployments moved from demo to production across 2024–2026, expanding real attack surface from bad chatbot output to unauthorized agent actions. Indirect prompt injection is now a named threat class with four public benchmarks (Dec 2023–Oct 2024) and a funded commercial red-teaming category ($3.6B raised across top-10 agentic-AI-security startups, `research/competitors.md`) — but no vendor in that category publishes the cross-defense comparison this platform is designed to produce.

## Traction / evidence

**Zero traction, stated plainly: no customers, no revenue, no funding, no pilots, no testimonials exist** (`ASSUMPTIONS.md`, Restated hard facts). This is a CMPE 295A/295B graduate capstone project at San José State University — a 4-person team, two semesters — not an operating company. The near-term evidence plan, not invented traction: a two-week, <$1,000 riskiest-assumption test (matched-budget design — N adaptive rounds vs. N random draws from InjecAgent's static set, same target/defense/budget) that reports the ASR gap either way, including a null result if that is what the data shows (`BRIEF.md`, Riskiest assumption). That test, not a customer logo, is the first real evidence this venture will produce.

## Market

Bottom-up, not top-down: ≈8,595 addressable companies (ML/AI-engineering-capable, agents in production, sufficient governance maturity to buy dedicated tooling — Fermi steps sourced to LangChain's State of Agent Engineering 2025 [S83] and McKinsey's State of AI Trust in 2026 [S87]) × 4 comparison reports/year × a **preliminary, not-yet-validated** $2,500/report price point ⇒ **SAM ≈ $86M/year**. At a conservative 0.1–0.5% year-1/2 capture rate for a pre-product, zero-traction, self-serve-only venture: **SOM ≈ $90K–$430K/year** (9–43 customers, `strategy/market_sizing.md`). Top-down check: Gartner's "securing AI" category, $4.8B by 2027 (S76) — the SAM above is ~1.8% of that, a plausible ratio for one product category within a multi-category market.

## Team edge

Four-person graduate capstone team, CMPE 295A/295B, San José State University. The edge is direct research access and rigor — sustained engagement with the four named public benchmarks and the adjacent academic literature (AutoDojo, AgentDojo, the joint OpenAI/Anthropic/DeepMind adaptive-attack study) as a graduate research project — **not** a go-to-market, distribution, or domain-operating advantage. No prior company, customers, or operating history exists to claim otherwise (`BRIEF.md`, Founder edge).

## The ask

Not currently fundraising — this pack is a research-to-startup translation exercise, not an active raise. Two honest, appropriately-scoped asks for this stage: **(1)** introductions to 3–5 security or ML-platform teams willing to act as design partners for the riskiest-assumption test above (running it against a staging/sandboxed reference agent, not production — `BRIEF.md` Year-one scope); **(2)** feedback on the comparison-protocol thesis from anyone close to AgentDojo, AutoDojo, or the agent-security vendor landscape, before the team decides whether to continue building past the capstone's two semesters.

---
*Note on sourcing: `product/journeys/` and `tech/architecture/` were still empty when drafting began on this file and populated mid-session; this one-pager's mechanism claims were cross-checked against both once they landed and found consistent — no changes were needed.*
