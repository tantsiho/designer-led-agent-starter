# 範例：簡單預約 App

這是一個小範例，用來示範這套模板應該如何使用。它不是完整 app。

## 原始設計輸入

一間本地工作室想做簡單的預約 MVP。

顧客應該可以選擇服務、選擇時段、輸入聯絡資料，然後送出預約請求。工作室老闆應該可以查看請求，並標記接受或拒絕。

MVP 先不要收線上付款。不要公開顧客私人電話。顧客送出請求後要得到清楚回饋。老闆需要看到足夠資訊，以便人工後續聯絡。

## 抽出的產品真相

- 這是預約請求工具，不是即時付費訂位系統。
- MVP 要證明請求收件與老闆審核。
- 付款、自動日曆同步、SMS 提醒是未來工程。

## 核心規則

- 預約請求在老闆接受前不算確認。
- 顧客聯絡資訊是私密資料。
- 關閉中的未來功能不得以可用 UI 出現。
- 本地 demo 資料不得被當成 production 資料。

## PM 問題

1. 顧客在 MVP 能取消請求嗎？
2. 老闆審核前，兩位顧客可以請求同一個時段嗎？
3. 老闆在 MVP 需要 email 通知，還是 dashboard 查看就夠？
4. 必填資訊有哪些：姓名、電話、email、備註？

## 能力閉環範例

| 能力 | UI | API | Data | Permission | Error | Verification |
|---|---|---|---|---|---|---|
| 送出預約請求 | 服務 / 時段 / 聯絡表單 | create request | booking_requests | public create only | invalid slot/contact | local smoke + integration |
| 老闆審核 | dashboard list/actions | accept/reject request | status transition | owner only | stale request | integration + protected route smoke |

## 防禦筆記

- public submission 需要 rate limit。
- 不要在 public URL 暴露顧客聯絡資料。
- 老闆操作應該可稽核。
- 重複送出要能優雅處理。
