# 11 RISK AND DEFENSE

This document records defensive thinking. MVPs still need basic risk judgment, especially around accounts, data, payments, content, permissions, admin, or external callbacks.

## Abuse Cases

| Risk | Attack / Abuse Method | Impact | Defense | Unhandled |
|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled |

## Required Checklist

- unauthorized read
- unauthorized write
- duplicate submission
- callback / webhook replay
- data leak
- sensitive data leak in URLs
- error messages leaking internal logic
- direct route bypassing UI
- direct API calls bypassing frontend
- refund / payment / order abuse
- fake account / spam / rate limit
- admin action without audit
- destructive action without confirmation

## Defense Design

| Feature | Permission Check | Idempotency | Audit | Rate Limit | Error Policy |
|---|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled | To be filled |
