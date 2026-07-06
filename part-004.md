# API流程验证设计

- 来源: https://chatgpt.com/c/6a30db25-a6bc-83e8-ba19-4bc5fc0a5e28?mweb_fallback=1
- 导出时间: 2026-07-04T10:37:12+09:00
- 分片: 4/4
- 总消息数: 364
- 总轮数: 178

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
