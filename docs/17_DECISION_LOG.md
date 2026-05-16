# 17 DECISION LOG

這份文件記錄「為什麼這樣決定」。它不是單純列出最後答案，而是保存當時排除的替代方案、取捨與重估條件。

長期使用 AI agent 時，agent 可能會回頭推翻舊決策，或把曾經排除的方案重新包裝成新建議。Decision log 的用途是讓後續 agent 先理解「為什麼當時不那樣做」。

## 使用原則

- 用產品語言寫，不需要寫成正式 ADR。
- 每個重要決策都要連到產品真相、規則、能力或風險。
- 如果替代方案被排除，要寫清楚原因。
- 如果決策未來可能改，要寫重估條件。
- 若新決策覆蓋舊決策，不刪舊文；新增 supersedes / superseded by。

## Decision Index

| ID | 決策 | 狀態 | 影響範圍 | 日期 | 文件 |
|---|---|---|---|---|---|
| D-0001 | 待填 | proposed / accepted / superseded | 待填 | YYYY-MM-DD | `DECISIONS/0001-template.md` |

## Decision Template

```md
# D-0001: Decision Title

## Status

proposed / accepted / superseded

## Context

當時遇到什麼產品、流程、風險或工程問題？

## Decision

最後決定是什麼？用產品語言寫。

## Alternatives Considered

| Alternative | Why Not |
|---|---|
| 待填 | 待填 |

## Tradeoffs

- Gain:
- Cost:
- Risk:

## Non-Goals

這個決策明確不處理什麼？

- 待填

## Reassessment Trigger

什麼情況發生時需要重估？

- 待填

## Links

- Product truth:
- Rules:
- Capability:
- Risk:
```
