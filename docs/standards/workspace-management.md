# 多仓库工作区管理规范

## 模板与项目实例

FSHING 源仓库只维护可复用的工作流，不保存任何具体项目数据。

| 模式 | 识别方式 | 允许的数据 |
|---|---|---|
| FSHING 模板 | workspace.yaml 不存在 | workflow-version.yaml、workspace.example.yaml、标准、技能和模板 |
| 本地覆盖 | workspace.yaml 与 workspace.lock.yaml 仅被 .git/info/exclude 忽略 | 仅用于在本机映射真实仓库和验证 FSHING，不得提交项目数据 |
| 初始化 | workspace.yaml 存在，但必填身份、仓库、克隆或锁文件不完整 | 仅允许补全和验证工作区 |
| 项目实例 | workspace.yaml 与 workspace.lock.yaml 完整且匹配实际仓库 | 项目身份、仓库清单、锁文件、需求、测试和发布记录 |

每个项目必须从 FSHING 创建自己的项目控制仓库，并使用独立 Git origin。项目数据不得推送回 FSHING。

FSHING 维护者可以在本地 clone 的 **.git/info/exclude** 中忽略 workspace.yaml 和 workspace.lock.yaml，临时映射真实仓库验证工作流。不得把这两个文件加入模板的 .gitignore，因为项目实例必须正常跟踪它们。

进入项目实例模式前必须验证：

- project.id、project.name、project.control_repository 非空；
- 至少声明一个 required repository；
- 每个 required repository 的 ID、角色、路径、URL、默认分支和组件列表完整；
- 每个 required repository 已存在于声明路径，origin 与声明一致；
- workspace.lock.yaml 与实际 branch、HEAD 和 dirty 状态一致。

## 仓库边界

~~~text
project-control/.git
project-control/repos/service-a/.git
project-control/repos/web-app/.git
project-control/repos/worker/.git
~~~

规则：

1. 父仓库通过 **.gitignore** 忽略 **repos/*/**。
2. 禁止在父仓库中强制添加子仓库目录。
3. 每次 Git 操作前明确目标是父仓库还是某个子仓库。
4. 跨仓库需求必须记录每个仓库各自的 commit SHA 或 PR URL。
5. 父仓库提交不能替代子仓库提交，子仓库提交也不能替代需求和验证证据。

## 工作区示例

FSHING 提供不含项目数据的 **workspace.example.yaml**。项目创建后复制为 **workspace.yaml** 并填写：

~~~yaml
schema_version: 1
project:
  id: sample-product
  name: Sample Product
  control_repository: "git@github.com:organization/sample-product-control.git"
workflow:
  version_file: workflow-version.yaml
repositories:
  - id: service-api
    role: service
    path: repos/service-api
    url: "git@github.com:organization/service-api.git"
    default_branch: main
    required: true
    components:
      - public-api
      - background-jobs
~~~

仓库 ID 和组件 ID 是两个维度：

- repository ID 标识 Git 仓库，例如 **service-api**；
- component ID 标识仓库内的产品组件，例如 **public-api**、**background-jobs**。

需求索引使用 component ID；任务和验证证据同时记录 repository ID 与 component ID；发布快照使用 repository ID。URL 不得包含凭证。

## 工作区锁定

项目实例创建 **workspace.lock.yaml** 保存一次已解析工作区快照：

~~~yaml
schema_version: 1
workflow_version: v1.0.0
resolved_at: "2026-07-14"
repositories:
  - id: service-api
    path: repos/service-api
    branch: main
    commit: 0123456789abcdef0123456789abcdef01234567
    dirty: false
~~~

锁文件用于复现和诊断，但不是正式发布证据。更新锁文件前必须读取每个子仓库的实际 HEAD 和工作区状态，不得猜测。

## 新项目初始化

1. 使用 GitHub Template 功能从 FSHING 创建独立的项目控制仓库。
2. 确认项目控制仓库的 origin 不是 FSHING。
3. 复制 workspace.example.yaml 为 workspace.yaml。
4. 填写项目身份、仓库 URL、路径、默认分支和组件映射。
5. 把子仓库克隆到声明路径。
6. 验证每个 origin、默认分支、HEAD 和工作区状态。
7. 创建 workspace.lock.yaml。
8. 在父仓库提交控制文件，在子仓库分别管理代码提交。

多个项目不得把需求、发布和锁文件推送到同一个控制仓库。

## 跨仓库变更

一个需求涉及多个仓库时：

- tasks.md 为每个 TASK 同时指定 repository ID 和 component ID；
- 每个仓库独立创建 commit 或 PR；
- verification.md 记录 repository ID、component ID、commit/PR 和对应 TC；
- 任一必需仓库未完成时，需求不能进入 release-ready；
- 发布快照必须列出最终实际发布的全部仓库 revision。

## FSHING 升级

工作流版本独立于产品版本。升级时：

1. 读取 FSHING 发布说明和兼容要求；
2. 更新标准、技能和模板；
3. 更新 workflow-version.yaml；
4. 验证现有项目数据仍符合新 schema；
5. 在项目控制仓库中创建单独的工作流升级提交。

不得因为产品发布或 Spec 修订而修改 FSHING 版本。

## 安全与恢复

- 不在 workspace.yaml、锁文件或发布快照中保存令牌、私钥和密码。
- 子仓库不可访问时保留现有克隆，并明确报告无法刷新。
- 移动子仓库前确认工作区状态；目录移动不得丢弃未提交变更。
- 错误的父仓库提交应从父仓库移除 gitlink 或嵌入目录，但不得删除子仓库工作区。
