# ノートテンプレート

Foamは、常に空のノートから始める代わりに、ノートの開始内容をカスタマイズできるノートテンプレートをサポートしています。

ノートテンプレートは、ワークスペースの特別なディレクトリ `.foam/templates` にある `.md` ファイルです。

## クイックスタート

テンプレートを作成する:

* コマンドパレットから `Foam: Create New Template` コマンドを実行します
* または、`.foam/templates` ディレクトリに通常の `.md` ファイルを手動で作成します

![新しいテンプレートの作成 GIF](../../assets/images/create-new-template.gif)

_テーマ: Ayu Light_

テンプレートからノートを作成するには:

* `Foam: Create New Note From Template` コマンドを実行し、指示に従います。まだテンプレートを作成していない場合でも心配はいりません! テンプレートが存在しない場合は、新しいテンプレートの作成を促されます。
* または、特別なデフォルトテンプレート (存在する場合は `.foam/templates/new-note.md`) を使用する `Foam: Create New Note` コマンドを実行します。

![テンプレートから新しいノートを作成する GIF](../../assets/images/create-new-note-from-template.gif)

_テーマ: Ayu Light_

## 特別なテンプレート

### デフォルトテンプレート

`.foam/templates/new-note.md` テンプレートは、`Foam: Create New Note` コマンドによって使用される特別なテンプレートです。
このテンプレートをカスタマイズして、ノートを作成するたびに含めたい内容を定義します。始めるには、テンプレートの YAML Front-Matter を以下のように定義することを*推奨*します:

```markdown
---
type: basic-note
---
```

### デフォルトの日次ノートテンプレート

`.foam/templates/daily-note.md` テンプレートは、日次ノートを作成する際 (例えば `Foam: Open Daily Note` を使用する場合) に使用される特別なテンプレートです。
このテンプレートをカスタマイズして、日次ノートを作成するたびに含めたい内容を定義します。始めるには、テンプレートの YAML Front-Matter を以下のように定義することを*推奨*します:

```markdown
---
type: daily-note
---
```

## 変数

テンプレートでは、[VS Code スニペット](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables)で利用可能なすべての変数を使用できます。

さらに、Foamによって提供される変数も使用できます:

| 名前                 | 説明      |
| -------------------- | ------------ |
| `FOAM_SELECTED_TEXT` | 新しいノートを作成する際に、テキストが選択されている場合、Foamはそれを選択されたテキストで埋めます。選択されたテキストは新しいノートへのウィキリンクで置き換えられます。     |
| `FOAM_TITLE`         | ノートのタイトル。使用されると、Foamはノートのタイトルを入力するように求めます。        |
| `FOAM_TITLE_SAFE`    | ファイルシステムで安全な形式のノートのタイトル。使用されると、`FOAM_TITLE` が既にプロンプトを引き起こしていない限り、Foamはノートのタイトルを入力するように求めます。   |
| `FOAM_SLUG`          | ノートのタイトルをスラッグ化したもの (デフォルトのgithubスラッグ方法を使用) 。使用されると、`FOAM_TITLE` が既にプロンプトを引き起こしていない限り、Foamはノートのタイトルを入力するように求めます。   |
| `FOAM_DATE_*`        | `FOAM_DATE_YEAR`, `FOAM_DATE_MONTH`, `FOAM_DATE_WEEK` など。[VS Code の日付時刻スニペット変数](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables)と同様の振る舞いをするFoam固有のバージョン。VS Code のバージョンよりもこれらのバージョンを優先してください。 |

### `FOAM_DATE_` 変数

Foamは、[VS Codeの日付スニペット変数](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables)と同様の動作をする独自の日付変数セットを定義しています。

例えば、`FOAM_DATE_YEAR`はVS Codeの`CURRENT_YEAR`と同じ動作をし、`FOAM_DATE_SECONDS_UNIX`は`CURRENT_SECONDS_UNIX`と同じ動作をしますなど。

