---
title: "第 8 课：创建并合并功能 PR"
description: "一起审查筛选功能、指令、技能、QA 配置文件和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选功能实现、指令更新、技能自定义、质量保证（QA）配置文件和测试都保存在同一个分支中。现在需要一起审查这些更改并创建拉取请求。你之前手动合并了星级评分 PR；这次将由 **Agent Merge** 管理该流程。

> [!NOTE]
> 通常，我们会把功能、指令更新、技能更新和 QA 智能体分别放入几个 PR。为了简化本教程，我们将筛选功能和质量工作流放在同一对话和分支中，并提交到一个 PR。

本课将完成以下任务：

- 了解 Agent Merge 以及它如何自动管理 PR 生命周期。
- 检查完整的功能更改和验证证据。
- 创建筛选功能 PR。
- 仅在审查后启用 Agent Merge，并确认 PR 已合并。

## 场景

在筛选工作流中，你使用 Copilot 规划、实现并验证了一项功能。Tailspin Toys 现在希望自动处理剩余的 PR 工作，同时由开发者掌控合并授权。

## 了解 Agent Merge

**Agent Merge** 会自动完成合并拉取请求所需的剩余工作。启用后，Copilot 会处理阻碍 PR 合并的问题，例如修复失败的持续集成（CI）检查、回复审查意见，以及在需要时执行 rebase。如果仓库允许，之后会启用 GitHub 自动合并。

此前，你一直自行选择 **Merge pull request**。现在也可以将这项工作交给 Agent Merge，但启用前请先审查并确认更改已准备就绪。

## 使用 Agent Merge 管理 PR

代码完成后，请一起审查更改、创建 PR，并让 Agent Merge 管理后续流程。

1. 返回 Codespace。
2. 输入 `/agent` 打开智能体对话框。
3. 从列表中选择 **Default**，然后按 <kbd>Enter</kbd>。
4. 使用 `/pr create` 命令创建新 PR。
5. 使用 `/pr agentmerge` 启用 Agent Merge。
6. Copilot 会监视 PR 的持续集成流程。所有检查通过后，它会执行合并。
7. 确认 Copilot 显示了类似“PR #14 was squash-merged successfully”的消息。

> [!IMPORTANT]
> Agent Merge 不会绕过必需的审批、分支保护、合并队列、仓库设置或缺失的权限。如果遇到阻塞，请查看原因，并在仓库允许时手动完成经过审查的合并。

## 总结与后续步骤

你已自动化开发流程中的多个环节，包括代码生成、测试和验证，以及拉取请求流程。本课中，你：

- 了解了 Agent Merge 以及它如何自动管理 PR 生命周期；
- 检查了完整的功能更改和验证证据；
- 创建了筛选功能 PR；
- 在审查后启用了 Agent Merge，并确认 PR 已合并。

接下来，你将[探索 Copilot CLI 斜杠命令][next-lesson]，了解如何管理上下文、模型、共享会话以及可选的云智能体委派。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
