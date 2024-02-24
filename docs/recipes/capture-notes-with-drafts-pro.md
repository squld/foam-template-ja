# Drafts Proでメモをキャプチャする

この #レシピ を使用すると、iOSデバイス上でメモを作成し、自動的にFoamにインポートすることができます。

## コンテキスト

* [Foam for VSCode](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode)を使用してメモを管理しています
* [A writing inbox for transient and incomplete notes](https://notes.andymatuschak.org/A%20writing%20inbox%20for%20transient%20and%20incomplete%20notes)のような習慣を採用したいと考えています
* iOSデバイスからFoamのメモに素早くメモをキャプチャするために[Drafts Pro](https://docs.getdrafts.com/)を使用したいと考えています

## 他のツール

* GitHubの使用方法に慣れていることを前提としています (Foamを使用している場合、これは暗黙の了解です)
* [Drafts](https://getdrafts.com/)を搭載したiOSデバイスを持っています
* アクションを編集するために[Drafts Pro](https://docs.getdrafts.com/draftspro)にアップグレードしています

## 使用方法

1. [Draftsで新しいアクションを作成します](https://docs.getdrafts.com/docs/actions/editing-actions)
2. スクリプトのタイプの単一の[ステップ](https://docs.getdrafts.com/actions/steps/)を追加します
3. 下記のブロックからコードを追加してスクリプトを編集します
4. スクリプトの上部にある設定を好みに合わせて編集します
5. Draftsの他のアクションオプションをお好みで設定します
6. アクションを保存します
7. GitHubで[個人アクセストークンを作成します](https://github.com/settings/tokens) そして`repo`スコープを与えます - トークンをメモしておきます
8. Draftsでメモを作成します
9. ステップ1-6で作成したアクションを選択します
10. 最初の実行時には、以下の情報を追加する必要があります:
    1. GitHubのユーザー名
    2. Foamリポジトリのリポジトリ名
    3. ステップ7からのGitHubアクセストークン
    4. 著者名
11. GitHubリポジトリでコミットを確認します
12. WebにFoamを公開している場合は、公開ファイルからインボックスファイルを除外するために公開設定を編集することをお勧めします - 公開 (および方法) はユーザーの選択であり、このレシピの範囲を超えています

## Drafts Actionのコード

```javascript
// https://forums.getdrafts.com/t/script-step-post-to-github-without-working-copy/3594 から適応
// Foamデジタルガーデンのライティング受信箱に投稿

/*
 * 環境に合わせてこれらの行を編集
 */
const inboxFolder = "inbox/";   // Foamリポジトリ内のノートが保存されるフォルダ。末尾にスラッシュが必要ですが、ルートの場合は''を使用
const requiredTags = ['inbox']; // これらに加えてDraftsアプリからのタグがすべて追加されます
const addLinkToInbox = true;    // true = 作成されたノートに[[index]]へのリンクが追加されます、false = リンクなし
const addTimeStamp = true;      // true = ノートの末尾にキャプチャ日時を追加

/*
 * 編集を停止
 */

const credential = Credential.create("GitHub garden repo", "Foamノートをホストしているリポジトリ名とその認証情報");
credential.addTextField("username", "GitHubユーザー名");
credential.addTextField('repo', 'リポジトリ名');
credential.addPasswordField("key", "GitHubパーソナルアクセストークン");
credential.addTextField('author', '著者');
credential.authorize();

const githubKey = credential.getValue('key');
const githubUser = credential.getValue('username');
const repo = credential.getValue('repo');
const author = credential.getValue('author');

const http = HTTP.create(); // HTTPオブジェクトを作成
const base = 'https://api.github.com';


const posttime = new Date();
const title = draft.title;
const txt = draft.processTemplate("[[line|3..]]");
const mergedTags = [...draft.tags, ...requiredTags];
const slugbase = title.toLowerCase().replace(/\s/g, "-");

const datestr = `${posttime.getFullYear()}-${pad(posttime.getMonth() + 1)}-${pad(posttime.getDate())}`;
const timestr = `${pad(posttime.getHours())}:${pad(posttime.getMinutes())}:00`;
const yr = `${posttime.getFullYear()}`;
const pdOffset = posttime.getTimezoneOffset();
const offsetChar = pdOffset >= 0 ? '-' : '+';
var pdHours = Math.floor(pdOffset/60);
console.log(pdHours);
pdHours = pdHours >= 0 ? pdHours : pdHours * -1;
console.log(pdHours);
const tzString = `${offsetChar}${pad(pdHours)}:00`;
const postdate = `${datestr}T${timestr}${tzString}`;


const slug = `${slugbase}`
const fn = `${slug}.md`;
let preamble = `# ${title} \n\n`;

mergedTags.forEach(function(item,index){
   preamble += `#${item} `;
  }
);

if (addLinkToInbox) {
    preamble += "\n\n[[inbox]]\n";
}

preamble += "\n\n";

var doc = `${preamble}${txt}`;

if (addTimeStamp){

    doc += `\n\nキャプチャ: ${postdate}\n`
}

const options = {
    url: `https://api.github.com/repos/${githubUser}/${repo}/contents/${inboxFolder}${fn}`,
    method: 'PUT',
    data: {
        message: `Draftsからの受信箱 ${datestr}`,
        content: Base64.encode(doc)
    },
    headers: {
        'Authorization': `token ${githubKey}`
    }
};

var response = http.request(options);

if (response.success) {
    // やったね
} else {
    console.log(response.statusCode);
    console.log(response.error);
}

function pad(n) {
    let str = String(n);
    while (str.length < 2) {
        str = `0${str}`;
    }
    return str;
}

```


