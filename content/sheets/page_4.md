---
title: "シートを操作する"
date: 2020-08-18T05:50:19+09:00
pre: "<b>4. </b>"
weight: 4
---
### Sheetクラスとは
***Sheetクラス*** は、シートを操作する機能を提供するクラスです。

シートの情報を取得するメソッドや行・列の操作、シート上のセルを取得するなどのメソッドが提供されています。

早速、次のサンプルを実行し、シートの様々な情報を取得してみましょう。

```js
function spreadsheet_5() {
  var sheet = SpreadsheetApp.getActiveSheet();

  console.log(sheet.getIndex()); // シートのインデックス
  console.log(sheet.getName());　// シートの名前
}
```

#### セルを取得する
Sheetクラスはセルを取得する機能が備わっていることが大きな特徴です。

セルを取得するいくつかのメソッドが用意されていますが、その中でも最もスタンダードなメソッドが ***getRangeメソッド*** です。

getRangeメソッドは引数の数によって様々なパターンのセルを取得することができます。

一番シンプルなのは、引数に「A1」や「A1:C3」のようなセルのアドレスを文字列で渡して取得する方法です。

```js
Sheetオブジェクト.getRange(アドレス)
```

他のパターンとしては、行番号・列番号・行数・列数を引数に指定することでセルを取得する方法です。
```js
Sheetオブジェクト.getRange(行番号, 列番号[, 行数, 列数])
```
※ []は任意のため省略可能です。

行番号から行数分、列番号から列数分の範囲を指定して取得することができます。行数と列数は省略することができ、省略した場合はそれぞれの値は1となります。

各値は数値で設定するため、セルを動的に取得したい場合はこの方法を用います。

それでは、次のサンプルを実行してセルを取得できているか確認してみましょう。

```js
function spreadsheet_6() {
  var sheet = SpreadsheetApp.getActiveSheet();
  console.log(sheet.getRange('A1').getA1Notation()); // A1
  console.log(sheet.getRange('B2:D5').getA1Notation()); // B2:D5
  console.log(sheet.getRange('2:2').getA1Notation()); // 2:2
  console.log(sheet.getRange('B:B').getA1Notation()); // B:B
  console.log(sheet.getRange(3, 3).getA1Notation()); // C3
  console.log(sheet.getRange(3, 3, 2).getA1Notation()); // C3:C4
  console.log(sheet.getRange(3, 3, 2, 2).getA1Notation()); // C3:D4
}
```
サンプル内で実行しているgetA1Notationメソッドはセル範囲のアドレスをA1形式で取得するメソッドです。

アドレスの指定では、行または列全体のしても可能です。

また、行番号・列番号・行数・列数は変数で指定することも可能です。

#### シートのデータ範囲を取得する
アドレスや行番号、列番号がわからない場合や、シートに値が追加されていって取得するセル範囲が変化する場合はどのようにして取得するとよいでしょう？

このようなときに ***getDataRangeメソッド*** は非常に便利で、シート上のデータが存在する範囲をすべて取得してくれます。

```js
Sheetオブジェクト.getDataRange()
```
また、セルの範囲ではなく、データが存在する最後の行番号を取得する ***getLastRowメソッド*** や、データが存在する最後の列を取得する ***getLastColumメソッド*** も便利なメソッドです。

```js
Sheetオブジェクト.getLastRow()
```
```js
Sheetオブジェクト.getLastColumn()
```

これらのメソッドの使用例を次のサンプルで確認してみましょう。

```js
function spreadsheet_7() {
  var sheet = SpreadsheetApp.getActiveSheet();
  console.log(sheet.getDataRange().getA1Notation());
  console.log(sheet.getlastRow());
  console.log(sheet.getlastColumn());
}
```
getDataRangeメソッドの取得範囲の起点はA1セルで、そこからデータが入っている最終行および最終列までの範囲を取得します。
