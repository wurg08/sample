# API流程验证设计

- 来源: https://chatgpt.com/c/6a30db25-a6bc-83e8-ba19-4bc5fc0a5e28
- 导出时间: 2026-07-02T13:38:06+09:00
- 分片: 1/2
- 总消息数: 210
- 总轮数: 91

## 第 1 轮

### 你

要做一个验证api调用的验证agent
比如有一个业务 需要按业务先后顺序连续调用多个api
要求
1.第一个api是入口 参数可以随意制定 后面的api可能会按照条件来设定 也可以手动指定
2.我需要验证每个api
2.1 调用是否成功 status code确认
2.2 request的参数个数 类型 长度 必须 存在等是否有变化
2.3 response也是一样 返回的项目个数 类型 长度等和之前是否有变化
2.4 返回值的变化 比如上版本是0、1 之后变成了1、2等
3.每次执行都要生成一版确认结果一览表 把确认的时间 api request url post等请求信息 各个项目 设定的值 已经返回的类型 值 包括和之前版本差异判断
4.利用方法 用户填写api的测试数据一览等 作为入力条件 你可以安装这个文档自己去跑完所有的api并且生成结果

帮我设计一下

### ChatGPT

我会按“工业可落地”的方式设计：先定义 Agent 职责边界，再设计输入文件、执行流程、差异比对、结果表、目录结构和给 Codex 的实现任务。

### ChatGPT

可以。这个应该设计成 **API业务流程验证 Agent**，不是单纯接口测试工具。核心目标是：

**用户只维护一份“业务流程测试数据一览”，Agent 自动按业务顺序调用多个 API，记录 request / response / schema / value / 差异，并生成每次验证报告。**

---

# 1. Agent 定位

## 名称

`api_flow_validation_agent`

## 目标

验证一个业务流程中多个 API 的连续调用是否仍然正确。

它要验证：

1. API 是否调用成功
2. request 参数结构是否变化
3. response 返回结构是否变化
4. 字段类型、长度、必填、枚举值是否变化
5. 返回值是否和前一版本不同
6. 后续 API 参数是否能从前面 API response 中自动取得
7. 每次执行生成一版验证结果表
8. 支持和上次执行结果、基准版本、指定版本进行 diff

---

# 2. 整体架构

```text
用户填写测试数据一览
        ↓
Input Loader
读取 Excel / YAML / JSON 测试定义
        ↓
Flow Planner
按业务顺序生成 API 调用计划
        ↓
Param Resolver
解析参数：固定值 / 手动值 / 前序 API 返回值 / 条件值
        ↓
API Executor
实际调用 API
        ↓
Request Validator
检查 request 参数个数、类型、长度、必填、枚举
        ↓
Response Validator
检查 response 字段、类型、长度、必填、枚举、值域
        ↓
Diff Engine
和上一版 / 基准版比较
        ↓
Report Generator
生成 Excel / HTML / JSON / Markdown 报告
        ↓
Evidence Store
保存每次执行证迹
```

---

# 3. 用户输入文件设计

建议用户主要维护一个 Excel。

## 3.1 API流程定义 Sheet：`api_flow`

| flow_id | step_no | api_id | name | method | url | enabled | depends_on | condition | retry |
|---|---:|---|---|---|---|---|---|---|---:|
| order_create | 1 | login | 登录 | POST | /auth/login | Y |  |  | 0 |
| order_create | 2 | create_order | 创建订单 | POST | /orders | Y | login | $.login.response.status == 200 | 0 |
| order_create | 3 | get_order | 查询订单 | GET | /orders/{order_id} | Y | create_order |  | 0 |

说明：

- `step_no` 控制调用顺序
- `depends_on` 表示依赖哪个 API
- `condition` 表示条件执行
- `enabled` 可以临时跳过某个 API

---

## 3.2 请求参数定义 Sheet：`request_params`

| api_id | param_location | name | required | type | max_length | value_source | value | json_path | enum |
|---|---|---|---|---|---:|---|---|---|---|
| login | body | userId | Y | string | 20 | manual | test01 |  |  |
| login | body | password | Y | string | 50 | manual | pass123 |  |  |
| create_order | header | Authorization | Y | string | 300 | previous_response |  | $.login.response.body.token |  |
| create_order | body | productCode | Y | string | 20 | manual | P001 |  |  |
| get_order | path | order_id | Y | string | 50 | previous_response |  | $.create_order.response.body.orderId |  |

`value_source` 支持：

```text
manual              用户手动指定
fixed               固定值
previous_response   从前面 API response 取得
previous_request    从前面 API request 取得
env                 从环境变量取得
generated           自动生成
condition           按条件设定
```

---

## 3.3 Response 期待定义 Sheet：`response_expectation`

| api_id | json_path | required | type | max_length | enum | compare_value | description |
|---|---|---|---|---:|---|---|---|
| login | $.token | Y | string | 300 |  | N | 登录token |
| login | $.user.status | Y | number | 1 | 0,1 | Y | 用户状态 |
| create_order | $.orderId | Y | string | 50 |  | N | 订单ID |
| create_order | $.status | Y | number | 1 | 0,1 | Y | 订单状态 |

`compare_value`：

```text
Y：和上一版比较实际返回值
N：只比较结构，不比较值
```

---

## 3.4 测试场景 Sheet：`test_cases`

| case_id | flow_id | case_name | env | base_version | compare_target | enabled |
|---|---|---|---|---|---|---|
| TC001 | order_create | 正常订单创建流程 | dev | 20260601_100000 | latest | Y |
| TC002 | order_create | 商品不存在 | dev | 20260601_100000 | latest | Y |

---

# 4. Agent 执行逻辑

## 4.1 第一个 API 是入口

第一个 API 的参数允许用户自由设定：

```text
step_no = 1
value_source = manual / fixed / generated
```

例如：

```text
login.userId = test01
login.password = pass123
```

---

## 4.2 后续 API 参数来源

后续 API 可以：

### 自动从前一个 API response 取得

```text
create_order.header.Authorization
= $.login.response.body.token
```

### 从多个前序 API 取得

```text
confirm_payment.body.orderId
= $.create_order.response.body.orderId

confirm_payment.body.paymentId
= $.create_payment.response.body.paymentId
```

### 用户手动指定

```text
create_order.body.productCode = P001
```

### 条件设定

```text
if $.login.response.body.userType == "admin"
then approvalType = "AUTO"
else approvalType = "MANUAL"
```

---

# 5. 每个 API 的验证内容

## 5.1 Status Code 验证

检查：

```text
实际 status code
期待 status code
是否成功
是否和上一版不同
```

结果例：

| api_id | expected_status | actual_status | result | diff |
|---|---:|---:|---|---|
| login | 200 | 200 | OK | 无 |
| create_order | 200 | 500 | NG | 由200变为500 |

---

## 5.2 Request 参数验证

检查：

```text
参数是否存在
参数个数是否变化
字段名是否变化
类型是否变化
长度是否变化
必填是否变化
enum 是否变化
实际传入值是什么
```

例：

| api_id | location | field | expected_type | actual_type | expected_required | actual_exists | value | result | diff |
|---|---|---|---|---|---|---|---|---|---|
| create_order | body | productCode | string | string | Y | Y | P001 | OK | 无 |
| create_order | body | quantity | number | missing | Y | N |  | NG | 字段消失 |

---

## 5.3 Response 结构验证

检查：

```text
字段是否存在
字段个数是否变化
字段类型是否变化
字段长度是否变化
必填字段是否返回
enum 是否变化
数组长度是否变化
object 结构是否变化
```

例：

| api_id | json_path | expected_type | actual_type | expected_length | actual_length | result | diff |
|---|---|---|---|---:|---:|---|---|
| login | $.token | string | string | 300 | 128 | OK | 无 |
| login | $.user.status | number | number | 1 | 1 | OK | enum变化：0,1 → 1,2 |
| create_order | $.orderId | string | missing | 50 | 0 | NG | 字段消失 |

---

## 5.4 返回值变化验证

比如上版本：

```json
{
  "status": 0
}
```

新版本：

```json
{
  "status": 2
}
```

则报告：

```text
字段：$.status
旧值：0
新值：2
判断：变化
风险：enum / 业务状态码可能变化
```

---

# 6. 差异判断规则

## 6.1 Schema Diff

比较：

```text
字段新增
字段删除
字段类型变化
字段最大长度变化
字段必填变化
数组结构变化
object 层级变化
```

## 6.2 Value Diff

比较：

```text
返回值是否变化
枚举值集合是否变化
null / 非 null 是否变化
空数组 / 有数据是否变化
固定业务状态是否变化
```

## 6.3 Request Diff

比较：

```text
请求 URL 是否变化
method 是否变化
header 是否变化
body 字段是否变化
query 参数是否变化
path 参数是否变化
实际传入值是否变化
```

---

# 7. 每次执行生成的结果

建议每次执行生成一个目录：

```text
runs/
  20260616_153000_TC001/
    input/
      api_test_definition.xlsx
    raw/
      01_login_request.json
      01_login_response.json
      02_create_order_request.json
      02_create_order_response.json
    normalized/
      request_schema.json
      response_schema.json
      api_trace.json
    diff/
      diff_against_previous.json
      diff_against_baseline.json
    reports/
      result_summary.xlsx
      result_detail.xlsx
      result_report.html
      result_report.md
```

---

# 8. 结果一览表设计

## Sheet 1：执行概要 `summary`

| 执行时间 | case_id | flow_id | 环境 | 总API数 | 成功 | 失败 | 差异数 | 结果 |
|---|---|---|---|---:|---:|---:|---:|---|
| 2026-06-16 15:30 | TC001 | order_create | dev | 3 | 2 | 1 | 5 | NG |

---

## Sheet 2：API调用结果 `api_result`

| step | api_id | method | url | status | elapsed_ms | result | error |
|---:|---|---|---|---:|---:|---|---|
| 1 | login | POST | /auth/login | 200 | 320 | OK |  |
| 2 | create_order | POST | /orders | 200 | 510 | OK |  |
| 3 | get_order | GET | /orders/{order_id} | 404 | 120 | NG | order not found |

---

## Sheet 3：Request确认结果 `request_check`

| api_id | location | field | expected_type | actual_type | required | exists | value | length | result | diff |
|---|---|---|---|---|---|---|---|---:|---|---|

---

## Sheet 4：Response确认结果 `response_check`

| api_id | json_path | expected_type | actual_type | required | exists | value | length | result | diff |
|---|---|---|---|---|---|---|---:|---|---|

---

## Sheet 5：差异一览 `diff_summary`

| api_id | target | field | diff_type | before | after | severity | comment |
|---|---|---|---|---|---|---|---|
| login | response | $.user.status | enum_changed | 0,1 | 1,2 | HIGH | 业务状态码变化 |
| create_order | response | $.orderId | removed | exists | missing | HIGH | 必须字段消失 |

---

# 9. 严重度规则

```text
HIGH:
- status code 变为非成功
- 必须字段消失
- 字段类型变化
- enum 删除或业务状态变化
- 后续 API 参数无法解析

MEDIUM:
- 新增字段
- 长度变化
- null / 非 null 变化
- 数组数量变化

LOW:
- 非关键返回值变化
- 响应时间变化
- 字段顺序变化
```

---

# 10. Agent 内部模块

```text
api_flow_validation_agent/
  README.md
  config/
    env.dev.yaml
    env.stg.yaml
  inputs/
    api_test_definition.xlsx
  src/
    agent.py
    input_loader.py
    flow_planner.py
    param_resolver.py
    api_executor.py
    request_validator.py
    response_validator.py
    schema_extractor.py
    diff_engine.py
    report_generator.py
    evidence_store.py
  templates/
    result_summary_template.xlsx
    report_template.html
  runs/
  tests/
```

---

# 11. 核心 JSON 数据结构

## API执行轨迹

```json
{
  "run_id": "20260616_153000_TC001",
  "case_id": "TC001",
  "flow_id": "order_create",
  "steps": [
    {
      "step_no": 1,
      "api_id": "login",
      "method": "POST",
      "url": "/auth/login",
      "request": {
        "headers": {},
        "body": {
          "userId": "test01",
          "password": "pass123"
        }
      },
      "response": {
        "status_code": 200,
        "body": {
          "token": "xxxxx",
          "user": {
            "status": 1
          }
        }
      },
      "result": "OK"
    }
  ]
}
```

---

# 12. 这个 Agent 最重要的能力

不是“能不能调 API”。

真正重要的是：

```text
1. API业务流程编排
2. 前后 API 参数传递
3. request / response 自动结构化
4. 每次执行证迹保存
5. 和历史版本自动比较
6. 输出业务人员能看的确认表
```

---

# 13. 推荐先实现顺序

## Phase 1：基础执行

```text
读取 Excel
按 step_no 调用 API
保存 request / response
生成 summary.xlsx
```

## Phase 2：参数传递

```text
支持 previous_response json_path
支持 path/query/header/body 参数
支持条件执行
```

## Phase 3：结构验证

```text
request schema 检查
response schema 检查
字段存在、类型、长度、必填检查
```

## Phase 4：差异比较

```text
和上次执行比较
和 baseline 比较
生成 diff_summary
```

## Phase 5：工业化

```text
HTML报告
失败重试
敏感信息mask
CI/CD集成
Slack/邮件通知
历史版本管理
```

---

# 14. 给 Codex 的一句话任务

可以这样给 Codex：

```text
请实现一个 api_flow_validation_agent。
它读取用户维护的 api_test_definition.xlsx，按照 api_flow sheet 中定义的业务顺序连续调用多个 API。
第一个 API 作为入口，参数由用户手动或固定指定。
后续 API 的参数可以从前序 API 的 response/request 中通过 JSONPath 自动取得，也可以手动指定。
每个 API 调用后，需要保存 request、response、status code、执行时间。
系统需要验证 request 和 response 的字段存在性、类型、长度、必填、enum、实际值，并和上一版或 baseline 执行结果进行差异比较。
每次执行必须生成 result_summary.xlsx、result_detail.xlsx、result_report.html，并保存完整 raw evidence。
请按照工业级目录结构、模块边界、测试用例、错误处理和可扩展设计实现。
```

---

结论：
这个 Agent 应该做成 **“API业务流程回归验证 + Schema差异检测 + 结果证迹生成”** 的工具。
用户只负责维护测试数据一览，Agent 负责自动跑流程、自动比对、自动出确认表。

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "6a48482f-55e9-4750-bd4a-4246b231f1e0"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 2 ～ 3 秒"
}
```

## 第 2 轮

### 你

调用的是e6 developer 的api

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "b6b5bdbd-3ce0-461e-bb68-3394b7a1664f"
}
```

### ChatGPT

如果是 **Episode Six / E6 Developer API**，这个 Agent 需要偏向 **支付/账户/ledger 业务流程验证**。E6 官方开发者门户定位是用 API 管理 payments、ledgers、accounts 等能力。citeturn962265search0

你这个设计可以补强成：

```text
e6_api_flow_validation_agent
```

重点增加：

1. **认证层**
   - API Key / Bearer Token / OAuth
   - tenant / program / account / customer 等上下文参数
   - token 自动刷新

2. **业务流程模板**
   - customer 创建
   - account 创建
   - ledger 查询
   - card / payment instrument 创建
   - transaction / authorization / settlement
   - balance 查询

3. **E6 专用校验**
   - 金额字段精度
   - currency
   - ledger balance 前后变化
   - transaction status 状态迁移
   - account status / card status enum 变化
   - idempotency key
   - requestId / correlationId

4. **结果表增加 E6 字段**

```text
program_id
customer_id
account_id
ledger_id
transaction_id
currency
amount
balance_before
balance_after
transaction_status
```

5. **业务链路例子**

```text
1. authenticate
2. create customer
3. create account
4. create ledger / wallet
5. fund account
6. create transaction
7. query transaction
8. query balance
```

6. **更重要的验证点**

```text
不是只看 status code = 200
还要验证：
- 交易状态是否正确
- balance 是否按金额正确变化
- currency 是否一致
- ledger entry 是否成对
- failed transaction 是否不会改变余额
- enum 是否从 old set 变成 new set
```

也就是说，这个 Agent 应该命名为：

```text
E6 Business API Regression Validation Agent
```

定位是：

```text
针对 Episode Six API 的业务流程级自动回归验证工具。
用户维护测试数据一览，Agent 自动调用 E6 API，验证 customer / account / ledger / transaction 等业务链路，并生成 request、response、balance、status、enum、schema 差异确认表。
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 4s"
}
```

## 第 3 轮

### 你

可能这个不能适应agent 能作为python 工具 实现执行吗

### ChatGPT

可以，**完全可以先不做 Agent，先做成 Python 执行工具**。
而且我建议你第一版就应该做成 Python 工具，Agent 只是后面包一层。

最合理结构是：

```text
用户 Excel 测试数据一览
        ↓
Python CLI 工具执行
        ↓
连续调用 E6 Developer API
        ↓
保存 request / response / diff
        ↓
生成 Excel 确认结果一览
```

---

# 推荐定位

不要一开始叫 Agent，先叫：

```text
e6_api_flow_validator
```

它是一个 Python 命令行工具。

执行方式：

```bash
python -m e6_api_flow_validator run \
  --input ./inputs/e6_api_test_definition.xlsx \
  --env dev \
  --case TC001 \
  --compare latest
```

---

# Python 工具职责

## 1. 读取测试定义

从 Excel 读取：

```text
api_flow
request_params
response_expectation
test_cases
env_config
```

---

## 2. 按业务顺序调用 API

例如：

```text
1. login / token
2. create customer
3. create account
4. create ledger
5. execute transaction
6. query transaction
7. query balance
```

---

## 3. 后续 API 参数自动继承

比如：

```text
create_account.customer_id
= 上一步 create_customer.response.customerId
```

用 JSONPath 表达：

```text
$.create_customer.response.body.customerId
```

---

## 4. 保存证迹

每一步都保存：

```text
request url
method
headers
body
status code
response body
elapsed time
error
```

目录：

```text
runs/
  20260616_160000_TC001/
    raw/
      01_create_customer_request.json
      01_create_customer_response.json
    reports/
      result_summary.xlsx
      result_detail.xlsx
```

---

## 5. 自动检查 request / response

检查：

```text
字段是否存在
字段数量
字段类型
字段长度
必填
enum
实际值
和上次差异
```

---

# Python 项目结构

```text
e6_api_flow_validator/
  pyproject.toml
  README.md

  inputs/
    e6_api_test_definition.xlsx

  config/
    dev.yaml
    stg.yaml

  src/
    e6_api_flow_validator/
      __init__.py
      cli.py
      input_loader.py
      flow_runner.py
      param_resolver.py
      api_client.py
      validators.py
      diff_engine.py
      report_writer.py
      evidence_store.py
      masking.py
      errors.py

  runs/

  tests/
    test_param_resolver.py
    test_diff_engine.py
    test_validators.py
```

---

# 核心模块说明

## `cli.py`

负责命令行入口。

```bash
e6-validator run --input xxx.xlsx --env dev --case TC001
```

---

## `input_loader.py`

读取 Excel。

```python
load_api_flow()
load_request_params()
load_response_expectation()
load_test_cases()
```

---

## `flow_runner.py`

负责流程编排。

```text
按 step_no 排序
判断 enabled
判断 condition
调用 param_resolver
调用 api_client
调用 validator
保存 evidence
```

---

## `param_resolver.py`

负责参数解析。

支持：

```text
manual
fixed
previous_response
previous_request
env
generated
condition
```

---

## `api_client.py`

真正调用 E6 API。

建议用：

```python
httpx
```

不要用 requests。
因为 httpx 更适合后面扩展异步、timeout、retry、日志。

---

## `validators.py`

验证：

```text
status code
request 字段
response 字段
type
length
required
enum
value
```

---

## `diff_engine.py`

和上一版比较。

比较对象：

```text
status code
request schema
response schema
response value
enum set
字段新增/删除
```

---

## `report_writer.py`

生成 Excel。

建议用：

```python
openpyxl
```

生成：

```text
summary
api_result
request_check
response_check
diff_summary
raw_value
```

---

# Agent 和 Python 工具的关系

正确关系应该是：

```text
Agent = 指挥者
Python 工具 = 执行者
```

也就是：

```text
用户：
帮我验证 TC001

Agent：
读取测试定义 → 调用 Python 工具 → 分析结果 → 总结风险

Python 工具：
真正执行 API、保存证迹、生成 Excel
```

不要让 Agent 自己直接调用所有 API。
因为这样不稳定、不可重复、证迹不好管理。

---

# 推荐实现路线

## 第一阶段：Python 工具

先实现：

```text
读取 Excel
连续调用 API
保存 request / response
生成结果 Excel
```

## 第二阶段：差异比较

增加：

```text
和上一版比较
和 baseline 比较
schema diff
value diff
```

## 第三阶段：Agent 包装

Agent 只负责：

```text
解释测试定义
启动 Python 工具
读取结果
总结问题
生成改善建议
```

---

# 结论

可以，而且应该这样做：

```text
先做 Python 执行工具
再做 Agent 包装
```

最终结构是：

```text
e6_api_flow_validator     ← Python 工具，负责执行
e6_validation_agent       ← Agent，负责理解、调度、解释
```

这样最稳、最容易测试、也最适合给 Codex 实现。

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "08f0b1c3-dde6-4d61-84fe-95e0e0a88fa0"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 2 ～ 3 秒"
}
```

## 第 4 轮

### 你

确实只能是api调用测试的工具或者是batch

### ChatGPT

对，**它本质上应该是 API 调用测试工具 / Batch，不是 Agent。**

最合适定位：

```text
E6 API Flow Regression Batch
```

也就是：

```text
读取测试数据
按顺序调用 API
保存证迹
比较前后版本
生成确认结果一览
```

Agent 最多只是外壳：

```text
Agent：帮人准备测试数据、解释结果、总结风险
Batch：真正执行 API 测试
```

推荐最终命名：

```text
e6-api-flow-validator
```

执行方式：

```bash
python -m e6_api_flow_validator run \
  --input ./inputs/e6_api_test_definition.xlsx \
  --env dev \
  --case TC001 \
  --baseline latest
```

核心成果物：

```text
runs/
  20260624_153000_TC001/
    raw_request_response/
    normalized_result.json
    diff_result.json
    result_summary.xlsx
    result_report.html
```

设计原则：

```text
1. 不依赖 LLM
2. 可重复执行
3. 可放进 Jenkins / GitHub Actions / Cron / Windows Task Scheduler
4. 每次都有证迹
5. 每次都有 Excel 确认表
6. 可和上一版结果比较
```

所以你现在应该给 Codex 的任务不是：

```text
做一个 Agent
```

而是：

```text
做一个 Python Batch 工具，用于 E6 Developer API 的业务流程级回归验证。
```

这条路是对的。

## 第 5 轮

### 你

如果做成java jar调用可以不

### ChatGPT

可以，**做成 Java JAR 更适合企业现场**。

推荐定位：

```text
e6-api-flow-validator.jar
```

执行方式：

```bash
java -jar e6-api-flow-validator.jar \
  --input ./inputs/e6_api_test_definition.xlsx \
  --env dev \
  --case TC001 \
  --baseline latest
```

Java 版优势：

```text
1. 更适合日本企业环境
2. 容易放进 Jenkins / JP1 / Windows Task Scheduler / Linux cron
3. 方便和现有 Java 系统、Spring 项目、社内Batch联动
4. 证迹、日志、Excel报告更容易规范化
5. 不依赖 Python 环境
```

推荐技术栈：

```text
Java 17
Spring Boot CLI Batch
Apache POI 读取/生成 Excel
OkHttp 或 Spring WebClient 调 API
Jackson 处理 JSON
JsonPath 解析前序 API response
Picocli 或 Spring Shell 处理命令行参数
Logback 输出日志
```

项目结构：

```text
e6-api-flow-validator/
  pom.xml
  src/main/java/com/company/e6validator/
    E6ApiFlowValidatorApplication.java
    cli/
      CommandRunner.java
    excel/
      ExcelInputLoader.java
      ExcelReportWriter.java
    flow/
      FlowRunner.java
      ParamResolver.java
      ConditionEvaluator.java
    http/
      ApiClient.java
      AuthProvider.java
    validate/
      RequestValidator.java
      ResponseValidator.java
      SchemaValidator.java
    diff/
      DiffEngine.java
    evidence/
      EvidenceStore.java
    model/
      ApiFlow.java
      RequestParam.java
      ResponseExpectation.java
      TestCase.java
      ApiResult.java
```

最终它就是：

```text
Excel测试定义书
    ↓
Java Batch JAR
    ↓
按顺序调用 E6 API
    ↓
保存 raw request / response
    ↓
验证 status / request / response
    ↓
和 baseline 比较
    ↓
生成 Excel确认结果一览
```

结论：
**可以，而且 Java JAR 版比 Agent 版更稳、更像正式验收工具。**

## 第 6 轮

### 你

我想的是比如 相同类型的api处理 作为一个java main 然后按方法作为api。然后一个usecase调用 可以调用多个类java main的api方法 这个设计合理吗

### ChatGPT

合理，但建议不要做成“多个 Java main 互相调用”。更好的设计是：

```text
一个 Main / 一个 Jar 入口
多个 ApiClient 类
多个 Api 方法
一个 UseCase 负责编排调用顺序
```

也就是：

```text
Main 只是启动器
UseCase 是业务流程
ApiClient 是同类 API 的集合
ApiMethod 是具体 API 调用
```

结构可以这样：

```text
e6-api-flow-validator
  Main.java

  usecase/
    CreateAccountUseCase.java
    PaymentFlowUseCase.java
    BalanceCheckUseCase.java

  api/
    CustomerApi.java
    AccountApi.java
    CardApi.java
    TransactionApi.java
    LedgerApi.java

  client/
    E6HttpClient.java

  model/
    request/
    response/

  report/
    ExcelReportWriter.java
```

调用关系：

```text
Main
 ↓
UseCaseRunner
 ↓
PaymentFlowUseCase
 ↓
CustomerApi.createCustomer()
 ↓
AccountApi.createAccount()
 ↓
LedgerApi.getBalance()
 ↓
TransactionApi.createTransaction()
 ↓
LedgerApi.getBalance()
 ↓
ReportWriter
```

例子：

```java
public class PaymentFlowUseCase {

    private final CustomerApi customerApi;
    private final AccountApi accountApi;
    private final TransactionApi transactionApi;
    private final LedgerApi ledgerApi;

    public void execute(TestContext ctx) {
        var customer = customerApi.createCustomer(ctx.getCreateCustomerRequest());

        ctx.put("customerId", customer.getCustomerId());

        var account = accountApi.createAccount(
            ctx.getCreateAccountRequest(customer.getCustomerId())
        );

        ctx.put("accountId", account.getAccountId());

        var beforeBalance = ledgerApi.getBalance(account.getAccountId());

        var transaction = transactionApi.createTransaction(
            ctx.getTransactionRequest(account.getAccountId())
        );

        var afterBalance = ledgerApi.getBalance(account.getAccountId());

        ctx.record("beforeBalance", beforeBalance);
        ctx.record("transaction", transaction);
        ctx.record("afterBalance", afterBalance);
    }
}
```

重点是：

```text
不要：
CustomerMain.java
AccountMain.java
TransactionMain.java
互相调用 main()

要：
CustomerApi.java
AccountApi.java
TransactionApi.java
由 UseCase 统一调用
```

原因：

```text
main 方法适合程序入口，不适合业务组合
api 方法适合被 usecase 重复调用
usecase 适合表达业务顺序
```

最终设计：

```text
Java Jar
  ├─ Main：入口
  ├─ UseCase：业务流程编排
  ├─ Api：同类型 API 方法集合
  ├─ Validator：验证 request/response
  ├─ Evidence：保存证迹
  └─ Report：生成 Excel
