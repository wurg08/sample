# 新的开始

- 来源: https://chatgpt.com/g/g-p-6a5f4d3570688191a63c36d8624e43cc/c/6a5f4d4f-70a4-83ee-bd47-94f6ea917670
- 导出时间: 2026-07-21T21:29:35+09:00
- 分片: 1/1
- 总消息数: 26
- 总轮数: 10

## 第 1 轮

### 你

new

### ChatGPT

好的，我们从一个全新的内容开始。请直接告诉我这次要做什么。

## 第 2 轮

### 你

这个peoject的情报源里的6个md文件 告诉我名字 并且里面我们的对话内容全部理解一遍

### ChatGPT

可以，而且我已经把这 6 个文件的内容进行了整体理解。

这 6 个 md 文件实际上就是我们之前 **《API流程验证设计》** 那个超长对话（551条消息，254轮）拆分出来的完整上下文。fileciteturn1file15fileciteturn0file4fileciteturn0file3

### 6 个文件名称

1. **part-001.md** fileciteturn1file15
2. **part-002.md**
3. **part-003.md** fileciteturn1file1
4. **part-004.md** fileciteturn1file2
5. **part-005.md** fileciteturn1file0
6. **part-006.md** fileciteturn0file5

---

## 我已经理解的内容（整体）

它们并不是 6 个独立主题，而是一套完整设计的连续讨论。

目前我已经能够把它们当成一个整体来看，而不是单独几个文件。

整个内容大概可以归纳成下面几个阶段。

---

### 第一阶段：项目定位

主要讨论：

- 为什么做 E6 API Verification Platform
- 日本 SI 项目的开发方式
- Tool 与业务系统的职责划分
- Verification 的真正目标
- 与业务 Team、E6 Team 的责任边界
- Capability Catalog 思想
- Verification Policy 思想

例如 part-001 中大量讨论了：

- 成果物规划
- Capability Catalog
- Verification Policy
- UseCase
- Framework
- Test Strategy
- Operation 等。fileciteturn1file19fileciteturn1file17

---

### 第二阶段：Repository 与设计资产

主要讨论：

- Repository 如何组织
- system/
- runtime/
- outputs/
- build/
- staging/
- master/
- framework/
- api/
- usecase/

后来逐渐冻结成：

Documentation First

AI Native

Markdown First

SSOT（Single Source of Truth）

---

### 第三阶段：Design Kit 思想

这是后面很重要的一部分。

我们提出：

不是 Template。

而是：

Design Kit

每个 Kit 包含：

- README
- Template
- Guide
- Checklist
- Example

例如：

Business Analysis Design Kit

API Design Kit

UseCase Design Kit

Context Design Kit

Framework Design Kit

还提出：

JEADS

Japanese Enterprise AI Documentation Standard。fileciteturn0file4

---

### 第四阶段：Business Analysis（BA）

讨论了：

如何把

现行业务分析

做到工业级。

包括：

- Business Flow
- Data Flow
- Context
- API
- Verification
- Compare
- Expected Result
- QA
- Traceability

后来 Example 已经开始成型。

例如：

Customer 查询

Business Flow

Verification Matrix

Expected Result

Evidence

Traceability

等。fileciteturn1file10fileciteturn1file4

---

### 第五阶段：UseCase Design

后来开始固定：

一个 UseCase 应包含：

- Entry Input
- Context
- Main Flow
- Scenario
- Business Check
- Evidence
- Traceability

并且已经形成 Example。fileciteturn1file5fileciteturn1file2

---

### 第六阶段：Context Master

后来把 Context 做成真正 Master。

包括：

- Producer
- Consumer
- Lifetime
- Snapshot
- Binding
- Scenario Selection
- Skip Rule
- Runtime Context

甚至 Runtime Read Flow

Runtime Write Flow

Security Validation

Production Validation

全部已经设计。fileciteturn1file12fileciteturn1file13fileciteturn1file8

---

### 第七阶段：Compare Policy

后来 Compare Policy 已经扩展到企业级。

包括：

- Normalize
- Ignore
- Collection Compare
- Baseline
- Security Validation
- Production Validation
- Error Code

已经不是简单 Ignore Rule。

而是完整 Compare Framework。fileciteturn1file11fileciteturn1file9

---

### 第八阶段：Verification Policy

后来又独立出：

Verification Policy Master

里面包括：

- Validation Rule
- Production Validation
- Security Validation
- Error Code

比 Compare Policy 更高一层。

定义：

哪些验证必须执行。

哪些 Severity。

哪些 Runtime 可以 Override。

哪些 Production 禁止。fileciteturn1file7

---

### 第九阶段：Runtime

后面开始真正进入 Runtime。

包括：

- Bootstrap
- Loader
- Planner
- Runner
- ApiExecutor
- Validator
- Snapshot
- Diff
- Report

甚至 Java Package

Interface

Thread Safety

Recovery

全部已经讨论。fileciteturn0file3

---

### 第十阶段：Master

最后进入：

system/02_master/

开始设计真正工业级 Master。

已经讨论很多：

例如：

- Version
- Governance
- Cache
- Lifecycle
- Scheduling
- Import
- Export
- Synchronization

最后一个文件已经做到：

Import / Export / Synchronization

超过两百多个章节。fileciteturn0file5

---

# 我的理解程度

我现在不是只知道这些文件"讲了什么"。

而是已经建立了整个设计体系。

也就是说，我已经能够把这些内容串起来理解：

```text
Business Analysis
        ↓
API Design
        ↓
UseCase Design
        ↓
Context Master
        ↓
Compare Policy
        ↓
Verification Policy
        ↓
Master
        ↓
Runtime
        ↓
Snapshot
        ↓
Diff
        ↓
Report
```

整个体系在我这里已经形成了一套连续的设计思路。

## 接下来

以后我们继续这个项目时，我会默认以这 **6 个 md 文件**作为当前项目的知识基础，不需要再重新解释前面的设计思路，可以直接在此基础上继续推进新的设计或完善已有内容。

## 第 3 轮

### 你

我发现写完 compare_policy_master設計書.md文件之后 然后写了一堆不是design里冻结的设计书

### ChatGPT

是的，我也发现了，而且你说的是对的。

我重新梳理了导出的对话，时间线实际上是这样的：

### 第一阶段（这是我们冻结的设计）
我们一直在完善 `system/02_master/design/`。

一直到：

```text
Compare_Policy_Master設計書.md
```

完成。fileciteturn1file0L1-L30

当时的流程实际上是：

```text
Business Master
↓

Environment Master

↓

API Master

↓

UseCase Master

↓

Scenario Master

↓

Context Master

↓

Verification Master

↓

Verification Policy Master

↓

Compare Policy Master   ← 到这里
```

这一段属于 **02_master 的正式 Design**。

---

## 第二阶段

但是 Compare Policy 写完以后，我们聊天的方向变了。

开始不断扩充例如：

```
Report設計書
Snapshot設計書
ExecutionSpecスキーマ設計書
Master Migration
Master Loader
Backup
Import/Export
Synchronization
Release
Rollback
...
```

例如：

```
system/05_framework/Report設計書.md
```

就是那时候开始写的。fileciteturn1file1L1-L35

还有：

```
Snapshot設計書.md
```

fileciteturn1file7L1-L32

以及：

```
ExecutionSpecスキーマ設計書.md
```

fileciteturn1file3L1-L35

---

## 第三阶段（越来越偏）

后来又开始继续无限扩展：

例如

```
Master Migration
Master Version
Backup
Recovery
Security
Scheduling
Notification
```

这些其实已经不是我们当初冻结目录里的内容，而是**工业化平台扩展设计**。从导出的内容可以看到，后面已经进入 Backup、Import/Export、Synchronization 等大量主题。fileciteturn1file17L1-L40 fileciteturn1file15L1-L40

---

# 所以实际上应该分成两部分

## A. 冻结设计（真正的 Repository）

也就是：

```
system/
└──02_master/
    ├──README
    ├──design/
    │
    ├──Business_Master設計書
    ├──Environment_Master設計書
    ├──API_Master設計書
    ├──UseCase_Master設計書
    ├──Scenario_Master設計書
    ├──Context_Master設計書
    ├──Verification_Master設計書
    ├──Verification_Policy_Master設計書
    └──Compare_Policy_Master設計書
```

**这部分才属于冻结的 Repository Design。**

---

## B. 后续扩展设计

例如：

```
Framework

Runtime

ExecutionSpec

Snapshot

Diff

Report

Import

Export

Migration

Backup

Recovery

...
```

这些其实属于：

```
system/05_framework/

runtime/

system/runtime/

```

甚至有一些已经属于未来版本。

---

# 我建议我们现在这样做

以后我们把整个工程严格分成两个阶段。

### 第一阶段（必须完成）

**把冻结 Repository 全部补齐。**

例如：

```
system/02_master/design/
```

里面所有设计书。

一份不少。

做到 Review Ready。

---

### 第二阶段（再继续）

再开始：

```
system/05_framework/
runtime/
execution/
report/
```

这样不会再出现：

> Master 还没全部完成，却跑去写 Runtime。

---

我建议把目前已有内容重新整理成两张清单：

1. **冻结版 Repository（必须完成）**——这是我们的主线。
2. **后续扩展设计（Industrial Extension）**——把 Compare Policy 之后那些设计书全部归档到这里，不再和主线混在一起。

这样整个项目会重新回到我们最初规划的节奏，也方便继续完成剩余的设计。

## 第 4 轮

### 你

是的 所以我想的是先补完vertification_policy_master.md文件 然后02_master文件夹下的其他的design template等文件 之后再进入其他

### ChatGPT

我完全赞成，而且我认为这才是正确的开发顺序。

实际上，我们之前最大的偏离就是**Repository 本身还没有封板，就开始设计 Runtime 和 Framework**。对于工业化项目来说，这样后续很容易反复修改。

我建议现在正式冻结开发顺序，以后就严格按这个顺序推进，不再跳跃。

---

# Phase 1：完成 Repository（冻结）

目标：

> **把 `system/02_master` 做成可以独立交付的工业级 Repository。**

完成之前，不进入 Runtime。

---

## Step 1：补完遗漏

目前真正缺的就是：

```
system/
└──02_master/
    ├──README.md
    ├──Repository_Structure.md
    │
    ├──design/
    │    ...
    │
    └──Verification_Policy_Master設計書.md   ← 补完
```

这是目前最大的缺口。

---

## Step 2：检查 design 是否全部完成

例如：

```
design/

Business_Master設計書.md

Environment_Master設計書.md

API_Master設計書.md

UseCase_Master設計書.md

Scenario_Master設計書.md

Context_Master設計書.md

Verification_Master設計書.md

Verification_Policy_Master設計書.md

Compare_Policy_Master設計書.md
```

这一层全部完成。

全部达到：

```
Review Ready
```

---

## Step 3：不是 design，而是 Repository 自己需要的文件

也就是：

```
02_master/

README.md

Repository_Structure.md

CHANGELOG.md

VERSION.md

Glossary.md

Naming_Convention.md

Coding_Rule.md

Directory_Rule.md

Master_Overview.md
```

这些不是设计书。

而是 Repository 的规范文件。

---

## Step 4：Template

例如：

```
template/

Business_Master_Template.md

API_Master_Template.md

Scenario_Template.md

Context_Template.md

Verification_Template.md

Compare_Template.md

...
```

这些全部补齐。

---

## Step 5：Example

```
example/

Business/

API/

Scenario/

Context/

Verification/

Compare/
```

真正的样例。

---

## Step 6：Checklist

```
checklist/

Review_Checklist.md

Quality_Checklist.md

Release_Checklist.md
```

---

## Step 7：Guide

```
guide/

How_to_Add_API.md

How_to_Add_Scenario.md

How_to_Update_Master.md

Review_Guide.md
```

---

# 到这里

Repository 才真正结束。

也就是说：

```
system/
└──02_master/
```

已经可以独立发布。

---

# 然后才进入下一阶段

## Phase 2

```
03_api_design
```

---

## Phase 3

```
04_usecase_design
```

---

## Phase 4

```
05_framework
```

这里才开始：

```
Snapshot

Diff

Report

Execution

Runtime

...
```

---

# 我建议我们以后遵守一个原则

以后我每次开始写任何文件之前，都先给出当前进度，例如：

```
system/
└──02_master/

README.md                  ✅ 已完成
Repository_Structure.md    ✅ 已完成

design/
├── Business_Master                 ✅
├── Environment_Master              ✅
├── API_Master                      ✅
├── UseCase_Master                  ✅
├── Scenario_Master                 ✅
├── Context_Master                  ✅
├── Verification_Master             ✅
├── Verification_Policy_Master      ⏳ 下一份
└── Compare_Policy_Master           ✅

template/               ⏳ 未开始
example/                ⏳ 未开始
guide/                  ⏳ 未开始
checklist/              ⏳ 未开始
```

然后**严格只在 `02_master` 范围内推进**，直到整个目录完全封板（Frozen）。

我建议把这作为后续工作的固定规则：**`02_master` 不完成，不进入 `03_api_design`、`04_usecase_design` 和 `05_framework`。**这样整个仓库的基础会非常扎实，后续所有设计都能建立在稳定的 Master Repository 之上。

## 第 5 轮

### 你

你按照整个repo目录和文件 来总结下已经完成和未完成的文件

### ChatGPT

我重新对照了我们导出的对话，我建议**不要按照后来不断扩展后的版本统计**，而是按照**最终冻结的 Repo Structure**统计，这样以后才不会混乱。

我们就以这版作为基准（也是我建议以后一直使用的版本）：

```text
repository/
├── project/
├── system/
│   ├──00_repository/
│   ├──01_business/
│   ├──02_master/
│   ├──03_api_design/
│   ├──04_usecase_design/
│   ├──05_framework/
│   └──06_verification_assets/
├──runtime/
├──build/
├──staging/
└──outputs/
```

这是我们冻结过的目录结构。fileciteturn2file6L1-L36

---

# 当前完成状态（我建议作为以后唯一统计口径）

