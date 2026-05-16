# 18 CONTRADICTION AUDIT

This document makes the agent actively find product contradictions instead of only organizing design drafts.

A truly designer-led agent should do more than "avoid making things up." It should point out issues that will break later implementation: flow conflicts, business contradictions, impossible states, incentive mismatches, and inconsistent data truth.

## When To Use

- after the first raw-design organization pass
- after PM questions are answered
- before implementing a core capability
- after implementation reveals conflicting states or data
- before launch readiness review

## Contradiction Types

| Type | Check Question | Example |
|---|---|---|
| Flow conflict | Can two flows produce opposite outcomes? | cancellation and payment completion both succeed |
| Business contradiction | Does the business promise conflict with the actual rule? | copy promises instant completion, but manual review is required |
| Impossible state | Does the state machine allow an impossible state? | an order is both canceled and fulfilled |
| Incentive mismatch | Does the user's best move undermine the product goal? | users can exploit cancellation / retry loops |
| Data inconsistency | Can two sources answer the same fact differently? | frontend says complete, DB says pending |
| Permission contradiction | Does visible UI exceed role permissions? | a seller can see another seller's data |
| Copy contradiction | Does copy imply a disabled capability is available? | button says pay now, but MVP has no payments |

## Audit Table

| ID | Type | Finding | Impact | Needs Decision | Handling |
|---|---|---|---|---|---|
| C-001 | To be filled | To be filled | To be filled | yes / no | fix / ask / document / defer |

## Agent Prompt

```text
Do not implement. Based on the current PRODUCT_TRUTH, RULES, FLOWS, CAPABILITY_MAP, and PM_QUESTIONS, actively find product contradictions.

Check these categories:
1. flow conflict
2. business contradiction
3. impossible state
4. incentive mismatch
5. data inconsistency
6. permission contradiction
7. copy contradiction

For every finding, say:
- where the contradiction is
- what consequence it creates
- whether it blocks the current capability
- what the designer needs to answer
- which source-of-truth doc should be updated
```
