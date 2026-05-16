# AGENTS

This file defines operating rules for AI agents. The user may not be an engineer and may not use fixed commands. The agent must infer the task mode from natural language and actively turn rough design input into executable source of truth.

## 0. Highest-Priority Principles

1. **Design documents are the source of truth.**
   - Completion is judged by design documents, rule sources, and capability closure, not by whether a screen exists or tests pass.
   - The decision order is:
     1. Does it match product truth?
     2. Does it match rules and capability boundaries?
     3. Does it close the UI / API / data / permission / error / test loop?
     4. Has the matching verification been completed?

2. **Raw design input is not the implementation entry point.**
   - Raw design can be long, messy, repeated, and amended over time.
   - Do not code directly from `docs/en/01_RAW_DESIGN.md`.
   - First extract product truth, glossary terms, roles, rules, flows, states, contradictions, and PM questions.

3. **The designer owns product truth. The agent owns engineering closure.**
   - Do not require the designer to understand APIs, databases, auth, CI, deployment, or security vocabulary before work can start.
   - Ask in product language, then translate answers into engineering requirements.
   - Do not lower the completion bar because the user is new to engineering.

4. **Specification documents grow continuously.**
   - Extract source-of-truth docs before building, and keep writing back during development.
   - Every implementation pass, audit, environment check, risk check, or designer correction can create new rules.
   - New rules must be written back into the matching source document, not left in chat history.

5. **Do not shrink scope by assuming traditional team cost.**
   - This template exists so the agent catches checks that beginners usually miss.
   - Value priority can decide sequencing, but it cannot reduce the completion standard for a capability that has entered scope.

6. **Capabilities that enter scope must close consistently with the design.**
   - Do not accept half-built flows, fake entry points, misleading copy, mock-only behavior, or behavior that contradicts the design.
   - If a capability is future work or disabled, mark it clearly and keep UI / API / direct route behavior consistent.

7. **Make surgical edits.**
   - Do not delete, simplify, or refactor unrelated logic.
   - Change only the scope directly related to the current request.
   - Do not opportunistically alter code just because it looks optimizable.

8. **MVP does not mean production guarantee.**
   - Passing locally does not mean production-ready.
   - If staging, production-like, or post-deploy smoke tests have not run, say so explicitly.

## 1. Required Agent Entry Point

If a task involves product understanding, flows, identity, payments, orders, permissions, data persistence, launch, security, operations, or source-of-truth docs, read these first:

1. `docs/en/00_START_HERE.md`
2. `docs/en/02_PRODUCT_TRUTH.md`
3. `docs/en/03_GLOSSARY.md`
4. `docs/en/04_RULES.md`
5. `docs/en/06_FLOWS_AND_STATES.md`
6. `docs/en/07_CAPABILITY_MAP.md`
7. `docs/en/08_ARCHITECTURE_DECISIONS.md`
8. `docs/en/09_DATA_SOURCE_OF_TRUTH.md`
9. `docs/en/10_ENVIRONMENT_MODEL.md`
10. `docs/en/11_RISK_AND_DEFENSE.md`
11. `docs/en/12_ACCEPTANCE_AND_VERIFICATION.md`

Notes:

- `docs/en/01_RAW_DESIGN.md` is raw material only; do not use it as direct implementation truth.
- `docs/en/05_PM_QUESTIONS.md` contains unresolved questions. If any affect the current implementation pass, ask first.
- `docs/en/14_DOCS_MAINTENANCE.md` defines conflict and archive rules. Current source-of-truth docs win over historical references.
- `docs/en/15_NATURAL_LANGUAGE_EXAMPLES.md` helps infer mode when users do not use commands.

If required source documents do not exist yet, create or fill them before implementation.

## 2. Natural-Language Work Modes

The user may describe needs in ordinary language. Infer the current mode:

1. **Design Intake**
   - The user shares a long draft, idea, design doc, or chat excerpt.
   - Extract and organize only. Do not code.

2. **Truth Update**
   - The user adds, corrects, or says "not like that."
   - Update product truth, rules, flows, or the capability map.

3. **PM Clarification**
   - The design contains contradictions, ambiguity, or undefined flows.
   - Ask product-language questions instead of forcing engineering terms.

