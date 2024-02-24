# GitHub Gistでノートを書く

この #レシピ を使用すると、GitHubリポジトリにノートを永続化し、手動でコミット/プッシュ/プルする必要なく変更を自動的に同期できる場合、GistPadが検討する価値のあるオプションかもしれません。

[GistPad](https://aka.ms/gistpad)は、何もローカルにクローンすることなく、GitHubのgistとリポジトリを編集できるVisual Studio Code拡張機能です。

`[[link]]` [completion/navigation](https://github.com/vsls-contrib/gistpad#links)、[daily pages](https://github.com/vsls-contrib/gistpad#daily-pages)、[pasting images](https://github.com/vsls-contrib/gistpad#pasting-images-1)、[backlinks](https://github.com/vsls-contrib/gistpad#backlinks)を完備したFoamワークスペースの編集をサポートしています。

<img width="700px" src="https://user-images.githubusercontent.com/116461/87234714-96ba9400-c388-11ea-92c3-544d9a3bb633.png" />

## 始め方

GistPadをFoamベースのナレッジベースで使用するには、以下の手順を実行してください:

1. [GistPad拡張機能](https://aka.ms/gistpad)をダウンロードし、Visual Studio Codeを再起動します。

1. `GistPad: Sign In`コマンドを実行し、GitHubアカウントを使用して認証フローを完了します。

1. `GistPad: Open Repository`コマンドを実行し、`Create repo from template...`または`Create private repo from template...`を選択します。好みに応じて選択してください。

1. `Foam-style wiki`テンプレートを選択し、Foamワークスペースに名前を指定します (例: `my-foam-notes`, `johns-knowledge-base`) 。

新しいリポジトリがGitHubアカウントに作成され、`Foam`のウェルカムページが自動的に開かれます。既にGitHubにFoamワークスペースがある場合は、上記の手順#3で、GitHubリポジトリの名前を選択または指定してください。

> 注意: GistPadをFoamワークフローに合わせて改善するためのフィードバックがあれば、遠慮なく[お知らせください](https://github.com/vsls-contrib/gistpad)!👍

<img width="700px" src="https://user-images.githubusercontent.com/116461/87863222-c1b76180-c90d-11ea-87d9-04bee1c58a0d.png" />

## ワークスペースの管理

Foamリポジトリを開いたり作成したりすると、`GistPad`タブ (小さなノートブックアイコンが付いたもの) の`Repositories`ビューに表示されます。このツリービューから、新しいページを追加/編集/削除/名前変更したり、ローカルファイルをアップロードしたり、各ページのバックリンクを表示したりすることができます (ページの子ノートとして表示されます) 。

<img width="250px" src="https://user-images.githubusercontent.com/116461/87234704-83a7c400-c388-11ea-90a8-2a660bef4dc5.png" />

## ワークスペースの編集

ページを作成または開くと、通常どおりマークダウンコンテンツを編集したり、[画像を貼り付けたり](https://github.com/vsls-contrib/gistpad#pasting-images-1)、他のページへの[`[[links]]`を作成したりすることができます。`[[`と入力すると、ワークスペース内の既存のページの自動補完が表示され、リンクを作成することで新しいページを自動的に作成することもできます。

Visual Studio Codeのマークダウンエディターを使用しているので、豊富な言語サービス (例: 構文ハイライト、ヘッダーの折りたたみ) や拡張機能エコシステム (例: [Emojisense](https://marketplace.visualstudio.com/items?itemName=bierner.emojisense)) の恩恵を受けることができます。

## ワークスペースのナビゲーション

ファイルを編集しているときに、`[[links]]`をホバーして内容のプレビューを表示したり、`cmd+click`して該当するページにジャンプしたりすることが簡単にできます。さらに、ページへのリンクを追加すると、そのページに[バックリンク](https://github.com/vsls-contrib/gistpad#backlinks)が自動的に追加されます。

ページのバックリンクを表示するには、以下のいずれかの方法を使用できます:

1. `Repositories`ツリーでファイルのノードを展開すると、子ノードがバックリンクを表すため、ページとそのバックリンクを1つの階層ビューで簡単に閲覧できます。

1. ファイルを開いて、エディタービューの下部にあるバックリンクリストを表示します。これにより、ページを読んでから、コンテキストに富んだ方法でバックリンクを確認できます。

## 日次ページ

任意のページを作成するだけでなく、GistPadを使用して日記をつけたり、[日次ノート](https://github.com/vsls-contrib/gistpad#daily-pages)をキャプチャしたりすることもできます。`Repositories`ツリーでカレンダーアイコンをクリックすると、今日を表すページが開きます。ページがまだ存在しない場合は、ワークスペースに作成されてから開かれます。

<img width="700px" src="https://user-images.githubusercontent.com/116461/87234721-b356cc00-c388-11ea-946a-e7f9c92258a6.png" />


