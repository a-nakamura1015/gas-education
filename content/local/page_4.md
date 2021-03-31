---
title: "clasp を使ってみよう"
date: 2021-04-01T07:57:33+09:00
pre: "<b>4. </b>"
weight: 4
---
### ログイン・ログアウト
Webエディタを使用する際と同様に Google アカウント でログインする必要があります。  
Webエディタにアクセスできない Google アカウントでログインをすると clasp でも利用することができないため、  
どの Google アカウントでログインしているかを意識するようにしましょう。  
```
clasp login
🔑 Authorize clasp by visiting this url:
https://accounts.google.com/o/oauth2/v2/auth?access_type=offline&scope=https%3A%2F%2Fwww.googleapis.com...
```
clasp にログインするアカウントを切り替える場合は一度ログアウトする必要があります。  
ログアウト後に再度ログインしたいアカウントでログインを行いましょう。  
```
clasp logout
```

### GASプロジェクトの新規作成
clasp で新規のプロジェクトを作成することができます。  
コマンドの最後にはプロジェクト名を指定します。
※今回はプロジェクト名を newProject としています。
```
clasp create newProject
```
コマンドが正常終了すると、作成されたプロジェクトのURLが表示されます。  
このURLをブラウザに貼り付けてアクセスすることができますが、  
次のコマンドを実行するだけで開くことができます。  
```
clasp open
```
ここでローカル環境を確認してみましょう。  
以下の２ファイルが生成されていることが確認できます。  
- .clasp.json
- appsscript.json

clasp.json はローカル環境とクラウド上のWebエディタを紐付けている重要なファイルです。  
appsscript.json はGASプロジェクトの情報を持っているファイルです。  
このファイルは実はこれまで作成してきたGASプロジェクトにも存在しており、  
Webエディタ上で確認することができます。（デフォルトで非表示になっています。）  

### Webエディタ上のファイルを取得する（clasp pull）
clasp でWebエディタ上の最新のファイルを取得することができます。  
このコマンドを実行することで、ローカル環境をWebエディタと同じ内容にすることができます。  
`clasp create` の際にWebエディタ上に Code.gs が生成されているため、以下のコマンドでローカルに落としてみましょう。
```
clasp pull
```
この際に注目してほしいのはローカルに落としたファイルの拡張子です。  
Code.gs を落としてきたはずが、拡張子が変わり Code.js になっています。  
これは clasp が自動的に拡張子を変更してくれているためです。  
また、このコマンドを実行すると**ローカルの同名ファイルを強制的に上書き**してしまうため、  
実行の際は上書きしても問題がないか確認をしたうえで実行しましょう。  

### Webエディタ上にファイルを送る（clasp push）
ローカルで編集したファイルをWeb上に送ることができます。  
このコマンドを実行することで、Webエディタをローカル環境と同じ内容にすることができます。  
試しに Code.js にコーディングされている `myFunction` を以下の内容に変更してみましょう。  
```js
function myFunction() {
	console.log('Hello!');
}
```
変更して保存が完了したら、以下のコマンドを実行してWebエディタに送ってみましょう。
```
clasp push
```
コマンド実行後にWebエディタを再表示するとWebエディタがローカル環境と同じ内容になっています。  
`clasp pull` と同様にローカルの .js ファイルはWebエディタ上では .gs に変換されています。  
このコマンドで気をつけるべきことは、カレントディレクトリにある全てのファイルをWebエディタ上に送ろうとします。  
Webエディタ上には拡張子が .gs と .htmlのファイルと appsscript.json しか作成することができないため、  
それ以外のファイルを送ろうとするとエラーが発生して失敗します。  
このようなときはpush対象のファイルから除外するファイルを指定する .claspignore を作成する必要があります。  
```
touch .claspignore
```
.claspignore の内容は適宜必要に応じて変更する必要がありますが、  
以下の内容で .js と appsscript.json 以外のファイルがpushされないようにすることができます。  
```
**/**
!.js
!appsscript.json
```
1行目の`**/**`はカレントフォルダ配下にあるフォルダ・ファイルを全て対象にするという意味です。  
これで全てのファイルがpush対象ではなくなります。  
ただこれでは何もWebエディタ上に送ることができないため、2行目以降で送りたいファイルを指定します。  
2行目の !.js は拡張子が.jsのファイルを除外対象にしないという意味です。  
.js のみですと .js をpushしない対象にするという意味になるため、  
それを否定する！を先頭につけることで、.jsのファイルを除外対象にしないという意味になります。  
同様に3行目で !appsscript.json は appsscript.json を除外対象にしないという意味になります。  

また、もう一点注意点があり、pushの際にWebエディタにのみファイルがあって、ローカル環境に同ファイルがない場合は消えてしまいます。  
pushする際はWebエディタ上にあるファイルを確認したうえで実行するようにしましょう。

### ディレクトリ構成
ファイルの数が増えてくるとフォルダの数を増やしたくなることがあると思います。  
仮にsrcフォルダ内にファイルをまとめるように変更した場合は、  
.claspignore を以下のように変更することでpushできるようになります。  
```
**/**
!src/.js
!appsscript.json
```
先ほど違うのは2行目で`!src/.js`とすることでsrcフォルダ配下の .js ファイルを除外対象にしないようにしています。  
`clasp push` をしてWebブラウザを確認してみましょう。  
注目して欲しいのはファイル名で フォルダ名/ファイル名 の形式に変わっています。  
これにより、`clasp pull` をした際もsrcフォルダ内のファイルを更新することができます。  

また、.clasp.json でpush対象の最上位フォルダを指定することができます。  
以下のように rootDir にフォルダ名を追加することで、追加したフォルダ名を push 対象の最上位フォルダにすることができます。  
```js
{
　"scriptId": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXx",
　"rootDir": "src"
}
```
### 既存のGASプロジェクトからクローンする
ここまでは clasp で新規作成をしてみましたが、既存のGASプロジェクトとローカル環境を紐づけることもできます。  
Google Drive上に新規のスクリプトエディタを作成したのち、以下のコマンドを実行してみましょう。  
対象のスクリプトエディタ内のコードがローカル環境に落とすことができれば成功です。  
```
clasp clone XXXXXX
```
コマンドの最後の`XXXXXX`には対象のスクリプトエディタのスクリプトIDを設定してください。  
スクリプトIDはスクリプトエディタの `プロジェクトの設定` で確認することができます。