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

## 驗收表

| 能力 | 驗收條件 | 驗證方式 | 狀態 | 未驗證 |
|---|---|---|---|---|
| 待填 | 待填 | 待填 | 待填 | 待填 |

