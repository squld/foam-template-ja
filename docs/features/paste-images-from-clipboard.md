# クリップボードから画像を貼り付ける

[vscode-paste-image](https://github.com/mushanshitiancai/vscode-paste-image)拡張機能をインストールすることで、`cmd+alt+v`でクリップボードから画像を貼り付けることができます。

画像は自動的に`/attachments`フォルダにコピーされ、貼り付けたファイルに参照が追加されます。

画像の名前を確認するプロンプトが表示されますが、設定で`"pasteImage.showFilePathConfirmInputBox": false,`を設定することで無効にできます。

画像の作成場所を変更するには、`pasteImage.path`プロパティを変更します。例えば:

- `${currentFileDir}`: ファイルの隣に画像を保存します
- `${currentFileDir}/images`: ファイルの隣に`images`ディレクトリを作成し、そこに画像を保存します


