# 21 NEGATIVE SMOKE AND FAIL-CLOSED

這份文件要求 agent 不只驗證「可以成功」，也要驗證「應該被擋的事情真的被擋」。

很多不穩定產品不是壞在成功路徑，而是壞在不該通過的路徑被 UI、API、direct route、mock 或 fallback 偷偷放行。

## Negative smoke 是什麼

Negative smoke 是小範圍、低成本地確認禁止路徑仍然禁止。

每條高風險能力至少要考慮：

| 類型 | 要確認什麼 |
|---|---|
| 匿名存取 | 未登入使用者是否被擋 |
| 角色錯誤 | 沒有權限的角色是否被擋 |
| direct route | 直接打 URL 是否不能繞過 UI |
| direct API | 直接呼叫 API 是否不能繞過前端 |
| capability off | 關閉中的能力是否所有入口都關閉 |
| 缺 env / provider | 缺必要外部條件時是否 fail closed |
| duplicate / replay | 重複提交或 replay 是否不會產生第二次效果 |
| production read-only smoke | 上線 smoke 是否避免寫入或破壞資料 |

## Fail closed 原則

高風險 mutation 失敗時，必須 fail closed：

- 不回報假成功
- 不建立半套資料
- 不用 local fallback 偽裝正式完成
- 不在 audit、通知、回報裡寫成完成
- 不因為 provider 不通就跳過必要檢查
- 不把工程模式結果宣告成正式環境完成

public read 可以在明確標示下受控降級，例如快取、空狀態或可追蹤錯誤。高風險 mutation 不可以降級成假成功。

## 檢查表

| 檢查 | 成功時應該看到 | 失敗時應該看到 |
|---|---|---|
| 權限 gate | 有權限者可進入 | 無權限者被拒絕且無副作用 |
| capability gate | 開啟時可用 | 關閉時 UI、API、direct route 都一致拒絕 |
| env / provider gate | 條件齊全才執行 | 缺條件時明確阻擋 |
| duplicate guard | 第一次有效 | 第二次被拒絕或回傳同一結果 |
| replay guard | 合法事件可處理 | 重播事件不再產生新副作用 |
| error policy | 可追蹤錯誤 | 不洩漏內部資訊，不假裝成功 |

## 回報要求

每次回報請列出：

- 驗證的是正向路徑還是負向路徑
- 哪個 gate 擋住了請求
- 狀態碼或錯誤類型
- 是否產生副作用
- 是否使用 mock、seed、engineering mode 或 local-only 條件
- 最高驗證層級是 L0-L5 哪一級

如果只驗證正向路徑，要明說 negative smoke 尚未完成。

## 常見 agent 錯誤

- 只看 UI 按鈕消失，沒有打 direct route 或 API
- 把 500 當成「有擋住」，但其實是未處理錯誤
- 把工程模式成功當成正式流程成功
- 把 local env var 補齊當成 provider dashboard 完成
- 為了讓測試通過，把測試改成接受半套行為

