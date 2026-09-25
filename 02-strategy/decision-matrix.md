# AI Solution Decision Matrix · Juno

# AI Solution Decision Matrix · Juno

## The decision

Whether RocketShip builds Automated Prioritization in Juno as a Hybrid (RAG + Agentic) Copilot, vs buying a generic LLM API or fine-tuning a model on our corpus.

Why now: roadmap discussions are driven by the loudest voice in Slack rather than customer evidence. Priorities reverse weekly, and the PM cannot defend the call to leadership.

## Options scored

| Option | Cost | Speed | Control | Moat | Risk | Score |
|---|---|---|---|---|---|---|
| Build | 2 | 2 | 5 | 4 | 2 | 3.0 |
| Buy / API | 4 | 4 | 1 | 1 | 1 | 2.2 |
| Fine-tune | 3 | 3 | 2 | 2 | 3 | 2.6 |

## Recommendation

BUILD. Buy/API and Fine-tune both fail on the core requirement: we cannot enforce 100% source traceability and immutable audit trail without owning the verification gate. Build score (2+2+5+4+2 = 15/25) is lower than it looks, but it's the only path that meets the safety/trust constraint. We must control the verification gate and audit trail. Trade-off: 6–8 week timeline vs. immediate launch with Buy/API, but the guardrail cost is non-negotiable for roadmap decisions.
