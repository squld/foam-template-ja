# Janitor

個人の知識グラフをデータベースではなくマークダウンファイルで保存するためには、ノート間の関係を作成し維持するための追加のツールが必要です。

**Foam Janitor** (Andy Matuschakの[note-link-janitor](https://github.com/andymatuschak/note-link-janitor)に触発されて) は、既存のノートをFoamに移行し、時間をかけてFoamの健康を維持するのに役立ちます。

現在、FoamのJanitorは以下を助けます:

- [[link-reference-definitions]]が最新であることを確認します
- すべてのドキュメントに適切にフォーマットされたタイトルがあることを確認します (Markdown Links、Markdown Notes、Foam Gatsby Templateとの互換性に必要です)

将来的には、Janitorは以下を助けることができます:

- [[materialized-backlinks]]の更新
- ノートのリント、フォーマット、構造化
- 参照を最新の状態に保ちながら、ノートの名前を変更し、移動します。

## VS CodeからJanitorを使用する (実験的)

コマンドパレットから"Foam: Run Janitor"コマンドを実行します。

![Foam Janitorデモ](../../assets/images/foam-janitor-demo.gif)

## コマンドラインからJanitorを使用する (実験的)

> ⚠️ Improvements to this documentation are welcome!

Janitorは[NPM](https://www.npmjs.com/)からインストールされ、スタンドアロンのCLIツールとして実行されます:

```sh
> npm install -g foam-cli
> foam janitor path/to/workspace
```

Janitorをgitフックとして各コミットで実行し、ワークスペースのリンクが最新であることを確認することができます。これは、他のアプリからマークダウンドキュメントを編集する場合に特に役立ちます。

GitHubアクションからJanitorを実行して、ワークスペースに来るすべての変更が最新であることを確認することもできます。これは、モバイルからFoamノートを編集する場合 (例: [GitJournal](https://gitjournal.io)経由) 、またはFoamに複数の貢献者がいて、すべての変更が正しく統合されていることを確認したい場合に便利です。



