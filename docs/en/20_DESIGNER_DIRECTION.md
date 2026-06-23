# 20 DESIGNER DIRECTION

This document is for designer direction control.

It is not an engineering checklist and not a product-specific template. Its purpose is to help a non-engineering designer keep leading the agent: correct misreadings, protect product intent, mark what should not be built, and force the agent back to source-of-truth docs instead of letting implementation details take over.

## What The Designer Controls

The agent can organize, ask questions, implement, and verify. Product direction must still be controlled by the designer:

- what the product is really trying to solve
- what the product is not
- which capabilities are current mainline
- which capabilities are only future possibilities
- which experiences must not be pulled into a generic template
- which user misunderstandings must never happen
- which decisions are intentional tradeoffs, not things the agent can overturn

## When To Intervene

Stop the agent and correct direction when:

- the agent forces the product into a generic SaaS / marketplace / dashboard template
- the agent invents business models, roles, or flows you did not define
- the agent packages future capabilities as current scope
- the agent changes product rules for engineering convenience
- the agent ignores non-goals or known uncertainties
- the agent reports completion but only completed a screen or technical task
- the copy makes the product look more mature than its real stage
- the agent tries to implement a question that has not been decided

## Phrases You Can Use

```text
You are drifting from the product direction. Do not change code yet. Return to PRODUCT_TRUTH and RULES, then restate what this product is, what it is not, and what the current mainline is.
```

```text
This is not my product judgment. List your assumptions, mark which ones have no source truth, then turn them into PM questions for me.
```

```text
Do not force this into a generic product template. First list how this product differs from the generic template, then propose the implementation scope again.
```

```text
What is this version intentionally not doing? Write it into NON_GOALS so future agents do not add it back.
```

```text
Record this decision in product language: why we chose it, which alternatives were rejected, what tradeoff it carries, and when to reassess.
```

## Direction Check

Before implementation, the designer can ask the agent:

| Question | Purpose |
|---|---|
| Which capability are we completing in this pass? | prevent the agent from doing too much |
| Which source-truth doc does this capability map to? | avoid implementation from chat memory |
| What are we intentionally not doing this pass? | prevent scope creep |
| Which assumptions are not confirmed by the designer yet? | prevent invented rules |
| Could this make the product look like a different generic template? | protect positioning |
| How will we verify this is not only a screen? | preserve completion criteria |

## Where Designer Answers Should Be Written Back

- product direction: `02_PRODUCT_TRUTH.md`
- terms and meaning: `03_GLOSSARY.md`
- hard rules / forbidden behavior: `04_RULES.md`
- open questions: `05_PM_QUESTIONS.md`
- flows and states: `06_FLOWS_AND_STATES.md`
- mainline and disabled capabilities: `07_CAPABILITY_MAP.md`
- important tradeoffs: `17_DECISION_LOG.md`
- product contradictions: `18_CONTRADICTION_AUDIT.md`

## Core Principle

Designer-led does not mean the designer needs to understand every engineering detail.

Designer-led means the agent must not replace product judgment with engineering details, generic templates, or its own guesses. When direction is unclear, the agent should return to the designer, source-of-truth docs, and explicit tradeoffs.
