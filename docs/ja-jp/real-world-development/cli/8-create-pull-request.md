---
title: "レッスン 8: 機能の PR を作成してマージする"
description: "フィルター機能、指示、スキル、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルター機能の実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストが 1 つのブランチに保存されています。すべての変更をまとめてレビューし、プル リクエストを開きます。星評価の PR は手動でマージしましたが、今回は **Agent Merge** にプロセスを任せます。

> [!NOTE]
> 通常は機能、指示、スキル、QA エージェントを複数の PR に分けます。このワークショップでは、フィルターと品質ワークフローを 1 つの会話とブランチにまとめ、作業を簡略化しています。

このレッスンでは、次のことを行います。

- Agent Merge と PR のライフサイクルを自動化する方法を学びます。
- 機能全体の変更と検証の根拠を確認します。
- フィルター機能の PR を作成します。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

フィルター機能の開発を通じて、Copilot で計画、実装、検証を行いました。Tailspin Toys は PR の残りの作業を自動化したいと考えていますが、マージの承認は開発者が管理します。

## Agent Merge について

**Agent Merge** は、プル リクエストをマージするために必要な残りの作業を自動化します。有効にすると、Copilot は PR のブロッカーを解消します。たとえば、継続的インテグレーション (CI) のチェック失敗を修正し、レビュー コメントに対応し、必要に応じてリベースします。その後、リポジトリが許可すれば GitHub の自動マージを有効にします。

これまでは自分で **Merge pull request** を選択していました。Agent Merge に任せることもできますが、有効にする前に作業をレビューして、準備ができていることを確認します。

## Agent Merge で PR を管理する

コードの作成が完了したので、変更をレビューし、PR を作成して、残りのプロセスを Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. **Default** を選択して <kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` で Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視し、すべて成功するとマージします。
7. Copilot が「PR #14 was squash-merged successfully」のようなメッセージを表示したことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限不足を回避しません。ブロックされた場合は理由を確認し、リポジトリで許可される範囲でレビュー後に手動でマージします。

## まとめと次のステップ

コード生成、テストと検証、そしてプル リクエストのプロセスなど、開発の複数の部分を自動化しました。このレッスンでは次のことを行いました。

- Agent Merge と PR のライフサイクルを自動化する方法を学びました。
- 機能全体の変更と検証の根拠を確認しました。
- フィルター機能の PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

次は、コンテキスト、モデル、セッション共有、クラウドへの任意の委任に使える[Copilot CLI のスラッシュ コマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI でプル リクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
