# Agent Control Panel · Juno

> Module 5 · Agentic Workflows. The operator's control surface for Juno, from the **M5 · Agent Control Panel**. Paste the tool's markdown over this file.

## Four Levers

**Stop Conditions** (Loop):

Max steps: 5
Juno's loop: read strategy → extract candidate insights → verify each insight → batch writes to roadmap → audit log. Five steps max; no iterative refinement loops.

Abort if:
Verification gate fails (unverified insight detected attempting to reach write_roadmap)
Same tool fails 2x in a row (e.g., two consecutive read_strategy failures)
write_roadmap rejected for any reason (permission tier enforcement, approval missing, etc.)
Audit log fails to record a write (critical integrity failure—hard stop)

Hard timeout: 30 seconds wall clock
Strategy synthesis should be fast. If Juno hits 30s, abort and return partial results to PM.

**Structured Tool Outputs** (Tools):

read_strategy	{status: "success", text: string, word_count: int}	{status: "failed", error: string}	Abort if word_count < 500 (strategy too thin) OR status="failed"

extract_insights	{status: "success", insights: [{text, confidence_0_to_100}], count: int}	{status: "failed", error: string}	Abort if count=0 (no insights found) OR status="failed"

verify_insight	{status: "verified" | "paraphrased" | "unverified", source_clause: string, match_score_0_to_100: int}	{status: "error", error: string}	Never silent. Unverified goes to PM review, not abort. Error → abort.

write_roadmap	{status: "committed", roadmap_id: string, timestamp: ISO8601}	{status: "rejected", reason: string, error: string}	Abort if status="rejected". No partial commits.
log_audit	{status: "logged", trace_id: string, timestamp: ISO8601}	{status: "failed", error: string}	CRITICAL: status="failed" → hard abort. Audit trail break cannot be hidden.

**Confidence Thresholds** (Verification):

High Confidence (Juno commits autonomously):

Insight is verified (match_score ≥ 95)
Extraction confidence ≥ 80%
Guardrails all passed
Action: write_roadmap directly, log to audit trail

Medium Confidence (Goes to PM review first):

Insight is paraphrased (match_score 70–94, status="paraphrased")
Extraction confidence 60–79%
Guardrails passed but with warnings
Action: Draft the insight, surface to PM in review queue with confidence score and warning flags. Require PM approval before write_roadmap.

Low Confidence (Waits for PM approval):

Insight is unverified (match_score < 70, status="unverified")
Extraction confidence < 60%
Guardrail concern (e.g., quote accuracy low)

**North Star** (Context):

Extract verified insights from strategy with PM approval and audit every step; never ship unverified work, never skip approval, never hide a guardrail failure.

## Rules of Engagement

**Agency Permission:**

Extract Insights - read strategy, generate insights 
Verify Insight - check verbatim match, score confidence

**Access Control:**

Strategy document - source of truth for extraction
Roadmap items - to understand structure, audit log - trace every decision

**Fallback Protocols:**

Verification fails - unverified insight detected
Tools fail 2x in a row - same tool errors
Audit log fails - cannot write to the trace

**Checkpoints:**

Approval modal - Before any write_roadmap
Verification review - Insight marketed unverified
