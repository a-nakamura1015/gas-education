---
title: "Web画面にスプレッドシートの値を表示してみましょう"
date: 2020-07-24T23:57:51+09:00
pre: "<b>7. </b>"
weight: 7
---
### Scriptletについて
GASで生成した値を画面に出力したいときは　**Scriptlet** を使用すると簡単に出力することができます。  
Scriptletには「Standard scriptlets」と「Printing scriptlets」の２種類があります。

#### Standard scriptlets
スクリプトとして実行しますが、結果は画面に出力されません。  
for文などの処理をしたい場合に記述します。
```
<? ... ?>
```

#### Printing scriptlets
スクリプトの実行結果を画面に出力することができます。
```
<?= ... ?>
```

### スプレッドシートの値を表示する
Scriptletを使用するとスプレッドシートの値を画面に出力することができます。  
以下のサンプルで確認をしてみましょう。

Code.gs
```js
function doGet(e) {
  var template = HtmlService.createTemplateFromFile('index');
  var sheet = SpreadsheetApp.openById('XXXX').getSheetByName('XXXX');
  var values = sheet.getRange(2, 1, sheet.getLastRow() - 1, sheet.getLastColumn()).getValues();
  template.values = values; // シートから取得した値を画面に渡します
  return template.evaluate();
}
```
index.html
```
<!DOCTYPE html>
<html>
<head>
  <base target="_top">
</head>
<body>
  <div class="wrapper">
    <div id="header">
      <h1>成績表</h1>
    </div>
    <div class="main">
      <div class="events">
        <table>
          <tr>
            <th>名前</th>
            <th>国語</th>
            <th>英語</th>
            <th>数学</th>
          </tr>
          <? for (var i = 0; i < values.length; i++) { ?>
          <tr>
            <td><?= values[i][0]; ?></td>
            <td><?= values[i][1]; ?></td>
            <td><?= values[i][2]; ?></td>
            <td><?= values[i][3]; ?></td>
          </tr>
          <? } ?>
          <tr></tr>
        </table>
      </div>
    </div>
  </div>
</body>
```

注目する点は index.html の以下の処理です。  
Scriptlet を活用してスプレッドシートから取得した値（`values`）を設定しています。  

```
<? for (var i = 0; i < values.length; i++) { ?>
<tr>
  <td><?= values[i][0]; ?></td>
  <td><?= values[i][1]; ?></td>
  <td><?= values[i][2]; ?></td>
  <td><?= values[i][3]; ?></td>
</tr>
<? } ?>
```
