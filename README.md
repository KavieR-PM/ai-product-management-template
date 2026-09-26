# Juno PM

> An AI Associate PM that turns escalations from tickets (Jira & support) & Slack into strategic insights and creation of draft PRD

_Kavena Ramsoobhag · AI PM Cohort · September 2026

Repo: https://github.com/KavieR-PM/ai-product-management-template.git

This repo is my final project for the AI Product Management Certification — **Juno PM**. Each module’s artefact lives in its own folder; this README is the dashboard and the pitch.

---

## Module artefacts

### M1 · Prompting
- **System prompt** — [`01-prompting/system-prompt.md`](01-prompting/system-prompt.md)
- **Prototype** — [https://claude.ai/artifact/M4iRgj17dm1UxMy1yik9fB](https://claude.ai/artifact/M4iRgj17dm1UxMy1yik9fB)

### M2 · Strategy
- **Decision matrix** — [`02-strategy/decision-matrix.md`](02-strategy/decision-matrix.md)
- **AI Strategy one-pager** — [`02-strategy/strategy-one-pager.md`](02-strategy/strategy-one-pager.md)

### M3 · RAG / AI PRD
- **AI PRD** — [`03-rag-prd/prd.md`](03-rag-prd/prd.md)

### M4 · AI-Native UX
- **AI user flow** — [`04-ai-ux/user-flow.md`](04-ai-ux/user-flow.md)
- **Trust-gap mitigations** — [`04-ai-ux/trust-gaps.md`](04-ai-ux/trust-gaps.md)

### M5 · Agentic Workflows
- **Agent Workflow Spec (AWSpec)** — [`05-agentic-workflows/awspec.md`](05-agentic-workflows/awspec.md)
- **Agent Control Panel** — [`05-agentic-workflows/agent-control-panel.md`](05-agentic-workflows/agent-control-panel.md)

### M6 · Evals &amp; Guardrails
- **Eval stack** — [`06-evals/eval-stack.md`](06-evals/eval-stack.md)
- **Human evaluation rubric** — [`06-evals/human-rubric.md`](06-evals/human-rubric.md)

---

## PM Execution Plan

### Where Juno is today
- M1–M6 specced and committed.
- The prototype validates the M1 flow with the team.
- Basic Juno pipeline: read escalations → RAG strategy → score risk+alignment → output risk list + draft PRD → PM approves"
- User-facing UI for browsing insights, approving writes
- Tool tracing/logging 
- Initial anti-pattern detection logic
- Human rubric drafted; 2 grader candidates lined up; no calibration round yet.

### What ships next (next 2 sprints)
- Sprint 1: wire the eval harness to CI; staff and calibrate 2 graders; ship the dashboard tool.
- Sprint 2: open closed beta with 3 PMs (1 RocketShip, 2 customers); weekly rubric review; instrument abandon-rate.

### What I watch (dashboards)
- Daily: thumbs-down rate, regen rate, hand-off rate.
- Weekly: human-rubric mean per dimension; refusal hit-rate; cost per run, engagement patterns, sentiment in chat/Slack.
- Per release: golden-set accuracy; format/citation/refusal pass rate.

### Red lines (what blocks shipping)
- Any critical-safety fail (any "1" on safety dimension in human eval).
- golden-set accuracy on automated layer.
- Customer-name fabrication in last 30 days.
- Cost >$0.50 per run.
- P99 latency >5s on triage flow.

### Governance
- Compliance: PII scrubber pre-LLM; GDPR DSR handler in /docs/dsr-runbook.md.
- Safety: prompt-injection eval row in golden set; refusal on legal/contract content.
- Reliability: 99.5% SLO; cached top-3 fallback if model is down.
- Reputation: 2-hour incident-response playbook in /docs; canary deploys for every model swap.

---

## Build Insights

- **Friction point.** PM verification is too binary - it required a 100% match to the strategy which can lead to the system rejecting insights that could improve the product.
- **Key learning.** Eval scores from any single layer of the Eval stack is incomplete. Utilizing the three layers: Component tests will indicate if the guardrails implemented are working; human eval (grader scores) will tell if the output quality is high; user feedback will tell if Juno is valuable to the users. 
- **Aha moment.** The rubric doesn't define success - problem statement does. Define the problem first, then design the eval to prove you solved it

---

_Certification submission — AI Product Management Certification._