4. **Build**
   - The user says "start," "do this first," or similar.
   - Read source docs and the capability map, then implement one clear capability line.

5. **Review / Audit**
   - The user asks whether something is right, complete, or half-built.
   - Review first. Do not implement unless asked or necessary to complete the task.

6. **Readiness Review**
   - The user asks whether it can launch or be used.
   - Separate local, engineering, staging, production-like, and unverified states.

When unsure, ask PM-style clarification questions.

## 3. Design Extraction Rules

When extracting from raw design, organize at least:

1. What the product is / is not
2. User roles and permissions
3. Core flows
4. States and state transitions
5. Identity and data ownership
6. Data that must be saved
7. Data that must not be exposed
8. Failure states and exceptions
9. Forbidden behavior
10. Current mainline / disabled capability / future work / historical reference
11. Areas where generic product templates may mislead the agent
12. Contradictions, vague terms, and undefined questions

After extraction, update:

- `docs/en/02_PRODUCT_TRUTH.md`
- `docs/en/03_GLOSSARY.md`
- `docs/en/04_RULES.md`
- `docs/en/05_PM_QUESTIONS.md`
- `docs/en/06_FLOWS_AND_STATES.md`
- `docs/en/07_CAPABILITY_MAP.md`

## 4. PM Question Rules

The agent must proactively ask:

1. Does this term have a fixed definition?
2. When these two rules conflict, which wins?
3. What happens when the user is logged out, unauthorized, missing data, or an external service fails?
4. Is this required for MVP, disabled for now, or future work?
5. When disabled, should UI, API, and direct routes all reject it?
6. What state counts as done?
7. What must users never misunderstand?
8. What data must never appear in URLs, public pages, logs, or error messages?
9. What behavior could be abused?
10. What needs admin or operations traceability?

After the user answers, write the answer back into source-of-truth docs.

## 5. Editing Safety Rules

1. Do not delete, comment out, replace, or simplify existing logic unless the user explicitly asks.
2. Prefer touching only files directly related to the request. Open dependencies only as needed.
3. UI tasks should default to visual, layout, className, and necessary component-structure changes unless the request involves flow behavior.
4. Flow, security, identity, order, payment, launch, and E2E tasks should change only the relevant logic and verification.
5. Do not modify code just because it looks unused or optimizable.
6. Before finishing UI work, check for duplicate features, duplicate entry points, and duplicate buttons.

## 6. Architecture Choice Gate

Before implementation, decide:

1. Is this capability frontend-only, full-stack, or does it need an independent backend?
2. Does it need persistent storage?
3. Does it need identity, permissions, sessions, or re-authentication?
4. Does it need files, images, notifications, scheduling, webhooks, payments, or external providers?
5. What can be mocked, and what cannot?
6. Will the current choice block future core capabilities?
7. Does it need admin, ops, or audit surfaces?

Record the result in `docs/en/08_ARCHITECTURE_DECISIONS.md`.

## 7. Data Source Gate

For any data-related capability, answer:

1. What is the source of truth for this data?
2. Does it need persistence?
3. Does it remain consistent after refresh, restart, or re-login?
4. If local, seed/mock, and remote data conflict, which wins?
5. What data must not appear in URLs, public pages, logs, or error messages?
6. Can deleted, canceled, or expired data revive?

Record the result in `docs/en/09_DATA_SOURCE_OF_TRUTH.md`.

## 8. Environment / Launch Gate

During implementation and verification, distinguish:

1. local development
2. engineering mode
3. test / seed mode
4. staging / submission-like
5. production

Explain:

- whether real data or seed/mock data was used
- whether engineering-only entry points were involved
- required env vars or external services
- what must be disabled in production
- what local verification proves and does not prove
- what smoke checks are still needed after deploy

Record the result in `docs/en/10_ENVIRONMENT_MODEL.md`.

## 9. Defense / Risk Gate

For any account, payment, order, data, content, permission, admin, or callback flow, check:

1. unauthorized read / write
2. duplicate submission
3. webhook / callback replay
4. refund / abuse / fraud
5. direct route access
6. hidden API access
7. sensitive data exposure
8. URL / log / error message leaks
9. rate limits / idempotency
10. admin audit trail
11. destructive action confirmation

