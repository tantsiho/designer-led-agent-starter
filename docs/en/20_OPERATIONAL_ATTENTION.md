# 20 OPERATIONAL ATTENTION

This document defines which states should be marked as requiring attention in long-running flows, background work, external callbacks, or manual operations.

The goal is not to create more error messages. The goal is to make the agent understand that some states are not complete and not immediately failed. They need tracking, retry, graceful degradation, or human judgment.

## When Attention States Are Needed

Design explicit attention states when a flow:

- depends on background work or scheduled jobs
- depends on an external callback
- needs manual review, confirmation, or correction
- affects multiple records or multiple users in one operation
- can be retried after failure, but must not fake success
- allows public reads to degrade, but not mutations to silently succeed
- needs the next agent to know that work is still incomplete

## Suggested States

Do not use only `success` / `failed`. Long-running flows should at least distinguish:

| State | Meaning | Agent Behavior |
|---|---|---|
| `queued` | accepted, not started yet | report queued state and record enqueue time |
| `running` | processing now | avoid starting the same work twice |
| `retryable_failed` | failed but retryable | record reason, retry count, and next retry condition |
| `manual_review_required` | needs human judgment | stop automatic completion claims and list what a human must inspect |
| `completed` | done | record completion evidence |

Projects may rename these states, but they should preserve the same meanings.

## Attention Is Not Always Error

Separate attention into two categories:

| Type | Example | Report As |
|---|---|---|
| Non-error attention | waiting for external callback, waiting for manual review, scheduled job not run yet | waiting condition and next step |
| Error attention | external service failed, data mismatch, retry budget exhausted | impact, blocked scope, and repair path |

Do not report "waiting" as failure. Do not package "needs manual handling" as completion.

## Trace Fields

Flows that can require attention should keep at least:

| Field | Purpose |
|---|---|
| `trace_id` | connects request, job, callback, and audit |
| `actor_id` | who triggered the work |
| `subject_id` | the main resource being processed |
| `step` | where the flow is blocked |
| `status` | current state |
| `attention_reason` | why attention is needed |
| `first_seen_at` | when this state first appeared |
| `last_attempt_at` | most recent processing attempt |
| `retry_count` | retry count |
| `next_action` | automatic retry, manual action, or abandon |

If the data set is large, summarize only the first few ids and record the omitted count. Do not dump large or sensitive data into logs or reports.

## Agent Report Format

When operational attention appears, report at least:

- what happened
- whether this is waiting, retryable failure, or manual handling
- which capability or user path is affected
- which trace / audit data exists
- whether the next step is automatic or human-owned
- which part cannot be claimed complete yet

## Writeback

When a flow adds an attention state, check and update:

- `06_FLOWS_AND_STATES.md`
- `07_CAPABILITY_MAP.md`
- `11_RISK_AND_DEFENSE.md`
- `12_ACCEPTANCE_AND_VERIFICATION.md`
- `13_BUILD_AUDIT.md`
- `19_CUTOVER_AND_INCIDENT_LESSONS.md`

