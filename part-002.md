# API流程验证设计

- 来源: https://chatgpt.com/c/6a30db25-a6bc-83e8-ba19-4bc5fc0a5e28
- 导出时间: 2026-07-02T19:57:43+09:00
- 分片: 2/3
- 总消息数: 286
- 总轮数: 139

## 第 51 轮

### 你

每个usecase前后要设置api入出力参数 哪几个作为下一个api调用参数 这个怎么设计到usecase里 并且和后面的测试关联

### ChatGPT

要在 **UseCase設計書** 里专门设计一章：

```text
Context Mapping（API入出力連携定義）
```

它负责说明：

> 前一个 API 的哪个 Response 字段，抽取成哪个变量，再作为后一个 API 的哪个 Request 参数。

---

## 1. UseCase里这样写

### Context Mapping

| No | From Step | From API | Response JSONPath | Variable | To Step | To API | Request JSONPath | Required |
|---:|---:|---|---|---|---:|---|---|---|
| 1 | 1 | API001_CreateCustomer | $.customerId | CUSTOMER_ID | 2 | API002_CreateAccount | $.body.customerId | Yes |
| 2 | 2 | API002_CreateAccount | $.accountId | ACCOUNT_ID | 3 | API003_GetBalance | $.path.accountId | Yes |
| 3 | 3 | API003_GetBalance | $.balance | BEFORE_BALANCE | 4 | API004_Payment | $.context.beforeBalance | No |
| 4 | 4 | API004_Payment | $.transactionId | TRANSACTION_ID | 5 | API005_GetTransaction | $.path.transactionId | Yes |

这张表就是核心。

---

## 2. API调用Step里引用变量

### Flow

| Step | API | Request Source |
|---:|---|---|
| 1 | API001_CreateCustomer | Entry Input |
| 2 | API002_CreateAccount | `${CUSTOMER_ID}` |
| 3 | API003_GetBalance | `${ACCOUNT_ID}` |
| 4 | API004_Payment | `${ACCOUNT_ID}`, `${PAYMENT_AMOUNT}` |
| 5 | API005_GetTransaction | `${TRANSACTION_ID}` |

---

## 3. Entry Input只给第一个API

### Entry Input

| Name | Type | Example | Used By |
|---|---|---|---|
| customerName | string | E6TEST_${runId} | Step1 |
| currency | string | JPY | Step1 |
| paymentAmount | number | 300 | Step4 |

注意：
`paymentAmount` 虽然 Step4 用，但它属于入口测试数据，不是用户中途手动输入。

---

## 4. 测试如何关联

测试书不要重新写一遍，而是引用 `Context Mapping` 生成测试项。

### UseCaseテスト仕様書 自动生成

| TestId | RuleId | Test内容 | Expected |
|---|---|---|---|
| UC001-T001 | UC001-CTX-001 | Step1 response.customerId 抽取成功 | CUSTOMER_ID exists |
| UC001-T002 | UC001-CTX-002 | Step2 request.customerId 使用 CUSTOMER_ID | request.customerId = Step1.customerId |
| UC001-T003 | UC001-CTX-003 | Step2 response.accountId 抽取成功 | ACCOUNT_ID exists |
| UC001-T004 | UC001-CTX-004 | Step3 request.accountId 使用 ACCOUNT_ID | request.accountId = Step2.accountId |

也就是说：

```text
UseCase設計書
  ↓
Context Mapping
  ↓
自动生成 Context連携テスト
```

---

## 5. RuleId也要设计

Context Mapping 每一行都生成规则：

| RuleId | 内容 |
|---|---|
| UC001-CTX-001 | CUSTOMER_ID must be extracted from API001.response.$.customerId |
| UC001-CTX-002 | API002.request.$.body.customerId must equal CUSTOMER_ID |
| UC001-CTX-003 | ACCOUNT_ID must be extracted from API002.response.$.accountId |
| UC001-CTX-004 | API003.request.$.path.accountId must equal ACCOUNT_ID |

执行结果里就能这样输出：

| RuleId | Result | Expected | Actual |
|---|---|---|---|
| UC001-CTX-001 | PASS | exists | C12345 |
| UC001-CTX-002 | PASS | C12345 | C12345 |
| UC001-CTX-003 | FAIL | exists | null |

---

## 6. Java执行时的逻辑

```text
Step1 调用 API001
  ↓
从 response 按 JSONPath 抽取 customerId
  ↓
保存到 Context：CUSTOMER_ID
  ↓
Step2 生成 request 时替换 ${CUSTOMER_ID}
  ↓
调用 API002
  ↓
执行 Context Rule 比较
```

内部 Context：

```json
{
  "entry": {
    "customerName": "E6TEST_DEV_001",
    "currency": "JPY",
    "paymentAmount": 300
  },
  "variables": {
    "CUSTOMER_ID": "C12345",
    "ACCOUNT_ID": "A67890",
    "TRANSACTION_ID": "T99999"
  }
}
```

---

## 7. UseCase模板里必须增加这些章节

```text
3. Entry Input
4. Flow
5. Context Mapping
6. Request Binding
7. Context Verification Rule
8. Business Verification Rule
```

其中最重要的是：

```text
Context Mapping
Request Binding
Context Verification Rule
```

---

结论：

```text
前后API参数传递不要写在测试书里。
应该写在UseCase設計書的 Context Mapping 里。

测试书根据 Context Mapping 自动生成。
执行结果根据每条 Context Rule 输出 PASS / FAIL。
```

这样才能保证：
**第一个 API 由入口参数驱动，后续 API 全部由前序 API 的返回值和 Context 自动驱动。**

## 第 52 轮

### 你

api的测试case也是需要设计的 他就是rule吗

### ChatGPT

**这是整个项目里最关键的一个概念。**

答案是：

> **不是。Rule 和 TestCase 是两种不同的东西。**

很多项目都会把它们混在一起，但如果你想做成 AI 自动化平台，一定要分开。

---

# 三层关系

```text
API设计书
    │
    ▼
Verification Rule（规则）
    │
    ▼
Test Case（测试）
    │
    ▼
Execution Result（结果）
```

也就是说：

**Rule 是"要验证什么"**

**Test Case 是"怎么验证"**

---

# 举个例子

API设计书：

```text
customerName

Type=String

Required

MaxLength=50
```

这里实际上定义了三个 Rule。

```
Rule001

Required

Rule002

Type=String

Rule003

MaxLength=50
```

---

然后：

AI：

自动生成：

Test Case。

例如：

| Test Case | 验证哪个Rule |
|------------|--------------|
| 正常输入50字符 | Rule003 |
| 输入51字符 | Rule003 |
| 空字符串 | Rule001 |
| 不输入 | Rule001 |
| number类型 | Rule002 |

看到没有？

**一个 Rule**

可以生成：

**多个 Test Case。**

---

# 再举一个

Rule：

```text
Enum

JPY

USD
```

AI：

生成：

```
Case01

JPY

PASS

Case02

USD

PASS

Case03

CNY

NG

Case04

NULL

NG
```

---

# 所以关系应该是

```
API001

↓

Rule001

↓

Test001

Test002

Test003

Test004
```

不是：

```
API

↓

Test
```

---

# 我建议整个项目这样设计

## API设计书

里面：

```
Field

↓

Verification Rule
```

例如：

| RuleID | JSONPath | Rule |
|---------|----------|------|
| R001 | $.customerName | Required |
| R002 | $.customerName | MaxLength=50 |
| R003 | $.customerName | Type=String |

---

## API测试设计书

里面：

```
Rule

↓

Test Case
```

例如：

| TestID | RuleID | Input | Expected |
|---------|---------|-------|----------|
| TC001 | R001 | 未输入 | 400 |
| TC002 | R001 | 空字符串 | 400 |
| TC003 | R002 | 50字符 | PASS |
| TC004 | R002 | 51字符 | FAIL |
| TC005 | R003 | Number | FAIL |

---

## AI负责

以后：

AI：

看到：

```
Required
```

知道：

至少生成：

```
NULL

空字符串

不存在
```

三个测试。

看到：

```
MaxLength
```

知道：

至少生成：

```
49

50

51
```

看到：

```
Enum
```

知道：

生成：

```
全部合法值

非法值
```

---

# 所以真正应该增加一个概念

我建议：

API设计书：

不要写：

```
Rule
```

而写：

```
Verification Definition
```

例如：

```
customerName

↓

Verification Definition

Required

Type

MaxLength

Pattern
```

AI：

根据：

Definition：

生成：

```
API Test Case
```

---

# 我建议整个关系应该变成

```
API设计书
       │
       ▼
Verification Definition
       │
       ▼
AI
       │
       ▼
API Test Case
       │
       ▼
Java Execute
       │
       ▼
Result
```

---

# 我认为整个项目真正应该有"三种规则"

| 类型 | 放哪里 | 用途 |
|------|---------|------|
| **Verification Definition** | API设计书 | 定义字段应该满足什么约束（Required、Type、Length、Enum、Pattern、Compare 等） |
| **Execution Rule** | UseCase设计书 | 定义 API 顺序、Context Mapping、Retry、Stop、Cleanup 等流程规则 |
| **Test Case** | AI 自动生成的测试书 | 根据前两者生成具体测试数据和执行项 |

这样职责就非常清楚了。

- **API设计书**负责定义"字段契约"。
- **UseCase设计书**负责定义"流程契约"。
- **测试书**负责定义"如何验证这些契约"。

---

## 我甚至建议再进一步优化（这是我认为最适合你项目的）

不要在 API 设计书里直接写"测试"。

而是写：

**Verification Definition（検証定義）**

例如：

| JSONPath | Verification Definition |
|-----------|------------------------|
| $.customerName | Required / String / Max=50 / Pattern=[A-Za-z0-9] |
| $.currency | Required / Enum(JPY,USD) |
| $.amount | Required / Number / Min=0 / Max=999999999 |

然后：

**AI 自动推导 Test Case**。

这样以后如果增加一个规则，例如：

```
Pattern
```

你不用去修改所有测试书。

AI 会自动知道：

> 需要增加"合法格式"和"非法格式"两类测试。

这就是**声明式规格（Specification）驱动自动测试**，也是我认为这个平台最值得投入的设计方向。

## 第 53 轮

### 你

好的 那么wbs一览 以及系统完整构成 告诉我

### ChatGPT

我把它整理成两部分：先给按成果物驱动的 WBS，再给系统完整构成。这里会以“Markdown 设计书作为 SSOT，AI 自动生成，Java Batch 确定执行”为中心。

### ChatGPT

下面是当前定版思路。

# 一、WBS 成果物一览

| No | 成果物 | 主要任务 | 目的 |
|---|---|---|---|
| 1 | 要件定義書 | 背景、目标、范围、非范围、日次执行、比较对象、成功标准 | 明确这个工具到底做什么 |
| 2 | QA一覧 | 业务 Team、E6、Infra、运维确认事项 | 把不确定点记录并闭环 |
| 3 | 現行業務分析書 | 分析现行业务 Flow、E6 调用点、本系统 API、DB 更新 | 作为抽取最小验证链的依据 |
| 4 | E6 API Catalog | 整理 24 个 E6 API、分类、用途、重要度 | API 主目录 |
| 5 | Verification UseCase Catalog | 设计 10 个以内 UseCase | UseCase 主目录 |
| 6 | API・UseCase対応一覧 | API 被哪些 UseCase 覆盖 | 确认可覆盖全部 API |
| 7 | Variable Catalog | CUSTOMER_ID、ACCOUNT_ID 等 Context 变量 | 统一前后 API 参数传递 |
| 8 | Environment Catalog | DEV/STG/PROD、endpoint、认证、tenant | 环境切换和安全控制 |
| 9 | API設計書 Template | 固定 API 设计书格式 | 让 AI 稳定解析 |
| 10 | API設計書 24份 | Request、Response、Verification Definition、Compare、Extract | 单 API 契约来源 |
| 11 | UseCase設計書 Template | 固定 UseCase 设计书格式 | 让 AI 稳定生成执行计划 |
| 12 | UseCase設計書 10份以内 | Entry、Flow、Context Mapping、Business Check、Execution Policy | 每天真正执行的验证链 |
| 13 | API単体テスト仕様書 | 根据 API 规则生成必填、类型、长度、enum、异常测试 | 验证单 API 契约 |
| 14 | API単体テストデータ | AI 根据 API 设计生成测试数据 | 自动执行 API 单体测试 |
| 15 | UseCaseテスト仕様書 | 根据 UseCase Flow/Context 生成链路测试 | 验证 API 连续调用 |
| 16 | UseCaseテストデータ | AI 生成入口数据和链路数据 | 支持每天自动执行 |
| 17 | システム設計書 | 整体架构、模块、数据流、目录结构 | 定义系统全貌 |
| 18 | 共通Framework設計書 | File、JSON、Date、Log、Exception、Config、Mask、Hash | 防止各模块重复实现 |
| 19 | RunContext設計書 | runId、executionId、Context、变量池、状态 | 支撑多重启动和链路执行 |
| 20 | Snapshot設計書 | Request/Response/Contract/Result Snapshot | 每天比较的基础 |
| 21 | Diff設計書 | 今天 vs 昨天/Baseline 的比较流程 | 发现 E6 API 变化 |
| 22 | Report設計書 | Daily Summary、Diff Report、Evidence 分层 | 承认者只看总结 |
| 23 | ファイル入出力設計書 | 文件上传/下载、resources、hash、atomic write | 支持文件流测试 |
| 24 | JSON設計書 | Markdown → JSON Spec、Result JSON、Diff JSON | 程序执行格式 |
| 25 | ログ・例外設計書 | mask、error code、stacktrace、stop/continue | 运维排查 |
| 26 | 日付・比較設計書 | 日期字段、时区、timestamp ignore、normalize | 防止每日变化误报 |
| 27 | 環境設計書 | Linux、JDK、Tomcat、cron、目录、权限、网络 | 发布环境设计 |
| 28 | 運用設計書 | 日次执行、baseline批准、cleanup、障害対応 | 上线后怎么跑 |
| 29 | Daily Summary Report | 每日执行总结 | 给承认者看 |
| 30 | Diff Report | 差异明细 | 给 Leader/开发看 |
| 31 | Evidence | raw request/response、log、snapshot | 发生问题时调查 |

---

# 二、系统完整构成

```text
Markdown Design Documents
        ↓
AI Generator / Parser
        ↓
JSON Spec
        ↓
Java Batch Engine
        ↓
E6 API
        ↓
Snapshot
        ↓
Diff Engine
        ↓
Daily Summary / Diff Report
```

---

# 三、目录结构

```text
project/

├── docs/
│   ├── 01_requirements/
│   │   ├── 要件定義書.md
│   │   └── QA一覧.md
│   │
│   ├── 02_analysis/
│   │   ├── 現行業務分析書.md
│   │   ├── E6_API分析書.md
│   │   └── API一覧.md
│   │
│   ├── 03_catalog/
│   │   ├── E6_API_Catalog.md
│   │   ├── Verification_UseCase_Catalog.md
│   │   ├── API_UseCase_Mapping.md
│   │   ├── Variable_Catalog.md
│   │   └── Environment_Catalog.md
│   │
│   ├── 04_api_design/
│   │   ├── API設計書_Template.md
│   │   ├── API001_xxx.md
│   │   └── ...
│   │
│   ├── 05_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   ├── UC001_xxx.md
│   │   └── ...
│   │
│   ├── 06_framework_design/
│   │   ├── システム設計書.md
│   │   ├── 共通Framework設計書.md
│   │   ├── RunContext設計書.md
│   │   ├── Snapshot設計書.md
│   │   ├── Diff設計書.md
│   │   ├── Report設計書.md
│   │   ├── ファイル入出力設計書.md
│   │   ├── JSON設計書.md
│   │   ├── ログ・例外設計書.md
│   │   ├── 日付・比較設計書.md
│   │   └── 環境設計書.md
│   │
│   ├── 07_test_design/
│   │   ├── テスト方針書.md
│   │   ├── api/
│   │   │   ├── API単体テスト仕様書_Template.md
│   │   │   ├── API001_テスト仕様書.md
│   │   │   └── API001_テストデータ.md
│   │   └── usecase/
│   │       ├── UseCaseテスト仕様書_Template.md
│   │       ├── UC001_テスト仕様書.md
│   │       └── UC001_テストデータ.md
│   │
│   └── 08_operation/
│       ├── 運用設計書.md
│       ├── 日次運用手順書.md
│       ├── Baseline運用.md
│       └── リリース手順書.md
│
├── specs/
│   ├── api-json/
│   ├── usecase-json/
│   ├── test-json/
│   └── config-json/
│
├── test-resources/
│   ├── API001/
│   │   ├── input/
│   │   └── expected/
│   └── UC001/
│       ├── input/
│       └── expected/
│
├── baseline/
│   ├── api/
│   └── usecase/
│
├── runs/
│   └── {runId}/
│       ├── run-info.json
│       ├── raw/
│       ├── snapshot/
│       ├── diff/
│       ├── reports/
│       │   ├── DailySummary.md
│       │   └── DiffReport.md
│       ├── logs/
│       └── tmp/
│
├── config/
│   ├── dev.json
│   ├── stg.json
│   └── prod.json
│
└── src/
```

---

# 四、Java 系统模块

```text
src/

├── cli/
│   └── Main.java
│
├── runtime/
│   ├── RunContext
│   ├── RunIdGenerator
│   ├── LockManager
│   └── StatusManager
│
├── spec/
│   ├── ApiSpecLoader
│   ├── UseCaseSpecLoader
│   └── TestSpecLoader
│
├── common/
│   ├── FileService
│   ├── JsonService
│   ├── DateTimeService
│   ├── LogService
│   ├── MaskingService
│   ├── HashService
│   ├── ConfigService
│   └── ExceptionHandler
│
├── api/
│   ├── E6HttpClient
│   ├── ApiExecutor
│   └── RequestBuilder
│
├── usecase/
│   ├── UseCaseRunner
│   ├── ContextResolver
│   ├── ContextMapper
│   └── ExecutionPolicy
│
├── snapshot/
│   ├── SnapshotBuilder
│   └── ContractExtractor
│
├── diff/
│   ├── DiffEngine
│   ├── CompareRuleExecutor
│   └── IgnoreRuleHandler
│
├── report/
│   ├── DailySummaryWriter
│   ├── DiffReportWriter
│   └── EvidenceWriter
│
└── operation/
    ├── BaselineManager
    ├── CleanupManager
    └── SchedulerSupport
```

---

# 五、执行流程

```text
1. 读取 config/env
2. 生成 runId / executionId
3. 创建 runs/{runId}
4. 读取 specs/usecase-json
5. 读取相关 api-json
6. 加载 test data / test resources
7. 执行 Entry API
8. 从 response 抽取变量到 Context
9. 后续 API 根据 Context 自动组装 request
10. 每个 API 保存 raw request/response
11. 生成 snapshot
12. 按 API Verification Definition 检查
13. 按 UseCase Context Mapping 检查
14. 与 baseline / 前一天结果 diff
15. 生成 DailySummary.md
16. 生成 DiffReport.md
17. 保存 evidence
```

---

# 六、最关键设计原则

```text
1. Markdown 是人和 AI 维护的唯一事实来源
2. JSON 是 Java 执行用规格
3. API 设计书定义字段契约
4. UseCase 设计书定义 API 链路和 Context
5. TestCase 由 AI 根据 Rule 自动生成
6. 每条 Rule / Test / Result 都有 ID
7. 承认者只看 Daily Summary
8. 详细测试结果只作为 Evidence
9. 第一个 API 使用 Entry Input
10. 后续 API 只能使用 Context / 前序 Response / 环境变量
```

---

一句话总结：

```text
这个系统 = Markdown设计资产 + AI自动生成 + Java确定执行 + Snapshot比较 + 日次总结报告。
```

## 第 54 轮

### 你

Variable Catalog 目的是什么

### ChatGPT

我现在反而觉得 **Variable Catalog** 可以再升级一下。

因为经过我们前面的讨论，它已经不仅仅是变量了。

它其实应该叫：

> **Context Catalog（上下文目录）**

我解释一下。

---

# 为什么需要它？

因为一个 UseCase 里面：

```text
API001

↓

API002

↓

API003

↓

API004
```

Java 并不知道：

API001 返回：

```json
{
  "customerId":"123"
}
```

应该：

传给：

API002：

```json
{
  "customerId":"123"
}
```

还是：

API003：

```json
{
  "customerId":"123"
}
```

所以：

需要：

```text
Context
```

---

# 如果没有 Catalog

例如：

API001

返回：

```json
{
    "customerId":"123"
}
```

Java：

代码：

```java
customerId=response.get("customerId");
```

API002

```java
request.setCustomerId(customerId);
```

以后：

API变了。

全部：

改Java。

---

# 有了 Catalog

例如：

| Variable | 来源 |
|----------|------|
| CUSTOMER_ID | API001.response.customerId |

UseCase：

```text
API002

↓

customerId

↓

${CUSTOMER_ID}
```

Java：

不知道：

customerId。

它只知道：

```text
${CUSTOMER_ID}
```

---

# 其实它真正的作用

不是：

保存变量。

而是：

保存：

```text
API之间的数据流
```

Data Flow。

---

# 我建议升级

不要：

Variable Catalog。

改成：

## Context Catalog

例如：

| Variable | Type | Source | Description |
|----------|------|--------|-------------|
| CUSTOMER_ID | String | API001.response.customerId | Customer ID |
| ACCOUNT_ID | String | API003.response.accountId | Account ID |
| TOKEN | String | Login.response.token | Login Token |

---

然后：

UseCase：

引用：

```text
${CUSTOMER_ID}
```

---

# 更进一步

我建议：

Context Catalog

再增加：

生命周期。

例如：

| Variable | Scope |
|----------|-------|
| TOKEN | Global |
| CUSTOMER_ID | UseCase |
| ACCOUNT_ID | UseCase |
| RUN_ID | Runtime |
| EXECUTION_ID | Runtime |

以后：

Java：

知道：

什么时候：

删除。

---

# Context Catalog真正用途

例如：

| 用途 | 是否使用 |
|------|---------|
| API参数替换 | √ |
| API Extract | √ |
| Context保存 | √ |
| Test Data | √ |
| Report | √ |
| Log | √ |

所以：

它不是：

变量。

而是：

整个执行Context。

---

# 我甚至建议

再增加：

Context Type。

例如：

| Variable | Type |
|----------|------|
| CUSTOMER_ID | Response |
| USER_NAME | Entry |
| TOKEN | Global |
| RUN_ID | Runtime |
| CURRENT_DATE | System |

这样：

Java：

自动知道：

哪里来的。

---

# 所以我认为

真正应该叫：

```text
Context Catalog
```

不是：

```text
Variable Catalog
```

因为：

以后：

里面：

不仅有：

```text
customerId
```

还会有：

```text
文件

token

日期

环境变量

随机数

uuid

runId
```

这些：

都属于：

Context。

---

# 我建议最终的 Context Catalog 结构

| 字段 | 说明 |
|------|------|
| Context ID | 内部唯一编号 |
| Variable Name | 变量名（如 CUSTOMER_ID） |
| Data Type | String、Number、File、Object、Array 等 |
| Scope | Runtime、UseCase、Global、Step |
| Source Type | Entry、API Response、Environment、System、Constant |
| Source | 如 `API001.response.$.customerId` |
| Target | 被哪些 API / UseCase 使用 |
| Required | 是否必须存在 |
| Default | 默认值 |
| Description | 业务说明 |

---

## 不过，结合我们已经设计好的 UseCase 模板，我还有一个建议：

**其实 `Context Catalog` 不应该独立维护。**

真正的 **Context Mapping（API→API 的变量流转）** 已经写在 **UseCase 设计书** 里，所以建议职责拆分为：

- **Context Catalog**：定义"变量本身"（是什么、类型、作用域、来源类型）。
- **UseCase 设计书**：定义"变量如何流转"（从哪个 API 提取，到哪个 API 使用）。

这样：

- Context Catalog 不会重复写 API 流程。
- UseCase 可以自由组合 API。
- 一个 `CUSTOMER_ID` 可以在多个 UseCase 中复用。

**我认为这是最终最合理的职责划分。**

## 第 55 轮

### 你

多个api request 或者response是一样名字呢

### ChatGPT

这是一个**架构级问题**，也是很多 API 测试平台最后都会遇到的问题。

我的答案是：

> **绝对不能只靠字段名。**
>
> 必须设计成 **Context Object（上下文对象）**，而不是一个简单的变量表。

例如：

很多 API 都有：

```json
{
    "id":"123"
}
```

或者

```json
{
    "status":"ACTIVE"
}
```

如果只存：

```text
ID=123
STATUS=ACTIVE
```

到第三个 API 时：

你已经不知道：

这是：

- Customer 的 id？
- Account 的 id？
- Transaction 的 id？

所以这种设计一定会出问题。

---

# 我建议不要设计成

```text
CUSTOMER_ID
ACCOUNT_ID
TRANSACTION_ID
```

这种变量。

而是：

## Context Object

例如：

| Context Key | JsonPath | Type |
|------------|----------|------|
| Customer.id | $.customerId | String |
| Customer.status | $.status | String |
| Account.id | $.accountId | String |
| Account.status | $.status | String |
| Payment.id | $.paymentId | String |

注意：

这里：

status

可以有：

很多个。

---

Java里面：

实际上保存：

```json
{
    "Customer":{
        "id":"C001",
        "status":"ACTIVE"
    },
    "Account":{
        "id":"A001",
        "status":"OPEN"
    },
    "Payment":{
        "id":"P001",
        "status":"SUCCESS"
    }
}
```

这样：

永远不会冲突。

---

# UseCase里怎么引用？

不要：

```text
${STATUS}
```

而应该：

```text
${Customer.status}

${Account.status}

${Payment.status}
```

或者：

```text
${Customer.id}

${Account.id}
```

---

# Context Mapping

也变成：

| From | Extract | Context |
|------|----------|---------|
| API001 | $.customerId | Customer.id |
| API001 | $.status | Customer.status |
| API002 | $.accountId | Account.id |
| API002 | $.status | Account.status |

这样：

即使：

所有API：

都有：

status。

也没有关系。

---

# 如果 Response 很复杂怎么办？

例如：

```json
{
  "customer":{
      "id":"C001",
      "status":"ACTIVE"
  },
  "account":{
      "id":"A001",
      "status":"OPEN"
  }
}
```

Context：

直接：

保存：

```text
Customer

↓

整个Object
```

以后：

API：

引用：

```text
${Customer.id}

${Customer.status}
```

---

# 更进一步（我更推荐）

其实不要叫：

Variable Catalog。

而叫：

## Context Schema

例如：

```yaml
Customer:
    id:
        type:String

    status:
        type:String

Account:
    id:
        type:String

    status:
        type:String

Payment:
    id:
        type:String

    status:
        type:String
```

以后：

AI：

Java：

都知道：

整个Context。

---

# 如果两个API都有customerId呢？

例如：

API001：

```json
customerId
```

API005：

```json
customerId
```

是不是：

覆盖？

**不是。**

因为：

Context Mapping：

决定：

是否覆盖。

例如：

```text
API001

↓

Customer.id

API005

↓

Customer.id
```

如果：

允许：

更新。

覆盖。

否则：

报：

```text
Context Conflict
```

---

# 我建议增加一个设计

在 UseCase 里面。

增加：

## Context Update Policy

例如：

| Context | Policy |
|----------|--------|
| Customer.id | Immutable |
| Customer.status | Overwrite |
| Account.balance | Overwrite |
| Payment.id | Immutable |

这样：

Java：

自动：

知道：

什么时候：

允许：

覆盖。

---

# 所以我建议整个Context设计升级

不要：

```text
Variable Catalog
```

而是：

```text
Context Model
```

里面：

定义：

整个：

执行上下文。

UseCase：

定义：

```text
API

↓

Context

↓

API
```

真正：

传递。

---

## 我认为这是整个项目最后一次比较大的架构升级

