# 13 BUILD AUDIT

This document records post-implementation review. The agent must update it after finishing work.

## Implementation Batches

| Date | Capability | Source Truth | Changes | Verification | Unverified | Follow-Up |
|---|---|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled | To be filled | To be filled |

## False-Completion Review

After every build, ask:

- Is it only UI?
- Are there fake buttons, fake entries, or fake options?
- Are duplicate entry points causing product confusion?
- Does the API truly support it?
- Are permissions checked against the correct identity?
- Is data persisted?
- Is it consistent after refresh / restart?
- Were tests changed to accept a half-built feature?
- Did it use mock / engineering mode?
- Does it need production-like or post-deploy smoke?
- Did a new risk or rule gap appear that must be written back?

## Blocker Reassessment

After a high-value blocker is resolved, the agent should classify remaining work as:

- still a core blocker
- required completeness gap
- low-risk polish
- docs / copy cleanup
- future work

Do not pretend something is complete because the remaining risk is low. Also do not stay indefinitely on non-blockers.
