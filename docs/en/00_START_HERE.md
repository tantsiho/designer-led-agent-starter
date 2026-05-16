# 00 START HERE

This is the agent entry point.

The template workflow is:

1. Read the raw design draft
2. Extract product truth, rules, roles, flows, and states
3. Ask PM questions
4. After the designer answers, update source-of-truth docs
5. Create a capability map
6. Make architecture, data source, environment, and defense decisions
7. Only then start implementation
8. Audit after implementation and write discoveries back

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

If the design draft is too large, process it in batches and record what has and has not been organized.

## What To Do During Development

After every implementation pass, decide whether to update:

- product truth
- glossary
- rules
- PM questions
- flows / states
- capability map
- architecture decisions
- data source of truth
- environment model
- risk and defense
- acceptance and verification
- build audit

If a discovery is not written back into docs, the next agent will likely repeat the same mistake.
