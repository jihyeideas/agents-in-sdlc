---
title: "レッスン 4: カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、フィルター機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときはコンテキストが重要です。タスクの進め方に指定がある場合は、そのガイダンスを Copilot に提供します。[指示ファイル][instruction-files]では、作成したいコードだけでなく、コードの構成方法も説明できます。フィルター機能を作成したので、Copilot が使った指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、次のことを行います。

- リポジトリの指示とパス固有の指示がエージェントに届く方法を確認します。
- コーディング標準を適用するために指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には、開発プラクティスに関するガイドラインがあります。たとえば、次のとおりです。

- コメントではコードを繰り返さず、意図や自明でない決定を説明します。
- `db/` と `src/lib/` のエクスポート関数は、目的、パラメーター、戻り値を TSDoc/JSDoc で記述します。該当する場合は、注入可能な `db` 引数も説明します。
- 再利用可能な Astro コンポーネントは `Props` の契約を記述し、関連コードの変更時にはコメントも更新します。
- 既存のフォーマットと lint のガイダンスを維持します。

指示ファイルを使って、Copilot がこれらのプラクティスに沿うための情報を提供します。

## 指示ファイル

カスタム指示を使うと、コンテキストや好みを Copilot に伝え、開発スタイルや要件を理解しやすくできます。コーディング規約、ライブラリ、コードに含めるコメントを指定できます。リポジトリ全体、または特定のファイルの種類を対象に指示を作成できます。

指示ファイルには 2 種類あります。

- `.github/copilot-instructions.md`: リポジトリの**すべて**のリクエストで Copilot に送信される単一のファイルです。プロジェクト全般に関する情報を記述します。
- `.github/instructions/*.instructions.md`: 特定の言語、ファイルの種類、タスクに関するガイドラインを記述するファイルです。

> [!NOTE]
> その他の指示形式のサポートは環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポートに関するリファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示を確認する

スターター プロジェクトには、いくつかの指示ファイルが含まれています。変更する前に内容を確認しましょう。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの概要とコーディング ガイダンスを確認します。この指示は、リポジトリでの Copilot とのすべてのやり取りに適用されます。
4. `.github/instructions` フォルダーを調べ、Astro、Drizzle、テストなどの指示ファイルを確認します。
5. `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` フィールドを確認します。glob によって指示が適用されるファイルが決まります。
6. `.github/instructions/drizzle.instructions.md` を開き、他の指示ファイルやプロジェクト内の既存ファイルへのリンクを確認します。

> [!NOTE]
> プロジェクトの指示には開発標準が記載されていますが、TypeScript の TSDoc コメントはまだ必須ではありません。次の手順で追加します。

## このプロジェクトのカスタム指示を確認する

スターター プロジェクトには `copilot-instructions.md` と、タスクごとの複数の `*.instructions.md` ファイルが含まれています。変更する前に内容を確認しましょう。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの概要とガイダンスを確認します。この指示は、リポジトリでの Copilot とのすべてのやり取りに適用されます。
4. `.github/instructions` フォルダーを調べます。Astro、Drizzle のデータ レイヤー、テストなどの指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` フィールドを確認します。glob によって適用対象のファイルが決まります。ここでは、`**/*.test.ts` などの TypeScript テスト ファイルが対象です。
6. `.github/instructions/drizzle.instructions.md` を開き、`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内のファイルへのリンクを確認します。長い指示を再利用可能な小さなファイルに分け、Copilot に参考例を示せます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat でコードを生成するときに使われ、コード補完や次の編集候補には使われません。Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリの指示と `applyTo` frontmatter を含む `*.instructions.md` の両方を使います。AGENTS.md や CLAUDE.md など、ほかの形式もサポートされています。

## チームの標準に合わせて指示を更新する

スターターに含まれる指示には、TypeScript の新しいコードに TSDoc コメントを求めるルールがありません。`.github/copilot-instructions.md` を更新しましょう。

1. `.github/copilot-instructions.md` を開きます。
2. 35 行目付近にある **Code formatting guidance** セクションを探します。
3. 最後の箇条書きとして、次を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。フィルター機能のコンテキストを維持したまま新しい指示を使うため、会話を終了して再開します。

1. フィルターの会話がまだ開いている場合は `/exit` を入力します。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートで `game-filters-cli` ブランチにいることを確認し、保存した会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められた場合はフィルターの会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. 更新したガイダンスを適用するよう Copilot に依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力して変更された TypeScript ファイルを確認します。新しい TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot がリポジトリの指示を使う方法を確認し、新しい標準を適用しました。このレッスンでは、次のことを行いました。

- リポジトリの指示とパス固有の指示がエージェントに届く方法を確認しました。
- コーディング標準を適用するよう指示を更新しました。
- 指示ファイルがコードに与える影響を確認しました。

次は、再利用可能な `quality-checks` スキルをカスタマイズして実行し、lint とテストを一貫して実施します。

## リソース

- [Copilot CLI にカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示作成のベスト プラクティス][instructions-best-practices]
- [Awesome Copilot: 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
