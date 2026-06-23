# 20 OPERATIONAL ATTENTION

這份文件定義長流程、背景工作、外部 callback 或人工處理流程裡，哪些狀態需要被標成「需要注意」。

目標不是讓 agent 製造更多錯誤訊息，而是讓它知道：有些狀態不是完成，也不是立即失敗，而是需要追蹤、重試、降級或人工判斷。

## 何時需要 attention state

以下流程應該明確設計 attention state：

- 需要背景工作或排程完成
- 需要外部服務 callback
- 需要人工審核、人工確認或人工修正
- 一次操作會影響多個資料或多個使用者
- 失敗後可以重試，但不能假裝成功
- public read 可以降級，但 mutation 不能默默成功
- agent 需要在下次接手時知道還有未完成事項

## 建議狀態

不要只用 `success` / `failed`。長流程至少要能區分：

| 狀態 | 意義 | Agent 應該怎麼處理 |
|---|---|---|
| `queued` | 已接受，尚未開始 | 回報排隊中，記錄 enqueue 時間 |
| `running` | 正在處理 | 避免重複啟動同一件事 |
| `retryable_failed` | 可重試失敗 | 記錄原因、retry 次數與下次重試條件 |
| `manual_review_required` | 需要人工判斷 | 停止自動宣告完成，列出人工要看什麼 |
| `completed` | 已完成 | 記錄完成證據 |

專案可以換成自己的狀態名稱，但必須保留同等語意。

## Attention 不等於錯誤

請把 attention 分成兩類：

| 類型 | 例子 | 回報方式 |
|---|---|---|
| 非錯誤 attention | 等待外部 callback、等待人工審核、排程尚未跑完 | 說明等待條件與下一步 |
| 錯誤 attention | 外部服務失敗、資料不一致、重試耗盡 | 說明影響、封鎖範圍與修復路徑 |

不要把「等待」寫成失敗，也不要把「需要人工處理」包裝成完成。

## Trace 欄位

需要 attention 的流程，至少留下這些資訊：

| 欄位 | 用途 |
|---|---|
| `trace_id` | 串起 request、job、callback、audit |
| `actor_id` | 誰觸發了這件事 |
| `subject_id` | 被處理的主要資料或資源 |
| `step` | 卡在哪個流程步驟 |
| `status` | 目前狀態 |
| `attention_reason` | 為什麼需要注意 |
| `first_seen_at` | 第一次進入此狀態的時間 |
| `last_attempt_at` | 最近一次處理時間 |
| `retry_count` | 重試次數 |
| `next_action` | 下一步是自動重試、人工處理或放棄 |

若資料量很大，摘要只列前幾筆 id，並記錄被省略數量。不要在 log 或回報中傾倒大量敏感資料。

## Agent 回報格式

遇到 operational attention 時，回報至少包含：

- 發生了什麼
- 這是等待、可重試失敗、還是人工處理
- 影響哪些能力或使用者路徑
- 已留下哪些 trace / audit
- 下一步由系統自動做，還是需要人做
- 目前不能宣告完成的部分

## 文件回寫

如果某個流程新增 attention state，請同步檢查：

- `06_FLOWS_AND_STATES.md`
- `07_CAPABILITY_MAP.md`
- `11_RISK_AND_DEFENSE.md`
- `12_ACCEPTANCE_AND_VERIFICATION.md`
- `13_BUILD_AUDIT.md`
- `19_CUTOVER_AND_INCIDENT_LESSONS.md`