```

这个方向是对的，只要把“多个 main”改成“多个 api class + usecase 调用方法”，就是很合理的企业级 Batch 设计。

## 第 7 轮

### 你

那这个batch需要满足多重启动 还能操持各个文件 进程不影响

### ChatGPT

对，这个 Batch 必须支持 **多重启动**，否则企业现场很危险。

正确设计是：

```text
同一个 jar 可以同时启动多个进程
每个进程都有独立 run_id
每个进程写自己的目录
日志、结果、临时文件、锁文件互不影响
```

---

# 核心原则

不要写到公共文件：

```text
NG:
runs/latest/
result.xlsx
temp.json
log/app.log
```

要按每次执行隔离：

```text
OK:
runs/{run_id}/
logs/{run_id}.log
tmp/{run_id}/
reports/{run_id}/
```

---

# 推荐执行方式

```bash
java -jar e6-api-flow-validator.jar \
  --input ./inputs/e6_api_test_definition.xlsx \
  --env dev \
  --case TC001 \
  --run-id 20260624_153000_TC001_001
```

如果用户不传 `run-id`，系统自动生成：

```text
yyyyMMdd_HHmmss_SSS + caseId + randomSuffix
```

例如：

```text
20260624_153000_123_TC001_a8f31c
```

---

# 目录设计

```text
workspace/
  inputs/
    e6_api_test_definition.xlsx

  runs/
    20260624_153000_123_TC001_a8f31c/
      input/
        e6_api_test_definition.xlsx
      raw/
        001_login_request.json
        001_login_response.json
        002_create_customer_request.json
        002_create_customer_response.json
      normalized/
        api_trace.json
        request_schema.json
        response_schema.json
      diff/
        diff_result.json
      reports/
        result_summary.xlsx
        result_detail.xlsx
        result_report.html
      tmp/
      logs/
        run.log
      status/
        RUNNING
        SUCCESS
        FAILED

  baselines/
    TC001/
      20260601_100000/
        api_trace.json
        result_summary.xlsx

  latest/
    TC001/
      latest_run_id.txt
```

---

# 多重启动时要避免的问题

## 1. 文件名冲突

所有输出必须带 `run_id` 或放在 `run_id` 目录下。

```text
result_summary.xlsx       NG
runs/{run_id}/result.xlsx OK
```

---

## 2. latest 更新冲突

多个进程同时执行时，不能随便覆盖：

```text
latest/TC001/latest_run_id.txt
```

必须使用文件锁。

```java
FileChannel channel = FileChannel.open(lockPath);
FileLock lock = channel.lock();
try {
    // update latest_run_id.txt
} finally {
    lock.release();
}
```

---

## 3. baseline 不能被执行过程修改

baseline 应该只读。

```text
执行时读取 baseline
执行结束后不能自动覆盖 baseline
```

只有明确命令才允许更新：

```bash
java -jar e6-api-flow-validator.jar promote-baseline \
  --case TC001 \
  --run-id 20260624_153000_123_TC001_a8f31c
```

---

## 4. 日志不能共用一个文件

不要所有进程写：

```text
logs/app.log
```

要写：

```text
runs/{run_id}/logs/run.log
```

---

## 5. 临时文件不能共用

不要：

```text
tmp/request.json
```

要：

```text
runs/{run_id}/tmp/request.json
```

---

# 进程隔离设计

每个执行进程启动后创建自己的 `RunContext`：

```java
public class RunContext {
    private String runId;
    private String caseId;
    private Path runDir;
    private Path rawDir;
    private Path reportDir;
    private Path tmpDir;
    private Path logDir;
    private Instant startTime;
}
```

所有模块都只能通过 `RunContext` 写文件。

```text
ApiClient       → rawDir
EvidenceStore  → rawDir / normalizedDir
ReportWriter   → reportDir
DiffEngine     → diffDir
Logger         → logDir
```

---

# 状态文件设计

每个 run 目录下保存状态：

```text
status/RUNNING
status/SUCCESS
status/FAILED
```

开始时：

```text
RUNNING
```

成功结束：

```text
SUCCESS
```

失败结束：

```text
FAILED
```

同时保存：

```text
status/result.json
```

内容：

```json
{
  "runId": "20260624_153000_123_TC001_a8f31c",
  "caseId": "TC001",
  "status": "FAILED",
  "startTime": "2026-06-24T15:30:00+09:00",
  "endTime": "2026-06-24T15:31:12+09:00",
  "successApiCount": 5,
  "failedApiCount": 1,
  "diffCount": 3
}
```

---

# 是否允许同一个 case 同时执行？

建议支持两种模式。

## 模式1：允许并行

```bash
--parallel-policy allow
```

同一个 TC001 可以同时跑多次。
每次 run_id 不同，互不影响。

## 模式2：同 case 禁止并行

```bash
--parallel-policy deny-same-case
```

执行前创建锁：

```text
locks/TC001.lock
```

如果已经有进程在跑 TC001，则直接退出：

```text
TC001 is already running.
```

---

# 推荐默认策略

```text
默认允许不同 case 并行
默认禁止同一个 case 并行
```

也就是：

```text
TC001 + TC002 可以同时跑
TC001 + TC001 不建议同时跑
```

原因是 E6 API 可能会产生真实业务数据，比如 customer、account、transaction。
同一个 case 同时跑，可能造成测试数据冲突。

---

# Java 结构补充

```text
src/main/java/com/company/e6validator/
  runtime/
    RunContext.java
    RunIdGenerator.java
    WorkspaceManager.java
    LockManager.java
    StatusManager.java

  evidence/
    EvidenceStore.java

  report/
    ExcelReportWriter.java

  baseline/
    BaselineRepository.java
    LatestRunRepository.java
```

---

# 最重要的设计结论

这个 Batch 要做到：

```text
1. 每次执行一个独立 run_id
2. 每个 run_id 一个独立目录
3. 所有输出禁止写公共文件
4. latest / baseline 更新必须加锁
5. baseline 默认只读
6. 日志按 run_id 分离
7. 临时文件按 run_id 分离
8. 同 case 是否并行由参数控制
```

一句话：

```text
Main 可以多重启动，但所有执行状态必须进入 RunContext，所有文件必须进入 runs/{run_id}/，公共资源必须加锁。
```

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "f431aea5-e977-41f4-a39f-30dc4948f038"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 1 秒"
}
```

## 第 8 轮

### 你

业务上不会有同一usecase一起跑 但如果特意多个相同的一起执行了 怎么办

### ChatGPT

要按 **安全优先** 设计：默认禁止同一 `usecase + env` 并行。

处理方式：

```text
1. 启动时创建锁：
   locks/{env}_{usecase}.lock

2. 如果锁已存在并且进程还活着：
   直接退出，返回错误码，例如 409

3. 如果锁已存在但进程已经死了：
   判断为 stale lock，自动清理后继续

4. 如果用户明确要强制并行：
   必须加参数 --parallel-policy allow-same-usecase
```

推荐默认行为：

```bash
java -jar e6-api-flow-validator.jar run \
  --env dev \
  --usecase PaymentFlow
```

如果已有同一 usecase 在执行：

```text
ERROR:
UseCase PaymentFlow on env dev is already running.
lock: locks/dev_PaymentFlow.lock
runningRunId: 20260624_153000_PaymentFlow_a8f31c

ExitCode: 409
```

强制允许：

```bash
java -jar e6-api-flow-validator.jar run \
  --env dev \
  --usecase PaymentFlow \
  --parallel-policy allow-same-usecase
```

但强制并行时必须自动隔离测试数据：

```text
run_id 不同
idempotency_key 不同
request_id 不同
external_customer_id 不同
external_account_id 不同
测试数据 suffix 不同
输出目录不同
```

例如：

```text
externalCustomerId = TC001_${runId}
idempotencyKey     = ${runId}_${stepNo}
requestId          = ${runId}_${apiId}
```

最终规则：

```text
业务上不应该同一 usecase 同时跑
系统上默认禁止
误操作时安全退出
强制并行时必须显式指定参数
并且所有测试数据、文件、日志、idempotency key 都按 run_id 隔离
```

## 第 9 轮

### 你

runid如何生成

### ChatGPT

这个其实很关键。

你的系统未来会有：

```text
几十个 UseCase
多个环境(dev/stg/uat/prod)
几个月甚至几年的执行历史
Excel报告
Raw Request/Response
Diff结果
```

所以 **run_id 绝对不能只是时间戳**。

---

# 推荐工业版格式

```text
{env}_{usecase}_{yyyyMMddHHmmssSSS}_{shortUuid}
```

例如：

```text
dev_PaymentFlow_20260624153015123_a8f31c
```

或者：

```text
stg_CreateCustomer_20260624153015123_b9d812
```

这样看到目录就知道：

```text
什么环境
什么业务流程
什么时间
唯一编号
```

---

# Java实现

```java
public class RunIdGenerator {

    public static String generate(
            String env,
            String useCase) {

        String ts = LocalDateTime.now()
                .format(DateTimeFormatter.ofPattern(
                    "yyyyMMddHHmmssSSS"));

        String uuid = UUID.randomUUID()
                .toString()
                .replace("-", "")
                .substring(0, 6);

        return env + "_"
                + useCase + "_"
                + ts + "_"
                + uuid;
    }
}
```

结果：

```text
dev_PaymentFlow_20260624153015123_a8f31c
```

---

# 为什么不用纯UUID

不要：

```text
8f7e31c9-1f4b-4f78-aac0-8c21...
```

因为运维看不懂。

目录：

```text
runs/
  8f7e31c9-1f4b-4f78-aac0...
```

根本不知道是什么。

---

# 为什么不用纯时间

不要：

```text
20260624153015
```

因为：

```text
同毫秒启动
多服务器启动
重跑
```

都有可能撞号。

---

# 我实际推荐再加一个序列号

例如：

```text
dev_PaymentFlow_20260624153015123_001_a8f31c
```

结构：

```text
环境
UseCase
时间
当日序号
随机码
```

---

# 对应目录

```text
runs/
 ├── dev_PaymentFlow_20260624153015123_a8f31c
 ├── dev_PaymentFlow_20260624153100881_c7d213
 ├── stg_PaymentFlow_20260624154011234_f2aa91
```

非常容易查。

---

# 更工业化：Run Metadata

除了 run_id 之外，再生成：

```json
{
  "runId": "dev_PaymentFlow_20260624153015123_a8f31c",
  "useCase": "PaymentFlow",
  "env": "dev",
  "executor": "wu.rg",
  "host": "WIN-001",
  "pid": 12345,
  "startTime": "2026-06-24T15:30:15.123+09:00",
  "version": "1.4.2",
  "gitCommit": "a1b2c3d"
}
```

保存：

```text
runs/{run_id}/run-info.json
```

以后查问题特别方便。

---

# 如果未来扩展成调度平台

到后面我甚至建议区分：

```text
job_id
run_id
```

例如：

```text
job_id = PaymentFlow_DEV

run_id =
dev_PaymentFlow_20260624153015123_a8f31c
```

关系：

```text
一个 Job
    ↓
执行很多次
    ↓
产生多个 Run
```

```text
PaymentFlow_DEV
 ├─ run1
 ├─ run2
 ├─ run3
```

这是 Jenkins、Airflow、Control-M、JP1 等调度系统常见的设计。

---

对于你的 E6 验证工具，我推荐最终采用：

```text
run_id =
{env}_{usecase}_{yyyyMMddHHmmssSSS}_{6位随机码}
```

例如：

```text
dev_CreateAccount_20260624153015123_a8f31c
```

既唯一、可读，又适合后续扩展到多进程、多服务器和历史追踪。

## 第 10 轮

### 你

这个可以保证唯一吗

### ChatGPT

严格来说：

```text
时间戳 + 6位随机码
```

**不能数学上保证 100% 唯一**，只能说碰撞概率极低。

对于企业级系统，我不会把唯一性完全寄托在随机数上。

---

# 推荐方案1（单机版）

如果你的 Batch 运行在一台机器上：

```text
run_id =
{env}_{usecase}_{yyyyMMddHHmmssSSS}_{AtomicLong}
```

例如：

```text
dev_PaymentFlow_20260624153015123_00001
dev_PaymentFlow_20260624153015123_00002
```

但这要求维护一个本地计数器。

---

# 推荐方案2（工业版）

直接使用：

```java
UUID.randomUUID()
```

例如：

```text
550e8400-e29b-41d4-a716-446655440000
```

UUID v4 有 122 位随机空间。

碰撞概率低到可以认为：

```text
全世界每天执行几十亿次
跑几百年
都几乎不会撞
```

---

# 推荐方案3（最适合你）

同时保留：

```text
可读ID
+
UUID
```

例如：

```text
run_id =
dev_PaymentFlow_20260624153015123

run_uuid =
550e8400-e29b-41d4-a716-446655440000
```

目录：

```text
runs/
  dev_PaymentFlow_20260624153015123/
```

run-info.json：

```json
{
  "runId": "dev_PaymentFlow_20260624153015123",
  "runUuid": "550e8400-e29b-41d4-a716-446655440000"
}
```

这样：

```text
人看目录方便
系统保证唯一
```

---

# 如果要绝对唯一

很多金融系统采用：

```text
Snowflake ID
```

结构：

```text
时间戳
+ 机器ID
+ 进程ID
+ 序列号
```

例如：

```text
1987654321098765432
```

同毫秒内生成几十万条都不会重复。

Java 有成熟实现。

---

# 我给你的建议

对于 E6 API Validator 这种工具：

```text
runId      = 可读
runUuid    = UUID
```

例如：

```text
runId:
dev_PaymentFlow_20260624153015123

runUuid:
550e8400-e29b-41d4-a716-446655440000
```

然后目录名用：

```text
dev_PaymentFlow_20260624153015123_550e8400
```

这样：

```text
人能看懂
机器能保证唯一
多进程安全
多服务器安全
未来扩展安全
```

这是我认为最平衡、最工业化的方案。

## 第 11 轮

### 你

进程id这个可以保证唯一吗

### ChatGPT

不能。

**进程 ID（PID）绝对不能作为唯一 ID 的保证。**

原因很简单：

```text
Windows:
PID = 1234

进程结束
↓
过一会儿

新进程
PID = 1234
```

操作系统会复用 PID。

---

# 举例

今天：

```text
java.exe
PID=8888
```

执行：

```text
PaymentFlow
```

产生：

```text
run_id = 8888
```

进程结束。

---

明天：

```text
java.exe
PID=8888
```

再次执行：

```text
CreateCustomer
```

如果你用 PID 当唯一值：

```text
run_id = 8888
```

直接冲突。

---

# PID 的正确用途

PID 适合：

```text
调试
监控
锁文件检查
判断进程是否存活
```

例如：

```json
{
  "runId":"dev_PaymentFlow_20260624_153015",
  "pid":8888,
  "host":"SERVER01"
}
```

方便排查：

```text
是谁在跑？
哪个 JVM？
哪个服务器？
```

---

# PID + 时间戳 呢？

例如：

```text
20260624153015_8888
```

比单独 PID 好很多。

但仍然不能理论保证唯一。

因为：

```text
同一秒
PID复用
多机器
```

都有可能碰撞。

虽然概率已经很低。

---

# 企业级唯一 ID 一般怎么做

### 方案1 UUID（最简单）

```java
UUID.randomUUID()
```

保证程度：

```text
实际上可认为唯一
```

---

### 方案2 Snowflake（大型系统）

结构：

```text
timestamp
workerId
datacenterId
sequence
```

例如：

```text
1987654321098765432
```

分布式系统常用。

---

### 方案3 你的场景推荐

对于 E6 Validator：

```text
runId =
{env}_{usecase}_{timestamp}
```

例如：

```text
dev_PaymentFlow_20260624153015123
```

再保存：

```json
{
  "runUuid":"550e8400-e29b-41d4-a716-446655440000",
  "pid":8888,
  "host":"WIN-DEV01"
}
```

目录：

```text
runs/
  dev_PaymentFlow_20260624153015123/
```

这样：

```text
人看 runId
机器用 UUID
运维查 PID
```

三者职责分离。

---

# 如果考虑你前面说的

> 同一个 usecase 不应该同时执行，但有人误操作执行了两次

我会这样设计：

```text
Lock Key:
env + usecase
```

例如：

```text
dev_PaymentFlow.lock
```

锁文件内容：

```json
{
  "runId":"dev_PaymentFlow_20260624153015123",
  "runUuid":"550e8400-e29b-41d4-a716-446655440000",
  "pid":8888,
  "host":"WIN-DEV01",
  "startTime":"2026-06-24T15:30:15+09:00"
}
```

启动时：

1. 发现 lock
2. 检查 PID 是否还活着
3. PID 活着 → 拒绝启动
4. PID 不存在 → 删除 stale lock
5. 继续执行

这里 PID 只是：

```text
判断旧进程是否存活
```

不是唯一 ID。

---

所以结论：

```text
PID 不保证唯一
PID 不应该作为 run_id
PID 只适合做进程存活检查
```

对于你的 Java Batch：

```text
run_id      = 可读时间ID
run_uuid    = UUID
pid         = 调试信息
lock_key    = env + usecase
```

这是比较标准的企业级设计。

## 第 12 轮

### 你

线程id呢

### ChatGPT

线程 ID 也**不能保证唯一**。

它和 PID 一样，只适合做调试信息，不适合做 `run_id`。

原因：

```text
1. 线程结束后，线程 ID 可能被复用
2. 不同 JVM / 不同机器里的线程 ID 会重复
3. Java Thread.getId() 只在当前 JVM 生命周期内相对唯一
4. 程序重启后，线程 ID 又重新开始
```

正确用法：

```json
{
  "runId": "dev_PaymentFlow_20260624153015123",
  "runUuid": "550e8400-e29b-41d4-a716-446655440000",
  "host": "WIN-DEV01",
  "pid": 8888,
  "threadId": 31
}
```

职责分离：

```text
runUuid  = 唯一识别一次执行
runId    = 人能看懂的执行名
pid      = 哪个进程
threadId = 哪个线程
```

推荐最终方案：

```text
目录名：
runs/dev_PaymentFlow_20260624153015123_550e8400/

run-info.json：
{
  "runId": "dev_PaymentFlow_20260624153015123",
  "runUuid": "550e8400-e29b-41d4-a716-446655440000",
  "env": "dev",
  "usecase": "PaymentFlow",
  "host": "WIN-DEV01",
  "pid": 8888,
  "threadId": 31
}
```

结论：

```text
线程 ID 不能当唯一 ID。
唯一性用 UUID。
排查问题才记录 PID / threadId。
```

## 第 13 轮

### 你

我是说 比如进程id加上时间和uid等

### ChatGPT

那就不一样了。

如果你是说：

```text
run_id =
时间戳
+ PID
+ ThreadId
+ UUID片段
```

那完全可以，而且已经达到企业级要求了。

例如：

```text
20260624_153015_123_8888_31_a8f31c
│        │      │    │   └ UUID前6位
│        │      │    └ ThreadId
│        │      └ PID
│        └ 毫秒
└ 时间
```

但是这里要理解一件事：

---

# 真正保证唯一的是谁？

实际上是：

```text
UUID
```

或者：

```text
Snowflake
```

---

PID 和 ThreadId 的作用是：

```text
辅助定位
```

不是保证唯一。

例如：

```text
20260624_153015_123
PID=8888
Thread=31
UUID=a8f31c
```

以后查问题时：

```text
这是哪台机器？
哪个 JVM？
哪个线程？
```

很容易找到。

---

# 我在企业项目里的做法

通常分成两层。

## 人看的 RunId

```text
DEV_PaymentFlow_20260624_153015123
```

用于：

```text
目录
Excel
HTML报告
邮件
```

---

## 系统看的 ExecutionId

```text
550e8400-e29b-41d4-a716-446655440000
```

用于：

```text
数据库主键
日志关联
唯一识别
```

---

# 你的场景更推荐

因为你不会有几百万并发。

直接：

```java
String runId =
    env
    + "_"
    + useCase
    + "_"
    + timestamp
    + "_"
    + ProcessHandle.current().pid()
    + "_"
    + UUID.randomUUID().toString().substring(0,8);
```

例如：

```text
DEV_PaymentFlow_20260624_153015123_8888_a8f31c2
```

这个基本可以认为：

```text
全公司跑几年都不会重复
```

---

# 更工业化一点

再加主机名：

```text
DEV_PaymentFlow_20260624_153015123_WINDEV01_8888_a8f31c2
```

这样看到目录就知道：

```text
环境
UseCase
时间
机器
进程
随机ID
```

---

# 不过对于你的 E6 Validator

我反而建议：

```text
runId
executionId
```

分离。

例如：

```text
runId:
DEV_PaymentFlow_20260624_153015123

executionId:
WINDEV01_8888_a8f31c2
```

最后目录：

```text
runs/
  DEV_PaymentFlow_20260624_153015123/
      run-info.json
```

run-info.json：

```json
{
  "runId":"DEV_PaymentFlow_20260624_153015123",
  "executionId":"WINDEV01_8888_a8f31c2",
  "host":"WINDEV01",
  "pid":8888,
  "threadId":31
}
```

这样比把所有东西堆进目录名更容易维护。

---

所以结论：

```text
时间戳 + PID + ThreadId + UUID片段
当然可以

但真正负责唯一的是 UUID
PID/ThreadId/HostName 负责排查问题
时间戳负责可读性
```

这是比较成熟的 Batch 系统设计。

## 第 14 轮

### 你

那按照你的推荐设计uid

### ChatGPT

按照你这个 **E6 API Flow Validator Batch** 的场景（单公司内部工具、Java Batch、多实例启动、需要追溯、需要生成报告），我会采用 **双ID设计**。

不要只有一个 ID。

---

# 第一层：RunId（业务可读）

给人看。

格式：

```text
{env}_{usecase}_{yyyyMMddHHmmssSSS}
```

例如：

```text
DEV_PaymentFlow_20260624153015123
```

或者：

```text
STG_CreateCustomer_20260624153100211
```

用途：

```text
Excel报告
HTML报告
邮件标题
目录名
运维查看
```

---

# 第二层：ExecutionId（系统唯一）

给机器看。

直接：

```java
UUID.randomUUID()
```

例如：

```text
550e8400-e29b-41d4-a716-446655440000
```

用途：

```text
数据库主键
日志关联ID
锁文件关联
API Trace关联
Raw Evidence关联
```

---

# 我最终推荐的数据结构

```java
public class RunContext {

    private String runId;

    private UUID executionId;

    private String env;

    private String useCase;

    private String hostName;

    private long pid;

    private Instant startTime;

}
```

---

# 目录结构

目录不要用 UUID。

因为人看不懂。

```text
runs/

 └── DEV_PaymentFlow_20260624153015123/
      run-info.json
      reports/
      raw/
      diff/
      logs/
```

---

# run-info.json

```json
{
  "runId": "DEV_PaymentFlow_20260624153015123",

  "executionId":
  "550e8400-e29b-41d4-a716-446655440000",

  "env": "DEV",

  "useCase": "PaymentFlow",

  "hostName": "WIN-DEV01",

  "pid": 8888,

  "startTime":
  "2026-06-24T15:30:15.123+09:00"
}
```

---

# Lock设计

锁文件：

```text
locks/
  DEV_PaymentFlow.lock
```

内容：

```json
{
  "runId":
  "DEV_PaymentFlow_20260624153015123",

  "executionId":
  "550e8400-e29b-41d4-a716-446655440000",

  "pid": 8888,

  "host": "WIN-DEV01"
}
```

检查：

```text
同一个 usecase 是否已经运行
PID 是否存活
锁是否过期
```

---

# 如果你一定想做成一个字符串

我推荐：

```text
{env}_{usecase}_{timestamp}_{uuid8}
```

例如：

```text
DEV_PaymentFlow_20260624153015123_A8F31C2D
```

其中：

```text
A8F31C2D
=
UUID前8位
```

Java：

```java
String uid =
    UUID.randomUUID()
        .toString()
        .replace("-", "")
        .substring(0, 8)
        .toUpperCase();
```

最终：

```text
DEV_PaymentFlow_20260624153015123_A8F31C2D
```

这个已经足够工业化。

---

# 如果是我来做

我会选：

```text
RunId
    = DEV_PaymentFlow_20260624153015123

ExecutionId
    = UUID

目录
    用 RunId

系统关联
    用 ExecutionId
```

因为：

```text
可读性最好
扩展性最好
排查问题最方便
以后接 Jenkins
以后接数据库
以后接 Agent
都不用改
```

这也是很多企业 Batch、调度平台、CI/CD 系统常见的设计思路。

## 第 15 轮

### 你

好的 这个设计我认可。接下来 有多个api 但是目前我还不能把这些API归类 而且是api平台提供的api 我只是实现java 按照usecase去调用api 来验证这些api的参数个数 参数类型 接受的信息长度 返回值个数 类型 返回值长度 等没有变化  我如何设计才能知道api平台的api它是否被变动过 因为是他api平台实现的 我如何实现这种按usecase的业务确认 以及每个usecase里各个api可能发生的变化种类的一一设计和执行结果监控。 比如对单个api 设计各种类型的单个调用验证 对于每个usecase的全链条调用正常异常的验证设计 。

### ChatGPT

这里的关键不是先给 API 分类，而是先把“调用证迹”和“契约快照”做出来。只要每次把同一个 usecase 的 request/response 结构抽取成基准，就能发现 API 平台有没有变动。

### ChatGPT

可以这样设计：
**你不需要先知道 API 平台怎么分类。你只要把 API 当成黑盒，通过“契约快照 + 基准比较 + usecase链路验证”来判断它有没有变。**

---

# 1. 总体思路

```text
API平台 = 黑盒
你的Java Batch = 外部验证器
```

你能做的是：

```text
1. 按 usecase 调用 API
2. 保存每次 request / response
3. 抽取字段结构
4. 和 baseline 比较
5. 判断 API 是否变动
6. 判断 usecase 是否还能正常跑通
```

---

# 2. 两种验证层

必须分两层。

## 第一层：单 API 契约验证

验证某一个 API 本身有没有变化。

例如：

```text
POST /customer/create
```

检查：

```text
status code
request字段个数
request字段名
request字段类型
request字段长度
request必填
response字段个数
response字段名
response字段类型
response字段长度
response枚举值
返回值变化
```

---

## 第二层：UseCase 链路验证

验证业务流程还能不能跑通。

例如：

```text
CreateCustomer
 → CreateAccount
 → FundAccount
 → QueryBalance
 → CreateTransaction
 → QueryTransaction
 → QueryBalance
```

检查：

```text
前一个API返回值能不能传给后一个API
整个链路是否成功
业务状态是否正确
金额/余额是否正确
异常场景是否符合期待
```

---

# 3. 核心概念：API Contract Snapshot

每次 API 调用后，生成一份结构快照。

例如 response：

```json
{
  "apiId": "create_customer",
  "method": "POST",
  "url": "/customers",
  "statusCode": 200,
  "responseSchema": {
    "$.customerId": {
      "type": "string",
      "exists": true,
      "length": 36
    },
    "$.status": {
      "type": "string",
      "exists": true,
      "length": 6,
      "value": "ACTIVE"
    }
  }
}
```

下次执行时比较：

```text
旧：
$.status = string, value=ACTIVE

新：
$.status = number, value=1
```

判断：

```text
类型变化：HIGH
值变化：MEDIUM/HIGH
```

---

# 4. API变化种类设计

每个 API 可能发生这些变化：

## Request 变化

```text
字段新增
字段删除
字段类型变化
字段长度限制变化
必填变化
enum变化
默认值变化
URL变化
method变化
header变化
认证方式变化
```

## Response 变化

```text
字段新增
字段删除
字段类型变化
字段长度变化
字段路径变化
null变非null
非null变null
数组结构变化
数组元素类型变化
enum值变化
错误码变化
错误message变化
status code变化
```

## 业务行为变化

```text
同样request返回不同业务状态
余额变化规则不同
交易状态迁移不同
失败场景变成功
成功场景变失败
错误码变了
后续API拿不到必要字段
```

---

# 5. 结果严重度

```text
BLOCKER:
- usecase无法继续执行
- 前序API没有返回后续API必需字段
- status code 从成功变失败

HIGH:
- 必填字段消失
- 字段类型变化
- enum值变化
- 业务状态码变化
- 金额/余额计算不一致

MEDIUM:
- 字段长度变化
- 新增字段
- 非关键字段值变化
- error message变化

LOW:
- response时间变化
- 字段顺序变化
- 非验证字段新增
```

