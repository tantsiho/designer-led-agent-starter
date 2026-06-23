# 15 NATURAL LANGUAGE EXAMPLES

This document is for beginners who do not want to memorize commands. You can speak to the agent in ordinary language.

## When Pasting Raw Design

```text
This is my product design draft. Do not write code yet. First organize product truth, roles, rules, flows, contradictions, and questions I need to answer.
```

```text
This design is messy. Do not rush into implementation. First separate core rules, loose ideas, and possible future features.
```

## When You Want The Agent To Ask Questions

```text
Act as a PM. Find the unclear, contradictory, or blocking parts of this design, then ask me in a way I can answer.
```

```text
Do not ask me with engineering jargon. Turn the questions into product decisions so I can answer how this feature should work.
```

## After Answering Questions

```text
These are my answers. Update product truth, rules, flows, and the capability map. Do not start coding yet.
```

```text
Write the clarified rules back into the docs and mark which questions are still unanswered.
```

## When Preparing To Implement

```text
Build the first core flow now. Before starting, read the source-of-truth docs and list the UI, API, data persistence, permissions, error states, and verification method this capability needs.
```

```text
Do not build everything at once. Choose the smallest complete capability loop, and after building it verify that it is not only a screen.
```

## When Worried AI Built Only Half

```text
Check whether this feature is only UI. Confirm API, data persistence, permissions, error states, and whether data remains after refresh.
```

```text
Use the BUILD_AUDIT format: what is truly complete, what only appears to exist, and what has not been verified?
```

## When Worried Local Works But Launch Fails

```text
Separate whether this verification was local, engineering mode, staging, or production-like. Do not describe local passing as launch-ready.
```

```text
If this feature is going to launch, what env vars, external services, database setup, permissions, or post-deploy smoke checks are still missing?
```

## When Worried About Security And Abuse

```text
Review this flow with defensive thinking: unauthorized access, duplicate submission, direct route, data leak, error messages, audit, and rate limit.
```

```text
Assume a user wants to exploit this feature. How could they abuse it? List the risks and minimum defenses.
```

## When The Agent Drifts From Product Direction

```text
Your understanding is drifting toward a generic product template. Return to PRODUCT_TRUTH, restate what this product is not, then correct the rules.
```

```text
This feature is not in the direction I want. Do not change code directly. First correct product truth and rules, then propose a new implementation plan.
```

## After Each Build

```text
Report which source truth this maps to, what changed, what was verified, what was not verified, whether mock or engineering mode was used, and what launch checks are still needed.
```

## When Recording Decisions

```text
Write this product decision into DECISION_LOG: why it was decided, which alternatives were rejected, what the tradeoffs are, and when it should be reassessed.
```

```text
This is not an engineering ADR. Write it in product language so the next agent does not overturn it later.
```

## When Finding Product Contradictions

```text
Do not implement. First use CONTRADICTION_AUDIT to check flow conflict, business contradiction, impossible state, incentive mismatch, and data inconsistency.
```

```text
Find where this design makes user states, data truth, permissions, or copy contradict each other.
```

## When Handling Cutover / Production Incident Review

```text
Do not only say migration is done. Use CUTOVER_AND_INCIDENT_LESSONS to check env, auth, storage, email, provider dashboard, schema drift, rollback, and production smoke gates.
```

```text
Turn this production issue into an incident lesson: what happened, root cause category, what was automated, which manual gates remain, the fixed process going forward, and which verification levels must not be confused.
```

## When Correcting Design Direction

```text
Use DESIGNER_DIRECTION to check this pass: did the agent drift into a generic template, add assumptions I never gave, or treat future work as current scope?
```

```text
Do not package inference as product truth. List your assumptions, which ones have no source truth, what I need to answer, and which doc should be updated.
```