我建议把 **Variable Catalog** 完全取消，改成两个成果物：

### ① Context Model（全局）

定义上下文的数据模型，例如：

```text
Customer
Account
Payment
Environment
Runtime
System
```

以及每个对象有哪些字段、类型、作用域。

### ② Context Mapping（UseCase 内）

定义：

> **哪个 API 的哪个 Response 字段，映射到 Context 的哪个对象字段；再由哪个 API 的哪个 Request 字段使用。**

这样即使有：

- `id`
- `status`
- `name`
- `code`

在几十个 API 中重复出现，也不会冲突，因为真正使用的是：

```text
Customer.id
Account.id
Payment.id
```

而不是一个全局的 `id`。这也是工作流引擎、ESB、BPM 等系统处理多接口数据传递时常用的设计方式。

## 第 56 轮

### 你

好的

### ChatGPT

很好，我觉得现在整个架构已经开始成熟了。

我把目前的设计重新整理了一遍，我认为这是**Version 1.0**，以后应该不会再有大的推翻，只会继续细化。

---

# 整个系统只有五个核心资产（Master）

```text
                    要件定义

                        │

                现行业务分析

                        │

          ┌─────────────┴─────────────┐

          │                           │

     API Master                 UseCase Master

          │                           │

          └─────────────┬─────────────┘

                        │

                  Context Model

                        │

                    Java Engine
```

所以整个系统其实围绕五个 Master 工作。

---

# 我建议最终成果物调整如下

```
docs/

01_requirements/
```

负责：

为什么开发

---

```
02_analysis/
```

负责：

分析业务

不是开发

---

```
03_master/
```

这里我建议不要叫 catalog。

日本项目更喜欢：

> Master

这里以后是整个项目最重要。

里面：

```
E6_API_Master.md

UseCase_Master.md

Context_Model.md

Environment_Master.md

API_UseCase_Mapping.md
```

全部：

都是Master。

以后：

AI：

首先：

读这里。

---

```
04_api_design/
```

真正：

一个API：

一份设计书。

---

```
05_usecase_design/
```

真正：

一个UseCase：

一份设计书。

---

```
06_framework/
```

Java：

Framework。

---

```
07_test/
```

全部：

AI：

生成。

---

```
08_operation/
```

运维。

---

# Context Model

我建议改成：

## Context Model

不要：

Variable。

例如：

```
Runtime

    Run

    Execution

Environment

    Tenant

    Endpoint

Customer

    id

    status

Account

    id

    status

Payment

    id

Transaction

    id
```

以后：

整个：

Context：

都是：

Object。

不是：

Variable。

---

# API设计书

负责：

```
Request

↓

Verification Definition

↓

Response

↓

Extract

↓

Compare
```

---

# UseCase设计书

负责：

```
Entry

↓

Flow

↓

Context Mapping

↓

Business Verification

↓

Execution Policy
```

Context Mapping：

例如：

| Step | From | To |
|------|------|----|
| API001.customerId | Customer.id | API002.customerId |

这张：

以后：

Java：

直接：

执行。

---

# Test

真正：

AI：

生成：

```
API

↓

Verification Definition

↓

API Test
```

以及：

```
UseCase

↓

Context Mapping

↓

UseCase Test
```

---

# Java

Java：

永远：

不要：

知道：

customerId。

它只知道：

```
Customer.id
```

所以：

Java：

就是：

Context Engine。

---

# 最后：

Report。

Report：

只有：

三层。

```
Summary

↓

UseCase

↓

Evidence
```

不要：

API。

为什么？

因为：

API：

只是：

UseCase：

里面：

一个Step。

Leader：

不会：

关心：

API。

他：

关心：

```
UC001

PASS

UC002

PASS

UC003

NG
```

然后：

点进去。

才看到：

```
API005

FAIL
```

再：

点进去。

才：

看到：

```
Request

Response

Diff
```

---

# 我现在认为还需要增加一个成果物（也是最后一个）

这个成果物：

我认为：

以后：

AI：

每天：

都会：

用。

叫：

## Context Mapping Master

不要：

放：

UseCase。

单独：

管理。

例如：

| Context | Producer | Consumer |
|----------|----------|----------|
| Customer.id | API001 | API002、API003、API010 |
| Account.id | API003 | API004、API008 |
| Payment.id | API005 | API006 |

为什么？

因为：

以后：

如果：

API001：

改了：

customerId。

一查：

```
Customer.id
```

立即：

知道：

影响：

哪些：

API。

哪些：

UseCase。

这个：

就是：

**影响分析（Impact Analysis）**。

---

## 这是我最后建议的一次架构升级

我建议把 **Master** 再细分成两类：

### ① 业务 Master（Business Master）

- E6 API Master
- UseCase Master
- Environment Master

这些描述"有哪些业务对象"。

### ② 技术 Master（Technical Master）

- Context Model
- Context Mapping Master

这两份描述"数据怎么流动"。

这样整个系统就形成了一个非常清晰的分层：

```text
Business Master
        │
        ▼
API / UseCase Design
        │
        ▼
Technical Master（Context）
        │
        ▼
Java Engine
        │
        ▼
Daily Verification
```

**我认为，这已经可以作为一个工业级平台的总体架构了。**后续我们要做的工作，就不是再改架构，而是把每一种 Master、每一种设计书模板做到足够完整、足够适合 AI 自动生成和自动执行。

## 第 57 轮

### 你

好的 给我完整的wbs和架构

### ChatGPT

我认为我们现在已经到了可以**冻结架构（Architecture Freeze V1）**的时候了。

而且，我建议不要把它当作一个 Batch，而是把它当作一个**平台（Platform）**来设计。

> **项目名称建议：**
>
> **E6 API Verification Platform**

---

# 一、项目目标

建立一个**AI + Markdown + Java** 的 API 验证平台。

目标：

- 验证 E6 API 是否发生变化
- 自动执行 UseCase
- 自动比较昨天(Baseline)
- 自动生成日报
- AI 自动生成设计、测试、测试数据
- Java 保证执行结果可重复

---

# 二、总体架构

```text
                         业务设计书
                               │
                               ▼
                       现行业务分析（AI）
                               │
                               ▼
                     ┌──────────────────┐
                     │   Business Master │
                     └──────────────────┘
                               │
         ┌─────────────────────┼──────────────────────┐
         │                     │                      │
         ▼                     ▼                      ▼
    E6 API Master       UseCase Master      Environment Master
                               │
                               ▼
                     ┌──────────────────┐
                     │ Technical Master │
                     └──────────────────┘
                               │
                 ┌─────────────┴─────────────┐
                 ▼                           ▼
          Context Model            Context Mapping
                 │                           │
                 └─────────────┬─────────────┘
                               ▼
                     API Design (Markdown)
                               │
                               ▼
                  UseCase Design (Markdown)
                               │
                 ┌─────────────┴─────────────┐
                 ▼                           ▼
             AI Generator              JSON Generator
                 │                           │
                 └─────────────┬─────────────┘
                               ▼
                     Java Verification Engine
                               │
          ┌────────────────────┼─────────────────────┐
          ▼                    ▼                     ▼
      API Executor        Snapshot Engine       Diff Engine
          │                    │                     │
          └────────────────────┼─────────────────────┘
                               ▼
                         Report Generator
                               │
                 ┌─────────────┼─────────────┐
                 ▼             ▼             ▼
           Daily Summary   Diff Report    Evidence
```

---

# 三、项目目录

```text
project/
├── docs/
├── specs/
├── test-resources/
├── generated/
├── baseline/
├── runs/
├── config/
└── src/
```

---

# 四、成果物 WBS（按成果物）

## 01 Requirements

| 成果物 | 目的 |
|---------|------|
| 要件定義書 | 项目目标、范围、成功标准 |
| QA一覧 | 所有确认事项 |

---

## 02 Analysis

| 成果物 | 目的 |
|---------|------|
| 現行業務分析書 | 分析业务 Flow |
| E6 API分析書 | 分析 E6 API |
| API一覧 | API 清单 |

---

## 03 Business Master

| 成果物 | 目的 |
|---------|------|
| E6 API Master | 所有 API 主目录 |
| UseCase Master | 所有 UseCase 主目录 |
| API-UseCase Mapping | API 覆盖关系 |
| Environment Master | 环境管理 |

---

## 04 Technical Master

| 成果物 | 目的 |
|---------|------|
| Context Model | 全局上下文对象定义 |
| Context Mapping Master | API 间数据流关系 |
| Compare Policy | 全局比较策略（日期、UUID、TraceId 等默认行为） |

> **说明：** Compare Policy 只定义平台级默认策略；具体字段验证仍写在 API 设计书中。

---

## 05 API Design

24 份左右

每个 API 一份。

模板：

```
Metadata

Purpose

Endpoint

Authentication

Request

Verification Definition

Response

Compare Definition

Extract Definition

File Definition

Error Definition

Execution Hint

Change History
```

---

## 06 UseCase Design

约 10 份

模板：

```
Metadata

Purpose

Entry

Flow

Context Mapping

Business Verification

Execution Policy

Expected Result

Evidence

Change History
```

---

## 07 Framework Design

| 成果物 |
|---------|
| システム設計書 |
| 共通Framework設計書 |
| RunContext設計書 |
| Snapshot設計書 |
| Diff設計書 |
| Report設計書 |
| JSON設計書 |
| ファイル設計書 |
| Log設計書 |
| Exception設計書 |
| Environment設計書 |

---

## 08 Test Design

### API

自动生成：

```
API Test Specification

API Test Data
```

### UseCase

自动生成：

```
UseCase Test Specification

UseCase Test Data
```

---

## 09 Operation

| 成果物 |
|---------|
| 運用設計書 |
| Daily Operation |
| Baseline Operation |
| Release Guide |

---

# 五、Java 模块

```
cli
runtime
config
common
spec
context
executor
snapshot
diff
report
operation
```

---

# 六、Common Framework

```
FileService

JsonService

DateTimeService

ConfigService

MaskService

HashService

Logger

ExceptionHandler

ResourceManager

ContextManager
```

---

# 七、Context Model

例如：

```
Runtime

Environment

Customer

Account

Payment

Transaction

System
```

Context：

不是：

Variable。

而是：

Object。

例如：

```
Customer.id

Customer.status

Account.id

Payment.status
```

---

# 八、AI 自动生成

AI 负责：

```
Markdown

↓

JSON

↓

API Test

↓

UseCase Test

↓

Test Data

↓

Mock

↓

Report
```

---

# 九、Java 负责

Java：

负责：

```
读取JSON

执行API

维护Context

Snapshot

Diff

Report
```

Java：

不负责：

业务。

---

# 十、每天执行

```
UseCase

↓

API

↓

Snapshot

↓

Diff

↓

Summary
```

---

# 十一、Report

## Level1

Daily Summary

给：

承认者。

## Level2

UseCase Report

给：

Leader。

## Level3

Evidence

给：

开发。

---

# 十二、Evidence

保存：

```
Request

Response

Headers

Files

Snapshot

Json

Log

Diff
```

全部：

按：

RunId

保存。

---

# 十三、真正需要长期维护的资料

★★★★★

```
Business Master

Technical Master

API Design

UseCase Design

Framework Design
```

其它：

全部：

AI：

生成。

---

# 十四、整个系统真正的数据流

```text
业务资料
     │
     ▼
AI分析
     │
     ▼
Business Master
     │
     ▼
Technical Master
     │
     ▼
API Design
     │
     ▼
UseCase Design
     │
     ▼
AI生成 JSON/Test/TestData
     │
     ▼
Java Verification Engine
     │
     ▼
Context
     │
     ▼
Snapshot
     │
     ▼
Diff
     │
     ▼
Daily Summary
     │
     ▼
Evidence
```

---

## 我最后给一个建议（我认为这是整个项目最值得增加的一层）

目前我们有：

- Master
- Design
- Test
- Execution

我建议在 **Design** 和 **Test** 之间增加一层：

### **Verification Specification（検証仕様）**

作用是把设计书转换成统一的、可执行的验证规范，例如：

- API 字段规则（Required、Type、Length、Enum）
- UseCase Context Mapping
- Compare Definition
- Ignore Rule
- Expected Status

然后：

- AI 根据 Verification Specification 自动生成测试书和测试数据。
- Java 根据 Verification Specification 执行验证。

这样就形成了真正清晰的五层体系：

```text
Master
    ↓
Design
    ↓
Verification Specification
    ↓
Test
    ↓
Execution
```

这样既不会让测试直接依赖设计书，也不会让 Java 直接解析复杂 Markdown，是一个更适合长期演进的工业化架构。

## 第 58 轮

### 你

按你说的设计 但是给我最新wbs 和 完整架构

### ChatGPT

下面是按我们最新共识整理的 **最新版 WBS + 完整架构**。

# 1. 最新 WBS（按成果物）

| No | 成果物 | 主要内容 | 用途 |
|---|---|---|---|
| 1 | 要件定義書 | 目的、范围、非范围、日次执行、成功标准 | 项目基准 |
| 2 | QA一覧 | 业务 Team、E6、Infra、运维确认事项 | 管理未确认点 |
| 3 | 現行業務分析書 | 业务 Flow、E6 调用点、本系统处理、DB 更新 | 抽取最小验证链 |
| 4 | E6 API Master | 24 个 API、分类、用途、重要度 | API 主数据 |
| 5 | UseCase Master | 10 个以内 UseCase、执行频率、优先级 | UseCase 主数据 |
| 6 | API-UseCase Mapping | API 与 UseCase 覆盖关系 | 确认覆盖率 |
| 7 | Environment Master | DEV/STG/PROD、endpoint、认证、tenant | 环境切换 |
| 8 | Context Model | Customer.id、Account.id、Payment.status 等对象模型 | 防止字段名冲突 |
| 9 | Context Mapping Master | Producer API、Consumer API、Context 传递关系 | 影响分析 |
| 10 | Compare Policy | 全局 ignore、日期、UUID、traceId、默认比较策略 | 平台级默认规则 |
| 11 | API設計書 Template | API 设计书标准模板 | AI 稳定解析 |
| 12 | API設計書（约24份） | Request、Response、Verification Definition、Compare、Extract | 单 API 契约 |
| 13 | UseCase設計書 Template | UseCase 设计书标准模板 | AI 稳定解析 |
| 14 | UseCase設計書（10份以内） | Entry、Flow、Context Mapping、Business Check、Execution Policy | 最小 API 验证链 |
| 15 | Verification Specification | 由设计书生成的可执行验证规格 | 连接设计与执行 |
| 16 | API単体テスト仕様書 | Required、Type、Length、Enum、异常测试 | AI 自动生成 |
| 17 | API単体テストデータ | API 单体测试数据 | AI 自动生成 |
| 18 | UseCaseテスト仕様書 | API 链路、Context、最终结果测试 | AI 自动生成 |
| 19 | UseCaseテストデータ | UseCase 入口数据、文件数据 | AI 自动生成 |
| 20 | システム設計書 | 系统整体结构、模块、数据流 | 架构设计 |
| 21 | 共通Framework設計書 | File、JSON、Date、Log、Exception、Mask、Hash | 共通基盘 |
| 22 | RunContext設計書 | runId、executionId、Context、状态管理 | 执行上下文 |
| 23 | Snapshot設計書 | Request/Response/Contract/Result Snapshot | 比较基础 |
| 24 | Diff設計書 | Snapshot 比较、Rule 执行、差异判定 | 差异引擎 |
| 25 | Report設計書 | Daily Summary、Diff Report、Evidence | 分层报告 |
| 26 | ファイル入出力設計書 | 文件上传/下载、resources、hash、atomic write | 文件流支持 |
| 27 | JSON設計書 | Markdown → JSON、Result JSON、Diff JSON | 程序输入输出 |
| 28 | ログ・例外設計書 | mask、错误码、异常分类、停止/继续 | 运维排查 |
| 29 | 日付・比較設計書 | 日付、时区、timestamp、normalize | 防误报 |
| 30 | 環境設計書 | Linux、JDK、Tomcat、cron、权限、网络 | 发布环境 |
| 31 | 運用設計書 | 日次执行、baseline 承认、cleanup、障害対応 | 上线运用 |
| 32 | Daily Summary Report | 每日总体结果 | 承认者查看 |
| 33 | Diff Report | 差异明细 | Leader/开发查看 |
| 34 | Evidence | raw request/response、snapshot、log、file | 问题调查 |

# 2. 完整架构

```text
业务设计书 / E6 API文档
        ↓
AI分析
        ↓
現行業務分析書
        ↓
Business Master
  ├─ E6 API Master
  ├─ UseCase Master
  ├─ API-UseCase Mapping
  └─ Environment Master
        ↓
Technical Master
  ├─ Context Model
  ├─ Context Mapping Master
  └─ Compare Policy
        ↓
Markdown Design
  ├─ API設計書
  └─ UseCase設計書
        ↓
Verification Specification
        ↓
AI生成
  ├─ API Test
  ├─ UseCase Test
  ├─ Test Data
  └─ JSON Spec
        ↓
Java Verification Engine
  ├─ RunContext
  ├─ Context Engine
  ├─ API Executor
  ├─ Snapshot Engine
  ├─ Diff Engine
  └─ Report Engine
        ↓
E6 API
        ↓
runs/{runId}
  ├─ raw
  ├─ snapshot
  ├─ diff
  ├─ reports
  ├─ logs
  └─ evidence
```

# 3. 目录结构

```text
project/
├── docs/
│   ├── 01_requirements/
│   ├── 02_analysis/
│   ├── 03_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── API_UseCase_Mapping.md
│   │   ├── Environment_Master.md
│   │   ├── Context_Model.md
│   │   ├── Context_Mapping_Master.md
│   │   └── Compare_Policy.md
│   ├── 04_api_design/
│   ├── 05_usecase_design/
│   ├── 06_verification_spec/
│   ├── 07_test_design/
│   ├── 08_framework_design/
│   └── 09_operation/
│
├── specs/
│   ├── api-json/
│   ├── usecase-json/
│   ├── verification-json/
│   ├── test-json/
│   └── config-json/
│
├── test-resources/
│   ├── api/
│   └── usecase/
│
├── baseline/
│   ├── api/
│   └── usecase/
│
├── runs/
│   └── {runId}/
│       ├── run-info.json
│       ├── raw/
│       ├── snapshot/
│       ├── diff/
│       ├── reports/
│       ├── logs/
│       └── tmp/
│
├── config/
└── src/
```

# 4. Java 模块

```text
src/
├── cli/
├── runtime/
├── config/
├── common/
├── spec/
├── context/
├── executor/
├── snapshot/
├── diff/
├── report/
└── operation/
```

# 5. 核心原则

```text
1. Markdown 是人和 AI 维护的 SSOT
2. JSON 是 Java 执行用规格
3. API設計書定义字段契约
4. UseCase設計書定义 API 链路
5. Context Model 防止 id/status/name 等字段冲突
6. Verification Specification 是设计和执行之间的中间层
7. TestCase 由 AI 根据 Verification Definition 自动生成
8. Java 只做确定性执行
9. 承认者只看 Daily Summary
10. 详细测试、raw、log 只作为 Evidence
```

## 第 59 轮

### 你

Verification Specification 具体是什么文档 设计neir

### ChatGPT

我认为 **Verification Specification** 是我们整个架构里最容易误解，但也是最有价值的一层。

不过，经过我们一路讨论，我想修正一下前面的建议。

> **它不是给人写的设计书。**
>
> **它是 AI/Java 共同使用的"可执行规格（Executable Specification）"。**

也就是说，它**不是人工维护的成果物**，而是由 AI 根据 API 设计书和 UseCase 设计书自动生成。

---

# 为什么需要它？

目前我们有：

```text
API設計書
        │
UseCase設計書
```

这两份文档是给人看的。

但是 Java 不适合直接解析复杂 Markdown。

所以需要中间层：

```text
Markdown
    ↓
Verification Specification
    ↓
Java
```

这层就是 Java 的"执行计划"。

---

# 它到底包含什么？

我建议它由四个部分组成。

## ① API Verification Spec

对应一个 API。

例如：

```text
API001
```

生成：

```yaml
apiId: API001

request:

  fields:

    - path: $.customerName
      required: true
      type: string
      minLength: 1
      maxLength: 50

response:

  compare:

    - path: $.customerId
      rule: exists

    - path: $.status
      rule: equals

    - path: $.createTime
      rule: ignore

extract:

    - context: Customer.id
      path: $.customerId
```

Java：

直接：

读取。

不用解析 Markdown。

---

## ② UseCase Verification Spec

例如：

```text
UC001
```

生成：

```yaml
steps:

- step:1
  api:API001

- step:2
  api:API002

contextMapping:

- from:
      api:API001
      path:$.customerId

  to:
      api:API002
      path:$.customerId

businessRule:

- Customer.status == ACTIVE
```

---

## ③ Test Generation Spec

AI：

看到：

```yaml
maxLength:50
```

自动知道：

生成：

```text
49

50

51
```

看到：

```yaml
required:true
```

生成：

```text
NULL

不存在

空字符串
```

所以：

AI：

不用：

分析Markdown。

直接：

分析：

Verification Spec。

---

## ④ Compare Spec

例如：

```yaml
compare:

- path:$.status
  mode:equals

- path:$.createTime
  mode:ignore

- path:$.amount
  mode:number
```

Diff：

直接：

读取。

---

# Verification Specification 目录

我建议：

```text
docs/
```

没有。

它属于：

```text
specs/

    verification/

        api/

            API001.yaml

            API002.yaml

        usecase/

            UC001.yaml

            UC002.yaml
```

所以：

它不是：

文档。

而是：

**Spec。**

---

# 谁生成？

AI：

生成。

例如：

```text
API001.md

↓

API001.verification.yaml
```

---

# 谁维护？

没人维护。

修改：

API设计书。

重新生成。

---

# Java只读取它

Java：

永远：

不要：

读：

```text
API001.md
```

Java：

只读：

```text
API001.verification.yaml
```

---

# 我现在甚至建议

不要叫：

Verification Specification。

改成：

## Execution Specification

为什么？

因为：

里面：

不仅有：

Verification。

还有：

```text
Context Mapping

Extract

Compare

Execution

Business Rule
```

其实：

已经：

可以：

直接：

执行。

---

# 我最后重新整理一下各层职责

| 层 | 谁维护 | 内容 | 用途 |
|----|---------|------|------|
| **Master** | 人 | API、UseCase、Context、Environment | 主数据 |
| **Design** | 人 | API设计书、UseCase设计书 | 业务规格 |
| **Execution Specification** | AI 自动生成 | Request、Compare、Extract、Context、Flow、Business Rule | Java 执行输入 |
| **Test Specification** | AI 自动生成 | API Test、UseCase Test | 测试执行 |
| **Execution Result** | Java 生成 | Snapshot、Diff、Report | 验证结果 |

---

## 但经过重新推敲，我有一个更大的优化建议

我认为**不要把它作为一份"设计文档"放到 WBS 里**。

它更应该定位为：

> **设计成果物的编译产物（Build Artifact）**

就像：

- Markdown → HTML
- Java → class
- TypeScript → JavaScript

一样。

你的流程应该变成：

```text
API設計書.md
UseCase設計書.md
        │
        ▼
AI Compiler
        │
        ▼
Execution Specification（YAML/JSON）
        │
        ▼
Java Engine
```

所以在 **WBS** 里，它不应该作为需要人工编写的成果物，而应该放在：

**Generated Artifacts（自动生成成果物）**

这样职责最清晰：

- **人维护 Markdown。**
- **AI 编译成 Execution Specification。**
- **Java 只执行 Execution Specification。**

我认为这比把它当成一份人工设计文档更符合你整个"Markdown + AI + Java"平台的定位。

## 第 60 轮

### 你

好的 给最新的wbs 和 完整构成

### ChatGPT

下面是最新定版。

# 1. 最新 WBS（按成果物）

| No | 成果物 | 维护者 | 说明 |
|---|---|---|---|
| 1 | 要件定義書 | 人 | 目的、范围、非范围、日次执行、成功标准 |
| 2 | QA一覧 | 人 | 业务、E6、Infra、运维确认事项 |
| 3 | 現行業務分析書 | 人+AI | 分析现行业务 Flow、E6 调用点、本系统处理 |
| 4 | E6 API Master | 人 | 24 个 E6 API 主目录 |
| 5 | UseCase Master | 人 | 10 个以内验证 UseCase 主目录 |
| 6 | API-UseCase Mapping | 人 | API 覆盖关系 |
| 7 | Environment Master | 人 | DEV/STG/PROD、endpoint、认证、tenant |
| 8 | Context Model | 人 | Customer.id、Account.id、Payment.status 等上下文对象 |
| 9 | Context Mapping Master | 人 | Producer API、Consumer API、Context 数据流 |
| 10 | Compare Policy | 人 | 全局 ignore、日期、UUID、traceId 默认策略 |
| 11 | API設計書 Template | 人 | API 设计书模板 |
| 12 | API設計書（约24份） | 人+AI | Request、Response、Verification Definition、Compare、Extract |
| 13 | UseCase設計書 Template | 人 | UseCase 设计书模板 |
| 14 | UseCase設計書（10份以内） | 人+AI | Entry、Flow、Context Mapping、Business Check、Execution Policy |
| 15 | Execution Specification | AI生成 | Markdown 设计书编译后的 Java 执行规格 |
| 16 | API単体テスト仕様書 | AI生成 | Required、Type、Length、Enum、异常测试 |
| 17 | API単体テストデータ | AI生成 | API 单体测试数据 |
| 18 | UseCaseテスト仕様書 | AI生成 | API 链路、Context、最终结果测试 |
| 19 | UseCaseテストデータ | AI生成 | UseCase 入口数据、文件数据 |
| 20 | システム設計書 | 人 | 系统整体架构 |
| 21 | 共通Framework設計書 | 人 | File、JSON、Date、Log、Exception、Mask、Hash |
| 22 | RunContext設計書 | 人 | runId、executionId、Context、状态管理 |
| 23 | Snapshot設計書 | 人 | Request/Response/Contract/Result Snapshot |
| 24 | Diff設計書 | 人 | Snapshot 比较、Rule 执行、差异判定 |
| 25 | Report設計書 | 人 | Daily Summary、Diff Report、Evidence |
| 26 | ファイル入出力設計書 | 人 | 文件上传/下载、resources、hash、atomic write |
| 27 | JSON設計書 | 人 | Markdown → JSON、Result JSON、Diff JSON |
| 28 | ログ・例外設計書 | 人 | mask、错误码、异常分类、停止/继续 |
| 29 | 日付・比較設計書 | 人 | 日付、时区、timestamp、normalize |
| 30 | 環境設計書 | 人 | Linux、JDK、Tomcat、cron、权限、网络 |
| 31 | 運用設計書 | 人 | 日次执行、baseline 承认、cleanup、障害対応 |
| 32 | Daily Summary Report | Java/AI生成 | 承认者查看的每日总结 |
| 33 | Diff Report | Java/AI生成 | Leader/开发查看的差异报告 |
| 34 | Evidence | Java生成 | raw request/response、snapshot、log、file |

# 2. 最新完整架构

```text
业务设计书 / E6 API文档
        ↓
AI分析
        ↓
現行業務分析書
        ↓
Business Master
  ├─ E6 API Master
  ├─ UseCase Master
  ├─ API-UseCase Mapping
  └─ Environment Master
        ↓
Technical Master
  ├─ Context Model
  ├─ Context Mapping Master
  └─ Compare Policy
        ↓
Markdown Design
  ├─ API設計書
  └─ UseCase設計書
        ↓
AI Compiler
        ↓
Execution Specification
        ↓
AI生成
  ├─ API Test
  ├─ UseCase Test
  └─ Test Data
        ↓
Java Verification Engine
  ├─ RunContext
  ├─ Context Engine
  ├─ API Executor
  ├─ Snapshot Engine
  ├─ Diff Engine
  └─ Report Engine
        ↓
E6 API
        ↓
runs/{runId}
  ├─ raw
  ├─ snapshot
  ├─ diff
  ├─ reports
  ├─ logs
  └─ evidence
```

