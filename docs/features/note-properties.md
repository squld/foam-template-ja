---
type: feature
keywords: hello world, bonjour
tags: [hello, bonjour]
---

# ノートプロパティ

ファイルの先頭には、プロパティを定義するセクションがあります。このセクションはドキュメントの[Front-Matter](https://learn.cloudcannon.com/jekyll/introduction-to-jekyll-front-matter/)として知られ、[YAMLフォーマット](https://www.codeproject.com/Articles/1214409/Learn-YAML-in-five-minutes)を使用しています。

> このYAMLセクションはファイルの非常に上部にある必要があります。

例えば、このファイルの場合、以下のようになります:

```markdown
---
type: feature
keywords: hello world, bonjour
---
```

これにより、このドキュメントの`type`が`feature`に設定され、ドキュメントのキーワードが**3つ**設定されます: `hello`、`world`、`bonjour`。YAMLパーサーは、これらのYAMLプロパティの区切り文字としてスペースとカンマの両方を扱います。これらのプロパティに複数の単語の値を使用したい場合は、単語をダッシュまたはアンダースコアで結合する必要があります (つまり、`hello world`の代わりに`hello_world`または`hello-world`を使用します) 。

> ドキュメントに好きなだけカスタムプロパティを設定できますが、Foamによって定義されたいくつかの[特別なプロパティ](#special-properties)があります。

## 特別なプロパティ

Foamには特別な意味を持ついくつかのプロパティがあります:

| 名前    | 説明                                                                                                                                                                      |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title` | グラフで見ることになるノートの名前を割り当てます。ファイル名や最初の見出しに関係なく ([[write-notes-in-foam]]も参照) 。                       |
| `type`  | グラフでノートを異なるスタイルで表示するために使用できます ([[graph-visualization]]も参照) 。ドキュメントのデフォルトタイプは`note`ですが、このプロパティで指定されていない限り。 |
| `tags`  | ノートにタグを追加するために使用できます ([[tags]]を参照) 。                                                                                                                                 |

例えば:

```markdown
---
title: "Note Title"
type: "daily-note"
tags: daily, funny, planning

---
```

## Foamテンプレートプロパティ

Foamテンプレートに特有のプロパティも存在します。詳細については、[[note-templates#Metadata]]を参照してください。



