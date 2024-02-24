# Wikilinks

Wikilinksは、知識ベース内のファイルを接続する内部リンクです。 (`[[MediaWiki]]`リンクとも呼ばれます) 。

## Wikilinksの作成とナビゲーション

Wikilinkを作成するには、`[[`と入力し、リポジトリ内の別のノートの名前を入力し始めます。目的のノートが選択されたら、`tab`キーを押して自動補完します。例: [[graph-visualization]]。

`Cmd` + `Click` (Windowsでは`Ctrl` + `Click`) でwikilinkをナビゲートします (カーソルがwikilink上にある間は`F12`も機能します) 。ファイルが存在しない場合は、デフォルトの[[note-templates]]設定に基づいてワークスペースに作成されます。

## プレースホルダー

[[placeholder]]のように、ターゲットファイルがないwikilinkも作成できます。<!--NOTE: このプレースホルダーリンクには関連ファイルが存在しません。これは概念を示すためです-->
プレースホルダーは、ターゲットファイルがないwikilinkで、プレースホルダーへのリンクは異なるスタイルで表示されるため、簡単に区別できます。
それでも、接続を強調するのに役立ちます。

`Foam: Show Graph`コマンドでグラフを開き、プレースホルダーノードを見てください。

`CTRL/CMD+click`でwikilinkをナビゲートしたり、プレースホルダーのリンクであれば (ファイルが存在しない場合) 作成することを覚えておいてください。

## セクションのサポート

Foamは、ノートセクションの自動補完、ナビゲーション、埋め込み、診断をサポートしています。標準のwiki構文`[[resource#Section Title]]`を使用してください。
- 外部ファイルの場合は、`[your link will need the filename](other-file.md#that-section-I-want-to-link-to)`が必要ですが、
- 同じドキュメント内のアンカーの場合は、`[you just need an octothorpe and the section name](#that-section-above)`だけです。
- アンカーがどの見出しレベルであっても、`H1`のような`# MEN WALK ON MOON`や`H2`のような`## Astronauts Land on Plain`にリンクする場合、リンク構文は単一のオクトーソープを使用します: `[Walk!](#men-walk-on-moon)`や`[Land!](#astronauts-land-on-plain-collect-rocks-plant-flag)`。ここでも自動補完が役立ちます。

## Markdownの互換性

[VSCode用Foam](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode)拡張機能は、他のMarkdownツールやパーサーとwikilinksが互換性を持つように、ファイルの下部に[[link-reference-definitions]]を自動生成します。

## 続きを読む

- [[foam-file-format]]
- [[note-templates]]
- 現在の問題と潜在的な解決策についてのさらなる議論については、[[link-reference-definition-improvements]]を参照してください。



