# AI Strategy One-Pager - Juno Automated Prioritization

# AI Strategy One-Pager - Juno Automated Prioritization

## 1. Problem & Workflow

The Problem: RocketShip PMs triage P0/P1 escalations from Slack (#escalations), Jira (ROCKET), and Support tickets without strategic context. Result: escalations get prioritized by noise, not by strategic impact. Teams spin up work misaligned to Q3 strategy. PRDs lack evidence trails.

Prevention: Juno grounds every escalation against RocketShip's Q3 2026 Strategy One-Pager via RAG. Every claim cites its source (Slack ID, Jira key, Support ticket). Strategic alignment is scored before any output ships. Ambiguous claims are flagged "NEEDS CLARIFICATION" instead of guessed.

## 2. Target Metrics

Cycle time: Time from P0 escalation to draft PRD + prioritized risk list drops from 3–4 hours to <20 minutes. Measurable in ≤ 30 days (first beta use case).

Strategic alignment: 100% of P0 escalations in output have a strategic pillar cited (no escalations reach the PM without strategic grounding).

Leadership proof:
- 100% of claims are sourced (zero fabricated customer names, ARR, or contractual terms)
- Zero instances of verification gate or citation enforcement failing
- PM adoption ≥ 20% in first week; daily active users ≥ 15% by week 4
- Draft PRDs created for 100% of P0 escalations (traceability to strategy)

## 3. Autonomy Level

Choice: Copilot. Juno synthesizes escalations, scores strategic alignment, and drafts PRDs. But requires explicit PM approval before publishing the risk list or PRD to the Structured Insights store. The PM remains the decision-maker; Juno is the synthesis engine.

Explicitly avoiding:
- Agent (autonomous escalation triage and PRD generation without approval—unacceptable for strategic decisions)
- Assist (read-only synthesis, no priority ranking—misses the point)

## 4. Data & Model Approach

Approach: Ground (RAG). Juno reads three sources of truth:
- Slack threads (#escalations, P0/P1 tagged)
- Jira tickets (ROCKET project)
- Support tickets (customer context)
Then RAG-retrieves over RocketShip Q3 2026 Strategy One-Pager to ground every escalation against strategic pillars. Every claim is traced back to its original source. No external data; no hallucination tolerance.

Explicitly avoiding:
- Fine-tuning (not cost-effective for variable escalation patterns and evolving strategy)
- Buy-only LLM (no grounding means no source citation, no strategic alignment scoring, verification gate becomes impossible)

## 5. Risks & Mitigations

Risk: Fabricated or strategically misaligned claims reach the PRD and risk list (e.g., invented customer name, mismatched strategic pillar, or lack of evidence), eroding trust in escalation triage and causing the team to build work that drifts from Q3 strategy.

Mitigation: Immutable audit trail with code-enforced citation + alignment gate. Every escalation in the output requires:
- Source citation (Slack ID, Jira key, or Support ticket link)
- Strategic pillar alignment (mapped to Q3 strategy via RAG, or marked "NEEDS CLARIFICATION")
- Evidence quote (verbatim from source)
- Immutable trace log (all tool calls, retrieval chunks, scoring rationale)
Any missing source, fabricated claim, or unmapped strategic pillar blocks publication entirely. Zero exceptions.

## 6. V1 Scope

In:
- Read Slack #escalations threads (P0/P1 tagged), Jira ROCKET tickets, Support tickets
- RAG-retrieve over RocketShip Q3 2026 Strategy One-Pager
- Score each escalation: risk level (P0–P3), strategic pillar alignment, and customer impact
- Synthesize into structured format: Rank | Risk | Customer signal | Source ID | Strategic pillar | Suggested action
- Generate draft PRD cards for P0 escalations (problem statement + evidence + strategic rationale)
- Cite every claim with source and evidence quote
- Full audit trail logged
- PM approval required before publishing to Structured Insights store

Out:

- Does NOT publish risk list or PRD without PM approval
- Does NOT generate claims from external sources (web search, competitor research—only Slack, Jira, Support, Strategy KB)
- Does NOT invent customer names, ARR, or contractual terms (refuse and mark "NEEDS CLARIFICATION")
- Does NOT handle requests involving contracts, legal, or regulators (hand off to human PM)
- Does NOT score strategic alignment without RAG-retrieving strategy context (marks as "NEEDS CLARIFICATION" if strategy KB is unavailable)