---

# 6. 单 API 验证设计

每个 API 可以准备多种调用模式。

## 6.1 正常调用

```text
必填参数全部正确
期待 200 / 201
期待返回关键字段
```

## 6.2 必填缺失

```text
删除一个必填字段
期待 400
期待错误码不变
```

## 6.3 类型错误

```text
string字段传number
number字段传string
期待错误
```

## 6.4 长度超限

```text
最大20位字段传21位
期待错误
```

## 6.5 enum非法值

```text
status=A/B/C
传入 status=Z
期待错误
```

## 6.6 边界值

```text
length=0
length=max
length=max+1
amount=0
amount=1
amount=-1
amount=max
```

---

# 7. UseCase验证设计

每个 usecase 至少设计两类。

## 7.1 正常链路

```text
所有API按顺序成功
后续API参数从前序API response取得
最终业务结果正确
```

例：

```text
create_customer
 → create_account
 → query_balance
 → fund_account
 → query_balance
```

验证：

```text
customerId存在
accountId存在
fund前余额 = 0
fund后余额 = fund前余额 + amount
transactionStatus = SUCCESS
```

---

## 7.2 异常链路

故意制造业务错误。

例如：

```text
不存在的customerId创建account
余额不足扣款
重复requestId
非法currency
非法accountStatus
```

验证：

```text
是否返回期待错误码
是否没有产生不该产生的数据
余额是否没有变化
后续API是否正确停止
```

---

# 8. 你现在不需要 API 分类，先这样组织

用 `usecase` 作为第一分类。

```text
usecases/
  UC001_CreateCustomer/
  UC002_CreateAccount/
  UC003_FundAccount/
  UC004_PaymentSuccess/
  UC005_PaymentInsufficientBalance/
```

每个 usecase 里面列出 API steps：

```text
step_no
api_id
method
url
request_template
expected_status
extract_values
validation_rules
```

---

# 9. 每次执行保存三类结果

```text
1. raw evidence
   原始request/response

2. contract snapshot
   字段结构快照

3. diff result
   和baseline比较后的差异
```

目录：

```text
runs/
  DEV_PaymentFlow_20260624153015123/
    raw/
      001_create_customer_request.json
      001_create_customer_response.json
    contract/
      001_create_customer_request_contract.json
      001_create_customer_response_contract.json
    diff/
      001_create_customer_diff.json
      usecase_diff.json
    reports/
      result_summary.xlsx
```

---

# 10. Baseline机制

第一次确认正常后，把结果提升为 baseline。

```bash
java -jar e6-validator.jar promote-baseline \
  --env DEV \
  --usecase PaymentFlow \
  --run-id DEV_PaymentFlow_20260624153015123
```

之后每次执行：

```bash
java -jar e6-validator.jar run \
  --env DEV \
  --usecase PaymentFlow \
  --compare-baseline latest
```

比较对象：

```text
当前执行结果
vs
上一次认可的baseline
```

---

# 11. 监控结果表设计

## summary

| usecase | runId | result | apiCount | success | failed | diffCount |
|---|---|---|---:|---:|---:|---:|

## api_result

| step | apiId | method | url | status | result | elapsed |
|---:|---|---|---|---:|---|---:|

## contract_diff

| apiId | target | jsonPath | diffType | before | after | severity |
|---|---|---|---|---|---|---|

## usecase_check

| checkName | expected | actual | result | severity |
|---|---|---|---|---|

例如：

| checkName | expected | actual | result |
|---|---|---|---|
| balance_after | before + amount | 1000 | OK |
| transaction_status | SUCCESS | SUCCESS | OK |
| customerId_pass_to_account | exists | exists | OK |

---

# 12. Java模块设计

```text
validator/
  Main.java

  runtime/
    RunContext.java
    RunIdGenerator.java

  usecase/
    UseCase.java
    UseCaseRunner.java
    PaymentFlowUseCase.java

  api/
    GenericApiStepExecutor.java
    ApiStepDefinition.java

  contract/
    ContractExtractor.java
    ContractSnapshot.java
    ContractDiffEngine.java

  validation/
    RequestValidator.java
    ResponseValidator.java
    BusinessValidator.java

  baseline/
    BaselineRepository.java

  evidence/
    EvidenceStore.java

  report/
    ExcelReportWriter.java
```

---

# 13. 最重要的执行流程

```text
1. 加载 usecase定义
2. 创建 runId / executionId
3. 创建独立run目录
4. 按step调用API
5. 保存raw request
6. 保存raw response
7. 抽取request contract
8. 抽取response contract
9. 执行单API验证
10. 执行业务链路验证
11. 和baseline比较
12. 生成Excel/HTML报告
13. 更新run状态
```

---

# 14. 你判断 API 平台是否变动的方法

不是问 API 平台。

而是通过这四个证据判断：

```text
1. 同一API的 response schema 变了
2. 同一API的 status code 变了
3. 同一API的业务字段值域变了
4. 同一usecase链路跑不通了
```

这就是黑盒 API 变动检测。

---

# 15. 最终结论

你要做的是：

```text
UseCase驱动的 API黑盒回归验证Batch
```

它包含两条线：

```text
单API验证：
发现API接口契约变化

UseCase验证：
发现业务链路行为变化
```

最关键的设计是：

```text
raw evidence
contract snapshot
baseline
diff engine
usecase business check
Excel report
```

这样即使 API 平台不是你实现的，你也能持续监控它有没有变化。

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "7597732f-045c-473b-bb48-48c9ade6fd96"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 2 ～ 3 秒"
}
```

## 第 16 轮

### 你

作为用户 我需要设计用来验证的输入 以及可以确认输出 或者说检查输出是否和上次一致的结果文档 希望是markdown文档

### ChatGPT

我认为你已经发现一个关键问题了：

> 用户真正维护的不是 Excel，而是“测试规格书（Test Specification）”。

对于你这种 E6 API 回归验证工具，长期来看：

```text
Excel = 维护困难
JSON = 人看不懂
YAML = 开发人员喜欢
Markdown = 最适合业务人员和开发人员共同维护
```

所以我会设计成：

```text
UseCase.md
```

作为唯一输入。

然后工具执行后生成：

```text
Result.md
Diff.md
```

作为输出。

---

# 1. 用户维护什么

例如：

```text
specs/
 ├── UC001_CreateCustomer.md
 ├── UC002_CreateAccount.md
 ├── UC003_PaymentFlow.md
```

---

# 2. UC003_PaymentFlow.md

:::writing{variant="document" id="58371"}
# UseCase: PaymentFlow

## Metadata

| Item | Value |
|--------|--------|
| UseCaseId | UC003 |
| Name | Payment Flow |
| Environment | DEV |
| Version | 1.0 |
| Owner | QA |

---

# Preconditions

- Customer exists
- Account exists
- Balance >= 1000

---

# Variables

| Name | Value |
|--------|--------|
| FUND_AMOUNT | 1000 |
| PAYMENT_AMOUNT | 300 |

---

# Steps

## Step 1 - Create Customer

API:
POST /customers

Expected Status:
200

Expected Response:

| Path | Type | Required |
|--------|--------|--------|
| $.customerId | string | Y |
| $.status | string | Y |

Extract:

| Name | JsonPath |
|--------|--------|
| CUSTOMER_ID | $.customerId |

---

## Step 2 - Create Account

API:
POST /accounts

Request:

customerId = ${CUSTOMER_ID}

Expected Status:
200

Expected Response:

| Path | Type | Required |
|--------|--------|--------|
| $.accountId | string | Y |

Extract:

| Name | JsonPath |
|--------|--------|
| ACCOUNT_ID | $.accountId |

---

## Step 3 - Fund Account

API:
POST /fund

Request:

accountId = ${ACCOUNT_ID}
amount = ${FUND_AMOUNT}

Expected Status:
200

Business Check:

balance_after =
balance_before + FUND_AMOUNT

---

## Step 4 - Payment

API:
POST /payment

Request:

accountId = ${ACCOUNT_ID}
amount = ${PAYMENT_AMOUNT}

Expected Status:
200

Business Check:

transactionStatus = SUCCESS

---

# Expected Final State

| Item | Expected |
|--------|--------|
| Balance | 700 |
| TransactionStatus | SUCCESS |
| CustomerExists | true |
| AccountExists | true |
:::

---

# 3. Batch执行后生成什么

生成：

```text
runs/
 └── DEV_PaymentFlow_20260624153015/
      result.md
      diff.md
      run-info.json
      raw/
```

---

# 4. result.md

:::writing{variant="document" id="58372"}
# Execution Result

RunId:
DEV_PaymentFlow_20260624153015

ExecutionTime:
2026-06-24 15:30:15

Result:
PASS

---

# API Results

| Step | API | Status | Result |
|--------|--------|--------|--------|
| 1 | CreateCustomer | 200 | PASS |
| 2 | CreateAccount | 200 | PASS |
| 3 | FundAccount | 200 | PASS |
| 4 | Payment | 200 | PASS |

---

# Business Validation

| Check | Expected | Actual | Result |
|--------|--------|--------|--------|
| Balance | 700 | 700 | PASS |
| TransactionStatus | SUCCESS | SUCCESS | PASS |

---

# Summary

Total APIs:
4

Passed:
4

Failed:
0

Diff Count:
0
:::

---

# 5. diff.md

这是最重要的。

用户真正每天看的其实是这个。

:::writing{variant="document" id="58373"}
# Diff Report

Baseline:
20260620

Current:
20260624

---

## API Contract Changes

### Payment API

Field:
$.transactionStatus

Before:

type = string

After:

type = number

Severity:
HIGH

---

Field:
$.approvalCode

Before:

not exists

After:

exists

Severity:
LOW

---

## Business Changes

PaymentFlow

Expected:

Balance = 700

Actual:

Balance = 650

Severity:
HIGH

---

# Summary

HIGH:
1

MEDIUM:
0

LOW:
1
:::

---

# 6. 真正工业化的Baseline

不要比较：

```text
上次执行结果
```

因为：

```text
上次可能失败
上次可能有脏数据
上次可能环境异常
```

应该比较：

```text
Approved Baseline
```

目录：

```text
baseline/

 ├── UC001/
 │    └── approved.md

 ├── UC002/
 │    └── approved.md

 └── UC003/
      └── approved.md
```

只有人工确认：

```bash
validator approve-baseline \
  --run DEV_PaymentFlow_20260624
```

才更新 baseline。

---

# 7. 我最推荐的最终结构

```text
specs/

 ├── UC001_CreateCustomer.md
 ├── UC002_CreateAccount.md
 └── UC003_PaymentFlow.md

baseline/

 └── UC003/
      approved.md

runs/

 └── DEV_PaymentFlow_20260624/
      result.md
      diff.md
      raw/
      logs/
```

这样：

```text
输入 = Markdown
输出 = Markdown
比较基准 = Approved Markdown
```

然后你未来还可以：

```text
MkDocs
Git
GitHub
RAG
Agent
VSCode
```

全部直接利用 Markdown，不需要再维护 Excel 版本和 Markdown 版本两套资料。

对于你后面想做的 Agent OS、MkDocs Wiki、RAG 入库体系来说，这种 **Spec-as-Markdown** 的设计是最统一、最长期可维护的方案。

## 第 17 轮

### 你

你设计的uscase md文档 如果是文件读入的字节流以及回答也是文件流 我们该怎么办 比如在做一个共通utils的包 负责生成或解析这些 json的共通 log等肯定需要

### ChatGPT

对，这里要分层设计。
**Markdown 只是给人维护和确认的外层文档，程序内部不能直接靠 Markdown 表格跑。**

推荐设计：

```text
Markdown Spec
    ↓ 解析
Spec JSON
    ↓ 执行
Run Result JSON
    ↓ 渲染
Result Markdown / Diff Markdown
```

---

# 1. 最合理的设计

```text
用户维护：
UC001_PaymentFlow.md

工具内部使用：
UC001_PaymentFlow.spec.json

执行结果：
run-result.json
contract-snapshot.json
diff-result.json

用户确认：
result.md
diff.md
```

也就是说：

```text
Markdown = 人看的输入/输出
JSON = 程序真正执行和比较的标准格式
```

---

# 2. 共通 utils 包必须要有

建议独立成：

```text
e6-validator-common
```

里面放所有共通能力：

```text
common/
  json/
    JsonUtils
    JsonPathUtils
    JsonSchemaUtils

  markdown/
    MarkdownSpecParser
    MarkdownReportRenderer

  file/
    FileStore
    AtomicFileWriter
    ResourceLoader

  log/
    RunLogger
    MaskingLogger

  runtime/
    RunContext
    RunIdGenerator

  diff/
    DiffType
    DiffSeverity

  security/
    MaskingUtils
```

---

# 3. 文件流怎么处理

不要到处直接传 `byte[]`。

建议统一用：

```java
InputStream
OutputStream
Path
```

设计成：

```java
public interface SpecLoader {
    UseCaseSpec load(InputStream inputStream);
}

public interface ReportWriter {
    void write(RunResult result, OutputStream outputStream);
}
```

这样未来可以支持：

```text
本地文件
S3文件
数据库BLOB
HTTP上传文件
ZIP里的文件
```

---

# 4. Markdown 输入解析流程

```text
UC001.md
  ↓
MarkdownSpecParser
  ↓
UseCaseSpec Java Object
  ↓
SpecJsonWriter
  ↓
UC001.spec.json
```

核心模型：

```java
public class UseCaseSpec {
    String useCaseId;
    String name;
    String env;
    List<ApiStepSpec> steps;
    List<BusinessCheckSpec> businessChecks;
}
```

```java
public class ApiStepSpec {
    int stepNo;
    String apiId;
    String method;
    String url;
    Map<String, Object> request;
    List<ResponseExpectation> expectedResponses;
    List<ExtractRule> extractRules;
}
```

---

# 5. 执行结果也不要直接生成 Markdown

先生成标准 JSON：

```text
run-result.json
```

例如：

```json
{
  "runId": "DEV_PaymentFlow_20260624153015123",
  "useCaseId": "UC003",
  "result": "FAIL",
  "apiResults": [
    {
      "stepNo": 1,
      "apiId": "createCustomer",
      "statusCode": 200,
      "result": "PASS"
    }
  ],
  "diffs": [
    {
      "apiId": "payment",
      "path": "$.status",
      "diffType": "TYPE_CHANGED",
      "before": "string",
      "after": "number",
      "severity": "HIGH"
    }
  ]
}
```

然后：

```text
run-result.json
  ↓
MarkdownReportRenderer
  ↓
result.md
diff.md
```

---

# 6. 为什么一定要 JSON 中间层

因为 Markdown 不适合做严格比较。

Markdown 会有这些问题：

```text
表格空格变化
换行变化
顺序变化
人手修改格式
不同编辑器格式化
```

所以比较必须基于 JSON：

```text
baseline-contract.json
vs
current-contract.json
```

Markdown 只负责展示。

---

# 7. 推荐最终包结构

```text
e6-api-flow-validator/
  e6-validator-common/
    JsonUtils
    FileUtils
    MarkdownUtils
    RunContext
    MaskingUtils

  e6-validator-spec/
    UseCaseSpec
    ApiStepSpec
    MarkdownSpecParser
    SpecJsonWriter

  e6-validator-core/
    UseCaseRunner
    ApiExecutor
    ContractExtractor
    DiffEngine
    Validator

  e6-validator-report/
    MarkdownReportRenderer
    ExcelReportWriter
    HtmlReportWriter

  e6-validator-cli/
    Main
    RunCommand
    PromoteBaselineCommand
```

---

# 8. 输入输出统一接口

```java
public interface UseCaseSpecReader {
    UseCaseSpec read(InputStream input);
}
```

```java
public interface RunResultWriter {
    void write(RunResult result, OutputStream output);
}
```

```java
public interface ContractSnapshotWriter {
    void write(ContractSnapshot snapshot, OutputStream output);
}
```

这样你的 Batch 不关心文件来自哪里。

---

# 9. 最终执行流程

```text
1. 读取 UC001.md 字节流
2. 解析成 UseCaseSpec
3. 保存 UC001.spec.json
4. 按 UseCaseSpec 调用 API
5. 保存 raw request/response
6. 抽取 contract-snapshot.json
7. 和 baseline-contract.json 比较
8. 生成 diff-result.json
9. 用 JSON 渲染 result.md / diff.md
```

---

# 10. 结论

你这个设计应该是：

```text
Markdown 负责人类可读
JSON 负责机器执行
Common Utils 负责文件流、JSON、Markdown、日志、Mask
Core 只处理 Java Object
Report 负责把 JSON 渲染成 Markdown
```

一句话：

```text
不要让业务执行逻辑直接依赖 Markdown。
Markdown 先转 JSON/Java Object，再执行；执行结果先落 JSON，再生成 Markdown。
```

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "ceb380cf-e4d8-477e-8160-0c6617c824ad"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 2 ～ 3 秒"
}
```

## 第 18 轮

### 你

那如果是文件流json能搞定吗

### ChatGPT

可以，**文件流 JSON 完全能搞定**。
而且比 Markdown 更适合程序执行。

推荐变成：

```text
输入：usecase.json
输出：run-result.json / diff-result.json
展示：result.md / diff.md
```

---

# 1. 文件流 JSON 读取

Java 里直接这样设计：

```java
public interface UseCaseSpecReader {
    UseCaseSpec read(InputStream inputStream);
}
```

实现：

```java
public class JsonUseCaseSpecReader implements UseCaseSpecReader {

    private final ObjectMapper objectMapper = new ObjectMapper();

    @Override
    public UseCaseSpec read(InputStream inputStream) throws IOException {
        return objectMapper.readValue(inputStream, UseCaseSpec.class);
    }
}
```

这样输入可以来自：

```text
本地文件
HTTP上传
S3
ZIP
数据库BLOB
```

---

# 2. JSON 输入例子

```json
{
  "useCaseId": "UC003",
  "name": "PaymentFlow",
  "env": "DEV",
  "variables": {
    "FUND_AMOUNT": 1000,
    "PAYMENT_AMOUNT": 300
  },
  "steps": [
    {
      "stepNo": 1,
      "apiId": "createCustomer",
      "method": "POST",
      "url": "/customers",
      "request": {
        "body": {
          "name": "test-${runId}",
          "status": "ACTIVE"
        }
      },
      "expectedStatus": 200,
      "expectResponse": [
        {
          "path": "$.customerId",
          "type": "string",
          "required": true
        }
      ],
      "extract": [
        {
          "name": "CUSTOMER_ID",
          "path": "$.customerId"
        }
      ]
    },
    {
      "stepNo": 2,
      "apiId": "createAccount",
      "method": "POST",
      "url": "/accounts",
      "request": {
        "body": {
          "customerId": "${CUSTOMER_ID}"
        }
      },
      "expectedStatus": 200,
      "expectResponse": [
        {
          "path": "$.accountId",
          "type": "string",
          "required": true
        }
      ],
      "extract": [
        {
          "name": "ACCOUNT_ID",
          "path": "$.accountId"
        }
      ]
    }
  ]
}
```

---

# 3. 输出 JSON

```json
{
  "runId": "DEV_PaymentFlow_20260624153015123",
  "executionId": "550e8400-e29b-41d4-a716-446655440000",
  "useCaseId": "UC003",
  "result": "PASS",
  "apiResults": [
    {
      "stepNo": 1,
      "apiId": "createCustomer",
      "method": "POST",
      "url": "/customers",
      "statusCode": 200,
      "result": "PASS"
    }
  ],
  "diffs": []
}
```

---

# 4. 输出写入文件流

```java
public interface RunResultWriter {
    void write(RunResult result, OutputStream outputStream);
}
```

```java
public class JsonRunResultWriter implements RunResultWriter {

    private final ObjectMapper objectMapper = new ObjectMapper();

    @Override
    public void write(RunResult result, OutputStream outputStream)
            throws IOException {
        objectMapper
            .writerWithDefaultPrettyPrinter()
            .writeValue(outputStream, result);
    }
}
```

---

# 5. 推荐最终设计

```text
JSON = 主输入 / 主输出
Markdown = 展示报告
Excel = 给业务确认用，可选
```

也就是：

```text
usecase.json
   ↓
Java Batch
   ↓
run-result.json
diff-result.json
   ↓
result.md
diff.md
```

结论：

```text
文件流 JSON 不但能搞定，而且是最稳的实现方式。
Markdown 可以保留为人看的报告，不建议作为唯一机器输入。
```

## 第 19 轮

### 你

json哪个是文件的内容

### ChatGPT

这个问题问得非常好。

我觉得你现在发现了我前面方案里最大的缺陷。

对于 E6 这种 API 测试工具来说：

```text
JSON 适合描述：
- API定义
- UseCase定义
- 验证规则

但是不适合描述：
- 文件内容
- 文件流
- PDF
- Excel
- 图片
- 二进制
```

因为 JSON 本身不能直接保存文件流。

---

# 方案1 Base64（不推荐）

例如：

```json
{
  "fileName": "test.pdf",
  "contentType": "application/pdf",
  "content": "JVBERi0xLjQKJ..."
}
```

问题：

```text
文件变大30%以上
JSON巨大
Git diff失效
不好维护
```

工业项目基本不用。

---

# 方案2 文件引用（推荐）

UseCase只保存文件路径。

例如：

```json
{
  "stepNo": 1,
  "apiId": "uploadDocument",
  "request": {
    "file": {
      "source": "file",
      "path": "resources/test.pdf"
    }
  }
}
```

运行时：

```text
UseCase JSON
    ↓
读取 path
    ↓
FileResolver
    ↓
InputStream
    ↓
API Upload
```

---

# 方案3 Resource目录（最推荐）

目录：

```text
usecases/
  UC001/

    usecase.json

    resources/
      test.pdf
      image1.png
      sample.xlsx
```

JSON：

```json
{
  "apiId": "uploadDocument",
  "request": {
    "file": {
      "resource": "test.pdf"
    }
  }
}
```

运行时：

```java
Path resourcePath =
    useCaseRoot
      .resolve("resources")
      .resolve("test.pdf");

InputStream is =
    Files.newInputStream(resourcePath);
```

---

# 文件上传请求设计

定义统一对象：

```java
public class FileResource {

    private String resourceName;

    private String contentType;

}
```

---

# Request模型

不要：

```java
byte[]
```

要：

```java
InputStream
```

或者：

```java
Path
```

例如：

```java
public class RequestFile {

    private String fileName;

    private Path filePath;

    private String contentType;

}
```

---

# API执行器

统一：

```java
MultipartFileRequest
```

例如：

```java
public class MultipartRequestBuilder {

    public HttpEntity<?> build(
        RequestFile file) {

        Resource resource =
            new FileSystemResource(
                file.getFilePath());

        ...
    }
}
```

---

# Response如果返回文件怎么办

E6虽然不太常见，但以后可能会有：

```text
PDF
CSV
Excel
Statement
Image
```

例如：

```http
Content-Type: application/pdf
```

不要保存到 JSON。

应该：

```text
runs/

  raw/

    response.pdf

  metadata/

    response.json
```

metadata：

```json
{
  "fileName": "response.pdf",
  "contentType": "application/pdf",
  "size": 103424
}
```

---

# Contract比较怎么办

文件流无法比较 JSON。

要比较：

```text
文件名
ContentType
文件大小
SHA256
```

例如：

```json
{
  "responseFile": {
    "fileName": "statement.pdf",
    "contentType": "application/pdf",
    "size": 103424,
    "sha256": "A34F..."
  }
}
```

比较：

```text
size变化
sha变化
mime变化
```

---

# 我建议增加一个 Resource Layer

这是后面一定会用到的。

```text
e6-validator-common

  resource/

    ResourceResolver
    ResourceLoader

    LocalResourceProvider
    ZipResourceProvider
    S3ResourceProvider

    ResourceMetadata

    FileHashCalculator
```

统一接口：

```java
public interface ResourceProvider {

    InputStream open(
        String resourceName);

    ResourceMetadata getMetadata(
        String resourceName);
}
```

---

# 最终工业版结构

```text
usecases/

  UC001/

    usecase.json

    resources/

      test.pdf
      test.xlsx
      image.png

runs/

  run_xxx/

    raw/

      upload_request.json

      statement.pdf

    metadata/

      statement.metadata.json

    reports/

      result.md

      diff.md
```

---

所以最终答案是：

```text
JSON里面不要存文件内容
JSON里面只存文件引用
真正文件放 resources 目录
运行时转换成 InputStream
Response文件保存到 runs/raw
比较时比较 metadata + hash
```

这才是企业级 Batch、Agent、RAG 系统里处理文件流最稳定的方案。

## 第 20 轮

### 你

现在手头关于业务信息有如何调用e6api的设计书 有flow说明 但是咱们只需要验证调用api的usecase不需要业务调用业务实现。还知道 业务系统和这个测试工具调用一个E6业务系统 那么更新等处理会有影响 。还知道 这个系统是linux jdk tomcat的平台执行 上面有其他系统也在运行。 我需要注意什么样的问题

### ChatGPT

这个前提很重要：你的工具不是业务系统的一部分，而是“外部黑盒验证器”。所以重点要从功能设计转到运行安全、数据隔离、环境影响、权限和可恢复性。

### ChatGPT

你需要特别注意这几类问题。

# 1. 绝对不要影响真实业务数据

因为业务系统和测试工具都调用同一个 E6 业务系统。

所以必须设计：

```text
测试专用 customer
测试专用 account
测试专用 card / ledger
测试专用 externalId
测试专用 idempotencyKey
测试专用 prefix
```

例如：

```text
externalCustomerId = E6TEST_${usecase}_${runId}
requestId          = E6TEST_${runId}_${stepNo}
idempotencyKey     = E6TEST_${runId}_${apiId}
```

所有测试数据都必须能识别、能清理、不能和业务数据混在一起。

---

# 2. 更新系 API 要非常小心

如果 API 会产生数据变更，比如：

```text
create
update
delete
fund
payment
cancel
settlement
status change
```

必须分级。

```text
READ_ONLY      只查询
SAFE_WRITE     写测试专用数据
DANGEROUS      可能影响真实业务
FORBIDDEN      禁止自动执行
```

默认只允许：

```text
READ_ONLY
SAFE_WRITE
```

`DANGEROUS` 必须显式参数才允许：

```bash
--allow-dangerous
```

---

# 3. 一定要有环境保护

不能让 DEV 的测试误打到 UAT / PROD。

配置里必须明确：

```json
{
  "env": "DEV",
  "baseUrl": "https://xxx-dev",
  "allowWrite": true,
  "allowDangerous": false
}
```

启动时打印并要求确认，尤其是 PROD：

```text
ENV=PROD
WRITE=true
危险：当前环境禁止自动写入
```

建议直接设计：

```text
PROD 默认禁止写 API
```

---

# 4. 不能部署成影响 Tomcat 的重任务

既然服务器上有 Tomcat 和其他系统，最好不要把验证 Batch 跑在 Tomcat 进程里。

推荐：

```text
独立 java -jar 执行
独立用户
独立目录
独立日志
独立内存限制
独立 cron / shell
```

不要：

```text
放进 Tomcat webapp 里跑大批量验证
```

否则会影响其他系统。

---

# 5. Linux 运行资源限制

启动脚本必须限制资源：

```bash
java -Xms128m -Xmx512m \
  -jar e6-api-flow-validator.jar
```

注意：

```text
CPU不能打满
内存不能无限增长
日志不能写爆磁盘
临时文件必须清理
连接必须有 timeout
API必须有 retry 上限
```

---

# 6. 并发控制

你前面说业务上不会同一个 usecase 一起跑。
系统上还是要防误操作。

```text
锁粒度：
env + usecase
```

锁文件：

```text
locks/DEV_PaymentFlow.lock
```

发现同 usecase 正在跑：

```text
直接退出
不要并行执行
```

---

# 7. Timeout 和 Retry 必须保守

不能因为 API 平台慢，就把连接挂死。

建议：

```text
connectTimeout = 5秒
readTimeout    = 30秒
retry          = 0~2次
retryInterval  = 1~3秒
```

