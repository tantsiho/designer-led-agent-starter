# Designer-Led Agent Starter

English | [繁體中文](README.zh.md)

A starter template for non-engineer product designers who use AI coding agents to turn messy product ideas or long design drafts into a verifiable MVP.

The goal is not to generate a production-grade system in one shot. The goal is to make the agent slow down, extract product truth, ask PM-style questions, create source-of-truth docs, and only then build one capability at a time.

Core idea:

> The designer owns product truth. The agent owns engineering closure.

This is not a one-time planning step. The source-of-truth docs should keep growing during development. Every implementation pass, audit, environment check, risk review, or designer correction may reveal new rules. The agent must write those discoveries back into the docs instead of leaving them buried in chat history.

You do not need to understand databases, APIs, auth, tests, deployment, or security vocabulary before you start. You do need to describe the product as completely as you can, and answer product judgment questions when the agent asks.

## Origin

This template was extracted from the development process behind [HAIBUNKA](https://haibunka.com), a real creator-platform product.

It came out of roughly three months of AI-assisted product and engineering work, including:

- an 80,000-word source-of-truth design corpus
- 200+ continuously evolving specification, verification, and audit documents
- 500+ implementation files
- repeated loops of product clarification, capability closure, audit, and launch-readiness checks

This is not a theoretical prompt collection. It is a distilled workflow from a real project where product rules, implementation details, environment gaps, and agent mistakes had to be made explicit over time.

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
2. Choose a language track:
   - English: copy `AGENTS.en.template.md` to the project root as `AGENTS.md`, then use `docs/en/`.
   - Traditional Chinese: copy `AGENTS.template.md` to the project root as `AGENTS.md`, then use `docs/`.
3. Put your rough design notes into `docs/en/01_RAW_DESIGN.md` or `docs/01_RAW_DESIGN.md`.
4. Ask your AI agent, in natural language:

```text
This is my product design draft. Do not implement yet. First read AGENTS.md and docs/en/00_START_HERE.md, then extract product truth, roles, rules, flows, contradictions, and PM questions.
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

- `AGENTS.en.template.md` - English hard operating rules for the AI agent. Copy it to `AGENTS.md` in an English project.
- `AGENTS.template.md` - Traditional Chinese hard operating rules for the AI agent. Copy it to `AGENTS.md` in a Chinese project.
- `docs/en/` - complete English source-of-truth document set.
- `docs/` - complete Traditional Chinese source-of-truth document set.
- `examples/simple-booking-app/README.md` - English example.
- `examples/simple-booking-app/README.zh.md` - Traditional Chinese example.
- `LICENSE` - canonical MIT License in English.
- `LICENSE.zh.md` - unofficial Traditional Chinese reference translation of the MIT License.

Both language tracks contain the same document structure:

- `00_START_HERE.md` - agent entry point.
- `01_RAW_DESIGN.md` - raw product notes. They can be messy and long.
- `02_PRODUCT_TRUTH.md` - what the product is, is not, and who it is for.
- `03_GLOSSARY.md` - terms and definitions.
- `04_RULES.md` - hard rules, forbidden behavior, exceptions, stage classification.
- `05_PM_QUESTIONS.md` - PM questions and designer answers.
- `06_FLOWS_AND_STATES.md` - flows, state machines, failure paths.
- `07_CAPABILITY_MAP.md` - capability closure map.
- `08_ARCHITECTURE_DECISIONS.md` - architecture choices and tradeoffs.
- `09_DATA_SOURCE_OF_TRUTH.md` - persistence and data ownership.
- `10_ENVIRONMENT_MODEL.md` - local, test, staging, production differences.
- `11_RISK_AND_DEFENSE.md` - abuse cases, security boundaries, audit needs.
- `12_ACCEPTANCE_AND_VERIFICATION.md` - acceptance criteria and verification tiers.
- `13_BUILD_AUDIT.md` - post-build audit log.
- `14_DOCS_MAINTENANCE.md` - source-of-truth maintenance and archive rules.
- `15_NATURAL_LANGUAGE_EXAMPLES.md` - phrases you can use with an agent.
- `16_WORKFLOW_MODULES.md` - full checklist of workflow modules.
- `17_DECISION_LOG.md` - product-language decision log with alternatives and tradeoffs.
- `18_CONTRADICTION_AUDIT.md` - active audit for flow conflicts, impossible states, and product contradictions.
- `DECISIONS/0001-template.md` - copyable decision record template.

## When Is It Okay To Start Coding?

Only start implementation when:

- Product truth has been extracted
- Core roles and rules are defined
- The first capability appears in the capability map
- Important PM questions are answered, or clearly marked as not blocking the current pass
- Architecture, data source, environment, and defense risks have at least a minimum decision
- Non-goals and known uncertainties are explicit enough to prevent scope creep
- Product contradictions and impossible states have been checked
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
- Old decisions the agent may try to overturn without context
- Product contradictions, impossible states, and incentive mismatches

When this happens, do not only patch the code. Update the matching source-of-truth doc so the next agent does not repeat the same mistake.

## 中文簡介

這是一套給「有產品想法或長篇設計文件，但不是工程師」的人使用的 AI 代理開工模板。

它不是一鍵產生 production 系統的工具，而是要求代理先把混亂設計稿整理成產品真相、規則、流程、PM 問題與能力地圖，再逐條實作與稽核 MVP。

核心原則：

> 設計者負責產品真相。代理負責工程閉環。

最重要的規則是：不要一開始就叫 AI 寫 app。先叫它抽規則、問問題、建立真源文件。真源穩了，後面才會穩。

## 中文快速開始

1. 把這份模板複製到新專案。
2. 複製 `AGENTS.template.md` 到專案根目錄，命名為 `AGENTS.md`。
3. 把粗糙設計稿放進 `docs/01_RAW_DESIGN.md`。
4. 用自然語言要求代理：

```text
這是我的產品設計稿。先不要實作。請先讀 AGENTS.md 和 docs/00_START_HERE.md，整理產品真相、角色、規則、流程、矛盾和 PM 問題。
```

5. 回答 PM 問題。
6. 要求代理更新真源文件。
7. 真源文件夠穩後，再開始做第一條核心能力。
8. 每次實作後，要求代理把新規則、風險、環境差異和驗收缺口寫回文件。

## Status

Early template / beta. This was extracted from a long-running AI-assisted MVP build process by a non-engineer designer. It is intended as a practical starter kit, not a complete software engineering methodology.
