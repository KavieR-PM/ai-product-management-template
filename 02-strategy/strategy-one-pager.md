# AI Strategy One-Pager - Juno Automated Prioritization

# AI Strategy One-Pager - Juno Automated Prioritization

## 1. Problem & Workflow

The Problem: RocketShip PMs waste 2–3 hours per week wading through P0/P1 escalations across Slack (#escalations), Notion (Product workspace), and Jira (ROCKET project) to synthesize a ranked risk list. Result: priority mismatches, duplicated triage work, and slow response to customer-blocking issues.

Prevention: Juno explicitly prevents unverified and fabricated claims from the risk list. Every claim cites its Slack thread ID, Jira key, or Notion page. Ambiguous sources are flagged "NEEDS CLARIFICATION" instead of guessed.

## 2. Target Metrics

Cycle time: Time from escalation spike to prioritized risk list drops from 2–3 hours to <15 minutes. Measurable in ≤ 30 days (first beta use case).

Leadership proof:
100% of claims are sourced (zero fabricated customer names, ARR, or contractual terms)
Zero instances of verification gate or citation enforcement failing
PM adoption ≥ 20% in first week; daily active users ≥ 15% by week 4

## 3. Autonomy Level

Choice: Copilot. Juno synthesizes and ranks escalations, but requires explicit PM approval before publishing the risk list. The PM remains the decision-maker; Juno is the synthesis engine.

Explicitly avoiding:
Agent (autonomous escalation triage without approval—unacceptable for customer-blocking decisions)
Assist (read-only synthesis, no priority ranking—misses the point)

## 4. Data & Model Approach

Approach: Ground (RAG). Juno reads Slack threads (#escalations), Notion pages (Product workspace), and Jira tickets (ROCKET project) as the sources of truth. Every claim is traced back to its original source. No external data; no fabrication tolerance.

Explicitly avoiding:
Fine-tuning (not cost-effective for variable escalation patterns)
Buy-only LLM (no grounding means no source citation, verification gate becomes impossible to enforce)

## 5. Risks & Mitigations

Risk: Fabricated or unverified claims reach the risk list (e.g., invented customer name, ARR, or contractual term), eroding trust in escalation triage and causing the PM to act on false information.

Mitigation: Immutable audit trail with code-enforced citation gate. Every claim in the output requires:
- Source citation (Slack ID, Jira key, or Notion page link)
- Verification check (exact quote from source or marked "NEEDS CLARIFICATION")
- Immutable trace log
Any missing source or fabricated claim blocks publication entirely. Zero exceptions.

## 6. V1 Scope

In:
- Read Slack #escalations threads, Notion Product workspace pages, Jira ROCKET tickets
- Synthesize P0/P1 escalations into a ranked risk list (max 5 rows)
- Cite every claim with Slack ID, Jira key, or Notion link
- Suggest action for each risk
- Full audit trail logged
- PM approval required before publishing

Out:
- Does NOT publish risk list without PM approval
- Does NOT generate claims from external sources (web search, competitor research, etc.—only Slack, Notion, Jira)
- Does NOT invent customer names, ARR, or contractual terms (refuse and mark "NEEDS CLARIFICATION")
- Does NOT handle requests involving contracts, legal, or regulators (hand off to human PM)
