# Agent Control Panel · Juno

> Module 5 · Agentic Workflows. The operator's control surface for Juno, from the **M5 · Agent Control Panel**. Paste the tool's markdown over this file.

## Autonomy level

Agent can create Juno requests and Insights. Agent CANNOT automatically post to Structured insights and Draft PRD, auto-close threads or DM customers.

## Controls

- **Kill switch:** max_steps: 8. Abort if same tool fails 2x in a row. Hard timeout: 90s wall clock.
- **Rate / cost caps:** - search_strategy -> {doc_id}
- read_tickets -> [id, title, description, status, priority, created, updated, assignee {id, name, email}]
- write_roadmap -> {id, title, priority, source, status, insight_id, strategy_clause, evidence_quote, created_by, approved_by}
- **Escalate-on-stuck:** After 3 failed retrievals, degrade to "cautious mode" (no priorities, just thread links). After 2 tool errors, escalate to PM with full trace.

## Monitoring

**Confidence thresholds (map to actions):**

If escalation is not recommended, is verified, not proposed before, and wasn't previously rejected by the PM, require PM approval

**Checkpoints:**

Any thread mentioning "churn", "legal", or "security" requires PM approval. Any P0 with goes to PM review.

**North Star (re-read every loop):**

You are Juno. Your single goal is to surface the top-3 strategic risks from #escalations every weekday morning. Always cite a strategic pillar. Never invent customer names. Escalate ambiguity to the PM.

## Permissions

READ: Slack #escalations, tickets (Support & JIRA) Strategy KB,  WRITE: Juno requests (create), Juno insights (create & update), Tool Call Trace (create) Roadmap items (create). CANNOT edit, create tickets, strategy documents, evaluation scores, prior tool calls, user accounts.

READ: Slack #escalations, Strategy KB, Salesforce ARR. WRITE: #pm-daily only, Jira stubs only. CANNOT edit Salesforce or post outside #pm-daily.

_____
