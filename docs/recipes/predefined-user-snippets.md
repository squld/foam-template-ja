# 事前定義されたユーザースニペット

この #レシピ を使用すると、[VS Codeスニペット](https://code.visualstudio.com/docs/editor/userdefinedsnippets)を使用してFoamにRoamスタイルのコマンドを導入できます。以下のスニペットを考えてみてください:

```json
{
  "Zettelkasten Id": {
    "scope": "markdown",
    "prefix": "/id",
    "description": "Zettelkasten Id",
    "body": [
      "${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE} ${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}"
    ]
  },
  "Current date": {
    "scope": "markdown",
    "prefix": "/date",
    "description": "現在の日付",
    "body": [
      "${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE} ${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}"
    ]
  }
}
```

これは以下のようになります:
![ユーザースニペットを示すGIF](../../assets/images/snippets.gif)

スニペットを使用することで、Foamユーザーは自分自身で[[custom-snippets]]を追加できるため、ファーストクラスの`/commands`と並んで存在します。

## ノートと考慮事項

- VS Codeは既にコマンドパレットを介して"コマンド"を提供しています
  - これに関するUXを考慮してください。VS Codeにあまり慣れていないユーザーは、コマンドメニューをトリガーするために`/`を使用することにより慣れている可能性が高いです。経験豊富なVS Codeユーザーは、コマンドパレットを好むかもしれません。
- `TabCompletionProvider`と`snippets`を混ぜることができます (多分) 以下のVS Code設定を通じて: `"editor.snippetSuggestions": "inline" | "top" | "bottom" | "none"`
- 詳細な議論については、[こちら](https://github.com/foambubble/foam/pull/192)のPRを参照してください。

## Markdown構文の簡素化

一部のmarkdown構文は、以前にmarkdownを作成したことがないユーザーにとって難しい場合があります。例えば、チェックボックス/TODOです。以下の構文が必要です:

```
- [ ] 何かのtodo...
```

以下のGIFのように、関連するmarkdown構文に展開されるスニペットを提供することができます:
![markdownスニペットを示すGIF](../../assets/images/markdown-snippets.gif)

これらのスニペットのJSONは[こちら](https://github.com/foambubble/foam/pull/192#issuecomment-666736270)で見つけることができます。



