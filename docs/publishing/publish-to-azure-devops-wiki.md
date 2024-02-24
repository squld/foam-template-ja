# Azure DevOps Wikiへの公開

FoamワークスペースをAzure DevOps wikiとして公開します。

[Azure DevOps](https://azure.microsoft.com/en-us/services/devops/)は、ソフトウェア開発チームのためのMicrosoftのコラボレーションソフトウェアで、以前はTeam Foundation Server (TFS)およびVisual Studio Team Servicesとして知られていました。オンプレミスまたはSaaSバージョンで利用可能です。以下のレシピはSaaSバージョンでテストされましたが、オンプレミスでも同じ方法で動作するはずです。

以下のレシピは、すでに[Azure DevOps](https://azure.microsoft.com/en-us/services/devops/)プロジェクトを持っていることを前提として書かれています。

## Foamワークスペースのセットアップ

1. [foam-template-jaプロジェクト](https://github.com/squld/foam-template-ja)を使用してFoamワークスペースを生成します。
2. リモートをAzure DevOpsのgitリポジトリに変更します (Repos -> Import a Repository -> Add Clone URL with Authentication) 、またはすべてのファイルを新しいAzure DevOps gitリポジトリにコピーします。
3. ウィキのホームページになるドキュメントを定義します。そのために、Foamワークスペースのルートフォルダに`.order`というファイルを作成し、最初の行に`.md`拡張子なしのドキュメントファイル名を記載します。Foamテンプレートから作成されたプロジェクトの場合、ファイルは次のようになります:

```
readme
```

4. リポジトリをAzure DevOpsのリモートにプッシュします。

## リポジトリをwikiとして公開する

1. ウェブブラウザでAzure DevOpsプロジェクトに移動します。
2. **Overview** > **Wiki**を選択します。プロジェクトにwikiがない場合は、ウェルカムページで**Publish code as a wiki**を選択します。
3. Foamワークスペースが含まれるリポジトリ、ブランチ (通常は`master`または`main`) 、フォルダ (foam-template-jaから作成されたワークスペースの場合は`/`) 、およびwiki名を選択し、**Publish**を押します。

公開されたワークスペースは次のようになります:

![Azure DevOps wiki](../../assets/images/azure-devops-wiki-demo.png)

wikiコンテンツの左側には、デフォルトの目次ペインがあります。ここでは、Foamワークスペースに存在するすべてのディレクトリとすべてのwikiページが表示されます。ページ名はファイル名から派生しており、アルファベット順にリストされています。`.order`ファイルに`.md`拡張子なしのファイル名を追加することで、ページを並び替えることができます。

_`.order`ファイルの最初のエントリがwikiのホームページを定義します。_

## Wikiの更新

GitHubへの変更をプッシュしている間、Azureをリモートに追加しない限り、wikiが更新されることはありません。複数のリポジトリに同時にプッシュすることができます。

 1. まず、ターミナルを開いて、`git remote show origin`を実行し、Azureが追加されているかどうかを確認します。出力にAzureが表示されない場合は、次の手順に従ってください。
 2. 現在のリモート (おそらくoriginという名前) を別の名前に変更します。例: `git remote rename origin main`
 3. 次に、2番目のリモートリポジトリのリモートを追加します。この場合はAzureです。例: `git remote add azure https://<YOUR_ID>@dev.azure.com/<YOUR_ID>/foam-notes/_git/foam-notes`。これは、Repos->Files->CloneからURLをコピーして取得できます。
 4. これで、originリモートを設定して、これらの両方にプッシュする必要があります。そのためには、`git config -e`を実行して編集します。
 5. プッシュしたい各リモートリポジトリのURLを含む`remote origin`セクションをファイルの下部に追加します。以下のようなものが表示されます:

 ```bash
 [core]
  ...
   (この部分は無視)
   ...
[branch "master"]
  remote = github
  merge = refs/heads/master
[remote "github"]
  url = git@github.com:username/repo.git
  fetch = +refs/heads/*:refs/remotes/github/*
[remote "azure"]
  url = https://<YOUR_ID>@dev.azure.com/<YOUR_ID>/foam-notes/_git/foam-notes
  fetch = +refs/heads/*:refs/remotes/azure/*
[remote "origin"]
  url = git@github.com:username/repo.git
  url = https://<YOUR_ID>@dev.azure.com/<YOUR_ID>/foam-notes/_git/foam-notes
 ```

 6. これで、`git push origin master`を使用して両方のリポジトリにプッシュするか、`git push github master`または`git push azure master`を使用して1つのリポジトリにプッシュできます。

詳細については、[Azure DevOpsドキュメント](https://docs.microsoft.com/en-us/azure/devops/project/wiki/publish-repo-to-wiki)を参照してください。


