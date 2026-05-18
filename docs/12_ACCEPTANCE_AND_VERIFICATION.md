# 12 ACCEPTANCE AND VERIFICATION

這份文件定義什麼叫完成，以及怎麼驗證。

## 完成定義

功能完成不等於畫面存在。每條能力至少檢查：

- UI 入口存在且不誤導
- API / action 真支援
- 資料能保存
- 權限正確
- 錯誤狀態可處理
- 重新整理 / 重啟後不丟失關鍵資料
- 測試或 smoke 驗證真流程
- 文件已更新

## 驗證分層

| 層級 | 用途 | 何時需要 | 不能代表什麼 |
|---|---|---|---|
| static / type / lint | 基本品質 | 大多數 code 改動 | 不代表流程可用 |
| unit | 單一邏輯 | 規則、轉換、計算 | 不代表整條流程 |
| integration | API / DB / service | 高風險 mutation | 不代表 UI 真可用 |
| local smoke | 本地流程 | 核心路徑 | 不代表上線 |
| non-engineering smoke | 關掉工程入口 | 上線前 | 不代表外部 provider 真通 |
| production-like / post-deploy | 上線環境 | 外部服務、env、webhook | 不保證無風險 |

## 回報用 L0-L5 驗證層級

每次完成回報必須標明最高驗證層級，避免把本地測試、工程模式或 production smoke 誤認成完整產品驗證。

| 層級 | 意義 | 可宣告什麼 | 不可宣告什麼 |
|---|---|---|---|
| L0 未驗證 | 只讀碼、推論或尚未操作 | 尚未驗證 | 不可宣告完成 |
| L1 本地靜態檢查 | typecheck / lint / build / diff check | 本地靜態檢查通過 | 不代表流程可用 |
| L2 本地 API / integration | 本地 route / unit / integration / script | 本地邏輯或 API 通過 | 不代表真頁面可用 |
| L3 本地真頁面流程 | 本地 server 上操作真頁面 | 本地真流程可走 | 不代表線上可用 |
| L4 production smoke | staging / preview / production-like 網域基本頁面、API、env、schema、provider 存活 | 線上 smoke 通過 | 不代表完整產品閉環 |
| L5 production product flow | production-like 或正式環境走完產品必要閉環 | 該能力 production product flow 已驗證 | 不保證沒有殘餘風險 |

`production-like` 必須是非本機部署目標，或明確命名的 staging / preview / production-like domain，且使用真實 env、schema、provider 條件。本地 server、mock provider、或只設定 production env var 的本地測試不得算 L4 / L5。

回報時必須列出：

- 已驗證層級
- 未驗證層級
- 剩餘 production / provider / deploy gate
- 是否可宣告完成，或只能宣告本地完成

## 驗收表

| 能力 | 驗收條件 | 驗證方式 | 狀態 | 未驗證 |
|---|---|---|---|---|
| 待填 | 待填 | 待填 | 待填 | 待填 |
