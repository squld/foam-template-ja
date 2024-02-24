# Foamノートテンプレート

Foamにはノートテンプレートが含まれています!
これにより、コピー＆ペーストを使用せずに、類似の構造を持つノートを簡単に作成できます :)

テンプレートは[VS Codeのスニペット構文](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_snippet-syntax)をサポートしているため、以下が可能です:
- 新しく作成されたノートに変数を追加する
- フォームのように、ノートの重要な部分に自動的にナビゲートするためのタブストップを追加する
以下の例では、todoリストとタイムスタンプを示しています。

## Todoリスト

1. ${1:最初のタブストップ}
2. ${2:2番目のタブストップ}
3. ${3:3番目のタブストップ}

ノート作成日: ${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}

---

上記の例を試すには、`Foam: Create New Note From Template`コマンドを実行し、`your-first-template`テンプレートを選択してください。新しいノートが作成されたときに何が起こるかに注目してください!

このテンプレートを削除するには、単に`.foam/templates/your-first-template.md`ファイルを削除してください。

お楽しみください!
