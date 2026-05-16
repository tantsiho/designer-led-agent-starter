# 17 DECISION LOG

This document records why decisions were made. It does not only store the final answer; it preserves rejected alternatives, tradeoffs, and reassessment triggers.

During long-running AI-agent work, agents may later overturn old decisions or repackage rejected alternatives as new suggestions. The decision log helps future agents understand why a path was not chosen.

## Usage Rules

- Write in product language. This does not need to be a formal ADR.
- Every important decision should link to product truth, rules, capabilities, or risks.
- If an alternative is rejected, explain why.
- If a decision may change later, record the reassessment trigger.
- If a new decision overrides an old one, do not delete the old entry; add supersedes / superseded by.

## Decision Index

| ID | Decision | Status | Scope | Date | File |
|---|---|---|---|---|---|
| D-0001 | To be filled | proposed / accepted / superseded | To be filled | YYYY-MM-DD | `DECISIONS/0001-template.md` |

## Decision Template

```md
# D-0001: Decision Title

## Status

proposed / accepted / superseded

## Context

What product, flow, risk, or engineering problem existed at the time?

## Decision

What was decided? Write in product language.

## Alternatives Considered

| Alternative | Why Not |
|---|---|
| To be filled | To be filled |

## Tradeoffs

- Gain:
- Cost:
- Risk:

## Non-Goals

What does this decision explicitly not handle?

- To be filled

## Reassessment Trigger

What would make this decision worth revisiting?

- To be filled

## Links

- Product truth:
- Rules:
- Capability:
- Risk:
```
