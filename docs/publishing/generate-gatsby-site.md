# Gatsbyを使用してサイトを生成する

## foam-gatsby-templateの使用

[foam-gatsby-template](https://github.com/mathieudutour/foam-gatsby-template)を使用して、GitHubまたは[Vercel](https://vercel.com)上でオンラインでホストできる静的サイトを生成できます。

### GitHubページへのfoamの公開

メインブランチに変更がプッシュされると、GitHubアクションがGitHubページに自動デプロイするように設定されています。

### Vercelへのfoamの公開

公開する準備ができたら、ローカルビルドを実行します。

```bash
cd _layouts
npm run build
```

.gitignoreファイルから`public`を削除し、`_layouts`内のpublicフォルダをGitHubにコミットしてプッシュします。

Vercelアカウントにログインします (まだ持っていない場合は作成してください) 。

プロジェクトをインポートします。ルートディレクトリとして`_layouts/public`を選択し、**Continue**をクリックします。次に、プロジェクトに名前を付けて、**Deploy**をクリックします。

それだけです!

## foam-template-gatsby-kbの使用

別のテンプレート[foam-template-gatsby-kb](https://github.com/hikerpig/foam-template-gatsby-kb)を使用し、[Vercel](https://vercel.com)または[Netlify](https://www.netlify.com/)上でホストできます。

## foam-template-gatsby-theme-primer-wikiの使用

別のテンプレート[foam-template-gatsby-theme-primer-wiki](https://github.com/theowenyoung/foam-template-gatsby-theme-primer-wiki) ([デモ](https://demo-wiki.owenyoung.com/)) を使用し、Githubページ、[Vercel](https://vercel.com)または[Netlify](https://www.netlify.com/)上でホストできます。


