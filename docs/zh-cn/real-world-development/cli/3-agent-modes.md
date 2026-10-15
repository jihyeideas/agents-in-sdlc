---
title: "第 3 课：智能体模式：Plan 和 Autopilot"
description: "使用 Plan 确定实施方案，使用 Autopilot 根据 issue 构建筛选功能，并在 Interactive 模式下审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们先为项目添加了一项小功能。较大的更改则需要更完善的流程。GitHub Copilot CLI 能够融入组织现有的工作流程，帮助我们用正确的方式构建正确的功能。在接下来的课程中，你将遵循典型的智能体驱动开发流程：从 issue 开始开发新功能，确认代码有效、功能符合预期，最后将其合并到项目中。

> [!NOTE]
> 完成功能工作流时，你将继续使用同一对话和分支。通常，不同类型的文件会分别使用不同分支或 PR；本教程会简化流程，让你专注于核心概念。

本课将完成以下任务：

- 从 GitHub issue 开始新的 Copilot 对话。
- 在 Plan 模式下定义要求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续开发此功能时，你将更新仓库指令、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体，并创建功能 PR。

## 场景

Tailspin Toys 的目录不断扩大，访客需要按类别和发行商筛选游戏。待办 issue 描述了这项功能，但在开始编码之前，仍需就组合多个类别等细节达成一致。你将使用 Plan 模式确定这些决策，然后授权 Autopilot 在限定范围内实现功能。

## 背景

将 AI 编码智能体加入开发流程，并不会改变基本原则。事实上，这些原则变得更加重要！大多数开发者遵循的流程大致如下：

1. 从描述待完成工作的 issue 开始。
2. 制定要构建内容的计划。
3. 编写并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求（PR）。
7. 代码经过审查且持续集成检查通过后，合并代码。

> [!NOTE]
> 具体流程会因团队和组织而异，但大多数流程都与上述过程类似。

坚持这种标准做法，可以确保 AI 生成的代码满足要求，并经过与手写代码相同的验证流程。

## 对话模式

**对话模式**用于控制智能体的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协作。智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先制定计划，但不能编辑项目文件。
- **Autopilot**：智能体自主工作，编写代码、运行测试并反复迭代，直到完成任务。

先使用 Plan 模式，审查计划，然后再使用 Autopilot 实施。

## 从 issue 开始

开始筛选功能前，请返回 Codespace，并确认仓库和终端已准备就绪。

1. 返回 Codespace。如果 Codespace 已停止，请先重启。
2. 确认星级评分 PR 已合并。
3. 如果终端未打开，请按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为筛选工作创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有 issue。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的 issue。
9. 按 <kbd>C</kbd> 将 issue 添加到提示中，然后返回 **Session** 选项卡。

请注意，提示现在以 `#7`（或类似编号）开头。`#` 可将 GitHub issue 或拉取请求（PR）添加到上下文中。

## 规划筛选功能

规划可让你在委托 Copilot 实施功能或执行任务之前，先确定采用的方法。处理复杂任务时，花些时间规划通常很有帮助。现在切换到 Plan 模式，并请 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式。确认提示下方的模式指示器显示 **Plan**。
2. 在上一步添加的 issue 引用后输入以下提示：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 将开始制定计划！它会先探索项目，然后确定最佳方案。

3. 在此过程中，Copilot 可能会询问筛选功能应如何工作。根据你的偏好回答即可，没有错误答案。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动以审查计划。
6. 如果计划的某些部分不符合你的决定，请让 Copilot 修改。

## 批准 Autopilot

计划编写并审查完毕后，就可以开始实施了！使用 Autopilot 让 Copilot 执行任务。

Autopilot 会让 Copilot 持续迭代，直到它认为问题已解决。

1. 选择 **Accept plan and build on autopilot (recommended)**，或所安装版本中名称相似的选项。
2. 确认提示下方的模式指示器显示 **Autopilot**。
3. 观察 Copilot 如何遵循既定计划、生成代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实施，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再将检查视为已完成。

## 审查并验证实现

代码生成后，和其他代码一样，必须在合并前审查。现在一起审查代码并运行网站，确认一切正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff` 并检查筛选功能的实现和测试。
3. 将结果与 issue 以及规划时做出的决定进行比较。
4. 审查完代码后，按 <kbd>Esc</kbd> 退出 diff 视图。
5. 查看项目检查结果，并请 Copilot 解决任何失败项。

## 探索新功能

代码看起来不错，但它真的能运行吗？像之前一样启动应用，并通过 Codespaces 转发的端口打开网站。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 显示端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别和发行商筛选，并测试计划中商定的组合。
4. 确认重置和无结果时的行为符合 issue 以及你的决定。
5. 返回 Codespace，并请 Copilot 停止它启动的开发服务器。

## 总结与后续步骤

你使用不同的对话模式构建并审查了功能。本课中，你：

- 从 GitHub issue 开始了新的 Copilot 对话；
- 在 Plan 模式下定义了要求；
- 使用 Autopilot 模式实现了新功能；
- 审查了代码；
- 在转发的浏览器中手动验证了功能。

接下来，你将[使用自定义指令][next-lesson]进一步了解代码生成方式，并确保代码遵循已记录的实践。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
