# Markdownでのダイアグラム

Markdownコンテンツにダイアグラムを表示するための2つの代替 #レシピ があります:

- [Markdownでのダイアグラム](#markdownでのダイアグラム)
  - [Mermaid](#mermaid)
  - [Draw.io](#drawio)
    - [Draw.ioの使用](#drawioの使用)

## Mermaid

[Mermaid](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)プラグインを使用して、コンテンツ内でダイアグラムを描画し、プレビューすることができます。

## Draw.io

[Draw.io](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)拡張機能を使用すると、Visual Studio Codeを離れることなくダイアグラムを作成、編集、表示できます。`.drawio.svg`または`.drawio.png`ファイルは、エクスポートする必要なく、公開されたFoamに自動的に埋め込まれ、表示されます。ちなみに、以下のダイアグラムはDraw.ioを使用して作成されました! ダイアグラムは[こちら](../../assets/images/diagram-drawio-demo.drawio.svg)で確認できます。

![diagram-drawio-demo](../../assets/images/diagram-drawio-demo.drawio.svg)

### Draw.ioの使用

1. [Draw.io](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) VS Code拡張機能をインストールします。
2. 新しい`*.drawio.svg`または`*.drawio.png`ファイルを作成します。
3. ダイアグラムを描画します。完了したら、保存します。
4. 画像ファイルを埋め込むように、ダイアグラムファイルを埋め込みます。例: `![My Diagram](my-diagram.drawio.svg)`


