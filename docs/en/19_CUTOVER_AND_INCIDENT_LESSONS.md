# 19 CUTOVER AND INCIDENT LESSONS

This document turns production cutover, external-service switching, and incident review into reusable specs. The goal is not blame; it is to turn preventable future failures into preflight checks, runbooks, and acceptance gates.

## Core Lessons

### 1. Repo migration does not equal a complete production environment

The code repo usually manages only part of the system state. These often live in external dashboards or providers and are not completed by migrations:

- storage buckets / file permissions
- auth provider enabled state
- OAuth client id / secret / redirect allowlist
- email sender domain / DNS / template
- project API keys / JWT secret
- deploy platform env vars
- provider webhook / callback URL
- dashboard-only toggles or quota limits

### 2. Schema drift needs runtime preflight

A table existing does not prove columns, indexes, RLS, storage policy, or schema cache match runtime expectations. Before cutover, check:

- required tables are readable
- runtime-required columns exist
- write-path-required columns exist
- RLS / permissions do not create fake-success public reads or protected mutations
- storage buckets exist with correct public/private behavior
- schema cache has reloaded or will not read old columns

### 3. Public reads may degrade under control, high-risk mutations must fail closed

When production is unhealthy, public reads may use short TTL cache, local snapshots, explicit empty states, or controlled errors to protect availability. But creation, permission, delete, admin operations, or other high-risk mutations must not fake success.

### 4. Production is not an agent load-test target

Production smoke must be low-frequency, non-destructive, and rollback-safe. Full L5 rehearsal should run on staging / preview first. If a provider or database is unhealthy, stop automated retries and investigate in staging / local.

### 5. Incident lessons must be written back into specs

Every incident review should add at least:

- what happened
- root cause category
- automation added
- external gates that remain manual
- the fixed process going forward
- verification boundaries that must not be confused in reports

## Cutover Preflight Template

| Gate | Check | Owner | Automated | Status | Notes |
|---|---|---|---|---|---|
| backend env | private env points to target project | engineering | yes / no | pending | |
| frontend env | public env points to target project | engineering | yes / no | pending | |
| auth | provider enabled and redirect allowlist correct | operator | no | pending | |
| storage | required buckets exist with expected visibility | engineering | yes / no | pending | |
| schema | runtime tables and columns readable | engineering | yes | pending | |
| email | sender/domain/mailbox smoke works | operator | partial | pending | |
| provider | callbacks/webhooks point to target deploy | operator | no | pending | |
| owner/admin | emergency account can log in | operator | yes / no | pending | |
| rollback | old env and redeploy path documented | engineering | no | pending | |

## Incident Lesson Template

```md
# Incident Lesson: YYYY-MM-DD Title

## What Happened

- 

## Impact

- affected users:
- affected capabilities:
- affected environments:

## Root Cause Category

- schema drift
- missing external dashboard setting
- env mismatch
- provider outage
- rate / quota / pressure issue
- data migration issue
- unclear verification report

## What Was Automated

- 

## Manual Gates That Remain

- 

## New Rules To Write Back

- PRODUCT_TRUTH:
- ENVIRONMENT_MODEL:
- RISK_AND_DEFENSE:
- ACCEPTANCE_AND_VERIFICATION:
- DECISION_LOG:

## Reporting Boundary

What can be claimed now, and what remains unverified?
```
