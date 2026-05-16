# 10 ENVIRONMENT MODEL

這份文件區分本地、測試、上線。代理不得把本地成功包裝成 production 已驗證。

## 環境表

| 環境 | 用途 | 資料 | 可用 mock | 禁止事項 | 驗證意義 |
|---|---|---|---|---|---|
| local | 本地開發 | seed / local | 可 | 不可宣稱上線可用 | 檢查基本流程 |
| engineering mode | 工程檢測 | seed / debug | 可 | 不可作正式入口 | 快速切情境 |
| staging / submission-like | 上線前檢查 | 接近正式 | 少量 | 不應依賴 debug 入口 | 檢查能力邊界 |
| production | 正式 | 真資料 | 不可 | 不可開工程入口 | 真實使用 |

## Env Vars

| 變數 | 必填環境 | 用途 | 缺失時行為 |
|---|---|---|---|
| 待填 | 待填 | 待填 | 待填 |

## 上線前檢查

- 本地跑過什麼？
- 是否關閉 engineering mode？
- 是否用真 provider？
- 是否跑 staging / production-like smoke？
- 哪些功能仍需 post-deploy 檢查？
- 若外部服務失敗，是否 fail closed 或有清楚降級？

