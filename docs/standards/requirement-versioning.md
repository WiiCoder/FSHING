# 需求编号与文档版本规范

## 目的

把需求身份、产品发布版本和需求文档修订版本分开管理，确保延期、拆分、跨版本实现和后续变更不会破坏历史追溯。

## 三个独立维度

| 维度 | 示例 | 规则 |
|---|---|---|
| 需求 ID | FEAT-2026-0042 | 永久不变，不包含目标产品版本 |
| 目标产品版本 | v1.4.0 | 可调整，表示当前计划发布版本 |
| Spec 版本 | 1.3 | 随需求内容变化，独立于产品版本 |

Git commit、PR、测试计划版本和测试报告版本是独立证据，不得代替以上字段。

## 需求 ID

格式为 **TYPE-YYYY-NNNN**：

| 前缀 | 类型 |
|---|---|
| FEAT | 新功能 |
| BUG | 缺陷修复 |
| TECH | 技术改造 |
| SEC | 安全需求 |
| OPS | 运维需求 |

分配规则：

1. 使用创建时所在自然年。
2. 在 **docs/features/index.yaml** 中查找同类型、同年份的最大序号并加一。
3. 序号固定为四位，不复用已取消或已替代需求的号码。
4. 创建目录 **docs/features/<ID>-<short-slug>/**。
5. 一旦分配，不因延期、拆分、重命名或跨版本发布而修改。

并发创建需求时，合并前必须重新检查索引；发现冲突时，仅未合并的新需求重新取号。

## 子项编号

每个 Feature 内独立编号：

| 前缀 | 含义 |
|---|---|
| FR | 功能需求 |
| NFR | 非功能需求 |
| AC | 验收条件 |
| TASK | 实现任务 |
| TC | 测试用例 |
| RISK | 风险 |
| DEC | 产品或技术决策 |

当前需求目录内可以写 **FR-001**；跨文档或跨需求引用必须写成 **FEAT-2026-0042 / FR-001**。

不得重新编号已经被任务、测试或发布文档引用的子项。删除的子项保留编号，并标记为 removed 或 superseded。

## Spec 版本

Spec 使用两段式版本 **主版本.次版本**，初始版本为 **1.0**。

次版本升级适用于不改变当前已确认核心行为的修改，例如：

- 补充说明、边界条件或示例；
- 修正文案；
- 增加测试场景；
- 澄清但不改变接口、数据模型、权限和关键验收标准。

主版本升级适用于：

- 修改核心业务流程或主要范围；
- 增删主要功能；
- 修改 API 契约、数据库结构或权限模型；
- 修改关键验收条件；
- 开发开始后发生影响实现方向的重要变化。

主版本升级必须把需求状态退回 **review**，主动向用户说明受影响的行为和取舍，并重新完成需求确认、技术设计影响分析、任务影响分析和测试更新。确认结果写回后即可恢复到 **ready**，不需要审批字段或签字记录。

## Spec 元数据

每个 **spec.md** 必须包含：

~~~yaml
---
id: FEAT-2026-0042
title: 客户标签管理
type: feature
spec_version: "1.3"
status: ready
target_release: v1.4.0
introduced_in: null
released_in: null
priority: P1
owner: product
components:
  - public-api
  - admin-web
created_at: 2026-07-14
updated_at: 2026-07-18
supersedes: null
superseded_by: null
---
~~~

字段规则：

- **target_release**：当前计划进入的软件版本，可调整。
- **introduced_in**：首次出现可验证实现的版本，可为预发布版本。
- **released_in**：实际正式发布版本，仅在发布确认后填写。
- **supersedes / superseded_by**：保存替代关系，不删除历史需求。

## 变更记录

每个 **spec.md** 末尾必须有 Change Log。每次 Spec 变化追加一行，禁止覆盖历史：

| Spec Version | Date | Change | Impact | Decision Context |
|---|---|---|---|---|
| 1.0 | 2026-07-14 | 创建初始需求 | 无 | 对话确认核心范围和验收条件 |

重大变更还必须创建 **changes/<spec-version>.md**，记录受影响的 FR、AC、API、数据、权限、任务、测试和发布版本。

## 需求索引条目

**docs/features/index.yaml** 不替代 Spec；它是从各需求 Spec 元数据同步得到的机器可读目录。不得把 **_template** 当成实际需求。

每个 requirement 条目使用：

~~~yaml
- id: FEAT-2026-0042
  title: 客户标签管理
  type: feature
  priority: P1
  status: verifying
  spec_version: "1.3"
  target_release: v1.4.0
  introduced_in: v1.4.0-rc.1
  released_in: null
  owner: product
  components:
    - public-api
    - admin-web
  path: docs/features/FEAT-2026-0042-customer-tags
  updated_at: 2026-07-18
~~~

索引字段必须与对应 **spec.md** 一致。Markdown 表格或汇总页面应从 YAML/Spec 生成，不再建立第二份人工维护的需求总表。
