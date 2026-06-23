# AGENTS

這份文件是給 AI 代理看的工作規則。使用者可能不是工程師，也可能不會使用固定指令。代理必須根據自然語言判斷任務類型，並主動把原始設計稿整理成可執行真源。

## 0. 最高優先原則

1. **設計文件是真源。**
   - 功能是否完成，以設計文件、規則真源與能力閉環為準，不以「畫面看起來有」或「測試會過」代替。
   - 判斷順序固定是：
     1) 是否符合產品真相
     2) 是否符合規則與能力邊界
     3) 是否形成 UI / API / data / permission / error / test 閉環
     4) 是否完成對應驗證

2. **原始設計稿不是實作入口。**
   - 原始設計稿可能很長、很亂、重複、前後補充。
   - 不得直接從 `docs/01_RAW_DESIGN.md` 開始寫 code。
   - 代理第一步必須抽產品真相、名詞、角色、規則、流程、狀態、矛盾與 PM 問題。

3. **設計者負責產品真相，代理負責工程閉環。**
   - 不要求設計者先懂 API、資料庫、auth、CI、部署或安全術語。
   - 代理要用產品語言提問，再把答案轉成工程需求。
   - 不得因為使用者是新手，就降低完成判準。

4. **規範文件是持續長出來的，不是一次性前置產物。**
   - 開工前要先抽真源；開工後也要持續回寫規範。
   - 每次實作、稽核、環境檢查、風險檢查或設計者補充，都可能產生新規則。
   - 新規則不得只留在聊天紀錄，必須寫回對應真源文件。

5. **不要用傳統團隊成本替使用者縮範圍。**
   - 這套模板的目的，是讓代理替新手補上容易漏掉的檢查。
   - 價值排序只能決定先做哪條，不能降低已進場能力的完成標準。

6. **已進場的線，要收成設計一致。**
   - 不能接受半套、假入口、錯誤敘事、mock-only 或與設計不一致的 capability。
   - 若能力屬未來工程或關閉中，必須明確標註，並保持 UI / API / direct route 一致。

7. **只做外科手術。**
   - 不刪除、不簡化、不重構無關邏輯。
   - 只改與本次需求直接相關的範圍。
   - 不因為「看起來可優化」就順手改別的。

8. **MVP 不等於 production guarantee。**
   - 本地通過不等於上線可用。
   - 若未做 staging、production-like 或 post-deploy smoke，必須明說。

## 1. 代理進場入口（必讀）

若任務涉及產品理解、流程判讀、身份、權限、資料保存、外部服務、高風險 mutation、上線、安全、營運、文件真源，開始前先讀：

1. `docs/00_START_HERE.md`
2. `docs/02_PRODUCT_TRUTH.md`
3. `docs/03_GLOSSARY.md`
4. `docs/04_RULES.md`
5. `docs/06_FLOWS_AND_STATES.md`
6. `docs/07_CAPABILITY_MAP.md`
7. `docs/17_DECISION_LOG.md`
8. `docs/18_CONTRADICTION_AUDIT.md`
9. `docs/19_CUTOVER_AND_INCIDENT_LESSONS.md`
10. `docs/20_OPERATIONAL_ATTENTION.md`
11. `docs/21_NEGATIVE_SMOKE_AND_FAIL_CLOSED.md`
12. `docs/22_CONCURRENCY_AND_IDEMPOTENCY.md`
13. `docs/08_ARCHITECTURE_DECISIONS.md`
14. `docs/09_DATA_SOURCE_OF_TRUTH.md`
15. `docs/10_ENVIRONMENT_MODEL.md`
16. `docs/11_RISK_AND_DEFENSE.md`
17. `docs/12_ACCEPTANCE_AND_VERIFICATION.md`

補充：

- `docs/01_RAW_DESIGN.md`：只作原始材料，不可直接作實作真源。
- `docs/05_PM_QUESTIONS.md`：未回答問題若影響本輪實作，必須先問清楚。
- `docs/14_DOCS_MAINTENANCE.md`：若文件互相衝突，以現行真源優先；歷史參考不得覆蓋現行規則。
- `docs/15_NATURAL_LANGUAGE_EXAMPLES.md`：使用者不下指令時，代理應依自然語言判斷模式。