|目录|状态|
|------|------|
|project|🟡 基本规划，未系统编写|
|00_repository|🟡 讨论较多，未整理完成|
|01_business|🟡 模板与结构完成，业务实例未完成|
|02_master|🟡 正在完成（当前重点）|
|03_api_design|⚪ 未开始|
|04_usecase_design|⚪ 未开始|
|05_framework|⚠️ **设计写了很多，但建议暂时冻结不用继续**|
|06_verification_assets|⚪ 未开始|
|runtime|⚠️ 写过很多设计，但建议以后再继续|
|build|⚪ 未开始|
|staging|⚪ 未开始|
|outputs|无需编写|

---

# 00_repository

## 已完成（讨论完成）

- Repository结构
- Documentation Standard
- Traceability Rule
- Naming Convention
- Review Checklist
- Glossary
- Repository Philosophy

这些都讨论过，而且还有完整内容。fileciteturn2file2L1-L35

---

## 未整理

真正应该存在：

```text
00_repository/

README.md

Repository_Structure.md

Document_Style_Guide.md

Traceability_Rule.md

Naming_Convention.md

Glossary.md

Review_Checklist.md

AI_Authoring_Rule.md
```

目前**没有作为一个完整目录整理完成**。

---

# 01_business

完成情况：

✅ BA模板

✅ BA设计思想

✅ README

✅ Design Kit思想

这些都已经讨论。fileciteturn2file17L1-L40 fileciteturn2file18L1-L35

真正业务实例：

```text
BA-001

BA-002

...

BA-007
```

还没有写。

---

# 02_master（当前重点）

这是目前最重要的目录。

## 已完成 Design

```text
Master共通設計書

Business_Master設計書

Environment_Master設計書

API_Master設計書

UseCase_Master設計書

Scenario_Master設計書

API・UseCase・Scenario対応表設計書

Context_Master設計書

Verification_Master設計書

Compare_Policy_Master設計書
```

这些都已经完成。fileciteturn2file3L1-L35

---

## 未完成

真正缺少的是：

```text
Verification_Policy_Master設計書
```

这也是你今天提出要先补完的文件。

---

## design完成以后

下一步原本规划的是：

```text
templates/

schemas/

definitions/

samples/
```

这一套。fileciteturn2file3L1-L35

但是我们后来没有继续，而是跳去写 Runtime。

---

# 03_api_design

应该包含：

```text
README

Template

Guide

Checklist

Example

API设计书
```

目前：

**几乎没有正式完成。**

---

# 04_usecase_design

应该包含：

```text
README

Template

Guide

Checklist

Example

UseCase设计书
```

目前：

**没有正式开始。**

---

# 05_framework

这里其实写了很多很多。

例如：

```text
RunContext

Snapshot

Diff

Report

Framework

System

ExecutionSpec

CommonModel

Identity

Result
```

这些设计已经写了不少。fileciteturn2file0L1-L40

但是按照我们今天达成的一致意见：

> **这一部分先暂停，不继续推进。**

---

# 06_verification_assets

应该包含：

```text
Verification

ExecutionSpec

Schema

Samples

TestData

Evidence
```

目前：

基本没有开始。

---

# runtime

已经讨论过：

```text
Runtime

Bootstrap

Loader

Planner

Runner

Snapshot

Diff

Report
```

但是以后放到最后。

---

# 我建议我们重新冻结开发计划

这是我认为最合理、也最符合我们今天讨论结果的顺序：

|阶段|状态|
|------|------|
|① 补完 `Verification_Policy_Master設計書`|⏳ 下一份|
|② 完成 `02_master/design` 的冻结设计|⏳|
|③ 完成 `02_master/templates`|⏳|
|④ 完成 `02_master/definitions`|⏳|
|⑤ 完成 `02_master/schemas`|⏳|
|⑥ 完成 `02_master/samples`|⏳|
|⑦ 回头整理 `00_repository`（README、规范、Guide、Checklist 等）|⏳|
|⑧ 开始 `03_api_design`|⏳|
|⑨ 开始 `04_usecase_design`|⏳|
|⑩ 最后才进入 `05_framework`、`06_verification_assets`、`runtime`|⏳|

---

我还有一个建议。

**我建议重新建立一份《Repository Progress（Repository完成度一览）》**，里面把整个 Repo 的**所有目录、所有文件**逐个列出来，并标注：

- 🟢 已完成
- 🟡 已设计（对话完成，未整理）
- 🔵 当前编写中
- ⚪ 未开始

以后我们每完成一份文件就更新一次这张总表。这样整个项目始终知道还剩哪些成果物，没有遗漏，也不会再跳到后面的设计。

## 第 6 轮

### 你

你读6个md 然后按照目录阶层 以及每个文件 完整的表示 哪些已经完成 哪些还没有 不要分着写

### ChatGPT

我会把这 6 个 Markdown 作为一份连续设计记录重新通读，然后只输出一棵完整 Repo 目录树，在每个文件后直接标注“已给出内容 / 已实际写入仓库 / 未完成 / 待确认”，不再按目录分段说明。

### ChatGPT

我已经确认这 6 个文件确实是同一段 254 轮对话的六个连续分片。接下来我正在解决两个容易混淆的问题：一是“对话里已经给出完整内容”不等于“已写入 Git”；二是 `02_master` 原始 Master 文件与后来扩展的 `design/` 设计书必须分开标记。

### ChatGPT

我已把 6 个 Markdown 当作一段连续的 254 轮对话重新核对。它们分别是 `part-001.md`～`part-006.md`，共同记录了 Repository 冻结、各模板与设计书制作，以及后来偏离主线继续扩展 `02_master/design` 和 `runtime` 的全过程。fileciteturn6file0 fileciteturn6file1 fileciteturn6file2 fileciteturn7file0 fileciteturn7file1 fileciteturn7file2

下面统一采用：

- `✅ / G?`：六个 MD 中已给出完整内容；是否实际写入 Git 待确认
- `🟨 / G?`：给过结构、片段或组合示例，但尚未形成独立冻结文件
- `⬜ / G?`：尚未完成
- `⚠️ / G?`：内容已完成，但属于 `Compare_Policy_Master設計書.md` 之后偏离冻结主线的扩展设计
- `◻️`：运行生成物，不属于当前手工编写成果物
- `G?`：六个 MD 是聊天记录，不能证明文件已实际写入你的 Repository

外层目录以冻结的 `Repository構成.md v1.1` 为准；`02_master` 内部则结合后来确定的 `design / templates / definitions / schemas / samples` 结构整理。fileciteturn11file0 fileciteturn11file2 fileciteturn8file0

```text
repository/
│
├── README.md
│   └── [🟨 / G?] 提到过Repository入口职责，但未确认最终独立完整版本
│
├── project/
│   ├── 要件定義書.md
│   │   └── [🟨 / G?] 要件、范围、目标讨论较完整，未确认形成最终完整文件
│   ├── WBS.md
│   │   └── [🟨 / G?] 已给出成果物型WBS和项目任务清单，未确认最终冻结文件
│   ├── スケジュール.md
│   │   └── [🟨 / G?] 只有结构和管理字段，没有完整计划内容
│   ├── QA一覧.md
│   │   └── [🟨 / G?] 已定义用途和字段，没有完整QA实例一览
│   └── 課題・リスク管理表.md
│       └── [🟨 / G?] 已定义用途和字段，没有完整项目实例
│
├── system/
│   │
│   ├── 00_repository/
│   │   ├── Repository構成.md
│   │   │   └── [✅ / G?] 完整给出，状态Frozen，外层目录冻结依据
│   │   ├── 文書作成規約.md
│   │   │   └── [✅ / G?] 已给出完整内容
│   │   ├── トレーサビリティ規約.md
│   │   │   └── [✅ / G?] 已给出完整内容
│   │   ├── 命名規約.md
│   │   │   └── [✅ / G?] 已给出完整内容
│   │   ├── レビュー観点一覧.md
│   │   │   └── [✅ / G?] 已给出完整内容
│   │   └── 用語集.md
│   │       └── [✅ / G?] 已给出完整内容
│   │
│   ├── 01_business/
│   │   │
│   │   ├── 01_業務分析/
│   │   │   ├── 現行業務分析書_Template.md
│   │   │   │   └── [✅ / G?] 企业版模板与完整填写例已给出
│   │   │   ├── BA-001_顧客情報照会業務.md
│   │   │   │   └── [✅ / G?] 完整示例已给出
│   │   │   ├── BA分析書_シナリオ一覧_Template.md
│   │   │   │   └── [✅ / G?] 业务分歧/API调用路径模板已给出
│   │   │   ├── BA-001_顧客情報照会業務_シナリオ一覧.md
│   │   │   │   └── [✅ / G?] 完整示例已给出
│   │   │   ├── BA-002_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-002_＜業務名未確定＞_シナリオ一覧.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-003_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-003_＜業務名未確定＞_シナリオ一覧.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-004_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-004_＜業務名未確定＞_シナリオ一覧.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-005_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-005_＜業務名未確定＞_シナリオ一覧.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-006_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-006_＜業務名未確定＞_シナリオ一覧.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── BA-007_＜業務名未確定＞.md
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   └── BA-007_＜業務名未確定＞_シナリオ一覧.md
│   │   │       └── [⬜ / G?] 未完成
│   │   │
│   │   └── 02_E6_API分析/
│   │       ├── API分析書_Template.md
│   │       │   └── [✅ / G?] 完整工业模板已给出
│   │       ├── API-ANL-001_顧客存在確認API分析.md
│   │       │   └── [✅ / G?] 示例内容已给出
│   │       ├── API一覧.md
│   │       │   └── [🟨 / G?] 表结构已给出，24个API实际清单未完成
│   │       ├── API依存関係一覧.md
│   │       │   └── [🟨 / G?] 示例已给出，完整24个API依赖未完成
│   │       ├── API呼出シーケンス一覧.md
│   │       │   └── [🟨 / G?] 示例已给出，完整业务序列未完成
│   │       ├── API共通仕様一覧.md
│   │       │   └── [🟨 / G?] 结构已定义，实际E6规格未完成
│   │       ├── APIエラーコード一覧.md
│   │       │   └── [🟨 / G?] 结构已定义，实际E6错误码未完成
│   │       ├── API認証方式一覧.md
│   │       │   └── [🟨 / G?] 结构已定义，实际环境认证内容未完成
│   │       ├── APIレスポンスコード一覧.md
│   │       │   └── [🟨 / G?] 结构已定义，实际响应码未完成
│   │       └── API調査メモ.md
│   │           └── [⬜ / G?] 未形成正式内容
│   │
│   ├── 02_master/
│   │   │
│   │   ├── README.md
│   │   │   └── [✅ / G?] 02_master的职责、构成、正式化顺序已给出
│   │   │
│   │   ├── E6_API_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── UseCase_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── Scenario_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── Context_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── Verification_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── API_UseCase_Scenario対応表.md
│   │   │   └── [✅ / G?] 模板和使用例已给出
│   │   ├── Compare_Policy_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── Environment_Master.md
│   │   │   └── [✅ / G?] 根目录Master定义内容已给出
│   │   ├── verification_policy_master.md
│   │   │   └── [⬜ / G?] 当前真正缺失；下一份必须先补完
│   │   │
│   │   ├── Business_Master.md
│   │   │   └── [🟨 / G?] 后续设计中出现，但未在最初冻结根文件清单中确认
│   │   ├── variable_catalog_master.md
│   │   │   └── [🟨 / G?] 后续盘点中被提及，正式命名与冻结位置待确认
│   │   │
│   │   ├── design/
│   │   │   │
│   │   │   ├── Master共通設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Business_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Environment_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── API_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── UseCase_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Scenario_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── API・UseCase・Scenario対応表設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Context_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Verification_Master設計書.md
│   │   │   │   └── [✅ / G?] 完整内容已给出
│   │   │   ├── Verification_Policy_Master設計書.md
│   │   │   │   └── [✅ / G?] 设计书内容已给出；注意它不是根目录缺失的verification_policy_master.md
│   │   │   ├── Compare_Policy_Master設計書.md
│   │   │   │   └── [✅ / G?] 冻结主线最后一份核心Master设计书
│   │   │   │
│   │   │   ├── Master間整合性・参照検証設計書.md
│   │   │   │   └── [⚠️ / G?] Compare Policy之后生成，非原冻结主线
│   │   │   ├── Master_Loader設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Registry設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Version・Hash・Snapshot設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Change・Impact・Migration設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_CI・Release・Deployment_Gate設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Operations・Monitoring・Audit設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Security・Access_Control設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Test_Strategy・Quality_Assurance設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Governance・Ownership・Lifecycle設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Data_Quality・Integrity・Consistency設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Compatibility・Evolution・Deprecation設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Configuration・Feature_Flag・Override設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Notification・Escalation・Communication設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Scheduling・Calendar・Execution_Window設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Cache・Index・Search・Lookup設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Import・Export・Synchronization設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计
│   │   │   ├── Master_Backup・Restore・Disaster_Recovery設計書.md
│   │   │   │   └── [⚠️ / G?] 后续扩展设计，内容已给到第273节
│   │   │   └── Master_Migration・Bootstrap・Seed_Data設計書.md
│   │   │       └── [⬜ / G?] 只列为下一份，尚未制作
│   │   │
│   │   ├── templates/
│   │   │   ├── Business_Master_Template.md
│   │   │   │   └── [🟨 / G?] 字段和结构散见设计书，独立冻结文件未完成
│   │   │   ├── Environment_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板内容给过，需重新整理成独立最终文件
│   │   │   ├── E6_API_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── UseCase_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── Scenario_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── API_UseCase_Scenario対応表_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── Context_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── Verification_Master_Template.md
│   │   │   │   └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │   ├── Verification_Policy_Master_Template.md
│   │   │   │   └── [🟨 / G?] 结构已定义，独立最终模板未确认
│   │   │   └── Compare_Policy_Master_Template.md
│   │   │       └── [🟨 / G?] 模板+例子给过，需独立整理
│   │   │
│   │   ├── definitions/
│   │   │   ├── business-master.yml
│   │   │   │   └── [⬜ / G?] 独立正式定义文件未完成
│   │   │   ├── environment-master.yml
│   │   │   │   └── [⬜ / G?] 设计书有YAML片段，正式文件未完成
│   │   │   ├── api-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── usecase-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── scenario-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── api-usecase-scenario-mapping.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── context-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── verification-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── verification-policy-master.yml
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   └── compare-policy-master.yml
│   │   │       └── [⬜ / G?] 未完成
│   │   │
│   │   ├── schemas/
│   │   │   ├── business-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── environment-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── api-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── usecase-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── scenario-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── api-usecase-scenario-mapping.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── context-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── verification-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   ├── verification-policy-master.schema.json
│   │   │   │   └── [⬜ / G?] 未完成
│   │   │   └── compare-policy-master.schema.json
│   │   │       └── [⬜ / G?] 未完成
│   │   │
│   │   └── samples/
│   │       ├── business-master.sample.yml
│   │       │   └── [⬜ / G?] 独立Sample文件未完成
│   │       ├── environment-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── api-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── usecase-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── scenario-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── api-usecase-scenario-mapping.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── context-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── verification-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       ├── verification-policy-master.sample.yml
│   │       │   └── [⬜ / G?] 未完成
│   │       └── compare-policy-master.sample.yml
│   │           └── [⬜ / G?] 未完成
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   │   └── [✅ / G?] 完整工业模板已给出
│   │   ├── API-001_CustomerExistsAPI.md
│   │   │   └── [✅ / G?] 完整示例已给出
│   │   └── API-002～API-024_各API設計書.md
│   │       └── [⬜ / G?] 其余约23个API实际设计书未完成
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   │   └── [✅ / G?] v2.0冻结模板已给出
│   │   ├── UC-001_顧客情報照会.md
│   │   │   └── [✅ / G?] 完整示例已给出
│   │   └── UC-002～UC-010_各UseCase設計書.md
│   │       └── [⬜ / G?] 其余实际UseCase设计书未完成
│   │
│   ├── 05_framework/
│   │   ├── システム設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── 共通Framework設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── RunContext設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── Snapshot設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── Diff設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── Report設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── ファイル入出力設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── ログ・例外設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── 環境設計書.md
│   │   │   └── [✅ / G?] 完整内容已给出
│   │   ├── Framework・業務定義連携設計書.md
│   │   │   └── [⚠️ / G?] 后续追加，不在最初冻结的9份Framework清单中
│   │   ├── Framework設計入力・決定事項一覧.md
│   │   │   └── [⚠️ / G?] 后续追加
│   │   └── 共通Identity・Resultモデル設計書.md
│   │       └── [⚠️ / G?] 后续追加
│   │
│   └── 06_verification_assets/
│       ├── Verification仕様書_Template.md
│       │   └── [✅ / G?] 完整模板已给出
│       ├── VER-001_顧客情報照会.md
│       │   └── [🟨 / G?] 示例内容已给出，最终独立文件待整理
│       │
│       ├── execution_spec/
│       │   ├── Execution仕様書設計書.md
│       │   │   └── [✅ / G?] 设计内容已给出
│       │   ├── Execution仕様書_Template.yml
│       │   │   └── [🟨 / G?] 完整YAML示例给过，独立文件待整理
│       │   └── EXEC-001_顧客情報照会.yml
│       │       └── [🟨 / G?] 示例给过，最终文件待整理
│       │
│       ├── api_test_spec/
│       │   ├── API単体テスト仕様書_Template.md
│       │   │   └── [🟨 / G?] 测试体系和表结构已给出，独立最终文件待确认
│       │   └── API-001_単体テスト仕様書.md
│       │       └── [🟨 / G?] 示例级内容，未确认完成
│       │
│       ├── usecase_test_spec/
│       │   ├── UseCaseテスト仕様書_Template.md
│       │   │   └── [🟨 / G?] 测试结构已给出，独立最终文件待确认
│       │   └── UC-001_テスト仕様書.md
│       │       └── [🟨 / G?] 示例级内容，未确认完成
│       │
│       ├── test_data/
│       │   ├── TestData設計書.md
│       │   │   └── [✅ / G?] 完整内容已给出
│       │   ├── TestData_Template.json
│       │   │   └── [✅ / G?] 模板内容已给出
│       │   └── TD-001_SC-001_normal.json
│       │       └── [🟨 / G?] 示例结构存在，正式文件待整理
│       │
│       ├── reports/
│       │   └── 各Report Template
│       │       └── [🟨 / G?] Report格式已在Report設計書定义，独立模板未完成
│       │
│       └── evidence/
│           └── Evidence定義・Template
│               └── [🟨 / G?] Evidence结构已定义，独立模板未完成
│
├── runtime/
│   ├── Runtimeアーキテクチャ設計書.md
│   │   └── [⚠️ / G?] 已给出完整内容，但进入Runtime过早
│   ├── Javaパッケージ・クラス設計書.md
│   │   └── [⚠️ / G?] 后续Runtime扩展内容
│   ├── ExecutionSpecスキーマ設計書.md
│   │   └── [⚠️ / G?] 后续Runtime扩展内容
│   ├── TestDataスキーマ設計書.md
│   │   └── [🟨 / G?] 有规划和部分内容，完成状态不明确
│   ├── RunContextデータモデル設計書.md
│   │   └── [🟨 / G?] 有规划和相关模型，独立完成状态不明确
│   ├── Validator設計書.md
│   │   └── [⬜ / G?] 未确认完整制作
│   ├── API実行エンジン設計書.md
│   │   └── [⬜ / G?] 未确认完整制作
│   ├── Runner制御設計書.md
│   │   └── [⬜ / G?] 未确认完整制作
│   ├── Snapshot・Diff・Report実装設計書.md
│   │   └── [⬜ / G?] 未确认完整制作
│   ├── Runtimeテスト設計書.md
│   │   └── [⬜ / G?] 未确认完整制作
│   ├── config/
│   │   └── [⬜ / G?] 配置结构有设计，实际配置文件未完成
│   ├── scripts/
│   │   └── [⬜ / G?] 未实现
│   └── src/
│       ├── main/java/
│       │   └── [⬜ / G?] Java正式实现尚未开始
│       ├── main/resources/
│       │   └── [⬜ / G?] 未实现
│       └── test/
│           └── [⬜ / G?] 未实现
│
├── build/
│   ├── scripts/
│   │   ├── generate-spec.sh
│   │   │   └── [⬜ / G?] 只规划，未实现
│   │   ├── test-local.sh
│   │   │   └── [⬜ / G?] 只规划，未实现
│   │   ├── build-jar.sh
│   │   │   └── [⬜ / G?] 只规划，未实现
│   │   ├── package-release.sh
│   │   │   └── [⬜ / G?] 只规划，未实现
│   │   └── build-image.sh
│   │       └── [⬜ / G?] 只规划，未实现
│   ├── docker/
│   │   ├── Dockerfile
│   │   │   └── [⬜ / G?] 未实现
│   │   └── docker-compose.dev.yml
│   │       └── [⬜ / G?] 未实现
│   └── release/
│       └── e6-verifier-*.zip
│           └── [◻️] Build生成物，目前不存在
│
├── staging/
│   ├── config/
│   │   └── [⬜ / G?] 未实现
│   ├── data/
│   │   └── [◻️] 运行生成目录
│   └── logs/
│       └── [◻️] 运行生成目录
│
└── outputs/
    ├── baseline/
    │   └── [◻️] Runtime生成，不是当前设计文件
    ├── runs/
    │   └── [◻️] Runtime生成
    ├── reports/
    │   └── [◻️] Runtime生成
    └── evidence/
        └── [◻️] Runtime生成
```

