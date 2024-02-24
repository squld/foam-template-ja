# KaTeXを使用した数式レンダリング

[[math-support-with-mathjax]]で述べた方法とは別に、Foamで数式をレンダリングするためにKaTeXも使用できます。ただし、JekyllがKaTeXをサポートするために使用するプラグインがGitHub Pagesとうまく連携しないため、もうGitHub Pagesを使用してウェブサイトをホストおよびデプロイすることはできません。

代替解決策は、[[publish-to-vercel]]を使用してウェブサイトを構築および公開することです。そのため、FoamプロジェクトにKaTeXを統合する前に、まず[[publish-to-vercel]]の指示に従ってFoamワークスペースをホストしてください。

## 必要なプラグインの追加

まだ行っていない場合は、Foamワークスペースの`_config.yml`と`Gemfile`にプラグイン`jekyll-katex`を追加してください。詳細な指示については、[[publish-to-vercel]]の`#Adding a _config.yml`および`#Adding a Gemfile`を参照してください。

## KaTeXのJSとCSSの読み込み

数式をレンダリングするためにKaTeXを使用しているため、CDNからKaTeXのJSとCSSファイルもインポートする必要があります。これらのファイルを読み込む公式の方法は、[KaTeX/KaTeX#starter-template](https://github.com/KaTeX/KaTeX#starter-template)で文書化されています。この場合、`_layouts/page.html`に次のコードスニペットを追加する必要があります:

```html
<!-- _layouts/page.html -->
---
layout: default
---

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">

<!-- ページのレンダリング速度を上げるために、KaTeXの読み込みを遅延させます -->
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.js" integrity="sha384-g7c+Jr9ZivxKLnZTDUhnkOnsh30B4H0rpLUpJ4jAIKs4fnJI+sEnkvrMWph2EDg4" crossorigin="anonymous"></script>

<!-- テキスト要素内の数式を自動的にレンダリングするには、auto-render拡張機能を含めます:  -->
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/contrib/auto-render.min.js" integrity="sha384-mll67QQFJfxn0IYznZYonOWZ644AWYC+Pt2cHqMaRhXVrursRwvLnLaebdGIlYNa" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>

<!-- ... -->
```

## ページコンテンツをラップするためのliquidタグの追加

`jekyll-katex`プラグインは以下のレンダリングに焦点を当てています:

- `katex` liquidタグでラップされた単一の数式、例: {% raw %}`{% katex %} ... {% endkatex %}`{% endraw %}。
- または、{% raw %}`{% katexmm %} ... {% endkatexmm %}`{% endraw %}でラップされた複数の数式を含む段落。

この場合、後者のタグを使用して{% raw %}`{{ content }}`{% endraw %}をラップします。`_layouts/page.html`内で{% raw %}`{{ content }}`{% endraw %}をliquidタグでラップする方法は以下の通りです:

```html
<!-- _layouts/page.html -->

<!-- ... -->
{% raw %}{% katexmm %} {{ content }} {% endkatexmm %}{% endraw %}
<!-- ... -->
```

## Foamのホームページでも数式をレンダリングする

`_layouts/page.html`のテンプレートにのみ変更を加えたことに気付いたかもしれませんが、これは`_layouts/home.html`がKaTeXサポートを持たないことを意味します。Foamのホームページで数式をレンダリングしたい場合は、`_layouts/home.html`にも同じ変更を加える必要があります。

最終的に、すべてがうまくいけば、これらの変更をGitHubにコミットした後、Vercelでホストされた私たちのサイトはKaTeXを使用して数式をレンダリングするサポートを持つことになります。KaTeXサポートを持つデフォルトテンプレートのデモはこちらです: [KaTeXサポート付きFoamテンプレート](https://foam-template.vercel.app/)。



