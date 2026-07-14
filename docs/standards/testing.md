# 需求测试与验证规范

## 目标

测试必须证明指定 Spec 版本的需求已实现，而不是只证明代码可以运行。

追溯链为：

~~~text
FR/NFR → AC → TC → Test Run → Evidence
~~~

跨文档引用时附带 Requirement ID；测试报告还必须记录 Spec 版本和目标产品版本。

## 测试计划元数据

每个 **test-plan.md** 必须包含：

~~~yaml
---
feature_id: FEAT-2026-0042
spec_version: "1.3"
target_release: v1.4.0
test_plan_version: "1.2"
status: active
updated_at: 2026-07-18
---
~~~

当测试内容变化时升级 test_plan_version。Spec 变化时必须更新 spec_version，并执行覆盖影响分析。

## 测试用例

最低字段：

| 字段 | 要求 |
|---|---|
| Test ID | 当前需求内唯一，格式 TC-NNN |
| Requirement | 至少关联一个 FR 或 NFR |
| Acceptance | 至少关联一个 AC |
| Since Spec | 首次要求该测试的 Spec 版本 |
| Test Type | Unit、API、UI、Integration、E2E、Security、Performance 等 |
| Status | not-run、passed、failed、blocked、not-applicable |
| Evidence | 命令输出、报告路径、截图、日志或人工验收记录 |

没有证据的 passed 无效。not-applicable 必须记录原因和批准者。

## 覆盖规则

1. 每个 AC 至少被一个 TC 覆盖。
2. 每个 NFR 必须有可测量方法，或明确记录不可自动化的人工验证步骤。
3. API、数据迁移、权限、安全和并发变化必须有对应专项测试。
4. 缺陷需求必须包含能够在修复前失败、修复后通过的回归用例。
5. 任务完成不能替代验收测试。

## Spec 变更影响

Spec 版本升级时：

1. 比较新增、修改、删除的 FR/NFR/AC。
2. 标记受影响的 TC。
3. 新增缺失测试，更新 Since Spec。
4. 将失效的旧通过结果重置为 not-run。
5. 在 verification.md 记录重新执行的范围和结果。

主版本升级时，必须重新评估全部验收覆盖；不得默认沿用上一主版本的测试结论。

## 验证证据

证据应包含：

- 执行日期和执行者；
- 组件和环境；
- 精确命令、测试报告路径或人工步骤；
- 结果及失败摘要；
- 关联的 TC、AC 和 Spec 版本；
- 已知偏差、豁免和批准。

敏感信息不得写入文档。日志和截图应脱敏。