最关键的事实是：

1. **冻结主线的 `02_master/design` 已经完整做到 `Compare_Policy_Master設計書.md`。**当时的完成清单明确包含 README、共通、Environment、API、UseCase、Scenario、对应表、Context、Verification、Verification Policy 和 Compare Policy。fileciteturn13file6
2. **当前真正应该补的是根目录的 `verification_policy_master.md`，不是重新写 `Verification_Policy_Master設計書.md`。**后者已经有完整设计内容；前者是实际Master定义文件。fileciteturn8file6 fileciteturn10file5
3. `Compare_Policy_Master設計書.md` 之后生成的整合性、Loader、Registry、CI、运维、安全、备份、同步等文件，虽然内容很多已经写完，但它们是后来偏离冻结主线产生的扩展，当前全部暂停。fileciteturn13file0 fileciteturn10file7 fileciteturn10file8
4. 六个 MD 只能确认“对话中已经给出内容”，不能确认任何文件已经真实写进 Git；导出记录本身也明确承认了这一点。fileciteturn10file6

因此当前唯一正确的继续顺序是：

```text
verification_policy_master.md
→ 02_master核心Design整合Review
→ templates独立化
→ definitions
→ schemas
→ samples
→ 02_master封板
→ 再进入其他目录
```

## 第 7 轮

### 你

按照你的说法把不应该或者偏离冻结的文件都标红或者需要重做 给一个最新的文件构成

### ChatGPT

我会把最新结构统一整理成一棵目录树，并把每个文件直接标成：保留、需要重做、偏离冻结应移出、尚未完成。重点先纠正 `02_master`，再把全 Repo 的后续目录放回正确顺序。

### ChatGPT

下面这版作为**最新的 Repository 文件构成基准**。

六个 Markdown 能确认的是“对话中是否已经给出内容”，不能证明文件已经写入 Git。最初冻结的外层结构包含 `project / system/00～06 / runtime / build / staging / outputs`；`02_master` 后来正式修正为 10 类 Master，并区分 Master 实体、设计书、模板、运行定义、Schema 和 Sample。fileciteturn12file7 fileciteturn12file3

状态说明：

```text
🟢 保留       已冻结或内容基本完整，可继续使用
🟡 未完成     正式计划内，但尚未制作完成
🟠 需要重做   内容可保留，但命名、位置、结构或上游依赖需要重新整理
🔴 移出主线   Compare Policy之后偏离冻结范围产生，当前不得继续
⚪ 自动生成物 不属于当前手工设计阶段
G?            是否已经实际写入Git尚未确认
```

