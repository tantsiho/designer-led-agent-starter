# 11 RISK AND DEFENSE

這份文件記錄防禦思維。MVP 也需要基本風險判斷，尤其涉及帳號、資料、付款、內容、權限、admin 或外部 callback。

## Abuse Cases

| 風險 | 攻擊 / 濫用方式 | 影響 | 防線 | 尚未處理 |
|---|---|---|---|---|
| 待填 | 待填 | 待填 | 待填 | 待填 |

## 必查清單

- 越權讀取
- 越權寫入
- 重複提交
- callback / webhook replay
- 資料外洩
- URL 洩漏敏感資料
- 錯誤訊息洩漏內部邏輯
- direct route 繞過 UI
- API 直接呼叫繞過前端
- refund / payment / order abuse
- fake account / spam / rate limit
- admin 操作缺 audit
- destructive action 缺確認

## 防禦設計

| 功能 | 權限檢查 | Idempotency | Audit | Rate limit | Error policy |
|---|---|---|---|---|---|
| 待填 | 待填 | 待填 | 待填 | 待填 | 待填 |

