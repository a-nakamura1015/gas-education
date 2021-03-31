---
title: "clasp を使う前に"
date: 2021-04-01T07:27:56+09:00
pre: "<b>3. </b>"
weight: 3
---
### 前準備
#### 1. Google Apps Script API を有効化しましょう
実は clasp をインストールしても、Google アカウントの設定で Google Apps Script APIを有効にしなければ clasp を利用することはできません。  
下記リンク先から Google Apps Script を有効化することができます。  
https://script.google.com/home/usersettings

設定画面の「Google Apps Script API 」の下に「オフ」と表示されていると、  
Google Apps Script API が無効化の状態になっています。  
「Google Apps Script API 」をクリックしますと、「オン」「オフ」を切り替える画面に遷移します。  
![page_3_1.png](../img/page_3_1.png)

遷移先の画面で右端にトグルボタン表示されていますので、  
こちらをクリックして左端の文字が「オフ」から「オン」に変われば設定完了です。  
![page_3_2.png](../img/page_3_2.png)

#### 2. エディタをインストールしましょう  
お気に入りのエディタをインストールしましょう。  
基本的に好きなエディタを使っていただいたも問題ありませんが、  
以降は VSCode でコーディングをしている前提で進めていくため、  
特にこだわりがなければ VSCode をインストールしてください。  
https://azure.microsoft.com/ja-jp/products/visual-studio-code/

#### 3. Node.js をインストールしましょう
clasp を利用するにはPCに Node.js と呼ばれるJavaScriptの実行環境をインストールする必要があります。  
以下リンク先から Node.js をインストールしてください。  
https://nodejs.org/ja/

インストールを完了しましたら、以下のコマンドを実行して Node.js と npm がインストールされているかを確認しましょう。  
npm は　Node.js　のパッケージを管理しており、そのパッケージの中に clasp があります。  
`-v`でインストールされているバージョンを確認することができます。  
以下のバージョンよりも新しければ問題ありません。
```
node -v
 v12.14.1
npm -v
 6.13.4
```

#### 4. clasp をインストールしましょう
Node.js と npm がインストールされましたら、以下のnpmコマンドで clasp をインストールしましょう。
```
npm install @google/clasp -g
```

これで前準備は完了です！