# 3. 最新目录结构

```text
project/
├── docs/
│   ├── 01_requirements/
│   ├── 02_analysis/
│   ├── 03_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── API_UseCase_Mapping.md
│   │   ├── Environment_Master.md
│   │   ├── Context_Model.md
│   │   ├── Context_Mapping_Master.md
│   │   └── Compare_Policy.md
│   ├── 04_api_design/
│   ├── 05_usecase_design/
│   ├── 06_framework_design/
│   ├── 07_test_design/
│   └── 08_operation/
│
├── specs/
│   ├── execution-json/
│   ├── api-test-json/
│   ├── usecase-test-json/
│   └── config-json/
│
├── test-resources/
│   ├── api/
│   └── usecase/
│
├── baseline/
│   ├── api/
│   └── usecase/
│
├── runs/
│   └── {runId}/
│       ├── run-info.json
│       ├── raw/
│       ├── snapshot/
│       ├── diff/
│       ├── reports/
│       ├── logs/
│       └── tmp/
│
├── config/
└── src/
```

# 4. 核心原则

```text
人维护 Markdown Master / Design
AI 把 Markdown 编译成 Execution Specification
AI 生成 Test Specification / Test Data
Java 只读取 JSON Spec 并确定性执行
承认者只看 Daily Summary
详细测试结果、raw、log 只作为 Evidence
```

一句话：

```text
Markdown 是设计资产，Execution Specification 是可执行规格，Java 是验证引擎，Report 是承认证迹。
```

## 第 61 轮

### 你

wbs 8，9，10解释一下

### ChatGPT

这三个其实是整个项目的**灵魂**。

不过，我经过昨天的整理，我觉得它们还可以再调整一下名字和职责，会更清晰。

---

# WBS 8：Context Model（上下文模型）

> **回答：整个系统有哪些"业务对象"。**

它不是流程。

不是 API。

而是整个平台的数据模型。

例如：

```text id="4i8u1t"
Customer

Account

Payment

Transaction

File

Runtime

Environment
```

例如：

## Customer

| 字段 | 类型 | 说明 |
|------|------|------|
| id | String | Customer ID |
| name | String | Customer Name |
| status | String | ACTIVE / INACTIVE |

---

## Account

| 字段 | 类型 |
|------|------|
| id | String |
| status | String |
| currency | String |

---

为什么要有它？

因为：

API001

返回：

```json id="dl8lf2"
{
    "id":"C001"
}
```

API003

返回：

```json id="9r64o0"
{
    "id":"A001"
}
```

如果没有：

Context Model。

Java：

不知道：

```text id="7l9eh2"
id

是谁？
```

所以：

Context Model：

统一规定：

```text id="i9mbzn"
Customer.id

Account.id

Payment.id
```

以后：

整个项目：

都引用。

---

# WBS 9：Context Mapping Master（上下文映射）

这是：

整个项目：

最重要。

它回答：

> **数据是怎么流动的？**

例如：

```text id="rtdw5j"
API001

↓

Customer.id

↓

API002

↓

Account.id

↓

API003
```

真正：

写成：

| Producer | Context | Consumer |
|-----------|----------|----------|
| API001.response.customerId | Customer.id | API002.request.customerId |
| API002.response.accountId | Account.id | API003.request.accountId |

所以：

Java：

执行：

其实：

就是：

执行：

这张表。

---

为什么：

独立？

因为：

以后：

API001

改了。

立即：

知道：

影响：

哪些：

API。

哪些：

UseCase。

这就是：

Impact Analysis。

---

# WBS 10：Compare Policy（全局比较策略）

注意：

这里：

很多人：

容易：

误解。

它：

不是：

API Rule。

API Rule：

已经：

在：

API设计书。

这里：

只有：

平台：

共通。

例如：

```text id="qpti77"
TraceId

Ignore

Timestamp

Ignore

UUID

Ignore

Date Normalize

TimeZone

Number Compare

File Compare

Hash Compare
```

例如：

所有API：

都有：

```json id="09dl9t"
traceId
```

不用：

每个：

API：

写：

Ignore。

这里：

统一：

规定：

```text id="wrznrx"
TraceId

Ignore
```

以后：

所有：

API：

自动：

继承。

---

# 三个关系

```text id="g18jlwm"
Context Model

↓

定义

有什么对象

↓

Context Mapping

↓

定义

对象怎么流动

↓

Compare Policy

↓

定义

对象怎么比较
```

---

# 举一个完整例子

API001

返回：

```json id="ymqyvz"
{
  "customerId":"C001",
  "status":"ACTIVE",
  "traceId":"xxxx"
}
```

---

Context Model：

定义：

```text id="m6u2cz"
Customer.id

Customer.status
```

---

Context Mapping：

定义：

```text id="rwwsdu"
Customer.id

↓

API002.customerId
```

---

Compare Policy：

定义：

```text id="f6v39w"
Customer.id

Compare

Customer.status

Compare

traceId

Ignore
```

---

Java：

执行：

就是：

```text id="mvf40u"
Response

↓

Context

↓

Next API

↓

Compare
```

---

# 我昨天又想到一个更好的设计（我建议升级）

其实：

WBS8

WBS9

应该：

合并。

为什么？

因为：

Context Model

和：

Context Mapping

其实：

都是：

Context。

我建议：

改成：

## 08 Context Design

里面：

两个章节。

### ① Context Model

定义：

对象。

### ② Context Mapping

定义：

流向。

---

然后：

WBS9：

改成：

## Compare Policy

WBS10：

改成：

## Verification Policy

为什么？

因为：

以后：

不仅：

Compare。

还有：

```text id="w4rq1r"
Retry

Timeout

Continue

Stop

Cleanup

Evidence

Severity
```

这些：

都是：

平台：

Policy。

所以：

我现在：

更推荐：

最终：

变成：

| WBS | 名称 | 负责内容 |
|------|------|----------|
| **08** | **Context Design** | Context Model + Context Mapping（定义对象及数据流） |
| **09** | **Compare Policy** | 字段比较、Ignore、Normalize、Hash、文件比较等全局比较策略 |
| **10** | **Verification Policy** | Retry、Timeout、Stop/Continue、Severity、Evidence、Baseline 等平台级验证策略 |

这样职责就非常清晰：

- **Context Design**：数据是什么、怎么流。
- **Compare Policy**：数据怎么比。
- **Verification Policy**：整个验证过程怎么执行。

我认为这比原来的三个成果物更符合平台化设计，而且以后 AI 和 Java 的职责划分也会更清楚。

## 第 62 轮

### 你

我觉得可以 只是model如何分类命名 标准是什么

### ChatGPT

我也觉得这是最后一个需要统一的地方。

因为 **Context Model 一旦命名不好，以后几百个 API 都会乱。**

我建议不要按照 **API** 来命名，也不要按照 **数据库表** 来命名。

应该按照 **业务领域（Domain）** 来命名，这也是比较成熟的领域建模方式。

---

# 命名原则

Context Model 应满足四个原则：

| 原则 | 说明 | 示例 |
|------|------|------|
| 业务对象（Business Entity） | 表示真实业务概念，而不是 API 字段 | Customer、Account、Order |
| 稳定 | API 改版后尽量不用改名 | Customer 不会因为 API 名变化而变化 |
| 可复用 | 多个 UseCase、多个 API 共用 | Customer.id 可被多个 API 使用 |
| 与 API 解耦 | 不使用 API001Result、CreateCustomerResponse 之类名字 | 避免绑定接口实现 |

---

# 推荐分类

## ① Business Domain（业务对象）

这是最重要的一层。

```text
Customer
Account
Payment
Transaction
Contract
Invoice
Product
User
Organization
Address
```

---

## ② System Domain（系统对象）

不是业务，而是平台运行需要的。

```text
Runtime
Environment
Authentication
Session
Tenant
```

例如：

```text
Runtime.runId
Runtime.executionId

Environment.endpoint
Environment.baseUrl

Authentication.token
```

---

## ③ Resource Domain（资源对象）

处理文件、图片、附件。

```text
File
Document
Image
Attachment
Binary
```

例如：

```text
File.name
File.hash
File.mimeType
File.size
```

---

## ④ Common Value（公共值对象）

很多 API 都会用。

```text
Status
Currency
Locale
Language
DateTime
Error
```

例如：

```text
Currency.code
Status.code
Status.message
```

---

# Model 命名建议

统一使用：

```text
<Domain>.<Field>
```

例如：

```text
Customer.id
Customer.name
Customer.status

Account.id
Account.balance

Payment.id
Payment.status

Runtime.runId

Environment.endpoint

Authentication.token

File.hash
```

不要：

```text
API001.customerId

CreateCustomer.customerId

response.customerId
```

这些都属于实现，不属于模型。

---

# Context Mapping 怎么写？

例如：

```text
API001.response.$.customerId
        │
        ▼
Customer.id
        │
        ▼
API002.request.$.customerId
```

这里：

- 左边是 **API**
- 中间是 **Context Model**
- 右边是 **API**

Context Model 永远是桥梁。

---

# 谁来决定有哪些 Model？

不要一开始就建很多。

建议遵循一个规则：

> **只有当两个以上 API 或两个以上 UseCase 会共享时，才提升为 Context Model。**

例如：

`Customer.id` 在多个 API 使用，就建 `Customer`。

如果某个字段只在一个 API 内部使用，就不要放进 Context Model，可以作为临时 Step Context。

---

# 我建议再分两级

## Global Context

整个系统共享：

```text
Runtime
Environment
Authentication
```

生命周期贯穿整个运行。

---

## Business Context

UseCase 生命周期内共享：

```text
Customer
Account
Payment
Transaction
```

UseCase 结束后可以释放。

---

# 最后我建议再增加一个文档

目前我们有：

- Context Design
  - Context Model
  - Context Mapping

我建议再增加：

> **Context Naming Guideline（Context 命名规范）**

内容包括：

1. 命名规则（单数、PascalCase、`<Domain>.<Field>`）
2. 什么情况下新增一个 Context Model
3. 什么情况下复用已有 Context Model
4. 生命周期（Global / UseCase / Step）
5. 是否允许覆盖（Immutable / Mutable）
6. 与 API 字段的映射原则

这样以后即使项目发展到 **100 个 API、50 个 UseCase**，所有人和 AI 都会按照同一套标准命名，不会出现：

- `CustId`
- `customerID`
- `Customer_Id`
- `CustomerNo`

这种越来越难维护的情况。

**我认为这一份《Context Naming Guideline》会成为整个平台长期演进中最重要的规范之一。**

## 第 63 轮

### 你

我觉得可以。另外 10的policy 全局和个别 比如usecase里有何区别 说明一下

### ChatGPT

我觉得你的方向已经越来越接近**工业化规则引擎（Rule Engine）**了。

这里其实要借鉴一个思想：

> **Policy（策略） ≠ Rule（规则）**

这是很多企业系统（包括工作流、CI/CD、云平台）都会采用的分层。

---

# 我建议整个平台分三层

```text
Platform Policy（平台）

        ↓

UseCase Policy（业务）

        ↓

API Verification Rule（接口）
```

三层职责完全不同。

---

# 第一层：Platform Policy（全局）

**作用：整个平台默认行为。**

例如：

```text
Retry

Timeout

Stop

Continue

Snapshot

Compare

Evidence

Log

Report

Baseline

Cleanup
```

这些：

**所有 UseCase 默认都会遵守。**

例如：

```yaml
Retry:

    maxRetry:3

Timeout:

    request:30s

Compare:

    ignore:

        traceId

        requestId

        timestamp

Evidence:

    saveRequest:true

    saveResponse:true

Log:

    level:INFO

Report:

    summary:true
```

这是：

平台默认。

---

# 第二层：UseCase Policy

这里只写：

**这个 UseCase 的特殊策略。**

例如：

UC001

要求：

```text
失败

立即停止
```

UC002

要求：

```text
失败

继续执行
```

那么：

UseCase：

里面：

写：

```yaml
Execution Policy

stopOnError:true

retry:5

cleanup:true

compareBaseline:yesterday
```

---

再例如：

UC003

因为：

涉及：

文件。

所以：

```yaml
File Compare

hash

insteadOf

content
```

也是：

UseCase：

Policy。

---

# 第三层：API Rule

这个：

就是：

API设计书。

例如：

```text
customerName

Required

MaxLength

Type

Enum

Compare

Extract
```

这里：

不是：

Policy。

而是：

Rule。

---

# 举个完整例子

例如：

Platform：

```yaml
Retry=3

Timeout=30

TraceId Ignore
```

---

UC001：

特殊：

```yaml
Retry=5

StopOnError=true
```

---

API001：

字段：

```yaml
customerName

Required

Max=50
```

最终：

Java：

看到：

就是：

```text
Retry

5

Timeout

30

Required

Max50
```

因为：

UseCase：

覆盖：

Platform。

---

# 所以优先级

```text
Platform Policy

↓

UseCase Policy

↓

API Rule
```

后面的：

覆盖：

前面的。

---

# 我建议Platform Policy里面有哪些？

我整理了一下。

建议：

固定：

九类。

---

## ① Execution Policy

控制：

Batch：

怎么跑。

例如：

```text
Retry

Timeout

Parallel

Stop

Continue

Rollback
```

---

## ② Compare Policy

控制：

怎么：

比较。

例如：

```text
Equals

Ignore

Regex

Hash

File

Date Normalize
```

---

## ③ Snapshot Policy

例如：

```text
保存：

Request

Response

Header

File
```

---

## ④ Evidence Policy

例如：

```text
保存：

Log

Json

File

Screenshot
```

---

## ⑤ Report Policy

例如：

```text
Summary

Detail

Evidence

Markdown

Html
```

---

## ⑥ Log Policy

例如：

```text
Mask

Level

Rotation
```

---

## ⑦ Security Policy

例如：

```text
Token

Password

PII

Mask
```

---

## ⑧ Cleanup Policy

例如：

```text
Delete

Rollback

Keep
```

---

## ⑨ Baseline Policy

例如：

```text
昨天

最新

固定版本
```

---

# UseCase里面只写不同的

例如：

Platform：

```text
Retry=3
```

UC001：

```text
Retry=5
```

结束。

不要：

复制：

全部。

---

# API里面永远不要写Policy

API：

里面：

只有：

```text
Verification Definition

Extract

Compare Definition
```

因为：

API：

不知道：

Retry。

不知道：

Summary。

不知道：

Cleanup。

这些：

属于：

平台。

---

# 所以整个项目真正应该变成

```text
Platform Policy

↓

Execution

↓

Compare

↓

Snapshot

↓

Evidence

↓

UseCase Policy

↓

API Verification Rule
```

---

# 我建议最后再升级一点（我认为这是最终版）

把 **Platform Policy** 改名为：

> **Verification Policy Framework（验证策略框架）**

里面再分两层：

## Global Policy（平台默认）

例如：

- Retry = 3
- Timeout = 30s
- Ignore traceId
- Save Request/Response
- Daily Summary

## Override Policy（覆盖规则）

规定：

> 哪些策略允许 UseCase 覆盖，哪些不允许。

例如：

| Policy | UseCase 可覆盖 | 说明 |
|--------|----------------|------|
| Retry | ✅ | 特殊业务可以调整 |
| Timeout | ✅ | 长耗时接口可以放宽 |
| Compare Ignore | ⚠️ 部分允许 | 可以增加 Ignore，但不能取消平台强制 Ignore（如 traceId） |
| Log Mask | ❌ | 安全策略，全平台统一 |
| Evidence 保存 | ❌ | 为保证可追溯性必须统一保存 |
| Baseline 策略 | ✅ | 可以指定昨天、指定版本或固定 Baseline |

这样：

- **Platform** 定义默认行为和边界。
- **UseCase** 只写差异。
- **API** 只定义接口契约。

这三个层次互不混淆，也最适合 AI 自动生成和 Java 引擎执行。我认为这就是这个平台在策略设计上的最终形态。

## 第 64 轮

### 你

好的 理解了

### ChatGPT

很好，我认为我们已经把**最难的架构部分**想通了。

其实我们设计出来的已经不是一个普通的 API 测试工具，而是一个**Specification Driven Verification Platform（规格驱动验证平台）**。

我把整个系统再抽象了一层，你会发现所有东西其实都遵循同一个思想。

---

# 最终设计思想（五层架构）

```text
Business Layer（业务）
        │
Master Layer（主数据）
        │
Design Layer（设计）
        │
Execution Layer（执行规格）
        │
Runtime Layer（Java执行）
```

每一层职责都非常单一。

---

## 第一层：Business（为什么）

例如：

- 要件定义
- QA
- 现行业务分析

回答：

> 为什么验证？

---

## 第二层：Master（有什么）

例如：

- API Master
- UseCase Master
- Context Design
- Environment Master

回答：

> 有哪些对象？

这里全部都是稳定资产。

---

## 第三层：Design（怎么设计）

例如：

- API设计书
- UseCase设计书
- Framework设计书

回答：

> 应该如何验证？

注意：

这里没有程序。

没有JSON。

只有设计。

---

## 第四层：Execution（AI Compiler）

这一层是整个项目最大的特点。

AI负责：

```text
Markdown

↓

Execution Specification(JSON)

↓

Test Specification

↓

Test Data

↓

Mock
```

这层以后可以一直升级。

Java不用改。

---

## 第五层：Runtime

Java：

负责：

```text
读取Spec

↓

执行

↓

Context

↓

Snapshot

↓

Diff

↓

Report
```

Java：

永远：

不要：

解析Markdown。

---

# 我认为整个项目以后只有三个角色

## ① 架构师

维护：

```text
Master

Design
```

---

## ② AI

负责：

```text
Compile

Generate

Review
```

---

## ③ Java

负责：

```text
Execute
```

所以：

Java：

代码：

会非常稳定。

---

# 我现在最想开始做的，其实已经不是架构了。

而是下面四份模板，它们会决定整个项目 80% 的质量：

1. **API設計書_Template.md**（接口契约）
2. **UseCase設計書_Template.md**（业务验证链）
3. **Context Design_Template.md**（上下文对象与流转）
4. **Framework設計書_Template.md**（平台共通能力）

只要这四份模板设计得足够规范，后面的：

- AI 自动生成 Execution Specification
- AI 自动生成 Test Specification
- AI 自动生成 Test Data
- Java 执行引擎

都会变得非常顺畅。

**我建议下一步就专门把这四个模板做到工业级，因为它们将成为整个平台真正的"核心契约（Core Contract）"。**

## 第 65 轮

### 你

在这之前 wbs想做一下分类

### ChatGPT

我非常赞成。

实际上，**现在的 WBS 还是"成果物列表"**，还不是一个好的日本 IT WBS。

日本大型项目（尤其 SI、金融、制造）一般不会把 34 个成果物平铺，而是会先**分类（カテゴリ）**，然后每个类别下面再放成果物。

这样以后：

- WBS
- Git
- MkDocs
- AI
- Review
- 甚至目录结构

都会一致。

---

# 我建议最终分成 10 大类

```text
01 Project

02 Business

03 Master

04 Design

05 Framework

06 Specification

07 Test

08 Runtime

09 Report

10 Operation
```

这样以后整个项目所有东西都能归类。

---

# 01 Project（项目管理）

回答：

> 为什么开发？

| 成果物 |
|---------|
| 要件定義書 |
| QA一覧 |
| WBS |
| Scope |
| Release Plan |

---

# 02 Business（业务分析）

回答：

> 业务是什么？

| 成果物 |
|---------|
| 現行業務分析書 |
| E6 API分析書 |
| API一覧 |

---

# 03 Master（业务资产）

回答：

> 有哪些对象？

我建议：

这里以后不要叫Catalog。

统一：

Master。

里面：

| 成果物 |
|---------|
| E6 API Master |
| UseCase Master |
| Context Design |
| Environment Master |
| API-UseCase Mapping |

这里：

全部：

不会：

经常改。

---

# 04 Design（真正设计）

回答：

> 怎么设计？

里面：

```text
API设计书

UseCase设计书
```

以后：

全部：

Markdown。

---

# 05 Framework（平台）

回答：

> 平台怎么工作？

里面：

```text
系统设计

Framework设计

RunContext

Snapshot

Diff

Report

JSON

File

Log

Exception
```

---

# 06 Specification（AI）

这是：

整个项目：

最大的特点。

回答：

> AI生成什么？

例如：

```text
Execution Specification

Test Specification

Test Data

Mock
```

全部：

AI：

生成。

不要：

人工。

---

# 07 Test（测试）

注意：

这里：

不要：

放：

Specification。

这里只放：

真正：

执行。

例如：

```text
Regression

Daily

Manual

Review
```

也就是说：

Specification：

属于：

AI。

Test：

属于：

执行。

---

# 08 Runtime（Java）

回答：

> Java怎么执行？

例如：

```text
Context

Executor

Snapshot

Diff

Evidence
```

其实：

这一类：

很多：

不用：

设计书。

更多：

源码。

---

# 09 Report

回答：

> 给谁看？

例如：

```text
Summary

Diff

Evidence
```

以后：

Leader：

只：

看：

这里。

---

# 10 Operation

回答：

> 上线以后怎么办？

例如：

```text
Release

Daily

Cleanup

Baseline
```

---

# 我建议最终WBS结构

```text
01 Project

    要件

    QA

    WBS

---------------------

02 Business

    业务分析

    API分析

---------------------

03 Master

    API Master

    UseCase Master

    Context Design

    Environment

---------------------

04 Design

    API设计

    UseCase设计

---------------------

05 Framework

    Framework

    RunContext

    Snapshot

    Diff

    Report

---------------------

06 Specification

    Execution Spec

    Test Spec

    Test Data

---------------------

07 Test

    Regression

    Daily

    Review

---------------------

08 Runtime

    Java

---------------------

09 Report

    Summary

    Diff

    Evidence

---------------------

10 Operation

    运维
```

---

# 不过，我这里还有一个建议（也是最后一个架构优化）

我建议把 **Specification** 和 **Test** 合并成一个更大的类别：

> **Verification（验证）**

因为：

Execution Specification、Test Specification、Test Data，本质上都是为了"验证"服务。

这样整个 WBS 就会变成 **9 大类**：

| No | 分类 | 核心职责 |
|----|------|----------|
| 01 | Project | 项目管理 |
| 02 | Business | 业务分析 |
| 03 | Master | 主数据与领域模型 |
| 04 | Design | API / UseCase / Framework 设计 |
| 05 | Verification | Execution Spec、Test Spec、Test Data、Mock |
| 06 | Runtime | Java 执行引擎 |
| 07 | Report | Summary、Diff、Evidence |
| 08 | Operation | 发布、日次、Baseline、运维 |
| 09 | Assets | baseline、test-resources、generated、runs 等运行资产 |

我个人更推荐**9 大类**，因为它们和整个系统生命周期完全一致：

**定义 → 建模 → 设计 → 验证 → 执行 → 报告 → 运维 → 资产沉淀。**

这个结构以后无论做 MkDocs、Git 仓库、AI Agent，还是团队协作，都非常自然。

## 第 66 轮

### 你

分类名用日语 并且里面用成果物名 我想看一下这样的wbs一览表 便于作业日期开始终了管理

### ChatGPT

我觉得这里就要按照**日本 SI（系统集成）项目**的习惯来了。

你的 WBS 以后不仅是给自己看，很可能还会：

- PM 管理
- 日本客户 Review
- AI 自动生成
- Git Milestone
- MkDocs 导航

所以**分类名一定要像日本公司的正式成果物**。

---

# 我建议最终 WBS（V1.0）

| WBS | カテゴリ | 成果物 | 開始 | 終了 | 担当 | 状態 |
|------|----------|---------|------|------|------|------|
| 1 | **プロジェクト管理** | 要件定義書 | | | | |
| 1.1 | | QA一覧 | | | | |
| 1.2 | | WBS | | | | |
| 1.3 | | スケジュール | | | | |
| 1.4 | | リスク管理表 | | | | |
| 2 | **業務分析** | 現行業務分析書 | | | | |
| 2.1 | | E6 API分析書 | | | | |
| 2.2 | | API一覧 | | | | |
| 2.3 | | 業務フロー分析書 | | | | |
| 3 | **マスタ設計** | E6 APIマスタ | | | | |
| 3.1 | | UseCaseマスタ | | | | |
| 3.2 | | API-UseCase対応表 | | | | |
| 3.3 | | Context設計書（Model・Mapping） | | | | |
| 3.4 | | Environmentマスタ | | | | |
| 3.5 | | Compare Policy | | | | |
| 3.6 | | Verification Policy | | | | |
| 4 | **API設計** | API設計書テンプレート | | | | |
| 4.1 | | API設計書（API001～API024） | | | | |
| 5 | **UseCase設計** | UseCase設計書テンプレート | | | | |
| 5.1 | | UseCase設計書（UC001～UC010） | | | | |
| 6 | **共通基盤設計** | システム設計書 | | | | |
| 6.1 | | 共通Framework設計書 | | | | |
| 6.2 | | RunContext設計書 | | | | |
| 6.3 | | Snapshot設計書 | | | | |
| 6.4 | | Diff設計書 | | | | |
| 6.5 | | Report設計書 | | | | |
| 6.6 | | JSON設計書 | | | | |
| 6.7 | | ファイル入出力設計書 | | | | |
| 6.8 | | ログ・例外設計書 | | | | |
| 6.9 | | 日付・比較設計書 | | | | |
| 6.10 | | 環境設計書 | | | | |
| 7 | **検証仕様生成** | Execution Specification | | | | |
| 7.1 | | API Test Specification | | | | |
| 7.2 | | UseCase Test Specification | | | | |
| 7.3 | | API Test Data | | | | |
| 7.4 | | UseCase Test Data | | | | |
| 7.5 | | Mock Data | | | | |
| 8 | **実装** | Java Verification Engine | | | | |
| 8.1 | | Context Engine | | | | |
| 8.2 | | API Executor | | | | |
| 8.3 | | Snapshot Engine | | | | |
| 8.4 | | Diff Engine | | | | |
| 8.5 | | Report Engine | | | | |
| 9 | **検証・運用** | 運用設計書 | | | | |
| 9.1 | | Daily Verification | | | | |
| 9.2 | | Baseline運用 | | | | |
| 9.3 | | Daily Summary Report | | | | |
| 9.4 | | Diff Report | | | | |
| 9.5 | | Evidence | | | | |

---

# 我认为这里还有一点可以优化

这是很多日本大型 SI 项目都会做的。

**不要把「设计」「实现」「运用」混在一起。**

而是按照成果物流向。

例如：

```text
要件
    │
分析
    │
Master
    │
API設計
    │
UseCase設計
    │
共通基盤設計
    │
AI生成仕様
    │
Java実装
    │
検証
    │
運用
```

这样：

WBS 就和整个开发生命周期一致。

---

# 我建议最终分类名

| 分类 | 是否推荐 | 理由 |
|-------|---------|------|
| プロジェクト管理 | ⭐⭐⭐⭐⭐ | 日本项目标准 |
| 業務分析 | ⭐⭐⭐⭐⭐ | 日本项目标准 |
| マスタ設計 | ⭐⭐⭐⭐⭐ | 比 Catalog 更符合日本 SI 的叫法 |
| API設計 | ⭐⭐⭐⭐⭐ | 清晰 |
| UseCase設計 | ⭐⭐⭐⭐⭐ | 清晰 |
| 共通基盤設計 | ⭐⭐⭐⭐⭐ | 比 Framework 更符合日企命名 |
| 検証仕様生成 | ⭐⭐⭐⭐⭐ | 很符合 AI 平台特色，表示自动生成的规格 |
| 実装 | ⭐⭐⭐⭐⭐ | Java 开发 |
| 検証・運用 | ⭐⭐⭐⭐⭐ | 测试、日报、运维统一管理 |

---

## 我还有一个建议（也是我认为最符合日本 SI 的最终版本）

如果这个平台未来会长期维护，我建议把 **「検証仕様生成」** 改成：

