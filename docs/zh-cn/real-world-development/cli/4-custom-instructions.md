---
title: "第 4 课：使用自定义指令引导 Copilot"
description: "探索仓库指令，添加文档标准，并将其应用于筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，就要将相关指导提供给 Copilot。[指令文件][instruction-files]不仅说明你想要什么代码，也说明代码应如何组织。现在你已经实现了筛选功能，接下来将了解 Copilot 使用的指令、添加文档标准，并将其应用于代码。

本课将完成以下任务：

- 了解仓库指令和路径特定指令如何传递给智能体。
- 更新指令文件，确保遵循代码标准。
- 观察指令文件对代码的影响。

## 场景

Tailspin Toys 制定了开发实践指南，包括：

- 注释应说明意图和不明显的设计决策，而不是重复代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值；如果存在可注入的 `db` 参数，也应予以说明。
- 可复用的 Astro 组件应记录 `Props` 契约；相关代码更改时，注释也应同步更新。
- 保留现有格式和 lint 指南。

使用指令文件可以确保 Copilot 获取正确的信息，按照这些实践完成任务。

## 指令文件

自定义指令可提供上下文和偏好，帮助 Copilot 更好地理解你的开发风格和要求。你可以指定代码规范、库，以及希望包含的注释。指令可以适用于整个仓库，也可以针对特定文件类型。

指令文件分为两类：

- `.github/copilot-instructions.md`：在仓库的**每个**请求中都会发送给 Copilot 的单个文件，应包含项目级别的通用指导。
- `.github/instructions/*.instructions.md`：针对特定语言、文件类型或任务提供指南的文件。

> [!NOTE]
> 其他指令格式的支持情况因环境而异。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

## 探索项目中的自定义指令文件

入门项目已包含一组指令文件。先探索这些文件，再进行修改，以了解它们的作用。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而非终端）中打开 `.github/copilot-instructions.md`。
3. 阅读项目简介和代码指南。这些指令适用于你在此仓库中与 Copilot 进行的所有交互。
4. 探索 `.github/instructions` 文件夹中的文件，包括 Astro、Drizzle 和测试相关指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`，查看 `applyTo` 字段。glob 用于确定指令适用的文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看指向其他指令文件和现有项目文件的链接。

> [!NOTE]
> 项目指令记录了开发标准，但尚未要求 TypeScript 代码使用 TSDoc 注释。接下来将添加这项要求。

## 探索项目中的自定义指令文件

入门项目已包含一个 `copilot-instructions.md` 文件，以及多个针对不同任务的 `*.instructions.md` 文件。修改前先探索这些文件。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而非终端）中打开 `.github/copilot-instructions.md`。
3. 阅读项目简介和指南。这些指令适用于你在此仓库中与 Copilot 进行的所有交互。
4. 探索 `.github/instructions` 文件夹中的文件，其中包含 Astro、Drizzle 数据层、测试等方面的指南。
5. 打开 `.github/instructions/unit-tests.instructions.md`，查看 `applyTo` 字段。glob 用于确定指令适用的文件；此处适用于 TypeScript 测试文件，例如匹配 `**/*.test.ts` 的文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看其指向其他指令文件（例如 `unit-tests.instructions.md`）和项目文件的链接。这样可以将较长的指令拆分为可复用的小文件，并为 Copilot 提供示例。

> [!NOTE]
> 在 IDE 中，指令文件用于通过 Copilot Chat 生成代码，不用于代码补全或下一步编辑建议。Copilot Chat、Copilot CLI 和 Copilot 云智能体都会使用仓库指令，以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。Copilot 还支持 AGENTS.md 和 CLAUDE.md 等其他格式。

## 更新指令以符合团队标准

入门项目中的指令是很好的起点，但还缺少一条规则。更新 `.github/copilot-instructions.md`，要求新编写的 TypeScript 包含 TSDoc 注释。

1. 打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting guidance** 部分，通常位于第 35 行附近。
3. 在该部分末尾添加以下项目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 应用更新后的指令

Copilot CLI 会在对话开始时加载仓库指令。退出并恢复筛选对话，即可让 Copilot 使用新指令，同时保留功能上下文。

1. 如果筛选对话仍处于打开状态，请输入 `/exit`。Copilot CLI 会自动保存对话。
2. 在仓库根目录的 `game-filters-cli` 分支上恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统要求选择对话，请选择筛选对话，并确认当前检出的是 `game-filters-cli` 分支。
3. 请 Copilot 应用更新后的指南：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff` 并检查更改过的 TypeScript 文件。确认新的 TSDoc 注释准确说明了代码。

## 总结与后续步骤

你了解了 Copilot 如何使用仓库指令，并应用了新标准。本课中，你：

- 了解了仓库指令和路径特定指令如何传递给智能体；
- 更新指令以确保遵循代码标准；
- 观察了指令文件对代码的影响。

接下来，你将自定义并运行可复用的 `quality-checks` 技能，以一致地执行 lint 和测试。

## 资源

- [向 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot：指令文件和其他资源集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
