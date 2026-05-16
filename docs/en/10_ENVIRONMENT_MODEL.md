# 10 ENVIRONMENT MODEL

This document separates local, test, and launch environments. The agent must not present local success as production verification.

## Environment Table

| Environment | Purpose | Data | Mock Allowed | Forbidden | Verification Meaning |
|---|---|---|---|---|---|
| local | local development | seed / local | yes | must not claim launch readiness | checks basic flow |
| engineering mode | engineering checks | seed / debug | yes | must not be a formal user entry | fast scenario switching |
| staging / submission-like | pre-launch checks | close to production | limited | should not depend on debug entries | checks capability boundaries |
| production | live use | real data | no | no engineering entry points | real usage |

## Env Vars

| Variable | Required Environment | Purpose | Behavior When Missing |
|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled |

## Pre-Launch Check

- What ran locally?
- Is engineering mode disabled?
- Are real providers used?
- Did staging / production-like smoke run?
- Which features still need post-deploy checks?
- If an external service fails, does the system fail closed or degrade clearly?
