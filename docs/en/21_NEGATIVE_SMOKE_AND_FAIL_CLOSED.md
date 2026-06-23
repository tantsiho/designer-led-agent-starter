# 21 NEGATIVE SMOKE AND FAIL-CLOSED

This document requires agents to verify not only "the happy path succeeds" but also "the blocked path is actually blocked."

Many unstable products fail because forbidden paths are quietly allowed through UI gaps, APIs, direct routes, mocks, or fallback behavior.

## What Negative Smoke Means

Negative smoke is a small, low-cost check that forbidden paths remain forbidden.

For every high-risk capability, consider:

| Type | What To Confirm |
|---|---|
| anonymous access | unauthenticated users are rejected |
| wrong role | users without permission are rejected |
| direct route | typing the URL cannot bypass UI gates |
| direct API | direct API calls cannot bypass frontend gates |
| capability off | disabled capabilities are disabled everywhere |
| missing env / provider | missing required external conditions fail closed |
| duplicate / replay | duplicate submissions or replays do not create a second effect |
| production read-only smoke | online smoke checks avoid destructive writes |

## Fail-Closed Principle

High-risk mutations must fail closed:

- do not report fake success
- do not create partial records
- do not use local fallback as formal completion
- do not write audit, notification, or report entries that claim completion
- do not skip required checks because a provider is unavailable
- do not present engineering-mode results as production completion

Public reads may degrade under clear labeling, such as cache, empty state, or traceable error. High-risk mutations must not degrade into fake success.

## Checklist

| Check | Success Should Show | Failure Should Show |
|---|---|---|
| permission gate | authorized user can enter | unauthorized user is rejected with no side effect |
| capability gate | enabled path works | disabled path rejects consistently across UI, API, and direct route |
| env / provider gate | required conditions exist before execution | missing conditions block execution clearly |
| duplicate guard | first request is effective | second request is rejected or returns the same result |
| replay guard | valid event can be handled | replay does not create a new side effect |
| error policy | error is traceable | internal details are not leaked and success is not faked |

## Report Requirements

Each report should state:

- whether the check was positive path or negative path
- which gate blocked the request
- status code or error type
- whether a side effect occurred
- whether mock, seed, engineering mode, or local-only conditions were used
- the highest L0-L5 verification level reached

If only the positive path was checked, say that negative smoke is still incomplete.

## Common Agent Mistakes

- checking only that the UI button disappeared without trying direct route or API access
- treating a 500 as a valid block when it is really an unhandled error
- treating engineering-mode success as formal flow success
- treating local env var setup as provider dashboard completion
- changing tests to accept incomplete behavior just to make them pass