```text
repository/
│
├── README.md
│   └── 🟠 G? 需要重做
│       └── 原因：必须改为指向最新冻结目录和当前推进顺序
│
├── project/
│   ├── 要件定義書.md
│   │   └── 🟠 G? 内容已有讨论，需整理为正式冻结版
│   ├── WBS.md
│   │   └── 🟠 G? 已给过多版，需按最新成果物目录重做
│   ├── スケジュール.md
│   │   └── 🟡 G? 未完成
│   ├── QA一覧.md
│   │   └── 🟡 G? 未完成实际内容
│   └── 課題・リスク管理表.md
│       └── 🟡 G? 未完成实际内容
│
├── system/
│   │
│   ├── 00_repository/
│   │   ├── Repository構成.md
│   │   │   └── 🟠 G? 必须重做
│   │   │       └── 原因：旧版未正确反映02_master最终结构和偏离文件处理
│   │   ├── 文書作成規約.md
│   │   │   └── 🟢 G? 保留
│   │   ├── トレーサビリティ規約.md
│   │   │   └── 🟢 G? 保留
│   │   ├── 命名規約.md
│   │   │   └── 🟠 G? 需要补充Master文件名统一规则
│   │   ├── レビュー観点一覧.md
│   │   │   └── 🟢 G? 保留
│   │   └── 用語集.md
│   │       └── 🟠 G? 需要追加Verification Policy、Compare Policy等定义
│   │
│   ├── 01_business/
│   │   │
│   │   ├── 01_業務分析/
│   │   │   ├── 現行業務分析書_Template.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── BA分析書_シナリオ一覧_Template.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── BA-001_顧客情報照会業務.md
│   │   │   │   └── 🟢 G? 示例保留
│   │   │   ├── BA-001_顧客情報照会業務_シナリオ一覧.md
│   │   │   │   └── 🟢 G? 示例保留
│   │   │   ├── BA-002_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-002_＜業務名＞_シナリオ一覧.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-003_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-003_＜業務名＞_シナリオ一覧.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-004_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-004_＜業務名＞_シナリオ一覧.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-005_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-005_＜業務名＞_シナリオ一覧.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-006_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-006_＜業務名＞_シナリオ一覧.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── BA-007_＜業務名＞.md
│   │   │   │   └── 🟡 G? 未完成
│   │   │   └── BA-007_＜業務名＞_シナリオ一覧.md
│   │   │       └── 🟡 G? 未完成
│   │   │
│   │   └── 02_E6_API分析/
│   │       ├── API分析書_Template.md
│   │       │   └── 🟢 G? 保留
│   │       ├── API-ANL-001_顧客存在確認API分析.md
│   │       │   └── 🟢 G? 示例保留
│   │       ├── API一覧.md
│   │       │   └── 🟡 G? 24个API实际数据未完成
│   │       ├── API依存関係一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       ├── API呼出シーケンス一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       ├── API共通仕様一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       ├── APIエラーコード一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       ├── API認証方式一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       ├── APIレスポンスコード一覧.md
│   │       │   └── 🟡 G? 未完成
│   │       └── API調査メモ.md
│   │           └── 🟡 G? 未完成
│   │
│   ├── 02_master/
│   │   │
│   │   ├── README.md
│   │   │   └── 🟠 G? 需要重做并重新冻结
│   │   │       ├── 必须成为02_master唯一文件构成基准
│   │   │       ├── 必须记录文件职责、状态和依赖关系
│   │   │       └── 必须明确禁止擅自新增Master平台设计书
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   Master实体文件：人工维护的正式Master
│   │   │  ─────────────────────────────────────
│   │   │
│   │   ├── Business_Master.md
│   │   │   └── 🟠 G? 内容需要从已有模板整理为正式实体文件
│   │   ├── Environment_Master.md
│   │   │   └── 🟢 G? 保留，需最终Review
│   │   ├── API_Master.md
│   │   │   └── 🟠 G? 统一名称
│   │   │       └── 旧名E6_API_Master.md不得与本文件并存
│   │   ├── UseCase_Master.md
│   │   │   └── 🟢 G? 保留
│   │   ├── Scenario_Master.md
│   │   │   └── 🟢 G? 保留
│   │   ├── API・UseCase・Scenario対応表.md
│   │   │   └── 🟠 G? 统一名称和表结构
│   │   │       └── 旧名API_UseCase対応表.md、
│   │   │           API_UseCase_Scenario対応表.md不得并存
│   │   ├── Context_Master.md
│   │   │   └── 🟢 G? 保留
│   │   ├── Verification_Master.md
│   │   │   └── 🟢 G? 保留
│   │   ├── Verification_Policy_Master.md
│   │   │   └── 🟡 G? 当前第一优先，尚未完成
│   │   │       ├── 正确拼写：Verification
│   │   │       └── vertification_policy_master.md属于错误文件名
│   │   └── Compare_Policy_Master.md
│   │       └── 🟢 G? 保留
│   │
│   │   ├── Variable_Catalog_Master.md
│   │   │   └── 🔴 G? 不属于当前冻结的10类Master
│   │   │       ├── 不得直接放入当前正式构成
│   │   │       └── 将来确认与Context_Master的职责边界后再决定
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   design：冻结范围内的核心设计书
│   │   │  ─────────────────────────────────────
│   │   │
│   │   ├── design/
│   │   │   ├── Master共通設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Business_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Environment_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── API_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── UseCase_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Scenario_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── API・UseCase・Scenario対応表設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Context_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Verification_Master設計書.md
│   │   │   │   └── 🟢 G? 保留
│   │   │   ├── Verification_Policy_Master設計書.md
│   │   │   │   └── 🟢 G? 已有内容，保留
│   │   │   └── Compare_Policy_Master設計書.md
│   │   │       └── 🟢 G? 冻结核心设计书最后一份
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   templates：10类Master对应人工填写模板
│   │   │  ─────────────────────────────────────
│   │   │
│   │   ├── templates/
│   │   │   ├── Business_Master_Template.md
│   │   │   │   └── 🟠 G? 已有片段，需整理为独立最终文件
│   │   │   ├── Environment_Master_Template.md
│   │   │   │   └── 🟠 G? 需整理
│   │   │   ├── API_Master_Template.md
│   │   │   │   └── 🟠 G? 需从E6_API_Master模板统一名称
│   │   │   ├── UseCase_Master_Template.md
│   │   │   │   └── 🟠 G? 需整理
│   │   │   ├── Scenario_Master_Template.md
│   │   │   │   └── 🟠 G? 需整理
│   │   │   ├── API・UseCase・Scenario対応表_Template.md
│   │   │   │   └── 🟠 G? 需统一旧版模板
│   │   │   ├── Context_Master_Template.md
│   │   │   │   └── 🟠 G? 需整理
│   │   │   ├── Verification_Master_Template.md
│   │   │   │   └── 🟠 G? 需整理
│   │   │   ├── Verification_Policy_Master_Template.md
│   │   │   │   └── 🟡 G? 尚未形成最终独立模板
│   │   │   └── Compare_Policy_Master_Template.md
│   │   │       └── 🟠 G? 需整理
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   definitions：Runtime读取的正式定义
│   │   │  ─────────────────────────────────────
│   │   │
│   │   ├── definitions/
│   │   │   ├── business-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── environment-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── api-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── usecase-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── scenario-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── api-usecase-scenario-mapping.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── context-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── verification-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── verification-policy-master.yml
│   │   │   │   └── 🟡 G? 未完成
│   │   │   └── compare-policy-master.yml
│   │   │       └── 🟡 G? 未完成
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   schemas：definitions的机器验证约束
│   │   │  ─────────────────────────────────────
│   │   │
│   │   ├── schemas/
│   │   │   ├── business-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── environment-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── api-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── usecase-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── scenario-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── api-usecase-scenario-mapping.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── context-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── verification-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   ├── verification-policy-master.schema.json
│   │   │   │   └── 🟡 G? 未完成
│   │   │   └── compare-policy-master.schema.json
│   │   │       └── 🟡 G? 未完成
│   │   │
│   │   │  ─────────────────────────────────────
│   │   │   samples：每类Master的完整样例
│   │   │  ─────────────────────────────────────
│   │   │
│   │   └── samples/
│   │       ├── business-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── environment-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── api-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── usecase-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── scenario-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── api-usecase-scenario-mapping.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── context-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── verification-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       ├── verification-policy-master.sample.yml
│   │       │   └── 🟡 G? 未完成
│   │       └── compare-policy-master.sample.yml
│   │           └── 🟡 G? 未完成
│   │
│   ├── 03_api_design/
│   │   ├── API設計書_Template.md
│   │   │   └── 🟢 G? 保留
│   │   ├── API-001_CustomerExistsAPI.md
│   │   │   └── 🟢 G? 示例保留
│   │   └── API-002～API-024_各API設計書.md
│   │       └── 🟡 G? 未完成；实际文件名待API分析确定
│   │
│   ├── 04_usecase_design/
│   │   ├── UseCase設計書_Template.md
│   │   │   └── 🟢 G? 保留
│   │   ├── UC-001_顧客情報照会.md
│   │   │   └── 🟢 G? 示例保留
│   │   └── UC-002～UC-010_各UseCase設計書.md
│   │       └── 🟡 G? 未完成；实际名称待业务分析确定
│   │
│   ├── 05_framework/
│   │   ├── システム設計書.md
│   │   │   └── 🟠 G? 内容保留，02_master封板后整合Review
│   │   ├── 共通Framework設計書.md
│   │   │   └── 🟠 G? 内容保留，需重新核对Policy Loader职责
│   │   ├── RunContext設計書.md
│   │   │   └── 🟠 G? 内容保留，需核对Context Master
│   │   ├── Snapshot設計書.md
│   │   │   └── 🟠 G? 内容保留，暂不继续
│   │   ├── Diff設計書.md
│   │   │   └── 🟠 G? 需核对Compare Policy与Verification Policy边界
│   │   ├── Report設計書.md
│   │   │   └── 🟠 G? 内容保留，暂不继续
│   │   ├── ファイル入出力設計書.md
│   │   │   └── 🟠 G? 内容保留，暂不继续
│   │   ├── ログ・例外設計書.md
│   │   │   └── 🟠 G? 内容保留，暂不继续
│   │   └── 環境設計書.md
│   │       └── 🟠 G? 需与Environment Master重新核对
│   │
│   └── 06_verification_assets/
│       ├── Verification仕様書_Template.md
│       │   └── 🟠 G? 内容保留，Verification Policy完成后重做引用关系
│       ├── execution_spec/
│       │   ├── Execution仕様書設計書.md
│       │   │   └── 🟠 G? 内容保留，需基于02_master重新Review
│       │   ├── Execution仕様書_Template.yml
│       │   │   └── 🟠 G? 需重做Policy Reference部分
│       │   └── EXEC-001_顧客情報照会.yml
│       │       └── 🟠 G? 示例需随Template重新生成
│       ├── api_test_spec/
│       │   ├── API単体テスト仕様書_Template.md
│       │   │   └── 🟠 G? 需核对Verification Policy
│       │   └── API-001_単体テスト仕様書.md
│       │       └── 🟠 G? 示例需重新生成
│       ├── usecase_test_spec/
│       │   ├── UseCaseテスト仕様書_Template.md
│       │   │   └── 🟠 G? 需核对Scenario与Policy
│       │   └── UC-001_テスト仕様書.md
│       │       └── 🟠 G? 示例需重新生成
│       ├── test_data/
│       │   ├── TestData設計書.md
│       │   │   └── 🟠 G? 内容保留，需基于Schema重新Review
│       │   ├── TestData_Template.json
│       │   │   └── 🟠 G? 需重做Schema一致性
│       │   └── TD-001_SC-001_normal.json
│       │       └── 🟠 G? 示例需重新生成
│       ├── reports/
│       │   └── Report Templates
│       │       └── 🟡 G? 未形成正式独立文件
│       └── evidence/
│           └── Evidence Templates
│               └── 🟡 G? 未形成正式独立文件
│
├── runtime/
│   ├── Runtimeアーキテクチャ設計書.md
│   │   └── 🔴 G? 偏离当前顺序，移出主线
│   │       └── 02_master封板后根据正式definitions重新设计
│   ├── Javaパッケージ・クラス設計書.md
│   │   └── 🔴 G? 偏离当前顺序，需重做
│   ├── ExecutionSpecスキーマ設計書.md
│   │   └── 🔴 G? 偏离当前顺序，需与06目录重新整合
│   ├── TestDataスキーマ設計書.md
│   │   └── 🔴 G? 当前暂停
│   ├── RunContextデータモデル設計書.md
│   │   └── 🔴 G? 当前暂停
│   ├── Validator設計書.md
│   │   └── 🟡 G? 尚未完成，不得现在继续
│   ├── API実行エンジン設計書.md
│   │   └── 🟡 G? 尚未完成，不得现在继续
│   ├── Runner制御設計書.md
│   │   └── 🟡 G? 尚未完成，不得现在继续
│   ├── Snapshot・Diff・Report実装設計書.md
│   │   └── 🟡 G? 尚未完成，不得现在继续
│   ├── Runtimeテスト設計書.md
│   │   └── 🟡 G? 尚未完成，不得现在继续
│   ├── config/
│   │   └── 🟡 G? 未实现
│   ├── scripts/
│   │   └── 🟡 G? 未实现
│   └── src/
│       ├── main/java/
│       │   └── 🟡 G? 未实现
│       ├── main/resources/
│       │   └── 🟡 G? 未实现
│       └── test/
│           └── 🟡 G? 未实现
│
├── build/
│   ├── scripts/
│   │   ├── generate-spec.sh
│   │   │   └── 🟡 G? 未实现
│   │   ├── test-local.sh
│   │   │   └── 🟡 G? 未实现
│   │   ├── build-jar.sh
│   │   │   └── 🟡 G? 未实现
│   │   ├── package-release.sh
│   │   │   └── 🟡 G? 未实现
│   │   └── build-image.sh
│   │       └── 🟡 G? 未实现
│   ├── docker/
│   │   ├── Dockerfile
│   │   │   └── 🟡 G? 未实现
│   │   └── docker-compose.dev.yml
│   │       └── 🟡 G? 未实现
│   └── release/
│       └── e6-verifier-*.zip
│           └── ⚪ Build自动生成物
│
├── staging/
│   ├── config/
│   │   └── 🟡 G? 未实现
│   ├── data/
│   │   └── ⚪ 运行生成物
│   └── logs/
│       └── ⚪ 运行生成物
│
├── outputs/
│   ├── baseline/
│   │   └── ⚪ Runtime生成物
│   ├── runs/
│   │   └── ⚪ Runtime生成物
│   ├── reports/
│   │   └── ⚪ Runtime生成物
│   └── evidence/
│       └── ⚪ Runtime生成物
│
└── archive/
    └── deferred_master_platform_design/
        ├── Master間整合性・参照検証設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Loader設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Registry設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Version・Hash・Snapshot設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Change・Impact・Migration設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_CI・Release・Deployment_Gate設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Operations・Monitoring・Audit設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Security・Access_Control設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Test_Strategy・Quality_Assurance設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Governance・Ownership・Lifecycle設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Data_Quality・Integrity・Consistency設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Compatibility・Evolution・Deprecation設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Configuration・Feature_Flag・Override設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Notification・Escalation・Communication設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Scheduling・Calendar・Execution_Window設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Cache・Index・Search・Lookup設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Import・Export・Synchronization設計書.md
        │   └── 🔴 从02_master/design移出
        ├── Master_Backup・Restore・Disaster_Recovery設計書.md
        │   └── 🔴 从02_master/design移出
        └── Master_Migration・Bootstrap・Seed_Data設計書.md
            └── 🔴 未制作，取消当前计划
```

`Compare_Policy_Master設計書.md` 之后继续生成的 Loader、Registry、版本、CI、运维、安全、缓存、同步、备份等文件，确实不是当时冻结的核心 Master 设计书；部分虽然已经写出大量内容，但应从活动中的 `02_master/design/` 移出，保留到延期区，而不是继续制作下一份。fileciteturn10file0 fileciteturn10file6 fileciteturn10file10

当前正式推进顺序固定为：

```text
1. Verification_Policy_Master.md
2. 重做02_master/README.md并冻结文件名
3. 对11份核心design进行整合Review
4. 完成10份templates
5. 完成10份definitions
6. 完成10份schemas
7. 完成10份samples
8. 重新制作system/00_repository/Repository構成.md
9. 正式封板02_master
10. 再依次返回03、04、05、06和runtime
```

其中需要特别纠正的是：应写作 `Verification_Policy_Master.md`，不是 `vertification_policy_master.md`。

## 第 8 轮

### 你

02master根目录给的之前都是模版吧

### ChatGPT

对，**你说得对**。

我上一版把 `02_master` 根目录中的 `.md` 文件误标成了“正式 Master 实体文件”，这是不准确的。它们最初是按你的要求制作的 **Master 模板**。

当时你明确说：

> 接下来把 master 的各个模版给我

随后给出的文件直接放在：

```text
system/02_master/
```

而且文件头明确写着：

```yaml
status: Template
document_type: Master
```

例如 `E6_API_Master.md`、`UseCase_Master.md`、`Scenario_Master.md` 都是这种形式。fileciteturn11file2

后面的对话也再次确认了正确顺序：

```text
保留原有模板
补齐遗漏模板
新增 design 目录
再逐步生成 definitions 和 schemas
```

并明确说明当时已有的是“多份 MD 模板”，缺少的是 `Verification Policy Master` 等未补齐模板。fileciteturn11file1 fileciteturn11file7

所以，原始正确关系应当是：

```text
system/
└── 02_master/
    ├── README.md
    │
    │  # 根目录：Master Markdown模板
    ├── E6_API_Master.md
    ├── UseCase_Master.md
    ├── Scenario_Master.md
    ├── Context_Master.md
    ├── Verification_Master.md
    ├── API_UseCase_Scenario対応表.md
    ├── Compare_Policy_Master.md
    ├── Environment_Master.md
    ├── Variable_Catalog_Master.md          # 是否属于冻结清单需按原文件确认
    └── Verification_Policy_Master.md       # 当时唯一明确缺少
    │
    ├── design/
    │   ├── Master共通設計書.md
    │   ├── Environment_Master設計書.md
    │   ├── API_Master設計書.md
    │   ├── UseCase_Master設計書.md
    │   ├── Scenario_Master設計書.md
    │   ├── API・UseCase・Scenario対応表設計書.md
    │   ├── Context_Master設計書.md
    │   ├── Verification_Master設計書.md
    │   ├── Verification_Policy_Master設計書.md
    │   └── Compare_Policy_Master設計書.md
    │
    ├── schemas/
    ├── definitions/
    ├── samples/
    └── examples/
```

