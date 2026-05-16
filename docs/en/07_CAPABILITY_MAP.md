# 07 CAPABILITY MAP

This document breaks features into capability loops. Before implementing, the agent must find the matching capability.

## Capability Loop Template

| Field | Content |
|---|---|
| Capability name | To be filled |
| Related product truth | To be filled |
| User entry point | To be filled |
| UI | To be filled |
| API / action | To be filled |
| Data persistence | To be filled |
| Permission | To be filled |
| Error states | To be filled |
| Notification / feedback | To be filled |
| Tests | To be filled |
| Verification method | To be filled |
| Launch risk | To be filled |
| Known uncertainties | To be filled |
| Explicit non-goals | To be filled |
| Unfinished work | To be filled |

## Capability Classification

| Capability | Classification | Status | Notes |
|---|---|---|---|
| To be filled | current mainline / disabled / future work / historical reference | not started / partial / complete / blocked | To be filled |

## False-Completion Check

For every capability, ask:

- Is it only UI?
- Does the API really exist?
- Is data really persisted?
- Does it remain after refresh?
- Are permissions correct?
- Are error states handled?
- Do tests verify the real flow?
- Is it only available in engineering mode?
- Does it depend on an unresolved product, legal, payment, pricing, data, or provider decision?
- Does this capability violate an explicit non-goal in `02_PRODUCT_TRUTH.md`?

## Known Uncertainties

When the agent encounters these, it must not invent a fixed answer. It should ask, degrade, or mark the item as blocked.

| Uncertainty | Affected Capability | Risk | Current Handling | Decision Owner |
|---|---|---|---|---|
| To be filled | To be filled | To be filled | stop / degrade / future work | To be filled |
