# デイリーノート

デイリーノートを使用すると、毎日の新しいノートファイルをすばやく作成してアクセスできます。これは、ノートを整理し、イベントを管理するための驚くほど効果的で、ますます一般的な戦略です。

`Foam: Open Daily Note` コマンドを実行するか、ショートカット `alt+d` を使用するか、または [#snippets](#スニペット) を使用して、今日のノートファイルを表示します。デイリーノートファイルの名前、場所、およびタイトルは [#configurable](#設定) で設定できます。

## Roamスタイルの自動デイリーノート

`Foam › Open Daily Note: On Startup` 設定を `true` に設定することで、起動時に自動的に今日のノートを開くことができます。

## デイリーノートテンプレート

デイリーノートは、特別な `.foam/templates/daily-note.md` テンプレートを定義することで、[[Note Templates]] を使用することもできます。

## スニペット

[スニペット](https://code.visualstudio.com/docs/editor/userdefinedsnippets) を使用して、最近のデイリーノートへのリンクを作成します。`/today` と入力して `enter` を押すと、今日のノートへのリンクが作成されます。また、以下のように書くこともできます:

| スニペット    | 日付          |
| ------------ | ------------- |
| `/tomorrow`  | 明日          |
| `/yesterday` | 昨日          |
| `/monday`    | 次の月曜日    |
| `/+1d`       | 明日          |
| `/-3d`       | 3日前         |
| `/+1w`       | 1週間後       |
| `/-1m`       | 1ヶ月前       |
| `/+1y`       | 1年後         |

## 設定

デフォルトでは、デイリーノートはワークスペースの `journals` フォルダ内に `yyyy-mm-dd.md` というファイル名で、見出し `yyyy-mm-dd` で作成されます。

これらの設定は、ワークスペースまたはグローバルの `.vscode/settings.json` ファイルで、[**dateformat** 日付マスキング構文](https://github.com/felixge/node-dateformat#mask-options)を使用して上書きすることができます:

デイリーノートのパスと見出しをカスタマイズすることができます。[dateformat マスキング構文](https://github.com/felixge/node-dateformat#mask-options)に従ってください。
以下のプロパティを使用できます:

```json
  "foam.openDailyNote.directory": "journal",
  "foam.openDailyNote.filenameFormat": "'daily-note'-yyyy-mm-dd",
  "foam.openDailyNote.fileExtension": "mdx",
  "foam.openDailyNote.titleFormat": "'Journal Entry, ' dddd, mmmm d",
```

上記の設定では、`journal/daily-note-2020-07-25.mdx` というファイルが作成され、見出しは `Journal Entry, Sunday, July 25` になります。

> 注意: 特別な [[note-properties]] を使用して、日付に基づいてデイリーノートのファイルパスを設定することができます。これは [[Note Templates]] で設定可能です。具体的には [[note-templates#Example of date-based|日付ベースの例]] を参照してください。テンプレートプロパティを使用すると、`.vscode/settings.json` を通じて設定された任意の設定が上書きされます。

## 機能の拡張 (週次、月次、四半期ごとのノート)

[[note-macros]]を参照してください。



