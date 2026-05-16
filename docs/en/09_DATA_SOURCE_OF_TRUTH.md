# 09 DATA SOURCE OF TRUTH

This document defines data sources of truth. Large MVPs often break because data appears to exist but is only frontend state or test data.

## Data Source Table

| Data | Source of Truth | Read Sources | Write Sources | Untrusted Sources | Notes |
|---|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled | To be filled |

## Persistence Rules

- Data that must go into the database:
- Data that can stay frontend-only:
- Data that can be filled by an external provider:
- Data that must not be placed in URLs:
- Data that must not appear on public pages:

## Data Drift Check

The agent must check:

- Does data survive refresh?
- Does data survive server restart?
- If local and remote data conflict, which wins?
- Can seed/mock data mix into production data?
- Can deleted, canceled, or expired old data revive?
