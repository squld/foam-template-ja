# GitHub Pagesの公開

1. VSCodeのワークスペース設定で`"foam.edit.linkReferenceDefinitions": "withoutExtensions"`を設定してください。
2. コマンドパレットから"Foam: Run Janitor"コマンドを実行してください。
3. [リポジトリの設定で**GitHub Pages**を有効にしてください](https://guides.github.com/features/pages/)。
   - GitHub Pagesのデフォルトテンプレートは[Primer](https://github.com/pages-themes/primer)と呼ばれています。htmlのレイアウトやテンプレートをカスタマイズする方法については、Primerのドキュメントを参照してください。
   - GitHub Pagesは[Jekyll](https://jekyllrb.com/)をベースに構築されているため、パーマリンクやフロントマターのメタデータなどをサポートしています。

## ローカルで公開する方法

公開されたFoamをテストしたい場合は、以下の手順に従ってください:

- <https://docs.github.com/ja/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll>
- <https://docs.github.com/ja/free-pro-team@latest/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll>

ruby/jekyllなどがインストールされていると仮定して:

- `touch Gemfile`
  - ファイルを開いて、以下を貼り付けます:

```
source 'https://rubygems.org'

gem "github-pages", "VERSION"
```

`VERSION`を<https://rubygems.org/gems/github-pages>で最新のものに置き換えます (例: `gem "github-pages", "209"`)

- `bundle`
- `bundle exec jekyll 3.9.0 new .`
- [Creating Your Site](https://docs.github.com/ja/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll#creating-your-site)の指示に従って`Gemfile`を編集します。ポイントn.8
- `bundle exec jekyll serve`

## 他のテンプレート

GitHubページにFoamワークスペースを公開することもサポートしている他の多くのテンプレートがあります

* gatsby-digital-garden
  * [リポジトリ](https://github.com/mathieudutour/gatsby-digital-garden)
  * [デモウェブサイト](https://mathieudutour.github.io/gatsby-digital-garden/)
* foam-mkdocs-template
  * [リポジトリ](https://github.com/Jackiexiao/foam-mkdocs-template)
  * [デモウェブサイト](https://jackiexiao.github.io/foam/)
* foam-jekyll-template
  * [リポジトリ](https://github.com/hikerpig/foam-jekyll-template)
  * [デモウェブサイト](https://hikerpig.github.io/foam-jekyll-template/)

[[todo]] [[good-first-task]] このドキュメントを改善する



