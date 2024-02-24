# ショートカットとGitHubアクションを使用したノートのキャプチャ

この #レシピ を使用すると、iOSデバイスでノートを作成し、自動的にFoamにインポートすることができます。

## コンテキスト

* [Foam for VSCode](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode)を使用してノートを管理しています
* [一時的で不完全なノートのためのライティングインボックス](https://notes.andymatuschak.org/A%20writing%20inbox%20for%20transient%20and%20incomplete%20notes)のような習慣を採用したいと考えています
* iOSデバイスからFoamノートに素早くノートをキャプチャするために[ショートカット](https://support.apple.com/guide/shortcuts/welcome/ios)を使用したいと考えています

## その他のツール

* GitHubの使用方法に慣れていることを前提としています (Foamを使用している場合、これは暗黙の了解です)
* iOSデバイスを持っています。

## 使用方法

1. GitHubリポジトリで[`foam-capture-action`]()をセットアップし、"ワークフローのディスパッチ"イベントによってトリガーされるようにします。

```
name: Manually triggered workflow
on:
  workflow_dispatch:
    inputs:
      data:
        description: '知識ベースに入れる情報。'
        required: true

jobs:
  store_data:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - uses: anglinb/foam-capture-action@main
      with:
        {% raw %}
        capture: ${{ github.event.inputs.data }}
        {% endraw %}
    - run: |
        git config --local user.email "example@gmail.com"
        git config --local user.name "Your name"
        git commit -m "ワークフロートリガーからキャプチャ" -a
        git push -u origin master
```

2. GitHubで[パーソナルアクセストークンを作成](https://github.com/settings/tokens)し、`repo`スコープを付与します - トークンをメモしておきます
3. ショートカットで使用する`workflow-id`を見つけるために、このコマンドを実行します。

```bash
curl \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: Bearer <GITHUB_TOKEN>" \
    https://api.github.com/repos/<owner>/<repository>/actions/workflows
```

4. この[ショートカット](https://www.icloud.com/shortcuts/57d2ed90c40e43a5badcc174ebfaaf1d)をiOSデバイスにコピーし、最後のステップ`GetContentsOfURL`の内容を編集します。
   - ショートカットステップのURLを、前のステップからの`owner`、`repository`、`workflow-id`で更新してください
   - ショートカットステップのヘッダーを更新し、`[GITHUB_TOKEN]`をステップ2で取得したパーソナルアクセストークンに置き換えてください

5. ショートカットを実行し、お祝いしましょう! ✨ (GitHubアクションの実行が開始され、入力したテキストがリポジトリの`inbox.md`に表示されるはずです。)