如果必要真源文件尚未建立，本輪先建立或補齊文件，不得直接實作。

## 2. 自然語言工作模式

使用者可能只用自然語言描述需求。代理必須自行判斷目前模式：

1. **Design Intake**
   - 使用者貼長文、想法、設計稿、聊天摘錄。
   - 只做整理與抽取，不寫 code。

2. **Truth Update**
   - 使用者補充、糾正、說「不是這樣」。
   - 更新產品真相、規則、流程或能力地圖。

3. **PM Clarification**
   - 設計稿有矛盾、模糊、未定義流程。
   - 用產品語言提出問題，不用工程術語逼問使用者。

4. **Build**
   - 使用者說「開始做」「先做這個」「做起來」。
   - 先讀真源與能力地圖，再實作一條明確能力線。

5. **Review / Audit**
   - 使用者問「這樣對嗎」「有沒有問題」「是不是半套」。
   - 先審查，不擅自實作。

6. **Readiness Review**
   - 使用者問「可以上線嗎」「能不能用了」。
   - 區分 local、engineering、staging、production-like 與未驗證項。

不確定時，先問 PM 式澄清問題。

## 3. 設計稿抽取規則

從原始設計稿抽取時，至少整理：

1. 產品是什麼 / 不是什麼
2. 使用者角色與權限
3. 核心流程
4. 狀態與狀態轉移
5. 身份與資料歸屬
6. 必須保存的資料
7. 不能外露的資料
8. 失敗狀態與例外
9. 禁止事項
10. 現在主線 / 關閉中能力 / 未來工程 / 歷史參考
11. 容易被一般產品模板帶偏的地方
12. 矛盾、模糊詞、未定義問題

抽取完成後，必須更新：

- `docs/02_PRODUCT_TRUTH.md`
- `docs/03_GLOSSARY.md`
- `docs/04_RULES.md`
- `docs/05_PM_QUESTIONS.md`
- `docs/06_FLOWS_AND_STATES.md`
- `docs/07_CAPABILITY_MAP.md`

## 4. PM 問答規則

代理必須主動問：

1. 這個詞是否有固定定義？
2. 這兩條規則衝突時誰優先？
3. 未登入、權限不足、資料不存在、外部服務失敗時怎麼辦？
4. 這是 MVP 必做、先關閉，還是未來工程？
5. 功能關閉時，UI、API、direct route 是否都要拒絕？
6. 什麼狀態才算完成？
7. 哪些事情絕對不能讓使用者誤解？
8. 哪些資料不能放在 URL、公開頁、log 或錯誤訊息？
9. 哪些行為可能被濫用？
10. 哪些流程需要營運或 admin 追查？

使用者回答後，必須寫回真源文件。不得只把答案留在聊天裡。

## 5. 編輯安全規則

1. 不得刪除、註解、替換、簡化任何現有邏輯，除非使用者明確要求移除或重構。
2. 優先只碰本次需求直接相關檔案；需要跨檔時，只開必要相依檔案。
3. UI 任務預設只動視覺、排版、className、必要組件結構；除非需求本身涉及流程。
4. 流程 / 安全 / 身份 / 權限 / 外部服務 / 高風險 mutation / 上線 / E2E 任務，只動與缺口直接相關的邏輯與驗證，不做順手重構。
5. 不因為某段程式碼像死碼、可優化、沒用到，就自行刪改。
6. UI 任務完成前，必做一次「重複功能 / 重複入口 / 重複按鈕」自查。

## 6. 架構選擇 Gate

任何實作前，代理必須判斷：

1. 這條能力是 frontend-only、full-stack，還是需要獨立 backend？
2. 是否需要資料庫持久化？
3. 是否需要身份、權限、session、re-auth？
4. 是否需要檔案、圖片、通知、排程、webhook、付費服務或外部 provider？
5. 哪些可以 mock，哪些不能 mock？
6. 現在的選擇是否會堵死未來核心能力？
7. 是否需要 admin / ops / audit 介面？

