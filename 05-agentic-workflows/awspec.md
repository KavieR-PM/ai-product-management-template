# Agent Workflow Spec (AWSpec) · Juno

> Module 5 · Agentic Workflows. Juno's agentic workflow specification, built with the **M5 · Agent Workflow Spec Builder**. Paste the tool's markdown over this file.

## Goal

Triage prioritized P-level list daily into the structured insights list, with a strategic-rationale citation per item which feeds into a draft PRD. 

**Primary actor:** Agent + Human-in-the-loop

## Trigger

New message in #escalations tagged P0 AND thread length >= 5 messages within 10 minutes.
New message in #escalations tagged P1 AND thread length >= 5 messages within 10 minutes
New message in #escalations tagged P2 AND thread length >= 5 messages within 20 minutes
New message in #escalations tagged P3 AND thread length >= 5 messages within 30 minutes




## Steps & tools

**Pattern:** ReAct (single-agent reason-act-observe loop)

| Step | Action | Tool / model | Guardrail |
|---|---|---|---|
| 1 | Read the tickets (Jira + Support) and Slack threads and retrieve customer ID and Application ID  if mentioned. | search_strategy(), read-only - retrieve and parse the strategy document that it queries against | Agent can READ Slack #escalations + Strategy KB + JIRA tickets. Agent can WRITE to structured insights and Draft PRD. Agent CANNOT edit write or edit tickets, strategy documents, access user accounts/permissions, evaluation scores.  |
| 2 | RAG retrieval over the RocketShip Strategy One-Pager (M3 KB), top-K = 6. | read_tickets(), read-only - fetch tickets for correlation |  |
| 3 | Score risk + alignment vs strategic pillars; emit P0-P3 with rationale. | write_roadmap, write-only - commit decisions to a persistent backlog |  |
| 4 | Create Structured insights (transcript quote) and Draft PRD cards (problem statement + evidence). | Juno Session & Request Store - Store transcript uploads, request state and tool trace logs |  |
| 5 | PM review based on confidence threshold. | Insight Store - Persist all synthesized insights (seeded and refined) and their metadata |  |
| 6 | _ | Tool trace log - Audit trail of every tool call, result, and guardrail check |  |
| 7 | _ | Strategy Document Index - fast lookups without re-parsing every time |  |
| 8 | _ | Evaluation and Metrics Store - Log weekly human evaluation scores and track guardrail health |  |

**Schemas**

- search_strategy -> {doc_id}
- read_tickets -> [id, title, description, status, priority, created, updated, assignee {id, name, email}]
- write_roadmap -> {id, title, priority, source, status, insight_id, strategy_clause, evidence_quote, created_by, approved_by}

**Memory (in or out of scope)**

- **Episodic:** In-scope, tool results, retrieved chunks, intermediate scores. Lifetime: end of run.
- **Semantic:** In-scope, RocketShip strategic taxonomy + Juno system prompt + PM preferences. Lifetime: indefinite, refreshed weekly. Out of scope, do NOT persist customer-specific contracts or PII.
- **Working:** In-scope, current thread, customer ID, Application ID, KB chunks, current confidence score. Held in working context only.
- **External:** Slack thread API (read), RocketShip Strategy KB (read), Jira (write, stub creation only).

## Human-in-the-loop

PM reviews any P0 with confidence < 70% before posting. PM will review and approve any P0 escalations before it is posted to the structured insights and draft PRD.

## Success & failure

- **Done when:** - Success: Draft PRD is created with PM approval.
- Failure: > 2 tool errors in a run → log + abort.
- Escalation: confidence < 70% on any P0 → hand to PM.
- Timeout: 90s wall clock → abort with partial output.
- **Fails safe when:** Agent can READ Slack #escalations + Strategy KB + JIRA tickets. Agent can WRITE to structured insights and Draft PRD. Agent CANNOT edit write or edit tickets, strategy documents, access user accounts/permissions, evaluation scores. 
