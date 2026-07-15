# 需求生命周期规范

## 主流程

~~~text
backlog
  → draft
  → review
  → ready
  → scheduled
  → in-progress
  → verifying
  → release-ready
  → released
~~~

## 状态准入条件

| 状态 | 准入条件 |
|---|---|
| backlog | 已记录标题、类型和基本背景 |
| draft | 已分配需求 ID，正在编写 Spec |
| review | FR/NFR、AC、范围、风险和目标版本已可评审 |
| ready | 关键问题已在对话中确认并写回当前 Spec，没有阻塞规划的未决项 |
| scheduled | 已纳入具体发布版本且 target_release 一致 |
| in-progress | 设计和任务已建立，开发已经开始 |
| verifying | 实现完成或达到可测试状态，正在执行验证 |
| release-ready | 所有适用 AC 通过，证据完整，无阻塞问题 |
| released | 已随 released_in 对应的正式版本发布 |

状态变化必须由文档和证据驱动。对话中的确认必须先写回权威文档，不能仅根据口头描述或代码存在推断。

## 例外状态

| 状态 | 处理规则 |
|---|---|
| blocked | 记录阻塞原因、负责人和解除条件；解除后回到原主流程状态 |
| deferred | 在原版本记录延期原因和新目标版本；重新排期后进入 scheduled |
| cancelled | 保留 ID、Spec 和历史，不再进入发布 |
| superseded | 填写 superseded_by，新需求填写 supersedes |

例外状态不得删除历史目标版本、确认决定或验证证据。

## 变更对状态的影响

- **次版本 Spec 变化**：根据影响保留当前状态或退回 review；所有受影响测试必须重新评估。
- **主版本 Spec 变化**：必须退回 review，主动讨论所有重大影响并完成回写后才能回到 ready。
- **目标版本调整**：在原发布目录记录 deferred；新版本纳入后进入 scheduled。
- **测试失败**：保持 verifying，或在无法继续时进入 blocked。
- **代码完成**：最多进入 verifying，不等于 release-ready。
- **发布门禁通过**：进入 release-ready，不等于 released。
- **实际正式发布**：填写 released_in 后进入 released。

## 一致性约束

- ready 及后续状态必须没有未解决的阻塞需求决定，确认结果必须存在于当前 Spec。
- scheduled 及后续状态必须存在 target_release。
- verifying 及后续状态必须存在 test-plan.md。
- release-ready 必须存在 verification.md 中的通过证据。
- released 必须存在 released_in，且对应发布版本状态为 released。
- superseded 必须存在 superseded_by。
