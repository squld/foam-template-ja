---
layout: mathjax
---

# 数式サポート

公開されたFoamページはデフォルトで数式をサポートしていません。この機能を有効にするには、`_layouts/page.html`の最後に次のコードスニペットを追加できます:

```html
<script src="https://cdn.jsdelivr.net/npm/mathjax@2/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
        }
    });
</script>
```

このアプローチは、AMS-LaTeX方言をMathJaxに組み込んで、`$` (上記のスニペットでカスタマイズ可能) で区切られたものをインライン数式として、`$$`を数式のブロック (html divタグのように) としてレンダリングする[MathJax](https://www.mathjax.org/)ライブラリを使用します。

`$...$`を使用したインライン数式の例:

`$e^{i \pi}+1=0$`は、$e^{i \pi}+1=0$になります

`$$...$$`を使用した数式ブロックの例:

`$$ f_{\mathbf{X}}\left(x_{1}, \ldots, x_{k}\right)=\frac{\exp \left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^{\mathrm{T}} \mathbf{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right)}{\sqrt{(2 \pi)^{k}|\mathbf{\Sigma}|}} $$`

は、次のようになります:

$$ f_{\mathbf{X}}\left(x_{1}, \ldots, x_{k}\right)=\frac{\exp \left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^{\mathrm{T}} \mathbf{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right)}{\sqrt{(2 \pi)^{k}|\mathbf{\Sigma}|}} $$

## 代替アプローチ

AMS以外のLaTeX方言や、使用したい他のJavaScriptレンダリングライブラリがあります。将来のFoamバージョンでは、KaTeX構文を標準でサポートするかもしれませんが、現時点ではこれらの統合はユーザーに任されています。

## Foamのホームページで数式が機能しないのはなぜですか?

Foamサイトのインデックスページで数学をレンダリングしたい場合は、`_layouts/home.html`にもそれを追加する必要があります。または、`readme.md/index.md`の先頭にこのFront Matterを置くことで、インデックスページのレイアウトを"home"ではなく"page"に変更します:

```
---
layout: page
---

# 通常のタイトルはここに
```

参照: [How to support latex in github-pages](https://stackoverflow.com/questions/26275645/how-to-support-latex-in-github-pages)


