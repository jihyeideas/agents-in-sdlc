---
title: "レッスン 7: QA エージェントを作成して使用する"
description: "issue の要件、quality-checks スキル、Playwright MCP を組み合わせた QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザーからフィルター機能を確認しました。次は、明確な QA プロセスを備えたカスタム エージェントにこれらの機能をまとめます。

このレッスンでは、次のことを行います。

- カスタム エージェントが指示、スキル、MCP ツールを使う方法を確認します。
- 再利用可能な品質保証プロファイルを作成して確認します。
- QA エージェントを選択し、フィルター機能の issue に照らして結果をレビューします。

## シナリオ

プル リクエスト (PR) を開く前に、要件、コード品質、自動チェック、テスト カバレッジ、ブラウザーでの動作を一貫して確認したいと考えています。カスタム エージェントを使うと QA プロセスを調整し、再利用可能なレポートを作成できます。

## カスタム エージェントとは

カスタム エージェントは、Markdown プロファイルで定義する Copilot の特化版です。プロファイルにはエージェントの目的、指示、使用可能なツールを記述します。このワークショップでは、`.github/agents/qa.agent.md` に QA ロールを定義し、Copilot CLI で選択します。

これまで使ったカスタマイズにはそれぞれ異なる役割があります。リポジトリの指示はチーム標準を説明し、`quality-checks` スキルは繰り返し可能なチェックをまとめ、Playwright MCP はブラウザー ツールを提供します。QA プロファイルは、要件を評価して結果を報告するために、これらをどう使うかを Copilot に伝えます。他のカスタマイズを置き換えるものではなく、別の会話も必要ありません。

## QA プロファイルを作成する

機能の PR を開く前に、再利用可能な QA プロファイルを Copilot に作成してもらいます。プロファイルには QA が実行するチェックと守るべき境界を定義します。

1. Codespace に戻り、フィルターの会話が Interactive モードであることを確認します。
2. 既定のエージェントに次のカスタム エージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

新しいエージェントを使う前に、Copilot が意図した QA フローと制限を記述したことを確認します。

1. `/diff` を入力して `.github/agents/qa.agent.md` を開きます。
2. frontmatter を確認します。`description` は必須です。`name` は任意ですが、表示名を指定できます。
3. 要件を起点にし、リポジトリの指示に従い、`quality-checks` スキルを実行し、Playwright MCP を使うよう記述されていることを確認します。
4. QA が根拠とともに結果を報告し、実装コードを変更する前に許可を求め、コミットや PR 作成を行わないことを確認します。
5. 役割や境界が不足していたら、続行前に既定のエージェントへ修正を依頼します。

## issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクトのエージェントを読み込みます。プロファイルを作成した後、同じフィルターの会話を再開して QA を選択すると、issue と計画の決定事項を引き継げます。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 作成直後のため、使用可能なエージェント一覧に表示されない場合があります。上記のコマンドで有効にできます。

2. QA エージェントに機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業を開始します。
4. レポートが完了したら内容を確認します。

## まとめと次のステップ

再利用可能な専門ロールを追加し、その成果をレビューしました。このレッスンでは次のことを行いました。

- カスタム エージェントが指示、スキル、MCP ツールを使う方法を確認しました。
- 再利用可能な QA プロファイルを作成して確認しました。
- QA エージェントを選択し、issue に照らして結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートがそろいました。次は、[機能の PR にまとめて Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
