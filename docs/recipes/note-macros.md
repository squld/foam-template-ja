# カスタムノートマクロ

この #レシピ を使用すると、カスタムノートマクロを作成できます。

## インストール

**この拡張機能はテンプレートに含まれていません**

VScodeでnote-macrosを検索するか、[note-macros - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=NeelyInnovations.note-macros)にアクセスしてインストールします。

## 使用方法

### コマンドパレットからマクロを実行

`Ctrl+P`またはOSに応じて`Alt+P`を使用し、`Note Macros: Run A Macro`と入力して実行したいマクロを選択します。

### カスタムノートマクロの作成

`settings.json`にマクロを追加することでカスタムマクロを作成できます (Code|File > Preferences > User Settings) 。完全な例は[note-macrosのsettings.json](https://github.com/kneely/note-macros/blob/master/settings.json)で見つけることができます。

例えば:

このマクロは、WeeklyノートディレクトリにWeeklyノートを作成します。

```json
{
  "note-macros": {
    "Weekly": [
      {
        "type": "note",
        "directory": "Weekly",
        "extension": ".md",
        "name": "weekly-note",
        "date": "yyyy-W"
      }
    ]
  }
}
```

フィールドの説明については、[note-macros - フィールドの説明](https://github.com/kneely/note-macros#explanation-of-fields)を参照してください。

### マクロを実行するためのキーバインドの追加

`keybindings.json`にマクロへのバインディングを追加します (Code|File > Preferences > Keyboard Shortcuts) :

```json
{
  "key": "ctrl+cmd+/",
  "command": "note-macros.Weekly"
}
```

## 問題とフィードバック

問題や質問がある場合は、[note-macros](https://github.com/kneely/note-macros) GitHubの[README.md](https://github.com/kneely/note-macros#note-macros)を参照してください。

READMEを参照しても解決しない問題や機能リクエストがある場合は、[issue](https://github.com/kneely/note-macros/issues)を開いてください。


