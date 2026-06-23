# 16 WORKFLOW MODULES

這份文件整理一個長期 AI 代理開發流程中，除了「寫 code」以外實際會做的工作。它可以用來檢查模板是否漏掉重要模組。

## 1. 原始設計稿整理

- 收集長篇、混亂、重複、補充式的產品設計
- 不急著實作
- 先分出核心、例子、未來想法、硬規則、模糊點

## 2. 規則抽取

- 產品真相
- 角色
- 權限
- 狀態
- 流程
- 禁止事項
- 例外情境
- 完成判準

## 3. PM 問答釐清

- 讓代理扮演 PM 追問
- 釐清矛盾、模糊詞、未定義失敗狀態
- 設計者回答後寫回真源文件

## 4. 流程圖與狀態機

- 使用者流程
- 角色泳道
- 狀態轉移
- 失敗路徑
- 資料寫入點
- 權限檢查點

## 5. 能力地圖

- 不按頁面拆，而按能力線拆
- 每條能力要有 UI、API、data、permission、error、test、verification
- 標註現在主線、關閉中、未來工程、歷史參考

## 6. 架構選擇

- 前端 / 後端 / full-stack 判斷
- 資料庫與資料持久化
- 身份系統
- 檔案與圖片儲存
- 外部 provider
- 排程、webhook、通知
- 未來可替換性

## 7. 資料真源治理

- 哪個資料以誰為準
- local / remote / seed / mock 衝突時誰優先
- 重新整理、重啟、重新登入後是否一致
- 舊資料、刪除資料、取消資料是否會復活

## 8. 本地與上線差異

- local development
- engineering mode
- seed / rich seed
- staging / submission-like
- production
- post-deploy smoke
- env var 與外部服務差異

## 9. 防禦與濫用思維

- 越權
- 重複提交
- callback / webhook replay
- 濫用 / spam / rate limit
- direct route
- hidden API
- 敏感資料外露
- rate limit / idempotency
- audit trail

## 10. Capability 開關與關閉一致性

- 功能不是只有做或不做
- 關閉中能力要 UI、API、direct route、文案、測試一致
- 未來工程不得包裝成快完成
- 已做好的未來能力可以保留，但不得變成當前主線假入口

## 11. Seed / Mock / 測試資料治理

- 工程測試資料不能混進正式資料
- mock 不能掩蓋產品缺口
- rich seed 只能幫助驗證，不等於真流程完成
- production fixture 要能被辨識、隔離、清理

## 12. 功能完整性稽核

- UI 有不算完成
- API 有不算完成
- 測試綠也不一定完成
- 要反查是否真流程可走、資料可保存、權限正確、錯誤可處理

## 13. 上線 Readiness

- launch checklist
- deployment checklist
- smoke checklist
- rollback / backup
- production-like verification
- 外部服務與 env gate

## 14. Admin / Ops / 追查能力

- admin 操作
- audit log
- account / user timeline
- report / moderation
- operation feedback
- emergency controls
- 事後追查與人工修正流程

## 15. 通知、Deep Link 與回流

- 通知要帶到正確上下文
- 登入後要回原流程
- 不同角色不要跳錯殼
- 錯誤、取消、完成後要有合理落點

## 16. 對外敘事與 public copy

- 產品不是什麼
- 對外不能誤導已開放能力
- 文案不能暗示未完成或錯誤階段
- 不能被一般模板帶偏定位

## 17. 文件分層與封存

- 現行真源
- 工作草稿
- 歷史參考
- archive
- runbook
- 舊文件不得覆蓋新真源

## 18. 代理回報格式

每批回報要說：

- 為什麼改
- 對應哪條真源
- 改了哪些檔案
- 怎麼驗證
- 哪些沒驗證
- 是否用了 mock / engineering mode / local-only
- 是否還需要 production-like 或 post-deploy 檢查

## 19. Blocker 重估

- 高價值 blocker 解掉後，要判斷是否還值得留在線上
- 剩下若只是低風險 polish，要明說
- 但不能因為低風險就放寬已進場能力的完成標準

## 20. 規範持續回寫

- 每次踩坑都要變成規範
- 每次設計者補充都要寫回真源
- 每次環境、風險、測試、上線差異被發現，都要更新文件
- 不讓下一輪代理重新靠聊天記憶猜

## 21. 決策紀錄

- 記錄為什麼這樣決定
- 保存被排除的 alternative
- 寫清楚 tradeoff、風險與重估條件
- 防止後續 agent 在缺少脈絡時推翻舊決策

## 22. 產品矛盾稽核

- flow conflict
- business contradiction
- impossible state
- incentive mismatch
- data inconsistency
- permission contradiction
- copy contradiction
- 讓 agent 主動發現矛盾，而不是只照單整理

## 23. Cutover 與 incident lessons

- repo migration 不等於完整 production environment
- 外部 dashboard / provider gate 必須列出
- schema drift 要有 runtime preflight
- production 不做代理壓測
- public read 可受控降級，高風險 mutation 必須 fail closed
- incident 復盤要寫回規範、runbook 與驗收 gate

## 24. Designer direction

- 設計師可以用自然語言修正 agent 方向
- agent 偏向一般模板時，要回到 PRODUCT_TRUTH
- agent 補出未確認假設時，要改成 PM 問題
- 未來能力不得包裝成現在主線
- 明確不做事項要寫回 NON_GOALS
- 重要取捨要寫回 decision log，避免後續 agent 推翻
