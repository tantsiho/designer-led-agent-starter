# 16 WORKFLOW MODULES

This document lists the non-coding work that appears in a long-running AI-agent development process. Use it to check whether the template is missing important modules.

## 1. Raw Design Organization

- collect long, messy, repeated, amended product design
- do not rush implementation
- separate core rules, examples, future ideas, hard rules, and ambiguous points

## 2. Rule Extraction

- product truth
- roles
- permissions
- states
- flows
- forbidden behavior
- exceptions
- completion criteria

## 3. PM Clarification

- have the agent act as PM and ask follow-up questions
- clarify contradictions, vague terms, and undefined failure states
- write designer answers back into source-of-truth docs

## 4. Flowcharts And State Machines

- user flows
- role swimlanes
- state transitions
- failure paths
- data write points
- permission check points

## 5. Capability Map

- split work by capability line, not by page
- each capability needs UI, API, data, permission, error, test, and verification
- mark current mainline, disabled, future work, and historical reference

## 6. Architecture Choice

- frontend / backend / full-stack judgment
- database and persistence
- identity system
- file and image storage
- external providers
- scheduling, webhooks, notifications
- future replaceability

## 7. Data Source Governance

- which source owns each data type
- conflict priority across local / remote / seed / mock
- consistency after refresh, restart, or re-login
- whether old, deleted, or canceled data can revive

## 8. Local And Launch Differences

- local development
- engineering mode
- seed / rich seed
- staging / submission-like
- production
- post-deploy smoke
- env vars and external service differences

## 9. Defense And Abuse Thinking

- unauthorized access
- duplicate submission
- callback / webhook replay
- abuse / spam / rate limit
- direct routes
- hidden APIs
- sensitive data exposure
- rate limits / idempotency
- audit trail

## 10. Capability Toggles And Disabled Consistency

- capabilities are not just done or not done
- disabled capabilities must be consistent across UI, API, direct route, copy, and tests
- future work must not be packaged as nearly finished
- completed future capabilities can remain, but must not become fake entry points in the current mainline

## 11. Seed / Mock / Test Data Governance

- engineering test data must not mix into production data
- mocks must not hide product gaps
- rich seed helps verification but does not prove the real flow
- production fixtures must be identifiable, isolated, and cleanable

## 12. Functional Completeness Audit

- UI existing does not mean complete
- API existing does not mean complete
- green tests do not always mean complete
- review whether the real flow works, data persists, permissions are correct, and errors are handled

## 13. Launch Readiness

- launch checklist
- deployment checklist
- smoke checklist
- rollback / backup
- production-like verification
- external service and env gates

## 14. Admin / Ops / Traceability

- admin operations
- audit log
- account / user timeline
- reports / moderation
- operation feedback
- emergency controls
- post-incident tracing and manual correction

## 15. Notifications, Deep Links, And Return Paths

- notifications should lead to the right context
- after login, users should return to the original flow
- different roles should not land in the wrong shell
- error, cancel, and done states need reasonable destinations

## 16. Public Narrative And Copy

- what the product is not
- public copy must not mislead about available capabilities
- copy must not imply unfinished or incorrect stage
- positioning must not be pulled into a generic template

## 17. Document Layers And Archive

- current source truth
- working drafts
- historical references
- archive
- runbooks
- old documents must not override new source truth

## 18. Agent Report Format

Every batch report should say:

- why it changed
- which source truth it maps to
- which files changed
- how it was verified
- what was not verified
- whether mock / engineering mode / local-only behavior was used
- whether production-like or post-deploy checks are still needed

## 19. Blocker Reassessment

- after a high-value blocker is resolved, decide whether that line is still worth active focus
- if only low-risk polish remains, say so clearly
- do not lower the completion standard for entered capabilities just because risk is low

## 20. Continuous Spec Writeback

- every pitfall should become a spec
- every designer correction should be written back into source truth
- every environment, risk, test, or launch difference discovered should update docs
- do not make the next agent guess from chat memory again

## 21. Decision Log

- record why decisions were made
- preserve rejected alternatives
- make tradeoffs, risks, and reassessment triggers explicit
- prevent future agents from overturning old decisions without context

## 22. Product Contradiction Audit

- flow conflict
- business contradiction
- impossible state
- incentive mismatch
- data inconsistency
- permission contradiction
- copy contradiction
- make the agent actively find contradictions instead of only organizing input

## 23. Cutover And Incident Lessons

- repo migration does not equal a complete production environment
- external dashboard / provider gates must be listed
- schema drift needs runtime preflight
- production is not an agent load-test target
- public reads may degrade under control, high-risk mutations must fail closed
- incident review should write back into specs, runbooks, and acceptance gates

## 24. Operational Attention

- long-running flows should not use only success / failed
- queued, running, retryable_failed, and manual_review_required should be visible
- waiting for callback or manual handling is not completion
- attention summaries need trace, reason, next step, age, and owner
- large data sets should be summarized, not dumped into logs or reports

## 25. Negative Smoke And Fail-Closed

- test blocked paths, not only success paths
- direct route / direct API must not bypass UI gates
- capability-off behavior must match across UI, API, copy, and tests
- missing env / provider must not fake success for high-risk mutations
- production smoke should default to low-frequency, non-destructive, rollback-safe checks

## 26. Concurrency And Idempotency

- frontend disabled buttons are not concurrency protection
- duplicate, retry, replay, and rerun background jobs need a strategy
- idempotency key scope, unique constraint, and transaction boundary must be explicit
- external side effects should be claimed complete only after durable write commit
- rehearsal should include sequential submit, retry, replay, job rerun, and concurrent edits