并且：

```text
POST/更新类 API 默认不自动 retry
```

因为可能造成重复交易、重复创建、重复扣款。

---

# 8. Idempotency Key 必须强制

所有写入类 API 都要有：

```text
requestId
correlationId
idempotencyKey
```

而且和 runId 绑定。

```text
idempotencyKey = ${runId}_${stepNo}_${apiId}
```

这样即使误重试，也能降低重复处理风险。

---

# 9. 敏感信息必须 Mask

日志和报告里不能直接输出：

```text
token
authorization
api key
password
card number
PAN
CVV
个人信息
```

必须输出：

```text
Authorization: Bearer ****
cardNumber: ************1234
```

raw 文件也要分级：

```text
raw_original/   受限保存，可关闭
raw_masked/     默认保存
```

---

# 10. Baseline 不要自动更新

不要每次跑完都覆盖基准。

必须人工确认：

```bash
approve-baseline --run-id xxx
```

否则 API 平台已经坏了，你还把坏结果当成新基准。

---

# 11. 清理机制必须有

测试数据和文件都要能清理。

```text
cleanup usecase
cleanup API
cleanup policy
retention days
```

例如：

```bash
java -jar e6-validator.jar cleanup --older-than 30d
```

清理：

```text
runs旧目录
tmp文件
过期lock
测试用customer/account
```

---

# 12. 结果判断不能只看 200

E6 这种业务 API，重点是业务结果。

必须检查：

```text
status code
业务status
errorCode
balance变化
transaction状态
ledger entry
response字段结构
后续API是否还能接上
```

---

# 13. 最终注意点总结

你现在这个项目最重要的是：

```text
1. 测试数据和真实业务数据隔离
2. 写入类API必须有保护
3. 同usecase禁止并行
4. 不在Tomcat进程里跑重Batch
5. 限制CPU/内存/日志/磁盘
6. 所有API设置timeout
7. POST类API谨慎retry
8. 所有敏感信息mask
9. baseline人工批准
10. 每次执行都有runId和证迹
```

一句话：

```text
这个工具不是难在调用API，而是难在“安全地调用API，并且不影响同一E6系统上的真实业务”。
```

## 第 21 轮

### 你

这些注意点 你分下类 哪些我需要和业务team或者E6去协调

### ChatGPT

这是一个非常好的问题。

因为这里面有些是**你自己能决定的技术设计**，有些是**必须向业务团队确认**，还有一些是**必须向 E6 团队确认**。

如果不区分，后面会浪费很多时间。

---

# A类：你自己就能决定（开发团队内部）

这些不用问业务，也不用问 E6。

## A-1 Run管理

```text
runId生成规则
executionId设计
目录结构
日志结构
lock机制
baseline机制
diff机制
```

例如：

```text
runs/
baseline/
logs/
reports/
```

完全自己决定。

---

## A-2 报告设计

```text
result.md
diff.md
result.json
diff.json
```

以及：

```text
字段类型变化
字段新增删除
status code变化
```

这些规则你自己定义。

---

## A-3 Batch运行方式

```text
Java17
Jar执行
Linux Cron
JP1
Jenkins
```

自己决定。

---

## A-4 通用技术规则

```text
timeout
retry
mask
hash
file保存
资源限制
```

这些都是内部实现。

---

# B类：必须和业务Team确认

这类最重要。

因为你验证的是业务流程，不是 API 本身。

---

## B-1 哪些是UseCase

这是第一件事。

例如：

```text
UC001 Create Customer
UC002 Create Account
UC003 Fund Account
UC004 Payment Success
UC005 Payment Failure
```

必须业务确认。

因为：

```text
你不知道哪些流程真正重要
```

---

## B-2 哪些字段是业务关键字段

例如：

```json
{
  "customerId":"",
  "status":"",
  "nickname":""
}
```

业务会告诉你：

```text
customerId -> 关键
status -> 关键
nickname -> 不关键
```

否则你会产生大量无意义Diff。

---

## B-3 哪些变化算异常

例如：

```text
status
0 → 1
```

有可能：

```text
业务认为正常
```

也可能：

```text
业务认为重大异常
```

必须确认。

---

## B-4 最终业务检查规则

例如：

```text
余额变化
交易状态
账户状态
```

必须业务定义。

例如：

```text
fund 1000
payment 300

最终余额=700
```

这个规则不是你发明的。

---

## B-5 测试数据生命周期

必须确认：

```text
测试customer保留多久
测试account保留多久
是否允许删除
```

---

# C类：必须和E6 Team确认

这一类非常重要。

---

## C-1 API兼容策略

必须问：

```text
E6升级时是否保证Backward Compatibility
```

例如：

```text
字段新增
字段删除
字段类型变化
```

是否允许。

很多系统有官方规则。

---

## C-2 E6版本信息

你必须知道：

```text
当前版本
升级计划
发布时间
```

否则：

```text
发现Diff
不知道是不是升级导致
```

---

## C-3 Idempotency规则

必须确认：

```text
requestId
correlationId
idempotencyKey
```

哪些API支持。

例如：

```text
create payment
fund
transfer
```

是否幂等。

---

## C-4 Rate Limit

必须确认：

```text
QPS限制
分钟限制
小时限制
```

否则批量测试可能被封。

---

## C-5 Sandbox / Test Tenant

最关键之一。

问：

```text
有没有专门测试Tenant
有没有Sandbox
有没有测试Program
```

如果有：

```text
绝对优先用Sandbox
```

---

## C-6 Error Code定义

例如：

```text
400
401
403
409
422
500
```

哪些是预期错误。

必须有文档。

---

## C-7 数据清理策略

必须问：

```text
测试数据能否删除
多久自动清理
是否影响业务统计
```

---

# D类：业务Team + E6 Team一起确认

这部分经常扯皮。

---

## D-1 测试数据命名规范

例如：

```text
E6TEST_*
```

业务同意吗？

E6允许吗？

---

## D-2 测试执行时间

例如：

```text
凌晨
白天
生产冻结期间
```

需要双方同意。

---

## D-3 升级验证范围

例如：

```text
每次E6升级

验证哪些UseCase
验证哪些API
哪些必须PASS
哪些允许Warning
```

---

# 最优先先去问的10个问题

如果我是架构师，下周开会我先问这10个：

```text
1. 当前有哪些核心UseCase需要验证？

2. 哪些UseCase是P1？

3. 哪些字段属于业务关键字段？

4. 哪些变化必须报警？

5. 是否有Sandbox环境？

6. 是否有专门测试Tenant？

7. 是否支持Idempotency Key？

8. E6升级兼容策略是什么？

9. 测试数据是否允许长期存在？

10. 升级后验收标准是什么？
```

---

# 责任边界图

```text
你负责
────────────────────
Batch设计
Run管理
Diff引擎
Report
日志
锁
目录结构

业务Team负责
────────────────────
UseCase
业务规则
关键字段
验收标准

E6负责
────────────────────
API定义
兼容策略
限流
幂等
错误码
Sandbox

双方负责
────────────────────
测试数据
执行窗口
升级验收范围
```

这是最适合你当前项目推进的分工方式。现在你的第一步其实不是写代码，而是先把 **B类和C类问题整理成一份确认清单**，拿着去和业务团队、E6团队分别确认。这样后面的设计才不会反复推翻。

## 第 22 轮

### 你

业务team还有一个 这个检查工具是我们自己设计验证方式 但是api是E6网站上有api说明文档 ，调用这些API的业务逻辑的业务team的设计书也有，但是我们这个工具的实现目标就是验证是否有变化 本来E6 api的解释权也不在现行的业务team。现行team也只是在使用e6 api ，倒是知道在某种情况下如何使用。 那么针对这个业务team ，我需要了解和协调什么。针对检查工具的实现 我需要了解E6API  可以在E6和业务team分别可以提供或者获得什么。另外，作为工具本身设计的业务 咱们可以根据这些确认内容及现实经验规则 如何决定。

### ChatGPT

这次要把责任边界再切细：业务 Team 不是 E6 API 的解释者，但他们是“本系统如何使用 E6 API”的解释者。所以检查工具的规则来源会分成三层：E6官方契约、现行业务使用方式、工具自身安全规则。

### ChatGPT

你这个理解是对的。

业务 Team 不负责解释 E6 API 本身。
他们负责解释：

```text
现行业务系统在什么场景下，如何使用 E6 API。
```

所以要分三层。

---

# 1. 三个责任来源

```text
E6 官方
  ↓
API 本身规格、兼容性、错误码、限制

业务 Team
  ↓
本系统实际怎么用 E6 API

检查工具 Team
  ↓
如何验证、如何判定差异、如何出报告
```

---

# 2. 向业务 Team 需要确认什么

## 2.1 现行业务 UseCase

你要问：

```text
当前系统有哪些调用 E6 的业务流程？
哪些流程最重要？
哪些流程升级前后必须确认？
```

例如：

```text
开户
账户查询
入金
出金
交易
取消
余额查询
状态变更
```

---

## 2.2 每个 UseCase 的 API 调用顺序

业务 Team 应该提供：

```text
这个业务场景下：
第1个 API 调什么
第2个 API 调什么
第3个 API 依赖哪个返回值
失败时是否继续
```

他们不解释 API 语义，但他们知道现行系统怎么调用。

---

## 2.3 现行系统实际使用的字段

你要确认：

```text
request 里实际设了哪些字段
response 里实际使用了哪些字段
哪些字段只是返回了但系统没用
```

这非常关键。

否则你会把所有 response 字段都当关键字段，diff 会很多。

---

## 2.4 关键业务字段

业务 Team 需要告诉你：

```text
哪些字段变化会影响业务？
哪些字段变化可以忽略？
```

例如：

```text
transactionId       关键
status              关键
balance             关键
createdAt           可能忽略
message             可能忽略
traceId             忽略
```

---

## 2.5 正常场景和异常场景

你要让业务 Team 给：

```text
正常场景
异常场景
边界场景
```

例如：

```text
余额充足支付成功
余额不足支付失败
重复请求
不存在账户
冻结账户交易
非法金额
```

---

## 2.6 验收标准

比如：

```text
升级后什么叫OK？
什么叫NG？
什么叫Warning？
```

这部分必须业务 Team 决定。

---

## 2.7 测试数据规则

确认：

```text
测试用 customer/account/card 能否创建？
是否允许残留？
是否需要清理？
是否影响业务报表？
是否有专用 test tenant / test program？
```

---

# 3. 向 E6 需要确认什么

## 3.1 API 官方规格

需要拿到：

```text
endpoint
method
request schema
response schema
required
type
max length
enum
error code
status code
```

---

## 3.2 版本和升级规则

确认：

```text
E6什么时候升级？
升级会不会提前通知？
是否有release note？
是否保证向后兼容？
字段新增/删除/类型变化算不算破坏性变更？
```

---

## 3.3 幂等规则

确认：

```text
哪些API支持 idempotency key？
重复 requestId 会怎样？
超时后重试安全吗？
```

这个非常重要。

---

## 3.4 限流和执行限制

确认：

```text
每秒最多多少请求？
批量测试是否允许？
是否会触发风控？
测试数据是否会影响限额？
```

---

## 3.5 测试环境

确认：

```text
有没有 sandbox？
有没有 test tenant？
有没有专用 program？
有没有测试账号？
是否和业务系统共享数据？
```

---

## 3.6 错误码和异常响应

确认：

```text
400 / 401 / 403 / 409 / 422 / 500
各自代表什么？
业务错误码有哪些？
哪些错误是预期错误？
```

---

# 4. 检查工具自己决定什么

你们工具侧可以根据现实经验直接决定。

## 4.1 差异判定规则

默认规则可以是：

```text
字段删除       HIGH
字段类型变化   HIGH
必填字段缺失   HIGH
status code变化 HIGH
新增字段       LOW
非关键字段值变化 LOW
关键字段值变化 HIGH
```

---

## 4.2 Baseline机制

工具自己决定：

```text
baseline 必须人工批准
不能自动覆盖
每个 usecase 一个 approved baseline
```

---

## 4.3 安全规则

工具自己决定：

```text
PROD禁止写API
写API必须 test prefix
同usecase禁止并行
POST默认不自动retry
日志必须mask
```

---

## 4.4 输出文档

工具自己决定：

```text
result.json
diff.json
result.md
diff.md
raw request/response
contract snapshot
```

---

# 5. 最重要的设计原则

你这个工具不是判断：

```text
E6 API 正不正确
```

而是判断：

```text
本系统依赖的 E6 API 使用方式有没有被破坏
```

所以判断标准是三层叠加：

```text
E6官方规格
+
现行业务使用方式
+
工具默认安全规则
```

---

# 6. 最终确认表

| 项目 | E6提供 | 业务Team提供 | 工具决定 |
|---|---|---|---|
| API endpoint | 是 | 参考 | 否 |
| request schema | 是 | 实际使用字段 | 比较规则 |
| response schema | 是 | 实际使用字段 | 比较规则 |
| enum | 是 | 业务关键enum | 变化判定 |
| error code | 是 | 哪些错误场景会出现 | 严重度 |
| usecase顺序 | 否 | 是 | 执行编排 |
| 参数传递关系 | 否 | 是 | JsonPath实现 |
| 关键字段 | 否 | 是 | 报告突出 |
| baseline | 否 | 批准 | 工具保存 |
| retry规则 | 幂等信息 | 业务风险判断 | 默认保守 |
| 测试数据 | 环境限制 | 数据规则 | prefix隔离 |

---

# 7. 你可以这样向业务 Team 说明

```text
我们不是让业务 Team 解释 E6 API 官方含义。
我们需要业务 Team 提供“现行业务系统如何使用 E6 API”的信息。

包括：
1. 哪些业务流程调用了 E6
2. 每个流程调用哪些 API
3. API 调用顺序
4. 前后 API 参数如何传递
5. 业务系统实际使用哪些 request/response 字段
6. 哪些字段变化会影响业务
7. 哪些正常/异常场景需要回归确认
8. 测试数据如何准备和清理
```

---

# 8. 你可以这样向 E6 确认

```text
我们要做一个黑盒回归验证工具，用于确认本系统依赖的 E6 API 在升级前后是否发生影响性变化。

请提供或确认：
1. API官方规格
2. request/response schema
3. 字段类型、长度、required、enum
4. error code
5. status code规则
6. 版本升级通知方式
7. 兼容性策略
8. idempotency规则
9. rate limit
10. sandbox/test tenant
```

---

# 9. 工具业务规则如何决定

你们可以按这个现实规则定：

```text
只要影响现行业务系统使用字段，就是HIGH。
只影响未使用字段，就是LOW。
无法继续usecase，就是BLOCKER。
E6官方允许的新增字段，默认LOW。
E6官方未通知的删除/类型变化，默认HIGH。
写API重试默认关闭。
baseline必须人工批准。
```

---

最终结论：

```text
业务 Team 不是 E6 API 的解释者。
业务 Team 是“现行业务使用方式”的解释者。

E6 是“API契约”的解释者。

检查工具是“变化检测和风险判定”的执行者。
```

这样责任边界就非常清楚。

## 第 23 轮

### 你

业务team是现行系统的解释者 但是他们是基于正确的业务流使用API。 而检查api的业务流则不需要中间那些编辑 业务系统的本身业务处理。所以咱们的调用testcase如何设计 可能不是由业务teams来定，而是由检查工具team来理解业务流 自己设计测试工作流 极简的实现usecase的api调用。这种情况下 什么是关键点

### ChatGPT

我认为你已经把这个项目的本质看出来了，而且这个判断非常重要。

你现在要做的其实不是：

```text
业务系统回归测试工具
```

而是：

```text
E6 API Consumer Contract Validator
```

也就是说：

```text
我们不验证业务系统实现
我们验证：
如果按照正确方式使用 E6 API
E6 是否仍然满足原来的契约
```

这是完全不同的目标。

---

# 1. 最容易犯的错误

很多团队会这样设计：

```text
现行业务系统
 ↓
复制全部业务逻辑
 ↓
测试
```

最后得到：

```text
100个UseCase
300个画面
500个Batch
200个IF
```

然后：

```text
升级一次
跑两天
没人看结果
```

这种方式最后一定失败。

---

# 2. 你的工具应该验证什么

应该验证：

```text
E6 API最小可运行业务链
```

例如：

```text
Create Customer
 ↓
Create Account
 ↓
Get Account
```

你不关心：

```text
画面
审批
通知
DB更新
日志
Batch
MQ
```

这些是业务系统自己的事。

---

# 3. 业务Team真正价值

业务Team最大的价值不是：

```text
解释API
```

而是：

```text
告诉你：

为了完成这个业务目标，
最少需要调用哪些API
```

例如：

业务系统：

```text
开户
 ↓
画面输入
 ↓
校验
 ↓
审批
 ↓
DB
 ↓
调用E6
 ↓
邮件
 ↓
通知
```

但是你的测试工具：

```text
CreateCustomer
 ↓
CreateAccount
```

结束。

---

# 4. 测试工具UseCase设计原则

不是：

```text
业务UseCase
```

而是：

```text
E6 Capability UseCase
```

例如：

---

## UC01 Customer Lifecycle

验证：

```text
Create Customer
Get Customer
Update Customer
```

---

## UC02 Account Lifecycle

验证：

```text
Create Account
Get Account
Close Account
```

---

## UC03 Balance Flow

验证：

```text
Fund
Balance
Debit
Balance
```

---

## UC04 Transaction Flow

验证：

```text
Create Transaction
Get Transaction
```

---

## UC05 Error Flow

验证：

```text
非法参数
缺失参数
不存在ID
重复请求
```

---

# 5. UseCase设计目标

不要问：

```text
业务系统怎么实现？
```

而要问：

```text
如何最小化验证这个API能力？
```

例如：

---

业务系统：

```text
开户
```

可能：

```text
20个API
5个DB
3个审批
```

你：

```text
CreateCustomer
CreateAccount
```

即可。

---

# 6. 真正关键点

你们工具应该验证三层。

---

## Layer1 API Contract

验证：

```text
request字段
response字段
类型
长度
required
enum
```

例如：

```text
customerId
string
36
```

有没有变化。

---

## Layer2 API Behavior

验证：

```text
同样请求
返回是否一样
状态码是否一样
业务状态是否一样
```

例如：

```text
ACTIVE
```

变成：

```text
1
```

就要发现。

---

## Layer3 Capability Flow

验证：

```text
Create Customer
 ↓
Create Account
 ↓
Fund
 ↓
Balance
```

是否还能跑通。

---

# 7. 业务Team应该提供什么

现在就变得简单了。

你不需要：

```text
业务设计书全部内容
```

你需要：

---

## 业务流程图

例如：

```text
开户

1 Create Customer
2 Create Account
3 Activate Account
```

---

## API调用顺序

例如：

```text
A
 ↓
B
 ↓
C
```

---

## 参数依赖

例如：

```text
customerId
来自CreateCustomer
```

---

## 最终业务结果

例如：

```text
余额应该增加
状态应该ACTIVE
```

---

# 8. E6应该提供什么

---

## API契约

```text
OpenAPI
Swagger
Schema
```

---

## Enum定义

例如：

```text
ACTIVE
SUSPENDED
CLOSED
```

---

## Error定义

例如：

```text
40001
40002
50001
```

---

## Version Policy

例如：

```text
新增字段允许
删除字段禁止
```

---

# 9. 工具Team自己决定什么

这部分最多。

---

## Capability UseCase

你自己设计。

例如：

```text
UC01 Customer
UC02 Account
UC03 Balance
UC04 Transaction
UC05 Error
```

---

## Diff规则

你自己设计。

---

## Severity

你自己设计。

---

## Baseline

你自己设计。

---

## Markdown格式

你自己设计。

---

# 10. 最终最重要的原则

我建议你把项目目标重新定义成：

```text
验证E6能力
而不是验证业务系统
```

然后UseCase定义变成：

```text
Capability-Based UseCase
```

而不是：

```text
Business-System UseCase
```

例如：

```text
UC001 Create Customer

目标：
验证Customer API能力

最小链路：
Create Customer
Get Customer

验证：
Contract
Behavior
Flow
```

这样以后：

```text
E6升级
↓
跑20个Capability UseCase
↓
30分钟
↓
出Diff报告
```

就能知道：

```text
Customer API变了
Account API没变
Transaction API变了
```

而不用复制整个业务系统逻辑。

对于你这个项目，我认为这是最核心的设计原则，也是后面所有 UseCase 设计的出发点。

## 第 24 轮

### 你

是的 认识是对的 现在是一组usecass其实也是业务里的flow一样实现 不过没必要同样实现 那么如何保证只有第一个api是用户指定后面的api都是根据前面的API来调用 。要做到这种设计程度 我们必须要做什么样的设计 。现在也有业务系统的flow设计书 ，我们需要在这个基础上 ，做同样的设计书吗

### ChatGPT

这里要把“业务系统 flow 设计书”和“检查工具 usecase 设计书”分开。前者说明完整业务怎么做，后者只说明为了验证 E6 能力，最小 API 链如何跑通。

### ChatGPT

是的，**需要做一份新的检查工具用 UseCase 设计书**。
但它不是复制业务系统 flow 设计书，而是从业务 flow 里抽出 **最小 API 调用链**。

---

# 1. 两种设计书不同

```text
业务系统Flow设计书
= 完整业务实现

检查工具UseCase设计书
= 最小API验证链
```

业务系统设计书里可能有：

```text
画面输入
业务校验
DB更新
审批
日志
通知
状态管理
E6 API调用
```

检查工具只需要：

```text
入口参数
API调用顺序
前后API参数传递
期待状态
期待返回字段
差异检查规则
```

---

# 2. 如何保证只有第一个API由用户指定

核心是设计 **Context变量池**。

执行规则：

```text
Step1：
用户指定入口参数

Step2以后：
只能从以下来源取值：
1. 前面API response抽取值
2. 固定系统变量
3. runId生成值
4. 环境配置
```

不允许随便手动填。

---

# 3. UseCase设计书必须写清楚4件事

## 3.1 入口参数

只允许第一个 API 使用。

```json
"entryInput": {
  "customerName": "TEST_${runId}",
  "currency": "JPY"
}
```

---

## 3.2 每一步 API

```json
{
  "stepNo": 1,
  "apiId": "createCustomer",
  "method": "POST",
  "url": "/customers"
}
```

---

## 3.3 抽取规则

从 response 里取出后续需要的值。

```json
"extract": [
  {
    "name": "CUSTOMER_ID",
    "from": "$.customerId",
    "required": true
  }
]
```

---

## 3.4 参数绑定规则

后续 API 只能引用 context。

```json
"request": {
  "body": {
    "customerId": "${CUSTOMER_ID}"
  }
}
```

---

# 4. 最小UseCase JSON例子

```json
{
  "useCaseId": "UC001",
  "name": "CreateCustomerAndAccount",
  "entryInput": {
    "customerName": "TEST_${runId}",
    "currency": "JPY"
  },
  "steps": [
    {
      "stepNo": 1,
      "apiId": "createCustomer",
      "method": "POST",
      "url": "/customers",
      "request": {
        "body": {
          "name": "${entry.customerName}"
        }
      },
      "expectedStatus": 200,
      "extract": [
        {
          "name": "CUSTOMER_ID",
          "from": "$.customerId",
          "required": true
        }
      ]
    },
    {
      "stepNo": 2,
      "apiId": "createAccount",
      "method": "POST",
      "url": "/accounts",
      "request": {
        "body": {
          "customerId": "${CUSTOMER_ID}",
          "currency": "${entry.currency}"
        }
      },
      "expectedStatus": 200,
      "extract": [
        {
          "name": "ACCOUNT_ID",
          "from": "$.accountId",
          "required": true
        }
      ]
    }
  ]
}
```

重点是：

```text
Step2 不能手动指定 customerId。
必须来自 Step1 response。
```

---

# 5. 工具层必须强制校验

执行前先做 `Spec Validation`：

```text
1. stepNo > 1 的 request 不允许使用 manual value
2. 引用的变量必须已在前序 step extract 出来
3. required extract 取不到时立即失败
4. 后续 API 不能跳过必要依赖
5. 禁止引用未来 step 的值
```

例如：

```text
Step2 引用了 ${CUSTOMER_ID}
系统检查 CUSTOMER_ID 是否由 Step1 extract
如果没有，启动前直接报错
```

---

# 6. Context设计

运行时维护：

```json
{
  "entry": {
    "customerName": "TEST_DEV_xxx",
    "currency": "JPY"
  },
  "runtime": {
    "runId": "DEV_UC001_20260624..."
  },
  "variables": {
    "CUSTOMER_ID": "C123",
    "ACCOUNT_ID": "A456"
  }
}
```

每一步执行：

```text
读取request模板
替换变量
调用API
保存response
extract变量
放入context
继续下一步
```

---

# 7. 是否需要同样的设计书？

需要，但不是“同样”。

应该叫：

```text
API Verification UseCase Spec
```

它基于业务 flow 设计书，但只抽取：

```text
E6 API调用部分
参数依赖
期待结果
检查规则
```

可以这样写：

```text
来源：
业务Flow设计书：XX章
抽取目标：
验证E6 Customer + Account API链路
省略内容：
画面、DB、审批、通知、业务内部状态
```

---

# 8. 推荐设计书章节

```text
1. UseCase概要
2. 参考的业务Flow设计书
3. 验证目标
4. 入口参数
5. API调用链
6. 参数传递关系
7. 每个API期待结果
8. 抽取变量定义
9. 业务检查规则
10. 差异检查规则
11. 异常时停止规则
12. 测试数据清理规则
```

---

# 9. 最关键点

你要保证的不是：

```text
和业务系统完全一样
```

而是：

```text
用最小调用链覆盖业务系统依赖的E6能力
```

所以设计标准是：

```text
能少一步就少一步
但不能少掉E6依赖关系
```

例如：

```text
create customer → create account
```

如果业务系统中间有 DB 保存、画面确认、审批，这些全部不要。

---

# 10. 结论

你必须做新的 UseCase 设计书。

它的定位是：

```text
从业务Flow设计书抽取出来的
E6 API最小验证流程设计书
```

并且工具必须强制：

```text
第一个API = entry input
后续API = 只能从前序response / runtime / env 取值
```

这样才能保证：

```text
不是人在每一步手动拼API
而是真正验证API链路是否还能连续跑通
```

## 第 25 轮

### 你

系统背景就是这样 我现在需要整理一些qa  什么是比较重要的必须提前确认内容

### ChatGPT

以你现在的背景来看：

```text
E6 API Provider
    ↑
现行业务系统（生产使用者）
    ↑
你们的 API Verification Tool（新开发）
```

你们的工具目标：

```text
验证 E6 API 是否发生影响性变化
验证 E6 API 链路是否仍然成立
验证现行业务系统依赖的 E6 能力是否被破坏
```

所以现在最重要的不是技术，而是把 **未知事项（Unknowns）变成已确认事项（Confirmed）**。

我建议把 QA 分成 6 个分类。

---

# P0：必须最先确认（否则设计不了）

## Q1. E6升级的触发点是什么？

```text
什么时候跑验证？

E6升级前？
E6升级后？
每周？
每月？
人工触发？
CI自动触发？
```

因为这决定：

```text
Baseline
Diff
报告
```

的设计。

---

## Q2. 验证目标是什么？

这是最重要的问题。

例如：

```text
A.
验证API Schema变化

B.
验证API行为变化

C.
验证业务链路变化

D.
全部验证
```

很多项目最后发现：

```text
其实只需要验证 Schema
```

或者：

```text
必须验证整个 Capability Flow
```

成本差10倍。

---

## Q3. 最终谁签字？

必须问。

```text
Diff报告谁看？

业务Team？
E6 Team？
QA Team？
开发Team？
运维Team？
```

因为：

```text
报告内容
粒度
格式
```

完全不一样。

---

# P1：向业务Team确认

---

## Q4. 系统依赖哪些 E6 Capability？

不要问：

```text
有哪些API
```

而要问：

```text
系统依赖哪些能力？
```

例如：

```text
Customer
Account
Balance
Transaction
Card
Authorization
Settlement
```

---

