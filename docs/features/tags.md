---
tags: my-tag1 my-tag2 my-tag3/notes
---

# タグ

メモにタグを追加して、カテゴリ分けしたり、メモ同士をリンクさせたりすることができます。

## タグの作成

タグを作成する方法は2つあります:

- メモのテキストのどこかに `#tag` を追加することで、例えば: #my-tag1
- `tags: tag1, tag2` のyamlフロントマターを使用すること。このドキュメントにはこの方法で `my-tag1` と `my-tag2` タグが追加されています。

タグは階層構造を持つこともできるので、`#parent/child` のように #my-tag3/info のようなタグを持つことができます。

### タグの補完

`#` 文字を入力すると、VS Codeの"Intellisense"が起動します。この機能は、入力された文字に一致する可能なタグのリストを表示します。フロントマターで編集している場合は、`tags:` 行で `#` 文字を入力するか、["trigger suggest"](https://code.visualstudio.com/docs/editor/intellisense) キーバインド (通常は `ctrl+space`) を使用してタグ補完を呼び出すことができます。フロントマターで `#` を使用した場合、タグが挿入されるときに `#` は削除されます。

## *Tag Explorer* の使用

Tag Explorerパネルを通じてタグをナビゲートすることができます。左サイドバーでTag Explorerビューを展開すると、現在のFoam環境で見つかったすべてのタグがリストされます。その後、タグの各レベルを展開すると、タグで検索するオプションと、特定のタグを含むすべてのファイルのリストが表示されます。

タグはFoam Graph Explorerでも視覚化することができます。タグを表すノードの色を変更する方法を含む詳細については、[[graph-visualization]]を参照してください。

## タグのスタイリング

FoamノートをレンダリングするMarkdownプレビューパネルでタグの見た目をカスタマイズすることができます。これにはCSS言語の知識が必要です。CSSはVSCodeなどのウェブ技術のスタイルをカスタマイズするために使用されます。CSSの簡単な紹介は[こちら](https://www.freecodecamp.org/news/get-started-with-css-in-5-minutes-e0804813fc3e/)で見つけることができます。

1. Foamプロジェクト内にCSSファイルを作成します。例えば、`.foam/css/custom-tag-style.css` または [.vscode/custom-tag-style.css](../../.vscode/custom-tag-style.css) にします。
2. `.foam-tag` クラスを対象とするCSSコードを追加します。
3. タグに適用したい各[CSSプロパティ](https://www.w3schools.com/cssref/index.php)に対するルールを追加します。
4. `.vscode/settings.json` ファイルを開くか (または `ctrl+,` で設定ブラウザを開きます) 。
5. 新しいスタイルシートのパスを `markdown.styles` 設定に追加します。

> 注: スタイルシートのファイルパスは、ワークスペースで現在開いているフォルダに対して相対的になります。ユーザーの設定を変更する場合、ファイルパスはグローバルな[VSCode設定](https://code.visualstudio.com/docs/getstarted/settings)に対して相対的になります。

最終的な結果は、以下の内容に似たCSSファイルになります。これで、ノートプレビューでタグを目立たせることができます。

```css
.foam-tag{
  color:#ffffff;
  background-color: #000000;
}
```

![カスタムタグスタイルデモ](../../assets/images/custom-tag-style.png)

## タグの代わりにバックリンクを使用する

バックリンクの力を考えると、タグとして使用することを好む人もいます。
例えば、本に関するノートを [[book]] でタグ付けすることができます。

[note-properties|note property]: note-properties.md "ノートのプロパティ"
[graph-visualization]: graph-visualization.md "グラフの可視化"



