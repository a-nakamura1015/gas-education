---
title: "スプレッドシートを操作する"
date: 2020-08-18T05:25:07+09:00
pre: "<b>3. </b>"
weight: 3
---
## Spreadsheetクラスとは
**Spreadsheetクラス** は、文字通りスプレッドシートを操作する機能を提供するクラスです。  
シートを取得したり作成したりするメソッドやスプレッドシートの情報など（メンバー）が提供されています。  
では早速、Spreadsheetクラスのメンバーを使って、スプレッドシートの様々な情報を取得してみましょう。  
次のサンプルはスプレッドシートのID、スプレッドシート名、URLがログに出力されます。

```js
function spreadsheet_3() {
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  console.log(spreadsheet.getId()); // スプレッドシートのID
  console.log(spreadsheet.getName()); // スプレッドシートの名前
  console.log(spreadsheet.getURL()); // スプレッドシートのURL
}
```
### シートを取得する
Spreadsheetクラスはその配下であるシートを取得することができます。  
シートの取得方法は次のような方法があります。

- アクティブなシートを取得する
- シート名で特定して取得する
- インデックスで配列からシートを特定して取得する

アクティブなシートは先ほど説明した通りコンテナバインドスクリプトに限り、SpreadsheetAppクラスから直接取得することができます。  
別な方法として、**getSheetByNameメソッド** を使用してシート名で特定して取得する方法があります。  
シート名で取得するのは簡単ではありますが、シート名が変わると取得できなくなる点に注意です。

```js
Spreadsheetオブジェクト.getSheetByName(シート名)
```
他にも、**getSheetsメソッド** でシートを配列として取得した上で、インデックスでシートを特定する方法もあります。

```js
Spreadsheetオブジェクト.getSheets()
```

getSheetsメソッドは、スプレッドシートに含まれるシートのうち最も左に位置するシートのインデックスを0として、  
そこから右方向に順番にシートを配列に格納して取得します。
戻り値が配列になりますので、全てのシートに処理を行いたい場合などに便利です。  
しかし、インデックスは並び順に依存しているため、  
特定のシートのみ処理をしたい（例えば左から2つめのシートのみ処理したい）場合はシートの並び順が変更された場合は意図したシートが処理されないことになります。

それでは、次のサンプルを実行して確認してみましょう。

```js
function spreadsheet_4() {
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = spreadsheet.getSheetByName('シート1');
  conosole.log(sheet.getName());

  var sheets = spreadsheetApp.getSheets();
  console.log(sheet[0].getName());
  console.log(sheet[1].getName());
}
```

**getNameメソッド** はシート名を取得するメソッドです。getSheetsメソッドはシートを配列として取得するため、角括弧内にインデックスを用いて各シートを取り出すことができます。