## Q5. 哪些能力是P1？

例如：

```text
Balance 查询
Payment
Fund
```

必须验证。

而：

```text
Address Update
```

可能不重要。

---

## Q6. 最小业务链是什么？

例如：

```text
CreateCustomer
↓
CreateAccount
↓
Fund
↓
Balance
```

业务Team最清楚。

---

## Q7. 哪些字段真正被业务系统使用？

这是超级重要的问题。

例如：

response：

```json
{
  "customerId":"",
  "status":"",
  "createdAt":"",
  "traceId":"",
  "message":""
}
```

真正业务使用：

```text
customerId
status
```

其它：

```text
完全没用
```

那么 Diff 规则就不一样。

---

## Q8. 哪些异常场景最重要？

例如：

```text
余额不足
账户冻结
客户不存在
重复请求
```

这些应该优先进入 UseCase。

---

# P1：向E6确认

---

## Q9. 是否有 OpenAPI / Swagger？

必须拿到。

否则：

```text
字段
类型
长度
required
```

没法自动比对。

---

## Q10. 是否有 Version Policy？

例如：

```text
新增字段允许
删除字段禁止
类型变化禁止
```

这是 Diff 判断依据。

---

## Q11. 是否有 Release Note？

每次升级：

```text
改了什么
什么时候改
哪些API受影响
```

否则 Diff 出来无法解释。

---

## Q12. 是否有 Sandbox？

这个必须问。

如果没有：

```text
测试数据管理
风险
```

都会变复杂。

---

## Q13. Rate Limit 是多少？

否则：

```text
100个UseCase一起跑
```

可能被限流。

---

## Q14. Idempotency 规则？

哪些 API：

```text
允许重试
不允许重试
```

必须知道。

---

# P1：工具团队自己确认

---

## Q15. Baseline 定义是什么？

例如：

```text
最后一次成功
还是

人工批准版本
```

我建议：

```text
人工批准版本
```

---

## Q16. Diff 粒度是什么？

比较：

```text
字段
类型
长度
值
行为
业务结果
```

哪些必须做。

---

## Q17. UseCase 粒度是什么？

例如：

```text
一个 Capability 一个 UseCase

还是

一个 API 一个 UseCase
```

我建议：

```text
Capability Level
```

---

## Q18. 失败策略是什么？

例如：

```text
Step2失败

停止？

继续？
```

通常：

```text
依赖失败停止
```

---

# P2：运维环境确认

---

## Q19. 部署位置？

```text
独立Linux
现行业务服务器
Tomcat服务器
```

---

## Q20. 执行频率？

```text
按需
每日
每周
升级后
```

---

## Q21. 数据保留多久？

```text
run
raw
diff
logs
```

保存：

```text
30天？
90天？
1年？
```

---

# 我认为最关键的10个问题

如果只能问10个。

我会问：

```text
1. 系统依赖哪些E6 Capability？

2. 哪些Capability是P1？

3. 每个Capability最小API链是什么？

4. 哪些response字段真正被业务系统使用？

5. 哪些异常场景必须验证？

6. E6是否提供OpenAPI/Swagger？

7. E6兼容性策略是什么？

8. 是否有Sandbox？

9. Diff报告谁最终确认？

10. Baseline由谁批准？
```

---

如果这10个问题全部得到答案。

其实：

```text
UseCase设计
Diff规则
Report设计
技术架构
```

基本都可以定稿了。

以架构师角度看，目前最缺的不是代码，而是：

```text
Capability清单
关键字段清单
最小API链清单
```

这三个清单拿到之后，你的 UseCase Spec 基本就能开始设计了。

## 第 26 轮

### 你

又加了一个要件 就是发布是和业务team的执行环境，但是我们检查工具team用的开发环境没有、必须做一套和业务开发系统一样的环境 只是里面的调用元不是业务系统了 而是只有检查工具了。但是目前不清楚调用e6还是同一个系统吗？

### ChatGPT

这个新增要件很关键，必须先确认 **环境拓扑**。

现在有两种可能：

```text
模式A：工具环境独立，但调用同一个 E6
检查工具环境 → E6测试/业务共用环境
业务系统环境 → 同一个 E6测试/业务共用环境
```

风险：测试工具产生的数据、更新、交易可能影响业务系统验证数据。

```text
模式B：工具环境独立，也调用独立 E6
检查工具环境 → E6专用Sandbox/Test Tenant
业务系统环境 → 业务用E6环境
```

这是最安全、最推荐的。

---

你现在必须追加确认这些 QA：

```text
1. 检查工具专用环境是否必须和业务开发环境完全同构？
   OS / JDK / Tomcat / 网络 / 证书 / Proxy / DNS / FW 是否一致？

2. 检查工具是否部署在独立服务器？
   还是和业务系统共用 Linux / Tomcat？

3. 检查工具是否需要 Tomcat？
   还是 java -jar batch 即可？

4. 检查工具调用的 E6 endpoint 是哪个？
   和业务开发系统相同，还是专用 endpoint？

5. E6 tenant / program / API key 是否独立？
   还是和业务系统共用？

6. 测试数据是否和业务开发数据混在一起？
   如果共用，必须定义 prefix 和 cleanup 规则。

7. 写入类 API 是否允许在这个环境执行？
   create / update / payment / fund / cancel 等是否可执行？

8. 谁提供 E6 连接信息？
   endpoint、证书、认证信息、clientId、secret、API key。

9. 网络连通由谁开通？
   防火墙、proxy、allowlist、IP制限、DNS。

10. 检查工具的执行结果谁确认？
   工具Team、业务Team、运维、E6？
```

---

我建议你的原则是：

```text
检查工具环境 = 业务开发环境同构
但 E6连接资源最好独立
```

也就是：

```text
OS/JDK/Tomcat/网络结构：尽量同业务开发环境一致

E6侧资源：
最好使用检查工具专用 tenant / program / credential / test data
```

最危险的是：

```text
工具环境独立
但 E6 tenant / account / test data 和业务系统共用
```

因为你会遇到：

```text
业务系统测试中创建的数据被工具改了
工具创建的数据影响业务系统查询
余额、状态、交易历史互相污染
Diff结果不可信
```

---

所以现在你要先把问题压成一句话：

```text
检查工具环境虽然要和业务开发环境同构，但它调用的 E6 endpoint / tenant / credential / test data 是否可以独立？
```

这个答案决定后面所有安全设计。

## 第 27 轮

### 你

作为日本it开发流程 需要做成的成果物一览表可以帮我整理下 告诉我为什么

### ChatGPT

可以，而且我建议**不要按照一般的软件开发成果物整理**，而是按照**日本 SI（要件定义→基本设计→详细设计→开发→测试→发布）**的方式整理。

你的项目本质上是：

> **E6 API Verification Tool（API验证工具）**

它虽然是一个工具，但在日本开发流程里，它仍然要经过和业务系统一样的审查（Review）、设计（Design）、测试（Test）和运维（Operation）。

我建议成果物分成 **9 大类**。

---

# Phase 0 项目定义（为什么做）

这是 PM、架构师最先准备的。

| 成果物 | 为什么需要 | 谁看 |
|---------|-----------|------|
| 项目概要书 | 说明开发目的、范围、背景 | PM、管理者 |
| 系统背景说明 | 为什么需要这个工具，它和业务系统/E6的关系 | 所有人 |
| 用语定义（Glossary） | E6、UseCase、Baseline、Contract 等统一术语 | 全体 |

**为什么？**

日本项目最怕大家理解不一致。

例如：

```text
UseCase

业务Team理解：
开户流程

工具Team理解：
API调用链
```

必须统一。

---

# Phase 1 要件定义（Requirements）

这是最重要的。

## ① 要件定义书（Requirements Specification）

里面包括：

```text
开发目标

范围

非范围

功能

非功能

限制条件
```

为什么？

以后所有 Review 都依据这个。

---

## ② UseCase定义书

不是业务系统的。

而是：

```text
API Capability UseCase
```

例如：

```text
UC001 Customer

UC002 Account

UC003 Balance

UC004 Transaction
```

为什么？

这是整个工具最核心的输入。

---

## ③ QA确认书

就是我们刚讨论那些。

例如：

```text
业务Team确认事项

E6确认事项

工具决定事项
```

为什么？

避免后面一直返工。

---

# Phase 2 基本设计（Basic Design）

这里开始画图。

---

## 系统构成图

例如：

```text
Tool
 ↓
API Client
 ↓
E6
```

为什么？

所有人知道系统边界。

---

## 环境构成图

例如：

```text
DEV

STG

PROD
```

以及：

```text
Linux

JDK

Tomcat
```

为什么？

运维要看。

---

## 网络构成图

例如：

```text
Tool

↓

Firewall

↓

Proxy

↓

E6
```

为什么？

网络 Team 要确认。

---

## 模块设计书

例如：

```text
Runner

ApiExecutor

DiffEngine

Report

Baseline
```

为什么？

开发分工。

---

## 数据流设计

例如：

```text
UseCase Spec

↓

RunContext

↓

API

↓

Snapshot

↓

Diff

↓

Report
```

为什么？

整个工具最重要。

---

# Phase 3 详细设计（Detail Design）

这是 Codex 最需要的。

---

## RunContext设计

为什么？

整个 Batch 都依赖。

---

## UseCase Spec设计

为什么？

定义 JSON/Markdown 格式。

---

## Contract设计

为什么？

以后 Diff 都根据它。

---

## Diff Rule设计

例如：

```text
新增字段

删除字段

类型变化

长度变化
```

为什么？

避免开发各自理解。

---

## Report设计

例如：

```text
result.md

diff.md

excel
```

为什么？

统一格式。

---

## Log设计

例如：

```text
INFO

WARN

ERROR

MASK
```

为什么？

运维排查。

---

## Exception设计

例如：

```text
Retry

Stop

Continue
```

为什么？

错误处理统一。

---

# Phase 4 Interface设计

这个项目特别重要。

---

## E6 API Mapping

例如：

```text
API

↓

UseCase

↓

Step
```

为什么？

以后升级最好维护。

---

## Context变量设计

例如：

```text
${CUSTOMER_ID}
```

为什么？

保证 API 串联。

---

## Extract Rule

例如：

```text
$.customerId
```

为什么？

后续 API 用。

---

# Phase 5 Test设计

不要只写 TestCase。

要写 Test Strategy。

---

## Test Strategy

例如：

```text
单API

UseCase

Regression

Performance
```

为什么？

保证覆盖率。

---

## UseCase TestCase

例如：

```text
正常

异常

Boundary
```

为什么？

真正执行。

---

## Baseline管理

例如：

```text
Approve

Rollback

History
```

为什么？

Diff 有依据。

---

# Phase 6 运维设计

很多工具没有。

但是日本项目一定会问。

---

## Operation Manual

例如：

```text
如何执行

如何升级

如何恢复
```

---

## Release Procedure

例如：

```text
发布步骤

Rollback
```

---

## Monitoring

例如：

```text
CPU

Memory

Log

Run Status
```

---

# Phase 7 开发规范

例如：

```text
Package

Naming

Review

Commit

Branch
```

为什么？

Codex 和人工统一。

---

# Phase 8 用户文档

例如：

```text
如何写 UseCase

如何看 Diff

如何更新 Baseline
```

为什么？

业务 Team 会用。

---

# 我建议最终成果物一览

```text
01_Project_Overview.md

02_Glossary.md

03_Requirement_Spec.md

04_QA_Confirmation.md

05_System_Architecture.md

06_Environment_Architecture.md

07_Network_Architecture.md

08_Module_Design.md

09_DataFlow_Design.md

10_UseCase_Spec.md

11_Context_Design.md

12_API_Mapping.md

13_Contract_Design.md

14_Diff_Rule_Design.md

15_Report_Design.md

16_Log_Design.md

17_Exception_Design.md

18_Test_Strategy.md

19_TestCase_Design.md

20_Baseline_Design.md

21_Operation_Manual.md

22_Release_Procedure.md

23_Coding_Convention.md

24_User_Guide.md
```

---

## 我认为还应该增加两份（这是很多项目会遗漏，但你的项目非常需要）

### 25. Verification Policy（验证策略）

回答：

```text
为什么这样验证？
哪些变化必须拦截？
哪些变化允许通过？
Severity 如何定义？
```

这是整个工具的"业务规则"。

---

### 26. Capability Catalog（能力目录）

这是你的工具最核心的资产。

例如：

```text
Customer

Account

Balance

Payment

Settlement

Transaction
```

每个 Capability：

```text
涉及哪些 API

最小 UseCase

输入

输出

验证点

依赖关系
```

以后：

```text
业务系统Flow

↓

Capability Catalog

↓

Tool UseCase
```

全部自动对应。

---

## 我的建议（按日本SI项目经验）

如果按重要程度排序，我会先完成：

1. **Requirement Specification（要件定义）**
2. **QA Confirmation（确认事项）**
3. **Capability Catalog（能力目录）**
4. **UseCase Specification（API最小验证链）**
5. **Verification Policy（验证策略）**
6. **System Architecture（系统架构）**
7. **Data Flow Design（数据流设计）**
8. **Contract & Diff Design（契约和差异规则）**

这 8 份文档其实就构成了这个项目的"设计骨架"。有了它们，后面的详细设计、编码、测试和运维都会非常顺畅，而且也符合日本企业常见的开发流程和评审方式。

## 第 28 轮

### 你

现在有各个api调用可以参考的设计书  有的就是一个usecase的api调用 当然不只是调E6 api ，还有本身系统逻辑处理调用本身系统设计的api以及db更新 有调用flow图 有各个逻辑处理的设计书 我们现在预定的设计里面包含了吗

### ChatGPT

包含了一部分，但**还不够明确**。

你现在手头这些资料应该作为 **输入参考资料**，但不能原样变成检查工具设计。需要增加一层：

```text
现行业务资料
  ↓ 抽取
E6 Capability / API依赖分析
  ↓ 再设计
检查工具 UseCase
```

你预定的成果物里已经包含：

```text
Capability Catalog
UseCase Spec
API Mapping
DataFlow Design
Verification Policy
```

但建议再追加 3 份成果物。

---

# 需要追加的成果物

## 1. 现行资料分析表

目的：把现有设计书里和 E6 相关的部分抽出来。

```text
资料名
业务flow名
涉及API
是否E6 API
是否本系统API
是否DB更新
是否检查工具需要
备注
```

为什么需要？

因为现行业务 flow 里混有：

```text
E6 API调用
本系统API调用
DB更新
画面处理
内部业务逻辑
```

而检查工具只需要抽取 E6 API 最小验证链。

---

## 2. 业务Flow → 检查UseCase转换表

目的：说明哪些保留，哪些省略。

例：

| 现行业务处理 | 检查工具是否需要 | 理由 |
|---|---|---|
| 画面输入 | 不需要 | 只验证 E6 API |
| 本系统DB更新 | 不需要 | 不验证业务系统实现 |
| E6 Create Customer | 需要 | E6能力验证 |
| E6 Create Account | 需要 | 后续API依赖 |
| 邮件通知 | 不需要 | 非E6范围 |

为什么需要？

否则 Review 时别人会问：

```text
为什么业务flow里有这个处理，但检查工具没有？
```

这张表就是回答依据。

---

## 3. E6 API Dependency Map

目的：明确后续 API 参数来自哪里。

例如：

```text
Step1 CreateCustomer
  response.customerId
    ↓
Step2 CreateAccount.request.customerId
    ↓
Step3 GetAccount.request.accountId
```

为什么需要？

因为你前面要求：

```text
第一个API由用户指定
后续API必须根据前序API返回值调用
```

这个设计必须靠依赖关系图保证。

---

# 所以最终应调整为

你之前的设计包含了核心，但现在要补成：

```text
01 Project Overview
02 Glossary
03 Requirement Spec
04 QA Confirmation
05 Existing Document Analysis
06 Business Flow to Verification UseCase Mapping
07 Capability Catalog
08 E6 API Dependency Map
09 UseCase Spec
10 Verification Policy
11 API Mapping
12 Contract Design
13 Diff Rule Design
14 Report Design
15 System Architecture
16 Data Flow Design
17 Module Design
18 Test Strategy
19 Operation Manual
```

---

# 结论

**现在预定设计里包含方向，但没有充分覆盖“从现行业务设计书抽取检查工具UseCase”的过程。**

必须追加：

```text
现行资料分析表
业务Flow到检查UseCase转换表
E6 API依赖关系图
```

这三份非常关键。否则你无法说明：

```text
为什么检查工具只调用这些API
为什么省略本系统API和DB更新
为什么后续API参数来自前序API
```

这三份文档会成为你后面设计和评审的核心依据。

## 第 29 轮

### 你

设计书能用日语吗

### ChatGPT

**可以，而且我建议全部用日语。**

如果这个项目是日本企业开发（从你的描述来看就是日本 SI 开发流程），那么**设计书、成果物、Review资料最好全部使用日语**。

不过，我建议不要完全照搬传统日本设计书，而是采用**日本设计书格式 + AI/Agent时代的内容组织方式**。

例如：

---

## 第一层：项目管理文档（管理者阅读）

```text
01_プロジェクト概要書.md
02_用語集.md
03_要件定義書.md
04_確認事項一覧(QA).md
```

---

## 第二层：分析文档（架构师阅读）

这里就是你刚刚提到的。

```text
10_現行業務分析書.md

11_E6 API分析書.md

12_現行業務Flow分析書.md

13_検証対象一覧.md
```

这里有一个我建议新增的成果物：

```text
現行業務 → 検証UseCase対応表.md
```

这个会变成整个项目最重要的文档之一。

例如：

| 現行業務 | E6 API | 検証対象 | 理由 |
|----------|---------|---------|------|
| 顧客登録 | CreateCustomer | ○ | Capability確認 |
| DB更新 | × | × | Tool対象外 |
| メール送信 | × | × | Tool対象外 |

这个日本Review的人特别容易理解。

---

## 第三层：设计文档

```text
20_システム構成設計書.md

21_環境設計書.md

22_ネットワーク設計書.md

23_モジュール設計書.md

24_データフロー設計書.md
```

---

## 第四层：工具设计（这个是你们自己的）

这是业务系统没有的。

```text
30_検証ポリシー設計書.md

31_検証UseCase設計書.md

32_API依存関係設計書.md

33_Contract設計書.md

34_Diff判定設計書.md

35_Report設計書.md

36_Baseline管理設計書.md
```

---

## 第五层：开发设计

```text
40_RunContext設計書.md

41_JsonSpec設計書.md

42_Context変数設計書.md

43_API実行設計書.md

44_Result保存設計書.md

45_ログ設計書.md

46_Exception設計書.md
```

---

## 第六层：测试

```text
50_テスト方針書.md

51_テストケース設計書.md

52_異常系一覧.md

53_回帰テスト設計書.md
```

---

## 第七层：运维

```text
60_運用手順書.md

61_リリース手順書.md

62_障害対応手順書.md
```

---

# 我建议新增一份（非常重要）

这是一般日本项目没有，但是你的项目一定需要。

```text
E6 Capability カタログ.md
```

里面不是 API，而是：

```text
Customer

Account

Balance

Transaction

Settlement
```

每一个 Capability：

```text
目的

対象API

入力

出力

依存API

最小UseCase

確認ポイント
```

以后：

```text
业务Flow

↓

Capability

↓

Tool UseCase
```

全部由这份文档连接。

---

# 再增加一份（我认为整个项目最重要）

```text
検証設計方針書.md
```

里面回答：

```text
为什么不用业务Flow

为什么不复制业务逻辑

为什么只调用E6

为什么第一个API由用户指定

为什么后续API自动关联

为什么这样设计Baseline

为什么这样设计Diff
```

以后任何人问：

> 为什么这样设计？

直接看这份文档。

---

# 最后一个建议（日本项目很有用）

所有文档统一编号。

例如：

```text
PJ01_プロジェクト概要書.md

RQ01_要件定義書.md

AN01_現行業務分析書.md

AR01_システム構成設計書.md

AR02_環境設計書.md

UC01_検証UseCase設計書.md

UC02_API依存関係設計書.md

TS01_テスト方針書.md

OP01_運用手順書.md
```

这样在日本的 Review、Redmine、Jira、Backlog 或成果物管理中，引用会非常方便。

---

**我的建议是：**

**文档语言全部使用日语，文档结构遵循日本 SI 的成果物体系；但内容采用 AI/Agent 时代的设计思想。**

这样既符合日本企业的开发习惯，又不会受传统设计书的限制，后续无论是 Review、交付还是交给 Codex/Agent 使用，都非常自然。

## 第 30 轮

### 你

如果只需要必须的 你给个一览

### ChatGPT

如果站在**日本企业实际开发**（不是为了文档而文档），并且结合你的项目特点：

> **E6 API Verification Tool（验证工具）**

我会把成果物压缩到 **10 份必须有的文档**。

这 10 份已经足够完成要件定义、设计、开发、测试、Review。

| No | 文档（日文） | 为什么必须 |
|----|-------------|-----------|
| 01 | **要件定義書** | 定义项目目的、范围、功能、非功能，是所有工作的依据。 |
| 02 | **確認事項一覧（QA一覧）** | 记录需要与业务 Team、E6 Team 确认的问题及结论，避免口头沟通丢失。 |
| 03 | **現行業務分析書** | 分析现有业务 Flow、API 调用、DB 更新、内部逻辑，明确哪些属于工具范围，哪些不属于。 |
| 04 | **検証UseCase設計書** | 工具真正要执行的最小 API 调用链（不是业务 Flow），这是整个工具的核心。 |
| 05 | **API依存関係設計書** | 定义 API 间参数如何传递、哪些值从前序 API 提取、Context 如何流转。 |
| 06 | **システム設計書** | 工具整体架构（Batch、RunContext、Report、Diff、Baseline、E6 Client 等模块）。 |
| 07 | **検証ルール設計書** | 定义如何判断 API 有变化（字段、类型、长度、枚举、业务结果、Severity 等）。 |
| 08 | **テスト設計書** | 定义正常、异常、边界测试策略，以及每个 UseCase 的验证方式。 |
| 09 | **運用手順書** | 如何执行 Batch、如何生成 Baseline、如何查看报告、如何处理失败。 |
| 10 | **リリース・環境構成書** | 环境、JDK、Tomcat、Linux、E6 Endpoint、部署方式、配置说明。 |

---

## 如果只能保留 5 份（真正最小集合）

我会选：

1. **要件定義書**
2. **確認事項一覧（QA一覧）**
3. **検証UseCase設計書**
4. **API依存関係設計書**
5. **検証ルール設計書**

原因很简单：

- **要件定义**：明确做什么、不做什么。
- **QA 一览**：把所有需要确认的事项沉淀下来，避免返工。
- **UseCase**：决定工具到底执行哪些 API 链路。
- **API 依赖关系**：保证只有第一个 API 由用户输入，后续全部自动关联。
- **验证规则**：定义什么算变更、什么算通过，这是工具的核心价值。

---

### 我对你的项目还有一个建议

我会把 **「検証UseCase設計書」** 做成整个项目的中心文档。

因为以后：

```text
现行业务设计书
        ↓
   抽取 E6 API
        ↓
検証UseCase設計書
        ↓
JSON Spec
        ↓
Java Batch
        ↓
Result / Diff
```

整个工具都是围绕它展开的。

所以在这 10 份文档里，**「検証UseCase設計書」** 会是最重要、更新最频繁，也是开发、测试和运维共同依赖的核心成果物。

## 第 31 轮

### 你

大概有24个api  组合出来10种以内的case

### ChatGPT

这个数量其实非常理想。

> **24 个 API，最终组合成 10 个以内的 UseCase**，这是一个非常合理的规模。

**不要设计成 24 个 UseCase。**

应该按照 **Capability（能力）** 来设计，而不是 API 数量。

例如：

| UseCase | 包含 API 数 | 验证目标 |
|---------|------------:|----------|
| UC01 Customer | 2~4 | Customer 生命周期 |
| UC02 Account | 2~5 | Account 生命周期 |
| UC03 Balance | 2~3 | Balance 查询与变化 |
| UC04 Transaction | 3~5 | Transaction 生命周期 |
| UC05 Payment | 2~4 | Payment 成功流程 |
| UC06 Cancel | 2~3 | Cancel 流程 |
| UC07 Inquiry | 2~4 | 查询类 API |
| UC08 Error | 多个 | 异常场景验证 |
| UC09 Master | 1~3 | Master 数据查询 |
| UC10 End-to-End | 多个 | 最小业务链验证 |

这样大约覆盖：

```text
24 API
    ↓
Capability分类
    ↓
8~10个UseCase
```

---

## 为什么不要按 API 数设计？

假设：

```text
API01 CreateCustomer
API02 GetCustomer
API03 UpdateCustomer
API04 DeleteCustomer
```

如果做成：

```text
UC01 CreateCustomer
UC02 GetCustomer
UC03 UpdateCustomer
UC04 DeleteCustomer
```

以后升级一次：

```text
要跑24个UseCase
```

没有意义。

应该：

```text
UC01 Customer Lifecycle

Step1 CreateCustomer
↓

Step2 GetCustomer
↓

Step3 UpdateCustomer
↓

Step4 GetCustomer
```

这样：

- 能验证 API Contract
- 能验证 API Behavior
- 能验证 API Dependency
- 能验证 Capability

---

## 建议增加一份文档（其实只要一页）

### API → UseCase Mapping

例如：

| API | UC01 | UC02 | UC03 | UC04 |
|------|:----:|:----:|:----:|:----:|
| CreateCustomer | ● | | | |
| GetCustomer | ● | | | |
| CreateAccount | | ● | | |
| GetAccount | | ● | | |
| Balance | | ● | ● | |
| Payment | | | ● | |
| Cancel | | | | ● |

这样你一眼就知道：

- 每个 API 被哪些 UseCase 覆盖。
- 是否有 API 没被验证。
- 是否有重复覆盖。

---

## 我建议你的设计目标

不要追求：

```text
24 API
=
24 TestCase
```

而应该追求：

```text
24 API
↓
Capability分析
↓
8~10 UseCase
↓
覆盖全部24 API
```

这样：

- **维护成本最低**
- **业务意义最清晰**
- **升级回归最快**
- **最符合你们这个验证工具的定位**

这也是我认为最适合你这个 E6 API Verification Tool 的设计方式。

## 第 32 轮

### 你

要件内容就是确认e6 api是都有变化 用各种usecase每天来执行 然后和前一天的比较 并且数据可能都是一样的 比如某些字段随着日期改变会变的可以忽略。 运行环境 程序等都要设计。我要做wbs 所以每个成果物 任务都要明确下来。

### ChatGPT

我觉得现在已经可以把项目重新定义了。

这个项目**不是 API 测试工具**，而是：

> **E6 API Daily Regression Verification Platform（E6 API日次回归验证平台）**

这样一来，WBS 就很好拆了。

---

# 项目目标（Project Goal）

```text
每天自动执行约10个 Verification UseCase

↓

调用约24个 E6 API

↓

生成当天 Snapshot

↓

与昨天（Approved Baseline）比较

↓

输出 Diff Report

↓

发现 E6 API 的 Contract / Behavior 是否发生变化
```

注意：

> **业务结果不是主要目标。**

真正目标：

```text
API有没有变化
```

---

# 我建议WBS按照成果物（Deliverable）来拆，而不是按照开发阶段拆。

例如：

```
1. 要件定义
2. UseCase设计
3. Verification Rule设计
4. 系统设计
5. 共通Framework
6. API执行器
7. Diff Engine
8. Report
9. Operation
10. Test
```

---

# WBS（建议）

## 1. 要件定义

成果物：

```
要件定義書
```

任务：

```
目的整理

范围

非范围

功能

非功能

限制条件

成功标准
```

---

## 2. QA确认

成果物：

```
QA一覧
```

任务：

```
业务确认

E6确认

Infra确认

Environment确认

Security确认
```

---

## 3. Verification UseCase设计

成果物：

```
検証UseCase設計書
```

任务：

```
整理24 API

Capability分类

设计10个UseCase

入口参数

API顺序

Extract

Context

Business Check
```

---

## 4. Verification Rule设计