デフォルトでは、`FOAM_DATE_`バージョンを優先して使用します。`FOAM_DATE_`とVS Codeの変数の両方で値を計算する際の日時は同じになりますが、日次ノートテンプレートを使用してノートを作成する場合を除きます。

より詳細な日付フォーマットについては、[こちらを参照してください](https://github.com/foambubble/foam/blob/master/packages/foam-vscode/src/services/variable-resolver.ts)。

#### 相対的な日次ノート

日次ノートを参照する際には、相対的なスニペット (`/+1d`、`/tomorrow`など) を使用できます。これらのケースでは、新しいノートは日次ノートテンプレートで作成されますが、使用される日時は現在の日時ではなく、相対的な日時になります。
`FOAM_DATE_`バージョンの変数を使用することで、現在の日時ではなく、期待通り明日の日付で変数が埋められます。

例えば、この日次ノートテンプレート (`.foam/templates/daily-note.md`) があるとします:

```markdown
# $FOAM_DATE_YEAR-$FOAM_DATE_MONTH-$FOAM_DATE_DATE

## 今日やること

* 事項1
* 事項2
```

`/tomorrow`スニペットを使用した場合、`FOAM_DATE_`変数は期待通り明日の日付で埋められます。
代わりにVS Codeバージョンのこれらの変数を使用した場合、今日の日付で埋められ、予期しない動作を引き起こします。

他のシナリオでノートを作成する場合、`FOAM_DATE_`の値はVS Codeのものと同じ日時を使用して計算されるため、デフォルトで全てのシナリオにおいて`FOAM_DATE_`バージョンを使用できます。

## メタデータ

テンプレートには、テンプレート自体に関するメタデータも含めることができます。メタデータはテンプレート内のYAML "Frontmatter"ブロックで定義されます。

| 名前         | 説明         |
| ------------- | ---------------------- |
| `filepath`    | 新しいノートを作成する際に使用するファイルパス。ファイルパスが相対ファイルパスの場合、現在のワークスペースに対して相対的です。 |
| `name`        | テンプレートピッカーに表示する人間が読める名前。    |
| `description` | テンプレートピッカーに表示する人間が読める説明。       |

Foam固有の変数 (例: `$FOAM_TITLE`) はテンプレートのメタデータ内で使用できます。しかし、VS Codeスニペット変数は ([現在のところ](https://github.com/foambubble/foam/pull/655)) サポートされていません。

### `filepath` 属性

`filepath` メタデータ属性を使用すると、テンプレートを使用してノートを作成する際に使用する相対パスまたは絶対パスを定義できます。ファイルパスが相対パスの場合、現在のワークスペースに対して相対的です。

#### **相対** `filepath` の例

例えば、`.foam/templates/new-note.md` をカスタマイズして、アクティブなファイルと同じディレクトリではなく、特定のディレクトリにファイルを開く `Foam: Create New Note` のデフォルト動作を上書きする場合、`filepath` を使用できます:

```yaml
---
# これは、アクティブなファイルに関係なく、現在のワークスペースの "journal" サブディレクトリにノートを作成します。
foam_template:
  filepath: 'journal/$FOAM_TITLE.md'
---
```

#### **絶対** `filepath` の例

`filepath` は絶対ファイルパスであり、エディターが現在開いているファイルやワークスペースに関係なく、ノートが同じ場所に作成されるようにすることができます。
絶対ファイルパスの形式は、使用されるファイルシステムによって異なる場合があります。

```yaml
---
foam_template:
  # Unix / MacOS ファイルシステム
  filepath: '/Users/john.smith/foam/journal/$FOAM_TITLE.md'

  # Windows ファイルシステム
  filepath: 'C:\Users\john.smith\Documents\foam\journal\$FOAM_TITLE.md'
---
```

#### **日付ベース** `filepath` の例

現在の日付を使用して `filepath` 値を変更することができます。これは、年、月などで整理したい場合に特に便利です。以下は、`journal/YEAR/MONTH-MONTH_NAME/` ファイルパスの下に新しい日次ノートを作成する[[daily-notes]]テンプレートのメタデータセクションの例です。例えば、2022年11月15日にノートを作成すると、新しいファイルは `C:\Users\foam_user\foam_notes\journal\2022\11-Nov\2022-11-15-daily-note.md` に作成されます。この方法は、現在の日付に関連する日次ノートの作成 (例: `/+1d`) も尊重します。

```markdown
---
type: daily-note
foam_template:
    description: $FOAM_TITLE の日次ノート
    filepath: "C:\\Users\\foam_user\\foam_notes\\journal\\$FOAM_DATE_YEAR\\$FOAM_DATE_MONTH-$FOAM_DATE_MONTH_NAME_SHORT\\$FOAM_DATE_YEAR-$FOAM_DATE_MONTH-$FOAM_DATE_DATE-daily-note.md"
---
# $FOAM_DATE_YEAR-$FOAM_DATE_MONTH-$FOAM_DATE_DATE の日次ノート
```

> 注: この方法は絶対ファイルパスの使用を**要求**し、この例ではWindowsのパス規則を使用しています。この方法は `.vscode/settings.json` で定義されたファイル名のフォーマットも上書きします。

### `name` と `description` 属性

これらの属性は、テンプレートピッカーで表示される人間が読める名前と説明を提供します (例: ユーザーが `Foam: Create New Note From Template` コマンドを使用する場合) :

![テンプレートピッカーに属性を注釈付けした画像](../../assets/images/template-picker-annotated.png)

### 既存の YAML Frontmatter ブロックにテンプレートメタデータを追加する

テンプレートが既に YAML Frontmatter ブロックを持っている場合、Foam テンプレートメタデータを追加できます。

#### 制限事項

Foam は *YAML* Frontmatter ブロックにテンプレートメタデータを追加することのみをサポートしています。既存の Frontmatter ブロックが他の形式 (例: JSON) を使用している場合、テンプレートメタデータを独自の YAML Frontmatter ブロックに追加する必要があります。

さらに、テンプレートメタデータは [YAML ブロックマッピング](https://yaml.org/spec/1.2/spec.html#id2798057) として提供されなければならず、属性は `foam_template` 行の直後の行に配置されなければなりません:

```yaml
---
existing_frontmatter: "既存の Frontmatter ブロック"
foam_template: # これは YAML の "ブロック" マッピングです ("フロー" マッピングはサポートされていません)
  name: 私のノートテンプレート # 属性は `foam_template` の直後の行に配置されなければなりません
  description: これは私のノートテンプレートです
  filepath: `journal/$FOAM_TITLE.md`
---
これはテンプレートの残りの部分です
```

複雑な YAML 形式の解析の技術的制限のため、メタデータがこの特定の形式で提供されない限り、Foam はテンプレートメタデータを正しく削除することができません。

この制限が不便である場合は、お知らせください。パース機能を拡張して、使用例をカバーできるかもしれません。その間、この制限なしでテンプレートメタデータを追加するには、独自の YAML Frontmatter ブロックに提供できます。

### テンプレートメタデータを独自の YAML Frontmatter ブロックに追加する

テンプレートの先頭にテンプレートメタデータを独自の YAML Frontmatter ブロックとして追加できます:

```yaml
---
foam_template:
  name: 私のノートテンプレート
  description: これは私のノートテンプレートです
  filepath: 'journal/$FOAM_TITLE.md'
---
これはテンプレートの残りの部分です
```

ノートが既に Frontmatter ブロックを持っている場合、Foam 固有の Frontmatter ブロックをテンプレートの先頭に追加できます。Foam 固有の Frontmatter ブロックは、ファイルの非常に始めに配置されなければならず、2つの Frontmatter ブロックの間には空白のみがあることができます。

```yaml
---
foam_template:
  name: 私のノートテンプレート
  description: これは私のノートテンプレートです
  filepath: 'journal/$FOAM_TITLE.md'
---

---
existing_frontmatter: "既存の Frontmatter ブロック"
---
これはテンプレートの残りの部分です
```



