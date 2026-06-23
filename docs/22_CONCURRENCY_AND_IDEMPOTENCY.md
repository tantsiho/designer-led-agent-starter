# 22 CONCURRENCY AND IDEMPOTENCY

這份文件定義 agent 在處理重複提交、重試、外部 callback、背景工作、多分頁與併發操作時，必須檢查的規則。

前端 disable button 不是併發保護。只要同一個操作可以被 API、重試、callback、script 或多個 tab 觸發，就需要更深的防線。

## 什麼時候要檢查

以下情境必須檢查 concurrency / idempotency：

- 使用者可能連點或重新送出表單
- 瀏覽器、網路或 SDK 可能自動重試
- 外部 callback 可能重送
- 背景 job 可能重跑
- 多個操作者可能同時改同一份資料
- 一次操作會寫入多個表或觸發副作用
- 成功後會送通知、更新 audit 或啟動下一個流程

## 防線層級

| 防線 | 適合用途 | 不足之處 |
|---|---|---|
| 前端 disable / loading | 改善使用者體驗 | 擋不住 direct API、重試、多分頁 |
| API duplicate guard | 擋同一使用者短時間重送 | 需要穩定 key 與資料庫支援 |
| idempotency key | 重送同一操作回同一結果 | key scope 與 request fingerprint 要清楚 |
| unique constraint | 保證資料不重複 | 需要搭配清楚錯誤與回傳策略 |
| transaction / row lock | 多資料寫入一致 | 要避免鎖順序混亂與長交易 |
| durable queue | 背景工作可重試 | 仍需去重、狀態與 attention policy |

## Idempotency key 規則

Idempotency key 應該包含或綁定：

- actor scope
- operation type
- subject/resource id
- request fingerprint
- created time 或有效期限
- 最終結果或可重放的 response

同一個 key 重送時，應該回同一結果或明確拒絕，不應再產生第二次副作用。

## Transaction 與副作用

多步驟操作要先定義 transaction boundary：

- 哪些資料必須同時成功或同時失敗
- 哪些副作用只能在 durable write 成功後發生
- audit 是記錄 attempt、success，還是 failure
- 通知、外部呼叫、排程是否可能重送
- rollback 後是否會留下誤導性的成功訊號

一般原則：外部副作用不要在核心資料成功 commit 前宣告完成。

## 併發回報格式

當實作或稽核高風險操作時，回報：

- 可能重複觸發的入口
- 使用哪一層防線
- idempotency key 或 unique constraint 的 scope
- transaction boundary
- 重試 / replay 會得到什麼結果
- 哪些副作用在 commit 後才發生
- 哪些情境尚未驗證

## Rehearsal

最小 rehearsal 應該包含：

| 情境 | 預期 |
|---|---|
| 連續提交兩次 | 只有一次有效，或第二次回同一結果 |
| 同一 request 重試 | 不產生第二份資料 |
| callback replay | 不再觸發新副作用 |
| 背景 job 重跑 | 已完成項目不重做 |
| 兩個操作者同時修改 | 結果符合鎖定、版本或衝突規則 |

