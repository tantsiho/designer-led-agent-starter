# 18 CONTRADICTION AUDIT

這份文件用來讓 agent 主動找產品矛盾，而不是只被動整理設計稿。

真正的 designer-led agent 不只是「不要亂做」，還要能指出設計中會讓後續實作爆炸的地方：流程衝突、商業矛盾、impossible state、誘因不一致、資料真源不一致。

## 何時使用

- 原始設計稿整理完第一輪後
- PM 問題回答後
- 開始實作核心能力前
- 實作後發現狀態或資料互相打架
- 上線 readiness review 前

## 矛盾類型

| 類型 | 檢查問題 | 例子 |
|---|---|---|
| Flow conflict | 兩條流程是否會產生相反結果？ | 取消流程與完成流程同時成立 |
| Business contradiction | 商業承諾和實際規則是否衝突？ | 宣稱即時完成，但需要人工審核 |
| Impossible state | 狀態機是否允許不可能狀態？ | 同一筆資料同時是 canceled 與 completed |
| Incentive mismatch | 使用者最佳行為是否會破壞產品目標？ | 使用者能靠取消 / 重試套利 |
| Data inconsistency | 兩個真源是否會對同一事實給不同答案？ | 前端狀態說已完成，DB 說 pending |
| Permission contradiction | UI 可見能力是否超出角色權限？ | 一般成員看得到管理者資料 |
| Copy contradiction | 文案是否暗示未開放能力已可用？ | 按鈕寫立即啟用，但該能力仍關閉 |

## Audit Table

| ID | 類型 | 發現 | 影響 | 需要決策 | 處置 |
|---|---|---|---|---|---|
| C-001 | 待填 | 待填 | 待填 | yes / no | fix / ask / document / defer |

## Agent Prompt

```text
請不要實作。請根據目前的 PRODUCT_TRUTH、RULES、FLOWS、CAPABILITY_MAP 和 PM_QUESTIONS 主動找產品矛盾。

請分類檢查：
1. flow conflict
2. business contradiction
3. impossible state
4. incentive mismatch
5. data inconsistency
6. permission contradiction
7. copy contradiction

每個發現都要說：
- 矛盾在哪
- 會造成什麼後果
- 是否阻擋目前能力
- 需要設計者回答什麼
- 應寫回哪份真源文件
```