其中必须区分：

```text
02_master/*.md
= 给人填写和维护的Master模板

02_master/design/*設計書.md
= 说明这些Master如何设计、字段为何存在、关系和校验规则是什么

02_master/definitions/*.yml
= 将来Runtime实际读取的正式定义数据

02_master/schemas/*
= 对definitions进行机器校验的Schema

02_master/samples或examples/*
= 完整填写样例
```

因此目前正确的主线不是重新制作根目录全部 Master 实体，而是：

```text
1. 补完根目录 Verification_Policy_Master.md 模板
2. 确认根目录原有模板完整清单和最终文件名
3. Review冻结范围内的核心design设计书
4. 补齐其他尚未完成的模板、Schema、Definition和Sample
5. 完成02_master后再进入其他目录
```

之前第 254 轮把根目录文件称为“Master定义文件／Master实体文件”，是后续对话中的再次混淆，不能用它覆盖更早已经实际给出的模板属性。fileciteturn11file10

所以最终结论是：

> **`02_master` 根目录此前给出的确实主要是 Master 模板；当时根目录模板基本完成，只缺 `Verification_Policy_Master.md`。**

## 第 9 轮

### 你

目前咱们推进顺序 详细

### ChatGPT

我先把“当前推进顺序”和“02_master 当前文件状态”合并成一份唯一基准，避免再把根目录模板、design 设计书和后续 Runtime 文件混在一起。

### ChatGPT

# 当前推进顺序：唯一执行基准

目前不再继续扩展新设计书，也不进入 Runtime。当前主线固定为：

```text
先恢复并封板 system/02_master
        ↓
更新 Repository 总体结构与WBS
        ↓
完成业务与API现行分析
        ↓
完成 API / UseCase 正式设计
        ↓
重新审查 Framework
        ↓
完成 Verification Assets
        ↓
最后进入 Runtime、Build、Staging
```

原先 `02_master` 根目录明确给过 8 份 Markdown 模板：API、UseCase、Scenario、Context、Verification、API-UseCase-Scenario 对应表、Compare Policy、Environment；这些文件头也标记为 `status: Template`。fileciteturn15file1 fileciteturn15file3

后来才发现 Verification Policy 模板遗漏，并形成了“保留已有模板→补齐遗漏模板→完成正式设计书→生成 YAML、Schema、Sample”的顺序。fileciteturn15file0

---

# 一、当前状态标记规则

```text
【已给出内容】
六个Markdown对话中已经完整输出过文件内容。

【已实际写入仓库】
文件已真实存在于Git Repository。
目前没有仓库连接或目录文件，因此全部待确认。

【未完成】
对话中尚未给出完整文件。

【待确认】
历史设计存在冲突，需要在冻结时决定是否保留、改名或移出。
```

---

# 二、当前 `system/02_master/` 完整结构

这里按最新理解修正：

- 根目录 `.md` 是**人工填写的 Master 模板**。
- 不再重复建立一个内容完全相同的 `templates/` 目录。
- `design/` 只保留做到 `Compare_Policy_Master設計書.md` 为止的核心设计。
- Compare Policy 之后的 Master 平台扩展设计全部移出活动目录。

```text
system/
└── 02_master/
    │
    ├── README.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：需要重做
    │       └── 在所有文件名冻结后重新生成
    │
    │  ─────────────────────────────────────
    │   根目录：人工填写用 Master 模板
    │  ─────────────────────────────────────
    │
    ├── E6_API_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── UseCase_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── Scenario_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── Context_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── Verification_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── API_UseCase_Scenario対応表.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留，统一最终文件名
    │
    ├── Compare_Policy_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    ├── Environment_Master.md
    │   ├── 内容：已给出内容
    │   ├── 仓库：待确认
    │   └── 动作：保留并Review
    │
    └── Verification_Policy_Master.md
        ├── 内容：未完成
        ├── 仓库：未写入
        └── 动作：当前第一优先文件
```

原来的 8 份模板与文件名在对话中有明确记录。fileciteturn15file7

正确拼写是：

```text
Verification_Policy_Master.md
```

不是：

```text
Vertification_Policy_Master.md
```

---

## 根目录暂不加入的两个文件

```text
Business_Master.md
Variable_Catalog_Master.md
```

当前状态统一标记为：

```text
内容：部分讨论过
仓库：待确认
状态：待确认
当前动作：不新增、不删除、不进入当前第一步
```

原因是历史记录存在两套口径：

- 最初冻结并实际给出的是 8 份根目录模板。
- 后来设计体系又提出了 Business Master 等 10 类 Master。
- `Variable Catalog` 早期也出现过，但其职责可能已经由 `Context_Master` 承担。

因此，当前不能凭印象直接把它们加入正式根目录。它们将在“根目录模板冻结 Review”中处理，但不阻塞 `Verification_Policy_Master.md`。

---

# 三、当前第一阶段：补完缺失模板

## Step 1：制作 `Verification_Policy_Master.md`

这是下一份唯一允许制作的文件。

```text
system/02_master/Verification_Policy_Master.md
```

它是**模板**，不是设计书。

该模板至少需要包含：

```text
1. 文书信息
2. Verification Policy一览
3. Policy ID
4. Policy名称
5. Policy分类
6. 适用范围
7. Default Severity
8. Failure Policy
9. Null Policy
10. Missing Field Policy
11. Empty Value Policy
12. Type Policy
13. String Normalize Policy
14. Numeric Tolerance
15. Decimal Scale
16. Date / Datetime Tolerance
17. Case Sensitivity
18. Whitespace Policy
19. Array Policy
20. Schema Validation Mode
21. Stop / Continue Policy
22. Retry Policy
23. Environment Override
24. Production限制
25. Evidence Policy
26. Result Aggregation
27. Override许可范围
28. 状态与版本
29. 填写例
30. Review检查项
```

需要明确它与其他文件的边界：

```text
Verification_Policy_Master.md
= 共通判断机制、默认值、覆盖规则

Verification_Master.md
= 具体API、字段、JSONPath使用哪条验证规则

Compare_Policy_Master.md
= 当前结果与Baseline／前次结果怎样比较
```

`Verification_Policy_Master設計書.md` 已经在对话中完整给出，所以当前模板应以该设计书为依据制作，而不是重新发明规则。fileciteturn14file10

### Step 1完成条件

```text
□ 文件名拼写正确
□ status明确为Template
□ 与Verification Master职责不重复
□ 与Compare Policy职责不重复
□ 支持API字段必填、类型、固定值、Enum、长度验证
□ 支持Request、Response、Context
□ 支持Global、API、UseCase、Scenario层级覆盖
□ 包含完整填写例
□ 包含Review Checklist
□ 可直接提交Git
```

---

# 四、第二阶段：冻结根目录模板集合

`Verification_Policy_Master.md` 完成后，不立即写 definitions 或 Runtime，而是先冻结根目录。

## Step 2.1：逐个Review现有模板

顺序固定为：

```text
1. Environment_Master.md
2. E6_API_Master.md
3. UseCase_Master.md
4. Scenario_Master.md
5. API_UseCase_Scenario対応表.md
6. Context_Master.md
7. Verification_Master.md
8. Verification_Policy_Master.md
9. Compare_Policy_Master.md
```

这个顺序反映实际依赖：

```text
Environment
    ↓
API
    ↓
UseCase
    ↓
Scenario
    ↓
API调用顺序
    ↓
Context传递
    ↓
具体Verification
    ↓
共通Verification Policy
    ↓
Baseline Compare Policy
```

## Step 2.2：解决两个待确认项

在这一阶段只做决定，不马上扩展：

```text
Business_Master.md
    是否独立存在？
    还是由01_business负责并由UseCase_Master引用？

Variable_Catalog_Master.md
    是否独立存在？
    还是全部并入Context_Master？
```

判断标准：

```text
有独立职责、独立维护者、独立生命周期
    → 可以保留独立Master

仅仅是其他Master的重复字段
    → 不建立独立Master
```

## Step 2.3：统一命名

需要消除这些历史命名冲突：

```text
E6_API_Master.md
API_Master.md

API_UseCase対応表.md
API_UseCase_Scenario対応表.md
API・UseCase・Scenario対応表.md

verification_policy_master.md
Verification_Policy_Master.md
```

在正式冻结前，只允许保留一个文件名。

当前建议：

```text
E6_API_Master.md
API_UseCase_Scenario対応表.md
Verification_Policy_Master.md
```

---

# 五、第三阶段：核心 `design/` 收口

根目录模板冻结后，进入设计书整合Review。

这里**不是继续新增设计书**，而是审查已经给出的设计书。

```text
system/
└── 02_master/
    └── design/
        ├── Master共通設計書.md
        ├── Business_Master設計書.md
        ├── Environment_Master設計書.md
        ├── API_Master設計書.md
        ├── UseCase_Master設計書.md
        ├── Scenario_Master設計書.md
        ├── API・UseCase・Scenario対応表設計書.md
        ├── Context_Master設計書.md
        ├── Verification_Master設計書.md
        ├── Verification_Policy_Master設計書.md
        └── Compare_Policy_Master設計書.md
```

当前状态统一为：

```text
内容：已给出内容
仓库：待确认
完成状态：正文已给出，但尚未完成整合Review
```

## Step 3.1：先审查 `Master共通設計書.md`

确认所有 Master 共通规则：

```text
Master ID
Version
Status
Owner
Reviewer
Approver
Effective From / To
Reference
Override
Lifecycle
Traceability
Audit字段
命名规则
```

## Step 3.2：按依赖顺序审查各设计书

```text
Environment
    ↓
Business
    ↓
API
    ↓
UseCase
    ↓
Scenario
    ↓
对应表
    ↓
Context
    ↓
Verification
    ↓
Verification Policy
    ↓
Compare Policy
```

## Step 3.3：每份设计书必须检查

```text
□ 是否有对应根目录模板
□ 模板字段是否全部能在设计书中找到定义
□ 字段名和ID是否统一
□ 必填／任意是否明确
□ Enum是否明确
□ 默认值是否明确
□ Reference关系是否明确
□ Override优先级是否明确
□ 状态与生命周期是否明确
□ 是否包含错误条件
□ 是否包含正常例和异常例
□ 是否混入Runtime实现细节
□ 是否和其他Master职责重叠
```

## Step 3.4：处理 `Business_Master設計書.md`

它不删除，但需要决定：

```text
A. 保留Business Master
   → 根目录必须补Business_Master.md模板

B. 不保留Business Master
   → Business_Master設計書.md移出核心设计
   → Business信息由01_business和UseCase_Master管理
```

这一项必须在设计Review阶段解决，不能继续悬空。

---

# 六、第四阶段：把偏离冻结的设计移出活动目录

以下文件不再放在活动中的：

```text
system/02_master/design/
```

统一移动到：

```text
archive/
└── deferred_master_platform_design/
```

包括：

```text
Master間整合性・参照検証設計書.md
Master_Loader設計書.md
Master_Registry設計書.md
Master_Version・Hash・Snapshot設計書.md
Master_Change・Impact・Migration設計書.md
Master_CI・Release・Deployment_Gate設計書.md
Master_Operations・Monitoring・Audit設計書.md
Master_Security・Access_Control設計書.md
Master_Test_Strategy・Quality_Assurance設計書.md
Master_Governance・Ownership・Lifecycle設計書.md
Master_Data_Quality・Integrity・Consistency設計書.md
Master_Compatibility・Evolution・Deprecation設計書.md
Master_Configuration・Feature_Flag・Override設計書.md
Master_Notification・Escalation・Communication設計書.md
Master_Scheduling・Calendar・Execution_Window設計書.md
Master_Cache・Index・Search・Lookup設計書.md
Master_Import・Export・Synchronization設計書.md
Master_Backup・Restore・Disaster_Recovery設計書.md
```

处理原则：

```text
不删除内容
不继续完善
不计入02_master当前完成度
不作为Runtime实现依据
以后有明确需求时重新审查
```

Compare Policy 以后确实开始进入 Loader、Registry、版本、CI、运维、备份、同步等 Master 平台级设计，而不是当前冻结的业务验证 Master 主线。fileciteturn15file10

---

# 七、第五阶段：完成 `02_master` 配套资产

根目录模板与核心设计完成后，才制作配套文件。

由于根目录文件本身已经是模板，所以当前**不再建立重复的 `templates/` 目录**。

最终建议结构为：

```text
system/
└── 02_master/
    ├── README.md
    │
    ├── E6_API_Master.md
    ├── UseCase_Master.md
    ├── Scenario_Master.md
    ├── Context_Master.md
    ├── Verification_Master.md
    ├── API_UseCase_Scenario対応表.md
    ├── Environment_Master.md
    ├── Verification_Policy_Master.md
    ├── Compare_Policy_Master.md
    │
    ├── design/
    │   └── 核心设计书
    │
    ├── guide/
    │   ├── Master作成・更新ガイド.md
    │   └── Master_ID・Reference記述ガイド.md
    │
    ├── checklist/
    │   ├── MasterレビューChecklist.md
    │   └── Master整合性Checklist.md
    │
    ├── examples/
    │   ├── E6_API_Master_Example.md
    │   ├── UseCase_Master_Example.md
    │   ├── Scenario_Master_Example.md
    │   ├── Context_Master_Example.md
    │   ├── Verification_Master_Example.md
    │   ├── API_UseCase_Scenario対応表_Example.md
    │   ├── Environment_Master_Example.md
    │   ├── Verification_Policy_Master_Example.md
    │   └── Compare_Policy_Master_Example.md
    │
    ├── schemas/
    │   ├── api-master.schema.json
    │   ├── usecase-master.schema.json
    │   ├── scenario-master.schema.json
    │   ├── context-master.schema.json
    │   ├── verification-master.schema.json
    │   ├── api-usecase-scenario-mapping.schema.json
    │   ├── environment-master.schema.json
    │   ├── verification-policy-master.schema.json
    │   └── compare-policy-master.schema.json
    │
    ├── definitions/
    │   ├── api-master.yml
    │   ├── usecase-master.yml
    │   ├── scenario-master.yml
    │   ├── context-master.yml
    │   ├── verification-master.yml
    │   ├── api-usecase-scenario-mapping.yml
    │   ├── environment-master.yml
    │   ├── verification-policy-master.yml
    │   └── compare-policy-master.yml
    │
    ├── validation/
    │   ├── master-reference-rules.yml
    │   ├── master-semantic-rules.yml
    │   └── master-validation-error-catalog.yml
    │
    └── samples/
        ├── valid/
        │   └── 各Master正常样例
        └── invalid/
            └── 各Master异常样例
```

