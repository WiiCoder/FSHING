# FSHING

[English](README.md) | [简体中文](README.zh-CN.md)

FSHING 是一个可复用的 GitHub 模板，用于管理由多个 Git 仓库组成的软件项目，并通过 AI 辅助完成需求、实现、测试、评审和发布流程。

FSHING 只保存工作流规范、技能和文档模板，不保存任何具体产品的仓库地址、分支、提交、需求或发布记录。

## 运行模式

### 模板模式

当 **workspace.yaml** 不存在且 **workspace.example.yaml** 存在时，FSHING 源仓库处于模板模式。

模板模式包含：

- **workflow-version.yaml**：FSHING 工作流版本；
- **workspace.example.yaml**：不含具体项目信息的工作区配置模板；
- **.agents/skills/**：可复用的工作流技能；
- **docs/standards/**：通用管理规范；
- **docs/features/_template/**：需求文档模板；
- **docs/releases/_template/**：发布文档模板。

为了开发或验证 FSHING，本地可以在 **repos/** 下放置项目仓库，但这些目录会被 Git 忽略，也不会成为 FSHING 模板的一部分。

### 初始化模式

从模板创建的项目如果已有 **workspace.yaml**，但项目身份、子仓库声明或 **workspace.lock.yaml** 尚未补全，就处于初始化模式。

该模式只允许配置工作区。所有必需的子仓库完成克隆和校验前，不能创建需求，也不能执行实现、测试和发布流程。

### 本地覆盖模式

FSHING 维护者可以创建 **workspace.yaml** 和 **workspace.lock.yaml**，用于在本地真实仓库上验证工作流。这两个文件必须通过当前克隆的 **.git/info/exclude** 忽略，不能写入仓库跟踪的 **.gitignore**。

本地覆盖数据不能提交或推送到 FSHING。实际产品仍然需要独立的项目控制仓库，用于管理该产品的需求和发布记录。

### 项目模式

满足以下条件后，从 FSHING 创建的仓库进入项目模式：

- **workspace.yaml** 已填写完整的项目身份和项目控制仓库地址；
- 至少声明了一个信息完整的必需子仓库；
- 每个必需子仓库都已完成克隆；
- **workspace.lock.yaml** 与子仓库的实际分支、提交和工作区状态一致。

每个项目控制仓库必须使用自己的 Git 远程仓库。项目数据不能推送回 FSHING 模板仓库。

## 创建项目

1. 在 GitHub 上通过 **Use this template** 创建新的项目控制仓库。
2. 将 **workspace.example.yaml** 复制为 **workspace.yaml**。
3. 填写项目身份、项目控制仓库地址，以及各子仓库的 ID、路径、远程地址、默认分支和组件 ID。
4. 将每个子仓库克隆到 **repos/** 下声明的路径中。
5. 检查子仓库的实际 Git 状态并创建 **workspace.lock.yaml**。
6. 将工作区配置文件提交到项目控制仓库。
7. 在 **docs/features/** 下创建需求，在 **docs/releases/** 下管理发布记录。

## 简化命令

FSHING 提供七个对外工作流入口：

| 命令 | 用途 |
|---|---|
| /fs-init | 初始化或校验项目工作区 |
| /fs-requirement | 创建需求或修改已有需求 |
| /fs-plan | 将已确认且可规划的需求排入版本并完成规划 |
| /fs-implement | 实现已完成规划的需求 |
| /fs-test | 测试需求并收集验证证据 |
| /fs-review | 评审实现结果和追溯链 |
| /fs-release | 规划或验证产品发布 |

Claude Code 和 Cursor 通过仓库中的命令适配文件使用上面的斜杠命令。

Codex 通过 Skills 共享仓库工作流，不使用自定义斜杠命令。在 Codex 中使用：

~~~text
$fs-init
$fs-requirement
$fs-plan
$fs-implement
$fs-test
$fs-review
$fs-release
~~~

也可以在 Codex 中打开 **/skills**，选择对应的 FSHING 技能。这七个入口技能会调用现有的需求、规划、实现、测试、评审和发布技能。

典型用法：

~~~text
$fs-requirement 创建客户标签管理需求，目标版本为 v1.4.0
$fs-plan FEAT-2026-0001
$fs-implement FEAT-2026-0001
$fs-test FEAT-2026-0001
$fs-review FEAT-2026-0001
$fs-release v1.4.0
~~~

所有 fs 阶段都会主动在对话中提出待确认项、解释影响并给出建议。用户确认后，Agent 必须立即把决定回写到需求及受影响的设计、任务、测试和发布文档；需求流转不依赖 **approved_at** 或单独审批记录。

## 项目目录结构

~~~text
project-control/
├── AGENTS.md
├── .agents/skills/
├── docs/
├── workflow-version.yaml
├── workspace.example.yaml
├── workspace.yaml
├── workspace.lock.yaml
└── repos/
    ├── service-a/   独立 Git 仓库
    ├── web-app/     独立 Git 仓库
    └── worker/      独立 Git 仓库
~~~

父仓库不会跟踪 **repos/*/** 下的文件。涉及多个仓库的工作通过带仓库 ID 的 commit SHA 或 PR 地址记录在任务、验证证据和发布快照中。

## 版本边界

- **workflow-version.yaml** 表示当前安装的 FSHING 工作流版本；
- 产品版本表示实际发布的软件版本；
- Spec 版本表示需求文档的修订版本；
- 子仓库提交表示准确的代码版本；
- 发布目录中的 **repositories.yaml** 表示某个产品版本实际包含的代码。

这些标识相互独立，不能混用。

## 更新 FSHING

更新工作流规范、技能和模板时，应在父仓库中单独提交。修改 **workflow-version.yaml** 前，需要先确认现有项目数据仍符合新版本的兼容性 schema。
