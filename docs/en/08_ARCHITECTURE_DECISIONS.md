# 08 ARCHITECTURE DECISIONS

This document records architecture choices. Beginners do not need to understand all options upfront; the agent should explain tradeoffs in plain language.

## Basic Architecture

- Frontend:
- Backend:
- Database:
- Identity system:
- File / image storage:
- External services:
- Deployment platform:

## Decision Record

| ID | Decision | Options | Why This Choice | Risk | Replaceable Later |
|---|---|---|---|---|---|
| ADR-001 | To be filled | To be filled | To be filled | To be filled | To be filled |

## Architecture Gate Check

Before implementation, the agent must answer:

- Does this capability need a backend?
- Does it need database persistence?
- Does it need identity / permissions?
- Does it need background jobs, scheduling, webhooks, or external providers?
- What can be mocked first?
- What cannot be mocked?
- Will this choice block future core capabilities?