---

## 配套资产制作顺序

### Step 5.1：重做 `README.md`

README 固定：

```text
目录结构
文件职责
正式文件名
状态
依赖关系
维护者
输入
输出
Review条件
冻结规则
禁止事项
```

### Step 5.2：制作 Guide 和 Checklist

先把人工填写、Review 和更新规则固定，避免后面的 Example、YAML、Schema各写一套。

### Step 5.3：制作 Markdown Examples

每个根目录模板一份完整填写例。

不能只放一两行数据，必须覆盖：

```text
正常
异常
Override
Disabled
Deprecated
Environment差异
Reference关系
```

### Step 5.4：制作 JSON Schema

先把机器约束固定：

```text
Required
Type
Enum
Pattern
Min / Max
Additional Properties
ID格式
Version格式
Reference格式
```

### Step 5.5：制作 YAML Definitions

它们是将来 Runtime 真正读取的数据。

```text
Markdown模板
    ↓ 人工／AI填写
YAML Definition
    ↓ Schema验证
Runtime加载
```

### Step 5.6：制作 Validation Rules

JSON Schema只能检查单文件结构，不能检查跨文件关系。

因此还必须验证：

```text
UseCase引用的API是否存在
Scenario引用的UseCase是否存在
对应表中的Scenario和API是否存在
Context Producer是否存在
Context Consumer是否存在
Verification引用的Policy是否存在
Compare Policy引用是否存在
Environment引用是否存在
ID是否重复
生命周期是否冲突
```

### Step 5.7：制作正常和异常 Sample

用于：

```text
Schema测试
Reference测试
Semantic测试
将来Loader测试
Codex实现参考
```

---

# 八、`02_master` 封板条件

只有以下项目全部满足，才能进入其他目录：

```text
□ Verification_Policy_Master.md已完成
□ 根目录模板清单已冻结
□ 所有文件名已统一
□ Business Master是否存在已决定
□ Variable Catalog是否存在已决定
□ 11份核心设计书已完成整合Review
□ Compare Policy之后的扩展设计已移出活动目录
□ README已按最终结构重做
□ 每个模板都有完整Example
□ 每个Runtime Definition都有Schema
□ 每个Schema都有正常／异常Sample
□ 跨Master Reference Validation已定义
□ 所有Critical Open Issue已关闭
□ Repo中的真实文件存在状态已确认
```

完成后，状态才可以写成：

```text
system/02_master
Status: FROZEN / REVIEW READY
```

不能因为对话里已经给过内容，就写成“已实际完成”。六个 Markdown 只能证明内容曾被输出，不能证明它已经写入 Git。fileciteturn14file15

---

# 九、`02_master` 完成后的整个 Repo 推进顺序

## Phase 6：更新 Repository 管理文件

```text
system/00_repository/Repository構成.md
system/00_repository/命名規約.md
system/00_repository/トレーサビリティ規約.md
project/WBS.md
project/スケジュール.md
```

目的：

```text
把最终02_master结构写回整个Repo基准
删除旧目录描述
更新完成／未完成状态
更新后续成果物顺序
```

---

## Phase 7：完成 `01_business`

顺序：

```text
7个业务Flow的现行业务分析
        ↓
业务分歧／Scenario一览
        ↓
24个API现行分析
        ↓
API依赖关系
        ↓
API调用顺序
        ↓
错误码、认证、共通规格
```

输出用于：

```text
02_master实际数据
03_api_design
04_usecase_design
```

---

## Phase 8：完成 `03_api_design`

先冻结：

```text
API設計書_Template.md
API設計書_Example.md
APIレビューChecklist.md
```

然后根据实际 API 分析生成：

```text
API-001～API-024
```

每个 API 必须明确：

```text
Request
Response
Header
Auth
Status Code
Error
Required
Type
Length
Fixed Value
Enum
Dynamic Field
Context Input / Output
Verification Target
Compare Target
```

---

## Phase 9：完成 `04_usecase_design`

先冻结：

```text
UseCase設計書_Template.md
UseCase設計書_Example.md
UseCaseレビューChecklist.md
```

再生成约 10 个实际 UseCase：

```text
Entry
Precondition
Scenario
API顺序
分支
Skip条件
Context Mapping
Expected Result
Cleanup
Data Impact
Environment限制
```

---

## Phase 10：重新审查 `05_framework`

不是直接沿用此前内容，也不是全部推翻。

处理方式：

```text
已有内容保留
    ↓
基于已冻结Master／API／UseCase重新Review
    ↓
修正职责、输入输出、数据结构
    ↓
再冻结
```

Review顺序：

```text
システム設計書
共通Framework設計書
RunContext設計書
Snapshot設計書
Diff設計書
Report設計書
ファイル入出力設計書
ログ・例外設計書
環境設計書
```

---

## Phase 11：完成 `06_verification_assets`

顺序：

```text
Verification仕様書
        ↓
API単体テスト仕様
        ↓
UseCaseテスト仕様
        ↓
Execution Spec
        ↓
Test Data
        ↓
Report Template
        ↓
Evidence Template
```

所有内容必须引用已冻结的：

```text
Master ID
API ID
UseCase ID
Scenario ID
Context ID
Verification ID
Policy ID
```

---

## Phase 12：Runtime 重新设计

只有到这里才恢复 Runtime。

此前 Runtime 是在上游尚未完全冻结时开始的，因此只能作为参考，不视为最终设计。历史对话确实曾在认为 `system/00～06` 已经基本齐全后直接进入 Runtime，这正是本次需要纠正的顺序。fileciteturn13file1

正确顺序：

```text
Runtime Architecture
Java Package / Class
Loader
Startup Validator
Planner
Runner
Request Builder
API Executor
Context Engine
Verification Engine
Snapshot
Diff
Report
Runtime Test
```

---

## Phase 13：实现与发布

```text
runtime/src
    ↓
Unit Test
    ↓
Integration Test
    ↓
build/scripts
    ↓
Docker
    ↓
staging
    ↓
Daily Execution
    ↓
outputs / reports / evidence
```

---

# 十、现在明确禁止做的事情

在 `02_master` 封板前，不做：

```text
× 不继续Master Migration设计
× 不继续Backup／Restore设计
× 不继续Cache／Search设计
× 不继续Notification／Scheduling设计
× 不继续Runtime设计
× 不写Java Class
× 不做Docker
× 不扩充新的Master类型
× 不重新改整个Repo编号
× 不进入实际24个API设计
```

---

# 本次新增或变更

本次没有新增文件内容，只冻结了推进规则：

```text
1. 确认02_master根目录文件是模板
2. 取消重复templates目录
3. 确认当前第一份文件是Verification_Policy_Master.md
4. 核心design截止到Compare_Policy_Master設計書.md
5. Compare Policy之后的设计全部移出当前主线
6. 02_master完成后再进入其他目录
```

# 下一份计划文件

```text
system/02_master/Verification_Policy_Master.md
```

它完成以后，下一步不是写新的设计书，而是进行：

```text
02_master根目录模板清单冻结Review
```

## 第 10 轮

### 你

按照你说的来

### ChatGPT

好，正式按这个顺序推进。现在只做第一件事：依据既有设计书和根目录模板格式，完成 `system/02_master/Verification_Policy_Master.md`，不继续其他目录。

### ChatGPT

已确认设计依据：Verification Policy 管理“如何判定”，Verification Master 管理“验证什么”，Compare Policy 管理与 Baseline 的差分；优先级也按个别定义、Group、Policy、Environment、Framework Default 处理。

下面直接给出当前第一份正式成果物。

### ChatGPT

第一份缺失模板正式补完如下。它沿用现有根目录 Master 的 `status: Template` 格式，并保留“模板＋完整记入例”的写法。现有 8 份根目录模板此前就是按这种方式制作的。fileciteturn13file0 fileciteturn15file5

**文件位置：**

```text
system/02_master/Verification_Policy_Master.md
```

:::writing{variant="document" id="60427"}
---
title: Verification Policy Master
document_id: MST-VPOL-001
version: 1.0.0
status: Template
document_type: Master
system_name: E6 API Verification Platform
phase: Master Definition
author:
reviewer:
approver:
created:
updated:
---

# Verification_Policy_Master

---

# 1. 文書目的

本書は、E6 API Verification Platform において使用する共通検証方式、既定値、正規化方式、許容差、結果判定、実行継続方針、Evidence 方針および Override 制御を一元管理するための Master Template である。

Verification Policy Master は、API、UseCase、Scenario、Request、Response および Context に依存しない、再利用可能な共通検証方針を定義する。

---

# 2. 責務

## 2.1 本Masterが管理する内容

本Masterは以下を管理する。

- Default Severity
- Default Failure Policy
- Missing Field Policy
- Null Policy
- Empty Value Policy
- Type Comparison Mode
- Type Coercion
- String Normalize
- Case Sensitivity
- Whitespace Policy
- Numeric Tolerance
- Decimal Scale
- Date／Datetime Tolerance
- Array Comparison Policy
- Object Comparison Policy
- Schema Validation Mode
- Verification Timeout
- Retry Policy
- Execution Continue／Stop Policy
- Result Aggregation Policy
- Evidence Capture Policy
- Environment Override
- Runtime Override
- Production Lock
- Policy Status
- Policy Version
- Effective Period
- Owner
- Traceability

---

## 2.2 本Masterが管理しない内容

本Masterでは以下を直接管理しない。

|管理対象外|正本|
|---|---|
|具体的な検証対象JSONPath|Verification Master|
|具体的なExpected Value|Verification Master|
|API別の固定値、Enum、Required|API設計書／Verification Master|
|Scenarioで実行するAPI順序|API・UseCase・Scenario対応表|
|API間の値受渡し|Context Master|
|CurrentとBaselineの差分方式|Compare Policy Master|
|実行対象の選択|Execution Specification|
|Runtime内部実装|Runtime設計書|

---

# 3. 他Masterとの責務境界

## 3.1 Verification Masterとの境界

|観点|Verification Master|Verification Policy Master|
|---|---|---|
|主目的|何を検証するかを定義する|どのように検証するかを定義する|
|対象Path|保持する|原則保持しない|
|Expected Value|保持する|原則保持しない|
|API依存|API／項目に依存する|原則として共通|
|再利用性|API、Step、項目単位|複数API、複数Verificationで再利用|
|Severity|個別指定またはPolicy参照|Default Severityを定義|
|Failure処理|個別Override可能|既定のFailure Policyを定義|
|Normalize|Policyを参照する|Normalize方式を定義|
|Tolerance|必要に応じて個別Override|既定のToleranceを定義|

---

## 3.2 Compare Policy Masterとの境界

|観点|Verification Policy Master|Compare Policy Master|
|---|---|---|
|主目的|現在値が期待仕様を満たすか判定|CurrentとBaselineの差分を判定|
|固定値確認|対象|対象外|
|Required確認|対象|差分として追加・削除を評価可能|
|Type確認|対象|Schema差分として評価可能|
|Enum確認|対象|Enum集合差分として評価可能|
|Numeric Tolerance|現在値検証用|Snapshot差分比較用|
|Dynamic項目除外|原則対象外|主対象|
|Array Key Match|現在値検証で必要な場合のみ|Baseline比較の主対象|
|Baseline選択|対象外|対象|

---

# 4. Policy一覧

## 4.1 記述ルール

- Policy ID は `VP-` で開始する。
- Policy ID はRepository内で一意とする。
- Policy名称は目的が分かる名称とする。
- API固有の値やJSONPathは原則として記載しない。
- Policyを緩和する場合は影響分析を実施する。
- Production適用PolicyはProduction Lockを設定する。
- Disabled、Deprecated、RetiredのPolicyを新規Verificationから参照してはならない。
- Verification Masterから参照されるPolicy IDは本一覧に存在しなければならない。

---

## 4.2 Policy一覧Template

|Policy ID|Policy名称|分類|適用Scope|主なVerification Type|Default Severity|Failure Policy|Environment Override|Runtime Override|Production Lock|Version|状態|Owner|備考|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|VP-XXX|（記載）|STANDARD / STRICT / LENIENT / SECURITY / CUSTOM|REQUEST / RESPONSE / CONTEXT / STEP / SCENARIO / USECASE / SCHEMA|（記載）|CRITICAL / HIGH / MEDIUM / LOW / INFO|FAIL_STEP / FAIL_SCENARIO / FAIL_USECASE / FAIL_RUN / WARN / CONTINUE|Allowed / Denied|Allowed / Denied|Enabled / Disabled|1.0.0|DRAFT / REVIEW / APPROVED / ACTIVE / DEPRECATED / RETIRED|（記載）|（記載）|

---

# 5. Policy基本情報

Policyごとに以下を記載する。

|項目|必須|内容|
|---|:---:|---|
|Policy ID|○|Policyを一意に識別するID|
|Policy名称|○|Policyの名称|
|説明|○|Policyの目的および適用意図|
|分類|○|STANDARD / STRICT / LENIENT / SECURITY / CUSTOM|
|Version|○|Semantic Versioning形式|
|状態|○|DRAFT / REVIEW / APPROVED / ACTIVE / DEPRECATED / RETIRED|
|Enabled|○|Policyが利用可能か|
|Owner|○|Policyの保守責任者|
|Reviewer|－|レビュー責任者|
|Approver|－|承認責任者|
|Effective From|－|適用開始日|
|Effective To|－|適用終了日|
|Replacement Policy ID|－|廃止時の移行先Policy|
|Source Reference|○|根拠となる仕様書、設計書、規約|
|備考|－|補足事項|

