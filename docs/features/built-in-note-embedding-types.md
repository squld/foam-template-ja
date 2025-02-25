# ノート埋め込みタイプ

ノートを埋め込む際には、コンテンツの範囲や表示スタイルを変更するいくつかの方法があります。以下は、ノート埋め込みを記述するために使用されるFoamのキーワードです。

注意: これはノートの埋め込みにのみ適用され、添付ファイルや画像の埋め込みには適用されません。

![ノート埋め込みタイプ GIF](../../assets/images/note-embed-type-demo.gif)

## 範囲

- `full` - `![[note]]`の場合はノート全体、`![[note#section1]]`の場合はセクション全体
- `content` - セクションのタイトルを除くすべて。つまり、`![[note]]`の場合はタイトルを除くノート全体、または`![[note#section1]]`の場合はセクションヘッダーを除くセクション全体

## スタイル

- `card` - 埋め込まれたノートに枠線を追加
- `inline` - テキストが呼び出しノートの一部であるかのように、ノートを連続して追加

## デフォルト設定

Foamはノート表示タイプを`<範囲>-<スタイル>`として表現します。

デフォルトでは、Foamはノート埋め込みを`full-card`に設定しています。つまり、標準的な埋め込み構文`![[note]]`が使用された場合、ノートは`full`範囲と`card`スタイル表示になります。この設定は`foam.preview.embedNoteStyle`の下に保存されており、変更することができます。

## 明示的な修飾子

デフォルト設定を上書きしたい場合は、スコープまたはスタイルのキーワードのいずれか、またはその両方をwikilinkの前に追加して、ノート埋め込みを明示的に変更します。

例えば、`foam.embedNoteStyle`が`content-card`に設定されている場合、標準構文`![[note-a]]`で埋め込まれたノートは、タイトルを除く枠線付きのノートとして表示されます。特定の`note-b`のタイトルを表示したい場合は、上記のキーワードのいずれかを使用してデフォルト設定を単純に上書きすることができます: `full![[note-b]]`。この場合、`full`はデフォルトの`content`範囲を上書きし、スタイルが指定されていないため、デフォルトのスタイル設定`card`にフォールバックします。インラインにしたい場合は、それも上書きします: `full-inline![[note-b]]`。

