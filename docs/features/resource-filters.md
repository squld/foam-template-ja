# リソースフィルター

リソースフィルターは、Foamコマンドのスコープを制限するためにいくつかのコマンドに渡すことができます。

フィルターは以下のパラメータをサポートしています:

- `tag`: 指定されたタグを持つリソースを含める (例: `{"tag": "#research"}`)
- `type`: 指定されたタイプのリソースを含める (例: `{"type": "daily-note"}`)
- `path`: そのパスが指定されたregexに一致するリソースを含める (例: `{"path": "/projects/*"}`) 。**このパラメータはregexをサポートしており、globsはサポートしていません。**
- `expression`: 指定された式が`true`になるリソースを含める (例: `{"expression": "resource.type ==='weekly-note'"}`)
- `title`: タイトルが指定されたregexに一致するリソースを含める (例: `{"title": "Team meeting:*"}`)

フィルターはいくつかの論理演算子もサポートしています:

- `and`: すべてのサブパラメータに一致するリソースを含める (例: `{"and": [{"tag": "#research"}, {"title": "Paper *"}]}`)
- `or`: いずれかのサブパラメータに一致するリソースを含める (例: `{"or": [{"tag": "#research"}, {"title": "Paper *"}]}`)
- `not`: ネストされたフィルタの結果を反転させる (例: `{"not": {"type": "daily-note"}}`)

例えば、ワークスペースのサブセットのみのFoamグラフを表示するための複雑なフィルタは以下のようになります:

```
{
  "key": "alt+f",
  "command": "foam-vscode.show-graph",
  "args": {
    "filter": {
      "and": [
        {
          "or": [
            { "type": 'daily-note' },
            { "type": 'weekly-note' },
            { "path": '/projects/*' },
          ],
          "not": {
            { "tag": '#b' },
          },
        },
      ],
    }
  }
}
```