成果物：

```
検証ルール設計書
```

任务：

```
Schema Diff

Behavior Diff

Ignore Rule

Severity

Baseline Rule

Snapshot Rule
```

例如：

```
createdAt
lastUpdate

↓

Ignore
```

因为每天都会变。

---

## 5. 系统设计

成果物：

```
システム設計書
```

任务：

```
Architecture

Package

RunContext

Directory

RunId

Lock

Baseline

Scheduler
```

---

## 6. Environment设计

成果物：

```
環境設計書
```

任务：

```
Linux

JDK

Tomcat

Batch

Cron

Network

Proxy

Config
```

这一块刚才你说了。

必须设计。

---

## 7. Common Framework

成果物：

```
共通Framework設計書
```

任务：

```
Json

File

Context

Logger

Mask

Config

Resource

Http

Retry

Timeout
```

---

## 8. API Execution设计

成果物：

```
API実行設計書
```

任务：

```
ApiClient

Extract

Context

Variable

Flow

Retry

Error
```

---

## 9. Snapshot设计

成果物：

```
Snapshot設計書
```

任务：

```
Request Snapshot

Response Snapshot

Contract Snapshot

Metadata

Hash
```

---

## 10. Diff Engine设计

成果物：

```
Diff設計書
```

任务：

```
Contract

Behavior

Ignore

Baseline

History
```

---

## 11. Report设计

成果物：

```
Report設計書
```

任务：

```
Markdown

Excel

Json

Summary

Detail
```

---

## 12. Operation设计

成果物：

```
運用設計書
```

任务：

```
Daily

Cron

Run

Approve

Rollback

Retention

Cleanup
```

---

## 13. Logging设计

成果物：

```
ログ設計書
```

任务：

```
Info

Warn

Error

Mask

Trace
```

---

## 14. Test设计

成果物：

```
テスト設計書
```

任务：

```
Unit

Integration

Regression

UseCase

Exception

Performance
```

---

# 这里还有两个成果物我建议一定加

这是你这个项目最大的特点。

---

## Snapshot Definition

成果物：

```
Snapshot設計書
```

内容：

```
保存哪些字段

哪些字段Ignore

哪些字段Hash

哪些字段Mask
```

例如：

```
createdAt

↓

Ignore

lastUpdate

↓

Ignore

traceId

↓

Ignore

customerId

↓

Compare

status

↓

Compare
```

这个文档以后会非常重要。

---

## Ignore Rule Definition

成果物：

```
IgnoreRule設計書
```

例如：

```
日期

UUID

TraceId

Timestamp

ServerTime

ResponseTime
```

为什么？

因为：

每天跑

一定会变。

必须提前定义：

```
哪些变化

属于正常变化
```

---

# 我建议整个项目真正的核心成果物其实只有4份

如果让我排优先级。

一定是：

```
① 要件定義書

② 検証UseCase設計書

③ 検証ルール設計書

④ IgnoreRule設計書
```

为什么？

因为：

**这个项目真正开发的不是 API Client。**

真正开发的是：

```
今天

↓

Snapshot

↓

昨天

↓

Diff

↓

Ignore Rule

↓

最终告诉用户：

E6有没有真正变化
```

---

## 我认为还应该再加一个成果物（这是整个项目的灵魂）

**「Snapshot & Comparison Policy（スナップショット比較方針書）」**

里面回答：

- Snapshot 保存哪些内容？
- 比较哪些字段？
- 哪些字段忽略？
- 哪些字段按规则转换后再比较（例如日期格式、大小写、空白）？
- 如何判定 HIGH / MEDIUM / LOW？

**因为对于你的项目来说，真正的核心不是“调用 API”，而是“定义什么叫变化，什么叫没有变化”。**

如果这份文档设计得好，后面的 Java 实现会非常清晰，WBS 也会围绕它展开。

## 第 33 轮

### 你

你用日本it开发文档来帮我做出wbs

### ChatGPT

可以，而且我建议**完全按照日本 SI（要件定義→基本設計→詳細設計）的 WBS 思路**来做，而不是按照程序模块来拆。

对于你的项目，我认为应该按照**成果物（Deliverable）驱动**来拆 WBS。这样每个任务都有对应的 Review 和交付物，也符合日本 IT 项目管理方式。

---

# WBS Level 1

| WBS | 成果物（日文） | Review |
|------|----------------|---------|
| 1 | プロジェクト準備 | ○ |
| 2 | 要件定義 | ○ |
| 3 | 現行調査・分析 | ○ |
| 4 | 基本設計 | ○ |
| 5 | 詳細設計 | ○ |
| 6 | 開発 | ○ |
| 7 | テスト | ○ |
| 8 | リリース・運用 | ○ |

---

# 1. プロジェクト準備

成果物

```text
プロジェクト概要書
```

任务

```text
1.1 プロジェクト目的整理

1.2 スコープ整理

1.3 成果物一覧作成

1.4 スケジュール作成
```

---

# 2. 要件定義

成果物

```text
要件定義書
```

任务

```text
2.1 背景整理

2.2 開発目的整理

2.3 機能要件

2.4 非機能要件

2.5 制約事項

2.6 前提条件

2.7 対象範囲

2.8 対象外
```

---

成果物

```text
確認事項一覧
```

任务

```text
2.9 業務確認事項

2.10 E6確認事項

2.11 インフラ確認事項

2.12 運用確認事項
```

---

# 3. 現行調査・分析

这是你现在马上要做的。

成果物

```text
現行調査結果
```

任务

```text
3.1 API一覧整理

3.2 Flow一覧整理

3.3 業務設計書調査

3.4 E6利用箇所整理

3.5 API依存関係整理
```

---

成果物

```text
Capability一覧
```

任务

```text
3.6 API分類

3.7 Capability整理

3.8 UseCase候補作成
```

---

成果物

```text
検証対象一覧
```

任务

```text
3.9 対象API決定

3.10 非対象整理
```

---

# 4. 基本設計

这是整个项目最重要。

---

成果物

```text
システム構成設計書
```

任务

```text
4.1 システム構成

4.2 モジュール構成

4.3 ディレクトリ構成

4.4 パッケージ構成
```

---

成果物

```text
検証UseCase設計書
```

任务

```text
4.5 UseCase一覧

4.6 API呼出順序

4.7 Entry Parameter

4.8 Context設計

4.9 Extract設計
```

---

成果物

```text
API依存設計書
```

任务

```text
4.10 API依存図

4.11 Context変数

4.12 JsonPath設計
```

---

成果物

```text
検証ルール設計書
```

任务

```text
4.13 Contract比較

4.14 Behavior比較

4.15 IgnoreRule

4.16 Severity

4.17 Baseline
```

---

成果物

```text
環境設計書
```

任务

```text
4.18 Linux

4.19 JDK

4.20 Tomcat

4.21 Config

4.22 Scheduler

4.23 Log
```

---

# 5. 詳細設計

成果物

```text
内部設計書
```

任务

```text
5.1 RunContext

5.2 ApiExecutor

5.3 Snapshot

5.4 Diff

5.5 Report

5.6 Baseline

5.7 Retry

5.8 Timeout
```

---

成果物

```text
JSON設計書
```

任务

```text
5.9 UseCase Json

5.10 Snapshot Json

5.11 Result Json

5.12 Config Json
```

---

成果物

```text
ログ設計書
```

任务

```text
5.13 Log Format

5.14 Mask

5.15 TraceId

5.16 RunId
```

---

# 6. 開発

任务

```text
6.1 Common

6.2 ApiClient

6.3 UseCaseRunner

6.4 Snapshot

6.5 Diff

6.6 Report

6.7 Config

6.8 CLI

6.9 Batch
```

---

# 7. テスト

成果物

```text
テスト仕様書
```

任务

```text
7.1 Unit Test

7.2 Integration Test

7.3 UseCase Test

7.4 Daily Test

7.5 Exception Test
```

---

成果物

```text
テスト結果報告書
```

任务

```text
7.6 Test Evidence

7.7 Defect

7.8 Fix確認
```

---

# 8. リリース・運用

成果物

```text
運用手順書
```

任务

```text
8.1 Install

8.2 Config

8.3 Run

8.4 Rollback

8.5 Cleanup

8.6 Backup
```

---

成果物

```text
運用引継書
```

任务

```text
8.7 Daily運用

8.8 障害対応

8.9 Baseline更新

8.10 Report確認
```

---

# 我认为还应该增加一个日本项目很少写，但你的项目必须写的成果物

```
比較ルール一覧
```

例如：

| 項目 | Rule |
|------|------|
| createdAt | Ignore |
| updatedAt | Ignore |
| TraceId | Ignore |
| UUID | Ignore |
| status | Compare |
| amount | Compare |
| customerId | Compare |

这份文档以后：

```text
Diff Engine

↓

直接读取
```

而不是：

```text
Java代码写死
```

---

# 最后我建议把 WBS 编号规范化

```
1. プロジェクト準備

2. 要件定義

3. 現行調査

4. 基本設計

5. 詳細設計

6. 実装

7. 単体試験

8. 結合試験

9. 総合試験

10. リリース
```

**这是日本 SI 项目最常见的一级 WBS。**

---

## 不过，结合你这个项目，我会在传统日本 WBS 基础上再增加两个一级成果物（这是这个项目特有的）：

**11. 検証ポリシー設計**（定义什么算变化、什么算忽略）

**12. UseCase資産整備**（把现行业务 Flow 抽象成工具自己的 Verification UseCase）

我认为这两项才是这个项目真正的核心资产，也是后续每天自动验证能长期维护的关键。

## 第 34 轮

### 你

不要工程阶段 我需要每个成果物来排

### ChatGPT

这个项目我反而**不建议按工程阶段（要件→基本→详细）排**。

因为你的项目以后会不断增加 UseCase、API、Diff Rule。

**最好的方式是按成果物（Deliverable）管理。**

这也是很多日本大型项目（特别是平台类、Framework类）的做法。

---

# 推荐成果物WBS（按Deliverable）

| No | 成果物(日文) | 目的 | 优先级 |
|-----|-------------|------|--------|
| 01 | **要件定義書** | 定义为什么做、做到什么程度 | ★★★★★ |
| 02 | **確認事項一覧（QA一覧）** | 与业务、E6、Infra确认事项及结论 | ★★★★★ |
| 03 | **現行業務分析書** | 分析现有业务Flow和设计书 | ★★★★★ |
| 04 | **E6 API分析書** | 整理24个API能力、限制、版本 | ★★★★★ |
| 05 | **検証対象一覧** | 明确哪些API需要验证，哪些不验证 | ★★★★★ |
| 06 | **Capability一覧** | 将24个API按能力分组 | ★★★★★ |
| 07 | **検証UseCase設計書** | 设计约10个最小API调用链 | ★★★★★ |
| 08 | **API依存関係設計書** | 定义API之间参数传递和Context | ★★★★★ |
| 09 | **検証ルール設計書** | 定义字段、类型、长度、业务行为比较规则 | ★★★★★ |
| 10 | **IgnoreRule設計書** | 定义哪些字段每天变化应忽略 | ★★★★★ |
| 11 | **Snapshot設計書** | 定义每天保存哪些Request/Response快照 | ★★★★★ |
| 12 | **Baseline管理設計書** | 定义Baseline生成、批准、回退策略 | ★★★★★ |
| 13 | **Diff判定設計書** | 定义如何比较昨天与今天 | ★★★★★ |
| 14 | **システム構成設計書** | 工具整体架构 | ★★★★☆ |
| 15 | **環境設計書** | Linux、JDK、Tomcat、配置、网络 | ★★★★☆ |
| 16 | **設定管理設計書** | Endpoint、认证、环境切换、配置项 | ★★★★☆ |
| 17 | **共通ライブラリ設計書** | JSON、文件、日志、Context、HTTP等共通模块 | ★★★★☆ |
| 18 | **API実行設計書** | API执行、变量替换、Extract、Retry | ★★★★☆ |
| 19 | **Context設計書** | Entry、Runtime、Variable生命周期 | ★★★★☆ |
| 20 | **Report設計書** | Markdown、JSON、Excel报告格式 | ★★★★☆ |
| 21 | **ログ設計書** | 日志、Mask、RunId、Trace | ★★★★☆ |
| 22 | **例外処理設計書** | Timeout、Retry、Stop、Continue策略 | ★★★★☆ |
| 23 | **テスト設計書** | Unit、UseCase、Regression、异常验证 | ★★★★☆ |
| 24 | **運用設計書** | 日常执行、Cron、Cleanup、Baseline更新 | ★★★☆☆ |

---

## 如果只保留真正必须的（我建议 12 份）

按你这个项目的重要程度，我会留下：

1. **要件定義書**
2. **確認事項一覧（QA一覧）**
3. **現行業務分析書**
4. **E6 API分析書**
5. **検証対象一覧**
6. **検証UseCase設計書**
7. **API依存関係設計書**
8. **検証ルール設計書**
9. **IgnoreRule設計書**
10. **Snapshot設計書**
11. **システム構成設計書**
12. **環境設計書**

---

# 我建议再增加一个成果物（这是你的项目特有的）

我认为最重要的是：

### **「現行業務→検証UseCase対応表」**

例如：

| 現行Flow | 本系统处理 | E6 API | Tool UseCase |
|----------|-----------|--------|--------------|
| 开户 | DB更新 | CreateCustomer | UC01 |
| 开户 | 发送邮件 | × | 不实现 |
| 开户 | CreateAccount | CreateAccount | UC01 |

这份文档回答的是：

> **为什么检查工具没有照搬业务系统，而是只实现这一条最小 API 链？**

以后 Review 时，这会是最有说服力的一份成果物。

---

## 我认为这套 WBS 的核心思想只有一句话

**所有成果物都围绕一个中心展开：**

```text
现行业务设计书
        ↓
E6 API分析
        ↓
Capability分析
        ↓
Verification UseCase
        ↓
Snapshot
        ↓
Diff
        ↓
Report
```

所以**成果物之间是有依赖关系的**，而不是孤立的文档。

这也是我认为最符合日本 IT 项目（特别是平台类、验证工具类项目）的成果物组织方式。

## 第 35 轮

### 你

检证rule设计是做什么

### ChatGPT

这是整个项目里**最容易被忽略，但实际上最重要的成果物之一。**

如果让我给这个项目排重要程度，我会排：

```text
① 要件定義書
② 検証UseCase設計書
③ 検証ルール設計書
```

它的重要程度甚至高于系统设计。

---

## 什么是「検証ルール設計書」？

一句话：

> **定义工具"如何判断 API 有没有变化"。**

注意：

它**不是**定义 API。

它定义的是：

```text
今天

↓

API Response

↓

如何比较

↓

什么算OK

什么算NG

什么算Warning
```

---

## 举个例子

昨天：

```json
{
  "customerId":"123",
  "status":"ACTIVE",
  "updateDate":"2025-06-01"
}
```

今天：

```json
{
  "customerId":"123",
  "status":"ACTIVE",
  "updateDate":"2025-06-02"
}
```

如果没有 Rule：

程序会说：

```text
NG

updateDate变了
```

但是：

实际上：

```text
每天都会变

应该PASS
```

这就是：

```text
Ignore Rule
```

---

再举例：

昨天

```json
status:"ACTIVE"
```

今天

```json
status:1
```

Rule：

```text
类型变化

Severity = HIGH

NG
```

---

再举例：

昨天

```json
{
  "customerId":"",
  "status":""
}
```

今天

```json
{
  "customerId":"",
  "status":"",
  "message":"OK"
}
```

Rule：

```text
新增字段

允许

Warning
```

---

## 所以 Rule 是什么？

它不是程序。

它是：

```text
比较政策（Comparison Policy）
```

例如：

---

### Rule01

```text
Status Code

必须一致
```

---

### Rule02

```text
Request Method

必须一致
```

---

### Rule03

```text
Request Parameter 数

必须一致
```

---

### Rule04

```text
Request Parameter Type

必须一致
```

---

### Rule05

```text
新增Request字段

Warning
```

---

### Rule06

```text
删除Request字段

Error
```

---

### Rule07

```text
Response Type变化

Error
```

---

### Rule08

```text
Response新增字段

Warning
```

---

### Rule09

```text
Ignore字段

timestamp

requestTime

traceId
```

---

### Rule10

```text
Date

忽略
```

---

### Rule11

```text
UUID

忽略
```

---

### Rule12

```text
金额

必须一致
```

---

### Rule13

```text
Enum

必须一致
```

---

### Rule14

```text
Array顺序

是否比较
```

---

### Rule15

```text
Null

是否允许
```

---

## 为什么要写成设计书？

因为：

以后程序就不用写：

```java
if(name.equals("updateDate"))
```

而是：

程序读取：

```text
検証ルール設計書
```

然后：

```text
updateDate

↓

Ignore
```

---

## 所以这份设计书其实就是

以后程序里的：

```text
Rule Engine
```

例如：

```text
Rule001

Request

↓

Method

↓

Equals
```

---

## 我建议以后不要叫

```text
検証ルール設計書
```

我更建议叫：

```text
比較ルール設計書
```

或者：

```text
比較ポリシー設計書
```

因为：

真正做的是：

```text
Snapshot

↓

Compare

↓

Ignore

↓

Diff

↓

Severity
```

---

## 我认为里面至少应该有这些章节

```text
1.
比較対象

2.
Ignore対象

3.
Request比較Rule

4.
Response比較Rule

5.
Contract比較Rule

6.
Business比較Rule

7.
Severity Rule

8.
Baseline Rule

9.
Diff Rule

10.
Report Rule
```

---

## 为什么我认为它这么重要？

因为以后：

E6升级了。

程序不用改。

只需要：

修改：

```text
比較ルール
```

例如：

今天：

```text
新增字段

↓

Warning
```

以后：

客户要求：

```text
新增字段

↓

PASS
```

程序：

**一行代码不用改。**

所以：

> **这份文档不是开发文档，而是整个检查工具的"判定规则"。**

---

## 不过，结合你整个项目，我建议再调整一下命名

与其叫：

```text
検証ルール設計書
```

我建议拆成两份，更符合日本项目习惯：

1. **比較ポリシー設計書（Comparison Policy）**
   定义比较原则：哪些项目比较、哪些忽略、严重度如何划分。

2. **比較ルール一覧（Comparison Rule Catalog）**
   用表格列出每一条规则，例如：

| 対象 | JSONPath | Rule | Severity |
|------|----------|------|----------|
| Response | $.status | 必须一致 | HIGH |
| Response | $.updateDate | Ignore | - |
| Response | $.traceId | Ignore | - |
| Response | $.message | 新增允许 | LOW |

这样设计后，Java 的 Diff Engine 就可以直接读取规则配置，而不是把规则写死在代码里。这也是后续维护成本最低的方式。

## 第 36 轮

### 你

这些不应该是每个api设计书 和usecase里面写吗

### ChatGPT

**我认为你这个判断是对的，而且比我前面的建议更符合日本 SI 的设计方式。**

实际上，我刚才是站在"平台产品"角度在拆。

但是如果站在**日本业务开发（要件定义→基本设计→详细设计）**来看：

> **大部分 Rule 不应该独立成一本设计书。**

而应该**跟着 API 或 UseCase 走。**

---

# 为什么？

因为 Rule 是有作用域（Scope）的。

例如：

```text
API01

status

必须一致
```

这是：

**API01 的 Rule**

不是整个系统的 Rule。

---

例如：

```text
Payment

amount

必须一致
```

这是：

**Payment UseCase 的 Rule**

---

例如：

```text
createdDate

Ignore
```

如果：

Customer API

Ignore

但是：

History API

可能：

**不能 Ignore。**

所以：

不能放系统级 Rule。

---

# 我现在更推荐这样分

## 第一层

**API设计书**

里面写：

```text
API01

Request

Response

Contract

Validation Rule

Ignore

Severity
```

例如：

```text
CreateCustomer API

Request

customerName

string

50

Required

Validation

customerName

必须一致

Response

customerId

必须存在

createdDate

Ignore

traceId

Ignore
```

---

## 第二层

**UseCase设计书**

里面写：

```text
UseCase

API顺序

Context

Business Check

最终结果
```

例如：

```text
Customer

↓

Account

↓

Balance

↓

Payment
```

然后：

Business Check：

```text
余额

必须减少

Transaction

必须SUCCESS
```

---

## 第三层

系统设计

只写：

```text
Diff Engine

如何执行Rule

Report

如何输出
```

而不是：

写：

```text
status

必须一致
```

---

# 所以成果物应该这样调整

## API设计书负责

```text
Request

Response

Compare Rule

Ignore

Extract

Expected Status
```

---

## UseCase设计书负责

```text
Flow

Context

Entry

Dependency

Business Result

Exception
```

---

## 系统设计负责

```text
如何读取API设计

如何读取UseCase

如何执行

如何Compare

如何Report
```

---

# 那还有没有系统级 Rule？

**有，但是很少。**

真正系统级只有：

例如：

```text
RunId生成

Retry

Timeout

Log

Mask

Baseline

Snapshot

Diff Engine
```

这些属于：

```text
Framework Rule
```

而不是：

```text
Business Rule
```

---

# 所以我建议整个项目重新整理

实际上：

只有三类成果物。

---

## ① API设计书（24份）

例如：

```text
CreateCustomer

CreateAccount

...

共24份
```

里面：

```text
Contract

Rule

Extract

Compare
```

---

## ② UseCase设计书（约10份）

里面：

```text
API顺序

Context

Business Check

Exception
```

---

## ③ Framework设计书（约6份）

例如：

```text
Architecture

RunContext

Diff

Snapshot

Report

Operation
```

---

# 我现在反而建议取消

我前面说的：

```text
検証Rule設計書
```

改成：

```text
API設計書

UseCase設計書
```

因为：

Rule：

应该跟着：

```text
API
```

走。

Business Check：

应该跟着：

```text
UseCase
```

走。

---

## 我觉得你提出的这一点非常关键

因为它符合日本设计书一直遵循的一个原则：

> **"规则跟着对象走（Rule follows the object）"**

也就是说：

- **API 的规则写在 API 设计书里。**
- **UseCase 的业务验证写在 UseCase 设计书里。**
- **Framework 只负责"如何执行规则"，不负责定义业务规则。**

---

## 我唯一建议保留的"系统级规则"

只有一份：

**「比較エンジン設計書」**

它不定义：

```text
status必须一致
```

它定义的是：

```text
比较流程：

读取API设计

↓

读取Rule

↓

生成Snapshot

↓

Compare

↓

输出Diff
```

也就是说：

**系统负责执行规则，而规则本身属于 API 和 UseCase。**

**我认为这是更符合日本 SI 设计思想，也更适合你这个项目长期维护的方案。**

## 第 37 轮

### 你

给一个表 需要哪些成果物 为什么

### ChatGPT

结合我们前面的讨论，以及**日本 IT（SI）开发**的习惯，我认为你的项目真正需要的成果物不用很多，但每一份都有明确职责。

> **原则：Rule 跟着对象走。**
>
> - API 的规则写在 **API 设计书**
> - UseCase 的规则写在 **UseCase 设计书**
> - Framework 只负责如何执行，不负责定义业务规则

下面这份表是我认为最适合你这个项目的成果物一览。

| No. | 成果物（日文） | 主要内容 | 为什么需要 |
|------|---------------|----------|------------|
| 1 | **要件定義書** | 开发目的、范围、功能、非功能、限制、成功标准 | 定义项目边界，所有设计的依据。 |
| 2 | **確認事項一覧（QA一覧）** | 与业务 Team、E6 Team、Infra Team 确认的问题及结论 | 把假设变成已确认事项，避免后续返工。 |
| 3 | **現行業務分析書** | 分析现行业务 Flow、设计书、E6 API 使用方式 | 理解现行业务如何使用 E6，为抽取最小验证链做准备。 |
| 4 | **E6 API一覧・分析書** | 24 个 E6 API 的整理（接口、用途、依赖、限制） | 建立 E6 API 全貌，是设计 UseCase 的基础。 |
| 5 | **API設計書（24API）** | 每个 API 的 Request、Response、字段、Extract、比较规则、注意事项 | API 是最小设计单元，也是后续自动执行和比较的依据。 |
| 6 | **検証UseCase設計書（约10件）** | 最小 API 调用链、入口参数、Context、API 顺序、Business Check | 定义每天真正执行的验证流程，是工具的核心。 |
| 7 | **システム設計書** | 整体架构、模块、目录、RunContext、Batch 流程 | 描述工具整体结构和各模块职责。 |
| 8 | **環境設計書** | Linux、JDK、Tomcat、配置、网络、E6 Endpoint、认证 | 保证开发、测试、发布环境一致，便于部署和运维。 |
| 9 | **共通設計書（Framework設計書）** | JSON、HTTP、文件、日志、Context、Config、异常处理等共通组件 | 定义可复用基础框架，避免各模块实现不一致。 |
| 10 | **運用設計書** | Batch 执行方式、定时、Baseline 更新、日志、Cleanup、异常处理 | 定义工具上线后的日常运行方式。 |
| 11 | **テスト設計書** | Unit、Integration、Regression、UseCase、异常场景测试 | 保证工具本身质量，也定义如何验证工具正确性。 |

---

## 我认为这 11 份里，真正的核心只有 5 份

如果按重要程度排序：

1. **要件定義書**（做什么）
2. **現行業務分析書**（理解现状）
3. **API設計書**（定义每个 API）
4. **検証UseCase設計書**（定义最小验证链）
5. **システム設計書**（定义工具如何执行）

这 5 份文档构成了整个项目的主干。

---

## 我建议再增加一个“索引型成果物”（不是设计书）

虽然不是传统设计书，但对你的项目非常有价值：

### **成果物：API・UseCase対応一覧**

| API | UseCase | Step | 是否入口API | Extract变量 |
|------|----------|------|------------|------------|
| CreateCustomer | UC01 | 1 | ○ | CUSTOMER_ID |
| CreateAccount | UC01 | 2 | × | ACCOUNT_ID |
| Balance | UC01 | 3 | × | BALANCE |
| Payment | UC02 | 2 | × | TRANSACTION_ID |

**为什么需要？**

因为你的项目有：

- 24 个 API
- 约 10 个 UseCase
- 每个 API 可能被多个 UseCase 使用

这张对应表会成为维护和 Review 时最常查阅的资料，也方便确认 API 覆盖率、UseCase 影响范围，以及后续新增 API 时应该加入哪些 UseCase。它不是传统意义上的设计书，但在平台型项目中往往是最有价值的成果物之一。

## 第 38 轮

### 你

你说的对的

### ChatGPT

我觉得我们现在已经把这个项目真正的形态看清楚了，而且我建议**不要照搬日本传统业务系统开发**，而是借鉴它，再结合平台产品的特点。

我现在会把成果物重新组织一下，我认为这才是真正适合你这个项目的。

---

# 这个项目真正的资产（Asset）是什么？

不是 Java。

不是 Batch。

而是：

```text
业务Flow
    ↓
E6 API
    ↓
Verification UseCase
    ↓
每天自动执行
```

所以真正需要长期维护的是：

```text
API
UseCase
Rule
```

程序反而比较稳定。

---

# 我重新整理后的成果物（我认为以后几年都不会推翻）

| No | 成果物 | 是否长期维护 | 谁维护 |
|-----|---------|-------------|---------|
| 01 | 要件定義書 | ★ | Tool Team |
| 02 | QA一覧 | ★ | Tool Team |
| 03 | 現行業務分析書 | ★ | Tool Team |
| 04 | E6 API Catalog | ★★★★★ | Tool Team |
| 05 | Verification UseCase Catalog | ★★★★★ | Tool Team |
| 06 | API設計書（24 API） | ★★★★★ | Tool Team |
| 07 | UseCase設計書（约10件） | ★★★★★ | Tool Team |
| 08 | システム設計書 | ★★ | Tool Team |
| 09 | 共通Framework設計書 | ★★ | Tool Team |
| 10 | 運用設計書 | ★★ | Tool Team |

你会发现：

真正天天维护的是：

```text
API

↓

UseCase
```

---

# 我建议增加两个Catalog（我认为是整个项目最重要）

