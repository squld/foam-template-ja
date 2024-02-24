# Foamコマンド

Foamには"Foam"と入力してコマンドパレットを呼び出すことで探索できるさまざまなコマンドがあります。

特に、いくつかのコマンドは非常にカスタマイズ可能であり、カスタムワークフローやユースケースに役立ちます。

## foam-vscode.create-noteコマンド

このコマンドはノートを作成します。
そのままでも十分に機能しますが、さまざまなユースケースを実現するためにカスタマイズすることができます。
ここに、コマンドのための利用可能な設定があります:

- `notePath`: 作成するノートのパス。相対パスの場合、ワークスペースのルートに対して解決されます。
- `templatePath`: 使用するテンプレートのパス。相対パスの場合、ワークスペースのルートに対して解決されます。
- `title`: ノートのタイトル (つまり、`FOAM_TITLE`変数)
- `text`: ノートに使用するテキスト。テンプレートも提供されている場合、テンプレートが優先されます
- `variables`: テキストまたはテンプレートで使用する変数
- `date`: FOAM*DATE*\*変数を解決するために使用される日付。`YYYY-MM-DD`形式
- `onFileExists?: 'overwrite' | 'open' | 'ask' | 'cancel'`: ターゲットファイルが既に存在する場合の対応

コマンドをカスタマイズしてキーバインドを関連付けるには、キーバインド設定を開いて適切な設定を追加します。ここにいくつかの例があります:

- `test note.md`という名前のノートをいくつかのテキストで作成します。ノートが既に存在する場合は、新しい名前を尋ねます。

```
{
  "key": "alt+f",
  "command": "foam-vscode.create-note",
  "args": {
    "text": "test note ${FOAM_DATE_YEAR}",
    "notePath": "test note.md",
    "onFileExists": "ask"
  }
}
```

- `weekly-note.md`テンプレートに従ってノートを作成します。ノートが既に存在する場合は、それを開きます。

```
{
  "key": "alt+g",
  "command": "foam-vscode.create-note",
  "args": {
    "templatePath": ".foam/templates/weekly-note.md",
    "onFileExists": "open"
  }
}
```

## foam-vscode.open-resourceコマンド

このコマンドはリソースを開きます。

通常、開くリソースを識別する`URI`を受け取ります。

フィルターを渡すことも可能で、ワークスペースのリソースに対して実行され、一致するものを1つ以上見つけます。

- 一致するものが1つの場合、それが開かれます
- 一致するものが複数ある場合、ユーザーが望むリソースを選択できるようにクイックピックが表示されます

例:

```
{
  "key": "alt+f",
  "command": "foam-vscode.open-resource",
  "args": {
    "filter": {
      "title": "Weekly Note*"
    }
  }
}
```