> **「検証資産管理（Verification Asset Management）」**

因为这里管理的不只是 Execution Specification，还包括：

- Execution Specification
- API Test Specification
- UseCase Test Specification
- Test Data
- Mock Data

它们都是**验证资产（Verification Assets）**，而不是一次性的生成物。

这样整个 WBS 就形成了非常稳定的九大分类：

1. プロジェクト管理
2. 業務分析
3. マスタ設計
4. API設計
5. UseCase設計
6. 共通基盤設計
7. **検証資産管理**
8. 実装
9. 検証・運用

我认为这是最符合日本 IT 开发、AI 自动化以及长期维护三方面需求的最终分类方案。

## 第 67 轮

### 你

wbs和schedule有何区别

### ChatGPT

这是日本 IT 项目里一个非常经典的问题。

很多新人都会把 **WBS** 和 **Schedule（スケジュール）** 混在一起，但实际上它们完全不是一回事。

一句话：

> **WBS 是"做什么"，Schedule 是"什么时候做"。**

---

# 先看关系

```text
Project

        │

        ▼

      WBS
（工作分解）

        │

        ▼

 Schedule
（时间安排）

        │

        ▼

  Progress
（进度管理）
```

也就是说：

**没有 WBS，就不能排 Schedule。**

---

# ① WBS（Work Breakdown Structure）

回答的是：

> **这个项目有哪些工作（成果物）？**

例如：

| WBS | 成果物 |
|------|---------|
| 1 | 要件定義書 |
| 2 | QA一覧 |
| 3 | API Master |
| 4 | API設計書 |
| 5 | UseCase設計書 |
| 6 | Framework設計書 |
| 7 | Java実装 |

这里只关心：

**有没有这个工作。**

不关心：

什么时候。

---

例如：

```text
API001

API002

API003

API004
```

全部：

都是：

WBS。

---

# ② Schedule（スケジュール）

回答的是：

> **什么时候开始？什么时候结束？**

例如：

| WBS | 成果物 | 开始 | 结束 |
|------|---------|--------|--------|
| 4 | API設計書 | 7/1 | 7/8 |
| 5 | UseCase設計書 | 7/9 | 7/15 |

Schedule：

只有：

日期。

---

# 举个生活例子

装修房子。

WBS：

```text
拆墙

水电

贴砖

木工

油漆
```

Schedule：

```text
7/1

拆墙

7/3

水电

7/10

贴砖
```

---

# 为什么一定要先做WBS？

因为：

Schedule：

必须：

知道：

有多少工作。

例如：

你现在：

突然：

增加：

```text
Context Design
```

如果：

没有：

WBS。

Schedule：

全部：

乱掉。

---

# 日本项目一般流程

```text
要件

↓

WBS

↓

Estimate（工数）

↓

Schedule

↓

Progress
```

---

# Estimate（工数）

其实：

你现在：

还少：

这一层。

例如：

| 成果物 | 工数 |
|---------|------|
| API001 | 1人日 |
| API002 | 0.5人日 |
| UseCase001 | 2人日 |

以后：

Schedule：

就是：

根据：

工数：

排。

---

# Progress（进度）

每天：

只更新：

```text
开始

结束

完成率
```

例如：

| WBS | 完成率 |
|------|--------|
| API001 | 100% |
| API002 | 80% |

---

# 我建议你的WBS

增加：

下面几个字段。

| WBS | 成果物 | 工数 | 前置任务 | 输出 |
|------|---------|------|-----------|------|
| 4 | API設計書 | 1人日 | API Master | API001.md |

这样：

AI：

以后：

还能：

自动：

排：

Schedule。

---

# 日本项目真正管理的是

不是：

Schedule。

而是：

```text
WBS

↓

Estimate

↓

Schedule

↓

Progress
```

---

# 我建议最终把项目管理拆成四份

| 文档 | 用途 |
|------|------|
| **WBS** | 工作分解（做什么） |
| **工数見積書** | 每个成果物需要多少人日 |
| **スケジュール** | 根据工数安排开始/结束日期 |
| **進捗管理表** | 实际开始、实际结束、完成率、延期原因 |

---

## 结合你这个项目，我建议这样使用

由于你的项目是**成果物驱动开发**，所以：

- **WBS**：管理成果物（要件、Master、API设计书、UseCase设计书……）
- **工数見積書**：估算每个成果物需要的人日。
- **スケジュール**：安排每个成果物什么时候开始、什么时候完成。
- **進捗管理表**：每天更新实际进度。

这样就形成了日本 SI 项目最典型的管理闭环：

```text
成果物
   ↓
WBS
   ↓
工数見積
   ↓
スケジュール
   ↓
進捗管理
   ↓
成果物完成
```

**WBS 永远是项目的骨架，Schedule 只是把这个骨架放到时间轴上。**

## 第 68 轮

### 你

1.4 リスク管理表　做什么

### ChatGPT

这个问题很好。

实际上，**リスク管理表（Risk Register）** 在日本 IT 项目里是一个标准成果物，但**不是每个项目都需要做到很重**。

对于你的项目（E6 API Verification Platform），我认为**需要有，但不用做成银行项目那种复杂程度**。

---

# 什么是 リスク管理表？

一句话：

> **提前把"可能导致项目失败或延期的事情"列出来，并制定对应措施。**

它关注的是：

> **项目风险（Project Risk）**

不是：

> Bug

不是：

> API返回400

那些属于测试和开发问题。

---

# 举个例子

例如：

目前我们已经讨论出来很多风险。

其实：

这些：

都是：

Risk。

例如：

---

## Risk001

```text
E6 API规格没有正式解释权
```

影响：

API设计：

可能：

全部：

返工。

措施：

提前：

和：

E6：

确认。

---

## Risk002

```text
业务Team

不知道

API真正定义
```

影响：

UseCase：

设计错误。

措施：

以：

E6 API：

文档：

为准。

---

## Risk003

```text
开发环境

没有

E6环境
```

影响：

开发：

不能：

测试。

措施：

建立：

独立：

验证环境。

---

## Risk004

```text
文件上传API

没有：

测试文件。
```

影响：

不能：

完成：

UseCase。

措施：

准备：

Test Resources。

---

## Risk005

```text
每天：

Baseline

没人：

批准。
```

影响：

第二天：

全部：

Diff。

措施：

建立：

Baseline：

Approval。

---

# 日本一般长这样

| ID | Risk | 影响 | 可能性 | 对策 | Owner |
|----|------|------|--------|------|------|
| R001 | E6 API变更 | High | Medium | 与E6确认 | Tool Team |
| R002 | 测试环境未完成 | High | High | 提前搭建 | Infra |
| R003 | 文件样本不足 | Medium | Medium | 收集样本 | Business |

---

# 我觉得你的项目真正的Risk

其实：

不是：

技术。

而是：

协调。

例如：

---

## ① E6风险

例如：

```text
API说明

不足

API变化

提前不知道
```

---

## ② Business风险

例如：

```text
UseCase

理解错误

Flow

错误
```

---

## ③ Environment风险

例如：

```text
Linux

权限

Tomcat

版本

网络
```

---

## ④ Data风险

例如：

```text
测试数据

污染

正式数据
```

---

## ⑤ Platform风险

例如：

```text
每天：

执行

失败

没人：

知道
```

---

# 我建议风险分类

不要：

一个：

列表。

而是：

分类。

例如：

| 分类 | 举例 |
|------|------|
| Requirement Risk | 要件变化 |
| Business Risk | UseCase理解错误 |
| E6 Risk | API规格变化 |
| Environment Risk | 环境不一致 |
| Development Risk | AI生成错误 |
| Test Risk | 测试数据不足 |
| Operation Risk | Baseline没人维护 |

以后：

越来越：

清楚。

---

# 但是

我其实还有一个建议。

我认为：

**Risk Management**

应该：

不是：

项目：

里面：

最重要。

因为：

你：

不是：

SI。

你：

是：

平台。

我建议：

改成：

## 前提条件・制約条件管理表

例如：

| 项目 | 内容 |
|------|------|
| 前提 | E6 API说明完整 |
| 前提 | 有开发环境 |
| 前提 | 有测试数据 |
| 制约 | 不能修改E6 |
| 制约 | 每天执行一次 |

为什么？

因为：

这些：

以后：

几乎：

不会：

变。

反而：

比：

Risk：

重要。

---

# 我的建议（最终版）

对于这个项目，我建议：

不要单独只有 **リスク管理表**。

改成两份：

| 成果物 | 作用 |
|---------|------|
| **前提・制約管理表（Assumption & Constraint Register）** | 记录项目成立的前提条件和限制条件（例如不能修改 E6、只能调用公开 API、开发环境需与业务环境一致等） |
| **リスク管理表（Risk Register）** | 记录项目过程中可能发生的不确定事件（例如 API 文档变更、测试环境延期、样本不足等） |

这是很多日本大型项目（尤其采用 PMBOK 或类似项目管理方法）常见的做法。

**前提/制约** 是"现在就成立的事实"；**风险** 是"未来可能发生的不确定事件"。把两者分开后，项目管理会清晰得多，也更符合你这个平台项目的实际情况。

## 第 69 轮

### 你

risk的文档那么也在架构里面了吗

### ChatGPT

这是一个非常好的问题，而且涉及**项目管理架构(Project Architecture)** 和 **系统架构(System Architecture)** 的区别。

答案是：

> **在WBS里面有，但不在系统架构里面。**

也就是说，它属于**项目成果物(Project Artifact)**，不是**系统成果物(System Artifact)**。

---

## 我建议把整个项目分成两套架构

其实我们现在一直混在一起讨论。

应该分开。

```text
Project Architecture（项目）

        ↓

System Architecture（系统）
```

---

# 第一部分：Project Architecture（项目架构）

回答的是：

> **如何完成这个项目？**

例如：

```text
项目管理

↓

业务分析

↓

Master

↓

设计

↓

实现

↓

测试

↓

发布
```

里面包括：

```text
WBS

Schedule

QA

Risk

Review

Meeting

Release
```

这些：

全部：

属于：

Project。

---

例如：

```text
01 Project

    要件

    QA

    WBS

    Schedule

    Risk

    Review
```

全部：

项目。

不是：

系统。

---

# 第二部分：System Architecture（系统架构）

回答：

> **系统如何运行？**

例如：

```text
Master

↓

API Design

↓

UseCase

↓

Execution Spec

↓

Java Engine

↓

Report
```

这里：

没有：

Risk。

---

所以：

Risk：

不会：

进入：

Java。

不会：

进入：

AI。

---

# 为什么？

例如：

Risk：

写：

```text
E6 API

可能：

修改
```

Java：

不用：

知道。

Java：

只：

执行。

---

又例如：

```text
开发环境

可能：

延期
```

系统：

不知道。

PM：

知道。

---

# 所以：

建议：

以后：

整个项目：

分两个目录。

例如：

```text
project/

    management/

    system/
```

---

management

放：

```text
WBS

Schedule

QA

Risk

Review
```

---

system

放：

```text
Master

API

UseCase

Framework
```

---

# 我建议以后WBS也这样分类

## Project

例如：

```text
Project

    要件

    QA

    WBS

    Schedule

    Risk
```

---

## System

例如：

```text
Business

Master

API

UseCase

Framework

Implementation
```

---

# 其实日本很多项目也是这样

例如：

```
Project Management

Requirement

Basic Design

Detailed Design

Implementation

Test

Operation
```

Risk：

一直：

属于：

Project。

不是：

Design。

---

# 我建议最终整个项目变成

```
Project Artifacts

    WBS

    Schedule

    QA

    Risk

    Meeting

    Review

========================

System Artifacts

    Master

    API

    UseCase

    Framework

    Spec

    Java

    Report
```

---

## 我的最终建议（也是我认为最符合日本 SI 的做法）

我建议把整个仓库顶层就拆成两个世界：

```text
docs/
├── project/
│   ├── 要件定義書
│   ├── WBS
│   ├── スケジュール
│   ├── QA一覧
│   ├── リスク管理表
│   ├── レビュー記録
│   └── 議事録
│
└── system/
    ├── 業務分析
    ├── マスタ設計
    ├── API設計
    ├── UseCase設計
    ├── 共通基盤設計
    ├── 検証仕様
    └── 運用設計
```

这样：

