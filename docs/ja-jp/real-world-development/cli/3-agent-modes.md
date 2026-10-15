---
title: "レッスン 3: エージェント モード: Plan と Autopilot"
description: "Plan で方針を合意し、Autopilot で issue からフィルター機能を実装し、Interactive で結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

プロジェクトに小さな機能を追加しました。より大きな変更には、さらに堅牢なプロセスが必要です。GitHub Copilot CLI は組織の既存のフローに沿って動作するため、正しい方法で適切なものを作成できます。これから数回のレッスンでは、一般的なエージェント主導の開発プロセスに取り組みます。issue から新しい機能を作成し、コードが有効で機能が期待どおりに動作することを確認して、最後にプロジェクトにマージします。

> [!NOTE]
> 機能の作業を続ける間は、同じ会話とブランチを使います。通常はファイルの種類ごとに異なるブランチや PR を使いますが、このワークショップでは基本的な概念に集中するために簡略化します。

このレッスンでは、次のことを行います。

- GitHub issue から Copilot との新しい会話を開始します。
- Plan モードで要件を定義します。
- Autopilot モードで新しい機能を実装します。
- コードをレビューします。
- ポート転送されたブラウザーで機能を手動検証します。

この機能の作業を続けながら、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP 検証を追加し、QA エージェントを作成して、機能の PR を開きます。

## シナリオ

Tailspin Toys のカタログが拡大し、訪問者はカテゴリと発行元でゲームを絞り込む必要があります。バックログの issue には機能が記載されていますが、カテゴリを組み合わせる方法など、実装前に合意すべき詳細があります。Plan モードで決定事項を整理し、Autopilot に範囲を限定した実装を許可します。

## 背景

AI コーディング エージェントを開発フローに加えても、基本は変わりません。むしろ重要になります。多くの開発者は次のようなフローに従います。

1. 作業内容を説明する issue から始めます。
2. 実装する内容を計画します。
3. コードを作成してレビューします。
4. テストを実行してコードを検証します。
5. 新しい機能を手動で検証します。
6. プル リクエスト (PR) を作成します。
7. コードがレビューされ、継続的インテグレーションのチェックに合格したら、コードをマージします。

> [!NOTE]
> 正確な手順はチームや組織によって異なりますが、多くは上記の流れに沿っています。

この標準的なアプローチに従うことで、AI が生成したコードが要件を満たし、手作業で書いたコードと同じ検証プロセスを経ることを確認できます。

## 会話モード

**会話モード**は、エージェントの自律性のレベルを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押してモードを切り替えます。

- **Interactive**: エージェントと協力して作業します。エージェントは変更を提案し、続行前に入力を待ちます。
- **Plan**: エージェントが計画を作成しますが、プロジェクト ファイルを編集できません。
- **Autopilot**: エージェントが自律的にコードを書き、テストを実行して、タスクが完了するまで反復します。

Plan モードで開始し、計画をレビューしてから、Autopilot で実装します。

## issue から開始する

フィルター機能に取り組む前に Codespace に戻り、リポジトリとターミナルの準備ができていることを確認します。

1. Codespace に戻ります。停止している場合は再起動してから続けます。
2. 星評価の PR がマージされていることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、フィルター機能用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの issue を選択します。
9. <kbd>C</kbd> を押して issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトが `#7` (または同様の番号) で始まることを確認します。`#` を使うと、GitHub の issue やプル リクエスト (PR) をコンテキストに追加できます。

## フィルター機能を計画する

計画を立てると、機能の実装やタスクの実行を Copilot に任せる前に、方針を決められます。複雑な作業は少し時間をかけて計画するのがお勧めです。Plan モードに切り替えて、Copilot に計画を作成するよう依頼しましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプトの下にあるモード表示が **Plan** であることを確認します。
2. 前の手順で追加した issue の参照の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot が計画の作成を開始します。まずプロジェクトを調べ、次に最適な方法を決定します。

3. フィルター機能の動作について Copilot から質問されることがあります。希望に基づいて回答してください。どの回答も間違いではありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開します。
5. 上下にスクロールして計画をレビューします。
6. 決定内容と一致しない部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を作成してレビューしたので、実装を始めます。Autopilot を使って Copilot に作業を任せましょう。

Autopilot を使うと、Copilot は完了と判断するまで問題に取り組み、反復できます。

1. **Accept plan and build on autopilot (recommended)**、またはインストールしたバージョンの同様のオプションを選択します。
2. プロンプトの下のモード表示が **Autopilot** になっていることを確認します。
3. Copilot が合意した計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認するとすぐに実装が始まる場合があるため、先に計画をレビューしてください。依存関係が見つからない、またはポートが競合していると Copilot が報告した場合は、チェック完了とみなす前にセットアップの問題を解決します。

## 実装をレビューして検証する

コードが生成されたら、他のコードと同じようにマージ前にレビューします。コードを確認し、サイトを実行してすべてが正しく動作することを確かめましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。モード表示に **Plan** または **Autopilot** が表示されないことを確認します。
2. `/diff` を入力し、フィルター機能の実装とテストを確認します。
3. 結果を issue および計画中に決めた内容と比較します。
4. コードのレビューが終わったら、<kbd>Esc</kbd> を押して diff ビューを終了します。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に解決を依頼します。

## 新しい機能を試す

コードはよさそうですが、実際に動作するでしょうか。前と同じようにアプリを起動し、Codespaces の転送ポートを通じてサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が使用可能になったら、**Open in Browser** を選択します。
3. カテゴリ、発行元、および計画で合意した組み合わせを使ってフィルターを試します。
4. リセットと該当なしの動作が issue および決定内容と一致することを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

異なる会話モードを使って機能を作成し、レビューしました。このレッスンでは次のことを行いました。

- GitHub issue から Copilot との新しい会話を開始しました。
- Plan モードで要件を定義しました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- ポート転送されたブラウザーで機能を手動検証しました。

次は、コード生成の仕組みと、文書化されたプラクティスに沿わせる方法について、[カスタム指示][next-lesson]を使ってさらに詳しく学びます。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
