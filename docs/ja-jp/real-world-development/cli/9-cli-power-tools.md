---
title: "レッスン 9: Copilot CLI のスラッシュ コマンド"
description: "スラッシュ コマンドでコンテキストやモデルを管理し、セッションを共有して、必要に応じてクラウド エージェントにタスクを委任します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

他の優れた CLI ツールと同様、GitHub Copilot CLI には多くのスラッシュ コマンドがあります。高度な機能、内部情報、追加の構成オプションを利用できます。すでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` などを使いました。ほかの便利なコマンドも確認しましょう。

このレッスンでは、次のことを行います。

- `/context` と `/compact` を使って Copilot のコンテキスト管理を確認します。
- `/model` を使って使用可能なモデルを調べます。
- `/share` でセッションをエクスポートまたは共有する方法を学びます。
- 並列作業、ワークツリー、クラウド エージェントへの委任に使う任意のコマンドを確認します。

## シナリオ

CLI の基本的なワークフローを完了しました。次は、コンテキスト管理、モデルの切り替え、セッション共有、[Copilot cloud agent][about-cloud-agent]への任意の委任など、その他の機能を確認します。

## Copilot CLI のコンテキストを確認する

大規模または複雑なタスクでは、モデルのコンテキスト ウィンドウの上限に近づくことがあります。Copilot CLI は必要に応じて会話を自動的に圧縮しますが、スラッシュ コマンドを使って自分で確認したり圧縮したりできます。

1. Codespace に戻ります。Copilot CLI が開いていない場合は、リポジトリのルートから起動します。
2. 次を入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム指示、ツール、メッセージ、空き領域へのコンテキストの分割を確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. もう一度 `/context` を入力し、結果を比較します。会話がすでに短い場合、大きな変化がないことがあります。

> [!NOTE]
> Copilot CLI はコンテキスト ウィンドウが埋まると自動的に圧縮します。`/compact` を使うと圧縮するタイミングを選べます。関係のないタスクに切り替えて新しい会話を始める場合は、`/clear` または `/new` を使います。

## モデルを選択する

モデルによって得意分野は異なり、開発者にもそれぞれ好みがあります。Copilot CLI ではモデル一覧を表示して選択できます。

1. 次を入力します。

   ```plaintext
   /model
   ```

2. 使用可能なモデルと使用状況の情報を確認します。
3. 現在のモデルを使い続けるか、別のモデルを選択するか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで作業し、学んだことを共有すると、AI ツールをより効果的に使えます。`/share` コマンドでは、セッションを Markdown または HTML ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist を公開したりできます。

1. `/help` を入力し、インストールしたバージョンの `/share` オプションを確認します。
2. 共有する場合は、ローカルの Markdown ファイルに出力する `/share file` など、目的に合った保存先を選びます。
3. 送信または公開する前に、エクスポートされた内容を確認します。プロンプト、応答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は任意です。チームが共有を意図していないリポジトリや会話の内容は公開しないでください。

## 任意: 作業を拡張または委任する

基本的なワークショップは完了しました。Copilot CLI には、より大きなタスクに使えるコマンドもあります。

- `/fleet` は独立したサブタスクをサブエージェントに割り当て、並行して実行できます。
- `/worktree` は別のタスク用に独立した Git ワークツリーを作成できます。
- `/delegate` は Copilot cloud agent にタスクを送信できます。非同期で作業し、プル リクエストを作成する場合があります。

これらのコマンドを使うと、別のワークツリーやリモート作業が発生する可能性があるため、任意です。試す場合は新しい範囲の明確なタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントの作業を詳しく学ぶには、[cloud agent ワークショップ][cloud-workshop]に進みます。

## まとめと次のステップ

Copilot CLI のスラッシュ コマンドを使うと、構成を変更し、セッションを共有し、内部の状態を確認できます。このレッスンでは次のことを行いました。

- `/context` と `/compact` を使ってコンテキスト管理を確認しました。
- `/model` を使って使用可能なモデルを調べました。
- `/share` でセッションをエクスポートまたは共有する方法を学びました。
- 並列作業、ワークツリー、クラウドへの委任に使う任意のコマンドを確認しました。

Copilot CLI にはほかにも多くのスラッシュ コマンドがあります。[学んだ内容を振り返り][next-lesson]、次のステップに進みましょう。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
