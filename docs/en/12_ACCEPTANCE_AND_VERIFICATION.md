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

## L0-L5 Verification Levels For Reports

Every completion report must state the highest verification level reached, so local tests, engineering mode, and production smoke are not mistaken for full product verification.

| Level | Meaning | What You Can Claim | What You Cannot Claim |
|---|---|---|---|
| L0 unverified | code reading, inference, or no operation yet | not verified | cannot claim completion |
| L1 local static check | typecheck / lint / build / diff check | local static checks passed | does not prove flow usability |
| L2 local API / integration | local route / unit / integration / script | local logic or API passed | does not prove real page usability |
| L3 local real-page flow | real page operation on a local server | local real flow works | does not prove online readiness |
| L4 production smoke | basic page, API, env, schema, provider checks on staging / preview / production-like domain | online smoke passed | does not prove full product loop |
| L5 production product flow | full required product loop in production-like or production environment | this capability's production product flow is verified | does not guarantee no residual risk |

`production-like` must be a non-local deployment target or an explicitly named staging / preview / production-like domain using real env, schema, and provider conditions. A local server, mock provider, or local test with production env vars does not count as L4 / L5.

Reports must list:

- verified level
- unverified level
- remaining production / provider / deploy gates
- whether completion can be claimed, or only local completion

## Acceptance Table

| Capability | Acceptance Criteria | Verification Method | Status | Unverified |
|---|---|---|---|---|
| To be filled | To be filled | To be filled | To be filled | To be filled |
