---
title: "レッスン 10: まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプル リクエスト、再利用可能なカスタマイズ、関連リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連のワークフローで GitHub Copilot CLI を使用しました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールしてプロジェクトを調べ、フィルターの issue を見つけました。
- 星評価を追加し、ポート転送されたブラウザーで結果を確認して、最初のプル リクエスト (PR) を手動でマージしました。
- フィルターの issue から始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニット テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルター機能を確認しました。
- 品質保証 (QA) カスタム エージェントを作成して選択し、要件、カバレッジ、スキルの結果、ブラウザーの根拠を評価しました。
- フィルター機能のすべての変更をレビューし、その PR で Agent Merge を許可しました。
- コンテキスト、モデル、共有、クラウドへの任意の委任に使うスラッシュ コマンドを確認しました。

## 公開した内容

ワークショップには、更新済みの `main` から作成した別々のブランチで進める PR のマイルストーンが 2 つあります。

1. **星評価:** 既存の `starRating` と、未評価であることを示す表示をゲーム カードに追加します。
2. **フィルターと品質ワークフロー:** フィルターを実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルを作成して、関連するテストを追加します。

フィルターの計画から PR の作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、この作業を 1 つの PR にまとめました。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP を使った Copilot のブラウザー操作という複数の方法でコードを検証しました。`quality-checks` スキルはユニット テスト、lint、型チェックを実行し、新しい形式で結果を報告しました。QA はその結果に要件とテスト カバレッジのレビューを加えてから PR に進みました。

追加するテストは実際の不足を補うものにします。新しいテストが不要という QA の結果も正しい場合があります。マージを許可する前にコードと根拠をレビューし、変更後は影響を受けた検証結果を更新します。

## ベスト プラクティス

Copilot の作業は、提供するコンテキストとツールによって変わります。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを構成しました。これらをほかの会話でも再利用し、チームのニーズに合わせて調整します。指示は標準を設定し、スキルは繰り返し可能なタスクを説明し、カスタム エージェントは専門ロールを定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。実装前に方針を考えるには **Plan**、範囲の明確な変更で作業に参加するには **Interactive**、明確に範囲を定めたタスクには **Autopilot** を使います。定型的な編集には高速なモデル、複雑な問題には高性能なモデルを選びます。

コンテキストはインフラストラクチャと同じくらい重要です。作りたいもの、その理由、方法を明確に説明すると結果が大きく変わります。

## さらに試す

基本的なワークフローを学びました。ほかにも次の CLI 機能があります。

- `/review`: コード レビュー エージェントに変更を分析させます。
- `/rubber-duck`: 問題について話し合い、別の視点を得ます。
- `/fleet`: 独立したサブタスクを並行して調整します。
- `/worktree`: 別のタスクを分離します。
- `/delegate`: Copilot cloud agent にタスクを送信します。

## 次のステップ

どのツールも、使い続けることが上達への近道です。運用コード、趣味のプロジェクト、何年も作りたいと思っていた小さなアプリなどで活用してください。チームに学びを共有し、ほかの人の経験からも学びましょう。そして、ドキュメントも確認してください。

ターミナルから Tailspin Toys を拡張する場合は、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot アプリのワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプル リクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
