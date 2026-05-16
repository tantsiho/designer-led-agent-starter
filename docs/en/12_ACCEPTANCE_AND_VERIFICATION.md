# 12 ACCEPTANCE AND VERIFICATION

This document defines what "done" means and how to verify it.

## Definition Of Done

A feature is not done just because the screen exists. Every capability should check at least:

- UI entry exists and does not mislead
- API / action truly supports it
- data can be persisted
- permissions are correct
- error states are handled
- important data survives refresh / restart
- tests or smoke checks verify the real flow
- docs are updated

## Verification Layers

| Layer | Purpose | When Needed | What It Does Not Prove |
|---|---|---|---|
| static / type / lint | basic quality | most code changes | does not prove the flow works |
| unit | single logic unit | rules, transforms, calculations | does not prove the full flow |
| integration | API / DB / service | high-risk mutations | does not prove UI usability |
| local smoke | local flow | core paths | does not prove launch readiness |
| non-engineering smoke | debug entries off | before launch | does not prove external providers work |
| production-like / post-deploy | launch environment | external services, env, webhooks | does not guarantee no risk |

## Acceptance Table

| Capability | Acceptance Criteria | Verification Method | Status | Unverified |
|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled |
