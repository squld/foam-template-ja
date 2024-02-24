# Vercelへの公開

この #レシピ では、デフォルトのFoamウェブサイトテンプレートをVercelにデプロイする方法を示します。

[Vercel](https://vercel.com/)は、GitHubページ ([[publish-to-github-pages]]を参照) と同様の静的ウェブサイトホスティングソリューションです。

## プロジェクトの設定

### Foamのテンプレートを使用する

デフォルトの[Foamテンプレート](https://github.com/squld/foam-template-ja)を使用してGitHubリポジトリを生成します。これがVercelでデプロイするワークスペースになります。このワークスペースはベアボーンのJekyllソースウェブサイトであり、他のJekyllウェブサイトと同様にプラグインをカスタマイズしてインストールできます。

GitHubページを使用しないため、Vercelがサイトのビルド方法を把握するためにいくつかの設定ファイルを追加する必要があります。

### `_config.yml`の追加

まず、ルートディレクトリに`_config.yml`を追加する必要があります。これはJekyllの設定ファイルです。ここでは、サイトのタイトル、テーマ、リポジトリ、パーマリンクオプションを設定し、Jekyllに使用するプラグインを指示します:

```yaml
# _config.yml
title: Foam
# GitHubページを使用しないためにインストールするすべてのプラグイン
plugins:
  - jekyll-katex  # オプション
  - jekyll-default-layout
  - jekyll-relative-links
  - jekyll-readme-index
  - jekyll-titles-from-headings
  - jekyll-optional-front-matter
# 使用するデフォルトのJekyllテーマ
theme: jekyll-theme-primer
# FoamワークスペースをホストしているGitHubリポジトリ
repository: user/repo
# https://jekyllrb.com/docs/permalinks/#built-in-formats で指定された形式でパーマリンクを生成
permalink: pretty
```

`theme`は、デプロイされたJekyllウェブサイトのテーマを指定します。デフォルトのGitHubページテンプレートは[Primer](https://github.com/pages-themes/primer)と呼ばれます。htmlレイアウトとテンプレートのカスタマイズ方法については、Primerのドキュメントを参照してください。[Jekyll Themes](https://jekyllthemes.io/)などの場所からテーマを選択することもできます。

`plugins`は、GitHubページを使用しないため、GitHubページが内部でインストールしてくれるこれらのプラグインをインストールする必要があるJekyllプラグインのリストを指定します。

_KaTeXを使用してLaTeXをレンダリングしたい場合 (`jekyll-katex`プラグインが行うこと) 、ここで指定できます。Vercelでデプロイする利点の1つは、KaTeXを使用してLaTeXをレンダリングできることです! 詳細は: [[math-support-with-katex]]_

### `Gemfile`の追加

次に、ルートディレクトリに`Gemfile`という新しいファイルを作成します。これにより、Vercelがウェブサイトをビルドする際にインストールするプラグインを知らせます。

`Gemfile`では、Rubyパッケージを指定する必要があります:

```ruby
# Gemfile
source "https://rubygems.org"
gem "jekyll"
gem "kramdown-parser-gfm"
gem "jekyll-theme-primer"
gem "jekyll-optional-front-matter"
gem "jekyll-default-layout"
gem "jekyll-relative-links"
gem "jekyll-readme-index"
gem "jekyll-titles-from-headings"
gem "jekyll-katex"  # オプション、KaTeX数式レンダリングを有効にするパッケージ
```

### KaTeXを使用した数式レンダリングの有効化 (オプション)

`_config.yml`と`Gemfile`にプラグイン`jekyll-katex`を追加するだけでなく、[[math-support-with-katex]]のガイドに従って、サイトがKaTeXを使用して数式をレンダリングすることを完全にサポートする必要があります。

### GitHubリポジトリへの変更のコミット

最後に、新しく作成されたファイルをGitHubにコミットします。

## Vercelへのプロジェクトのインポート

まず、[Vercelの _Import Git Repository_](https://vercel.com/import/git)を使用して、Foamワークスペース (GitHubリポジトリ) をVercelにインポートします。GitHubリポジトリのURLを貼り付けると、Vercelは自動的にプルして分析し、ウェブサイトをデプロイするために使用するツールを認識します。 (この場合はJekyllです。)

次に、プロンプトが表示された場合はデプロイするフォルダを選択します。デフォルトテンプレートを使用している場合、VercelはFoamワークスペースのルートディレクトリをデフォルトとします。

最後に、すべてが成功した場合、Vercelは検出されたフレームワーク: Jekyllを表示します。`Deploy`を押してプロジェクトの公開を進めます。

![](../../assets/images/vercel-detect-preset.png)

これで、VercelはプッシュするたびにFoamワークスペースのビルドとレンダリングを行います。Vercelはサイトを`xxx.vercel.app`に公開し、Vercelウェブサイトのカスタムドメイン名も定義できます。



