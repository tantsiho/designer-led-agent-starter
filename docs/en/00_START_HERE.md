# 00 START HERE

This is the agent entry point.

The template workflow is:

1. Read the raw design draft
2. Extract product truth, rules, roles, flows, and states
3. Ask PM questions
4. After the designer answers, update source-of-truth docs
5. Create a capability map
6. Record important decisions, known uncertainties, and explicit non-goals
7. Make architecture, data source, environment, defense, and cutover decisions
8. Actively find product contradictions and impossible states
9. For high-risk flows, define operational attention, negative smoke, and concurrency / idempotency checks
10. Only then start implementation
11. Audit after implementation and write discoveries back

This order is not a one-time setup. Every new feature, risk, environment difference, or product judgment should return to the docs, update source truth, and then continue.

## Things The Agent Must Not Skip

- Do not code directly from `01_RAW_DESIGN.md`
- Do not force a generic product template onto the project
- Do not treat UI as completion
- Do not treat local smoke tests as a launch guarantee
- Do not lower the completion bar because the user is a beginner

## What To Do In The First Pass

If `02_PRODUCT_TRUTH.md` through `12_ACCEPTANCE_AND_VERIFICATION.md` are still empty, the first pass is organization only. Do not implement.

Produce or update:

- `02_PRODUCT_TRUTH.md`
- `03_GLOSSARY.md`
- `04_RULES.md`
- `05_PM_QUESTIONS.md`
- `06_FLOWS_AND_STATES.md`
- `07_CAPABILITY_MAP.md`
- `17_DECISION_LOG.md`
- `18_CONTRADICTION_AUDIT.md`
- `19_CUTOVER_AND_INCIDENT_LESSONS.md`
- `20_OPERATIONAL_ATTENTION.md`
- `21_NEGATIVE_SMOKE_AND_FAIL_CLOSED.md`
- `22_CONCURRENCY_AND_IDEMPOTENCY.md`

If the design draft is too large, process it in batches and record what has and has not been organized.

## What To Do During Development

After every implementation pass, decide whether to update:

- product truth
- glossary
- rules
- PM questions
- flows / states
- capability map
- decision log
- known uncertainties
- product contradictions / impossible states
- architecture decisions
- data source of truth
- environment model
- cutover / incident lessons
- operational attention
- negative smoke / fail-closed
- concurrency / idempotency
- risk and defense
- acceptance and verification
- build audit

If a discovery is not written back into docs, the next agent will likely repeat the same mistake.