---

# 6. 適用Scope

## 6.1 Scope定義

|Scope|説明|
|---|---|
|API_REQUEST|API送信前のRequest検証|
|API_RESPONSE|API受信後のResponse検証|
|CONTEXT|Context登録後または参照前の検証|
|STEP|API Step単位の検証|
|SCENARIO|Scenario終了時の検証|
|USECASE|UseCase終了時の検証|
|SCHEMA|Request／Response Schema検証|
|TRANSITION|前後値および状態遷移検証|
|DIFF|差分結果に対する追加検証|
|SECURITY|機密情報、Mask、Evidence関連検証|

---

## 6.2 Scope設定Template

|Policy ID|適用Scope|適用Verification Type|対象環境|除外環境|優先度|備考|
|---|---|---|---|---|---:|---|
|VP-XXX|API_REQUEST, API_RESPONSE|REQUIRED, TYPE, FIXED_VALUE|ENV-DEV, ENV-STG|－|100|（記載）|

---

# 7. Default判定方針

## 7.1 Default設定Template

|Policy ID|Default Severity|Default Failure Policy|Validator Timeout|Evidence Required|Continue After Warning|Continue After Failure|備考|
|---|---|---|---:|---|---|---|---|
|VP-XXX|HIGH|FAIL_SCENARIO|1000ms|Yes|Yes|No|（記載）|

---

## 7.2 Severity定義

|Severity|定義|推奨Result|
|---|---|---|
|CRITICAL|検証継続または業務結果の信頼性を失う重大不一致|FAIL / ERROR|
|HIGH|API契約または主要業務結果に影響する不一致|FAIL|
|MEDIUM|確認が必要だが即時停止までは不要な不一致|WARN / FAIL|
|LOW|軽微な差異または参考情報|WARN|
|INFO|判定結果に影響しない情報|INFO|

---

## 7.3 Failure Policy定義

|Failure Policy|処理|
|---|---|
|CONTINUE|記録して後続処理を継続する|
|WARN|WARNとして記録し継続する|
|FAIL_STEP|現在のStepをFAILとして終了する|
|FAIL_SCENARIO|現在のScenarioをFAILとして終了する|
|FAIL_USECASE|現在のUseCaseをFAILとして終了する|
|FAIL_RUN|Run全体をFAILとして終了する|
|ERROR|定義不正またはRuntime異常として終了する|
|BLOCK|前提不足として実行対象をBLOCKEDにする|

---

# 8. Missing／Null／Empty Policy

## 8.1 定義

|種別|説明|
|---|---|
|Missing|対象PathまたはField自体が存在しない|
|Null|Fieldは存在するが値がNull|
|Empty String|文字列が空文字|
|Blank String|空白文字のみ|
|Empty Array|要素数0の配列|
|Empty Object|Propertyを持たないObject|

---

## 8.2 設定Template

|Policy ID|Required Missing|Optional Missing|Null|Empty String|Blank String|Empty Array|Empty Object|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|FAIL|PASS / WARN|FAIL / PASS|FAIL / PASS|FAIL / NORMALIZE|FAIL / PASS|FAIL / PASS|（記載）|

---

# 9. Type Policy

## 9.1 Type比較方式

|Mode|説明|
|---|---|
|STRICT|実際の型が期待型と完全一致すること|
|COMPATIBLE|互換性のある型変換を限定的に許可する|
|COERCE|許可された型変換後に比較する|
|SCHEMA_ONLY|Schema Validatorの型判定結果を使用する|

---

## 9.2 Type Coercion設定Template

|Policy ID|Type Mode|String→Number|Number→String|String→Boolean|String→Date|Integer→Decimal|Invalid Coercion Result|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|STRICT|Denied|Denied|Denied|Denied|Allowed / Denied|FAIL|（記載）|

---

# 10. String Policy

## 10.1 String Normalize設定Template

|Policy ID|Trim|Collapse Whitespace|Normalize Line Ending|Unicode Normalize|Case Sensitive|Empty After Normalize|Maximum Length|備考|
|---|---|---|---|---|---|---|---:|---|
|VP-XXX|Yes / No|Yes / No|Yes / No|NONE / NFC / NFKC|Yes / No|FAIL / PASS|（記載）|（記載）|

---

## 10.2 推奨ルール

- ID、Code、Tokenは原則Case Sensitiveとする。
- 表示名称は業務仕様によりCase Insensitiveを許可できる。
- Trimを使用する場合でもOriginal ValueをEvidenceへ保存できるようにする。
- NormalizeによってRequired違反が隠蔽されてはならない。
- Secret値をNormalize後の平文としてEvidenceへ保存してはならない。

---

# 11. Numeric Policy

## 11.1 Numeric設定Template

|Policy ID|Comparison Mode|Absolute Tolerance|Relative Tolerance|Decimal Scale|Rounding Mode|NaN許可|Infinity許可|備考|
|---|---|---:|---:|---:|---|---|---|---|
|VP-XXX|EXACT / TOLERANCE|0.00|0.00%|2|HALF_UP / HALF_EVEN / DOWN|No|No|（記載）|

---

## 11.2 Numeric判定ルール

- 金額は通貨ごとのScaleを考慮する。
- Toleranceは負数を禁止する。
- Absolute ToleranceとRelative Toleranceを同時使用する場合は判定順序を明確にする。
- 丸め前値と丸め後値をEvidenceへ記録できるようにする。
- Expected Value自体はVerification Masterで管理する。

---

# 12. Date／Datetime Policy

## 12.1 Date設定Template

|Policy ID|Input Format|Timezone|Normalize Timezone|Tolerance|Future許容|Past許容|Invalid Format Result|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|ISO-8601|UTC / Asia/Tokyo / Environment|UTC / None|±0秒|Yes / No|Yes / No|FAIL|（記載）|

---

## 12.2 Date判定ルール

- DateとDatetimeを混同しない。
- Timezoneが存在する値と存在しない値の比較方式を明確にする。
- Environment依存TimezoneはEnvironment Masterを参照する。
- 実行時刻との差を許容する場合はToleranceを明示する。
- Dynamic TimestampのBaseline差分除外はCompare Policy Masterで管理する。

---

# 13. Array／Object Policy

## 13.1 Array設定Template

|Policy ID|Order Sensitive|Comparison Mode|Key Path|Duplicate Key|Minimum Count|Maximum Count|Null Element|備考|
|---|---|---|---|---|---:|---:|---|---|
|VP-XXX|Yes / No|ORDER / SET / KEY_MATCH / CONTAINS|$.id|FAIL / WARN|0|（記載）|FAIL / PASS|（記載）|

---

## 13.2 Object設定Template

|Policy ID|Additional Property|Unknown Property Result|Property Order|Maximum Depth|Circular Reference|備考|
|---|---|---|---|---:|---|---|
|VP-XXX|Allowed / Denied / Schema Controlled|FAIL / WARN / IGNORE|Ignore|（記載）|Denied|（記載）|

---

# 14. Schema Validation Policy

## 14.1 Schema Mode

|Mode|説明|
|---|---|
|STRICT|Schemaに存在しないPropertyおよび型不一致をFAILとする|
|STANDARD|Required、Type、主要Constraintを検証する|
|LENIENT|重大なSchema違反のみFAILとする|
|DISABLED|Schema Validationを実行しない|

---

## 14.2 Schema設定Template

|Policy ID|Schema Mode|Required Check|Type Check|Format Check|Additional Property|Deprecated Field|Schema Error Result|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|STRICT|Yes|Yes|Yes|Denied|WARN / FAIL|FAIL|（記載）|

---

# 15. Execution Policy

## 15.1 実行制御Template

|Policy ID|Stop on First Failure|Maximum Failures|Maximum Warnings|Retry Count|Retry Interval|Retry Target|Timeout Result|備考|
|---|---|---:|---:|---:|---|---|---|---|
|VP-XXX|Yes / No|1|（記載）|0|0ms|TIMEOUT / TRANSIENT_ERROR|ERROR / FAIL|（記載）|

---

## 15.2 Retry制約

- 値不一致を理由とするVerification Retryは原則実施しない。
- Timeout、接続断、一時的な依存障害のみRetry候補とする。
- Retryによって副作用を重複発生させてはならない。
- 更新系APIに関するRetryはIdempotency保証を確認する。
- Retry回数および間隔は上限を設定する。

---

# 16. Result Aggregation Policy

## 16.1 集約Template

|Policy ID|Child ERROR|Child FAIL|Child WARN|All PASS|All SKIPPED|Mixed BLOCKED|Aggregation Result|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|ERROR|FAIL|WARN|PASS|SKIPPED|BLOCKED / WARN|Worst Result|（記載）|

---

## 16.2 Result優先順位

初期推奨順位：

```text
ERROR
  ↓
FAIL
  ↓
BLOCKED
  ↓
WARN
  ↓
PASS
  ↓
SKIPPED
  ↓
INFO
```

個別Policyで変更する場合は、Reportおよび運用判断への影響を明確化する。

---

# 17. Evidence Policy

## 17.1 Evidence設定Template

|Policy ID|Evidence Required|Expected Value|Actual Value|Original Value|Normalized Value|Source Path|Validator Info|Maximum Length|Sensitive Value|Secret Value|備考|
|---|---|---|---|---|---|---|---|---:|---|---|---|
|VP-XXX|Yes|Capture|Capture|Capture / None|Capture / None|Capture|Capture|1024|MASK / HASH / NONE|NONE|（記載）|

---

## 17.2 Evidence制約

- Password、Token、Secret Keyを平文保存してはならない。
- 個人情報はMaskまたはHashを適用する。
- Evidenceを削減するOverrideは原則禁止する。
- FAILおよびERRORは判定根拠を追跡できなければならない。
- Normalizeを適用した場合は、許可された範囲でOriginalとNormalizedを識別可能にする。

---

# 18. Override Policy

## 18.1 Override設定Template

|Policy ID|Environment Override|Verification Override|Group Override|Runtime Override|Severity Lowering|Failure Relaxation|Evidence Reduction|Strictness Reduction|Allowed Paths|備考|
|---|---|---|---|---|---|---|---|---|---|---|
|VP-XXX|Allowed|Allowed|Allowed|Denied|Denied|Denied|Denied|Denied|（記載）|（記載）|

---

## 18.2 Policy優先順位

Policy解決順序は以下とする。

```text
Verification Definition Override
  ↓
Verification Group Policy
  ↓
Verification Policy Master
  ↓
Environment Override
  ↓
Framework Default
```

ただし、以下は上位Overrideであっても緩和してはならない。

- Production Lock対象
- Security Policy
- Secret Evidence Policy
- Required Security Field
- Critical Verification
- Approval必須項目
- 法令または顧客規約に基づく制約

---

# 19. Environment Override

## 19.1 Environment別設定Template

|Policy ID|Environment ID|変更対象|Base Value|Override Value|理由|Production適用|承認者|備考|
|---|---|---|---|---|---|---|---|---|
|VP-XXX|ENV-DEV|schema.mode|STRICT|STANDARD|開発中API対応|No|（記載）|（記載）|

---

## 19.2 Environment Override制約

- Environment IDはEnvironment Masterに存在しなければならない。
- STGおよびPROD-LIKEでは原則としてDEVより厳格度を下げない。
- Production相当環境でLENIENTを使用する場合は明示承認を必須とする。
- Environment Overrideには理由、有効期間、承認者を記録する。
- 一時Overrideには失効日を設定する。

---

# 20. Production Lock

## 20.1 Production Lock設定Template

|Policy ID|Enabled|対象Environment|Locked Paths|Override禁止|Approval Required|備考|
|---|---|---|---|---|---|---|
|VP-XXX|Yes|ENV-PLK|defaults.severity, defaults.failurePolicy, evidence|Yes|Yes|（記載）|

---

## 20.2 Production Lock対象例

- Default Severity
- Failure Policy
- Required Missing Policy
- Type Coercion
- Numeric Tolerance
- Schema Mode
- Evidence Required
- Sensitive Value Policy
- Secret Value Policy
- Runtime Override
- Continue After Failure

---

# 21. Status・Lifecycle

## 21.1 Status定義

|Status|説明|新規参照|
|---|---|---|
|DRAFT|作成中|禁止|
|REVIEW|レビュー中|禁止|
|APPROVED|承認済み、適用待ち|条件付き|
|ACTIVE|利用可能|許可|
|DISABLED|一時停止|禁止|
|DEPRECATED|廃止予定|新規禁止|
|RETIRED|利用終了|禁止|

---

## 21.2 Version更新ルール

|変更種別|Version|
|---|---|
|Policyの意味、Null／Missing、Type Coercion、Production Lock変更|MAJOR|
|Scope追加、Verification Type追加、Environment Override追加|MINOR|
|説明、備考、参照資料の修正|PATCH|

---

# 22. Verification Master参照一覧

|Verification ID|Verification名称|Policy ID|Override有無|Override内容|対象Environment|備考|
|---|---|---|---|---|---|---|
|VER-XXX|（記載）|VP-XXX|Yes / No|（記載）|ENV-XXX|（記載）|

---

# 23. Policy整合性チェック

以下を確認する。

|Check ID|確認内容|不一致時Result|
|---|---|---|
|VP-CHK-001|Policy IDが一意である|ERROR|
|VP-CHK-002|参照Policyが存在する|ERROR|
|VP-CHK-003|Environment IDが存在する|ERROR|
|VP-CHK-004|Toleranceが0以上である|ERROR|
|VP-CHK-005|Decimal Scaleが許容範囲内である|ERROR|
|VP-CHK-006|Statusが有効値である|ERROR|
|VP-CHK-007|ACTIVE Policyが承認済みである|ERROR|
|VP-CHK-008|Deprecated PolicyにReplacementが設定されている|WARN / ERROR|
|VP-CHK-009|Production Lockが緩和されていない|ERROR|
|VP-CHK-010|Secret Evidenceが平文保存になっていない|ERROR|
|VP-CHK-011|Runtime Overrideが許可範囲内である|ERROR|
|VP-CHK-012|Effective Periodが矛盾していない|ERROR|

