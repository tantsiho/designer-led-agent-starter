# Designer-Led Agent Starter

A starter template for non-engineer product designers who use AI coding agents to turn messy product ideas or long design drafts into a verifiable MVP.

The goal is not to generate a production-grade system in one shot. The goal is to make the agent slow down, extract product truth, ask PM-style questions, create source-of-truth docs, and only then build one capability at a time.

Core idea:

> The designer owns product truth. The agent owns engineering closure.

This is not a one-time planning step. The source-of-truth docs should keep growing during development. Every implementation pass, audit, environment check, risk review, or designer correction may reveal new rules. The agent must write those discoveries back into the docs instead of leaving them buried in chat history.

You do not need to understand databases, APIs, auth, tests, deployment, or security vocabulary before you start. You do need to describe the product as completely as you can, and answer product judgment questions when the agent asks.

## What This Helps With

- Turn long, messy design drafts into product truth, rules, roles, flows, and acceptance criteria
- Stop AI agents from coding before they understand the product
- Make the agent ask PM-style clarification questions
- Split features into UI / API / data / permission / error / test capability loops
- Distinguish current MVP scope, disabled capabilities, future work, and historical references
- Force architecture, environment, deployment, data source, and risk checks before implementation
- Avoid "it has a screen, so it must be done" false completion
- Preserve reusable source-of-truth docs so future agents do not depend on chat memory

## What This Does Not Guarantee

- It does not make a complete product in one prompt
- It does not decide your product truth for you
- It does not replace senior engineering review, security review, legal review, payment compliance, or production SRE
- It does not guarantee external providers, payments, email, deployment, or production smoke tests will work immediately
- It does not turn a weak product idea into a strong one automatically

Use it as a disciplined MVP workflow, not as a production guarantee.

## Quick Start

1. Copy this template into a new project.
2. Copy `AGENTS.template.md` to the project root as `AGENTS.md`.
3. Put your rough design notes into `docs/01_RAW_DESIGN.md`.
4. Ask your AI agent, in natural language:

```text
This is my product design draft. Do not implement yet. First read AGENTS.md and docs/00_START_HERE.md, then extract product truth, roles, rules, flows, contradictions, and PM questions.
```

5. Answer the PM questions.
6. Ask the agent to update the source-of-truth docs.
7. Only after the source docs are stable enough, ask the agent to build the first core capability.
8. After each build pass, ask the agent to write new rules, risks, environment differences, and acceptance gaps back into the docs.

## No Slash Commands Required

This template assumes a natural-language workflow. You can say things like:

- "Here is my design document."
- "I need to clarify this rule."
- "Find contradictions before building."
- "Build this flow first."
- "Is this just a half-finished UI?"
- "Turn this into development rules."

The agent should infer whether the current task is design intake, rule extraction, clarification, implementation, audit, readiness review, or documentation backfill.

## Repository Map

- `AGENTS.template.md` - hard operating rules for the AI agent. Copy it to `AGENTS.md` in a new project.
- `docs/00_START_HERE.md` - agent entry point.
- `docs/01_RAW_DESIGN.md` - raw product notes. They can be messy and long.
- `docs/02_PRODUCT_TRUTH.md` - what the product is, is not, and who it is for.
- `docs/03_GLOSSARY.md` - terms and definitions.
- `docs/04_RULES.md` - hard rules, forbidden behavior, exceptions, stage classification.
- `docs/05_PM_QUESTIONS.md` - PM questions and designer answers.
- `docs/06_FLOWS_AND_STATES.md` - flows, state machines, failure paths.
- `docs/07_CAPABILITY_MAP.md` - capability closure map.
- `docs/08_ARCHITECTURE_DECISIONS.md` - architecture choices and tradeoffs.
- `docs/09_DATA_SOURCE_OF_TRUTH.md` - persistence and data ownership.
- `docs/10_ENVIRONMENT_MODEL.md` - local, test, staging, production differences.
- `docs/11_RISK_AND_DEFENSE.md` - abuse cases, security boundaries, audit needs.
- `docs/12_ACCEPTANCE_AND_VERIFICATION.md` - acceptance criteria and verification tiers.
- `docs/13_BUILD_AUDIT.md` - post-build audit log.
- `docs/14_DOCS_MAINTENANCE.md` - source-of-truth maintenance and archive rules.
- `docs/15_NATURAL_LANGUAGE_EXAMPLES.md` - phrases you can use with an agent.
- `docs/16_WORKFLOW_MODULES.md` - full checklist of workflow modules.

## When Is It Okay To Start Coding?

Only start implementation when:

- Product truth has been extracted
- Core roles and rules are defined
- The first capability appears in the capability map
- Important PM questions are answered, or clearly marked as not blocking the current pass
- Architecture, data source, environment, and defense risks have at least a minimum decision
- The acceptance criteria are clear enough to verify

If these are missing, do not rush into code. Stable source docs make the build phase more stable.

## Keep Writing Specs During Development

Do not treat documentation as a one-time setup task. Development will reveal things the raw draft missed:

- Missing exceptions
- Undefined states
- Environment differences between local and production
- Mock behavior hiding product gaps
- Misleading copy or public positioning
- Admin / ops / audit needs
- Abuse cases and defense requirements
- Acceptance criteria the first tests did not cover

When this happens, do not only patch the code. Update the matching source-of-truth doc so the next agent does not repeat the same mistake.

## 中文簡介

這是一套給「有產品想法或長篇設計文件，但不是工程師」的人使用的 AI 代理開工模板。

它不是一鍵產生 production 系統的工具，而是要求代理先把混亂設計稿整理成產品真相、規則、流程、PM 問題與能力地圖，再逐條實作與稽核 MVP。

核心原則：

> 設計者負責產品真相。代理負責工程閉環。

最重要的規則是：不要一開始就叫 AI 寫 app。先叫它抽規則、問問題、建立真源文件。真源穩了，後面才會穩。

## Status

Early template / beta. This was extracted from a long-running AI-assisted MVP build process by a non-engineer designer. It is intended as a practical starter kit, not a complete software engineering methodology.
