# 22 CONCURRENCY AND IDEMPOTENCY

This document defines what agents must check when handling duplicate submissions, retries, external callbacks, background jobs, multiple tabs, or concurrent operations.

A disabled frontend button is not concurrency protection. If the same operation can be triggered by an API call, retry, callback, script, or multiple tabs, deeper defenses are required.

## When To Check

Check concurrency / idempotency when:

- a user can click or submit twice
- a browser, network layer, or SDK can retry
- an external callback can be resent
- a background job can run again
- multiple actors can modify the same record
- one operation writes multiple records or triggers side effects
- success sends a notification, updates audit, or starts another flow

## Defense Layers

| Defense | Good For | Not Enough For |
|---|---|---|
| frontend disabled / loading state | user experience | direct API, retry, multiple tabs |
| API duplicate guard | short-window duplicate from the same actor | needs stable key and database support |
| idempotency key | same operation replay returns same result | key scope and request fingerprint must be clear |
| unique constraint | prevents duplicate records | needs clear error and response strategy |
| transaction / row lock | consistent multi-record writes | requires stable lock order and short transactions |
| durable queue | retryable background work | still needs dedupe, status, and attention policy |

## Idempotency Key Rules

An idempotency key should include or bind to:

- actor scope
- operation type
- subject / resource id
- request fingerprint
- creation time or expiry
- final result or replayable response

When the same key is submitted again, return the same result or reject clearly. Do not create a second side effect.

## Transactions And Side Effects

Multi-step operations need an explicit transaction boundary:

- which records must succeed or fail together
- which side effects can happen only after durable write success
- whether audit records attempt, success, or failure
- whether notifications, external calls, or scheduled work can be retried
- whether rollback leaves a misleading success signal

General rule: do not claim external side effects completed before the core data has committed.

## Concurrency Report Format

When building or auditing a high-risk operation, report:

- which entry points can trigger duplicates
- which defense layer is used
- the scope of the idempotency key or unique constraint
- transaction boundary
- what retry / replay returns
- which side effects happen only after commit
- which cases remain unverified

## Rehearsal

Minimum rehearsal should include:

| Scenario | Expected Result |
|---|---|
| submit twice in sequence | only one effect, or second returns the same result |
| retry the same request | no second record |
| callback replay | no new side effect |
| rerun background job | completed items are not repeated |
| two actors modify the same record | result follows locking, version, or conflict rules |

