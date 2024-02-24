# FoamのVsCodeでのログ

Foam拡張機能は、vscodeの`Output`タブで何をしているかの詳細をログに記録します。
通常、これはFoamに関する問題を報告する場合にのみ役立ちます。

1. タブを表示するには、`View > Output`をクリックします。
2. タブの右側のドロップダウンで、`Foam`を選択します。

![Foamのログを見つける](../../assets/images/foam-log.png)

Foamに関する問題を報告する際は、ログレベルを`Debug`に設定してください:

## セッションのログレベルを変更する

`Foam: Set log level`コマンドを実行します。

## デフォルトのログレベルを変更する

1. ワークスペース設定を開きます (`cmd+,`、または`Preferences: Open Workspace Settings`コマンドを実行)
2. `Foam > Logging: Level`エントリを探します。


