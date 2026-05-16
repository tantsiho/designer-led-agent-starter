# 14 DOCS MAINTENANCE

This document defines document layering and long-term maintenance.

Specification documents are not written once before development and then frozen. They are strengthened throughout development. Every implementation, audit, launch check, risk check, or designer correction can make source-of-truth docs more complete.

## Document Layers

| Type | Purpose | Examples | Rule |
|---|---|---|---|
| current source truth | future agents must follow | PRODUCT_TRUTH, RULES, FLOWS | read first |
| working draft | not final yet | PM_QUESTIONS | not hard rules |
| historical reference | understand context | old notes | must not override current truth |
| archive | outdated | archive | verify only, do not assume |
| runbook | operation and verification | deployment, smoke | use by environment |

## Writeback Rules

Update docs when:

- the designer adds or corrects product truth
- implementation reveals a rule conflict
- a capability becomes disabled or future work
- an architecture decision changes
- local versus launch environment differences are discovered
- a new risk or abuse case is discovered
- tests or smoke checks reveal flow gaps

## Specs Generated During Development

If the agent discovers any of these during implementation, it should update docs as well as code:

- previously undefined role or permission
- previously undefined state transition
- previously undefined error handling
- previously undefined data storage location
- previously undefined environment difference
- previously undefined abuse case
- previously undefined acceptance criteria
- previously undefined "not now" or "future work" boundary

Principle:

> Every pitfall should become a spec that the next agent does not need to rediscover.

## Archive Rules

When a document is outdated, do not delete it directly. Instead:

1. Mark it archived
2. Explain why it was archived
3. Point to the new source-of-truth document
4. Prevent future agents from misusing it
