---
title: "第 9 课：Copilot CLI 斜杠命令"
description: "探索用于管理上下文、选择模型、共享会话以及可选委派给云智能体的斜杠命令。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

与其他优秀的 CLI 工具一样，GitHub Copilot CLI 提供了许多斜杠命令，可用于访问高级功能、后台信息和其他配置选项。你已经使用过 `/diff`、`/mcp`、`/skills`、`/agent` 和 `/pr` 等命令。现在来了解其他实用命令。

本课将完成以下任务：

- 使用 `/context` 和 `/compact` 了解 Copilot 如何管理上下文。
- 使用 `/model` 查看可用模型。
- 了解 `/share` 如何导出或共享会话。
- 探索用于并行工作、工作树和可选云智能体委派的命令。

## 场景

你已完成 CLI 的核心工作流。现在将了解其他功能：管理上下文、切换模型、共享会话，以及可选地委派给 [Copilot 云智能体][about-cloud-agent]。

## 探索 Copilot CLI 上下文

处理较大或较复杂的任务时，可能会接近模型的上下文窗口上限。Copilot CLI 会在需要时自动压缩对话；你也可以使用斜杠命令自行检查或压缩上下文。

1. 返回 Codespace。如果 Copilot CLI 尚未打开，请从仓库根目录启动。
2. 输入：

   ```plaintext
   /context
   ```

3. 查看模型、当前 token 用量，以及上下文在系统指令、工具、消息和剩余空间之间的分配情况。
4. 压缩对话：

   ```plaintext
   /compact
   ```

5. 再次输入 `/context` 并比较结果。如果对话本来就很短，变化可能不大。

> [!NOTE]
> 上下文窗口即将填满时，Copilot CLI 会自动压缩上下文。使用 `/compact` 可自行选择压缩时间。切换到无关任务并希望开始全新对话时，使用 `/clear` 或 `/new`。

## 选择模型

不同模型各有所长，开发者也有各自的偏好。Copilot CLI 允许你查看并选择所需模型。

1. 输入：

   ```plaintext
   /model
   ```

2. 查看可用模型和用量信息。
3. 保留当前模型、选择其他模型，或按 <kbd>Esc</kbd> 关闭列表。

## 共享会话

团队成员之间共享经验有助于改进 AI 工具的使用方式。`/share` 命令可以将会话导出为 Markdown 或 HTML 文件、创建共享链接，或发布 GitHub gist。

1. 输入 `/help` 并查看已安装版本中的 `/share` 选项。
2. 如果要共享会话，请选择合适的目标，例如使用 `/share file` 导出本地 Markdown 文件。
3. 发送或发布导出内容前先进行审查。会话导出内容可能包含提示、回复和项目详情。

发布链接或 gist 是可选操作。不要公开团队无意分享的仓库或对话内容。

## 可选：扩展工作或委派任务

本教程的核心工作流已经完成。Copilot CLI 还提供了适用于较大任务的命令：

- `/fleet` 可将互相独立的子任务分配给多个子智能体并行执行。
- `/worktree` 可为另一个任务创建隔离的 Git 工作树。
- `/delegate` 可将任务发送给 Copilot 云智能体；它会异步工作，并可能创建拉取请求。

这些命令可能创建额外工作树或启动远程工作，因此属于可选功能。请先开始一个新的、范围明确的任务，并通过常规工作流审查结果。若要深入了解异步智能体任务，请继续学习[云智能体教程][cloud-workshop]。

## 总结与后续步骤

Copilot CLI 斜杠命令可用于配置工具、共享会话并查看后台状态。本课中，你：

- 使用 `/context` 和 `/compact` 了解了上下文管理；
- 使用 `/model` 查看了可用模型；
- 了解了 `/share` 如何导出或共享会话；
- 探索了用于并行任务、工作树和云智能体委派的可选命令。

Copilot CLI 还有许多其他斜杠命令值得探索！接下来，我们将[回顾所学内容][next-lesson]并了解后续步骤。

## 资源

- [Copilot CLI 命令参考][cli-reference]
- [Copilot CLI 上下文管理][context-management]
- [关于 Copilot 云智能体][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
