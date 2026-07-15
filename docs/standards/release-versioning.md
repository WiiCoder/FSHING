# 产品发布版本规范

## 版本格式

正式产品版本使用语义化版本 **vMAJOR.MINOR.PATCH**：

| 变化 | 使用场景 |
|---|---|
| v1.1.0 → v2.0.0 | 重大架构变化、破坏性 API 变化或产品定位变化 |
| v1.1.0 → v1.2.0 | 新功能或兼容性能力增强 |
| v1.1.0 → v1.1.1 | Bug、安全修复或小范围修正 |

预发布版本可使用 **v1.4.0-alpha.1**、**v1.4.0-beta.1**、**v1.4.0-rc.1**。产品版本不得因需求文档修改而升级。

## 版本字段

- **target_release**：计划版本，允许调整。
- **introduced_in**：首次出现实现并可验证的版本，允许是预发布版本。
- **released_in**：正式发布版本，只能在发布事实确认后填写。

延期只修改 **target_release**，不得修改需求 ID。原版本的 **requirements.md** 必须保留延期记录、目标新版本和原因。

## 发布目录

每个计划发布的版本使用：

~~~text
docs/releases/<version>/
├── release-plan.md
├── requirements.md
├── repositories.yaml
├── test-report.md
└── release-notes.md
~~~

**docs/releases/index.yaml** 保存版本、状态、计划日期和目录路径。**requirements.md** 是该版本需求范围和延期历史的发布记录。

每个 release 索引条目使用：

~~~yaml
- version: v1.4.0
  status: planning
  release_manager: Noah
  planned_release_date: 2026-08-15
  code_freeze_date: 2026-08-10
  released_at: null
  path: docs/releases/v1.4.0
  updated_at: 2026-07-18
~~~

发布索引只维护版本级元数据；需求成员关系和延期历史只维护在对应版本的 **requirements.md**，避免两份发布范围数据发生漂移。

## 发布仓库快照

每个版本的 **repositories.yaml** 保存实际纳入发布的精确代码 revision：

~~~yaml
schema_version: 1
release: v1.4.0
workflow_version: v1.0.0
captured_at: 2026-08-15
repositories:
  - id: service-api
    path: repos/service-api
    branch: main
    commit: 0123456789abcdef0123456789abcdef01234567
    tag: v1.4.0
    deployed_revision: 0123456789abcdef0123456789abcdef01234567
    pull_requests:
      - https://github.com/organization/service-api/pull/42
    dirty: false
~~~

发布快照必须来自子仓库实际 Git 状态，不得从计划分支或 workspace.lock.yaml 盲目复制。正式发布时，commit 或 deployed_revision 必须能够证明实际部署代码。

## 发布状态

| 状态 | 含义 |
|---|---|
| planning | 正在确定范围 |
| active | 范围已确认，正在实现和验证 |
| code-freeze | 仅允许发布阻塞问题修复 |
| release-ready | 所有门禁满足，等待正式发布 |
| released | 已正式发布 |
| cancelled | 版本取消，保留历史记录 |

发布状态不得自动推导需求状态。版本进入 **released** 后，只有实际包含且已部署的需求才能填写 **released_in** 并变为 **released**。

## 纳入版本

需求进入版本前必须满足：

1. Spec 的关键问题已确认并完成回写，状态至少为 **ready**。
2. **target_release** 与目标版本一致。
3. 组件、优先级和负责人已明确。
4. 主要风险和依赖已记录。
5. 发布需求清单已更新。

纳入后需求状态变为 **scheduled**。如果需求从版本移除，在原版本记录延期或取消原因，并同步更新 Spec 和需求索引。

## 发布门禁

最低门禁：

- 所有 P0/P1 需求已达到 release-ready，或有明确记录的移除决定；
- 每个 AC 都有测试结果和证据；
- 不存在阻塞级缺陷；
- API、数据库迁移、权限和安全变化已验证；
- 回滚方案已验证或明确说明不适用；
- repositories.yaml 已记录所有必需仓库的精确发布 revision；
- 测试报告和发布说明已完成；
- 实际发布负责人已确认版本状态。