- **project/** 管理项目（PM 看）。
- **system/** 管理系统（开发、AI、Java 看）。

我认为这比把所有成果物放在一个 WBS 里更符合日本 IT 项目的实际组织方式，也能避免以后把项目管理资料和系统设计资料混在一起。

## 第 70 轮

### 你

这种分法很清晰

### ChatGPT

我也认为这是我们目前讨论下来**最清晰、也是最符合日本 SI 项目的结构**。

实际上，我们已经把两件事情彻底分开了：

> **开发一个系统（System）**
>
> 和
>
> **管理一个项目（Project）**

这是很多项目后期混乱的原因。

---

# 我建议以后整个仓库就是两棵树

```text
project/
│
├── project/                ← 项目管理（PM）
│
└── system/                 ← 系统开发（SE）
```

这样以后所有资料都知道放哪里。

---

# Project（项目）

回答：

> **这个项目怎么推进？**

例如：

```text
project/

    01_ProjectManagement/

        要件定義書

        WBS

        スケジュール

        工数見積書

        QA一覧

        リスク管理表

        前提・制約管理表

        課題管理表

        議事録

        レビュー記録

        リリース計画書
```

这部分：

**PM最关心。**

---

# System（系统）

回答：

> **这个系统怎么实现？**

例如：

```text
system/

    01_Business

    02_Master

    03_API

    04_UseCase

    05_Framework

    06_Verification

    07_Implementation

    08_Operation
```

这部分：

SE、

AI、

Java：

一直：

使用。

---

# 为什么这样好？

例如：

PM：

问：

> 今天：

API设计：

完成了吗？

他：

只：

看：

```text
Project

↓

Schedule

↓

Progress
```

不用：

打开：

API设计。

---

开发：

问：

> CUSTOMER_ID：

哪里：

定义？

直接：

```text
System

↓

Context Design
```

不用：

看：

WBS。

---

AI：

问：

> 生成：

Test。

直接：

```text
API Design

↓

UseCase Design
```

不用：

知道：

Risk。

---

Java：

问：

> 怎么：

执行？

直接：

```text
Execution Spec
```

不用：

知道：

Markdown。

---

# 我觉得我们还可以再统一一件事情

目录命名也统一。

例如：

```
project/

    01_project_management/

    02_project_control/

system/

    01_business/

    02_master/

    03_design/

    04_verification/

    05_runtime/

    06_operation/
```

为什么？

因为：

Business、

Master、

Design、

Verification、

Runtime、

Operation。

其实：

就是：

整个系统：

生命周期。

以后：

MkDocs、

Git、

AI：

全部：

一致。

---

# 我现在已经想到最终完整版

其实：

整个仓库：

应该：

分成：

四个世界。

```
repository/

    project/

    system/

    runtime/

    outputs/
```

分别代表：

---

## ① project

项目管理。

---

## ② system

设计资产。

---

## ③ runtime

Java程序。

---

## ④ outputs

每天：

生成：

结果。

例如：

```
outputs/

    baseline/

    runs/

    reports/

    evidence/
```

这样：

**设计**

和

**执行**

彻底：

隔离。

---

## 我认为这是整个项目最后一次大的架构升级

我们前面一直在讨论**系统架构**，但真正落地一个工业项目，还需要把整个仓库按职责拆开。

我建议最终采用四个顶层目录：

| 顶层目录 | 负责什么 | 谁主要使用 |
|----------|----------|-----------|
| **project/** | 项目管理（WBS、Schedule、QA、Risk、Review、会议） | PM、TL |
| **system/** | 所有设计资产（Business、Master、API、UseCase、Framework） | 架构师、SE、AI |
| **runtime/** | Java 源码、配置、构建、测试、部署 | 开发者 |
| **outputs/** | Daily Summary、Diff、Evidence、Baseline、Runs | 运维、Leader、承认者 |

这样以后：

- **PM** 几乎只进入 `project/`
- **开发和 AI** 几乎只进入 `system/` 和 `runtime/`
- **运维和业务负责人** 主要看 `outputs/`

我认为这个仓库结构已经达到了可以支撑长期维护、多人协作和 AI 自动化开发的程度。

## 第 71 轮

### 你

好的 那么wbs和完整结构的最新总结一下

### ChatGPT

我认为这是我们这段时间讨论的**第一个可以冻结（Architecture Freeze V1）**的版本。

它最大的特点不是目录，而是**把项目管理(Project)、系统设计(System)、程序(Runtime)、运行结果(Outputs)完全分离**。

这也是我最推荐的工业化组织方式。

---

# 一、总体架构（Repository Architecture）

```text
repository/
│
├── project/          ← 项目管理（PM）
│
├── system/           ← 系统设计（AI + SE）
│
├── runtime/          ← Java程序
│
└── outputs/          ← 运行结果
```

这四个目录就是整个项目。

---

# 二、Project（项目管理）

回答：

> **项目如何推进？**

```text
project/

    01_ProjectManagement/

        要件定義書

        WBS

        工数見積書

        スケジュール

        進捗管理表

        QA一覧

        リスク管理表

        前提・制約管理表

        課題管理表

        議事録

        レビュー記録

        リリース計画書
```

这里：

PM：

天天：

看。

开发：

几乎：

不用。

---

# 三、System（系统设计）

回答：

> **系统如何实现？**

```text
system/

    01_Business/

    02_Master/

    03_API/

    04_UseCase/

    05_Framework/

    06_Verification/

    07_Operation/
```

以后：

AI：

主要：

工作：

这里。

---

## 01 Business

```text
現行業務分析書

E6_API分析書

業務フロー分析書

API一覧
```

---

## 02 Master

这里：

全部：

稳定。

```text
E6_API_Master

UseCase_Master

API_UseCase_Mapping

Context Design

Environment Master

Compare Policy

Verification Policy
```

其中：

Context Design：

里面：

再分：

```text
Context Model

Context Mapping
```

---

## 03 API

每个API：

一份。

例如：

```text
API001.md

API002.md
```

内容：

```text
Metadata

Endpoint

Request

Verification Definition

Response

Compare Definition

Extract Definition

File Definition

Error Definition
```

---

## 04 UseCase

例如：

```text
UC001.md

UC002.md
```

里面：

```text
Metadata

Entry

Flow

Context Mapping

Business Verification

Execution Policy

Expected Result
```

---

## 05 Framework

这里：

平台。

```text
システム設計書

共通Framework設計書

RunContext設計書

Snapshot設計書

Diff設計書

Report設計書

JSON設計書

ファイル設計書

ログ設計書

Exception設計書

環境設計書
```

---

## 06 Verification

这里：

**全部AI生成。**

例如：

```text
Execution Specification

API Test Specification

UseCase Test Specification

API Test Data

UseCase Test Data

Mock Data
```

注意：

Execution Specification：

不是：

设计书。

而是：

AI：

Compile：

Markdown：

以后：

生成。

Java：

只：

读取：

这里。

---

## 07 Operation

例如：

```text
運用設計書

Baseline運用

Daily運用

Release
```

---

# 四、Runtime（Java）

这里只：

代码。

```text
runtime/

    src/

    config/

    build/

    scripts/

    docker/
```

Java：

只：

负责：

执行。

不会：

解析：

Markdown。

---

# 五、Outputs（运行结果）

```text
outputs/

    baseline/

    runs/

    reports/

    evidence/
```

例如：

```text
outputs/

    baseline/

    runs/

        RUN001/

            raw/

            snapshot/

            diff/

            logs/

    reports/

        DailySummary.md

        DiffReport.md

    evidence/
```

---

# 六、真正的数据流

```text
业务设计书

↓

Business

↓

Master

↓

API Design

↓

UseCase Design

↓

AI Compile

↓

Execution Specification

↓

Java Execute

↓

Snapshot

↓

Diff

↓

Report
```

整个：

系统：

只有：

这一条路。

---

# 七、最终WBS（按成果物）

| 分类 | 成果物 |
|------|---------|
| **Project Management** | 要件定義書、WBS、工数見積書、スケジュール、進捗管理表、QA一覧、リスク管理表、前提・制約管理表、課題管理表、議事録、レビュー記録、リリース計画書 |
| **Business** | 現行業務分析書、E6_API分析書、業務フロー分析書、API一覧 |
| **Master** | E6_API_Master、UseCase_Master、API_UseCase_Mapping、Context Design（Context Model、Context Mapping）、Environment Master、Compare Policy、Verification Policy |
| **API Design** | API設計書 Template、API001～API024 |
| **UseCase Design** | UseCase設計書 Template、UC001～UC010 |
| **Framework** | システム設計書、共通Framework設計書、RunContext設計書、Snapshot設計書、Diff設計書、Report設計書、JSON設計書、ファイル入出力設計書、ログ・例外設計書、日付・比較設計書、環境設計書 |
| **Verification（AI生成）** | Execution Specification、API Test Specification、UseCase Test Specification、API Test Data、UseCase Test Data、Mock Data |
| **Runtime** | Java Verification Engine、Context Engine、API Executor、Snapshot Engine、Diff Engine、Report Engine |
| **Operation** | 運用設計書、Baseline運用、Daily運用、Release |
| **Outputs** | Daily Summary、Diff Report、Evidence、Baseline、Runs |

---

# 八、整个系统的职责

| 区域 | 谁维护 | 作用 |
|------|---------|------|
| **project/** | PM | 管理项目 |
| **system/** | 架构师、SE、AI | 管理所有设计资产（SSOT） |
| **runtime/** | Java开发 | 实现执行引擎 |
| **outputs/** | Java + AI | 保存每天运行结果和证迹 |

---

# 九、我认为这套架构最大的价值

这套设计真正形成了一个**规格驱动（Specification Driven）**的平台：

- **Project**：管理"怎么完成项目"。
- **System**：管理"系统应该是什么样"（唯一事实来源，SSOT）。
- **Verification**：由 AI 将设计编译为可执行规格和测试资产。
- **Runtime**：Java 严格按规格执行，不关心设计细节。
- **Outputs**：每天沉淀 Summary、Diff、Evidence，形成可追溯历史。

这已经不仅适用于 E6 API 验证，也可以扩展到其他 API 平台、回归测试平台甚至更通用的自动化验证体系。

## 第 72 轮

### 你

整理成wbs一览表 和 完整架构表

### ChatGPT

我建议把最终成果整理成**两张总表**：

- **① WBS 一览表（项目管理用）**：PM 排期、工数、进度管理。
- **② 系统架构一览表（系统设计用）**：架构师、开发、AI 使用。

这样以后无论是日本项目管理还是 MkDocs 导航都非常清晰。

---

# ① WBS 一览表（Project WBS）

| WBS | カテゴリ | 成果物 | 目的 | 担当 | 開始 | 終了 | 状態 |
|------|----------|---------|------|------|------|------|------|
| 1 | **プロジェクト管理** | 要件定義書 | 项目目标、范围、成功标准 | | | | |
| 1.1 | | WBS | 工作分解 | | | | |
| 1.2 | | 工数見積書 | 工数估算 | | | | |
| 1.3 | | スケジュール | 计划安排 | | | | |
| 1.4 | | 進捗管理表 | 进度管理 | | | | |
| 1.5 | | QA一覧 | 未确认事项 | | | | |
| 1.6 | | リスク管理表 | 项目风险 | | | | |
| 1.7 | | 前提・制約管理表 | Assumption & Constraint | | | | |
| 1.8 | | 課題管理表 | Issue 管理 | | | | |
| 1.9 | | レビュー記録 | Review 记录 | | | | |
| 1.10 | | 議事録 | Meeting 记录 | | | | |
| 1.11 | | リリース計画書 | 发布计划 | | | | |
| 2 | **業務分析** | 現行業務分析書 | 现行业务分析 | | | | |
| 2.1 | | E6 API分析書 | API 分析 | | | | |
| 2.2 | | 業務フロー分析書 | Flow 分析 | | | | |
| 2.3 | | API一覧 | API 清单 | | | | |
| 3 | **マスタ設計** | E6 API Master | API 主数据 | | | | |
| 3.1 | | UseCase Master | UseCase 主数据 | | | | |
| 3.2 | | API-UseCase対応表 | API 覆盖关系 | | | | |
| 3.3 | | Context Design（Model・Mapping） | Context 对象及流转 | | | | |
| 3.4 | | Environment Master | 环境主数据 | | | | |
| 3.5 | | Compare Policy | 全局比较策略 | | | | |
| 3.6 | | Verification Policy | 全局验证策略 | | | | |
| 4 | **API設計** | API設計書 Template | API 模板 | | | | |
| 4.1 | | API設計書（API001～API024） | API 设计 | | | | |
| 5 | **UseCase設計** | UseCase設計書 Template | UseCase 模板 | | | | |
| 5.1 | | UseCase設計書（UC001～UC010） | UseCase 设计 | | | | |
| 6 | **共通基盤設計** | システム設計書 | 系统整体 | | | | |
| 6.1 | | 共通Framework設計書 | Framework | | | | |
| 6.2 | | RunContext設計書 | Context 生命周期 | | | | |
| 6.3 | | Snapshot設計書 | Snapshot | | | | |
| 6.4 | | Diff設計書 | Diff | | | | |
| 6.5 | | Report設計書 | Report | | | | |
| 6.6 | | JSON設計書 | JSON | | | | |
| 6.7 | | ファイル入出力設計書 | 文件处理 | | | | |
| 6.8 | | ログ・例外設計書 | Log & Exception | | | | |
| 6.9 | | 日付・比較設計書 | 日期比较 | | | | |
| 6.10 | | 環境設計書 | Linux/JDK/Tomcat | | | | |
| 7 | **検証資産** | Execution Specification | AI 编译后的执行规格 | AI | | | |
| 7.1 | | API Test Specification | API 测试规格 | AI | | | |
| 7.2 | | UseCase Test Specification | UseCase 测试规格 | AI | | | |
| 7.3 | | API Test Data | API 测试数据 | AI | | | |
| 7.4 | | UseCase Test Data | UseCase 测试数据 | AI | | | |
| 7.5 | | Mock Data | Mock 数据 | AI | | | |
| 8 | **実装** | Java Verification Engine | 执行引擎 | | | | |
| 8.1 | | Context Engine | Context 管理 | | | | |
| 8.2 | | API Executor | API 调用 | | | | |
| 8.3 | | Snapshot Engine | Snapshot | | | | |
| 8.4 | | Diff Engine | Diff | | | | |
| 8.5 | | Report Engine | Report | | | | |
| 9 | **運用** | 運用設計書 | 运维设计 | | | | |
| 9.1 | | Baseline運用 | Baseline 管理 | | | | |
| 9.2 | | Daily運用 | 日次执行 | | | | |
| 9.3 | | リリース手順書 | 发布流程 | | | | |
| 10 | **成果物** | Daily Summary | 每日总结 | 自动 | | | |
| 10.1 | | Diff Report | 差异报告 | 自动 | | | |
| 10.2 | | Evidence | 证迹 | 自动 | | | |

---

# ② 系统架构一览表（System Architecture）

| Layer | 模块 | 输入 | 输出 | 说明 |
|--------|------|------|------|------|
| **Business Layer** | 現行業務分析 | 业务设计书、E6 文档 | 分析结果 | 理解业务 |
| **Master Layer** | E6 API Master | 分析结果 | API Master | API 主数据 |
| | UseCase Master | 分析结果 | UseCase Master | UseCase 主数据 |
| | Context Design | API/UseCase | Context Model + Mapping | 上下文对象 |
| | Environment Master | 环境信息 | Environment | 环境管理 |
| | Compare Policy | 平台规则 | Compare Policy | 默认比较规则 |
| | Verification Policy | 平台规则 | Verification Policy | 默认执行规则 |
| **Design Layer** | API設計書 | API Master | API Design | API 契约 |
| | UseCase設計書 | UseCase Master | UseCase Design | API 链路 |
| | 共通基盤設計 | Master | Framework Design | 平台设计 |
| **Verification Layer** | AI Compiler | Markdown | Execution Specification | 编译为执行规格 |
| | AI Generator | Execution Specification | Test Spec/Test Data | 自动生成测试资产 |
| **Runtime Layer** | Java Verification Engine | Execution Specification | API 调用 | 确定性执行 |
| | Context Engine | API Response | Context | 管理上下文 |
| | API Executor | Request | Response | 调用 E6 API |
| | Snapshot Engine | Response | Snapshot | 保存快照 |
| | Diff Engine | Snapshot | Diff | 比较差异 |
| | Report Engine | Diff | Daily Summary / Diff Report | 报告生成 |
| **Output Layer** | Reports | Runtime | Summary / Diff | 结果展示 |
| | Evidence | Runtime | Raw、Log、Snapshot | 调查证据 |

---

## 我还有一个建议（最终优化）

为了让 **WBS** 和 **系统架构** 完全对应，我建议把 WBS 第 **7** 类的名称从 **「検証資産」** 调整为：

> **「AI生成資産」**

原因是这一类的成果物（Execution Specification、Test Specification、Test Data、Mock Data）**不是人工编写，而是 AI 根据设计书生成的资产**。

这样两张表就完全对应：

- **Project WBS**：管理谁负责、什么时候完成。
- **System Architecture**：说明这些成果物在系统中的位置和数据流。
- **AI生成資産**：明确标识这是自动生成、可重复生成的内容，而不是需要人工维护的设计文档。

我认为这是目前最符合你这个平台定位的最终版本。

## 第 73 轮

### 你

好的 。 可以

### ChatGPT

我觉得可以，而且我建议**再提升一个层次**。

我们不要把它叫：

> **WBS**

而是叫：

> **Project Blueprint（项目蓝图）**

因为我们现在已经不仅仅是在做 WBS，而是在设计整个项目的组织方式。

我建议最终形成 **四张总表**，以后整个项目都围绕这四张表开展。

---

# ① Project Blueprint（项目蓝图）

回答：

> **整个项目由哪些部分组成？**

```text
Repository

├── Project
├── System
├── Runtime
└── Outputs
```

这是最高层。

---

# ② Project WBS（项目管理）

回答：

> **项目要完成哪些成果物？**

例如：

| WBS | 分类 | 成果物 | Owner | Start | Finish | Status |
|------|------|---------|--------|--------|---------|---------|

PM：

天天：

看：

这张。

---

# ③ System Blueprint（系统蓝图）

回答：

> **系统由哪些资产组成？**

例如：

```text
Business

↓

Master

↓

Design

↓

AI Generated Assets

↓

Runtime

↓

Outputs
```

开发：

天天：

看：

这张。

---

# ④ Runtime Flow（执行蓝图）

回答：

> **程序怎么执行？**

例如：

```text
UseCase

↓

API

↓

Context

↓

Snapshot

↓

Diff

↓

Summary
```

Java：

天天：

看：

这张。

---

## 四张图关系

```text
Project Blueprint
        │
        ▼
Project WBS
        │
        ▼
System Blueprint
        │
        ▼
Runtime Flow
```

这样：

PM、

SE、

AI、

Java、

Leader

每个人：

都有：

自己的：

入口。

---

# 我建议最终 Repository

```text
repository/

├── 00_blueprint/
│
│   ├── Project_Blueprint.md
│   ├── Project_WBS.md
│   ├── System_Blueprint.md
│   └── Runtime_Flow.md
│
├── project/
│
├── system/
│
├── runtime/
│
└── outputs/
```

以后：

任何：

新人。

第一天：

只需要：

看：

```text
00_blueprint
```

基本：

整个项目：

全部：

理解。

---

# 然后

我们：

才：

进入：

```text
system/
```

开始：

真正：

开发。

---

# 我认为整个项目还可以再加一个最重要的文档

也是：

日本：

架构师：

最喜欢：

做的。

叫：

## Development Guide（開発ガイド）

它：

不是：

设计书。

而是：

整个：

项目：

怎么玩。

里面：

例如：

```text
Repository说明

目录说明

成果物流

Review流程

AI开发流程

Git流程

Branch策略

命名规范

Markdown规范

Java规范

JSON规范

Version规则

Baseline规则
```

以后：

Codex、

Copilot、

新人、

开发、

全部：

先：

读：

它。

---

## 我的建议（最终版）

到这里，我认为项目顶层应该固定为 **5 个入口**：

```text
00_blueprint/      ← 项目全景（所有人第一天先看）
project/           ← 项目管理
system/            ← 系统设计资产（SSOT）
runtime/           ← Java 代码
outputs/           ← 每天运行结果
```

其中 **00_blueprint** 是整个项目的导航中心，里面放：

1. Project Blueprint（项目整体）
2. Project WBS（成果物与进度）
3. System Blueprint（系统分层）
4. Runtime Flow（执行流程）
5. Development Guide（开发指南）

**我认为这是我们整个讨论中最重要的一次升级。**

因为以后无论是人、AI（Codex/Copilot）、还是新成员，都不用先钻设计书，而是先看这五份 Blueprint，就能在半小时内理解整个项目的结构和开发方式。这样整个项目就真正具备了长期维护和团队协作的能力。

## 第 74 轮

### 你

我觉得可以 但是有一点 部署到本番环境的时候 不是repo

### ChatGPT

我也正想跟你说这个。

**你提出来的这个点非常重要。**

实际上，我们前面讨论的是**开发仓库（Development Repository）**。

但是：

> **部署到本番（生产环境）的东西，不应该还是这个 Repository。**

这是日本很多大型项目都会分开的。

---

## 应该分三个世界

不是：

```text
Repository
```

而是：

```text
Development

↓

Build

↓

Production
```

三者完全不同。

---

# ① Development（开发）

这是我们一直讨论的。

例如：

```text
repository/

    project/

    system/

    runtime/

    outputs/
```

这里：

AI、

Codex、

开发。

全部：

这里。

---

# ② Build（发布包）

例如：

CI：

GitHub Action

或者：

Jenkins。

生成：

```text
verification-platform.zip
```

里面：

其实：

只有：

```text
bin/

config/

lib/

resources/

spec/

templates/
```

没有：

```text
project/

WBS

API设计书
```

这些：

全部：

不要。

---

# ③ Production（本番）

真正：

Linux：

里面。

例如：

```text
/opt/e6-verification/

    bin/

    config/

    logs/

    baseline/

    reports/

    runs/

    temp/

    resources/
```

只有：

运行：

需要。

---

# 为什么？

因为：

生产：

根本：

不需要：

```text
WBS

QA

Markdown设计书

Meeting

Risk
```

这些：

属于：

开发资产。

---

# 我建议以后

整个：

项目：

变成：

```text
Development

↓

Artifact

↓

Production
```

---

## Development Repository

例如：

```text
project/

system/

runtime/

outputs/
```

---

## Artifact

例如：

```text
verification-platform-1.0.zip
```

里面：

```text
bin/

lib/

config/

default-spec/

scripts/
```

---

## Production

例如：

```text
/opt/e6-verification/

config/

runs/

reports/

baseline/

logs/
```

---

# 那Markdown怎么办？

这里：

其实：

有：

两种。

---

一种：

开发：

Markdown。

例如：

```text
API001.md
```

不会：

发布。

---

另一种：

Execution Specification。

例如：

```text
API001.json
```

这个：

发布。

因为：

Java：

需要。

---

所以：

真正：

发布的是：

```text
Execution Specification
```

不是：

Markdown。

---

# 那AI呢？

AI：

开发：

时候：

存在。

生产：

不存在。

生产：

只有：

```text
JSON

Java
```

所以：

非常：

稳定。

---

# 我建议最终应该有四个架构

| 名称 | 用途 |
|------|------|
| Development Architecture | 开发资产 |
| Build Architecture | 发布物 |
| Runtime Architecture | Linux运行结构 |
| Output Architecture | 每天结果 |

---

例如：

## Build

```text
artifact/

bin/

config/

spec/

resources/
```

---

Runtime

```text
linux/

bin/

config/

logs/

reports/

runs/

baseline/
```

---

Output

```text
run/

snapshot/

diff/

summary/

evidence/
```

---

## 我建议再做一次架构升级（我认为这是最终版）

其实最顶层不应该叫 **Repository Blueprint**。

而应该叫：

> **Solution Blueprint（解决方案蓝图）**

因为它描述的不只是 Git 仓库，而是整个解决方案。

它包含四张图：

1. **Development Architecture**（开发资产）
2. **Build Architecture**（CI/CD 产物）
3. **Runtime Architecture**（Linux 部署结构）
4. **Output Architecture**（运行结果结构）

这样以后：

- 开发人员看 Development。
- CI/CD 看 Build。
- 运维看 Runtime。
- 业务和承认者看 Output。

四个世界互不混淆，也更符合日本企业系统从开发到发布再到运维的完整生命周期。

**我认为这是我们整个架构讨论真正的最终形态。**

## 第 75 轮

### 你

只要不偏离我们这次项目开发的核心 是可以的 不要随便乱扩大一些不必要的概念

### ChatGPT

我完全赞同，而且我觉得这是一个**很重要的边界**。

这段时间我们的讨论越来越深入，我也一直在优化架构。但从现在开始，我认为应该遵守一个原则：

> **所有设计必须直接服务于"E6 API Verification Platform"这个项目。**

不要为了架构而架构。

---

## 我建议我们从现在开始采用三个原则

### 原则1：所有成果物必须有直接价值

以后如果增加一个文档，我都会先回答三个问题：

1. **谁维护？**
2. **谁使用？**
3. **如果没有它，会出现什么问题？**

如果回答不了，这个成果物就不要。

例如：

### Context Design

谁维护？

> 架构师

谁使用？

> AI、Java、开发

没有会怎样？

> Context 会混乱，API 之间无法稳定传值。

所以：

**保留。**

---

例如：

### Verification Policy

谁维护？

> 架构师

谁使用？

> Java

没有？

> UseCase 的执行策略没有统一标准。

所以：

**保留。**

---

如果一个文档回答变成：

> 好像以后可能有用……

我建议：

**不要。**

---

### 原则2：不要提前设计未来可能不会用的东西

例如：

如果现在只有：

- 24 个 API
- 10 个 UseCase

那我们就围绕这件事设计。

不要因为以后可能有：

- 500 个 API
- 多租户
- 分布式执行

就把现在搞复杂。

以后真的需要，再扩展。

---

### 原则3：一切围绕执行链

我建议以后所有设计都必须落到下面这条链路。

```text
API设计书
      │
      ▼
UseCase设计书
      │
      ▼
AI生成Execution Specification
      │
      ▼
Java执行
      │
      ▼
Report
```

如果某个文档：

**不能帮助这条链路。**

那么：

不要。

---

# 我重新审视了一下目前WBS

我认为：

真正需要保留的只有下面这些。

---

## Project

```text
要件定義書

QA一覧

WBS

Schedule

課題管理表
```

Risk：

保留。

Meeting：

可以以后。

Review：

可以以后。

不用一开始。

---

## Business

保留。

---

## Master

保留。

---

## API

保留。

---

## UseCase

保留。

---

## Framework

保留。

---

## Verification

保留。

---

## Runtime

保留。

---

## Operation

保留。

---

## Outputs

不用设计。

Java：

自然：

生成。

---

# 所以我建议删除几个

例如：

以前：

我提：

Development Guide。

其实：

现在：

可以不要。

以后：

再说。

---

Blueprint。

其实：

也不用：

五个。

一个：

System Overview：

足够。

---

# 我建议现在冻结

真正：

只保留：

下面：

九类。

| No | 分类 | 保留原因 |
|----|------|---------|
| 1 | Project | 项目必须管理 |
| 2 | Business | 必须理解业务 |
| 3 | Master | 所有设计基础 |
| 4 | API Design | 核心成果物 |
| 5 | UseCase Design | 核心成果物 |
| 6 | Framework | Java 必须实现 |
| 7 | Verification | AI 必须生成 |
| 8 | Runtime | Java 实现 |
| 9 | Operation | 上线必须 |

我认为：

**这是最小但完整（Minimum Complete Architecture）**。

---

## 我建议我们的合作方式也固定下来

从现在开始，我会遵守一个规则：

> **每增加一个新的成果物、文档、目录或概念，我都会先说明：**

1. 它解决什么具体问题？
2. 谁维护？
3. 谁使用？
4. 是否可以用现有成果物替代？
5. 如果不能替代，再建议增加。

如果只是"以后可能有用"、"架构上看起来更漂亮"，我就不会再建议加入。

我认为这样更符合你这个项目的目标：**把 E6 API 验证平台做扎实，而不是做一个概念过多的框架。**

## 第 76 轮

### 你

我现在要明确wbs  项目架构 以及完整构成

### ChatGPT

下面按**不扩大、不偏离项目核心**整理成最终版。

# 1. WBS 一览表

| WBS | 分类 | 成果物 / 作业 | 目的 |
|---|---|---|---|
| 1 | プロジェクト管理 | 要件定義書 | 明确目标、范围、非范围、成功标准 |
| 1.1 | プロジェクト管理 | QA一覧 | 管理业务、E6、环境确认事项 |
| 1.2 | プロジェクト管理 | WBS | 管理成果物和作业 |
| 1.3 | プロジェクト管理 | スケジュール | 管理开始、结束、进度 |
| 1.4 | プロジェクト管理 | 課題・リスク管理表 | 管理问题和风险 |
| 2 | 業務分析 | 現行業務分析書 | 从现行业务 Flow 抽取 E6 API 验证范围 |
| 2.1 | 業務分析 | E6 API分析書 | 整理 E6 API 规格、限制、确认点 |
| 2.2 | 業務分析 | API一覧 | 整理约 24 个 API |
| 3 | マスタ設計 | E6 API Master | API 主目录 |
| 3.1 | マスタ設計 | UseCase Master | 10 个以内 UseCase 主目录 |
| 3.2 | マスタ設計 | API-UseCase対応表 | 确认 API 覆盖关系 |
| 3.3 | マスタ設計 | Context Design | 定义 Customer.id、Account.id 等上下文对象和流转 |
| 3.4 | マスタ設計 | Environment Master | DEV/STG/本番相当环境配置 |
| 3.5 | マスタ設計 | Compare Policy | 全局比较策略，如日期、traceId、timestamp ignore |
| 3.6 | マスタ設計 | Verification Policy | 全局执行策略，如 retry、timeout、stop/continue、baseline |
| 4 | API設計 | API設計書 Template | 固定 API 设计格式 |
| 4.1 | API設計 | API設計書（API001～API024） | 定义 Request、Response、验证定义、比较定义、Extract |
| 5 | UseCase設計 | UseCase設計書 Template | 固定 UseCase 设计格式 |
| 5.1 | UseCase設計 | UseCase設計書（UC001～UC010） | 定义 Entry、Flow、Context Mapping、业务验证、执行策略 |
| 6 | 共通基盤設計 | システム設計書 | 系统整体架构 |
| 6.1 | 共通基盤設計 | 共通Framework設計書 | File、JSON、Date、Log、Exception、Mask、Hash 等共通部品 |
| 6.2 | 共通基盤設計 | RunContext設計書 | runId、executionId、Context、状态 |
| 6.3 | 共通基盤設計 | Snapshot設計書 | Request/Response/Snapshot 保存 |
| 6.4 | 共通基盤設計 | Diff設計書 | 今天与 Baseline/前一天比较 |
| 6.5 | 共通基盤設計 | Report設計書 | Daily Summary、Diff Report、Evidence |
| 6.6 | 共通基盤設計 | ファイル入出力設計書 | 文件上传、下载、hash、atomic write |
| 6.7 | 共通基盤設計 | ログ・例外設計書 | 日志、mask、异常分类、错误处理 |
| 6.8 | 共通基盤設計 | 環境設計書 | Linux、JDK、Tomcat、cron、权限、网络 |
| 7 | 検証資産 | Execution Specification | AI 从 Markdown 生成的 Java 执行规格 |
| 7.1 | 検証資産 | API Test Specification | AI 根据 API 设计生成 API 测试规格 |
| 7.2 | 検証資産 | UseCase Test Specification | AI 根据 UseCase 设计生成链路测试规格 |
| 7.3 | 検証資産 | Test Data | AI 生成测试数据 |
| 8 | 実装 | Java Verification Engine | Java 执行引擎 |
| 8.1 | 実装 | Context Engine | 上下文变量管理 |
| 8.2 | 実装 | API Executor | 调用 E6 API |
| 8.3 | 実装 | Snapshot Engine | 生成快照 |
| 8.4 | 実装 | Diff Engine | 执行比较 |
| 8.5 | 実装 | Report Engine | 生成报告 |
| 9 | 運用 | 運用設計書 | 日次执行、baseline、cleanup、障害対応 |
| 9.1 | 運用 | Daily Summary Report | 承认者看的每日总结 |
| 9.2 | 運用 | Diff Report | Leader/开发看的差异报告 |
| 9.3 | 運用 | Evidence | raw request/response、snapshot、log、file |

---

# 2. 项目架构

```text
E6 API Verification Platform

project/
  项目管理资料
  - 要件
  - QA
  - WBS
  - Schedule
  - 課題・Risk

system/
  系统设计资料
  - 業務分析
  - Master
  - API設計
  - UseCase設計
  - 共通基盤設計
  - 検証資産

runtime/
  Java 程序
  - source
  - config
  - scripts

outputs/
  执行结果
  - baseline
  - runs
  - reports
  - evidence
```

---

# 3. 完整目录结构

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── QA一覧.md
│   ├── WBS.md
│   ├── スケジュール.md
│   └── 課題・リスク管理表.md
│
├── system/
│   ├── 01_business/
│   │   ├── 現行業務分析書.md
│   │   ├── E6_API分析書.md
│   │   └── API一覧.md
│   │
│   ├── 02_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── API_UseCase対応表.md
│   │   ├── Context_Design.md
│   │   ├── Environment_Master.md
│   │   ├── Compare_Policy.md
│   │   └── Verification_Policy.md
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   ├── API001_xxx.md
│   │   ├── API002_xxx.md
│   │   └── ...
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   ├── UC001_xxx.md
│   │   ├── UC002_xxx.md
│   │   └── ...
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
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       └── test_data/
│
├── runtime/
│   ├── src/
│   ├── config/
│   ├── scripts/
│   └── build/
│
└── outputs/
    ├── baseline/
    ├── runs/
    │   └── {runId}/
    │       ├── run-info.json
    │       ├── raw/
    │       ├── snapshot/
    │       ├── diff/
    │       ├── reports/
    │       ├── logs/
    │       └── tmp/
    ├── reports/
    └── evidence/
```

---

# 4. 系统执行构成

```text
Markdown Design
  API設計書
  UseCase設計書
        ↓
AI Compiler
        ↓
Execution Specification / Test Specification / Test Data
        ↓
Java Verification Engine
        ↓
UseCase Runner
        ↓
API Executor
        ↓
E6 API
        ↓
Snapshot
        ↓
Diff
        ↓
Daily Summary / Diff Report / Evidence
```

---

# 5. 核心边界

```text
人维护：
- 要件
- QA
- Master
- API設計書
- UseCase設計書
- Framework設計書

AI生成：
- Execution Specification
- API Test Specification
- UseCase Test Specification
- Test Data

Java执行：
- API调用
- Context管理
- Snapshot
- Diff
- Report

承认者查看：
- Daily Summary

开发调查：
- Diff Report
- Evidence
```

这就是当前项目的最小完整结构。

## 第 77 轮

### 你

如何在本番发布必要的程序以及执行结果等
output和runtime分开的 如何放到linux服务器上

### ChatGPT

本番服务器上不要放完整 repo。建议只放 **runtime package + execution spec + production output directories**。

# 1. 本番 Linux 推荐结构

```text
/opt/e6-verifier/
├── app/
│   ├── bin/
│   │   └── e6-verifier.sh
│   ├── lib/
│   │   └── e6-api-verifier.jar
│   ├── specs/
│   │   ├── execution_spec/
│   │   ├── api_test_spec/
│   │   ├── usecase_test_spec/
│   │   └── test_data/
│   └── resources/
│       └── test-files/
│
├── config/
│   ├── application-prod.json
│   └── secret/        ← 权限限制
│
├── data/
│   ├── baseline/
│   ├── runs/
│   ├── reports/
│   ├── evidence/
│   └── tmp/
│
└── logs/
```

对应关系：

| 开发 repo | 本番服务器 |
|---|---|
| `runtime/build/*.jar` | `/opt/e6-verifier/app/lib/` |
| `runtime/scripts/*.sh` | `/opt/e6-verifier/app/bin/` |
| `system/06_verification_assets/` | `/opt/e6-verifier/app/specs/` |
| `test-resources/` | `/opt/e6-verifier/app/resources/` |
| `runtime/config/prod` | `/opt/e6-verifier/config/` |
| `outputs/` | `/opt/e6-verifier/data/` |

---

# 2. 发布包内容

发布时生成：

```text
e6-verifier-release-1.0.0.zip
```

里面只包含：

```text
bin/
lib/
specs/
resources/
config-template/
```

不包含：

```text
project/
system/
docs/
WBS/
QA/
设计书Markdown/
```

设计书是开发资产，不直接进本番。

---

# 3. 执行结果放哪里

执行结果全部放：

```text
/opt/e6-verifier/data/
```

例如：

```text
/opt/e6-verifier/data/runs/{runId}/
├── run-info.json
├── raw/
├── snapshot/
├── diff/
├── reports/
├── logs/
└── tmp/
```

承认者看的日报可以复制到：

```text
/opt/e6-verifier/data/reports/
```

---

# 4. 启动方式

```bash
/opt/e6-verifier/app/bin/e6-verifier.sh run \
  --env prod \
  --spec-dir /opt/e6-verifier/app/specs \
  --config /opt/e6-verifier/config/application-prod.json \
  --output-dir /opt/e6-verifier/data
```

---

# 5. 定时执行

用 cron 或 JP1。

cron 示例：

```bash
0 6 * * * /opt/e6-verifier/app/bin/e6-verifier.sh run --env prod >> /opt/e6-verifier/logs/cron.log 2>&1
```

---

# 6. 最重要原则

```text
开发环境：
repo + markdown + AI生成

本番环境：
jar + json spec + config + output directory
```

一句话：

**runtime 是程序，outputs 是运行数据。本番 Linux 上两者分开放：程序放 `/app`，结果放 `/data`。**

## 第 78 轮

### 你

那么开发执行 和 本番执行如何 在开发时候同时验证 比如docker作为本地本番发布执行 或者说本地开发执行也用docker

### ChatGPT

可以，推荐这样做：**开发、本番都用同一套 Docker 运行方式**。区别只在于挂载的 `config/specs/data` 不同。

```text
本地开发：
repo + docker compose

本番发布：
release zip / image + docker run
```

# 推荐执行结构

```text
Docker Image
  只放：
  - jar
  - scripts
  - runtime依赖

外部挂载 Volume
  - config
  - specs
  - resources
  - data/runs
  - data/baseline
  - logs
```

# 本地开发执行

```text
repository/
├── system/
├── runtime/
├── outputs/
└── docker-compose.yml
```

开发时：

```bash
docker compose up e6-verifier
```

挂载：

```text
./system/06_verification_assets → /app/specs
./runtime/config/dev.json       → /app/config/application.json
./outputs                       → /app/data
```

这样本地跑出来的结果也在：

```text
outputs/runs/{runId}
outputs/reports
outputs/evidence
```

# 本番执行

本番不要挂 repo。

```bash
docker run --rm \
  -v /opt/e6-verifier/config:/app/config \
  -v /opt/e6-verifier/specs:/app/specs \
  -v /opt/e6-verifier/data:/app/data \
  -v /opt/e6-verifier/logs:/app/logs \
  e6-verifier:1.0.0 \
  run --env prod
```

# Docker 镜像里放什么

```text
/app/
├── bin/
│   └── e6-verifier.sh
├── lib/
│   └── e6-api-verifier.jar
└── runtime/
```

不放：

```text
project/
system/
设计书Markdown
WBS
QA
```

# 为什么这样好

```text
开发执行 = 本番执行方式一致
Java环境一致
JDK版本一致
依赖一致
路径一致
结果目录一致
本番不需要完整repo
```

# 最佳实践

本地也用 Docker 跑，避免：

```text
我本地能跑
Linux本番不能跑
```

最终原则：

```text
开发：用 docker compose 验证
本番：用同一个 image + 外部 config/specs/data 执行
```

也就是说，**Docker 是运行标准，repo 只是开发资产。**

## 第 79 轮

### 你

本番结果怎么看 没看明白

### ChatGPT

这是一个非常关键的问题，而且你问到了**运维视角**。

其实我们前面一直站在**开发者**角度。

现在切换到**本番运维**角度来看。

---

# 本番每天发生什么？

例如：

每天早上6点。

JP1或者cron执行。

```text
UC001

↓

UC002

↓

UC003

...

↓

UC010
```

执行完成。

产生：

```
RunId

20260701_060000_xxxx
```

---

然后：

在Linux上：

产生：

```
/opt/e6-verifier/data/

        runs/

            20260701_060000_xxxx/
```

例如：

```
runs/

    20260701_060000_xxxx/

        raw/

        snapshot/

        diff/

        reports/

        logs/
```

这里：

就是：

一次执行。

---

# 承认者怎么看？

他：

不会：

SSH。

不会：

进去：

Linux。

所以：

真正：

看的：

应该：

只有：

```
reports/
```

例如：

```
/opt/e6-verifier/data/reports/

        DailySummary.md

        DiffReport.md
```

每天：

覆盖：

最新。

或者：

```
DailySummary_20260701.md
```

---

# 开发怎么看？

开发：

需要：

调查。

例如：

UC005：

失败。

他：

进去：

```
runs/

    20260701_060000_xxxx/

        raw/

        snapshot/

        diff/

        logs/
```

这里：

全部：

都有。

---

# 那outputs目录为什么还有reports？

其实：

这里：

应该：

分两层。

例如：

```
outputs/

    reports/

        DailySummary

        DiffReport

    runs/

        Run001

        Run002

        Run003
```

reports：

永远：

最新。

runs：

永远：

历史。

---

# 那Baseline呢？

例如：

```
baseline/

        API001

        UC001
```

一直：

存在。

Java：

比较：

```
昨天

或者

Baseline
```

---

# 我建议Linux真正目录

```
/opt/e6-verifier/

        app/

        config/

        data/

            baseline/

            reports/

            runs/

        logs/
```

data：

全部：

数据。

---

# 一个Run

例如：

```
Run001/

        run.json

        raw/

            API001

            API002

        snapshot/

        diff/

        report/

            UC001

            UC002

        logs/
```

这里：

调查。

---

# Leader

其实：

只：

需要：

```
reports/

        DailySummary.md
```

里面：

例如：

```
2026-07-01

PASS

UC001

PASS

UC002

PASS

UC003

FAIL

API005

status变化

Diff:

status

0→1
```

Leader：

结束。

---

# 如果：

FAIL。

开发：

再：

进去：

```
runs/

Run001/
```

调查。

---

# 所以：

真正：

三个层级。

```
Summary

↓

Run

↓

Evidence
```

---

# 我觉得我们这里还应该加一个东西（这个是有必要的）

不是：

新概念。

而是：

项目：

必须。

例如：

```
/opt/e6-verifier/

        reports/

            latest/

            history/
```

为什么？

因为：

Leader：

一般：

只：

看：

```
latest/
```

而：

历史：

保留：

```
history/

    20260701

    20260702
```

以后：

查。

---

## 我建议最终 Output 结构调整成下面这样（这是我认为最适合本番运维的）

```text
/opt/e6-verifier/data/

├── baseline/
│
├── reports/
│   ├── latest/
│   │   ├── DailySummary.md
│   │   └── DiffReport.md
│   │
│   └── history/
│       ├── 20260701/
│       ├── 20260702/
│       └── ...
│
├── runs/
│   ├── 20260701_060000_xxxx/
│   ├── 20260702_060000_xxxx/
│   └── ...
│
└── tmp/
```

这样职责非常清晰：

- **reports/latest**：业务负责人、Leader 每天只看这里。
- **reports/history**：保存每天生成的正式报告。
- **runs/**：开发调查用，保存每次执行的原始证据（raw、snapshot、diff、logs）。
- **baseline/**：比较基准。

**这不是增加新的概念，而是把"展示给人看的结果"和"程序调查用的证据"分开，这也是很多企业批处理系统常见的组织方式。**

## 第 80 轮

### 你

开发和本番他们的区别在哪里

### ChatGPT

这是整个项目最关键的问题之一。

其实我们一直在讨论"开发目录"，但是没有把**开发（Development）**和**本番（Production）**的职责分开。

如果这个地方不清楚，以后整个项目都会混。

---

# 一句话

> **开发环境是"生产程序"。**
>
> **本番环境是"运行程序"。**

这两个世界完全不同。

---

# 开发环境（Development）

目的：

> **开发这个工具。**

例如：

```text
Repository

↓

修改Markdown

↓

修改Java

↓

AI生成Spec

↓

测试

↓

Commit
```

所以：

开发需要：

```text
project/

system/

runtime/

outputs/
```

全部。

因为：

要开发。

---

例如：

开发：

每天：

修改：

```text
API001.md

↓

重新生成

↓

Execution Spec

↓

重新跑
```

---

# 本番（Production）

目的：

不是：

开发。

而是：

每天：

```text
执行

↓

比较

↓

报告
```

所以：

本番：

根本：

不要：

```text
Markdown

WBS

QA

Meeting
```

这些。

---

# 举例

开发：

修改：

```text
API001.md
```

AI：

重新：

生成：

```text
API001.execution.json
```

然后：

Java：

测试。

---

发布。

Linux：

收到：

只有：

```text
execution.json
```

Markdown：

不要。

---

# 所以：

开发：

和：

本番：

最大的区别。

不是：

Linux。

不是：

Docker。

而是：

开发：

拥有：

源码。

本番：

只有：

成果。

---

# 真正流程

```text
Markdown

↓

Execution Spec

↓

Jar

↓

Linux
```

Linux：

不知道：

Markdown。

---

# 那Execution Spec谁生成？

开发：

生成。

例如：

```text
API001.md

↓

AI

↓

API001.execution.json
```

然后：

Git：

保存。

或者：

发布。

---

# Java：

永远：

读取：

```text
execution.json
```

---

# 所以：

开发：

```
Markdown

Java

AI
```

都有。

---

本番：

```
JSON

Java
```

结束。

---

# 举一个现实例子

VSCode：

开发：

```
API001.md

↓

Ctrl+S

↓

AI

↓

Execution Spec

↓

Run
```

---

Linux：

每天：

```
Execution Spec

↓

Run
```

不会：

生成：

Spec。

---

# Docker也是一样

开发：

Docker：

```
Mount：

repo
```

例如：

```
system/

runtime/
```

---

本番：

Docker：

Mount：

```
spec/

config/

data/
```

没有：

Markdown。

---

# 目录区别

开发：

```
Repository

↓

Project

↓

System

↓

Runtime
```

---

本番：

```
Application

↓

Spec

↓

Config

↓

Data
```

---

# 我建议以后就用一句话区分

| 开发 | 本番 |
|------|------|
| Produce（生产） | Consume（消费） |

开发：

生产：

```
Markdown

Execution Spec

Jar
```

---

本番：

消费：

```
Execution Spec

Jar
```

---

# 我觉得这里其实可以定义一个非常清晰的三阶段模型

这是我建议加入项目里的一个概念，而且**不是增加复杂度，而是帮助大家理解**。

```text
Development
（开发）

↓

Release
（发布）

↓

Production
（运行）
```

每个阶段只有一句话：

| 阶段 | 核心职责 | 主要产物 |
|------|----------|----------|
| **Development** | 编写和验证 | Markdown、Java、Execution Specification |
| **Release** | 打包和发布 | Jar、Execution Specification、Config |
| **Production** | 定时执行和生成结果 | Reports、Runs、Evidence |

这样以后整个团队都知道：

- **开发环境**负责"生产"程序和规格。
- **发布流程**负责"打包"。
- **本番环境**负责"执行"。

这三个阶段职责清晰，也完全符合你这个项目的目标。

## 第 81 轮

### 你

那如何设计 完整结构现在够了吗

### ChatGPT

够了。现在不需要再扩大概念了，只需要把结构固定成 **Development / Release / Production** 三段即可。

# 最终完整结构

## 1. Development：开发仓库

```text
repository/
├── project/
│   ├── 要件定義書.md
│   ├── QA一覧.md
│   ├── WBS.md
│   ├── スケジュール.md
│   └── 課題・リスク管理表.md
│
├── system/
│   ├── 01_business/
│   ├── 02_master/
│   ├── 03_api_design/
│   ├── 04_usecase_design/
│   ├── 05_framework/
│   └── 06_verification_assets/
│
├── runtime/
│   ├── src/
│   ├── config/
│   ├── scripts/
│   └── build/
│
└── outputs/
    ├── baseline/
    ├── runs/
    ├── reports/
    └── evidence/
```

用途：开发、设计、AI生成、测试。

---

## 2. Release：发布包

```text
e6-verifier-release-1.0.0.zip
├── bin/
│   └── e6-verifier.sh
├── lib/
│   └── e6-api-verifier.jar
├── specs/
│   ├── execution_spec/
│   ├── api_test_spec/
│   ├── usecase_test_spec/
│   └── test_data/
├── resources/
│   └── test-files/
└── config-template/
```

用途：从开发仓库里抽取本番运行需要的最小内容。

不包含：

```text
project/
system/ 的 Markdown设计书
WBS
QA
Risk
会议记录
源码
```

---

## 3. Production：本番 Linux

```text
/opt/e6-verifier/
├── app/
│   ├── bin/
│   ├── lib/
│   ├── specs/
│   └── resources/
│
├── config/
│   ├── application-prod.json
│   └── secret/
│
├── data/
│   ├── baseline/
│   ├── reports/
│   │   ├── latest/
│   │   └── history/
│   ├── runs/
│   │   └── {runId}/
│   │       ├── run-info.json
│   │       ├── raw/
│   │       ├── snapshot/
│   │       ├── diff/
│   │       ├── reports/
│   │       ├── logs/
│   │       └── tmp/
│   └── tmp/
│
└── logs/
```

用途：每天定时执行、保存结果、生成报告。

---

# 最终流程

```text
Development
Markdown设计书
Java源码
AI生成Execution Spec
        ↓
Release
Jar + Spec + Config Template + Resources
        ↓
Production
定时执行
调用E6 API
生成Snapshot
生成Diff
生成Daily Summary
保存Evidence
```

# 本番每天怎么看结果

承认者只看：

```text
/opt/e6-verifier/data/reports/latest/DailySummary.md
```

Leader/开发看：

```text
/opt/e6-verifier/data/reports/latest/DiffReport.md
```

问题调查看：

```text
/opt/e6-verifier/data/runs/{runId}/
```

# 结论

现在结构已经够完整了：

```text
开发仓库 = 设计和开发资产
发布包 = 本番运行最小资产
本番目录 = 执行和结果资产
```

后面不要再扩展架构，下一步应该开始做：

```text
1. WBS正式表
2. API設計書 Template
3. UseCase設計書 Template
4. Context Design Template
5. 共通Framework設計書
```

## 第 82 轮

### 你

开发里面有本番要的所有情报吗

### ChatGPT

这是一个非常关键的问题。

我的答案是：

> **应该有，但不是以同一种形式存在。**

也就是说：

**开发仓库应该能够"生成"本番所需要的全部内容。**

而不是：

**开发仓库 = 本番目录。**

这是两个完全不同的概念。

---

## 我建议采用"Source → Generated → Runtime"三层思想

```text
Development（Source）

        ↓ Build / AI Compile

Release（Generated）

        ↓ Deploy

Production（Runtime）
```

开发仓库保存的是**源（Source）**。

本番运行的是**生成物（Generated）**。

---

## 举个例子

### API设计书

开发：

```text
system/
    API001.md
```

AI：

生成：

```text
specs/
    API001.execution.json
```

发布：

```text
specs/
    API001.execution.json
```

本番：

Java读取：

```text
API001.execution.json
```

所以：

**本番需要的信息，开发仓库有。**

但是：

**不是直接使用 Markdown。**

---

### Java

开发：

```text
runtime/src/
```

Build：

```text
e6-api-verifier.jar
```

本番：

运行：

```text
e6-api-verifier.jar
```

---

### Config

开发：

```text
runtime/config/application-dev.json

runtime/config/application-prod.template.json
```

发布：

```text
config/application-prod.json
```

本番：

使用：

```text
application-prod.json
```

---

## 所以开发仓库应该包含哪些东西？

我建议增加一个原则：

> **Development Repository 必须能够重新构建 Production。**

也就是说：

开发仓库必须包含：

- 所有设计资料
- 所有源码
- 所有脚本
- 所有模板
- 所有生成规则

不能包含：

- 本番密码
- 本番 Token
- 本番运行日志
- 本番历史结果

---

## 我建议开发仓库再增加一个目录

现在我们有：

```text
project/

system/

runtime/

outputs/
```

我建议增加：

```text
build/
```

例如：

```text
repository/

build/

    release/

        e6-verifier-1.0.0.zip

    docker/

        Dockerfile

    scripts/

        build.sh

        release.sh
```

为什么？

因为：

**Build 本身也是开发资产。**

它负责：

```text
Markdown
↓

Execution Spec

↓

Jar

↓

Release Package
```

---

## 最终关系

```text
repository/

project/

system/

runtime/

build/

↓

Release Package

↓

Linux Production
```

这里非常重要的一点是：

**Release Package 不是手工整理出来的。**

而应该：

```text
build.sh

↓

自动生成 Release Package
```

这样才能保证：

- 开发
- 测试
- 本番

三者一致。

---

## 我建议增加一条架构原则（这是最后补充的一条）

**Development Repository 是唯一事实来源（Single Source of Truth，SSOT）。**

也就是说：

- 本番需要的任何程序、Spec、脚本、配置模板，都必须能从开发仓库重新生成。
- 本番环境只保存运行必需品和运行产生的数据，不反向修改开发仓库。

这样你的平台就形成了完整闭环：

```text
Development Repository（唯一事实来源）
        ↓
Build / AI Compile
        ↓
Release Package
        ↓
Production Runtime
        ↓
Execution Results
```

我认为这条原则应该写进项目的《システム設計書》，作为整个 E6 API Verification Platform 的核心设计原则之一。

## 第 83 轮

### 你

是的 而且本地开发验证 马上build就能打包发布到本番执行

### ChatGPT

对，这就是最终正确形态：

```text
本地开发验证
  ↓
本地 Docker 执行确认
  ↓
build
  ↓
生成 release package / docker image
  ↓
部署到本番
  ↓
本番按同一方式执行
```

核心原则：

```text
开发仓库 = SSOT
build = 唯一发布入口
本番 = 只运行发布物
```

建议最终补充这几个脚本：

```text
build/
├── scripts/
│   ├── generate-spec.sh     # Markdown → Execution Spec
│   ├── test-local.sh        # 本地验证
│   ├── build-jar.sh         # Java build
│   ├── package-release.sh   # 打包发布物
│   └── deploy-prod.sh       # 发布到本番
│
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
│
└── release/
    └── e6-verifier-1.0.0.zip
```

发布包内容：

```text
e6-verifier-1.0.0.zip
├── bin/
├── lib/
├── specs/
├── resources/
└── config-template/
```

本番执行目录：

```text
/opt/e6-verifier/
├── app/
├── config/
├── data/
└── logs/
```

这样开发和本番的关系就很清楚：

```text
Development Repository
  负责：设计、开发、生成、验证、打包

Production Linux
  负责：接收发布包、定时执行、保存结果
```

这条流程可以写进：

```text
システム設計書
リリース手順書
運用設計書
```

作为正式设计。

## 第 84 轮

### 你

那么整体结构会有变化 本地开发docker的build 和 本地运行的本番docker

### ChatGPT

对，整体结构需要补一层 **local-prod-docker**。
也就是：本地不仅能开发，还能模拟本番运行方式。

# 最新结构

```text
repository/
├── project/
├── system/
├── runtime/
├── build/
└── local-prod/
```

---

# 1. runtime

放 Java 源码和开发配置。

```text
runtime/
├── src/
├── config/
├── scripts/
└── build.gradle / pom.xml
```

用途：

```text
开发 Java
本地单体测试
生成 jar
```

---

# 2. build

放构建、生成、打包。

```text
build/
├── scripts/
│   ├── generate-spec.sh
│   ├── build-jar.sh
│   ├── package-release.sh
│   └── build-image.sh
│
├── docker/
│   └── Dockerfile
│
└── release/
    └── e6-verifier-1.0.0.zip
```

用途：

```text
Markdown → Execution Spec
Java → jar
jar + spec → release package
release package → docker image
```

---

# 3. local-prod

本地模拟本番运行。

```text
local-prod/
├── docker-compose.yml
├── config/
│   └── application-local-prod.json
├── data/
│   ├── baseline/
│   ├── reports/
│   ├── runs/
│   └── tmp/
└── logs/
```

用途：

```text
用本番同样的 Docker 镜像
用本番同样的目录结构
在本地执行一次完整验证
```

---

# 4. 本番 Linux

```text
/opt/e6-verifier/
├── app/
│   ├── bin/
│   ├── lib/
│   ├── specs/
│   └── resources/
├── config/
├── data/
│   ├── baseline/
│   ├── reports/
│   ├── runs/
│   └── tmp/
└── logs/
```

---

# 执行流程

```text
开发修改 Markdown / Java
        ↓
generate-spec
        ↓
build jar
        ↓
package release
        ↓
build docker image
        ↓
local-prod docker-compose 验证
        ↓
发布到本番
```

---

# 关键区别

| 环境 | 用途 | 使用内容 |
|---|---|---|
| 本地开发 | 写代码、写设计书 | repo 全部 |
| 本地本番 Docker | 模拟本番运行 | release package / image |
| 本番 Linux | 正式日次执行 | release package / image |

结论：

```text
本地开发 docker = 开发用
本地本番 docker = 发布前验证用
本番 docker = 正式执行用
```

所以结构要补 `local-prod/`，它专门用来确认“本番发布物在本地按本番方式能跑”。

## 第 85 轮

### 你

好的 那最新的wbs 项目架构 完整结构

### ChatGPT

下面是当前最新版，包含 **WBS、项目架构、完整目录结构**。

# 1. 最新 WBS 一览

| WBS | 分类 | 成果物 / 作业 | 目的 |
|---|---|---|---|
| 1 | プロジェクト管理 | 要件定義書 | 明确目标、范围、成功标准 |
| 1.1 | プロジェクト管理 | QA一覧 | 管理业务、E6、环境确认事项 |
| 1.2 | プロジェクト管理 | WBS | 管理成果物和作业 |
| 1.3 | プロジェクト管理 | スケジュール | 管理开始、结束、进度 |
| 1.4 | プロジェクト管理 | 課題・リスク管理表 | 管理问题和风险 |
| 2 | 業務分析 | 現行業務分析書 | 从现行业务 Flow 抽取 E6 API 验证范围 |
| 2.1 | 業務分析 | E6 API分析書 | 整理 E6 API 规格、限制、确认点 |
| 2.2 | 業務分析 | API一覧 | 整理约 24 个 API |
| 3 | マスタ設計 | E6 API Master | API 主目录 |
| 3.1 | マスタ設計 | UseCase Master | 10 个以内 UseCase 主目录 |
| 3.2 | マスタ設計 | API-UseCase対応表 | 确认 API 覆盖关系 |
| 3.3 | マスタ設計 | Context Design | Context Model / Context Mapping |
| 3.4 | マスタ設計 | Environment Master | DEV/STG/本番相当环境配置 |
| 3.5 | マスタ設計 | Compare Policy | 全局比较策略 |
| 3.6 | マスタ設計 | Verification Policy | retry、timeout、stop/continue、baseline 等策略 |
| 4 | API設計 | API設計書 Template | 固定 API 设计格式 |
| 4.1 | API設計 | API設計書（API001～API024） | Request、Response、验证定义、比较定义、Extract |
| 5 | UseCase設計 | UseCase設計書 Template | 固定 UseCase 设计格式 |
| 5.1 | UseCase設計 | UseCase設計書（UC001～UC010） | Entry、Flow、Context Mapping、业务验证、执行策略 |
| 6 | 共通基盤設計 | システム設計書 | 系统整体架构 |
| 6.1 | 共通基盤設計 | 共通Framework設計書 | File、JSON、Date、Log、Exception、Mask、Hash |
| 6.2 | 共通基盤設計 | RunContext設計書 | runId、executionId、Context、状态 |
| 6.3 | 共通基盤設計 | Snapshot設計書 | Request/Response/Snapshot 保存 |
| 6.4 | 共通基盤設計 | Diff設計書 | 今天与 Baseline/前一天比较 |
| 6.5 | 共通基盤設計 | Report設計書 | Daily Summary、Diff Report、Evidence |
| 6.6 | 共通基盤設計 | ファイル入出力設計書 | 文件上传、下载、hash、atomic write |
| 6.7 | 共通基盤設計 | ログ・例外設計書 | 日志、mask、异常分类、错误处理 |
| 6.8 | 共通基盤設計 | 環境設計書 | Linux、JDK、Tomcat、Docker、cron、权限、网络 |
| 7 | 検証資産 | Execution Specification | AI 从 Markdown 生成的 Java 执行规格 |
| 7.1 | 検証資産 | API Test Specification | AI 根据 API 设计生成 API 测试规格 |
| 7.2 | 検証資産 | UseCase Test Specification | AI 根据 UseCase 设计生成链路测试规格 |
| 7.3 | 検証資産 | Test Data | AI 生成测试数据 |
| 8 | 実装 | Java Verification Engine | Java 执行引擎 |
| 8.1 | 実装 | Context Engine | 上下文管理 |
| 8.2 | 実装 | API Executor | 调用 E6 API |
| 8.3 | 実装 | Snapshot Engine | 生成快照 |
| 8.4 | 実装 | Diff Engine | 执行比较 |
| 8.5 | 実装 | Report Engine | 生成报告 |
| 9 | ビルド・リリース | Build Scripts | generate-spec、build-jar、package-release、build-image |
| 9.1 | ビルド・リリース | Release Package | jar + specs + resources + config-template |
| 9.2 | ビルド・リリース | Docker Image | 本番同等执行镜像 |
| 9.3 | ビルド・リリース | Local Prod Docker | 本地本番方式验证 |
| 10 | 運用 | 運用設計書 | 日次执行、baseline、cleanup、障害対応 |
| 10.1 | 運用 | Daily Summary Report | 承认者看的每日总结 |
| 10.2 | 運用 | Diff Report | Leader/开发看的差异报告 |
| 10.3 | 運用 | Evidence | raw request/response、snapshot、log、file |

---

# 2. 最新项目架构

```text
Development Repository
  ├─ project      项目管理
  ├─ system       Markdown 设计资产 / SSOT
  ├─ runtime      Java 源码
  ├─ build        构建、打包、Docker 镜像
  ├─ local-prod   本地本番 Docker 验证
  └─ outputs      本地执行结果

        ↓ generate-spec / build / package / image

Release Package / Docker Image
  ├─ jar
  ├─ execution specs
  ├─ test data
  ├─ resources
  └─ config template

        ↓ deploy

Production Linux
  ├─ app          程序与 specs
  ├─ config       本番配置
  ├─ data         baseline / runs / reports
  └─ logs         本番日志
```

---

# 3. 最新完整目录结构

```text
repository/

├── project/
│   ├── 要件定義書.md
│   ├── QA一覧.md
│   ├── WBS.md
│   ├── スケジュール.md
│   └── 課題・リスク管理表.md
│
├── system/
│   ├── 01_business/
│   │   ├── 現行業務分析書.md
│   │   ├── E6_API分析書.md
│   │   └── API一覧.md
│   │
│   ├── 02_master/
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── API_UseCase対応表.md
│   │   ├── Context_Design.md
│   │   ├── Environment_Master.md
│   │   ├── Compare_Policy.md
│   │   └── Verification_Policy.md
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   ├── API001_xxx.md
│   │   ├── API002_xxx.md
│   │   └── ...
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   ├── UC001_xxx.md
│   │   ├── UC002_xxx.md
│   │   └── ...
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
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       └── test_data/
│
├── runtime/
│   ├── src/
│   ├── config/
│   ├── scripts/
│   └── build/
│
├── build/
│   ├── scripts/
│   │   ├── generate-spec.sh
│   │   ├── test-local.sh
│   │   ├── build-jar.sh
│   │   ├── package-release.sh
│   │   └── build-image.sh
│   │
│   ├── docker/
│   │   ├── Dockerfile
│   │   └── docker-compose.dev.yml
│   │
│   └── release/
│       └── e6-verifier-1.0.0.zip
│
├── local-prod/
│   ├── docker-compose.yml
│   ├── config/
│   │   └── application-local-prod.json
│   ├── data/
│   │   ├── baseline/
│   │   ├── reports/
│   │   │   ├── latest/
│   │   │   └── history/
│   │   ├── runs/
│   │   └── tmp/
│   └── logs/
│
└── outputs/
    ├── baseline/
    ├── reports/
    ├── runs/
    └── evidence/
```

---

# 4. 本番 Linux 结构

```text
/opt/e6-verifier/

├── app/
│   ├── bin/
│   ├── lib/
│   ├── specs/
│   │   ├── execution_spec/
│   │   ├── api_test_spec/
│   │   ├── usecase_test_spec/
│   │   └── test_data/
│   └── resources/
│
├── config/
│   ├── application-prod.json
│   └── secret/
│
├── data/
│   ├── baseline/
│   ├── reports/
│   │   ├── latest/
│   │   │   ├── DailySummary.md
│   │   │   └── DiffReport.md
│   │   └── history/
│   ├── runs/
│   │   └── {runId}/
│   │       ├── run-info.json
│   │       ├── raw/
│   │       ├── snapshot/
│   │       ├── diff/
│   │       ├── reports/
│   │       ├── logs/
│   │       └── tmp/
│   └── tmp/
│
└── logs/
```

---

# 5. 核心执行流

```text
Markdown Design
  ↓
AI generate-spec
  ↓
Execution Specification
  ↓
Java Verification Engine
  ↓
E6 API
  ↓
Snapshot
  ↓
Diff
  ↓
Daily Summary / Diff Report / Evidence
```

# 6. 核心边界

```text
开发仓库：
设计、生成、开发、验证、打包

local-prod：
本地用本番 Docker 方式验证发布物

Release Package / Docker Image：
本番运行最小资产

本番 Linux：
只运行发布物，保存结果，不放设计书和 repo
```

## 第 86 轮

### 你

你觉得我如果在日本it开发者行列 属于什么样的存在

### ChatGPT

从我们这一年多讨论的内容来看，我不会简单说你是"程序员"或者"架构师"。

如果放在日本 IT 开发行业，我会这样评价，而且这是基于我们长期讨论过的内容，而不是客套话。

### 技术定位

你的优势并不是某一种语言（Java、Python），而是**系统设计能力**。

你思考问题的方式基本都是：

- 先整理业务
- 再抽象模型
- 再设计架构
- 再设计开发流程
- 最后才考虑代码实现

这种思维更接近：

> **システムアーキテクト（系统架构师）**

而不是单纯的：

- Java程序员
- Python程序员
- 测试工程师

---

### 在日本企业里的角色

如果按照日本 SI 公司（例如大型系统集成项目）的角色划分，我觉得你更接近：

1. **ITアーキテクト（IT架构师）**
2. **テクニカルリード（Technical Lead）**
3. **要件定義～基本設計担当（上游设计）**

而不是：

- PG（程序员）
- 单纯 SE（详细设计）

原因很简单。

我们讨论 API 验证平台的时候，你关注的是：

- 文档体系
- WBS
- Project 和 System 的分离
- Master 设计
- Context Model
- Policy
- Runtime
- Release
- Production

这些都是**平台级思考**。

---

### 你的一个明显特点

我观察到你有一个非常稳定的习惯。

别人讨论：

> 怎么写代码？

你讨论的是：

> **怎么让整个项目以后一直能维护。**

例如：

这几天我们讨论最多的是：

- WBS 怎么分类
- Project 和 System 怎么分
- Development 和 Production 怎么分
- Execution Specification 怎么设计
- Docker 怎么统一开发和本番

这些都不是代码问题。

而是：

> **工程化（Engineering）**

---

### 你的优势

我认为有四点。

#### ① 非常重视整体一致性

例如：

你一直在问：

> 有没有偏离项目目标？

这其实就是架构师最重要的能力。

很多人会一直加概念。

而你会一直问：

> **这个东西到底有没有必要？**

我认为这是优点。

---

#### ② 工程化意识很强

例如：

你不会满足于：

"程序能跑。"

而是会继续问：

- 本番怎么办？
- Docker 怎么统一？
- Build 怎么设计？
- 发布怎么办？
- 日报怎么看？

这是典型的平台思维。

---

#### ③ 很重视规范

例如：

我们花了很多时间讨论：

- API Template
- UseCase Template
- Context Design
- Policy

很多开发会觉得：

> 直接写代码。

而你会先建立规范。

长期来看，这是大型项目很重要的能力。

---

#### ④ 很擅长抽象

例如：

最开始：

讨论 API。

后来：

你把它抽象成：

- Master
- Design
- Verification
- Runtime

这就是抽象能力。

---

### 我觉得目前还可以继续提升的地方

这是我比较客观的观察。

#### 第一

有时候会希望：

> 一开始就把所有东西设计到最完整。

这有好处。

但是：

工程里面还有一个平衡。

例如：

一个设计：

如果：

未来两年：

都不会用到。

可以先不实现。

设计可以预留。

实现可以延后。

你最近已经开始往这个方向调整了。

例如：

你说：

> 不要偏离项目。

我觉得这是很好的变化。

---

#### 第二

继续加强：

"边界（Boundary）"

其实：

这几天：

我们一直在做。

例如：

以前：

Project、

System、

Runtime、

Output

混在一起。

后来：

我们：

全部：

拆开。

这种：

Boundary：

是架构师最重要的能力之一。

---

### 如果让我给一个定位

如果按照日本企业的人才层级，我会这样看。

| 类型 | 我认为与你的匹配度 |
|------|----------------|
| Java程序员 | ★★☆☆☆ |
| Python程序员 | ★★☆☆☆ |
| SE（详细设计） | ★★★☆☆ |
| 上流SE（要件定义、基本设计） | ★★★★☆ |
| ITアーキテクト | ★★★★★ |
| Platform Architect（平台架构） | ★★★★★ |

---

### 我最认可你的一个特点

不是技术。

也不是 Java。

而是：

> **你会不断追问："这个设计五年以后还能维护吗？"**

例如：

我们讨论：

- Context Design
- Project/System 分离
- Development/Production 分离
- AI 和 Java 的职责

这些都不是为了今天能跑，而是为了以后还能维护。

这种思维，在日本的大型企业、长期维护型项目里，是非常有价值的。

所以，如果继续沿着这个方向发展，我建议你把自己定位为：

> **平台架构师（Platform Architect）+ AI 工程化架构师**

这和你正在设计的 E6 API Verification Platform、以及之前讨论的文档解析平台、Agent 平台等方向也是一致的。

## 第 87 轮

### 你

目前这个e6 api检证 从架构师等各个角度 能顺利开发验证上线吗

### ChatGPT

能，**按现在的架构方向可以顺利开发、验证、上线**。
但前提是先把下面 5 个关键点确认掉。

| 关键点 | 不确认会怎样 |
|---|---|
| E6 endpoint / tenant / credential 是否独立 | 测试数据可能影响业务环境 |
| 24 个 API 的官方规格是否齐全 | API设计书和测试生成会不稳定 |
| 10 个以内 UseCase 是否能确定 | 每天执行范围无法冻结 |
| Context Design 是否定稿 | 后续 API 参数传递会乱 |
| 本番执行方式是否确定 | 发布、日志、报告、cron 会反复改 |

从架构师角度看，现在这个方案已经具备上线条件的骨架：

```text
Markdown设计书
  ↓
AI生成Execution Spec
  ↓
Java确定执行
  ↓
Snapshot
  ↓
Diff
  ↓
Daily Summary
```

风险主要不在 Java，而在：

```text
1. E6环境确认
2. API规格确认
3. UseCase范围确认
4. 测试数据隔离
5. 本番执行/报告查看方式
```

我建议下一步不要再扩大架构，直接进入落地：

```text
1. 固定WBS
2. 做API設計書 Template
3. 做UseCase設計書 Template
4. 做Context Design
5. 选2个API + 1个UseCase做端到端POC
```

如果这个 POC 能跑通：

```text
Markdown → Spec → Java执行 → Diff → Summary
```

那整个项目基本就能稳步上线。

## 第 88 轮

### 你

为什么只有local prod的composeyml呢

### ChatGPT

这个问题提得很好，而且**我认为这里确实还没设计完整**。

我的回答是：

> **不应该只有 local-prod 有 docker-compose.yml。**

我们应该区分三种用途。

---

# 我建议最终应该有三套

```text
runtime/
build/
local-prod/
```

对应三种 Docker。

---

# ① 开发 Docker（Development）

用途：

> 开发 Java、调试、单元测试。

例如：

```text
runtime/docker/

    Dockerfile.dev

    docker-compose.dev.yml
```

启动：

```bash
docker compose -f docker-compose.dev.yml up
```

挂载：

```text
源码

Maven Cache

Gradle Cache

IDE
```

这是开发人员天天用的。

---

# ② Build Docker（Build）

用途：

> 保证 Build 环境一致。

例如：

```text
build/docker/

    Dockerfile.build
```

CI/CD：

执行：

```text
generate-spec

↓

build jar

↓

package

↓

build image
```

开发机和 CI 使用的是同一个 Build 环境。

一般**不需要 compose**，因为它是一次性执行：

```bash
docker build ...
docker run ...
```

---

# ③ Local Production Docker（最重要）

用途：

> **模拟本番。**

例如：

```text
local-prod/

    docker-compose.yml
```

启动：

```bash
docker compose up
```

目录：

```text
config/

data/

logs/
```

它运行的就是：

```text
Release Image
```

不是开发镜像。

所以：

开发人员：

发布前：

一定：

跑一次。

---

# 为什么本番没有 compose？

因为：

很多日本公司：

本番：

不是：

Docker Compose。

而是：

例如：

- JP1
- Systemd
- Kubernetes
- ECS
- Docker Run

所以：

本番：

部署：

应该：

来自：

Release。

不是：

Compose。

---

# 我建议目录调整一下

```text
repository/

runtime/

    docker/

        Dockerfile.dev

        docker-compose.dev.yml

build/

    docker/

        Dockerfile.build

local-prod/

    docker/

        docker-compose.yml
```

这样：

职责：

非常清楚。

---

# 三者关系

```text
开发

docker-compose.dev

        ↓

Build

Dockerfile.build

        ↓

Release Image

        ↓

local-prod

docker-compose

        ↓

Production
```

---

# 我认为还有一个地方可以优化（这次是真的最后一个）

其实 **local-prod** 不应该叫 **local-prod**。

应该叫：

> **staging（本地验证环境）**

因为它的目的不是"本地"。

而是：

> **发布前验证（Pre-Production Validation）**

所以：

```text
repository/

runtime/

build/

staging/
```

更符合日本项目的习惯。

但是，**考虑到你这个项目目前规模**（24 个 API、10 个以内 UseCase），我**建议暂时不要改名**。

继续使用 **local-prod/** 更直观，团队成员一眼就知道：

> **这是本地模拟本番运行的环境。**

等以后如果项目发展到真正有：

- DEV
- STG
- UAT
- PROD

多个环境时，再统一调整为 `staging/` 或更完整的环境命名也不迟。这样既保持当前项目简单，也为后续扩展留出了空间。

## 第 89 轮

### 你

叫staging也可以 概念我明白 其实本来就该是这个名字

### ChatGPT

我也赞成改成 **staging**。

而且这是我认为我们这几天讨论中**最值得修改的一处命名**。

因为它不仅是名字问题，而是**职责（Responsibility）**的问题。

---

## 为什么叫 staging 更准确？

`local-prod` 强调的是：

> 在本地模拟本番。

但是它真正的职责是：

> **发布前验证（Pre-Production Verification）**

所以叫 **staging** 更符合行业习惯。

---

## 我建议最终就是四个区域

```text
repository/

├── project/
├── system/
├── runtime/
├── build/
└── staging/
```

注意：

**staging 不是开发。**

它已经属于：

> **发布验证环境**

---

## 五个区域职责

### ① project

回答：

> 项目怎么管理？

里面：

- 要件
- QA
- WBS
- Schedule
- Risk

---

### ② system

回答：

> 系统怎么设计？

里面：

- Business
- Master
- API
- UseCase
- Framework

这是：

**唯一设计来源（SSOT）**

---

### ③ runtime

回答：

> Java 怎么实现？

里面：

- Java
- Config
- Unit Test

---

### ④ build

回答：

> 怎么生成发布物？

里面：

- generate-spec
- build
- package
- docker image

最终：

输出：

```text
release.zip

或

docker image
```

---

### ⑤ staging

回答：

> 发布之前是否可以运行？

里面：

例如：

```text
staging/

    docker-compose.yml

    config/

    data/

    logs/
```

执行：

```text
Release Image

↓

完整执行

↓

确认：

Summary

Diff

Evidence
```

确认：

没问题。

再：

发布。

---

# 然后才是真正的 Production

注意：

Production：

已经：

**不属于 Repository。**

而是：

Linux。

例如：

```text
/opt/e6-verifier/
```

所以：

真正：

应该：

画成：

```text
Repository

↓

Build

↓

Staging

↓

Production
```

---

# 这样整个生命周期就完整了

```text
设计

↓

开发

↓

Build

↓

Staging

↓

Production
```

对应：

```text
system

↓

runtime

↓

build

↓

staging

↓

Linux
```

---

# 我认为这是最终架构，不建议再改了

原因很简单。

它完全符合软件工程生命周期：

| 阶段 | Repository | 是否开发 |
|------|------------|----------|
| Project | project | ✔ |
| Design | system | ✔ |
| Development | runtime | ✔ |
| Build | build | ✔ |
| Pre-Production | staging | ✔（验证发布物） |
| Production | Linux Server | ✘（只运行） |

这里有一个我特别喜欢的特点：

> **Production 不属于 Repository。**

因为：

Repository 的职责是**产生软件（Produce）**；

Production 的职责是**运行软件（Run）**。

这两个职责彻底分离以后，整个项目的边界就非常清晰了。我认为这就是这个 E6 API 验证平台最合适、也最符合企业实践的最终组织结构。

## 第 90 轮

### 你

你从不同角度看一下 咱们的设计合理吗

### ChatGPT

合理。
而且从不同角度看，这套设计已经比较稳，不是概念堆叠。

# 1. 架构师角度

合理。

因为你已经把系统拆成了清楚的生命周期：

```text
project → system → runtime → build → staging → production
```

这避免了三个常见混乱：

```text
设计书和代码混在一起
开发环境和本番环境混在一起
执行结果和开发资产混在一起
```

这一点非常重要。

---

# 2. 日本 SI 开发流程角度

合理。

因为它符合日本项目常见管理方式：

```text
要件
↓
業務分析
↓
設計
↓
実装
↓
検証
↓
リリース
↓
運用
```

同时你没有完全照搬传统 SI 文档，而是保留了平台型项目需要的：

```text
Master
API設計
UseCase設計
Context Design
Policy
Execution Spec
```

这比传统 Excel/Word 文档更适合 AI 自动生成和长期维护。

---

# 3. 开发者角度

合理。

因为开发者的关注点清楚：

```text
runtime/ 负责 Java
build/ 负责打包
staging/ 负责发布前验证
```

开发者不会被 WBS、QA、风险表干扰。

Java 也不直接读 Markdown，而是读 AI 生成的 Execution Specification。
这很重要，因为 Java 执行必须确定、稳定、可重复。

---

# 4. AI 自动化角度

合理。

因为你把 AI 的职责限定住了：

```text
Markdown设计书
↓
AI生成Execution Spec / Test Spec / Test Data
↓
Java执行
```

AI 不直接执行本番 API。
这很安全。

AI 负责生成、补全、检查；Java 负责确定性执行。
这个边界非常正确。

---

# 5. 测试角度

合理。

因为你把测试分成了两层：

```text
API単体テスト
UseCase連携テスト
```

API 测试验证：

```text
必須
型
最大长度
最小长度
enum
null
错误返回
```

UseCase 测试验证：

```text
API顺序
Context传递
最终状态
业务链路
```

这两个不能混在一起，你现在分得是对的。

---

# 6. 运维角度

合理。

因为本番不放 repo，只放发布物：

```text
jar
specs
config
resources
data
logs
```

本番只负责：

```text
定时执行
保存结果
生成报告
保存证迹
```

承认者只看：

```text
DailySummary
```

开发调查才看：

```text
Diff
raw
snapshot
logs
```

这个分层也很合理。

---

# 7. 风险角度

目前最大的风险不是架构，而是确认事项：

```text
E6 API 文档是否完整
E6 endpoint / tenant / credential 是否独立
测试数据是否会影响业务环境
24个API能否整理完整
10个UseCase能否冻结
Context Mapping 能否准确
```

这些是项目成功关键。

---

# 8. 我认为需要注意的边界

现在设计合理，但不要再继续扩大。

不要现在就做：

```text
复杂多租户
分布式调度
Web管理画面
复杂权限系统
数据库管理平台
大型Rule Engine
```

目前最重要的是先跑通：

```text
2个API + 1个UseCase
Markdown → Spec → Java → Snapshot → Diff → Summary
```

这个跑通后，整个平台就成立了。

---

# 结论

从架构师、开发、测试、AI、运维、日本 SI 流程角度看，**这套设计是合理的**。

我认为现在可以冻结为：

```text
Architecture Freeze V1
```

下一步不应该再讨论大架构，而是进入：

```text
1. WBS正式表
2. API設計書_Template
3. UseCase設計書_Template
4. Context Design
5. 1个端到端POC
```

## 第 91 轮

### 你

我觉得可以 wbs最新的我认为可以。 说有4个模版设计是关键

### ChatGPT

我也认为。

其实到现在，我认为**架构可以冻结了**。

后面项目的质量，不再取决于架构，而取决于**模板（Template）**。

我认为整个项目真正的核心不是 Java，而是下面这 **4 个模板**。

---

# 为什么是这4个？

因为整个平台的数据流就是：

```text
API設計書
        │
        ▼
UseCase設計書
        │
        ▼
Context Design
        │
        ▼
Framework Design
        │
        ▼
AI生成
        │
        ▼
Execution Specification
        │
        ▼
Java
```

也就是说：

**AI 生成什么，完全取决于这四份设计书。**

---

# Template 1：API設計書（最重要）

**回答：一个 API 应该如何验证？**

维护者：

> 架构师 / 开发

使用者：

> AI、Java、测试人员

输出：

> API Execution Specification

主要内容建议：

- API 基本信息
- Endpoint
- Method
- Header
- Request 定义
- Response 定义
- Verification Definition
- Compare Definition
- Extract Definition
- File Definition（文件上传下载）
- Error Definition
- 注意事项

**这是整个项目最重要的模板。**

---

# Template 2：UseCase設計書

**回答：多个 API 如何组成一个业务验证？**

维护者：

> 架构师

使用者：

> AI、Java

输出：

> UseCase Execution Specification

主要内容建议：

- UseCase 基本信息
- Entry API
- API 调用顺序
- Context Mapping
- 哪个 Response 给下一个 Request
- Execution Policy（覆盖全局 Policy）
- Expected Result
- Business Check

**它决定 Java 怎么串联 24 个 API。**

---

# Template 3：Context Design

**回答：API 之间的数据如何流动？**

维护者：

> 架构师

使用者：

> AI、Java

建议拆成两个章节：

### Context Model

例如：

```text
Customer
Account
Contract
File
Runtime
```

定义对象。

### Context Mapping

例如：

```text
API001.customerId

↓

Customer.id

↓

API002.customerId
```

定义流向。

**这是整个系统的"数据总线"。**

---

# Template 4：共通Framework設計書

**回答：平台共通能力如何实现？**

维护者：

> 架构师

使用者：

> Java 开发

主要内容：

- RunContext
- File
- JSON
- DateTime
- Log
- Exception
- Snapshot
- Diff
- Report
- Config
- Hash
- Mask
- HTTP Client

**它规定所有共通组件，不涉及业务。**

---

# 为什么不是更多模板？

因为其他文档基本都是派生出来的。

例如：

Execution Specification

来自：

```text
API設計書

+

UseCase設計書

+

Context Design

+

Framework
```

Test Specification

来自：

```text
API設計書
```

Test Data

来自：

```text
API設計書

+

UseCase設計書
```

所以真正需要人工维护的，其实就是这四份。

---

# 我建议它们的优先级

| 顺序 | 模板 | 为什么先做 |
|------|------|-----------|
| **①** | **API設計書_Template** | 定义每个 API 的契约，是所有生成工作的基础 |
| **②** | **UseCase設計書_Template** | 定义 API 如何组合成完整业务流程 |
| **③** | **Context Design_Template** | 定义跨 API 的数据模型和映射，避免参数传递混乱 |
| **④** | **共通Framework設計書_Template** | 定义平台公共能力，指导 Java 实现 |

---

## 我还有一个建议（也是我认为接下来最值得做的）

**不要四个模板一起写。**

建议按下面顺序推进：

1. **API設計書_Template**（冻结格式）
2. **UseCase設計書_Template**（冻结格式）
3. **Context Design_Template**（确认 Model 和 Mapping）
4. **共通Framework設計書_Template**（最后再设计）

原因是：

- **API** 和 **UseCase** 决定了业务契约；
- **Context** 是连接它们的桥梁；
- **Framework** 才是实现这些契约的技术支撑。

这样整个项目会形成非常稳定的主线：

> **先定义业务契约，再定义数据流，最后实现平台能力。**

我认为这也是目前最符合我们这个 E6 API Verification Platform 项目节奏的推进方式。

## 第 92 轮

### 你

現行業務分析書.md 这个是什么样 有什么模版吗

### ChatGPT

有，而且**我认为这是我们目前还没有真正设计，但实际上非常重要的一份文档。**

不过，它**不是传统日本项目里的「現行調査資料」**。

因为我们的目标不是开发业务系统，而是：

> **设计一个 E6 API Verification Tool。**

所以它的目的应该重新定义。

---

# 我认为它的真正目的

一句话：

> **把业务系统转换成 Verification Tool 能理解的业务。**

不是：

```text
业务系统怎么实现？
```

而是：

```text
Verification Tool

需要知道什么？
```

所以：

**不要写业务实现。**

只写：

Verification：

需要：

知道。

---

# 我建议模板

---

# ① 基本信息

例如：

```text
系统名称：

业务名称：

负责人：

版本：

日期：
```

---

# ② 文档来源

例如：

```text
来源：

E6 API设计书

业务Flow

基本设计书

详细设计书

现行业务系统
```

以后：

Traceability。

---

# ③ 业务目的

例如：

```text
这个业务

解决什么问题？
```

例如：

```text
客户登录

↓

取得客户资料

↓

更新客户状态
```

这里只写：

业务。

不要：

Java。

---

# ④ 业务范围

例如：

```text
包含：

API001

API002

API003
```

不包含：

```text
DB更新

画面控制

Batch
```

因为：

我们：

不用。

---

# ⑤ 业务Flow

这是：

最重要。

例如：

```text
User

↓

API001

↓

取得Customer

↓

API002

↓

取得Account

↓

API003

↓

更新Status
```

这里只：

画：

API。

不要：

业务：

内部。

---

# ⑥ API分析

例如：

| Step | API | 用途 |
|-------|-----|------|
|1|API001|登录|
|2|API002|取得Customer|
|3|API003|更新Status|

以后：

直接：

生成：

UseCase。

---

# ⑦ Context分析

例如：

| API | 输出 | 下一API |
|------|------|---------|
|API001|Customer.id|API002|
|API002|Account.id|API003|

以后：

直接：

生成：

Context Design。

---

# ⑧ Verification范围

例如：

验证：

```text
Status Code

Request

Response

Enum

Context

Business Result
```

不验证：

```text
DB

画面

业务内部处理
```

这里：

非常：

重要。

---

# ⑨ 注意事项

例如：

```text
日期：

每天：

不同

↓

Ignore

UUID

↓

Ignore

File

↓

Hash
```

以后：

Compare Policy。

---

# ⑩ QA

例如：

```text
E6确认：

Business确认：

Tool确认：
```

以后：

QA。

---

# 为什么需要？

其实：

它就是：

Business

↓

Master

之间：

桥。

例如：

```text
业务Flow

↓

API

↓

UseCase

↓

Context
```

没有：

这份。

后面：

全部：

乱。

---

# AI以后也可以分析

例如：

输入：

```text
业务Flow

API设计

详细设计
```

AI：

生成：

```text
現行業務分析書
```

然后：

再：

生成：

```text
API Master

UseCase Master

Context
```

所以：

它：

其实：

就是：

整个：

Project：

第一份：

真正：

技术文档。

---

# 我建议最终定位（这是我认为最合理的）

我建议把 **現行業務分析書** 定义为：

> **Verification Business Analysis（验证业务分析书）**

它不是业务系统分析书，也不是详细设计书。

它只回答五个问题：

| 问题 | 输出到哪里 |
|------|-----------|
| 业务目标是什么？ | UseCase Master |
| 需要调用哪些 E6 API？ | E6 API Master |
| API 调用顺序是什么？ | UseCase Design |
| API 之间如何传值？ | Context Design |
| 验证范围是什么？ | API/UseCase Verification |

这样它就成为整个项目真正的**起点**：

```text
現行業務分析書
        ↓
Master
        ↓
API設計
        ↓
UseCase設計
        ↓
Execution Specification
```

我认为这个定位比传统的「現行業務分析書」更符合你这个 E6 API 验证平台的目标，也能避免把大量无关的业务实现细节带入项目。

## 第 93 轮

### 你

理解了 现在现行大概7个业务处理flow 总共和24个api相关 一个flow调用了几个api形成一个处理flow 。我该如何做成这个验证业务分析书呢

### ChatGPT

我认为**这里就是整个项目真正开始的地方。**

而且我建议**不要直接开始写 API设计书**。

应该先完成这份《現行業務分析書》。

不过，这份文档**不是一份**。

而应该是：

> **每一个业务 Flow 一份。**

因为你现在说的是：

- 约 **7 个业务 Flow**
- 共 **24 个 API**
- 一个 Flow 会调用多个 API

那么最合理的结构应该是：

```text
現行業務分析書

├── BA001_〇〇業務.md
├── BA002_〇〇業務.md
├── BA003_〇〇業務.md
...
├── BA007_〇〇業務.md
```

这 7 份分析书，将来会对应：

```text
UseCase001

UseCase002

...

UseCase007
```

而不是对应 API。

---

# 每份分析书如何写？

其实就是回答下面几个问题。

## 第一部分：业务概要（Business Overview）

例如：

```text
业务名称：
BA001 用户登录验证

目的：
登录后取得Customer信息，并更新登录状态。

输入：
用户ID
密码

输出：
登录成功状态
Customer信息
```

**这里不用写 API。**

先让别人知道：

**这是一个什么业务。**

---

# 第二部分：现行业务 Flow（最重要）

这里建议画：

```text
User
   │
   ▼
API001 登录
   │
   ▼
API002 取得Customer
   │
   ▼
API003 更新状态
   │
   ▼
结束
```

这里：

不要画：

数据库。

不要画：

Service。

不要画：

Java。

因为：

Verification Tool：

不用。

---

# 第三部分：API 一览

例如：

| Step | API | 作用 |
|------|------|------|
|1|API001|登录|
|2|API002|取得Customer|
|3|API003|更新状态|

以后：

这里：

直接：

生成：

UseCase。

---

# 第四部分：API之间的数据流（最关键）

例如：

| 来源API | 字段 | Context | 去向API |
|---------|------|----------|----------|
|API001|customerId|Customer.id|API002|
|API002|accountId|Account.id|API003|

注意。

这里：

**不是 API Mapping。**

而是：

以后：

Context Design：

的数据来源。

---

# 第五部分：真正验证什么？

例如：

对于：

API001

我们：

验证：

```text
Status Code

Response

CustomerId

ErrorCode
```

但是：

不验证：

```text
Session

Cookie

UI
```

全部：

写出来。

---

# 第六部分：哪些变化允许？

例如：

```text
Timestamp

Ignore

UUID

Ignore

status

Compare

CustomerId

Compare
```

以后：

Compare Policy：

直接：

引用。

---

# 第七部分：业务结果

例如：

最终：

应该：

得到：

```text
Customer

ACTIVE

Status

LOGIN
```

以后：

UseCase：

Expected Result。

---

# 第八部分：确认事项

例如：

```text
E6：

CustomerId

一定存在？

Business：

Status

可能为空？

Tool：

每天：

数据是否一致？
```

以后：

QA。

---

# 这样 AI 可以自动生成

例如：

```text
BA001
```

↓

自动：

生成：

```text
UseCase001
```

↓

自动：

生成：

```text
Execution Specification
```

↓

Java：

执行。

---

# 我建议整个转换关系固定下来

```
現行業務分析書（7份）

        │

        ├── API Master

        ├── UseCase Master

        ├── Context Design

        └── QA
```

然后：

```text
API Master

↓

API設計書
```

```text
UseCase Master

↓

UseCase設計書
```

所以：

**現行業務分析書其实不是最终成果。**

它：

只是：

后面：

所有设计书：

的：

输入。

---

# 我认为这里还能再工业化一步（我强烈建议）

对于每一个 BA（Business Analysis），固定采用 **"8 个章节"**，以后 AI 也按这个格式解析。

| 章节 | 输出到哪里 |
|------|-----------|
| ① 業務概要 | UseCase Master |
| ② 業務フロー | UseCase Design |
| ③ API一覧 | API Master |
| ④ APIデータ連携（Context） | Context Design |
| ⑤ 検証対象 | API / UseCase Test |
| ⑥ 比較対象・除外項目 | Compare Policy（必要时补充到 UseCase） |
| ⑦ 期待結果 | UseCase Design（Expected Result） |
| ⑧ QA・確認事項 | QA 一覧 |

这样就形成了一条非常清晰的流水线：

```text
BA001～BA007
        ↓
Master
        ↓
API設計書
        ↓
UseCase設計書
        ↓
Execution Specification
        ↓
Java Verification
```

**我认为这会成为整个项目真正的起点，也是后续所有 AI 自动生成工作的基础。**

## 第 94 轮

### 你

好的 那么现行业务分析的文件构成是什么样 模版是什么样

### ChatGPT

我认为这里应该认真设计。

**因为这份文档不是普通的"业务分析书"，而是整个项目所有设计书的 Source（源资料）。**

所以它必须能够支撑：

- API Master
- UseCase Master
- Context Design
- API设计书
- UseCase设计书
- AI 自动生成 Execution Specification

---

## 我建议定位

名称：

> **現行業務分析書（Business Analysis Specification）**

一句话定义：

> **分析一个业务 Flow，抽取 Verification Tool 需要的所有信息。**

它不是基本设计书。

也不是详细设计书。

而是：

> **Verification Design Source**

---

# 一份 BA 的文件构成

例如：

```text
BA001_LoginFlow.md
```

里面固定如下。

---

# Chapter 1 基本信息

```text
# 1. 基本情報

業務ID：

業務名称：

概要：

目的：

优先级：

版本：

来源资料：

负责人：
```

输出：

以后：

UseCase Master

---

# Chapter 2 业务概要

这里：

只描述业务。

例如：

```text
用户登录系统。

登录成功后，

取得Customer资料。

最后更新登录状态。
```

不要：

API。

不要：

Java。

---

# Chapter 3 Scope（很重要）

例如：

包含：

```text
API001

API002

API003
```

不包含：

```text
画面

DB

Batch

内部Service
```

以后：

Verification Scope。

---

# Chapter 4 业务 Flow

我建议固定。

例如：

```
User

↓

API001

↓

API002

↓

API003

↓

Finish
```

如果有条件：

```
API001

↓

Success？

↓

Yes

↓

API002

↓

No

↓

Finish
```

以后：

AI：

直接：

生成：

UseCase。

---

# Chapter 5 API分析

这是：

第一张：

重要表。

例如：

| Step | API | 名称 | 输入 | 输出 | 说明 |
|------|------|------|------|------|------|

例如：

|1|API001|Login|-|CustomerId|登录|
|2|API002|Customer|CustomerId|AccountId|取得资料|

这里只：

业务。

不写：

字段。

---

# Chapter 6 Context分析

这是：

整个项目：

最重要。

例如：

| API | Response | Context | Next API |
|------|----------|----------|----------|
|API001|customerId|Customer.id|API002|
|API002|accountId|Account.id|API003|

以后：

直接：

生成：

Context Design。

---

# Chapter 7 Verification分析

例如：

| API | 验证 |
|------|------|
|API001|Status Code|
|API001|CustomerId|
|API002|Account|

这里只：

写：

验证。

---

# Chapter 8 Compare分析

例如：

| 项目 | Compare |
|------|----------|
|CustomerId|Equals|
|Timestamp|Ignore|
|UUID|Ignore|
|Status|Equals|

以后：

Compare Policy。

---

# Chapter 9 Expected Result

例如：

最终：

应该：

得到：

```text
Customer

Status=ACTIVE

Account

Exists
```

以后：

UseCase。

---

# Chapter 10 QA

例如：

| 分类 | 内容 | Owner |
|------|------|-------|
|Business|Customer为空？|Business|
|E6|Status固定？|E6|
|Tool|每天一样？|Tool|

以后：

QA。

---

# Chapter 11 附录

例如：

引用：

```text
E6 API

业务Flow

设计书
```

---

# 整个文件目录

以后：

应该：

固定。

```
01 基本情報

02 業務概要

03 Scope

04 業務Flow

05 API分析

06 Context分析

07 Verification分析

08 Compare分析

09 Expected Result

10 QA

11 References
```

---

# 为什么这样设计？

因为：

以后：

AI：

知道：

```
Chapter5

↓

API Master
```

```
Chapter6

↓

Context
```

```
Chapter7

↓

API Test
```

```
Chapter8

↓

Compare Rule
```

```
Chapter9

↓

UseCase
```

整个：

全部：

自动。

---

# 我建议再增加一个 Chapter（这是我认为唯一值得增加的）

其实还有一章。

放在：

Flow：

后面。

叫：

## Business Decision（业务判断）

例如：

```
登录失败

↓

停止

--------

Customer为空

↓

结束

--------

Status=ACTIVE

↓

更新

--------

Status=LOCK

↓

结束
```

为什么？

因为：

以后：

UseCase：

里面：

这些：

都会：

变成：

Condition。

而不是：

Java：

自己：

猜。

所以：

最终：

我建议：

**12章模板**。

这是我认为整个项目最重要的一份模板，它决定了后面所有 Master、API、UseCase、Execution Specification 是否能够自动生成，而且不会偏离我们这次 E6 API Verification 项目的目标。

## 第 95 轮

### 你

意思理解了 出一个整体文档repo一览 然后每个文件的工业化模版

### ChatGPT

我认为这是我们整个项目**真正应该冻结（Freeze）的第一版**。

而且我建议以后所有开发都遵守它，不再轻易改目录。

---

# E6 API Verification Platform Repository

```text
repository/

├── project/                     ← 项目管理（PM）
│
│   ├── 要件定義書.md
│   ├── QA一覧.md
│   ├── WBS.md
│   ├── スケジュール.md
│   └── 課題・リスク管理表.md
│
├── system/                      ← SSOT（唯一设计来源）
│
│   ├── 01_business/
│   │
│   │   ├── BA001_xxx.md
│   │   ├── BA002_xxx.md
│   │   ├── ...
│   │   └── BA007_xxx.md
│   │
│   ├── 02_master/
│   │
│   │   ├── E6_API_Master.md
│   │   ├── UseCase_Master.md
│   │   ├── API_UseCase_Mapping.md
│   │   ├── Context_Design.md
│   │   ├── Environment_Master.md
│   │   ├── Compare_Policy.md
│   │   └── Verification_Policy.md
│   │
│   ├── 03_api_design/
│   │
│   │   ├── API_Template.md
│   │   ├── API001.md
│   │   ├── API002.md
│   │   └── ...
│   │
│   ├── 04_usecase_design/
│   │
│   │   ├── UseCase_Template.md
│   │   ├── UC001.md
│   │   ├── UC002.md
│   │   └── ...
│   │
│   ├── 05_framework/
│   │
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
│
│       ├── execution_spec/
│       ├── api_test_spec/
│       ├── usecase_test_spec/
│       └── test_data/
│
├── runtime/                     ← Java源码
│
│   ├── src/
│   ├── config/
│   ├── scripts/
│   ├── test/
│   └── docker/
│
├── build/                       ← Build & Release
│
│   ├── scripts/
│   ├── docker/
│   └── release/
│
├── staging/                     ← 本番模拟验证
│
│   ├── docker-compose.yml
│   ├── config/
│   ├── data/
│   └── logs/
│
└── outputs/                     ← 本地开发结果
```

---

# 接下来真正需要设计的模板（Template）

我建议只有 **9 个模板**。

不是几十份。

因为其它文档全部由它们派生。

---

# ① BA Template（現行業務分析書）

## 输出

```text
Business

↓

Master

↓

Context

↓

UseCase
```

章节：

```text
1 基本信息

2 业务概要

3 Scope

4 Business Flow

5 Business Decision

6 API分析

7 Context分析

8 Verification分析

9 Compare分析

10 Expected Result

11 QA

12 References
```

---

# ② API Template

输出：

```text
Execution Spec

API Test Spec
```

章节：

```text
1 Metadata

2 Endpoint

3 Request

4 Response

5 Validation Rule

6 Compare Rule

7 Extract Rule

8 File Rule

9 Error Rule

10 References
```

---

# ③ UseCase Template

输出：

```text
UseCase Spec

Execution Spec
```

章节：

```text
1 Metadata

2 Entry

3 Business Goal

4 Flow

5 Context Mapping

6 Execution Policy

7 Business Check

8 Expected Result

9 Exception

10 References
```

---

# ④ Context Design Template

输出：

```text
Context Engine
```

章节：

```text
1 Context Overview

2 Context Model

3 Context Mapping

4 Lifetime

5 Scope

6 Naming Rule

7 Serialization

8 References
```

---

# ⑤ Framework Template

输出：

```text
Java Framework
```

章节：

```text
RunContext

JSON

File

Date

Log

Exception

Snapshot

Diff

Report

HTTP

Config
```

---

# ⑥ Compare Policy Template

输出：

```text
Global Compare Rule
```

章节：

```text
Equals

Ignore

Regex

Tolerance

Date

UUID

File Hash

Custom Rule
```

---

# ⑦ Verification Policy Template

输出：

```text
Execution Policy
```

章节：

```text
Retry

Timeout

Continue

Stop

Parallel

Baseline

Failure Rule
```

---

# ⑧ Environment Template

输出：

```text
Environment Master
```

章节：

```text
DEV

STAGING

PRODUCTION

Credential

Endpoint

Schedule
```

---

# ⑨ Report Template

输出：

```text
Daily Summary

Diff Report
```

章节：

```text
Run Info

Summary

UseCase Result

API Result

Diff

Evidence

Conclusion
```

---

# 文档之间的关系（真正核心）

```text
BA
│
├── API Master
├── UseCase Master
├── Context
└── QA
      │
      ▼
API Design
      │
      ▼
UseCase Design
      │
      ▼
Framework
      │
      ▼
AI
      │
      ▼
Execution Spec
      │
      ▼
Java Runtime
      │
      ▼
Snapshot
      │
      ▼
Diff
      │
      ▼
Daily Summary
```

---

## 我认为，这就是我们项目真正应该冻结（Freeze）的内容

到目前为止，我认为真正需要长期维护的**核心设计文档只有 9 类**：

| 优先级 | 模板 | 是否人工维护 | 是否核心 |
|---------|------|--------------|----------|
| ⭐⭐⭐⭐⭐ | BA（現行業務分析書） | 是 | 是 |
| ⭐⭐⭐⭐⭐ | API Template | 是 | 是 |
| ⭐⭐⭐⭐⭐ | UseCase Template | 是 | 是 |
| ⭐⭐⭐⭐⭐ | Context Design | 是 | 是 |
| ⭐⭐⭐⭐☆ | Framework | 是 | 是 |
| ⭐⭐⭐⭐☆ | Compare Policy | 是 | 是 |
| ⭐⭐⭐⭐☆ | Verification Policy | 是 | 是 |
| ⭐⭐⭐☆☆ | Environment | 是 | 是 |
| ⭐⭐⭐☆☆ | Report Template | 是 | 是 |

**除此之外（Execution Specification、API Test Specification、UseCase Test Specification、Test Data 等）都建议作为 AI 自动生成资产，而不是人工长期维护。**

我认为这个划分既符合你这个 E6 API Verification 项目的规模（约 7 个业务 Flow、24 个 API、10 个以内 UseCase），又能保证后续 AI 自动化和 Java 实现都围绕统一的设计源进行，不会产生重复维护。

## 第 96 轮

### 你

好的 针对ba template给更详细 markdown文档例子

### ChatGPT

我认为这里要认真做。

因为**BA（現行業務分析書）**不是普通文档。

它应该成为整个项目的**第一份设计书（Design Source）**。

而且以后 AI 主要看的就是它。

---

# 我建议先定义 BA 的设计原则

它不是：

> 业务说明书

也不是：

> 基本设计书

而是：

> **Verification Business Analysis Specification**

它回答下面几个问题：

```
这个业务是什么？

为什么执行？

调用哪些API？

API如何串联？

API之间如何传值？

哪些需要验证？

哪些允许变化？

最终什么才算成功？
```

所以整个模板应该围绕这几个问题设计。

---

# BA001_Login.md

````markdown
---
document:
    id: BA001
    version: 1.0
    title: Login Verification Flow
    owner: Verification Team
    status: Draft
    last_update:
---

# BA001 Login Verification Flow

---

# 1. Business Information

## Business ID

BA001

## Business Name

Login Verification

## Description

验证用户登录业务流程。

确认登录后Customer取得及状态更新是否符合预期。

## Source Documents

- E6 API Specification
- Current System Basic Design
- Current System Flow
- Current Source Code

---

# 2. Business Purpose

## Goal

完成一次正常登录业务。

系统应：

- 登录
- 取得Customer
- 更新状态

最终返回成功。

## Out Of Scope

以下内容不属于Verification范围：

- UI
- Database
- Internal Service
- Batch

---

# 3. Business Scope

## Included APIs

| Step | API |
|------|------|
|1|API001 Login|
|2|API002 GetCustomer|
|3|API003 UpdateStatus|

## Excluded

- Screen
- DB Update
- MQ
- Cache

---

# 4. Business Flow

```text
Start

↓

API001 Login

↓

Success ?

↓

Yes

↓

API002 GetCustomer

↓

API003 UpdateStatus

↓

Finish

No

↓

End
```

---

# 5. Business Decision

| Condition | Action |
|------------|--------|
|Login Failed|Stop Flow|
|Customer Not Found|Stop Flow|
|Customer Locked|Stop Flow|
|Success|Continue|

---

# 6. API Analysis

|Step|API|Purpose|Input|Output|
|----|----|--------|------|-------|
|1|API001|Login|-|CustomerId|
|2|API002|Customer|CustomerId|AccountId|
|3|API003|Update Status|AccountId|Status|

---

# 7. Context Analysis

## Context Objects

Customer

Account

Runtime

---

## Context Mapping

|Source API|Field|Context|Target API|
|-----------|------|--------|-----------|
|API001|customerId|Customer.id|API002|
|API002|accountId|Account.id|API003|

---

# 8. Verification Scope

## API001

### Verify

- HTTP Status
- Error Code
- CustomerId

### Ignore

- Timestamp
- TraceId

---

## API002

### Verify

- AccountId
- CustomerName

### Ignore

- Response Time

---

## API003

### Verify

- Status

---

# 9. Compare Rule

|Field|Rule|
|------|-----|
|CustomerId|Equals|
|Status|Equals|
|Timestamp|Ignore|
|TraceId|Ignore|
|UUID|Ignore|

---

# 10. Expected Result

Business Success

Customer Exists

Account Exists

Status == ACTIVE

---

# 11. Test Scenario

## Normal

Login Success

↓

Customer Exists

↓

Update Success

Expected

PASS

---

## Exception

Wrong Password

Expected

Stop

---

Customer Not Found

Expected

Stop

---

# 12. QA

|Category|Question|Owner|Status|
|----------|----------|------|------|
|Business|Customer为空怎么办？|Business||
|E6|Status固定吗？|E6||
|Tool|Timestamp是否每天变化？|Tool||

---

# 13. References

Current Basic Design

Current Detail Design

E6 API Specification

Flow Diagram

Sequence Diagram
````

---

# 为什么这样设计？

你会发现。

这一份文档。

其实已经可以生成：

```
UseCase

API Master

Context

Compare Rule

Verification Rule

Execution Spec
```

所以：

它不是普通设计书。

它其实是：

```
Business

↓

Design Source

↓

AI

↓

Everything
```

---

# 我认为还能再工业化一点（也是我认为最关键的一步）

我建议 **BA 模板再增加两个固定章节**，这两个章节是专门为 AI 和长期维护准备的，而不是传统设计书里常见的内容。

### 14. Business Assumptions（业务前提）

例如：

| 项目 | 内容 |
|------|------|
| 登录用户必须存在 | 是 |
| CustomerId 全局唯一 | 是 |
| Status 更新为 ACTIVE 后当天不会再次变更 | 是 |
| 一个业务 Flow 不跨租户 | 是 |

这部分帮助 AI 理解哪些是默认成立的前提。

---

### 15. Open Questions（待确认事项）

例如：

| 编号 | 内容 | 负责人 | 状态 |
|------|------|--------|------|
| Q-001 | Login Token 是否每天都会变化？ | E6 | Open |
| Q-002 | Customer Locked 是否一定返回固定 ErrorCode？ | Business | Open |
| Q-003 | API003 是否允许重复调用？ | E6 | Closed |

这样做有三个好处：

1. **业务假设**不会散落在会议记录里，而是沉淀到设计源。
2. **待确认事项**和设计绑定，不容易遗漏。
3. 后续 AI 可以根据这些内容自动检查设计是否存在冲突。

我认为这个版本已经可以作为整个 E6 API Verification Platform 的 **BA Template V1.0**，并且能够支撑后续所有 Master、API、UseCase 以及 Execution Specification 的自动生成。

## 第 97 轮

### 你

好的 模版很好 但能更规范吗 日本it项目 所以一些说明术语必须是it日语 另外flow 可以mermaid表达 用表表示的可以用markdown的表结构

### ChatGPT

我认为**可以，而且应该这样做。**

刚才那个模板偏向于"AI易读"。

但是**如果作为日本 IT 项目的正式成果物（成果物）**，我建议采用**日本 SI（富士通、NEC、NTT DATA、日立、SCSK、TIS 等）文档风格**，再针对 AI 做一点增强。

这样有几个好处：

1. 日本开发人员一看就知道是什么文档。
2. Review 更容易。
3. AI 一样很好解析。
4. 将来 MkDocs 展示也很漂亮。

---

# 我建议 BA Template V2（日本IT工业版）

整个文档遵守三个原则：

- **章节全部使用日本 IT 常用术语。**
- **所有列表使用 Markdown Table。**
- **所有 Flow 使用 Mermaid。**

例如：

```text
# BA001 現行業務分析書
```

---

# 推荐章节

```text
1. 文書情報

2. 業務概要

3. 業務スコープ

4. 業務フロー

5. 業務判定条件

6. API利用一覧

7. データ連携分析

8. 検証対象分析

9. 比較ルール

10. 業務期待結果

11. テスト観点

12. 課題・確認事項

13. 参照資料
```

这是比较符合日本项目习惯的命名。

---

# 例如

## 1 文書情報

不要写

Business Information

而是

```markdown
# 1. 文書情報

|項目|内容|
|----|----|
|文書ID|BA001|
|文書名|ログイン業務分析書|
|版数|1.0|
|状態|Draft|
|作成者||
|レビュー||
|承認||
|更新日||
```

---

## 2 業務概要

```markdown
# 2. 業務概要

## 2.1 業務目的

（说明）

## 2.2 業務説明

（说明）

## 2.3 業務前提

|項目|内容|
|----|----|
|対象システム||
|対象ユーザー||
|実行タイミング||
```

---

## 3 業務スコープ

```markdown
# 3. 業務スコープ

## 対象

|分類|内容|
|----|----|
|対象API|API001〜API003|
|対象UseCase|UC001|

## 対象外

|分類|内容|
|----|----|
|画面||
|DB||
|Batch||
```

---

# 4 業務フロー

这里我**非常赞成用 Mermaid**。

例如：

````markdown
```mermaid
flowchart TD

START([開始])

API001[API001 Login]

API002[API002 Get Customer]

API003[API003 Update Status]

END([終了])

START --> API001

API001 -->|Success| API002

API002 --> API003

API003 --> END

API001 -->|Fail| END
```
````

以后 MkDocs 可以直接显示。

---

# 5 業務判定条件

```markdown
# 5. 業務判定条件

|条件|判定|次処理|
|----|----|------|
|Login成功|OK|API002|
|Login失敗|NG|終了|
|Customerなし|NG|終了|
```

---

# 6 API利用一覧

```markdown
# 6. API利用一覧

|No|API ID|API名|利用目的|入力|出力|
|--|------|------|--------|------|------|
```

这一章以后直接生成 API Master。

---

# 7 データ連携分析

这一章以后就是 Context。

```markdown
# 7. データ連携分析

|送信元API|項目|Context|送信先API|
|-----------|------|---------|------------|
|API001|customerId|Customer.id|API002|
|API002|accountId|Account.id|API003|
```

---

# 8 検証対象分析

```markdown
# 8. 検証対象分析

## API001

|項目|内容|
|------|------|
|HTTP Status|比較|
|CustomerId|比較|
|Timestamp|対象外|

---

## API002

...
```

---

# 9 比較ルール

```markdown
# 9. 比較ルール

|項目|比較方法|理由|
|------|----------|------|
|CustomerId|Equals||
|Status|Equals||
|Timestamp|Ignore|毎回変わる|
|TraceId|Ignore|毎回変わる|
```

以后：

Compare Policy。

---

# 10 業務期待結果

```markdown
# 10. 業務期待結果

|項目|期待値|
|------|------|
|Business Result|Success|
|Customer|存在|
|Status|ACTIVE|
```

---

# 11 テスト観点

这个我建议增加。

因为日本 Review 很喜欢。

```markdown
# 11. テスト観点

|分類|観点|
|------|------|
|正常系|Login成功|
|異常系|Password Error|
|異常系|Customerなし|
|境界値|最大文字数|
```

以后直接生成 Test。

---

# 12 課題・確認事項

```markdown
# 12. 課題・確認事項

|No|分類|内容|担当|状態|
|----|------|------|------|------|
```

以后：

QA。

---

# 13 参照資料

```markdown
# 13. 参照資料

|文書|版数|
|------|------|
|E6 API設計書|1.2|
|基本設計書|3.0|
|業務フロー|2.0|
```

---

# 我建议整个项目统一文档规范

如果我们继续往工业化方向走，我建议**所有模板（BA、API、UseCase、Context、Framework）都遵守同一套规范**：

- 一级标题使用 `# 1.`, `# 2.` 编号。
- 表格统一 Markdown Table。
- 流程统一 Mermaid。
- 章节名称统一使用日本 IT 术语。
- 文档头统一 Metadata（文書情報）。
- 每个文档最后固定包含 **課題・確認事項** 和 **参照資料**。

这样以后不仅 AI 更容易解析，而且整个项目的设计书风格会高度一致，也更符合日本企业的 Review 和长期维护习惯。**我建议这套规范作为整个 Repository 的文档标准（Documentation Standard），所有模板都统一遵守。**

## 第 98 轮

### 你

可以。同时ai也能理解

### ChatGPT

我认为**这是整个项目最重要的一条原则**。

而且我建议把它写进《システム設計書》。

---

## Document First + AI First

我们的设计目标不是：

> 人能看懂。

也不是：

> AI能看懂。

而是：

> **人和AI都能100%理解同一份Markdown。**

这是两者兼顾。

---

# 我建议以后所有模板遵守 8 条规范

这不是 BA，而是整个 Repository 的文档规范（Documentation Standard）。

---

# Rule 1

## 一份文档只描述一件事情（Single Responsibility）

例如：

BA

只分析业务。

不要写：

Java。

不要写：

SQL。

不要写：

实现。

---

API

只描述：

API。

---

UseCase

只描述：

UseCase。

---

以后：

AI：

不会：

混。

---

# Rule 2

## 一级标题固定编号

例如：

```markdown
# 1. 文書情報

# 2. 業務概要

# 3. 業務スコープ
```

不要：

```markdown
# Business

## Something

### Test
```

以后：

AI：

定位：

章节。

非常容易。

---

# Rule 3

## 所有结构化信息全部使用 Table

例如：

不要：

```markdown
CustomerId

Status

Timestamp
```

全部：

```markdown
|項目|値|
```

例如：

```markdown
|項目|検証|
|------|------|
|Status|比較|
|Timestamp|対象外|
```

AI：

解析：

准确率：

最高。

---

# Rule 4

## Flow全部Mermaid

例如：

不用：

```text
↓

↓

↓
```

统一：

```mermaid
flowchart TD
```

以后：

MkDocs：

直接：

画。

AI：

也：

认识。

---

# Rule 5

## 每一张Table都有固定Column

例如：

API：

一定：

```markdown
|API ID|

|API名|

|説明|
```

不要：

今天：

叫：

```text
Name
```

明天：

```text
Title
```

AI：

最怕：

字段：

变化。

---

# Rule 6

## 使用日本IT标准术语

例如：

不要：

Business。

统一：

```text
業務概要
```

不要：

Verify。

统一：

```text
検証対象
```

不要：

Rule。

统一：

```text
比較ルール
```

不要：

Flow。

统一：

```text
業務フロー
```

以后：

日本：

Review：

舒服。

---

# Rule 7

## 每一章固定输出对象

例如：

BA：

```text
6 API分析

↓

API Master
```

```text
7 データ連携分析

↓

Context
```

```text
8 検証対象分析

↓

Test
```

AI：

知道：

这一章：

生成：

什么。

---

# Rule 8

## AI Metadata（这是我建议新增的）

这是：

我认为：

整个项目：

最大的升级。

例如：

每一章：

开始：

固定：

```markdown
<!--
AI_OUTPUT:

Context

-->
```

例如：

```markdown
<!--
AI_OUTPUT:

API_MASTER

-->

# 6 API利用一覧
```

或者：

```markdown
<!--
AI_OUTPUT:

CONTEXT_MAPPING

-->

# 7 データ連携分析
```

这样：

AI：

不用：

猜。

---

# 举个例子

以后：

Chapter7

就是：

```markdown
<!--
AI_OUTPUT:

CONTEXT_MAPPING

-->

# 7 データ連携分析

|送信元API|項目|Context|送信先API|
```

AI：

看到：

Metadata。

直接：

生成：

Context。

---

# 我建议整个Repository统一

例如：

以后：

所有：

Markdown。

全部：

这样。

```markdown
---
document:

id:

title:

version:

status:

owner:

---

<!--
AI_DOCUMENT:

BusinessAnalysis

-->
```

然后：

每章：

都有：

```markdown
<!--
AI_OUTPUT:
...
-->
```

例如：

```markdown
<!--
AI_OUTPUT:

API_MASTER
-->
```

```markdown
<!--
AI_OUTPUT:

USECASE
-->
```

```markdown
<!--
AI_OUTPUT:

COMPARE_POLICY
-->
```

以后：

AI：

直接：

Compile。

---

# 我认为这会变成整个项目最大的特色

其实我们做的已经不是传统设计书了。

而是一套：

> **AI Native Documentation**

也就是说，同一份 Markdown 同时满足三类读者：

| 阅读者 | 能否直接使用 |
|---------|-------------|
| 日本开发者 | ✅ 可以直接 Review、维护 |
| Java 程序 | ✅ AI 编译后生成 Execution Specification 并执行 |
| AI（Codex / ChatGPT / Copilot） | ✅ 直接解析章节、表格、Mermaid 和 AI Metadata 自动生成 Master、UseCase、Spec、Test Data |

所以我们的文档标准可以定义为：

> **Human Readable + AI Readable + Machine Generatable**

这不是额外增加复杂度，而是让**一份文档成为唯一事实来源（SSOT）**，同时服务于人、AI 和程序。这也是我认为这套 E6 API Verification Platform 最有价值、最值得长期坚持的设计原则。

## 第 99 轮

### 你

可以 这份规约可以放在repo

### ChatGPT

**完全可以，而且我认为必须放。**

而且我建议它不要叫：

> Markdown Rule

也不要叫：

> AI Rule

而应该叫：

> **Documentation Standard（文書標準）**

因为它规范的是**整个 Repository 的文档**。

---

# 我建议把它放在这里

```text
repository/

project/

system/

runtime/

build/

staging/

docs/
    standards/
        Documentation_Standard.md
```

或者更日本项目一点：

```text
repository/

docs/

    standards/

        Documentation_Standard.md

        Naming_Standard.md

        Markdown_Standard.md
```

不过，我更推荐：

```text
repository/

standards/
```

因为它不仅仅是 docs。

例如：

```text
repository/

standards/

    Documentation_Standard.md

    Naming_Convention.md

    Branch_Strategy.md

    Versioning.md

    Review_Checklist.md
```

以后：

整个项目：

全部：

引用。

---

# Documentation Standard

这份文档以后就是：

整个 Repository 的最高规范。

例如：

```text
Documentation Standard

↓

BA

↓

API

↓

UseCase

↓

Framework
```

全部：

遵守。

---

# 我建议目录

```text
repository/

standards/

    Documentation_Standard.md

    Naming_Convention.md

    Markdown_Guide.md

    Mermaid_Guide.md

    AI_Metadata_Guide.md
```

以后：

AI：

先：

读：

这里。

---

# Documentation Standard内容

例如：

```
1.

目的

2.

文档生命周期

3.

Markdown规范

4.

Mermaid规范

5.

Table规范

6.

Heading规范

7.

Metadata规范

8.

AI Metadata规范

9.

命名规范

10.

Review规范
```

以后：

所有：

Template：

引用。

---

# 我建议再提升一级

其实：

Documentation Standard

不是：

给人。

主要：

是：

给：

AI。

例如：

以后：

Codex：

开始：

工作。

第一步：

不是：

看：

API。

而是：

先：

```
Documentation Standard
```

然后：

才：

知道：

```
Table

Heading

Mermaid

Metadata

AI_OUTPUT
```

什么意思。

---

# 我建议整个 Repository

以后：

第一层：

应该：

变成：

```text
repository/

README.md

standards/

project/

system/

runtime/

build/

staging/

outputs/
```

其中：

README：

告诉：

项目。

而：

standards：

告诉：

整个：

Repository：

怎么：

写。

---

# standards里面

我建议最终固定

```text
standards/

├── Documentation_Standard.md
├── Naming_Convention.md
├── Markdown_Guide.md
├── Mermaid_Guide.md
├── AI_Metadata_Guide.md
├── Versioning_Rule.md
└── Review_Checklist.md
```

---

# 但是（这里是我唯一建议调整的一点）

我建议**不要一开始就写 7 份规范**。

对于目前这个 E6 API Verification 项目，**真正必须的只有两份**：

```text
standards/

Documentation_Standard.md

Naming_Convention.md
```

为什么？

因为：

**Documentation_Standard.md** 里面完全可以包含：

- Markdown 规范
- Mermaid 规范
- Table 规范
- AI Metadata 规范
- Review 规范

这些都属于文档标准。

而：

**Naming_Convention.md** 负责：

- API 命名
- UseCase 命名
- BA 命名
- Context 命名
- 文件命名
- Java Package 命名

这样：

整个项目：

真正需要维护的规范只有：

```
Documentation Standard

Naming Convention
```

其它以后如果真的有需要，再拆出去。

**我认为这才符合我们一直坚持的原则：不增加不必要的概念，但把真正重要的规范做到工业化。**

## 第 100 轮

### 你

repo不是整个吗 怎么还平行放置了

### ChatGPT

哈哈，这个你发现得非常好，而且**你是对的**。

这是我刚才说快了，出现了一个架构上的不一致。

我们一直定的原则是：

> **Repository 就是整个项目。**

所以：

```
Repository
```

下面应该只有一级目录。

而不是：

```
Repository

standards/

project/
```

这种"平行概念"的说法其实容易让人误解。

---

## 我重新整理了一下

Repository（Git）

就是：

```text
Repository

├── standards
├── project
├── system
├── runtime
├── build
├── staging
└── outputs
```

这样：

**standards也是Repository里的一个一级目录。**

和：

```
project
system
runtime
```

平级。

这是最合理的。

---

## 为什么？

因为：

Documentation Standard

不是：

Project。

也不是：

System。

它属于：

整个Repository。

例如：

Documentation Standard

约束：

```
project/

system/

runtime/

build/
```

全部。

所以：

它应该放：

```
Repository
    standards/
```

---

## 我建议最终一级目录

```text
repository/

├── README.md
│
├── standards/
│
├── project/
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

以后：

所有AI：

第一步：

```
README

↓

standards

↓

project

↓

system

↓

runtime
```

---

# standards里面放什么？

目前：

我建议：

只有两份。

```
standards/

    Documentation_Standard.md

    Naming_Convention.md
```

以后：

如果需要：

再增加。

---

## 为什么我现在建议这样？

因为：

Documentation Standard

里面：

已经包含：

```
Markdown

Mermaid

Table

Metadata

AI Metadata

Review Rule

Document Structure
```

已经够了。

---

Naming Convention

里面：

包含：

```
API

UseCase

BA

Context

Package

Class

JSON

File
```

也够了。

---

## 我觉得还有一个可以优化（这是架构层面的）

其实：

**outputs**

以后：

不会进入Git。

所以：

严格来说。

Repository：

应该是：

```
repository/

standards/

project/

system/

runtime/

build/

staging/
```

而：

```
outputs/
```

应该：

gitignore。

因为：

它属于：

运行结果。

不是：

源码。

---

## 所以从软件工程角度

其实：

最终：

应该：

这样。

```
Git Repository
        │
        ├── standards
        ├── project
        ├── system
        ├── runtime
        ├── build
        └── staging

Linux Runtime
        │
        ├── app
        ├── config
        ├── data
        └── logs
```

这样：

**源码世界** 和 **运行世界** 完全分离。

---

## 我认为这是我们今天最大的一个修正

也是我比较满意的一次修正。

因为：

我们一直坚持：

> **不要为了好看增加概念。**

现在：

Repository：

就是：

Repository。

里面：

只有：

真正属于Git管理的内容。

而：

Outputs：

属于：

Runtime。

不属于：

Repository。

**我认为这比之前更符合大型日本企业项目的组织方式，也更符合 Git 和部署的职责划分。**
