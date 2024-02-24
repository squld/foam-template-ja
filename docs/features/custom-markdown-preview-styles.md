# カスタムMarkdownプレビュースタイル

Visual Studio Codeでは、Markdownプレビュータブで独自のCSSを使用できます。

## 使用方法

MarkdownプレビューのカスタムCSSは、`settings.json`の`"markdown.styles": []`設定を使用して実装できます。スタイルシートはhttpsのURLまたは現在のワークスペース内のローカルファイルへの相対パスのいずれかにすることができます。

例えば、`Style.css`というスタイルシートを読み込むには、`settings.json`に次の行を追加します:

```
{
  "markdown.styles": ["Style.css"]
}
```

## Foam要素

### Foamノート & プレースホルダーリンク

ノートまたはプレースホルダーへのリンクのカスタムスタイルを設定することができます。リンクは`<a>`タグです。ノートには`foam-note-link`クラスを、プレースホルダーには`foam-placeholder-link`クラスを使用します。

### 循環含有警告

Foamは、他のノートをあなたのノートに含める機能を提供します。これはプレビュータブで表示されます。Foamはノートの循環含有を認識し、検出された場合に警告を表示します。以下のhtmlが使用され、`foam-cyclic-link-warning`クラスを使用してカスタムスタイルを設定できます。

```html
<div class="foam-cyclic-link-warning">
  wikilink: ${wikilink}に対する循環リンクが検出されました
</div>
```