結果必須寫入或更新 `docs/08_ARCHITECTURE_DECISIONS.md`。

## 7. 資料真源 Gate

任何涉及資料的能力，必須回答：

1. 這筆資料的真源是誰？
2. 資料是否需要持久化？
3. 重新整理、重啟、重新登入後是否仍一致？
4. 本地資料、seed/mock、遠端資料衝突時誰優先？
5. 哪些資料不能放 URL、公開頁、log 或錯誤訊息？
6. 刪除、取消、失效後，舊資料是否可能復活？

結果必須寫入或更新 `docs/09_DATA_SOURCE_OF_TRUTH.md`。

## 8. 環境 / 上線 Gate

實作與驗證時必須區分：

1. local development
2. engineering mode
3. test / seed mode
4. staging / submission-like
5. production

必須說明：

- 使用真資料還是 seed/mock
- 是否依賴 engineering-only 入口
- 哪些 env var 或外部服務是必要條件
- 哪些功能在 production 必須關閉
- 本地驗證能代表什麼，不能代表什麼
- 上線後還需要跑什麼 smoke

結果必須寫入或更新 `docs/10_ENVIRONMENT_MODEL.md`。

補充：

- repo migration 完成不等於外部 Auth / Storage / Email / OAuth / provider dashboard 已完成。
- production 不是代理壓測場；完整重複驗證預設先跑 staging / preview。
- public read 可以受控降級，高風險 mutation 必須 fail closed。
- cutover、外部 provider、production incident 的教訓必須寫回 `docs/19_CUTOVER_AND_INCIDENT_LESSONS.md`。
- 長流程、背景工作、callback 或人工處理狀態必須寫回 `docs/20_OPERATIONAL_ATTENTION.md`。
- 禁止路徑、direct route、direct API、capability off 與缺 env/provider 的驗證必須寫回 `docs/21_NEGATIVE_SMOKE_AND_FAIL_CLOSED.md`。
- 重複提交、重試、replay、lock、transaction 與副作用順序必須寫回 `docs/22_CONCURRENCY_AND_IDEMPOTENCY.md`。

## 9. 防禦 / 風險 Gate

任何涉及帳號、資料、內容、權限、admin、外部 callback、背景工作或高風險 mutation 的功能，必須檢查：

1. 越權讀取 / 寫入
2. 重複提交
3. webhook / callback replay
4. 濫用 / spam / rate limit
5. direct route access
6. hidden API access
7. 敏感資料外露
8. URL / log / error message 洩漏
9. rate limit / idempotency
10. admin audit trail
11. fail-closed behavior
12. transaction boundary / side-effect order
13. destructive action confirmation

結果必須寫入或更新 `docs/11_RISK_AND_DEFENSE.md`。

## 10. 功能完整性稽核原則

若本輪目的是確認「功能是否真的做完、是否只是半套、是否可視為可上線」，必須遵守：

1. UI 已露出，不等於完成。
   - 必須確認 API 是否真支援、資料是否保存、權限是否正確、錯誤狀態是否處理。

2. mock / engineering-only 不等於正式完成。
   - 若使用 mock、seed、engineering mode，回報必須明說。

3. capability 關閉時要一致。
   - UI、API、direct route、文案、測試都不得假裝可用。

4. 若發現「產品沒做到底，但測試已被改到會過」：
   - 不得宣告功能完成。
   - 必須先修產品，再修測試。
   - 不得為了讓 CI / smoke 變綠，把測試改成接受半套、mock-only、或與設計不一致的行為。

5. 做這類稽核時，必須同步更新：
   - `docs/13_BUILD_AUDIT.md`
   - 若影響工作規則，更新 `AGENTS.md`

## 11. 上線 / 安全 / 驗證原則

1. 目標是「MVP 可驗證且基本安全運作」，不是宣稱已達成熟 production-grade。
2. 但 MVP 也必須有基本防禦與追查能力，不得裸奔。
3. 優先補：
   - 身份來源一致
   - 權限邊界
   - 高風險 mutation 正確性
   - 資料保存與資料外露邊界
   - audit / 追查能力
   - 本地與上線環境差異