Record the result in `docs/en/11_RISK_AND_DEFENSE.md`.

## 10. Functional Completeness Audit

When checking whether a capability is truly done or launchable:

1. UI exposure does not equal completion.
   - Confirm API support, data persistence, permissions, and error states.

2. Mock / engineering-only behavior does not equal formal completion.
   - If mock, seed, or engineering mode was used, report it clearly.

3. Disabled capabilities must be consistently disabled.
   - UI, API, direct routes, copy, and tests must not pretend they work.

4. If product behavior is incomplete but tests were changed to pass:
   - Do not declare completion.
   - Fix product behavior first, then tests.
   - Do not make tests accept half-built, mock-only, or design-inconsistent behavior just to turn CI green.

5. For audits, update:
   - `docs/en/13_BUILD_AUDIT.md`
   - `AGENTS.md` if the working rule changes

## 11. Launch / Security / Verification Principles

1. The target is a verifiable MVP with basic safe operation, not a claim of mature production-grade readiness.
2. MVPs still need basic defense and traceability.
3. Prioritize:
   - consistent identity source
   - permission boundaries
   - high-risk mutation correctness
   - data persistence and data exposure boundaries
   - audit / traceability
   - local versus launch environment differences
4. Tests should protect high-risk flows. Do not lower the depth only because this is a beginner project.
5. Still distinguish:
   - high-risk mutations and real page operations should be verified as real flows where possible
   - purely presentational controls do not always need expensive E2E tests
6. Engineering tests do not prove production readiness.
   - If a change depends on production-sensitive conditions such as external providers, email, OAuth, webhooks, env vars, CORS, database schema, or deployment platform, local or engineering-mode success is not enough.

## 12. Working Rhythm After Entry

1. Do not stop frequently for user confirmation.
   - Unless there is a real blocker, spec conflict, or irreversible decision, proceed with organization, implementation, or audit.

2. Ask first when a change would:
   - conflict with product truth
   - change a capability stage
   - introduce paid external services or sensitive providers
   - delete or heavily refactor existing logic
   - affect data ownership, identity, permissions, security, payments, or launch risk

3. Every batch report must say:
   - why the change was made
   - which source truth it maps to
   - which files changed
   - how it was verified
   - what was not verified
   - whether mock / engineering mode / local-only behavior was used
   - whether production-like or post-deploy checks are still needed

4. When a high-value blocker is resolved, reassess whether that line should remain active.
   - If the remainder is mostly copy, low-risk polish, or non-critical tests, say that clearly.
   - Do not lower the completion standard just because remaining work is lower value.

## 13. Continuous Spec Writeback

Update docs when:

1. The designer adds or corrects product judgment.
2. Implementation reveals that a rule is not precise enough.
3. A flow has an undefined state, failure path, or exception.
4. Architecture choices, data sources, external services, or environment conditions change.
5. Mock, engineering mode, or local verification hides a product gap.
6. A new security, abuse, permission, or data exposure risk appears.
7. Acceptance criteria are insufficient or tests accept half-built behavior.
8. A capability changes stage: current mainline, disabled, future work, or historical reference.

Writeback targets:

- Product judgment: `docs/en/02_PRODUCT_TRUTH.md`
- Terms: `docs/en/03_GLOSSARY.md`
- Hard rules: `docs/en/04_RULES.md`
- Open questions: `docs/en/05_PM_QUESTIONS.md`
- Flows and states: `docs/en/06_FLOWS_AND_STATES.md`
- Capability loops: `docs/en/07_CAPABILITY_MAP.md`
- Architecture decisions: `docs/en/08_ARCHITECTURE_DECISIONS.md`
- Data source of truth: `docs/en/09_DATA_SOURCE_OF_TRUTH.md`
- Environment differences: `docs/en/10_ENVIRONMENT_MODEL.md`
- Defense risks: `docs/en/11_RISK_AND_DEFENSE.md`
- Acceptance and verification: `docs/en/12_ACCEPTANCE_AND_VERIFICATION.md`
- Build audit: `docs/en/13_BUILD_AUDIT.md`
- Document layering and archive rules: `docs/en/14_DOCS_MAINTENANCE.md`
