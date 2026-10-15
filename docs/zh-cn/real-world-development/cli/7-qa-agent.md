---
title: "第 7 课：创建并使用 QA 智能体"
description: "创建 QA 自定义智能体，将 issue 要求、quality-checks 技能和 Playwright MCP 结合起来。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并使用 Playwright MCP 在浏览器中查看筛选体验。现在，你将把这些能力整合到一个具有明确 QA 流程的自定义智能体中。

本课将完成以下任务：

- 探索自定义智能体如何配合指令、技能和 MCP 工具工作。
- 创建并检查可复用的质量保证配置文件。
- 选择 QA 智能体，并根据筛选 issue 审查其发现。

## 场景

创建拉取请求（PR）前，Tailspin Toys 希望一致地审查要求、代码质量、自动检查、测试覆盖率和浏览器行为。自定义智能体可以协调 QA 流程并生成可复用的报告。

## 什么是自定义智能体？

自定义智能体是在 Markdown 配置文件中定义的 Copilot 专用版本。配置文件描述智能体的用途、指令和可用工具。本教程将使用 `.github/agents/qa.agent.md` 定义 QA 角色，并在 Copilot CLI 中选择它。

你之前使用的自定义功能各有不同用途：仓库指令描述团队标准；`quality-checks` 技能封装可重复执行的检查；Playwright MCP 提供浏览器工具；QA 配置文件则告诉 Copilot 如何结合这些能力评估要求并报告结果。它不会取代其他自定义功能，也不需要另开对话。

## 创建 QA 配置文件

创建功能 PR 前，请 Copilot 创建可复用的 QA 配置文件。配置文件将定义 QA 要执行的检查以及必须遵循的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 请默认智能体创建自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置文件

使用智能体前，先审查配置文件，确认 Copilot 记录了预期的 QA 工作流和限制。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 是可选项，但可为智能体设置显示名称。
3. 确认指令要求 QA 从需求出发、遵循仓库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据，将每项要求报告为通过、失败或受阻，在更改实现代码前征求许可，并且不会提交更改或创建拉取请求。
5. 如果职责或边界有所遗漏，请默认智能体在继续之前修改配置文件。

## 根据 issue 运行 QA

Copilot CLI 会在对话开始时加载项目智能体。创建配置文件后，恢复同一筛选对话并选择 QA，使其能够使用 issue 和规划决策。

1. 使用以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 智能体刚刚创建，可能尚未显示在可用智能体列表中。仍可通过上述命令将其激活。

2. 请 QA 智能体审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 智能体将开始工作。
4. 完成后阅读它提供的报告。

## 总结与后续步骤

你添加了可复用的专用角色，并审查了它的工作。本课中，你：

- 探索了自定义智能体如何使用指令、技能和 MCP 工具；
- 创建并检查了可复用的质量保证配置文件；
- 选择 QA 智能体，并根据 issue 审查了它的发现。

实现、技能更新、QA 配置文件、测试和验证报告现已准备就绪。接下来，你将[把它们汇总到功能 PR 中，并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
