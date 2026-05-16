# Designer-Led Agent Starter

[English](README.md) | 繁體中文

這是一套給非工程師產品設計者使用的 starter template，目標是幫助你用 AI coding agent，把混亂的產品想法或長篇設計稿，整理成可以驗證的 MVP。

它的目標不是一口氣產生 production-grade 系統，而是讓 agent 慢下來，先抽出產品真相、問 PM 式問題、建立真源文件，然後一次只完成一條能力閉環。

核心概念：

> 設計者負責產品真相。代理負責工程閉環。

這不是一次性的前置規劃。真源文件應該在開發過程中持續長出來。每次實作、稽核、環境檢查、風險檢查或設計者修正，都可能發現新規則。Agent 必須把這些發現寫回文件，而不是讓它們埋在聊天紀錄裡。

你不需要在開始前理解資料庫、API、auth、測試、部署或安全術語。你需要做的是盡可能完整描述產品，並在 agent 問你產品判斷問題時回答。

## 來源

這套模板是從正式產品 [HAIBUNKA](https://haibunka.com) 的開發過程中抽取出來的。

它不是理論上的 prompt collection，而是來自約三個月 AI 協作開發的實際撞牆經驗，包括：

- 八萬字級的產品真源文件
- 兩百多份持續生長的規範、驗證與稽核文件
- 五百多個實作檔案
- 多輪產品釐清、能力閉環、稽核與上線 readiness 檢查

這套模板整理的是：當 AI agent 真的參與一個產品從設計、實作到驗證時，哪些東西不能只留在聊天紀錄裡，必須變成可維護的真源文件。

## 這能幫你什麼

- 把長篇、混亂的設計稿整理成產品真相、規則、角色、流程與驗收條件
- 阻止 AI agent 在理解產品前就開始寫 code
- 讓 agent 主動提出 PM 式澄清問題
- 把功能拆成 UI / API / data / permission / error / test 能力閉環
- 區分目前 MVP 範圍、關閉中能力、未來工程與歷史參考
- 在實作前強制檢查架構、環境、部署、資料真源與風險
- 避免「畫面有了，所以功能完成了」這種假完成
- 保存可重用的真源文件，讓未來 agent 不依賴聊天記憶

## 這不能保證什麼

- 它不會用一個 prompt 做出完整產品
- 它不會替你決定產品真相
- 它不能取代資深工程審查、安全審查、法律審查、付款合規或 production SRE
- 它不保證外部 provider、付款、email、部署或 production smoke test 會立刻可用
- 它不會自動把弱產品想法變成強產品

請把它當作一套有紀律的 MVP 工作流，而不是 production 保證。

## 快速開始

1. 把這份模板複製到新專案。
2. 選擇語言軌：
   - 繁體中文：複製 `AGENTS.template.md` 到專案根目錄，命名為 `AGENTS.md`，使用 `docs/`。
   - 英文：複製 `AGENTS.en.template.md` 到專案根目錄，命名為 `AGENTS.md`，使用 `docs/en/`。
3. 把粗糙設計稿放進 `docs/01_RAW_DESIGN.md` 或 `docs/en/01_RAW_DESIGN.md`。
4. 用自然語言要求 AI agent：

```text
這是我的產品設計稿。先不要實作。請先讀 AGENTS.md 和 docs/00_START_HERE.md，整理產品真相、角色、規則、流程、矛盾和 PM 問題。
```

5. 回答 PM 問題。
6. 要求 agent 更新真源文件。
7. 真源文件夠穩後，再開始做第一條核心能力。
8. 每次實作後，要求 agent 把新規則、風險、環境差異和驗收缺口寫回文件。

## 不需要 Slash Commands

這套模板假設你使用自然語言工作流。你可以直接說：

- 「這是我的設計文件。」
- 「我需要釐清這條規則。」
- 「先找矛盾，不要急著做。」
- 「先做這條流程。」
- 「這是不是只有半套 UI？」
- 「把這些整理成開發規則。」

Agent 應該自行判斷目前任務是設計輸入、規則抽取、澄清、實作、稽核、readiness review，還是文件回寫。

## Repository Map

- `AGENTS.template.md` - 繁體中文 AI agent 硬規則。中文專案複製成 `AGENTS.md`。
- `AGENTS.en.template.md` - 英文 AI agent 硬規則。英文專案複製成 `AGENTS.md`。
- `docs/` - 完整繁體中文真源文件組。
- `docs/en/` - 完整英文真源文件組。
- `examples/simple-booking-app/README.zh.md` - 繁體中文範例。
- `examples/simple-booking-app/README.md` - 英文範例。
- `LICENSE` - canonical MIT License 英文版。
- `LICENSE.zh.md` - MIT License 繁體中文非正式參考版。

兩個語言軌都包含同樣的文件結構：

- `00_START_HERE.md` - agent 進場入口。
- `01_RAW_DESIGN.md` - 原始產品筆記，可以很長、很亂。
- `02_PRODUCT_TRUTH.md` - 產品是什麼、不是什麼、給誰用。
- `03_GLOSSARY.md` - 名詞與定義。
- `04_RULES.md` - 硬規則、禁止事項、例外、階段分類。
- `05_PM_QUESTIONS.md` - PM 問題與設計者回答。
- `06_FLOWS_AND_STATES.md` - 流程、狀態機、失敗路徑。
- `07_CAPABILITY_MAP.md` - 能力閉環地圖。
- `08_ARCHITECTURE_DECISIONS.md` - 架構選擇與取捨。
- `09_DATA_SOURCE_OF_TRUTH.md` - 資料持久化與資料歸屬。
- `10_ENVIRONMENT_MODEL.md` - local、test、staging、production 差異。
- `11_RISK_AND_DEFENSE.md` - 濫用情境、安全邊界、稽核需求。
- `12_ACCEPTANCE_AND_VERIFICATION.md` - 驗收條件與驗證分層。
- `13_BUILD_AUDIT.md` - 實作後稽核紀錄。
- `14_DOCS_MAINTENANCE.md` - 真源文件維護與封存規則。
- `15_NATURAL_LANGUAGE_EXAMPLES.md` - 可以直接對 agent 說的自然語言範例。
- `16_WORKFLOW_MODULES.md` - 完整工作流模組 checklist。
- `17_DECISION_LOG.md` - 用產品語言記錄決策、替代方案與取捨。
- `18_CONTRADICTION_AUDIT.md` - 主動檢查流程衝突、impossible state 與產品矛盾。
- `DECISIONS/0001-template.md` - 可複製的決策紀錄模板。

## 什麼時候可以開始寫 Code

只有在以下條件成立時，才開始實作：

- 產品真相已經抽出
- 核心角色與規則已定義
- 第一條能力已出現在能力地圖
- 重要 PM 問題已回答，或明確標成不阻擋本輪
- 架構、資料真源、環境與防禦風險至少有基本決策
- 明確不做事項與已知不確定性已標出，避免 scope creep
- 產品矛盾與 impossible state 已檢查
- 驗收條件清楚到可以驗證

如果這些還缺，不要急著寫 code。真源文件穩，後面的實作才會穩。

## 開發中也要持續寫規格

不要把文件當成一次性 setup。開發會揭露原始設計稿沒寫到的事：

- 缺少例外
- 未定義狀態
- local 和 production 的環境差異
- mock 行為掩蓋產品缺口
- 誤導性的文案或 public positioning
- admin / ops / audit 需求
- 濫用情境與防禦需求
- 第一輪測試沒有涵蓋的驗收條件
- agent 可能在缺少脈絡時推翻的舊決策
- 產品矛盾、impossible state、誘因不一致

發生這些事時，不要只 patch code。請更新對應真源文件，讓下一個 agent 不會重踩同一個坑。

## Status

Early template / beta。這套模板萃取自一個由非工程師設計者長期使用 AI 協作完成 MVP 的過程。它是一個實用 starter kit，不是完整軟體工程方法論。
