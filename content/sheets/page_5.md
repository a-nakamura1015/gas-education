---
title: "セル範囲を操作する"
date: 2020-08-18T06:32:07+09:00
pre: "<b>5. </b>"
weight: 5
---
## Rangeクラスとは
**Rangeクラス** は、セル範囲を操作する機能を提供するクラスです。  
セルの値や数式の取得や設定、セル範囲の情報の取得、書式の設定、並べ替えなどのメンバーが用意されています。  
試しに、セル範囲の様々な情報を取得するサンプルを実行してみましょう。
```js
function spreadsheet_8() {
  var range = SpreadsheetApp.getActiveSheet().getRange('A2:C5');
  console.log(range.getRow()); // 2
  console.log(range.getColumn()); // 1
  console.log(range.getNumRows()); // 4
  console.log(range.getNumColumns()); // 3
  console.log(range.getLastRow()); // 5
  console.log(range.getLastColumn()); // 3
}
```

## 値を取得・設定する
Rangeクラスのメンバーで最も基本的な操作はセルからの値の取得・設定といえます。  
単体セルの値を取得する **getValueメソッド** と単体セルの値を設定する **setValueメソッド** の構文を確認していきましょう。  
```js
Rangeオブジェクト.getValue()
```
```js
Rangeオブジェクト.setValue(値)
```
このメソッドには注意すべきことがありまして、セルを1つ1つ処理していくため、  
そのセルの数の分だけスプレッドシートへのアクセス回数がかさんでしまいます。  
アクセス回数がかさむと処理速度も遅くなります。
そのため、複数のセル範囲を取得・設定する場合は、  
セル範囲の値を取得する **getValuesメソッド** と、  
セル範囲の値を設定する **setValuesメソッド** を使用するようにしましょう。

```js
Rangeオブジェクト.getValues()
```
```js
Rangeオブジェクト.setValues(配列)
```
{{% notice info %}}
setValuesメソッドでは、対象となるセル範囲の「行数×列数」と、引数の二次元配列の「要素数×要素数」が一致している必要があります。
{{% /notice %}}

```js
function spreadsheet_9() {
  var sheet = SpreadsheetApp.getActiveSheet();
  sheet.getRange('A1').setValue('Google');
  console.log(sheet.getRange('A1').getValue()); // Google
  var values = [
    ['Taro', 22, '東京'],
    ['Hanako', 25, '大阪']
  ];
  sheet.getRange('A2:C3').setValues(values);
  console.log(sheet.getRange('A2:C3').getValues()); // ['Taro', 22, '東京'],['Hanako', 25, '大阪']
}
```
