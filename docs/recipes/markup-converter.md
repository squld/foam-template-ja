# マークアップコンバーター

この #レシピ では、任意のドキュメントをマークダウンに変換し、ノートに保存する方法を紹介します。

[Pandoc](https://pandoc.org/)、人気のあるユニバーサルドキュメントコンバーターを使用します。Microsoft Word、HTML、LaTeXなどのドキュメントをマークダウンを含む様々な形式に変換できます。

## 使用方法

Microsoft WordドキュメントをMarkdownに変換する例を通して説明します。Pandocの使用方法の詳細については、[Pandocのドキュメント](https://pandoc.org/MANUAL.html)を参照してください。

1. [Pandocをインストールする](https://pandoc.org/installing.html)
1. お好みのターミナルを開き、`pandoc --version`を実行してPandocがインストールされていることを確認する
1. 変換したいMicrosoft Wordドキュメントを新しいフォルダにコピーする
1. Microsoft Wordドキュメントが含まれているフォルダに現在のディレクトリを変更する
1. 次のコマンドのいずれかをコピーしてターミナルに貼り付け、`Enter`を押して実行する (お使いのオペレーティングシステムに基づく)

### LinuxとmacOS (Bash)

```bash
find -name "*.docx" -type f -exec sh -c '
      for f; do
         pandoc --extract-media=./ -f docx -t markdown -o "${f%.*}.md" "$f"
      done
   ' find-sh {} +
```

### Windows (PowerShell)

```powershell
Get-ChildItem . -Filter *.docx |
Foreach-Object {
    pandoc --extract-media=./ --from docx --to markdown $_ -o $_.Name.Replace('.docx', '.md')
}
```

### 関連する設定

[Pandoc](https://pandoc.org/)は、変換プロセスを制御するためのさまざまなコマンドライン引数を受け入れます。ここでは、上記の例に関連するいくつかを紹介します。

- `--extract-media=./`は、Microsoft Wordドキュメントから画像を抽出し、`media`というサブフォルダに保存するために使用されます
- `-t markdown`は、Microsoft Wordドキュメントを[PandocのMarkdown](https://pandoc.org/MANUAL.html#pandocs-markdown)に変換します。[GitHub Flavored Markdown](https://docs.github.com/ja/get-started/writing-on-github)に変換するには、`-t gfm`を使用することもできます

変換されたMarkdownファイルを確認し、変換が成功したことを確認することをお勧めします。その後、元のMicrosoft Wordドキュメントを削除することを検討してください。


