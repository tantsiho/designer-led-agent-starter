# 19 CUTOVER AND INCIDENT LESSONS

這份文件把 production cutover、外部服務切換、incident 復盤變成可重用規範。它的目標不是追責，而是把下一次可預防的問題變成 preflight、runbook 和驗收 gate。

## 核心教訓

### 1. Repo migration 不等於完整 production environment

Code repo 通常只能管理一部分狀態。以下項目常在外部 dashboard 或 provider 裡，不會因 migration 完成而自動完成：

- storage buckets / file permissions
- auth provider enabled 狀態
- OAuth client id / secret / redirect allowlist
- email sender domain / DNS / template
- project API keys / JWT secret
- deploy platform env vars
- provider webhook / callback URL
- dashboard-only toggles or quota limits

### 2. Schema drift 要用 runtime preflight 查

Table 存在不代表欄位、index、RLS、storage policy、schema cache 都符合 runtime 期待。Cutover 前應檢查：

- 必要 tables 可讀
- runtime 必要欄位存在
- write path 所需欄位存在
- RLS / permissions 不會讓 public read 或 protected mutation 假成功
- storage bucket 存在、public/private 行為正確
- schema cache 已 reload 或不會讀到舊欄位

### 3. Public read 可以受控降級，高風險 mutation 必須 fail closed

Production 不健康時，公開讀取可以短 TTL cache、local snapshot、明確空狀態或受控錯誤保護 availability。但建立、權限、刪除、admin 操作或其他高風險 mutation 不得假成功。

### 4. Production 不是代理壓測場

Production smoke 必須低頻、非破壞、可回滾。完整 L5 rehearsal 應先在 staging / preview 跑完。若 provider / database unhealthy，停止自動化重試，改回 staging / local 排查。

### 5. Incident lesson 要寫回規範

每次 incident 復盤至少補：

- 發生了什麼
- 根因分類
- 已補自動化
- 仍需人工的外部 gate
- 之後固定流程
- 回報時不得混淆的驗證邊界

## Cutover Preflight Template

| Gate | Check | Owner | Automated | Status | Notes |
|---|---|---|---|---|---|
| backend env | private env points to target project | engineering | yes / no | pending | |
| frontend env | public env points to target project | engineering | yes / no | pending | |
| auth | provider enabled and redirect allowlist correct | operator | no | pending | |
| storage | required buckets exist with expected visibility | engineering | yes / no | pending | |
| schema | runtime tables and columns readable | engineering | yes | pending | |
| email | sender/domain/mailbox smoke works | operator | partial | pending | |
| provider | callbacks/webhooks point to target deploy | operator | no | pending | |
| owner/admin | emergency account can log in | operator | yes / no | pending | |
| rollback | old env and redeploy path documented | engineering | no | pending | |

## Incident Lesson Template

```md
# Incident Lesson: YYYY-MM-DD Title

## What Happened

- 

## Impact

- affected users:
- affected capabilities:
- affected environments:

## Root Cause Category

- schema drift
- missing external dashboard setting
- env mismatch
- provider outage
- rate / quota / pressure issue
- data migration issue
- unclear verification report

## What Was Automated

- 

## Manual Gates That Remain

- 

## New Rules To Write Back

- PRODUCT_TRUTH:
- ENVIRONMENT_MODEL:
- RISK_AND_DEFENSE:
- ACCEPTANCE_AND_VERIFICATION:
- DECISION_LOG:

## Reporting Boundary

What can be claimed now, and what remains unverified?
```
