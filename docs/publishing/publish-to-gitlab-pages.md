# GitLab Pages

Foamページを提供するためにGitHubを使用する必要はありません。GitLabも使用できます。

GitLabページは、プライベートリポジトリの場合はプライベートに保つことができるため、メモがプライベートのままになります。

## プロジェクトのセットアップ

### GitHubからディレクトリを生成する

[Foamテンプレート](https://github.com/squld/foam-template-ja)を使用してソリューションを生成します。

リモートをGitLabに変更するか、すべてのファイルを新しいGitLabリポジトリにコピーします

## Gatsbyを使用したページの公開

### Gatsby設定のセットアップ

次のように `.gatsby-config.js` ファイルを追加します:

* `$REPO_NAME` はあなたのgtlabリポジトリの名前に対応します。
* `$USER_NAME` はあなたのgitlabユーザー名に対応します。

```js
const path = require("path");
const pathPrefix = `/$REPO_NAME`;

// 変更してください
const siteMetadata = {
  title: "タイトル",
  shortName: "短い名前",
  description: "",
  imageUrl: "/graph-visualization.jpg",
  siteUrl: "https://$USER_NAME.gitlab.io",
};
module.exports = {
  siteMetadata,
  pathPrefix,
  flags: {
    DEV_SSR: true,
  },
  plugins: [
    `gatsby-plugin-sharp`,
    {
      resolve: "gatsby-theme-primer-wiki",
      options: {
        defaultColorMode: "night",
        icon: "./path_to/logo.png",
        sidebarComponents: ["tag", "category"],
        nav: [
          {
            title: "Github",
            url: "https://github.com/$USER_NAME/",
          },
          {
            title: "Gitlab",
            url: "https://gitlab.com/$USER_NAME/",
          },
        ],
        editUrl:
          "https://gitlab.com/$USER_NAME/$REPO_NAME/tree/main/",
      },
    },
    {
      resolve: "gatsby-source-filesystem",
      options: {
        name: "content",
        path: `${__dirname}`,
        ignore: [`**/\.*/**/*`],
      },
    },

    {
      resolve: "gatsby-plugin-manifest",
      options: {
        name: siteMetadata.title,
        short_name: siteMetadata.shortName,
        start_url: pathPrefix,
        background_color: `#f7f0eb`,
        display: `standalone`,
        icon: path.resolve(__dirname, "./path_to/logo.png"),
      },
    },
    {
      resolve: `gatsby-plugin-sitemap`,
    },
    {
      resolve: "gatsby-plugin-robots-txt",
      options: {
        host: siteMetadata.siteUrl,
        sitemap: `${siteMetadata.siteUrl}/sitemap/sitemap-index.xml`,
        policy: [{ userAgent: "*", allow: "/" }],
      },
    },
  ],
};
```

そして、以下を含む `package.json` ファイル:

```json
{
    "private": true,
    "name": "wiki",
    "version": "1.0.0",
    "license": "MIT",
    "scripts": {
        "develop": "gatsby develop -H 0.0.0.0",
        "start": "gatsby develop -H 0.0.0.0",
        "build": "gatsby build",
        "clean": "gatsby clean",
        "serve": "gatsby serve",
        "test": "echo test"
    },
    "dependencies": {
        "@primer/react": "^34.1.0",
        "@primer/css": "^17.5.0",
        "foam-cli": "^0.11.0",
        "gatsby": "^3.12.0",
        "gatsby-plugin-manifest": "^3.12.0",
        "gatsby-plugin-robots-txt": "^1.6.9",
        "gatsby-plugin-sitemap": "^5.4.0",
        "gatsby-source-filesystem": "^3.12.0",
        "gatsby-theme-primer-wiki": "^1.14.5",
        "react": "^17.0.2",
        "react-dom": "^17.0.2"
    }
}
```

テーマは [gatsby-theme-primer-wiki](https://github.com/theowenyoung/gatsby-theme-primer-wiki) を基にしています。

テーマをローカルでテストするには、最初に `yarn install` を実行し、その後 `gatsby develop` を使用してウェブサイトを提供します。
詳細については、gatsbyのドキュメントを参照してください。

### デプロイメントのためのCIのセットアップ

`.gitlab-ci.yml` ファイルを作成し、以下の内容を含めます:

```yml
# CI/CDテンプレートの改善に貢献するには、以下の開発ガイドに従ってください:
# https://docs.gitlab.com/ee/development/cicd/templates.html
# この特定のテンプレートはこちらにあります:
# https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Pages/Gatsby.gitlab-ci.yml

image: node:latest

stages:
  - deploy

pages:
  stage: deploy
  # このフォルダはビルド間でキャッシュされます
  # https://docs.gitlab.com/ee/ci/yaml/index.html#cache
  cache:
    paths:
      - node_modules/
      # git-lab CIのキャッシュを有効にします。.cacheとpublicは両方キャッシュされなければならず、そうでないとビルドが失敗します。
      - .cache/
      - public/
  script:
    - yarn install
    - ./node_modules/.bin/gatsby build --prefix-paths
  artifacts:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

このパイプラインにより、プロジェクトのメインブランチにプッシュするたびに、ウェブサイトが提供されるようになります。

## Jekyllを使用した公開

### _config.yamlの追加

ルートディレクトリ (`readme.md`が含まれているディレクトリ) に`_config.yaml` (拡張子なし) という別のファイルを追加します

```yaml
title: My Awesome Foam Project
baseurl: "" # サイトのサブパス、例: /blog
url: "/" # サイトの基本ホスト名＆プロトコル
theme: jekyll-theme-minimal
plugins:
  - jekyll-optional-front-matter
optional_front_matter:
  remove_originals: true
defaults:
  -
    scope:
      path: "" # レイアウトを正しくレンダリングするためにこれを追加する必要があります
    values:
      layout: "default"
```

[Jekyll Themes](https://jekyllthemes.io/)などの場所からテーマを選択できます。

### Gemlockファイルの追加

ルートディレクトリ (`readme.md`が含まれているディレクトリ) に`Gemfile` (拡張子なし) という別のファイルを追加します

```ruby
source "https://rubygems.org"

gem "jekyll"
gem "jekyll-theme-minimal"
gem "jekyll-optional-front-matter"
```

ファイルをコミットし、gitlabにプッシュします。

### CI/CDのセットアップ

1. GitLabのプロジェクトホームから`Set up CI/CD`をクリックします
2. テンプレートドロップダウンから`Jekyll`を選択します
3. `commit`をクリックします
4. これで、CI / CD > Pipelinesに移動すると、コードが実行されているのが見えるはずです

### トラブルシューティング

- *Could not locate Gemfile* - 上記の[Add a Gemlock file](#add-a-gemlock-file)の手順に従っていません
- *Conversion error: Jekyll::Converters::Scss encountered an error while converting* - テーマを参照する必要があります。
- *Pages are running in CI/CD, but I only ever see `test`, and never deploy* - メインブランチ (マスターから) の名前を変更した可能性があります - `.gitlab-ci.yml`の設定を確認し、デプロイコマンドが期待するブランチで実行されていることを確認してください。
- *I deployed, but my .msd files don't seem to be being converted into .html files* - GitHubがデフォルトでインストールするgemが必要です - `Gemfile`に`gem "jekyll-optional-front-matter"`が含まれていることを確認してください