4. 測試優先保護高風險流程，不以「新手專案」為理由壓低必要深度。
5. 但仍要區分：
   - 高風險 mutation / 真頁面操作，應盡量做到真流程驗證
   - 純展示控制，不必一律升成同級高成本 E2E
6. 工程測試不等於上線可用。
   - 凡是改動可能受正式環境影響，例如外部 provider、email、OAuth、webhook、env、CORS、資料庫 schema、部署平台，都不能只以 local 或 engineering mode 通過作為完成。

## 12. 進場後的工作節奏

1. 不要頻繁停下來要使用者確認。
   - 除非遇到真正 blocker、規格衝突、或不可逆決策，否則直接往前整理、實作或稽核。

2. 但以下情況必須先問：
   - 產品真相衝突
   - 會改變能力階段
   - 會引入外部付費服務或敏感 provider
   - 會刪除或大幅重構既有邏輯
   - 會影響資料歸屬、身份、權限、安全、付費服務或上線風險

3. 每一批回報都必須講清楚：
   - 為什麼改
   - 對應哪條設計真源
   - 改了哪些檔案
   - 怎麼驗證
   - 哪些沒有驗證
   - 是否使用 mock / engineering mode / local-only
   - 是否仍需要 production-like 或 post-deploy 檢查

4. 當某條線的高價值 blocker 已解除時，必須主動重估是否還值得留在線上。
   - 若剩下主要只是文案整理、低風險 polishing、非關鍵測試補強，必須明說這已是收尾，不是主 blocker。
   - 但不得因為「價值較低」就放寬已進場工作的完成標準。

## 13. 規範文件持續回寫

以下情況必須同步更新文件：

1. 設計者補充或修正產品判斷。
2. 實作時發現原規則不夠精確。
3. 流程出現未定義狀態、失敗路徑或例外。
4. 重要產品決策、替代方案、取捨或重估條件改變。
5. 架構選擇、資料真源、外部服務或環境條件改變。
6. 發現 mock、engineering mode 或本地驗證掩蓋產品缺口。
7. 發現 cutover、provider dashboard、schema drift、storage/auth/email/env 或 production incident 教訓。
8. 發現新的產品矛盾、impossible state、誘因不一致或資料真源衝突。
9. 發現新的安全、濫用、權限或資料外露風險。
10. 發現驗收條件不足或測試接受半套。
11. 某能力被改成現在主線、關閉中、未來工程或歷史參考。

回寫目標：

- 產品判斷：`docs/02_PRODUCT_TRUTH.md`
- 名詞定義：`docs/03_GLOSSARY.md`
- 硬規則：`docs/04_RULES.md`
- 未解問題：`docs/05_PM_QUESTIONS.md`
- 流程與狀態：`docs/06_FLOWS_AND_STATES.md`
- 能力閉環：`docs/07_CAPABILITY_MAP.md`
- 決策紀錄：`docs/17_DECISION_LOG.md`
- 產品矛盾：`docs/18_CONTRADICTION_AUDIT.md`
- Cutover / incident lessons：`docs/19_CUTOVER_AND_INCIDENT_LESSONS.md`
- Operational attention：`docs/20_OPERATIONAL_ATTENTION.md`
- Negative smoke / fail-closed：`docs/21_NEGATIVE_SMOKE_AND_FAIL_CLOSED.md`
- Concurrency / idempotency：`docs/22_CONCURRENCY_AND_IDEMPOTENCY.md`
- 架構決策：`docs/08_ARCHITECTURE_DECISIONS.md`
- 資料真源：`docs/09_DATA_SOURCE_OF_TRUTH.md`
- 環境差異：`docs/10_ENVIRONMENT_MODEL.md`
- 防禦風險：`docs/11_RISK_AND_DEFENSE.md`
- 驗收驗證：`docs/12_ACCEPTANCE_AND_VERIFICATION.md`
- 實作稽核：`docs/13_BUILD_AUDIT.md`
- 文件分層與封存：`docs/14_DOCS_MAINTENANCE.md`
