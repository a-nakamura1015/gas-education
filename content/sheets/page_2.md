---
title: "Spreadsheetサービス"
date: 2020-08-18T04:28:44+09:00
pre: "<b>2. </b>"
weight: 2
---
### Spreadsheetサービスとは
**Spreadsheetサービス** は、GASでスプレッドシートを操作するためのメソッドやスプレッドシートの情報をを提供するサービスです。  
Spreadsheetサービスの中でよく使うクラスを下記にまとめています。

| クラス名 | 概要 |
| --- | --- |
| SpreadsheetApp | Spreadsheetサービスのグローバルオブジェクト |
| Spreadsheet | スプレッドシートを操作する機能を提供する |
| Sheet | シートを操作する機能を提供する |
| Range | セルを操作する機能を提供する |

Spreadsheetサービスの各クラスは、SpreadsheetApp → Spreadsheet → Sheet → Range という階層構造になっています。  
各クラスにはそのオブジェクトを操作するメンバーとともに、その配下のオブジェクトを取得するメンバーが用意されています。  
これはスプレッドシートに限らず、他のサービスでもオブジェクトを操作する際の基本的な流れとなります。
また、GASのクラスに対して new 演算子でインスタンスを生成することはありません。

{{% notice tip %}}
GASのオブジェクト操作の基本動作は、グローバルオブジェクトから辿って目的のオブジェクトを取得し、操作をしていきます。
スプレッドシートの場合は **SpreadsheetApp** がグローバルオブジェクトになります。
{{% /notice %}}

### SpreadsheetAppクラスとは
**SpreadsheetAppクラス** はSpreadsheetサービスの最上位に位置するグローバルオブジェクトです。  
Spreadsheetサービスが提供する機能を利用するには、まずSpreadsheetAppクラスからアクセスすることになります。  
SpreadsheetAppクラスでは、直下のオブジェクトであるスプレッドシートを取得するメソッドや、  
現在アクティブになっているシートやセル範囲を取得するメソッドが用意されています。

#### スプレッドシートを取得する
スプレッドシートを操作するには、スプレッドシートを取得する必要があります。
GASでスプレッドシートを取得する主な方法は下記の通りです。

- アクティブなスプレッドシートを取得する
- IDでスプレッドシートを特定して取得する
- URLでスプレッドシートを特定して取得する

アクティブなスプレッドシートとは、スクリプトにバインドされているスプレッドシートを指します。  
スプレッドシートのコンテナバインドスクリプトであれば、次の構文でスプレッドシートを取得することができます。

```js
SpreadhsheetApp.getActiveSpreadsheet()
```

{{% notice info %}}
getActiveSpreadsheetメソッドをはじめ、「アクティブ」なオブジェクトを取得するメソッドは、コンテナバインドスクリプトでのみ使用できます。
{{% /notice %}}

そのため、バインドされていないスプレッドシートを取得する場合は、別の方法で取得する必要があります。  
その方法としては、IDで特定して取得するopenByIdメソッドと、URLで特定して取得するopenByUrlメソッドがあります。

```js
SpreaadsheetApp.openById(スプレッドシートのID);
```
```js
SpreadsheetApp.openByUrl(スプレッドシートのURL);
```

スプレッドシートをはじめ Google Apps のファイルは一意のURLが定められています。  
ブラウザではそのURLにアクセスすることで、そのファイルを開くことができます。  
GASでも同じように、そのURLがわかればスクリプトからスプレッドシートを特定して取得することができます。  
また、IDも一意に定められており、このIDはURLの一部を構成しています。以下の{ID}の部分がIDです。
```
https://docs.google.com/Spreadsheets/d/{ID}/edit#gid=0
```

このように、URLがわかればIDを取得することが可能です。  
では、実際にスクリプトでスプレッドシートを取得してみましょう。  
まずは、新規のスプレッドシートを作成して「別のスプレッドシート」と名前をつけてください。  
先ほどの手順で作成した「別のスプレッドシート」のURLとIDを確認した上で、下記のサンプルを記述して実行してください。

```js
function spreadsheet_1() {
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  SpreaadsheetApp.openById(スプレッドシートのID) // はじめてのGAS

  var url = 'https://docs.google.com/Spreadsheets/d/XXXX/edit#gid=0';
  spreadsheet = SpreadsheetApp.openByUrl(url);
  SpreaadsheetApp.openById(スプレッドシートのID); // バインドしていないスプレッドシート

  var id = 'XXXX';
  spreadhsheet = SpreaadsheetApp.openById(id); // バインドしていないスプレッドシート
}
```
```
はじめてのGAS
別のスプレッドシート
別のスプレッドシート
```

#### アクティブなシートを取得する
GASでスプレッドシートを操作する場合、シートやセルを操作対象とすることが多いでしょう。  
その度に、SpreadsheetApp → Spreadsheet → Sheet と辿っていくのは手間に感じるかもしれません。  
また、メソッド実行による Google Apps へのアクセスは実行時間が遅いという事実があります。  
GASには実行時間に関する制限がありますので、**処理速度を落とさないためにも Google Apps へアクセスするメソッドの実行回数はできる限り減らしたほうがよいです。**  
コンテナバインドスクリプトであれば、そのような場合にアクティブなシートを取得する方法として ***getActiveSheetメソッド*** を使用できます。
```js
SpreadsheetApp.getActiveSheet()
```
SpreadsheetAppから直接取得できるので、次のサンプルのように簡潔に記述することができます。また、スプレッドシートへアクセスするメソッドの実行回数が減らすこともできます。

```js
function spreadsheet_2() {
  var sheet = SpreadsheetApp.getActiveSheet();
  console.log(sheet.getName());
}
```
```
シート1
```
{{% notice tip %}}
Google Apps へのアクセスは事項時間が遅いので、できる限りアクセスするメソッドの実行回数は少なくなるようにしましょう。
{{% /notice %}}
