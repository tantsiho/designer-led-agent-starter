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

## Production / Staging 壓力邊界

Production 驗證必須保守限流。任何會大量查 schema、反覆登入、刷新 dashboard、建立批量測試資料、跨角色重跑完整流程、或對外部 provider 造成壓力的檢查，預設先跑 staging / preview。

Production 只適合：

- `/health` 或基本 API 存活
- 首頁 / 高流量 public page 少量讀取
- 少量真人登入 / callback / mailbox smoke
- 非破壞性、低頻、可回滾的 provider 檢查

Production unhealthy 或 provider timeout 時：

1. 停止 L5、自動化重試、schema reload、Table Editor 反覆刷新。
2. 只保留低頻 health / homepage / public read。
3. 改在 staging / local 查 schema、migration、程式與資料問題。
4. Production 恢復後只做最小 smoke。

## Env 成對切換

若 frontend、API、auth provider、database 或 storage 指向不同 project / environment，會出現「註冊寫到 A、登入讀 B」這類難查問題。切環境時必須同批確認：

- backend private env
- frontend public env
- auth callback / redirect allowlist
- storage bucket / file URL 行為
- email sender / domain / template
- external provider dashboard setting

Repo migration 完成不等於外部 dashboard 已完成；SQL schema 完成也不等於 Auth / Storage / OAuth / Email / Env 完整切換。