---

# 24. Policy一覧記入例

|Policy ID|Policy名称|分類|適用Scope|主なVerification Type|Default Severity|Failure Policy|Environment Override|Runtime Override|Production Lock|Version|状態|Owner|備考|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|VP-DEFAULT-STRICT|共通Strict Policy|STRICT|REQUEST, RESPONSE, CONTEXT|REQUIRED, TYPE, FORMAT, FIXED_VALUE, ENUM|HIGH|FAIL_SCENARIO|Allowed|Denied|Enabled|1.0.0|ACTIVE|verification-team|共通既定Policy|
|VP-REQUEST-STANDARD|Request標準検証Policy|STANDARD|API_REQUEST|REQUIRED, TYPE, LENGTH, PATTERN|HIGH|FAIL_STEP|Allowed|Denied|Enabled|1.0.0|ACTIVE|api-team|送信前検証|
|VP-RESPONSE-STRICT|Response厳格検証Policy|STRICT|API_RESPONSE, SCHEMA|REQUIRED, TYPE, ENUM, FIXED_VALUE, SCHEMA|HIGH|FAIL_SCENARIO|Allowed|Denied|Enabled|1.0.0|ACTIVE|verification-team|日次回帰標準|
|VP-CONTEXT-STRICT|Context厳格検証Policy|STRICT|CONTEXT|EXISTS, TYPE, NOT_EMPTY, FORMAT|CRITICAL|FAIL_SCENARIO|Denied|Denied|Enabled|1.0.0|ACTIVE|framework-team|後続API入力保証|
|VP-LOCAL-LENIENT|Local開発用Policy|LENIENT|REQUEST, RESPONSE, CONTEXT|TYPE, FORMAT, SCHEMA|MEDIUM|WARN|Allowed|Allowed|Disabled|1.0.0|ACTIVE|development-team|LOCAL限定|
|VP-PRODUCTION-CRITICAL|Production相当Critical Policy|STRICT|REQUEST, RESPONSE, CONTEXT, SCENARIO|ALL|CRITICAL|FAIL_RUN|Denied|Denied|Enabled|1.0.0|ACTIVE|platform-owner|PROD-LIKE限定|
|VP-SENSITIVE-DATA|機密情報検証Policy|SECURITY|REQUEST, RESPONSE, CONTEXT, SECURITY|MASK, EVIDENCE, REQUIRED|HIGH|FAIL_SCENARIO|Denied|Denied|Enabled|1.0.0|ACTIVE|security-team|機密値Evidence制御|

---

# 25. 詳細記入例：VP-RESPONSE-STRICT

## 25.1 基本情報

|項目|内容|
|---|---|
|Policy ID|VP-RESPONSE-STRICT|
|Policy名称|Response厳格検証Policy|
|説明|E6 APIのResponse契約を厳格に検証する共通Policy|
|分類|STRICT|
|Version|1.0.0|
|状態|ACTIVE|
|Enabled|Yes|
|Owner|verification-team|
|Reviewer|api-architect|
|Approver|verification-platform-owner|
|Effective From|2026-08-01|
|Effective To|－|
|Replacement Policy ID|－|

---

## 25.2 Scope

|項目|内容|
|---|---|
|適用Scope|API_RESPONSE, SCHEMA|
|Verification Type|REQUIRED, TYPE, LENGTH, PATTERN, ENUM, FIXED_VALUE, SCHEMA|
|対象環境|ENV-STG, ENV-PLK|
|除外環境|ENV-LOCAL|
|優先度|200|

---

## 25.3 Default

|項目|内容|
|---|---|
|Default Severity|HIGH|
|Default Failure Policy|FAIL_SCENARIO|
|Validator Timeout|1000ms|
|Evidence Required|Yes|
|Continue After Warning|Yes|
|Continue After Failure|No|

---

## 25.4 Missing／Null／Empty

|項目|内容|
|---|---|
|Required Missing|FAIL|
|Optional Missing|PASS|
|Null|仕様定義に従う|
|Empty String|仕様定義に従う|
|Blank String|Trim後に再評価|
|Empty Array|Minimum Countに従う|
|Empty Object|Schemaに従う|

---

## 25.5 Type／String／Numeric

|項目|内容|
|---|---|
|Type Mode|STRICT|
|Type Coercion|Denied|
|Trim|No|
|Case Sensitive|Yes|
|Unicode Normalize|NFC|
|Numeric Comparison|EXACT|
|Absolute Tolerance|0|
|Decimal Scale|API設計書に従う|

---

## 25.6 Date／Array／Schema

|項目|内容|
|---|---|
|Date Format|ISO-8601|
|Timezone|値に含まれるTimezoneを使用|
|Datetime Tolerance|0秒|
|Array Order Sensitive|API設計書に従う|
|Array Duplicate Key|FAIL|
|Schema Mode|STRICT|
|Additional Property|Denied|
|Schema Error Result|FAIL|

---

## 25.7 Evidence

|項目|内容|
|---|---|
|Expected Value|Capture|
|Actual Value|Capture|
|Original Value|Capture|
|Normalized Value|Capture|
|Source Path|Capture|
|Validator Information|Capture|
|Maximum Value Length|1024|
|Sensitive Value|MASK|
|Secret Value|NONE|

---

## 25.8 Override／Production Lock

|項目|内容|
|---|---|
|Environment Override|Allowed|
|Verification Override|Allowed|
|Runtime Override|Denied|
|Severity Lowering|Denied|
|Failure Relaxation|Denied|
|Evidence Reduction|Denied|
|Strictness Reduction|Denied|
|Production Lock|Enabled|
|Locked Paths|defaults.severity, defaults.failurePolicy, schema, evidence|

---

# 26. 詳細記入例：VP-LOCAL-LENIENT

|項目|内容|
|---|---|
|Policy ID|VP-LOCAL-LENIENT|
|Policy名称|Local開発用緩和Policy|
|分類|LENIENT|
|適用Scope|API_REQUEST, API_RESPONSE, CONTEXT|
|対象環境|ENV-LOCAL|
|Default Severity|MEDIUM|
|Failure Policy|WARN|
|Type Mode|COMPATIBLE|
|String Trim|Yes|
|Case Sensitive|No|
|Schema Mode|STANDARD|
|Additional Property|Allowed|
|Evidence Required|Yes|
|Runtime Override|Allowed|
|Production Lock|Disabled|
|状態|ACTIVE|
|備考|ENV-LOCAL以外での使用禁止|

---

# 27. 詳細記入例：VP-SENSITIVE-DATA

|項目|内容|
|---|---|
|Policy ID|VP-SENSITIVE-DATA|
|Policy名称|機密情報検証Policy|
|分類|SECURITY|
|適用Scope|API_REQUEST, API_RESPONSE, CONTEXT, SECURITY|
|Default Severity|HIGH|
|Failure Policy|FAIL_SCENARIO|
|Evidence Required|Yes|
|Expected Value|MASK|
|Actual Value|MASK|
|Original Value|NONE|
|Normalized Value|NONE|
|Sensitive Value Policy|MASK|
|Secret Value Policy|NONE|
|Runtime Override|Denied|
|Evidence Reduction|Denied|
|Production Lock|Enabled|
|Owner|security-team|
|状態|ACTIVE|

---

# 28. Review Checklist

## 28.1 文書チェック

```text
□ Metadataが記載されている
□ Policy IDが一意である
□ Policy名称と目的が一致している
□ Owner、Reviewer、Approverが明確である
□ VersionとStatusが適切である
□ Effective Periodが矛盾していない
```

## 28.2 責務チェック

```text
□ Verification Masterの具体的Expected Valueを重複管理していない
□ Compare Policy MasterのBaseline差分Ruleを重複管理していない
□ API固有JSONPathを共通Policyへ持ち込んでいない
□ Environment Masterとの参照関係が明確である
```

## 28.3 判定チェック

```text
□ Missing、Null、Emptyの違いが明確である
□ Type ModeとType Coercionが明確である
□ String Normalizeが明確である
□ Numeric Toleranceが0以上である
□ Date／Datetime Toleranceが明確である
□ Array比較方式が明確である
□ Schema Modeが明確である
□ Result Aggregationが明確である
```

## 28.4 実行制御チェック

```text
□ Failure Policyが明確である
□ Stop／Continue条件が明確である
□ Retry対象が一時障害に限定されている
□ Timeoutが設定されている
□ Verification結果による停止範囲が明確である
```

## 28.5 Overrideチェック

```text
□ Override可能な項目が明確である
□ Severityを不正に低下できない
□ Failure Policyを不正に緩和できない
□ Evidenceを不正に削減できない
□ Runtime Overrideの許可範囲が明確である
□ Production Lockが設定されている
```

## 28.6 Securityチェック

```text
□ Secret値を平文保存しない
□ Sensitive値にMaskまたはHashを適用する
□ Security PolicyをRuntime Overrideできない
□ ProductionでLENIENT Policyを無承認使用できない
□ Evidenceから機密情報が漏えいしない
```

---

# 29. 完了条件

本Master Templateは以下を満たした場合に完成とする。

```text
□ Verification Policyの責務が明確である
□ Verification Masterとの境界が明確である
□ Compare Policy Masterとの境界が明確である
□ Policy一覧Templateが存在する
□ Policy詳細項目が定義されている
□ Missing／Null／Empty Policyが定義されている
□ Type／String／Numeric／Date Policyが定義されている
□ Array／Object／Schema Policyが定義されている
□ Failure／Execution／Aggregation Policyが定義されている
□ Evidence Policyが定義されている
□ Environment Overrideが定義されている
□ Production Lockが定義されている
□ 完整な記入例が存在する
□ Review Checklistが存在する
□ Verification_Policy_Master設計書と矛盾しない
```
:::

## `system/02_master/` 当前完整状态

```text
system/
└── 02_master/
    │
    ├── README.md
    │   ├── 状态：需要重做
    │   └── 仓库写入：待确认
    │
    ├── E6_API_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── UseCase_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── Scenario_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── Context_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── Verification_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── API_UseCase_Scenario対応表.md
    │   ├── 状态：已给出内容／文件名待冻结
    │   └── 仓库写入：待确认
    ├── Compare_Policy_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── Environment_Master.md
    │   ├── 状态：已给出内容／待Review
    │   └── 仓库写入：待确认
    ├── Verification_Policy_Master.md
    │   ├── 状态：本次已给出完整内容
    │   └── 仓库写入：尚未确认
    │
    ├── Business_Master.md
    │   └── 状态：待确认是否纳入冻结范围
    ├── Variable_Catalog_Master.md
    │   └── 状态：待确认是否由Context_Master代替
    │
    ├── design/
    │   ├── Master共通設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── Business_Master設計書.md
    │   │   └── 已给出内容／保留与否待确认
    │   ├── Environment_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── API_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── UseCase_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── Scenario_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── API・UseCase・Scenario対応表設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── Context_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── Verification_Master設計書.md
    │   │   └── 已给出内容／待整合Review
    │   ├── Verification_Policy_Master設計書.md
    │   │   └── 已给出内容／本次模板已据此补完
    │   └── Compare_Policy_Master設計書.md
    │       └── 已给出内容／冻结核心设计最后一份
    │
    ├── guide/
    │   ├── Master作成・更新ガイド.md
    │   │   └── 未完成
    │   └── Master_ID・Reference記述ガイド.md
    │       └── 未完成
    │
    ├── checklist/
    │   ├── MasterレビューChecklist.md
    │   │   └── 未完成
    │   └── Master整合性Checklist.md
    │       └── 未完成
    │
    ├── examples/
    │   ├── E6_API_Master_Example.md
    │   ├── UseCase_Master_Example.md
    │   ├── Scenario_Master_Example.md
    │   ├── Context_Master_Example.md
    │   ├── Verification_Master_Example.md
    │   ├── API_UseCase_Scenario対応表_Example.md
    │   ├── Environment_Master_Example.md
    │   ├── Verification_Policy_Master_Example.md
    │   └── Compare_Policy_Master_Example.md
    │       └── 全部未独立制作
    │
    ├── definitions/
    │   ├── api-master.yml
    │   ├── usecase-master.yml
    │   ├── scenario-master.yml
    │   ├── context-master.yml
    │   ├── verification-master.yml
    │   ├── api-usecase-scenario-mapping.yml
    │   ├── environment-master.yml
    │   ├── verification-policy-master.yml
    │   └── compare-policy-master.yml
    │       └── 全部未完成
    │
    ├── schemas/
    │   ├── api-master.schema.json
    │   ├── usecase-master.schema.json
    │   ├── scenario-master.schema.json
    │   ├── context-master.schema.json
    │   ├── verification-master.schema.json
    │   ├── api-usecase-scenario-mapping.schema.json
    │   ├── environment-master.schema.json
    │   ├── verification-policy-master.schema.json
    │   └── compare-policy-master.schema.json
    │       └── 全部未完成
    │
    ├── validation/
    │   ├── master-reference-rules.yml
    │   ├── master-semantic-rules.yml
    │   └── master-validation-error-catalog.yml
    │       └── 全部未完成
    │
    └── samples/
        ├── valid/
        │   └── 各Master正常样例：未完成
        └── invalid/
            └── 各Master异常样例：未完成
```

## 本次新增或变更

```text
新增完整内容：
system/02_master/Verification_Policy_Master.md

状态变化：
未完成
  ↓
已给出完整内容／待实际写入仓库
```

至此，最初约定的根目录 8 份已有模板，加上缺失的 `Verification_Policy_Master.md`，内容层面已补齐为 9 份。该模板覆盖了设计书要求的 Missing、Null、Type、Normalize、Tolerance、Evidence、Override、Production Lock 等主要政策项。fileciteturn15file0

## 下一步

下一步先执行：

```text
02_master根目录模板冻结Review
```

Review结束后，下一份实际重做文件是：

```text
system/02_master/README.md
```

在根目录文件名、`Business_Master` 和 `Variable_Catalog_Master` 是否保留尚未决定前，不提前重写 README。