日本很多项目没有。

但是平台项目都会有。

---

## ① E6 API Catalog

不是API设计书。

而是：

```text
API编号

API名称

Capability

使用UseCase

依赖API

重要度

版本
```

例如：

| API | Capability | UseCase |
|------|------------|----------|
| CreateCustomer | Customer | UC01 |
| GetCustomer | Customer | UC01 |
| CreateAccount | Account | UC01 |
| Balance | Balance | UC02 |

以后：

**所有设计书都引用它。**

---

## ② Verification UseCase Catalog

例如：

| UseCase | 验证目标 | API数 |
|----------|----------|-------|
| UC01 | Customer生命周期 | 4 |
| UC02 | Balance | 3 |
| UC03 | Payment | 5 |

以后：

业务Flow变化：

↓

只更新：

UseCase Catalog

---

# 然后设计书全部引用Catalog

例如：

API设计书：

```
API-001

参照：

E6 API Catalog
```

---

UseCase设计书：

```
UC-001

参照：

UseCase Catalog
```

---

# 这样最大的好处

假设：

以后：

24 API

变成：

30 API

你：

不用改：

全部设计书。

只改：

```
API Catalog
```

然后：

新增：

```
API设计书
```

即可。

---

假设：

以后：

10 UseCase

变成：

15 UseCase

你：

只更新：

```
UseCase Catalog
```

即可。

---

# 我认为整个项目应该形成这种关系

```text
                要件定義

                     │

              QA一覧

                     │

         現行業務分析書

                     │

             API Catalog
                  │
        ┌─────────┴─────────┐
        │                   │
   API設計書           UseCase Catalog
                            │
                    UseCase設計書
                            │
                 システム設計書
                            │
                    Java Framework
```

---

## 我现在反而建议

以后：

**不要让设计书直接引用设计书。**

全部引用：

```
Catalog
```

这样：

整个项目：

会变得非常容易维护。

---

**我认为，这是我们这几天讨论下来，最大的一个设计优化。**

因为你的项目已经不是一个普通 Batch，而是一个**Verification Platform**。

对于平台来说：

> **Catalog（资产目录）永远比 Design（设计）更重要。**

而日本很多项目没有这一层，所以后期维护非常痛苦。

我建议我们下一步就先把这两个 **Catalog** 做成工业级规范，它们会成为整个项目最核心的资产。

## 第 39 轮

### 你

可以

### ChatGPT

我觉得这是我们整个项目到目前为止**最重要的一次架构调整**。

因为我们终于找到这个项目真正的"主数据（Master Data）"了。

以后整个项目都围绕它展开。

---

# 我建议整个项目叫做

> **E6 API Verification Platform**

整个项目只有两个 Master。

```text
                E6 API Catalog
                       │
                       │
               Verification UseCase Catalog
                       │
          ┌────────────┼────────────┐
          │            │            │
      API Design   UseCase Design  Framework
```

所以，以后所有设计书都来自这两个 Catalog。

---

# Catalog①

# E6 API Catalog（APIマスター）

这是整个项目最重要。

建议编号：

```text
CAT-API-001
```

字段如下：

| 项目 | 内容 | 说明 |
|------|------|------|
| API ID | API001 | 工具内部唯一编号 |
| API Name | CreateCustomer | API名称 |
| E6 API Name | 官方名称 | 对应E6文档 |
| Version | v1 | API版本 |
| Category | Customer | Capability分类 |
| Method | POST | HTTP Method |
| URI | /customer | Endpoint |
| Auth | OAuth | 认证方式 |
| Request Spec | API-001 | 对应API设计书 |
| Response Spec | API-001 | 对应API设计书 |
| Used UseCase | UC001、UC004 | 被哪些UseCase使用 |
| Depends On | API000 | 前置API |
| Output Variable | CUSTOMER_ID | 输出Context |
| Status | Active | 是否使用 |
| Owner | E6 | API所有者 |
| Note | 备注 | 特殊说明 |

---

# Catalog②

# Verification UseCase Catalog

建议编号：

```text
CAT-UC-001
```

字段：

| 项目 | 内容 |
|------|------|
| UC ID | UC001 |
| 名称 | Customer Registration |
| Purpose | Customer API验证 |
| Priority | High |
| Capability | Customer |
| Entry API | API001 |
| API Count | 4 |
| API List | API001~004 |
| Expected Result | PASS |
| Baseline | Yes |
| Daily Execute | Yes |
| Auto | Yes |
| Owner | Tool Team |

---

# Catalog③

# API Mapping Catalog

这个以后最好维护。

例如：

| API | UC001 | UC002 | UC003 | UC004 |
|------|:----:|:----:|:----:|:----:|
| API001 | ○ | | | |
| API002 | ○ | | | |
| API003 | | ○ | | |
| API004 | | ○ | | |
| API005 | | | ○ | |

以后：

一眼知道：

```text
哪些API没人验证

哪些UseCase覆盖了哪些API
```

---

# Catalog④

# Variable Catalog

这是以后Java最重要。

例如：

| Variable | 来源 | 类型 |
|-----------|------|------|
| CUSTOMER_ID | API001 | String |
| ACCOUNT_ID | API003 | String |
| TOKEN | Login | String |
| BALANCE | API005 | Decimal |

以后：

UseCase：

不用写：

```text
customerId
```

全部：

```text
${CUSTOMER_ID}
```

---

# Catalog⑤

# Environment Catalog

例如：

| ENV | Endpoint | Auth | Tenant |
|-----|----------|------|--------|
| DEV | xxxx | OAuth | DEV |
| STG | xxxx | OAuth | STG |
| PROD | xxxx | OAuth | PROD |

以后：

不用：

设计书里面：

写：

Endpoint。

全部引用：

Catalog。

---

# 然后真正设计书只有几份

---

## API设计书

一份API一份。

里面：

```text
Request

Response

Extract

Compare

Error

Retry
```

---

## UseCase设计书

里面：

```text
Flow

Entry

API顺序

Business Check

Exception
```

---

## Framework设计书

里面：

```text
RunContext

Runner

Diff

Snapshot

Report
```

---

# 我认为最终成果物应该这样

```text
documents/

    catalog/

        api-catalog.xlsx

        usecase-catalog.xlsx

        variable-catalog.xlsx

        environment-catalog.xlsx

        api-mapping.xlsx

    api/

        API001.md

        API002.md

        ...

    usecase/

        UC001.md

        UC002.md

        ...

    architecture/

        system.md

        framework.md

        operation.md

        deployment.md

    requirements/

        requirement.md

        qa.md

        current-analysis.md
```

---

# 我认为这是最大的变化

以前：

```text
业务设计书

↓

开发
```

现在：

```text
Catalog

↓

Design

↓

Java

↓

Execution
```

整个项目以后：

维护：

不是：

Java。

而是：

```text
API Catalog

↓

UseCase Catalog
```

---

## 我最后再提一个建议（这是我最推荐的）

如果让我做这个项目。

**我不会用Excel维护Catalog。**

我会：

```text
catalog/

api/

API001.yaml

API002.yaml

...

usecase/

UC001.yaml

UC002.yaml
```

然后：

自动生成：

- API设计书（Markdown）
- UseCase设计书（Markdown）
- MkDocs
- Java Spec JSON
- 测试报告模板

这样以后：

> **Catalog 才是真正唯一的数据源（Single Source of Truth，SSOT）。**

这也非常符合你之前一直在推进的 **Agent + MkDocs + RAG + Spec 自动生成** 的整体架构思想。

## 第 40 轮

### 你

就是想用markdown来做设计书 并且开发和测试书 测试数据 以及测试都用ai自动

### ChatGPT

完全可以，而且这就是最适合你的方向。

你的目标可以定义成：

```text
Markdown Design as Source
  ↓
AI 自动生成开发任务
  ↓
AI 自动生成测试书
  ↓
AI 自动生成测试数据
  ↓
Java Batch 自动执行
  ↓
AI/工具自动生成结果报告
```

核心原则是：

```text
Markdown = 人和 AI 共通的设计书
JSON/YAML = 程序执行用规格
Java = 执行引擎
AI = 生成、补全、检查、测试辅助
```

---

## 最终资料结构

```text
docs/
  01_requirements/
    要件定義書.md
    QA一覧.md

  02_catalog/
    E6_API_Catalog.md
    Verification_UseCase_Catalog.md
    Variable_Catalog.md
    Environment_Catalog.md
    API_UseCase_Mapping.md

  03_api_design/
    API001_CreateCustomer.md
    API002_GetCustomer.md
    API003_CreateAccount.md

  04_usecase_design/
    UC001_CustomerLifecycle.md
    UC002_AccountLifecycle.md
    UC003_BalanceFlow.md

  05_framework_design/
    システム設計書.md
    RunContext設計書.md
    Snapshot設計書.md
    Diff設計書.md
    Report設計書.md

  06_test_design/
    テスト方針書.md
    UC001_テスト仕様書.md
    UC002_テスト仕様書.md

  07_operation/
    運用手順書.md
    リリース手順書.md
```

---

## AI自动化要做的事情

### 1. 从 Markdown 生成程序用 JSON

```text
API001_CreateCustomer.md
        ↓
API001.json
```

```text
UC001_CustomerLifecycle.md
        ↓
UC001.usecase.json
```

Java Batch 不直接读 Markdown，而是读生成后的 JSON。

---

### 2. 从 API设计书自动生成测试书

例如 API 设计书里有：

```text
customerName: string, required, maxLength=50
```

AI/工具自动生成：

```text
正常系：50文字以内
異常系：未指定
異常系：51文字
異常系：number型指定
```

---

### 3. 从 UseCase 设计书自动生成测试数据

比如：

```text
Entry API = CreateCustomer
後続 API = CreateAccount
```

自动生成：

```json
{
  "customerName": "E6TEST_${runId}",
  "currency": "JPY"
}
```

---

### 4. 自动执行

```bash
java -jar e6-api-verifier.jar run --usecase UC001 --env DEV
```

---

### 5. 自动生成结果报告

```text
runs/
  DEV_UC001_20260701/
    result.json
    diff.json
    result.md
    diff.md
```

---

## 你真正需要设计的核心成果物

| 成果物 | 作用 |
|---|---|
| E6 API Catalog.md | 24个API主目录 |
| Verification UseCase Catalog.md | 10个以内UseCase主目录 |
| API设计書.md | 每个API的输入、输出、比较规则 |
| UseCase設計書.md | API调用链、变量传递、期待结果 |
| テスト仕様書.md | AI根据设计自动生成，可人工修正 |
| テストデータ.md/json | AI根据UseCase自动生成 |
| Result/Diff.md | 每天自动生成结果 |

---

## 最重要的实现思想

不要让 AI 直接“猜着调用 API”。

必须是：

```text
Markdown设计书
  ↓
结构化抽取
  ↓
JSON Spec
  ↓
Java执行
```

AI 负责：

```text
生成设计草案
补全测试点
检查矛盾
生成测试数据
解释Diff结果
```

Java 负责：

```text
确定性执行
保存证迹
比较Snapshot
生成报告
```

这样既能用 AI 提效，又不会让执行不可控。

一句话：
**Markdown 做设计资产，AI 做生成和检查，Java Batch 做确定执行。**

## 第 41 轮

### 你

除usecase测试书之外 还需要api的各种测试 比如必须 最大 最小位数等

### ChatGPT

需要。应该分成两类测试书：

| 类型 | 目的 | 谁生成 |
|---|---|---|
| **API単体テスト仕様書** | 验证单个 API 的参数、类型、长度、必填、enum、错误返回是否变化 | 根据 API設計書 自动生成 |
| **UseCaseテスト仕様書** | 验证多个 API 连续调用、参数传递、最终业务结果是否变化 | 根据 UseCase設計書 自动生成 |

你说的：

```text
必須
最大桁数
最小桁数
型
enum
null
空文字
不正値
```

这些属于 **API単体テスト仕様書**。

---

## API単体テスト需要覆盖

| 分类 | 测试内容 |
|---|---|
| 必须 | 必填字段未指定 |
| 型 | string / number / boolean / object / array 错误 |
| 最大长度 | maxLength 正常、maxLength+1 异常 |
| 最小长度 | minLength 正常、minLength-1 异常 |
| 数值范围 | min、max、0、负数 |
| enum | 正常 enum、非法 enum |
| null | null 是否允许 |
| 空文字 | `""` 是否允许 |
| 格式 | date、datetime、email、uuid、currency |
| 组合 | A字段有值时B字段必填 |
| Header | Authorization、requestId、idempotencyKey |
| Status Code | 200/400/401/403/409/422 等 |

---

## 成果物建议增加

| No | 成果物 | 为什么 |
|---|---|---|
| 1 | **API単体テスト仕様書** | 验证每个 API 的输入输出契约 |
| 2 | **API単体テストデータ** | 保存必填、长度、型、enum 等测试数据 |
| 3 | **UseCaseテスト仕様書** | 验证 API 链路 |
| 4 | **UseCaseテストデータ** | 保存入口数据和链路验证数据 |

---

## AI自动生成方式

从 API设计書：

```text
customerName
type=string
required=true
minLength=1
maxLength=50
```

自动生成测试：

| Case | 值 | 期待 |
|---|---|---|
| 正常 | 50文字以内 | OK |
| 必须未指定 | 无 | NG |
| 空文字 | `""` | NG |
| 最大+1 | 51文字 | NG |
| 型错误 | number | NG |

---

所以最终测试体系应该是：

```text
API設計書
   ↓
API単体テスト仕様書
   ↓
API単体テストデータ

UseCase設計書
   ↓
UseCaseテスト仕様書
   ↓
UseCaseテストデータ
```

结论：
**UseCase 测试确认“链路是否变”；API 单体测试确认“单个 API 契约是否变”。两者都需要。**

## 第 42 轮

### 你

资料结构最新是什么

### ChatGPT

经过我们这几轮讨论，我觉得整个项目已经稳定下来了。

最大的变化就是：

> **设计书不再是为了人写，而是作为 AI 和程序共同使用的唯一规格（Single Source of Truth）。**

所以我建议资料结构最终定成下面这样。

---

# E6 API Verification Platform

```text
project/

├── docs/
│
│   ├── 01_requirements/
│   │
│   │   要件定義書.md
│   │   QA一覧.md
│   │
│   ├── 02_analysis/
│   │
│   │   現行業務分析書.md
│   │   E6_API分析書.md
│   │   API一覧.md
│   │
│   ├── 03_catalog/
│   │
│   │   E6_API_Catalog.md
│   │   Verification_UseCase_Catalog.md
│   │   API_UseCase_Mapping.md
│   │   Variable_Catalog.md
│   │   Environment_Catalog.md
│   │
│   ├── 04_api/
│   │
│   │   API001_CreateCustomer.md
│   │   API002_GetCustomer.md
│   │   ...
│   │
│   ├── 05_usecase/
│   │
│   │   UC001_CustomerLifecycle.md
│   │   UC002_AccountLifecycle.md
│   │   ...
│   │
│   ├── 06_framework/
│   │
│   │   システム設計書.md
│   │   共通Framework設計書.md
│   │   RunContext設計書.md
│   │   Snapshot設計書.md
│   │   Report設計書.md
│   │   環境設計書.md
│   │   運用設計書.md
│   │
│   ├── 07_test/
│   │
│   │   テスト方針書.md
│   │
│   │   api/
│   │
│   │      API001_テスト仕様書.md
│   │      API001_テストデータ.md
│   │      ...
│   │
│   │   usecase/
│   │
│   │      UC001_テスト仕様書.md
│   │      UC001_テストデータ.md
│   │      ...
│   │
│   └── 08_operation/
│
│       リリース手順書.md
│       Baseline運用.md
│       日次運用.md
│
├── generated/
│
│   api-json/
│
│   usecase-json/
│
│   test-json/
│
├── baseline/
│
│   API/
│
│   UseCase/
│
├── runs/
│
│   20260701/
│
│      result.json
│
│      diff.json
│
│      result.md
│
│      diff.md
│
│      snapshot/
│
│      raw/
│
└── src/
```

---

# 每层职责

## ① Requirements

回答：

```text
为什么开发？
```

AI不会执行。

---

## ② Analysis

回答：

```text
现在业务系统是什么？
```

AI辅助分析。

---

## ③ Catalog

整个项目最重要。

回答：

```text
有哪些API？

有哪些UseCase？

API属于哪个UseCase？
```

以后：

所有设计书：

都引用这里。

---

## ④ API

回答：

```text
一个API是什么？
```

里面：

```text
Request

Response

Extract

Compare Rule

Error

Retry

备注
```

AI：

根据它：

生成：

API测试。

---

## ⑤ UseCase

回答：

```text
多个API如何串起来？
```

里面：

```text
Entry

API顺序

Context

Business Check

Expected
```

AI：

根据它：

生成：

UseCase测试。

---

## ⑥ Framework

回答：

```text
程序如何执行？
```

不是：

业务。

而是：

```text
RunContext

Runner

Diff

Snapshot

Report
```

---

## ⑦ Test

这里全部：

AI自动生成。

例如：

API：

```text
API001.md

↓

API001_テスト仕様書.md

↓

API001_テストデータ.md
```

UseCase：

```text
UC001.md

↓

UC001_テスト仕様書.md

↓

UC001_テストデータ.md
```

---

## ⑧ generated

全部：

AI生成。

例如：

```text
Markdown

↓

JSON
```

程序：

读JSON。

不是：

Markdown。

---

# 最重要的一点

我现在建议：

**不要写重复内容。**

例如：

API001：

```text
最大长度

50
```

不要：

再写：

测试书：

```text
最大长度50
```

AI：

自动生成：

```text
50

↓

49

50

51

null

空字符串
```

---

同样：

UseCase：

```text
API001

↓

API002

↓

API003
```

AI：

自动生成：

UseCase测试。

---

# 我认为真正需要人工维护的只有这些

```text
Requirements

↓

Analysis

↓

Catalog

↓

API设计

↓

UseCase设计
```

其他：

全部：

AI生成。

---

# 我认为这是整个项目最理想的流程

```text
业务设计书
      │
      ▼
AI分析
      │
      ▼
API Catalog
      │
      ▼
UseCase Catalog
      │
      ▼
API设计书
      │
      ▼
UseCase设计书
      │
      ├─────────────┐
      ▼             ▼
AI生成API测试     AI生成UseCase测试
      │             │
      └──────┬──────┘
             ▼
      JSON Spec
             ▼
      Java Batch
             ▼
      Snapshot
             ▼
      Diff
             ▼
      AI生成Result.md
```

---

## 我现在还有一个建议（也是最后一个比较大的优化）

我建议把 **API设计书** 和 **UseCase设计书** 都设计成**固定模板（Template）**。

这样以后：

- 新增第 25 个 API，只需要按模板填写。
- 新增第 11 个 UseCase，也只需要按模板填写。
- AI 能稳定解析。
- 可以自动生成 JSON、测试书、测试数据、MkDocs 和 RAG。

**也就是说，模板本身也应该成为这个项目的一项正式成果物。**我认为这是整个体系实现长期自动化和标准化的关键一步。

## 第 43 轮

### 你

好 我也认为必要。另外测试有可能有文件读入输出 如何设计 比如开发的时候是否准备文件的写入写出util 还有json的处理 日期处理 异常log处理等等

### ChatGPT

这部分应该作为「共通Framework設計」里的核心内容来提前定。否则后面 API、UseCase、测试数据、报告都会各自写文件处理，最后很难维护。

### ChatGPT

需要，而且必须提前设计成 **共通部品**。

建议新增或细化这份成果物：

```text
共通Framework設計書.md
```

里面至少包含这些共通模块。

| 共通模块 | 作用 | 为什么必须 |
|---|---|---|
| FileUtil / FileService | 文件读入、写出、复制、目录创建、临时文件、Atomic Write | 测试数据、结果、Snapshot、Report 都依赖文件操作 |
| ResourceResolver | 解析测试文件路径、resources目录、文件流 InputStream | API 测试可能上传文件或接收文件 |
| JsonUtil | JSON 读写、格式化、JsonPath、对象转换 | UseCase JSON、Result JSON、Diff JSON 都需要 |
| DateTimeUtil | 日期生成、格式化、时区、日期字段比较 | 每天执行，日期字段变化要稳定处理 |
| MaskingUtil | Token、密码、个人信息、卡号脱敏 | 日志和报告不能泄露敏感信息 |
| LogUtil / RunLogger | 按 runId 输出日志、错误栈、TraceId | 多重启动、日次执行、障害调查必须用 |
| ExceptionHandler | 统一异常分类、错误码、停止/继续策略 | API失败、文件失败、JSON失败都要统一处理 |
| HashUtil | 文件 hash、response hash、snapshot hash | 文件比较、差异确认、证迹完整性 |
| ConfigLoader | 环境配置、Endpoint、认证、timeout | DEV/STG/本番相当环境切换 |
| Retry/TimeoutPolicy | HTTP timeout、retry控制 | 防止 Batch 挂死或重复更新 |
| PathManager | runs、baseline、generated、logs 路径管理 | 保证所有输出按 runId 隔离 |

---

## 文件输入输出要这样设计

不要各模块自己写：

```java
Files.write(...)
```

而是统一：

```java
fileService.writeJson(path, object);
fileService.readJson(path, clazz);
fileService.openResource(resourceId);
fileService.writeAtomic(path, bytes);
```

特别是结果文件必须用 **Atomic Write**：

```text
先写 result.json.tmp
成功后 rename 成 result.json
```

避免执行中断时产生半个文件。

---

## 文件流测试的目录设计

```text
docs/
  07_test/
    api/
      API010_テストデータ.md

test-resources/
  API010/
    input/
      sample.pdf
      sample.csv
    expected/
      expected_response.pdf

runs/
  DEV_UC001_20260701/
    raw/
      request.json
      response.json
      response_file.pdf
    snapshot/
      request_snapshot.json
      response_snapshot.json
    report/
      result.md
      diff.md
```

JSON 里不要放文件内容，只放引用：

```json
{
  "file": {
    "resource": "API010/input/sample.pdf",
    "contentType": "application/pdf",
    "compare": {
      "type": "hash"
    }
  }
}
```

---

## 这部分对应的设计文档

建议在资料结构里补充：

| 文档 | 内容 |
|---|---|
| **共通Framework設計書.md** | 共通部品整体 |
| **ファイル入出力設計書.md** | 文件读写、目录、资源、Atomic Write |
| **JSON設計書.md** | JSON格式、JsonPath、schema、序列化 |
| **ログ・例外設計書.md** | 日志、异常、错误码、mask、stacktrace |
| **日付・比較設計書.md** | 日期字段、时区、忽略规则、日期比较 |

如果要压缩文档数量，可以把后面四个都作为 **共通Framework設計書** 的章节。

---

## 结论

要提前做。

尤其这 5 个必须先定：

```text
1. FileService
2. JsonUtil
3. DateTimeUtil
4. RunLogger
5. ExceptionHandler
```

否则后面 AI 自动生成代码时，会各写各的，项目很快失控。

## 第 44 轮

### 你

最新的结构

### ChatGPT

最新建议结构如下：

```text
project/

├── docs/
│
│  ├── 01_requirements/
│  │   ├── 要件定義書.md
│  │   └── QA一覧.md
│
│  ├── 02_analysis/
│  │   ├── 現行業務分析書.md
│  │   ├── E6_API分析書.md
│  │   └── API一覧.md
│
│  ├── 03_catalog/
│  │   ├── E6_API_Catalog.md
│  │   ├── Verification_UseCase_Catalog.md
│  │   ├── API_UseCase_Mapping.md
│  │   ├── Variable_Catalog.md
│  │   └── Environment_Catalog.md
│
│  ├── 04_api_design/
│  │   ├── API設計書_Template.md
│  │   ├── API001_xxx.md
│  │   ├── API002_xxx.md
│  │   └── ...
│
│  ├── 05_usecase_design/
│  │   ├── UseCase設計書_Template.md
│  │   ├── UC001_xxx.md
│  │   ├── UC002_xxx.md
│  │   └── ...
│
│  ├── 06_framework_design/
│  │   ├── システム設計書.md
│  │   ├── 共通Framework設計書.md
│  │   ├── ファイル入出力設計書.md
│  │   ├── JSON設計書.md
│  │   ├── RunContext設計書.md
│  │   ├── Snapshot設計書.md
│  │   ├── Diff設計書.md
│  │   ├── Report設計書.md
│  │   ├── ログ・例外設計書.md
│  │   ├── 日付・比較設計書.md
│  │   └── 環境設計書.md
│
│  ├── 07_test_design/
│  │   ├── テスト方針書.md
│  │   │
│  │   ├── api/
│  │   │   ├── API単体テスト仕様書_Template.md
│  │   │   ├── API001_テスト仕様書.md
│  │   │   ├── API001_テストデータ.md
│  │   │   └── ...
│  │   │
│  │   └── usecase/
│  │       ├── UseCaseテスト仕様書_Template.md
│  │       ├── UC001_テスト仕様書.md
│  │       ├── UC001_テストデータ.md
│  │       └── ...
│
│  └── 08_operation/
│      ├── 運用設計書.md
│      ├── 日次運用手順書.md
│      ├── Baseline運用.md
│      └── リリース手順書.md
│
├── specs/
│  ├── api-json/
│  ├── usecase-json/
│  ├── test-json/
│  └── config-json/
│
├── test-resources/
│  ├── API001/
│  │   ├── input/
│  │   └── expected/
│  └── UC001/
│      ├── input/
│      └── expected/
│
├── generated/
│  ├── markdown/
│  ├── json/
│  ├── reports/
│  └── mkdocs/
│
├── baseline/
│  ├── api/
│  └── usecase/
│
├── runs/
│  └── {runId}/
│      ├── run-info.json
│      ├── raw/
│      ├── snapshot/
│      ├── diff/
│      ├── reports/
│      ├── logs/
│      └── tmp/
│
├── config/
│  ├── dev.json
│  ├── stg.json
│  └── prod.json
│
└── src/
```

核心理解：

```text
docs/        人和AI维护的设计书
specs/       Markdown生成的程序执行用JSON
test-resources/ 文件读入/上传/期待输出资源
generated/   AI或工具自动生成物
baseline/    昨日/承认済み基准
runs/        每次执行结果
config/      环境配置
src/         Java实现
```

最重要的人工维护对象：

```text
1. E6_API_Catalog.md
2. Verification_UseCase_Catalog.md
3. API設計書
4. UseCase設計書
5. 共通Framework設計書
```

其余测试书、测试数据、JSON Spec、报告，尽量由 AI/工具自动生成。

## 第 45 轮

### 你

可能最后承认者需要看一个总结报告即可 有必要再看各个测试里的

### ChatGPT

我认为**没有必要**。

而且这是日本项目里很典型的一个分层思想：

> **不同角色，看不同粒度的成果物。**

如果让承认者（承认者/PM/业务负责人）去看几百个测试结果，那这个工具基本就失败了。

---

## 我建议分成四层

### Level 1（承认者）

只看：

```text
日次検証サマリー
```

例如：

```text
E6 API Daily Verification Report

日期：
2026/07/01

结果：
PASS

API
24 / 24 PASS

UseCase
10 / 10 PASS

Diff
0

Ignore
15

Warning
0

Error
0

新增API
0

删除API
0

类型变化
0

承认：
□□□□
```

如果有问题：

```text
UseCase

UC004 Payment

↓

NG

↓

点击进入
```

---

### Level 2（Leader）

看：

```text
UseCase Summary
```

例如：

```text
UC001

PASS

----------------

UC002

PASS

----------------

UC003

NG

API005

status

String→Integer
```

Leader一般看到这里。

---

### Level 3（开发）

看：

```text
API Report
```

例如：

```text
API005

Request

Response

Diff

Snapshot

Raw
```

---

### Level 4（调查）

才需要：

```text
Raw Request

Raw Response

Json

Log

Trace

File
```

---

# 所以报告应该设计成树

```text
Summary Report

    │

    ▼

UseCase Report

    │

    ▼

API Report

    │

    ▼

Raw Evidence
```

---

## 我建议成果物也调整

其实：

不用：

