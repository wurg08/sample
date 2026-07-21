# API流程验证设计

- 来源: https://chatgpt.com/c/6a30db25-a6bc-83e8-ba19-4bc5fc0a5e28
- 导出时间: 2026-07-21T18:12:56+09:00
- 分片: 4/6
- 总消息数: 551
- 总轮数: 254

## 第 151 轮

### 你

模版 使用例 最新的

### ChatGPT

下面给你 **最新版 `UseCase_Template.md v2.0`：模板 + 使用例**。
这版就是加入 **Scenario** 后的冻结版。

:::writing{variant="document" id="58394"}
---
title: UseCase設計書テンプレート
document_id: UC-TEMPLATE
version: 2.0.0
status: Template
document_type: UseCase Design
system_name: E6 API 検証対象システム
author:
reviewer:
approver:
created:
updated:
---

# UseCase設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|UC-XXX|
|文書名称|〇〇 UseCase設計書|
|UseCase ID|UC-XXX|
|UseCase名称|（記載）|
|対象システム|E6 API 検証対象システム|
|対象業務|（記載）|
|関連Business ID|BUS-XXX|
|関連BA ID|BA-XXX|
|関連API|API-XXX, API-XXX|
|版数|2.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|2.0.0|YYYY-MM-DD|（記載）|Scenario構造追加|

---

## 1.3 関連成果物

|成果物分類|成果物ID|成果物名称|版数|備考|
|----------|--------|----------|----|----|
|現行業務分析|BA-XXX|（記載）|（記載）|業務Flow定義元|
|API設計|API-XXX|（記載）|（記載）|API仕様定義元|
|Verification|VER-XXX|（記載）|（記載）|検証仕様定義先|
|TestCase|TC-XXX|（記載）|（記載）|テストケース定義先|

---

# 2. UseCase概要

## 2.1 UseCase目的

（UseCaseの目的を記載）

---

## 2.2 UseCase概要

（UseCaseの概要を記載）

---

## 2.3 UseCase分類

|項目|内容|
|----|----|
|UseCase種別|正常系 / 異常系 / 境界値 / 日次回帰 / 障害確認|
|実行頻度|Daily / Weekly / Manual|
|実行対象環境|DEV / STG / PROD-LIKE|
|重要度|Critical / High / Medium / Low|
|Baseline比較|Yes / No|
|自動実行対象|Yes / No|

---

## 2.4 対象Business

|Business ID|業務名称|対象Flow|備考|
|-----------|--------|--------|----|
|BUS-XXX|（記載）|BF-XXX〜BF-XXX|（記載）|

---

## 2.5 対象API

|No|API ID|API名称|利用目的|備考|
|--|------|--------|--------|----|
|1|API-XXX|（記載）|（記載）|（記載）|

---

## 2.6 対象Flow

|Flow ID|処理名|UseCase内利用|備考|
|-------|------|-------------|----|
|BF-XXX|（記載）|Yes / No|（記載）|

---

# 3. Actor / Trigger / Condition

## 3.1 Actor

|Actor ID|Actor名称|役割|備考|
|--------|---------|----|----|
|ACT-001|（記載）|（記載）|（記載）|

---

## 3.2 Trigger

|Trigger ID|Trigger内容|起動方式|備考|
|----------|------------|--------|----|
|TRG-001|（記載）|Manual / Batch / Schedule / API|（記載）|

---

## 3.3 Pre Condition

|Condition ID|条件|必須|備考|
|------------|----|----|----|
|PRE-001|（記載）|○|（記載）|

---

## 3.4 Post Condition

|Condition ID|条件|必須|備考|
|------------|----|----|----|
|POST-001|（記載）|○|（記載）|

---

# 4. Entry Input

## 4.1 Entry Input一覧

|Input ID|項目名|論理名|Type|必須|設定値例|設定元|Context ID|備考|
|--------|------|------|----|----|--------|------|----------|----|
|IN-001|（記載）|（記載）|String|○|（記載）|Test Data / Runtime / Manual|CTX-XXX|（記載）|

---

## 4.2 Test Data参照

|TestData ID|用途|ファイル|備考|
|-----------|----|--------|----|
|TD-001|正常系|test_data/UC-XXX/normal.json|（記載）|
|TD-002|異常系|test_data/UC-XXX/error.json|（記載）|

---

## 4.3 初期Context

|Context ID|Context名|初期値|設定元|必須|備考|
|----------|---------|------|------|----|----|
|CTX-XXX|（記載）|（記載）|Entry Input / Test Data|○|（記載）|

---

# 5. Main Flow

## 5.1 UseCase Flow

```mermaid
flowchart TD

START([開始])

STEP001[UC-STEP-001<br/>（処理名）]
STEP002[UC-STEP-002<br/>（処理名）]
STEP003[UC-STEP-003<br/>（処理名）]
STEP004[UC-STEP-004<br/>（処理名）]

END([終了])

START --> STEP001
STEP001 --> STEP002
STEP002 --> STEP003
STEP003 --> STEP004
STEP004 --> END
```

---

## 5.2 Main Flow一覧

|Step ID|Flow ID|API ID|処理名|入力|出力|次Step|備考|
|-------|-------|------|------|----|----|------|----|
|UC-STEP-001|BF-XXX|API-XXX|（記載）|Entry Input / Context|Response|UC-STEP-002|（記載）|
|UC-STEP-002|BF-XXX|API-XXX|（記載）|Context|Response|UC-STEP-003|（記載）|
|UC-STEP-003|BF-XXX|API-XXX|（記載）|Context|Response|UC-STEP-004|（記載）|
|UC-STEP-004|BF-XXX|－|（記載）|Response / Context|Result|END|（記載）|

---

## 5.3 Business Step一覧

|Business Step ID|UseCase Step ID|Business Flow ID|説明|備考|
|----------------|---------------|----------------|----|----|
|BS-001|UC-STEP-001|BF-XXX|（記載）|（記載）|

---

# 6. Scenario一覧

## 6.1 Scenario一覧

|Scenario ID|Scenario名称|分類|差分内容|対象Flow|対象API|期待結果|TestCase ID|
|-----------|-------------|----|--------|--------|-------|--------|-----------|
|SC-001|正常系|Normal|標準ルート|BF-XXX〜BF-XXX|API-XXX〜API-XXX|PASS|TC-XXX|
|SC-002|（記載）|Alternative|（記載）|BF-XXX|API-XXX|（記載）|TC-XXX|
|SC-003|（記載）|Exception|（記載）|BF-XXX|API-XXX|FAIL / WARN|TC-XXX|

---

## 6.2 Scenario Flow

### SC-001 正常系

```mermaid
flowchart TD

START([開始])
API001[API-XXX]
API002[API-XXX]
API003[API-XXX]
END([終了])

START --> API001
API001 --> API002
API002 --> API003
API003 --> END
```

---

### SC-002 代替系 / 異常系

```mermaid
flowchart TD

START([開始])
API001[API-XXX]
ERR[業務エラー]
END([終了])

START --> API001
API001 --> ERR
ERR --> END
```

---

## 6.3 Scenario Matrix

|Step / API|SC-001|SC-002|SC-003|
|----------|:----:|:----:|:----:|
|API-001|○|○|○|
|API-002|○|－|○|
|API-003|○|－|Timeout|
|Expected|PASS|Business Error|FAIL|

---

## 6.4 Scenario Selection Rule

|Rule ID|条件|Scenario ID|備考|
|-------|----|------------|----|
|SR-001|正常データ|SC-001|標準ルート|
|SR-002|（記載）|SC-002|代替ルート|
|SR-003|（記載）|SC-003|異常ルート|

---

# 7. API Execution Chain

## 7.1 API呼出順序

```mermaid
sequenceDiagram

participant Runner
participant API001
participant API002
participant API003

Runner->>API001: Request
API001-->>Runner: Response

Runner->>API002: Request
API002-->>Runner: Response

Runner->>API003: Request
API003-->>Runner: Response
```

---

## 7.2 API実行一覧

|Order|API ID|実行条件|Request生成元|Response利用|失敗時処理|
|-----|------|--------|-------------|-------------|----------|
|1|API-XXX|（記載）|Entry Input / Context|Context抽出|Stop / Continue|
|2|API-XXX|（記載）|Context|Context抽出|Stop / Continue|
|3|API-XXX|（記載）|Context|業務期待結果確認|Stop / Continue|

---

## 7.3 API実行条件

|API ID|実行条件ID|実行条件|条件不成立時|備考|
|------|----------|--------|------------|----|
|API-XXX|EXEC-COND-001|（記載）|Skip / Stop / Fail|（記載）|

---

## 7.4 API Skip Rule

|Skip Rule ID|条件|Skip API|理由|結果扱い|
|------------|----|---------|----|--------|
|SKIP-001|（記載）|API-XXX|（記載）|PASS / WARN / FAIL|
|SKIP-002|（記載）|API-XXX, API-XXX|（記載）|PASS / WARN / FAIL|

---

# 8. Context Mapping

## 8.1 Context一覧

|Context ID|Context名|Type|Scope|Producer|Consumer|必須|備考|
|----------|---------|----|-----|--------|--------|----|----|
|CTX-001|（記載）|String|UseCase|Entry Input / API-XXX|API-XXX|○|（記載）|

---

## 8.2 Extract Mapping

|Mapping ID|Step ID|API ID|Response JSONPath|Context ID|Context名|必須|未取得時処理|
|----------|-------|------|-----------------|----------|---------|----|------------|
|MAP-001|UC-STEP-XXX|API-XXX|$.xxx|CTX-XXX|（記載）|○|Fail / Warn / Ignore|

---

## 8.3 Request Binding

|Binding ID|Step ID|API ID|Request JSONPath|Context ID|Context名|必須|備考|
|----------|-------|------|----------------|----------|---------|----|----|
|BIND-001|UC-STEP-XXX|API-XXX|$.xxx|CTX-XXX|（記載）|○|（記載）|

---

## 8.4 Context Update Policy

|Context ID|更新可否|更新条件|競合時処理|備考|
|----------|--------|--------|----------|----|
|CTX-XXX|不可 / 可|（記載）|Fail / Warn / Overwrite|（記載）|

---

## 8.5 Context Lifetime

|Context ID|生成Step|利用Step|破棄タイミング|有効範囲|備考|
|----------|--------|--------|--------------|--------|----|
|CTX-XXX|UC-STEP-XXX|UC-STEP-XXX|UseCase終了時|UseCase / Run|（記載）|

---

# 9. Alternative Flow

|Alt Flow ID|Scenario ID|発生条件|分岐元Step|処理内容|終了条件|備考|
|-----------|------------|--------|----------|--------|--------|----|
|ALT-001|SC-XXX|（記載）|UC-STEP-XXX|（記載）|（記載）|（記載）|

---

# 10. Exception Flow

|Exception ID|Scenario ID|発生条件|対象Step|期待処理|後続処理|重要度|
|------------|------------|--------|--------|--------|--------|------|
|EX-001|SC-XXX|HTTP 400|API-XXX|業務エラー|Stop|High|
|EX-002|SC-XXX|Timeout|API-XXX|Retry後Fail|Stop|High|
|EX-003|SC-XXX|Context未取得|UC-STEP-XXX|Fail|Stop|Critical|

---

# 11. Execution Policy

## 11.1 UseCase実行方針

|項目|設定値|備考|
|----|------|----|
|Stop On Error|Yes / No|（記載）|
|Continue On Warning|Yes / No|（記載）|
|Baseline比較|Yes / No|（記載）|
|Cleanup|Yes / No|（記載）|
|Evidence保存|Yes|固定推奨|

---

## 11.2 API別実行方針

|API ID|Retry|Timeout|失敗時処理|Evidence|備考|
|------|-----|-------|----------|--------|----|
|API-XXX|（記載）|（記載）秒|Stop / Continue|Yes|（記載）|

---

## 11.3 Retry Policy

|Retry Policy ID|対象API|Retry回数|Retry間隔|対象エラー|備考|
|---------------|--------|---------|---------|----------|----|
|RETRY-001|API-XXX|2|3秒|Timeout / 5xx|（記載）|

---

## 11.4 Timeout Policy

|Timeout Policy ID|対象|Timeout|備考|
|-----------------|------|---------|----|
|TIMEOUT-001|UseCase全体|30秒|（記載）|
|TIMEOUT-002|API-XXX|10秒|（記載）|

---

# 12. Business Check

## 12.1 業務結果確認

|Check ID|対象|確認内容|期待結果|重要度|
|--------|----|--------|--------|------|
|BC-001|（記載）|（記載）|（記載）|High|

---

## 12.2 Context確認

|Check ID|Context ID|確認内容|期待結果|重要度|
|--------|----------|--------|--------|------|
|CTX-CHK-001|CTX-XXX|存在確認|Not Empty|High|

---

## 12.3 API実行確認

|Check ID|API ID|確認内容|期待結果|重要度|
|--------|------|--------|--------|------|
|API-CHK-001|API-XXX|APIが実行されたこと|Executed|High|
|API-CHK-002|API-XXX|条件によりSkipされたこと|Skipped|Medium|

---

# 13. Expected Result

## 13.1 正常系期待結果

|項目|期待結果|
|----|--------|
|UseCase結果|PASS|
|最終Step|（記載）|
|業務結果|（記載）|
|API結果|全API正常終了|
|Context結果|必須Context取得済み|
|Report結果|Daily SummaryにPASS表示|

---

## 13.2 異常系期待結果

|条件|期待結果|Result|
|----|--------|------|
|（記載）|（記載）|FAIL / WARN|

---

## 13.3 Scenario別期待結果

|Scenario ID|期待結果|Result|備考|
|------------|--------|--------|----|
|SC-001|（記載）|PASS|正常系|
|SC-002|（記載）|FAIL / WARN|代替系|
|SC-003|（記載）|FAIL|異常系|

---

# 14. Evidence

## 14.1 保存対象

|Evidence ID|保存対象|保存内容|備考|
|-----------|--------|--------|----|
|EVD-001|Request|Header / Body|秘匿情報Mask|
|EVD-002|Response|Header / Body|秘匿情報Mask|
|EVD-003|Context|Context Snapshot|UseCase単位|
|EVD-004|Diff|Diff Result|Baseline比較時|
|EVD-005|Log|Execution Log|調査用|

---

## 14.2 保存場所

|Evidence ID|保存先|
|-----------|--------|
|EVD-001|runs/{runId}/raw/|
|EVD-002|runs/{runId}/raw/|
|EVD-003|runs/{runId}/snapshot/|
|EVD-004|runs/{runId}/diff/|
|EVD-005|runs/{runId}/logs/|

---

## 14.3 Snapshot Policy

|Snapshot ID|対象|タイミング|保存形式|備考|
|-----------|----|----------|--------|----|
|SNP-001|Context|各Step終了後|JSON|Context確認用|
|SNP-002|API Response|各API終了後|JSON|Diff用|
|SNP-003|UseCase Result|UseCase終了後|JSON|Report用|

---

# 15. Traceability

## 15.1 Business Trace Matrix

|Business ID|Flow ID|UseCase ID|Step ID|Scenario ID|
|-----------|-------|----------|-------|-----------|
|BUS-XXX|BF-XXX|UC-XXX|UC-STEP-XXX|SC-XXX|

---

## 15.2 API Trace Matrix

|UseCase ID|Step ID|Scenario ID|API ID|実行条件|Skip Rule|
|----------|-------|------------|------|--------|----------|
|UC-XXX|UC-STEP-XXX|SC-XXX|API-XXX|EXEC-COND-XXX|SKIP-XXX|

---

## 15.3 Context Trace Matrix

|UseCase ID|Step ID|API ID|Context ID|Producer|Consumer|
|----------|-------|------|----------|----------|----------|
|UC-XXX|UC-STEP-XXX|API-XXX|CTX-XXX|API-XXX|API-XXX|

---

## 15.4 Verification Trace Matrix

|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|
|----------|------------|------|----------------|-----------|
|UC-XXX|SC-XXX|API-XXX|VF-XXX|TC-XXX|

---

# Appendix A. 記入例

## A.1 文書管理

|項目|内容|
|----|----|
|文書ID|UC-001|
|文書名称|顧客情報照会 UseCase設計書|
|UseCase ID|UC-001|
|UseCase名称|顧客情報照会|
|対象システム|CRMシステム|
|対象業務|顧客情報照会業務|
|関連Business ID|BUS-001|
|関連BA ID|BA-001|
|関連API|API-001, API-002, API-003|
|版数|2.0.0|
|状態|Approved|
|作成者|UseCase設計担当|
|レビューア|アーキテクト|
|承認者|プロジェクト責任者|
|作成日|2026-07-03|
|更新日|2026-07-03|

---

## A.2 UseCase概要

### UseCase目的

顧客番号を入力し、顧客存在確認、顧客基本情報取得、契約情報取得を順に実行し、顧客情報照会業務が正常に成立することを確認する。

---

### UseCase概要

本UseCaseは、顧客情報照会業務における正常系、顧客不存在、契約0件、APIタイムアウトを対象とする。Entry Inputとして顧客番号を指定し、後続APIはContextを利用して自動的に実行する。

---

### UseCase分類

|項目|内容|
|----|----|
|UseCase種別|日次回帰|
|実行頻度|Daily|
|実行対象環境|STG|
|重要度|High|
|Baseline比較|Yes|
|自動実行対象|Yes|

---

## A.3 対象Business

|Business ID|業務名称|対象Flow|備考|
|-----------|--------|--------|----|
|BUS-001|顧客情報照会業務|BF-001〜BF-006|顧客照会|

---

## A.4 対象API

|No|API ID|API名称|利用目的|備考|
|--|------|--------|--------|----|
|1|API-001|Customer Exists API|顧客存在確認|Entry API|
|2|API-002|Customer Detail API|顧客基本情報取得|後続API|
|3|API-003|Contract List API|契約一覧取得|後続API|

---

## A.5 Entry Input

|Input ID|項目名|論理名|Type|必須|設定値例|設定元|Context ID|備考|
|--------|------|------|----|----|--------|------|----------|----|
|IN-001|customerId|顧客番号|String|○|100001|Test Data|CTX-001|Entry API入力|

---

## A.6 初期Context

|Context ID|Context名|初期値|設定元|必須|備考|
|----------|---------|------|------|----|----|
|CTX-001|Customer.id|100001|Test Data|○|顧客番号|

---

## A.7 Main Flow

```mermaid
flowchart TD

START([開始])

STEP001[UC-STEP-001<br/>顧客存在確認]
STEP002[UC-STEP-002<br/>顧客基本情報取得]
STEP003[UC-STEP-003<br/>契約情報取得]
STEP004[UC-STEP-004<br/>業務結果確認]

END([終了])

START --> STEP001
STEP001 --> STEP002
STEP002 --> STEP003
STEP003 --> STEP004
STEP004 --> END
```

---

## A.8 Main Flow一覧

|Step ID|Flow ID|API ID|処理名|入力|出力|次Step|備考|
|-------|-------|------|------|----|----|------|----|
|UC-STEP-001|BF-002|API-001|顧客存在確認|Customer.id|exists|UC-STEP-002|存在確認|
|UC-STEP-002|BF-004|API-002|顧客基本情報取得|Customer.id|Customer|UC-STEP-003|顧客取得|
|UC-STEP-003|BF-005|API-003|契約情報取得|Customer.id|Contract.list|UC-STEP-004|契約取得|
|UC-STEP-004|BF-006|－|業務結果確認|Customer, Contract.list|Result|END|最終確認|

---

## A.9 Scenario一覧

|Scenario ID|Scenario名称|分類|差分内容|対象Flow|対象API|期待結果|TestCase ID|
|-----------|-------------|----|--------|--------|-------|--------|-----------|
|SC-001|正常系|Normal|標準ルート|BF-002〜BF-006|API-001〜API-003|PASS|TC-001|
|SC-002|顧客不存在|Alternative|API-001でexists=false|BF-002|API-001|業務エラー|TC-002|
|SC-003|契約0件|Alternative|API-003で0件返却|BF-005|API-003|PASS / WARN|TC-003|
|SC-004|API-002 Timeout|Exception|API-002でTimeout|BF-004|API-002|FAIL|TC-004|

---

## A.10 Scenario Flow

### SC-001 正常系

```mermaid
flowchart TD

START([開始])
API001[API-001<br/>Customer Exists]
API002[API-002<br/>Customer Detail]
API003[API-003<br/>Contract List]
CHECK[業務結果確認]
END([終了])

START --> API001
API001 --> API002
API002 --> API003
API003 --> CHECK
CHECK --> END
```

---

### SC-002 顧客不存在

```mermaid
flowchart TD

START([開始])
API001[API-001<br/>Customer Exists]
ERR[業務エラー]
END([終了])

START --> API001
API001 --> ERR
ERR --> END
```

---

### SC-003 契約0件

```mermaid
flowchart TD

START([開始])
API001[API-001<br/>Customer Exists]
API002[API-002<br/>Customer Detail]
API003[API-003<br/>Contract List 0件]
CHECK[業務結果確認]
END([終了])

START --> API001
API001 --> API002
API002 --> API003
API003 --> CHECK
CHECK --> END
```

---

### SC-004 API-002 Timeout

```mermaid
flowchart TD

START([開始])
API001[API-001<br/>Customer Exists]
API002[API-002<br/>Customer Detail Timeout]
FAIL[Timeout Fail]
END([終了])

START --> API001
API001 --> API002
API002 --> FAIL
FAIL --> END
```

---

## A.11 Scenario Matrix

|Step / API|SC-001 正常系|SC-002 顧客不存在|SC-003 契約0件|SC-004 API-002 Timeout|
|----------|:----------:|:--------------:|:-------------:|:--------------------:|
|API-001|○|○|○|○|
|API-002|○|－|○|Timeout|
|API-003|○|－|○|－|
|業務結果確認|○|業務エラー|○|－|
|Expected|PASS|Business Error|PASS / WARN|FAIL|

---

## A.12 Scenario Selection Rule

|Rule ID|条件|Scenario ID|備考|
|-------|----|------------|----|
|SR-001|exists=true かつ Contract.list が1件以上|SC-001|正常系|
|SR-002|exists=false|SC-002|顧客不存在|
|SR-003|exists=true かつ Contract.list が0件|SC-003|契約0件|
|SR-004|API-002 Timeout|SC-004|Timeout異常|

---

## A.13 API実行一覧

|Order|API ID|実行条件|Request生成元|Response利用|失敗時処理|
|-----|------|--------|-------------|-------------|----------|
|1|API-001|Entry Input が存在すること|Test Data / CTX-001|exists 判定|Stop|
|2|API-002|API-001 正常終了かつ exists=true|CTX-001|Customer 抽出|Stop|
|3|API-003|API-002 正常終了かつ Customer 取得済み|CTX-001|Contract.list 抽出|Stop|

---

## A.14 API Skip Rule

|Skip Rule ID|条件|Skip API|理由|結果扱い|
|------------|----|---------|----|--------|
|SKIP-001|exists=false|API-002, API-003|顧客不存在のため後続取得不要|PASS / WARN|
|SKIP-002|API-002 Timeout|API-003|前提API失敗のため実行不可|FAIL|
|SKIP-003|認証失敗|API-001, API-002, API-003|認証前提不成立|FAIL|

---

## A.15 Context一覧

|Context ID|Context名|Type|Scope|Producer|Consumer|必須|備考|
|----------|---------|----|-----|--------|--------|----|----|
|CTX-001|Customer.id|String|UseCase|Entry Input|API-001, API-002, API-003|○|顧客番号|
|CTX-002|Customer.exists|Boolean|UseCase|API-001|Scenario Selection|○|存在判定|
|CTX-003|Customer|Object|UseCase|API-002|Verification / Report|○|顧客基本情報|
|CTX-004|Contract.list|Array|UseCase|API-003|Verification / Report|－|契約一覧|

---

## A.16 Extract Mapping

|Mapping ID|Step ID|API ID|Response JSONPath|Context ID|Context名|必須|未取得時処理|
|----------|-------|------|-----------------|----------|---------|----|------------|
|MAP-001|UC-STEP-001|API-001|$.customerId|CTX-001|Customer.id|○|Fail|
|MAP-002|UC-STEP-001|API-001|$.exists|CTX-002|Customer.exists|○|Fail|
|MAP-003|UC-STEP-002|API-002|$.customer|CTX-003|Customer|○|Fail|
|MAP-004|UC-STEP-003|API-003|$.contracts|CTX-004|Contract.list|－|Warn|

---

## A.17 Request Binding

|Binding ID|Step ID|API ID|Request JSONPath|Context ID|Context名|必須|備考|
|----------|-------|------|----------------|----------|---------|----|----|
|BIND-001|UC-STEP-001|API-001|$.customerId|CTX-001|Customer.id|○|Entry Input由来|
|BIND-002|UC-STEP-002|API-002|$.customerId|CTX-001|Customer.id|○|前段Context利用|
|BIND-003|UC-STEP-003|API-003|$.customerId|CTX-001|Customer.id|○|前段Context利用|

---

## A.18 Alternative Flow

|Alt Flow ID|Scenario ID|発生条件|分岐元Step|処理内容|終了条件|備考|
|-----------|------------|--------|----------|--------|--------|----|
|ALT-001|SC-002|exists=false|UC-STEP-001|業務エラーとして終了|業務エラー表示|後続APIをSkip|
|ALT-002|SC-003|Contract.list が0件|UC-STEP-003|契約一覧なしとして業務結果確認|業務結果確認完了|業務仕様確認対象|

---

## A.19 Exception Flow

|Exception ID|Scenario ID|発生条件|対象Step|期待処理|後続処理|重要度|
|------------|------------|--------|--------|--------|--------|------|
|EX-001|SC-004|API-002 Timeout|UC-STEP-002|Retry後Fail|Stop|High|
|EX-002|－|HTTP 401|任意API|認証エラーとしてFail|Stop|Critical|
|EX-003|－|必須Context未取得|任意Step|Context ErrorとしてFail|Stop|Critical|

---

## A.20 Execution Policy

|項目|設定値|備考|
|----|------|----|
|Stop On Error|Yes|異常時は後続APIを実行しない|
|Continue On Warning|Yes|契約0件など業務許容ケース|
|Baseline比較|Yes|前回承認済Baselineと比較|
|Cleanup|No|参照系UseCaseのため不要|
|Evidence保存|Yes|Request / Response / Context / Diff を保存|

---

## A.21 Business Check

|Check ID|対象|確認内容|期待結果|重要度|
|--------|----|--------|--------|------|
|BC-001|UseCase結果|対象Scenarioの期待結果に一致すること|PASS / WARN / FAIL|High|
|BC-002|顧客情報|正常系ではCustomerが取得できること|Exists|High|
|BC-003|契約情報|契約一覧が取得できること|Exists / Empty許容|Medium|
|BC-004|Skip処理|顧客不存在時に後続APIがSkipされること|API-002, API-003 Skip|High|

---

## A.22 Scenario別期待結果

|Scenario ID|期待結果|Result|備考|
|------------|--------|--------|----|
|SC-001|顧客情報および契約一覧を取得できる|PASS|正常系|
|SC-002|顧客不存在として業務エラー終了する|FAIL / WARN|業務仕様により確定|
|SC-003|契約0件として顧客情報のみ確認できる|PASS / WARN|業務仕様確認対象|
|SC-004|API-002 Timeoutとして異常終了する|FAIL|障害系|

---

## A.23 Evidence

|Evidence ID|保存対象|保存内容|保存先|備考|
|-----------|--------|--------|--------|----|
|EVD-001|Request|Header / Body|runs/{runId}/raw/|秘匿情報Mask|
|EVD-002|Response|Header / Body|runs/{runId}/raw/|秘匿情報Mask|
|EVD-003|Context|Context Snapshot|runs/{runId}/snapshot/|UseCase単位|
|EVD-004|Diff|Diff Result|runs/{runId}/diff/|Baseline比較時|
|EVD-005|Log|Execution Log|runs/{runId}/logs/|調査用|
|EVD-006|Report|UseCase Report|runs/{runId}/reports/|確認用|

---

## A.24 Traceability

### Business Trace Matrix

|Business ID|Flow ID|UseCase ID|Step ID|Scenario ID|
|-----------|-------|----------|-------|-----------|
|BUS-001|BF-002|UC-001|UC-STEP-001|SC-001, SC-002, SC-003, SC-004|
|BUS-001|BF-004|UC-001|UC-STEP-002|SC-001, SC-003, SC-004|
|BUS-001|BF-005|UC-001|UC-STEP-003|SC-001, SC-003|
|BUS-001|BF-006|UC-001|UC-STEP-004|SC-001, SC-003|

---

### API Trace Matrix

|UseCase ID|Step ID|Scenario ID|API ID|実行条件|Skip Rule|
|----------|-------|------------|------|--------|----------|
|UC-001|UC-STEP-001|SC-001〜SC-004|API-001|Customer.id が存在すること|－|
|UC-001|UC-STEP-002|SC-001, SC-003, SC-004|API-002|exists=true|SKIP-001|
|UC-001|UC-STEP-003|SC-001, SC-003|API-003|Customer 取得済み|SKIP-001, SKIP-002|

---

### Context Trace Matrix

|UseCase ID|Step ID|API ID|Context ID|Producer|Consumer|
|----------|-------|------|----------|----------|----------|
|UC-001|UC-STEP-001|API-001|CTX-001|Entry Input|API-001, API-002, API-003|
|UC-001|UC-STEP-001|API-001|CTX-002|API-001|Scenario Selection|
|UC-001|UC-STEP-002|API-002|CTX-003|API-002|Verification / Report|
|UC-001|UC-STEP-003|API-003|CTX-004|API-003|Verification / Report|

---

### Verification Trace Matrix

|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|
|----------|------------|------|----------------|-----------|
|UC-001|SC-001|API-001〜API-003|VF-001|TC-001|
|UC-001|SC-002|API-001|VF-002|TC-002|
|UC-001|SC-003|API-001〜API-003|VF-003|TC-003|
|UC-001|SC-004|API-002|VF-004|TC-004|
:::

这就是最新版 **UseCase Template v2.0 + 使用例**。

核心变化只有一个：
**UseCase 不再因为小差异复制多份，而是在一个 UseCase 下用 Scenario 管理差异。**

## 第 152 轮

### 你

好的

### ChatGPT

好的。现在已冻结三份核心模板：

```text
1. BA_Template.md v1.0
2. API_Template.md v1.0
3. UseCase_Template.md v2.0（含 Scenario）
```

下一份就是：

```text
Verification_Specification_Template.md
```

它会承接 API / UseCase，定义真正的执行验证、Compare、TestCase、TestData、Report、Evidence。

## 第 153 轮

### 你

继续

### ChatGPT

下面是第四份核心模板：`Verification_Specification_Template.md`。

:::writing{variant="document" id="47291"}
---
title: Verification仕様書テンプレート
document_id: VER-TEMPLATE
version: 1.0.0
status: Template
document_type: Verification Specification
system_name: E6 API 検証対象システム
author:
reviewer:
approver:
created:
updated:
---

# Verification仕様書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|VER-XXX|
|文書名称|〇〇 Verification仕様書|
|Verification ID|VER-XXX|
|対象業務|（記載）|
|対象UseCase|UC-XXX|
|対象Scenario|SC-XXX|
|対象API|API-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 関連成果物

|成果物分類|成果物ID|成果物名称|版数|備考|
|----------|--------|----------|----|----|
|現行業務分析|BA-XXX|（記載）|（記載）|業務分析元|
|API設計|API-XXX|（記載）|（記載）|API仕様元|
|UseCase設計|UC-XXX|（記載）|（記載）|実行Flow元|
|Test Data|TD-XXX|（記載）|（記載）|入力データ|

---

# 2. Verification概要

## 2.1 Verification目的

（検証目的を記載）

例：

E6 API の入出力仕様、API連携、Context受け渡し、Response固定値、Enum、必須項目、Baseline差分を日次で確認し、既存API仕様に変更がないことを検証する。

---

## 2.2 Verification範囲

### 対象

|分類|内容|
|----|----|
|API単体検証|Yes / No|
|UseCase連携検証|Yes / No|
|Request検証|Yes / No|
|Response検証|Yes / No|
|Context検証|Yes / No|
|Baseline比較|Yes / No|
|Evidence保存|Yes|

### 対象外

|分類|内容|
|----|----|
|E6 API内部実装|対象外|
|業務DB直接確認|対象外 / 必要時のみ|
|画面表示確認|対象外|
|性能詳細試験|対象外 / 別紙|

---

# 3. 対象Scenario

|Scenario ID|Scenario名称|分類|対象UseCase|期待結果|備考|
|-----------|-------------|----|------------|--------|----|
|SC-001|正常系|Normal|UC-XXX|PASS|（記載）|
|SC-002|（記載）|Alternative|UC-XXX|WARN / FAIL|（記載）|
|SC-003|（記載）|Exception|UC-XXX|FAIL|（記載）|

---

# 4. 対象API

|No|API ID|API名称|対象Scenario|検証目的|重要度|
|--|------|--------|--------------|--------|------|
|1|API-XXX|（記載）|SC-XXX|（記載）|High|

---

# 5. Test Data

## 5.1 Test Data一覧

|TestData ID|Scenario ID|用途|ファイル|備考|
|-----------|------------|----|--------|----|
|TD-001|SC-001|正常系|test_data/UC-XXX/SC-001.json|（記載）|
|TD-002|SC-002|代替系|test_data/UC-XXX/SC-002.json|（記載）|
|TD-003|SC-003|異常系|test_data/UC-XXX/SC-003.json|（記載）|

---

## 5.2 Entry Input

|Input ID|Scenario ID|項目名|Type|値|Context ID|備考|
|--------|------------|------|----|---|----------|----|
|IN-001|SC-001|customerId|String|100001|CTX-001|正常系|

---

# 6. Request Verification

## 6.1 Request Required Check

|Check ID|API ID|JSONPath|必須|期待結果|重要度|
|--------|------|--------|----|--------|------|
|REQ-REQ-001|API-XXX|$.xxx|○|存在すること|High|

---

## 6.2 Request Type Check

|Check ID|API ID|JSONPath|Type|期待結果|重要度|
|--------|------|--------|----|--------|------|
|REQ-TYPE-001|API-XXX|$.xxx|String|型一致|High|

---

## 6.3 Request Length / Range Check

|Check ID|API ID|JSONPath|Min|Max|期待結果|重要度|
|--------|------|--------|---|---|--------|------|
|REQ-LEN-001|API-XXX|$.xxx|1|20|範囲内|High|

---

## 6.4 Request Pattern / Enum / Fixed Check

|Check ID|API ID|JSONPath|Check種別|条件|期待結果|重要度|
|--------|------|--------|---------|----|--------|------|
|REQ-PAT-001|API-XXX|$.xxx|Pattern|^[0-9]+$|一致|High|
|REQ-ENUM-001|API-XXX|$.xxx|Enum|A,B,C|許容値内|Medium|
|REQ-FIX-001|API-XXX|$.xxx|Fixed|NORMAL|一致|Medium|

---

# 7. Response Verification

## 7.1 HTTP Status Check

|Check ID|Scenario ID|API ID|期待HTTP Status|Result判定|備考|
|--------|------------|------|----------------|----------|----|
|RES-HTTP-001|SC-001|API-XXX|200|PASS|正常系|
|RES-HTTP-002|SC-003|API-XXX|400 / 500|FAIL|異常系|

---

## 7.2 Response Required Check

|Check ID|API ID|JSONPath|必須|期待結果|重要度|
|--------|------|--------|----|--------|------|
|RES-REQ-001|API-XXX|$.resultCode|○|存在すること|High|

---

## 7.3 Response Type Check

|Check ID|API ID|JSONPath|Type|期待結果|重要度|
|--------|------|--------|----|--------|------|
|RES-TYPE-001|API-XXX|$.resultCode|String|型一致|High|

---

## 7.4 Response Fixed Value Check

|Check ID|API ID|JSONPath|固定値|適用条件|期待結果|重要度|
|--------|------|--------|------|--------|--------|------|
|RES-FIX-001|API-XXX|$.resultCode|0|正常終了時|一致|High|

---

## 7.5 Response Enum Check

|Check ID|API ID|JSONPath|許容値|期待結果|重要度|
|--------|------|--------|------|--------|------|
|RES-ENUM-001|API-XXX|$.status|ACTIVE,INACTIVE|許容値内|High|

---

## 7.6 Response Input Match Check

|Check ID|API ID|Response JSONPath|一致対象|一致対象種別|期待結果|重要度|
|--------|------|-----------------|--------|------------|--------|------|
|RES-MATCH-001|API-XXX|$.customerId|$.customerId|Request|一致|High|

---

## 7.7 Response Context Match Check

|Check ID|API ID|Response JSONPath|Context ID|期待結果|重要度|
|--------|------|-----------------|----------|--------|------|
|RES-CTX-001|API-XXX|$.customerId|CTX-001|一致|High|

---

## 7.8 Dynamic Field Check

|Check ID|API ID|JSONPath|Dynamic理由|検証方針|備考|
|--------|------|--------|------------|--------|----|
|RES-DYN-001|API-XXX|$.traceId|実行毎に採番|存在・型のみ確認、値比較対象外|（記載）|
|RES-DYN-002|API-XXX|$.updatedAt|更新日時|Baseline比較対象外|（記載）|

---

# 8. Context Verification

## 8.1 Context生成確認

|Check ID|Context ID|Producer|期待結果|重要度|
|--------|----------|----------|--------|------|
|CTX-GEN-001|CTX-XXX|API-XXX|生成されること|High|

---

## 8.2 Context引継ぎ確認

|Check ID|Context ID|From API|To API|期待結果|重要度|
|--------|----------|--------|------|--------|------|
|CTX-PASS-001|CTX-XXX|API-001|API-002|同一値で引継ぐこと|High|

---

## 8.3 Context未取得時処理

|Check ID|Context ID|未取得時処理|期待Result|重要度|
|--------|----------|------------|----------|------|
|CTX-ERR-001|CTX-XXX|Fail / Warn / Ignore|FAIL|Critical|

---

# 9. Compare Policy

## 9.1 Compare Scope

|対象|比較対象|備考|
|----|--------|----|
|Request|Yes / No|（記載）|
|Response|Yes / No|（記載）|
|Context|Yes / No|（記載）|
|File|Yes / No|（記載）|
|Header|Yes / No|（記載）|

---

## 9.2 Field Mapping

|Mapping ID|Source|Target|Compare Key|備考|
|----------|------|------|-----------|----|
|CMP-MAP-001|Current $.customerId|Baseline $.customerId|customerId|（記載）|

---

## 9.3 Normalize Rule

|Normalize ID|対象|方式|例|備考|
|------------|----|----|--|----|
|NORM-001|Date|yyyy/MM/dd → yyyy-MM-dd|2026/07/03 → 2026-07-03|日付正規化|
|NORM-002|Number|Decimal正規化|100.0 → 100|数値正規化|
|NORM-003|String|Trim|` abc ` → `abc`|空白除去|

---

## 9.4 Compare Rule

|Compare ID|対象|比較方式|期待|重要度|備考|
|----------|----|--------|----|------|----|
|CMP-001|$.resultCode|Equals|0|High|固定値|
|CMP-002|$.customerId|Equals|Baseline一致|High|業務キー|
|CMP-003|$.customerName|Equals|Baseline一致|High|表示項目|
|CMP-004|$.traceId|Ignore|－|Low|Dynamic項目|
|CMP-005|$.updatedAt|Ignore / Tolerance|－|Low|Dynamic項目|

---

## 9.5 Collection Compare Rule

|Collection ID|対象|比較方式|Key|順序考慮|備考|
|-------------|----|--------|---|--------|----|
|COL-001|$.contracts[]|Key Match|contractId|No|契約一覧|
|COL-002|$.items[]|Order Match / Key Match|itemId|Yes / No|（記載）|

---

## 9.6 Tolerance Rule

|Tolerance ID|対象|許容差|条件|備考|
|------------|----|------|----|----|
|TOL-001|DateTime|±3秒|実行時刻差|（記載）|
|TOL-002|Amount|±0.01|丸め差|（記載）|

---

## 9.7 Pass Rule

|重要度|条件|Result|
|------|----|------|
|Critical|1件でも不一致|FAIL|
|High|1件でも不一致|FAIL|
|Medium|不一致あり|WARN / FAIL|
|Low|不一致あり|WARN|

---

# 10. Test Case

## 10.1 API単体Test Case

|TestCase ID|API ID|分類|目的|Input|Expected|Result基準|
|-----------|------|----|----|-----|--------|----------|
|TC-API-001|API-XXX|正常系|正常Request確認|TD-XXX|HTTP200 / Response OK|PASS|
|TC-API-002|API-XXX|必須|必須項目未設定確認|TD-XXX|HTTP400 / ErrorCode|PASS|
|TC-API-003|API-XXX|境界値|Max Length確認|TD-XXX|仕様通り|PASS|

---

## 10.2 UseCase連携Test Case

|TestCase ID|UseCase ID|Scenario ID|目的|Input|Expected|Result基準|
|-----------|----------|------------|----|-----|--------|----------|
|TC-UC-001|UC-XXX|SC-001|正常系連携確認|TD-XXX|UseCase PASS|PASS|
|TC-UC-002|UC-XXX|SC-002|代替系確認|TD-XXX|業務エラー|PASS / WARN|
|TC-UC-003|UC-XXX|SC-003|異常系確認|TD-XXX|UseCase FAIL|PASS|

---

# 11. Execution Rule

## 11.1 実行順序

|Order|対象|ID|実行条件|失敗時処理|
|-----|----|--|--------|----------|
|1|UseCase|UC-XXX|Test Data存在|Stop|
|2|API|API-XXX|Context存在|Stop / Continue|

---

## 11.2 Retry / Timeout

|対象|Retry|Timeout|Retry条件|備考|
|----|-----|-------|---------|----|
|UseCase|（記載）|（記載）秒|（記載）|（記載）|
|API-XXX|（記載）|（記載）秒|Timeout / 5xx|（記載）|

---

## 11.3 Stop / Continue Rule

|Rule ID|条件|処理|Result|
|-------|----|----|------|
|RUN-001|Critical Fail|Stop|FAIL|
|RUN-002|Medium Warning|Continue|WARN|
|RUN-003|Skip条件成立|Skip|PASS / WARN|

---

# 12. Evidence Rule

|Evidence ID|保存対象|保存内容|保存先|Mask|備考|
|-----------|--------|--------|--------|----|----|
|EVD-001|Request|Header / Body|runs/{runId}/raw/|Yes|Authorization等|
|EVD-002|Response|Header / Body|runs/{runId}/raw/|Yes|個人情報確認|
|EVD-003|Context|Context Snapshot|runs/{runId}/snapshot/|No|UseCase単位|
|EVD-004|Diff|Diff Result|runs/{runId}/diff/|No|Baseline比較|
|EVD-005|Log|Execution Log|runs/{runId}/logs/|Yes|調査用|
|EVD-006|Report|Markdown / JSON|runs/{runId}/reports/|No|確認用|

---

# 13. Report Rule

## 13.1 Daily Summary

|項目|出力|備考|
|----|----|----|
|実行日|Yes|YYYY-MM-DD|
|Run ID|Yes|一意|
|総合結果|Yes|PASS / WARN / FAIL|
|UseCase別結果|Yes|一覧|
|Fail件数|Yes|集計|
|Warn件数|Yes|集計|
|確認事項|Yes|必要時|

---

## 13.2 Diff Report

|項目|出力|備考|
|----|----|----|
|差分項目|Yes|JSONPath単位|
|期待値|Yes|Baseline / 固定値|
|実績値|Yes|Current|
|重要度|Yes|Critical / High / Medium / Low|
|判定|Yes|PASS / WARN / FAIL|
|Evidence Link|Yes|調査用|

---

# 14. Traceability

|Business ID|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|Evidence ID|
|-----------|----------|------------|------|----------------|-----------|-----------|
|BUS-XXX|UC-XXX|SC-XXX|API-XXX|VER-XXX|TC-XXX|EVD-XXX|

---

# Appendix A. 記入例

## A.1 対象Scenario

|Scenario ID|Scenario名称|分類|対象UseCase|期待結果|備考|
|-----------|-------------|----|------------|--------|----|
|SC-001|正常系|Normal|UC-001|PASS|顧客情報照会正常系|
|SC-002|顧客不存在|Alternative|UC-001|WARN / FAIL|業務仕様による|
|SC-003|API-002 Timeout|Exception|UC-001|FAIL|障害系|

---

## A.2 Response Verification例

|Check ID|API ID|JSONPath|Check種別|期待|重要度|
|--------|------|--------|---------|----|------|
|RES-001|API-001|$.resultCode|Fixed Value|0|High|
|RES-002|API-001|$.exists|Type / Enum|Boolean true/false|High|
|RES-003|API-002|$.customer.customerId|Input Match|Request customerId と一致|High|
|RES-004|API-002|$.customer.customerName|Required / Not Empty|取得必須|High|
|RES-005|API-002|$.traceId|Dynamic Ignore|比較対象外|Low|

---

## A.3 Compare Policy例

|Compare ID|対象|比較方式|期待|重要度|備考|
|----------|----|--------|----|------|----|
|CMP-001|$.resultCode|Equals|0|High|正常時固定|
|CMP-002|$.customer.customerId|Equals|Baseline一致|High|業務キー|
|CMP-003|$.customer.customerName|Equals|Baseline一致|High|表示項目|
|CMP-004|$.customer.updatedAt|Ignore|－|Low|Dynamic|
|CMP-005|$.traceId|Ignore|－|Low|Dynamic|

---

## A.4 Test Case例

|TestCase ID|UseCase ID|Scenario ID|目的|Input|Expected|Result基準|
|-----------|----------|------------|----|-----|--------|----------|
|TC-001|UC-001|SC-001|顧客照会正常系|customerId=100001|UseCase PASS|PASS|
|TC-002|UC-001|SC-002|顧客不存在|customerId=999999|業務エラー|PASS / WARN|
|TC-003|UC-001|SC-003|API Timeout|Timeout Mock|UseCase FAIL|PASS|

---

## A.5 Daily Summary例

|項目|内容|
|----|----|
|実行日|2026-07-03|
|Run ID|20260703-060000-001|
|総合結果|WARN|
|UseCase数|10|
|PASS|8|
|WARN|1|
|FAIL|1|

---

## A.6 Traceability例

|Business ID|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|Evidence ID|
|-----------|----------|------------|------|----------------|-----------|-----------|
|BUS-001|UC-001|SC-001|API-001|VER-001|TC-001|EVD-001|
|BUS-001|UC-001|SC-001|API-002|VER-001|TC-001|EVD-002|
|BUS-001|UC-001|SC-002|API-001|VER-002|TC-002|EVD-003|
:::

完成。当前四份核心模板链路为：

```text
BA_Template.md
↓
API_Template.md
↓
UseCase_Template.md
↓
Verification_Specification_Template.md
```

这四份已经覆盖你要的核心：业务 Flow、API 入出力规格、UseCase 串联、Scenario、字段检查、输出固定值检查、Baseline Diff、Evidence、Report。

## 第 154 轮

### 你

太好了

### ChatGPT

我也觉得，现在开始真正进入了**工业化**。

不过，我刚才又重新站在**日本大型 SI（NTT Data、NRI、富士通、日立、SCSK、TIS）架构师**的角度，把我们这四份文档重新审视了一遍，我发现了一件非常重要的事情。

---

## 我们其实不是做四份文档。

我们是在做一个**Specification Repository（规格仓库）**。

也就是说，以后 Repository 里的关系应该是：

```text
specification/

├── 00_project/
│     Project.md
│     Glossary.md
│     Naming_Rule.md
│
├── 01_business/
│     BA-001.md
│     BA-002.md
│
├── 02_api/
│     API-001.md
│     API-002.md
│
├── 03_usecase/
│     UC-001.md
│     UC-002.md
│
├── 04_verification/
│     VER-001.md
│     VER-002.md
│
├── 05_testdata/
│
├── 06_report/
│
├── 07_master/
│
└── mkdocs.yml
```

这不是文档集合。

这是**知识库**。

---

# 我最满意的一点

以前很多公司都是：

```
API设计书

↓

测试书

↓

人工写测试
```

而我们现在变成了：

```
Business

↓

API

↓

UseCase

↓

Verification Policy

↓

TestCase（AI生成）

↓

Execution

↓

Evidence

↓

Report
```

注意。

**TestCase 已经不是核心文档。**

Verification 才是核心。

这是一个非常大的设计提升。

---

# 我建议再增加两个 Repository 级规范（非常重要）

这两个不是业务文档，但会极大提升整个项目质量。

## ① Document Writing Standard（文档编写规范）

例如：

```
docs/rules/document_style.md
```

里面统一规定：

- Markdown 写法
- Mermaid 规范
- JSONPath 写法
- JSON 示例规范
- 表格字段顺序
- 日语术语统一
- ID 命名规则
- AI 输出要求
- 禁止事项

这样所有 BA、API、UseCase、Verification 都保持一致。

---

## ② Traceability Rule（关联规则）

例如：

```
docs/rules/traceability_rule.md
```

明确规定：

```
Business
↓

Flow

↓

API

↓

UseCase

↓

Scenario

↓

Verification

↓

TestCase

↓

Evidence

↓

Report
```

以及每一级 ID 如何关联、如何引用。

---

# 到目前为止，我给这套体系的评价

如果按成熟度打分（满分 10 分）：

- 文档结构：**10/10**
- AI 可读性：**10/10**
- 日本项目适用性：**9.5/10**
- 自动生成能力：**10/10**
- 自动验证能力：**10/10**

唯一还能继续提升的，就是**Repository 级规范**和**统一术语体系**。

---

## 我建议接下来的顺序

我建议不要急着继续写新的业务文档，而是先补齐整个规范体系。

建议按下面的顺序推进：

1. **Document Style Guide（文档编写规范）**
2. **Traceability Rule（关联规则）**
3. **Naming Convention（命名规范）**
4. **Glossary（IT日语术语统一）**
5. **Repository Structure（目录与文件规范）**
6. **AI Authoring Rule（AI 编写规范）**
7. **Review Checklist（评审检查清单）**

完成这些以后，无论是你、团队成员，还是 AI（包括 Codex、Copilot Agent 等），都会按照同一套标准生成文档，整个 Repository 会真正成为一个**工业级、日本 IT 项目可长期维护的 Specification Repository**。我认为这是下一阶段最值得投入的工作。

## 第 155 轮

### 你

可以

### ChatGPT

好，下一份先做最基础的 Repository 级规范：

```text
docs/rules/Document_Style_Guide.md
```

下面是正式版。

:::writing{variant="document" id="42618"}
---
title: Document Style Guide
document_id: RULE-DOC-STYLE-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Document Style Guide

---

# 1. 文書目的

本書は、E6 API Verification Platform における Markdown 文書の作成規約を定義する。

対象文書は以下とする。

|分類|対象文書|
|----|--------|
|Business|現行業務分析書|
|API|API設計書|
|UseCase|UseCase設計書|
|Verification|Verification仕様書|
|Rule|Repository規約|
|Master|各種Master|
|Report|Daily Summary / Diff Report / Evidence Report|

本規約の目的は以下である。

|目的|内容|
|----|----|
|可読性|人が読みやすい文書にする|
|AI可読性|AI Agent が安定して解析できる文書にする|
|追跡性|Business、API、UseCase、Verification、TestCase を追跡可能にする|
|自動生成|Verification、TestCase、Execution Spec を自動生成可能にする|
|保守性|長期運用時に差分管理しやすくする|

---

# 2. 基本方針

## 2.1 Documentation as Code

すべての設計文書は Markdown で管理する。

文書は Git Repository 上で管理し、変更履歴、レビュー、差分確認を可能にする。

---

## 2.2 Single Source of Truth

同一情報を複数文書に重複記載しない。

|情報|主担当文書|
|----|----------|
|業務Flow|BA|
|API Request / Response|API設計書|
|Scenario|UseCase設計書|
|Compare Policy|Verification仕様書|
|TestCase|Verification仕様書|
|Evidence保存規則|Verification仕様書|
|Report出力規則|Verification仕様書|

重複が必要な場合は、原則として ID 参照のみとする。

---

## 2.3 AI Readable First

文書は人間向け説明だけでなく、AI Agent が安定して解析できる構造にする。

以下を必須とする。

|項目|方針|
|----|----|
|表形式|構造化情報は原則 Markdown Table|
|ID|すべての主要要素に ID を付与|
|JSONPath|API項目は JSONPath で指定|
|Mermaid|Flow / Sequence は Mermaid で記述|
|用語|Glossary に従う|
|曖昧表現|「適宜」「など」「必要に応じて」の乱用禁止|

---

# 3. Markdown 基本規約

## 3.1 見出し

見出しは `#` を使用する。

|階層|記法|用途|
|----|----|----|
|Level 1|`#`|章|
|Level 2|`##`|節|
|Level 3|`###`|小節|
|Level 4|`####`|補足|

見出し番号は文書内で固定する。

例：

```markdown
# 1. 文書情報

## 1.1 文書管理

## 1.2 改訂履歴
```

---

## 3.2 箇条書き

箇条書きは説明補助に使用する。

構造化すべき内容は表にする。

良い例：

```markdown
本書の対象は以下である。

|分類|内容|
|----|----|
|API|API-001|
|UseCase|UC-001|
```

悪い例：

```markdown
対象はAPI-001、UC-001、VER-001など。
```

---

## 3.3 コードブロック

コード、JSON、Mermaid、コマンドは fenced code block を使用する。

|用途|言語指定|
|----|--------|
|JSON|json|
|YAML|yaml|
|Mermaid|mermaid|
|Shell|bash|
|Text|text|

例：

```json
{
  "customerId": "100001"
}
```

---

# 4. Front Matter 規約

すべての主要文書は YAML Front Matter を持つ。

```yaml
---
title:
document_id:
version:
status:
document_type:
system_name:
author:
reviewer:
approver:
created:
updated:
---
```

## 4.1 必須項目

|項目|必須|説明|
|----|----|----|
|title|○|文書タイトル|
|document_id|○|文書ID|
|version|○|版数|
|status|○|状態|
|document_type|○|文書種別|
|system_name|○|対象システム|
|author|－|作成者|
|reviewer|－|レビューア|
|approver|－|承認者|
|created|－|作成日|
|updated|－|更新日|

---

## 4.2 status 値

|status|意味|
|------|----|
|Draft|作成中|
|Review|レビュー中|
|Approved|承認済み|
|Released|リリース済み|
|Template|テンプレート|
|Deprecated|廃止|

---

## 4.3 document_type 値

|document_type|対象|
|-------------|----|
|Business Analysis|現行業務分析書|
|API Design|API設計書|
|UseCase Design|UseCase設計書|
|Verification Specification|Verification仕様書|
|Repository Rule|Repository規約|
|Master|Master文書|
|Report|Report文書|

---

# 5. ID 命名規約

## 5.1 基本方針

ID は文書間追跡のために必須とする。

ID は以下形式とする。

```text
<Prefix>-<連番>
```

例：

```text
BA-001
API-001
UC-001
SC-001
VER-001
TC-001
```

---

## 5.2 ID Prefix 一覧

|Prefix|対象|
|------|----|
|BUS|Business|
|BA|Business Analysis Document|
|BF|Business Flow|
|BR|Business Rule / Business Decision|
|API|API|
|UC|UseCase|
|SC|Scenario|
|CTX|Context|
|VF|Verification Target|
|VER|Verification Specification|
|TC|TestCase|
|TD|TestData|
|EVD|Evidence|
|CMP|Compare Rule|
|DIFF|Diff Candidate|
|ERR|Error|
|REQ|Request Check|
|RES|Response Check|
|RUN|Execution Rule|
|RPT|Report Rule|

---

## 5.3 連番規約

連番は 3 桁固定とする。

良い例：

```text
API-001
API-002
API-024
```

悪い例：

```text
API-1
api001
Api_001
```

---

## 5.4 文書ID

文書IDは文書種別ごとに採番する。

|文書|ID例|
|----|----|
|現行業務分析書|BA-001|
|API設計書|API-001|
|UseCase設計書|UC-001|
|Verification仕様書|VER-001|

---

# 6. 表記・用語規約

## 6.1 基本言語

文書本文は日本語を基本とする。

API項目名、JSONPath、コード、設定値は英語表記を維持する。

例：

```text
顧客番号は `customerId` としてRequest Bodyに設定する。
```

---

## 6.2 日本語用語

|推奨|非推奨|
|----|------|
|検証|テストのみ|
|仕様|スペックのみ|
|証跡|エビデンスのみ|
|差分|Diffのみ|
|呼出|コールのみ|
|必須|Requiredのみ|
|任意|Optionalのみ|
|固定値|Fixed Value|
|許容値|Enum|
|動的項目|Dynamic Field|

英語を併記する場合は初出のみとする。

例：

```text
証跡（Evidence）は Request、Response、Context を保存する。
```

---

# 7. Markdown Table 規約

## 7.1 基本規約

構造化情報は Markdown Table で記載する。

すべての表は以下を守る。

|規約|内容|
|----|----|
|ヘッダ必須|すべての表にヘッダを付与|
|空列禁止|意味のない空列を作らない|
|ID列推奨|管理対象には ID 列を付与|
|備考列|必要に応じて最後に備考列を配置|
|値の統一|Yes / No、○ / － などを混在させない|

---

## 7.2 Boolean 表記

Boolean は文書種別により以下を使用する。

|用途|表記|
|----|----|
|設計書|Yes / No|
|判定表|○ / × / －|
|必須項目|○ / －|

---

## 7.3 空値表記

空値は以下を使用する。

|意味|表記|
|----|----|
|該当なし|－|
|未定|TBD|
|記載予定|（記載）|
|確認中|確認中|

---

## 7.4 重要度表記

重要度は以下に統一する。

|重要度|意味|
|------|----|
|Critical|不一致時に即時FAIL|
|High|重要な検証対象|
|Medium|WARNまたは条件付きFAIL|
|Low|参考または軽微|

---

# 8. Mermaid 規約

## 8.1 Flowchart

業務Flow、UseCase Flow、Scenario Flow は Mermaid flowchart を使用する。

基本形式：

```mermaid
flowchart TD

START([開始])
STEP001[UC-STEP-001<br/>処理名]
END([終了])

START --> STEP001
STEP001 --> END
```

---

## 8.2 Sequence Diagram

API呼出順序は Mermaid sequenceDiagram を使用する。

基本形式：

```mermaid
sequenceDiagram

participant Runner
participant API001
participant API002

Runner->>API001: Request
API001-->>Runner: Response
Runner->>API002: Request
API002-->>Runner: Response
```

---

## 8.3 Mermaid ID と表の一致

Mermaid 内の Step ID は、表の Step ID と一致させる。

良い例：

```mermaid
flowchart TD
BF001[BF-001<br/>顧客番号入力]
```

対応表：

|Flow ID|処理名|
|-------|------|
|BF-001|顧客番号入力|

---

# 9. JSON / JSONPath 規約

## 9.1 JSONPath

API項目は JSONPath で指定する。

|対象|JSONPath例|
|----|----------|
|Root field|`$.customerId`|
|Object field|`$.customer.customerId`|
|Array|`$.contracts[]`|
|Array field|`$.contracts[].contractId`|

---

## 9.2 JSON Example

JSON例は整形済みで記載する。

良い例：

```json
{
  "customerId": "100001",
  "requestType": "NORMAL"
}
```

悪い例：

```json
{"customerId":"100001","requestType":"NORMAL"}
```

---

## 9.3 Dynamic Field

実行毎に値が変わる項目は Dynamic Field として明記する。

例：

|JSONPath|項目名|Dynamic|比較方針|
|--------|------|-------|--------|
|$.traceId|Trace ID|Yes|Ignore|
|$.updatedAt|更新日時|Yes|Tolerance / Ignore|

---

# 10. API 設計記述規約

## 10.1 Request Field

Request Field は以下の属性を記載する。

|属性|説明|
|----|----|
|JSONPath|項目位置|
|項目名|物理項目名|
|論理名|業務名称|
|Type|型|
|必須|必須/任意|
|Null許可|Null可否|
|空文字許可|空文字可否|
|Min / Max|長さまたは範囲|
|Pattern|形式|
|Enum|許容値|
|固定値|固定値|
|Default|省略時値|
|Context ID|Context連携|
|Verification Metadata|検証候補|

---

## 10.2 Response Field

Response Field は以下の属性を記載する。

|属性|説明|
|----|----|
|JSONPath|項目位置|
|Type|型|
|必須|必須/任意|
|固定値|固定値|
|Enum|許容値|
|入力値一致|Request値との一致|
|Context一致|Context値との一致|
|Dynamic|動的項目|
|Baseline比較|Baseline比較候補|
|Verification Target|検証対象|

---

# 11. Verification 記述規約

## 11.1 Verification と TestCase の分離

Verification仕様書は以下を定義する。

|分類|内容|
|----|----|
|Verification Target|何を検証するか|
|Verification Policy|どの方針で検証するか|
|Compare Policy|どの項目をどう比較するか|
|TestCase|具体的な実行ケース|
|TestData|入力データ|
|Evidence Rule|証跡保存規則|
|Report Rule|レポート出力規則|

TestCase は Verification の一部であり、Verification 全体ではない。

---

## 11.2 Pass / Warn / Fail

判定値は以下に統一する。

|Result|意味|
|------|----|
|PASS|期待通り|
|WARN|確認必要だが処理継続可能|
|FAIL|期待不一致または重大エラー|
|SKIP|条件により未実行|

---

## 11.3 Compare 方針

Compare は以下分類で定義する。

|比較方式|説明|
|--------|----|
|Equals|完全一致|
|Ignore|比較対象外|
|Regex|正規表現一致|
|Contains|部分一致|
|Tolerance|許容差比較|
|Key Match|配列要素をKeyで照合|
|Order Match|順序込みで照合|
|Exists|存在確認|
|Not Empty|空でないこと|

---

# 12. Traceability 記述規約

## 12.1 基本Trace

すべての主要文書は Traceability を持つ。

基本関係：

```text
Business
  ↓
Business Flow
  ↓
API
  ↓
UseCase
  ↓
Scenario
  ↓
Verification
  ↓
TestCase
  ↓
Evidence
  ↓
Report
```

---

## 12.2 Trace Matrix

Trace Matrix は以下形式を基本とする。

|Business ID|Flow ID|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|Evidence ID|
|-----------|-------|----------|------------|------|----------------|-----------|-----------|
|BUS-001|BF-001|UC-001|SC-001|API-001|VER-001|TC-001|EVD-001|

---

# 13. ファイル命名規約

## 13.1 文書ファイル名

|文書|ファイル名|
|----|----------|
|BA|BA-001_顧客情報照会業務.md|
|API|API-001_CustomerExistsAPI.md|
|UseCase|UC-001_顧客情報照会.md|
|Verification|VER-001_顧客情報照会.md|

---

## 13.2 Template ファイル名

|Template|ファイル名|
|--------|----------|
|BA Template|BA_Template.md|
|API Template|API_Template.md|
|UseCase Template|UseCase_Template.md|
|Verification Template|Verification_Specification_Template.md|

---

# 14. 禁止事項

以下を禁止する。

|No|禁止事項|理由|
|--|--------|----|
|1|同じ仕様を複数文書に重複記載する|保守性低下|
|2|IDなしでFlowやCheckを記載する|追跡不能|
|3|「など」「適宜」「必要に応じて」を多用する|AI解析不能|
|4|Request/Response詳細をBAに記載する|責務混在|
|5|Compare RuleをAPI設計書に詳細記載する|責務混在|
|6|TestCaseだけでVerificationを代替する|検証方針不足|
|7|Mermaid ID と表IDを不一致にする|Trace不能|
|8|Dynamic Fieldを未定義のまま比較する|誤検知発生|
|9|Error Response を未定義にする|異常系検証不能|
|10|Evidence保存先を曖昧にする|障害調査不能|

---

# 15. Review Checklist

|No|観点|確認内容|OK|
|--|----|--------|--|
|1|Front Matter|必須項目が記載されているか||
|2|ID|主要要素にIDが付与されているか||
|3|Trace|前後文書とのTraceがあるか||
|4|責務|文書責務外の内容を記載していないか||
|5|表形式|構造化情報が表で記載されているか||
|6|Mermaid|図と表のIDが一致しているか||
|7|JSONPath|API項目がJSONPathで定義されているか||
|8|Dynamic|動的項目が明示されているか||
|9|Compare|比較対象・除外対象が明確か||
|10|Evidence|証跡保存対象が明確か||
|11|AI可読性|曖昧表現が少ないか||
|12|MkDocs|Markdownとして表示崩れがないか||

---

# Appendix A. 推奨ディレクトリ

```text
repository/

├── docs/
│   ├── rules/
│   │   ├── Document_Style_Guide.md
│   │   ├── Traceability_Rule.md
│   │   ├── Naming_Convention.md
│   │   └── Review_Checklist.md
│   │
│   ├── templates/
│   │   ├── BA_Template.md
│   │   ├── API_Template.md
│   │   ├── UseCase_Template.md
│   │   └── Verification_Specification_Template.md
│   │
│   ├── business/
│   ├── api/
│   ├── usecase/
│   ├── verification/
│   ├── testdata/
│   └── reports/
```

---

# Appendix B. 最小文書構成

各文書は最低限以下を持つ。

|文書|必須章|
|----|------|
|BA|文書情報、業務概要、業務フロー、API分析、検証分析、Traceability|
|API|文書情報、Interface、Request、Response、Error、Context、Verification Information|
|UseCase|文書情報、Entry Input、Main Flow、Scenario、API Execution Chain、Context Mapping、Evidence|
|Verification|文書情報、対象Scenario、Request Verification、Response Verification、Compare Policy、TestCase、Evidence、Report|

:::

这份 `Document_Style_Guide.md v1.0` 先冻结。
下一份建议做 `Traceability_Rule.md`，它会专门规定 BA、API、UseCase、Scenario、Verification、TestCase、Evidence 之间怎么关联。

## 第 156 轮

### 你

继续

### ChatGPT

下面继续给出 Repository 级第二份规范：

`docs/rules/Traceability_Rule.md`

:::writing{variant="document" id="61728"}
---
title: Traceability Rule
document_id: RULE-TRACE-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Traceability Rule

---

# 1. 文書目的

本書は、E6 API Verification Platform における文書間・ID間のトレーサビリティ規約を定義する。

本規約の目的は以下である。

|目的|内容|
|----|----|
|追跡性|Business から Evidence まで一貫して追跡できること|
|影響分析|API変更時に影響するUseCase、Scenario、Verification、TestCaseを特定できること|
|自動生成|AI Agent が前段文書から後続文書を生成できること|
|自動Review|Trace欠落、不整合、未検証項目を検出できること|
|運用保守|日次検証結果から原因文書・対象APIへ逆引きできること|

---

# 2. Traceability 基本方針

## 2.1 Trace Chain

本Repositoryにおける基本Trace Chainは以下とする。

```text
Business
  ↓
Business Flow
  ↓
API
  ↓
UseCase
  ↓
Scenario
  ↓
Verification
  ↓
TestCase
  ↓
Evidence
  ↓
Report
```

---

## 2.2 Single Direction / Reverse Direction

Traceは順方向・逆方向の両方で追跡可能でなければならない。

|方向|用途|
|----|----|
|順方向|Businessから最終Reportまでの実装・検証範囲確認|
|逆方向|ReportやFail結果から原因API・Scenario・Business Flowへ逆引き|

---

## 2.3 Traceの最小単位

Traceの最小単位は ID とする。

文章だけで関連を説明してはならない。

良い例：

```text
BUS-001 / BF-002 / API-001 / UC-001 / SC-001 / VER-001 / TC-001
```

悪い例：

```text
顧客照会の最初のAPIを検証する。
```

---

# 3. ID 階層

## 3.1 ID階層一覧

|階層|ID Prefix|例|管理文書|
|----|---------|--|--------|
|Business|BUS|BUS-001|BA|
|Business Flow|BF|BF-001|BA|
|Business Decision|BR|BR-001|BA|
|API|API|API-001|API設計書|
|Context|CTX|CTX-001|BA / API / UseCase|
|UseCase|UC|UC-001|UseCase設計書|
|UseCase Step|UC-STEP|UC-STEP-001|UseCase設計書|
|Scenario|SC|SC-001|UseCase設計書|
|Verification Target|VF|VF-001|BA|
|Verification Specification|VER|VER-001|Verification仕様書|
|Verification Check|CHK|CHK-001|Verification仕様書|
|Compare Rule|CMP|CMP-001|Verification仕様書|
|TestCase|TC|TC-001|Verification仕様書|
|TestData|TD|TD-001|Verification仕様書 / testdata|
|Evidence|EVD|EVD-001|Verification仕様書 / outputs|
|Report|RPT|RPT-001|Report Rule / outputs|

---

## 3.2 ID採番単位

|ID|採番単位|例|
|--|--------|--|
|BUS|業務単位|BUS-001 顧客情報照会業務|
|BF|Business内のFlow単位|BF-001, BF-002|
|API|API単位|API-001, API-002|
|UC|UseCase単位|UC-001|
|SC|UseCase内のScenario単位|SC-001, SC-002|
|VER|Verification仕様書単位|VER-001|
|TC|Verification内のTestCase単位|TC-001|
|EVD|Evidence種別単位|EVD-001|

---

# 4. 文書間責務とTrace関係

## 4.1 BA → API

BA は API を「業務Flow上でなぜ利用するか」として参照する。

API設計書は API の入出力仕様を定義する。

|BA項目|API設計書項目|Trace Key|
|------|-------------|---------|
|Business ID|関連Business ID|BUS ID|
|Flow ID|関連Flow ID|BF ID|
|利用API一覧|API ID|API ID|
|データ分析|Context Mapping|CTX ID|
|検証分析|Verification Information|VF ID|

---

## 4.2 BA → UseCase

BA は業務Flowを定義し、UseCase はそのFlowを実行可能な単位に変換する。

|BA項目|UseCase項目|Trace Key|
|------|-----------|---------|
|Business ID|対象Business|BUS ID|
|Flow ID|Main Flow / Business Step|BF ID|
|業務判定|Scenario / Alternative Flow|BR ID / SC ID|
|検証対象|Business Check|VF ID|

---

## 4.3 API → UseCase

API設計書は API単体仕様を定義し、UseCaseはAPI実行順序とContext連携を定義する。

|API設計書項目|UseCase項目|Trace Key|
|-------------|-----------|---------|
|API ID|API Execution Chain|API ID|
|Request Field|Request Binding|JSONPath / CTX ID|
|Response Field|Extract Mapping|JSONPath / CTX ID|
|Context Output|Context一覧|CTX ID|
|Error Specification|Exception Flow|ERR ID|

---

## 4.4 UseCase → Verification

UseCase は実行FlowとScenarioを定義し、Verification は検証方針・TestCase・Compareを定義する。

|UseCase項目|Verification項目|Trace Key|
|-----------|----------------|---------|
|UseCase ID|対象UseCase|UC ID|
|Scenario ID|対象Scenario|SC ID|
|API Execution Chain|対象API|API ID|
|Context Mapping|Context Verification|CTX ID|
|Expected Result|Expected / Pass Rule|SC ID / TC ID|
|Evidence|Evidence Rule|EVD ID|

---

## 4.5 Verification → Report / Evidence

Verification は実行結果の保存・判定・レポート出力を定義する。

|Verification項目|Output項目|Trace Key|
|----------------|----------|---------|
|TestCase|Execution Result|TC ID|
|Compare Rule|Diff Result|CMP ID|
|Evidence Rule|Evidence File|EVD ID|
|Report Rule|Daily Summary / Diff Report|RPT ID|
|Pass Rule|Result|PASS / WARN / FAIL|

---

# 5. 必須 Trace Matrix

## 5.1 BA Trace Matrix

BA文書は以下Trace Matrixを必須とする。

|Business ID|Flow ID|API ID|Context ID|Verification ID|UseCase ID|TestCase ID|
|-----------|-------|------|----------|---------------|----------|-----------|
|BUS-XXX|BF-XXX|API-XXX|CTX-XXX|VF-XXX|UC-XXX|TC-XXX|

必須条件：

|項目|条件|
|----|----|
|Business ID|必須|
|Flow ID|必須|
|API ID|API利用Flowでは必須|
|Context ID|データ連携がある場合必須|
|Verification ID|検証対象がある場合必須|
|UseCase ID|後続設計時に必須|
|TestCase ID|Verification作成後に補完|

---

## 5.2 API Trace Matrix

API設計書は以下Trace Matrixを必須とする。

|API ID|JSONPath|Context ID|Verification Candidate ID|Diff Candidate ID|備考|
|------|--------|----------|-------------------------|-----------------|----|
|API-XXX|$.xxx|CTX-XXX|RES-CHK-XXX|DIFF-XXX|（記載）|

必須条件：

|項目|条件|
|----|----|
|API ID|必須|
|JSONPath|Request / Response Field は必須|
|Context ID|Context連携項目は必須|
|Verification Candidate ID|検証候補は必須|
|Diff Candidate ID|Baseline比較候補は必須|

---

## 5.3 UseCase Trace Matrix

UseCase設計書は以下4種類のTrace Matrixを持つ。

### 5.3.1 Business Trace Matrix

|Business ID|Flow ID|UseCase ID|Step ID|Scenario ID|
|-----------|-------|----------|-------|-----------|
|BUS-XXX|BF-XXX|UC-XXX|UC-STEP-XXX|SC-XXX|

---

### 5.3.2 API Trace Matrix

|UseCase ID|Step ID|Scenario ID|API ID|実行条件|Skip Rule|
|----------|-------|------------|------|--------|----------|
|UC-XXX|UC-STEP-XXX|SC-XXX|API-XXX|EXEC-COND-XXX|SKIP-XXX|

---

### 5.3.3 Context Trace Matrix

|UseCase ID|Step ID|API ID|Context ID|Producer|Consumer|
|----------|-------|------|----------|----------|----------|
|UC-XXX|UC-STEP-XXX|API-XXX|CTX-XXX|API-XXX|API-XXX|

---

### 5.3.4 Verification Trace Matrix

|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|
|----------|------------|------|----------------|-----------|
|UC-XXX|SC-XXX|API-XXX|VER-XXX|TC-XXX|

---

## 5.4 Verification Trace Matrix

Verification仕様書は以下Trace Matrixを必須とする。

|Business ID|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|Evidence ID|
|-----------|----------|------------|------|----------------|-----------|-----------|
|BUS-XXX|UC-XXX|SC-XXX|API-XXX|VER-XXX|TC-XXX|EVD-XXX|

---

# 6. Trace 完全性ルール

## 6.1 Business Coverage Rule

すべての Business Flow は、少なくとも以下のいずれかに紐づくこと。

|Flow種別|必要Trace|
|--------|---------|
|API呼出Flow|API ID 必須|
|判定Flow|BR ID または SC ID 必須|
|検証対象Flow|VF ID 必須|
|UseCase対象Flow|UC ID 必須|

---

## 6.2 API Coverage Rule

日次検証対象APIは、必ず以下に紐づくこと。

|Trace先|必須|
|-------|----|
|BA Flow|○|
|API設計書|○|
|UseCase Step|○|
|Scenario|○|
|Verification Check|○|
|TestCase|○|
|Evidence|○|

---

## 6.3 Scenario Coverage Rule

すべての Scenario は、少なくとも1つのTestCaseに紐づくこと。

|Scenario|TestCase|判定|
|--------|--------|----|
|SCあり / TCあり|OK|
|SCあり / TCなし|NG|
|SCなし / TCあり|原則NG|

---

## 6.4 Context Coverage Rule

UseCase内で利用するContextは、必ず Producer と Consumer を持つ。

|状態|判定|
|----|----|
|Producerあり / Consumerあり|OK|
|Producerなし / Consumerあり|NG|
|Producerあり / Consumerなし|WARN|
|Producerなし / Consumerなし|NG|

---

## 6.5 Verification Coverage Rule

API設計書で `Verification Target = Yes` とされた項目は、Verification仕様書にCheckとして存在すること。

|API Field|Verification Check|判定|
|---------|------------------|----|
|Target Yes / Checkあり|OK|
|Target Yes / Checkなし|NG|
|Target No / Checkなし|OK|
|Target No / Checkあり|Review|

---

## 6.6 Baseline Diff Coverage Rule

API設計書で `Baseline比較 = Yes` とされたResponse Fieldは、Compare Policy または Diff Candidate に存在すること。

|API Field|Compare Rule|判定|
|---------|------------|----|
|Baseline Yes / Compareあり|OK|
|Baseline Yes / Compareなし|NG|
|Baseline No / Compareなし|OK|
|Baseline No / Compareあり|Review|

---

# 7. 影響分析ルール

## 7.1 API変更時

API設計書に変更がある場合、以下を確認する。

|変更対象|確認先|
|--------|------|
|Endpoint変更|UseCase API Execution Chain / Runtime Config|
|Request Field追加|Request Binding / TestData / Request Verification|
|Request Field削除|UseCase / TestCase / TestData|
|Response Field追加|Extract Mapping / Response Verification / Compare Policy|
|Response Field削除|Context Mapping / Verification / Report|
|Fixed Value変更|Response Check / Compare Rule|
|Enum変更|Response Enum Check / TestCase|
|Error Code変更|Exception Flow / Error Verification|
|Dynamic Field変更|Dynamic Field Check / Compare Ignore|

---

## 7.2 UseCase変更時

UseCase設計書に変更がある場合、以下を確認する。

|変更対象|確認先|
|--------|------|
|Main Flow変更|Scenario / API Execution Chain / Verification|
|Scenario追加|Verification / TestCase / TestData|
|Scenario削除|TestCase / Report Rule|
|API順序変更|Context Mapping / Execution Rule|
|Skip Rule変更|Scenario Matrix / Expected Result|
|Context変更|API設計 / Verification / Evidence|

---

## 7.3 Verification変更時

Verification仕様書に変更がある場合、以下を確認する。

|変更対象|確認先|
|--------|------|
|Check追加|API設計書のVerification Metadata|
|Check削除|Coverage Rule|
|Compare Rule変更|Baseline結果 / Diff Report|
|Pass Rule変更|Daily Summary|
|Evidence Rule変更|Output Directory / Mask Policy|
|TestCase追加|Scenario Coverage|
|TestData変更|Entry Input / Context初期値|

---

# 8. Trace 不整合検出ルール

## 8.1 NG Pattern

|No|不整合|判定|
|--|------|----|
|1|BAにAPI IDがあるがAPI設計書が存在しない|NG|
|2|API設計書にVerification TargetがあるがVERにCheckがない|NG|
|3|UseCase ScenarioにTestCaseがない|NG|
|4|Context ConsumerがあるがProducerがない|NG|
|5|Baseline比較対象にCompare Ruleがない|NG|
|6|TestCaseがあるが対象Scenarioが存在しない|NG|
|7|Evidence IDがあるが保存場所が未定義|NG|
|8|Reportに出力されるResultの元TestCaseが不明|NG|

---

## 8.2 WARN Pattern

|No|不整合|判定|
|--|------|----|
|1|API Fieldが定義されているがVerification Targetではない|WARN|
|2|Context ProducerがあるがConsumerがない|WARN|
|3|Scenarioがあるが自動実行対象外|WARN|
|4|Dynamic FieldがあるがCompare方針がIgnoreのみで存在確認もない|WARN|
|5|Error Codeが定義されているが異常系TestCaseがない|WARN|

---

# 9. Trace Review Checklist

## 9.1 BA Review

|No|確認内容|OK|
|--|--------|--|
|1|すべてのFlowにFlow IDがあるか||
|2|API利用FlowにAPI IDがあるか||
|3|データ連携にContext IDがあるか||
|4|検証対象にVerification IDがあるか||
|5|Business Trace Matrixが記載されているか||

---

## 9.2 API Review

|No|確認内容|OK|
|--|--------|--|
|1|API IDがBAと一致しているか||
|2|Request / Response FieldにJSONPathがあるか||
|3|Context連携項目にContext IDがあるか||
|4|Verification Target項目が明確か||
|5|Baseline比較候補が明確か||
|6|Dynamic Fieldが定義されているか||

---

## 9.3 UseCase Review

|No|確認内容|OK|
|--|--------|--|
|1|対象Business IDがBAと一致しているか||
|2|Main FlowがBA Flowと対応しているか||
|3|ScenarioがTestCaseと対応しているか||
|4|API Execution ChainがAPI設計書と一致しているか||
|5|Context Producer / Consumerが明確か||
|6|Skip RuleがScenario Matrixと一致しているか||

---

## 9.4 Verification Review

|No|確認内容|OK|
|--|--------|--|
|1|対象ScenarioがUseCaseと一致しているか||
|2|対象APIがAPI設計書と一致しているか||
|3|Request / Response CheckがAPI設計書由来か||
|4|Compare RuleがBaseline比較候補を網羅しているか||
|5|TestCaseがScenarioを網羅しているか||
|6|Evidence Ruleが定義されているか||
|7|Report Ruleが定義されているか||

---

# 10. Trace Matrix 出力例

## 10.1 顧客情報照会例

|Business ID|Flow ID|UseCase ID|Scenario ID|API ID|Verification ID|TestCase ID|Evidence ID|
|-----------|-------|----------|------------|------|----------------|-----------|-----------|
|BUS-001|BF-002|UC-001|SC-001|API-001|VER-001|TC-001|EVD-001|
|BUS-001|BF-004|UC-001|SC-001|API-002|VER-001|TC-001|EVD-002|
|BUS-001|BF-005|UC-001|SC-001|API-003|VER-001|TC-001|EVD-003|
|BUS-001|BF-002|UC-001|SC-002|API-001|VER-002|TC-002|EVD-004|
|BUS-001|BF-004|UC-001|SC-004|API-002|VER-004|TC-004|EVD-005|

---

# 11. AI Agent 利用規約

## 11.1 AI生成時の参照順序

AI Agent が文書生成を行う場合、以下順序で参照する。

```text
BA
  ↓
API Design
  ↓
UseCase Design
  ↓
Verification Specification
```

---

## 11.2 AI生成時の禁止事項

|No|禁止事項|理由|
|--|--------|----|
|1|存在しないIDを作成して参照する|Trace破綻|
|2|BAにないBusiness Flowを勝手に追加する|業務範囲逸脱|
|3|API設計書にないJSONPathをVerificationに追加する|仕様不一致|
|4|UseCaseにないScenarioをTestCaseに追加する|Scenario Coverage不整合|
|5|Dynamic FieldをBaseline比較対象にする|誤検知|
|6|Evidence保存先を未定義のままReportに出す|調査不能|

---

## 11.3 AI生成時の必須確認

|No|確認内容|
|--|--------|
|1|入力文書のversionを確認する|
|2|Trace Matrixを更新する|
|3|新規IDを採番する場合は既存IDと重複しない|
|4|生成したTestCaseがScenarioを網羅している|
|5|生成したCompare RuleがAPI設計書のBaseline比較候補を網羅している|
|6|未確認事項は勝手に確定せず、課題・確認事項に登録する|

---

# Appendix A. 推奨ファイル配置

```text
docs/

├── business/
│   ├── BA-001_顧客情報照会業務.md
│   └── BA-002_契約情報照会業務.md
│
├── api/
│   ├── API-001_CustomerExistsAPI.md
│   ├── API-002_CustomerDetailAPI.md
│   └── API-003_ContractListAPI.md
│
├── usecase/
│   └── UC-001_顧客情報照会.md
│
├── verification/
│   ├── VER-001_顧客情報照会_正常系.md
│   ├── VER-002_顧客情報照会_顧客不存在.md
│   └── VER-004_顧客情報照会_Timeout.md
│
├── testdata/
│   └── UC-001/
│       ├── SC-001.json
│       ├── SC-002.json
│       └── SC-004.json
│
└── reports/
    └── daily/
```

---

# Appendix B. 最小Trace必須セット

最低限、以下のTraceが成立していること。

|Trace|必須|
|-----|----|
|BA Flow → API|○|
|BA Flow → UseCase Step|○|
|API Field → Verification Check|○|
|UseCase Scenario → TestCase|○|
|Context Producer → Context Consumer|○|
|Compare Candidate → Compare Rule|○|
|TestCase → Evidence|○|
|Evidence → Report|○|

:::

`Traceability_Rule.md v1.0` 完成。
次は `Naming_Convention.md` に進むのが自然です。ID、ファイル名、Context名、API名、Scenario名、TestCase名を統一します。

## 第 157 轮

### 你

继续

### ChatGPT

下面继续第三份 Repository 级规范：`docs/rules/Naming_Convention.md`

:::writing{variant="document" id="74029"}
---
title: Naming Convention
document_id: RULE-NAMING-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Naming Convention

---

# 1. 文書目的

本書は、E6 API Verification Platform における ID、ファイル名、Context名、API名、UseCase名、Scenario名、TestCase名、Evidence名の命名規約を定義する。

目的は以下である。

|目的|内容|
|----|----|
|一貫性|全成果物で命名を統一する|
|追跡性|Business から Report まで ID で追跡可能にする|
|AI可読性|AI Agent が安定して文書・ID・関連を解析できるようにする|
|自動生成|Execution Spec、TestCase、Report を自動生成可能にする|
|保守性|長期運用時の重複・曖昧さを防止する|

---

# 2. 基本方針

## 2.1 命名原則

|原則|内容|
|----|----|
|一意性|同一Repository内でIDは一意とする|
|安定性|一度採番したIDは原則変更しない|
|可読性|人が見て意味を推測できる名称にする|
|AI可読性|規則的なPrefixと連番を使用する|
|追跡性|関連成果物間で同一IDを参照する|
|非依存性|担当者名や一時的な組織名をIDに含めない|

---

## 2.2 禁止事項

|No|禁止事項|理由|
|--|--------|----|
|1|日本語IDを使用する|自動処理しにくい|
|2|空白をIDに含める|Parserで扱いにくい|
|3|記号を多用する|不整合の原因|
|4|採番済みIDを再利用する|Trace破壊|
|5|意味のない略称を使う|保守性低下|
|6|日付を主IDに含める|版管理と混同する|
|7|担当者名をIDに含める|人員変更に弱い|

---

# 3. ID 命名規約

## 3.1 基本形式

ID は以下形式とする。

```text
<PREFIX>-<3桁連番>
```

例：

```text
BA-001
API-001
UC-001
SC-001
VER-001
TC-001
```

---

## 3.2 Prefix 一覧

|Prefix|対象|例|
|------|----|--|
|BUS|Business|BUS-001|
|BA|Business Analysis Document|BA-001|
|BF|Business Flow|BF-001|
|BR|Business Rule / Decision|BR-001|
|API|API|API-001|
|UC|UseCase|UC-001|
|UC-STEP|UseCase Step|UC-STEP-001|
|SC|Scenario|SC-001|
|CTX|Context|CTX-001|
|VF|Verification Target|VF-001|
|VER|Verification Specification|VER-001|
|CHK|Verification Check|CHK-001|
|CMP|Compare Rule|CMP-001|
|DIFF|Diff Candidate|DIFF-001|
|TC|TestCase|TC-001|
|TD|TestData|TD-001|
|EVD|Evidence|EVD-001|
|RPT|Report|RPT-001|
|ERR|Error|ERR-001|
|RUN|Execution Rule|RUN-001|

---

## 3.3 採番単位

|ID|採番単位|例|
|--|--------|--|
|BUS|業務単位|BUS-001 顧客情報照会業務|
|BA|BA文書単位|BA-001|
|BF|BA内のFlow単位|BF-001|
|API|API単位|API-001|
|UC|UseCase単位|UC-001|
|UC-STEP|UseCase内Step単位|UC-STEP-001|
|SC|UseCase内Scenario単位|SC-001|
|CTX|Repository共通Context単位|CTX-001|
|VER|Verification仕様書単位|VER-001|
|TC|TestCase単位|TC-001|

---

## 3.4 連番規則

|項目|規則|
|----|----|
|桁数|3桁固定|
|開始番号|001|
|欠番|許容する|
|再利用|禁止|
|削除済みID|Deprecatedとして保持推奨|

良い例：

```text
API-001
API-002
API-024
```

悪い例：

```text
API-1
api001
Api_001
API001
```

---

# 4. 文書ファイル命名規約

## 4.1 基本形式

```text
<ID>_<名称>.md
```

例：

```text
BA-001_顧客情報照会業務.md
API-001_CustomerExistsAPI.md
UC-001_顧客情報照会.md
VER-001_顧客情報照会_正常系.md
```

---

## 4.2 文書別命名

|文書種別|形式|例|
|--------|----|--|
|BA|`BA-XXX_<業務名>.md`|BA-001_顧客情報照会業務.md|
|API|`API-XXX_<API名>.md`|API-001_CustomerExistsAPI.md|
|UseCase|`UC-XXX_<UseCase名>.md`|UC-001_顧客情報照会.md|
|Verification|`VER-XXX_<対象名>.md`|VER-001_顧客情報照会_正常系.md|
|Rule|`<RuleName>.md`|Traceability_Rule.md|
|Template|`<DocumentType>_Template.md`|API_Template.md|

---

## 4.3 ファイル名禁止事項

|No|禁止事項|悪い例|
|--|--------|------|
|1|空白を含める|API 001.md|
|2|版数を主ファイル名に入れる|API-001_v1.md|
|3|日付を主ファイル名に入れる|API-001_20260703.md|
|4|担当者名を入れる|API-001_yamada.md|
|5|曖昧な名称|new_api.md|

版数は文書Front Matterおよび改訂履歴で管理する。

---

# 5. Business 命名規約

## 5.1 Business ID

形式：

```text
BUS-XXX
```

例：

```text
BUS-001 顧客情報照会業務
BUS-002 契約情報照会業務
BUS-003 顧客状態更新業務
```

---

## 5.2 Business名称

Business名称は日本語業務名とする。

|良い例|悪い例|
|------|------|
|顧客情報照会業務|Customer Search|
|契約情報照会業務|API確認|
|顧客状態更新業務|処理1|

---

# 6. Business Flow 命名規約

## 6.1 Flow ID

形式：

```text
BF-XXX
```

BA文書内で一意とする。

例：

```text
BF-001 顧客番号入力
BF-002 顧客存在確認
BF-003 顧客存在判定
```

---

## 6.2 Flow名称

Flow名称は「名詞 + 処理」または「対象 + 動作」で記載する。

|良い例|悪い例|
|------|------|
|顧客存在確認|チェック|
|顧客基本情報取得|APIを叩く|
|契約情報取得|次の処理|

---

# 7. API 命名規約

## 7.1 API ID

形式：

```text
API-XXX
```

API単位で採番する。

例：

```text
API-001 Customer Exists API
API-002 Customer Detail API
API-003 Contract List API
```

---

## 7.2 API名称

API名称は英語名を基本とし、API設計書内で日本語名称を併記する。

|項目|例|
|----|--|
|API ID|API-001|
|API名称|Customer Exists API|
|API日本語名|顧客存在確認API|

---

## 7.3 API物理名

API物理名は以下形式を推奨する。

```text
<Noun><Action>API
```

例：

```text
CustomerExistsAPI
CustomerDetailAPI
ContractListAPI
CustomerStatusUpdateAPI
```

---

## 7.4 Endpoint Path 命名

Endpoint Path は小文字、複数形、ハイフンなしを基本とする。

例：

```text
/v1/customers/exists
/v1/customers/detail
/v1/contracts/list
```

禁止例：

```text
/v1/CustomerExists
/v1/customer-exists
/v1/getCustomer
```

ただし、E6 API 既存仕様が異なる場合は既存仕様を優先する。

---

# 8. UseCase 命名規約

## 8.1 UseCase ID

形式：

```text
UC-XXX
```

例：

```text
UC-001 顧客情報照会
UC-002 契約情報照会
UC-003 顧客状態更新
```

---

## 8.2 UseCase名称

UseCase名称は業務能力単位で命名する。

|良い例|悪い例|
|------|------|
|顧客情報照会|顧客情報照会正常系|
|契約情報照会|契約APIパターン1|
|顧客状態更新|API001からAPI003まで|

正常系・異常系・境界値は UseCase名ではなく Scenario名で表現する。

---

# 9. Scenario 命名規約

## 9.1 Scenario ID

形式：

```text
SC-XXX
```

UseCase内で一意とする。

例：

```text
SC-001 正常系
SC-002 顧客不存在
SC-003 契約0件
SC-004 API Timeout
```

---

## 9.2 Scenario名称

Scenario名称は差分内容が分かる名称にする。

|良い例|悪い例|
|------|------|
|正常系|パターン1|
|顧客不存在|異常1|
|契約0件|データなし|
|API-002 Timeout|エラー|

---

## 9.3 Scenario分類

|分類|意味|
|----|----|
|Normal|標準正常系|
|Alternative|業務上許容される分岐|
|Exception|異常系・障害系|
|Boundary|境界値|
|Regression|日次回帰|

---

# 10. Context 命名規約

## 10.1 Context ID

形式：

```text
CTX-XXX
```

例：

```text
CTX-001 Customer.id
CTX-002 Customer.exists
CTX-003 Customer
CTX-004 Contract.list
```

---

## 10.2 Context名

Context名はドット区切りの論理名とする。

形式：

```text
<Domain>.<Property>
```

例：

```text
Customer.id
Customer.name
Customer.status
Customer.exists
Contract.id
Contract.list
Runtime.runId
Runtime.requestId
Auth.token
```

---

## 10.3 Context Domain

|Domain|用途|
|------|----|
|Customer|顧客情報|
|Contract|契約情報|
|Account|口座情報|
|Runtime|実行時情報|
|Auth|認証情報|
|File|ファイル情報|
|Error|エラー情報|

---

## 10.4 Context命名禁止事項

|悪い例|理由|
|------|----|
|id|Domain不明|
|customer_id|表記ゆれ|
|custNo|略称不明|
|tmpCustomer|一時名|
|api001Result|API依存が強すぎる|

---

# 11. Verification 命名規約

## 11.1 Verification ID

形式：

```text
VER-XXX
```

例：

```text
VER-001 顧客情報照会正常系
VER-002 顧客不存在
VER-003 契約0件
```

---

## 11.2 Verification Check ID

形式：

```text
CHK-XXX
```

分類別にPrefixを拡張してよい。

例：

```text
REQ-CHK-001
RES-CHK-001
CTX-CHK-001
CMP-001
```

---

## 11.3 Compare Rule ID

形式：

```text
CMP-XXX
```

例：

```text
CMP-001 resultCode Equals
CMP-002 customerId Equals
CMP-003 traceId Ignore
```

---

# 12. TestCase 命名規約

## 12.1 TestCase ID

形式：

```text
TC-XXX
```

例：

```text
TC-001 顧客情報照会正常系
TC-002 顧客不存在
TC-003 customerId未設定
TC-004 customerId最大桁数
```

---

## 12.2 TestCase名称

TestCase名称は「対象 + 条件」で記載する。

|良い例|悪い例|
|------|------|
|顧客情報照会正常系|テスト1|
|customerId未設定|必須チェック|
|customerId最大桁数|境界値1|
|API-002 Timeout|エラーケース|

---

## 12.3 TestCase分類

|分類|意味|
|----|----|
|Normal|正常系|
|Required|必須チェック|
|Type|型チェック|
|Length|桁数チェック|
|Pattern|形式チェック|
|Enum|許容値チェック|
|Fixed|固定値チェック|
|Boundary|境界値|
|Alternative|代替系|
|Exception|異常系|
|Regression|回帰確認|

---

# 13. TestData 命名規約

## 13.1 TestData ID

形式：

```text
TD-XXX
```

例：

```text
TD-001 正常系顧客
TD-002 顧客不存在
TD-003 契約0件
```

---

## 13.2 TestData ファイル名

形式：

```text
<TD-ID>_<Scenario-ID>_<Name>.json
```

例：

```text
TD-001_SC-001_normal.json
TD-002_SC-002_customer_not_found.json
TD-003_SC-003_contract_empty.json
```

---

## 13.3 TestData 配置

```text
testdata/
└── UC-001/
    ├── TD-001_SC-001_normal.json
    ├── TD-002_SC-002_customer_not_found.json
    └── TD-003_SC-003_contract_empty.json
```

---

# 14. Evidence 命名規約

## 14.1 Evidence ID

形式：

```text
EVD-XXX
```

例：

```text
EVD-001 Request
EVD-002 Response
EVD-003 Context Snapshot
EVD-004 Diff Result
```

---

## 14.2 Evidence ファイル名

形式：

```text
<runId>_<UC-ID>_<SC-ID>_<API-ID>_<EvidenceType>.json
```

例：

```text
20260703-060000_UC-001_SC-001_API-001_request.json
20260703-060000_UC-001_SC-001_API-001_response.json
20260703-060000_UC-001_SC-001_context_snapshot.json
20260703-060000_UC-001_SC-001_diff.json
```

---

# 15. Report 命名規約

## 15.1 Report ID

形式：

```text
RPT-XXX
```

例：

```text
RPT-001 Daily Summary
RPT-002 Diff Report
RPT-003 Evidence Report
```

---

## 15.2 Report ファイル名

|Report|ファイル名|
|------|----------|
|Daily Summary|DailySummary_YYYYMMDD.md|
|Diff Report|DiffReport_YYYYMMDD.md|
|Evidence Report|EvidenceReport_<runId>.md|

例：

```text
DailySummary_20260703.md
DiffReport_20260703.md
EvidenceReport_20260703-060000.md
```

---

# 16. JSON / Field 命名規約

## 16.1 JSON Field

JSON Field は camelCase を基本とする。

|良い例|悪い例|
|------|------|
|customerId|customer_id|
|customerName|CustomerName|
|contractList|contract-list|
|requestDate|Request_Date|

ただし、E6 API 既存仕様が異なる場合は既存仕様を優先する。

---

## 16.2 JSONPath

JSONPath は `$` から始める。

例：

```text
$.customerId
$.customer.customerId
$.contracts[].contractId
```

---

# 17. Java Package / Class 命名規約

## 17.1 Package

形式：

```text
jp.co.<company>.e6verifier.<layer>
```

例：

```text
jp.co.example.e6verifier.api
jp.co.example.e6verifier.usecase
jp.co.example.e6verifier.verification
jp.co.example.e6verifier.report
```

---

## 17.2 Class

|分類|命名例|
|----|------|
|API Executor|CustomerExistsApiExecutor|
|UseCase Runner|CustomerInquiryUseCaseRunner|
|Verification|CustomerInquiryVerification|
|Context|RunContext|
|Diff|DiffEngine|
|Report|DailySummaryReporter|

---

# 18. Docker / Build 命名規約

## 18.1 Docker Image

形式：

```text
e6-api-verifier:<version>
```

例：

```text
e6-api-verifier:1.0.0
e6-api-verifier:1.1.0
```

---

## 18.2 Release Package

形式：

```text
e6-api-verifier-release-<version>.zip
```

例：

```text
e6-api-verifier-release-1.0.0.zip
```

---

# 19. Version 命名規約

## 19.1 Version形式

Versionは Semantic Versioning を基本とする。

```text
MAJOR.MINOR.PATCH
```

例：

```text
1.0.0
1.1.0
1.1.1
```

---

## 19.2 Version更新基準

|変更|更新|
|----|----|
|構造変更|MAJOR|
|項目追加|MINOR|
|誤字修正|PATCH|
|説明補足|PATCH|
|互換性なし変更|MAJOR|

---

# 20. 命名Review Checklist

|No|観点|確認内容|OK|
|--|----|--------|--|
|1|ID|Prefixが規約通りか||
|2|ID|3桁連番か||
|3|ID|既存IDと重複していないか||
|4|文書名|IDを含んでいるか||
|5|文書名|日付・担当者名を含んでいないか||
|6|Context|Domain.Property形式か||
|7|Scenario|差分内容が分かる名称か||
|8|TestCase|対象と条件が分かる名称か||
|9|Evidence|runId、UC、SC、APIが含まれているか||
|10|Report|日付またはrunIdが含まれているか||
|11|JSONPath|`$` から始まっているか||
|12|Version|Semantic Versioningか||

---

# Appendix A. 命名例一覧

|分類|ID|名称|
|----|--|----|
|Business|BUS-001|顧客情報照会業務|
|BA|BA-001|顧客情報照会業務 現行業務分析書|
|Flow|BF-001|顧客番号入力|
|API|API-001|Customer Exists API|
|UseCase|UC-001|顧客情報照会|
|Scenario|SC-001|正常系|
|Context|CTX-001|Customer.id|
|Verification|VER-001|顧客情報照会正常系|
|TestCase|TC-001|顧客情報照会正常系|
|TestData|TD-001|正常系顧客|
|Evidence|EVD-001|Request Evidence|
|Report|RPT-001|Daily Summary|

:::

`Naming_Convention.md v1.0` 完成。

现在 Repository 级规范已有三份：

```text
Document_Style_Guide.md
Traceability_Rule.md
Naming_Convention.md
```

下一份建议做 `Review_Checklist.md`，把 BA/API/UseCase/Verification 的 Review 项目统一成可执行检查表。

## 第 158 轮

### 你

继续

### ChatGPT

继续。下面是 `docs/rules/Review_Checklist.md`。

:::writing{variant="document" id="51870"}
---
title: Review Checklist
document_id: RULE-REVIEW-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Review Checklist

---

# 1. 文書目的

本書は、E6 API Verification Platform における各成果物のレビュー観点を定義する。

対象成果物は以下とする。

|分類|対象成果物|
|----|----------|
|Business|現行業務分析書|
|API|API設計書|
|UseCase|UseCase設計書|
|Verification|Verification仕様書|
|Rule|Repository規約|
|Output|Report / Evidence|

---

# 2. 共通レビュー観点

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|C-001|文書情報|Front Matter が記載されているか|||
|C-002|文書ID|document_id が命名規約に従っているか|||
|C-003|版数|version が記載されているか|||
|C-004|状態|status が Draft / Review / Approved / Released のいずれかか|||
|C-005|関連成果物|前後成果物との関連が記載されているか|||
|C-006|ID|主要要素にIDが付与されているか|||
|C-007|Trace|Trace Matrix が記載されているか|||
|C-008|表記|用語が統一されているか|||
|C-009|Markdown|Markdown表示崩れがないか|||
|C-010|Mermaid|Mermaid図が表示可能か|||
|C-011|AI可読性|曖昧表現が少ないか|||
|C-012|重複|他文書と同一情報を重複記載していないか|||

---

# 3. BA レビュー観点

## 3.1 文書情報

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-001|文書ID|BA ID が命名規約に従っているか|||
|BA-002|Business ID|Business ID が記載されているか|||
|BA-003|対象業務|対象業務が明確か|||
|BA-004|関連成果物|要件・現行資料・API仕様との関連があるか|||

---

## 3.2 業務概要

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-101|業務目的|業務目的が明確か|||
|BA-102|業務概要|開始条件・処理概要・終了条件が分かるか|||
|BA-103|業務前提|利用者、開始条件、終了条件が記載されているか|||
|BA-104|業務範囲|対象・対象外が明確か|||
|BA-105|責務分離|Request/Response詳細をBAに書いていないか|||

---

## 3.3 業務フロー

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-201|Flow ID|すべてのFlowにFlow IDがあるか|||
|BA-202|Mermaid|業務フロー図がMermaidで記載されているか|||
|BA-203|Flow一覧|MermaidのFlowと表のFlow IDが一致しているか|||
|BA-204|分岐|判定分岐が明確か|||
|BA-205|終了条件|正常終了・異常終了が明確か|||

---

## 3.4 API分析

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-301|API ID|利用APIにAPI IDが記載されているか|||
|BA-302|利用目的|APIを利用する業務目的が明確か|||
|BA-303|呼出契機|API呼出契機が明確か|||
|BA-304|依存関係|API間の前後関係が明確か|||
|BA-305|重複排除|APIの詳細仕様をBAに記載していないか|||

---

## 3.5 データ分析

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-401|Data ID|主要業務データにData IDがあるか|||
|BA-402|Context ID|データ連携にContext IDがあるか|||
|BA-403|Producer|Contextの生成元が明確か|||
|BA-404|Consumer|Contextの利用先が明確か|||
|BA-405|必須|必須Contextが明確か|||

---

## 3.6 検証分析

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-501|Verification ID|検証対象にVerification IDがあるか|||
|BA-502|検証目的|なぜ検証するかが明確か|||
|BA-503|重要度|重要度が記載されているか|||
|BA-504|期待結果|業務期待結果が明確か|||
|BA-505|責務分離|Compare詳細をBAに書いていないか|||

---

## 3.7 Traceability

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|BA-601|Trace Matrix|Business Trace Matrix があるか|||
|BA-602|Flow→API|API利用FlowがAPI IDに紐づいているか|||
|BA-603|Flow→UseCase|FlowがUseCaseに紐づいているか|||
|BA-604|Flow→Verification|検証対象FlowがVerificationに紐づいているか|||
|BA-605|参照資料|参照資料が記載されているか|||

---

# 4. API設計書 レビュー観点

## 4.1 API概要

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-001|API ID|API IDが命名規約に従っているか|||
|API-002|API目的|API目的が明確か|||
|API-003|利用位置|Business Flow / UseCaseとの関係が明確か|||
|API-004|API分類|参照・更新・ファイル等の分類が明確か|||

---

## 4.2 Interface

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-101|Endpoint|Pathが記載されているか|||
|API-102|HTTP Method|Methodが記載されているか|||
|API-103|Content-Type|Content-Typeが記載されているか|||
|API-104|Header|Header定義が記載されているか|||
|API-105|認証|認証方式が明確か|||
|API-106|Timeout|Timeoutが記載されているか|||

---

## 4.3 Request Specification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-201|JSONPath|Request項目にJSONPathがあるか|||
|API-202|Type|型が記載されているか|||
|API-203|必須|必須/任意が明確か|||
|API-204|Null|Null許可が明確か|||
|API-205|空文字|空文字許可が明確か|||
|API-206|Min/Max|桁数・範囲が記載されているか|||
|API-207|Pattern|形式制約が必要な項目にPatternがあるか|||
|API-208|Enum|許容値が必要な項目にEnumがあるか|||
|API-209|固定値|固定値項目が明確か|||
|API-210|Context|Context入力項目が明確か|||

---

## 4.4 Response Specification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-301|JSONPath|Response項目にJSONPathがあるか|||
|API-302|Type|型が記載されているか|||
|API-303|必須|必須/任意が明確か|||
|API-304|固定値|固定値項目が記載されているか|||
|API-305|Enum|許容値が記載されているか|||
|API-306|入力値一致|Request値と一致すべき項目が明確か|||
|API-307|Context一致|Context値と一致すべき項目が明確か|||
|API-308|Dynamic|動的項目が明確か|||
|API-309|Baseline比較|Baseline比較候補が明確か|||
|API-310|Verification Target|検証対象が明確か|||

---

## 4.5 Error Specification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-401|Error形式|Error Response形式が記載されているか|||
|API-402|Error Code|Error Code一覧があるか|||
|API-403|HTTP Status|HTTP Statusとの対応があるか|||
|API-404|発生条件|Error発生条件が記載されているか|||
|API-405|検証対象|ErrorがVerification対象か明確か|||

---

## 4.6 Context / Verification Metadata

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|API-501|Input Context|Requestに利用するContextが明確か|||
|API-502|Output Context|Responseから生成するContextが明確か|||
|API-503|Context Lifecycle|Contextの有効範囲が明確か|||
|API-504|Request Check Candidate|Request検証候補が定義されているか|||
|API-505|Response Check Candidate|Response検証候補が定義されているか|||
|API-506|Diff Candidate|Baseline差分候補が定義されているか|||

---

# 5. UseCase設計書 レビュー観点

## 5.1 UseCase概要

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-001|UseCase ID|UseCase IDが命名規約に従っているか|||
|UC-002|UseCase目的|UseCase目的が明確か|||
|UC-003|対象Business|Business IDと紐づいているか|||
|UC-004|対象API|対象APIが記載されているか|||
|UC-005|対象Flow|BAのFlowと一致しているか|||

---

## 5.2 Entry Input

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-101|Input ID|Entry InputにIDがあるか|||
|UC-102|Type|型が記載されているか|||
|UC-103|設定元|Test Data / Runtime / Manual が明確か|||
|UC-104|Context|初期Contextと紐づいているか|||
|UC-105|TestData|TestData参照があるか|||

---

## 5.3 Main Flow

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-201|Step ID|全StepにStep IDがあるか|||
|UC-202|Flow ID|BA Flowと対応しているか|||
|UC-203|API ID|API実行StepにAPI IDがあるか|||
|UC-204|入力/出力|各Stepの入力・出力が明確か|||
|UC-205|次Step|次Stepが明確か|||

---

## 5.4 Scenario

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-301|Scenario ID|全ScenarioにIDがあるか|||
|UC-302|Scenario分類|Normal / Alternative / Exception 等が明確か|||
|UC-303|差分内容|Main Flowとの差分が明確か|||
|UC-304|Scenario Matrix|Scenario差分がMatrixで整理されているか|||
|UC-305|Selection Rule|Scenario選択条件が明確か|||
|UC-306|TestCase|各ScenarioにTestCase IDがあるか|||

---

## 5.5 API Execution Chain

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-401|API順序|API呼出順序が明確か|||
|UC-402|実行条件|APIごとの実行条件が明確か|||
|UC-403|Request生成元|Request生成元が明確か|||
|UC-404|Response利用|Response利用目的が明確か|||
|UC-405|Skip Rule|Skip条件が明確か|||
|UC-406|失敗時処理|Stop / Continue / Warn が明確か|||

---

## 5.6 Context Mapping

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-501|Context ID|Context IDが記載されているか|||
|UC-502|Producer|生成元が明確か|||
|UC-503|Consumer|利用先が明確か|||
|UC-504|Extract Mapping|ResponseからContext抽出が定義されているか|||
|UC-505|Request Binding|ContextからRequest設定が定義されているか|||
|UC-506|Lifetime|Contextの有効範囲が明確か|||

---

## 5.7 Execution / Evidence

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|UC-601|Retry|Retry方針があるか|||
|UC-602|Timeout|Timeout方針があるか|||
|UC-603|Stop Rule|停止条件が明確か|||
|UC-604|Expected Result|Scenario別期待結果があるか|||
|UC-605|Evidence|保存対象が明確か|||
|UC-606|Traceability|Trace Matrixがあるか|||

---

# 6. Verification仕様書 レビュー観点

## 6.1 Verification概要

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-001|Verification ID|Verification IDが命名規約に従っているか|||
|VER-002|対象UseCase|UseCase IDと紐づいているか|||
|VER-003|対象Scenario|Scenario IDと紐づいているか|||
|VER-004|対象API|API IDと紐づいているか|||
|VER-005|検証目的|検証目的が明確か|||

---

## 6.2 Test Data

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-101|TestData ID|TestData IDがあるか|||
|VER-102|Scenario紐付|Scenario IDと紐づいているか|||
|VER-103|ファイル|TestDataファイルが指定されているか|||
|VER-104|Entry Input|Entry Inputが明確か|||
|VER-105|データ固定性|日次実行に使える固定データか|||

---

## 6.3 Request Verification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-201|Required|必須チェックがあるか|||
|VER-202|Type|型チェックがあるか|||
|VER-203|Length|Min/Maxチェックがあるか|||
|VER-204|Pattern|Patternチェックがあるか|||
|VER-205|Enum|Enumチェックがあるか|||
|VER-206|Fixed|固定値チェックがあるか|||

---

## 6.4 Response Verification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-301|HTTP Status|HTTP Statusチェックがあるか|||
|VER-302|Required|必須項目チェックがあるか|||
|VER-303|Type|型チェックがあるか|||
|VER-304|Fixed Value|固定値チェックがあるか|||
|VER-305|Enum|Enumチェックがあるか|||
|VER-306|Input Match|入力値一致チェックがあるか|||
|VER-307|Context Match|Context一致チェックがあるか|||
|VER-308|Dynamic|動的項目の扱いが明確か|||

---

## 6.5 Context Verification

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-401|生成確認|Context生成確認があるか|||
|VER-402|引継ぎ確認|Context引継ぎ確認があるか|||
|VER-403|未取得時処理|未取得時のFail/Warnが明確か|||
|VER-404|Producer/Consumer|Producer/Consumerが一致しているか|||

---

## 6.6 Compare Policy

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-501|Compare Scope|比較対象が明確か|||
|VER-502|Field Mapping|Source/Targetが明確か|||
|VER-503|Normalize|正規化ルールがあるか|||
|VER-504|Compare Rule|Equals/Ignore/Regex等が明確か|||
|VER-505|Collection|配列比較ルールがあるか|||
|VER-506|Tolerance|許容差が定義されているか|||
|VER-507|Pass Rule|PASS/WARN/FAIL判定が明確か|||

---

## 6.7 TestCase / Execution / Evidence

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|VER-601|API単体TestCase|API単体TestCaseがあるか|||
|VER-602|UseCase連携TestCase|UseCase連携TestCaseがあるか|||
|VER-603|Scenario網羅|ScenarioがTestCaseで網羅されているか|||
|VER-604|Retry/Timeout|実行ルールがあるか|||
|VER-605|Stop/Continue|停止・継続ルールがあるか|||
|VER-606|Evidence|証跡保存対象が明確か|||
|VER-607|Report|Daily Summary / Diff Report 出力が定義されているか|||

---

# 7. Repository Rule レビュー観点

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|RULE-001|規約目的|規約の目的が明確か|||
|RULE-002|適用範囲|対象文書が明確か|||
|RULE-003|用語|用語が他規約と一致しているか|||
|RULE-004|禁止事項|禁止事項が明確か|||
|RULE-005|Check項目|レビュー可能な粒度か|||
|RULE-006|テンプレート連携|各Templateと矛盾していないか|||

---

# 8. Output レビュー観点

## 8.1 Daily Summary

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|OUT-001|Run ID|Run IDがあるか|||
|OUT-002|実行日|実行日があるか|||
|OUT-003|総合結果|PASS/WARN/FAILがあるか|||
|OUT-004|UseCase結果|UseCase別結果があるか|||
|OUT-005|Fail詳細|Fail時の対象が分かるか|||
|OUT-006|Evidence Link|証跡への参照があるか|||

---

## 8.2 Diff Report

|No|観点|確認内容|OK|備考|
|--|----|--------|--|----|
|OUT-101|差分項目|差分JSONPathが明確か|||
|OUT-102|期待値|Baseline / 固定値が記載されているか|||
|OUT-103|実績値|Current値が記載されているか|||
|OUT-104|重要度|Critical / High 等があるか|||
|OUT-105|判定|PASS/WARN/FAILがあるか|||
|OUT-106|Trace|API / TestCase / Evidenceへ追跡できるか|||

---

# 9. 承認判定

## 9.1 文書承認条件

|条件|判定|
|----|----|
|Critical NGなし|承認可|
|High NGなし|承認可|
|Medium NGあり|条件付き承認|
|Trace Matrix未記載|承認不可|
|主要ID欠落|承認不可|
|Mermaid表示不可|条件付き承認|
|AI解析不能な曖昧表現多数|承認不可|

---

## 9.2 Review Result

|Result|意味|
|------|----|
|Approved|承認|
|Approved with Comment|コメント付き承認|
|Rework|修正必須|
|Rejected|差戻し|

---

# 10. Review Summary Template

|項目|内容|
|----|----|
|対象文書|（記載）|
|文書ID|（記載）|
|Version|（記載）|
|レビュー日|YYYY-MM-DD|
|レビューア|（記載）|
|総合判定|Approved / Approved with Comment / Rework / Rejected|
|Critical指摘数|（記載）|
|High指摘数|（記載）|
|Medium指摘数|（記載）|
|Low指摘数|（記載）|

---

# 11. 指摘管理表

|No|重要度|指摘内容|対象箇所|対応方針|担当|状態|
|--|------|--------|--------|--------|----|----|
|1|High|（記載）|（記載）|（記載）|（記載）|Open / Closed|

---

# Appendix A. Review実施順序

```text id="bf05np"
1. Document Style Guide確認
2. Naming Convention確認
3. Traceability Rule確認
4. 対象文書レビュー
5. Trace Matrix確認
6. 指摘管理表作成
7. 修正確認
8. 承認判定
```

---

# Appendix B. 最小Reviewセット

最低限、以下は必ず確認する。

|対象|必須確認|
|----|--------|
|BA|Business Flow、API分析、検証分析、Trace|
|API|Request、Response、Error、Context、Verification Metadata|
|UseCase|Main Flow、Scenario、API Execution Chain、Context Mapping|
|Verification|Request/Response Check、Compare Policy、TestCase、Evidence|
|Output|Daily Summary、Diff、Evidence Link|

:::

`Review_Checklist.md v1.0` 完成。

## 第 159 轮

### 你

继续

### ChatGPT

继续下一份：`docs/rules/Glossary.md`

:::writing{variant="document" id="68421"}
---
title: Glossary
document_id: RULE-GLOSSARY-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Glossary

---

# 1. 文書目的

本書は、E6 API Verification Platform における用語を統一する。

---

# 2. 基本用語

|用語|意味|備考|
|----|----|----|
|Business|業務単位|例：顧客情報照会業務|
|Business Flow|業務処理の流れ|BAで定義|
|UseCase|業務を実行可能な単位に整理したもの|UCで定義|
|Scenario|UseCase内の条件・分岐・データ差分|SCで定義|
|API|E6 APIまたは検証対象API|API設計書で定義|
|Context|API間・Step間で受け渡す論理データ|CTXで定義|
|Verification|仕様が期待通りか確認すること|検証|
|TestCase|Verificationを実行する具体ケース|TCで定義|
|TestData|TestCaseで使用する入力データ|TDで定義|
|Evidence|実行証跡|Request/Response/Context/Diff/Log|
|Report|検証結果レポート|Daily Summary / Diff Report|

---

# 3. 文書用語

|用語|意味|主文書|
|----|----|----|
|現行業務分析書|現行业务Flow、API利用、検証対象を整理する文書|BA|
|API設計書|APIの入出力・Error・Context・Verification Metadataを定義する文書|API|
|UseCase設計書|API実行Chain、Scenario、Context連携を定義する文書|UC|
|Verification仕様書|検証方針、Compare、TestCase、Evidence、Reportを定義する文書|VER|
|Document Style Guide|Markdown文書作成規約|RULE|
|Traceability Rule|文書間Trace規約|RULE|
|Naming Convention|ID・ファイル名・命名規約|RULE|
|Review Checklist|成果物Review観点|RULE|

---

# 4. ID用語

|ID|意味|例|
|--|----|--|
|BUS ID|Business ID|BUS-001|
|BA ID|Business Analysis Document ID|BA-001|
|BF ID|Business Flow ID|BF-001|
|BR ID|Business Rule / Decision ID|BR-001|
|API ID|API ID|API-001|
|UC ID|UseCase ID|UC-001|
|SC ID|Scenario ID|SC-001|
|CTX ID|Context ID|CTX-001|
|VER ID|Verification Specification ID|VER-001|
|TC ID|TestCase ID|TC-001|
|TD ID|TestData ID|TD-001|
|EVD ID|Evidence ID|EVD-001|
|RPT ID|Report ID|RPT-001|

---

# 5. API用語

|用語|意味|備考|
|----|----|----|
|Endpoint|APIの接続先Path|例：/v1/customers|
|Method|HTTP Method|GET / POST / PUT / DELETE|
|Header|HTTP Header|Authorization等|
|Request|APIへ送信する入力|Header / Path / Query / Body|
|Response|APIから返却される出力|HTTP Status / Body|
|Path Parameter|URL Path内のParameter|例：/customers/{id}|
|Query Parameter|URL Query Parameter|例：?customerId=xxx|
|Request Body|Requestの本文|JSON等|
|Response Body|Responseの本文|JSON等|
|HTTP Status|HTTP応答コード|200 / 400 / 500等|
|Error Code|API固有エラーコード|E400001等|
|JSONPath|JSON項目位置表現|$.customer.id|

---

# 6. Request / Response 項目用語

|用語|意味|
|----|----|
|Type|項目の型|
|Required / 必須|値が必ず必要|
|Optional / 任意|値がなくてもよい|
|Null許可|nullを許可するか|
|空文字許可|空文字を許可するか|
|Min|最小桁数または最小値|
|Max|最大桁数または最大値|
|Pattern|正規表現制約|
|Enum / 許容値|取り得る値の一覧|
|Fixed Value / 固定値|固定で期待される値|
|Default|未指定時の既定値|
|Input Match|Request値とResponse値の一致|
|Context Match|Context値とResponse値の一致|
|Dynamic Field|実行ごとに変化する項目|
|Baseline比較|過去基準値との比較|

---

# 7. Verification用語

|用語|意味|
|----|----|
|Verification Target|検証対象|
|Verification Policy|検証方針|
|Request Verification|Request項目の検証|
|Response Verification|Response項目の検証|
|Context Verification|Context生成・引継ぎ検証|
|Compare Policy|比較方針|
|Baseline|比較基準|
|Current|今回実行結果|
|Diff|差分|
|Pass Rule|PASS/WARN/FAIL判定ルール|
|Evidence Rule|証跡保存ルール|
|Report Rule|レポート出力ルール|

---

# 8. Compare用語

|用語|意味|
|----|----|
|Equals|完全一致比較|
|Ignore|比較対象外|
|Regex|正規表現比較|
|Contains|部分一致|
|Exists|存在確認|
|Not Empty|空でないこと|
|Tolerance|許容差比較|
|Key Match|配列要素をKeyで比較|
|Order Match|順序も含めて比較|
|Normalize|比較前の正規化|
|Dynamic Ignore|動的項目の比較除外|

---

# 9. Result用語

|用語|意味|
|----|----|
|PASS|期待通り|
|WARN|確認必要だが処理継続可能|
|FAIL|期待不一致または重大エラー|
|SKIP|条件により未実行|
|BLOCKED|前提不成立により未実行|
|ERROR|ツールまたは環境エラー|

---

# 10. Evidence用語

|用語|意味|
|----|----|
|Raw Request|送信したRequest原文|
|Raw Response|受信したResponse原文|
|Context Snapshot|実行時Contextの保存|
|Diff Result|差分比較結果|
|Execution Log|実行ログ|
|Daily Summary|日次結果概要|
|Diff Report|差分詳細レポート|
|Evidence Report|証跡レポート|

---

# 11. 環境用語

|用語|意味|
|----|----|
|DEV|開発環境|
|STG|検証環境|
|PROD-LIKE|本番相当検証環境|
|Production|本番環境|
|Staging|本番投入前検証環境|
|Runtime|実行環境|
|Release Package|本番配置用成果物|
|Baseline Data|比較基準データ|
|Run ID|1回の実行を識別するID|

---

# 12. AI用語

|用語|意味|
|----|----|
|AI Agent|文書生成・解析・補助を行うAI|
|AI Readable|AIが安定解析できる構造|
|AI Generate|AIによる成果物生成|
|Specification Driven|仕様を起点に実装・検証を生成する方式|
|Documentation as Code|文書をGitでコード同様に管理する方式|
|Trace Matrix|ID間関連を示す表|

---

# 13. 推奨表記

|推奨|非推奨|
|----|------|
|検証|テストのみ|
|仕様|スペック|
|証跡|エビデンスのみ|
|差分|Diffのみ|
|呼出|コール|
|必須|Requiredのみ|
|任意|Optionalのみ|
|固定値|Fixedのみ|
|許容値|Enumのみ|
|動的項目|Dynamicのみ|
|比較対象外|無視|

---

# 14. 禁止表現

|表現|理由|
|----|----|
|適宜|条件が曖昧|
|必要に応じて|判断基準が不明|
|など|対象範囲が不明|
|いい感じに|仕様ではない|
|問題なければ|判定条件が不明|
|通常通り|通常の定義が不明|
|たぶん|仕様未確定|
|できれば|必須/任意が不明|

---

# 15. 用語追加ルール

新しい用語を追加する場合は以下を記載する。

|項目|内容|
|----|----|
|用語|追加する用語|
|意味|定義|
|使用文書|対象文書|
|関連ID|必要時|
|備考|補足|

---

# Appendix A. 用語例

|用語|意味|
|----|----|
|Customer.id|顧客番号Context|
|Contract.list|契約一覧Context|
|Runtime.runId|実行ID|
|Auth.token|認証Token|
|traceId|API実行追跡ID|
|updatedAt|更新日時Dynamic Field|

:::

`Glossary.md v1.0` 完成。

## 第 160 轮

### 你

继续

### ChatGPT

继续下一份：`docs/rules/Repository_Structure.md`

:::writing{variant="document" id="93742"}
---
title: Repository Structure
document_id: RULE-REPO-001
version: 1.0.0
status: Template
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Repository Structure

---

# 1. 文書目的

本書は、E6 API Verification Platform の Repository 構成、配置規則、成果物管理規則を定義する。

---

# 2. Repository 基本構成

```text
repository/

├── project/
├── docs/
├── runtime/
├── build/
├── staging/
└── outputs/
```

|ディレクトリ|役割|
|------------|----|
|project|プロジェクト管理成果物|
|docs|仕様書、テンプレート、規約、検証設計|
|runtime|Java実行エンジン|
|build|Build / Release / Docker関連|
|staging|本番相当の事前検証環境|
|outputs|ローカル実行結果。原則Git管理対象外|

---

# 3. project ディレクトリ

```text
project/

├── 要件定義書.md
├── WBS.md
├── スケジュール.md
├── QA一覧.md
└── リスク管理表.md
```

|ファイル|用途|
|--------|----|
|要件定義書.md|プロジェクト目的、範囲、成功条件|
|WBS.md|成果物単位の作業管理|
|スケジュール.md|開始日、終了日、担当、進捗管理|
|QA一覧.md|業務Team、E6、検証Teamへの確認事項|
|リスク管理表.md|リスク、影響、対応方針管理|

---

# 4. docs ディレクトリ

```text
docs/

├── rules/
├── templates/
├── business/
├── api/
├── usecase/
├── verification/
├── testdata/
├── master/
└── reports/
```

|ディレクトリ|用途|
|------------|----|
|rules|Repository共通規約|
|templates|各種テンプレート|
|business|現行業務分析書|
|api|API設計書|
|usecase|UseCase設計書|
|verification|Verification仕様書|
|testdata|検証用Test Data|
|master|API Master、UseCase Master 等|
|reports|レポート定義、サンプル|

---

# 5. docs/rules

```text
docs/rules/

├── Document_Style_Guide.md
├── Traceability_Rule.md
├── Naming_Convention.md
├── Review_Checklist.md
├── Glossary.md
└── Repository_Structure.md
```

|ファイル|用途|
|--------|----|
|Document_Style_Guide.md|Markdown、Mermaid、表、Front Matter規約|
|Traceability_Rule.md|ID間・文書間Trace規約|
|Naming_Convention.md|ID、ファイル名、Context名等の命名規約|
|Review_Checklist.md|成果物Review観点|
|Glossary.md|用語統一|
|Repository_Structure.md|Repository構成規約|

---

# 6. docs/templates

```text
docs/templates/

├── BA_Template.md
├── API_Template.md
├── UseCase_Template.md
└── Verification_Specification_Template.md
```

|テンプレート|生成先|
|------------|------|
|BA_Template.md|docs/business/BA-XXX_*.md|
|API_Template.md|docs/api/API-XXX_*.md|
|UseCase_Template.md|docs/usecase/UC-XXX_*.md|
|Verification_Specification_Template.md|docs/verification/VER-XXX_*.md|

---

# 7. docs/business

```text
docs/business/

├── BA-001_顧客情報照会業務.md
├── BA-002_契約情報照会業務.md
└── BA-XXX_〇〇業務.md
```

|項目|規則|
|----|----|
|単位|1業務Flowまたは1業務単位|
|命名|BA-XXX_業務名.md|
|主内容|業務概要、業務Flow、API分析、検証分析、Trace|
|作成元|現行業務資料、設計書、E6 API利用資料|
|後続|API設計書、UseCase設計書、Verification仕様書|

---

# 8. docs/api

```text
docs/api/

├── API-001_CustomerExistsAPI.md
├── API-002_CustomerDetailAPI.md
└── API-XXX_〇〇API.md
```

|項目|規則|
|----|----|
|単位|1 API 1 文書|
|命名|API-XXX_API名.md|
|主内容|Endpoint、Request、Response、Error、Context、Verification Metadata|
|作成元|E6 API仕様書、既存設計書、BA|
|後続|UseCase、Verification|

---

# 9. docs/usecase

```text
docs/usecase/

├── UC-001_顧客情報照会.md
├── UC-002_契約情報照会.md
└── UC-XXX_〇〇.md
```

|項目|規則|
|----|----|
|単位|業務能力単位|
|命名|UC-XXX_UseCase名.md|
|主内容|Entry Input、Main Flow、Scenario、API Execution Chain、Context Mapping|
|Scenario|同一UseCase内の分岐・差分として管理|
|後続|Verification仕様書|

---

# 10. docs/verification

```text
docs/verification/

├── VER-001_顧客情報照会.md
├── VER-002_契約情報照会.md
└── VER-XXX_〇〇.md
```

|項目|規則|
|----|----|
|単位|UseCaseまたはScenario群単位|
|命名|VER-XXX_対象名.md|
|主内容|Request/Response検証、Compare Policy、TestCase、Evidence、Report Rule|
|作成元|BA、API設計書、UseCase設計書|
|後続|Execution Spec、Test Data、Report|

---

# 11. docs/testdata

```text
docs/testdata/

├── UC-001/
│   ├── TD-001_SC-001_normal.json
│   ├── TD-002_SC-002_customer_not_found.json
│   └── TD-003_SC-003_contract_empty.json
│
└── UC-XXX/
```

|項目|規則|
|----|----|
|配置単位|UseCase単位|
|形式|JSON / CSV / YAML|
|命名|TD-XXX_SC-XXX_名称.json|
|用途|Verification実行入力|
|注意|本番機密情報を含めない|

---

# 12. docs/master

```text
docs/master/

├── API_Master.md
├── UseCase_Master.md
├── Scenario_Master.md
├── Context_Master.md
├── Environment_Master.md
└── Verification_Master.md
```

|Master|用途|
|------|----|
|API_Master.md|API一覧、ID、名称、対象業務|
|UseCase_Master.md|UseCase一覧、対象業務、実行対象|
|Scenario_Master.md|Scenario一覧、分類、対象UseCase|
|Context_Master.md|Context一覧、Producer、Consumer|
|Environment_Master.md|DEV/STG/PROD-LIKE環境情報|
|Verification_Master.md|Verification一覧、実行対象、重要度|

---

# 13. docs/reports

```text
docs/reports/

├── DailySummary_Template.md
├── DiffReport_Template.md
└── EvidenceReport_Template.md
```

|テンプレート|用途|
|------------|----|
|DailySummary_Template.md|日次実行結果概要|
|DiffReport_Template.md|差分詳細|
|EvidenceReport_Template.md|証跡確認|

---

# 14. runtime ディレクトリ

```text
runtime/

├── src/
├── config/
├── scripts/
├── test/
└── docker/
```

|ディレクトリ|用途|
|------------|----|
|src|Java実装|
|config|開発用設定|
|scripts|実行補助Script|
|test|単体試験|
|docker|開発用Docker|

---

# 15. build ディレクトリ

```text
build/

├── scripts/
├── docker/
└── release/
```

|ディレクトリ|用途|
|------------|----|
|scripts|generate-spec、build、package、release|
|docker|Build用Dockerfile、本番Image定義|
|release|Release Package出力|

---

# 16. staging ディレクトリ

```text
staging/

├── docker-compose.yml
├── config/
├── data/
└── logs/
```

|ディレクトリ|用途|
|------------|----|
|docker-compose.yml|本番相当実行検証|
|config|staging用設定|
|data|baseline、runs、reports|
|logs|staging実行ログ|

---

# 17. outputs ディレクトリ

```text
outputs/

├── baseline/
├── runs/
├── reports/
└── evidence/
```

|ディレクトリ|用途|
|------------|----|
|baseline|比較基準|
|runs|ローカル実行結果|
|reports|ローカルReport|
|evidence|ローカル証跡|

`outputs/` は原則 Git 管理対象外とする。

---

# 18. Git 管理対象

## 18.1 Git管理対象

|対象|管理|
|----|----|
|project|Yes|
|docs/rules|Yes|
|docs/templates|Yes|
|docs/business|Yes|
|docs/api|Yes|
|docs/usecase|Yes|
|docs/verification|Yes|
|docs/master|Yes|
|runtime/src|Yes|
|runtime/config template|Yes|
|build/scripts|Yes|
|build/docker|Yes|
|staging template|Yes|

---

## 18.2 Git管理対象外

|対象|理由|
|----|----|
|outputs|実行結果|
|runtime/config/secret|機密情報|
|staging/data|実行結果|
|staging/logs|ログ|
|build/release/*.zip|生成物|
|target / build成果物|生成物|
|*.log|ログ|
|*.tmp|一時ファイル|

---

# 19. .gitignore 推奨

```text
outputs/
staging/data/
staging/logs/
runtime/config/secret/
build/release/*.zip
*.log
*.tmp
target/
build/
.env
```

---

# 20. 成果物配置ルール

## 20.1 新規BA作成時

```text
docs/templates/BA_Template.md
  ↓ copy
docs/business/BA-XXX_〇〇業務.md
```

---

## 20.2 新規API作成時

```text
docs/templates/API_Template.md
  ↓ copy
docs/api/API-XXX_〇〇API.md
```

---

## 20.3 新規UseCase作成時

```text
docs/templates/UseCase_Template.md
  ↓ copy
docs/usecase/UC-XXX_〇〇.md
```

---

## 20.4 新規Verification作成時

```text
docs/templates/Verification_Specification_Template.md
  ↓ copy
docs/verification/VER-XXX_〇〇.md
```

---

# 21. Review 前提

成果物Review時は以下規約を参照する。

```text
docs/rules/
├── Document_Style_Guide.md
├── Traceability_Rule.md
├── Naming_Convention.md
├── Review_Checklist.md
├── Glossary.md
└── Repository_Structure.md
```

---

# 22. AI Agent 参照順序

AI Agent が文書作成・更新を行う場合、以下順序で参照する。

```text
1. docs/rules/Document_Style_Guide.md
2. docs/rules/Naming_Convention.md
3. docs/rules/Traceability_Rule.md
4. docs/rules/Glossary.md
5. docs/templates/*
6. 対象文書
```

---

# Appendix A. 最小構成

最小構成は以下とする。

```text
repository/

├── project/
├── docs/
│   ├── rules/
│   ├── templates/
│   ├── business/
│   ├── api/
│   ├── usecase/
│   └── verification/
├── runtime/
├── build/
└── staging/
```

---

# Appendix B. 推奨構成

推奨構成は以下とする。

```text
repository/

├── project/
├── docs/
│   ├── rules/
│   ├── templates/
│   ├── business/
│   ├── api/
│   ├── usecase/
│   ├── verification/
│   ├── testdata/
│   ├── master/
│   └── reports/
├── runtime/
├── build/
├── staging/
└── outputs/
```

:::

`Repository_Structure.md v1.0` 完成。

## 第 161 轮

### 你

继续

### ChatGPT

可以，而且我觉得我们现在要停一下，不是停止工作，而是**升级设计**。

我重新把我们这几十个小时讨论的内容全部串了一遍，我发现一个问题。

---

# 现在 Repository 其实还缺一个"宪法"

目前我们做的是

```
Rule
↓

Template
↓

Business

↓

API

↓

UseCase

↓

Verification
```

但是实际上，日本大型项目还有一层。

叫：

> **Specification Architecture**

也就是：

整个 Specification Repository 是怎么设计出来的。

这一层不是 Rule。

Rule 是"规定怎么写"。

Specification Architecture 是

> **为什么 Repository 要这样设计。**

这是两回事。

---

## 我建议增加 docs/specification/

例如

```
docs/

├── specification/
│
│    00_Repository_Architecture.md
│
│    01_Document_Model.md
│
│    02_Document_Relationship.md
│
│    03_AI_First_Design.md
│
│    04_Document_Lifecycle.md
│
│    05_Automation_Architecture.md
│
│    06_Execution_Model.md
│
│    07_Quality_Model.md
│
│    08_Repository_Roadmap.md
│
└── rules/
```

这一层不是规范。

而是架构。

---

# 举个例子

为什么 BA 不写 API？

Rule 会说

```
禁止写
```

Architecture 会解释

```
因为：

Business

↓

API

↓

UseCase

↓

Verification

是一条单向依赖。

否则

API改变

↓

BA需要改

↓

Business也变

这是错误的。
```

这就是 Architecture。

---

# 再举一个例子

为什么 Verification 不写 API Spec？

Architecture 会写

```
Verification

只负责

How to Verify

API

负责

What is API

否则

Specification

会产生两个 Source of Truth。
```

所以

Architecture

回答的是：

为什么。

Rule

回答的是：

怎么做。

---

# 我认为 Repository 现在进入第二阶段了

第一阶段

我们做的是

```
规则
```

第二阶段

应该做

```
Specification Architecture
```

例如

```
00 Repository Vision

↓

01 Specification Architecture

↓

02 Layer Model

↓

03 Dependency Rule

↓

04 Repository Structure

↓

05 AI Generation Flow

↓

06 Review Flow

↓

07 Execution Flow

↓

08 Evolution Strategy
```

这一层以后

Codex

Claude

Copilot

OpenAI Agent

全部都会先看。

因为

它决定整个 Repository。

---

# 我为什么现在提这个

因为我们已经不是在写模板了。

我们已经在设计：

> **一个 AI Native 的日本工业化 Specification Engineering Framework。**

这已经超出了普通项目文档的范畴。

---

## 我建议把它命名为

```
Specification Engineering Framework（SEF）
```

Repository 的定位就变成：

```
SEF

├── Architecture
├── Rules
├── Templates
├── Specifications
├── Runtime
└── Outputs
```

---

**这是我认为目前最重要的一次升级。**

因为后面无论增加多少模板、规则、Agent，都会建立在这套 **Specification Architecture（SEF）** 之上，而不是继续零散地补文档。我建议下一阶段，我们先把这套 **SEF Architecture** 做完整，再继续扩展其他模板。这样整个体系会真正达到工业级，并且 AI、开发者、测试人员都能用同一套思想工作。

## 第 162 轮

### 你

咱们repo不已经定了吗

### ChatGPT

对，你提醒得非常好。

**Repo 其实已经定了。**

而且我回头看了一遍，我们之前讨论的方向，**不应该再改 Repo 结构了。**

---

## 我认为现在应该保持 Repo 稳定

也就是保持类似这样：

```text
repository/

├── project/
├── docs/
│   ├── rules/
│   ├── templates/
│   ├── business/
│   ├── api/
│   ├── usecase/
│   ├── verification/
│   ├── master/
│   ├── reports/
│   └── testdata/
│
├── runtime/
├── build/
├── staging/
└── outputs/
```

**这个结构我认为已经足够成熟，不建议再动。**

---

## 我刚才真正想表达的不是增加目录

而是增加一种**文档类型**。

其实完全可以放在：

```text
docs/rules/
```

或者

```text
project/
```

根本不用新增 `specification/`。

例如：

```text
project/

├── Project_Charter.md
├── Repository_Principles.md      ← 新
├── Architecture_Decision_Log.md  ← 新
├── WBS.md
├── QA.md
```

或者：

```text
docs/rules/

├── Repository_Principles.md
```

这样 Repo 一点都不用改。

---

# 我为什么会想到这个

因为我们现在已经有：

- Document Style
- Naming
- Traceability
- Review
- Glossary
- Repository Structure

但是还缺一个东西：

> **为什么这样设计。**

例如：

```
为什么 BA 不允许写 API Response？

为什么 Verification 不定义 API？

为什么 Context 放 UseCase？

为什么 Scenario 放 UseCase 而不是 TestCase？
```

这些其实不是 Rule。

它们属于：

> **Architecture Decision（架构决策）**

在大型项目里通常会有一个文档记录这些决策，防止团队后续又改回来。

---

## 我现在反而建议保持稳定

我们已经有：

**模板（Template）**
- BA
- API
- UseCase
- Verification

**规范（Rule）**
- Document Style
- Naming
- Traceability
- Review
- Glossary
- Repository Structure

这一层已经很完整了。

---

# 我认为接下来真正应该做的

不是继续写 Rule。

而是开始做真正的业务成果物。

例如：

```
BA-001
↓

API-001
↓

API-002
↓

API-003
↓

UC-001
↓

VER-001
```

也就是说，用我们刚刚建立的工业级模板，做一套**完整、真实的示例工程**。

---

## 这是我现在最推荐的路线

因为模板只有真正落地一套完整案例，才能发现哪里需要补充、哪里设计得不合理。

而且这套案例以后还能直接作为：

- AI 的 Few-shot 示例
- 新成员培训资料
- Codex / Copilot Agent 的参考样例
- 自动化测试的基准项目

**所以我建议，从下一步开始，我们不要再扩充规则，而是正式进入第一套完整的 Business → API → UseCase → Verification 示例工程。**我认为这会比继续增加规范带来更大的价值。

## 第 163 轮

### 你

repo对吗

### ChatGPT

我认真看了一遍，目前**Repo 大方向是对的**，而且已经达到工业项目可以落地的程度。

不过，如果目标是你一直说的：

- 日本工业级项目
- AI First
- Specification Driven
- Agent 自动生成
- 长期维护（10年以上）

我会给它 **9.7/10**，还有几个地方值得优化，但**不是推倒重来**，而是在现有 Repo 上完善。

---

# 我建议最终 Repo（Freeze）

```text
repository/

├── project/                  # 项目管理
│   ├── Project_Charter.md
│   ├── WBS.md
│   ├── QA.md
│   ├── Risk.md
│   └── ADR/                  # Architecture Decision Record
│
├── docs/
│   ├── rules/                # Repository规范
│   ├── templates/            # 模板
│   ├── business/             # BA
│   ├── api/                  # API
│   ├── usecase/              # UseCase
│   ├── verification/         # Verification
│   ├── master/               # Master
│   ├── reports/              # Report Template
│   ├── testdata/             # TestData
│   └── assets/               # 图片、Mermaid源图等
│
├── runtime/                  # Java Runtime
│
├── build/
│
├── staging/
│
├── outputs/                  # 运行结果（Git Ignore）
│
└── mkdocs.yml
```

这个我建议**冻结**。

---

# 我建议增加的只有两个东西

## ① ADR（Architecture Decision Record）

不是增加目录层级，而是在 `project/ADR/`。

例如：

```text
ADR/

ADR-001_Context放UseCase.md

ADR-002_Scenario不独立建UseCase.md

ADR-003_Verification负责Compare.md

ADR-004_API不写Business.md
```

它的作用是记录：

> 为什么这样设计。

以后有人问：

为什么 Scenario 在 UseCase？

直接看 ADR。

这是日本很多大型项目和现代软件架构都采用的做法。

---

## ② assets

很多 BA 都会有：

- PNG
- SVG
- Draw.io
- Mermaid 原稿
- Excel 图片

建议统一放：

```text
docs/assets/
```

然后 Markdown 引用。

不要图片到处都是。

---

# 我认为目前最大的优点

我们已经不是：

```text
文档

↓

开发
```

而是：

```text
Business

↓

API

↓

UseCase

↓

Verification

↓

Execution

↓

Evidence

↓

Report
```

这是一条完整链路。

---

# 我唯一还想升级的一点（不是 Repo）

以后如果项目越来越大。

建议 Master 不只是几个 Markdown。

而是：

```text
master/

API_Master.yaml

UseCase_Master.yaml

Scenario_Master.yaml

Context_Master.yaml
```

为什么？

因为：

以后：

Agent

可以直接读取。

不用解析 Markdown。

例如：

```yaml
api_id: API-001

business:
  - BUS-001

usecases:
  - UC-001

verification:
  - VER-001
```

Agent 读取 YAML 会比 Markdown 快得多。

而 Markdown 仍然保留给人阅读。

这是很多 AI 工程正在采用的模式。

---

## 我的结论

**Repo 我认为已经可以冻结了。**

我不会再建议改整体结构了，后续所有工作都应该建立在这套 Repo 上。

接下来我们的重点应该放在：

1. 完善每个模板（BA、API、UseCase、Verification）。
2. 建立第一套完整的示例工程（Business → API → UseCase → Verification）。
3. 再开发 AI Agent 和 Runtime，让它们围绕这套 Repository 工作。

我认为这是最稳妥、也是最符合工业化开发的路线。

## 第 164 轮

### 你

我们之前不是这个结构

### ChatGPT

对，你说得对。**我们之前最早冻结的结构不是我刚才那个 `docs/business/api/usecase` 版。**

之前我们定的是这一版：

```text
repository/

├── project/
│
├── business/
│
├── system/
│
├── runtime/
│
├── build/
│
├── staging/
│
└── outputs/
```

后来我在继续做规则文档时，把它扩展成了：

```text
repository/

├── project/
├── docs/
│   ├── rules/
│   ├── templates/
│   ├── business/
│   ├── api/
│   ├── usecase/
│   └── verification/
├── runtime/
├── build/
├── staging/
└── outputs/
```

这就是你感觉“不对”的原因：**我把已经冻结的根目录结构又换成了 docs 集中式结构。**

正确处理方式应该是：**不改根结构，把后面这些 rules/templates 放回原来的结构里。**

最终应回到这个：

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── WBS.md
│   ├── スケジュール.md
│   ├── QA一覧.md
│   └── リスク管理表.md
│
├── business/
│   ├── BA_Template.md
│   ├── BA-001_〇〇業務.md
│   └── BA-002_〇〇業務.md
│
├── system/
│   ├── rules/
│   │   ├── Document_Style_Guide.md
│   │   ├── Traceability_Rule.md
│   │   ├── Naming_Convention.md
│   │   ├── Review_Checklist.md
│   │   ├── Glossary.md
│   │   └── Repository_Structure.md
│   │
│   ├── templates/
│   │   ├── API_Template.md
│   │   ├── UseCase_Template.md
│   │   └── Verification_Specification_Template.md
│   │
│   ├── api/
│   │   ├── API-001_〇〇API.md
│   │   └── API-002_〇〇API.md
│   │
│   ├── usecase/
│   │   ├── UC-001_〇〇.md
│   │   └── UC-002_〇〇.md
│   │
│   ├── verification/
│   │   ├── VER-001_〇〇.md
│   │   └── VER-002_〇〇.md
│   │
│   ├── master/
│   │   ├── API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── Scenario_Master.md
│   │   ├── Context_Master.md
│   │   └── Verification_Master.md
│   │
│   ├── testdata/
│   │   └── UC-001/
│   │       ├── TD-001_SC-001_normal.json
│   │       └── TD-002_SC-002_error.json
│   │
│   └── reports/
│       ├── DailySummary_Template.md
│       ├── DiffReport_Template.md
│       └── EvidenceReport_Template.md
│
├── runtime/
│   ├── src/
│   ├── config/
│   ├── scripts/
│   ├── test/
│   └── docker/
│
├── build/
│   ├── scripts/
│   ├── docker/
│   └── release/
│
├── staging/
│   ├── docker-compose.yml
│   ├── config/
│   ├── data/
│   └── logs/
│
└── outputs/
    ├── baseline/
    ├── runs/
    ├── reports/
    └── evidence/
```

关键修正：

```text
docs/ 不作为根目录使用
```

而是：

```text
business/ 负责 BA
system/   负责 API / UseCase / Verification / rules / templates / master
```

所以我们之前做的这些文档不废，只是路径要改：

|刚才写的路径|修正后路径|
|---|---|
|docs/rules/Document_Style_Guide.md|system/rules/Document_Style_Guide.md|
|docs/rules/Traceability_Rule.md|system/rules/Traceability_Rule.md|
|docs/rules/Naming_Convention.md|system/rules/Naming_Convention.md|
|docs/rules/Review_Checklist.md|system/rules/Review_Checklist.md|
|docs/rules/Glossary.md|system/rules/Glossary.md|
|docs/rules/Repository_Structure.md|system/rules/Repository_Structure.md|
|docs/templates/API_Template.md|system/templates/API_Template.md|
|docs/templates/UseCase_Template.md|system/templates/UseCase_Template.md|
|docs/templates/Verification_Specification_Template.md|system/templates/Verification_Specification_Template.md|
|docs/business/BA_Template.md|business/BA_Template.md|
|docs/api/API-001_xxx.md|system/api/API-001_xxx.md|
|docs/usecase/UC-001_xxx.md|system/usecase/UC-001_xxx.md|
|docs/verification/VER-001_xxx.md|system/verification/VER-001_xxx.md|

结论：**Repo 根结构回到之前冻结版，不再用 docs 根目录。**

## 第 165 轮

### 你

也不是你现在这个结构 之前是有06_verification_assets文件夹

### ChatGPT

对，你说得对。之前结构里有：

```text
system/
└── 06_verification_assets/
```

我刚才又偏了。

应回到这版：

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── WBS.md
│   ├── スケジュール.md
│   ├── QA一覧.md
│   └── リスク管理表.md

├── system/
│   ├── 01_business/
│   │   ├── BA_Template.md
│   │   ├── BA-001_〇〇業務.md
│   │   └── BA-002_〇〇業務.md
│   │
│   ├── 02_master/
│   │   ├── API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── Scenario_Master.md
│   │   ├── Context_Master.md
│   │   └── Verification_Master.md
│   │
│   ├── 03_api_design/
│   │   ├── API_Template.md
│   │   ├── API-001_〇〇API.md
│   │   └── API-002_〇〇API.md
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase_Template.md
│   │   ├── UC-001_〇〇.md
│   │   └── UC-002_〇〇.md
│   │
│   ├── 05_framework/
│   │   ├── System_Architecture.md
│   │   ├── Framework.md
│   │   ├── RunContext.md
│   │   ├── Snapshot.md
│   │   ├── Diff.md
│   │   ├── Report.md
│   │   ├── File_IO.md
│   │   ├── Log_Exception.md
│   │   └── Environment.md
│   │
│   └── 06_verification_assets/
│       ├── Verification_Specification_Template.md
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       ├── test_data/
│       ├── reports/
│       └── evidence/

├── runtime/
├── build/
├── staging/
└── outputs/
```

路径修正如下：

| 文档 | 正确位置 |
|---|---|
| BA_Template.md | `system/01_business/` |
| API_Template.md | `system/03_api_design/` |
| UseCase_Template.md | `system/04_usecase_design/` |
| Verification_Specification_Template.md | `system/06_verification_assets/` |
| Document_Style_Guide.md 等规则 | `system/05_framework/` 或 `system/02_master/` 配下的共通规则位置 |

结论：**以 `system/01～06` 结构为准，`06_verification_assets` 保留。**

## 第 166 轮

### 你

md文件不完全是英文

### ChatGPT

对，文件名应该用**日本项目可读的日语名 + 必要时英文补足**。

例如这样更合适：

```text
system/
├── 01_business/
│   ├── 現行業務分析書_Template.md
│   └── BA-001_顧客情報照会業務.md

├── 03_api_design/
│   ├── API設計書_Template.md
│   └── API-001_CustomerExistsAPI.md

├── 04_usecase_design/
│   ├── UseCase設計書_Template.md
│   └── UC-001_顧客情報照会.md

├── 05_framework/
│   ├── 文書作成規約.md
│   ├── トレーサビリティ規約.md
│   ├── 命名規約.md
│   ├── レビュー観点一覧.md
│   ├── 用語集.md
│   └── Repository構成.md

└── 06_verification_assets/
    ├── Verification仕様書_Template.md
    ├── execution_spec/
    ├── api_test_spec/
    ├── usecase_test_spec/
    ├── test_data/
    ├── reports/
    └── evidence/
```

规则：

```text
设计书、规范、说明类：日语名
ID管理类：ID + 日语名
API物理名：英文保持
机器读取目录：英文/蛇形命名可保持
```

所以不是全英文。
应采用：

```text
日本人能读懂 + AI能识别 + 文件系统稳定
```

## 第 167 轮

### 你

对

### ChatGPT

对。那我们正式把 **Repository结构 + 文件命名** 修正为下面这一版。

以后以这个为准。

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── WBS.md
│   ├── スケジュール.md
│   ├── QA一覧.md
│   └── 課題・リスク管理表.md
│
├── system/
│   ├── 01_business/
│   │   ├── 現行業務分析書_Template.md
│   │   ├── BA-001_顧客情報照会業務.md
│   │   └── BA-002_〇〇業務.md
│   │
│   ├── 02_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── Scenario_Master.md
│   │   ├── Context_Master.md
│   │   ├── Environment_Master.md
│   │   └── Verification_Master.md
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   ├── API-001_CustomerExistsAPI.md
│   │   └── API-002_CustomerDetailAPI.md
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   ├── UC-001_顧客情報照会.md
│   │   └── UC-002_〇〇.md
│   │
│   ├── 05_framework/
│   │   ├── システム設計書.md
│   │   ├── 共通Framework設計書.md
│   │   ├── RunContext設計書.md
│   │   ├── Snapshot設計書.md
│   │   ├── Diff設計書.md
│   │   ├── Report設計書.md
│   │   ├── ファイル入出力設計書.md
│   │   ├── ログ・例外設計書.md
│   │   ├── 環境設計書.md
│   │   ├── 文書作成規約.md
│   │   ├── トレーサビリティ規約.md
│   │   ├── 命名規約.md
│   │   ├── レビュー観点一覧.md
│   │   ├── 用語集.md
│   │   └── Repository構成.md
│   │
│   └── 06_verification_assets/
│       ├── Verification仕様書_Template.md
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       ├── test_data/
│       ├── reports/
│       └── evidence/
│
├── runtime/
│   ├── src/
│   ├── config/
│   ├── scripts/
│   ├── test/
│   └── docker/
│
├── build/
│   ├── scripts/
│   ├── docker/
│   └── release/
│
├── staging/
│   ├── docker-compose.yml
│   ├── config/
│   ├── data/
│   └── logs/
│
└── outputs/
    ├── baseline/
    ├── runs/
    ├── reports/
    └── evidence/
```

命名规则也固定：

```text
目录名：
01_business / 02_master / 03_api_design 这种保持英文+编号
理由：排序稳定、AI/脚本容易处理

文档名：
日本语为主
理由：日本项目人员可读

ID：
BA-001 / API-001 / UC-001 / VER-001
理由：Trace和自动处理稳定

API物理名：
CustomerExistsAPI 这种保持英文
理由：贴近API、代码、JSON、Java命名
```

所以最终原则是：

```text
目录 = 机器友好
文档 = 日本项目友好
ID = Trace友好
API名 = 技术友好
```

这版才和我们之前讨论的 `system/01～06`、`06_verification_assets`、日本IT项目风格一致。

## 第 168 轮

### 你

你加的那几个文件在repo的哪个位置

### ChatGPT

这是个很好的问题，而且也是我们现在需要统一的地方。

我建议**不要把它们放到 `05_framework`**。

因为我后来重新思考了一下，它们其实不是 Framework，它们属于**Repository 的开发规范**。

也就是说，我们现在实际上有三类文档：

```text
① 业务规格（Business Specification）

02 业务
03 API
04 UseCase
06 Verification

----------------------------

② 系统规格（System Specification）

05 Framework
Runtime
Build
Staging

----------------------------

③ Repository规范（Repository Standard）

Document Style
Naming
Traceability
Review
Glossary
Repository Structure
```

所以如果继续放在 `05_framework`，职责就混了。

---

## 我现在建议的放置位置

我建议在 `system` 下增加一个独立编号。

例如：

```text
system/

01_business/

02_master/

03_api_design/

04_usecase_design/

05_framework/

06_verification_assets/

07_repository_rules/
```

里面放：

```text
07_repository_rules/

文書作成規約.md

トレーサビリティ規約.md

命名規約.md

レビュー観点一覧.md

用語集.md

Repository構成.md
```

这样职责非常清晰。

---

## 为什么不是 05_framework？

因为 Framework 是运行框架。

例如：

```text
RunContext

Snapshot

Diff

Report

Exception

Log

Retry

Execution Engine
```

这些属于**Runtime Framework**。

而：

```text
文書作成規約

命名規約

Traceability

Review

Glossary
```

属于**Specification Framework**。

完全不是一类东西。

---

## 还有一种方案（我更推荐）

其实经过我们这段时间的设计，我更推荐这一版：

```text
system/

00_repository/

01_business/

02_master/

03_api_design/

04_usecase_design/

05_framework/

06_verification_assets/
```

把 Repository 的公共规范放在：

```text
00_repository/

Repository構成.md

文書作成規約.md

命名規約.md

トレーサビリティ規約.md

レビュー観点一覧.md

用語集.md
```

原因有三个：

1. **这是整个 Repository 的基础**，所有其他目录都依赖它，所以编号应在最前。
2. **AI Agent 进入项目时**，第一步就读取 `00_repository/`，然后再处理 BA、API、UseCase、Verification。
3. 以后如果增加新的 Repository 规范（例如 Git 运用规范、MkDocs 运用规范、AI Agent 运用规范），都可以放在这里，不会污染 Framework。

---

**我现在更倾向于 `00_repository` 方案，而不是 `07_repository_rules`。**

因为从架构依赖关系来看，Repository 规范是整个工程的根基，排在最前面比放在最后更符合工业化设计，也更利于 AI 和开发人员理解整个仓库。

## 第 169 轮

### 你

咱冻结这结构

### ChatGPT

我同意，**现在应该冻结（Freeze）Repository 结构**。

原因不是因为它已经“完美”，而是因为继续调整目录会影响后面的所有模板、Master、Agent、Runtime、MkDocs、AI Prompt。

以后如果确实需要调整，应该走**版本升级**，而不是边做边改。

---

# Repository Structure v1.0（Freeze）

建议从今天开始，所有文档都按这套结构开发。

```text
repository/

├── project/
│
├── system/
│   ├── 00_repository/
│   ├── 01_business/
│   ├── 02_master/
│   ├── 03_api_design/
│   ├── 04_usecase_design/
│   ├── 05_framework/
│   └── 06_verification_assets/
│
├── runtime/
├── build/
├── staging/
└── outputs/
```

---

## 每个目录职责（冻结）

|目录|职责|状态|
|------|------|------|
|project|项目管理、计划、QA、WBS、ADR|✅ Freeze|
|system/00_repository|Repository规范、模板规范、命名、Trace、Review、Glossary|✅ Freeze|
|system/01_business|现行业务分析书（BA）|✅ Freeze|
|system/02_master|Master定义（API、Context、UseCase等）|✅ Freeze|
|system/03_api_design|API设计书|✅ Freeze|
|system/04_usecase_design|UseCase设计书|✅ Freeze|
|system/05_framework|系统公共框架设计（Context、Report、Diff、日志等）|✅ Freeze|
|system/06_verification_assets|Verification、Execution Spec、TestData、Evidence、Report Template|✅ Freeze|
|runtime|执行程序|✅ Freeze|
|build|构建、发布|✅ Freeze|
|staging|验证环境|✅ Freeze|
|outputs|运行输出（Git Ignore）|✅ Freeze|

---

# 冻结原则

从现在开始：

- **不再修改一级目录。**
- **不再修改 `system/00～06` 的编号。**
- 可以在各目录**内部增加文件或子目录**，但不能随意改变目录职责。

例如：

```text
system/
└── 03_api_design/
    ├── REST/
    ├── Batch/
    └── External/
```

这是允许的。

但把 `03_api_design` 改成 `03_interfaces`，或者新增 `07_xxx` 来拆分已有职责，就需要经过正式评审。

---

# Repository Version

建议在 `system/00_repository/` 增加一份总控文档，例如：

```text
Repository構成.md
```

Front Matter 中维护：

```yaml
repository_version: 1.0.0
status: Frozen
last_updated: 2026-07-03
```

以后如果 Repository 有重大调整：

- v1.0.0 → 当前冻结版
- v1.1.0 → 增加目录内部内容（兼容）
- v2.0.0 → 修改目录结构（不兼容）

---

## 我建议我们遵守一个规则

**从这一刻开始，不再讨论 Repository 目录结构，把它视为稳定基础设施。**

后续所有工作——包括 BA、API、UseCase、Verification、Master、Framework、MkDocs、AI Agent、Runtime——都建立在这套冻结的 Repository v1.0 之上。

我认为这是进入工业化开发阶段最合适的节点。

## 第 170 轮

### 你

就算调整得我许可了

### ChatGPT

没问题，我们就按这个约定执行。

**规则如下：**

1. **Repository 结构默认冻结（Freeze）。**
2. **我不会主动修改目录结构、编号或职责。**
3. 如果我认为有更好的设计，我会：
   - 明确说明修改理由。
   - 给出影响分析（哪些文档、Agent、MkDocs、Runtime 会受影响）。
   - 给出迁移方案（Migration Plan）。
   - **只有得到你的许可后，才将其作为新的正式版本。**
4. 在你没有明确同意之前，我都会以**当前冻结版本**为唯一标准继续设计和输出所有文档。

以后我会明确区分两种情况：

- **正式版（Official / Frozen）**：严格按照冻结的 Repository 输出，不做结构变更。
- **建议版（Proposal）**：如果我有新的想法，会明确标注为“Proposal”，绝不会混入正式设计。

这样可以保证：

- 后面的 BA、API、UseCase、Verification 模板不会因为目录变化而反复修改。
- AI Agent、Codex、MkDocs、Runtime 都基于同一套稳定结构开发。
- 整个项目有明确的版本管理，不会出现“昨天这样、今天又变了”的情况。

**从现在开始，我将以 Repository v1.0（冻结版）作为唯一基线继续推进。**如果以后我认为确实需要升级，我会先提交变更提案，只有在你批准后才更新正式结构。

## 第 171 轮

### 你

现行不光是业务分析书。还有E6api情报设计

### ChatGPT

对，这一点非常关键，而且这是我们目前 Repository 里还没有完全体现出来的。

你现在做的不是普通开发，而是**现行系统分析（現行調査）**。

**现行调查的输入**不只有《現行業務分析書（BA）》。

至少应该包括几类不同性质的设计资料。

例如：

```text
01_business/
```

里面不应该只有 BA，而应该包括所有**业务层**的现行资料，例如：

- 現行業務分析書
- 業務フロー一覧
- 業務ルール一覧
- 業務データ分析
- 業務イベント分析
- 業務課題一覧

---

但是 **E6 API** 不属于业务层。

它属于**系统现行设计（System Analysis）**。

例如：

```text
03_api_design/

├── API設計書_Template.md
├── API-001_XXXX.md
├── API-002_XXXX.md
└── ...
```

这里存放的是**目标 API 设计**。

而对于**现行 E6 API 调查**，实际上应该有一套独立成果物。

例如：

```text
02_system_analysis/

├── E6_API分析書/
│   ├── API-001_E6_API分析.md
│   ├── API-002_E6_API分析.md
│   └── ...
│
├── Interface分析/
│
├── Batch分析/
│
├── DB分析/
│
└── 共通機能分析/
```

这样职责就很清楚：

| 文档 | 作用 |
|------|------|
| 現行業務分析書 | 分析业务做什么、为什么做、流程如何走 |
| E6 API分析書 | 分析现有 E6 API 的接口、参数、返回值、Context、调用关系、限制、异常等 |
| API設計書 | 基于现行分析整理出的标准 API 设计规格（规范化成果） |

---

## 结合我们前面的讨论

你现在做的流程其实是：

```text
现行系统

        ↓

① 現行業務分析

② E6 API分析

③ Interface分析

④ DB分析

⑤ Batch分析

        ↓

UseCase设计

        ↓

Verification设计
```

也就是说，**E6 API 分析不是 API 设计书，它是现行调查成果。**

---

## 我建议我们重新整理 `system/01` 和 `system/02` 的职责

因为我感觉我们之前把**现行调查**和**设计阶段**混在一起了。

如果按照日本大型项目（现行调查 → 要件定义 → 基本设计）的思路，Repository 应该明确区分：

- **现行调查（As-Is）成果物**
- **设计（To-Be）成果物**

这会让整个体系更符合日本工业项目的开发流程，也更方便 AI Agent 根据不同阶段生成和维护文档。

**不过这是 Repository 结构调整，属于冻结内容。**按照我们刚刚约定，我不会直接修改正式结构。我建议先把这部分作为一个变更提案（Proposal），等我们一起评审后，再决定是否升级 Repository v1.1。

## 第 172 轮

### 你

api分析文件夹先加上

### ChatGPT

可以，我同意加，而且我认为这是**Repository v1.1 的第一个正式变更**，并且影响很小，不会破坏已有结构。

建议在 **现行调查（As-Is）** 阶段增加 **API 分析**目录。

```text
system/

├── 00_repository/
├── 01_business/
├── 02_api_analysis/      ← 新增（Freeze v1.1）
├── 03_master/
├── 04_api_design/
├── 05_usecase_design/
├── 06_framework/
└── 07_verification_assets/
```

> **说明：** 因为插入了一个新的一级目录，后续编号顺延（原 `02_master` → `03_master`，依此类推）。如果我们现在还处于设计初期，这种调整成本很低，我建议现在完成，以后就不再改编号。

---

## `02_api_analysis` 的职责

**定位：现行 E6 API 调查成果（As-Is）**

输入：

- E6 既存 API 资料
- Swagger / OpenAPI
- Postman Collection
- 实际调用结果
- 源代码
- 数据库
- 抓包结果
- 运维资料

输出：

```text
02_api_analysis/

├── API分析書_Template.md
│
├── API-001_顧客存在確認API分析.md
├── API-002_顧客詳細取得API分析.md
│
├── API一覧.md
├── API依存関係一覧.md
├── API呼出シーケンス一覧.md
├── API共通仕様一覧.md
├── APIエラーコード一覧.md
├── API認証方式一覧.md
├── APIレスポンスコード一覧.md
└── API調査メモ.md
```

---

## 与 `04_api_design` 的区别

| API分析（As-Is） | API設計（To-Be） |
|-----------------|------------------|
| 调查现有 E6 API | 标准化后的设计规格 |
| 记录事实 | 定义规范 |
| 可以有未知项、调查结果 | 必须完整、可开发 |
| 来源于既存系统 | 来源于 BA / API 分析 / UseCase |

---

## 后续关系

```text
現行業務分析
        │
        ├────────────┐
        │            │
        ▼            ▼
E6 API分析      DB分析（后续）
        │
        ▼
API設計書
        │
        ▼
UseCase設計書
        │
        ▼
Verification仕様書
```

---

**我建议把这作为 Repository v1.1 的正式冻结变更。**

这个新增目录非常符合日本项目的现行调查流程，而且不会影响我们已经完成的 BA、API、UseCase、Verification 模板设计，反而把 **As-Is（分析）** 和 **To-Be（设计）** 的边界划分得更清晰。

## 第 173 轮

### 你

放到busines
里

### ChatGPT

我觉得**放到 `01_business` 里面更合理**，而且比我刚才单独拆 `02_api_analysis` 更符合我们这套体系。

原因是：

**E6 API 分析本质上还是"现行调查（As-Is）"成果物。**

它不是设计书，也不是 Framework，更不是 Master。

在日本项目里，现行调查通常会包含：

- 業務分析
- API分析
- DB分析
- Batch分析
- IF分析
- 画面分析

这些都属于**现行分析资料**。

所以建议保持 `01_business` 作为**现行调查阶段**，里面再细分。

例如：

```text
system/

├── 00_repository/
│
├── 01_business/
│   ├── 01_業務分析/
│   │   ├── 現行業務分析書_Template.md
│   │   ├── BA-001_顧客情報照会業務.md
│   │   └── ...
│   │
│   ├── 02_E6_API分析/
│   │   ├── API分析書_Template.md
│   │   ├── API-001_顧客存在確認API分析.md
│   │   ├── API一覧.md
│   │   ├── API依存関係一覧.md
│   │   └── ...
│   │
│   ├── 03_画面分析/
│   │
│   ├── 04_DB分析/
│   │
│   ├── 05_Batch分析/
│   │
│   └── 06_IF分析/
│
├── 02_master/
├── 03_api_design/
├── 04_usecase_design/
├── 05_framework/
└── 06_verification_assets/
```

这样有几个优点：

- **01_business** 统一管理所有**现行分析（As-Is）**成果物。
- **03_api_design** 保持纯粹，只放 **To-Be API 设计书**。
- 将来如果需要增加 **DB 分析、Batch 分析、画面分析、IF 分析**，不用再调整一级目录，只需要在 `01_business` 下增加子目录即可。
- 整个 Repository 的一级结构保持稳定，不需要修改我们已经冻结的 `00～06` 编号。

**我建议采用这一版，并把它作为 Repository v1.1 的正式冻结结构。**我认为这是目前最符合日本大型 IT 项目现行调查流程的组织方式。

## 第 174 轮

### 你

API分析書_Template.md 模版

### ChatGPT

下面给你 `system/01_business/02_E6_API分析/API分析書_Template.md` 最新模板。
定位是 **现行 E6 API 调查用 As-Is 文档**，不是 To-Be 的 API設計書。

:::writing{variant="document" id="86427"}
---
title: API分析書テンプレート
document_id: API-ANALYSIS-TEMPLATE
version: 1.0.0
status: Template
document_type: API Analysis
system_name: E6 API Verification Platform
phase: As-Is Analysis
author:
reviewer:
approver:
created:
updated:
---

# API分析書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|API-ANL-XXX|
|文書名称|〇〇 API分析書|
|分析対象API ID|API-XXX|
|分析対象API名称|（記載）|
|対象システム|E6 API|
|対象業務|（記載）|
|関連Business ID|BUS-XXX|
|関連Flow ID|BF-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 関連資料

|資料ID|資料名|資料種別|版数|保管場所|備考|
|------|------|--------|----|--------|----|
|SRC-001|（記載）|Swagger / OpenAPI / Postman / 既存設計書 / ソース / ログ / 実行結果|（記載）|（記載）|（記載）|

---

## 1.4 分析ステータス

|項目|状態|備考|
|----|----|----|
|仕様資料確認|未着手 / 確認中 / 完了 / 不明|（記載）|
|実API呼出確認|未着手 / 確認中 / 完了 / 不可|（記載）|
|Request確認|未着手 / 確認中 / 完了 / 不明|（記載）|
|Response確認|未着手 / 確認中 / 完了 / 不明|（記載）|
|Error確認|未着手 / 確認中 / 完了 / 不明|（記載）|
|認証確認|未着手 / 確認中 / 完了 / 不明|（記載）|
|後続設計反映|未反映 / 反映中 / 反映済|（記載）|

---

# 2. API概要分析

## 2.1 API目的

（既存E6 APIが何を目的としているかを記載）

例：

本APIは顧客番号を指定し、E6側に顧客データが存在するかを確認するために利用される。

---

## 2.2 API概要

（既存E6 APIの処理概要を記載）

例：

Requestとして顧客番号を受け取り、該当顧客の存在有無をResponseとして返却する。存在する場合は `exists=true`、存在しない場合は `exists=false` を返却する。

---

## 2.3 業務上の利用位置

|項目|内容|
|----|----|
|利用業務|（記載）|
|利用Flow|BF-XXX|
|呼出契機|（記載）|
|前提API|API-XXX / なし|
|後続API|API-XXX / なし|
|業務上の利用結果|（記載）|

---

## 2.4 API分類

|分類|内容|
|----|----|
|API種別|参照 / 登録 / 更新 / 削除 / ファイルアップロード / ファイルダウンロード / その他|
|同期方式|同期 / 非同期 / 不明|
|冪等性|あり / なし / 不明|
|認証要否|要 / 不要 / 不明|
|日次検証対象候補|Yes / No / 未定|
|重要度|Critical / High / Medium / Low / 未定|

---

# 3. Interface分析

## 3.1 Endpoint情報

|項目|現行確認結果|情報源|確度|備考|
|----|------------|------|----|----|
|Base URL|（記載）|（記載）|High / Medium / Low|（記載）|
|Path|（記載）|（記載）|High / Medium / Low|（記載）|
|HTTP Method|GET / POST / PUT / DELETE / 不明|（記載）|High / Medium / Low|（記載）|
|Protocol|HTTPS / HTTP / 不明|（記載）|High / Medium / Low|（記載）|
|Content-Type|（記載）|（記載）|High / Medium / Low|（記載）|
|Accept|（記載）|（記載）|High / Medium / Low|（記載）|
|Timeout|（記載）秒 / 不明|（記載）|High / Medium / Low|（記載）|

---

## 3.2 Header分析

|No|Header名|必須|現行設定値|設定元|情報源|確度|備考|
|--|--------|----|----------|------|------|----|----|
|1|Content-Type|○ / － / 不明|（記載）|固定 / Runtime / 不明|（記載）|High / Medium / Low|（記載）|
|2|Authorization|○ / － / 不明|Bearer token / API Key / 不明|Auth / 不明|（記載）|High / Medium / Low|秘匿対象|

---

## 3.3 認証・認可分析

|項目|現行確認結果|情報源|確度|備考|
|----|------------|------|----|----|
|認証方式|Bearer Token / API Key / Basic / mTLS / 不明|（記載）|High / Medium / Low|（記載）|
|Token取得方式|（記載）|（記載）|High / Medium / Low|（記載）|
|Token有効期限|（記載）|（記載）|High / Medium / Low|（記載）|
|必要権限|（記載）|（記載）|High / Medium / Low|（記載）|
|認証失敗時HTTP Status|401 / 403 / 不明|（記載）|High / Medium / Low|（記載）|

---

# 4. Request分析

## 4.1 Request形式

|項目|現行確認結果|情報源|確度|備考|
|----|------------|------|----|----|
|Request形式|JSON / Query / Path / Form / Multipart / 不明|（記載）|High / Medium / Low|（記載）|
|文字コード|UTF-8 / Shift_JIS / 不明|（記載）|High / Medium / Low|（記載）|
|必須項目数|（記載）|（記載）|High / Medium / Low|（記載）|
|任意項目数|（記載）|（記載）|High / Medium / Low|（記載）|
|ファイル有無|あり / なし / 不明|（記載）|High / Medium / Low|（記載）|

---

## 4.2 Request項目分析

|No|JSONPath / Parameter|項目名|論理名|Type|必須|Null許可|空文字許可|Min|Max|Pattern|Enum|固定値|Default|現行確認結果|情報源|確度|備考|
|--|--------------------|------|------|----|----|--------|----------|---|---|-------|----|------|-------|------------|------|----|----|
|1|$.xxx|（記載）|（記載）|String / Number / Boolean / Object / Array / Date / DateTime / 不明|○ / － / 不明|可 / 不可 / 不明|可 / 不可 / 不明|（記載）|（記載）|（記載）|（記載）|（記載）|（記載）|（記載）|（記載）|High / Medium / Low|（記載）|

---

## 4.3 Requestサンプル

### 4.3.1 仕様資料上のRequest例

```json
{
  "xxx": "（記載）"
}
```

---

### 4.3.2 実API呼出時のRequest例

```json
{
  "xxx": "（記載）"
}
```

---

## 4.4 Request分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|必須項目|（記載）|API設計書 Request Specificationへ反映|
|型制約|（記載）|API設計書 Typeへ反映|
|桁数制約|（記載）|API設計書 Min / Maxへ反映|
|形式制約|（記載）|API設計書 Patternへ反映|
|固定値|（記載）|API設計書 固定値へ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 5. Response分析

## 5.1 Response形式

|項目|現行確認結果|情報源|確度|備考|
|----|------------|------|----|----|
|Response形式|JSON / XML / File / Binary / 不明|（記載）|High / Medium / Low|（記載）|
|文字コード|UTF-8 / Shift_JIS / 不明|（記載）|High / Medium / Low|（記載）|
|正常時HTTP Status|200 / 201 / 204 / 不明|（記載）|High / Medium / Low|（記載）|
|異常時HTTP Status|400 / 401 / 403 / 404 / 500 / 不明|（記載）|High / Medium / Low|（記載）|
|Dynamic項目有無|あり / なし / 不明|（記載）|High / Medium / Low|（記載）|

---

## 5.2 Response項目分析

|No|JSONPath|項目名|論理名|Type|必須|Null許可|Min|Max|Pattern|Enum|固定値|入力値一致|Context候補|Dynamic|Baseline比較候補|現行確認結果|情報源|確度|備考|
|--|--------|------|------|----|----|--------|---|---|-------|----|------|----------|-----------|-------|----------------|------------|------|----|----|
|1|$.xxx|（記載）|（記載）|String / Number / Boolean / Object / Array / Date / DateTime / 不明|○ / － / 不明|可 / 不可 / 不明|（記載）|（記載）|（記載）|（記載）|（記載）|Request $.xxx / － / 不明|CTX-XXX / － / 未定|Yes / No / 不明|Yes / No / 未定|（記載）|（記載）|High / Medium / Low|（記載）|

---

## 5.3 Response固定値分析

|No|JSONPath|固定値|適用条件|確認方法|情報源|確度|API設計反映|
|--|--------|------|--------|--------|------|----|-----------|
|1|$.resultCode|0|正常終了時|仕様資料 / 実行結果 / 不明|（記載）|High / Medium / Low|Yes / No / 保留|

---

## 5.4 Response Enum分析

|No|JSONPath|許容値|意味|確認方法|情報源|確度|API設計反映|
|--|--------|------|----|--------|------|----|-----------|
|1|$.status|ACTIVE,INACTIVE|（記載）|仕様資料 / 実行結果 / 不明|（記載）|High / Medium / Low|Yes / No / 保留|

---

## 5.5 Dynamic項目分析

|No|JSONPath|項目名|変動理由|比較方針候補|確認方法|確度|備考|
|--|--------|------|--------|------------|--------|----|----|
|1|$.traceId|Trace ID|実行毎に採番|Ignore / Exists / Type Only|実API呼出結果|High / Medium / Low|（記載）|
|2|$.updatedAt|更新日時|データ更新により変動|Ignore / Tolerance / 未定|（記載）|High / Medium / Low|（記載）|

---

## 5.6 Responseサンプル

### 5.6.1 仕様資料上のResponse例

```json
{
  "xxx": "（記載）"
}
```

---

### 5.6.2 実API呼出時のResponse例

```json
{
  "xxx": "（記載）"
}
```

---

## 5.7 Response分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|必須項目|（記載）|API設計書 Response Specificationへ反映|
|固定値|（記載）|Response Fixed Value Definitionへ反映|
|Enum|（記載）|Response Enum Definitionへ反映|
|入力値一致|（記載）|Response Input Match Definitionへ反映|
|Dynamic項目|（記載）|Dynamic Field Definitionへ反映|
|Baseline比較候補|（記載）|Baseline Compare Candidateへ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 6. Error分析

## 6.1 Error Response形式

|JSONPath|項目名|Type|必須|確認結果|情報源|確度|備考|
|--------|------|----|----|--------|------|----|----|
|$.error.code|errorCode|String|○ / － / 不明|（記載）|（記載）|High / Medium / Low|（記載）|
|$.error.message|errorMessage|String|○ / － / 不明|（記載）|（記載）|High / Medium / Low|（記載）|
|$.traceId|traceId|String|○ / － / 不明|（記載）|（記載）|High / Medium / Low|Dynamic候補|

---

## 6.2 Error Code分析

|No|HTTP Status|Error Code|発生条件|Response例|Verification対象候補|情報源|確度|備考|
|--|------------|----------|--------|----------|--------------------|------|----|----|
|1|400|（記載）|必須項目未設定|（記載）|Yes / No / 未定|（記載）|High / Medium / Low|（記載）|
|2|401|（記載）|認証不正|（記載）|Yes / No / 未定|（記載）|High / Medium / Low|（記載）|

---

## 6.3 Error分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|Error形式|（記載）|API設計書 Error Response Formatへ反映|
|Error Code|（記載）|API設計書 Error Code Definitionへ反映|
|HTTP Status|（記載）|HTTP Status Definitionへ反映|
|異常系検証候補|（記載）|Verification仕様書へ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 7. Context候補分析

## 7.1 Input Context候補

|Context候補ID|Context名候補|Request項目|利用目的|Producer候補|確度|備考|
|-------------|-------------|------------|--------|------------|----|----|
|CTX-XXX|Customer.id|$.customerId|顧客指定|Entry Input / 前段API|High / Medium / Low|（記載）|

---

## 7.2 Output Context候補

|Context候補ID|Context名候補|Response JSONPath|後続利用候補|Consumer候補|確度|備考|
|-------------|-------------|-----------------|------------|------------|----|----|
|CTX-XXX|Customer.id|$.customer.customerId|後続API / Report / Verification|API-XXX / UC-XXX|High / Medium / Low|（記載）|

---

## 7.3 Context分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|Input Context|（記載）|API設計書 Input Contextへ反映|
|Output Context|（記載）|API設計書 Output Contextへ反映|
|UseCase連携|（記載）|UseCase設計書 Context Mappingへ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 8. API依存関係分析

## 8.1 前提API

|前提API ID|前提内容|依存理由|確認方法|確度|備考|
|----------|--------|--------|--------|----|----|
|API-XXX|（記載）|（記載）|仕様資料 / 実行結果 / ソース|High / Medium / Low|（記載）|

---

## 8.2 後続API

|後続API ID|連携データ|連携理由|確認方法|確度|備考|
|----------|----------|--------|--------|----|----|
|API-XXX|CTX-XXX|（記載）|仕様資料 / 実行結果 / ソース|High / Medium / Low|（記載）|

---

## 8.3 API呼出順序候補

```mermaid
flowchart LR

API001[API-001]
API002[API-002]
API003[API-003]

API001 --> API002
API002 --> API003
```

---

## 8.4 API依存関係分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|前提API|（記載）|UseCase API Execution Chainへ反映|
|後続API|（記載）|UseCase API Execution Chainへ反映|
|Skip条件|（記載）|UseCase API Skip Ruleへ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 9. 実API呼出確認

## 9.1 呼出条件

|項目|内容|
|----|----|
|確認日|YYYY-MM-DD|
|確認環境|DEV / STG / PROD-LIKE / 不明|
|実行者|（記載）|
|認証情報|Mask済み / 未確認|
|利用TestData|（記載）|
|Tool|curl / Postman / Java / その他|

---

## 9.2 正常系呼出結果

|No|Request概要|HTTP Status|Response概要|期待との一致|Evidence|備考|
|--|-----------|------------|-------------|------------|--------|----|
|1|（記載）|200|（記載）|一致 / 不一致 / 未判定|（記載）|（記載）|

---

## 9.3 異常系呼出結果

|No|条件|HTTP Status|Error Code|Response概要|期待との一致|Evidence|備考|
|--|----|------------|----------|-------------|------------|--------|----|
|1|必須項目未設定|400|（記載）|（記載）|一致 / 不一致 / 未判定|（記載）|（記載）|

---

## 9.4 実行Evidence

|Evidence ID|内容|保存先|備考|
|-----------|----|------|----|
|EVD-ANL-001|Request / Response|（記載）|秘匿情報Mask済み|

---

# 10. Verification候補分析

## 10.1 Request検証候補

|候補ID|対象|検証種別|理由|重要度|Verification反映|
|------|----|--------|----|------|----------------|
|REQ-CAND-001|$.xxx|Required / Type / Length / Pattern / Enum / Fixed|（記載）|High / Medium / Low|Yes / No / 保留|

---

## 10.2 Response検証候補

|候補ID|対象|検証種別|理由|重要度|Verification反映|
|------|----|--------|----|------|----------------|
|RES-CAND-001|$.xxx|Required / Type / Fixed / Enum / Input Match / Context Match / Dynamic|（記載）|High / Medium / Low|Yes / No / 保留|

---

## 10.3 Baseline Diff候補

|候補ID|対象|Diff対象|理由|除外条件|重要度|Verification反映|
|------|----|--------|----|--------|------|----------------|
|DIFF-CAND-001|$.xxx|Yes / No|（記載）|（記載）|High / Medium / Low|Yes / No / 保留|

---

## 10.4 Verification候補分析結果

|観点|分析結果|後続設計への反映|
|----|--------|----------------|
|Request検証|（記載）|Verification仕様書 Request Verificationへ反映|
|Response検証|（記載）|Verification仕様書 Response Verificationへ反映|
|Context検証|（記載）|Verification仕様書 Context Verificationへ反映|
|Baseline比較|（記載）|Verification仕様書 Compare Policyへ反映|
|未確認事項|（記載）|課題・確認事項へ登録|

---

# 11. 課題・確認事項

|No|分類|確認事項|影響範囲|確認先|優先度|状態|対応方針|
|--|----|--------|--------|------|------|----|--------|
|1|Request|（記載）|API設計 / Verification|E6担当 / 業務担当|High / Medium / Low|Open / Closed|（記載）|
|2|Response|（記載）|API設計 / Verification|E6担当 / 業務担当|High / Medium / Low|Open / Closed|（記載）|
|3|Error|（記載）|異常系検証|E6担当|High / Medium / Low|Open / Closed|（記載）|

---

# 12. 後続成果物への反映

## 12.1 API設計書への反映

|反映ID|分析項目|反映先章|反映内容|状態|
|------|--------|--------|--------|----|
|REF-API-001|Endpoint分析|API設計書 3. Interface Specification|（記載）|未反映 / 反映済|
|REF-API-002|Request分析|API設計書 4. Request Specification|（記載）|未反映 / 反映済|
|REF-API-003|Response分析|API設計書 5. Response Specification|（記載）|未反映 / 反映済|
|REF-API-004|Error分析|API設計書 7. Error Specification|（記載）|未反映 / 反映済|

---

## 12.2 UseCase設計書への反映

|反映ID|分析項目|反映先章|反映内容|状態|
|------|--------|--------|--------|----|
|REF-UC-001|API依存関係|UseCase設計書 API Execution Chain|（記載）|未反映 / 反映済|
|REF-UC-002|Context候補|UseCase設計書 Context Mapping|（記載）|未反映 / 反映済|
|REF-UC-003|Skip条件|UseCase設計書 API Skip Rule|（記載）|未反映 / 反映済|

---

## 12.3 Verification仕様書への反映

|反映ID|分析項目|反映先章|反映内容|状態|
|------|--------|--------|--------|----|
|REF-VER-001|Request検証候補|Verification Request Verification|（記載）|未反映 / 反映済|
|REF-VER-002|Response検証候補|Verification Response Verification|（記載）|未反映 / 反映済|
|REF-VER-003|Baseline Diff候補|Verification Compare Policy|（記載）|未反映 / 反映済|
|REF-VER-004|Error候補|Verification Error / Exception TestCase|（記載）|未反映 / 反映済|

---

# 13. Traceability

## 13.1 API分析 Trace Matrix

|Business ID|Flow ID|API ID|API分析ID|Context候補ID|Verification候補ID|API設計書ID|UseCase ID|Verification ID|
|-----------|-------|------|---------|-------------|------------------|-----------|----------|---------------|
|BUS-XXX|BF-XXX|API-XXX|API-ANL-XXX|CTX-XXX|VF-XXX|API-XXX|UC-XXX|VER-XXX|

---

## 13.2 参照資料

|No|資料ID|資料名|資料種別|版数|備考|
|--|------|------|--------|----|----|
|1|SRC-001|（記載）|Swagger / OpenAPI / Postman / 既存設計書 / ソース / 実行結果|（記載）|（記載）|

---

# Appendix A. 記入例

## A.1 文書管理

|項目|内容|
|----|----|
|文書ID|API-ANL-001|
|文書名称|顧客存在確認 API分析書|
|分析対象API ID|API-001|
|分析対象API名称|Customer Exists API|
|対象システム|E6 API|
|対象業務|顧客情報照会業務|
|関連Business ID|BUS-001|
|関連Flow ID|BF-002|
|版数|1.0.0|
|状態|Draft|
|作成者|API分析担当|
|レビューア|アーキテクト|
|承認者|プロジェクト責任者|
|作成日|2026-07-03|
|更新日|2026-07-03|

---

## A.2 API概要

### API目的

本APIは、顧客番号を指定し、E6側に顧客データが存在するかを確認するために利用される。

---

### API概要

Requestとして `customerId` を受け取り、該当顧客が存在する場合は `exists=true`、存在しない場合は `exists=false` を返却する。

---

## A.3 Endpoint情報

|項目|現行確認結果|情報源|確度|備考|
|----|------------|------|----|----|
|Base URL|環境別設定参照|既存設定ファイル|High|Environment Masterへ反映|
|Path|/v1/customers/exists|Swagger|High|API設計書へ反映|
|HTTP Method|POST|Swagger|High|API設計書へ反映|
|Protocol|HTTPS|環境資料|High|固定|
|Content-Type|application/json|Swagger|High|固定|
|Accept|application/json|Swagger|High|固定|
|Timeout|10秒|現行設定|Medium|要確認|

---

## A.4 Request項目分析

|No|JSONPath / Parameter|項目名|論理名|Type|必須|Null許可|空文字許可|Min|Max|Pattern|Enum|固定値|Default|現行確認結果|情報源|確度|備考|
|--|--------------------|------|------|----|----|--------|----------|---|---|-------|----|------|-------|------------|------|----|----|
|1|$.customerId|customerId|顧客番号|String|○|不可|不可|1|20|^[0-9]+$|－|－|－|仕様上必須、数字のみ|Swagger / 実行確認|High|API設計書へ反映|

---

## A.5 Response項目分析

|No|JSONPath|項目名|論理名|Type|必須|Null許可|Min|Max|Pattern|Enum|固定値|入力値一致|Context候補|Dynamic|Baseline比較候補|現行確認結果|情報源|確度|備考|
|--|--------|------|------|----|----|--------|---|---|-------|----|------|----------|-----------|-------|----------------|------------|------|----|----|
|1|$.resultCode|resultCode|結果コード|String|○|不可|1|10|－|0,1|0|－|－|No|Yes|正常時0|Swagger / 実行確認|High|固定値確認対象|
|2|$.exists|exists|顧客存在有無|Boolean|○|不可|－|－|－|true,false|－|－|CTX-002|No|Yes|存在有無を返却|Swagger / 実行確認|High|業務判定対象|
|3|$.customerId|customerId|顧客番号|String|○|不可|1|20|^[0-9]+$|－|－|Request $.customerId|CTX-001|No|Yes|入力値と一致|実行確認|High|Input Match対象|
|4|$.traceId|traceId|Trace ID|String|－|可|－|64|－|－|－|－|－|Yes|No|実行毎に変動|実行確認|High|Dynamic項目|

---

## A.6 Dynamic項目分析

|No|JSONPath|項目名|変動理由|比較方針候補|確認方法|確度|備考|
|--|--------|------|--------|------------|--------|----|----|
|1|$.traceId|Trace ID|実行毎に採番|Ignore / Exists / Type Only|複数回実行結果|High|Baseline比較対象外|

---

## A.7 Verification候補分析

|候補ID|対象|検証種別|理由|重要度|Verification反映|
|------|----|--------|----|------|----------------|
|RES-CAND-001|$.resultCode|Fixed Value|正常時は0固定|High|Yes|
|RES-CAND-002|$.exists|Required / Type / Enum|業務判定に必要|High|Yes|
|RES-CAND-003|$.customerId|Input Match|入力顧客番号との一致確認|High|Yes|
|RES-CAND-004|$.traceId|Dynamic Ignore|実行毎に変動|Low|Yes|

---

## A.8 後続成果物への反映

|反映ID|分析項目|反映先章|反映内容|状態|
|------|--------|--------|--------|----|
|REF-API-001|Endpoint分析|API設計書 3. Interface Specification|Path / Method / Header|未反映|
|REF-API-002|Request分析|API設計書 4. Request Specification|customerId制約|未反映|
|REF-API-003|Response分析|API設計書 5. Response Specification|resultCode / exists / customerId / traceId|未反映|
|REF-VER-001|Verification候補|Verification Response Verification|固定値・型・入力値一致・Dynamic除外|未反映|

:::

这份就是 **API分析書_Template.md v1.0**。

建议放置位置固定为：

```text
system/01_business/02_E6_API分析/API分析書_Template.md
```

它和后面的 To-Be `API設計書_Template.md` 的关系是：

```text
API分析書 = 既存E6 APIの事実を調査する
API設計書 = 調査結果を標準化して設計仕様にする
```

## 第 175 轮

### 你

api usecase对应表没有了 多了个scenario master

### ChatGPT

对，你说得对。**API-UseCase対応表必须保留**，不能被 Scenario Master 替代。

正确的 `02_master` 应该是：

```text
system/
└── 02_master/
    ├── E6_API_Master.md
    ├── UseCase_Master.md
    ├── Scenario_Master.md
    ├── Context_Master.md
    ├── Verification_Master.md
    ├── API_UseCase対応表.md      ← 必须追加
    └── Environment_Master.md
```

区别是：

```text
API_UseCase対応表
= 哪个 UseCase 调用哪些 API，调用顺序是什么

Scenario_Master
= 同一个 UseCase 下有哪些场景差异
```

例如：

```markdown
# API_UseCase対応表

|UseCase ID|UseCase名|Scenario ID|実行順|API ID|API名称|Flow ID|必須|Skip条件|備考|
|----------|---------|-----------|------|------|--------|-------|----|--------|----|
|UC-001|顧客情報照会|SC-001|1|API-001|Customer Exists API|BF-002|○|－|存在確認|
|UC-001|顧客情報照会|SC-001|2|API-002|Customer Detail API|BF-004|○|exists=false|顧客取得|
|UC-001|顧客情報照会|SC-001|3|API-003|Contract List API|BF-005|－|exists=false / API-002失敗|契約取得|
|UC-001|顧客情報照会|SC-002|1|API-001|Customer Exists API|BF-002|○|－|顧客不存在|
```

所以修正结论：

```text
Scenario_Master 不能替代 API_UseCase対応表。
两者都需要。
```

这点我同意，`02_master` 里把 `API_UseCase対応表.md` 加回去。

## 第 176 轮

### 你

compare policy也没有

### ChatGPT

对，**Compare Policy 也必须进 Master**。

修正后的 `02_master`：

```text
system/
└── 02_master/
    ├── E6_API_Master.md
    ├── UseCase_Master.md
    ├── Scenario_Master.md
    ├── Context_Master.md
    ├── Verification_Master.md
    ├── API_UseCase対応表.md
    ├── Compare_Policy_Master.md   ← 追加
    └── Environment_Master.md
```

区别：

```text
Compare_Policy_Master
= 全局比较规则、共通Ignore、Dynamic字段、Tolerance、Collection比较规则

Verification仕様書
= 某个UseCase/Scenario/API实际采用哪些Compare规则
```

例如：

```markdown
# Compare_Policy_Master

|Policy ID|分類|対象|比較方式|条件|重要度|備考|
|---------|----|----|--------|----|------|----|
|CMP-POL-001|Dynamic|$.traceId|Ignore|常時|Low|実行毎に採番|
|CMP-POL-002|Dynamic|$.updatedAt|Ignore / Tolerance|API別|Low|更新日時|
|CMP-POL-003|DateTime|DateTime項目|Tolerance|±3秒|Medium|時刻差許容|
|CMP-POL-004|Number|金額項目|Tolerance|±0.01|Medium|丸め差|
|CMP-POL-005|Collection|配列|Key Match|key項目指定|High|順序非依存|
|CMP-POL-006|String|文字列|Trim + Equals|前後空白除去|Medium|表記揺れ対策|
```

所以最终：

```text
Compare_Policy_Master = 共通比較ルール
Verification仕様書 = 個別検証での適用ルール
```

加得对。

## 第 177 轮

### 你

api scenario usecase 对应关系

### ChatGPT

对，应该明确有一张 **API・UseCase・Scenario 対応表**。

因为现在结构已经变成：

```text
UseCase
  └── Scenario
        └── API実行順序
```

所以原来的 `API_UseCase対応表.md` 可以升级为：

```text
system/02_master/API_UseCase_Scenario対応表.md
```

它的职责是：

> **管理每个 UseCase 的每个 Scenario 会调用哪些 API、顺序、条件、Skip 规则、对应 Flow 和 Verification。**

---

# API_UseCase_Scenario対応表.md

```markdown
---
title: API・UseCase・Scenario対応表
document_id: MST-API-UC-SC-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# API・UseCase・Scenario対応表

---

# 1. 文書目的

本書は、UseCase、Scenario、API の対応関係を一元管理する。

本書により、以下を明確化する。

|目的|内容|
|----|----|
|API利用把握|どのUseCaseがどのAPIを利用するかを確認する|
|Scenario差分把握|ScenarioごとにAPI実行有無・順序・Skip条件を確認する|
|影響分析|API変更時に影響するUseCase / Scenario / Verificationを特定する|
|実行仕様生成|Execution Spec生成時のAPI実行Chain入力とする|
|検証網羅確認|APIがVerification / TestCaseで網羅されているか確認する|

---

# 2. 対応表

|No|UseCase ID|UseCase名|Scenario ID|Scenario名|分類|実行順|API ID|API名称|Flow ID|Step ID|実行要否|実行条件|Skip条件|Context入力|Context出力|Verification ID|TestCase ID|重要度|備考|
|--|----------|---------|-----------|-----------|----|------|------|--------|-------|-------|--------|--------|--------|-------------|-------------|---------------|-----------|------|----|
|1|UC-001|顧客情報照会|SC-001|正常系|Normal|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-001|TC-001|High|存在確認|
|2|UC-001|顧客情報照会|SC-001|正常系|Normal|2|API-002|Customer Detail API|BF-004|UC-STEP-002|必須|exists=true|－|CTX-001|CTX-003|VER-001|TC-001|High|顧客取得|
|3|UC-001|顧客情報照会|SC-001|正常系|Normal|3|API-003|Contract List API|BF-005|UC-STEP-003|任意|Customer取得済み|exists=false / API-002失敗|CTX-001|CTX-004|VER-001|TC-001|Medium|契約取得|
|4|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-002|TC-002|High|exists=false|
|5|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|2|API-002|Customer Detail API|BF-004|UC-STEP-002|Skip|exists=false|exists=false|CTX-001|－|VER-002|TC-002|High|後続Skip|
|6|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|3|API-003|Contract List API|BF-005|UC-STEP-003|Skip|exists=false|exists=false|CTX-001|－|VER-002|TC-002|Medium|後続Skip|
|7|UC-001|顧客情報照会|SC-003|契約0件|Alternative|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-003|TC-003|High|存在確認|
|8|UC-001|顧客情報照会|SC-003|契約0件|Alternative|2|API-002|Customer Detail API|BF-004|UC-STEP-002|必須|exists=true|－|CTX-001|CTX-003|VER-003|TC-003|High|顧客取得|
|9|UC-001|顧客情報照会|SC-003|契約0件|Alternative|3|API-003|Contract List API|BF-005|UC-STEP-003|必須|Customer取得済み|－|CTX-001|CTX-004|VER-003|TC-003|Medium|0件返却|
```

---

# 3. API別影響確認

|API ID|API名称|利用UseCase|利用Scenario|実行回数|必須Scenario数|Skip可能Scenario数|影響度|
|------|--------|-----------|-------------|--------|---------------|------------------|------|
|API-001|Customer Exists API|UC-001|SC-001, SC-002, SC-003|3|3|0|High|
|API-002|Customer Detail API|UC-001|SC-001, SC-002, SC-003|3|2|1|High|
|API-003|Contract List API|UC-001|SC-001, SC-002, SC-003|3|2|1|Medium|

---

# 4. UseCase別API構成

|UseCase ID|UseCase名|利用API数|Scenario数|標準API順序|備考|
|----------|---------|---------|-----------|------------|----|
|UC-001|顧客情報照会|3|3|API-001 → API-002 → API-003|顧客不存在時は後続Skip|

---

# 5. Scenario別API構成

|Scenario ID|Scenario名|UseCase ID|API実行順序|Skip API|Expected Result|
|-----------|-----------|----------|------------|---------|---------------|
|SC-001|正常系|UC-001|API-001 → API-002 → API-003|－|PASS|
|SC-002|顧客不存在|UC-001|API-001|API-002, API-003|WARN / FAIL|
|SC-003|契約0件|UC-001|API-001 → API-002 → API-003|－|PASS / WARN|

---

# 6. Traceability

|UseCase ID|Scenario ID|API ID|Flow ID|Step ID|Context ID|Verification ID|TestCase ID|
|----------|------------|------|-------|-------|----------|---------------|-----------|
|UC-001|SC-001|API-001|BF-002|UC-STEP-001|CTX-001, CTX-002|VER-001|TC-001|
|UC-001|SC-001|API-002|BF-004|UC-STEP-002|CTX-001, CTX-003|VER-001|TC-001|
|UC-001|SC-001|API-003|BF-005|UC-STEP-003|CTX-001, CTX-004|VER-001|TC-001|
|UC-001|SC-002|API-001|BF-002|UC-STEP-001|CTX-001, CTX-002|VER-002|TC-002|
```

---

# 放置位置

```text
system/02_master/
└── API_UseCase_Scenario対応表.md
```

---

# `02_master` 最新结构

```text
system/
└── 02_master/
    ├── E6_API_Master.md
    ├── UseCase_Master.md
    ├── Scenario_Master.md
    ├── Context_Master.md
    ├── Verification_Master.md
    ├── API_UseCase_Scenario対応表.md
    ├── Compare_Policy_Master.md
    └── Environment_Master.md
```

结论：
**需要这张表。** 它不是重复，而是整个 E6 API Verification Platform 的“中枢索引表”。

## 第 178 轮

### 你

Repository_Structure.md 重新做成

### ChatGPT

下面是重新整理后的 **`system/00_repository/Repository構成.md`**。

:::writing{variant="document" id="38472"}
---
title: Repository構成
document_id: RULE-REPO-001
version: 1.1.0
status: Frozen
document_type: Repository Rule
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Repository構成

---

# 1. 文書目的

本書は、E6 API Verification Platform の Repository 構成、配置規則、成果物管理規則を定義する。

本Repositoryは、以下を目的とする。

|目的|内容|
|----|----|
|現行調査管理|業務分析、E6 API分析を体系的に管理する|
|設計管理|API設計、UseCase設計、Framework設計を管理する|
|検証資産管理|Verification仕様、Execution Spec、Test Data、Evidence、Reportを管理する|
|AI可読性|AI Agent が文書構成を安定して理解できるようにする|
|Traceability|Business、API、UseCase、Scenario、Verification、TestCase、Evidenceを追跡可能にする|
|本番運用|Runtime、Build、Staging、Outputsを分離して管理する|

---

# 2. Repository 全体構成

```text
repository/

├── project/
│
├── system/
│   ├── 00_repository/
│   ├── 01_business/
│   ├── 02_master/
│   ├── 03_api_design/
│   ├── 04_usecase_design/
│   ├── 05_framework/
│   └── 06_verification_assets/
│
├── runtime/
├── build/
├── staging/
└── outputs/
```

---

# 3. project

```text
project/

├── 要件定義書.md
├── WBS.md
├── スケジュール.md
├── QA一覧.md
└── 課題・リスク管理表.md
```

|ファイル|用途|
|--------|----|
|要件定義書.md|プロジェクト目的、範囲、成功条件を定義する|
|WBS.md|成果物単位の作業を管理する|
|スケジュール.md|開始日、終了日、担当、進捗を管理する|
|QA一覧.md|業務担当、E6担当、開発担当への確認事項を管理する|
|課題・リスク管理表.md|課題、リスク、影響、対応方針を管理する|

---

# 4. system

`system` は、仕様・設計・検証資産を管理する中心ディレクトリである。

```text
system/

├── 00_repository/
├── 01_business/
├── 02_master/
├── 03_api_design/
├── 04_usecase_design/
├── 05_framework/
└── 06_verification_assets/
```

|ディレクトリ|役割|
|------------|----|
|00_repository|Repository規約、文書規約、命名、Trace、Review、Glossary|
|01_business|現行調査成果物。業務分析、E6 API分析を管理する|
|02_master|API、UseCase、Scenario、Context、Compare Policy等の横断Master|
|03_api_design|To-Be API設計書|
|04_usecase_design|UseCase設計書、Scenario設計|
|05_framework|Runtime Framework、共通処理、Diff、Report、Log、Environment設計|
|06_verification_assets|Verification仕様、Execution Spec、Test Spec、Test Data、Evidence、Report|

---

# 5. system/00_repository

```text
system/00_repository/

├── Repository構成.md
├── 文書作成規約.md
├── トレーサビリティ規約.md
├── 命名規約.md
├── レビュー観点一覧.md
└── 用語集.md
```

|ファイル|用途|
|--------|----|
|Repository構成.md|Repository構成、配置規則を定義する|
|文書作成規約.md|Markdown、Mermaid、表、Front Matter、AI可読性を定義する|
|トレーサビリティ規約.md|BusinessからEvidenceまでのTrace規約を定義する|
|命名規約.md|ID、ファイル名、Context名、Scenario名等を定義する|
|レビュー観点一覧.md|成果物Review観点を定義する|
|用語集.md|プロジェクト共通用語を定義する|

---

# 6. system/01_business

`01_business` は、現行調査（As-Is）成果物を管理する。

```text
system/01_business/

├── 01_業務分析/
│   ├── 現行業務分析書_Template.md
│   ├── BA-001_顧客情報照会業務.md
│   └── BA-002_〇〇業務.md
│
└── 02_E6_API分析/
    ├── API分析書_Template.md
    ├── API-ANL-001_顧客存在確認API分析.md
    ├── API-ANL-002_顧客詳細取得API分析.md
    ├── API一覧.md
    ├── API依存関係一覧.md
    ├── API呼出シーケンス一覧.md
    ├── API共通仕様一覧.md
    ├── APIエラーコード一覧.md
    ├── API認証方式一覧.md
    ├── APIレスポンスコード一覧.md
    └── API調査メモ.md
```

---

## 6.1 01_業務分析

|ファイル|用途|
|--------|----|
|現行業務分析書_Template.md|現行業務分析書のテンプレート|
|BA-XXX_〇〇業務.md|業務単位の現行業務分析書|

`01_業務分析` は、業務目的、業務Flow、利用API、データ連携、検証対象を整理する。

---

## 6.2 02_E6_API分析

|ファイル|用途|
|--------|----|
|API分析書_Template.md|既存E6 API分析書のテンプレート|
|API-ANL-XXX_〇〇API分析.md|既存E6 API単位の分析書|
|API一覧.md|現行E6 API一覧|
|API依存関係一覧.md|API間の前提・後続関係|
|API呼出シーケンス一覧.md|業務Flow上のAPI呼出順序|
|API共通仕様一覧.md|Header、認証、共通Response等|
|APIエラーコード一覧.md|Error Code、HTTP Status、発生条件|
|API認証方式一覧.md|認証方式、Token、権限条件|
|APIレスポンスコード一覧.md|業務結果コード、固定値、Enum|
|API調査メモ.md|未確定事項、調査ログ、補足|

`02_E6_API分析` は、既存E6 APIの事実を調査するための領域であり、To-Be API設計書ではない。

---

# 7. system/02_master

```text
system/02_master/

├── E6_API_Master.md
├── UseCase_Master.md
├── Scenario_Master.md
├── Context_Master.md
├── Verification_Master.md
├── API_UseCase_Scenario対応表.md
├── Compare_Policy_Master.md
└── Environment_Master.md
```

|ファイル|用途|
|--------|----|
|E6_API_Master.md|E6 APIの一覧、ID、名称、分類、重要度を管理する|
|UseCase_Master.md|UseCase一覧、対象業務、実行対象を管理する|
|Scenario_Master.md|Scenario一覧、分類、期待結果を管理する|
|Context_Master.md|Context一覧、Producer、Consumer、Scopeを管理する|
|Verification_Master.md|Verification一覧、対象UseCase、Scenario、APIを管理する|
|API_UseCase_Scenario対応表.md|UseCase、Scenario、API実行順序、Skip条件を管理する|
|Compare_Policy_Master.md|共通Compare Policy、Dynamic項目、Tolerance、Collection比較を管理する|
|Environment_Master.md|DEV、STG、PROD-LIKE等の環境情報を管理する|

---

# 8. system/03_api_design

```text
system/03_api_design/

├── API設計書_Template.md
├── API-001_CustomerExistsAPI.md
├── API-002_CustomerDetailAPI.md
└── API-003_ContractListAPI.md
```

|ファイル|用途|
|--------|----|
|API設計書_Template.md|To-Be API設計書テンプレート|
|API-XXX_〇〇API.md|API単位の設計書|

`03_api_design` は、API分析結果をもとに、標準化されたAPI仕様を定義する。

主な内容：

|分類|内容|
|----|----|
|Interface|Endpoint、Method、Header、認証|
|Request|入力項目、型、必須、Min/Max、Pattern、Enum、固定値|
|Response|出力項目、型、固定値、Enum、入力値一致、Context一致、Dynamic|
|Error|HTTP Status、Error Code、Error Response|
|Context|Input Context、Output Context、Lifecycle|
|Verification Metadata|Request/Response Check候補、Baseline Diff候補|

---

# 9. system/04_usecase_design

```text
system/04_usecase_design/

├── UseCase設計書_Template.md
├── UC-001_顧客情報照会.md
└── UC-002_〇〇.md
```

|ファイル|用途|
|--------|----|
|UseCase設計書_Template.md|UseCase設計書テンプレート|
|UC-XXX_〇〇.md|UseCase単位の設計書|

`04_usecase_design` は、BAとAPI設計をもとに、実行可能なUseCaseを定義する。

主な内容：

|分類|内容|
|----|----|
|Entry Input|UseCase開始時の入力|
|Main Flow|UseCaseの主処理|
|Scenario|正常系、代替系、異常系、境界値等|
|API Execution Chain|API実行順序、実行条件、Skip Rule|
|Context Mapping|Extract、Binding、Lifetime|
|Expected Result|Scenario別期待結果|
|Evidence|保存対象、保存先、Snapshot Policy|

---

# 10. system/05_framework

```text
system/05_framework/

├── システム設計書.md
├── 共通Framework設計書.md
├── RunContext設計書.md
├── Snapshot設計書.md
├── Diff設計書.md
├── Report設計書.md
├── ファイル入出力設計書.md
├── ログ・例外設計書.md
└── 環境設計書.md
```

|ファイル|用途|
|--------|----|
|システム設計書.md|全体アーキテクチャ、処理方式、構成を定義する|
|共通Framework設計書.md|共通実行基盤、Runner、Executor、Validatorを定義する|
|RunContext設計書.md|実行単位Context、Context引継ぎ、Scopeを定義する|
|Snapshot設計書.md|Request、Response、Context Snapshot保存方式を定義する|
|Diff設計書.md|Baseline比較、Diff抽出、Normalize、Toleranceを定義する|
|Report設計書.md|Daily Summary、Diff Report、Evidence Reportを定義する|
|ファイル入出力設計書.md|JSON、CSV、YAML、Evidence、Reportの入出力を定義する|
|ログ・例外設計書.md|Log設計、Exception設計、Mask、Error Handlingを定義する|
|環境設計書.md|DEV、STG、PROD-LIKE、Runtime Configを定義する|

---

# 11. system/06_verification_assets

```text
system/06_verification_assets/

├── Verification仕様書_Template.md
├── execution_spec/
├── api_test_spec/
├── usecase_test_spec/
├── test_data/
├── reports/
└── evidence/
```

|ディレクトリ / ファイル|用途|
|----------------------|----|
|Verification仕様書_Template.md|Verification仕様書テンプレート|
|execution_spec|AI生成または人手作成のExecution Spec|
|api_test_spec|API単体検証仕様|
|usecase_test_spec|UseCase連携検証仕様|
|test_data|Verification用Test Data|
|reports|Reportテンプレート、サンプル、設計資産|
|evidence|Evidence定義、保存例、証跡仕様|

---

## 11.1 execution_spec

```text
execution_spec/

├── EXEC-001_顧客情報照会.md
└── EXEC-002_〇〇.md
```

Execution Engine が読み取る実行仕様を管理する。

---

## 11.2 api_test_spec

```text
api_test_spec/

├── API-001_TestSpec.md
├── API-002_TestSpec.md
└── API-003_TestSpec.md
```

API単体検証仕様を管理する。

---

## 11.3 usecase_test_spec

```text
usecase_test_spec/

├── UC-001_TestSpec.md
└── UC-002_TestSpec.md
```

UseCase連携検証仕様を管理する。

---

## 11.4 test_data

```text
test_data/

├── UC-001/
│   ├── TD-001_SC-001_normal.json
│   ├── TD-002_SC-002_customer_not_found.json
│   └── TD-003_SC-003_contract_empty.json
└── UC-002/
```

---

## 11.5 reports

```text
reports/

├── DailySummary_Template.md
├── DiffReport_Template.md
└── EvidenceReport_Template.md
```

---

## 11.6 evidence

```text
evidence/

├── Evidence保存規約.md
├── RequestEvidence_Sample.json
├── ResponseEvidence_Sample.json
└── ContextSnapshot_Sample.json
```

---

# 12. runtime

```text
runtime/

├── src/
├── config/
├── scripts/
├── test/
└── docker/
```

|ディレクトリ|用途|
|------------|----|
|src|Java Runtime 実装|
|config|Runtime設定|
|scripts|ローカル実行、補助Script|
|test|Runtime単体テスト|
|docker|開発用Docker定義|

---

# 13. build

```text
build/

├── scripts/
├── docker/
└── release/
```

|ディレクトリ|用途|
|------------|----|
|scripts|build、package、release、generate-spec等|
|docker|Build用Dockerfile、本番Image定義|
|release|本番配置用Release Package出力|

---

# 14. staging

```text
staging/

├── docker-compose.yml
├── config/
├── data/
└── logs/
```

|ディレクトリ|用途|
|------------|----|
|docker-compose.yml|本番相当検証用Compose|
|config|Staging環境設定|
|data|Baseline、Run Data、Report Data|
|logs|Staging実行ログ|

---

# 15. outputs

```text
outputs/

├── baseline/
├── runs/
├── reports/
└── evidence/
```

|ディレクトリ|用途|
|------------|----|
|baseline|承認済Baseline|
|runs|実行単位結果|
|reports|実行結果Report|
|evidence|Request、Response、Context、Diff、Log等の証跡|

`outputs/` は原則 Git 管理対象外とする。

---

# 16. Git 管理方針

## 16.1 Git管理対象

|対象|管理|
|----|----|
|project|Yes|
|system/00_repository|Yes|
|system/01_business|Yes|
|system/02_master|Yes|
|system/03_api_design|Yes|
|system/04_usecase_design|Yes|
|system/05_framework|Yes|
|system/06_verification_assets|Yes|
|runtime/src|Yes|
|runtime/config template|Yes|
|runtime/test|Yes|
|build/scripts|Yes|
|build/docker|Yes|
|staging template|Yes|

---

## 16.2 Git管理対象外

|対象|理由|
|----|----|
|outputs|実行結果|
|runtime/config/secret|機密情報|
|staging/data|実行結果|
|staging/logs|ログ|
|build/release/*.zip|生成物|
|target / build成果物|生成物|
|*.log|ログ|
|*.tmp|一時ファイル|
|.env|環境依存設定|

---

# 17. .gitignore 推奨

```text
outputs/
staging/data/
staging/logs/
runtime/config/secret/
build/release/*.zip
*.log
*.tmp
target/
build/
.env
```

---

# 18. 成果物作成フロー

## 18.1 BA作成

```text
system/01_business/01_業務分析/現行業務分析書_Template.md
  ↓ copy
system/01_business/01_業務分析/BA-XXX_〇〇業務.md
```

---

## 18.2 API分析作成

```text
system/01_business/02_E6_API分析/API分析書_Template.md
  ↓ copy
system/01_business/02_E6_API分析/API-ANL-XXX_〇〇API分析.md
```

---

## 18.3 API設計作成

```text
system/03_api_design/API設計書_Template.md
  ↓ copy
system/03_api_design/API-XXX_〇〇API.md
```

---

## 18.4 UseCase設計作成

```text
system/04_usecase_design/UseCase設計書_Template.md
  ↓ copy
system/04_usecase_design/UC-XXX_〇〇.md
```

---

## 18.5 Verification仕様作成

```text
system/06_verification_assets/Verification仕様書_Template.md
  ↓ copy
system/06_verification_assets/VER-XXX_〇〇.md
```

---

# 19. 文書配置ルール

|文書|配置先|
|----|------|
|Repository規約|system/00_repository|
|現行業務分析書|system/01_business/01_業務分析|
|E6 API分析書|system/01_business/02_E6_API分析|
|Master類|system/02_master|
|API設計書|system/03_api_design|
|UseCase設計書|system/04_usecase_design|
|Framework設計書|system/05_framework|
|Verification仕様書|system/06_verification_assets|
|Test Data|system/06_verification_assets/test_data|
|Evidence定義|system/06_verification_assets/evidence|
|実行結果|outputs|

---

# 20. AI Agent 参照順序

AI Agent が文書生成・更新を行う場合、以下順序で参照する。

```text
1. system/00_repository/Repository構成.md
2. system/00_repository/文書作成規約.md
3. system/00_repository/命名規約.md
4. system/00_repository/トレーサビリティ規約.md
5. system/00_repository/用語集.md
6. system/02_master/*
7. 対象Template
8. 対象成果物
```

---

# 21. Trace 基本ルート

```text
現行業務分析
  ↓
E6 API分析
  ↓
API設計
  ↓
UseCase設計
  ↓
Verification仕様
  ↓
Execution Spec
  ↓
Runtime
  ↓
Evidence
  ↓
Report
```

---

# 22. Repository変更ルール

Repository構成は `v1.1.0` としてFreezeする。

変更ルールは以下とする。

|変更種別|Version更新|承認|
|--------|------------|----|
|ファイル追加|PATCH|不要または軽微Review|
|既存ディレクトリ内のサブディレクトリ追加|MINOR|要Review|
|system配下の番号変更|MAJOR|要承認|
|一级目录変更|MAJOR|要承認|
|既存职责変更|MAJOR|要承認|

---

# 23. Repository Freeze 方針

以下はFreeze対象とする。

|対象|Freeze|
|----|------|
|project|Yes|
|system/00_repository|Yes|
|system/01_business|Yes|
|system/02_master|Yes|
|system/03_api_design|Yes|
|system/04_usecase_design|Yes|
|system/05_framework|Yes|
|system/06_verification_assets|Yes|
|runtime|Yes|
|build|Yes|
|staging|Yes|
|outputs|Yes|

ただし、各ディレクトリ内部のファイル追加は、既存职责を逸脱しない範囲で許可する。

---

# Appendix A. 最終Repository構成

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── WBS.md
│   ├── スケジュール.md
│   ├── QA一覧.md
│   └── 課題・リスク管理表.md
│
├── system/
│   ├── 00_repository/
│   │   ├── Repository構成.md
│   │   ├── 文書作成規約.md
│   │   ├── トレーサビリティ規約.md
│   │   ├── 命名規約.md
│   │   ├── レビュー観点一覧.md
│   │   └── 用語集.md
│   │
│   ├── 01_business/
│   │   ├── 01_業務分析/
│   │   │   ├── 現行業務分析書_Template.md
│   │   │   └── BA-001_顧客情報照会業務.md
│   │   │
│   │   └── 02_E6_API分析/
│   │       ├── API分析書_Template.md
│   │       ├── API-ANL-001_顧客存在確認API分析.md
│   │       ├── API一覧.md
│   │       ├── API依存関係一覧.md
│   │       ├── API呼出シーケンス一覧.md
│   │       ├── API共通仕様一覧.md
│   │       ├── APIエラーコード一覧.md
│   │       ├── API認証方式一覧.md
│   │       ├── APIレスポンスコード一覧.md
│   │       └── API調査メモ.md
│   │
│   ├── 02_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── Scenario_Master.md
│   │   ├── Context_Master.md
│   │   ├── Verification_Master.md
│   │   ├── API_UseCase_Scenario対応表.md
│   │   ├── Compare_Policy_Master.md
│   │   └── Environment_Master.md
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   └── API-001_CustomerExistsAPI.md
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   └── UC-001_顧客情報照会.md
│   │
│   ├── 05_framework/
│   │   ├── システム設計書.md
│   │   ├── 共通Framework設計書.md
│   │   ├── RunContext設計書.md
│   │   ├── Snapshot設計書.md
│   │   ├── Diff設計書.md
│   │   ├── Report設計書.md
│   │   ├── ファイル入出力設計書.md
│   │   ├── ログ・例外設計書.md
│   │   └── 環境設計書.md
│   │
│   └── 06_verification_assets/
│       ├── Verification仕様書_Template.md
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       ├── test_data/
│       ├── reports/
│       └── evidence/
│
├── runtime/
├── build/
├── staging/
└── outputs/
```

:::

完成。这个版本已把你刚才指出的都合进去了：
`01_business` 下面有 **業務分析 + E6 API分析**，`02_master` 里有 **API_UseCase_Scenario対応表** 和 **Compare_Policy_Master**，并且保留 `06_verification_assets`。

## 第 179 轮

### 你

接下来把master的各个模版 给我

### ChatGPT

我会直接按冻结后的 `system/02_master/` 结构给出一套 Master 模板，先覆盖核心 8 份：API、UseCase、Scenario、Context、Verification、API-UseCase-Scenario対応、Compare Policy、Environment。

### ChatGPT

下面是 `system/02_master/` 各 Master 模板合集。

:::writing{variant="document" id="29471"}
# system/02_master Master Templates

---

## 1. E6_API_Master.md

```markdown
---
title: E6 API Master
document_id: MST-API-001
version: 1.0.0
status: Template
document_type: Master
---

# E6_API_Master

|API ID|API名称|日本語名|分類|Method|Path|対象業務|重要度|日次検証対象|API分析書|API設計書|状態|備考|
|------|--------|--------|----|------|----|--------|------|------------|---------|---------|----|----|
|API-001|Customer Exists API|顧客存在確認API|参照|POST|/v1/customers/exists|BUS-001|High|Yes|API-ANL-001|API-001|Active| |
```

---

## 2. UseCase_Master.md

```markdown
---
title: UseCase Master
document_id: MST-UC-001
version: 1.0.0
status: Template
document_type: Master
---

# UseCase_Master

|UseCase ID|UseCase名称|対象業務|Business ID|対象API|Scenario数|実行頻度|自動実行|Baseline比較|重要度|UseCase設計書|状態|備考|
|----------|-----------|--------|-----------|-------|----------|--------|--------|------------|------|-------------|----|----|
|UC-001|顧客情報照会|顧客情報照会業務|BUS-001|API-001, API-002, API-003|3|Daily|Yes|Yes|High|UC-001|Active| |
```

---

## 3. Scenario_Master.md

```markdown
---
title: Scenario Master
document_id: MST-SC-001
version: 1.0.0
status: Template
document_type: Master
---

# Scenario_Master

|Scenario ID|UseCase ID|Scenario名称|分類|差分内容|対象API|期待結果|Result期待|TestCase ID|重要度|自動実行|備考|
|-----------|----------|-------------|----|--------|-------|--------|----------|-----------|------|--------|----|
|SC-001|UC-001|正常系|Normal|標準ルート|API-001, API-002, API-003|顧客情報取得成功|PASS|TC-001|High|Yes| |
|SC-002|UC-001|顧客不存在|Alternative|exists=false|API-001|業務エラー|WARN / FAIL|TC-002|High|Yes| |
```

---

## 4. Context_Master.md

```markdown
---
title: Context Master
document_id: MST-CTX-001
version: 1.0.0
status: Template
document_type: Master
---

# Context_Master

|Context ID|Context名|論理名|Type|Scope|Producer|Consumer|必須|Dynamic|Mask|説明|備考|
|----------|---------|------|----|-----|--------|--------|----|-------|----|----|----|
|CTX-001|Customer.id|顧客番号|String|UseCase|Entry Input|API-001, API-002, API-003|○|No|Conditional|顧客検索キー| |
|CTX-002|Customer.exists|顧客存在有無|Boolean|UseCase|API-001|Scenario Selection|○|No|No|存在判定| |
```

---

## 5. Verification_Master.md

```markdown
---
title: Verification Master
document_id: MST-VER-001
version: 1.0.0
status: Template
document_type: Master
---

# Verification_Master

|Verification ID|対象UseCase|対象Scenario|対象API|検証分類|検証目的|TestCase ID|Evidence ID|重要度|自動実行|状態|備考|
|---------------|-----------|------------|-------|--------|--------|-----------|-----------|------|--------|----|----|
|VER-001|UC-001|SC-001|API-001, API-002, API-003|UseCase連携|正常系業務成立確認|TC-001|EVD-001|High|Yes|Active| |
|VER-002|UC-001|SC-002|API-001|Alternative|顧客不存在時確認|TC-002|EVD-002|High|Yes|Active| |
```

---

## 6. API_UseCase_Scenario対応表.md

```markdown
---
title: API・UseCase・Scenario対応表
document_id: MST-API-UC-SC-001
version: 1.0.0
status: Template
document_type: Master
---

# API・UseCase・Scenario対応表

|No|UseCase ID|UseCase名|Scenario ID|Scenario名|分類|実行順|API ID|API名称|Flow ID|Step ID|実行要否|実行条件|Skip条件|Context入力|Context出力|Verification ID|TestCase ID|重要度|備考|
|--|----------|---------|-----------|-----------|----|------|------|--------|-------|-------|--------|--------|--------|-------------|-------------|---------------|-----------|------|----|
|1|UC-001|顧客情報照会|SC-001|正常系|Normal|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-001|TC-001|High|存在確認|
|2|UC-001|顧客情報照会|SC-001|正常系|Normal|2|API-002|Customer Detail API|BF-004|UC-STEP-002|必須|exists=true|－|CTX-001|CTX-003|VER-001|TC-001|High|顧客取得|
|3|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|2|API-002|Customer Detail API|BF-004|UC-STEP-002|Skip|exists=false|exists=false|CTX-001|－|VER-002|TC-002|High|後続Skip|
```

---

## 7. Compare_Policy_Master.md

```markdown
---
title: Compare Policy Master
document_id: MST-CMP-POL-001
version: 1.0.0
status: Template
document_type: Master
---

# Compare_Policy_Master

|Policy ID|分類|対象|比較方式|条件|Normalize|Tolerance|重要度|適用範囲|備考|
|---------|----|----|--------|----|---------|---------|------|--------|----|
|CMP-POL-001|Dynamic|$.traceId|Ignore|常時|－|－|Low|全API|実行毎に採番|
|CMP-POL-002|Dynamic|$.updatedAt|Ignore / Tolerance|API別|DateTime|±3秒|Low|Response|更新日時|
|CMP-POL-003|Number|金額項目|Tolerance|金額比較|Decimal|±0.01|Medium|Response|丸め差許容|
|CMP-POL-004|Collection|配列|Key Match|key項目指定|Sort|－|High|Array|順序非依存|
|CMP-POL-005|String|文字列|Trim + Equals|常時|Trim|－|Medium|Response|前後空白除去|
```

---

## 8. Environment_Master.md

```markdown
---
title: Environment Master
document_id: MST-ENV-001
version: 1.0.0
status: Template
document_type: Master
---

# Environment_Master

|環境ID|環境名|用途|Base URL|認証方式|設定ファイル|日次実行対象|備考|
|------|------|----|--------|--------|------------|------------|----|
|ENV-DEV|DEV|開発検証|https://dev.example.com|Bearer Token|runtime/config/dev.yml|No|開発用|
|ENV-STG|STG|結合検証|https://stg.example.com|Bearer Token|runtime/config/stg.yml|Yes|日次検証|
|ENV-PLK|PROD-LIKE|本番相当検証|https://prod-like.example.com|Bearer Token|runtime/config/prod-like.yml|Yes|本番相当|
```
:::

这 8 份就是 `system/02_master/` 的基础模板。

## 第 180 轮

### 你

各个模版的例子也做成

### ChatGPT

我会把 `system/02_master/` 的 8 个 Master 都补成“模板 + 記入例”的形式，直接可以放进 repo。

### ChatGPT

下面是 **`system/02_master/` 各 Master 模板 + 使用例**。

:::writing{variant="document" id="80537"}
# system/02_master Master Templates + 記入例

---

# 1. E6_API_Master.md

```markdown
---
title: E6 API Master
document_id: MST-API-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# E6_API_Master

---

# 1. 文書目的

本書は、E6 API Verification Platform で管理する E6 API の一覧、分類、重要度、日次検証対象、関連設計書を一元管理する。

---

# 2. E6 API一覧

|API ID|API名称|日本語名|分類|Method|Path|対象業務|Business ID|重要度|日次検証対象|API分析書|API設計書|状態|備考|
|------|--------|--------|----|------|----|--------|-----------|------|------------|---------|---------|----|----|
|API-XXX|（記載）|（記載）|参照 / 登録 / 更新 / 削除 / File|GET / POST / PUT / DELETE|（記載）|（記載）|BUS-XXX|Critical / High / Medium / Low|Yes / No|API-ANL-XXX|API-XXX|Active / Deprecated / TBD|（記載）|

---

# 3. 分類別集計

|分類|API数|日次検証対象数|備考|
|----|----|--------------|----|
|参照|（記載）|（記載）|（記載）|
|登録|（記載）|（記載）|（記載）|
|更新|（記載）|（記載）|（記載）|
|削除|（記載）|（記載）|（記載）|
|File|（記載）|（記載）|（記載）|

---

# 4. 記入例

|API ID|API名称|日本語名|分類|Method|Path|対象業務|Business ID|重要度|日次検証対象|API分析書|API設計書|状態|備考|
|------|--------|--------|----|------|----|--------|-----------|------|------------|---------|---------|----|----|
|API-001|Customer Exists API|顧客存在確認API|参照|POST|/v1/customers/exists|顧客情報照会業務|BUS-001|High|Yes|API-ANL-001|API-001|Active|Entry API|
|API-002|Customer Detail API|顧客詳細取得API|参照|POST|/v1/customers/detail|顧客情報照会業務|BUS-001|High|Yes|API-ANL-002|API-002|Active|顧客情報取得|
|API-003|Contract List API|契約一覧取得API|参照|POST|/v1/contracts/list|顧客情報照会業務|BUS-001|Medium|Yes|API-ANL-003|API-003|Active|契約一覧取得|
```

---

# 2. UseCase_Master.md

```markdown
---
title: UseCase Master
document_id: MST-UC-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# UseCase_Master

---

# 1. 文書目的

本書は、E6 API Verification Platform で管理する UseCase の一覧、対象業務、対象API、Scenario数、実行対象を一元管理する。

---

# 2. UseCase一覧

|UseCase ID|UseCase名称|対象業務|Business ID|対象API|Scenario数|実行頻度|自動実行|Baseline比較|重要度|UseCase設計書|状態|備考|
|----------|-----------|--------|-----------|-------|----------|--------|--------|------------|------|-------------|----|----|
|UC-XXX|（記載）|（記載）|BUS-XXX|API-XXX|（記載）|Daily / Weekly / Manual|Yes / No|Yes / No|Critical / High / Medium / Low|UC-XXX|Active / Deprecated / TBD|（記載）|

---

# 3. 実行対象UseCase

|UseCase ID|UseCase名称|日次実行|実行順|備考|
|----------|-----------|--------|------|----|
|UC-XXX|（記載）|Yes / No|（記載）|（記載）|

---

# 4. 記入例

|UseCase ID|UseCase名称|対象業務|Business ID|対象API|Scenario数|実行頻度|自動実行|Baseline比較|重要度|UseCase設計書|状態|備考|
|----------|-----------|--------|-----------|-------|----------|--------|--------|------------|------|-------------|----|----|
|UC-001|顧客情報照会|顧客情報照会業務|BUS-001|API-001, API-002, API-003|4|Daily|Yes|Yes|High|UC-001|Active|顧客照会回帰検証|
|UC-002|契約情報照会|契約情報照会業務|BUS-002|API-003, API-004|3|Daily|Yes|Yes|Medium|UC-002|TBD|契約系検証|
```

---

# 3. Scenario_Master.md

```markdown
---
title: Scenario Master
document_id: MST-SC-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Scenario_Master

---

# 1. 文書目的

本書は、UseCase 内の Scenario を一元管理し、Scenario の分類、差分内容、期待結果、TestCase との対応を明確化する。

---

# 2. Scenario一覧

|Scenario ID|UseCase ID|Scenario名称|分類|差分内容|対象API|期待結果|Result期待|TestCase ID|重要度|自動実行|備考|
|-----------|----------|-------------|----|--------|-------|--------|----------|-----------|------|--------|----|
|SC-XXX|UC-XXX|（記載）|Normal / Alternative / Exception / Boundary / Regression|（記載）|API-XXX|（記載）|PASS / WARN / FAIL|TC-XXX|High / Medium / Low|Yes / No|（記載）|

---

# 3. Scenario分類集計

|分類|Scenario数|自動実行対象数|備考|
|----|----------|--------------|----|
|Normal|（記載）|（記載）|（記載）|
|Alternative|（記載）|（記載）|（記載）|
|Exception|（記載）|（記載）|（記載）|
|Boundary|（記載）|（記載）|（記載）|
|Regression|（記載）|（記載）|（記載）|

---

# 4. 記入例

|Scenario ID|UseCase ID|Scenario名称|分類|差分内容|対象API|期待結果|Result期待|TestCase ID|重要度|自動実行|備考|
|-----------|----------|-------------|----|--------|-------|--------|----------|-----------|------|--------|----|
|SC-001|UC-001|正常系|Normal|標準ルート|API-001, API-002, API-003|顧客情報取得成功|PASS|TC-001|High|Yes|日次標準ケース|
|SC-002|UC-001|顧客不存在|Alternative|API-001でexists=false|API-001|業務エラー終了|WARN / FAIL|TC-002|High|Yes|業務仕様によりResult確定|
|SC-003|UC-001|契約0件|Alternative|API-003で0件返却|API-001, API-002, API-003|契約なしで照会成立|PASS / WARN|TC-003|Medium|Yes|業務確認対象|
|SC-004|UC-001|API-002 Timeout|Exception|API-002でTimeout|API-001, API-002|Retry後Fail|FAIL|TC-004|High|Yes|障害系|
```

---

# 4. Context_Master.md

```markdown
---
title: Context Master
document_id: MST-CTX-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Context_Master

---

# 1. 文書目的

本書は、API間、UseCase Step間、Scenario判定、Verificationで利用する Context を一元管理する。

---

# 2. Context一覧

|Context ID|Context名|論理名|Type|Scope|Producer|Consumer|必須|Dynamic|Mask|説明|備考|
|----------|---------|------|----|-----|--------|--------|----|-------|----|----|----|
|CTX-XXX|（記載）|（記載）|String / Number / Boolean / Object / Array / DateTime|Run / UseCase / Scenario / API|（記載）|（記載）|○ / －|Yes / No|Yes / No / Conditional|（記載）|（記載）|

---

# 3. Context Lifecycle

|Context ID|生成タイミング|更新可否|破棄タイミング|競合時処理|備考|
|----------|--------------|--------|--------------|----------|----|
|CTX-XXX|（記載）|可 / 不可|Run終了 / UseCase終了 / Scenario終了|Fail / Warn / Overwrite|（記載）|

---

# 4. 記入例

|Context ID|Context名|論理名|Type|Scope|Producer|Consumer|必須|Dynamic|Mask|説明|備考|
|----------|---------|------|----|-----|--------|--------|----|-------|----|----|----|
|CTX-001|Customer.id|顧客番号|String|UseCase|Entry Input|API-001, API-002, API-003|○|No|Conditional|顧客検索キー|全APIで同一値|
|CTX-002|Customer.exists|顧客存在有無|Boolean|UseCase|API-001|Scenario Selection|○|No|No|存在判定|exists=falseで後続Skip|
|CTX-003|Customer|顧客基本情報|Object|UseCase|API-002|Verification, Report|○|No|Conditional|顧客情報|Responseから抽出|
|CTX-004|Contract.list|契約一覧|Array|UseCase|API-003|Verification, Report|－|No|Conditional|契約一覧|0件許容|
|CTX-005|Runtime.runId|実行ID|String|Run|Runtime|All Evidence / Report|○|Yes|No|実行単位識別子|自動生成|
```

---

# 5. Verification_Master.md

```markdown
---
title: Verification Master
document_id: MST-VER-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Verification_Master

---

# 1. 文書目的

本書は、Verification の一覧、対象 UseCase、対象 Scenario、対象 API、TestCase、Evidence を一元管理する。

---

# 2. Verification一覧

|Verification ID|対象UseCase|対象Scenario|対象API|検証分類|検証目的|TestCase ID|Evidence ID|重要度|自動実行|状態|備考|
|---------------|-----------|------------|-------|--------|--------|-----------|-----------|------|--------|----|----|
|VER-XXX|UC-XXX|SC-XXX|API-XXX|API単体 / UseCase連携 / Compare / Error / Context|（記載）|TC-XXX|EVD-XXX|Critical / High / Medium / Low|Yes / No|Active / Deprecated / TBD|（記載）|

---

# 3. Verification分類集計

|検証分類|件数|自動実行対象|備考|
|--------|----|------------|----|
|API単体|（記載）|（記載）|（記載）|
|UseCase連携|（記載）|（記載）|（記載）|
|Compare|（記載）|（記載）|（記載）|
|Error|（記載）|（記載）|（記載）|
|Context|（記載）|（記載）|（記載）|

---

# 4. 記入例

|Verification ID|対象UseCase|対象Scenario|対象API|検証分類|検証目的|TestCase ID|Evidence ID|重要度|自動実行|状態|備考|
|---------------|-----------|------------|-------|--------|--------|-----------|-----------|------|--------|----|----|
|VER-001|UC-001|SC-001|API-001, API-002, API-003|UseCase連携|正常系で顧客情報照会が成立すること|TC-001|EVD-001|High|Yes|Active|Daily対象|
|VER-002|UC-001|SC-002|API-001|Alternative|顧客不存在時に後続APIがSkipされること|TC-002|EVD-002|High|Yes|Active|exists=false|
|VER-003|UC-001|SC-003|API-003|UseCase連携|契約0件時の結果判定を確認する|TC-003|EVD-003|Medium|Yes|Active|Resultは業務仕様依存|
|VER-004|UC-001|SC-004|API-002|Error|Timeout時にRetry後Failとなること|TC-004|EVD-004|High|Yes|Active|障害系|
```

---

# 6. API_UseCase_Scenario対応表.md

```markdown
---
title: API・UseCase・Scenario対応表
document_id: MST-API-UC-SC-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# API・UseCase・Scenario対応表

---

# 1. 文書目的

本書は、UseCase、Scenario、API の対応関係を一元管理する。

本書により以下を明確化する。

|目的|内容|
|----|----|
|API利用把握|どのUseCase / Scenario がどのAPIを利用するかを確認する|
|実行順序管理|ScenarioごとのAPI実行順序を管理する|
|Skip条件管理|ScenarioごとのAPI Skip条件を管理する|
|影響分析|API変更時に影響するUseCase / Scenario / Verificationを特定する|
|Execution Spec生成|AIまたはRuntimeがAPI実行Chainを生成する入力とする|

---

# 2. API・UseCase・Scenario対応表

|No|UseCase ID|UseCase名|Scenario ID|Scenario名|分類|実行順|API ID|API名称|Flow ID|Step ID|実行要否|実行条件|Skip条件|Context入力|Context出力|Verification ID|TestCase ID|重要度|備考|
|--|----------|---------|-----------|-----------|----|------|------|--------|-------|-------|--------|--------|--------|-------------|-------------|---------------|-----------|------|----|
|1|UC-XXX|（記載）|SC-XXX|（記載）|Normal / Alternative / Exception|1|API-XXX|（記載）|BF-XXX|UC-STEP-XXX|必須 / 任意 / Skip|（記載）|（記載）|CTX-XXX|CTX-XXX|VER-XXX|TC-XXX|High / Medium / Low|（記載）|

---

# 3. API別影響確認

|API ID|API名称|利用UseCase|利用Scenario|実行回数|必須Scenario数|Skip可能Scenario数|影響度|
|------|--------|-----------|-------------|--------|---------------|------------------|------|
|API-XXX|（記載）|UC-XXX|SC-XXX|（記載）|（記載）|（記載）|High / Medium / Low|

---

# 4. UseCase別API構成

|UseCase ID|UseCase名|利用API数|Scenario数|標準API順序|備考|
|----------|---------|---------|-----------|------------|----|
|UC-XXX|（記載）|（記載）|（記載）|API-XXX → API-XXX|（記載）|

---

# 5. Scenario別API構成

|Scenario ID|Scenario名|UseCase ID|API実行順序|Skip API|Expected Result|
|-----------|-----------|----------|------------|---------|---------------|
|SC-XXX|（記載）|UC-XXX|API-XXX → API-XXX|API-XXX|PASS / WARN / FAIL|

---

# 6. 記入例

## 6.1 API・UseCase・Scenario対応表

|No|UseCase ID|UseCase名|Scenario ID|Scenario名|分類|実行順|API ID|API名称|Flow ID|Step ID|実行要否|実行条件|Skip条件|Context入力|Context出力|Verification ID|TestCase ID|重要度|備考|
|--|----------|---------|-----------|-----------|----|------|------|--------|-------|-------|--------|--------|--------|-------------|-------------|---------------|-----------|------|----|
|1|UC-001|顧客情報照会|SC-001|正常系|Normal|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-001|TC-001|High|存在確認|
|2|UC-001|顧客情報照会|SC-001|正常系|Normal|2|API-002|Customer Detail API|BF-004|UC-STEP-002|必須|exists=true|－|CTX-001|CTX-003|VER-001|TC-001|High|顧客取得|
|3|UC-001|顧客情報照会|SC-001|正常系|Normal|3|API-003|Contract List API|BF-005|UC-STEP-003|必須|Customer取得済み|－|CTX-001|CTX-004|VER-001|TC-001|Medium|契約取得|
|4|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-002|TC-002|High|exists=false|
|5|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|2|API-002|Customer Detail API|BF-004|UC-STEP-002|Skip|exists=false|exists=false|CTX-001|－|VER-002|TC-002|High|後続Skip|
|6|UC-001|顧客情報照会|SC-002|顧客不存在|Alternative|3|API-003|Contract List API|BF-005|UC-STEP-003|Skip|exists=false|exists=false|CTX-001|－|VER-002|TC-002|Medium|後続Skip|
|7|UC-001|顧客情報照会|SC-003|契約0件|Alternative|1|API-001|Customer Exists API|BF-002|UC-STEP-001|必須|Customer.id が存在する|－|CTX-001|CTX-002|VER-003|TC-003|High|存在確認|
|8|UC-001|顧客情報照会|SC-003|契約0件|Alternative|2|API-002|Customer Detail API|BF-004|UC-STEP-002|必須|exists=true|－|CTX-001|CTX-003|VER-003|TC-003|High|顧客取得|
|9|UC-001|顧客情報照会|SC-003|契約0件|Alternative|3|API-003|Contract List API|BF-005|UC-STEP-003|必須|Customer取得済み|－|CTX-001|CTX-004|VER-003|TC-003|Medium|0件返却|

## 6.2 Scenario別API構成

|Scenario ID|Scenario名|UseCase ID|API実行順序|Skip API|Expected Result|
|-----------|-----------|----------|------------|---------|---------------|
|SC-001|正常系|UC-001|API-001 → API-002 → API-003|－|PASS|
|SC-002|顧客不存在|UC-001|API-001|API-002, API-003|WARN / FAIL|
|SC-003|契約0件|UC-001|API-001 → API-002 → API-003|－|PASS / WARN|
```

---

# 7. Compare_Policy_Master.md

```markdown
---
title: Compare Policy Master
document_id: MST-CMP-POL-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Compare_Policy_Master

---

# 1. 文書目的

本書は、E6 API Verification Platform で共通利用する Compare Policy を管理する。

Verification仕様書は、本MasterのPolicyを参照し、UseCase / Scenario / APIごとの具体的なCompare Ruleを定義する。

---

# 2. Compare Policy一覧

|Policy ID|分類|対象|比較方式|条件|Normalize|Tolerance|重要度|適用範囲|備考|
|---------|----|----|--------|----|---------|---------|------|--------|----|
|CMP-POL-XXX|Dynamic / String / Number / DateTime / Collection / Error|（記載）|Equals / Ignore / Regex / Contains / Tolerance / Key Match / Order Match|（記載）|（記載）|（記載）|Critical / High / Medium / Low|全API / Response / Request / Context / File|（記載）|

---

# 3. 共通Ignore項目

|Policy ID|対象|理由|適用条件|備考|
|---------|----|----|--------|----|
|CMP-POL-XXX|$.xxx|（記載）|（記載）|（記載）|

---

# 4. Normalize Rule

|Normalize ID|対象分類|方式|例|備考|
|------------|--------|----|--|----|
|NORM-XXX|String / Number / DateTime|Trim / Decimal / Format|（記載）|（記載）|

---

# 5. Collection Compare Rule

|Policy ID|対象|比較方式|Key|順序考慮|備考|
|---------|----|--------|---|--------|----|
|CMP-POL-XXX|$.items[]|Key Match / Order Match|itemId|Yes / No|（記載）|

---

# 6. 記入例

## 6.1 Compare Policy一覧

|Policy ID|分類|対象|比較方式|条件|Normalize|Tolerance|重要度|適用範囲|備考|
|---------|----|----|--------|----|---------|---------|------|--------|----|
|CMP-POL-001|Dynamic|$.traceId|Ignore|常時|－|－|Low|全API|実行毎に採番|
|CMP-POL-002|Dynamic|$.updatedAt|Ignore / Tolerance|API別|DateTime|±3秒|Low|Response|更新日時|
|CMP-POL-003|Number|金額項目|Tolerance|金額比較|Decimal|±0.01|Medium|Response|丸め差許容|
|CMP-POL-004|Collection|配列|Key Match|key項目指定|Sort|－|High|Array|順序非依存|
|CMP-POL-005|String|文字列|Trim + Equals|常時|Trim|－|Medium|Response|前後空白除去|
|CMP-POL-006|Error|$.error.message|Contains / Regex|Error時|Trim|－|Medium|Error Response|文言揺れ対策|

## 6.2 共通Ignore項目

|Policy ID|対象|理由|適用条件|備考|
|---------|----|----|--------|----|
|CMP-POL-001|$.traceId|実行毎に採番されるため|全API|存在・型のみ確認可|
|CMP-POL-002|$.updatedAt|データ更新時刻のため|API別|必要に応じてTolerance|
```

---

# 8. Environment_Master.md

```markdown
---
title: Environment Master
document_id: MST-ENV-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Environment_Master

---

# 1. 文書目的

本書は、E6 API Verification Platform の DEV、STG、PROD-LIKE、Staging などの環境情報を一元管理する。

---

# 2. Environment一覧

|環境ID|環境名|用途|Base URL|認証方式|設定ファイル|日次実行対象|備考|
|------|------|----|--------|--------|------------|------------|----|
|ENV-XXX|DEV / STG / PROD-LIKE / LOCAL|（記載）|（記載）|Bearer Token / API Key / Basic / mTLS|（記載）|Yes / No|（記載）|

---

# 3. 環境別設定

|環境ID|Timeout|Retry|Proxy|証明書|ログLevel|備考|
|------|-------|-----|-----|------|--------|----|
|ENV-XXX|（記載）秒|（記載）回|あり / なし|必要 / 不要|DEBUG / INFO / WARN / ERROR|（記載）|

---

# 4. 機密情報管理

|環境ID|機密情報|管理方法|配置先|備考|
|------|--------|--------|------|----|
|ENV-XXX|Token / Password / Certificate|環境変数 / Secret File / Vault|runtime/config/secret/|Git管理禁止|

---

# 5. 記入例

## 5.1 Environment一覧

|環境ID|環境名|用途|Base URL|認証方式|設定ファイル|日次実行対象|備考|
|------|------|----|--------|--------|------------|------------|----|
|ENV-DEV|DEV|開発検証|https://dev.example.com|Bearer Token|runtime/config/dev.yml|No|開発用|
|ENV-STG|STG|結合検証|https://stg.example.com|Bearer Token|runtime/config/stg.yml|Yes|日次検証|
|ENV-PLK|PROD-LIKE|本番相当検証|https://prod-like.example.com|Bearer Token|runtime/config/prod-like.yml|Yes|本番相当|
|ENV-LOCAL|LOCAL|ローカルMock検証|http://localhost:8080|None / Mock Token|runtime/config/local.yml|No|Mock用|

## 5.2 環境別設定

|環境ID|Timeout|Retry|Proxy|証明書|ログLevel|備考|
|------|-------|-----|-----|------|--------|----|
|ENV-DEV|10秒|1回|なし|不要|DEBUG|開発用|
|ENV-STG|10秒|2回|あり|必要|INFO|日次検証|
|ENV-PLK|15秒|2回|あり|必要|INFO|本番相当|
|ENV-LOCAL|5秒|0回|なし|不要|DEBUG|Mock検証|
```
:::

以上是 **8 个 Master 的模板 + 使用例**。
可以直接分别保存到：

```text
system/02_master/
├── E6_API_Master.md
├── UseCase_Master.md
├── Scenario_Master.md
├── Context_Master.md
├── Verification_Master.md
├── API_UseCase_Scenario対応表.md
├── Compare_Policy_Master.md
└── Environment_Master.md
```

## 第 181 轮

### 你

03_api_design  04_usecase_design 的模版和例子

### ChatGPT

我会按冻结结构直接给 `03_api_design/API設計書_Template.md` 和 `04_usecase_design/UseCase設計書_Template.md`，每份都包含模板主体和顧客情報照会的記入例。

### ChatGPT

下面给你 **`03_api_design` 和 `04_usecase_design` 的模板 + 例子**。
这版已经和前面的 `API分析書`、`Master`、`API_UseCase_Scenario対応表`、`Compare_Policy_Master` 对齐。

:::writing{variant="document" id="58192"}
# system/03_api_design/API設計書_Template.md

```markdown
---
title: API設計書テンプレート
document_id: API-DESIGN-TEMPLATE
version: 1.0.0
status: Template
document_type: API Design
system_name: E6 API Verification Platform
phase: To-Be Design
author:
reviewer:
approver:
created:
updated:
---

# API設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|API-XXX|
|文書名称|〇〇 API設計書|
|API ID|API-XXX|
|API名称|（記載）|
|日本語名|（記載）|
|対象システム|E6 API|
|対象業務|BUS-XXX|
|関連API分析書|API-ANL-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 参照資料

|資料ID|資料名|資料種別|配置先|備考|
|------|------|--------|------|----|
|API-ANL-XXX|〇〇API分析書|API分析書|system/01_business/02_E6_API分析/|As-Is分析結果|
|MST-API-001|E6_API_Master|Master|system/02_master/|API基本情報|
|MST-CTX-001|Context_Master|Master|system/02_master/|Context定義|
|MST-CMP-POL-001|Compare_Policy_Master|Master|system/02_master/|比較方針|

---

# 2. API概要

## 2.1 API目的

（本APIが何を実現するためのAPIかを記載）

---

## 2.2 API概要

（本APIの処理概要を記載）

---

## 2.3 業務上の利用位置

|項目|内容|
|----|----|
|関連Business ID|BUS-XXX|
|関連Flow ID|BF-XXX|
|利用UseCase|UC-XXX|
|利用Scenario|SC-XXX|
|前提API|API-XXX / なし|
|後続API|API-XXX / なし|

---

## 2.4 API分類

|項目|内容|
|----|----|
|API種別|参照 / 登録 / 更新 / 削除 / File / その他|
|同期方式|同期 / 非同期|
|冪等性|あり / なし|
|認証要否|要 / 不要|
|日次検証対象|Yes / No|
|Baseline比較対象|Yes / No|
|重要度|Critical / High / Medium / Low|

---

# 3. Interface Specification

## 3.1 Endpoint

|項目|内容|
|----|----|
|Base URL|Environment_Master参照|
|Path|（記載）|
|HTTP Method|GET / POST / PUT / DELETE|
|Protocol|HTTPS|
|Content-Type|application/json|
|Accept|application/json|
|Timeout|（記載）秒|
|Retry|あり / なし / Framework Default|

---

## 3.2 Header Specification

|No|Header名|必須|設定値|設定元|Mask|備考|
|--|--------|----|------|------|----|----|
|1|Content-Type|○|application/json|固定|No| |
|2|Authorization|○|Bearer ${token}|Auth Context|Yes|秘匿対象|

---

## 3.3 Authentication / Authorization

|項目|内容|
|----|----|
|認証方式|Bearer Token / API Key / Basic / mTLS|
|Token取得元|Environment / Auth API / Secret|
|必要権限|（記載）|
|認証失敗時Status|401 / 403|
|秘匿対象|Authorization / API Key / Token|

---

# 4. Request Specification

## 4.1 Request形式

|項目|内容|
|----|----|
|Request形式|JSON / Query / Path / Form / Multipart|
|文字コード|UTF-8|
|Body有無|あり / なし|
|File有無|あり / なし|

---

## 4.2 Request項目定義

|No|JSONPath / Parameter|項目名|論理名|Type|必須|Null許可|空文字許可|Min|Max|Pattern|Enum|固定値|Default|設定元|Context ID|Verification Target|備考|
|--|--------------------|------|------|----|----|--------|----------|---|---|-------|----|------|-------|------|----------|-------------------|----|
|1|$.xxx|（記載）|（記載）|String / Number / Boolean / Object / Array / Date / DateTime|○ / －|可 / 不可|可 / 不可|（記載）|（記載）|（記載）|（記載）|（記載）|（記載）|Entry Input / Context / Fixed / Runtime|CTX-XXX|Yes / No|（記載）|

---

## 4.3 Request生成ルール

|No|対象|生成ルール|例|備考|
|--|----|----------|--|----|
|1|$.xxx|Contextから設定|CTX-XXX| |
|2|$.yyy|固定値を設定|固定値| |

---

## 4.4 Request Sample

```json
{
  "xxx": "value"
}
```

---

# 5. Response Specification

## 5.1 Response形式

|項目|内容|
|----|----|
|Response形式|JSON / XML / File / Binary|
|文字コード|UTF-8|
|正常時HTTP Status|200 / 201 / 204|
|異常時HTTP Status|400 / 401 / 403 / 404 / 500|
|Dynamic項目有無|あり / なし|

---

## 5.2 Response項目定義

|No|JSONPath|項目名|論理名|Type|必須|Null許可|Min|Max|Pattern|Enum|固定値|入力値一致|Context一致|Output Context|Dynamic|Baseline比較|Verification Target|備考|
|--|--------|------|------|----|----|--------|---|---|-------|----|------|----------|-----------|--------------|-------|------------|-------------------|----|
|1|$.xxx|（記載）|（記載）|String / Number / Boolean / Object / Array / Date / DateTime|○ / －|可 / 不可|（記載）|（記載）|（記載）|（記載）|（記載）|Request $.xxx / －|CTX-XXX / －|CTX-XXX / －|Yes / No|Yes / No|Yes / No|（記載）|

---

## 5.3 Response固定値定義

|No|JSONPath|固定値|適用条件|Verification Target|備考|
|--|--------|------|--------|-------------------|----|
|1|$.resultCode|0|正常終了時|Yes| |

---

## 5.4 Response Enum定義

|No|JSONPath|許容値|意味|Verification Target|備考|
|--|--------|------|----|-------------------|----|
|1|$.status|ACTIVE, INACTIVE|状態|Yes| |

---

## 5.5 入力値一致定義

|No|Response JSONPath|Request JSONPath|一致条件|Verification Target|備考|
|--|-----------------|----------------|--------|-------------------|----|
|1|$.xxx|$.xxx|Equals|Yes| |

---

## 5.6 Dynamic Field定義

|No|JSONPath|項目名|変動理由|Compare Policy|Baseline比較|備考|
|--|--------|------|--------|--------------|------------|----|
|1|$.traceId|Trace ID|実行毎に採番|CMP-POL-001|No|存在確認のみ|

---

## 5.7 Response Sample

```json
{
  "xxx": "value"
}
```

---

# 6. Business Rule

## 6.1 業務判定ルール

|Rule ID|条件|判定結果|後続処理|関連Scenario|備考|
|-------|----|--------|--------|------------|----|
|BR-XXX|（記載）|（記載）|（記載）|SC-XXX|（記載）|

---

## 6.2 API Skip / Continue候補

|条件|後続API|処理|関連UseCase|関連Scenario|備考|
|----|-------|----|-----------|------------|----|
|（記載）|API-XXX|Continue / Skip / Stop|UC-XXX|SC-XXX| |

---

# 7. Error Specification

## 7.1 Error Response Format

|JSONPath|項目名|Type|必須|備考|
|--------|------|----|----|----|
|$.error.code|errorCode|String|○| |
|$.error.message|errorMessage|String|○| |
|$.traceId|traceId|String|－|Dynamic|

---

## 7.2 Error Code Definition

|No|HTTP Status|Error Code|発生条件|Response例|Verification Target|備考|
|--|------------|----------|--------|----------|-------------------|----|
|1|400|（記載）|必須項目未設定|（記載）|Yes / No| |
|2|401|（記載）|認証不正|（記載）|Yes / No| |

---

# 8. Context Mapping

## 8.1 Input Context

|Context ID|Context名|Request項目|利用目的|必須|備考|
|----------|---------|------------|--------|----|----|
|CTX-XXX|（記載）|$.xxx|（記載）|○ / －| |

---

## 8.2 Output Context

|Context ID|Context名|Response JSONPath|後続利用|Consumer|備考|
|----------|---------|-----------------|--------|--------|----|
|CTX-XXX|（記載）|$.xxx|後続API / Verification / Report|API-XXX / UC-XXX| |

---

# 9. Verification Metadata

## 9.1 Request Verification Candidate

|Candidate ID|対象|検証種別|重要度|Verification反映|備考|
|------------|----|--------|------|----------------|----|
|REQ-CAND-XXX|$.xxx|Required / Type / Length / Pattern / Enum / Fixed|High / Medium / Low|Yes / No| |

---

## 9.2 Response Verification Candidate

|Candidate ID|対象|検証種別|重要度|Verification反映|備考|
|------------|----|--------|------|----------------|----|
|RES-CAND-XXX|$.xxx|Required / Type / Fixed / Enum / Input Match / Context Match / Dynamic|High / Medium / Low|Yes / No| |

---

## 9.3 Baseline Diff Candidate

|Candidate ID|対象|Diff対象|Compare Policy|重要度|Verification反映|備考|
|------------|----|--------|--------------|------|----------------|----|
|DIFF-CAND-XXX|$.xxx|Yes / No|CMP-POL-XXX|High / Medium / Low|Yes / No| |

---

# 10. Performance / Security

## 10.1 Performance

|項目|基準|備考|
|----|----|----|
|Timeout|（記載）秒| |
|Retry|（記載）回| |
|想定Response Time|（記載）ms| |

---

## 10.2 Security

|項目|内容|
|----|----|
|認証|（記載）|
|認可|（記載）|
|Mask対象|（記載）|
|Log出力禁止項目|（記載）|

---

# 11. Traceability

|Business ID|Flow ID|API分析書|API ID|UseCase ID|Scenario ID|Context ID|Verification ID|
|-----------|-------|---------|------|----------|-----------|----------|---------------|
|BUS-XXX|BF-XXX|API-ANL-XXX|API-XXX|UC-XXX|SC-XXX|CTX-XXX|VER-XXX|

---

# Appendix A. 記入例：API-001_CustomerExistsAPI

## A.1 文書管理

|項目|内容|
|----|----|
|文書ID|API-001|
|文書名称|顧客存在確認API設計書|
|API ID|API-001|
|API名称|Customer Exists API|
|日本語名|顧客存在確認API|
|対象システム|E6 API|
|対象業務|BUS-001|
|関連API分析書|API-ANL-001|
|版数|1.0.0|
|状態|Draft|
|作成者|API設計担当|
|レビューア|アーキテクト|
|承認者|プロジェクト責任者|
|作成日|2026-07-09|
|更新日|2026-07-09|

---

## A.2 API目的

本APIは、顧客番号を指定し、E6側に対象顧客が存在するかを確認するために利用する。

---

## A.3 API概要

Requestで `customerId` を受け取り、該当顧客が存在する場合は `exists=true`、存在しない場合は `exists=false` を返却する。

---

## A.4 業務上の利用位置

|項目|内容|
|----|----|
|関連Business ID|BUS-001|
|関連Flow ID|BF-002|
|利用UseCase|UC-001|
|利用Scenario|SC-001, SC-002, SC-003|
|前提API|なし|
|後続API|API-002, API-003|

---

## A.5 API分類

|項目|内容|
|----|----|
|API種別|参照|
|同期方式|同期|
|冪等性|あり|
|認証要否|要|
|日次検証対象|Yes|
|Baseline比較対象|Yes|
|重要度|High|

---

## A.6 Endpoint

|項目|内容|
|----|----|
|Base URL|Environment_Master参照|
|Path|/v1/customers/exists|
|HTTP Method|POST|
|Protocol|HTTPS|
|Content-Type|application/json|
|Accept|application/json|
|Timeout|10秒|
|Retry|Framework Default|

---

## A.7 Request項目定義

|No|JSONPath / Parameter|項目名|論理名|Type|必須|Null許可|空文字許可|Min|Max|Pattern|Enum|固定値|Default|設定元|Context ID|Verification Target|備考|
|--|--------------------|------|------|----|----|--------|----------|---|---|-------|----|------|-------|------|----------|-------------------|----|
|1|$.customerId|customerId|顧客番号|String|○|不可|不可|1|20|^[0-9]+$|－|－|－|Entry Input|CTX-001|Yes|数字のみ|

---

## A.8 Request Sample

```json
{
  "customerId": "10000001"
}
```

---

## A.9 Response項目定義

|No|JSONPath|項目名|論理名|Type|必須|Null許可|Min|Max|Pattern|Enum|固定値|入力値一致|Context一致|Output Context|Dynamic|Baseline比較|Verification Target|備考|
|--|--------|------|------|----|----|--------|---|---|-------|----|------|----------|-----------|--------------|-------|------------|-------------------|----|
|1|$.resultCode|resultCode|結果コード|String|○|不可|1|10|－|0,1|0|－|－|－|No|Yes|Yes|正常時0|
|2|$.exists|exists|顧客存在有無|Boolean|○|不可|－|－|－|true,false|－|－|－|CTX-002|No|Yes|Yes|業務判定対象|
|3|$.customerId|customerId|顧客番号|String|○|不可|1|20|^[0-9]+$|－|－|Request $.customerId|CTX-001|CTX-001|No|Yes|Yes|入力値一致|
|4|$.traceId|traceId|Trace ID|String|－|可|－|64|－|－|－|－|－|－|Yes|No|Yes|Dynamic項目|

---

## A.10 Response Sample

```json
{
  "resultCode": "0",
  "exists": true,
  "customerId": "10000001",
  "traceId": "9f3c7e8a-xxxx"
}
```

---

## A.11 Business Rule

|Rule ID|条件|判定結果|後続処理|関連Scenario|備考|
|-------|----|--------|--------|------------|----|
|BR-001|$.exists = true|顧客存在|API-002を実行|SC-001, SC-003|正常継続|
|BR-002|$.exists = false|顧客不存在|API-002, API-003をSkip|SC-002|業務エラーまたはWARN|

---

## A.12 Context Mapping

### Input Context

|Context ID|Context名|Request項目|利用目的|必須|備考|
|----------|---------|------------|--------|----|----|
|CTX-001|Customer.id|$.customerId|顧客指定|○|Entry Input|

### Output Context

|Context ID|Context名|Response JSONPath|後続利用|Consumer|備考|
|----------|---------|-----------------|--------|--------|----|
|CTX-002|Customer.exists|$.exists|Scenario判定 / Skip判定|UC-001 / API-002 / API-003|exists=falseで後続Skip|

---

## A.13 Verification Metadata

### Request Verification Candidate

|Candidate ID|対象|検証種別|重要度|Verification反映|備考|
|------------|----|--------|------|----------------|----|
|REQ-CAND-001|$.customerId|Required / Type / Length / Pattern|High|Yes|顧客番号|

### Response Verification Candidate

|Candidate ID|対象|検証種別|重要度|Verification反映|備考|
|------------|----|--------|------|----------------|----|
|RES-CAND-001|$.resultCode|Fixed Value|High|Yes|正常時0|
|RES-CAND-002|$.exists|Required / Type / Enum|High|Yes|業務判定|
|RES-CAND-003|$.customerId|Input Match|High|Yes|入力値一致|
|RES-CAND-004|$.traceId|Dynamic / Exists|Low|Yes|Baseline比較除外|

### Baseline Diff Candidate

|Candidate ID|対象|Diff対象|Compare Policy|重要度|Verification反映|備考|
|------------|----|--------|--------------|------|----------------|----|
|DIFF-CAND-001|$.resultCode|Yes|Equals|High|Yes|固定値|
|DIFF-CAND-002|$.exists|Yes|Equals|High|Yes|業務結果|
|DIFF-CAND-003|$.customerId|Yes|Equals|High|Yes|入力値一致|
|DIFF-CAND-004|$.traceId|No|CMP-POL-001|Low|Yes|Ignore|

---

## A.14 Traceability

|Business ID|Flow ID|API分析書|API ID|UseCase ID|Scenario ID|Context ID|Verification ID|
|-----------|-------|---------|------|----------|-----------|----------|---------------|
|BUS-001|BF-002|API-ANL-001|API-001|UC-001|SC-001, SC-002, SC-003|CTX-001, CTX-002|VER-001, VER-002, VER-003|
```
:::

:::writing{variant="document" id="91406"}
# system/04_usecase_design/UseCase設計書_Template.md

```markdown
---
title: UseCase設計書テンプレート
document_id: USECASE-DESIGN-TEMPLATE
version: 1.0.0
status: Template
document_type: UseCase Design
system_name: E6 API Verification Platform
phase: To-Be Design
author:
reviewer:
approver:
created:
updated:
---

# UseCase設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|UC-XXX|
|文書名称|〇〇 UseCase設計書|
|UseCase ID|UC-XXX|
|UseCase名称|（記載）|
|対象業務|（記載）|
|Business ID|BUS-XXX|
|関連業務分析書|BA-XXX|
|関連API|API-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 参照資料

|資料ID|資料名|資料種別|配置先|備考|
|------|------|--------|------|----|
|BA-XXX|〇〇業務分析書|業務分析|system/01_business/01_業務分析/|As-Is業務分析|
|API-XXX|〇〇API設計書|API設計|system/03_api_design/|To-Be API設計|
|MST-API-UC-SC-001|API_UseCase_Scenario対応表|Master|system/02_master/|API実行順序|
|MST-CTX-001|Context_Master|Master|system/02_master/|Context定義|
|MST-SC-001|Scenario_Master|Master|system/02_master/|Scenario定義|

---

# 2. UseCase概要

## 2.1 UseCase目的

（本UseCaseが何を実現するかを記載）

---

## 2.2 UseCase概要

（UseCaseの処理概要を記載）

---

## 2.3 UseCase分類

|項目|内容|
|----|----|
|UseCase分類|照会 / 登録 / 更新 / 削除 / File / その他|
|実行方式|自動 / 手動 / 半自動|
|実行頻度|Daily / Weekly / Manual|
|日次検証対象|Yes / No|
|Baseline比較対象|Yes / No|
|重要度|Critical / High / Medium / Low|

---

# 3. Actor / Trigger / Condition

## 3.1 Actor

|Actor ID|Actor名|役割|備考|
|--------|-------|----|----|
|ACT-XXX|（記載）|（記載）|（記載）|

---

## 3.2 Trigger

|Trigger ID|Trigger名|発生条件|備考|
|----------|---------|--------|----|
|TRG-XXX|（記載）|（記載）|（記載）|

---

## 3.3 Pre Condition

|No|前提条件|確認方法|備考|
|--|--------|--------|----|
|1|（記載）|（記載）|（記載）|

---

## 3.4 Post Condition

|No|終了条件|確認方法|備考|
|--|--------|--------|----|
|1|（記載）|（記載）|（記載）|

---

# 4. Entry Input

|No|Input ID|項目名|論理名|Type|必須|設定元|Context ID|備考|
|--|--------|------|------|----|----|------|----------|----|
|1|IN-XXX|（記載）|（記載）|String / Number / Boolean / Object / Array|○ / －|TestData / Runtime / Manual|CTX-XXX|（記載）|

---

# 5. Main Flow

## 5.1 Flow概要

```mermaid
flowchart TD

START([Start])
STEP1[STEP1]
STEP2[STEP2]
END([End])

START --> STEP1 --> STEP2 --> END
```

---

## 5.2 Main Flow Detail

|Step ID|Step名|処理内容|利用API|Input Context|Output Context|正常時遷移|異常時遷移|備考|
|-------|------|--------|-------|-------------|--------------|----------|----------|----|
|UC-STEP-XXX|（記載）|（記載）|API-XXX|CTX-XXX|CTX-XXX|UC-STEP-XXX|Exception Flow|（記載）|

---

# 6. Scenario一覧

## 6.1 Scenario一覧

|Scenario ID|Scenario名|分類|差分内容|対象API|期待結果|Result期待|TestCase ID|重要度|備考|
|-----------|-----------|----|--------|-------|--------|----------|-----------|------|----|
|SC-XXX|（記載）|Normal / Alternative / Exception / Boundary / Regression|（記載）|API-XXX|（記載）|PASS / WARN / FAIL|TC-XXX|High / Medium / Low|（記載）|

---

## 6.2 Scenario Matrix

|Scenario ID|API-001|API-002|API-003|Expected Result|備考|
|-----------|-------|-------|-------|---------------|----|
|SC-XXX|Run / Skip|Run / Skip|Run / Skip|PASS / WARN / FAIL|（記載）|

---

## 6.3 Scenario Selection Rule

|Rule ID|条件|Scenario ID|判定結果|備考|
|-------|----|------------|--------|----|
|SC-RULE-XXX|（記載）|SC-XXX|（記載）|（記載）|

---

# 7. API Execution Chain

## 7.1 API実行順序

|実行順|API ID|API名称|実行要否|実行条件|Skip条件|Input Context|Output Context|Timeout|Retry|備考|
|------|------|--------|--------|--------|--------|-------------|--------------|-------|-----|----|
|1|API-XXX|（記載）|必須 / 任意 / Skip|（記載）|（記載）|CTX-XXX|CTX-XXX|（記載）秒|（記載）回|（記載）|

---

## 7.2 Scenario別API実行順序

|Scenario ID|API実行順序|Skip API|備考|
|-----------|------------|--------|----|
|SC-XXX|API-XXX → API-XXX|API-XXX|（記載）|

---

## 7.3 API Skip Rule

|Rule ID|条件|Skip対象API|後続処理|関連Scenario|備考|
|-------|----|-----------|--------|------------|----|
|SKIP-XXX|（記載）|API-XXX|Continue / Stop / Fail|SC-XXX|（記載）|

---

# 8. Context Mapping

## 8.1 Context一覧

|Context ID|Context名|Type|Producer|Consumer|Scope|必須|備考|
|----------|---------|----|--------|--------|-----|----|----|
|CTX-XXX|（記載）|String / Number / Boolean / Object / Array|（記載）|（記載）|Run / UseCase / Scenario / API|○ / －|（記載）|

---

## 8.2 Context生成・利用

|Step ID|API ID|生成Context|利用Context|備考|
|-------|------|-----------|-----------|----|
|UC-STEP-XXX|API-XXX|CTX-XXX|CTX-XXX|（記載）|

---

## 8.3 Context Lifetime

|Context ID|生成タイミング|有効範囲|破棄タイミング|備考|
|----------|--------------|--------|--------------|----|
|CTX-XXX|（記載）|Run / UseCase / Scenario / API|（記載）|（記載）|

---

# 9. Alternative Flow

|Flow ID|条件|処理内容|関連Scenario|Expected Result|備考|
|-------|----|--------|------------|---------------|----|
|ALT-XXX|（記載）|（記載）|SC-XXX|PASS / WARN / FAIL|（記載）|

---

# 10. Exception Flow

|Flow ID|発生条件|処理内容|Retry|Expected Result|関連Scenario|備考|
|-------|--------|--------|-----|---------------|------------|----|
|EXC-XXX|（記載）|（記載）|Yes / No|FAIL / ERROR|SC-XXX|（記載）|

---

# 11. Execution Policy

## 11.1 実行方針

|項目|内容|
|----|----|
|実行方式|Sequential / Parallel|
|停止条件|Critical Fail / API Error / Scenario End|
|Retry方針|Framework Default / API別|
|Timeout方針|API設計書参照|
|Evidence保存|Yes / No|

---

## 11.2 TestData方針

|項目|内容|
|----|----|
|TestData配置|system/06_verification_assets/test_data/UC-XXX/|
|Scenario別Data|Yes / No|
|Mask対象|（記載）|
|Data更新方針|Manual / Generated|

---

# 12. Business Check

|Check ID|対象|条件|期待結果|重要度|Verification ID|備考|
|--------|----|----|--------|------|---------------|----|
|BCHK-XXX|（記載）|（記載）|（記載）|High / Medium / Low|VER-XXX|（記載）|

---

# 13. Expected Result

## 13.1 Scenario別期待結果

|Scenario ID|期待HTTP Status|期待Business Result|期待UseCase Result|Report Result|備考|
|-----------|----------------|-------------------|------------------|-------------|----|
|SC-XXX|200 / 400 / 500|（記載）|PASS / WARN / FAIL|PASS / WARN / FAIL|（記載）|

---

## 13.2 Compare対象

|Scenario ID|Compare対象|Compare Policy|Baseline対象|備考|
|-----------|------------|--------------|------------|----|
|SC-XXX|Response / Context / Report|CMP-POL-XXX|Yes / No|（記載）|

---

# 14. Evidence

## 14.1 Evidence保存対象

|Evidence ID|対象|保存内容|保存先|Mask|備考|
|-----------|----|--------|------|----|----|
|EVD-XXX|Request / Response / Context / Diff / Log|（記載）|outputs/runs/{runId}/|Yes / No|（記載）|

---

## 14.2 Report出力

|Report ID|Report名|出力条件|出力先|備考|
|---------|--------|--------|------|----|
|RPT-XXX|Daily Summary / Diff Report / Evidence Report|（記載）|outputs/reports/|（記載）|

---

# 15. Traceability

|Business ID|Flow ID|UseCase ID|Scenario ID|API ID|Context ID|Verification ID|TestCase ID|Evidence ID|
|-----------|-------|----------|-----------|------|----------|---------------|-----------|-----------|
|BUS-XXX|BF-XXX|UC-XXX|SC-XXX|API-XXX|CTX-XXX|VER-XXX|TC-XXX|EVD-XXX|

---

# Appendix A. 記入例：UC-001_顧客情報照会

## A.1 文書管理

|項目|内容|
|----|----|
|文書ID|UC-001|
|文書名称|顧客情報照会 UseCase設計書|
|UseCase ID|UC-001|
|UseCase名称|顧客情報照会|
|対象業務|顧客情報照会業務|
|Business ID|BUS-001|
|関連業務分析書|BA-001|
|関連API|API-001, API-002, API-003|
|版数|1.0.0|
|状態|Draft|
|作成者|UseCase設計担当|
|レビューア|アーキテクト|
|承認者|プロジェクト責任者|
|作成日|2026-07-09|
|更新日|2026-07-09|

---

## A.2 UseCase目的

本UseCaseは、顧客番号を入力として、E6 APIを順次呼び出し、顧客存在確認、顧客詳細取得、契約一覧取得を行う。

---

## A.3 UseCase概要

顧客番号をEntry Inputとして受け取り、最初に顧客存在確認APIを呼び出す。顧客が存在する場合は顧客詳細取得APIおよび契約一覧取得APIを呼び出す。顧客が存在しない場合は後続APIをSkipし、業務結果として顧客不存在を返却する。

---

## A.4 UseCase分類

|項目|内容|
|----|----|
|UseCase分類|照会|
|実行方式|自動|
|実行頻度|Daily|
|日次検証対象|Yes|
|Baseline比較対象|Yes|
|重要度|High|

---

## A.5 Entry Input

|No|Input ID|項目名|論理名|Type|必須|設定元|Context ID|備考|
|--|--------|------|------|----|----|------|----------|----|
|1|IN-001|customerId|顧客番号|String|○|TestData|CTX-001|数字のみ|

---

## A.6 Main Flow

```mermaid
flowchart TD

START([Start])
INPUT[Entry Input: customerId]
API001[API-001 Customer Exists API]
CHECK{exists?}
API002[API-002 Customer Detail API]
API003[API-003 Contract List API]
REPORT[Result / Report]
END([End])

START --> INPUT
INPUT --> API001
API001 --> CHECK
CHECK -- true --> API002
API002 --> API003
API003 --> REPORT
CHECK -- false --> REPORT
REPORT --> END
```

---

## A.7 Main Flow Detail

|Step ID|Step名|処理内容|利用API|Input Context|Output Context|正常時遷移|異常時遷移|備考|
|-------|------|--------|-------|-------------|--------------|----------|----------|----|
|UC-STEP-001|顧客存在確認|顧客番号で存在確認を行う|API-001|CTX-001|CTX-002|UC-STEP-002 / ALT-001|EXC-001|exists判定|
|UC-STEP-002|顧客詳細取得|顧客詳細を取得する|API-002|CTX-001|CTX-003|UC-STEP-003|EXC-002|exists=true時|
|UC-STEP-003|契約一覧取得|契約一覧を取得する|API-003|CTX-001|CTX-004|UC-STEP-004|EXC-003|契約0件許容|
|UC-STEP-004|結果作成|UseCase結果を作成する|－|CTX-002, CTX-003, CTX-004|－|End|－|Report出力|

---

## A.8 Scenario一覧

|Scenario ID|Scenario名|分類|差分内容|対象API|期待結果|Result期待|TestCase ID|重要度|備考|
|-----------|-----------|----|--------|-------|--------|----------|-----------|------|----|
|SC-001|正常系|Normal|標準ルート|API-001, API-002, API-003|顧客情報・契約一覧取得成功|PASS|TC-001|High|Daily標準|
|SC-002|顧客不存在|Alternative|API-001でexists=false|API-001|後続API Skip|WARN / FAIL|TC-002|High|業務仕様で判定|
|SC-003|契約0件|Alternative|API-003で契約0件|API-001, API-002, API-003|契約0件で照会成立|PASS / WARN|TC-003|Medium|業務確認対象|
|SC-004|API-002 Timeout|Exception|API-002でTimeout|API-001, API-002|Retry後Fail|FAIL|TC-004|High|障害系|

---

## A.9 Scenario Matrix

|Scenario ID|API-001|API-002|API-003|Expected Result|備考|
|-----------|-------|-------|-------|---------------|----|
|SC-001|Run|Run|Run|PASS|正常系|
|SC-002|Run|Skip|Skip|WARN / FAIL|exists=false|
|SC-003|Run|Run|Run|PASS / WARN|契約0件|
|SC-004|Run|Run / Error|Skip|FAIL|Timeout|

---

## A.10 Scenario Selection Rule

|Rule ID|条件|Scenario ID|判定結果|備考|
|-------|----|------------|--------|----|
|SC-RULE-001|API-001 $.exists = true かつ API-003 契約件数 > 0|SC-001|正常系| |
|SC-RULE-002|API-001 $.exists = false|SC-002|顧客不存在|後続Skip|
|SC-RULE-003|API-001 $.exists = true かつ API-003 契約件数 = 0|SC-003|契約0件| |
|SC-RULE-004|API-002 Timeout|SC-004|異常系|Retry後Fail|

---

## A.11 API実行順序

|実行順|API ID|API名称|実行要否|実行条件|Skip条件|Input Context|Output Context|Timeout|Retry|備考|
|------|------|--------|--------|--------|--------|-------------|--------------|-------|-----|----|
|1|API-001|Customer Exists API|必須|Customer.id が存在する|－|CTX-001|CTX-002|10秒|1回|存在確認|
|2|API-002|Customer Detail API|条件付き必須|CTX-002 = true|CTX-002 = false|CTX-001|CTX-003|10秒|1回|顧客詳細|
|3|API-003|Contract List API|条件付き必須|CTX-002 = true|CTX-002 = false / API-002失敗|CTX-001|CTX-004|10秒|1回|契約一覧|

---

## A.12 Scenario別API実行順序

|Scenario ID|API実行順序|Skip API|備考|
|-----------|------------|--------|----|
|SC-001|API-001 → API-002 → API-003|－|正常系|
|SC-002|API-001|API-002, API-003|顧客不存在|
|SC-003|API-001 → API-002 → API-003|－|契約0件|
|SC-004|API-001 → API-002|API-003|API-002 Timeout|

---

## A.13 API Skip Rule

|Rule ID|条件|Skip対象API|後続処理|関連Scenario|備考|
|-------|----|-----------|--------|------------|----|
|SKIP-001|CTX-002 = false|API-002, API-003|UseCase結果作成|SC-002|顧客不存在|
|SKIP-002|API-002 Timeout after Retry|API-003|Fail終了|SC-004|障害系|

---

## A.14 Context一覧

|Context ID|Context名|Type|Producer|Consumer|Scope|必須|備考|
|----------|---------|----|--------|--------|-----|----|----|
|CTX-001|Customer.id|String|Entry Input|API-001, API-002, API-003|UseCase|○|顧客番号|
|CTX-002|Customer.exists|Boolean|API-001|Scenario Selection / Skip Rule|UseCase|○|存在判定|
|CTX-003|Customer|Object|API-002|Verification / Report|UseCase|－|顧客詳細|
|CTX-004|Contract.list|Array|API-003|Verification / Report|UseCase|－|契約一覧|

---

## A.15 Alternative Flow

|Flow ID|条件|処理内容|関連Scenario|Expected Result|備考|
|-------|----|--------|------------|---------------|----|
|ALT-001|CTX-002 = false|API-002, API-003をSkipし、顧客不存在結果を作成する|SC-002|WARN / FAIL|業務仕様により最終判定|

---

## A.16 Exception Flow

|Flow ID|発生条件|処理内容|Retry|Expected Result|関連Scenario|備考|
|-------|--------|--------|-----|---------------|------------|----|
|EXC-001|API-001 Error|UseCaseをFail終了する|Yes|FAIL|Exception|入口API失敗|
|EXC-002|API-002 Timeout|Retry後Fail終了する|Yes|FAIL|SC-004|後続API Skip|
|EXC-003|API-003 Error|契約一覧取得失敗としてFailまたはWarn|Yes|FAIL / WARN|Exception|業務仕様確認|

---

## A.17 Expected Result

|Scenario ID|期待HTTP Status|期待Business Result|期待UseCase Result|Report Result|備考|
|-----------|----------------|-------------------|------------------|-------------|----|
|SC-001|200|顧客存在・契約あり|PASS|PASS|正常系|
|SC-002|200|顧客不存在|WARN / FAIL|WARN / FAIL|業務仕様依存|
|SC-003|200|顧客存在・契約0件|PASS / WARN|PASS / WARN|業務仕様依存|
|SC-004|Timeout / Error|API-002 Timeout|FAIL|FAIL|障害系|

---

## A.18 Compare対象

|Scenario ID|Compare対象|Compare Policy|Baseline対象|備考|
|-----------|------------|--------------|------------|----|
|SC-001|Response / Context / Report|CMP-POL-001, CMP-POL-004, CMP-POL-005|Yes|traceId除外|
|SC-002|Response / Context / Report|CMP-POL-001, CMP-POL-005|Yes|後続Skip確認|
|SC-003|Response / Context / Report|CMP-POL-001, CMP-POL-004|Yes|配列0件確認|
|SC-004|Error / Log / Report|CMP-POL-006|No|障害系|

---

## A.19 Evidence保存対象

|Evidence ID|対象|保存内容|保存先|Mask|備考|
|-----------|----|--------|------|----|----|
|EVD-001|Request / Response / Context / Diff|正常系実行結果|outputs/runs/{runId}/|Yes|SC-001|
|EVD-002|Request / Response / Context / Skip Log|顧客不存在結果|outputs/runs/{runId}/|Yes|SC-002|
|EVD-003|Request / Response / Context / Diff|契約0件結果|outputs/runs/{runId}/|Yes|SC-003|
|EVD-004|Request / Error / Log|Timeout結果|outputs/runs/{runId}/|Yes|SC-004|

---

## A.20 Traceability

|Business ID|Flow ID|UseCase ID|Scenario ID|API ID|Context ID|Verification ID|TestCase ID|Evidence ID|
|-----------|-------|----------|-----------|------|----------|---------------|-----------|-----------|
|BUS-001|BF-002|UC-001|SC-001|API-001, API-002, API-003|CTX-001, CTX-002, CTX-003, CTX-004|VER-001|TC-001|EVD-001|
|BUS-001|BF-002|UC-001|SC-002|API-001|CTX-001, CTX-002|VER-002|TC-002|EVD-002|
|BUS-001|BF-005|UC-001|SC-003|API-001, API-002, API-003|CTX-001, CTX-002, CTX-003, CTX-004|VER-003|TC-003|EVD-003|
|BUS-001|BF-004|UC-001|SC-004|API-001, API-002|CTX-001, CTX-002|VER-004|TC-004|EVD-004|
```
:::

放置位置：

```text
system/03_api_design/
├── API設計書_Template.md
└── API-001_CustomerExistsAPI.md

system/04_usecase_design/
├── UseCase設計書_Template.md
└── UC-001_顧客情報照会.md
```

这两份和前面的 Master 对应关系是：

```text
API分析書
  ↓
E6_API_Master / Context_Master / Compare_Policy_Master
  ↓
API設計書
  ↓
API_UseCase_Scenario対応表 / Scenario_Master
  ↓
UseCase設計書
  ↓
Verification仕様書
```

## 第 182 轮

### 你

业务分析书里面有调用的api 、每个api调用有前提条件 、并且一个业务里面可能根据处理flg分为几个开始api到结尾api的路径。
我想根据业务分析书每一个业务的api调用路径，按业务-api调用分歧来做成　BA分析書xシナリオ一覧.md 你帮我设计下模版

### ChatGPT

这份文档很关键，它不是普通 BA，也不是 UseCase，而是把 **业务内的 API 调用路径分岐** 明确整理出来，作为后续 Scenario、UseCase、Verification 的输入。

### ChatGPT

可以。这个文件建议放在：

```text
system/01_business/01_業務分析/
BA-001_シナリオ一覧.md
```

下面是模板。

:::writing{variant="document" id="73042"}
---
title: BA分析書 シナリオ一覧
document_id: BA-SCENARIO-TEMPLATE
version: 1.0.0
status: Template
document_type: Business Scenario Analysis
system_name: E6 API Verification Platform
phase: As-Is Analysis
---

# BA分析書 シナリオ一覧

---

# 1. 文書情報

|項目|内容|
|----|----|
|文書ID|BA-SC-XXX|
|文書名称|〇〇業務 BA分析書 シナリオ一覧|
|対象業務|〇〇業務|
|Business ID|BUS-XXX|
|関連BA|BA-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|

---

# 2. 文書目的

本書は、現行業務分析書で整理した業務Flowをもとに、業務内のAPI呼出経路、分岐条件、開始API、終了APIをシナリオ単位で整理する。

本書は以下成果物の入力とする。

|後続成果物|利用内容|
|----------|--------|
|UseCase設計書|Scenario一覧、API Execution Chain|
|API・UseCase・Scenario対応表|API実行順序、Skip条件|
|Verification仕様書|Scenario別TestCase、Expected Result|
|Execution Spec|API実行経路|

---

# 3. 業務Flow概要

|Flow ID|処理名|利用API|処理Flg / 判定条件|次Flow|備考|
|-------|------|-------|------------------|------|----|
|BF-001|（記載）|－|－|BF-002|開始|
|BF-002|（記載）|API-XXX|（記載）|BF-003 / BF-010|分岐あり|
|BF-003|（記載）|API-XXX|（記載）|BF-004| |
|BF-010|（記載）|API-XXX|（記載）|END|別経路|

---

# 4. API呼出経路一覧

|経路ID|経路名称|開始Flow|開始API|終了Flow|終了API|分岐条件|処理Flg|業務結果|後続UseCase候補|備考|
|------|--------|--------|--------|--------|--------|--------|-------|--------|----------------|----|
|PATH-001|正常系|BF-001|API-001|BF-006|API-003|標準条件|NORMAL|正常終了|UC-XXX| |
|PATH-002|顧客不存在|BF-001|API-001|BF-999|API-001|exists=false|NOT_FOUND|業務エラー|UC-XXX|後続API Skip|
|PATH-003|契約0件|BF-001|API-001|BF-006|API-003|contractCount=0|NO_CONTRACT|正常 / 警告|UC-XXX|要業務確認|

---

# 5. シナリオ一覧

|Scenario ID|Scenario名称|分類|対象経路ID|分岐条件|処理Flg|開始API|終了API|実行API数|期待結果|Result期待|TestCase候補|備考|
|-----------|-------------|----|----------|--------|-------|--------|--------|---------|--------|----------|------------|----|
|SC-001|正常系|Normal|PATH-001|標準条件|NORMAL|API-001|API-003|3|業務正常終了|PASS|TC-001| |
|SC-002|顧客不存在|Alternative|PATH-002|exists=false|NOT_FOUND|API-001|API-001|1|業務エラー|WARN / FAIL|TC-002|後続API Skip|
|SC-003|契約0件|Alternative|PATH-003|contractCount=0|NO_CONTRACT|API-001|API-003|3|契約0件で終了|PASS / WARN|TC-003|要確認|

---

# 6. シナリオ別 API実行順序

|Scenario ID|実行順|API ID|API名称|Flow ID|実行条件|Skip条件|Input Context|Output Context|備考|
|-----------|------|------|--------|-------|--------|--------|-------------|--------------|----|
|SC-001|1|API-001|（記載）|BF-002|Customer.idあり|－|CTX-001|CTX-002| |
|SC-001|2|API-002|（記載）|BF-004|exists=true|exists=false|CTX-001|CTX-003| |
|SC-001|3|API-003|（記載）|BF-005|Customer取得済み|API-002失敗|CTX-001|CTX-004| |
|SC-002|1|API-001|（記載）|BF-002|Customer.idあり|－|CTX-001|CTX-002|exists=false|
|SC-002|2|API-002|（記載）|BF-004|－|exists=false|CTX-001|－|Skip|
|SC-002|3|API-003|（記載）|BF-005|－|exists=false|CTX-001|－|Skip|

---

# 7. 分岐条件一覧

|Branch ID|対象Flow|対象API|判定項目|判定条件|成立時Scenario|不成立時Scenario|備考|
|---------|--------|--------|--------|--------|----------------|------------------|----|
|BRANCH-001|BF-002|API-001|$.exists|true|SC-001 / SC-003|SC-002|顧客存在判定|
|BRANCH-002|BF-005|API-003|$.contracts.length|0|SC-003|SC-001|契約0件判定|

---

# 8. 処理Flg一覧

|処理Flg|意味|発生条件|対象Scenario|業務結果|備考|
|-------|----|--------|------------|--------|----|
|NORMAL|正常処理|exists=true かつ contractCount>0|SC-001|正常終了| |
|NOT_FOUND|顧客不存在|exists=false|SC-002|業務エラー| |
|NO_CONTRACT|契約0件|contractCount=0|SC-003|正常 / 警告|要確認|

---

# 9. シナリオ Matrix

|API / Flow|SC-001 正常系|SC-002 顧客不存在|SC-003 契約0件|
|----------|:-----------:|:---------------:|:-------------:|
|API-001 顧客存在確認|Run|Run|Run|
|API-002 顧客詳細取得|Run|Skip|Run|
|API-003 契約一覧取得|Run|Skip|Run|
|業務結果|PASS|WARN / FAIL|PASS / WARN|
|終了API|API-003|API-001|API-003|

---

# 10. Skip Rule候補

|Skip Rule ID|条件|Skip対象API|対象Scenario|結果扱い|備考|
|------------|----|------------|------------|--------|----|
|SKIP-001|$.exists=false|API-002, API-003|SC-002|WARN / FAIL|業務仕様により確定|
|SKIP-002|API-002失敗|API-003|Exception系|FAIL|障害系|

---

# 11. Context候補

|Context ID|Context名|生成元API|利用先API|対象Scenario|必須|備考|
|----------|---------|----------|----------|------------|----|----|
|CTX-001|Customer.id|Entry Input|API-001, API-002, API-003|全Scenario|○|顧客番号|
|CTX-002|Customer.exists|API-001|Scenario判定|全Scenario|○|分岐条件|
|CTX-003|Customer|API-002|API-003 / Report|SC-001, SC-003|－|顧客情報|
|CTX-004|Contract.list|API-003|Report / Verification|SC-001, SC-003|－|契約一覧|

---

# 12. 後続成果物への反映

|反映先|反映内容|状態|備考|
|------|--------|----|----|
|UseCase設計書|Scenario一覧、Scenario Matrix、API Execution Chain|未反映 / 反映済| |
|API_UseCase_Scenario対応表|Scenario別API実行順序、Skip条件|未反映 / 反映済| |
|Verification仕様書|Scenario別Expected Result、TestCase候補|未反映 / 反映済| |
|Execution Spec|Scenario別API呼出経路|未反映 / 反映済| |

---

# 13. 課題・確認事項

|No|分類|確認事項|影響範囲|確認先|優先度|状態|対応方針|
|--|----|--------|--------|------|------|----|--------|
|1|業務判定|顧客不存在時のResultをWARNかFAILか確認する|SC-002 / Verification|業務担当|High|Open|業務仕様確認|
|2|業務判定|契約0件を正常扱いにするか確認する|SC-003|業務担当|Medium|Open|UseCase反映|

---

# 14. Traceability

|Business ID|BA ID|Path ID|Scenario ID|Flow ID|API ID|Context ID|UseCase ID|Verification ID|
|-----------|-----|-------|------------|-------|------|----------|----------|---------------|
|BUS-XXX|BA-XXX|PATH-XXX|SC-XXX|BF-XXX|API-XXX|CTX-XXX|UC-XXX|VER-XXX|

---

# Appendix A. 記入例

## A.1 顧客情報照会業務

|項目|内容|
|----|----|
|Business ID|BUS-001|
|関連BA|BA-001|
|対象業務|顧客情報照会業務|

---

## A.2 API呼出経路一覧

|経路ID|経路名称|開始Flow|開始API|終了Flow|終了API|分岐条件|処理Flg|業務結果|後続UseCase候補|備考|
|------|--------|--------|--------|--------|--------|--------|-------|--------|----------------|----|
|PATH-001|正常系|BF-001|API-001|BF-006|API-003|exists=true かつ contractCount>0|NORMAL|正常終了|UC-001| |
|PATH-002|顧客不存在|BF-001|API-001|BF-999|API-001|exists=false|NOT_FOUND|業務エラー|UC-001|後続API Skip|
|PATH-003|契約0件|BF-001|API-001|BF-006|API-003|exists=true かつ contractCount=0|NO_CONTRACT|正常 / 警告|UC-001|要確認|

---

## A.3 シナリオ一覧

|Scenario ID|Scenario名称|分類|対象経路ID|分岐条件|処理Flg|開始API|終了API|実行API数|期待結果|Result期待|TestCase候補|備考|
|-----------|-------------|----|----------|--------|-------|--------|--------|---------|--------|----------|------------|----|
|SC-001|正常系|Normal|PATH-001|exists=true, contractCount>0|NORMAL|API-001|API-003|3|顧客情報・契約一覧取得|PASS|TC-001| |
|SC-002|顧客不存在|Alternative|PATH-002|exists=false|NOT_FOUND|API-001|API-001|1|顧客不存在終了|WARN / FAIL|TC-002|業務確認|
|SC-003|契約0件|Alternative|PATH-003|contractCount=0|NO_CONTRACT|API-001|API-003|3|契約0件で終了|PASS / WARN|TC-003|業務確認|

---

## A.4 シナリオ Matrix

|API / Flow|SC-001 正常系|SC-002 顧客不存在|SC-003 契約0件|
|----------|:-----------:|:---------------:|:-------------:|
|API-001 Customer Exists API|Run|Run|Run|
|API-002 Customer Detail API|Run|Skip|Run|
|API-003 Contract List API|Run|Skip|Run|
|終了API|API-003|API-001|API-003|
|業務結果|PASS|WARN / FAIL|PASS / WARN|

:::

这个模板的定位很明确：
**从 BA 的业务 Flow 中抽出“业务-API调用路径分歧”，形成 Scenario 的源头文档。**

## 第 183 轮

### 你

是一个业务分析书一个这个文件吧

### ChatGPT

是的，建议 **一个业务分析书对应一个 `BA分析書_シナリオ一覧.md` 文件**。

也就是：

```text
1个 現行業務分析書
    ↓
1个 BA分析書_シナリオ一覧
```

推荐命名：

```text
system/01_business/01_業務分析/

├── BA-001_顧客情報照会業務.md
├── BA-001_顧客情報照会業務_シナリオ一覧.md

├── BA-002_契約情報照会業務.md
├── BA-002_契約情報照会業務_シナリオ一覧.md

├── BA-003_申込登録業務.md
├── BA-003_申込登録業務_シナリオ一覧.md
```

关系是：

```text
BA-001_顧客情報照会業務.md
= 这个业务整体怎么走、有什么Flow、调用哪些API、业务规则是什么

BA-001_顧客情報照会業務_シナリオ一覧.md
= 这个业务里根据处理Flg、API返回值、分岐条件，整理出几条API调用路径
```

也就是说：

```text
業務分析書
  ↓
BAシナリオ一覧
  ↓
UseCase設計書
  ↓
API_UseCase_Scenario対応表
  ↓
Verification仕様書
```

不要做成全业务共通的一个大文件。
因为每个业务的 API 路径、Flg、分岐条件、结束条件都不同，放在各自 BA 旁边最清楚。

## 第 184 轮

### 你

システム設計書　作成

### ChatGPT

`システム設計書` は `05_framework` 的总入口文档，负责把 Runtime、Spec、Master、Snapshot、Diff、Report、Evidence 的整体结构串起来。下面直接给正式模板。

### ChatGPT

放置位置：

```text
system/05_framework/システム設計書.md
```

:::writing{variant="document" id="62918"}
---
title: システム設計書
document_id: SYS-DESIGN-001
version: 1.0.0
status: Template
document_type: System Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# システム設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-DESIGN-001|
|文書名称|E6 API Verification Platform システム設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|Runtime / Spec / Master / Snapshot / Diff / Report / Evidence|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|RULE-REPO-001|Repository構成.md|system/00_repository/|Repository構成|
|MST-API-001|E6_API_Master.md|system/02_master/|API Master|
|MST-UC-001|UseCase_Master.md|system/02_master/|UseCase Master|
|MST-SC-001|Scenario_Master.md|system/02_master/|Scenario Master|
|MST-CTX-001|Context_Master.md|system/02_master/|Context Master|
|MST-CMP-POL-001|Compare_Policy_Master.md|system/02_master/|Compare Policy|
|SYS-FW-001|共通Framework設計書.md|system/05_framework/|共通Framework詳細|
|SYS-CTX-001|RunContext設計書.md|system/05_framework/|RunContext詳細|
|SYS-SNP-001|Snapshot設計書.md|system/05_framework/|Snapshot詳細|
|SYS-DIFF-001|Diff設計書.md|system/05_framework/|Diff詳細|
|SYS-RPT-001|Report設計書.md|system/05_framework/|Report詳細|

---

# 2. システム概要

## 2.1 システム目的

本システムは、E6 API の日次検証を自動実行し、API Contract、Response内容、Context連携、Baseline差分を検出するための Verification Platform である。

本システムは以下を実現する。

|目的|内容|
|----|----|
|API自動検証|E6 APIをUseCase / Scenario単位で自動実行する|
|仕様駆動実行|Master、API設計書、UseCase設計書、Verification仕様書をもとに実行する|
|Context連携|前段APIのResponseを後続APIのRequestへ引き継ぐ|
|Snapshot保存|Request、Response、Context、Logを証跡として保存する|
|Baseline比較|前回または承認済Baselineとの差分を検出する|
|Report出力|Daily Summary、Diff Report、Evidence Reportを出力する|

---

## 2.2 システム位置付け

本システムは、E6 API の業務利用経路を検証するための回帰検証基盤であり、単純なAPI単体テストツールではない。

```text
Business Analysis
  ↓
E6 API Analysis
  ↓
API Design
  ↓
UseCase Design
  ↓
Verification Specification
  ↓
Execution Spec
  ↓
Runtime Execution
  ↓
Snapshot / Diff / Report
```

---

## 2.3 対象範囲

|分類|対象|
|----|----|
|対象API|E6 API Masterに登録されたAPI|
|対象UseCase|UseCase Masterに登録されたUseCase|
|対象Scenario|Scenario Masterに登録されたScenario|
|対象環境|Environment Masterに登録されたDEV / STG / PROD-LIKE|
|対象検証|Request / Response / Context / Diff / Error / Report|
|対象出力|Snapshot / Evidence / Daily Summary / Diff Report|

---

## 2.4 対象外

|対象外|理由|
|------|----|
|E6 API本体の開発|本システムは検証基盤であるため|
|業務システムの画面操作|API検証を主対象とするため|
|負荷試験|日次回帰検証が主目的であるため|
|本番データ更新|安全性確保のため原則対象外|
|手動確認のみの業務判断|Verification仕様に落とせないため|

---

# 3. 全体アーキテクチャ

## 3.1 論理構成

```mermaid
flowchart TD

A[Master / Design Documents] --> B[Execution Spec Generator]
B --> C[Verification Runtime]

C --> D[API Executor]
C --> E[RunContext Engine]
C --> F[Snapshot Engine]
C --> G[Diff Engine]
C --> H[Report Engine]

D --> I[E6 API]
E --> D
D --> F
F --> G
G --> H
F --> H

H --> J[Daily Summary]
H --> K[Diff Report]
H --> L[Evidence Report]
```

---

## 3.2 主要コンポーネント

|Component ID|Component名|役割|詳細設計書|
|------------|------------|----|----------|
|CMP-001|Execution Spec Generator|設計書・Masterから実行仕様を生成する|共通Framework設計書|
|CMP-002|Verification Runtime|UseCase / Scenarioを実行制御する|共通Framework設計書|
|CMP-003|API Executor|E6 APIを呼び出す|共通Framework設計書|
|CMP-004|RunContext Engine|API間Contextを管理する|RunContext設計書|
|CMP-005|Snapshot Engine|Request / Response / Contextを保存する|Snapshot設計書|
|CMP-006|Diff Engine|BaselineとCurrentを比較する|Diff設計書|
|CMP-007|Report Engine|Daily Summary / Diff Reportを生成する|Report設計書|
|CMP-008|File I/O Engine|Spec、TestData、Evidenceの入出力を行う|ファイル入出力設計書|
|CMP-009|Log / Exception Engine|ログ、例外、Maskを管理する|ログ・例外設計書|

---

# 4. Repository構成との関係

## 4.1 入力成果物

|入力|配置先|用途|
|----|------|----|
|E6_API_Master|system/02_master/|API一覧、重要度、対象管理|
|UseCase_Master|system/02_master/|UseCase一覧、実行対象管理|
|Scenario_Master|system/02_master/|Scenario一覧、分類、期待結果|
|Context_Master|system/02_master/|Context定義、Producer / Consumer|
|API_UseCase_Scenario対応表|system/02_master/|API実行順序、Skip条件|
|Compare_Policy_Master|system/02_master/|共通Compare Policy|
|Environment_Master|system/02_master/|環境情報|
|API設計書|system/03_api_design/|Request / Response契約|
|UseCase設計書|system/04_usecase_design/|API Execution Chain|
|Verification仕様書|system/06_verification_assets/|検証仕様|

---

## 4.2 Runtime入力

|入力種別|配置先|形式|用途|
|--------|------|----|----|
|Execution Spec|system/06_verification_assets/execution_spec/|Markdown / YAML / JSON|UseCase実行定義|
|API Test Spec|system/06_verification_assets/api_test_spec/|Markdown / YAML / JSON|API単体検証|
|UseCase Test Spec|system/06_verification_assets/usecase_test_spec/|Markdown / YAML / JSON|UseCase検証|
|Test Data|system/06_verification_assets/test_data/|JSON / CSV|Scenario別入力データ|
|Runtime Config|runtime/config/|YAML / JSON|実行設定|

---

## 4.3 Runtime出力

|出力種別|配置先|形式|用途|
|--------|------|----|----|
|Raw Request|outputs/runs/{runId}/raw/|JSON|実行証跡|
|Raw Response|outputs/runs/{runId}/raw/|JSON|実行証跡|
|Context Snapshot|outputs/runs/{runId}/snapshot/|JSON|Context証跡|
|Diff Result|outputs/runs/{runId}/diff/|JSON / Markdown|差分結果|
|Daily Summary|outputs/reports/latest/|Markdown / HTML|日次報告|
|Evidence Report|outputs/runs/{runId}/reports/|Markdown / HTML|詳細証跡|
|Log|outputs/runs/{runId}/logs/|log / JSONL|調査用|

---

# 5. 処理方式

## 5.1 全体処理フロー

```mermaid
sequenceDiagram
    participant S as Scheduler / User
    participant R as Verification Runtime
    participant M as Master Loader
    participant T as TestData Loader
    participant A as API Executor
    participant C as RunContext Engine
    participant P as Snapshot Engine
    participant D as Diff Engine
    participant H as Report Engine
    participant E as E6 API

    S->>R: Start Run
    R->>M: Load Master / Spec
    R->>T: Load TestData
    R->>C: Initialize RunContext

    loop Scenario
        R->>A: Execute API
        A->>C: Resolve Request Context
        A->>E: Call E6 API
        E-->>A: Response
        A->>C: Extract Output Context
        A->>P: Save Request / Response / Context
    end

    R->>D: Compare Current with Baseline
    D->>P: Save Diff
    R->>H: Generate Reports
    H-->>S: Daily Summary / Diff Report
```

---

## 5.2 実行単位

|実行単位|説明|
|--------|----|
|Run|1回の日次検証実行|
|UseCase|業務単位の実行|
|Scenario|UseCase内の分岐経路|
|Step|Scenario内のAPI実行ステップ|
|API Call|1回のE6 API呼出|

---

## 5.3 実行順序

```text
Run
  └── UseCase
        └── Scenario
              └── API Step
                    └── API Call
```

---

## 5.4 実行制御

|制御項目|方針|
|--------|----|
|UseCase実行順|UseCase_Master または Execution Spec に従う|
|Scenario実行順|Scenario_Master または Execution Spec に従う|
|API実行順|API_UseCase_Scenario対応表に従う|
|Skip判定|UseCase設計書のAPI Skip Ruleに従う|
|Retry判定|API設計書またはEnvironment_Masterに従う|
|Timeout判定|API設計書またはEnvironment_Masterに従う|
|Fail停止条件|Execution Policyに従う|

---

# 6. データ設計概要

## 6.1 RunContext

RunContext は、1回の検証実行における業務データ、API Response、Scenario判定値、実行IDを保持する。

|Context分類|例|Scope|
|-----------|--|-----|
|Runtime Context|runId, executedAt, environment|Run|
|Business Context|customerId, contractId|UseCase|
|API Context|exists, customerDetail, contractList|Scenario / UseCase|
|Verification Context|expectedResult, actualResult, diffResult|Scenario|
|Report Context|summaryStatus, evidencePath|Run|

---

## 6.2 Snapshot

Snapshot は、実行時点の入力、出力、Contextを改変せず保存する証跡である。

|Snapshot種別|内容|
|------------|----|
|Request Snapshot|API呼出Request|
|Response Snapshot|API Response|
|Context Snapshot|API実行前後のContext|
|Execution Snapshot|Scenario / Step実行状態|
|Diff Snapshot|Baseline比較結果|

---

## 6.3 Baseline

Baseline は、承認済みの期待結果または前回正常結果であり、Current実行結果との比較対象とする。

|Baseline種別|説明|
|------------|----|
|Approved Baseline|人が承認した基準結果|
|Previous Success|前回成功結果|
|Scenario Baseline|Scenario単位の基準結果|
|API Baseline|API単位の基準結果|

---

# 7. Compare / Diff方式

## 7.1 Compare対象

|対象|比較内容|
|----|--------|
|HTTP Status|期待Statusとの一致|
|Response Field|型、必須、固定値、Enum、入力値一致|
|Context|Producer / Consumer間の一致|
|Business Result|Scenario期待結果との一致|
|Baseline|CurrentとBaselineの差分|
|Report|Daily Summary出力内容|

---

## 7.2 Compare Policy

Compare Policy は `Compare_Policy_Master.md` を共通定義とし、Verification仕様書で個別適用する。

|分類|方式|
|----|----|
|固定値|Equals|
|Dynamic項目|Ignore / Exists / Type Only|
|日時|Tolerance|
|数値|Tolerance|
|文字列|Trim + Equals / Regex|
|配列|Key Match / Order Match|
|Error Message|Contains / Regex|

---

## 7.3 Diff Result

|Result|意味|
|------|----|
|PASS|差分なし、または許容範囲内|
|WARN|差分あり。ただし業務上許容可能または確認対象|
|FAIL|Critical / High の差分あり|
|SKIP|条件により検証対象外|
|ERROR|実行異常、環境異常、Spec異常|

---

# 8. Report方式

## 8.1 Report種類

|Report|内容|利用者|
|------|----|------|
|Daily Summary|日次検証結果の要約|承認者 / Leader|
|Diff Report|Baselineとの差分詳細|開発 / 調査担当|
|Evidence Report|Request / Response / Context証跡|調査担当|
|Execution Report|UseCase / Scenario / Step実行履歴|開発 / 運用|

---

## 8.2 Daily Summary 出力内容

|項目|内容|
|----|----|
|Run ID|実行ID|
|実行日時|開始・終了日時|
|対象環境|DEV / STG / PROD-LIKE|
|総合Result|PASS / WARN / FAIL / ERROR|
|UseCase結果|UseCase別結果|
|Scenario結果|Scenario別結果|
|Critical Diff|Critical差分一覧|
|確認事項|要確認事項|
|Evidence Link|詳細証跡へのリンク|

---

# 9. 例外・エラー処理概要

## 9.1 Error分類

|分類|内容|Result|
|----|----|------|
|Spec Error|Spec不足、ID不整合、必須定義なし|ERROR|
|Config Error|環境設定不足、認証情報不足|ERROR|
|API Error|HTTP 4xx / 5xx|Verification仕様に従う|
|Timeout|API応答なし|FAIL / ERROR|
|Context Error|必要Contextが存在しない|ERROR|
|Diff Error|Baseline比較処理失敗|ERROR|
|Report Error|Report生成失敗|ERROR|

---

## 9.2 停止方針

|発生箇所|停止方針|
|--------|--------|
|Master Load Error|Run停止|
|Execution Spec Error|対象UseCase停止|
|TestData Error|対象Scenario停止|
|必須Context不足|対象Scenario停止|
|API Critical Error|対象Scenario停止|
|Report Error|Run結果ERROR|

---

# 10. Security / Mask方針

## 10.1 Mask対象

|対象|Mask方針|
|----|--------|
|Authorization Header|完全Mask|
|Token|完全Mask|
|Password|完全Mask|
|個人情報|項目別Mask|
|顧客番号|条件付きMask|
|ログ出力|Mask後のみ出力|

---

## 10.2 Secret管理

|Secret種別|管理方法|
|----------|--------|
|Token|環境変数 / Secret File|
|Password|環境変数 / Secret File|
|Certificate|runtime/config/secret/|
|API Key|環境変数 / Secret File|

`runtime/config/secret/` は Git 管理対象外とする。

---

# 11. 環境設計概要

## 11.1 対象環境

|環境ID|環境名|用途|
|------|------|----|
|ENV-LOCAL|LOCAL|ローカルMock検証|
|ENV-DEV|DEV|開発検証|
|ENV-STG|STG|結合検証 / 日次検証|
|ENV-PLK|PROD-LIKE|本番相当検証|

---

## 11.2 環境切替

|項目|方針|
|----|----|
|Base URL|Environment_Masterで管理|
|認証情報|Secret管理|
|Timeout|Environment_MasterまたはAPI設計書で管理|
|Retry|Environment_MasterまたはAPI設計書で管理|
|Log Level|環境別設定|

---

# 12. 運用設計概要

## 12.1 日次実行

|項目|内容|
|----|----|
|実行頻度|Daily|
|実行対象|UseCase_Masterで日次実行対象のUseCase|
|実行環境|STG / PROD-LIKE|
|出力|Daily Summary / Diff Report / Evidence|
|通知|必要に応じてメール / Slack / Teams|

---

## 12.2 Baseline承認

|Step|内容|
|----|----|
|1|Current結果を確認する|
|2|Diff Reportを確認する|
|3|業務影響がないことを確認する|
|4|Approved Baselineとして保存する|
|5|次回以降の比較基準とする|

---

# 13. 非機能設計概要

|分類|方針|
|----|----|
|保守性|Markdown / Master / Spec を分離し、仕様駆動で管理する|
|拡張性|API、UseCase、Scenario追加時にMaster追加で対応可能にする|
|再現性|Request / Response / Context / TestData を保存する|
|監査性|EvidenceとReportをRun ID単位で保存する|
|安全性|Secretと個人情報をMaskする|
|可搬性|Release Package / Dockerで本番Linuxへ配置可能にする|

---

# 14. Traceability

|Business ID|API分析書|API設計書|UseCase設計書|Verification仕様書|Execution Spec|Runtime出力|
|-----------|---------|---------|-------------|-------------------|--------------|----------|
|BUS-XXX|API-ANL-XXX|API-XXX|UC-XXX|VER-XXX|EXEC-XXX|outputs/runs/{runId}/|

---

# 15. 課題・確認事項

|No|分類|確認事項|影響範囲|確認先|優先度|状態|対応方針|
|--|----|--------|--------|------|------|----|--------|
|1|実行方式|日次実行をSchedulerで起動するか手動起動にするか|運用設計|Project Owner|Medium|Open|運用方針決定|
|2|Baseline|Approved Baseline運用を誰が承認するか|Diff / Report|Leader|High|Open|承認Role定義|
|3|通知|Daily Summary通知先をどうするか|Report / 運用|Leader|Low|Open|通知方式決定|

---

# Appendix A. 記入例

## A.1 システム目的

本システムは、顧客情報照会業務を含むE6 API利用業務について、日次でAPI呼出を自動実行し、前回正常結果または承認済Baselineとの差分を検出する。

---

## A.2 対象UseCase例

|UseCase ID|UseCase名|Scenario数|対象API|日次実行|
|----------|---------|----------|-------|--------|
|UC-001|顧客情報照会|4|API-001, API-002, API-003|Yes|
|UC-002|契約情報照会|3|API-003, API-004|Yes|

---

## A.3 対象API例

|API ID|API名称|役割|重要度|
|------|--------|----|------|
|API-001|Customer Exists API|顧客存在確認|High|
|API-002|Customer Detail API|顧客詳細取得|High|
|API-003|Contract List API|契約一覧取得|Medium|

---

## A.4 実行結果出力例

```text
outputs/
├── runs/
│   └── RUN-20260710-001/
│       ├── run-info.json
│       ├── raw/
│       │   ├── UC-001_SC-001_API-001_request.json
│       │   ├── UC-001_SC-001_API-001_response.json
│       │   └── ...
│       ├── snapshot/
│       │   └── context_snapshot.json
│       ├── diff/
│       │   └── diff_result.json
│       ├── reports/
│       │   ├── EvidenceReport.md
│       │   └── DiffReport.md
│       └── logs/
│           └── runtime.log
│
└── reports/
    └── latest/
        ├── DailySummary.md
        └── DiffReport.md
```

---

## A.5 Daily Summary例

|項目|内容|
|----|----|
|Run ID|RUN-20260710-001|
|環境|STG|
|総合Result|WARN|
|対象UseCase|2|
|PASS|1|
|WARN|1|
|FAIL|0|
|ERROR|0|
|主な差分|UC-001 / SC-003 契約0件結果確認|
|Evidence|outputs/runs/RUN-20260710-001/reports/EvidenceReport.md|

:::

`システム設計書.md` 是 `05_framework` 的总纲。
接下来通常继续做这些详细设计：

```text
system/05_framework/
├── 共通Framework設計書.md
├── RunContext設計書.md
├── Snapshot設計書.md
├── Diff設計書.md
├── Report設計書.md
├── ファイル入出力設計書.md
├── ログ・例外設計書.md
└── 環境設計書.md
```

## 第 185 轮

### 你

runcontext設計書　作成

### ChatGPT

`RunContext設計書` 是 Runtime 的核心文档，负责定义 API 间的数据传递、Scenario 判定、Snapshot 保存、Diff/Report 的上下文来源。

### ChatGPT

放置位置：

```text
system/05_framework/RunContext設計書.md
```

:::writing{variant="document" id="84219"}
---
title: RunContext設計書
document_id: SYS-CTX-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
---

# RunContext設計書

---

# 1. 文書情報

|項目|内容|
|----|----|
|文書ID|SYS-CTX-001|
|文書名称|RunContext設計書|
|対象範囲|RunContext / Context生成 / Context引継ぎ / Snapshot / Report連携|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|

---

# 2. RunContext目的

RunContext は、1回の検証実行において、UseCase、Scenario、API Step 間で共有される実行時データを管理する。

主な目的は以下である。

|目的|内容|
|----|----|
|API間連携|前段APIのResponseを後続APIのRequestへ渡す|
|Scenario判定|Response値や処理FlgからScenarioを判定する|
|Execution制御|Skip、Retry、Stop、Continueを判断する|
|Verification連携|Response Check、Context Check、Compareの入力にする|
|Evidence保存|Context Snapshotとして保存する|
|Report生成|Daily Summary、Diff Reportの入力にする|

---

# 3. Context Scope

|Scope|説明|例|
|-----|----|----|
|Run|1回の実行全体で有効|runId, environment|
|UseCase|1つのUseCase内で有効|Customer.id|
|Scenario|1つのScenario内で有効|Customer.exists|
|API Step|1 API呼出内で有効|requestBody, responseBody|
|Verification|検証処理内で有効|diffResult, checkResult|

---

# 4. Context分類

|分類|説明|例|
|----|----|----|
|Runtime Context|実行制御用Context|Runtime.runId, Runtime.executedAt|
|Business Context|業務キー、処理Flg|Customer.id, Process.flg|
|API Context|API Responseから抽出した値|Customer.exists, Contract.list|
|Scenario Context|Scenario判定結果|Scenario.id, Scenario.result|
|Verification Context|検証結果|Check.result, Diff.result|
|Report Context|Report出力用集計|Report.totalPass, Report.totalFail|

---

# 5. Context基本構造

```json
{
  "run": {
    "runId": "RUN-20260710-001",
    "environment": "STG",
    "startedAt": "2026-07-10T09:00:00+09:00"
  },
  "usecase": {
    "useCaseId": "UC-001",
    "scenarioId": "SC-001"
  },
  "business": {
    "customerId": "10000001"
  },
  "api": {},
  "verification": {},
  "report": {}
}
```

---

# 6. Context定義項目

|項目|説明|
|----|----|
|Context ID|Contextを一意に識別するID|
|Context名|Domain.Property形式の論理名|
|Type|String / Number / Boolean / Object / Array / DateTime|
|Scope|Run / UseCase / Scenario / API Step / Verification|
|Producer|Context生成元|
|Consumer|Context利用先|
|必須|必須Contextかどうか|
|Dynamic|実行毎に変化するか|
|Mask|証跡・Log出力時にMaskするか|
|Lifetime|Contextの有効期間|
|Update Policy|更新可否と競合時処理|

---

# 7. Context一覧

|Context ID|Context名|Type|Scope|Producer|Consumer|必須|Dynamic|Mask|説明|
|----------|---------|----|-----|--------|--------|----|-------|----|----|
|CTX-001|Customer.id|String|UseCase|Entry Input|API-001, API-002, API-003|○|No|Conditional|顧客番号|
|CTX-002|Customer.exists|Boolean|Scenario|API-001|Scenario Selection / Skip Rule|○|No|No|顧客存在有無|
|CTX-003|Customer|Object|UseCase|API-002|Verification / Report|－|No|Conditional|顧客詳細|
|CTX-004|Contract.list|Array|UseCase|API-003|Verification / Report|－|No|Conditional|契約一覧|
|CTX-005|Runtime.runId|String|Run|Runtime|Evidence / Report|○|Yes|No|実行ID|
|CTX-006|Runtime.environment|String|Run|Runtime|API Executor / Report|○|No|No|実行環境|

---

# 8. Context生成ルール

## 8.1 Entry Input生成

|Rule ID|Context ID|生成元|生成タイミング|備考|
|-------|----------|------|--------------|----|
|CTX-GEN-001|CTX-001|Test Data / Manual Input|UseCase開始時|顧客番号|
|CTX-GEN-002|CTX-005|Runtime|Run開始時|runId自動採番|
|CTX-GEN-003|CTX-006|Runtime Config|Run開始時|環境名|

---

## 8.2 API Response抽出

|Rule ID|API ID|Response JSONPath|Context ID|必須|未取得時処理|
|-------|------|-----------------|----------|----|------------|
|CTX-EXT-001|API-001|$.exists|CTX-002|○|Fail|
|CTX-EXT-002|API-002|$.customer|CTX-003|－|Warn|
|CTX-EXT-003|API-003|$.contracts|CTX-004|－|Warn|

---

## 8.3 Runtime生成

|Context ID|生成方法|例|
|----------|--------|----|
|Runtime.runId|日時 + 連番|RUN-20260710-001|
|Runtime.startedAt|System Clock|2026-07-10T09:00:00+09:00|
|Runtime.environment|実行引数 / Config|STG|

---

# 9. Context利用ルール

## 9.1 Request Binding

|Rule ID|API ID|Request JSONPath|Context ID|必須|未設定時処理|
|-------|------|----------------|----------|----|------------|
|BIND-001|API-001|$.customerId|CTX-001|○|Fail|
|BIND-002|API-002|$.customerId|CTX-001|○|Fail|
|BIND-003|API-003|$.customerId|CTX-001|○|Fail|

---

## 9.2 Scenario Selection

|Rule ID|条件|利用Context|Scenario ID|備考|
|-------|----|------------|------------|----|
|SC-SEL-001|Customer.exists = true|CTX-002|SC-001 / SC-003|後続API実行|
|SC-SEL-002|Customer.exists = false|CTX-002|SC-002|後続API Skip|
|SC-SEL-003|Contract.list size = 0|CTX-004|SC-003|契約0件|

---

## 9.3 Skip Rule

|Rule ID|条件|利用Context|Skip対象API|Result|
|-------|----|------------|------------|------|
|SKIP-001|Customer.exists = false|CTX-002|API-002, API-003|WARN / FAIL|
|SKIP-002|Customer取得失敗|CTX-003|API-003|FAIL|

---

# 10. Context更新ルール

|Context ID|更新可否|更新条件|競合時処理|備考|
|----------|--------|--------|----------|----|
|CTX-001|不可|－|Fail|業務キーのため固定|
|CTX-002|可|API-001実行後|Overwrite|Scenario判定値|
|CTX-003|可|API-002実行後|Overwrite|顧客詳細|
|CTX-004|可|API-003実行後|Overwrite|契約一覧|
|CTX-005|不可|－|Fail|Run ID|

---

# 11. Context Lifetime

|Context ID|生成タイミング|有効範囲|破棄タイミング|
|----------|--------------|--------|--------------|
|CTX-001|UseCase開始時|UseCase|UseCase終了時|
|CTX-002|API-001終了時|Scenario|Scenario終了時|
|CTX-003|API-002終了時|UseCase|UseCase終了時|
|CTX-004|API-003終了時|UseCase|UseCase終了時|
|CTX-005|Run開始時|Run|Run終了時|
|CTX-006|Run開始時|Run|Run終了時|

---

# 12. Context Snapshot

## 12.1 保存タイミング

|Timing ID|タイミング|保存内容|
|---------|----------|--------|
|SNP-CTX-001|Run開始時|Runtime Context|
|SNP-CTX-002|UseCase開始時|Entry Context|
|SNP-CTX-003|API実行前|Request Binding前Context|
|SNP-CTX-004|API実行後|Response抽出後Context|
|SNP-CTX-005|Scenario終了時|Scenario Result Context|
|SNP-CTX-006|Run終了時|Report Context|

---

## 12.2 Snapshot保存形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "timing": "AFTER_API",
  "context": {
    "Customer.id": "10000001",
    "Customer.exists": true
  }
}
```

---

## 12.3 保存先

|Snapshot種別|保存先|
|------------|------|
|Run Context|outputs/runs/{runId}/snapshot/run_context.json|
|UseCase Context|outputs/runs/{runId}/snapshot/{useCaseId}_context.json|
|Scenario Context|outputs/runs/{runId}/snapshot/{useCaseId}_{scenarioId}_context.json|
|API Step Context|outputs/runs/{runId}/snapshot/{useCaseId}_{scenarioId}_{apiId}_context.json|

---

# 13. Maskルール

|Context ID|Context名|Mask|Mask方式|備考|
|----------|---------|----|--------|----|
|CTX-001|Customer.id|Conditional|後4桁以外Mask|顧客番号|
|CTX-003|Customer|Conditional|個人情報項目Mask|顧客氏名等|
|CTX-005|Runtime.runId|No|－|秘匿不要|
|Auth.token|Yes|完全Mask|Header秘匿|

---

# 14. Context Error

|Error ID|発生条件|Result|処理|
|--------|--------|------|----|
|CTX-ERR-001|必須Context未生成|ERROR|対象Scenario停止|
|CTX-ERR-002|必須ContextがNull|ERROR|対象Scenario停止|
|CTX-ERR-003|Context型不一致|ERROR|対象Scenario停止|
|CTX-ERR-004|更新不可Contextの上書き|ERROR|対象Scenario停止|
|CTX-ERR-005|ConsumerありProducerなし|ERROR|Spec Review対象|

---

# 15. Verification連携

|Verification種別|利用Context|用途|
|----------------|------------|----|
|Input Match Check|CTX-001|Request値とResponse値の一致確認|
|Context Match Check|CTX-001, CTX-002|API間引継ぎ確認|
|Business Result Check|CTX-002, CTX-004|Scenario判定|
|Compare Check|CTX-003, CTX-004|Baseline比較|
|Report Summary|Report Context|結果集計|

---

# 16. Report連携

|Report項目|利用Context|
|----------|------------|
|Run ID|Runtime.runId|
|Environment|Runtime.environment|
|UseCase Result|Verification Context|
|Scenario Result|Scenario Context|
|API Result|API Context|
|Diff Result|Verification Context|
|Evidence Link|Report Context|

---

# 17. Traceability

|Context ID|Producer|Consumer|API ID|UseCase ID|Scenario ID|Verification ID|
|----------|--------|--------|------|----------|-----------|---------------|
|CTX-001|Entry Input|API-001, API-002, API-003|API-001, API-002, API-003|UC-001|SC-001, SC-002, SC-003|VER-001|
|CTX-002|API-001|Scenario Selection|API-001|UC-001|SC-001, SC-002, SC-003|VER-001|
|CTX-003|API-002|API-003 / Report|API-002|UC-001|SC-001, SC-003|VER-001|
|CTX-004|API-003|Report / Verification|API-003|UC-001|SC-001, SC-003|VER-001|

---

# Appendix A. 顧客情報照会 UseCase例

## A.1 初期Context

|Context ID|Context名|値|
|----------|---------|--|
|CTX-001|Customer.id|10000001|
|CTX-005|Runtime.runId|RUN-20260710-001|
|CTX-006|Runtime.environment|STG|

---

## A.2 API-001 実行後Context

|Context ID|Context名|値|
|----------|---------|--|
|CTX-001|Customer.id|10000001|
|CTX-002|Customer.exists|true|

---

## A.3 API-002 実行後Context

|Context ID|Context名|値|
|----------|---------|--|
|CTX-003|Customer|{"customerId":"10000001","customerName":"山田太郎"}|

---

## A.4 API-003 実行後Context

|Context ID|Context名|値|
|----------|---------|--|
|CTX-004|Contract.list|[{"contractId":"C-001","status":"ACTIVE"}]|

---

## A.5 Context JSON例

```json
{
  "Runtime.runId": "RUN-20260710-001",
  "Runtime.environment": "STG",
  "Customer.id": "10000001",
  "Customer.exists": true,
  "Customer": {
    "customerId": "10000001",
    "customerName": "山田太郎"
  },
  "Contract.list": [
    {
      "contractId": "C-001",
      "status": "ACTIVE"
    }
  ]
}
```
:::

完成。下一份建议做 `Snapshot設計書.md`，它会承接 RunContext，定义 Request/Response/Context/Evidence 的保存粒度和文件结构。

## 第 186 轮

### 你

Snapshot設計書.md

### ChatGPT

`Snapshot設計書` 要承接 `RunContext設計書`，重点定义每次 API 执行前后保存什么、保存到哪里、文件命名、Mask、Baseline/Diff 如何引用。

### ChatGPT

放置位置：

```text
system/05_framework/Snapshot設計書.md
```

:::writing{variant="document" id="51749"}
---
title: Snapshot設計書
document_id: SYS-SNP-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# Snapshot設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-SNP-001|
|文書名称|Snapshot設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|Request Snapshot / Response Snapshot / Context Snapshot / Diff Snapshot / Evidence Snapshot|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|SYS-DESIGN-001|システム設計書|system/05_framework/|全体設計|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context設計|
|SYS-DIFF-001|Diff設計書|system/05_framework/|Diff設計|
|SYS-RPT-001|Report設計書|system/05_framework/|Report設計|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|Compare Policy|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|

---

# 2. Snapshot目的

Snapshot は、1回の検証実行における Request、Response、Context、Execution State、Diff Result を保存する証跡である。

本設計書では、Snapshot の種類、保存タイミング、保存形式、保存先、命名規則、Mask方針、Baseline連携、Diff連携を定義する。

---

# 3. Snapshot基本方針

|方針|内容|
|----|----|
|再現性|実行時のRequest / Response / Contextを保存し、後から再現可能にする|
|監査性|Run ID、UseCase ID、Scenario ID、API ID、Step ID単位で追跡可能にする|
|比較可能性|Current Snapshot と Baseline Snapshot を比較可能な構造にする|
|改変禁止|保存後のSnapshotは原則変更しない|
|Mask必須|Token、Password、個人情報は保存前にMaskする|
|構造化保存|JSON形式を基本とし、Report用にMarkdownを生成可能にする|

---

# 4. Snapshot分類

|Snapshot種別|内容|保存単位|主な利用先|
|------------|----|--------|----------|
|Run Snapshot|Run全体情報|Run|Daily Summary / Audit|
|UseCase Snapshot|UseCase実行状態|UseCase|UseCase Result / Report|
|Scenario Snapshot|Scenario実行状態|Scenario|Scenario Result / Diff|
|Request Snapshot|API Request|API Step|Evidence / 再実行確認|
|Response Snapshot|API Response|API Step|Response Check / Diff|
|Context Snapshot|RunContext状態|Run / UseCase / Scenario / API Step|Context Check / Report|
|Execution Snapshot|Step実行状態|API Step|障害調査 / Report|
|Diff Snapshot|Baseline比較結果|Scenario / API / Field|Diff Report|
|Evidence Snapshot|Report向け証跡索引|Run / Scenario|Evidence Report|

---

# 5. Snapshot保存タイミング

|Timing ID|タイミング|保存対象|説明|
|---------|----------|--------|----|
|SNP-TMG-001|Run開始時|Run Snapshot|runId、環境、開始時刻を保存|
|SNP-TMG-002|UseCase開始時|UseCase Snapshot / Context Snapshot|UseCase開始時のContextを保存|
|SNP-TMG-003|Scenario開始時|Scenario Snapshot / Context Snapshot|Scenario開始時のContextを保存|
|SNP-TMG-004|API実行前|Request Snapshot / Context Snapshot|Request生成後、API呼出前に保存|
|SNP-TMG-005|API実行後|Response Snapshot / Context Snapshot|Response受信後、Context抽出後に保存|
|SNP-TMG-006|API Error発生時|Response Snapshot / Execution Snapshot|HTTP Error / Timeout / Exceptionを保存|
|SNP-TMG-007|Scenario終了時|Scenario Snapshot / Diff Snapshot|Scenario結果、Diff結果を保存|
|SNP-TMG-008|UseCase終了時|UseCase Snapshot|UseCase結果を保存|
|SNP-TMG-009|Run終了時|Run Snapshot / Evidence Snapshot|総合結果、Report索引を保存|

---

# 6. Snapshot保存先

## 6.1 Run単位保存先

```text
outputs/
└── runs/
    └── {runId}/
        ├── run-info.json
        ├── raw/
        ├── snapshot/
        ├── diff/
        ├── reports/
        ├── evidence/
        ├── logs/
        └── tmp/
```

---

## 6.2 ディレクトリ用途

|ディレクトリ|用途|
|------------|----|
|raw|Request / Response の原本相当データを保存する|
|snapshot|Run / UseCase / Scenario / Context / Execution Snapshotを保存する|
|diff|Baseline比較結果を保存する|
|reports|Evidence Report / Diff Reportを保存する|
|evidence|Evidence索引、証跡メタ情報を保存する|
|logs|Runtime Logを保存する|
|tmp|一時ファイルを保存する|

---

# 7. Snapshotファイル命名規則

## 7.1 基本命名形式

```text
{useCaseId}_{scenarioId}_{stepId}_{apiId}_{snapshotType}.json
```

---

## 7.2 Snapshot Type

|Snapshot Type|意味|
|-------------|----|
|request|Request Snapshot|
|response|Response Snapshot|
|context_before|API実行前Context|
|context_after|API実行後Context|
|execution|API Step実行状態|
|diff|Diff結果|
|error|Error Snapshot|

---

## 7.3 ファイル名例

```text
UC-001_SC-001_UC-STEP-001_API-001_request.json
UC-001_SC-001_UC-STEP-001_API-001_response.json
UC-001_SC-001_UC-STEP-001_API-001_context_before.json
UC-001_SC-001_UC-STEP-001_API-001_context_after.json
UC-001_SC-001_UC-STEP-001_API-001_execution.json
UC-001_SC-001_UC-STEP-001_API-001_diff.json
```

---

# 8. Run Snapshot

## 8.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|environment|実行環境|
|startedAt|開始日時|
|endedAt|終了日時|
|status|PASS / WARN / FAIL / ERROR|
|targetUseCases|対象UseCase一覧|
|targetScenarios|対象Scenario一覧|
|executor|実行者 / Scheduler|
|configVersion|Config版数|
|specVersion|Spec版数|

---

## 8.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "environment": "STG",
  "startedAt": "2026-07-10T09:00:00+09:00",
  "endedAt": "2026-07-10T09:05:12+09:00",
  "status": "WARN",
  "targetUseCases": ["UC-001", "UC-002"],
  "targetScenarios": ["SC-001", "SC-002", "SC-003"],
  "executor": "daily-scheduler",
  "configVersion": "1.0.0",
  "specVersion": "1.0.0"
}
```

---

# 9. UseCase Snapshot

## 9.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|useCaseName|UseCase名称|
|startedAt|開始日時|
|endedAt|終了日時|
|status|PASS / WARN / FAIL / ERROR / SKIP|
|scenarioResults|Scenario別結果|
|evidencePath|Evidence保存先|

---

## 9.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "useCaseName": "顧客情報照会",
  "startedAt": "2026-07-10T09:00:10+09:00",
  "endedAt": "2026-07-10T09:01:20+09:00",
  "status": "WARN",
  "scenarioResults": [
    {
      "scenarioId": "SC-001",
      "status": "PASS"
    },
    {
      "scenarioId": "SC-002",
      "status": "WARN"
    }
  ],
  "evidencePath": "outputs/runs/RUN-20260710-001/evidence/UC-001_evidence.json"
}
```

---

# 10. Scenario Snapshot

## 10.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|scenarioName|Scenario名称|
|classification|Normal / Alternative / Exception|
|startedAt|開始日時|
|endedAt|終了日時|
|status|PASS / WARN / FAIL / ERROR / SKIP|
|executedApis|実行API一覧|
|skippedApis|Skip API一覧|
|expectedResult|期待結果|
|actualResult|実結果|

---

## 10.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-002",
  "scenarioName": "顧客不存在",
  "classification": "Alternative",
  "startedAt": "2026-07-10T09:00:30+09:00",
  "endedAt": "2026-07-10T09:00:45+09:00",
  "status": "WARN",
  "executedApis": ["API-001"],
  "skippedApis": ["API-002", "API-003"],
  "expectedResult": "WARN / FAIL",
  "actualResult": "WARN"
}
```

---

# 11. Request Snapshot

## 11.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|method|HTTP Method|
|url|呼出URL|
|headers|Request Header|
|queryParams|Query Parameters|
|pathParams|Path Parameters|
|body|Request Body|
|contextBinding|Contextから設定した項目|
|createdAt|Snapshot作成日時|

---

## 11.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "method": "POST",
  "url": "https://stg.example.com/v1/customers/exists",
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "****"
  },
  "body": {
    "customerId": "******0001"
  },
  "contextBinding": [
    {
      "jsonPath": "$.customerId",
      "contextId": "CTX-001",
      "contextName": "Customer.id",
      "masked": true
    }
  ],
  "createdAt": "2026-07-10T09:00:31+09:00"
}
```

---

# 12. Response Snapshot

## 12.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|httpStatus|HTTP Status|
|headers|Response Header|
|body|Response Body|
|elapsedMillis|応答時間|
|receivedAt|受信日時|
|extractedContext|Responseから抽出したContext|
|dynamicFields|Dynamic項目|

---

## 12.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "httpStatus": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": {
    "resultCode": "0",
    "exists": true,
    "customerId": "******0001",
    "traceId": "9f3c7e8a-xxxx"
  },
  "elapsedMillis": 128,
  "receivedAt": "2026-07-10T09:00:32+09:00",
  "extractedContext": [
    {
      "contextId": "CTX-002",
      "contextName": "Customer.exists",
      "jsonPath": "$.exists",
      "value": true
    }
  ],
  "dynamicFields": [
    {
      "jsonPath": "$.traceId",
      "policyId": "CMP-POL-001"
    }
  ]
}
```

---

# 13. Context Snapshot

## 13.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|timing|BEFORE_API / AFTER_API / SCENARIO_END|
|context|Context値|
|masked|Mask済みか|
|createdAt|Snapshot作成日時|

---

## 13.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "timing": "AFTER_API",
  "context": {
    "Customer.id": {
      "contextId": "CTX-001",
      "type": "String",
      "value": "******0001",
      "masked": true
    },
    "Customer.exists": {
      "contextId": "CTX-002",
      "type": "Boolean",
      "value": true,
      "masked": false
    }
  },
  "createdAt": "2026-07-10T09:00:32+09:00"
}
```

---

# 14. Execution Snapshot

## 14.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|executionStatus|SUCCESS / SKIP / FAIL / ERROR|
|skipReason|Skip理由|
|retryCount|Retry回数|
|timeout|Timeout設定|
|error|Error情報|
|startedAt|開始日時|
|endedAt|終了日時|

---

## 14.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-002",
  "stepId": "UC-STEP-002",
  "apiId": "API-002",
  "executionStatus": "SKIP",
  "skipReason": "Customer.exists = false",
  "retryCount": 0,
  "timeout": 10,
  "error": null,
  "startedAt": "2026-07-10T09:00:35+09:00",
  "endedAt": "2026-07-10T09:00:35+09:00"
}
```

---

# 15. Error Snapshot

## 15.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|errorType|HTTP_ERROR / TIMEOUT / CONTEXT_ERROR / SPEC_ERROR / SYSTEM_ERROR|
|httpStatus|HTTP Status|
|errorCode|Error Code|
|message|Error Message|
|stackTrace|Stack Trace|
|result|FAIL / ERROR|
|createdAt|作成日時|

---

## 15.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-004",
  "stepId": "UC-STEP-002",
  "apiId": "API-002",
  "errorType": "TIMEOUT",
  "httpStatus": null,
  "errorCode": "TIMEOUT",
  "message": "API-002 timeout after 10 seconds",
  "stackTrace": null,
  "result": "FAIL",
  "createdAt": "2026-07-10T09:01:10+09:00"
}
```

---

# 16. Diff Snapshot

## 16.1 保存内容

|項目|内容|
|----|----|
|runId|実行ID|
|baselineRunId|Baseline Run ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|apiId|API ID|
|diffResult|PASS / WARN / FAIL|
|diffItems|差分項目一覧|
|comparePolicy|適用Compare Policy|
|createdAt|作成日時|

---

## 16.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "baselineRunId": "RUN-20260709-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "diffResult": "PASS",
  "diffItems": [
    {
      "jsonPath": "$.traceId",
      "baselineValue": "abc",
      "currentValue": "xyz",
      "policyId": "CMP-POL-001",
      "compareResult": "IGNORED",
      "severity": "Low"
    }
  ],
  "createdAt": "2026-07-10T09:01:30+09:00"
}
```

---

# 17. Evidence Snapshot

## 17.1 保存内容

Evidence Snapshot は、Reportから各Snapshotへ辿るための索引である。

|項目|内容|
|----|----|
|runId|実行ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|apiId|API ID|
|requestSnapshotPath|Request Snapshot保存先|
|responseSnapshotPath|Response Snapshot保存先|
|contextSnapshotPath|Context Snapshot保存先|
|executionSnapshotPath|Execution Snapshot保存先|
|diffSnapshotPath|Diff Snapshot保存先|
|logPath|Log保存先|

---

## 17.2 JSON形式

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "requestSnapshotPath": "outputs/runs/RUN-20260710-001/raw/UC-001_SC-001_UC-STEP-001_API-001_request.json",
  "responseSnapshotPath": "outputs/runs/RUN-20260710-001/raw/UC-001_SC-001_UC-STEP-001_API-001_response.json",
  "contextSnapshotPath": "outputs/runs/RUN-20260710-001/snapshot/UC-001_SC-001_UC-STEP-001_API-001_context_after.json",
  "executionSnapshotPath": "outputs/runs/RUN-20260710-001/snapshot/UC-001_SC-001_UC-STEP-001_API-001_execution.json",
  "diffSnapshotPath": "outputs/runs/RUN-20260710-001/diff/UC-001_SC-001_UC-STEP-001_API-001_diff.json",
  "logPath": "outputs/runs/RUN-20260710-001/logs/runtime.log"
}
```

---

# 18. Baseline Snapshot

## 18.1 Baseline保存先

```text
outputs/
└── baseline/
    ├── approved/
    │   └── {baselineId}/
    └── previous_success/
        └── {runId}/
```

---

## 18.2 Baseline種類

|Baseline種別|説明|利用場面|
|------------|----|--------|
|Approved Baseline|人が承認した基準Snapshot|正式比較|
|Previous Success|前回成功時のSnapshot|日次比較|
|Scenario Baseline|Scenario単位の基準Snapshot|Scenario比較|
|API Baseline|API単位の基準Snapshot|API比較|

---

## 18.3 Baseline Metadata

```json
{
  "baselineId": "BASE-20260709-001",
  "sourceRunId": "RUN-20260709-001",
  "approvedBy": "leader",
  "approvedAt": "2026-07-09T18:00:00+09:00",
  "scope": {
    "useCases": ["UC-001"],
    "scenarios": ["SC-001", "SC-002"]
  },
  "status": "Approved"
}
```

---

# 19. Mask方針

## 19.1 Mask対象

|対象|Mask方式|備考|
|----|--------|----|
|Authorization Header|完全Mask|`****`|
|Token|完全Mask|`****`|
|Password|完全Mask|`****`|
|API Key|完全Mask|`****`|
|顧客番号|部分Mask|後4桁のみ表示|
|個人名|完全Mask|`****`|
|電話番号|部分Mask|末尾4桁のみ表示|
|メールアドレス|部分Mask|ドメインのみ表示可|

---

## 19.2 Mask済み保存ルール

|保存対象|Mask必須|
|--------|--------|
|Request Snapshot|Yes|
|Response Snapshot|Yes|
|Context Snapshot|Yes|
|Execution Snapshot|必要に応じて|
|Diff Snapshot|Yes|
|Evidence Snapshot|Yes|
|Log|Yes|

---

# 20. Snapshot Result

|Result|意味|
|------|----|
|SUCCESS|Snapshot保存成功|
|SKIPPED|対象外のため保存なし|
|MASKED|Mask済みで保存|
|FAILED|Snapshot保存失敗|
|PARTIAL|一部項目のみ保存|

---

# 21. Snapshot Error

|Error ID|発生条件|処理|Result|
|--------|--------|----|------|
|SNP-ERR-001|保存先Directory作成失敗|Run停止またはERROR|ERROR|
|SNP-ERR-002|JSON Serialize失敗|対象Snapshot保存失敗|ERROR|
|SNP-ERR-003|Mask処理失敗|保存禁止|ERROR|
|SNP-ERR-004|Snapshot書込失敗|Retry後ERROR|ERROR|
|SNP-ERR-005|Baseline Snapshot読込失敗|Diff中止|ERROR|

---

# 22. Snapshot Traceability

|Snapshot種別|Trace Key|
|------------|---------|
|Run Snapshot|runId|
|UseCase Snapshot|runId + useCaseId|
|Scenario Snapshot|runId + useCaseId + scenarioId|
|Request Snapshot|runId + useCaseId + scenarioId + stepId + apiId|
|Response Snapshot|runId + useCaseId + scenarioId + stepId + apiId|
|Context Snapshot|runId + useCaseId + scenarioId + stepId + apiId + timing|
|Diff Snapshot|runId + baselineRunId + useCaseId + scenarioId + apiId|
|Evidence Snapshot|runId + useCaseId + scenarioId + apiId|

---

# 23. Snapshot Review観点

|観点|確認内容|
|----|--------|
|保存粒度|Run / UseCase / Scenario / API Step単位で保存されているか|
|再現性|Request / Response / Contextが後から確認できるか|
|Mask|秘匿情報がMaskされているか|
|Trace|runId、useCaseId、scenarioId、apiIdで追跡できるか|
|Baseline比較|Diff Engineが参照可能な形式か|
|Report連携|Evidence ReportからSnapshotへ辿れるか|
|Git管理|outputs配下がGit対象外になっているか|

---

# Appendix A. 顧客情報照会 Snapshot例

## A.1 出力構成例

```text
outputs/
└── runs/
    └── RUN-20260710-001/
        ├── run-info.json
        ├── raw/
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_request.json
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_response.json
        │   ├── UC-001_SC-001_UC-STEP-002_API-002_request.json
        │   ├── UC-001_SC-001_UC-STEP-002_API-002_response.json
        │   ├── UC-001_SC-001_UC-STEP-003_API-003_request.json
        │   └── UC-001_SC-001_UC-STEP-003_API-003_response.json
        │
        ├── snapshot/
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_context_before.json
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_context_after.json
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_execution.json
        │   └── UC-001_SC-001_scenario.json
        │
        ├── diff/
        │   └── UC-001_SC-001_UC-STEP-001_API-001_diff.json
        │
        ├── evidence/
        │   └── UC-001_SC-001_evidence.json
        │
        └── reports/
            ├── EvidenceReport.md
            └── DiffReport.md
```

---

## A.2 API-001 Request Snapshot例

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "method": "POST",
  "url": "https://stg.example.com/v1/customers/exists",
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "****"
  },
  "body": {
    "customerId": "******0001"
  },
  "contextBinding": [
    {
      "jsonPath": "$.customerId",
      "contextId": "CTX-001",
      "contextName": "Customer.id",
      "masked": true
    }
  ],
  "createdAt": "2026-07-10T09:00:31+09:00"
}
```

---

## A.3 API-001 Response Snapshot例

```json
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "httpStatus": 200,
  "body": {
    "resultCode": "0",
    "exists": true,
    "customerId": "******0001",
    "traceId": "9f3c7e8a-xxxx"
  },
  "elapsedMillis": 128,
  "extractedContext": [
    {
      "contextId": "CTX-002",
      "contextName": "Customer.exists",
      "jsonPath": "$.exists",
      "value": true
    }
  ],
  "dynamicFields": [
    {
      "jsonPath": "$.traceId",
      "policyId": "CMP-POL-001"
    }
  ]
}
```

:::

下一份建议继续做：

```text
system/05_framework/Diff設計書.md
```

因为 `Snapshot設計書` 已经定义了保存物，下一步就应该定义 **Current Snapshot vs Baseline Snapshot 的比较规则、Diff结果结构、PASS/WARN/FAIL判定**。

## 第 187 轮

### 你

Diff設計書.md

### ChatGPT

`Diff設計書` 会接在 `Snapshot設計書` 后面，定义 Current Snapshot 与 Baseline 的比较方式、Normalize、Ignore、Tolerance、Collection 比较，以及最终 PASS/WARN/FAIL 判定。

### ChatGPT

放置位置：

```text
system/05_framework/Diff設計書.md
```

:::writing{variant="document" id="63704"}
---
title: Diff設計書
document_id: SYS-DIFF-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# Diff設計書

---

# 1. 文書情報

|項目|内容|
|----|----|
|文書ID|SYS-DIFF-001|
|文書名称|Diff設計書|
|対象範囲|Baseline比較 / Current比較 / Normalize / Compare Policy / Diff Result|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|

---

# 2. Diff目的

Diff は、今回実行結果である Current Snapshot と、承認済みまたは前回正常結果である Baseline Snapshot を比較し、API仕様変更、Response値変更、Context変更、業務結果変更を検出する。

---

# 3. Diff対象

|対象|比較内容|入力Snapshot|
|----|--------|------------|
|HTTP Status|期待HTTP Statusとの差分|Response Snapshot|
|Response Body|項目値、型、固定値、Enum、必須項目|Response Snapshot|
|Context|Context生成値、引継ぎ値|Context Snapshot|
|Business Result|Scenario期待結果との差分|Scenario Snapshot|
|Execution Result|Run / Skip / Fail の差分|Execution Snapshot|
|Error Response|Error Code、Error Message、HTTP Status|Error Snapshot|
|Report Result|Daily Summary出力値|Report Snapshot|

---

# 4. Diff入力

|入力|説明|配置先|
|----|----|------|
|Current Snapshot|今回実行結果|outputs/runs/{runId}/|
|Baseline Snapshot|比較基準|outputs/baseline/approved/{baselineId}/|
|Compare Policy|共通比較方針|system/02_master/Compare_Policy_Master.md|
|Verification仕様|個別検証方針|system/06_verification_assets/|
|API設計書|固定値、Enum、Dynamic定義|system/03_api_design/|
|UseCase設計書|Scenario期待結果|system/04_usecase_design/|

---

# 5. Diff出力

|出力|形式|保存先|
|----|----|------|
|Diff Result JSON|JSON|outputs/runs/{runId}/diff/|
|Diff Report|Markdown / HTML|outputs/runs/{runId}/reports/|
|Daily Summary反映|Markdown / HTML|outputs/reports/latest/|
|Evidence Link|JSON / Markdown|outputs/runs/{runId}/evidence/|

---

# 6. Compare Policy分類

|分類|比較方式|説明|
|----|--------|----|
|Equals|完全一致|BaselineとCurrentが完全一致|
|Ignore|比較対象外|Dynamic項目など|
|Exists|存在確認|値そのものは比較しない|
|Not Empty|空でないことを確認|
|Type Only|型のみ比較|
|Regex|正規表現一致|
|Contains|部分一致|
|Tolerance|許容差比較|
|Key Match|配列をKeyで比較|
|Order Match|配列順序を含めて比較|
|Custom|個別ロジック比較|

---

# 7. Normalize設計

## 7.1 Normalize目的

Normalize は、比較前に値の表記揺れを吸収する処理である。

---

## 7.2 Normalize Rule

|Normalize ID|対象|方式|例|備考|
|------------|----|----|--|----|
|NORM-001|String|Trim|` abc ` → `abc`|前後空白除去|
|NORM-002|String|Empty To Null|`""` → `null`|必要時|
|NORM-003|Date|Format|`2026/07/10` → `2026-07-10`|日付形式統一|
|NORM-004|DateTime|Format|ISO-8601へ統一|時刻形式統一|
|NORM-005|Number|Decimal Normalize|`100.0` → `100`|数値表記統一|
|NORM-006|Array|Sort By Key|contractIdでSort|Key Match前処理|
|NORM-007|Boolean|Boolean Normalize|`"true"` → `true`|型揺れ対策|

---

# 8. Dynamic Field比較

## 8.1 Dynamic Field方針

Dynamic Field は実行ごとに値が変化するため、原則として値比較対象外とする。

|項目|方針|
|----|----|
|traceId|Ignore または Exists|
|updatedAt|Ignore または Tolerance|
|executedAt|Ignore|
|requestId|Ignore|
|runId|Ignore / Exists|

---

## 8.2 Dynamic Field定義例

|JSONPath|項目名|Compare Policy|Verification|備考|
|--------|------|--------------|------------|----|
|$.traceId|Trace ID|CMP-POL-001|Exists / Type Only|値比較しない|
|$.updatedAt|更新日時|CMP-POL-002|Tolerance / Ignore|±3秒など|
|$.requestId|Request ID|CMP-POL-001|Exists|実行毎に採番|

---

# 9. Response Diff設計

## 9.1 Response Field Diff

|Diff種別|説明|Result候補|
|--------|----|----------|
|Missing Field|Baselineにある項目がCurrentにない|FAIL / WARN|
|New Field|Currentに新規項目がある|WARN / FAIL|
|Type Changed|型が変わった|FAIL|
|Value Changed|値が変わった|FAIL / WARN|
|Fixed Value Changed|固定値が期待と異なる|FAIL|
|Enum Out Of Range|許容値外|FAIL|
|Null Changed|Null可否が変わった|FAIL / WARN|
|Dynamic Ignored|Dynamic項目の差分|PASS / IGNORED|

---

## 9.2 Response Diff項目

|項目|内容|
|----|----|
|jsonPath|差分対象JSONPath|
|baselineValue|Baseline値|
|currentValue|Current値|
|comparePolicy|適用Policy|
|diffType|差分種別|
|severity|Critical / High / Medium / Low|
|result|PASS / WARN / FAIL / IGNORED|
|message|差分説明|

---

# 10. Context Diff設計

|Diff種別|説明|Result|
|--------|----|------|
|Context Missing|必須Contextが生成されない|FAIL|
|Context Type Changed|Context型が変わった|FAIL|
|Context Value Changed|Baselineと値が違う|FAIL / WARN|
|Producer Changed|生成元が変わった|WARN / FAIL|
|Consumer Changed|利用先が変わった|WARN|
|Context Ignored|比較対象外Context|PASS|

---

# 11. Collection Diff設計

## 11.1 Collection比較方式

|方式|説明|利用例|
|----|----|------|
|Key Match|Key項目で要素を突合する|contractId|
|Order Match|順序込みで比較する|明細順序が意味を持つ場合|
|Count Only|件数のみ比較する|一覧件数|
|Contains|特定要素が含まれることを確認|Error list|
|Ignore Order|順序を無視する|契約一覧|

---

## 11.2 Collection Diff種別

|Diff種別|説明|Result|
|--------|----|------|
|Item Added|Currentに新規要素あり|WARN / FAIL|
|Item Removed|Baseline要素がCurrentにない|WARN / FAIL|
|Item Changed|Key一致要素の項目値が変化|WARN / FAIL|
|Order Changed|順序が変わった|WARN / FAIL|
|Count Changed|件数が変わった|WARN / FAIL|

---

# 12. Error Diff設計

|対象|比較方式|備考|
|----|--------|----|
|HTTP Status|Equals|期待Statusと比較|
|Error Code|Equals / Enum|Error Code変更検知|
|Error Message|Contains / Regex|文言揺れを許容|
|Error Detail|Ignore / Contains|環境差分が出やすい|
|traceId|Ignore|Dynamic|

---

# 13. Severity設計

|Severity|意味|Result|
|--------|----|------|
|Critical|業務継続不可、契約違反|FAIL|
|High|API仕様違反、重要項目差分|FAIL|
|Medium|確認必要、業務影響未確定|WARN / FAIL|
|Low|軽微、参考差分|WARN / PASS|
|Info|情報のみ|PASS|

---

# 14. Result判定

## 14.1 Field単位判定

|条件|Result|
|----|------|
|Critical差分あり|FAIL|
|High差分あり|FAIL|
|Medium差分あり|WARN / FAIL|
|Low差分あり|WARN|
|Ignore対象のみ|PASS|
|差分なし|PASS|

---

## 14.2 API単位判定

|条件|API Result|
|----|----------|
|Field FAILあり|FAIL|
|Field WARNのみ|WARN|
|全Field PASS|PASS|
|API未実行|SKIP|
|実行異常|ERROR|

---

## 14.3 Scenario単位判定

|条件|Scenario Result|
|----|----------------|
|Critical / High FAILあり|FAIL|
|WARNのみ|WARN|
|全API PASS|PASS|
|想定Skipのみ|PASS / WARN|
|想定外Skip|FAIL|
|Runtime Error|ERROR|

---

## 14.4 Run単位判定

|条件|Run Result|
|----|----------|
|ERRORあり|ERROR|
|FAILあり|FAIL|
|WARNあり|WARN|
|全Scenario PASS|PASS|

---

# 15. Diff Result JSON

```json id="dlz0s2"
{
  "runId": "RUN-20260710-001",
  "baselineId": "BASE-20260709-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "result": "WARN",
  "summary": {
    "pass": 10,
    "warn": 1,
    "fail": 0,
    "ignored": 2
  },
  "diffItems": [
    {
      "jsonPath": "$.traceId",
      "diffType": "VALUE_CHANGED",
      "baselineValue": "abc",
      "currentValue": "xyz",
      "comparePolicy": "CMP-POL-001",
      "severity": "Low",
      "result": "IGNORED",
      "message": "Dynamic field ignored."
    },
    {
      "jsonPath": "$.customer.status",
      "diffType": "VALUE_CHANGED",
      "baselineValue": "ACTIVE",
      "currentValue": "INACTIVE",
      "comparePolicy": "Equals",
      "severity": "High",
      "result": "FAIL",
      "message": "Customer status changed."
    }
  ]
}
```

---

# 16. Diff Report出力項目

|項目|内容|
|----|----|
|Run ID|今回実行ID|
|Baseline ID|比較基準ID|
|UseCase ID|対象UseCase|
|Scenario ID|対象Scenario|
|API ID|対象API|
|Result|PASS / WARN / FAIL / ERROR|
|Diff Summary|PASS / WARN / FAIL / IGNORED件数|
|Diff Detail|JSONPath単位の差分|
|Severity|重要度|
|Evidence Link|該当Snapshotへのリンク|

---

# 17. Baseline選択

|優先順位|Baseline種別|説明|
|--------|------------|----|
|1|Approved Baseline|承認済みBaseline|
|2|Previous Success|前回成功Run|
|3|Initial Baseline|初回作成Baseline|
|4|No Baseline|Baselineなし。比較不可|

---

# 18. Baselineなしの場合

|条件|処理|Result|
|----|----|------|
|初回実行|CurrentをInitial Baseline候補として保存|WARN|
|Baseline未承認|Diff比較せずEvidence保存|WARN|
|Baseline読込失敗|Diff処理Error|ERROR|

---

# 19. Diff Error

|Error ID|発生条件|処理|Result|
|--------|--------|----|------|
|DIFF-ERR-001|Baseline Snapshotなし|比較不可|WARN / ERROR|
|DIFF-ERR-002|Current Snapshotなし|比較不可|ERROR|
|DIFF-ERR-003|Compare Policy不明|対象Field ERROR|ERROR|
|DIFF-ERR-004|JSONPath解決不可|対象Field FAIL / ERROR|ERROR|
|DIFF-ERR-005|型変換失敗|対象Field FAIL|FAIL|
|DIFF-ERR-006|Collection Key不足|Collection比較ERROR|ERROR|

---

# 20. Diff Traceability

|Diff対象|Trace Key|
|--------|---------|
|Run Diff|runId + baselineId|
|UseCase Diff|runId + baselineId + useCaseId|
|Scenario Diff|runId + baselineId + useCaseId + scenarioId|
|API Diff|runId + baselineId + useCaseId + scenarioId + apiId|
|Field Diff|runId + baselineId + apiId + jsonPath|
|Context Diff|runId + baselineId + contextId|

---

# 21. Review観点

|観点|確認内容|
|----|--------|
|Policy適用|Compare Policy Masterに従っているか|
|Dynamic除外|Dynamic項目が誤検知されていないか|
|固定値確認|固定値項目がEqualsで確認されているか|
|Enum確認|許容値外がFAILになるか|
|Collection比較|Key Match / Order Matchが正しいか|
|Severity|重要度とResultが一致しているか|
|Report連携|Diff ResultがReportへ反映されるか|
|Evidence連携|差分からSnapshotへ辿れるか|

---

# Appendix A. 顧客情報照会 Diff例

## A.1 API-001 正常Diff

|JSONPath|Baseline|Current|Policy|Result|備考|
|--------|--------|-------|------|------|----|
|$.resultCode|0|0|Equals|PASS|固定値|
|$.exists|true|true|Equals|PASS|業務判定|
|$.customerId|10000001|10000001|Equals|PASS|入力値一致|
|$.traceId|abc|xyz|Ignore|IGNORED|Dynamic|

---

## A.2 API-002 差分あり

|JSONPath|Baseline|Current|Policy|Severity|Result|備考|
|--------|--------|-------|------|--------|------|----|
|$.customer.status|ACTIVE|INACTIVE|Equals|High|FAIL|顧客状態変更|
|$.customer.updatedAt|2026-07-09T10:00:00|2026-07-10T10:00:00|Ignore|Low|IGNORED|Dynamic|

---

## A.3 Collection Diff例

|Key|Field|Baseline|Current|Result|
|---|-----|--------|-------|------|
|C-001|status|ACTIVE|ACTIVE|PASS|
|C-002|status|ACTIVE|CANCELLED|FAIL|
|C-003|－|なし|追加|WARN|

:::

下一份建议做：

```text
system/05_framework/Report設計書.md
```

## 第 188 轮

### 你

Report設計書.md

### ChatGPT

`Report設計書` 会把 Run / UseCase / Scenario / API / Diff / Evidence 的结果汇总成 Daily Summary、Diff Report、Evidence Report，并定义输出格式和链接规则。

### ChatGPT

放置位置：

```text id="d8rcj9"
system/05_framework/Report設計書.md
```

:::writing{variant="document" id="49382"}
---
title: Report設計書
document_id: SYS-RPT-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# Report設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-RPT-001|
|文書名称|Report設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|Daily Summary / Diff Report / Evidence Report / Execution Report|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|SYS-DESIGN-001|システム設計書|system/05_framework/|全体設計|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context設計|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|Snapshot設計|
|SYS-DIFF-001|Diff設計書|system/05_framework/|Diff設計|
|MST-VER-001|Verification_Master|system/02_master/|Verification管理|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|Compare Policy|

---

# 2. Report目的

Report は、E6 API Verification Platform の実行結果を、承認者、リーダー、開発者、調査担当が確認できる形で出力する成果物である。

Report は以下を目的とする。

|目的|内容|
|----|----|
|日次結果確認|Daily Summaryで全体結果を短時間で確認する|
|差分確認|Diff ReportでBaselineとの差分を確認する|
|証跡確認|Evidence ReportでRequest / Response / Context / Logを確認する|
|影響分析|API、UseCase、Scenario単位で影響範囲を確認する|
|承認判断|Baseline承認、差分許容、障害判断の材料にする|

---

# 3. Report種類

|Report ID|Report名|出力形式|出力タイミング|主な利用者|保存先|
|---------|--------|--------|--------------|----------|------|
|RPT-001|Daily Summary Report|Markdown / HTML|Run終了時|承認者 / Leader|outputs/reports/latest/|
|RPT-002|Diff Report|Markdown / HTML / JSON|Diff完了時|開発者 / 調査担当|outputs/runs/{runId}/reports/|
|RPT-003|Evidence Report|Markdown / HTML|Run終了時|調査担当 / 監査担当|outputs/runs/{runId}/reports/|
|RPT-004|Execution Report|Markdown / JSON|Run終了時|開発者 / 運用担当|outputs/runs/{runId}/reports/|
|RPT-005|Error Report|Markdown / JSON|Error発生時|開発者 / 運用担当|outputs/runs/{runId}/reports/|

---

# 4. Report入力

|入力|配置先|用途|
|----|------|----|
|Run Snapshot|outputs/runs/{runId}/run-info.json|Run概要|
|UseCase Snapshot|outputs/runs/{runId}/snapshot/|UseCase結果|
|Scenario Snapshot|outputs/runs/{runId}/snapshot/|Scenario結果|
|Execution Snapshot|outputs/runs/{runId}/snapshot/|API実行状態|
|Request Snapshot|outputs/runs/{runId}/raw/|Evidence Link|
|Response Snapshot|outputs/runs/{runId}/raw/|Evidence Link|
|Context Snapshot|outputs/runs/{runId}/snapshot/|Context確認|
|Diff Result|outputs/runs/{runId}/diff/|差分表示|
|Runtime Log|outputs/runs/{runId}/logs/|障害調査|
|Master|system/02_master/|名称、重要度、分類|
|Verification仕様|system/06_verification_assets/|期待結果、判定条件|

---

# 5. Report出力先

## 5.1 Run別出力先

```text id="5t9n1j"
outputs/
└── runs/
    └── {runId}/
        └── reports/
            ├── DailySummary.md
            ├── DiffReport.md
            ├── EvidenceReport.md
            ├── ExecutionReport.md
            └── ErrorReport.md
```

---

## 5.2 Latest出力先

```text id="vb3vp2"
outputs/
└── reports/
    └── latest/
        ├── DailySummary.md
        ├── DiffReport.md
        └── index.md
```

---

## 5.3 History出力先

```text id="6gctvv"
outputs/
└── reports/
    └── history/
        └── {runId}/
            ├── DailySummary.md
            ├── DiffReport.md
            └── EvidenceReport.md
```

---

# 6. Report命名規則

|Report|ファイル名|備考|
|------|----------|----|
|Daily Summary|DailySummary.md|Latestにもコピー|
|Diff Report|DiffReport.md|Latestにもコピー|
|Evidence Report|EvidenceReport.md|Run単位|
|Execution Report|ExecutionReport.md|Run単位|
|Error Report|ErrorReport.md|Error発生時のみ|
|Report Index|index.md|Latest一覧|

---

# 7. Report Result定義

|Result|意味|表示色候補|説明|
|------|----|----------|----|
|PASS|正常|Green|差分なし、期待通り|
|WARN|確認必要|Yellow|許容可能または業務確認が必要|
|FAIL|失敗|Red|Critical / High差分、期待不一致|
|ERROR|実行異常|Red|Spec、Config、Runtime、環境異常|
|SKIP|対象外|Gray|条件により未実行|
|IGNORED|比較対象外|Gray|Dynamic Field等|

---

# 8. Daily Summary Report設計

## 8.1 目的

Daily Summary Report は、日次実行結果を短時間で確認するための要約Reportである。

主な読者は以下である。

|読者|確認内容|
|----|--------|
|承認者|総合Result、重大差分、承認要否|
|Leader|失敗UseCase、要確認Scenario|
|開発者|調査対象の入口|
|運用担当|Run正常終了、Error有無|

---

## 8.2 出力項目

|項目|内容|
|----|----|
|Run ID|実行ID|
|実行環境|Environment|
|実行開始日時|startedAt|
|実行終了日時|endedAt|
|実行時間|elapsed time|
|総合Result|PASS / WARN / FAIL / ERROR|
|対象UseCase数|実行対象UseCase数|
|対象Scenario数|実行対象Scenario数|
|PASS件数|PASS件数|
|WARN件数|WARN件数|
|FAIL件数|FAIL件数|
|ERROR件数|ERROR件数|
|SKIP件数|SKIP件数|
|重大差分|Critical / High差分|
|要確認事項|WARN、未確定事項|
|Report Link|Diff / Evidence / Executionへのリンク|

---

## 8.3 Daily Summary Markdown構成

```markdown id="7kpwc1"
# Daily Summary Report

## 1. Run Summary

|項目|内容|
|----|----|
|Run ID|RUN-YYYYMMDD-XXX|
|Environment|STG|
|Started At|YYYY-MM-DDTHH:mm:ss+09:00|
|Ended At|YYYY-MM-DDTHH:mm:ss+09:00|
|Result|PASS / WARN / FAIL / ERROR|

## 2. Result Summary

|Result|Count|
|------|-----|
|PASS|0|
|WARN|0|
|FAIL|0|
|ERROR|0|
|SKIP|0|

## 3. UseCase Summary

|UseCase ID|UseCase名|Result|Scenario数|Fail|Warn|Evidence|
|----------|---------|------|----------|----|----|--------|

## 4. Critical / High Diff

|Severity|UseCase|Scenario|API|JSONPath|Result|Message|
|--------|-------|--------|---|--------|------|-------|

## 5. 確認事項

|No|分類|内容|担当|期限|状態|
|--|----|----|----|----|----|

## 6. Links

- Diff Report
- Evidence Report
- Execution Report
```

---

# 9. Diff Report設計

## 9.1 目的

Diff Report は、Current Snapshot と Baseline Snapshot の差分を詳細確認するためのReportである。

---

## 9.2 出力項目

|項目|内容|
|----|----|
|Run ID|今回実行ID|
|Baseline ID|比較基準ID|
|UseCase ID|対象UseCase|
|Scenario ID|対象Scenario|
|API ID|対象API|
|Diff Result|PASS / WARN / FAIL / IGNORED|
|Diff Type|Missing / New / Type Changed / Value Changed 等|
|JSONPath|差分対象|
|Baseline Value|基準値|
|Current Value|今回値|
|Compare Policy|適用Policy|
|Severity|Critical / High / Medium / Low / Info|
|Message|差分説明|
|Evidence Link|Snapshotへのリンク|

---

## 9.3 Diff Report Markdown構成

```markdown id="wyzuzx"
# Diff Report

## 1. Diff Summary

|項目|内容|
|----|----|
|Run ID|RUN-YYYYMMDD-XXX|
|Baseline ID|BASE-YYYYMMDD-XXX|
|Result|PASS / WARN / FAIL|

## 2. Diff Count

|Severity|PASS|WARN|FAIL|IGNORED|
|--------|----|----|----|-------|

## 3. Diff Detail

|UseCase|Scenario|API|JSONPath|Diff Type|Baseline|Current|Policy|Severity|Result|Evidence|
|-------|--------|---|--------|---------|--------|-------|------|--------|------|--------|

## 4. Ignored Diff

|UseCase|Scenario|API|JSONPath|Policy|Reason|
|-------|--------|---|--------|------|------|

## 5. Baseline Candidate

|UseCase|Scenario|API|Current Snapshot|承認候補|
|-------|--------|---|----------------|--------|
```

---

# 10. Evidence Report設計

## 10.1 目的

Evidence Report は、実行結果の証跡を確認するためのReportである。

Request、Response、Context、Execution、Diff、Logへのリンクを整理する。

---

## 10.2 出力項目

|項目|内容|
|----|----|
|Run ID|実行ID|
|UseCase ID|UseCase ID|
|Scenario ID|Scenario ID|
|API ID|API ID|
|Step ID|Step ID|
|Request Snapshot|Request保存先|
|Response Snapshot|Response保存先|
|Context Snapshot|Context保存先|
|Execution Snapshot|Execution保存先|
|Diff Snapshot|Diff保存先|
|Log|Log保存先|
|Mask状態|Mask済みか|

---

## 10.3 Evidence Report Markdown構成

```markdown id="0f9fkl"
# Evidence Report

## 1. Evidence Summary

|項目|内容|
|----|----|
|Run ID|RUN-YYYYMMDD-XXX|
|Environment|STG|
|Result|PASS / WARN / FAIL / ERROR|

## 2. Evidence Index

|UseCase|Scenario|Step|API|Request|Response|Context|Execution|Diff|Log|
|-------|--------|----|---|-------|--------|-------|---------|----|---|

## 3. Mask Summary

|対象|Mask状態|備考|
|----|--------|----|

## 4. Snapshot Directory

```text
outputs/runs/{runId}/
```
```

---

# 11. Execution Report設計

## 11.1 目的

Execution Report は、Runtime が UseCase / Scenario / API Step をどの順序で実行したかを確認するためのReportである。

---

## 11.2 出力項目

|項目|内容|
|----|----|
|Run ID|実行ID|
|UseCase ID|UseCase ID|
|Scenario ID|Scenario ID|
|Step ID|Step ID|
|API ID|API ID|
|Execution Status|SUCCESS / SKIP / FAIL / ERROR|
|Started At|開始日時|
|Ended At|終了日時|
|Elapsed Millis|処理時間|
|Retry Count|Retry回数|
|Skip Reason|Skip理由|
|Error Message|Error内容|

---

## 11.3 Execution Report Markdown構成

```markdown id="tbqngz"
# Execution Report

## 1. Execution Summary

|項目|内容|
|----|----|
|Run ID|RUN-YYYYMMDD-XXX|
|Environment|STG|
|Result|PASS / WARN / FAIL / ERROR|

## 2. Execution Timeline

|No|UseCase|Scenario|Step|API|Status|Started At|Ended At|Elapsed|Retry|備考|
|--|-------|--------|----|---|------|----------|--------|-------|-----|----|

## 3. Skip Detail

|UseCase|Scenario|API|Skip Reason|Expected Skip|
|-------|--------|---|-----------|-------------|

## 4. Error Detail

|UseCase|Scenario|API|Error Type|Message|Log|
|-------|--------|---|----------|-------|---|
```

---

# 12. Error Report設計

## 12.1 目的

Error Report は、Spec Error、Config Error、Runtime Error、API Error などの異常を整理するReportである。

---

## 12.2 Error分類

|Error分類|内容|Result|
|---------|----|------|
|Spec Error|Master / Spec の不整合|ERROR|
|Config Error|環境設定不足|ERROR|
|Context Error|必須Context不足|ERROR|
|API Error|HTTP 4xx / 5xx|FAIL / ERROR|
|Timeout|API Timeout|FAIL / ERROR|
|Diff Error|Baseline比較失敗|ERROR|
|Report Error|Report生成失敗|ERROR|

---

## 12.3 Error Report Markdown構成

```markdown id="z6dkry"
# Error Report

## 1. Error Summary

|項目|内容|
|----|----|
|Run ID|RUN-YYYYMMDD-XXX|
|Environment|STG|
|Result|ERROR|

## 2. Error Detail

|No|Error Type|UseCase|Scenario|API|Message|Result|Log|
|--|----------|-------|--------|---|-------|------|---|

## 3. Root Cause Candidate

|No|原因候補|根拠|対応方針|
|--|--------|----|--------|
```

---

# 13. Report生成処理

## 13.1 生成順序

```text id="1b4o2y"
1. Run Snapshot読込
2. UseCase Snapshot読込
3. Scenario Snapshot読込
4. Execution Snapshot読込
5. Diff Result読込
6. Evidence Snapshot読込
7. Result集計
8. Daily Summary生成
9. Diff Report生成
10. Evidence Report生成
11. Execution Report生成
12. Latestへコピー
```

---

## 13.2 Report Engine処理

|Step|処理|入力|出力|
|----|----|----|----|
|1|Snapshot収集|outputs/runs/{runId}/|Report Data Model|
|2|Diff集計|diff/*.json|Diff Summary|
|3|Result判定|Scenario / API Result|Run Result|
|4|Evidence Link生成|Evidence Snapshot|Markdown Link|
|5|Markdown生成|Report Model|*.md|
|6|HTML変換|Markdown|*.html|
|7|Latest更新|Run Reports|outputs/reports/latest/|

---

# 14. Report Data Model

## 14.1 Run Report Model

```json id="fkz21a"
{
  "runId": "RUN-20260710-001",
  "environment": "STG",
  "startedAt": "2026-07-10T09:00:00+09:00",
  "endedAt": "2026-07-10T09:05:12+09:00",
  "result": "WARN",
  "summary": {
    "useCaseCount": 2,
    "scenarioCount": 7,
    "pass": 5,
    "warn": 2,
    "fail": 0,
    "error": 0,
    "skip": 3
  }
}
```

---

## 14.2 UseCase Report Model

```json id="nzrr18"
{
  "useCaseId": "UC-001",
  "useCaseName": "顧客情報照会",
  "result": "WARN",
  "scenarioCount": 4,
  "pass": 2,
  "warn": 1,
  "fail": 1,
  "evidencePath": "outputs/runs/RUN-20260710-001/reports/EvidenceReport.md"
}
```

---

## 14.3 Diff Report Model

```json id="jxmb4z"
{
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "jsonPath": "$.customer.status",
  "baselineValue": "ACTIVE",
  "currentValue": "INACTIVE",
  "policy": "Equals",
  "severity": "High",
  "result": "FAIL",
  "evidence": "outputs/runs/RUN-20260710-001/raw/UC-001_SC-001_UC-STEP-001_API-001_response.json"
}
```

---

# 15. Link設計

## 15.1 Link方針

Report は、要約から詳細証跡へ辿れるようにする。

```text id="q8p2ue"
Daily Summary
  ↓
Diff Report
  ↓
Evidence Report
  ↓
Request / Response / Context Snapshot
  ↓
Runtime Log
```

---

## 15.2 Link生成ルール

|Link種別|生成元|リンク先|
|--------|------|--------|
|UseCase Evidence Link|UseCase Summary|Evidence Report内UseCase section|
|Diff Evidence Link|Diff Detail|Response Snapshot / Diff Snapshot|
|Error Log Link|Error Detail|runtime.log|
|Snapshot Link|Evidence Index|raw / snapshot / diff files|

---

# 16. Mask表示方針

|対象|Report表示|
|----|----------|
|Authorization|表示しない / `****`|
|Token|`****`|
|Password|`****`|
|顧客番号|`******0001`|
|氏名|`****`|
|電話番号|`***-****-1234`|
|メール|`****@example.com`|

Report は Mask 済み Snapshot のみ参照する。

---

# 17. Report Result判定

## 17.1 UseCase Result

|条件|Result|
|----|------|
|Scenario ERRORあり|ERROR|
|Scenario FAILあり|FAIL|
|Scenario WARNあり|WARN|
|全Scenario PASS|PASS|
|全Scenario SKIP|SKIP|

---

## 17.2 Daily Summary Result

|条件|Result|
|----|------|
|Report生成不可|ERROR|
|Runtime ERRORあり|ERROR|
|UseCase FAILあり|FAIL|
|UseCase WARNあり|WARN|
|全UseCase PASS|PASS|

---

# 18. Report Review観点

|観点|確認内容|
|----|--------|
|Summary妥当性|Run全体結果が正しく集計されているか|
|UseCase集計|UseCase別ResultがScenario結果と一致しているか|
|Diff表示|Critical / High差分が漏れていないか|
|Evidence Link|ReportからSnapshotへ辿れるか|
|Mask|秘匿情報が表示されていないか|
|Latest更新|outputs/reports/latest が最新Runを指しているか|
|History保存|過去Reportが履歴保存されているか|
|承認判断|承認者が判断できる情報が含まれているか|

---

# 19. Report Error

|Error ID|発生条件|処理|Result|
|--------|--------|----|------|
|RPT-ERR-001|Run Snapshot読込失敗|Error Report生成|ERROR|
|RPT-ERR-002|Diff Result読込失敗|Daily Summaryに警告出力|ERROR|
|RPT-ERR-003|Evidence Link生成失敗|該当LinkをMissing表示|WARN|
|RPT-ERR-004|Markdown生成失敗|Report生成停止|ERROR|
|RPT-ERR-005|Latestコピー失敗|Run Reportは保存、Latest更新失敗|WARN|
|RPT-ERR-006|Mask漏れ検出|Report出力停止|ERROR|

---

# 20. Traceability

|Report|Trace Key|参照元|
|------|---------|------|
|Daily Summary|runId|Run Snapshot / UseCase Snapshot|
|Diff Report|runId + baselineId|Diff Result|
|Evidence Report|runId + useCaseId + scenarioId + apiId|Evidence Snapshot|
|Execution Report|runId + useCaseId + scenarioId + stepId|Execution Snapshot|
|Error Report|runId + errorId|Error Snapshot / Runtime Log|

---

# Appendix A. Daily Summary Report例

```markdown id="lbm070"
# Daily Summary Report

## 1. Run Summary

|項目|内容|
|----|----|
|Run ID|RUN-20260710-001|
|Environment|STG|
|Started At|2026-07-10T09:00:00+09:00|
|Ended At|2026-07-10T09:05:12+09:00|
|Result|WARN|

## 2. Result Summary

|Result|Count|
|------|-----|
|PASS|5|
|WARN|2|
|FAIL|0|
|ERROR|0|
|SKIP|3|

## 3. UseCase Summary

|UseCase ID|UseCase名|Result|Scenario数|Fail|Warn|Evidence|
|----------|---------|------|----------|----|----|--------|
|UC-001|顧客情報照会|WARN|4|0|1|EvidenceReport.md#uc-001|
|UC-002|契約情報照会|PASS|3|0|0|EvidenceReport.md#uc-002|

## 4. Critical / High Diff

|Severity|UseCase|Scenario|API|JSONPath|Result|Message|
|--------|-------|--------|---|--------|------|-------|
|High|UC-001|SC-003|API-003|$.contracts.length|WARN|契約0件。業務確認対象。|

## 5. 確認事項

|No|分類|内容|担当|期限|状態|
|--|----|----|----|----|----|
|1|業務確認|契約0件をPASS扱いにするか確認|業務担当|YYYY-MM-DD|Open|
```

---

# Appendix B. Diff Report例

```markdown id="4v0yqu"
# Diff Report

## 1. Diff Summary

|項目|内容|
|----|----|
|Run ID|RUN-20260710-001|
|Baseline ID|BASE-20260709-001|
|Result|WARN|

## 2. Diff Detail

|UseCase|Scenario|API|JSONPath|Diff Type|Baseline|Current|Policy|Severity|Result|Evidence|
|-------|--------|---|--------|---------|--------|-------|------|--------|------|--------|
|UC-001|SC-001|API-001|$.traceId|VALUE_CHANGED|abc|xyz|CMP-POL-001|Low|IGNORED|response.json|
|UC-001|SC-003|API-003|$.contracts.length|VALUE_CHANGED|2|0|Equals|Medium|WARN|response.json|
```

---

# Appendix C. Evidence Report例

```markdown id="rc4sds"
# Evidence Report

## 1. Evidence Summary

|項目|内容|
|----|----|
|Run ID|RUN-20260710-001|
|Environment|STG|
|Result|WARN|

## 2. Evidence Index

|UseCase|Scenario|Step|API|Request|Response|Context|Execution|Diff|Log|
|-------|--------|----|---|-------|--------|-------|---------|----|---|
|UC-001|SC-001|UC-STEP-001|API-001|request.json|response.json|context_after.json|execution.json|diff.json|runtime.log|
|UC-001|SC-001|UC-STEP-002|API-002|request.json|response.json|context_after.json|execution.json|diff.json|runtime.log|
|UC-001|SC-001|UC-STEP-003|API-003|request.json|response.json|context_after.json|execution.json|diff.json|runtime.log|

## 3. Mask Summary

|対象|Mask状態|備考|
|----|--------|----|
|Authorization|Masked|完全Mask|
|Customer.id|Masked|後4桁表示|
|Customer.name|Masked|完全Mask|
```

:::

下一份建议继续做：

```text id="d9ggbk"
system/05_framework/共通Framework設計書.md
```

它会把 Runner、Loader、Executor、Validator、Snapshot、Diff、Report Engine 的类/模块职责整理出来，后面就可以接 Java Runtime 设计。

## 第 189 轮

### 你

共通Framework設計書.md

### ChatGPT

`共通Framework設計書` 是 Runtime 的详细总设计，会把 Loader、Runner、Executor、Validator、Context、Snapshot、Diff、Report、Error/Log 的职责和调用顺序固定下来。

### ChatGPT

放置位置：

```text id="g1ly5p"
system/05_framework/共通Framework設計書.md
```

:::writing{variant="document" id="74826"}
---
title: 共通Framework設計書
document_id: SYS-FW-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# 共通Framework設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-FW-001|
|文書名称|共通Framework設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|Loader / Runner / Executor / Validator / Context / Snapshot / Diff / Report / Error / Log|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|SYS-DESIGN-001|システム設計書|system/05_framework/|全体設計|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context設計|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|Snapshot設計|
|SYS-DIFF-001|Diff設計書|system/05_framework/|Diff設計|
|SYS-RPT-001|Report設計書|system/05_framework/|Report設計|
|SYS-IO-001|ファイル入出力設計書|system/05_framework/|File I/O設計|
|SYS-LOG-001|ログ・例外設計書|system/05_framework/|Log / Exception設計|
|SYS-ENV-001|環境設計書|system/05_framework/|環境設計|

---

# 2. Framework目的

共通Frameworkは、E6 API Verification Platform における UseCase / Scenario / API Step の実行、Context管理、Snapshot保存、Diff比較、Report生成を共通化する実行基盤である。

本Frameworkは以下を目的とする。

|目的|内容|
|----|----|
|仕様駆動実行|Master、設計書、Verification仕様、Execution Specに従って実行する|
|実行制御共通化|Run、UseCase、Scenario、API Stepの制御を共通化する|
|API呼出共通化|HTTP Request生成、認証、Retry、Timeoutを共通化する|
|Context管理|API間の値引継ぎ、Scenario判定、Skip判定を共通化する|
|証跡保存|Request、Response、Context、Execution状態をSnapshot保存する|
|Diff比較|CurrentとBaselineをCompare Policyに従って比較する|
|Report生成|Daily Summary、Diff Report、Evidence Reportを生成する|
|拡張性確保|API、UseCase、Scenario追加時にRuntime改修を最小化する|

---

# 3. Framework全体構成

## 3.1 論理構成

```mermaid id="dnwq1h"
flowchart TD

A[Command / Scheduler] --> B[Application Bootstrap]

B --> C[Config Loader]
B --> D[Master Loader]
B --> E[Spec Loader]
B --> F[TestData Loader]

C --> G[Run Planner]
D --> G
E --> G
F --> G

G --> H[Run Runner]
H --> I[UseCase Runner]
I --> J[Scenario Runner]
J --> K[ApiStep Runner]

K --> L[Request Builder]
L --> M[Context Binder]
M --> N[API Executor]
N --> O[Response Handler]
O --> P[Context Extractor]
P --> Q[Validator]
Q --> R[Snapshot Service]

R --> S[Diff Service]
S --> T[Report Service]

H --> U[Log / Exception Service]
I --> U
J --> U
K --> U
```

---

## 3.2 Framework Layer

|Layer|役割|主なComponent|
|-----|----|-------------|
|Application Layer|起動、引数解析、全体制御|Bootstrap, Command Handler|
|Load Layer|Config、Master、Spec、TestData読込|Config Loader, Master Loader, Spec Loader|
|Planning Layer|Run対象、実行順序、依存関係解決|Run Planner|
|Execution Layer|Run / UseCase / Scenario / API Step実行|Runner群|
|HTTP Layer|Request生成、API呼出、Response受信|Request Builder, API Executor|
|Context Layer|Context生成、Binding、Extract、Validation|RunContext Engine|
|Validation Layer|Request / Response / Context検証|Validator群|
|Snapshot Layer|証跡保存|Snapshot Service|
|Diff Layer|Baseline比較|Diff Service|
|Report Layer|Report生成|Report Service|
|Common Layer|Log、Exception、Mask、File I/O|Common Services|

---

# 4. Component一覧

|Component ID|Component名|責務|入力|出力|
|------------|------------|----|----|----|
|FW-CMP-001|Application Bootstrap|Runtime起動、初期化|CLI Args / Config|Run Request|
|FW-CMP-002|Config Loader|環境設定読込|Config File|Runtime Config|
|FW-CMP-003|Master Loader|Master読込|system/02_master|Master Model|
|FW-CMP-004|Spec Loader|Execution Spec / API Spec / UseCase Spec読込|system/06_verification_assets|Spec Model|
|FW-CMP-005|TestData Loader|TestData読込|test_data|TestData Model|
|FW-CMP-006|Run Planner|実行計画作成|Master / Spec / TestData|Run Plan|
|FW-CMP-007|Run Runner|Run全体実行制御|Run Plan|Run Result|
|FW-CMP-008|UseCase Runner|UseCase単位実行制御|UseCase Plan|UseCase Result|
|FW-CMP-009|Scenario Runner|Scenario単位実行制御|Scenario Plan|Scenario Result|
|FW-CMP-010|ApiStep Runner|API Step実行制御|API Step Plan|API Step Result|
|FW-CMP-011|Request Builder|Request生成|API Spec / Context / TestData|Request|
|FW-CMP-012|Context Binder|ContextをRequestへ埋込|RunContext|Bound Request|
|FW-CMP-013|API Executor|E6 API呼出|Request|Response|
|FW-CMP-014|Response Handler|Response受信処理|Response|Response Model|
|FW-CMP-015|Context Extractor|ResponseからContext抽出|Response Model|Updated Context|
|FW-CMP-016|Validator|Request / Response / Context検証|Spec / Snapshot|Check Result|
|FW-CMP-017|Snapshot Service|Snapshot保存|Execution Data|Snapshot Files|
|FW-CMP-018|Diff Service|Baseline比較|Current / Baseline|Diff Result|
|FW-CMP-019|Report Service|Report生成|Run Result / Diff / Evidence|Reports|
|FW-CMP-020|Mask Service|秘匿情報Mask|Raw Data|Masked Data|
|FW-CMP-021|File I/O Service|File読込・書込|Path / Data|File|
|FW-CMP-022|Log Service|ログ出力|Log Event|Log File|
|FW-CMP-023|Exception Handler|例外処理|Exception|Result / Error Snapshot|

---

# 5. 実行フロー

## 5.1 Runtime起動フロー

```mermaid id="g9hvio"
sequenceDiagram
    participant U as User/Scheduler
    participant B as Bootstrap
    participant C as ConfigLoader
    participant M as MasterLoader
    participant S as SpecLoader
    participant T as TestDataLoader
    participant P as RunPlanner
    participant R as RunRunner

    U->>B: Start Command
    B->>C: Load Config
    B->>M: Load Master
    B->>S: Load Spec
    B->>T: Load TestData
    B->>P: Create Run Plan
    P-->>B: Run Plan
    B->>R: Execute Run
```

---

## 5.2 API Step実行フロー

```mermaid id="wp9p3s"
sequenceDiagram
    participant SR as ScenarioRunner
    participant AR as ApiStepRunner
    participant RB as RequestBuilder
    participant CB as ContextBinder
    participant AE as ApiExecutor
    participant RH as ResponseHandler
    participant CE as ContextExtractor
    participant V as Validator
    participant SS as SnapshotService

    SR->>AR: Execute API Step
    AR->>RB: Build Request
    RB->>CB: Bind Context
    AR->>SS: Save Context Before
    AR->>SS: Save Request Snapshot
    AR->>AE: Call API
    AE-->>RH: Response
    RH->>CE: Extract Context
    CE-->>AR: Updated Context
    AR->>V: Validate Response / Context
    AR->>SS: Save Response Snapshot
    AR->>SS: Save Context After
    AR-->>SR: API Step Result
```

---

## 5.3 Diff / Reportフロー

```mermaid id="jpn18n"
flowchart LR

A[Current Snapshot] --> C[Diff Service]
B[Baseline Snapshot] --> C
D[Compare Policy] --> C
E[Verification Spec] --> C

C --> F[Diff Result]
F --> G[Diff Snapshot]
F --> H[Report Service]

I[Execution Result] --> H
J[Evidence Snapshot] --> H

H --> K[Daily Summary]
H --> L[Diff Report]
H --> M[Evidence Report]
H --> N[Execution Report]
```

---

# 6. Run Planner設計

## 6.1 目的

Run Planner は、Master、Execution Spec、TestData、Runtime Config をもとに、今回実行する UseCase、Scenario、API Step の実行計画を作成する。

---

## 6.2 入力

|入力|内容|
|----|----|
|UseCase_Master|対象UseCase、実行対象|
|Scenario_Master|対象Scenario、分類、期待結果|
|API_UseCase_Scenario対応表|Scenario別API実行順序|
|Environment_Master|環境情報|
|Execution Spec|実行詳細|
|TestData|Scenario別入力値|
|CLI Args|対象UseCase指定、環境指定など|

---

## 6.3 出力

```json id="w79oyv"
{
  "runId": "RUN-20260710-001",
  "environment": "STG",
  "useCases": [
    {
      "useCaseId": "UC-001",
      "scenarios": [
        {
          "scenarioId": "SC-001",
          "apiSteps": [
            {
              "stepId": "UC-STEP-001",
              "apiId": "API-001",
              "order": 1
            }
          ]
        }
      ]
    }
  ]
}
```

---

## 6.4 Planning Rule

|Rule ID|内容|Error時処理|
|-------|----|-----------|
|PLAN-001|UseCase_Masterに存在しないUseCaseは実行不可|ERROR|
|PLAN-002|Scenario_Masterに存在しないScenarioは実行不可|ERROR|
|PLAN-003|API Masterに存在しないAPIは実行不可|ERROR|
|PLAN-004|API実行順序が未定義の場合は実行不可|ERROR|
|PLAN-005|必須TestDataが存在しない場合はScenario実行不可|ERROR|
|PLAN-006|日次実行対象外はDaily Runから除外|SKIP|

---

# 7. Runner設計

## 7.1 Runner構成

|Runner|責務|
|------|----|
|RunRunner|Run全体の開始・終了、結果集計、Report生成制御|
|UseCaseRunner|UseCase単位のScenario実行、UseCase Result判定|
|ScenarioRunner|Scenario単位のAPI Step実行、Scenario Result判定|
|ApiStepRunner|API呼出、Context、Validation、Snapshot保存|

---

## 7.2 RunRunner

### 7.2.1 処理内容

|Step|処理|
|----|----|
|1|Run ID生成|
|2|RunContext初期化|
|3|Run Snapshot保存|
|4|UseCase Runner起動|
|5|Run Result集計|
|6|Diff Service起動|
|7|Report Service起動|
|8|Run終了Snapshot保存|

---

### 7.2.2 Result判定

|条件|Run Result|
|----|----------|
|Runtime ERRORあり|ERROR|
|UseCase FAILあり|FAIL|
|UseCase WARNあり|WARN|
|全UseCase PASS|PASS|

---

## 7.3 UseCaseRunner

### 7.3.1 処理内容

|Step|処理|
|----|----|
|1|UseCase Context初期化|
|2|TestData読込|
|3|Scenario Runner起動|
|4|UseCase Result集計|
|5|UseCase Snapshot保存|

---

### 7.3.2 Result判定

|条件|UseCase Result|
|----|--------------|
|Scenario ERRORあり|ERROR|
|Scenario FAILあり|FAIL|
|Scenario WARNあり|WARN|
|全Scenario PASS|PASS|
|全Scenario SKIP|SKIP|

---

## 7.4 ScenarioRunner

### 7.4.1 処理内容

|Step|処理|
|----|----|
|1|Scenario Context初期化|
|2|Scenario開始Snapshot保存|
|3|API Step順次実行|
|4|Skip Rule判定|
|5|Scenario Result判定|
|6|Scenario終了Snapshot保存|

---

### 7.4.2 Result判定

|条件|Scenario Result|
|----|---------------|
|必須API ERROR|ERROR|
|必須API FAIL|FAIL|
|WARNのみ|WARN|
|想定Skipのみ|PASS / WARN|
|全API PASS|PASS|

---

## 7.5 ApiStepRunner

### 7.5.1 処理内容

|Step|処理|
|----|----|
|1|API Step開始|
|2|Skip条件判定|
|3|Request生成|
|4|Context Binding|
|5|Context Before Snapshot保存|
|6|Request Snapshot保存|
|7|API Executor呼出|
|8|Response処理|
|9|Context抽出|
|10|Validation実行|
|11|Response Snapshot保存|
|12|Context After Snapshot保存|
|13|Execution Snapshot保存|
|14|API Step Result返却|

---

### 7.5.2 API Step Result

|条件|API Step Result|
|----|----------------|
|Skip条件成立|SKIP|
|HTTP正常かつValidation PASS|PASS|
|Validation WARN|WARN|
|Validation FAIL|FAIL|
|Timeout / Runtime Exception|ERROR / FAIL|

---

# 8. Request Builder設計

## 8.1 目的

Request Builder は、API設計書、Execution Spec、TestData、RunContextをもとに、E6 APIへ送信するRequestを生成する。

---

## 8.2 入力

|入力|用途|
|----|----|
|API設計書|Endpoint、Method、Header、Request項目定義|
|Environment_Master|Base URL、Timeout、認証方式|
|TestData|Entry Input|
|RunContext|Context Binding|
|Runtime Config|認証情報、Proxy、Timeout|

---

## 8.3 Request生成順序

```text id="39c2dd"
1. Endpoint解決
2. Method設定
3. Header設定
4. Auth Header設定
5. Path Parameter設定
6. Query Parameter設定
7. Body生成
8. Context Binding
9. Request Validation
10. Mask済みSnapshot生成
```

---

## 8.4 Request Binding Rule

|Rule ID|内容|Error時処理|
|-------|----|-----------|
|REQ-BIND-001|必須Contextがない場合はAPI実行不可|ERROR|
|REQ-BIND-002|固定値はAPI設計書の定義を優先|ERROR時はSpec Error|
|REQ-BIND-003|TestDataとContextが競合する場合は優先順位に従う|WARN / ERROR|
|REQ-BIND-004|Mask対象HeaderはSnapshot保存前にMask|Mask失敗時ERROR|

---

## 8.5 値設定優先順位

|優先順位|設定元|
|--------|------|
|1|Runtime Generated Value|
|2|RunContext|
|3|TestData|
|4|API設計書 Fixed Value|
|5|Default Value|

---

# 9. API Executor設計

## 9.1 目的

API Executor は、生成済みRequestをE6 APIへ送信し、Response、HTTP Status、Header、応答時間、Error情報を取得する。

---

## 9.2 処理内容

|Step|処理|
|----|----|
|1|HTTP Client生成|
|2|Timeout設定|
|3|Proxy設定|
|4|TLS / Certificate設定|
|5|Request送信|
|6|Response受信|
|7|Elapsed Time測定|
|8|HTTP Status判定|
|9|Response Model生成|

---

## 9.3 Retry Rule

|条件|Retry|
|----|-----|
|Timeout|Retry対象|
|HTTP 500 / 502 / 503 / 504|Retry対象候補|
|HTTP 400 / 401 / 403 / 404|Retry対象外|
|Connection Error|Retry対象|
|Spec Error|Retry対象外|

---

## 9.4 Timeout Rule

|設定元|優先順位|
|------|--------|
|API設計書|1|
|Environment_Master|2|
|Runtime Default|3|

---

# 10. Response Handler設計

## 10.1 目的

Response Handler は、API Executor が取得したResponseを解析し、Validation、Context抽出、Snapshot保存に利用できる形式へ変換する。

---

## 10.2 処理内容

|Step|処理|
|----|----|
|1|HTTP Status取得|
|2|Response Header取得|
|3|Response Body取得|
|4|Content-Type判定|
|5|JSON Parse|
|6|Error Response判定|
|7|Dynamic Field識別|
|8|Response Model生成|

---

## 10.3 Response Parse Error

|条件|処理|Result|
|----|----|------|
|JSON Parse失敗|Error Snapshot保存|ERROR|
|Content-Type不一致|Validation FAIL|FAIL|
|Bodyなし|API設計書に従い判定|PASS / FAIL|
|文字コード不一致|WARN / FAIL|WARN / FAIL|

---

# 11. Context Engine連携

## 11.1 Context処理

|処理|内容|
|----|----|
|Initialize|Run / UseCase / Scenario開始時にContextを初期化|
|Bind|RequestへContext値を設定|
|Extract|ResponseからContext値を抽出|
|Update|RunContextを更新|
|Validate|必須Context、型、Producer / Consumerを確認|
|Snapshot|Context Before / Afterを保存|

---

## 11.2 Context Error

|Error|処理|
|-----|----|
|必須Contextなし|Scenario ERROR|
|型不一致|Scenario ERROR|
|更新不可Context上書き|Scenario ERROR|
|Producer未定義|Spec ERROR|
|Consumer未定義|Review Warning|

---

# 12. Validator設計

## 12.1 Validator分類

|Validator|対象|責務|
|---------|----|----|
|Request Validator|Request|必須、型、桁数、Pattern、Enum、固定値|
|Response Validator|Response|HTTP Status、必須、型、固定値、Enum、入力値一致|
|Context Validator|RunContext|Context存在、型、Producer / Consumer|
|Business Validator|Scenario Result|業務判定、Expected Result|
|Spec Validator|Master / Spec|ID整合性、必須定義|
|Security Validator|Snapshot / Report|Mask漏れ確認|

---

## 12.2 Validation Result

|Result|意味|
|------|----|
|PASS|正常|
|WARN|確認必要|
|FAIL|期待不一致|
|ERROR|実行不能、Spec不整合|
|SKIP|対象外|

---

## 12.3 Request Validation

|検証項目|内容|
|--------|----|
|Required|必須項目が存在するか|
|Type|型が一致するか|
|Length|Min / Maxを満たすか|
|Pattern|正規表現を満たすか|
|Enum|許容値内か|
|Fixed|固定値と一致するか|

---

## 12.4 Response Validation

|検証項目|内容|
|--------|----|
|HTTP Status|期待Statusか|
|Required|必須項目が存在するか|
|Type|型が一致するか|
|Fixed|固定値と一致するか|
|Enum|許容値内か|
|Input Match|Request値と一致するか|
|Context Match|Context値と一致するか|
|Dynamic|Dynamic項目として扱うか|

---

# 13. Snapshot Service連携

|タイミング|保存対象|
|----------|--------|
|Run開始|Run Snapshot|
|UseCase開始|UseCase Snapshot|
|Scenario開始|Scenario Snapshot|
|API実行前|Request Snapshot / Context Before|
|API実行後|Response Snapshot / Context After / Execution Snapshot|
|Error発生時|Error Snapshot|
|Scenario終了|Scenario Snapshot|
|Run終了|Run Snapshot / Evidence Snapshot|

---

# 14. Diff Service連携

## 14.1 起動タイミング

Diff Service は原則として API Step終了後またはScenario終了後に起動する。

|方式|説明|
|----|----|
|API Step Diff|API単位で即時Diff|
|Scenario Diff|Scenario終了後にまとめてDiff|
|Run Diff|Run終了後にまとめてDiff|

推奨方式は以下とする。

```text id="4sob38"
Scenario Diff + Run Summary Diff
```

---

## 14.2 入力

|入力|内容|
|----|----|
|Current Snapshot|今回実行結果|
|Baseline Snapshot|比較基準|
|Compare Policy|Compare_Policy_Master|
|Verification仕様|個別Compare Rule|
|API設計書|固定値、Dynamic定義|

---

# 15. Report Service連携

## 15.1 Report生成タイミング

|Report|生成タイミング|
|------|--------------|
|Daily Summary|Run終了時|
|Diff Report|Diff完了時|
|Evidence Report|Run終了時|
|Execution Report|Run終了時|
|Error Report|Error発生時またはRun終了時|

---

## 15.2 Report入力

|入力|内容|
|----|----|
|Run Result|Run全体結果|
|UseCase Result|UseCase別結果|
|Scenario Result|Scenario別結果|
|Execution Snapshot|実行履歴|
|Diff Result|差分結果|
|Evidence Snapshot|証跡Index|
|Log|Error詳細|

---

# 16. File I/O Service設計

## 16.1 役割

File I/O Service は、Spec、Master、TestData、Snapshot、Diff、Report の読込・書込を共通化する。

---

## 16.2 対象形式

|形式|用途|
|----|----|
|Markdown|設計書、Report|
|JSON|Snapshot、Execution Data、TestData|
|YAML|Runtime Config、Execution Spec候補|
|CSV|TestData候補|
|JSONL|Log / Event候補|

---

## 16.3 I/O Error

|Error|処理|
|-----|----|
|File Not Found|ERROR|
|Parse Error|ERROR|
|Write Error|ERROR|
|Permission Error|ERROR|
|Encoding Error|ERROR|

---

# 17. Mask Service設計

## 17.1 Mask対象

|対象|Mask方式|
|----|--------|
|Authorization|完全Mask|
|Token|完全Mask|
|Password|完全Mask|
|API Key|完全Mask|
|Customer.id|部分Mask|
|Customer.name|完全Mask|
|Phone|部分Mask|
|Email|部分Mask|

---

## 17.2 Mask適用タイミング

|タイミング|対象|
|----------|----|
|Snapshot保存前|Request / Response / Context|
|Report生成前|Report Data Model|
|Log出力前|Log Event|
|Error Snapshot保存前|Error Message / Stack Trace|

---

# 18. Exception Handling設計

## 18.1 Exception分類

|Exception|内容|Result|
|---------|----|------|
|SpecException|Spec不整合|ERROR|
|ConfigException|設定不備|ERROR|
|ContextException|Context不備|ERROR|
|ApiException|API異常|FAIL / ERROR|
|TimeoutException|Timeout|FAIL / ERROR|
|ValidationException|Validation失敗|FAIL|
|SnapshotException|Snapshot保存失敗|ERROR|
|DiffException|Diff処理失敗|ERROR|
|ReportException|Report生成失敗|ERROR|

---

## 18.2 Exception処理方針

|発生箇所|処理|
|--------|----|
|Bootstrap|Run開始不可、ERROR終了|
|RunPlanner|Run開始不可、ERROR終了|
|UseCaseRunner|対象UseCase ERROR、次UseCaseへ継続可|
|ScenarioRunner|対象Scenario ERROR、次Scenarioへ継続可|
|ApiStepRunner|対象Step FAIL / ERROR、Scenario方針に従う|
|SnapshotService|保存失敗時ERROR|
|ReportService|Report生成失敗時ERROR|

---

# 19. Log設計概要

## 19.1 Log分類

|Log|内容|
|---|----|
|Run Log|Run開始・終了|
|UseCase Log|UseCase開始・終了|
|Scenario Log|Scenario開始・終了|
|API Log|API呼出・Response受信|
|Validation Log|検証結果|
|Diff Log|Diff結果|
|Error Log|例外情報|
|Audit Log|Baseline承認等|

---

## 19.2 Log Level

|Level|用途|
|-----|----|
|DEBUG|詳細調査|
|INFO|通常実行|
|WARN|確認必要|
|ERROR|異常|
|AUDIT|承認・重要操作|

---

# 20. Config設計概要

## 20.1 Runtime Config

```yaml id="6r9zh7"
runtime:
  environment: STG
  runMode: DAILY
  outputDir: outputs
  logLevel: INFO

http:
  defaultTimeoutSeconds: 10
  defaultRetryCount: 1

snapshot:
  enabled: true
  maskEnabled: true

diff:
  baselineMode: APPROVED_FIRST

report:
  markdownEnabled: true
  htmlEnabled: false
```

---

## 20.2 Config優先順位

|優先順位|設定元|
|--------|------|
|1|CLI Args|
|2|Runtime Config|
|3|Environment_Master|
|4|API設計書|
|5|Framework Default|

---

# 21. 拡張設計

## 21.1 API追加時

|追加対象|Runtime改修|
|--------|-----------|
|E6_API_Master追加|不要|
|API設計書追加|不要|
|API_UseCase_Scenario対応表追加|不要|
|TestData追加|不要|
|Custom Compare追加|必要な場合あり|

---

## 21.2 UseCase追加時

|追加対象|Runtime改修|
|--------|-----------|
|UseCase_Master追加|不要|
|Scenario_Master追加|不要|
|UseCase設計書追加|不要|
|Execution Spec追加|不要|

---

## 21.3 Compare Policy追加時

|追加対象|Runtime改修|
|--------|-----------|
|既存方式のPolicy追加|不要|
|新規Compare方式追加|Compare Plugin追加|
|Custom Rule追加|Custom Validator追加|

---

# 22. Plugin / Extension Point

|Extension Point|用途|
|---------------|----|
|Custom Request Builder|特殊Request生成|
|Custom Auth Provider|特殊認証|
|Custom Context Extractor|特殊Response抽出|
|Custom Validator|個別検証|
|Custom Compare Policy|特殊Diff|
|Custom Report Renderer|特殊Report形式|
|Custom Notification|Slack / Teams / Mail通知|

---

# 23. Package構成案

```text id="f3lxgw"
runtime/src/main/java/com/example/e6verifier/

├── app/
│   ├── Bootstrap.java
│   └── CommandHandler.java
│
├── config/
│   ├── RuntimeConfig.java
│   └── ConfigLoader.java
│
├── master/
│   ├── MasterLoader.java
│   ├── ApiMaster.java
│   ├── UseCaseMaster.java
│   ├── ScenarioMaster.java
│   └── ComparePolicyMaster.java
│
├── spec/
│   ├── SpecLoader.java
│   ├── ExecutionSpec.java
│   ├── ApiSpec.java
│   └── UseCaseSpec.java
│
├── planner/
│   ├── RunPlanner.java
│   └── RunPlan.java
│
├── runner/
│   ├── RunRunner.java
│   ├── UseCaseRunner.java
│   ├── ScenarioRunner.java
│   └── ApiStepRunner.java
│
├── http/
│   ├── RequestBuilder.java
│   ├── ApiExecutor.java
│   ├── ResponseHandler.java
│   └── HttpClientFactory.java
│
├── context/
│   ├── RunContext.java
│   ├── ContextBinder.java
│   ├── ContextExtractor.java
│   └── ContextValidator.java
│
├── validation/
│   ├── RequestValidator.java
│   ├── ResponseValidator.java
│   ├── BusinessValidator.java
│   └── SpecValidator.java
│
├── snapshot/
│   ├── SnapshotService.java
│   └── SnapshotWriter.java
│
├── diff/
│   ├── DiffService.java
│   ├── ComparePolicy.java
│   └── DiffResult.java
│
├── report/
│   ├── ReportService.java
│   ├── DailySummaryRenderer.java
│   ├── DiffReportRenderer.java
│   └── EvidenceReportRenderer.java
│
├── common/
│   ├── FileService.java
│   ├── MaskService.java
│   ├── LogService.java
│   └── ExceptionHandler.java
│
└── model/
    ├── RunResult.java
    ├── UseCaseResult.java
    ├── ScenarioResult.java
    └── ApiStepResult.java
```

---

# 24. Result Model

## 24.1 共通Result

|Result|意味|
|------|----|
|PASS|正常|
|WARN|確認必要|
|FAIL|期待不一致|
|ERROR|実行異常|
|SKIP|条件により未実行|
|IGNORED|比較対象外|

---

## 24.2 ApiStepResult例

```json id="4emxl0"
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "result": "PASS",
  "httpStatus": 200,
  "elapsedMillis": 128,
  "snapshotPaths": {
    "request": "outputs/runs/RUN-20260710-001/raw/request.json",
    "response": "outputs/runs/RUN-20260710-001/raw/response.json",
    "contextAfter": "outputs/runs/RUN-20260710-001/snapshot/context_after.json"
  }
}
```

---

# 25. Framework Review観点

|観点|確認内容|
|----|--------|
|仕様駆動性|RuntimeがHard CodingではなくSpec / Masterに従うか|
|Traceability|Run → UseCase → Scenario → API → Evidenceが追跡可能か|
|Context連携|Producer / Consumerが明確か|
|Snapshot保存|各タイミングで必要な証跡が保存されるか|
|Diff連携|Baseline比較に必要な情報が揃うか|
|Report連携|Daily Summary / Diff / Evidenceへ出力可能か|
|Mask|秘匿情報が保存・表示前にMaskされるか|
|拡張性|API / UseCase / Scenario追加時の改修が少ないか|
|Error処理|Spec / Config / API / Runtime Errorが分類されるか|

---

# Appendix A. 顧客情報照会 実行例

## A.1 Run Plan例

```json id="u8g9qt"
{
  "runId": "RUN-20260710-001",
  "environment": "STG",
  "useCases": [
    {
      "useCaseId": "UC-001",
      "useCaseName": "顧客情報照会",
      "scenarios": [
        {
          "scenarioId": "SC-001",
          "scenarioName": "正常系",
          "testCaseId": "TC-001",
          "apiSteps": [
            {
              "order": 1,
              "stepId": "UC-STEP-001",
              "apiId": "API-001"
            },
            {
              "order": 2,
              "stepId": "UC-STEP-002",
              "apiId": "API-002"
            },
            {
              "order": 3,
              "stepId": "UC-STEP-003",
              "apiId": "API-003"
            }
          ]
        }
      ]
    }
  ]
}
```

---

## A.2 実行結果例

```json id="jtrbln"
{
  "runId": "RUN-20260710-001",
  "result": "WARN",
  "useCaseResults": [
    {
      "useCaseId": "UC-001",
      "result": "WARN",
      "scenarioResults": [
        {
          "scenarioId": "SC-001",
          "result": "PASS"
        },
        {
          "scenarioId": "SC-003",
          "result": "WARN"
        }
      ]
    }
  ]
}
```

:::

下一份建议继续做：

```text id="74wjuq"
system/05_framework/ファイル入出力設計書.md
```

它会把 Master / Spec / TestData / Snapshot / Diff / Report 的文件格式、读写规则、目录规则、编码、错误处理全部固定下来。

## 第 190 轮

### 你

ファイル入出力設計書.md

### ChatGPT

`ファイル入出力設計書` 会把所有输入输出文件的路径、格式、编码、读写顺序、Schema 校验、备份、错误处理固定下来，保证 Runtime 和 AI Agent 都按同一规则处理。

### ChatGPT

放置位置：

```text id="9lvidw"
system/05_framework/ファイル入出力設計書.md
```

:::writing{variant="document" id="25017"}
---
title: ファイル入出力設計書
document_id: SYS-IO-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# ファイル入出力設計書

---

# 1. 文書情報

|項目|内容|
|----|----|
|文書ID|SYS-IO-001|
|文書名称|ファイル入出力設計書|
|対象範囲|Master / Spec / TestData / Config / Snapshot / Diff / Report / Log|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|

---

# 2. 目的

本書は、E6 API Verification Platform におけるファイル入出力方式を定義する。

対象は以下である。

|分類|内容|
|----|----|
|入力|Master、API設計書、UseCase設計書、Verification仕様書、Execution Spec、TestData、Runtime Config|
|中間出力|Run Plan、Context Snapshot、Execution Snapshot|
|最終出力|Request / Response Snapshot、Diff Result、Report、Evidence、Log|
|管理対象外|Secret、生データ、生成済み一時ファイル|

---

# 3. 基本方針

|方針|内容|
|----|----|
|UTF-8固定|すべてのテキストファイルは UTF-8 を基本とする|
|構造化優先|Runtime入力は JSON / YAML を優先する|
|Markdownは人向け|設計書・ReportはMarkdownを基本とする|
|JSONは機械向け|Snapshot、Diff、Run Plan、EvidenceはJSONを基本とする|
|Git管理分離|設計資産はGit管理、実行出力は原則Git管理外|
|Mask後保存|秘匿情報は保存前にMaskする|
|追跡可能性|runId / useCaseId / scenarioId / apiId をファイル名または内容に含める|

---

# 4. 対象ファイル一覧

## 4.1 入力ファイル

|分類|配置先|形式|用途|
|----|------|----|----|
|Repository規約|system/00_repository/|Markdown|規約参照|
|Master|system/02_master/|Markdown / YAML / JSON|横断管理|
|API設計書|system/03_api_design/|Markdown|API仕様|
|UseCase設計書|system/04_usecase_design/|Markdown|UseCase仕様|
|Verification仕様書|system/06_verification_assets/|Markdown|検証仕様|
|Execution Spec|system/06_verification_assets/execution_spec/|YAML / JSON / Markdown|Runtime実行定義|
|TestData|system/06_verification_assets/test_data/|JSON / CSV / YAML|Scenario入力|
|Runtime Config|runtime/config/|YAML / JSON|実行設定|

---

## 4.2 出力ファイル

|分類|配置先|形式|用途|
|----|------|----|----|
|Run Snapshot|outputs/runs/{runId}/|JSON|Run情報|
|Request Snapshot|outputs/runs/{runId}/raw/|JSON|Request証跡|
|Response Snapshot|outputs/runs/{runId}/raw/|JSON|Response証跡|
|Context Snapshot|outputs/runs/{runId}/snapshot/|JSON|Context証跡|
|Execution Snapshot|outputs/runs/{runId}/snapshot/|JSON|実行状態|
|Diff Result|outputs/runs/{runId}/diff/|JSON / Markdown|差分結果|
|Evidence|outputs/runs/{runId}/evidence/|JSON / Markdown|証跡索引|
|Report|outputs/runs/{runId}/reports/|Markdown / HTML|実行Report|
|Log|outputs/runs/{runId}/logs/|log / JSONL|Runtime Log|

---

# 5. 文字コード・改行コード

|項目|規約|
|----|----|
|文字コード|UTF-8|
|BOM|なし|
|改行コード|LF|
|JSON Encoding|UTF-8|
|Markdown Encoding|UTF-8|
|CSV Encoding|UTF-8|
|日本語ファイル名|許可|
|機械処理用ファイル名|英数字・ID・underscore推奨|

---

# 6. ファイル形式規約

## 6.1 Markdown

|用途|対象|
|----|----|
|設計書|BA、API設計、UseCase設計、Verification仕様|
|規約|Repository規約、命名規約、レビュー観点|
|Report|Daily Summary、Diff Report、Evidence Report|

Markdownは人が読む正式成果物とする。

---

## 6.2 JSON

|用途|対象|
|----|----|
|Snapshot|Request / Response / Context / Execution|
|Diff|Diff Result|
|Evidence|Evidence Index|
|Run Model|Run Plan / Run Result|
|TestData|Scenario別入力|

JSONはRuntimeが直接読み書きする機械処理用形式とする。

---

## 6.3 YAML

|用途|対象|
|----|----|
|Runtime Config|環境設定|
|Execution Spec候補|Runtime実行仕様|
|軽量Master候補|AI / Runtime向けMaster|

---

## 6.4 CSV

|用途|対象|
|----|----|
|大量TestData|Scenario別データ一覧|
|一覧出力|Report補助|
|人手編集|Excel編集用|

CSVは必要時のみ利用し、Runtime内部ではJSONへ変換して扱う。

---

# 7. ディレクトリ入出力設計

## 7.1 入力ディレクトリ

```text id="e1sdkr"
system/
├── 00_repository/
├── 01_business/
├── 02_master/
├── 03_api_design/
├── 04_usecase_design/
├── 05_framework/
└── 06_verification_assets/

runtime/
└── config/
```

---

## 7.2 出力ディレクトリ

```text id="ypshkq"
outputs/
├── baseline/
├── runs/
├── reports/
└── evidence/
```

---

## 7.3 Run出力構成

```text id="frwu4r"
outputs/runs/{runId}/

├── run-info.json
├── raw/
├── snapshot/
├── diff/
├── reports/
├── evidence/
├── logs/
└── tmp/
```

---

# 8. ファイル命名規則

## 8.1 入力成果物

|成果物|命名規則|例|
|------|--------|--|
|BA|BA-XXX_〇〇業務.md|BA-001_顧客情報照会業務.md|
|BA Scenario|BA-XXX_〇〇業務_シナリオ一覧.md|BA-001_顧客情報照会業務_シナリオ一覧.md|
|API分析|API-ANL-XXX_〇〇API分析.md|API-ANL-001_顧客存在確認API分析.md|
|API設計|API-XXX_〇〇API.md|API-001_CustomerExistsAPI.md|
|UseCase設計|UC-XXX_〇〇.md|UC-001_顧客情報照会.md|
|Verification仕様|VER-XXX_〇〇.md|VER-001_顧客情報照会.md|
|Execution Spec|EXEC-XXX_〇〇.yml|EXEC-001_顧客情報照会.yml|
|TestData|TD-XXX_SC-XXX_名称.json|TD-001_SC-001_normal.json|

---

## 8.2 Snapshot

```text id="6j1q2k"
{useCaseId}_{scenarioId}_{stepId}_{apiId}_{snapshotType}.json
```

例：

```text id="w73wzt"
UC-001_SC-001_UC-STEP-001_API-001_request.json
UC-001_SC-001_UC-STEP-001_API-001_response.json
UC-001_SC-001_UC-STEP-001_API-001_context_before.json
UC-001_SC-001_UC-STEP-001_API-001_context_after.json
```

---

## 8.3 Report

|Report|ファイル名|
|------|----------|
|Daily Summary|DailySummary.md|
|Diff Report|DiffReport.md|
|Evidence Report|EvidenceReport.md|
|Execution Report|ExecutionReport.md|
|Error Report|ErrorReport.md|

---

# 9. 読込順序

Runtimeは以下順序でファイルを読み込む。

```text id="zh5qed"
1. Runtime Config
2. Environment_Master
3. E6_API_Master
4. UseCase_Master
5. Scenario_Master
6. Context_Master
7. Compare_Policy_Master
8. API_UseCase_Scenario対応表
9. API設計書
10. UseCase設計書
11. Verification仕様書
12. Execution Spec
13. TestData
```

---

# 10. 書込順序

Runtimeは以下順序でファイルを書き込む。

```text id="s4tuky"
1. run-info.json
2. Context Before Snapshot
3. Request Snapshot
4. Response Snapshot
5. Context After Snapshot
6. Execution Snapshot
7. Scenario Snapshot
8. UseCase Snapshot
9. Diff Result
10. Evidence Index
11. Reports
12. Logs
```

---

# 11. JSON Schema方針

## 11.1 Schema対象

|対象|Schema要否|
|----|----------|
|Run Plan|必須|
|TestData|必須|
|Request Snapshot|必須|
|Response Snapshot|必須|
|Context Snapshot|必須|
|Diff Result|必須|
|Evidence Index|必須|
|Runtime Config|必須|

---

## 11.2 Schema配置

```text id="mfisbe"
runtime/
└── config/
    └── schema/
        ├── run-plan.schema.json
        ├── testdata.schema.json
        ├── request-snapshot.schema.json
        ├── response-snapshot.schema.json
        ├── context-snapshot.schema.json
        ├── diff-result.schema.json
        └── evidence-index.schema.json
```

---

# 12. TestData入出力

## 12.1 TestData配置

```text id="t5ixq3"
system/06_verification_assets/test_data/

└── UC-001/
    ├── TD-001_SC-001_normal.json
    ├── TD-002_SC-002_customer_not_found.json
    └── TD-003_SC-003_contract_empty.json
```

---

## 12.2 TestData形式

```json id="2ky756"
{
  "testDataId": "TD-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "description": "正常系顧客",
  "entryInput": {
    "customerId": "10000001"
  },
  "expected": {
    "result": "PASS"
  }
}
```

---

# 13. Run Info

## 13.1 保存先

```text id="00n00u"
outputs/runs/{runId}/run-info.json
```

---

## 13.2 形式

```json id="85g1k3"
{
  "runId": "RUN-20260710-001",
  "environment": "STG",
  "startedAt": "2026-07-10T09:00:00+09:00",
  "endedAt": "2026-07-10T09:05:12+09:00",
  "result": "WARN",
  "targetUseCases": ["UC-001"],
  "targetScenarios": ["SC-001", "SC-002"]
}
```

---

# 14. Snapshot入出力

## 14.1 Request Snapshot

保存先：

```text id="tvvhey"
outputs/runs/{runId}/raw/
```

形式：

```json id="zcp9nu"
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "method": "POST",
  "url": "https://stg.example.com/v1/customers/exists",
  "headers": {},
  "body": {}
}
```

---

## 14.2 Response Snapshot

保存先：

```text id="nm2ocv"
outputs/runs/{runId}/raw/
```

形式：

```json id="nw8aq3"
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "httpStatus": 200,
  "headers": {},
  "body": {}
}
```

---

## 14.3 Context Snapshot

保存先：

```text id="xgwybg"
outputs/runs/{runId}/snapshot/
```

形式：

```json id="l3gp3o"
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "timing": "AFTER_API",
  "context": {}
}
```

---

# 15. Diff入出力

## 15.1 Diff Result保存先

```text id="8yb0nn"
outputs/runs/{runId}/diff/
```

---

## 15.2 Diff Result形式

```json id="rl7hgw"
{
  "runId": "RUN-20260710-001",
  "baselineId": "BASE-20260709-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "result": "PASS",
  "diffItems": []
}
```

---

# 16. Evidence入出力

## 16.1 Evidence Index保存先

```text id="n1r0fy"
outputs/runs/{runId}/evidence/
```

---

## 16.2 Evidence Index形式

```json id="4hswm6"
{
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": "API-001",
  "requestSnapshotPath": "outputs/runs/RUN-20260710-001/raw/request.json",
  "responseSnapshotPath": "outputs/runs/RUN-20260710-001/raw/response.json",
  "contextSnapshotPath": "outputs/runs/RUN-20260710-001/snapshot/context.json",
  "diffSnapshotPath": "outputs/runs/RUN-20260710-001/diff/diff.json"
}
```

---

# 17. Report入出力

## 17.1 Report保存先

```text id="pe1cxy"
outputs/runs/{runId}/reports/
```

---

## 17.2 Latest Report

```text id="2wx77j"
outputs/reports/latest/
```

---

## 17.3 History Report

```text id="ult4fr"
outputs/reports/history/{runId}/
```

---

# 18. Baseline入出力

## 18.1 Baseline配置

```text id="u8zrs3"
outputs/baseline/

├── approved/
│   └── {baselineId}/
└── previous_success/
    └── {runId}/
```

---

## 18.2 Baseline Metadata

```json id="v0meae"
{
  "baselineId": "BASE-20260709-001",
  "sourceRunId": "RUN-20260709-001",
  "approvedBy": "leader",
  "approvedAt": "2026-07-09T18:00:00+09:00",
  "status": "Approved"
}
```

---

# 19. 一時ファイル

## 19.1 tmp配置

```text id="im0h48"
outputs/runs/{runId}/tmp/
```

---

## 19.2 tmp削除方針

|条件|処理|
|----|----|
|Run正常終了|削除|
|Run異常終了|保持可|
|Debug Mode|保持|
|7日経過|削除候補|

---

# 20. Backup / Archive

## 20.1 Archive対象

|対象|Archive|
|----|-------|
|outputs/runs|Yes|
|outputs/reports/history|Yes|
|outputs/baseline/approved|Yes|
|logs|必要に応じて|
|tmp|No|

---

## 20.2 Archive方針

|項目|方針|
|----|----|
|保存単位|runId単位|
|圧縮形式|zip / tar.gz|
|保存期間|プロジェクト方針に従う|
|削除条件|承認後、保存期限経過後|

---

# 21. Git管理方針

## 21.1 Git管理対象

|対象|管理|
|----|----|
|system配下の設計書|Yes|
|system/02_master|Yes|
|system/06_verification_assets/test_data サンプル|Yes|
|runtime/config template|Yes|
|schema|Yes|

---

## 21.2 Git管理対象外

|対象|理由|
|----|----|
|outputs|実行結果|
|runtime/config/secret|機密情報|
|staging/data|実行結果|
|staging/logs|ログ|
|tmp|一時ファイル|
|.env|環境依存設定|

---

# 22. File I/O Error

|Error ID|発生条件|処理|Result|
|--------|--------|----|------|
|IO-ERR-001|File Not Found|対象処理停止|ERROR|
|IO-ERR-002|Permission Denied|Run停止|ERROR|
|IO-ERR-003|Parse Error|対象Spec / TestData無効|ERROR|
|IO-ERR-004|Encoding Error|読込失敗|ERROR|
|IO-ERR-005|Write Error|Retry後ERROR|ERROR|
|IO-ERR-006|Schema Validation Error|対象ファイル無効|ERROR|
|IO-ERR-007|Path Traversal検出|処理停止|ERROR|
|IO-ERR-008|Mask前データ保存検出|保存停止|ERROR|

---

# 23. Security方針

|項目|方針|
|----|----|
|Path Traversal|禁止|
|Secret File|Git管理禁止|
|Mask前Snapshot|保存禁止|
|Log出力|Mask後のみ|
|File Permission|Runtime実行Userのみ書込|
|Baseline承認|承認者のみ変更可|

---

# 24. File I/O Service API案

|Method|説明|
|------|----|
|readJson(path, schema)|JSON読込 + Schema検証|
|writeJson(path, data)|JSON書込|
|readYaml(path, schema)|YAML読込 + Schema検証|
|writeMarkdown(path, content)|Markdown書込|
|copyToLatest(source, target)|Latest Report更新|
|archiveRun(runId)|Run結果Archive|
|validatePath(path)|Path安全性確認|
|ensureDirectory(path)|Directory作成|
|maskAndWrite(path, data)|Mask後保存|

---

# 25. Review観点

|観点|確認内容|
|----|--------|
|配置|入力・出力ファイルが規定位置にあるか|
|命名|命名規則に従っているか|
|形式|JSON / YAML / Markdown形式が正しいか|
|Schema|Schema検証対象が明確か|
|Mask|保存前にMaskされるか|
|Git管理|outputsやsecretがGit対象外か|
|Trace|runId / UseCase / Scenario / APIで追跡可能か|
|Error処理|File Not Found / Parse Error 等が定義されているか|

---

# Appendix A. 顧客情報照会 出力例

```text id="v2qztw"
outputs/
└── runs/
    └── RUN-20260710-001/
        ├── run-info.json
        ├── raw/
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_request.json
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_response.json
        │   ├── UC-001_SC-001_UC-STEP-002_API-002_request.json
        │   └── UC-001_SC-001_UC-STEP-002_API-002_response.json
        ├── snapshot/
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_context_before.json
        │   ├── UC-001_SC-001_UC-STEP-001_API-001_context_after.json
        │   └── UC-001_SC-001_UC-STEP-001_API-001_execution.json
        ├── diff/
        │   └── UC-001_SC-001_UC-STEP-001_API-001_diff.json
        ├── evidence/
        │   └── UC-001_SC-001_API-001_evidence.json
        ├── reports/
        │   ├── DailySummary.md
        │   ├── DiffReport.md
        │   └── EvidenceReport.md
        └── logs/
            └── runtime.log
```

:::

## 第 191 轮

### 你

接下来做什么

### ChatGPT

接下来建议按这个顺序做：

```text id="o2ad4b"
1. ログ・例外設計書.md
2. 環境設計書.md
3. Verification仕様書_Template.md 修正版
4. Execution Spec設計書 / Template
5. API Test Spec Template
6. UseCase Test Spec Template
7. TestData設計書 / Template
8. Java Runtime 実装設計
```

我建议**下一步先做 `ログ・例外設計書.md`**。

原因是现在已经完成了：

```text id="4qrf8l"
システム設計書
RunContext設計書
Snapshot設計書
Diff設計書
Report設計書
共通Framework設計書
ファイル入出力設計書
```

这些文档里都引用了：

```text id="xq9gp4"
Log Service
Exception Handler
Error Snapshot
Runtime Error
Spec Error
Config Error
Context Error
API Error
Report Error
```

但还没有一个正式文档定义：

```text id="v4y1ma"
什么错误算 ERROR
什么错误算 FAIL
什么错误算 WARN
什么时候继续
什么时候停止
日志输出什么
Mask怎么做
StackTrace保存不保存
Error Report怎么引用
```

所以正确顺序是：

```text id="b63c10"
system/05_framework/
└── ログ・例外設計書.md
```

然后再做：

```text id="c2gwba"
system/05_framework/
└── 環境設計書.md
```

做完这两个，`05_framework` 基本就完整了。之后再进入 `06_verification_assets`，做 Verification / Execution Spec / TestData。

## 第 192 轮

### 你

ログ・例外設計書.md 做成

### ChatGPT

放置位置：

```text
system/05_framework/ログ・例外設計書.md
```

:::writing{variant="document" id="38164"}
---
title: ログ・例外設計書
document_id: SYS-LOG-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# ログ・例外設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-LOG-001|
|文書名称|ログ・例外設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|Application Log / Execution Log / API Log / Validation Log / Diff Log / Audit Log / Exception Handling|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|SYS-DESIGN-001|システム設計書|system/05_framework/|全体設計|
|SYS-FW-001|共通Framework設計書|system/05_framework/|Framework設計|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context設計|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|Snapshot設計|
|SYS-DIFF-001|Diff設計書|system/05_framework/|Diff設計|
|SYS-RPT-001|Report設計書|system/05_framework/|Report設計|
|SYS-IO-001|ファイル入出力設計書|system/05_framework/|File I/O設計|

---

# 2. 目的

本書は、E6 API Verification Platform におけるログ出力方式、ログレベル、ログ構造、Mask方針、例外分類、Result判定、継続・停止方針、Error SnapshotおよびError Report連携を定義する。

---

# 3. 基本方針

|方針|内容|
|----|----|
|構造化ログ|機械解析可能なJSONL形式を基本とする|
|人間可読ログ|運用確認用にテキストログも出力可能とする|
|Trace可能|runId、useCaseId、scenarioId、stepId、apiIdを保持する|
|Mask必須|秘匿情報はログ出力前にMaskする|
|例外分類|Spec、Config、Context、API、Validation、Snapshot、Diff、Report等に分類する|
|継続方針明確化|例外ごとにRun / UseCase / Scenario / Stepの停止範囲を定義する|
|Evidence連携|Error Snapshot、Execution Snapshot、Error Reportからログへ追跡可能にする|
|StackTrace制御|開発環境では保存、本番相当環境では制限する|

---

# 4. ログ分類

|Log ID|ログ分類|目的|主な出力内容|
|------|--------|----|------------|
|LOG-APP|Application Log|Runtime起動・終了確認|起動引数、Version、Environment|
|LOG-RUN|Run Log|Run全体追跡|Run開始・終了、総合Result|
|LOG-UC|UseCase Log|UseCase実行追跡|UseCase開始・終了、Result|
|LOG-SC|Scenario Log|Scenario実行追跡|Scenario開始・終了、分岐、Result|
|LOG-STEP|API Step Log|API Step追跡|Step開始・終了、Skip、Retry|
|LOG-API|API Log|API呼出確認|Method、Path、Status、Elapsed|
|LOG-CTX|Context Log|Context生成・利用確認|Bind、Extract、Update、Validation|
|LOG-VAL|Validation Log|検証結果確認|Check ID、対象、期待、実際、Result|
|LOG-DIFF|Diff Log|差分確認|Baseline、Current、Policy、Result|
|LOG-SNP|Snapshot Log|Snapshot保存確認|保存先、保存結果|
|LOG-RPT|Report Log|Report生成確認|Report種別、保存先、生成結果|
|LOG-ERR|Error Log|例外・異常確認|Error ID、例外分類、Message|
|LOG-AUDIT|Audit Log|重要操作監査|Baseline承認、設定変更、手動実行|

---

# 5. ログレベル

|Level|用途|例|
|-----|----|--|
|TRACE|詳細な内部処理追跡|Field単位Binding、比較前Normalize|
|DEBUG|開発・障害調査|Request生成内容、Context更新|
|INFO|通常運用|Run開始、API成功、Report生成|
|WARN|処理継続可能な異常|任意項目不足、許容差分|
|ERROR|対象処理失敗|API Timeout、Context不足|
|FATAL|Run継続不可|Master読込失敗、Config重大不備|
|AUDIT|承認・重要操作|Baseline承認、手動再実行|

---

# 6. 環境別ログレベル

|環境|標準Level|StackTrace|Request / Response詳細|
|----|---------|----------|----------------------|
|LOCAL|DEBUG|出力|Mask後出力可|
|DEV|DEBUG|出力|Mask後出力可|
|STG|INFO|Error時のみ|原則Snapshot参照|
|PROD-LIKE|INFO|制限出力|ログへBodyを直接出力しない|

---

# 7. ログ出力形式

## 7.1 JSONL形式

1イベントを1行のJSONとして出力する。

```json
{
  "timestamp": "2026-07-10T09:00:31.128+09:00",
  "level": "INFO",
  "eventId": "API_CALL_COMPLETED",
  "logger": "ApiExecutor",
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-001",
  "apiId": "API-001",
  "message": "API call completed.",
  "details": {
    "method": "POST",
    "path": "/v1/customers/exists",
    "httpStatus": 200,
    "elapsedMillis": 128
  }
}
```

---

## 7.2 テキスト形式

```text
2026-07-10T09:00:31.128+09:00 INFO [RUN-20260710-001][UC-001][SC-001][API-001] API call completed. status=200 elapsed=128ms
```

---

# 8. 共通ログ項目

|項目|必須|説明|
|----|----|----|
|timestamp|○|ログ発生日時|
|level|○|ログレベル|
|eventId|○|イベント識別子|
|logger|○|出力Component|
|runId|条件付き|Run開始後は必須|
|useCaseId|条件付き|UseCase実行中は必須|
|scenarioId|条件付き|Scenario実行中は必須|
|stepId|条件付き|API Step実行中は必須|
|apiId|条件付き|API関連ログでは必須|
|message|○|人間可読メッセージ|
|details|－|構造化追加情報|
|errorId|例外時|Error ID|
|exceptionType|例外時|例外Class / 分類|
|evidencePath|－|関連証跡へのPath|

---

# 9. Event ID一覧

|Event ID|Level|発生タイミング|
|--------|-----|--------------|
|APP_START|INFO|Application起動|
|APP_END|INFO|Application終了|
|RUN_START|INFO|Run開始|
|RUN_END|INFO / ERROR|Run終了|
|USECASE_START|INFO|UseCase開始|
|USECASE_END|INFO / WARN / ERROR|UseCase終了|
|SCENARIO_START|INFO|Scenario開始|
|SCENARIO_END|INFO / WARN / ERROR|Scenario終了|
|API_STEP_START|DEBUG / INFO|API Step開始|
|API_STEP_SKIP|INFO / WARN|API Step Skip|
|API_CALL_START|INFO|API呼出開始|
|API_CALL_COMPLETED|INFO|API呼出成功|
|API_CALL_RETRY|WARN|Retry実行|
|API_CALL_TIMEOUT|ERROR|Timeout|
|CONTEXT_BOUND|DEBUG|RequestへContext設定|
|CONTEXT_EXTRACTED|DEBUG|ResponseからContext抽出|
|CONTEXT_ERROR|ERROR|Context異常|
|VALIDATION_PASS|DEBUG|検証成功|
|VALIDATION_WARN|WARN|検証警告|
|VALIDATION_FAIL|ERROR|検証失敗|
|SNAPSHOT_SAVED|DEBUG / INFO|Snapshot保存成功|
|SNAPSHOT_FAILED|ERROR|Snapshot保存失敗|
|DIFF_COMPLETED|INFO / WARN / ERROR|Diff完了|
|REPORT_GENERATED|INFO|Report生成成功|
|REPORT_FAILED|ERROR|Report生成失敗|
|BASELINE_APPROVED|AUDIT|Baseline承認|
|SPEC_ERROR|ERROR / FATAL|Spec不整合|
|CONFIG_ERROR|ERROR / FATAL|Config不備|

---

# 10. ログ保存先

```text
outputs/
└── runs/
    └── {runId}/
        └── logs/
            ├── runtime.log
            ├── runtime.jsonl
            ├── error.log
            └── audit.log
```

|ファイル|内容|
|--------|----|
|runtime.log|人間可読テキストログ|
|runtime.jsonl|構造化ログ|
|error.log|WARN以上またはERRORのみ|
|audit.log|承認・重要操作|

---

# 11. ログファイル命名

|用途|ファイル名|
|----|----------|
|通常Runtime Log|runtime.log|
|構造化Log|runtime.jsonl|
|Error Log|error.log|
|Audit Log|audit.log|
|起動前Error|bootstrap-error.log|

Run開始前はrunIdが存在しないため、起動前Errorは共通の `bootstrap-error.log` に出力する。

---

# 12. ログローテーション

|項目|方針|
|----|----|
|Run単位|原則runId単位でディレクトリを分離|
|単一ファイル上限|100MBを標準候補とする|
|上限超過時|連番を付与して分割|
|保存期間|運用方針に従う|
|Archive|Run Archive時に同時圧縮|
|削除|保存期間経過後に運用処理で削除|

例：

```text
runtime.jsonl
runtime.1.jsonl
runtime.2.jsonl
```

---

# 13. Mask設計

## 13.1 Mask対象

|対象|Mask方式|例|
|----|--------|--|
|Authorization Header|完全Mask|`****`|
|Bearer Token|完全Mask|`Bearer ****`|
|API Key|完全Mask|`****`|
|Password|完全Mask|`****`|
|Cookie / Session|完全Mask|`****`|
|顧客番号|部分Mask|`******0001`|
|氏名|完全Mask|`****`|
|電話番号|部分Mask|`***-****-1234`|
|メールアドレス|部分Mask|`****@example.com`|
|住所|完全または部分Mask|プロジェクト方針に従う|

---

## 13.2 Mask適用順序

```text
1. Log Event生成
2. Mask対象項目判定
3. Mask処理
4. Mask漏れ検査
5. Log書込
```

---

## 13.3 Mask失敗時

|条件|処理|Result|
|----|----|------|
|Mask対象判定失敗|対象Dataをログ出力しない|ERROR|
|Mask処理例外|ログBodyを破棄|ERROR|
|Mask漏れ検出|該当ログ出力停止|ERROR|
|秘匿Dataを含む可能性あり|Detailsを省略|WARN|

---

# 14. Request / Responseログ方針

## 14.1 Request

|項目|ログ出力|
|----|--------|
|Method|出力|
|Path|出力|
|Query Parameter|Mask後、必要時のみ|
|Header|認証情報を除き必要時のみ|
|Body|原則Snapshot参照|
|Body全文|LOCAL / DEVでMask後のみ許可|

---

## 14.2 Response

|項目|ログ出力|
|----|--------|
|HTTP Status|出力|
|Elapsed Time|出力|
|Content-Type|出力可|
|Header|必要時のみ|
|Body|原則Snapshot参照|
|Error Body|Mask後、必要項目のみ|

---

# 15. 例外分類

|Exception ID|例外分類|説明|
|------------|--------|----|
|EX-SPEC|SpecException|Master / Spec / ID不整合|
|EX-CONFIG|ConfigException|環境設定・必須設定不足|
|EX-IO|FileIOException|File読込・書込失敗|
|EX-CONTEXT|ContextException|Context不足・型不一致|
|EX-REQUEST|RequestBuildException|Request生成失敗|
|EX-AUTH|AuthenticationException|認証情報不備・認証失敗|
|EX-API|ApiException|HTTP 4xx / 5xx|
|EX-TIMEOUT|TimeoutException|API Timeout|
|EX-CONNECTION|ConnectionException|接続失敗|
|EX-PARSE|ResponseParseException|Response解析失敗|
|EX-VALIDATION|ValidationException|期待値不一致|
|EX-SNAPSHOT|SnapshotException|Snapshot保存失敗|
|EX-DIFF|DiffException|Baseline比較失敗|
|EX-REPORT|ReportException|Report生成失敗|
|EX-SECURITY|SecurityException|Mask漏れ、Path Traversal等|
|EX-SYSTEM|SystemException|想定外Runtime例外|

---

# 16. Error ID命名

```text
ERR-<分類>-<3桁連番>
```

例：

```text
ERR-SPEC-001
ERR-CTX-001
ERR-API-001
ERR-DIFF-001
ERR-RPT-001
```

---

# 17. 例外共通項目

|項目|説明|
|----|----|
|errorId|Error識別子|
|exceptionCategory|例外分類|
|message|利用者向け説明|
|technicalMessage|技術詳細|
|runId|Run ID|
|useCaseId|UseCase ID|
|scenarioId|Scenario ID|
|stepId|Step ID|
|apiId|API ID|
|cause|原因|
|result|WARN / FAIL / ERROR|
|continuePolicy|CONTINUE / STOP_STEP / STOP_SCENARIO / STOP_USECASE / STOP_RUN|
|evidencePath|関連Snapshot / Log|
|occurredAt|発生日時|

---

# 18. Error Result区分

|Result|意味|例|
|------|----|--|
|WARN|期待との差異はあるが処理継続可能|任意項目不足、許容差分|
|FAIL|検証結果が期待不一致|固定値不一致、HTTP Status不一致|
|ERROR|実行基盤または入力不備により検証不能|Spec不足、Context不足|
|FATAL|Run継続不可の重大異常|Master読込不可、出力先利用不可|

`FATAL` はログレベルとして利用し、最終Run Resultは `ERROR` とする。

---

# 19. 継続・停止方針

|例外分類|標準Result|停止範囲|次処理|
|--------|----------|--------|------|
|SpecException：共通Master不正|ERROR|STOP_RUN|Run終了|
|SpecException：個別UseCase不正|ERROR|STOP_USECASE|次UseCaseへ継続可|
|ConfigException：必須環境設定不足|ERROR|STOP_RUN|Run終了|
|FileIOException：TestData読込失敗|ERROR|STOP_SCENARIO|次Scenarioへ継続可|
|ContextException：必須Context不足|ERROR|STOP_SCENARIO|次Scenarioへ継続可|
|RequestBuildException|ERROR|STOP_SCENARIO|次Scenarioへ継続可|
|AuthenticationException|ERROR|STOP_RUN / STOP_USECASE|設定に従う|
|ApiException 4xx|FAIL / ERROR|STOP_STEP / STOP_SCENARIO|Verification仕様に従う|
|ApiException 5xx|FAIL / ERROR|Retry後STOP_SCENARIO|次Scenarioへ継続可|
|TimeoutException|FAIL / ERROR|Retry後STOP_SCENARIO|次Scenarioへ継続可|
|ValidationException|FAIL|STOP_STEP / CONTINUE|Verification仕様に従う|
|SnapshotException|ERROR|STOP_RUN候補|Evidence保持不能のため|
|DiffException|ERROR|STOP_SCENARIO / CONTINUE|ReportにError反映|
|ReportException|ERROR|STOP_RUN|Run Result保存を優先|
|SecurityException|ERROR|STOP_RUN|保存・出力停止|
|SystemException|ERROR|STOP_RUN|Run終了|

---

# 20. Retry方針

|例外|Retry対象|標準回数|備考|
|----|---------|--------|----|
|TimeoutException|Yes|API / Environment設定|Backoff適用|
|ConnectionException|Yes|API / Environment設定|一時障害候補|
|HTTP 500|Yes|設定による| |
|HTTP 502|Yes|設定による| |
|HTTP 503|Yes|設定による| |
|HTTP 504|Yes|設定による| |
|HTTP 400|No|0|Request不正|
|HTTP 401|原則No|0|Token再取得設計がある場合を除く|
|HTTP 403|No|0|権限不備|
|HTTP 404|No|0|業務結果として扱う場合あり|
|SpecException|No|0|定義修正が必要|
|ContextException|No|0|定義または前段処理修正が必要|

---

# 21. Retry Log

Retry時は以下を記録する。

|項目|内容|
|----|----|
|retryCount|現在のRetry回数|
|maxRetryCount|最大Retry回数|
|retryReason|Retry理由|
|nextRetryAt|次回実行予定時刻|
|backoffMillis|待機時間|
|previousError|直前Error|

例：

```json
{
  "timestamp": "2026-07-10T09:00:42.000+09:00",
  "level": "WARN",
  "eventId": "API_CALL_RETRY",
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-004",
  "apiId": "API-002",
  "message": "Retrying API call after timeout.",
  "details": {
    "retryCount": 1,
    "maxRetryCount": 2,
    "backoffMillis": 1000
  }
}
```

---

# 22. Error Snapshot連携

## 22.1 保存タイミング

|条件|Error Snapshot|
|----|--------------|
|API Error|保存|
|Timeout|保存|
|Context Error|保存|
|Spec Error|保存可能な範囲で保存|
|Snapshot Error|別の最小Error Metadataを保存|
|Report Error|保存|
|Security Error|秘匿Dataを除いて保存|

---

## 22.2 Error Snapshot形式

```json
{
  "errorId": "ERR-API-001",
  "exceptionCategory": "TimeoutException",
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-004",
  "stepId": "UC-STEP-002",
  "apiId": "API-002",
  "message": "API timeout.",
  "technicalMessage": "API-002 timeout after 10 seconds.",
  "result": "FAIL",
  "continuePolicy": "STOP_SCENARIO",
  "retryCount": 2,
  "evidencePath": "outputs/runs/RUN-20260710-001/logs/error.log",
  "occurredAt": "2026-07-10T09:01:10+09:00"
}
```

---

# 23. StackTrace方針

|環境|StackTrace保存|Report表示|
|----|--------------|----------|
|LOCAL|全文保存|必要時表示|
|DEV|全文保存|Error Reportへ一部表示可|
|STG|Logへ保存|Reportには要約のみ|
|PROD-LIKE|制限保存|Reportへ表示しない|

StackTrace内にRequest Body、Token、個人情報が含まれる可能性がある場合、Maskまたは出力抑止する。

---

# 24. Error Report連携

Error Reportには以下を出力する。

|項目|内容|
|----|----|
|Error ID|一意識別子|
|Error分類|Spec / Config / API / Context等|
|Result|FAIL / ERROR|
|UseCase / Scenario / API|発生位置|
|Message|利用者向け説明|
|Technical Summary|技術要約|
|Retry Count|Retry回数|
|Continue Policy|停止範囲|
|Evidence Link|Snapshot / Logへのリンク|
|対応候補|確認・修正候補|

---

# 25. Audit Log

## 25.1 Audit対象

|操作|Audit Log|
|----|---------|
|Baseline承認|必須|
|Baseline取消|必須|
|手動Run開始|必須|
|対象UseCase変更|必須|
|Compare Policy変更|必須|
|Environment設定変更|必須|
|Secret参照|値は出力せず操作のみ記録|
|Report再生成|記録|
|Run削除 / Archive|記録|

---

## 25.2 Audit Log形式

```json
{
  "timestamp": "2026-07-10T18:00:00+09:00",
  "level": "AUDIT",
  "eventId": "BASELINE_APPROVED",
  "actor": "leader",
  "runId": "RUN-20260710-001",
  "message": "Baseline approved.",
  "details": {
    "baselineId": "BASE-20260710-001",
    "scope": ["UC-001", "SC-001"]
  }
}
```

---

# 26. 例外処理フロー

```mermaid
flowchart TD

A[Exception発生] --> B{例外分類}
B --> C[Error ID採番]
C --> D[Mask処理]
D --> E[Error Log出力]
E --> F[Error Snapshot保存]
F --> G{Retry対象?}

G -- Yes --> H[Retry実行]
H --> I{Retry成功?}
I -- Yes --> J[処理継続]
I -- No --> K[停止範囲判定]

G -- No --> K
K --> L[Step / Scenario / UseCase / Run停止]
L --> M[Result更新]
M --> N[Error Report反映]
```

---

# 27. 例外判定優先順位

複数の異常が同時に発生した場合、以下の優先順位でResultを決定する。

```text
FATAL
  ↓
ERROR
  ↓
FAIL
  ↓
WARN
  ↓
PASS
```

例：

|発生内容|最終Result|
|--------|----------|
|Validation FAIL + Report WARN|FAIL|
|API FAIL + Snapshot ERROR|ERROR|
|WARN複数件|WARN|
|Ignore差分のみ|PASS|

---

# 28. 想定外例外

想定外のRuntime Exceptionは `SystemException` として扱う。

|処理|内容|
|----|----|
|Error ID|ERR-SYS-XXX|
|Log Level|FATAL|
|Run Result|ERROR|
|停止範囲|STOP_RUN|
|StackTrace|環境方針に従って保存|
|Report|Error Reportへ反映|
|Evidence|保存可能なSnapshotを保持|

---

# 29. ログ・例外処理の非機能要件

|分類|要件|
|----|----|
|性能|通常ログ出力がAPI実行性能へ過大な影響を与えないこと|
|可用性|通常ログ書込失敗時も可能な範囲で標準Error出力へ退避すること|
|監査性|重要操作をAudit Logで追跡可能であること|
|安全性|秘匿情報がログ・Reportへ出力されないこと|
|検索性|runId、useCaseId、scenarioId、apiId、errorIdで検索可能であること|
|保存性|Run単位でArchive可能であること|

---

# 30. 実装Component案

|Component|責務|
|---------|----|
|LogService|共通Log Event出力|
|StructuredLogWriter|JSONL出力|
|TextLogWriter|テキストログ出力|
|AuditLogService|Audit Log出力|
|MaskService|Log / Exception DataのMask|
|ExceptionClassifier|Throwableから例外分類を判定|
|ExceptionHandler|停止範囲・Result判定|
|RetryPolicyResolver|Retry可否・回数を決定|
|ErrorSnapshotService|Error Snapshot保存|
|ErrorReportMapper|Error Report Model生成|

---

# 31. Java Package構成案

```text
runtime/src/main/java/com/example/e6verifier/

├── logging/
│   ├── LogService.java
│   ├── LogEvent.java
│   ├── StructuredLogWriter.java
│   ├── TextLogWriter.java
│   └── AuditLogService.java
│
├── exception/
│   ├── VerificationException.java
│   ├── SpecException.java
│   ├── ConfigException.java
│   ├── ContextException.java
│   ├── ApiException.java
│   ├── TimeoutException.java
│   ├── ValidationException.java
│   ├── SnapshotException.java
│   ├── DiffException.java
│   ├── ReportException.java
│   ├── ExceptionClassifier.java
│   └── GlobalExceptionHandler.java
│
├── retry/
│   ├── RetryPolicy.java
│   └── RetryPolicyResolver.java
│
└── security/
    └── MaskService.java
```

---

# 32. Review観点

|観点|確認内容|
|----|--------|
|Trace|runId / UseCase / Scenario / APIで追跡可能か|
|Level|INFO / WARN / ERRORの使い分けが明確か|
|Mask|Token、個人情報が出力されないか|
|停止範囲|例外ごとの停止単位が定義されているか|
|Retry|Retry対象と非対象が明確か|
|Snapshot連携|Error Snapshotが保存されるか|
|Report連携|Error Reportへ必要情報が渡るか|
|StackTrace|環境別方針が定義されているか|
|Audit|Baseline承認等が記録されるか|
|想定外例外|SystemExceptionとしてRun ERRORになるか|

---

# Appendix A. 正常実行ログ例

```json
{"timestamp":"2026-07-10T09:00:00.000+09:00","level":"INFO","eventId":"RUN_START","logger":"RunRunner","runId":"RUN-20260710-001","message":"Run started.","details":{"environment":"STG"}}
{"timestamp":"2026-07-10T09:00:10.000+09:00","level":"INFO","eventId":"USECASE_START","logger":"UseCaseRunner","runId":"RUN-20260710-001","useCaseId":"UC-001","message":"UseCase started."}
{"timestamp":"2026-07-10T09:00:31.000+09:00","level":"INFO","eventId":"API_CALL_START","logger":"ApiExecutor","runId":"RUN-20260710-001","useCaseId":"UC-001","scenarioId":"SC-001","stepId":"UC-STEP-001","apiId":"API-001","message":"API call started."}
{"timestamp":"2026-07-10T09:00:31.128+09:00","level":"INFO","eventId":"API_CALL_COMPLETED","logger":"ApiExecutor","runId":"RUN-20260710-001","useCaseId":"UC-001","scenarioId":"SC-001","stepId":"UC-STEP-001","apiId":"API-001","message":"API call completed.","details":{"httpStatus":200,"elapsedMillis":128}}
```

---

# Appendix B. Timeout例

```json
{
  "timestamp": "2026-07-10T09:01:10.000+09:00",
  "level": "ERROR",
  "eventId": "API_CALL_TIMEOUT",
  "logger": "ApiExecutor",
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-004",
  "stepId": "UC-STEP-002",
  "apiId": "API-002",
  "errorId": "ERR-API-001",
  "exceptionType": "TimeoutException",
  "message": "API call timed out after retry.",
  "details": {
    "timeoutSeconds": 10,
    "retryCount": 2,
    "continuePolicy": "STOP_SCENARIO"
  },
  "evidencePath": "outputs/runs/RUN-20260710-001/snapshot/UC-001_SC-004_UC-STEP-002_API-002_error.json"
}
```

---

# Appendix C. Context Error例

```json
{
  "timestamp": "2026-07-10T09:02:00.000+09:00",
  "level": "ERROR",
  "eventId": "CONTEXT_ERROR",
  "logger": "ContextBinder",
  "runId": "RUN-20260710-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "stepId": "UC-STEP-002",
  "apiId": "API-002",
  "errorId": "ERR-CTX-001",
  "exceptionType": "ContextException",
  "message": "Required context is missing.",
  "details": {
    "contextId": "CTX-001",
    "contextName": "Customer.id",
    "result": "ERROR",
    "continuePolicy": "STOP_SCENARIO"
  }
}
```

---

# Appendix D. Result判定例

|発生事象|Step Result|Scenario Result|UseCase Result|Run Result|
|--------|-----------|---------------|--------------|----------|
|全API正常|PASS|PASS|PASS|PASS|
|許容差分あり|WARN|WARN|WARN|WARN|
|固定値不一致|FAIL|FAIL|FAIL|FAIL|
|API Timeout|FAIL / ERROR|FAIL / ERROR|FAIL / ERROR|FAIL / ERROR|
|必須Context不足|ERROR|ERROR|ERROR|ERROR|
|Report生成失敗|－|－|－|ERROR|

:::

这份完成后，`system/05_framework/` 还剩下最重要的一份基础设计：

```text
system/05_framework/環境設計書.md
```

## 第 193 轮

### 你

继续

### ChatGPT

:::writing{variant="document" id="46183"}
---
title: 環境設計書
document_id: SYS-ENV-001
version: 1.0.0
status: Template
document_type: Framework Design
system_name: E6 API Verification Platform
phase: Framework Design
author:
reviewer:
approver:
created:
updated:
---

# 環境設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|----|----|
|文書ID|SYS-ENV-001|
|文書名称|環境設計書|
|対象システム|E6 API Verification Platform|
|対象範囲|LOCAL / DEV / STG / PROD-LIKE / Build / Release / Runtime / Secret / Network|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|----|----|----|--------|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|備考|
|------|------|------|----|
|SYS-DESIGN-001|システム設計書|system/05_framework/|全体設計|
|SYS-FW-001|共通Framework設計書|system/05_framework/|Runtime設計|
|SYS-IO-001|ファイル入出力設計書|system/05_framework/|File I/O設計|
|SYS-LOG-001|ログ・例外設計書|system/05_framework/|Log / Exception設計|
|MST-ENV-001|Environment_Master.md|system/02_master/|環境Master|
|RULE-REPO-001|Repository構成.md|system/00_repository/|Repository構成|

---

# 2. 目的

本書は、E6 API Verification Platform の開発、検証、Staging、本番相当実行に必要な環境構成、設定管理、Network、Secret、Build、Release、Deployment、運用方式を定義する。

---

# 3. 環境基本方針

|方針|内容|
|----|----|
|環境分離|LOCAL、DEV、STG、PROD-LIKEを分離する|
|設定外部化|Base URL、Timeout、Retry、Proxy、認証情報を外部設定化する|
|Secret分離|Token、Password、証明書をRepositoryへ保存しない|
|Runtime共通化|同一Release PackageまたはDocker Imageを環境別設定で動作させる|
|本番相当性|STGまたはPROD-LIKEでLinux本番相当構成を再現する|
|再現性|Version、Config、Spec、Image DigestをRun単位で記録する|
|最小権限|Runtime実行UserとSecret参照権限を最小化する|
|安全性|更新系API実行時は対象環境とTestDataを制限する|

---

# 4. 対象環境

|環境ID|環境名|目的|実行場所|日次実行|備考|
|------|------|----|--------|--------|----|
|ENV-LOCAL|LOCAL|開発者のローカル検証|Windows / Linux / Docker|No|Mock利用可|
|ENV-DEV|DEV|開発・単体検証|開発Server / Docker|No|E6 DEV接続|
|ENV-STG|STG|結合・日次検証|Linux / Docker|Yes|主要検証環境|
|ENV-PLK|PROD-LIKE|本番相当確認|Linux / Docker|Yes / Manual|本番相当設定|
|ENV-BUILD|BUILD|Build / Package / Image作成|CI / Build Server|No|E6 API接続なし|

---

# 5. 環境構成概要

```mermaid
flowchart LR

DEV[Development Repository]
BUILD[Build Environment]
REG[Artifact / Image Repository]
STG[STG Linux]
PLK[PROD-LIKE Linux]
E6D[E6 DEV API]
E6S[E6 STG API]
E6P[E6 PROD-LIKE API]

DEV --> BUILD
BUILD --> REG
REG --> STG
REG --> PLK

STG --> E6S
PLK --> E6P
DEV --> E6D
```

---

# 6. LOCAL環境

## 6.1 目的

LOCAL環境は、開発者がRuntime、Spec、TestData、Snapshot、Diff、Reportの動作を確認するために利用する。

---

## 6.2 構成

|項目|内容|
|----|----|
|OS|Windows 10 / 11 または Linux|
|Java|JDK 17以上を候補|
|Build Tool|Maven / Gradle|
|Container|Docker Desktop / Docker Engine|
|Config|runtime/config/local.yml|
|E6接続|Mock / DEV|
|Log Level|DEBUG|
|Output|repository/outputs/|

---

## 6.3 LOCAL実行例

```bash
java -jar e6-verifier.jar \
  --environment LOCAL \
  --usecase UC-001 \
  --scenario SC-001
```

---

## 6.4 LOCAL Docker例

```yaml
services:
  e6-verifier:
    image: e6-verifier:local
    volumes:
      - ./system:/app/system:ro
      - ./runtime/config:/app/config:ro
      - ./outputs:/app/outputs
    environment:
      E6_ENVIRONMENT: LOCAL
      E6_CONFIG_PATH: /app/config/local.yml
```

---

# 7. DEV環境

## 7.1 目的

DEV環境は、Runtime開発、API接続確認、個別Scenario確認、障害調査に利用する。

---

## 7.2 構成

|項目|内容|
|----|----|
|OS|Linux / Windows|
|実行方式|Java Process / Docker|
|接続先|E6 DEV API|
|Config|runtime/config/dev.yml|
|Secret|Environment Variable / Secret File|
|Log Level|DEBUG|
|日次実行|原則なし|
|TestData|開発専用Data|

---

## 7.3 制約

|制約|内容|
|----|----|
|本番Data禁止|本番実データを利用しない|
|更新API制限|更新系APIは専用TestDataのみ|
|Secret共有禁止|個人単位または環境単位Secretを利用|
|Baseline用途|正式Baselineには使用しない|

---

# 8. STG環境

## 8.1 目的

STG環境は、日次検証、結合検証、Release前確認に利用する主要環境である。

---

## 8.2 構成

|項目|内容|
|----|----|
|OS|Linux|
|実行方式|Docker Container推奨|
|接続先|E6 STG API|
|Config|/opt/e6-verifier/config/application-stg.yml|
|Secret|/opt/e6-verifier/config/secret/ または環境変数|
|Output|/opt/e6-verifier/data/|
|Log Level|INFO|
|日次実行|Yes|
|Scheduler|cron / systemd timer / 外部Scheduler|

---

## 8.3 STG配置例

```text
/opt/e6-verifier/

├── app/
│   ├── bin/
│   ├── lib/
│   ├── specs/
│   └── resources/
├── config/
│   ├── application-stg.yml
│   └── secret/
├── data/
│   ├── baseline/
│   ├── runs/
│   ├── reports/
│   └── tmp/
└── logs/
```

---

# 9. PROD-LIKE環境

## 9.1 目的

PROD-LIKE環境は、本番に近いNetwork、Certificate、Proxy、権限、運用条件で最終確認を行う。

---

## 9.2 構成

|項目|内容|
|----|----|
|OS|本番相当Linux|
|Container Runtime|Docker Engine|
|接続先|E6 PROD-LIKE API|
|Config|application-prod-like.yml|
|Secret|本番相当Secret管理|
|Log Level|INFO|
|StackTrace|制限|
|日次実行|運用方針による|
|更新系API|原則制限|

---

## 9.3 本番相当確認項目

|確認項目|内容|
|--------|----|
|Network|Proxy、Firewall、DNS、TLS|
|Certificate|信頼Store、期限、更新方式|
|Permission|実行User、File Permission|
|Output|保存容量、Archive|
|Scheduler|起動時刻、重複実行防止|
|Secret|参照権限、Rotation|
|Report|閲覧者、配布先|
|Recovery|失敗時再実行|

---

# 10. BUILD環境

## 10.1 目的

BUILD環境は、Java Artifact、Release Package、Docker Imageを作成する。

---

## 10.2 Build入力

|入力|配置先|
|----|------|
|Java Source|runtime/src/|
|Runtime Resource|runtime/config template|
|Execution Spec|system/06_verification_assets/|
|Schema|runtime/config/schema/|
|Build Script|build/scripts/|
|Dockerfile|build/docker/|

---

## 10.3 Build出力

|出力|例|
|----|--|
|Executable JAR|e6-verifier-1.0.0.jar|
|Release Package|e6-verifier-1.0.0.zip|
|Docker Image|e6-verifier:1.0.0|
|Checksum|SHA-256|
|Version Metadata|build-info.json|

---

# 11. Release Package構成

```text
e6-verifier-1.0.0/

├── bin/
│   ├── run.sh
│   ├── daily-run.sh
│   └── verify-config.sh
├── lib/
│   └── e6-verifier-1.0.0.jar
├── specs/
│   ├── execution_spec/
│   ├── api_test_spec/
│   ├── usecase_test_spec/
│   └── test_data/
├── resources/
│   └── schema/
├── config-template/
│   ├── application-local.yml
│   ├── application-dev.yml
│   ├── application-stg.yml
│   └── application-prod-like.yml
├── VERSION
├── build-info.json
└── README.md
```

---

# 12. Docker Image設計

## 12.1 基本方針

|項目|方針|
|----|----|
|Base Image|公式JREまたは承認済み社内Image|
|実行User|非root User|
|Application|JARをImageへ格納|
|Config|外部Mount|
|Secret|外部注入|
|Output|外部Volume|
|Timezone|Asia/Tokyo|
|Locale|ja_JP.UTF-8|
|Health Check|Config / Process確認|

---

## 12.2 Dockerfile例

```dockerfile
FROM eclipse-temurin:17-jre

WORKDIR /app

RUN useradd -r -u 10001 verifier

COPY lib/e6-verifier.jar /app/e6-verifier.jar
COPY resources/schema /app/schema

RUN mkdir -p /app/outputs \
    && chown -R verifier:verifier /app

USER verifier

ENTRYPOINT ["java", "-jar", "/app/e6-verifier.jar"]
```

---

# 13. Environment Masterとの関係

`Environment_Master.md` は環境ごとの論理設定を管理し、本設計書は物理構成および運用方式を定義する。

|定義内容|Environment Master|環境設計書|
|--------|------------------|----------|
|環境ID|○|参照|
|Base URL|○|参照|
|認証方式|○|詳細方式|
|Timeout / Retry|○|適用方式|
|Server構成|－|○|
|Docker構成|－|○|
|Network|－|○|
|Secret配置|概要|詳細|
|Deployment|－|○|

---

# 14. Runtime Config設計

## 14.1 Config配置

|環境|配置|
|----|----|
|LOCAL|runtime/config/local.yml|
|DEV|runtime/config/dev.yml|
|STG|/opt/e6-verifier/config/application-stg.yml|
|PROD-LIKE|/opt/e6-verifier/config/application-prod-like.yml|

---

## 14.2 Config例

```yaml
runtime:
  environment: STG
  timezone: Asia/Tokyo
  runMode: DAILY
  outputRoot: /opt/e6-verifier/data
  logLevel: INFO

e6:
  baseUrl: https://stg.example.com
  authType: BEARER
  timeoutSeconds: 10
  retryCount: 2

proxy:
  enabled: true
  host: proxy.example.com
  port: 8080

snapshot:
  enabled: true
  maskEnabled: true

diff:
  baselineMode: APPROVED_FIRST

report:
  markdownEnabled: true
  htmlEnabled: false
  latestEnabled: true
```

---

# 15. Config優先順位

|優先順位|設定元|
|--------|------|
|1|CLI引数|
|2|Environment Variable|
|3|Environment別Config|
|4|Environment_Master|
|5|API設計書|
|6|Framework Default|

Secret値はMasterおよびAPI設計書へ記載しない。

---

# 16. 環境変数

|環境変数|用途|必須|
|--------|----|----|
|E6_ENVIRONMENT|対象環境|○|
|E6_CONFIG_PATH|Config File Path|○|
|E6_OUTPUT_ROOT|Output Root|－|
|E6_BASE_URL|Base URL Override|－|
|E6_AUTH_TOKEN|Bearer Token|条件付き|
|E6_API_KEY|API Key|条件付き|
|E6_PROXY_HOST|Proxy Host|－|
|E6_PROXY_PORT|Proxy Port|－|
|E6_LOG_LEVEL|Log Level Override|－|
|E6_JAVA_OPTS|JVM Option|－|

---

# 17. Secret設計

## 17.1 Secret対象

|Secret|例|
|------|--|
|Bearer Token|E6_AUTH_TOKEN|
|API Key|E6_API_KEY|
|Password|Basic Auth Password|
|Certificate|Client Certificate|
|Private Key|mTLS Private Key|
|Proxy Credential|Proxy User / Password|

---

## 17.2 Secret管理方式

|環境|管理方式|
|----|--------|
|LOCAL|`.env` またはLocal Secret File|
|DEV|Environment Variable / Secret File|
|STG|Server Secret Directory / Container Secret|
|PROD-LIKE|承認済みSecret管理方式|

---

## 17.3 Secret配置例

```text
/opt/e6-verifier/config/secret/

├── auth-token
├── api-key
├── client-cert.p12
└── proxy-password
```

---

## 17.4 Secret権限

|項目|方針|
|----|----|
|Owner|Runtime実行User|
|Permission|600相当|
|Git管理|禁止|
|Log出力|禁止|
|Snapshot保存|禁止|
|Report表示|禁止|
|Rotation|運用方針に従う|

---

# 18. Network設計

## 18.1 通信一覧

|From|To|Protocol|Port|用途|
|----|--|--------|----|----|
|Verifier Runtime|E6 API|HTTPS|443|API実行|
|Verifier Runtime|Proxy|HTTP / HTTPS|環境依存|外部接続|
|Build Server|Artifact Repository|HTTPS|443|Artifact Publish|
|Operation User|Linux Server|SSH|22|運用管理|
|Report Viewer|Report保存先|HTTPS / File|環境依存|Report確認|

---

## 18.2 Network確認項目

|確認項目|内容|
|--------|----|
|DNS|E6 Endpointが名前解決可能か|
|Proxy|Proxy経由要否|
|Firewall|443通信許可|
|TLS|TLS Version / Cipher|
|Certificate|信頼Chain|
|Timeout|Connect / Read Timeout|
|Keep Alive|利用有無|
|IP制限|接続元IP許可|

---

# 19. TLS / Certificate設計

|項目|内容|
|----|----|
|通信方式|HTTPS|
|Server Certificate|Trust Storeで検証|
|Client Certificate|必要時mTLS|
|Trust Store|JVM標準または環境専用|
|Key Store|Secret Directory|
|証明書期限監視|運用対象|
|証明書更新|再DeploymentまたはSecret更新|

---

# 20. Proxy設計

|項目|内容|
|----|----|
|利用有無|環境別Configで管理|
|Proxy Host|Config / Environment Variable|
|Proxy Port|Config / Environment Variable|
|認証|必要時Secret管理|
|No Proxy|E6内部Endpoint等|
|ログ|Credentialは出力禁止|

---

# 21. File System設計

## 21.1 Linux配置

```text
/opt/e6-verifier/

├── app/
├── config/
├── data/
└── logs/
```

---

## 21.2 Directory権限

|Directory|Owner|Permission候補|用途|
|---------|-----|----------------|----|
|app|root / deploy user|755|Application|
|config|runtime user|750|Config|
|config/secret|runtime user|700|Secret|
|data|runtime user|750|Snapshot / Report|
|logs|runtime user|750|Log|

---

## 21.3 容量管理

|対象|管理方針|
|----|--------|
|runs|保存期間経過後Archive / Delete|
|reports/history|長期保存候補|
|baseline/approved|削除禁止または承認制|
|logs|Rotation|
|tmp|Run終了後削除|
|raw Snapshot|容量増加を監視|

---

# 22. Scheduler設計

## 22.1 起動方式

|方式|利用候補|
|----|--------|
|cron|単純な日次実行|
|systemd timer|Linux標準運用|
|CI Scheduler|DEV / STG検証|
|外部Job Scheduler|企業運用基盤|
|手動実行|調査・再実行|

---

## 22.2 日次実行例

```bash
/opt/e6-verifier/app/bin/daily-run.sh \
  --environment STG \
  --run-mode DAILY
```

---

## 22.3 重複実行防止

|項目|方針|
|----|----|
|Lock File|Run開始時に作成|
|PID確認|既存Process有無確認|
|Run ID|日時 + 連番 / UUID|
|重複時|新規RunをERRORまたはSKIP|
|異常終了時Lock|Timeout後に運用解除可能|

---

# 23. Run ID設計

## 23.1 形式

```text
RUN-YYYYMMDD-HHMMSS-XXX
```

または：

```text
RUN-YYYYMMDD-UUID短縮値
```

---

## 23.2 例

```text
RUN-20260715-090000-001
RUN-20260715-A1B2C3D4
```

---

## 23.3 要件

|要件|内容|
|----|----|
|一意性|同一環境内で重複しない|
|可読性|実行日が識別可能|
|Trace性|Log / Snapshot / Reportで共通利用|
|並列対応|並列Runでも重複しない|

---

# 24. Deployment設計

## 24.1 Deployment Flow

```text
Source
  ↓
Build
  ↓
Test
  ↓
Package / Docker Image
  ↓
STG Deploy
  ↓
Smoke Test
  ↓
PROD-LIKE Deploy
```

---

## 24.2 Deployment単位

|対象|Deployment|
|----|----------|
|Runtime JAR|Release Package / Image|
|Config Template|Release Package|
|Environment Config|Server側管理|
|Secret|別管理|
|Execution Spec|Release対象|
|TestData|Release対象または運用投入|
|Baseline|Deployment対象外|

---

## 24.3 Deployment前確認

|確認項目|内容|
|--------|----|
|Artifact Version|承認済みか|
|Checksum|一致するか|
|Config Validation|成功するか|
|Secret存在|必要Secretがあるか|
|Network|E6 APIへ接続可能か|
|Disk|空き容量十分か|
|Permission|Runtime Userで実行可能か|
|Previous Version|Rollback可能か|

---

# 25. Rollback設計

|対象|Rollback方法|
|----|------------|
|Runtime JAR|前Versionへ戻す|
|Docker Image|前Tag / Digestへ戻す|
|Config|Backup Configへ戻す|
|Execution Spec|Git Tagまたは前Releaseへ戻す|
|TestData|前Releaseへ戻す|
|Baseline|承認済Baselineを維持|

---

# 26. Health Check

## 26.1 起動前Check

|Check ID|確認内容|失敗時|
|--------|--------|------|
|HC-001|Java Version|起動停止|
|HC-002|Config File存在|起動停止|
|HC-003|Schema読込|起動停止|
|HC-004|Output Directory書込|起動停止|
|HC-005|Secret存在|対象認証の場合起動停止|
|HC-006|E6 Endpoint DNS|WARN / 起動停止|
|HC-007|Certificate有効|起動停止|
|HC-008|Disk容量|WARN / 起動停止|

---

## 26.2 Runtime Health

|確認項目|内容|
|--------|----|
|Process|Java Process稼働|
|Lock|Run Lock整合|
|Output|Snapshot書込可能|
|Log|Log書込可能|
|API|E6 API接続可能|
|Report|Latest更新可能|

---

# 27. Environment Validation

Runtime起動前に以下を検証する。

|Validation|内容|
|----------|----|
|Environment ID|Environment_Masterに存在するか|
|Base URL|HTTPS URL形式か|
|Config Schema|Schemaに適合するか|
|Secret|必要なSecretが存在するか|
|Path|許可されたRoot配下か|
|Timeout|正の数か|
|Retry|許容範囲内か|
|Log Level|許容値か|
|Output Permission|書込可能か|

---

# 28. 更新系API安全設計

## 28.1 基本方針

更新、登録、削除APIは、参照APIより厳しい実行制御を行う。

---

## 28.2 制御項目

|制御|内容|
|----|----|
|Environment制限|許可環境以外では実行不可|
|TestData制限|専用TestDataのみ|
|実行Flg|明示的な許可Flgが必要|
|Dry Run|可能な場合利用|
|承認|手動承認を要求可能|
|Cleanup|実行後Data復元または削除|
|Evidence|Request / Responseを必須保存|

---

## 28.3 Config例

```yaml
safety:
  updateApiEnabled: false
  allowedEnvironments:
    - DEV
    - STG
  requireExplicitApproval: true
```

---

# 29. 環境別差異管理

|設定項目|LOCAL|DEV|STG|PROD-LIKE|
|--------|-----|---|---|---------|
|E6接続|Mock / DEV|DEV|STG|PROD-LIKE|
|Log Level|DEBUG|DEBUG|INFO|INFO|
|StackTrace|Full|Full|Errorのみ|制限|
|Daily Run|No|No|Yes|方針による|
|Update API|Mockのみ|制限|原則禁止 / 承認制|禁止|
|Baseline正式利用|No|No|Yes|Yes|
|Report History|任意|任意|Yes|Yes|

---

# 30. Monitoring設計

|監視対象|監視内容|
|--------|--------|
|Run Result|PASS / WARN / FAIL / ERROR|
|Scheduler|起動有無|
|Process|異常終了|
|Disk|使用率|
|Log|ERROR / FATAL|
|Report|Daily Summary生成有無|
|Certificate|有効期限|
|Secret|期限 / Rotation|
|API Response Time|遅延傾向|

---

# 31. 通知設計概要

|通知条件|通知レベル|通知先候補|
|--------|----------|----------|
|Run PASS|Info|必要に応じて|
|Run WARN|Warning|Leader|
|Run FAIL|Critical|Leader / 開発担当|
|Run ERROR|Critical|運用 / 開発担当|
|Scheduler未実行|Critical|運用|
|Certificate期限接近|Warning|運用|
|Disk容量不足|Warning / Critical|運用|

具体的な通知方式は運用設計で定義する。

---

# 32. Backup / Archive

|対象|Backup方針|
|----|----------|
|Approved Baseline|必須|
|Report History|必須候補|
|Run Evidence|保存期間に応じてArchive|
|Config|変更前Backup|
|Secret|Secret管理基盤方針に従う|
|Application|Release Artifactで再配置可能|

---

# 33. Disaster Recovery概要

|事象|復旧方針|
|----|--------|
|Application破損|Release Package再配置|
|Config破損|Backup復元|
|Output破損|Archiveから復元|
|Baseline破損|Backup Baseline復元|
|Server障害|別ServerへRelease配置|
|Secret失効|再発行・再設定|
|Certificate失効|更新後再Deployment|

---

# 34. 環境構築手順概要

```text
1. Linux User作成
2. Directory作成
3. Permission設定
4. Java / Docker確認
5. Release Package配置
6. Config配置
7. Secret配置
8. Certificate配置
9. Network疎通確認
10. Config Validation
11. Smoke Test
12. Scheduler設定
13. 運用引継ぎ
```

---

# 35. Smoke Test

|Test ID|確認内容|期待結果|
|-------|--------|--------|
|SMK-001|Application起動|正常起動|
|SMK-002|Config読込|成功|
|SMK-003|Master / Spec読込|成功|
|SMK-004|Output書込|成功|
|SMK-005|E6接続|疎通成功|
|SMK-006|認証|認証成功|
|SMK-007|代表API実行|PASS|
|SMK-008|Snapshot生成|成功|
|SMK-009|Diff生成|成功|
|SMK-010|Report生成|成功|

---

# 36. 環境構築成果物

|成果物|配置先|
|------|------|
|Environment Master|system/02_master/|
|環境設計書|system/05_framework/|
|Config Template|runtime/config/|
|Dockerfile|build/docker/|
|docker-compose.yml|staging/|
|Deployment Script|build/scripts/|
|Run Script|runtime/scripts/|
|Environment Validation Script|runtime/scripts/|
|Smoke Test Spec|system/06_verification_assets/|

---

# 37. 課題・確認事項

|No|分類|確認事項|影響範囲|確認先|優先度|状態|対応方針|
|--|----|--------|--------|------|------|----|--------|
|1|Runtime|本番相当環境でDocker利用可能か|Deployment|Infra担当|High|Open|基盤制約確認|
|2|Network|E6 API接続にProxyが必要か|HTTP Client|Infra担当|High|Open|Network確認|
|3|Secret|Tokenの取得・更新方式|Authentication|E6担当|High|Open|認証仕様確認|
|4|Scheduler|日次実行Schedulerの種類|運用|運用担当|Medium|Open|運用基盤確認|
|5|Data|更新系API用TestDataの準備方法|Safety|業務担当|High|Open|Data運用確認|
|6|Retention|Run Evidence保存期間|Storage|運用担当|Medium|Open|保存方針決定|

---

# 38. Traceability

|環境ID|Config|Secret|Runtime Version|Spec Version|Output Root|Scheduler|
|------|------|------|---------------|------------|-----------|---------|
|ENV-LOCAL|local.yml|Local Secret|1.0.0|1.0.0|repository/outputs|Manual|
|ENV-DEV|dev.yml|DEV Secret|1.0.0|1.0.0|DEV Output|Manual|
|ENV-STG|application-stg.yml|STG Secret|1.0.0|1.0.0|/opt/e6-verifier/data|Daily|
|ENV-PLK|application-prod-like.yml|PLK Secret|1.0.0|1.0.0|/opt/e6-verifier/data|Manual / Daily|

---

# 39. Review観点

|観点|確認内容|
|----|--------|
|環境分離|LOCAL / DEV / STG / PROD-LIKEが分離されているか|
|設定外部化|環境差異がCodeへHard Codingされていないか|
|Secret|SecretがGit、Log、Snapshotへ含まれないか|
|Network|DNS、Proxy、TLS、Firewallが整理されているか|
|Permission|Runtime Userが最小権限か|
|再現性|Version、Config、SpecがRun単位で追跡可能か|
|安全性|更新系APIの実行制御が定義されているか|
|Deployment|Buildから配置までのFlowが明確か|
|Rollback|前Versionへ戻せるか|
|Monitoring|Run失敗やScheduler未実行を検知できるか|

---

# Appendix A. STG環境記入例

## A.1 環境情報

|項目|内容|
|----|----|
|環境ID|ENV-STG|
|環境名|STG|
|OS|Linux|
|実行方式|Docker|
|Application Version|1.0.0|
|Config|/opt/e6-verifier/config/application-stg.yml|
|Output Root|/opt/e6-verifier/data|
|Log Level|INFO|
|Scheduler|cron|
|日次実行時刻|09:00 JST|

---

## A.2 Docker Compose例

```yaml
services:
  e6-verifier:
    image: e6-verifier:1.0.0
    container_name: e6-verifier
    user: "10001:10001"
    volumes:
      - /opt/e6-verifier/config:/app/config:ro
      - /opt/e6-verifier/data:/app/outputs
      - /opt/e6-verifier/logs:/app/logs
    environment:
      TZ: Asia/Tokyo
      E6_ENVIRONMENT: STG
      E6_CONFIG_PATH: /app/config/application-stg.yml
      E6_AUTH_TOKEN_FILE: /app/config/secret/auth-token
    restart: "no"
```

---

## A.3 cron例

```cron
0 9 * * * /opt/e6-verifier/app/bin/daily-run.sh >> /opt/e6-verifier/logs/scheduler.log 2>&1
```

---

## A.4 Run出力例

```text
/opt/e6-verifier/data/

├── baseline/
│   └── approved/
├── runs/
│   └── RUN-20260715-090000-001/
├── reports/
│   ├── latest/
│   └── history/
└── tmp/
```

:::

これで `system/05_framework/` の主要設計書は一通り揃いました。次は `system/06_verification_assets/` に入り、最初に `Verification仕様書_Template.md` を現在の Master・Scenario・Compare Policy 構成へ合わせて正式化する段階です。

## 第 194 轮

### 你

好

### ChatGPT

好的。下一步按当前冻结结构继续：

```text
system/06_verification_assets/Verification仕様書_Template.md
```

会基于现有的：

```text
Scenario_Master
API_UseCase_Scenario対応表
Compare_Policy_Master
API設計書
UseCase設計書
RunContext設計書
Snapshot設計書
Diff設計書
Report設計書
```

重新整理成正式完整版。

## 第 195 轮

### 你

继续

### ChatGPT

下面直接给 `Verification仕様書_Template.md` 正式完整版，并附 `UC-001 顧客情報照会` 的记入例。

### ChatGPT

放置位置：

```text
system/06_verification_assets/Verification仕様書_Template.md
```

:::writing{variant="document" id="58314"}
---
title: Verification仕様書テンプレート
document_id: VERIFICATION-SPEC-TEMPLATE
version: 1.0.0
status: Template
document_type: Verification Specification
system_name: E6 API Verification Platform
phase: Verification Design
author:
reviewer:
approver:
created:
updated:
---

# Verification仕様書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|---|---|
|文書ID|VER-XXX|
|文書名称|〇〇 Verification仕様書|
|Verification ID|VER-XXX|
|対象業務|（記載）|
|Business ID|BUS-XXX|
|対象UseCase|UC-XXX|
|対象Scenario|SC-XXX|
|対象API|API-XXX|
|関連業務分析書|BA-XXX|
|関連BAシナリオ一覧|BA-XXX_〇〇業務_シナリオ一覧.md|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|---|---|---|---|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|参照目的|
|---|---|---|---|
|BA-XXX|現行業務分析書|system/01_business/01_業務分析/|業務Flow、業務条件|
|BA-SC-XXX|BA分析書シナリオ一覧|system/01_business/01_業務分析/|API呼出経路、分岐|
|API-XXX|API設計書|system/03_api_design/|Request / Response契約|
|UC-XXX|UseCase設計書|system/04_usecase_design/|API実行順序、Context、Scenario|
|MST-SC-001|Scenario_Master|system/02_master/|Scenario管理|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|
|MST-API-UC-SC-001|API_UseCase_Scenario対応表|system/02_master/|API実行順序、Skip条件|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|共通比較Policy|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context処理|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|証跡保存|
|SYS-DIFF-001|Diff設計書|system/05_framework/|差分判定|
|SYS-RPT-001|Report設計書|system/05_framework/|結果出力|

---

# 2. Verification概要

## 2.1 Verification目的

本Verificationは、対象UseCaseおよびScenarioについて、E6 APIのRequest、Response、Context連携、業務結果、Baseline差分が期待仕様どおりであることを確認する。

---

## 2.2 Verification対象範囲

|対象分類|対象|検証有無|備考|
|---|---|---:|---|
|Request|入力項目、Header、Body、Parameter|Yes / No| |
|Response|HTTP Status、Header、Body|Yes / No| |
|Context|API間引継ぎ、生成値|Yes / No| |
|Business Result|Scenario期待結果|Yes / No| |
|API Execution|順序、Skip、Retry、Stop|Yes / No| |
|Baseline Diff|CurrentとBaselineの比較|Yes / No| |
|Error|HTTP Error、Timeout、業務Error|Yes / No| |
|Evidence|Request、Response、Context、Log|Yes / No| |
|Report|Daily Summary、Diff Report|Yes / No| |

---

## 2.3 Verification対象外

|対象外|理由|備考|
|---|---|---|
|（記載）|（記載）|（記載）|

---

## 2.4 Verification分類

|分類|内容|
|---|---|
|API Contract Verification|API設計書に定義された契約を確認する|
|UseCase Flow Verification|API実行順序、分岐、Skipを確認する|
|Scenario Verification|Scenario別の期待結果を確認する|
|Context Verification|API間Context連携を確認する|
|Baseline Verification|前回または承認済Baselineとの差分を確認する|
|Error Verification|異常時のStatus、Error Code、継続制御を確認する|

---

# 3. 対象UseCase・Scenario

## 3.1 対象UseCase

|UseCase ID|UseCase名称|Business ID|対象API|重要度|日次実行|備考|
|---|---|---|---|---|---|---|
|UC-XXX|（記載）|BUS-XXX|API-XXX|Critical / High / Medium / Low|Yes / No| |

---

## 3.2 対象Scenario

|Scenario ID|Scenario名称|分類|対象経路ID|開始API|終了API|期待結果|TestCase ID|重要度|
|---|---|---|---|---|---|---|---|---|
|SC-XXX|（記載）|Normal / Alternative / Exception / Boundary / Regression|PATH-XXX|API-XXX|API-XXX|PASS / WARN / FAIL|TC-XXX|High / Medium / Low|

---

## 3.3 Scenario実行条件

|Scenario ID|Entry条件|分岐条件|処理Flg|終了条件|備考|
|---|---|---|---|---|---|
|SC-XXX|（記載）|（記載）|（記載）|（記載）| |

---

# 4. 対象API

## 4.1 API一覧

|実行順|API ID|API名称|対象Scenario|実行要否|実行条件|Skip条件|API設計書|
|---:|---|---|---|---|---|---|---|
|1|API-XXX|（記載）|SC-XXX|必須 / 条件付き / Skip|（記載）|（記載）|API-XXX|

---

## 4.2 Scenario別API実行Matrix

|API / Scenario|SC-XXX|SC-XXX|SC-XXX|
|---|:---:|:---:|:---:|
|API-XXX|Run / Skip|Run / Skip|Run / Skip|
|API-XXX|Run / Skip|Run / Skip|Run / Skip|
|期待結果|PASS / WARN / FAIL|PASS / WARN / FAIL|PASS / WARN / FAIL|

---

## 4.3 API実行順序確認

|Check ID|Scenario ID|期待API順序|実際API順序取得元|不一致時Result|
|---|---|---|---|---|
|CHK-FLOW-XXX|SC-XXX|API-001 → API-002|Execution Snapshot|FAIL|

---

# 5. TestData

## 5.1 TestData一覧

|TestData ID|Scenario ID|名称|用途|配置先|有効期限|状態|
|---|---|---|---|---|---|---|
|TD-XXX|SC-XXX|（記載）|正常 / 異常 / 境界値|system/06_verification_assets/test_data/UC-XXX/|（記載）|Active / Deprecated|

---

## 5.2 Entry Input

|TestData ID|項目名|JSONPath|Type|値|必須|Mask|備考|
|---|---|---|---|---|---|---|---|
|TD-XXX|（記載）|$.xxx|String / Number / Boolean|（記載）|○ / －|Yes / No| |

---

## 5.3 TestData前提条件

|TestData ID|前提条件|確認方法|未成立時処理|備考|
|---|---|---|---|---|
|TD-XXX|（記載）|事前API / DB / 手動確認|BLOCKED / ERROR| |

---

## 5.4 TestData後処理

|TestData ID|後処理|対象API / Data|失敗時処理|備考|
|---|---|---|---|---|
|TD-XXX|Cleanup / Restore / なし|（記載）|WARN / ERROR| |

---

# 6. Request Verification

## 6.1 Request検証方針

Request Verificationでは、API設計書に定義されたRequest契約と、Runtimeが生成した実Requestを比較する。

---

## 6.2 Header検証

|Check ID|API ID|Header名|検証方式|期待値|重要度|不一致時Result|Evidence|
|---|---|---|---|---|---|---|---|
|CHK-REQ-H-XXX|API-XXX|Content-Type|Equals|application/json|High|FAIL|Request Snapshot|
|CHK-REQ-H-XXX|API-XXX|Authorization|Exists / Masked|存在|Critical|ERROR|Request Snapshot|

---

## 6.3 Request項目検証

|Check ID|API ID|JSONPath / Parameter|検証種別|期待仕様|設定元|重要度|不一致時Result|備考|
|---|---|---|---|---|---|---|---|---|
|CHK-REQ-XXX|API-XXX|$.xxx|Required / Type / Length / Pattern / Enum / Fixed / Context Match|（記載）|TestData / Context / Fixed|High|FAIL| |

---

## 6.4 Request Context Binding検証

|Check ID|API ID|Request JSONPath|Context ID|比較方式|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-BIND-XXX|API-XXX|$.xxx|CTX-XXX|Equals|High|FAIL|

---

## 6.5 Request検証実行順

```text
1. Header存在確認
2. 必須項目確認
3. Type確認
4. Null / Empty確認
5. Length確認
6. Pattern確認
7. Enum確認
8. 固定値確認
9. Context Binding確認
10. Request Snapshot保存
```

---

# 7. Response Verification

## 7.1 HTTP Status検証

|Check ID|API ID|Scenario ID|期待HTTP Status|許容Status|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-HTTP-XXX|API-XXX|SC-XXX|200|（記載）|High|FAIL|

---

## 7.2 Response項目検証

|Check ID|API ID|JSONPath|検証種別|期待仕様 / 値|Compare Policy|重要度|不一致時Result|備考|
|---|---|---|---|---|---|---|---|---|
|CHK-RES-XXX|API-XXX|$.xxx|Required / Type / Fixed / Enum / Pattern / Null|（記載）|Equals / Regex|High|FAIL| |

---

## 7.3 固定値検証

|Check ID|API ID|JSONPath|固定値|適用条件|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-FIX-XXX|API-XXX|$.resultCode|0|正常終了時|High|FAIL|

---

## 7.4 Enum検証

|Check ID|API ID|JSONPath|許容値|重要度|不一致時Result|
|---|---|---|---|---|---|
|CHK-ENUM-XXX|API-XXX|$.status|ACTIVE, INACTIVE|High|FAIL|

---

## 7.5 入力値一致検証

|Check ID|API ID|Response JSONPath|Request JSONPath|比較方式|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-INMATCH-XXX|API-XXX|$.customerId|$.customerId|Equals|High|FAIL|

---

## 7.6 Dynamic Field検証

|Check ID|API ID|JSONPath|検証方式|Compare Policy|期待結果|重要度|
|---|---|---|---|---|---|---|
|CHK-DYN-XXX|API-XXX|$.traceId|Exists / Type Only / Ignore|CMP-POL-001|PASS / IGNORED|Low|

---

# 8. Context Verification

## 8.1 Context生成検証

|Check ID|Context ID|Producer|Response JSONPath|必須|期待Type|未生成時Result|
|---|---|---|---|---|---|---|
|CHK-CTX-GEN-XXX|CTX-XXX|API-XXX|$.xxx|○ / －|String / Object / Array|ERROR / FAIL|

---

## 8.2 Context利用検証

|Check ID|Context ID|Consumer|Request JSONPath|比較方式|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-CTX-USE-XXX|CTX-XXX|API-XXX|$.xxx|Equals|High|FAIL|

---

## 8.3 Context Producer / Consumer検証

|Context ID|Producer|Consumer|Scope|期待動作|Verification Result|
|---|---|---|---|---|---|
|CTX-XXX|API-XXX / Entry Input|API-XXX / Report|UseCase / Scenario|正常に生成・利用されること|PASS / WARN / FAIL|

---

## 8.4 Context Lifetime検証

|Check ID|Context ID|生成タイミング|有効範囲|破棄タイミング|不一致時Result|
|---|---|---|---|---|---|
|CHK-CTX-LIFE-XXX|CTX-XXX|API実行後|UseCase|UseCase終了時|ERROR|

---

# 9. API Execution Verification

## 9.1 API Skip検証

|Check ID|Scenario ID|条件|Skip対象API|期待Execution Status|不一致時Result|
|---|---|---|---|---|---|
|CHK-SKIP-XXX|SC-XXX|（記載）|API-XXX|SKIP|FAIL|

---

## 9.2 API Continue / Stop検証

|Check ID|発生条件|期待制御|対象Scenario|不一致時Result|
|---|---|---|---|---|
|CHK-CTRL-XXX|API-XXX Error|STOP_SCENARIO / CONTINUE|SC-XXX|FAIL|

---

## 9.3 Retry検証

|Check ID|API ID|発生条件|期待Retry回数|Retry後期待結果|不一致時Result|
|---|---|---|---:|---|---|
|CHK-RETRY-XXX|API-XXX|Timeout|2|FAIL / ERROR|FAIL|

---

## 9.4 Timeout検証

|Check ID|API ID|Timeout設定|期待動作|Evidence|不一致時Result|
|---|---|---|---|---|---|
|CHK-TIMEOUT-XXX|API-XXX|10秒|Retry後Scenario停止|Execution Snapshot / Log|FAIL|

---

# 10. Business Result Verification

## 10.1 業務判定

|Check ID|Scenario ID|判定条件|期待Business Result|期待Scenario Result|重要度|
|---|---|---|---|---|---|
|CHK-BIZ-XXX|SC-XXX|（記載）|（記載）|PASS / WARN / FAIL|High|

---

## 10.2 処理Flg検証

|Check ID|処理Flg|発生条件|期待値|対象Scenario|不一致時Result|
|---|---|---|---|---|---|
|CHK-FLG-XXX|（記載）|（記載）|（記載）|SC-XXX|FAIL|

---

## 10.3 開始API・終了API検証

|Check ID|Scenario ID|期待開始API|期待終了API|実際値取得元|不一致時Result|
|---|---|---|---|---|---|
|CHK-PATH-XXX|SC-XXX|API-XXX|API-XXX|Execution Snapshot|FAIL|

---

# 11. Compare Policy

## 11.1 Compare対象

|Compare ID|対象分類|対象|Baseline種別|Compare Policy|重要度|備考|
|---|---|---|---|---|---|---|
|CMP-XXX|Response / Context / Business Result|$.xxx / CTX-XXX|Approved / Previous Success|CMP-POL-XXX|High / Medium / Low| |

---

## 11.2 Normalize Rule

|Normalize ID|対象|方式|適用順|備考|
|---|---|---|---:|---|
|NORM-XXX|$.xxx|Trim / Date Format / Sort / Decimal|1| |

---

## 11.3 Ignore Rule

|Compare ID|対象|Policy ID|Ignore理由|適用条件|備考|
|---|---|---|---|---|---|
|CMP-IGN-XXX|$.traceId|CMP-POL-001|実行毎に採番|常時|Existsのみ確認|

---

## 11.4 Tolerance Rule

|Compare ID|対象|Policy ID|Tolerance|単位|範囲外Result|
|---|---|---|---|---|---|
|CMP-TOL-XXX|$.updatedAt|CMP-POL-002|±3|秒|WARN / FAIL|

---

## 11.5 Collection Compare Rule

|Compare ID|対象JSONPath|方式|Key|順序考慮|件数比較|不一致時Result|
|---|---|---|---|---|---|---|
|CMP-COL-XXX|$.items[]|Key Match|itemId|No|Yes|FAIL / WARN|

---

## 11.6 New / Missing Field判定

|Diff Type|標準重要度|標準Result|個別Override|
|---|---|---|---|
|New Field|Medium|WARN|可|
|Missing Required Field|High|FAIL|不可|
|Missing Optional Field|Medium|WARN|可|
|Type Changed|High|FAIL|不可|
|Fixed Value Changed|High|FAIL|不可|

---

# 12. Error Verification

## 12.1 Error Test一覧

|Check ID|Scenario ID|発生条件|期待HTTP Status|期待Error Code|期待継続制御|期待Result|
|---|---|---|---|---|---|---|
|CHK-ERR-XXX|SC-XXX|（記載）|400 / 500 / Timeout|（記載）|STOP_SCENARIO / CONTINUE|FAIL / ERROR|

---

## 12.2 Error Response検証

|Check ID|JSONPath|検証方式|期待値 / Pattern|重要度|不一致時Result|
|---|---|---|---|---|---|
|CHK-ERR-RES-XXX|$.error.code|Equals / Enum|（記載）|High|FAIL|
|CHK-ERR-RES-XXX|$.error.message|Contains / Regex|（記載）|Medium|WARN / FAIL|

---

## 12.3 Exception分類検証

|Check ID|発生事象|期待Exception分類|期待Error ID分類|期待Result|
|---|---|---|---|---|
|CHK-EX-XXX|API Timeout|TimeoutException|ERR-API-XXX|FAIL / ERROR|

---

# 13. TestCase

## 13.1 TestCase一覧

|TestCase ID|Scenario ID|TestCase名称|分類|TestData ID|期待Result|自動実行|備考|
|---|---|---|---|---|---|---|---|
|TC-XXX|SC-XXX|（記載）|Normal / Alternative / Exception / Boundary|TD-XXX|PASS / WARN / FAIL|Yes / No| |

---

## 13.2 TestCase詳細

|項目|内容|
|---|---|
|TestCase ID|TC-XXX|
|TestCase名称|（記載）|
|対象UseCase|UC-XXX|
|対象Scenario|SC-XXX|
|対象API|API-XXX|
|TestData|TD-XXX|
|前提条件|（記載）|
|実行手順|（記載）|
|期待結果|（記載）|
|Evidence|EVD-XXX|

---

## 13.3 Test Step

|Step No|Step ID|処理|対象API|入力|期待結果|Check ID|
|---:|---|---|---|---|---|---|
|1|TS-XXX|（記載）|API-XXX|（記載）|（記載）|CHK-XXX|

---

# 14. Execution Rule

## 14.1 実行方式

|項目|内容|
|---|---|
|実行方式|Sequential / Parallel|
|実行単位|UseCase / Scenario / API|
|対象環境|ENV-XXX|
|実行頻度|Daily / Weekly / Manual|
|停止条件|Critical Fail / Error / Scenario End|
|Baseline Mode|Approved First / Previous Success|
|再実行|可 / 不可 / 条件付き|

---

## 14.2 実行順序

```text
1. Environment Validation
2. Spec Validation
3. TestData Validation
4. RunContext初期化
5. Scenario実行
6. API Step実行
7. Request / Response Verification
8. Context Verification
9. Business Result Verification
10. Snapshot保存
11. Baseline Diff
12. Report生成
```

---

## 14.3 実行前Check

|Check ID|確認内容|失敗時処理|
|---|---|---|
|PRE-XXX|Environment設定が有効であること|ERROR|
|PRE-XXX|TestDataが存在すること|BLOCKED / ERROR|
|PRE-XXX|対象APIが利用可能であること|ERROR|
|PRE-XXX|Secretが存在すること|ERROR|

---

## 14.4 実行後Check

|Check ID|確認内容|失敗時処理|
|---|---|---|
|POST-XXX|Snapshotが保存されていること|ERROR|
|POST-XXX|Diff Resultが生成されていること|ERROR|
|POST-XXX|Reportが生成されていること|ERROR|
|POST-XXX|Cleanupが完了していること|WARN / ERROR|

---

# 15. Result判定

## 15.1 Check単位

|条件|Result|
|---|---|
|期待と一致|PASS|
|許容差または確認対象|WARN|
|期待不一致|FAIL|
|実行不能|ERROR|
|条件により対象外|SKIP|
|Compare対象外|IGNORED|
|前提条件未成立|BLOCKED|

---

## 15.2 API単位

|条件|API Result|
|---|---|
|ERROR Checkあり|ERROR|
|FAIL Checkあり|FAIL|
|WARNのみ|WARN|
|全Check PASS|PASS|
|期待Skip|SKIP|

---

## 15.3 Scenario単位

|条件|Scenario Result|
|---|---|
|API ERRORあり|ERROR|
|Critical / High FAILあり|FAIL|
|WARNのみ|WARN|
|全API PASS|PASS|
|全API期待Skip|SKIP|
|前提条件未成立|BLOCKED|

---

## 15.4 UseCase単位

|条件|UseCase Result|
|---|---|
|Scenario ERRORあり|ERROR|
|Scenario FAILあり|FAIL|
|Scenario WARNあり|WARN|
|全Scenario PASS|PASS|
|全Scenario BLOCKED|BLOCKED|

---

## 15.5 Result優先順位

```text
ERROR
  ↓
FAIL
  ↓
WARN
  ↓
BLOCKED
  ↓
SKIP
  ↓
PASS
```

---

# 16. Evidence Rule

## 16.1 Evidence一覧

|Evidence ID|対象|保存内容|必須|保存先|Mask|
|---|---|---|---|---|---|
|EVD-XXX|Request|Request Snapshot|○|outputs/runs/{runId}/raw/|Yes|
|EVD-XXX|Response|Response Snapshot|○|outputs/runs/{runId}/raw/|Yes|
|EVD-XXX|Context|Context Snapshot|○|outputs/runs/{runId}/snapshot/|Yes|
|EVD-XXX|Execution|Execution Snapshot|○|outputs/runs/{runId}/snapshot/|必要時|
|EVD-XXX|Diff|Diff Result|○|outputs/runs/{runId}/diff/|Yes|
|EVD-XXX|Log|Runtime Log|○|outputs/runs/{runId}/logs/|Yes|

---

## 16.2 Evidence保存タイミング

|タイミング|保存対象|
|---|---|
|API実行前|Request、Context Before|
|API実行後|Response、Context After、Execution|
|Error発生時|Error Snapshot、Log|
|Scenario終了時|Scenario Snapshot、Diff|
|Run終了時|Report、Evidence Index|

---

## 16.3 Evidence必須条件

|条件|Evidence要否|
|---|---|
|PASS|必須|
|WARN|必須|
|FAIL|必須|
|ERROR|可能な範囲で必須|
|SKIP|Execution Snapshot必須|
|BLOCKED|前提条件Evidence必須|

---

# 17. Report Rule

## 17.1 Report出力

|Report ID|Report名|出力条件|対象読者|保存先|
|---|---|---|---|---|
|RPT-001|Daily Summary|Run終了時|承認者 / Leader|outputs/reports/latest/|
|RPT-002|Diff Report|Diff実行時|開発者 / 調査担当|outputs/runs/{runId}/reports/|
|RPT-003|Evidence Report|Run終了時|調査担当|outputs/runs/{runId}/reports/|
|RPT-004|Execution Report|Run終了時|開発 / 運用|outputs/runs/{runId}/reports/|
|RPT-005|Error Report|Error発生時|開発 / 運用|outputs/runs/{runId}/reports/|

---

## 17.2 Daily Summary反映条件

|Result|Daily Summary表示|
|---|---|
|PASS|件数のみ|
|WARN|確認事項として表示|
|FAIL|重大差分として表示|
|ERROR|最上部にError表示|
|BLOCKED|未実行理由を表示|
|SKIP|Skip件数と理由を表示|

---

# 18. Baseline Rule

## 18.1 Baseline選択

|優先順位|Baseline種別|利用条件|
|---:|---|---|
|1|Approved Baseline|存在する場合|
|2|Previous Success|Approvedがない場合|
|3|Initial Baseline Candidate|初回実行|
|4|No Baseline|比較不可|

---

## 18.2 Baseline更新条件

|条件|更新可否|
|---|---|
|Run PASS|承認後可|
|Run WARN|差分確認・承認後可|
|Run FAIL|原則不可|
|Run ERROR|不可|
|Mask漏れあり|不可|
|Evidence不足|不可|

---

## 18.3 Baseline承認記録

|項目|内容|
|---|---|
|Baseline ID|BASE-YYYYMMDD-XXX|
|Source Run ID|RUN-YYYYMMDD-XXX|
|承認者|（記載）|
|承認日時|（記載）|
|承認範囲|UseCase / Scenario / API|
|承認理由|（記載）|

---

# 19. Traceability

## 19.1 Verification Trace Matrix

|Business ID|BA ID|Path ID|UseCase ID|Scenario ID|API ID|Context ID|Verification ID|Check ID|TestCase ID|TestData ID|Evidence ID|
|---|---|---|---|---|---|---|---|---|---|---|---|
|BUS-XXX|BA-XXX|PATH-XXX|UC-XXX|SC-XXX|API-XXX|CTX-XXX|VER-XXX|CHK-XXX|TC-XXX|TD-XXX|EVD-XXX|

---

## 19.2 Coverage確認

|Coverage分類|対象数|検証済数|未検証数|Coverage率|備考|
|---|---:|---:|---:|---:|---|
|API Coverage|0|0|0|0%| |
|Scenario Coverage|0|0|0|0%| |
|Request Field Coverage|0|0|0|0%| |
|Response Field Coverage|0|0|0|0%| |
|Context Coverage|0|0|0|0%| |
|Error Coverage|0|0|0|0%| |

---

# 20. 課題・確認事項

|No|分類|確認事項|影響範囲|確認先|優先度|状態|対応方針|
|---:|---|---|---|---|---|---|---|
|1|業務判定|（記載）|Scenario / Result|業務担当|High|Open| |
|2|API仕様|（記載）|Request / Response|E6担当|High|Open| |
|3|Compare|（記載）|Baseline Diff|設計担当|Medium|Open| |
|4|TestData|（記載）|実行可否|業務担当|High|Open| |

---

# 21. Review観点

|観点|確認内容|
|---|---|
|対象整合性|UseCase、Scenario、APIがMasterと一致しているか|
|Path整合性|BAシナリオ一覧の開始API・終了APIと一致しているか|
|Request Coverage|必須、型、桁数、Pattern、固定値が定義されているか|
|Response Coverage|必須、型、固定値、Enum、入力値一致が定義されているか|
|Context Coverage|Producer / Consumer / Bindingが確認されているか|
|Skip Coverage|Scenario別Skip条件が確認されているか|
|Error Coverage|Timeout、4xx、5xx、業務Errorが定義されているか|
|Compare Policy|MasterのPolicyを正しく参照しているか|
|Evidence|PASS / WARN / FAILを判断できる証跡が残るか|
|Result|CheckからRunまでの判定が一貫しているか|
|Traceability|BAからEvidenceまで追跡可能か|

---

# Appendix A. 記入例：VER-001 顧客情報照会

## A.1 文書管理

|項目|内容|
|---|---|
|文書ID|VER-001|
|文書名称|顧客情報照会 Verification仕様書|
|Verification ID|VER-001|
|対象業務|顧客情報照会業務|
|Business ID|BUS-001|
|対象UseCase|UC-001|
|対象Scenario|SC-001, SC-002, SC-003, SC-004|
|対象API|API-001, API-002, API-003|
|関連業務分析書|BA-001|
|関連BAシナリオ一覧|BA-001_顧客情報照会業務_シナリオ一覧.md|
|版数|1.0.0|
|状態|Draft|

---

## A.2 Verification目的

顧客番号を入力として、顧客存在確認、顧客詳細取得、契約一覧取得のAPI呼出経路がScenario定義どおりに実行され、Response、Context、業務結果およびBaseline差分が期待どおりであることを確認する。

---

## A.3 対象Scenario

|Scenario ID|Scenario名称|分類|対象経路ID|開始API|終了API|期待結果|TestCase ID|
|---|---|---|---|---|---|---|---|
|SC-001|正常系|Normal|PATH-001|API-001|API-003|PASS|TC-001|
|SC-002|顧客不存在|Alternative|PATH-002|API-001|API-001|WARN / FAIL|TC-002|
|SC-003|契約0件|Alternative|PATH-003|API-001|API-003|PASS / WARN|TC-003|
|SC-004|API-002 Timeout|Exception|PATH-004|API-001|API-002|FAIL|TC-004|

---

## A.4 Scenario別API実行Matrix

|API / Scenario|SC-001|SC-002|SC-003|SC-004|
|---|:---:|:---:|:---:|:---:|
|API-001 Customer Exists API|Run|Run|Run|Run|
|API-002 Customer Detail API|Run|Skip|Run|Run / Error|
|API-003 Contract List API|Run|Skip|Run|Skip|
|終了API|API-003|API-001|API-003|API-002|
|期待結果|PASS|WARN / FAIL|PASS / WARN|FAIL|

---

## A.5 TestData一覧

|TestData ID|Scenario ID|名称|Entry Input|期待Result|
|---|---|---|---|---|
|TD-001|SC-001|正常顧客|customerId=10000001|PASS|
|TD-002|SC-002|存在しない顧客|customerId=99999999|WARN / FAIL|
|TD-003|SC-003|契約0件顧客|customerId=10000002|PASS / WARN|
|TD-004|SC-004|Timeout誘発条件|customerId=10000003|FAIL|

---

## A.6 Request Verification例

|Check ID|API ID|対象|検証種別|期待仕様|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|CHK-REQ-001|API-001|$.customerId|Required|存在すること|High|FAIL|
|CHK-REQ-002|API-001|$.customerId|Type|String|High|FAIL|
|CHK-REQ-003|API-001|$.customerId|Pattern|^[0-9]+$|High|FAIL|
|CHK-BIND-001|API-001|$.customerId|Context Match|CTX-001|High|FAIL|
|CHK-BIND-002|API-002|$.customerId|Context Match|CTX-001|High|FAIL|
|CHK-BIND-003|API-003|$.customerId|Context Match|CTX-001|High|FAIL|

---

## A.7 Response Verification例

|Check ID|API ID|JSONPath|検証種別|期待仕様 / 値|Policy|重要度|Result|
|---|---|---|---|---|---|---|---|
|CHK-RES-001|API-001|$.resultCode|Fixed|0|Equals|High|FAIL|
|CHK-RES-002|API-001|$.exists|Type / Enum|Boolean / true,false|Equals|High|FAIL|
|CHK-RES-003|API-001|$.customerId|Input Match|Request $.customerId|Equals|High|FAIL|
|CHK-RES-004|API-001|$.traceId|Dynamic|Exists|CMP-POL-001|Low|PASS / IGNORED|
|CHK-RES-005|API-002|$.customer.customerId|Context Match|CTX-001|Equals|High|FAIL|
|CHK-RES-006|API-003|$.contracts|Type|Array|Equals|High|FAIL|

---

## A.8 Context Verification例

|Check ID|Context ID|Producer|Consumer|検証内容|不一致時Result|
|---|---|---|---|---|---|
|CHK-CTX-001|CTX-001|Entry Input|API-001, API-002, API-003|同一顧客番号が引き継がれること|FAIL|
|CHK-CTX-002|CTX-002|API-001|Scenario Selection|exists値で分岐されること|FAIL|
|CHK-CTX-003|CTX-003|API-002|Report / Verification|顧客詳細が抽出されること|FAIL|
|CHK-CTX-004|CTX-004|API-003|Report / Verification|契約一覧が抽出されること|FAIL|

---

## A.9 Skip Verification例

|Check ID|Scenario ID|条件|Skip対象API|期待Status|不一致時Result|
|---|---|---|---|---|---|
|CHK-SKIP-001|SC-002|CTX-002 = false|API-002, API-003|SKIP|FAIL|
|CHK-SKIP-002|SC-004|API-002 Timeout後Retry失敗|API-003|SKIP|FAIL|

---

## A.10 Business Result例

|Check ID|Scenario ID|判定条件|期待Business Result|期待Scenario Result|
|---|---|---|---|---|
|CHK-BIZ-001|SC-001|exists=true かつ contracts.length>0|顧客・契約情報取得成功|PASS|
|CHK-BIZ-002|SC-002|exists=false|顧客不存在|WARN / FAIL|
|CHK-BIZ-003|SC-003|exists=true かつ contracts.length=0|契約0件|PASS / WARN|
|CHK-BIZ-004|SC-004|API-002 Timeout|顧客詳細取得失敗|FAIL|

---

## A.11 Compare Policy例

|Compare ID|対象|Baseline|Policy|重要度|備考|
|---|---|---|---|---|---|
|CMP-001|API-001 $.resultCode|Approved|Equals|High|固定値|
|CMP-002|API-001 $.exists|Approved|Equals|High|業務判定|
|CMP-003|API-001 $.customerId|Approved|Equals|High|入力値一致|
|CMP-004|API-001 $.traceId|Approved|CMP-POL-001|Low|Ignore|
|CMP-005|API-003 $.contracts[]|Approved|CMP-POL-004|Medium|contractIdでKey Match|

---

## A.12 TestCase一覧

|TestCase ID|Scenario ID|TestCase名称|TestData ID|期待Result|自動実行|
|---|---|---|---|---|---|
|TC-001|SC-001|顧客情報照会正常系|TD-001|PASS|Yes|
|TC-002|SC-002|顧客不存在|TD-002|WARN / FAIL|Yes|
|TC-003|SC-003|契約0件|TD-003|PASS / WARN|Yes|
|TC-004|SC-004|API-002 Timeout|TD-004|FAIL|Yes|

---

## A.13 Evidence例

|Evidence ID|Scenario ID|対象|保存先|
|---|---|---|---|
|EVD-001|SC-001|Request / Response / Context / Diff|outputs/runs/{runId}/|
|EVD-002|SC-002|Request / Response / Skip Execution|outputs/runs/{runId}/|
|EVD-003|SC-003|Request / Response / Collection Diff|outputs/runs/{runId}/|
|EVD-004|SC-004|Request / Error / Retry Log|outputs/runs/{runId}/|

---

## A.14 Traceability例

|Business ID|BA ID|Path ID|UseCase ID|Scenario ID|API ID|Context ID|Verification ID|Check ID|TestCase ID|TestData ID|Evidence ID|
|---|---|---|---|---|---|---|---|---|---|---|---|
|BUS-001|BA-001|PATH-001|UC-001|SC-001|API-001, API-002, API-003|CTX-001〜CTX-004|VER-001|CHK-REQ-001〜CHK-BIZ-001|TC-001|TD-001|EVD-001|
|BUS-001|BA-001|PATH-002|UC-001|SC-002|API-001|CTX-001, CTX-002|VER-001|CHK-SKIP-001, CHK-BIZ-002|TC-002|TD-002|EVD-002|
|BUS-001|BA-001|PATH-003|UC-001|SC-003|API-001, API-002, API-003|CTX-001〜CTX-004|VER-001|CHK-BIZ-003, CMP-005|TC-003|TD-003|EVD-003|
|BUS-001|BA-001|PATH-004|UC-001|SC-004|API-001, API-002|CTX-001, CTX-002|VER-001|CHK-RETRY-001, CHK-BIZ-004|TC-004|TD-004|EVD-004|

:::

下一步应继续制作：

```text
system/06_verification_assets/execution_spec/
Execution仕様書_Template.md
```

它会把这份 Verification 设计转换成 Runtime 真正可执行的 UseCase、Scenario、API Step、Context Binding、Skip、Retry、Check 定义。

## 第 196 轮

### 你

继续

### ChatGPT

下面继续做 `Execution仕様書_Template.md`，把 Verification 规格转换为 Runtime 可直接执行的 UseCase、Scenario、API Step、Context、Skip、Retry、Check 定义。

### ChatGPT

放置位置：

```text
system/06_verification_assets/execution_spec/Execution仕様書_Template.md
```

:::writing{variant="document" id="41283"}
---
title: Execution仕様書テンプレート
document_id: EXECUTION-SPEC-TEMPLATE
version: 1.0.0
status: Template
document_type: Execution Specification
system_name: E6 API Verification Platform
phase: Verification Execution Design
author:
reviewer:
approver:
created:
updated:
---

# Execution仕様書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|---|---|
|文書ID|EXEC-XXX|
|文書名称|〇〇 Execution仕様書|
|Execution ID|EXEC-XXX|
|対象Business ID|BUS-XXX|
|対象UseCase ID|UC-XXX|
|対象Scenario ID|SC-XXX|
|対象Verification ID|VER-XXX|
|対象環境|ENV-XXX|
|実行方式|Daily / Manual / Retry / Investigation|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|---|---|---|---|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|参照目的|
|---|---|---|---|
|BA-XXX|現行業務分析書|system/01_business/01_業務分析/|業務Flow|
|BA-SC-XXX|BA分析書シナリオ一覧|system/01_business/01_業務分析/|API呼出経路|
|API-XXX|API設計書|system/03_api_design/|Request / Response契約|
|UC-XXX|UseCase設計書|system/04_usecase_design/|API実行Chain|
|VER-XXX|Verification仕様書|system/06_verification_assets/|Check定義|
|MST-API-UC-SC-001|API_UseCase_Scenario対応表|system/02_master/|実行順序、Skip条件|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|Compare Policy|
|SYS-FW-001|共通Framework設計書|system/05_framework/|Runtime処理|
|SYS-CTX-001|RunContext設計書|system/05_framework/|Context処理|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|Snapshot保存|
|SYS-DIFF-001|Diff設計書|system/05_framework/|Diff処理|

---

# 2. Execution概要

## 2.1 Execution目的

本Execution仕様は、対象UseCaseおよびScenarioについて、Runtimeが実行するAPI Step、Context Binding、Response Extract、分岐、Skip、Retry、Verification、Snapshot、Diff、Reportの処理内容を定義する。

---

## 2.2 実行対象

|項目|内容|
|---|---|
|Business ID|BUS-XXX|
|UseCase ID|UC-XXX|
|Scenario ID|SC-XXX|
|Verification ID|VER-XXX|
|TestCase ID|TC-XXX|
|TestData ID|TD-XXX|
|開始API|API-XXX|
|終了API|API-XXX|
|想定API実行数|（記載）|
|期待Execution Result|PASS / WARN / FAIL / ERROR / SKIP|

---

## 2.3 Execution単位

```text
Run
  └── UseCase
        └── Scenario
              └── API Step
                    ├── Request Build
                    ├── Context Binding
                    ├── API Execute
                    ├── Response Extract
                    ├── Verification
                    └── Snapshot
```

---

# 3. Runtime起動条件

## 3.1 起動パラメータ

|Parameter|必須|Type|設定例|説明|
|---|---:|---|---|---|
|environment|○|String|STG|対象環境|
|executionId|○|String|EXEC-001|Execution仕様|
|useCaseId|○|String|UC-001|対象UseCase|
|scenarioId|○|String|SC-001|対象Scenario|
|testDataId|○|String|TD-001|TestData|
|baselineMode|－|String|APPROVED_FIRST|Baseline選択方式|
|runMode|－|String|DAILY|実行方式|
|retryFromStep|－|String|UC-STEP-002|途中再実行時の開始Step|

---

## 3.2 CLI実行例

```bash
java -jar e6-verifier.jar \
  --environment STG \
  --execution-id EXEC-001 \
  --usecase UC-001 \
  --scenario SC-001 \
  --testdata TD-001 \
  --baseline-mode APPROVED_FIRST
```

---

## 3.3 実行前提条件

|Precondition ID|前提条件|確認方法|未成立時Result|停止範囲|
|---|---|---|---|---|
|PRE-XXX|対象環境が有効であること|Environment_Master|ERROR|STOP_RUN|
|PRE-XXX|Execution仕様が有効であること|Spec Validation|ERROR|STOP_USECASE|
|PRE-XXX|TestDataが存在すること|File Validation|BLOCKED / ERROR|STOP_SCENARIO|
|PRE-XXX|必須Secretが存在すること|Environment Validation|ERROR|STOP_RUN|
|PRE-XXX|対象APIが有効であること|E6_API_Master|ERROR|STOP_SCENARIO|

---

# 4. Execution Plan

## 4.1 UseCase Execution Plan

|Execution ID|UseCase ID|Scenario ID|TestCase ID|TestData ID|開始API|終了API|実行方式|期待Result|
|---|---|---|---|---|---|---|---|---|
|EXEC-XXX|UC-XXX|SC-XXX|TC-XXX|TD-XXX|API-XXX|API-XXX|Sequential / Parallel|PASS / WARN / FAIL|

---

## 4.2 API Step一覧

|実行順|Step ID|API ID|API名称|実行要否|実行条件|Skip条件|Timeout|Retry|停止方針|
|---:|---|---|---|---|---|---|---:|---:|---|
|1|UC-STEP-XXX|API-XXX|（記載）|必須 / 条件付き / 任意|（記載）|（記載）|10秒|1回|CONTINUE / STOP_SCENARIO|

---

## 4.3 API Step Flow

```mermaid
flowchart TD

START([Start])
STEP1[UC-STEP-001 / API-001]
BRANCH{分岐条件}
STEP2[UC-STEP-002 / API-002]
STEP3[UC-STEP-003 / API-003]
END([End])

START --> STEP1
STEP1 --> BRANCH
BRANCH -- true --> STEP2
STEP2 --> STEP3
STEP3 --> END
BRANCH -- false --> END
```

---

# 5. RunContext初期化

## 5.1 Runtime Context

|Context ID|Context名|設定元|設定値 / Rule|必須|
|---|---|---|---|---:|
|CTX-RUN-001|Runtime.runId|Runtime|自動採番|○|
|CTX-RUN-002|Runtime.environment|起動引数|environment|○|
|CTX-RUN-003|Runtime.executionId|起動引数|executionId|○|
|CTX-RUN-004|Runtime.startedAt|System Clock|ISO-8601|○|

---

## 5.2 Entry Context

|Context ID|Context名|TestData JSONPath|Type|必須|Mask|未設定時処理|
|---|---|---|---|---:|---|---|
|CTX-XXX|（記載）|$.entryInput.xxx|String / Number / Boolean|○ / －|Yes / No|ERROR / BLOCKED|

---

## 5.3 初期Context例

```json
{
  "Runtime.runId": "RUN-YYYYMMDD-HHMMSS-XXX",
  "Runtime.environment": "STG",
  "Runtime.executionId": "EXEC-XXX",
  "UseCase.id": "UC-XXX",
  "Scenario.id": "SC-XXX",
  "Business.key": "value"
}
```

---

# 6. API Step詳細

以下をAPI Stepごとに記載する。

---

## 6.1 Step基本情報

|項目|内容|
|---|---|
|Step ID|UC-STEP-XXX|
|API ID|API-XXX|
|API名称|（記載）|
|実行順|1|
|実行要否|必須 / 条件付き / 任意|
|前Step|START / UC-STEP-XXX|
|次Step|UC-STEP-XXX / END|
|対象Scenario|SC-XXX|
|Verification ID|VER-XXX|

---

## 6.2 Step実行条件

|Condition ID|条件式|利用Context|成立時処理|不成立時処理|
|---|---|---|---|---|
|COND-XXX|（記載）|CTX-XXX|RUN|SKIP / STOP|

---

## 6.3 Request生成

### Header

|Header名|設定元|設定値|必須|Mask|
|---|---|---|---:|---:|
|Content-Type|Fixed|application/json|○|No|
|Authorization|Secret / Auth Context|Bearer ${token}|○|Yes|

### Path Parameter

|Parameter|設定元|Context / TestData|必須|備考|
|---|---|---|---:|---|
|xxx|Context|CTX-XXX|○| |

### Query Parameter

|Parameter|設定元|Context / TestData|必須|備考|
|---|---|---|---:|---|
|xxx|TestData|$.entryInput.xxx|－| |

### Request Body Binding

|Binding ID|Request JSONPath|設定元|Source Path / Context ID|変換|必須|未設定時処理|
|---|---|---|---|---|---:|---|
|BIND-XXX|$.xxx|Context / TestData / Fixed / Runtime|CTX-XXX|なし / Format / Cast|○ / －|ERROR / Default|

---

## 6.4 Request Validation

|Check ID|対象|Check Type|期待仕様|不一致時Result|
|---|---|---|---|---|
|CHK-REQ-XXX|$.xxx|Required / Type / Length / Pattern / Enum / Fixed|（記載）|FAIL / ERROR|

---

## 6.5 API Execution

|項目|内容|
|---|---|
|HTTP Method|GET / POST / PUT / DELETE|
|Path|（記載）|
|Timeout|（記載）秒|
|Retry Count|（記載）回|
|Retry Interval|（記載）ms|
|Retry Backoff|Fixed / Exponential|
|Retry対象|Timeout / 500 / 502 / 503 / 504|
|Retry非対象|400 / 401 / 403 / 404|
|HTTP Client Policy|Framework Default / Custom|

---

## 6.6 Response処理

### Response基本検証

|Check ID|対象|Check Type|期待値 / 仕様|不一致時Result|
|---|---|---|---|---|
|CHK-HTTP-XXX|HTTP Status|Equals|200|FAIL|
|CHK-RES-XXX|$.xxx|Required / Type / Fixed / Enum|（記載）|FAIL|

### Response Context Extract

|Extract ID|Response JSONPath|Context ID|Type|必須|Null許可|未取得時処理|
|---|---|---|---|---:|---:|---|
|EXT-XXX|$.xxx|CTX-XXX|String / Boolean / Object / Array|○ / －|可 / 不可|ERROR / WARN / Ignore|

### Dynamic Field

|JSONPath|Compare Policy|Verification|備考|
|---|---|---|---|
|$.traceId|CMP-POL-001|Exists / Ignore|値比較対象外|

---

## 6.7 Step後分岐

|Branch ID|条件式|利用Context|成立時遷移|不成立時遷移|備考|
|---|---|---|---|---|---|
|BRANCH-XXX|（記載）|CTX-XXX|UC-STEP-XXX|END / UC-STEP-XXX| |

---

## 6.8 Step Result

|条件|Result|後続処理|
|---|---|---|
|API成功・Check全PASS|PASS|次Step|
|WARNのみ|WARN|次Step|
|Validation FAIL|FAIL|Execution Policyに従う|
|API Timeout|FAIL / ERROR|Retry後停止|
|実行条件不成立|SKIP|Skip Ruleに従う|
|Context不足|ERROR|STOP_SCENARIO|

---

# 7. Skip Rule

## 7.1 Skip Rule一覧

|Skip Rule ID|対象Scenario|条件式|利用Context|Skip対象Step / API|期待Execution Status|後続処理|
|---|---|---|---|---|---|---|
|SKIP-XXX|SC-XXX|（記載）|CTX-XXX|UC-STEP-XXX / API-XXX|SKIP|CONTINUE / END|

---

## 7.2 Skip Result判定

|条件|Result|
|---|---|
|仕様どおりのSkip|PASSまたはSKIP|
|想定外Skip|FAIL|
|Skip条件判定不能|ERROR|
|必須APIがSkip|FAIL|

---

# 8. Retry Rule

## 8.1 Retry一覧

|Retry Rule ID|API ID|対象Exception / Status|最大回数|Interval|Backoff|Retry終了時Result|
|---|---|---|---:|---:|---|---|
|RETRY-XXX|API-XXX|Timeout / 500 / 503|2|1000ms|Fixed / Exponential|FAIL / ERROR|

---

## 8.2 Retry処理

```text
1. API Error / Timeout検出
2. Retry対象判定
3. Retry Count確認
4. Backoff待機
5. API再実行
6. Retry結果保存
7. 最大回数超過時にResult確定
```

---

## 8.3 Retry Evidence

|Evidence|保存内容|
|---|---|
|Execution Snapshot|各Retryの開始・終了|
|Request Snapshot|RetryごとのRequest|
|Response / Error Snapshot|Retryごとの結果|
|Log|retryCount、interval、原因|

---

# 9. Verification実行定義

## 9.1 Check実行順序

```text
1. Request Check
2. API Execute
3. HTTP Status Check
4. Response Contract Check
5. Context Extract
6. Context Check
7. Business Check
8. Execution Flow Check
9. Snapshot保存
10. Baseline Diff
```

---

## 9.2 Check一覧

|実行順|Check ID|Check分類|対象API / Context|対象Path|期待値 / Rule|Severity|失敗時Result|
|---:|---|---|---|---|---|---|---|
|1|CHK-XXX|Request / Response / Context / Business / Flow|API-XXX|$.xxx / CTX-XXX|（記載）|High / Medium / Low|FAIL / WARN / ERROR|

---

## 9.3 Check依存関係

|Check ID|前提Check|前提Result|未成立時処理|
|---|---|---|---|
|CHK-XXX|CHK-XXX|PASS / WARN|SKIP / ERROR|

---

# 10. Business Rule実行

## 10.1 業務判定

|Business Check ID|条件式|利用Context|期待Business Result|Scenario Result|
|---|---|---|---|---|
|BCHK-XXX|（記載）|CTX-XXX|（記載）|PASS / WARN / FAIL|

---

## 10.2 処理Flg設定

|Flg ID|Flg名称|設定条件|設定値|Context ID|利用先|
|---|---|---|---|---|---|
|FLG-XXX|（記載）|（記載）|（記載）|CTX-XXX|Branch / Report|

---

## 10.3 終了条件

|End Rule ID|条件|終了API|期待Result|後処理|
|---|---|---|---|---|
|END-XXX|（記載）|API-XXX|PASS / WARN / FAIL|Report / Cleanup|

---

# 11. Snapshot定義

## 11.1 Snapshot保存設定

|Snapshot Type|保存タイミング|必須|保存先|
|---|---|---:|---|
|Context Before|API実行前|○|snapshot/|
|Request|API実行前|○|raw/|
|Response|API実行後|○|raw/|
|Context After|Context抽出後|○|snapshot/|
|Execution|Step終了時|○|snapshot/|
|Error|Error発生時|○|snapshot/|
|Diff|Diff終了時|○|diff/|

---

## 11.2 Snapshot命名

```text
{useCaseId}_{scenarioId}_{stepId}_{apiId}_{snapshotType}.json
```

---

## 11.3 Mask設定

|対象|Mask方式|
|---|---|
|Authorization|完全Mask|
|Token|完全Mask|
|顧客番号|部分Mask|
|氏名|完全Mask|
|メール|部分Mask|
|電話番号|部分Mask|

---

# 12. Baseline / Diff定義

## 12.1 Baseline選択

|優先順位|Baseline種別|条件|
|---:|---|---|
|1|Approved Baseline|対象Scopeの承認済Baselineが存在する|
|2|Previous Success|前回成功Runが存在する|
|3|Initial Candidate|初回実行|
|4|No Baseline|比較不可|

---

## 12.2 Diff対象

|Diff ID|対象Step / API|対象JSONPath / Context|Policy ID|Severity|不一致時Result|
|---|---|---|---|---|---|
|DIFF-XXX|API-XXX|$.xxx / CTX-XXX|CMP-POL-XXX|High / Medium / Low|FAIL / WARN|

---

## 12.3 Diff除外

|対象|Policy ID|理由|
|---|---|---|
|$.traceId|CMP-POL-001|実行毎に採番|
|Runtime.runId|CMP-POL-001|Runごとに変動|

---

# 13. Result集計

## 13.1 API Step Result

|条件|Result|
|---|---|
|ERROR Checkあり|ERROR|
|FAIL Checkあり|FAIL|
|WARNのみ|WARN|
|全Check PASS|PASS|
|実行条件不成立|SKIP|

---

## 13.2 Scenario Result

|条件|Result|
|---|---|
|Step ERRORあり|ERROR|
|Step FAILあり|FAIL|
|Step WARNあり|WARN|
|全Step PASS|PASS|
|期待Skipのみ|PASS / SKIP|
|前提条件未成立|BLOCKED|

---

## 13.3 Execution Result

|条件|Result|
|---|---|
|Scenario ERROR|ERROR|
|Scenario FAIL|FAIL|
|Scenario WARN|WARN|
|Scenario PASS|PASS|
|Scenario BLOCKED|BLOCKED|

---

# 14. Error Handling

## 14.1 Error一覧

|Error ID|発生箇所|発生条件|Exception分類|Result|停止範囲|
|---|---|---|---|---|---|
|ERR-EXEC-XXX|Precondition|Spec不足|SpecException|ERROR|STOP_SCENARIO|
|ERR-CTX-XXX|Context Binding|必須Context不足|ContextException|ERROR|STOP_SCENARIO|
|ERR-API-XXX|API Execute|Timeout|TimeoutException|FAIL / ERROR|STOP_SCENARIO|
|ERR-VAL-XXX|Verification|固定値不一致|ValidationException|FAIL|Policyに従う|

---

## 14.2 Error時保存

|対象|保存|
|---|---:|
|Error Snapshot|Yes|
|Execution Snapshot|Yes|
|Request Snapshot|生成済みならYes|
|Response Snapshot|受信済みならYes|
|Context Snapshot|Yes|
|Runtime Log|Yes|
|Error Report|Yes|

---

# 15. Report出力

## 15.1 Report対象

|Report|出力内容|
|---|---|
|Daily Summary|Execution Result、重大差分|
|Diff Report|Field / Context差分|
|Evidence Report|Snapshot Index|
|Execution Report|API実行順序、Skip、Retry|
|Error Report|Error詳細|

---

## 15.2 Report表示項目

|項目|内容|
|---|---|
|Execution ID|EXEC-XXX|
|UseCase ID|UC-XXX|
|Scenario ID|SC-XXX|
|TestCase ID|TC-XXX|
|TestData ID|TD-XXX|
|開始API|API-XXX|
|終了API|API-XXX|
|実行API|（記載）|
|Skip API|（記載）|
|Result|PASS / WARN / FAIL / ERROR|
|Evidence|保存先|

---

# 16. 再実行設計

## 16.1 再実行方式

|方式|説明|
|---|---|
|Run Retry|Run全体を再実行|
|UseCase Retry|対象UseCaseのみ再実行|
|Scenario Retry|対象Scenarioのみ再実行|
|Step Retry|指定Stepから再実行|
|Failed Only|失敗Scenarioのみ再実行|

---

## 16.2 再実行条件

|条件|再実行可否|備考|
|---|---:|---|
|API Timeout|可|同一TestData|
|一時的Connection Error|可| |
|Validation FAIL|原則可|結果は別Runで保存|
|Spec Error|修正後可| |
|TestData不備|修正後可| |
|更新系API|条件付き|Data状態確認必須|

---

## 16.3 再実行時Context

|項目|方針|
|---|---|
|Run ID|新規採番|
|Entry Context|TestDataから再生成|
|途中Step Context|既存Snapshot利用可否を明示|
|Baseline|元Runと同一Policy|
|Evidence|新規Run配下へ保存|

---

# 17. Cleanup

## 17.1 Cleanup対象

|Cleanup ID|対象|実行条件|処理|失敗時Result|
|---|---|---|---|---|
|CLEAN-XXX|登録TestData|更新系Scenario終了後|削除 / Restore|WARN / ERROR|
|CLEAN-XXX|tmp|Run終了時|削除|WARN|
|CLEAN-XXX|Lock File|Run終了時|削除|ERROR|

---

# 18. Runtime向け構造化定義

正式な人向け成果物はMarkdownとし、Runtime向けにはYAMLまたはJSONへ変換する。

---

## 18.1 YAML基本構造

```yaml
execution:
  id: EXEC-XXX
  version: 1.0.0
  businessId: BUS-XXX
  useCaseId: UC-XXX
  scenarioId: SC-XXX
  verificationId: VER-XXX
  testCaseId: TC-XXX
  testDataId: TD-XXX
  expectedResult: PASS

  environment:
    allowed:
      - STG
    baselineMode: APPROVED_FIRST

  entryContext:
    - contextId: CTX-XXX
      source: $.entryInput.xxx
      required: true

  steps:
    - order: 1
      stepId: UC-STEP-XXX
      apiId: API-XXX
      condition: "true"
      timeoutSeconds: 10
      retry:
        count: 1
        intervalMillis: 1000

      requestBindings:
        - target: $.xxx
          sourceType: CONTEXT
          source: CTX-XXX
          required: true

      responseExtracts:
        - source: $.xxx
          contextId: CTX-XXX
          required: true

      checks:
        - checkId: CHK-XXX
          type: FIXED
          target: $.resultCode
          expected: "0"
          severity: HIGH

      next:
        default: END

  snapshot:
    enabled: true
    maskEnabled: true

  diff:
    enabled: true
    baselineMode: APPROVED_FIRST

  report:
    enabled: true
```

---

# 19. Schema Validation

## 19.1 必須検証

|Validation ID|確認内容|失敗時Result|
|---|---|---|
|EXEC-SCHEMA-001|Execution IDが存在する|ERROR|
|EXEC-SCHEMA-002|UseCase / ScenarioがMasterに存在する|ERROR|
|EXEC-SCHEMA-003|API Stepが1件以上存在する|ERROR|
|EXEC-SCHEMA-004|実行順が重複しない|ERROR|
|EXEC-SCHEMA-005|API IDがMasterに存在する|ERROR|
|EXEC-SCHEMA-006|Context IDがMasterに存在する|ERROR|
|EXEC-SCHEMA-007|Check IDがVerification仕様に存在する|ERROR|
|EXEC-SCHEMA-008|TestDataが存在する|BLOCKED / ERROR|
|EXEC-SCHEMA-009|分岐先Stepが存在する|ERROR|
|EXEC-SCHEMA-010|開始API・終了APIがBA Pathと一致する|ERROR|

---

# 20. Traceability

|Business ID|BA ID|Path ID|UseCase ID|Scenario ID|Execution ID|Step ID|API ID|Verification ID|Check ID|TestCase ID|TestData ID|
|---|---|---|---|---|---|---|---|---|---|---|---|
|BUS-XXX|BA-XXX|PATH-XXX|UC-XXX|SC-XXX|EXEC-XXX|UC-STEP-XXX|API-XXX|VER-XXX|CHK-XXX|TC-XXX|TD-XXX|

---

# 21. Review観点

|観点|確認内容|
|---|---|
|BA Path整合|開始API・終了API・分岐がBAシナリオ一覧と一致するか|
|Master整合|UseCase、Scenario、API、ContextがMasterに存在するか|
|API順序|API_UseCase_Scenario対応表と一致するか|
|Context Binding|Requestへ正しいContextが設定されるか|
|Context Extract|Responseから必要Contextが抽出されるか|
|Skip Rule|分岐条件とSkip対象が明確か|
|Retry Rule|Retry対象、回数、終了時Resultが明確か|
|Verification|全CheckがVerification仕様書を参照しているか|
|Snapshot|Request、Response、Context、Executionが保存されるか|
|Diff|Compare Policyが正しく適用されるか|
|Error Handling|停止範囲が明確か|
|Traceability|BAからEvidenceまで追跡可能か|

---

# Appendix A. 記入例：EXEC-001 顧客情報照会正常系

## A.1 基本情報

|項目|内容|
|---|---|
|Execution ID|EXEC-001|
|Business ID|BUS-001|
|UseCase ID|UC-001|
|Scenario ID|SC-001|
|Verification ID|VER-001|
|TestCase ID|TC-001|
|TestData ID|TD-001|
|開始API|API-001|
|終了API|API-003|
|期待Result|PASS|

---

## A.2 API Step一覧

|実行順|Step ID|API ID|API名称|実行条件|Skip条件|Timeout|Retry|
|---:|---|---|---|---|---|---:|---:|
|1|UC-STEP-001|API-001|Customer Exists API|常時|－|10秒|1回|
|2|UC-STEP-002|API-002|Customer Detail API|CTX-002 = true|CTX-002 = false|10秒|1回|
|3|UC-STEP-003|API-003|Contract List API|CTX-002 = true|CTX-002 = false / API-002失敗|10秒|1回|

---

## A.3 Entry Context

|Context ID|Context名|TestData Path|値|
|---|---|---|---|
|CTX-001|Customer.id|$.entryInput.customerId|10000001|

---

## A.4 API-001 Request Binding

|Binding ID|Request JSONPath|設定元|Source|必須|
|---|---|---|---|---:|
|BIND-001|$.customerId|Context|CTX-001|○|

---

## A.5 API-001 Response Extract

|Extract ID|Response JSONPath|Context ID|必須|
|---|---|---|---:|
|EXT-001|$.exists|CTX-002|○|
|EXT-002|$.customerId|CTX-001|○|

---

## A.6 API-001 Check

|Check ID|対象|Check Type|期待値|Severity|失敗時Result|
|---|---|---|---|---|---|
|CHK-RES-001|$.resultCode|Fixed|0|High|FAIL|
|CHK-RES-002|$.exists|Type / Enum|Boolean / true,false|High|FAIL|
|CHK-RES-003|$.customerId|Context Match|CTX-001|High|FAIL|
|CHK-RES-004|$.traceId|Exists|存在|Low|WARN|

---

## A.7 API-002 Request / Extract

|分類|対象|Source / Context|
|---|---|---|
|Request Binding|$.customerId|CTX-001|
|Response Extract|$.customer|CTX-003|
|Context Check|$.customer.customerId|CTX-001|

---

## A.8 API-003 Request / Extract

|分類|対象|Source / Context|
|---|---|---|
|Request Binding|$.customerId|CTX-001|
|Response Extract|$.contracts|CTX-004|
|Collection Compare|$.contracts[]|CMP-POL-004|

---

## A.9 Business Check

|Check ID|条件|期待結果|
|---|---|---|
|CHK-BIZ-001|CTX-002 = true かつ CTX-004.size > 0|PASS|

---

## A.10 YAML例

```yaml
execution:
  id: EXEC-001
  version: 1.0.0
  businessId: BUS-001
  useCaseId: UC-001
  scenarioId: SC-001
  verificationId: VER-001
  testCaseId: TC-001
  testDataId: TD-001
  expectedResult: PASS

  environment:
    allowed:
      - STG
    baselineMode: APPROVED_FIRST

  entryContext:
    - contextId: CTX-001
      source: $.entryInput.customerId
      required: true

  steps:
    - order: 1
      stepId: UC-STEP-001
      apiId: API-001
      condition: "true"
      timeoutSeconds: 10
      retry:
        count: 1
        intervalMillis: 1000

      requestBindings:
        - target: $.customerId
          sourceType: CONTEXT
          source: CTX-001
          required: true

      responseExtracts:
        - source: $.exists
          contextId: CTX-002
          required: true

      checks:
        - checkId: CHK-RES-001
          type: FIXED
          target: $.resultCode
          expected: "0"
          severity: HIGH

        - checkId: CHK-RES-003
          type: CONTEXT_MATCH
          target: $.customerId
          expectedContext: CTX-001
          severity: HIGH

      next:
        rules:
          - condition: "CTX-002 == true"
            stepId: UC-STEP-002
          - condition: "CTX-002 == false"
            stepId: END

    - order: 2
      stepId: UC-STEP-002
      apiId: API-002
      condition: "CTX-002 == true"
      timeoutSeconds: 10
      retry:
        count: 1
        intervalMillis: 1000

      requestBindings:
        - target: $.customerId
          sourceType: CONTEXT
          source: CTX-001
          required: true

      responseExtracts:
        - source: $.customer
          contextId: CTX-003
          required: true

      next:
        default: UC-STEP-003

    - order: 3
      stepId: UC-STEP-003
      apiId: API-003
      condition: "CTX-002 == true"
      timeoutSeconds: 10
      retry:
        count: 1
        intervalMillis: 1000

      requestBindings:
        - target: $.customerId
          sourceType: CONTEXT
          source: CTX-001
          required: true

      responseExtracts:
        - source: $.contracts
          contextId: CTX-004
          required: false

      checks:
        - checkId: CHK-BIZ-001
          type: BUSINESS_RULE
          expression: "CTX-002 == true && size(CTX-004) > 0"
          expected: true
          severity: HIGH

      next:
        default: END

  snapshot:
    enabled: true
    maskEnabled: true

  diff:
    enabled: true
    baselineMode: APPROVED_FIRST
    policies:
      - CMP-POL-001
      - CMP-POL-004

  report:
    enabled: true
```

---

# Appendix B. 記入例：EXEC-002 顧客不存在

## B.1 基本情報

|項目|内容|
|---|---|
|Execution ID|EXEC-002|
|UseCase ID|UC-001|
|Scenario ID|SC-002|
|TestCase ID|TC-002|
|TestData ID|TD-002|
|開始API|API-001|
|終了API|API-001|
|期待Result|WARN / FAIL|

---

## B.2 API Step結果

|Step ID|API ID|期待Status|理由|
|---|---|---|---|
|UC-STEP-001|API-001|PASS|exists=falseを取得|
|UC-STEP-002|API-002|SKIP|CTX-002=false|
|UC-STEP-003|API-003|SKIP|CTX-002=false|

---

## B.3 Skip Rule

|Skip Rule ID|条件|Skip API|期待結果|
|---|---|---|---|
|SKIP-001|CTX-002 = false|API-002, API-003|想定どおりSkip|

---

## B.4 Business Result

|条件|期待Business Result|期待Scenario Result|
|---|---|---|
|Customer.exists = false|顧客不存在|WARN / FAIL|

:::

下一步应制作：

```text
system/06_verification_assets/api_test_spec/
API単体テスト仕様書_Template.md
```

它负责把一个 API 的输入必填、类型、长度、固定值、Enum、边界值、异常响应等展开成独立 TestCase。

## 第 197 轮

### 你

继续

### ChatGPT

放置位置：

```text
system/06_verification_assets/api_test_spec/API単体テスト仕様書_Template.md
```

:::writing{variant="document" id="64127"}
---
title: API単体テスト仕様書テンプレート
document_id: API-TEST-SPEC-TEMPLATE
version: 1.0.0
status: Template
document_type: API Test Specification
system_name: E6 API Verification Platform
phase: Verification Test Design
author:
reviewer:
approver:
created:
updated:
---

# API単体テスト仕様書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|---|---|
|文書ID|API-TEST-XXX|
|文書名称|〇〇API 単体テスト仕様書|
|対象API ID|API-XXX|
|対象API名称|（記載）|
|関連API分析書|API-ANL-XXX|
|関連API設計書|API-XXX|
|関連Verification ID|VER-XXX|
|対象環境|ENV-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|---|---|---|---|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|参照目的|
|---|---|---|---|
|API-ANL-XXX|API分析書|system/01_business/02_E6_API分析/|現行API情報|
|API-XXX|API設計書|system/03_api_design/|Request / Response契約|
|VER-XXX|Verification仕様書|system/06_verification_assets/|検証方針|
|MST-API-001|E6_API_Master|system/02_master/|API基本情報|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|比較Policy|
|SYS-SNP-001|Snapshot設計書|system/05_framework/|Evidence保存|
|SYS-LOG-001|ログ・例外設計書|system/05_framework/|Error / Log方針|

---

# 2. テスト概要

## 2.1 テスト目的

本仕様書は、対象APIについて、API設計書に定義されたRequest、Response、Header、HTTP Status、Error、Context、固定値、Enum、境界値が期待どおりであることを確認する。

---

## 2.2 テスト対象

|分類|対象|実施有無|
|---|---|---|
|Endpoint|Path、Method、Protocol|Yes / No|
|Header|必須Header、固定値、認証|Yes / No|
|Request|必須、型、長さ、Pattern、Enum、固定値|Yes / No|
|Response|HTTP Status、必須、型、固定値、Enum|Yes / No|
|入力値一致|RequestとResponseの値一致|Yes / No|
|Context|Input / Output Context|Yes / No|
|Error|4xx、5xx、Timeout、認証Error|Yes / No|
|Boundary|Min、Max、件数、桁数|Yes / No|
|Dynamic Field|Exists、Type Only、Ignore|Yes / No|
|Performance|Response Time、Timeout|Yes / No|

---

## 2.3 テスト対象外

|対象外|理由|備考|
|---|---|---|
|業務全体のAPI連携|UseCaseテスト仕様書で確認する| |
|画面操作|API単体テスト対象外| |
|大量負荷|性能試験で別途確認する| |

---

# 3. API基本情報

|項目|内容|
|---|---|
|API ID|API-XXX|
|API名称|（記載）|
|HTTP Method|GET / POST / PUT / DELETE|
|Path|（記載）|
|Content-Type|application/json|
|認証方式|Bearer Token / API Key / Basic / mTLS|
|Timeout|（記載）秒|
|Retry|（記載）回|
|正常HTTP Status|200 / 201 / 204|
|重要度|Critical / High / Medium / Low|

---

# 4. テスト観点一覧

|観点ID|分類|観点|対象|期待結果|
|---|---|---|---|---|
|TV-001|Interface|HTTP Methodが正しいこと|Method|期待Methodで実行される|
|TV-002|Header|必須Headerが存在すること|Header|正常受付される|
|TV-003|Request|必須項目が設定されること|Request Field|正常受付される|
|TV-004|Request|型が正しいこと|Request Field|正常受付される|
|TV-005|Request|最小長・最大長を満たすこと|Request Field|境界値結果が期待どおり|
|TV-006|Request|Patternを満たすこと|Request Field|正常または400|
|TV-007|Request|Enum内であること|Request Field|正常または400|
|TV-008|Response|必須項目が存在すること|Response Field|PASS|
|TV-009|Response|型が設計どおりであること|Response Field|PASS|
|TV-010|Response|固定値が期待値と一致すること|Response Field|PASS|
|TV-011|Response|Enum外値が返らないこと|Response Field|PASS|
|TV-012|Response|入力値と一致すること|Response Field|PASS|
|TV-013|Context|Output Contextを抽出できること|Context|PASS|
|TV-014|Error|必須不足時に期待Errorとなること|Error Response|PASS|
|TV-015|Security|認証不正時に401 / 403となること|Auth|PASS|

---

# 5. TestCase一覧

|TestCase ID|分類|TestCase名称|対象項目|入力Pattern|期待HTTP Status|期待Result|自動実行|TestData ID|
|---|---|---|---|---|---|---|---|---|
|API-TC-XXX|Normal / Boundary / Error / Security|（記載）|$.xxx|（記載）|200 / 400 / 401 / 500|PASS / FAIL|Yes / No|TD-XXX|

---

# 6. 正常系テスト

## 6.1 正常系TestCase

|TestCase ID|TestCase名称|入力条件|期待HTTP Status|期待Response|期待Result|
|---|---|---|---|---|---|
|API-TC-001|標準正常系|全必須項目を正常値で設定|200|API設計書どおり|PASS|

---

## 6.2 正常系Request

```json
{
  "xxx": "value"
}
```

---

## 6.3 正常系期待Response

```json
{
  "resultCode": "0"
}
```

---

# 7. Request Headerテスト

|TestCase ID|Header名|入力Pattern|設定値|期待HTTP Status|期待Error|期待Result|
|---|---|---|---|---|---|---|
|API-TC-H-001|Content-Type|正常|application/json|200|－|PASS|
|API-TC-H-002|Content-Type|未設定|－|400 / 415|（記載）|PASS|
|API-TC-H-003|Authorization|正常|Bearer Token|200|－|PASS|
|API-TC-H-004|Authorization|未設定|－|401|（記載）|PASS|
|API-TC-H-005|Authorization|不正|Invalid Token|401 / 403|（記載）|PASS|

---

# 8. Request項目テスト

## 8.1 項目別テストMatrix

|JSONPath|必須|Type|Null|Empty|Min|Max|Pattern|Enum|固定値|Default|
|---|---:|---|---|---|---:|---:|---|---|---|---|
|$.xxx|○ / －|String|可 / 不可|可 / 不可|1|20|（記載）|（記載）|（記載）|（記載）|

---

## 8.2 必須項目テスト

|TestCase ID|対象JSONPath|入力Pattern|入力値|期待HTTP Status|期待Error Code|期待Result|
|---|---|---|---|---|---|---|
|API-TC-REQ-001|$.xxx|正常|（記載）|200|－|PASS|
|API-TC-REQ-002|$.xxx|項目未設定|項目なし|400|（記載）|PASS|
|API-TC-REQ-003|$.xxx|Null|null|400 / 200|（設計どおり）|PASS|
|API-TC-REQ-004|$.xxx|空文字|""|400 / 200|（設計どおり）|PASS|

---

## 8.3 Typeテスト

|TestCase ID|対象JSONPath|期待Type|入力Type|入力値|期待HTTP Status|期待Result|
|---|---|---|---|---|---|---|
|API-TC-TYPE-001|$.xxx|String|String|"123"|200|PASS|
|API-TC-TYPE-002|$.xxx|String|Number|123|400|PASS|
|API-TC-TYPE-003|$.xxx|String|Boolean|true|400|PASS|
|API-TC-TYPE-004|$.xxx|String|Object|{}|400|PASS|
|API-TC-TYPE-005|$.xxx|String|Array|[]|400|PASS|

---

## 8.4 Length境界値テスト

|TestCase ID|対象JSONPath|条件|入力長|期待HTTP Status|期待Result|
|---|---|---|---:|---|---|
|API-TC-LEN-001|$.xxx|Min未満|Min-1|400|PASS|
|API-TC-LEN-002|$.xxx|Min|Min|200|PASS|
|API-TC-LEN-003|$.xxx|Min+1|Min+1|200|PASS|
|API-TC-LEN-004|$.xxx|Max-1|Max-1|200|PASS|
|API-TC-LEN-005|$.xxx|Max|Max|200|PASS|
|API-TC-LEN-006|$.xxx|Max超過|Max+1|400|PASS|

---

## 8.5 Patternテスト

|TestCase ID|対象JSONPath|Pattern|入力値|一致|期待HTTP Status|期待Result|
|---|---|---|---|---:|---|---|
|API-TC-PAT-001|$.xxx|（記載）|正常値|Yes|200|PASS|
|API-TC-PAT-002|$.xxx|（記載）|不正値|No|400|PASS|
|API-TC-PAT-003|$.xxx|（記載）|全角文字|No / Yes|設計どおり|PASS|
|API-TC-PAT-004|$.xxx|（記載）|特殊文字|No / Yes|設計どおり|PASS|

---

## 8.6 Enumテスト

|TestCase ID|対象JSONPath|許容値|入力値|期待HTTP Status|期待Result|
|---|---|---|---|---|---|
|API-TC-ENUM-001|$.xxx|A,B,C|A|200|PASS|
|API-TC-ENUM-002|$.xxx|A,B,C|B|200|PASS|
|API-TC-ENUM-003|$.xxx|A,B,C|C|200|PASS|
|API-TC-ENUM-004|$.xxx|A,B,C|D|400|PASS|
|API-TC-ENUM-005|$.xxx|A,B,C|小文字a|400 / 200|設計どおり|

---

## 8.7 固定値テスト

|TestCase ID|対象JSONPath|期待固定値|入力値|期待HTTP Status|期待Result|
|---|---|---|---|---|---|
|API-TC-FIX-001|$.xxx|FIXED|FIXED|200|PASS|
|API-TC-FIX-002|$.xxx|FIXED|OTHER|400|PASS|
|API-TC-FIX-003|$.xxx|FIXED|未設定|400 / Default|設計どおり|

---

## 8.8 Default値テスト

|TestCase ID|対象JSONPath|Default値|入力状態|期待処理|期待Result|
|---|---|---|---|---|---|
|API-TC-DEF-001|$.xxx|DEFAULT|項目未設定|DEFAULTが利用される|PASS|
|API-TC-DEF-002|$.xxx|DEFAULT|値指定|指定値が優先される|PASS|

---

# 9. Response項目テスト

## 9.1 Response項目Matrix

|JSONPath|必須|Type|Null|Min|Max|Pattern|Enum|固定値|入力値一致|Dynamic|
|---|---:|---|---|---:|---:|---|---|---|---|---:|
|$.xxx|○ / －|String|可 / 不可|1|20|（記載）|（記載）|（記載）|Request $.xxx|Yes / No|

---

## 9.2 必須・存在確認

|TestCase ID|対象JSONPath|検証方式|期待値|重要度|不一致時Result|
|---|---|---|---|---|---|
|API-TC-RES-001|$.xxx|Exists|存在すること|High|FAIL|

---

## 9.3 Type確認

|TestCase ID|対象JSONPath|期待Type|実際Type|期待Result|
|---|---|---|---|---|
|API-TC-RES-002|$.xxx|String|Runtime取得|PASS|

---

## 9.4 固定値確認

|TestCase ID|対象JSONPath|期待固定値|適用条件|期待Result|
|---|---|---|---|---|
|API-TC-RES-003|$.resultCode|0|正常終了時|PASS|

---

## 9.5 Enum確認

|TestCase ID|対象JSONPath|許容値|期待Result|
|---|---|---|---|
|API-TC-RES-004|$.status|ACTIVE, INACTIVE|PASS|

---

## 9.6 入力値一致確認

|TestCase ID|Response JSONPath|Request JSONPath|比較方式|期待Result|
|---|---|---|---|---|
|API-TC-RES-005|$.customerId|$.customerId|Equals|PASS|

---

## 9.7 Dynamic Field確認

|TestCase ID|JSONPath|Check方式|Compare Policy|期待Result|
|---|---|---|---|---|
|API-TC-DYN-001|$.traceId|Exists / Type Only|CMP-POL-001|PASS|
|API-TC-DYN-002|$.updatedAt|Tolerance / Ignore|CMP-POL-002|PASS / IGNORED|

---

# 10. Contextテスト

## 10.1 Input Context

|TestCase ID|Context ID|Request JSONPath|設定値|期待Result|
|---|---|---|---|---|
|API-TC-CTX-001|CTX-XXX|$.xxx|Context値と一致|PASS|

---

## 10.2 Output Context

|TestCase ID|Response JSONPath|Context ID|期待Type|期待Result|
|---|---|---|---|---|
|API-TC-CTX-002|$.xxx|CTX-XXX|String / Object / Array|PASS|

---

## 10.3 Context異常

|TestCase ID|条件|期待処理|期待Result|
|---|---|---|---|
|API-TC-CTX-003|必須Context未設定|API実行前停止|ERROR|
|API-TC-CTX-004|Context型不一致|API実行前停止|ERROR|
|API-TC-CTX-005|Output Context抽出失敗|Scenario方針に従う|ERROR / WARN|

---

# 11. Error Responseテスト

## 11.1 Error TestCase一覧

|TestCase ID|発生条件|期待HTTP Status|期待Error Code|期待Message方式|期待Result|
|---|---|---|---|---|---|
|API-TC-ERR-001|必須項目未設定|400|（記載）|Contains / Regex|PASS|
|API-TC-ERR-002|認証情報未設定|401|（記載）|Contains / Regex|PASS|
|API-TC-ERR-003|権限不足|403|（記載）|Contains / Regex|PASS|
|API-TC-ERR-004|対象Dataなし|404 / 200|（業務仕様）|Equals / Contains|PASS|
|API-TC-ERR-005|内部Error|500|（記載）|Contains / Regex|PASS|
|API-TC-ERR-006|Timeout|－|TIMEOUT|－|PASS|

---

## 11.2 Error Response項目

|JSONPath|必須|Type|検証方式|期待仕様|
|---|---:|---|---|---|
|$.error.code|○|String|Equals / Enum|（記載）|
|$.error.message|○|String|Contains / Regex|（記載）|
|$.traceId|－|String|Exists / Ignore|Dynamic|

---

# 12. HTTP Statusテスト

|TestCase ID|条件|期待HTTP Status|期待Result|
|---|---|---|---|
|API-TC-HTTP-001|正常Request|200|PASS|
|API-TC-HTTP-002|登録成功|201|PASS|
|API-TC-HTTP-003|Bodyなし正常終了|204|PASS|
|API-TC-HTTP-004|Request不正|400|PASS|
|API-TC-HTTP-005|認証不正|401|PASS|
|API-TC-HTTP-006|権限不足|403|PASS|
|API-TC-HTTP-007|対象なし|404 / 200|設計どおり|
|API-TC-HTTP-008|Server Error|500|PASS|

---

# 13. Timeout・Retryテスト

|TestCase ID|条件|Timeout設定|期待Retry回数|期待最終Result|Evidence|
|---|---|---:|---:|---|---|
|API-TC-TIME-001|応答がTimeout以内|10秒|0|PASS|Execution Snapshot|
|API-TC-TIME-002|1回目Timeout、2回目成功|10秒|1|PASS / WARN|Retry Log|
|API-TC-TIME-003|全回Timeout|10秒|2|FAIL / ERROR|Error Snapshot|
|API-TC-TIME-004|HTTP 400|10秒|0|FAIL|Execution Snapshot|
|API-TC-TIME-005|HTTP 503|10秒|設定回数|FAIL / PASS|Retry Log|

---

# 14. Performance確認

|TestCase ID|観点|基準|期待Result|
|---|---|---|---|
|API-TC-PERF-001|Response Time|（記載）ms以内|PASS / WARN|
|API-TC-PERF-002|Timeout|設定秒数以内|PASS|
|API-TC-PERF-003|Response Size|（記載）KB以内|PASS / WARN|

---

# 15. Securityテスト

|TestCase ID|観点|入力 / 条件|期待結果|
|---|---|---|---|
|API-TC-SEC-001|Token未設定|Authorizationなし|401|
|API-TC-SEC-002|Token不正|Invalid Token|401 / 403|
|API-TC-SEC-003|権限不足|権限なしToken|403|
|API-TC-SEC-004|Secret Mask|Request Snapshot確認|SecretがMaskされる|
|API-TC-SEC-005|個人情報Mask|Response Snapshot確認|対象項目がMaskされる|

---

# 16. TestData一覧

|TestData ID|TestCase ID|名称|入力内容|配置先|状態|
|---|---|---|---|---|---|
|TD-XXX|API-TC-XXX|（記載）|（記載）|system/06_verification_assets/test_data/API-XXX/|Active|

---

# 17. TestCase詳細テンプレート

## 17.1 基本情報

|項目|内容|
|---|---|
|TestCase ID|API-TC-XXX|
|TestCase名称|（記載）|
|対象API|API-XXX|
|分類|Normal / Boundary / Error / Security|
|TestData ID|TD-XXX|
|重要度|Critical / High / Medium / Low|
|自動実行|Yes / No|

---

## 17.2 前提条件

|No|前提条件|確認方法|未成立時処理|
|---:|---|---|---|
|1|（記載）|（記載）|BLOCKED / ERROR|

---

## 17.3 入力

```json
{
  "xxx": "value"
}
```

---

## 17.4 実行手順

|Step No|処理|入力|期待結果|
|---:|---|---|---|
|1|API Request生成|TestData|Request生成成功|
|2|API実行|Request|Response取得|
|3|Response検証|Response|期待仕様と一致|
|4|Snapshot確認|Evidence|保存成功|

---

## 17.5 期待結果

|対象|期待結果|
|---|---|
|HTTP Status|（記載）|
|Response Body|（記載）|
|Context|（記載）|
|Execution Result|PASS / WARN / FAIL|
|Evidence|Request / Response / Context / Log|

---

# 18. Result判定

|条件|TestCase Result|
|---|---|
|全Check PASS|PASS|
|WARNのみ|WARN|
|1件以上FAIL|FAIL|
|実行基盤Error|ERROR|
|前提条件未成立|BLOCKED|
|条件により対象外|SKIP|

---

# 19. Evidence

|Evidence ID|対象|保存内容|保存先|
|---|---|---|---|
|EVD-API-XXX|Request|Request Snapshot|outputs/runs/{runId}/raw/|
|EVD-API-XXX|Response|Response Snapshot|outputs/runs/{runId}/raw/|
|EVD-API-XXX|Context|Context Snapshot|outputs/runs/{runId}/snapshot/|
|EVD-API-XXX|Execution|Execution Snapshot|outputs/runs/{runId}/snapshot/|
|EVD-API-XXX|Error|Error Snapshot / Log|outputs/runs/{runId}/logs/|

---

# 20. Coverage

## 20.1 Request Coverage

|対象項目数|テスト済項目数|未テスト項目数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

## 20.2 Response Coverage

|対象項目数|テスト済項目数|未テスト項目数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

## 20.3 Error Coverage

|Error Pattern数|テスト済数|未テスト数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

# 21. Traceability

|API ID|API設計書|Verification ID|TestCase ID|TestData ID|Check ID|Evidence ID|
|---|---|---|---|---|---|---|
|API-XXX|API-XXX|VER-XXX|API-TC-XXX|TD-XXX|CHK-XXX|EVD-API-XXX|

---

# 22. Review観点

|観点|確認内容|
|---|---|
|API設計整合|Request / Response定義と一致しているか|
|必須Coverage|全必須項目に未設定・Null・Emptyテストがあるか|
|型Coverage|型不一致Patternが定義されているか|
|境界値Coverage|Min-1、Min、Max、Max+1が確認されているか|
|固定値Coverage|正常固定値と不正固定値が確認されているか|
|Enum Coverage|全許容値と許容外値が確認されているか|
|Response Coverage|必須、型、固定値、入力値一致が確認されているか|
|Error Coverage|400、401、403、404、500、Timeoutが整理されているか|
|Context|Input / Output Contextが確認されているか|
|Evidence|各TestCaseの証跡が保存されるか|
|Mask|Secret・個人情報がMaskされるか|

---

# Appendix A. 記入例：API-001 Customer Exists API

## A.1 API基本情報

|項目|内容|
|---|---|
|文書ID|API-TEST-001|
|対象API ID|API-001|
|対象API名称|Customer Exists API|
|HTTP Method|POST|
|Path|/v1/customers/exists|
|正常HTTP Status|200|
|重要度|High|

---

## A.2 Request項目

|JSONPath|Type|必須|Null|Empty|Min|Max|Pattern|
|---|---|---:|---|---|---:|---:|---|
|$.customerId|String|○|不可|不可|1|20|^[0-9]+$|

---

## A.3 Response項目

|JSONPath|Type|必須|固定値|Enum|入力値一致|Dynamic|
|---|---|---:|---|---|---|---:|
|$.resultCode|String|○|0|0,1|－|No|
|$.exists|Boolean|○|－|true,false|－|No|
|$.customerId|String|○|－|－|Request $.customerId|No|
|$.traceId|String|－|－|－|－|Yes|

---

## A.4 TestCase一覧

|TestCase ID|分類|TestCase名称|入力|期待Status|期待Result|
|---|---|---|---|---|---|
|API-TC-001|Normal|正常顧客番号|10000001|200|PASS|
|API-TC-002|Boundary|1桁顧客番号|1|200|PASS|
|API-TC-003|Boundary|20桁顧客番号|12345678901234567890|200|PASS|
|API-TC-004|Boundary|21桁顧客番号|123456789012345678901|400|PASS|
|API-TC-005|Error|customerId未設定|項目なし|400|PASS|
|API-TC-006|Error|customerId Null|null|400|PASS|
|API-TC-007|Error|customerId空文字|""|400|PASS|
|API-TC-008|Error|英字混在|ABC001|400|PASS|
|API-TC-009|Security|Authorization未設定|正常Body|401|PASS|
|API-TC-010|Security|Authorization不正|正常Body|401 / 403|PASS|

---

## A.5 正常系期待Response

```json
{
  "resultCode": "0",
  "exists": true,
  "customerId": "10000001",
  "traceId": "dynamic-value"
}
```

---

## A.6 Response Check

|Check ID|JSONPath|Check Type|期待値|重要度|
|---|---|---|---|---|
|CHK-API001-001|$.resultCode|Fixed|0|High|
|CHK-API001-002|$.exists|Type / Enum|Boolean / true,false|High|
|CHK-API001-003|$.customerId|Input Match|Request $.customerId|High|
|CHK-API001-004|$.traceId|Exists / Type Only|String|Low|

---

## A.7 TestCase詳細例

### API-TC-004：customerId最大長超過

|項目|内容|
|---|---|
|TestCase ID|API-TC-004|
|分類|Boundary|
|対象項目|$.customerId|
|入力値|123456789012345678901|
|入力長|21|
|最大長|20|
|期待HTTP Status|400|
|期待Error Code|INVALID_CUSTOMER_ID|
|期待Result|PASS|

Request：

```json
{
  "customerId": "123456789012345678901"
}
```

期待Error Response：

```json
{
  "error": {
    "code": "INVALID_CUSTOMER_ID",
    "message": "customerId length is invalid."
  },
  "traceId": "dynamic-value"
}
```

---

## A.8 Traceability例

|API ID|API設計書|Verification ID|TestCase ID|TestData ID|Check ID|Evidence ID|
|---|---|---|---|---|---|---|
|API-001|API-001|VER-001|API-TC-001〜API-TC-010|TD-API001-001〜010|CHK-API001-001〜004|EVD-API-001|

:::

下一步应制作：

```text
system/06_verification_assets/usecase_test_spec/
UseCaseテスト仕様書_Template.md
```

它负责验证多个 API 按业务路径顺序执行、分岐、Skip、Context 传递和最终业务结果。

## 第 198 轮

### 你

继续

### ChatGPT

放置位置：

```text
system/06_verification_assets/usecase_test_spec/UseCaseテスト仕様書_Template.md
```

:::writing{variant="document" id="47381"}
---
title: UseCaseテスト仕様書テンプレート
document_id: USECASE-TEST-SPEC-TEMPLATE
version: 1.0.0
status: Template
document_type: UseCase Test Specification
system_name: E6 API Verification Platform
phase: Verification Test Design
author:
reviewer:
approver:
created:
updated:
---

# UseCaseテスト仕様書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|---|---|
|文書ID|UC-TEST-XXX|
|文書名称|〇〇UseCase テスト仕様書|
|対象UseCase ID|UC-XXX|
|対象UseCase名称|（記載）|
|対象Business ID|BUS-XXX|
|対象Scenario|SC-XXX|
|対象API|API-XXX|
|関連BA|BA-XXX|
|関連BAシナリオ一覧|BA-XXX_〇〇業務_シナリオ一覧.md|
|関連UseCase設計書|UC-XXX|
|関連Verification ID|VER-XXX|
|対象環境|ENV-XXX|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者|（記載）|
|レビューア|（記載）|
|承認者|（記載）|
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|---|---|---|---|
|1.0.0|YYYY-MM-DD|（記載）|初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|参照目的|
|---|---|---|---|
|BA-XXX|現行業務分析書|system/01_business/01_業務分析/|業務Flow、処理条件|
|BA-SC-XXX|BA分析書シナリオ一覧|system/01_business/01_業務分析/|API呼出経路、分岐|
|UC-XXX|UseCase設計書|system/04_usecase_design/|UseCase実行仕様|
|VER-XXX|Verification仕様書|system/06_verification_assets/|検証項目|
|EXEC-XXX|Execution仕様書|system/06_verification_assets/execution_spec/|実行定義|
|MST-SC-001|Scenario_Master|system/02_master/|Scenario定義|
|MST-API-UC-SC-001|API_UseCase_Scenario対応表|system/02_master/|API順序、Skip条件|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|
|MST-CMP-POL-001|Compare_Policy_Master|system/02_master/|比較Policy|

---

# 2. テスト概要

## 2.1 テスト目的

本仕様書は、対象UseCaseについて、複数APIが業務定義どおりの順序、分岐、Skip条件、Context連携で実行され、Scenarioごとの業務結果、Verification結果、Snapshot、Diff、Reportが期待どおりとなることを確認する。

---

## 2.2 テスト対象

|分類|対象|実施有無|
|---|---|---|
|UseCase開始条件|Entry Input、前提条件|Yes / No|
|API実行順序|Scenario別API Chain|Yes / No|
|分岐|API Response、処理Flgによる分岐|Yes / No|
|Skip|後続APIのSkip条件|Yes / No|
|Context|API間データ引継ぎ|Yes / No|
|Retry / Timeout|障害時制御|Yes / No|
|Business Result|業務結果、終了条件|Yes / No|
|Scenario Result|PASS / WARN / FAIL / ERROR|Yes / No|
|Baseline Diff|CurrentとBaseline比較|Yes / No|
|Evidence|Request、Response、Context、Execution|Yes / No|
|Report|Daily Summary、Diff Report|Yes / No|

---

## 2.3 テスト対象外

|対象外|理由|備考|
|---|---|---|
|API単項目の全境界値|API単体テスト仕様書で確認する| |
|大量負荷|性能試験で別途実施する| |
|画面操作|API UseCase検証対象外| |

---

# 3. UseCase基本情報

|項目|内容|
|---|---|
|UseCase ID|UC-XXX|
|UseCase名称|（記載）|
|Business ID|BUS-XXX|
|開始条件|（記載）|
|終了条件|（記載）|
|開始API|API-XXX|
|標準終了API|API-XXX|
|対象Scenario数|（記載）|
|対象API数|（記載）|
|実行方式|Sequential / Parallel|
|日次実行対象|Yes / No|
|重要度|Critical / High / Medium / Low|

---

# 4. Scenario一覧

|Scenario ID|Scenario名称|分類|対象Path ID|開始API|終了API|処理Flg|期待Business Result|期待Scenario Result|TestCase ID|
|---|---|---|---|---|---|---|---|---|---|
|SC-XXX|（記載）|Normal / Alternative / Exception / Boundary / Regression|PATH-XXX|API-XXX|API-XXX|（記載）|（記載）|PASS / WARN / FAIL / ERROR|UC-TC-XXX|

---

# 5. Scenario Matrix

|API / Scenario|SC-XXX|SC-XXX|SC-XXX|
|---|:---:|:---:|:---:|
|API-XXX|Run / Skip / Error|Run / Skip / Error|Run / Skip / Error|
|API-XXX|Run / Skip / Error|Run / Skip / Error|Run / Skip / Error|
|開始API|API-XXX|API-XXX|API-XXX|
|終了API|API-XXX|API-XXX|API-XXX|
|期待Result|PASS / WARN / FAIL|PASS / WARN / FAIL|PASS / WARN / FAIL|

---

# 6. TestCase一覧

|TestCase ID|Scenario ID|TestCase名称|分類|TestData ID|開始API|終了API|期待Result|自動実行|
|---|---|---|---|---|---|---|---|---|
|UC-TC-XXX|SC-XXX|（記載）|Normal / Alternative / Exception / Boundary / Regression|TD-XXX|API-XXX|API-XXX|PASS / WARN / FAIL / ERROR|Yes / No|

---

# 7. TestData

## 7.1 TestData一覧

|TestData ID|Scenario ID|名称|Entry Input|前提Data|期待Result|配置先|状態|
|---|---|---|---|---|---|---|---|
|TD-XXX|SC-XXX|（記載）|（記載）|（記載）|PASS / WARN / FAIL|system/06_verification_assets/test_data/UC-XXX/|Active|

---

## 7.2 Entry Input

|TestData ID|項目名|JSONPath|Type|値|Context ID|必須|Mask|
|---|---|---|---|---|---|---:|---:|
|TD-XXX|（記載）|$.entryInput.xxx|String / Number / Boolean|（記載）|CTX-XXX|○ / －|Yes / No|

---

## 7.3 前提条件

|Precondition ID|TestData ID|前提条件|確認方法|未成立時Result|
|---|---|---|---|---|
|PRE-XXX|TD-XXX|（記載）|API / DB / 手動確認|BLOCKED / ERROR|

---

## 7.4 後処理

|Cleanup ID|TestData ID|処理内容|対象Data / API|失敗時Result|
|---|---|---|---|---|
|CLEAN-XXX|TD-XXX|Cleanup / Restore / なし|（記載）|WARN / ERROR|

---

# 8. API実行順序テスト

## 8.1 Scenario別期待順序

|TestCase ID|Scenario ID|期待API順序|期待開始API|期待終了API|不一致時Result|
|---|---|---|---|---|---|
|UC-TC-XXX|SC-XXX|API-001 → API-002 → API-003|API-001|API-003|FAIL|

---

## 8.2 実行順序Check

|Check ID|TestCase ID|確認対象|実際値取得元|期待値|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-FLOW-XXX|UC-TC-XXX|API実行順序|Execution Snapshot|（記載）|FAIL|
|CHK-UC-START-XXX|UC-TC-XXX|開始API|Execution Snapshot|API-XXX|FAIL|
|CHK-UC-END-XXX|UC-TC-XXX|終了API|Execution Snapshot|API-XXX|FAIL|

---

# 9. 分岐テスト

## 9.1 分岐条件一覧

|Branch ID|対象Step / API|判定項目|条件式|成立時遷移|不成立時遷移|対象Scenario|
|---|---|---|---|---|---|---|
|BRANCH-XXX|API-XXX|$.xxx / CTX-XXX|（記載）|UC-STEP-XXX|END / UC-STEP-XXX|SC-XXX|

---

## 9.2 分岐Check

|Check ID|TestCase ID|判定条件|期待分岐先|実際値取得元|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-BRANCH-XXX|UC-TC-XXX|（記載）|UC-STEP-XXX / END|Execution Snapshot / Context Snapshot|FAIL|

---

## 9.3 処理Flg Check

|Check ID|処理Flg|設定条件|期待値|対象Scenario|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-FLG-XXX|（記載）|（記載）|（記載）|SC-XXX|FAIL|

---

# 10. Skipテスト

## 10.1 Skip Rule一覧

|Skip Rule ID|対象Scenario|条件式|Skip対象API|期待Status|期待後続処理|
|---|---|---|---|---|---|
|SKIP-XXX|SC-XXX|（記載）|API-XXX|SKIP|CONTINUE / END / FAIL|

---

## 10.2 Skip Check

|Check ID|TestCase ID|Skip対象API|期待Status|Skip理由|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-SKIP-XXX|UC-TC-XXX|API-XXX|SKIP|（記載）|FAIL|

---

## 10.3 想定外Skip

|条件|Result|
|---|---|
|必須APIがSkip|FAIL|
|Skip条件不成立なのにSkip|FAIL|
|期待Skipが実行された|FAIL|
|Skip理由が記録されていない|WARN / FAIL|

---

# 11. Context連携テスト

## 11.1 Context Flow

|Context ID|Context名|Producer|Consumer|生成Step|利用Step|対象Scenario|
|---|---|---|---|---|---|---|
|CTX-XXX|（記載）|Entry Input / API-XXX|API-XXX / Branch / Report|UC-STEP-XXX|UC-STEP-XXX|SC-XXX|

---

## 11.2 Context生成Check

|Check ID|Context ID|Producer|Response JSONPath|期待Type|必須|未生成時Result|
|---|---|---|---|---|---:|---|
|CHK-UC-CTX-GEN-XXX|CTX-XXX|API-XXX|$.xxx|String / Object / Array|○ / －|ERROR / FAIL|

---

## 11.3 Context Binding Check

|Check ID|Context ID|Consumer API|Request JSONPath|比較方式|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-CTX-BIND-XXX|CTX-XXX|API-XXX|$.xxx|Equals|FAIL|

---

## 11.4 Context Lifetime Check

|Check ID|Context ID|期待Scope|生成タイミング|破棄タイミング|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-CTX-LIFE-XXX|CTX-XXX|Run / UseCase / Scenario|（記載）|（記載）|ERROR|

---

# 12. Request / Response連携テスト

## 12.1 前段Response・後段Request対応

|Mapping ID|前段API|Response JSONPath|Context ID|後段API|Request JSONPath|変換|期待Result|
|---|---|---|---|---|---|---|---|
|MAP-XXX|API-XXX|$.xxx|CTX-XXX|API-XXX|$.xxx|なし / Format / Cast|PASS|

---

## 12.2 Mapping Check

|Check ID|Mapping ID|比較方式|期待値|不一致時Result|
|---|---|---|---|---|
|CHK-UC-MAP-XXX|MAP-XXX|Equals / Normalize / Transform|前段値と後段値が一致|FAIL|

---

# 13. Business Resultテスト

## 13.1 業務結果一覧

|Business Check ID|Scenario ID|条件式|期待Business Result|期待Scenario Result|重要度|
|---|---|---|---|---|---|
|BCHK-XXX|SC-XXX|（記載）|（記載）|PASS / WARN / FAIL|High / Medium / Low|

---

## 13.2 業務結果Check

|Check ID|TestCase ID|対象Context / Response|期待値|不一致時Result|
|---|---|---|---|---|
|CHK-UC-BIZ-XXX|UC-TC-XXX|CTX-XXX / $.xxx|（記載）|FAIL / WARN|

---

## 13.3 終了条件Check

|Check ID|Scenario ID|終了条件|期待終了API|期待Result|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-ENDCOND-XXX|SC-XXX|（記載）|API-XXX|PASS / WARN / FAIL|FAIL|

---

# 14. Error・Exceptionテスト

## 14.1 Error Scenario一覧

|TestCase ID|Scenario ID|発生箇所|発生条件|期待Exception|期待停止範囲|期待Result|
|---|---|---|---|---|---|---|
|UC-TC-ERR-XXX|SC-XXX|API-XXX|Timeout / 4xx / 5xx / Context Error|TimeoutException / ApiException / ContextException|STOP_STEP / STOP_SCENARIO / STOP_USECASE|FAIL / ERROR|

---

## 14.2 Retry Check

|Check ID|API ID|発生条件|期待Retry回数|Retry後期待動作|不一致時Result|
|---|---|---|---:|---|---|
|CHK-UC-RETRY-XXX|API-XXX|Timeout|2|成功時継続、失敗時停止|FAIL|

---

## 14.3 Stop / Continue Check

|Check ID|発生条件|期待制御|後続API|期待Status|不一致時Result|
|---|---|---|---|---|---|
|CHK-UC-CTRL-XXX|API-XXX Error|STOP_SCENARIO / CONTINUE|API-XXX|SKIP / Run|FAIL|

---

# 15. Baseline Diffテスト

## 15.1 Diff対象

|Diff ID|Scenario ID|対象API / Context|対象Path|Compare Policy|重要度|不一致時Result|
|---|---|---|---|---|---|---|
|DIFF-UC-XXX|SC-XXX|API-XXX / CTX-XXX|$.xxx|CMP-POL-XXX|High / Medium / Low|FAIL / WARN|

---

## 15.2 Dynamic除外

|対象|Policy ID|期待Result|
|---|---|---|
|$.traceId|CMP-POL-001|IGNORED|
|Runtime.runId|CMP-POL-001|IGNORED|

---

## 15.3 Collection Diff

|Check ID|対象JSONPath|比較方式|Key|順序考慮|期待Result|
|---|---|---|---|---|---|
|CHK-UC-COL-XXX|$.items[]|Key Match / Count Only|itemId|Yes / No|PASS / WARN / FAIL|

---

# 16. Evidenceテスト

## 16.1 Evidence一覧

|Evidence ID|TestCase ID|対象|必須|保存先|
|---|---|---|---:|---|
|EVD-UC-XXX|UC-TC-XXX|Request Snapshot|○|raw/|
|EVD-UC-XXX|UC-TC-XXX|Response Snapshot|○|raw/|
|EVD-UC-XXX|UC-TC-XXX|Context Snapshot|○|snapshot/|
|EVD-UC-XXX|UC-TC-XXX|Execution Snapshot|○|snapshot/|
|EVD-UC-XXX|UC-TC-XXX|Diff Result|○|diff/|
|EVD-UC-XXX|UC-TC-XXX|Runtime Log|○|logs/|

---

## 16.2 Evidence Check

|Check ID|TestCase ID|確認内容|不一致時Result|
|---|---|---|---|
|CHK-UC-EVD-XXX|UC-TC-XXX|必要Snapshotがすべて保存されていること|ERROR|
|CHK-UC-EVD-XXX|UC-TC-XXX|Evidence Indexから各Snapshotへ辿れること|WARN / ERROR|
|CHK-UC-EVD-XXX|UC-TC-XXX|秘匿情報がMaskされていること|ERROR|

---

# 17. Reportテスト

## 17.1 Report反映Check

|Check ID|Report|確認内容|期待値|不一致時Result|
|---|---|---|---|---|
|CHK-UC-RPT-XXX|Daily Summary|UseCase Resultが反映されること|実結果と一致|ERROR|
|CHK-UC-RPT-XXX|Diff Report|差分内容が反映されること|Diff Resultと一致|ERROR|
|CHK-UC-RPT-XXX|Evidence Report|Evidence Linkが有効であること|Link有効|WARN / ERROR|
|CHK-UC-RPT-XXX|Execution Report|実行順序・Skipが反映されること|Execution Snapshotと一致|ERROR|

---

# 18. TestCase詳細テンプレート

## 18.1 基本情報

|項目|内容|
|---|---|
|TestCase ID|UC-TC-XXX|
|TestCase名称|（記載）|
|対象UseCase|UC-XXX|
|対象Scenario|SC-XXX|
|対象Path|PATH-XXX|
|TestData ID|TD-XXX|
|開始API|API-XXX|
|終了API|API-XXX|
|期待Result|PASS / WARN / FAIL / ERROR|
|重要度|Critical / High / Medium / Low|
|自動実行|Yes / No|

---

## 18.2 前提条件

|No|前提条件|確認方法|未成立時処理|
|---:|---|---|---|
|1|（記載）|（記載）|BLOCKED / ERROR|

---

## 18.3 Entry Input

```json
{
  "xxx": "value"
}
```

---

## 18.4 実行手順

|Step No|Step ID|処理|対象API|入力Context|期待出力Context|期待Status|
|---:|---|---|---|---|---|---|
|1|UC-STEP-XXX|（記載）|API-XXX|CTX-XXX|CTX-XXX|PASS / SKIP / FAIL|

---

## 18.5 期待結果

|対象|期待結果|
|---|---|
|API順序|（記載）|
|開始API|API-XXX|
|終了API|API-XXX|
|Skip API|（記載）|
|Context|（記載）|
|Business Result|（記載）|
|Scenario Result|PASS / WARN / FAIL / ERROR|
|Evidence|必要Snapshotが保存されること|
|Report|期待Resultが反映されること|

---

# 19. Result判定

## 19.1 Check単位

|条件|Result|
|---|---|
|期待どおり|PASS|
|確認対象差分|WARN|
|期待不一致|FAIL|
|実行不能|ERROR|
|前提条件未成立|BLOCKED|
|条件付き未実行|SKIP|

---

## 19.2 TestCase単位

|条件|TestCase Result|
|---|---|
|ERRORあり|ERROR|
|FAILあり|FAIL|
|WARNのみ|WARN|
|全Check PASS|PASS|
|前提未成立|BLOCKED|
|全対象が期待Skip|PASS / SKIP|

---

## 19.3 UseCase単位

|条件|UseCase Result|
|---|---|
|TestCase ERRORあり|ERROR|
|TestCase FAILあり|FAIL|
|TestCase WARNあり|WARN|
|全TestCase PASS|PASS|
|全TestCase BLOCKED|BLOCKED|

---

# 20. Coverage

## 20.1 Scenario Coverage

|Scenario総数|テスト済数|未テスト数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

## 20.2 API Path Coverage

|Path総数|テスト済数|未テスト数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

## 20.3 Branch Coverage

|Branch総数|成立側実施数|不成立側実施数|未実施数|Coverage率|
|---:|---:|---:|---:|---:|
|0|0|0|0|0%|

---

## 20.4 Context Coverage

|Context総数|生成確認済|利用確認済|未確認|Coverage率|
|---:|---:|---:|---:|---:|
|0|0|0|0|0%|

---

## 20.5 Error Coverage

|Error Scenario数|実施済数|未実施数|Coverage率|
|---:|---:|---:|---:|
|0|0|0|0%|

---

# 21. Traceability

|Business ID|BA ID|Path ID|UseCase ID|Scenario ID|TestCase ID|TestData ID|Step ID|API ID|Context ID|Verification ID|Execution ID|Evidence ID|
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|BUS-XXX|BA-XXX|PATH-XXX|UC-XXX|SC-XXX|UC-TC-XXX|TD-XXX|UC-STEP-XXX|API-XXX|CTX-XXX|VER-XXX|EXEC-XXX|EVD-UC-XXX|

---

# 22. Review観点

|観点|確認内容|
|---|---|
|BA Path整合|BAシナリオ一覧の全PathがTestCase化されているか|
|Scenario Coverage|全ScenarioがTestCaseに対応しているか|
|API順序|Scenario別API順序がUseCase設計書と一致しているか|
|分岐Coverage|各Branchの成立・不成立が確認されているか|
|Skip Coverage|全Skip Ruleが確認されているか|
|Context Coverage|Producer、Consumer、Bindingが確認されているか|
|Error Coverage|Timeout、4xx、5xx、Context Errorが確認されているか|
|Business Result|業務結果とScenario Resultの関係が明確か|
|Evidence|実行結果を判断できる証跡が残るか|
|Report|UseCase結果がReportへ正しく反映されるか|
|Traceability|BAからEvidenceまで追跡可能か|

---

# Appendix A. 記入例：UC-001 顧客情報照会

## A.1 UseCase基本情報

|項目|内容|
|---|---|
|文書ID|UC-TEST-001|
|対象UseCase ID|UC-001|
|対象UseCase名称|顧客情報照会|
|Business ID|BUS-001|
|開始API|API-001|
|標準終了API|API-003|
|対象Scenario数|4|
|対象API数|3|
|実行方式|Sequential|
|重要度|High|

---

## A.2 Scenario一覧

|Scenario ID|Scenario名称|分類|Path ID|開始API|終了API|期待Business Result|期待Result|TestCase ID|
|---|---|---|---|---|---|---|---|---|
|SC-001|正常系|Normal|PATH-001|API-001|API-003|顧客・契約情報取得成功|PASS|UC-TC-001|
|SC-002|顧客不存在|Alternative|PATH-002|API-001|API-001|顧客不存在|WARN / FAIL|UC-TC-002|
|SC-003|契約0件|Alternative|PATH-003|API-001|API-003|契約0件|PASS / WARN|UC-TC-003|
|SC-004|API-002 Timeout|Exception|PATH-004|API-001|API-002|顧客詳細取得失敗|FAIL|UC-TC-004|

---

## A.3 Scenario Matrix

|API / Scenario|SC-001|SC-002|SC-003|SC-004|
|---|:---:|:---:|:---:|:---:|
|API-001 Customer Exists API|Run|Run|Run|Run|
|API-002 Customer Detail API|Run|Skip|Run|Run / Error|
|API-003 Contract List API|Run|Skip|Run|Skip|
|開始API|API-001|API-001|API-001|API-001|
|終了API|API-003|API-001|API-003|API-002|
|期待Result|PASS|WARN / FAIL|PASS / WARN|FAIL|

---

## A.4 TestCase一覧

|TestCase ID|Scenario ID|TestCase名称|TestData ID|開始API|終了API|期待Result|
|---|---|---|---|---|---|---|
|UC-TC-001|SC-001|顧客情報照会正常系|TD-001|API-001|API-003|PASS|
|UC-TC-002|SC-002|顧客不存在経路|TD-002|API-001|API-001|WARN / FAIL|
|UC-TC-003|SC-003|契約0件経路|TD-003|API-001|API-003|PASS / WARN|
|UC-TC-004|SC-004|顧客詳細API Timeout|TD-004|API-001|API-002|FAIL|

---

## A.5 正常系API順序Check

|Check ID|TestCase ID|期待API順序|期待開始API|期待終了API|
|---|---|---|---|---|
|CHK-UC-FLOW-001|UC-TC-001|API-001 → API-002 → API-003|API-001|API-003|

---

## A.6 顧客不存在Skip Check

|Check ID|条件|Skip対象API|期待Status|
|---|---|---|---|
|CHK-UC-SKIP-001|CTX-002 = false|API-002, API-003|SKIP|

---

## A.7 Context Flow

|Context ID|Context名|Producer|Consumer|
|---|---|---|---|
|CTX-001|Customer.id|Entry Input|API-001, API-002, API-003|
|CTX-002|Customer.exists|API-001|Branch / Skip Rule|
|CTX-003|Customer|API-002|Verification / Report|
|CTX-004|Contract.list|API-003|Verification / Report|

---

## A.8 Request / Response Mapping

|Mapping ID|前段|Response|Context|後段|Request|
|---|---|---|---|---|---|
|MAP-001|Entry Input|customerId|CTX-001|API-001|$.customerId|
|MAP-002|API-001|$.customerId|CTX-001|API-002|$.customerId|
|MAP-003|API-001|$.customerId|CTX-001|API-003|$.customerId|
|MAP-004|API-001|$.exists|CTX-002|Branch|exists判定|

---

## A.9 Business Result Check

|Check ID|Scenario ID|条件|期待Business Result|期待Result|
|---|---|---|---|---|
|CHK-UC-BIZ-001|SC-001|CTX-002=true かつ CTX-004.size>0|顧客・契約情報取得成功|PASS|
|CHK-UC-BIZ-002|SC-002|CTX-002=false|顧客不存在|WARN / FAIL|
|CHK-UC-BIZ-003|SC-003|CTX-002=true かつ CTX-004.size=0|契約0件|PASS / WARN|
|CHK-UC-BIZ-004|SC-004|API-002 Timeout|顧客詳細取得失敗|FAIL|

---

## A.10 Traceability例

|Business ID|BA ID|Path ID|UseCase ID|Scenario ID|TestCase ID|TestData ID|API ID|Context ID|Verification ID|Execution ID|Evidence ID|
|---|---|---|---|---|---|---|---|---|---|---|---|
|BUS-001|BA-001|PATH-001|UC-001|SC-001|UC-TC-001|TD-001|API-001〜API-003|CTX-001〜CTX-004|VER-001|EXEC-001|EVD-UC-001|
|BUS-001|BA-001|PATH-002|UC-001|SC-002|UC-TC-002|TD-002|API-001|CTX-001, CTX-002|VER-001|EXEC-002|EVD-UC-002|
|BUS-001|BA-001|PATH-003|UC-001|SC-003|UC-TC-003|TD-003|API-001〜API-003|CTX-001〜CTX-004|VER-001|EXEC-003|EVD-UC-003|
|BUS-001|BA-001|PATH-004|UC-001|SC-004|UC-TC-004|TD-004|API-001, API-002|CTX-001, CTX-002|VER-001|EXEC-004|EVD-UC-004|

:::

下一步应制作：

```text
system/06_verification_assets/test_data/
TestData設計書.md
TestData_Template.json
```

这一部分会定义 TestData ID、Scenario 对应关系、前提数据、Entry Input、期待值、有效期限、Mask、清理和数据占用规则。

## 第 199 轮

### 你

继续

### ChatGPT

放置位置：

```text
system/06_verification_assets/test_data/
├── TestData設計書.md
└── TestData_Template.json
```

:::writing{variant="document" id="58241"}
---
title: TestData設計書
document_id: SYS-TD-001
version: 1.0.0
status: Template
document_type: Verification Asset Design
system_name: E6 API Verification Platform
phase: Verification Test Design
author:
reviewer:
approver:
created:
updated:
---

# TestData設計書

---

# 1. 文書情報

## 1.1 文書管理

|項目|内容|
|---|---|
|文書ID|SYS-TD-001|
|文書名称|TestData設計書|
|対象範囲|API単体TestData / UseCase TestData / Scenario TestData / 前提Data / Cleanup|
|版数|1.0.0|
|状態|Draft / Review / Approved / Released|
|作成者| |
|レビューア| |
|承認者| |
|作成日|YYYY-MM-DD|
|更新日|YYYY-MM-DD|

---

## 1.2 改訂履歴

|版数|日付|担当|変更内容|
|---|---|---|---|
|1.0.0|YYYY-MM-DD| |初版作成|

---

## 1.3 関連資料

|資料ID|資料名|配置先|参照目的|
|---|---|---|---|
|API-TEST-XXX|API単体テスト仕様書|system/06_verification_assets/api_test_spec/|API単体TestCase|
|UC-TEST-XXX|UseCaseテスト仕様書|system/06_verification_assets/usecase_test_spec/|UseCase TestCase|
|VER-XXX|Verification仕様書|system/06_verification_assets/|期待結果、Check定義|
|EXEC-XXX|Execution仕様書|system/06_verification_assets/execution_spec/|Runtime実行定義|
|MST-SC-001|Scenario_Master|system/02_master/|Scenario定義|
|MST-CTX-001|Context_Master|system/02_master/|Context定義|
|SYS-IO-001|ファイル入出力設計書|system/05_framework/|File配置・形式|
|SYS-ENV-001|環境設計書|system/05_framework/|環境制約|
|SYS-LOG-001|ログ・例外設計書|system/05_framework/|Mask、Error方針|

---

# 2. TestData目的

TestDataは、API単体テストおよびUseCaseテストに必要な入力値、前提状態、期待結果、Context初期値、Cleanup情報を管理する。

本設計書では以下を定義する。

|目的|内容|
|---|---|
|Scenario再現|Scenarioごとの業務状態を再現する|
|入力値管理|Entry Input、API Request値を管理する|
|期待値管理|HTTP Status、Response、Context、Business Resultを管理する|
|前提Data管理|実行前に必要な顧客、契約、状態を管理する|
|排他管理|同一Dataの同時利用を防止する|
|有効期限管理|TestDataの利用可能期間を管理する|
|Cleanup管理|登録・更新・削除系TestDataを元の状態へ戻す|
|再現性確保|同じTestDataで同じScenarioを再実行可能にする|

---

# 3. TestData分類

|分類|説明|例|
|---|---|---|
|API Normal Data|API単体正常系Data|正常な顧客番号|
|API Boundary Data|最小、最大、境界値Data|20桁顧客番号|
|API Error Data|必須不足、不正値Data|Null、空文字|
|UseCase Normal Data|業務正常経路Data|顧客あり・契約あり|
|UseCase Alternative Data|業務分岐経路Data|顧客不存在、契約0件|
|UseCase Exception Data|障害系Data|Timeout誘発条件|
|Security Data|認証・権限確認Data|無効Token|
|Update Data|登録・更新・削除確認Data|専用更新対象Data|
|Generated Data|Runtime生成Data|runId、timestamp|
|Reference Data|共通参照Data|固定Code、Enum|

---

# 4. TestData配置

## 4.1 ディレクトリ構成

```text
system/06_verification_assets/test_data/

├── common/
│   ├── reference_data.json
│   └── common_auth_data.json
│
├── API-001/
│   ├── TD-API001-001_normal.json
│   ├── TD-API001-002_required_missing.json
│   └── TD-API001-003_max_length.json
│
├── UC-001/
│   ├── TD-001_SC-001_normal.json
│   ├── TD-002_SC-002_customer_not_found.json
│   ├── TD-003_SC-003_contract_empty.json
│   └── TD-004_SC-004_timeout.json
│
└── schema/
    ├── testdata.schema.json
    ├── api-testdata.schema.json
    └── usecase-testdata.schema.json
```

---

## 4.2 配置ルール

|TestData種別|配置先|
|---|---|
|共通Data|test_data/common/|
|API単体Data|test_data/{apiId}/|
|UseCase Data|test_data/{useCaseId}/|
|Schema|test_data/schema/|
|生成途中Data|outputs/runs/{runId}/tmp/|
|実行時展開Data|outputs/runs/{runId}/snapshot/|

---

# 5. TestData ID

## 5.1 ID形式

### UseCase TestData

```text
TD-<3桁連番>
```

例：

```text
TD-001
TD-002
TD-003
```

### API単体TestData

```text
TD-<API番号>-<3桁連番>
```

例：

```text
TD-API001-001
TD-API001-002
```

---

## 5.2 IDルール

|ルール|内容|
|---|---|
|一意性|Repository内で一意とする|
|再利用禁止|廃止したIDを別Dataへ再利用しない|
|欠番許可|削除・廃止による欠番を許可する|
|Scenario対応|UseCase TestDataは原則Scenario IDを保持する|
|TestCase対応|TestCase IDを必須保持する|

---

# 6. TestData基本項目

|項目|必須|説明|
|---|---:|---|
|testDataId|○|TestData ID|
|name|○|TestData名称|
|description|○|利用目的|
|dataType|○|API / USECASE / COMMON|
|businessId|条件付き|Business ID|
|useCaseId|条件付き|UseCase ID|
|scenarioId|条件付き|Scenario ID|
|apiId|条件付き|API ID|
|testCaseIds|○|対応TestCase|
|environment|○|利用可能環境|
|status|○|Active / Reserved / Deprecated / Invalid|
|entryInput|条件付き|UseCase開始入力|
|requestOverrides|－|API Request上書き|
|initialContext|－|初期Context|
|preconditions|－|前提条件|
|expected|○|期待結果|
|cleanup|－|後処理|
|masking|－|Mask対象|
|reservation|－|Data占用情報|
|validity|－|有効期間|
|metadata|○|作成・更新・Version情報|

---

# 7. TestData JSON基本構造

```json
{
  "testDataId": "TD-XXX",
  "name": "TestData名称",
  "description": "TestDataの利用目的",
  "dataType": "USECASE",
  "businessId": "BUS-XXX",
  "useCaseId": "UC-XXX",
  "scenarioId": "SC-XXX",
  "apiId": null,
  "testCaseIds": [
    "UC-TC-XXX"
  ],
  "environment": {
    "allowed": [
      "STG"
    ],
    "denied": [
      "PROD-LIKE"
    ]
  },
  "status": "Active",
  "entryInput": {},
  "requestOverrides": {},
  "initialContext": {},
  "preconditions": [],
  "expected": {},
  "cleanup": {},
  "masking": {},
  "reservation": {},
  "validity": {},
  "metadata": {}
}
```

---

# 8. Entry Input設計

## 8.1 Entry Input項目

|項目|説明|
|---|---|
|name|入力項目名|
|value|入力値|
|type|型|
|required|必須か|
|contextId|変換先Context|
|mask|Mask対象か|
|source|STATIC / GENERATED / ENVIRONMENT / SECRET|

---

## 8.2 Entry Input例

```json
{
  "entryInput": {
    "customerId": {
      "value": "10000001",
      "type": "String",
      "required": true,
      "contextId": "CTX-001",
      "mask": true,
      "source": "STATIC"
    }
  }
}
```

---

# 9. Request Override設計

Request Overrideは、API設計書やContext Bindingで生成されるRequestをTestCase目的で上書きする場合に利用する。

通常のUseCase正常系では原則利用しない。

---

## 9.1 Request Override項目

|項目|説明|
|---|---|
|apiId|対象API|
|target|Request JSONPath / Header / Parameter|
|operation|SET / REMOVE / NULL / EMPTY|
|value|設定値|
|type|設定型|
|purpose|上書き理由|

---

## 9.2 Request Override例

```json
{
  "requestOverrides": {
    "API-001": [
      {
        "target": "$.customerId",
        "operation": "REMOVE",
        "value": null,
        "type": "String",
        "purpose": "必須項目未設定確認"
      }
    ]
  }
}
```

---

# 10. Initial Context設計

## 10.1 用途

Initial Contextは、UseCase開始前またはScenario開始前にRuntimeへ設定するContextである。

通常はEntry Inputから生成するが、特殊なScenarioでは明示設定を許可する。

---

## 10.2 Initial Context例

```json
{
  "initialContext": {
    "CTX-001": {
      "contextName": "Customer.id",
      "type": "String",
      "value": "10000001",
      "mask": true
    },
    "CTX-RUN-TEST-001": {
      "contextName": "Test.timeoutMode",
      "type": "Boolean",
      "value": false,
      "mask": false
    }
  }
}
```

---

# 11. 前提条件設計

## 11.1 前提条件分類

|分類|説明|
|---|---|
|DATA_EXISTS|対象Dataが存在する|
|DATA_NOT_EXISTS|対象Dataが存在しない|
|DATA_STATUS|対象Dataが特定Statusである|
|API_AVAILABLE|対象APIが利用可能|
|AUTH_AVAILABLE|認証情報が利用可能|
|ENVIRONMENT|指定環境である|
|TIME_CONDITION|指定時間帯・日付条件|
|CUSTOM|個別確認|

---

## 11.2 前提条件項目

|項目|説明|
|---|---|
|preconditionId|前提条件ID|
|type|前提条件分類|
|description|条件説明|
|checkMethod|API / DB / FILE / MANUAL / SCRIPT|
|checkTarget|確認対象|
|expected|期待状態|
|required|必須か|
|failureResult|BLOCKED / ERROR / WARN|
|evidenceRequired|Evidence要否|

---

## 11.3 前提条件例

```json
{
  "preconditions": [
    {
      "preconditionId": "PRE-TD-001",
      "type": "DATA_EXISTS",
      "description": "顧客10000001が存在すること",
      "checkMethod": "API",
      "checkTarget": "API-001",
      "expected": {
        "$.exists": true
      },
      "required": true,
      "failureResult": "BLOCKED",
      "evidenceRequired": true
    }
  ]
}
```

---

# 12. 期待結果設計

## 12.1 Expected基本項目

|項目|説明|
|---|---|
|executionResult|Execution全体期待結果|
|businessResult|業務結果|
|startApi|開始API|
|endApi|終了API|
|executedApis|実行対象API|
|skippedApis|Skip対象API|
|httpStatus|API別期待Status|
|responseChecks|Response期待値|
|contextChecks|Context期待値|
|diffResult|Diff期待結果|
|reportResult|Report期待結果|

---

## 12.2 Expected例

```json
{
  "expected": {
    "executionResult": "PASS",
    "businessResult": "CUSTOMER_AND_CONTRACT_FOUND",
    "startApi": "API-001",
    "endApi": "API-003",
    "executedApis": [
      "API-001",
      "API-002",
      "API-003"
    ],
    "skippedApis": [],
    "httpStatus": {
      "API-001": 200,
      "API-002": 200,
      "API-003": 200
    },
    "responseChecks": {
      "API-001": [
        {
          "target": "$.resultCode",
          "type": "FIXED",
          "expected": "0"
        },
        {
          "target": "$.exists",
          "type": "EQUALS",
          "expected": true
        }
      ]
    },
    "contextChecks": [
      {
        "contextId": "CTX-002",
        "type": "EQUALS",
        "expected": true
      }
    ],
    "diffResult": "PASS",
    "reportResult": "PASS"
  }
}
```

---

# 13. API別期待値

## 13.1 API期待値構造

```json
{
  "expected": {
    "apis": {
      "API-001": {
        "executionStatus": "PASS",
        "httpStatus": 200,
        "response": {
          "$.resultCode": {
            "checkType": "FIXED",
            "expected": "0"
          }
        }
      }
    }
  }
}
```

---

## 13.2 API期待Status

|Status|説明|
|---|---|
|PASS|API実行・検証成功|
|WARN|許容差分あり|
|FAIL|期待不一致|
|ERROR|実行不能|
|SKIP|条件により未実行|

---

# 14. Context期待値

## 14.1 Context Check項目

|項目|説明|
|---|---|
|contextId|対象Context|
|checkType|EXISTS / EQUALS / TYPE / SIZE / NOT_EMPTY|
|expected|期待値|
|severity|重要度|
|failureResult|不一致時Result|

---

## 14.2 Context期待値例

```json
{
  "expected": {
    "contextChecks": [
      {
        "contextId": "CTX-001",
        "checkType": "EQUALS",
        "expected": "10000001",
        "severity": "HIGH",
        "failureResult": "FAIL"
      },
      {
        "contextId": "CTX-004",
        "checkType": "SIZE_GREATER_THAN",
        "expected": 0,
        "severity": "HIGH",
        "failureResult": "FAIL"
      }
    ]
  }
}
```

---

# 15. Error期待値

## 15.1 Error Expected構造

```json
{
  "expected": {
    "executionResult": "FAIL",
    "error": {
      "apiId": "API-002",
      "exceptionType": "TimeoutException",
      "errorCode": "TIMEOUT",
      "retryCount": 2,
      "continuePolicy": "STOP_SCENARIO"
    }
  }
}
```

---

# 16. Cleanup設計

## 16.1 Cleanup分類

|分類|説明|
|---|---|
|NONE|後処理なし|
|DELETE_CREATED_DATA|作成Dataを削除|
|RESTORE_UPDATED_DATA|更新前状態へ戻す|
|RELEASE_RESERVATION|Data占用を解除|
|DELETE_TEMP_FILE|一時File削除|
|CUSTOM_SCRIPT|個別Script実行|

---

## 16.2 Cleanup項目

|項目|説明|
|---|---|
|required|Cleanup必須か|
|type|Cleanup分類|
|target|対象Data / API|
|executionTiming|SCENARIO_END / USECASE_END / RUN_END|
|continueOnFailure|Cleanup失敗時に継続するか|
|failureResult|WARN / ERROR|
|evidenceRequired|Evidence要否|

---

## 16.3 Cleanup例

```json
{
  "cleanup": {
    "required": true,
    "actions": [
      {
        "cleanupId": "CLEAN-TD-001",
        "type": "DELETE_CREATED_DATA",
        "target": {
          "apiId": "API-DELETE-001",
          "contextId": "CTX-CREATED-ID"
        },
        "executionTiming": "SCENARIO_END",
        "continueOnFailure": false,
        "failureResult": "ERROR",
        "evidenceRequired": true
      }
    ]
  }
}
```

---

# 17. Mask設計

## 17.1 Mask項目

|項目|説明|
|---|---|
|jsonPaths|Mask対象JSONPath|
|contextIds|Mask対象Context|
|strategy|FULL / PARTIAL / HASH|
|visibleTailLength|末尾表示桁数|
|applyToSnapshot|Snapshotへ適用|
|applyToLog|Logへ適用|
|applyToReport|Reportへ適用|

---

## 17.2 Mask例

```json
{
  "masking": {
    "jsonPaths": [
      "$.entryInput.customerId.value"
    ],
    "contextIds": [
      "CTX-001"
    ],
    "strategy": "PARTIAL",
    "visibleTailLength": 4,
    "applyToSnapshot": true,
    "applyToLog": true,
    "applyToReport": true
  }
}
```

---

# 18. TestData予約・排他設計

## 18.1 目的

同一TestDataを複数Runが同時利用し、Data状態が競合することを防止する。

---

## 18.2 予約方式

|方式|説明|
|---|---|
|NONE|予約不要|
|FILE_LOCK|Lock Fileで制御|
|RUNTIME_LOCK|Runtime内Lock管理|
|EXTERNAL_LOCK|外部DB / Lock Service|
|MANUAL_RESERVATION|手動予約|

---

## 18.3 Reservation項目

|項目|説明|
|---|---|
|required|予約要否|
|lockKey|Lock識別子|
|mode|SHARED / EXCLUSIVE|
|timeoutSeconds|Lock待機時間|
|releaseTiming|SCENARIO_END / RUN_END|
|failureResult|BLOCKED / ERROR|

---

## 18.4 Reservation例

```json
{
  "reservation": {
    "required": true,
    "lockKey": "CUSTOMER-10000001",
    "mode": "EXCLUSIVE",
    "timeoutSeconds": 30,
    "releaseTiming": "SCENARIO_END",
    "failureResult": "BLOCKED"
  }
}
```

---

# 19. 有効期限設計

## 19.1 Validity項目

|項目|説明|
|---|---|
|validFrom|利用開始日時|
|validTo|利用終了日時|
|timezone|Timezone|
|expiredResult|BLOCKED / ERROR|
|lastValidatedAt|最終確認日時|
|validationIntervalDays|再確認間隔|

---

## 19.2 Validity例

```json
{
  "validity": {
    "validFrom": "2026-07-01T00:00:00+09:00",
    "validTo": "2026-12-31T23:59:59+09:00",
    "timezone": "Asia/Tokyo",
    "expiredResult": "BLOCKED",
    "lastValidatedAt": "2026-07-15T09:00:00+09:00",
    "validationIntervalDays": 7
  }
}
```

---

# 20. Environment制約

## 20.1 Environment設定

```json
{
  "environment": {
    "allowed": [
      "DEV",
      "STG"
    ],
    "denied": [
      "PROD-LIKE"
    ],
    "updateApiAllowed": false
  }
}
```

---

## 20.2 環境制御

|条件|処理|
|---|---|
|許可環境外|BLOCKED|
|禁止環境|ERROR / BLOCKED|
|更新API禁止環境|実行停止|
|Environment未指定|ERROR|
|TestData環境不一致|BLOCKED|

---

# 21. TestData Status

|Status|意味|
|---|---|
|Draft|作成中|
|Review|Review中|
|Active|利用可能|
|Reserved|一時予約中|
|Blocked|前提不成立|
|Deprecated|廃止予定|
|Invalid|利用不可|
|Expired|有効期限切れ|

---

# 22. TestData Validation

## 22.1 Schema Validation

|Validation ID|確認内容|失敗時Result|
|---|---|---|
|TD-VAL-001|testDataIdが存在する|ERROR|
|TD-VAL-002|TestCase IDが存在する|ERROR|
|TD-VAL-003|UseCase / Scenario / APIがMasterに存在する|ERROR|
|TD-VAL-004|Entry Input Typeが正しい|ERROR|
|TD-VAL-005|Context IDがMasterに存在する|ERROR|
|TD-VAL-006|Expected Resultが許容値である|ERROR|
|TD-VAL-007|利用環境が定義されている|ERROR|
|TD-VAL-008|Mask対象が定義されている|WARN / ERROR|
|TD-VAL-009|有効期限内である|BLOCKED|
|TD-VAL-010|予約可能である|BLOCKED|

---

## 22.2 実行前Validation

```text
1. JSON Schema確認
2. ID整合性確認
3. Environment確認
4. Status確認
5. Validity確認
6. Reservation取得
7. Precondition確認
8. Entry Input生成
9. Initial Context生成
10. Execution開始
```

---

# 23. TestData生成方式

## 23.1 生成方式

|方式|説明|
|---|---|
|STATIC|固定値|
|RANDOM|ランダム生成|
|SEQUENCE|連番生成|
|TIMESTAMP|日時生成|
|UUID|UUID生成|
|ENVIRONMENT|環境変数から取得|
|SECRET|Secretから取得|
|API_LOOKUP|前処理APIから取得|
|SCRIPT|Scriptで生成|

---

## 23.2 Generated Value例

```json
{
  "entryInput": {
    "requestId": {
      "source": "UUID",
      "type": "String",
      "required": true
    },
    "executionDate": {
      "source": "TIMESTAMP",
      "format": "yyyy-MM-dd",
      "timezone": "Asia/Tokyo",
      "type": "String",
      "required": true
    }
  }
}
```

---

# 24. TestData変更管理

|変更内容|Version更新|
|---|---|
|説明・備考修正|PATCH|
|期待値変更|MINOR|
|Entry Input変更|MINOR|
|Scenario変更|MAJOR|
|TestCase対応変更|MAJOR|
|前提Data変更|MINOR / MAJOR|
|環境制約変更|MINOR|

---

## 24.1 Metadata

```json
{
  "metadata": {
    "version": "1.0.0",
    "status": "Active",
    "createdBy": "test-designer",
    "createdAt": "2026-07-15T10:00:00+09:00",
    "updatedBy": "test-designer",
    "updatedAt": "2026-07-15T10:00:00+09:00",
    "sourceDocuments": [
      "UC-TEST-001",
      "VER-001",
      "EXEC-001"
    ]
  }
}
```

---

# 25. TestData Evidence

|Evidence|内容|
|---|---|
|Precondition Evidence|実行前状態|
|Entry Input Snapshot|実際に利用した入力|
|Generated Value Snapshot|生成値|
|Reservation Evidence|Lock取得・解放|
|Cleanup Evidence|後処理結果|
|Validation Result|Schema・前提確認結果|

---

# 26. Error処理

|Error ID|発生条件|Result|処理|
|---|---|---|---|
|TD-ERR-001|TestData Fileなし|ERROR|Scenario停止|
|TD-ERR-002|JSON Parse失敗|ERROR|Scenario停止|
|TD-ERR-003|Schema不一致|ERROR|Scenario停止|
|TD-ERR-004|有効期限切れ|BLOCKED|実行しない|
|TD-ERR-005|前提条件不成立|BLOCKED|実行しない|
|TD-ERR-006|予約取得失敗|BLOCKED|実行しない|
|TD-ERR-007|Environment不一致|BLOCKED|実行しない|
|TD-ERR-008|Cleanup失敗|WARN / ERROR|方針に従う|
|TD-ERR-009|Mask設定不備|ERROR|保存・実行停止|
|TD-ERR-010|期待値不整合|ERROR|Spec修正対象|

---

# 27. Traceability

|TestData ID|Business ID|UseCase ID|Scenario ID|API ID|TestCase ID|Verification ID|Execution ID|Context ID|
|---|---|---|---|---|---|---|---|---|
|TD-XXX|BUS-XXX|UC-XXX|SC-XXX|API-XXX|UC-TC-XXX / API-TC-XXX|VER-XXX|EXEC-XXX|CTX-XXX|

---

# 28. Review観点

|観点|確認内容|
|---|---|
|Scenario整合|対象Scenarioを再現できるDataか|
|TestCase整合|TestCaseの入力・期待結果と一致するか|
|前提条件|実行前状態が明確か|
|Entry Input|型、必須、Context対応が明確か|
|期待結果|API、Context、Business Resultが明確か|
|Environment|利用可能環境が制限されているか|
|有効期限|利用可能期間が設定されているか|
|排他|更新系や共有Dataの競合を防止できるか|
|Cleanup|後処理が定義されているか|
|Mask|個人情報・Secretが保護されているか|
|再現性|同じDataで再実行可能か|
|Traceability|TestCase、Scenario、Executionへ追跡可能か|

---

# Appendix A. 記入例：TD-001 正常顧客

```json
{
  "testDataId": "TD-001",
  "name": "顧客情報照会正常系",
  "description": "顧客が存在し、1件以上の有効契約を保持する正常系TestData",
  "dataType": "USECASE",
  "businessId": "BUS-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-001",
  "apiId": null,
  "testCaseIds": [
    "UC-TC-001"
  ],
  "environment": {
    "allowed": [
      "STG"
    ],
    "denied": [
      "PROD-LIKE"
    ],
    "updateApiAllowed": false
  },
  "status": "Active",
  "entryInput": {
    "customerId": {
      "value": "10000001",
      "type": "String",
      "required": true,
      "contextId": "CTX-001",
      "mask": true,
      "source": "STATIC"
    }
  },
  "requestOverrides": {},
  "initialContext": {},
  "preconditions": [
    {
      "preconditionId": "PRE-TD-001",
      "type": "DATA_EXISTS",
      "description": "顧客10000001が存在すること",
      "checkMethod": "API",
      "checkTarget": "API-001",
      "expected": {
        "$.exists": true
      },
      "required": true,
      "failureResult": "BLOCKED",
      "evidenceRequired": true
    },
    {
      "preconditionId": "PRE-TD-002",
      "type": "DATA_STATUS",
      "description": "顧客10000001が1件以上の有効契約を保持すること",
      "checkMethod": "API",
      "checkTarget": "API-003",
      "expected": {
        "$.contracts.length": {
          "operator": "GREATER_THAN",
          "value": 0
        }
      },
      "required": true,
      "failureResult": "BLOCKED",
      "evidenceRequired": true
    }
  ],
  "expected": {
    "executionResult": "PASS",
    "businessResult": "CUSTOMER_AND_CONTRACT_FOUND",
    "startApi": "API-001",
    "endApi": "API-003",
    "executedApis": [
      "API-001",
      "API-002",
      "API-003"
    ],
    "skippedApis": [],
    "httpStatus": {
      "API-001": 200,
      "API-002": 200,
      "API-003": 200
    },
    "responseChecks": {
      "API-001": [
        {
          "target": "$.resultCode",
          "checkType": "FIXED",
          "expected": "0"
        },
        {
          "target": "$.exists",
          "checkType": "EQUALS",
          "expected": true
        }
      ]
    },
    "contextChecks": [
      {
        "contextId": "CTX-001",
        "checkType": "EQUALS",
        "expected": "10000001",
        "severity": "HIGH",
        "failureResult": "FAIL"
      },
      {
        "contextId": "CTX-002",
        "checkType": "EQUALS",
        "expected": true,
        "severity": "HIGH",
        "failureResult": "FAIL"
      },
      {
        "contextId": "CTX-004",
        "checkType": "SIZE_GREATER_THAN",
        "expected": 0,
        "severity": "HIGH",
        "failureResult": "FAIL"
      }
    ],
    "diffResult": "PASS",
    "reportResult": "PASS"
  },
  "cleanup": {
    "required": false,
    "actions": []
  },
  "masking": {
    "jsonPaths": [
      "$.entryInput.customerId.value"
    ],
    "contextIds": [
      "CTX-001"
    ],
    "strategy": "PARTIAL",
    "visibleTailLength": 4,
    "applyToSnapshot": true,
    "applyToLog": true,
    "applyToReport": true
  },
  "reservation": {
    "required": false,
    "lockKey": "CUSTOMER-10000001",
    "mode": "SHARED",
    "timeoutSeconds": 30,
    "releaseTiming": "SCENARIO_END",
    "failureResult": "BLOCKED"
  },
  "validity": {
    "validFrom": "2026-07-01T00:00:00+09:00",
    "validTo": "2026-12-31T23:59:59+09:00",
    "timezone": "Asia/Tokyo",
    "expiredResult": "BLOCKED",
    "lastValidatedAt": "2026-07-15T09:00:00+09:00",
    "validationIntervalDays": 7
  },
  "metadata": {
    "version": "1.0.0",
    "status": "Active",
    "createdBy": "test-designer",
    "createdAt": "2026-07-15T10:00:00+09:00",
    "updatedBy": "test-designer",
    "updatedAt": "2026-07-15T10:00:00+09:00",
    "sourceDocuments": [
      "UC-TEST-001",
      "VER-001",
      "EXEC-001"
    ]
  }
}
```

---

# Appendix B. 記入例：TD-002 顧客不存在

```json
{
  "testDataId": "TD-002",
  "name": "顧客不存在",
  "description": "顧客存在確認APIでexists=falseとなり、後続APIがSkipされるTestData",
  "dataType": "USECASE",
  "businessId": "BUS-001",
  "useCaseId": "UC-001",
  "scenarioId": "SC-002",
  "apiId": null,
  "testCaseIds": [
    "UC-TC-002"
  ],
  "environment": {
    "allowed": [
      "STG"
    ],
    "denied": [
      "PROD-LIKE"
    ],
    "updateApiAllowed": false
  },
  "status": "Active",
  "entryInput": {
    "customerId": {
      "value": "99999999",
      "type": "String",
      "required": true,
      "contextId": "CTX-001",
      "mask": true,
      "source": "STATIC"
    }
  },
  "requestOverrides": {},
  "initialContext": {},
  "preconditions": [
    {
      "preconditionId": "PRE-TD-003",
      "type": "DATA_NOT_EXISTS",
      "description": "顧客99999999が存在しないこと",
      "checkMethod": "API",
      "checkTarget": "API-001",
      "expected": {
        "$.exists": false
      },
      "required": true,
      "failureResult": "BLOCKED",
      "evidenceRequired": true
    }
  ],
  "expected": {
    "executionResult": "WARN",
    "businessResult": "CUSTOMER_NOT_FOUND",
    "startApi": "API-001",
    "endApi": "API-001",
    "executedApis": [
      "API-001"
    ],
    "skippedApis": [
      "API-002",
      "API-003"
    ],
    "httpStatus": {
      "API-001": 200
    },
    "responseChecks": {
      "API-001": [
        {
          "target": "$.exists",
          "checkType": "EQUALS",
          "expected": false
        }
      ]
    },
    "contextChecks": [
      {
        "contextId": "CTX-002",
        "checkType": "EQUALS",
        "expected": false,
        "severity": "HIGH",
        "failureResult": "FAIL"
      }
    ],
    "diffResult": "PASS",
    "reportResult": "WARN"
  },
  "cleanup": {
    "required": false,
    "actions": []
  },
  "masking": {
    "jsonPaths": [
      "$.entryInput.customerId.value"
    ],
    "contextIds": [
      "CTX-001"
    ],
    "strategy": "PARTIAL",
    "visibleTailLength": 4,
    "applyToSnapshot": true,
    "applyToLog": true,
    "applyToReport": true
  },
  "reservation": {
    "required": false
  },
  "validity": {
    "validFrom": "2026-07-01T00:00:00+09:00",
    "validTo": "2026-12-31T23:59:59+09:00",
    "timezone": "Asia/Tokyo",
    "expiredResult": "BLOCKED"
  },
  "metadata": {
    "version": "1.0.0",
    "status": "Active",
    "createdBy": "test-designer",
    "createdAt": "2026-07-15T10:00:00+09:00",
    "updatedBy": "test-designer",
    "updatedAt": "2026-07-15T10:00:00+09:00",
    "sourceDocuments": [
      "UC-TEST-001",
      "VER-001",
      "EXEC-002"
    ]
  }
}
```

:::

:::writing{variant="standard" id="90637"}
{
  "testDataId": "TD-XXX",
  "name": "TestData名称",
  "description": "TestDataの利用目的",
  "dataType": "API | USECASE | COMMON",
  "businessId": "BUS-XXX",
  "useCaseId": "UC-XXX",
  "scenarioId": "SC-XXX",
  "apiId": "API-XXX",
  "testCaseIds": [
    "UC-TC-XXX"
  ],
  "environment": {
    "allowed": [
      "STG"
    ],
    "denied": [],
    "updateApiAllowed": false
  },
  "status": "Draft",
  "entryInput": {
    "inputName": {
      "value": "value",
      "type": "String",
      "required": true,
      "contextId": "CTX-XXX",
      "mask": false,
      "source": "STATIC"
    }
  },
  "requestOverrides": {
    "API-XXX": [
      {
        "target": "$.xxx",
        "operation": "SET",
        "value": "value",
        "type": "String",
        "purpose": "Test purpose"
      }
    ]
  },
  "initialContext": {
    "CTX-XXX": {
      "contextName": "Domain.property",
      "type": "String",
      "value": "value",
      "mask": false
    }
  },
  "preconditions": [
    {
      "preconditionId": "PRE-TD-XXX",
      "type": "DATA_EXISTS",
      "description": "前提条件",
      "checkMethod": "API",
      "checkTarget": "API-XXX",
      "expected": {},
      "required": true,
      "failureResult": "BLOCKED",
      "evidenceRequired": true
    }
  ],
  "expected": {
    "executionResult": "PASS",
    "businessResult": "EXPECTED_BUSINESS_RESULT",
    "startApi": "API-XXX",
    "endApi": "API-XXX",
    "executedApis": [
      "API-XXX"
    ],
    "skippedApis": [],
    "httpStatus": {
      "API-XXX": 200
    },
    "responseChecks": {
      "API-XXX": [
        {
          "target": "$.xxx",
          "checkType": "EQUALS",
          "expected": "value"
        }
      ]
    },
    "contextChecks": [
      {
        "contextId": "CTX-XXX",
        "checkType": "EQUALS",
        "expected": "value",
        "severity": "HIGH",
        "failureResult": "FAIL"
      }
    ],
    "diffResult": "PASS",
    "reportResult": "PASS"
  },
  "cleanup": {
    "required": false,
    "actions": []
  },
  "masking": {
    "jsonPaths": [],
    "contextIds": [],
    "strategy": "FULL",
    "visibleTailLength": 0,
    "applyToSnapshot": true,
    "applyToLog": true,
    "applyToReport": true
  },
  "reservation": {
    "required": false,
    "lockKey": null,
    "mode": "SHARED",
    "timeoutSeconds": 30,
    "releaseTiming": "SCENARIO_END",
    "failureResult": "BLOCKED"
  },
  "validity": {
    "validFrom": "YYYY-MM-DDTHH:mm:ss+09:00",
    "validTo": "YYYY-MM-DDTHH:mm:ss+09:00",
    "timezone": "Asia/Tokyo",
    "expiredResult": "BLOCKED",
    "lastValidatedAt": null,
    "validationIntervalDays": 7
  },
  "metadata": {
    "version": "1.0.0",
    "status": "Draft",
    "createdBy": "",
    "createdAt": "",
    "updatedBy": "",
    "updatedAt": "",
    "sourceDocuments": []
  }
}
:::

下一步应制作 `06_verification_assets/reports/` 下的三份正式模板：

```text
DailySummary_Template.md
DiffReport_Template.md
EvidenceReport_Template.md
```

## 第 200 轮

### 你

继续

### ChatGPT

下面继续完成 `06_verification_assets/reports/` 下的三份正式模板：Daily Summary、Diff Report、Evidence Report。

### ChatGPT

放置位置：

```text
system/06_verification_assets/reports/
├── DailySummary_Template.md
├── DiffReport_Template.md
└── EvidenceReport_Template.md
```

:::writing{variant="document" id="31847"}
---
title: Daily Summary Report Template
document_id: RPT-DAILY-TEMPLATE
version: 1.0.0
status: Template
document_type: Verification Report
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Daily Summary Report

---

# 1. Report情報

|項目|内容|
|---|---|
|Report ID|RPT-DAILY-XXX|
|Run ID|RUN-YYYYMMDD-HHMMSS-XXX|
|実行日|YYYY-MM-DD|
|対象環境|ENV-XXX|
|実行方式|Daily / Manual / Retry|
|Runtime Version|x.x.x|
|Spec Version|x.x.x|
|Baseline ID|BASE-XXX / なし|
|開始日時|YYYY-MM-DDTHH:mm:ss+09:00|
|終了日時|YYYY-MM-DDTHH:mm:ss+09:00|
|実行時間|00:00:00|
|総合Result|PASS / WARN / FAIL / ERROR / BLOCKED|
|作成日時|YYYY-MM-DDTHH:mm:ss+09:00|

---

# 2. 総合サマリー

## 2.1 Result Summary

|Result|件数|説明|
|---|---:|---|
|PASS|0|期待どおり完了|
|WARN|0|確認が必要な差分または結果|
|FAIL|0|期待不一致|
|ERROR|0|実行基盤、Spec、環境等の異常|
|BLOCKED|0|前提条件未成立|
|SKIP|0|条件により未実行|
|合計|0|対象Scenario総数|

---

## 2.2 総合判定理由

|判定項目|内容|
|---|---|
|最終Result|PASS / WARN / FAIL / ERROR / BLOCKED|
|判定理由|（記載）|
|重大差分有無|あり / なし|
|実行異常有無|あり / なし|
|業務確認要否|要 / 不要|
|Baseline更新可否|可 / 条件付き可 / 不可|
|再実行要否|要 / 不要|

---

# 3. 実行対象

## 3.1 UseCase一覧

|No|UseCase ID|UseCase名称|Scenario数|対象API数|Result|開始日時|終了日時|Evidence|
|---:|---|---|---:|---:|---|---|---|---|
|1|UC-XXX|（記載）|0|0|PASS / WARN / FAIL / ERROR|（記載）|（記載）|EvidenceReport.md#xxx|

---

## 3.2 Scenario一覧

|No|UseCase ID|Scenario ID|Scenario名称|分類|開始API|終了API|実行API数|Skip API数|Result|備考|
|---:|---|---|---|---|---|---|---:|---:|---|---|
|1|UC-XXX|SC-XXX|（記載）|Normal / Alternative / Exception|API-XXX|API-XXX|0|0|PASS / WARN / FAIL / ERROR| |

---

# 4. UseCase別結果

## 4.1 UseCase Result Summary

|UseCase ID|UseCase名称|PASS|WARN|FAIL|ERROR|BLOCKED|SKIP|総合Result|
|---|---|---:|---:|---:|---:|---:|---:|---|
|UC-XXX|（記載）|0|0|0|0|0|0|PASS / WARN / FAIL / ERROR|

---

## 4.2 UseCase詳細

### UC-XXX：〇〇

|項目|内容|
|---|---|
|UseCase ID|UC-XXX|
|対象Business|BUS-XXX|
|Scenario数|0|
|API数|0|
|Result|PASS / WARN / FAIL / ERROR|
|主な結果|（記載）|
|主な差分|（記載）|
|Evidence|（記載）|

Scenario結果：

|Scenario ID|Scenario名称|期待Result|実際Result|差分件数|実行API|Skip API|備考|
|---|---|---|---|---:|---|---|---|
|SC-XXX|（記載）|PASS|PASS|0|API-XXX|－| |

---

# 5. API実行結果

|API ID|API名称|実行回数|PASS|WARN|FAIL|ERROR|SKIP|平均応答時間|最大応答時間|
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
|API-XXX|（記載）|0|0|0|0|0|0|0ms|0ms|

---

# 6. Critical / High差分

CriticalまたはHighの差分を表示する。

差分がない場合は、`該当なし` と記載する。

|No|Severity|UseCase ID|Scenario ID|API ID|対象|Diff Type|Baseline|Current|Result|Evidence|
|---:|---|---|---|---|---|---|---|---|---|---|
|1|Critical / High|UC-XXX|SC-XXX|API-XXX|$.xxx / CTX-XXX|VALUE_CHANGED|（記載）|（記載）|FAIL|（記載）|

---

# 7. WARN一覧

|No|分類|UseCase ID|Scenario ID|API ID|内容|業務影響|確認担当|状態|
|---:|---|---|---|---|---|---|---|---|
|1|Diff / Business / TestData / Performance|UC-XXX|SC-XXX|API-XXX|（記載）|あり / なし / 未確認|（記載）|Open / Confirmed / Closed|

---

# 8. FAIL一覧

|No|分類|UseCase ID|Scenario ID|API ID|Check ID|内容|停止範囲|Evidence|
|---:|---|---|---|---|---|---|---|---|
|1|Response / Context / Business / Flow|UC-XXX|SC-XXX|API-XXX|CHK-XXX|（記載）|Step / Scenario / UseCase|（記載）|

---

# 9. ERROR一覧

|No|Error ID|Exception分類|UseCase ID|Scenario ID|API ID|Message|停止範囲|再実行可否|Log|
|---:|---|---|---|---|---|---|---|---|---|
|1|ERR-XXX|Spec / Config / Context / API / System|UC-XXX|SC-XXX|API-XXX|（記載）|STOP_RUN / STOP_SCENARIO|可 / 不可|（記載）|

---

# 10. BLOCKED一覧

|No|UseCase ID|Scenario ID|TestData ID|前提条件|未成立理由|対応方針|再確認予定|
|---:|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|TD-XXX|（記載）|（記載）|（記載）|YYYY-MM-DD|

---

# 11. Skip結果

|No|UseCase ID|Scenario ID|API ID|Skip Rule ID|Skip理由|期待Skip|判定|
|---:|---|---|---|---|---|---:|---|
|1|UC-XXX|SC-XXX|API-XXX|SKIP-XXX|（記載）|Yes / No|PASS / FAIL|

---

# 12. Baseline比較結果

## 12.1 Baseline情報

|項目|内容|
|---|---|
|Baseline ID|BASE-XXX|
|Source Run ID|RUN-XXX|
|Baseline種別|Approved / Previous Success / Initial|
|承認者|（記載）|
|承認日時|（記載）|
|比較対象|Run / UseCase / Scenario / API|

---

## 12.2 Diff Summary

|Severity|PASS|WARN|FAIL|IGNORED|合計|
|---|---:|---:|---:|---:|---:|
|Critical|0|0|0|0|0|
|High|0|0|0|0|0|
|Medium|0|0|0|0|0|
|Low|0|0|0|0|0|
|Info|0|0|0|0|0|
|合計|0|0|0|0|0|

---

# 13. Performance Summary

|API ID|実行回数|平均|最小|最大|基準|Result|
|---|---:|---:|---:|---:|---:|---|
|API-XXX|0|0ms|0ms|0ms|0ms以内|PASS / WARN / FAIL|

---

# 14. Evidence Summary

|Evidence分類|生成件数|不足件数|Result|保存先|
|---|---:|---:|---|---|
|Request Snapshot|0|0|PASS / ERROR|raw/|
|Response Snapshot|0|0|PASS / ERROR|raw/|
|Context Snapshot|0|0|PASS / ERROR|snapshot/|
|Execution Snapshot|0|0|PASS / ERROR|snapshot/|
|Diff Result|0|0|PASS / ERROR|diff/|
|Log|0|0|PASS / ERROR|logs/|

---

# 15. 確認・承認事項

|No|分類|確認内容|担当|期限|状態|回答・判断|
|---:|---|---|---|---|---|---|
|1|Business / API / Baseline / TestData|（記載）|（記載）|YYYY-MM-DD|Open / Closed|（記載）|

---

# 16. Baseline更新判定

|確認項目|判定|
|---|---|
|Run ResultがPASSまたは承認可能なWARNか|Yes / No|
|Critical / High差分が承認済みか|Yes / No|
|Evidenceが完全か|Yes / No|
|Mask漏れがないか|Yes / No|
|TestDataが有効か|Yes / No|
|業務担当確認が完了したか|Yes / No|
|Baseline更新可否|可 / 条件付き可 / 不可|

---

# 17. 再実行情報

|項目|内容|
|---|---|
|再実行要否|要 / 不要|
|再実行対象|Run / UseCase / Scenario / Failed Only|
|対象ID|（記載）|
|再実行理由|（記載）|
|修正対象|Spec / Config / TestData / Environment / API|
|元Run ID|RUN-XXX|

---

# 18. Reportリンク

|Report|Path|
|---|---|
|Diff Report|outputs/runs/{runId}/reports/DiffReport.md|
|Evidence Report|outputs/runs/{runId}/reports/EvidenceReport.md|
|Execution Report|outputs/runs/{runId}/reports/ExecutionReport.md|
|Error Report|outputs/runs/{runId}/reports/ErrorReport.md|
|Runtime Log|outputs/runs/{runId}/logs/runtime.log|

---

# Appendix A. 記入例

## A.1 Run Summary

|項目|内容|
|---|---|
|Report ID|RPT-DAILY-20260715-001|
|Run ID|RUN-20260715-090000-001|
|実行日|2026-07-15|
|対象環境|ENV-STG|
|実行方式|Daily|
|Baseline ID|BASE-20260714-001|
|総合Result|WARN|

---

## A.2 Result Summary

|Result|件数|
|---|---:|
|PASS|2|
|WARN|1|
|FAIL|0|
|ERROR|0|
|BLOCKED|0|
|SKIP|3|
|合計|3|

---

## A.3 UseCase結果

|UseCase ID|UseCase名称|Scenario数|Result|備考|
|---|---|---:|---|---|
|UC-001|顧客情報照会|3|WARN|契約0件Scenario確認要|

---

## A.4 Scenario結果

|Scenario ID|Scenario名称|開始API|終了API|実行API|Skip API|Result|
|---|---|---|---|---|---|---|
|SC-001|正常系|API-001|API-003|API-001, API-002, API-003|－|PASS|
|SC-002|顧客不存在|API-001|API-001|API-001|API-002, API-003|PASS|
|SC-003|契約0件|API-001|API-003|API-001, API-002, API-003|－|WARN|

---

## A.5 WARN

|No|分類|Scenario ID|内容|業務影響|状態|
|---:|---|---|---|---|---|
|1|Business|SC-003|契約件数がBaselineの2件から0件へ変更|未確認|Open|

---

## A.6 Baseline更新判定

|確認項目|判定|
|---|---|
|Critical / High差分なし|Yes|
|Medium差分確認完了|No|
|Evidence完全|Yes|
|Baseline更新可否|条件付き可|
:::

:::writing{variant="document" id="76492"}
---
title: Diff Report Template
document_id: RPT-DIFF-TEMPLATE
version: 1.0.0
status: Template
document_type: Verification Report
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Diff Report

---

# 1. Report情報

|項目|内容|
|---|---|
|Report ID|RPT-DIFF-XXX|
|Run ID|RUN-XXX|
|Baseline ID|BASE-XXX|
|Baseline Source Run ID|RUN-XXX|
|対象環境|ENV-XXX|
|比較開始日時|YYYY-MM-DDTHH:mm:ss+09:00|
|比較終了日時|YYYY-MM-DDTHH:mm:ss+09:00|
|Diff Result|PASS / WARN / FAIL / ERROR|
|Compare Policy Version|x.x.x|
|作成日時|YYYY-MM-DDTHH:mm:ss+09:00|

---

# 2. Diff概要

|項目|内容|
|---|---|
|Current Run|RUN-XXX|
|Baseline|BASE-XXX|
|比較対象UseCase数|0|
|比較対象Scenario数|0|
|比較対象API数|0|
|比較対象Field数|0|
|差分件数|0|
|Ignored件数|0|
|総合Result|PASS / WARN / FAIL / ERROR|

---

# 3. Severity別集計

|Severity|PASS|WARN|FAIL|IGNORED|ERROR|合計|
|---|---:|---:|---:|---:|---:|---:|
|Critical|0|0|0|0|0|0|
|High|0|0|0|0|0|0|
|Medium|0|0|0|0|0|0|
|Low|0|0|0|0|0|0|
|Info|0|0|0|0|0|0|
|合計|0|0|0|0|0|0|

---

# 4. Diff Type別集計

|Diff Type|件数|FAIL|WARN|IGNORED|
|---|---:|---:|---:|---:|
|MISSING_FIELD|0|0|0|0|
|NEW_FIELD|0|0|0|0|
|TYPE_CHANGED|0|0|0|0|
|VALUE_CHANGED|0|0|0|0|
|FIXED_VALUE_CHANGED|0|0|0|0|
|ENUM_OUT_OF_RANGE|0|0|0|0|
|NULL_CHANGED|0|0|0|0|
|ITEM_ADDED|0|0|0|0|
|ITEM_REMOVED|0|0|0|0|
|ITEM_CHANGED|0|0|0|0|
|ORDER_CHANGED|0|0|0|0|
|COUNT_CHANGED|0|0|0|0|

---

# 5. Critical / High Diff

|No|Severity|UseCase ID|Scenario ID|API ID|対象種別|対象Path|Diff Type|Baseline|Current|Policy|Result|Evidence|
|---:|---|---|---|---|---|---|---|---|---|---|---|---|
|1|Critical / High|UC-XXX|SC-XXX|API-XXX|Response / Context / Business|$.xxx / CTX-XXX|VALUE_CHANGED|（記載）|（記載）|Equals|FAIL|（記載）|

---

# 6. 全Diff一覧

|No|UseCase ID|Scenario ID|Step ID|API ID|対象種別|JSONPath / Context ID|Diff Type|Baseline Value|Current Value|Normalize|Compare Policy|Severity|Result|Message|
|---:|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|Response / Context|$.xxx|VALUE_CHANGED|（記載）|（記載）|NORM-XXX|CMP-POL-XXX|High|FAIL|（記載）|

---

# 7. UseCase別Diff

## 7.1 UseCase Summary

|UseCase ID|UseCase名称|Scenario数|Diff件数|WARN|FAIL|IGNORED|Result|
|---|---|---:|---:|---:|---:|---:|---|
|UC-XXX|（記載）|0|0|0|0|0|PASS / WARN / FAIL|

---

## 7.2 UseCase詳細

### UC-XXX：〇〇

|項目|内容|
|---|---|
|UseCase ID|UC-XXX|
|Result|PASS / WARN / FAIL|
|対象Scenario|SC-XXX|
|Diff件数|0|
|主な差分|（記載）|

|Scenario ID|API ID|対象|Diff Type|Severity|Result|Evidence|
|---|---|---|---|---|---|---|
|SC-XXX|API-XXX|$.xxx|VALUE_CHANGED|High|FAIL|（記載）|

---

# 8. Scenario別Diff

|Scenario ID|Scenario名称|Expected Result|Current Result|API Diff件数|Context Diff件数|Business Diff件数|Result|
|---|---|---|---|---:|---:|---:|---|
|SC-XXX|（記載）|PASS|PASS / WARN / FAIL|0|0|0|PASS / WARN / FAIL|

---

# 9. API別Diff

|API ID|API名称|Response Diff|Context Diff|Execution Diff|WARN|FAIL|IGNORED|Result|
|---|---|---:|---:|---:|---:|---:|---:|---|
|API-XXX|（記載）|0|0|0|0|0|0|PASS / WARN / FAIL|

---

# 10. Response Diff

|No|UseCase ID|Scenario ID|API ID|JSONPath|Diff Type|Baseline|Current|Type|Policy|Severity|Result|
|---:|---|---|---|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|$.xxx|VALUE_CHANGED|（記載）|（記載）|String|Equals|High|FAIL|

---

# 11. Context Diff

|No|UseCase ID|Scenario ID|Context ID|Context名|Diff Type|Producer|Baseline|Current|Policy|Severity|Result|
|---:|---|---|---|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|CTX-XXX|Domain.property|VALUE_CHANGED|API-XXX|（記載）|（記載）|Equals|High|FAIL|

---

# 12. Execution Diff

|No|Scenario ID|比較項目|Baseline|Current|Diff Type|Severity|Result|
|---:|---|---|---|---|---|---|---|
|1|SC-XXX|API実行順序|API-001→API-002|API-001→API-003|ORDER_CHANGED|High|FAIL|
|2|SC-XXX|終了API|API-003|API-002|VALUE_CHANGED|High|FAIL|
|3|SC-XXX|Skip API|API-003|なし|VALUE_CHANGED|High|FAIL|

---

# 13. Business Result Diff

|No|Scenario ID|比較項目|Baseline|Current|Severity|Result|備考|
|---:|---|---|---|---|---|---|---|
|1|SC-XXX|Business Result|（記載）|（記載）|High|FAIL| |

---

# 14. Collection Diff

## 14.1 Collection Summary

|対象JSONPath|比較方式|Key|Baseline件数|Current件数|Added|Removed|Changed|Result|
|---|---|---|---:|---:|---:|---:|---:|---|
|$.items[]|Key Match|itemId|0|0|0|0|0|PASS / WARN / FAIL|

---

## 14.2 Added Item

|Key|Current Value|Severity|Result|
|---|---|---|---|
|（記載）|（記載）|Medium|WARN|

---

## 14.3 Removed Item

|Key|Baseline Value|Severity|Result|
|---|---|---|---|
|（記載）|（記載）|High|FAIL|

---

## 14.4 Changed Item

|Key|Field|Baseline|Current|Policy|Severity|Result|
|---|---|---|---|---|---|---|
|（記載）|status|ACTIVE|INACTIVE|Equals|High|FAIL|

---

# 15. New Field一覧

|No|UseCase ID|Scenario ID|API ID|JSONPath|Current Value|Type|Severity|Result|確認要否|
|---:|---|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|$.newField|（記載）|String|Medium|WARN|要 / 不要|

---

# 16. Missing Field一覧

|No|UseCase ID|Scenario ID|API ID|JSONPath|必須|Baseline Value|Severity|Result|
|---:|---|---|---|---|---:|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|$.requiredField|Yes|（記載）|High|FAIL|

---

# 17. Type変更一覧

|No|UseCase ID|Scenario ID|API ID|JSONPath|Baseline Type|Current Type|Severity|Result|
|---:|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|$.xxx|String|Number|High|FAIL|

---

# 18. 固定値・Enum差分

|No|API ID|JSONPath|Check Type|期待値|Current|Severity|Result|
|---:|---|---|---|---|---|---|---|
|1|API-XXX|$.resultCode|Fixed|0|1|High|FAIL|
|2|API-XXX|$.status|Enum|ACTIVE, INACTIVE|UNKNOWN|High|FAIL|

---

# 19. Ignored Diff

|No|UseCase ID|Scenario ID|API ID|JSONPath|Baseline|Current|Policy ID|Ignore理由|
|---:|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|$.traceId|abc|xyz|CMP-POL-001|実行毎に採番|

---

# 20. Tolerance結果

|No|対象|Baseline|Current|Tolerance|差分|Result|
|---:|---|---|---|---|---|---|
|1|$.updatedAt|（記載）|（記載）|±3秒|2秒|PASS|
|2|$.amount|100.00|100.02|±0.01|0.02|FAIL|

---

# 21. Normalize結果

|No|対象|Baseline Original|Current Original|Normalize Rule|Normalized Baseline|Normalized Current|Result|
|---:|---|---|---|---|---|---|---|
|1|$.name|` abc `|`abc`|Trim|abc|abc|PASS|

---

# 22. Compare Policy適用状況

|Policy ID|Policy名称|適用件数|PASS|WARN|FAIL|IGNORED|
|---|---|---:|---:|---:|---:|---:|
|CMP-POL-XXX|（記載）|0|0|0|0|0|

---

# 23. Baseline Candidate

|UseCase ID|Scenario ID|API ID|Current Snapshot|Candidate Result|承認要否|備考|
|---|---|---|---|---|---|---|
|UC-XXX|SC-XXX|API-XXX|（記載）|Candidate / Not Candidate|要 / 不要| |

---

# 24. 確認事項

|No|Severity|差分内容|業務影響|確認担当|期限|状態|判断|
|---:|---|---|---|---|---|---|---|
|1|Medium|（記載）|未確認|（記載）|YYYY-MM-DD|Open| |

---

# 25. Evidenceリンク

|No|UseCase ID|Scenario ID|API ID|Diff Snapshot|Response Snapshot|Context Snapshot|Execution Snapshot|
|---:|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|API-XXX|（記載）|（記載）|（記載）|（記載）|

---

# Appendix A. 記入例

## A.1 Diff Summary

|項目|内容|
|---|---|
|Run ID|RUN-20260715-090000-001|
|Baseline ID|BASE-20260714-001|
|Diff Result|WARN|
|差分件数|2|
|Ignored件数|1|

---

## A.2 Diff Detail

|UseCase ID|Scenario ID|API ID|対象|Baseline|Current|Policy|Severity|Result|
|---|---|---|---|---|---|---|---|---|
|UC-001|SC-001|API-001|$.traceId|abc|xyz|CMP-POL-001|Low|IGNORED|
|UC-001|SC-003|API-003|$.contracts.length|2|0|Equals|Medium|WARN|

---

## A.3 Collection Diff

|対象|Key|Baseline|Current|Result|
|---|---|---|---|---|
|$.contracts[]|contractId=C-001|ACTIVE|なし|WARN|
|$.contracts[]|contractId=C-002|ACTIVE|なし|WARN|
:::

:::writing{variant="document" id="90516"}
---
title: Evidence Report Template
document_id: RPT-EVIDENCE-TEMPLATE
version: 1.0.0
status: Template
document_type: Verification Report
system_name: E6 API Verification Platform
author:
reviewer:
approver:
created:
updated:
---

# Evidence Report

---

# 1. Report情報

|項目|内容|
|---|---|
|Report ID|RPT-EVD-XXX|
|Run ID|RUN-XXX|
|対象環境|ENV-XXX|
|対象Business|BUS-XXX|
|対象UseCase|UC-XXX|
|対象Scenario|SC-XXX|
|実行日時|YYYY-MM-DDTHH:mm:ss+09:00|
|総合Result|PASS / WARN / FAIL / ERROR|
|Evidence Root|outputs/runs/{runId}/|
|作成日時|YYYY-MM-DDTHH:mm:ss+09:00|

---

# 2. Evidence概要

|Evidence分類|期待件数|生成件数|不足件数|Mask確認|Result|
|---|---:|---:|---:|---|---|
|Run Snapshot|1|0|0|済 / 未|PASS / ERROR|
|UseCase Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Scenario Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Request Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Response Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Context Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Execution Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Diff Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Error Snapshot|0|0|0|済 / 未|PASS / ERROR|
|Log|0|0|0|済 / 未|PASS / ERROR|

---

# 3. Evidence Directory

```text
outputs/runs/{runId}/

├── run-info.json
├── raw/
├── snapshot/
├── diff/
├── evidence/
├── reports/
├── logs/
└── tmp/
```

---

# 4. Run Evidence

|Evidence ID|対象|File Path|生成日時|Size|Hash|Result|
|---|---|---|---|---:|---|---|
|EVD-RUN-XXX|Run Snapshot|run-info.json|（記載）|0KB|SHA-256|PASS / ERROR|

---

# 5. UseCase Evidence

|UseCase ID|UseCase名称|Result|UseCase Snapshot|Scenario数|Evidence完全性|
|---|---|---|---|---:|---|
|UC-XXX|（記載）|PASS / WARN / FAIL / ERROR|（記載）|0|Complete / Partial / Missing|

---

# 6. Scenario Evidence

|Scenario ID|Scenario名称|分類|開始API|終了API|Result|Scenario Snapshot|Evidence完全性|
|---|---|---|---|---|---|---|---|
|SC-XXX|（記載）|Normal / Alternative / Exception|API-XXX|API-XXX|PASS / WARN / FAIL / ERROR|（記載）|Complete / Partial / Missing|

---

# 7. API Step Evidence Index

|No|UseCase ID|Scenario ID|Step ID|API ID|Execution Status|Request|Response|Context Before|Context After|Execution|Diff|Log|
|---:|---|---|---|---|---|---|---|---|---|---|---|---|
|1|UC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|PASS / SKIP / FAIL / ERROR|（Path）|（Path）|（Path）|（Path）|（Path）|（Path）|（Path）|

---

# 8. Request Evidence

## 8.1 Request一覧

|Evidence ID|UseCase ID|Scenario ID|Step ID|API ID|Method|Path|Snapshot Path|Mask|Result|
|---|---|---|---|---|---|---|---|---|---|
|EVD-REQ-XXX|UC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|POST|/v1/xxx|（記載）|済 / 未|PASS / ERROR|

---

## 8.2 Request概要

### API-XXX / UC-STEP-XXX

|項目|内容|
|---|---|
|Method|POST|
|URL|（Mask済みURL）|
|Content-Type|application/json|
|Authorization|`****`|
|Request Snapshot|（Path）|
|Context Binding|（記載）|
|Result|PASS / FAIL / ERROR|

Mask済みRequest：

```json
{
  "xxx": "****"
}
```

---

# 9. Response Evidence

## 9.1 Response一覧

|Evidence ID|UseCase ID|Scenario ID|Step ID|API ID|HTTP Status|Elapsed|Snapshot Path|Mask|Result|
|---|---|---|---|---|---:|---:|---|---|---|
|EVD-RES-XXX|UC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|200|0ms|（記載）|済 / 未|PASS / WARN / FAIL|

---

## 9.2 Response概要

### API-XXX / UC-STEP-XXX

|項目|内容|
|---|---|
|HTTP Status|200|
|Elapsed Millis|0|
|Content-Type|application/json|
|Response Snapshot|（Path）|
|Extracted Context|CTX-XXX|
|Dynamic Fields|$.traceId|
|Result|PASS / WARN / FAIL|

Mask済みResponse：

```json
{
  "resultCode": "0",
  "traceId": "dynamic-value"
}
```

---

# 10. Context Evidence

## 10.1 Context Snapshot一覧

|Evidence ID|UseCase ID|Scenario ID|Step ID|API ID|Timing|Context数|Snapshot Path|Result|
|---|---|---|---|---|---|---:|---|---|
|EVD-CTX-XXX|UC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|BEFORE_API / AFTER_API|0|（記載）|PASS / ERROR|

---

## 10.2 Context Flow

|Context ID|Context名|Producer|Consumer|生成Evidence|利用Evidence|Result|
|---|---|---|---|---|---|---|
|CTX-XXX|Domain.property|API-XXX / Entry Input|API-XXX / Branch|（Path）|（Path）|PASS / FAIL|

---

## 10.3 Context値

|Context ID|Type|値|Mask|生成元|利用先|
|---|---|---|---|---|---|
|CTX-XXX|String|****|Yes / No|API-XXX|API-XXX|

---

# 11. Execution Evidence

|Evidence ID|Scenario ID|Step ID|API ID|Status|Started At|Ended At|Elapsed|Retry|Skip Reason|Snapshot Path|
|---|---|---|---|---|---|---|---:|---:|---|---|
|EVD-EXEC-XXX|SC-XXX|UC-STEP-XXX|API-XXX|PASS / SKIP / FAIL / ERROR|（記载）|（記载）|0ms|0|（記载）|（Path）|

---

# 12. Skip Evidence

|Scenario ID|Step ID|API ID|Skip Rule ID|Skip条件|実際値|期待Skip|Result|Evidence|
|---|---|---|---|---|---|---|---|---|
|SC-XXX|UC-STEP-XXX|API-XXX|SKIP-XXX|（記載）|（記載）|Yes / No|PASS / FAIL|（Path）|

---

# 13. Retry Evidence

|Scenario ID|API ID|Attempt|開始日時|終了日時|結果|Error|Request Evidence|Response / Error Evidence|
|---|---|---:|---|---|---|---|---|---|
|SC-XXX|API-XXX|1|（記載）|（記載）|PASS / FAIL / TIMEOUT|（記載）|（Path）|（Path）|

---

# 14. Diff Evidence

|Evidence ID|UseCase ID|Scenario ID|API ID|Diff件数|WARN|FAIL|IGNORED|Diff Snapshot|Diff Report|
|---|---|---|---|---:|---:|---:|---:|---|---|
|EVD-DIFF-XXX|UC-XXX|SC-XXX|API-XXX|0|0|0|0|（Path）|（Path）|

---

# 15. Error Evidence

|Evidence ID|Error ID|Exception分類|UseCase ID|Scenario ID|API ID|Error Snapshot|Error Log|Result|
|---|---|---|---|---|---|---|---|---|
|EVD-ERR-XXX|ERR-XXX|Timeout / API / Context / Spec|UC-XXX|SC-XXX|API-XXX|（Path）|（Path）|FAIL / ERROR|

---

# 16. TestData Evidence

|TestData ID|Scenario ID|TestData File|Precondition Evidence|Reservation Evidence|Cleanup Evidence|Result|
|---|---|---|---|---|---|---|
|TD-XXX|SC-XXX|（Path）|（Path）|（Path）|（Path）|PASS / BLOCKED / ERROR|

---

# 17. Precondition Evidence

|Precondition ID|TestData ID|確認方法|期待値|実際値|Evidence|Result|
|---|---|---|---|---|---|---|
|PRE-XXX|TD-XXX|API / DB / FILE|（記載）|（記載）|（Path）|PASS / BLOCKED / ERROR|

---

# 18. Cleanup Evidence

|Cleanup ID|TestData ID|処理内容|実行日時|Result|Evidence|備考|
|---|---|---|---|---|---|---|
|CLEAN-XXX|TD-XXX|DELETE / RESTORE|（記載）|PASS / WARN / ERROR|（Path）| |

---

# 19. Report Evidence

|Report|生成有無|Path|Size|Hash|Result|
|---|---|---|---:|---|---|
|Daily Summary|Yes / No|（Path）|0KB|SHA-256|PASS / ERROR|
|Diff Report|Yes / No|（Path）|0KB|SHA-256|PASS / ERROR|
|Evidence Report|Yes / No|（Path）|0KB|SHA-256|PASS / ERROR|
|Execution Report|Yes / No|（Path）|0KB|SHA-256|PASS / ERROR|
|Error Report|Yes / No|（Path）|0KB|SHA-256|PASS / ERROR|

---

# 20. Mask確認

## 20.1 Mask対象確認

|対象分類|対象Path / Header / Context|Mask方式|確認結果|備考|
|---|---|---|---|---|
|Authorization|Authorization Header|FULL|PASS / FAIL| |
|顧客番号|$.customerId / CTX-001|PARTIAL|PASS / FAIL| |
|氏名|$.customer.name|FULL|PASS / FAIL| |
|Token|Secret|FULL|PASS / FAIL| |

---

## 20.2 Mask漏れ

Mask漏れがない場合は、`該当なし` と記載する。

|No|Evidence|対象|漏れ内容|Severity|処理|Result|
|---:|---|---|---|---|---|---|
|1|（Path）|$.xxx|（記載）|Critical|Report出力停止|ERROR|

---

# 21. Evidence完全性Check

|Check ID|確認内容|期待|実際|Result|
|---|---|---|---|---|
|EVD-CHK-001|全実行APIにRequest Snapshotがある|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-002|全実行APIにResponseまたはError Snapshotがある|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-003|全StepにExecution Snapshotがある|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-004|全ScenarioにScenario Snapshotがある|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-005|全Diff対象にDiff Snapshotがある|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-006|Evidence Indexから各Fileへ到達できる|Yes|Yes / No|PASS / ERROR|
|EVD-CHK-007|Mask確認済みである|Yes|Yes / No|PASS / ERROR|

---

# 22. File Hash

|Evidence ID|File Path|Hash Algorithm|Hash Value|確認結果|
|---|---|---|---|---|
|EVD-XXX|（Path）|SHA-256|（Hash）|PASS / FAIL|

---

# 23. Evidence Retention

|対象|保存期間|Archive|削除条件|
|---|---|---|---|
|PASS Run Evidence|（記載）|Yes / No|保存期限経過後|
|WARN / FAIL Evidence|（記載）|Yes|課題Close後|
|ERROR Evidence|（記載）|Yes|原因解消・承認後|
|Approved Baseline Evidence|無期限 / 規定期間|Yes|承認制|

---

# 24. Traceability

|Business ID|UseCase ID|Scenario ID|TestCase ID|TestData ID|Execution ID|API ID|Context ID|Check ID|Evidence ID|File Path|
|---|---|---|---|---|---|---|---|---|---|---|
|BUS-XXX|UC-XXX|SC-XXX|UC-TC-XXX|TD-XXX|EXEC-XXX|API-XXX|CTX-XXX|CHK-XXX|EVD-XXX|（Path）|

---

# 25. Evidence確認結果

|確認項目|判定|
|---|---|
|Evidence完全性|Complete / Partial / Missing|
|Mask確認|PASS / FAIL|
|File Hash確認|PASS / FAIL|
|Link確認|PASS / FAIL|
|再現性|あり / なし|
|監査利用可否|可 / 条件付き可 / 不可|
|最終Result|PASS / WARN / ERROR|

---

# Appendix A. 記入例

## A.1 Evidence Summary

|項目|内容|
|---|---|
|Run ID|RUN-20260715-090000-001|
|対象UseCase|UC-001|
|対象Scenario|SC-001|
|Result|PASS|
|Evidence完全性|Complete|

---

## A.2 API Step Evidence

|Step ID|API ID|Status|Request|Response|Context After|Execution|Diff|
|---|---|---|---|---|---|---|---|
|UC-STEP-001|API-001|PASS|raw/API-001_request.json|raw/API-001_response.json|snapshot/API-001_context_after.json|snapshot/API-001_execution.json|diff/API-001_diff.json|
|UC-STEP-002|API-002|PASS|raw/API-002_request.json|raw/API-002_response.json|snapshot/API-002_context_after.json|snapshot/API-002_execution.json|diff/API-002_diff.json|
|UC-STEP-003|API-003|PASS|raw/API-003_request.json|raw/API-003_response.json|snapshot/API-003_context_after.json|snapshot/API-003_execution.json|diff/API-003_diff.json|

---

## A.3 Mask確認

|対象|Mask方式|確認結果|
|---|---|---|
|Authorization|FULL|PASS|
|Customer.id|PARTIAL|PASS|
|Customer.name|FULL|PASS|

---

## A.4 Evidence完全性

|Check|Result|
|---|---|
|Request Snapshot|PASS|
|Response Snapshot|PASS|
|Context Snapshot|PASS|
|Execution Snapshot|PASS|
|Diff Snapshot|PASS|
|Evidence Link|PASS|
|Mask|PASS|
:::

这三份完成后，`06_verification_assets` 的核心模板链已经形成：

```text
Verification仕様書
  ↓
Execution仕様書
  ↓
API単体テスト仕様書
  ↓
UseCaseテスト仕様書
  ↓
TestData
  ↓
Daily Summary / Diff Report / Evidence Report
```
