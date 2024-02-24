# リンク参照定義

`[[wikilinks]]`を使用すると、[foam-vscode](https://github.com/foambubble/foam/tree/master/packages/foam-vscode)拡張機能はファイルの末尾に[Markdownリンク参照定義](https://spec.commonmark.org/0.29/#link-reference-definitions)を自動的に生成することができます。これはfoam-vscodeでワークスペースをナビゲートするために必要ではありませんが、`[[wikilinks]]`をサポートしていないさまざまなMarkdownツール (例: パーサー、静的サイトジェネレーター、VS codeプラグインなど) との互換性を保つために役立ちます。

## 例

以下の例:

  ```md
  - [[wikilinks]]
  - [[github-pages]]
  ```

...はファイルの末尾に以下のリンク参照定義を生成します:

  ```md
  [wikilinks]: wikilinks "Wikilinks"
  [github-pages]: github-pages "GitHub Pages"
  ```

このファイルの末尾にあるそれらを見るために、[raw markdown](https://foambubble.github.io/foam/features/link-reference-definitions.md)を開くことができます。
このファイルの末尾にあるそれらを見るために、[raw markdown](https://foambubble.github.io/foam/user/features/link-reference-definitions.md)を開くことができます。

## 仕様

リンク参照定義の3つのコンポーネントは`[link-label]: link-target "Link Title"`です。

- **リンクラベル:** 周囲のmarkdownドキュメントで一致するリンクテキスト。これは二重括弧`[[wikilink]]`表記の内側の括弧に一致します。
- **リンク先** 一致したリンクのターゲット
  - デフォルトでは拡張子なしでリンクを生成します。これは下記の[設定](#設定)で上書きできます。
- **"リンクタイトル"** リンクのオプショナルなタイトル (Foamテンプレートには、ウェブサイトの実行時にこれを置き換えるJavaScriptのスニペットがあります)

## 設定

ファイル拡張子を含むか含まないか、またはリンク参照定義の生成を完全に無効にするかを選択できます。一般的なルールとしては:

- ファイル拡張子を含むリンクは、GitHubウェブUIなどの標準的なmarkdownベースのツールとの互換性が高くなります。
- ファイル拡張子を含まないリンクは、リンクをリテラルURLとして扱い、自動的に変換しない特定のウェブ公開ツールとの互換性が高くなります。例えば、標準のGitHubページのインストールなどです。

デフォルトでは、Foamはレガシーな理由から拡張子なしでリンクを生成しますが、将来のバージョンではこれが変更される可能性があります。

Foamワークスペースの`settings.json`でこの設定を上書きできます:

- `"foam.edit.linkReferenceDefinitions": "withoutExtensions"` (デフォルト)
- `"foam.edit.linkReferenceDefinitions": "withExtensions"`
- `"foam.edit.linkReferenceDefinitions": "off"`

### ファイルの無視

場合によっては、特定のファイルやフォルダを無視して、Foamがそれらへのリンク参照定義を生成しないようにしたいことがあります。

Foamプロジェクトからファイルを除外するための3つのオプションがあります:

1. `files.exclude` (VSCodeから) は、フォルダがファイルエクスプローラに表示されないようにします。

    > "ファイルやフォルダを除外するためのglobパターンを設定します。例えば、ファイルエクスプローラはこの設定に基づいて、どのファイルやフォルダを表示または非表示にするかを決定します。検索固有の除外を定義するには、検索: 除外設定を参照してください。"

2. `files.watcherExclude` (VSCodeから) は、VSCodeがファイルの変更を常に監視するのを防ぎます。

    > "ファイル監視から除外するパスまたはglobパターンを設定します。相対パス (例: `build/output` や `*.js`) や基本的なglobパターンは、現在開いているワークスペースを使用して絶対パスに解決されます。複雑なglobパターンは、適切に一致させるために絶対パスに一致する必要があります (例: `**/build/output/**` や `/Users/name/workspaces/project/build/output/**`) 。ファイルウォッチャープロセスが多くのCPUを消費している場合は、ビルド出力フォルダなどの関心の低い大きなフォルダを除外することを確認してください。"

3. `foam.files.ignore` (Foamから) は、ファイルがFoamグラフに追加されるのを無視します。

    > "Foamによって無視されるglobのリストを指定します (例: グラフの作成時に考慮されません) 。特定のフォルダのすべてのコンテンツを無視するには、`<folderName>/**/*` を使用します" (VSCodeを再読み込みする必要があります) 。

例えば、[Jekyll](https://jekyllrb.com/)のローカルインスタンスを使用している場合、`.md`ファイルのコピーを`_site`ディレクトリに書き込むことがあります。これにより、Foamが元のソースノートではなく、これらのファイルへの参照を生成する原因となることがあります。

`_site`ディレクトリを無視するには、`.vscode/settings.json`ファイルに以下の設定のいずれかを追加します:

```json
  "files.exclude": {
    "**/_site": true
  },
  "files.watcherExclude": {
    "**/_site": true
  },
  "foam.files.ignore": [
    "_site/**/*"
  ]
```

ワークスペースで設定を変更した後、[[workspace-janitor]]コマンドを実行して、既存の定義をすべて変換できます。

現在の問題と潜在的な解決策についてのさらなる議論については、[[link-reference-definition-improvements]]を参照してください。



