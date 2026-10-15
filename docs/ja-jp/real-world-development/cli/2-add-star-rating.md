---
title: "レッスン 2: 最初の変更として星評価を追加する"
description: "Copilot CLI でゲーム カードに小さな変更を加え、転送ブラウザーでレビューして、最初のプル リクエストにマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールして、会話を試しました。次はプロジェクトに最初の変更を加えます。変更は小さくします。ゲームのデータには星評価がすでにありますが、ホーム ページのゲーム カードにはまだ表示されていません。エージェントに表示を依頼し、変更をレビューして、最初のプル リクエストにマージします。

このレッスンでは、次のことを行います。

- 機能ブランチで Copilot との会話を始めます。
- エージェントに小さなプロジェクト変更を依頼します。
- `/diff` で変更をレビューします。
- アプリを実行し、ポート転送されたブラウザーで変更を確認します。
- 最初のプル リクエストを開いてマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価を設定でき、ゲーム詳細ページにはすでに表示されています。一方、ホーム ページのゲーム カードに表示されるのはタイトル、カテゴリ、発行元、説明だけです。最初の練習として、既存の評価を各カードに表示するようエージェントに依頼します。最初のセッションにぴったりの、小さく独立した変更です。

## 会話の仕組み

**会話**は、Copilot CLI でタスクに取り組む場所です。Copilot アプリとは異なり、通常の CLI 会話では専用のワークツリーを作らず、ターミナルで現在チェックアウトされているリポジトリと Git ブランチを使います。保存した会話を使えば、ファイルとブランチがディスク上の通常の Git 状態のまま、後から同じ話し合いに戻れます。

会話には 3 つの要素があります。プロンプトとエージェントの応答、ファイルの調査や編集に使うツールの動作、そして `/diff` で確認できる変更です。

## 会話を始めて変更を依頼する

新しい会話を始めて、機能の実装に取りかかりましょう。

1. Codespace に戻ります。
2. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
3. Copilot がまだ起動していない場合は、次のコマンドで起動します。

   ```bash
   copilot --yolo
   ```

4. スラッシュ コマンド `/new` を使い、<kbd>Enter</kbd> を押して新しいセッションを開始します。
5. 次のプロンプトで変更を依頼します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot がプロジェクトを調べ、ゲームの詳細を表示するファイルを見つけて、必要なコードを作成します。これで Copilot CLI を使って新しい機能を追加できました。

## diff をレビューする

小さな変更でも、AI が生成した変更はマージする前にすべてレビューします。ここで Copilot CLI の変更を確認しましょう。

1. `/diff` を入力し、変更されたすべてのファイルを確認します。
2. 評価がある場合はカードに数値が表示され、`starRating` が `null` の場合は `No rating yet` と表示されることを確認します。
3. どちらの状態もテストされていることを確認します。
4. Copilot が実行したチェック結果を確認し、失敗があれば修正を依頼します。
5. レビューが終わったら、<kbd>Esc</kbd> を押して diff 画面を閉じます。

> [!NOTE]
> Copilot は他の生成 AI ツールと同様、確率的に動作し、結果は毎回同じとは限りません。特定の実装を期待するのではなく、動作をレビューしてください。

## 変更を確認する

コードを読むだけで動作すると判断するのではなく、Copilot にサイトを起動してもらい、Codespaces の転送ブラウザーで更新された UI を確認します。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が使用可能になったら、**Open in Browser** を選択します。
3. 各ゲーム カードに 5 段階の評価が表示されることを確認します。
4. Copilot に戻り、起動したサーバーの停止を依頼します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプル リクエストを開いてマージする

機能を作成できました。次はプル リクエストを作成し、プロジェクトにコードをマージします。

1. 既定のエージェントに変更のコミットを依頼します。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI は PR の作成時に既存のコミットをプッシュし、PR の URL を表示します。
3. Copilot CLI が表示した URL を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して PR を開きます。
4. 変更されたファイルとチェック結果をレビューします。
5. 準備ができたら **Merge pull request** を選択し、マージを確定します。
6. Codespace に戻り、`/exit` で Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

おめでとうございます。GitHub Copilot CLI を使って最初の変更をリリースしました。次の作業を行いました。

- 機能ブランチで Copilot との会話を始めました。
- ゲーム カードに小さな変更を加えるようエージェントに依頼しました。
- `/diff` で変更をレビューしました。
- アプリを実行し、ポート転送されたブラウザーで星評価を確認しました。
- 最初のプル リクエストを開いてマージしました。

次は[フィルターの issue から始め、Plan モードと Autopilot モードを使って][next-lesson]、より大きな機能を作成します。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
