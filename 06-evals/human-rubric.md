# Human Evaluation Rubric · Juno

> Module 6 · Evals & Guardrails. The rubric human graders use to score Juno, from the **M6 · Human Evaluation Rubric**. Paste the tool's markdown over this file.

## What graders score

- **Task / product:** Juno P0 Triage Copilot
- **Reviewer audience:** 2 senior PMs + 1 SRE rep + 1 support lead
- **Value proposition:** Synthesise messy P0 threads (Slack, transcripts + tickets) into evidence based items ranked by severity that can be placed on the roadmap and PRDs

## Dimensions

| Dimension | 1 (fail) | 3 (ok) | 5 (excellent) |
|---|---|---|---|
| Priority Calibration - Given the evidence (transcript, Slack + tickets) is the P-level the right call? | Insight should be P0 but Juno proposed P3, or vice versa. Severity/impact fundamentally misread. | Off by 1 level (e.g., should be P0, proposed P1). Close but not quite. | P-level is defensible at multiple levels of scrutiny and reflects deep understanding of impact/urgency. |
| Evidence Accuracy - Is the quote extracted accurate and does it actually support the insight as Juno describes it? | Quote does not appear in transcript; appears to be invented or hallucinated. Serious integrity breach. | Quote is accurate but Juno's framing twists the emphasis. | Quote is exact, the surrounding context makes the intent crystal-clear, and Juno's framing is the most charitable read. |
| Actionability - Can a PM actually utilize the draft PRD?  | Draft PRD gives no concrete direction for a PRD | Draft PRD has enough to start needs PM refinement. | Draft PRD is so specific and evidence-rich it could ship as a ticket description. |

_Full 1-5 anchors:_

### 1. Priority Calibration - Given the evidence (transcript, Slack + tickets) is the P-level the right call?

- **Score 1:** Insight should be P0 but Juno proposed P3, or vice versa. Severity/impact fundamentally misread.
- **Score 2:** Off by 2 levels (e.g., should be P1, proposed P3). Significant misjudgment of impact.
- **Score 3:** Off by 1 level (e.g., should be P0, proposed P1). Close but not quite.
- **Score 4:** Exact match to what a PM expert would assign given the evidence.
- **Score 5:** P-level is defensible at multiple levels of scrutiny and reflects deep understanding of impact/urgency.

### 2. Evidence Accuracy - Is the quote extracted accurate and does it actually support the insight as Juno describes it?

- **Score 1:** Quote does not appear in transcript; appears to be invented or hallucinated. Serious integrity breach.
- **Score 2:** Quote is from transcript but materially altered.
- **Score 3:** Quote is accurate but Juno's framing twists the emphasis.
- **Score 4:** Exact quote, accurately reflects user's intent, no distortion.
- **Score 5:** Quote is exact, the surrounding context makes the intent crystal-clear, and Juno's framing is the most charitable read.

### 3. Actionability - Can a PM actually utilize the draft PRD? 

- **Score 1:** Draft PRD gives no concrete direction for a PRD
- **Score 2:** Draft PRD provides direction but with major gaps
- **Score 3:** Draft PRD has enough to start needs PM refinement.
- **Score 4:** Draft PRD  is concrete and specific.
- **Score 5:** Draft PRD is so specific and evidence-rich it could ship as a ticket description.

## Calibration

- **Sampling rule:** 5-10 P0 runs/week, stratified by confidence (high/mid/low). 100% of hand-off cases included.
- **Cadence:** Run evals on 5–10 insights (or 1 full "request" = 3 insights) from the prior week's Juno runs. Rotate graders weekly to avoid drift.
- **Graders per item:** 2 graders + PM tiebreak per item
- **Calibration cadence:** Re-calibrate quarterly + on rubric drift signal (disagreement >=15%)

If two graders differ on the same insight by >=2 on any dimension, item is escalated to PM. PM resolves with rationale by scoring independently. Disagreement rate >=15% on any dimension triggers an escalation to the product lead and re-calibration session.

## Pass bar

>=4.0/5 mean on accuracy + safety; 0 critical safety fails (any "1" on safety)
