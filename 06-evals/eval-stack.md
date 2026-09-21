# Eval Stack · Juno

> Module 6 · Evals & Guardrails. Juno's layered evaluation stack, designed with the **M6 · Eval Stack Designer**. Paste the tool's markdown over this file.

## What "good" means

>=80% thumbs-up; regenerate rate <=15%; abandon rate <=20% on non-trivial intents

- Active: thumbs up/down on each Juno output; engagement patters (do users "regenerate" and "edit" committed insights?; free-text feedback when thumbs-down, sentiment in chat/Slack (unsolicited feedback, bug reports, praise)
- Passive: dismiss/suppress, time-to-first-action, abandon rate (PM closes thread without acting), churn (do users stop using Juno after 1st week?)

## The stack

| Layer | Evaluator | What it catches | Threshold / gate |
|---|---|---|---|
| Code-based | Automated checks · cadence: Every PR (CI gate) + nightly cron · owner: CI fails the PR. Eng owns format/citation. PM owns the accuracy bar. | - LLM-judge scores accuracy of top-3 (rubric-aligned) - Format check: valid markdown table with required columns - Citation check: each risk cites a message index that exists - Refusal check: contracts/legal language triggers refusal | >=90% golden-set accuracy; 100% format/citation/refusal pass |
| LLM-as-judge | Automated assessment on the golden set | Silent wrong outputs at the long tail | >=90% golden-set accuracy; 100% format/citation/refusal pass |
| Human | 06-evals/human-rubric.md · 2 graders + PM tiebreak per disagreement protocol · cadence: Weekly batch (Friday afternoon) | - Verification Enforcement: graders trace whether every committed insight has a source clause - Quote Accuracy: graders check whether quotes are verbatim, paraphrased, or fabricated - Strategic Alignment: graders score whether insights match the strategy doc's framing - Buildability: graders rate whether insights translate to actionable tickets | >=4.0/5 mean across accuracy + safety; 0 critical safety fails |

## Golden set

- write_roadmap refuses unverified insights 
- sample 10 recent commits for quote accuracy 
- Versioned in 06-evals/golden-set/
- Refresh quarterly and after every major incident

## Release gate

**Hard gates (auto-block):**

- verification enforcement  is <4.0 avg (if unverified insights leak to roadmap, Juno is broken) 
- guardrail audibility <4.0 avg  (if the trace is opaque, graders can't verify guardrails were fired) 
- anti-pattern recall <4.0 avg (if anti patterns aren't caught, low-quality requests ship unfiltered. Core filter is broken)

**Soft gates (PM sign-off):**

- source alignment is <3.5 avg (strategy matching is hard; weak matches are still usable)
- priority accuracy <3.0 (calibrating the P-levels is domain specific. One PM's P1 is another's P2)
- quote accuracy <3.5 (quotes are sensitive; paraphrasing erodes trust)
- build ability <3.0 (rough insights can be refined by the PM)

**User-feedback layer (online):** cadence Per request (real-time) + weekly aggregate review; owner PM reviews weekly; on-call PM triages >=2 thumbs-down on same intent within 24h.
