---
title: "第 2 课：添加星级评分，完成第一个小改进"
description: "使用 Copilot CLI 修改游戏卡片，在转发的浏览器中审查更改，并将其合并到第一个拉取请求中。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

安装 Copilot CLI 并尝试过一次对话后，现在可以开始修改项目了。先从一个小改动开始：游戏数据中已有星级评分，但主页上的游戏卡片尚未显示它。你将请智能体显示评分、审查更改，并将其合并到第一个拉取请求中。

本课将完成以下任务：

- 在功能分支中开始一次有明确目标的 Copilot 对话。
- 请智能体对项目进行小幅修改。
- 使用 `/diff` 审查更改。
- 运行应用，并在转发的浏览器中确认更改。
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都可以有星级评分，而且游戏详情页已经显示了评分。不过，主页上的游戏卡片只显示标题、类别、发行商和简介。作为热身练习，你将请智能体在每张卡片上显示已有评分。这项改动范围小、独立性强，非常适合作为第一次会话的任务。

## 对话的组成

**对话**是你使用 Copilot CLI 处理任务的工作空间。与 Copilot 应用不同，普通 CLI 对话使用终端当前检出的仓库和 Git 分支，而不会创建专用工作树。保存对话后可以稍后返回同一讨论；文件和分支仍是磁盘上的常规 Git 状态。

对话中包含三类内容：你的提示和智能体的回复；智能体探索并编辑文件时的工具活动；以及可通过 `/diff` 检查的更改。

## 开始对话并请求修改

开始一个新对话，以便实现这项功能。

1. 返回 Codespace。
2. 如果终端未打开，请按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
3. 如果 Copilot 尚未启动，请运行以下命令：

   ```bash
   copilot --yolo
   ```

4. 使用斜杠命令 `/new` 开始新会话，然后按 <kbd>Enter</kbd>。
5. 使用以下提示请求修改：

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot 会探索项目，找到用于显示游戏详情的文件，并创建所需代码。你已经使用 Copilot CLI 添加了一项功能！

## 审查 diff

所有 AI 生成的更改都应在合并前审查，即使是小改动也不例外。现在就在 Copilot CLI 中查看这些更改。

1. 输入 `/diff` 并检查每个已更改的文件。
2. 确认存在评分时，游戏卡片会显示数值；当 `starRating` 为 `null` 时，会显示 `No rating yet`。
3. 确认测试覆盖了这两种情况。
4. 查看 Copilot 运行的检查结果，并要求它修复任何失败项。
5. 完成审查后，按 <kbd>Esc</kbd> 退出 diff 视图。

> [!NOTE]
> Copilot 与所有生成式 AI 工具一样，具有概率性而非确定性，因此生成的代码可能各不相同。请审查实际行为，而不是期待某种固定实现。

## 检查更改

不要只阅读代码并假设它能正常工作。请 Copilot 启动网站，然后在 Codespaces 转发的浏览器中检查更新后的界面。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 显示端口 `4321` 可用时，选择 **Open in Browser**。
3. 确认游戏卡片显示五分制评分。
4. 返回 Copilot，并请它停止刚才启动的服务器：

   ```plaintext
   Stop the development server you started.
   ```

## 创建并合并第一个拉取请求

功能已经完成！现在创建拉取请求，将代码合并到项目中。

1. 请默认智能体提交更改：

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. 输入 `/pr create`。创建 PR 时，Copilot CLI 会推送已有提交并显示 PR URL。
3. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择 Copilot CLI 显示的 URL，以打开 PR。
4. 审查已更改的文件和检查结果。
5. 准备就绪后，选择 **Merge pull request**，然后确认合并。
6. 返回 Codespace，并使用 `/exit` 退出 Copilot CLI。
7. 更新本地 `main`：

   ```bash
   git checkout main
   git pull
   ```

## 总结与后续步骤

恭喜！你已使用 GitHub Copilot CLI 发布了第一个更改。具体来说，你：

- 在功能分支中开始了一次有明确目标的 Copilot 对话；
- 指示智能体修改游戏卡片；
- 使用 `/diff` 审查更改；
- 运行应用，并在转发的浏览器中确认星级评分；
- 创建并合并了第一个拉取请求。

接下来，你将[从筛选 issue 开始，并使用 Plan 和 Autopilot 模式][next-lesson]构建更大的功能。

## 资源

- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