```text
API001_テスト結果.md
```

每天都看。

而是：

自动生成：

```text
Daily_Report.md
```

里面：

```text
Summary

↓

UseCase Summary

↓

API Summary

↓

Detail Link
```

---

# 日本项目一般也是这样

例如：

每天：

CI：

```text
2000 Test

↓

PASS
```

Manager：

不会：

看：

```text
2000 Test Result
```

而是：

看：

```text
Regression Report

PASS
```

只有：

NG：

才点进去。

---

# 所以我建议增加一个Report层次

```text
Daily Summary

    │

UseCase Summary

    │

API Detail

    │

Evidence
```

这样：

不同角色：

看不同东西。

---

# 我甚至建议

**测试书**：

平时：

都不用看。

它只是：

AI生成。

执行。

真正每天看的：

只有：

```text
Summary Report
```

例如：

```text
今天

API：

24 PASS

UseCase：

10 PASS

Diff：

0

结论：

可以继续使用。
```

---

# 我认为整个项目最终真正每天会看的成果物只有两份

```text
① Daily Summary Report

② Diff Report
```

其它：

```text
API Test

UseCase Test

Raw

Json

Log
```

都是：

**Evidence（证迹）**

只有：

出问题：

才展开。

---

## 我建议把整个系统定位成

```text
Evidence Driven Verification Platform
```

也就是说：

**平时只看 Summary。**

发生异常：

再一层层钻：

```text
Summary

↓

UseCase

↓

API

↓

Raw

↓

Request/Response
```

这和日本很多银行、保险、支付系统的运维和回归验证方式非常接近，也最符合你这个项目"每天自动验证 E6 API 是否发生变化"的定位。

## 第 46 轮

### 你

对 那么最新结构以及各个成果物的使用说明一览

### ChatGPT

我觉得现在已经可以定版第一版了。

而且我建议不要再按照"开发文档"来看，而是按照**资料生命周期**来看。

因为你的资料以后会不断成长。

> **Markdown = 唯一事实来源（Single Source of Truth）**
>
> AI、Java、测试、报告全部围绕 Markdown 工作。

---

# E6 API Verification Platform

## 整体结构

```text
project
│
├── docs                ← 人维护（唯一事实来源）
│
├── specs               ← AI生成（程序执行规格）
│
├── test-resources      ← 测试文件资源
│
├── generated           ← AI自动生成成果物
│
├── baseline            ← 承认版本
│
├── runs                ← 每天执行结果
│
├── config              ← 环境配置
│
└── src                 ← Java程序
```

---

# docs（最重要）

这是整个项目真正维护的地方。

---

## 01_requirements

| 成果物 | 谁维护 | AI使用 | Java使用 | 用途 |
|---------|---------|---------|-----------|------|
| 要件定義書 | 人 | √ | × | 定义开发目标、范围、限制 |
| QA一覧 | 人 | √ | × | 所有确认事项及结论 |

---

## 02_analysis

| 成果物 | 谁维护 | AI | Java | 用途 |
|---------|--------|-----|-------|------|
| 現行業務分析書 | 人 | √ | × | 分析业务Flow |
| E6_API分析書 | 人 | √ | × | 分析E6 API |
| API一覧 | 人 | √ | × | API清单 |

作用：

> AI 理解业务。

不是执行。

---

## 03_catalog（★★★★★）

这是整个项目最大的资产。

| 成果物 | 谁维护 | AI | Java | 用途 |
|---------|--------|-----|-------|------|
| E6_API_Catalog | 人 | √ | √ | API目录 |
| Verification_UseCase_Catalog | 人 | √ | √ | UseCase目录 |
| API_UseCase_Mapping | 人 | √ | √ | API覆盖关系 |
| Variable_Catalog | 人 | √ | √ | Context变量 |
| Environment_Catalog | 人 | √ | √ | DEV/STG/PROD |

以后：

所有设计：

引用这里。

---

## 04_api_design（★★★★★）

每个API一份。

例如：

```text
API001_CreateCustomer.md
```

内容：

```text
API说明

Request

Response

Extract

Compare

Retry

Error

File Upload

File Download
```

作用：

> AI 自动生成：

- API测试
- JSON
- Mock
- Report

---

## 05_usecase_design（★★★★★）

例如：

```text
UC001.md
```

里面：

```text
Entry

Flow

API顺序

Context

Business Check

Expected

Cleanup
```

作用：

AI：

自动生成：

- UseCase测试
- Test Data
- JSON

Java：

直接执行。

---

## 06_framework_design

这里：

不是：

业务。

而是：

程序。

包括：

| 成果物 | 用途 |
|---------|------|
| システム設計書 | 系统架构 |
| 共通Framework設計書 | Common组件 |
| ファイル入出力設計書 | 文件流设计 |
| JSON設計書 | JSON处理 |
| RunContext設計書 | Context生命周期 |
| Snapshot設計書 | Snapshot生成 |
| Diff設計書 | 比较算法 |
| Report設計書 | 报告生成 |
| ログ・例外設計書 | Log/Exception |
| 日付・比較設計書 | 日期比较 |
| 環境設計書 | Linux/JDK/Tomcat |

---

## 07_test_design

这里：

**几乎全部AI生成。**

包括：

API：

```text
API001

↓

API001_Test.md

↓

API001_TestData.md
```

UseCase：

```text
UC001

↓

UC001_Test.md

↓

UC001_TestData.md
```

人工：

Review即可。

---

## 08_operation

包括：

```text
Release

Daily

Baseline

Cleanup
```

运维。

---

# specs

程序：

真正执行：

这里。

例如：

```text
API001.json

UC001.json

Config.json
```

全部：

AI：

从Markdown生成。

Java：

只读这里。

---

# test-resources

例如：

```text
pdf

csv

excel

image

zip
```

文件上传。

期待文件。

全部：

放这里。

---

# generated

全部：

AI：

生成。

例如：

```text
JSON

Test

MkDocs

HTML
```

不修改。

---

# baseline

每天：

批准：

这里。

例如：

```text
API

UseCase
```

---

# runs

每天：

一个Run。

例如：

```text
runs

  20260701

      Summary.md

      Diff.md

      API

      Raw

      Json

      Log
```

---

# config

例如：

```text
dev

stg

prod
```

---

# src

Java。

---

# 最终AI流程

```text
现行业务资料

↓

AI分析

↓

Catalog

↓

API设计

↓

UseCase设计

↓

AI生成Test

↓

AI生成JSON

↓

Java执行

↓

Snapshot

↓

Diff

↓

AI生成Summary
```

---

# 真正每天看的成果物

不是：

```text
API Test
```

不是：

```text
UseCase Test
```

而是：

## ① Daily Summary Report（给承认者）

```text
今天：

PASS

API：

24 PASS

UseCase：

10 PASS

Diff：

0
```

---

## ② Diff Report（给Leader）

例如：

```text
API005

status

String

↓

Integer
```

---

## ③ Evidence（开发调查）

需要时：

展开：

```text
Request

↓

Response

↓

Json

↓

Log

↓

Snapshot
```

---

# 我认为最终整个项目真正长期维护的只有五类资料（★★★★★）

```text
① Catalog

② API设计书

③ UseCase设计书

④ Framework设计书

⑤ 要件/QA
```

其余全部：

```text
AI生成

↓

Java执行

↓

AI生成报告
```

---

## 最后一个建议（我认为这是整个项目的最终形态）

为了让 AI、开发、测试完全统一，我建议每个 Markdown（API 设计书、UseCase 设计书、测试设计书）都采用**固定模板（Template）**，并在 `docs/templates/` 下维护，例如：

```text
docs/
└── templates/
    ├── API設計書_Template.md
    ├── UseCase設計書_Template.md
    ├── APIテスト仕様書_Template.md
    ├── UseCaseテスト仕様書_Template.md
    └── Report_Template.md
```

这样：

- **人**按模板编写。
- **AI**稳定解析并生成 JSON、测试书、测试数据。
- **Java**始终读取统一格式的 Spec。
- **MkDocs**可以直接生成 Wiki。

这套模板将成为整个平台的"文档契约"，也是未来自动化程度最高、维护成本最低的基础。

## 第 47 轮

### 你

结果比较这里的rule该在哪个文档设计呢

### ChatGPT

这是一个非常好的问题，我们前面讨论到这里，其实还差最后一块。

**我的答案是：不要只有一个地方。应该分层。**

因为"比较规则（Compare Rule）"有三种不同的作用域。

---

# 第一层：API级 Compare Rule（最主要）

**放在：API設計書**

这是最重要的，也是绝大部分 Rule 所在的位置。

例如：

```text
API001_CreateCustomer.md

## Compare Rule

Request

customerName
- Compare：完全一致

Response

customerId
- Compare：存在即可

status
- Compare：完全一致

createTime
- Ignore

traceId
- Ignore

message
- Compare：不比较
```

因为只有 API 自己最清楚：

- 哪些字段需要比较
- 哪些字段可以 Ignore
- 哪些字段只比较 Type
- 哪些字段只比较是否存在

所以 **80%~90% 的 Rule 都应该在 API 设计书里。**

---

# 第二层：UseCase级 Compare Rule

**放在：UseCase設計書**

这里不是比较字段。

而是比较：

```text
Business Result
```

例如：

```text
UC001

Customer
↓

Account
↓

Balance

Compare

Account Status
ACTIVE

Balance
>=0

Customer必须存在

Account必须建立成功
```

也就是说：

这里比较的是：

```text
业务结果
```

不是：

```text
JSON字段
```

---

# 第三层：Framework级 Compare Rule

**放在：Diff設計書**

这里只写：

```text
如何比较
```

而不是：

```text
比较什么
```

例如：

```text
Diff Engine

↓

读取API Compare Rule

↓

JsonPath

↓

Normalize

↓

Compare

↓

Output
```

这里不会写：

```text
status
```

因为：

Framework：

不知道：

status是什么。

---

# 还有一种特殊 Rule

例如：

```text
Date

UUID

Timestamp

RequestId

TraceId
```

这些：

所有API：

都一样。

我建议：

放：

```text
共通Framework設計書

↓

Global Compare Rule
```

例如：

```text
默认：

TraceId

Ignore

Timestamp

Ignore

UUID

Ignore

ResponseTime

Ignore
```

然后：

API：

如果：

需要：

覆盖：

即可。

例如：

```text
API001

Override

createTime

Compare
```

---

# 我建议最终的优先级

```text
Global Rule（Framework）

        ↓

API Rule

        ↓

UseCase Rule
```

后面的覆盖前面的。

例如：

```text
Global

TraceId Ignore

↓

API001

TraceId Compare

↓

最终：

Compare
```

---

# 所以最终资料关系应该是

```text
Framework

Global Rule
        │
        ▼
API设计书

Field Compare Rule
        │
        ▼
UseCase设计书

Business Compare Rule
        │
        ▼
Diff Engine
```

---

# 我建议在 API 设计书里增加一个章节

```text
## Compare Rule

### Request Compare

### Response Compare

### Ignore

### Normalize

### Expected Status

### Severity
```

例如：

| JSONPath | Rule | Severity |
|----------|------|----------|
| $.status | Equals | HIGH |
| $.customerId | Exists | HIGH |
| $.traceId | Ignore | - |
| $.createTime | Ignore | - |
| $.amount | Numeric Equals | HIGH |
| $.message | Ignore | - |

这样 AI 可以直接生成：

- JSON Compare Rule
- Diff Engine 配置
- API 测试
- 比较报告

---

## 我最后建议再细化一步（我认为这是最符合你项目的）

不要叫 **Compare Rule**。

统一叫：

**「Verification Rule（検証ルール）」**

然后按层次划分：

| 文档 | Verification Rule 内容 |
|------|-------------------------|
| **共通Framework設計書** | 全局规则（日期、TraceId、UUID、时区、默认 Ignore、比较算法） |
| **API設計書** | 字段级规则（Request/Response 每个字段如何验证、是否 Ignore、Severity） |
| **UseCase設計書** | 流程级规则（API 顺序、业务状态、最终结果、跨 API 一致性） |

这样职责非常清晰：

- **Framework** 决定"如何执行验证"。
- **API** 决定"字段怎么验证"。
- **UseCase** 决定"业务流程怎么验证"。

我认为这是最符合日本 SI 设计文档分层，也最利于 AI 自动生成和 Java 实现的方案。

## 第 48 轮

### 你

api里面可能很多入力 出力参数 。每个usecase 里可能调用很多api 。如何在测试书里按照设计的rule来对比 形成结果 。

### ChatGPT

这里要把“测试书”从人工确认表，升级成“规则执行矩阵”。也就是每个 API 字段、每个 UseCase Step 都有 ruleId，执行结果才能自动汇总。

### ChatGPT

要这样设计：

```text
API設計書 = 定义字段和字段级Rule
UseCase設計書 = 定义调用顺序和流程级Rule
テスト仕様書 = 把这些Rule展开成可执行检查项
実行結果 = 每个Rule的PASS/FAIL/WARN结果
Summary = 汇总给承认者看
```

核心是：**每条检查都要有 Rule ID。**

---

## 1. API设计书里定义字段级 Rule

例如 `API001_CreateCustomer.md`：

| RuleId | 対象 | JSONPath | Rule | Severity |
|---|---|---|---|---|
| API001-REQ-001 | Request | $.customerName | Required | HIGH |
| API001-REQ-002 | Request | $.customerName | MaxLength=50 | HIGH |
| API001-REQ-003 | Request | $.customerName | Type=string | HIGH |
| API001-RES-001 | Response | $.customerId | Exists | HIGH |
| API001-RES-002 | Response | $.customerId | Type=string | HIGH |
| API001-RES-003 | Response | $.createdAt | Ignore | - |
| API001-RES-004 | Response | $.status | EqualsBaseline | HIGH |

---

## 2. UseCase设计书里定义流程级 Rule

例如 `UC001_CustomerLifecycle.md`：

| RuleId | Step | Rule | 内容 | Severity |
|---|---:|---|---|---|
| UC001-FLOW-001 | 1 | StatusCode | API001 status = 200 | HIGH |
| UC001-FLOW-002 | 1→2 | ContextExtract | API001.response.customerId → CUSTOMER_ID | HIGH |
| UC001-FLOW-003 | 2 | ContextUse | API002.request.customerId = ${CUSTOMER_ID} | HIGH |
| UC001-BIZ-001 | Final | BusinessCheck | customer status = ACTIVE | HIGH |

---

## 3. 测试书不是手写全部，而是 AI/工具生成

从 API设计书 + UseCase设计书生成：

```text
API単体テスト仕様書
UseCaseテスト仕様書
```

生成后的测试书应该长这样：

### API単体テスト仕様書

| TestId | API | RuleId | Test内容 | Input | Expected |
|---|---|---|---|---|---|
| T-API001-001 | API001 | API001-REQ-001 | 必須チェック | customerNameなし | 400 |
| T-API001-002 | API001 | API001-REQ-002 | 最大桁数正常 | 50文字 | 200 |
| T-API001-003 | API001 | API001-REQ-002 | 最大桁数超過 | 51文字 | 400 |
| T-API001-004 | API001 | API001-RES-001 | customerId存在 | 正常request | exists |

### UseCaseテスト仕様書

| TestId | UC | Step | API | RuleId | Expected |
|---|---|---:|---|---|---|
| T-UC001-001 | UC001 | 1 | API001 | UC001-FLOW-001 | 200 |
| T-UC001-002 | UC001 | 1 | API001 | UC001-FLOW-002 | CUSTOMER_ID抽出成功 |
| T-UC001-003 | UC001 | 2 | API002 | UC001-FLOW-003 | CUSTOMER_ID使用成功 |
| T-UC001-004 | UC001 | Final | - | UC001-BIZ-001 | ACTIVE |

---

## 4. 执行结果也按 RuleId 输出

每天执行后生成：

```text
runs/{runId}/reports/DailySummary.md
runs/{runId}/reports/DiffReport.md
runs/{runId}/reports/rule-result.json
```

`rule-result.json` 示例：

```json
{
  "runId": "DEV_20260701",
  "results": [
    {
      "ruleId": "API001-RES-004",
      "apiId": "API001",
      "jsonPath": "$.status",
      "expected": "ACTIVE",
      "actual": "ACTIVE",
      "result": "PASS",
      "severity": "HIGH"
    },
    {
      "ruleId": "API002-RES-002",
      "apiId": "API002",
      "jsonPath": "$.accountType",
      "expected": "string",
      "actual": "number",
      "result": "FAIL",
      "severity": "HIGH"
    }
  ]
}
```

---

## 5. 最终报告按层级汇总

承认者只看：

| 项目 | 結果 |
|---|---|
| 総合結果 | PASS |
| UseCase | 10/10 PASS |
| API | 24/24 PASS |
| Rule | 320/320 PASS |
| HIGH Fail | 0 |
| Warning | 0 |
| Ignore | 42 |

Leader 看：

| UseCase | Result | Failed Rule |
|---|---|---|
| UC001 | PASS | 0 |
| UC002 | FAIL | API002-RES-002 |

开发才看：

| RuleId | API | Path | Expected | Actual | Result |
|---|---|---|---|---|---|

---

## 6. 结论

你的设计应该变成：

```text
API字段多也没关系
UseCase调用API多也没关系

因为全部拆成：
RuleId
↓
TestId
↓
ExecutionResult
↓
Summary
```

最关键的设计是：

```text
API設計書：字段级规则
UseCase設計書：流程级规则
テスト仕様書：规则展开后的测试项
実行結果：每条Rule的执行结果
DailySummary：汇总结果
```

这样才能自动对比、自动生成结果、自动给承认者看总结。

### ChatGPT

```json
{
  "content_type": "thoughts",
  "thoughts": [],
  "source_analysis_msg_id": "e6b7d268-7423-44bd-aeca-0c8bbed901ae"
}
```

### ChatGPT

```json
{
  "content_type": "reasoning_recap",
  "content": "思考時間: 8s"
}
```

## 第 49 轮

### 你

那api设计书模版是啥样 比如api设计书模版怎么设计

### ChatGPT

我觉得这里终于到了整个项目的**核心**。

因为以后：

- AI生成Java
- AI生成测试
- AI生成测试数据
- AI生成Mock
- AI生成Report
- Java执行

**全部都是从 API设计书来的。**

所以 **API设计书不是给人看的，而是给 AI + Java + 人共同使用的。**

我建议不要按照日本传统 API 设计书（Request/Response 两张表）来写，而是设计成 **Machine Readable Markdown**。

---

# 我建议的 API设计书模板（工业版）

```text
# API001 Create Customer

---
metadata
---

API ID

API Name

Category

Version

Owner

Status

E6 API Name

Reference

UseCase

Last Update

---

## 1. Purpose

这个API是干什么的。

---

## 2. Endpoint

Method

URL

Header

Auth

Timeout

Retry

---

## 3. Request

### Header

|Name|Type|Required|Rule|

### Query

|Name|Type|Required|Rule|

### Path

|Name|Type|Required|Rule|

### Body

|JSONPath|Type|Required|Min|Max|Enum|Default|Description|

---

## 4. Request Validation Rule

Rule ID

Rule

Severity

Expected

---

## 5. Response

HTTP200

Body

|JSONPath|Type|Required|Description|

HTTP400

HTTP401

HTTP500

---

## 6. Response Compare Rule

Rule ID

JSONPath

Compare Type

Expected

Ignore

Normalize

Severity

---

## 7. Extract Rule

Variable

JsonPath

Required

Type

Description

---

## 8. File

Upload

Download

Content-Type

Compare Method

Hash

Size

---

## 9. Error Rule

Status

Retry

Continue

Stop

---

## 10. Test Generation Hint

Boundary

Normal

Exception

Combination

---

## 11. Change History
```

---

# 第3章 Request

例如：

| JSONPath | Type | Required | Min | Max | Enum |
|----------|------|----------|-----|-----|------|
| $.customerName | string | ○ | 1 | 50 | - |
| $.currency | string | ○ | - | - | JPY USD |
| $.amount | number | ○ | 0 | 999999999 | - |

AI：

看到：

```text
Min

Max

Type
```

直接生成：

API测试。

---

# 第4章 Validation Rule

例如：

| RuleID | Rule |
|--------|------|
| API001-REQ-001 | Required |
| API001-REQ-002 | MaxLength=50 |
| API001-REQ-003 | Type=String |
| API001-REQ-004 | Enum=JPY USD |

以后：

Java：

也能读。

---

# 第6章 Compare Rule

这是整个项目最大的特色。

例如：

| RuleID | JSONPath | Compare | Severity |
|---------|----------|----------|----------|
| API001-RES-001 | $.customerId | Exists | HIGH |
| API001-RES-002 | $.status | Equals | HIGH |
| API001-RES-003 | $.createdAt | Ignore | - |
| API001-RES-004 | $.traceId | Ignore | - |
| API001-RES-005 | $.message | Ignore | - |

Diff：

直接：

读取。

---

# 第7章 Extract

例如：

| Variable | JsonPath |
|-----------|----------|
| CUSTOMER_ID | $.customerId |
| TOKEN | $.token |

UseCase：

直接：

引用：

```text
${CUSTOMER_ID}
```

---

# 第8章 File

以后：

你说的：

文件上传。

例如：

```text
Upload

PDF

Max

10MB

Compare

Hash
```

下载：

```text
CSV

Compare

Content

Hash

Row Count
```

---

# 第10章 Test Hint

这是：

AI：

最喜欢。

例如：

```text
Boundary

true

Normal

true

Exception

true

Combination

false
```

AI：

知道：

生成：

哪些测试。

---

# 更进一步（我建议）

其实：

每一个字段：

都应该有：

Rule。

例如：

| JSONPath | Required | Compare | Test |
|-----------|----------|----------|------|
| $.customerName | ○ | Equals | Boundary |
| $.status | ○ | Equals | Enum |
| $.traceId | ○ | Ignore | No |
| $.createDate | ○ | Ignore | No |

这样：

AI：

就知道：

```text
API

↓

Test

↓

Compare

↓

Diff
```

全部：

自动。

---

# 我认为最后应该再增加一列（这是整个项目以后最值钱）

叫：

```text
Evidence
```

例如：

| JSONPath | Compare | Evidence |
|-----------|----------|----------|
| $.status | Equals | Summary |
| $.traceId | Ignore | None |
| $.customerId | Exists | Detail |
| $.message | Ignore | None |

什么意思？

以后：

Summary：

只放：

```text
status

customerId
```

而：

Raw：

才放：

全部。

这样：

承认者：

不用：

看到：

200个字段。

---

## 我建议把 API 模板定位成"声明式规格（Declarative Spec）"

它不写：

"程序怎么实现"

而写：

- **接口是什么**
- **字段是什么**
- **如何验证**
- **如何比较**
- **如何抽取**
- **如何生成测试**
- **如何生成证迹**

然后：

- AI 生成测试书
- AI 生成测试数据
- AI 生成 JSON Spec
- Java 负责执行
- AI 再根据执行结果生成 Summary 和 Diff

这样一份 API 设计书就成为整个平台真正的"唯一事实来源（SSOT）"。这也是我认为最适合你这个项目长期发展的模板设计。

## 第 50 轮

### 你

usecase设计书模版吗

### ChatGPT

我觉得 **UseCase设计书** 比 **API设计书** 还重要。

因为：

- **API设计书** 定义"一个 API"。
- **UseCase设计书** 定义"多个 API 如何组成一条业务验证链"。

对于你的项目来说：

> **每天执行的不是 API，而是 UseCase。**

所以 UseCase 才是真正的执行单位。

---

# 我建议 UseCase 设计书不要照搬日本传统设计书

日本传统一般会写：

```text
処理概要
処理フロー
処理詳細
```

但是你的项目不是业务开发，而是 **Verification Platform**。

所以应该采用下面这种模板。

---

# UC001_XXX.md

---

# 1. 基本信息（Metadata）

| 项目 | 内容 |
|------|------|
| UseCase ID | UC001 |
| 名称 | Customer Registration |
| Category | Customer |
| Priority | High |
| Execute | Daily |
| Owner | Tool Team |
| Baseline | Yes |
| Description | Customer API验证 |

---

# 2. Purpose（验证目的）

例如：

```text
确认 Customer 生命周期相关 API
是否和前一天一致。
```

这里不是业务目的。

而是：

> 为什么验证。

---

# 3. Entry Input

这里只有：

**第一个API需要的输入。**

例如：

| Variable | Type | Source |
|-----------|------|--------|
| customerName | String | TestData |
| currency | String | TestData |

以后：

AI：

生成：

TestData。

---

# 4. Flow

整个UseCase。

例如：

| Step | API | Description |
|------|------|-------------|
| 1 | API001 | Create Customer |
| 2 | API002 | Get Customer |
| 3 | API003 | Create Account |
| 4 | API004 | Balance |

这里只写：

顺序。

---

# 5. Context Flow（★★★★★）

这是整个UseCase最重要。

例如：

| Step | Output | Variable | Next Step |
|------|----------|----------|-----------|
| API001 | customerId | CUSTOMER_ID | API003 |
| API003 | accountId | ACCOUNT_ID | API004 |

以后：

Java：

自动：

Context。

---

# 6. API Mapping

例如：

| Step | API | Request Source |
|------|------|---------------|
| 1 | API001 | Entry |
| 2 | API002 | CUSTOMER_ID |
| 3 | API003 | CUSTOMER_ID |
| 4 | API004 | ACCOUNT_ID |

---

# 7. Flow Verification Rule（★★★★★）

这里：

不是：

字段。

而是：

流程。

例如：

| RuleID | Rule | Severity |
|---------|------|----------|
| UC001-001 | 全部API必须200 | HIGH |
| UC001-002 | CUSTOMER_ID必须成功Extract | HIGH |
| UC001-003 | ACCOUNT_ID必须成功Extract | HIGH |
| UC001-004 | API顺序不可改变 | HIGH |

---

# 8. Business Verification

这里：

验证：

业务。

例如：

| Rule | Expected |
|------|----------|
| Customer Exists | Yes |
| Account Exists | Yes |
| Status | ACTIVE |

---

# 9. Cleanup

例如：

```text
Delete Customer

Delete Account
```

或者：

```text
No Cleanup
```

---

# 10. Test Data

这里只引用：

```text
UC001_TestData.md
```

不要写。

---

# 11. Expected Result

例如：

```text
PASS

API

4 PASS

Diff

0

Warning

0
```

---

# 12. Generated Files

执行以后：

生成：

```text
Summary.md

Diff.md

Snapshot

Json

Log
```

---

# 我建议再增加一章（这是整个项目最重要）

## 13. Evidence（证迹）

例如：

| Evidence | Keep |
|----------|------|
| Request | Yes |
| Response | Yes |
| Snapshot | Yes |
| Diff | Yes |
| Log | Yes |
| File | Yes |

以后：

调查：

直接：

这里。

---

# AI真正读取的是这些章节

```text
Entry

↓

Flow

↓

Context

↓

Verification Rule

↓

Business Rule
```

然后：

自动生成：

```text
UseCase Test

↓

Test Data

↓

JSON Spec

↓

Execution Plan
```

---

# 我建议最终的 UseCase 模板结构

```text
Metadata

Purpose

Entry Input

Flow

Context Flow

API Mapping

Flow Verification Rule

Business Verification

Cleanup

Test Data

Expected Result

Evidence

Change History
```

---

## 我还想再给你一个建议（我认为会成为这个项目最大的亮点）

在 **UseCase设计书** 最后增加一章：

### **Execution Policy（実行ポリシー）**

例如：

| 项目 | 内容 |
|------|------|
| Stop On Error | Yes |
| Continue On Warning | Yes |
| Retry Count | 3 |
| Timeout | 30s |
| Compare Baseline | Yesterday |
| Ignore Global Rule | Yes |

这样：

以后 Java Runner **完全不用写死逻辑**。

它直接读取：

- API设计书
- UseCase设计书

然后：

- 自动生成执行计划（Execution Plan）
- 自动执行
- 自动比较
- 自动生成 Summary

这也是我认为整个平台最符合 **AI 驱动 + 声明式设计（Declarative Design）** 的最终形态。
