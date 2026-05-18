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

## Production / Staging Pressure Boundary

Production verification must be conservative and rate-limited. Any check that repeatedly queries schema, logs in, refreshes dashboards, creates batches of test data, reruns full cross-role flows, or pressures external providers should default to staging / preview first.

Production is suitable only for:

- `/health` or basic API liveness
- small-volume homepage / high-traffic public-page reads
- small-volume human login / callback / mailbox smoke
- non-destructive, low-frequency, rollback-safe provider checks

When production is unhealthy or a provider times out:

1. Stop L5, automated retries, schema reloads, and repeated dashboard refreshes.
2. Keep only low-frequency health / homepage / public read checks.
3. Use staging / local to investigate schema, migration, code, and data issues.
4. After production recovers, run only minimal smoke.

## Paired Env Switching

If frontend, API, auth provider, database, or storage point to different projects / environments, failures such as "registration writes to A, login reads from B" become hard to diagnose. During environment switches, confirm these as one batch:

- backend private env
- frontend public env
- auth callback / redirect allowlist
- storage bucket / file URL behavior
- email sender / domain / template
- external provider dashboard setting

Repo migration completion does not mean external dashboards are configured; SQL schema completion does not mean Auth / Storage / OAuth / Email / Env are fully switched.
