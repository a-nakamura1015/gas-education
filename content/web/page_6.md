---
title: "Web画面からGASの関数を実行してみましょう"
date: 2020-07-24T23:57:40+09:00
pre: "<b>6. </b>"
weight: 6
---
ここまでは主にクライアントサイドのコーディングをしてきましたが、  
ここからはサーバーサイドのコーデイングをしていきましょう。  
Google Apps Script のサーバーサイドは`.gsファイル`にコーディングします。

### Google Apps Script の関数の作り方について
それでは`.gsファイル`にコーディングをしてみましょう。  
今回はスプレッドシートから値を取得する関数と、スプレッドシートへ値を設定する関数を作成してみます。

{{< tabs groupId="web_6_1" >}}
{{% tab name="コード.gs" %}}
```js
var SHEET_ID = 'シートのID'
var SHEET_NAME = 'シートの名前'

function getSheetData() {
  // 1. スプレッドシートを特定して取得します。
  var spreadsheet = SpreadsheetApp.openById(SHEET_ID);
  // 2. シートを特定して取得します。
  var sheet = spreadsheet.getSheetByName(SHEET_NAME);
  // 3. セル（範囲）を特定して取得します。
  var range = sheet.getRange('A1');
  // 4. 対象のセルの入力値を返します。
  return range.getValue();
}

function setSheetData() {
  // 1. スプレッドシートを特定して取得します。
  var spreadsheet = SpreadsheetApp.openById(SHEET_ID);
  // 2. シートを特定して取得します。
  var sheet = spreadsheet.getSheetByName(SHEET_NAME);
  // 3. セル（範囲）を特定して取得します。
  var range = sheet.getRange('A1');
  // 4. 対象のセルの入力値を返します。
  range.setValue('hello!');
}
```
{{% /tab %}}
{{< /tabs >}}

{{% notice info %}}
**シートのID** と **シートの名前** は作成した Google スプレッドシートの **ID** と **シートの名前** を入力してください。
{{% /notice %}}

これで Google Apps Script の関数は用意できました。  
次は用意した関数をクライアントサイドから呼び出してみましょう。

---
### google.script.run について

クライアントサイドで`google.script.run`を使用すると、サーバーサイドの Google Apps Script 関数を実行することができます。  
[【リファレンス】google.script.run](https://developers.google.com/apps-script/guides/html/reference/run)

それでは、早速先ほど作成した`setSheetData()`を呼び出してみましょう。

{{< tabs groupId="web_6_2" >}}
{{% tab name="index.html" %}}
```html
<script>
  google.script.run.setSheetData();
</script>
```
{{% /tab %}}
{{< /tabs >}}

今回はクライアントサイドで関数の中から呼び出さず、scriptタグの中にコーディングしているため、  
画面が表示されるタイミングで実行されます。

画面を表示したのち、対象のシートのA1セルに hello! と表示されるかを確認してみましょう。

#### 引数を渡す
先ほどは 対象のシートのA1セルに hello! と表示されるようにしましたが、  
クライアントサイドで表示する値を設定できるようにしてみましょう。  
`setSheetData()`に引数を渡せるようにコードを変更します。

変更点は次の３点です。
- クライアントサイドで`setSheetData()`を呼び出す際に、引数に値（'こんにちは！'）を設定する。
- サーバーサイドの`setSheetData()`が引数の値を受け取ることができるように、丸括弧内に変数 (`value`)を設定する。
- 最後の`range.setValue('hello!')`の丸括弧内の'hello!'を変数（`value`）に置き換える。

{{< tabs groupId="web_6_3" >}}
{{% tab name="index.html" %}}
```html
<script>
  google.script.run.setSheetData('こんにちは！');
</script>
```
{{% /tab %}}
{{% tab name="コード.gs" %}}
```js
function setSheetData(value) {
  // 1. スプレッドシートを特定して取得します。
  var spreadsheet = SpreadsheetApp.openById(SHEET_ID);
  // 2. シートを特定して取得します。
  var sheet = spreadsheet.getSheetByName(SHEET_NAME);
  // 3. セル（範囲）を特定して取得します。
  var range = sheet.getRange('A1');
  // 4. 対象のセルの入力値を返します。
  range.setValue(value);
}
```
{{% /tab %}}
{{< /tabs >}}

変更したのちWeb画面を更新して、対象のシートのA1セルに`こんにちは！`と出力されているかを確認しましょう。

#### 画面で入力した値をスプレッドシートに出力する
先ほど実行した関数によって、クライアントサイドから値を渡すことができることを確認しました。  
次はクライアントサイドで入力した値をサーバーサイドに渡してみましょう。

{{< tabs groupId="web_6_4" >}}
{{% tab name="index.html" %}}
```html
<input type='txt' id='msg' onclick='output()' />
<script>
  function output() {
    // 1. テキストボックスに入力した値を取得します。
    var value = document.getElementById('msg').value;
    // 2. 取得した値を setSheetData関数の引数として設定して呼び出します。
    google.script.run.setSheetData(value);
  }
</script>
```
{{% /tab %}}
{{< /tabs >}}

変更したのちWeb画面を更新して、対象のシートのA1セルに、テキストボックスに入力した値が出力されているかを確認しましょう。

---
### 同期処理と非同期処理について
次はサーバーサイドから値を取得してみましょう。  
先ほどコーディングした`getSheetData()`を実行してみます。  
`index.html`を下記の通りに変更したのち、Web画面を更新してコンソールログに値が表示されるかを確認してみましょう。

{{< tabs groupId="web_6_5" >}}
{{% tab name="index.html" %}}
```html
<script>
 // 1. スプレッドシートから値を取得する
 var result = google.script.run.getSheetData();
 // 2. 取得した値をコンソールログ表示する
 console.log(result);
</script>
```
{{% /tab %}}
{{< /tabs >}}

コンソールログには`undefined`と表示されました。  
これは`console.log(result)`で表示しようとしているresult変数の中身が空っぽということになります。

`getSheetData()`が実行されなかったのでしょうか。  
実は`getSheetData()`は実行されていますが、その戻り値が返ってくる前に`console.log(result)`が実行されているのです。  

このような事象が起きるのは、JavaScriptのアプリケーションが「シングルスレッド」で実行されているためです。  
「シングルスレッド」を端的に説明すると、 **一度にひとつのことを実行していく処理** ということです。  
つまり、1度に1つの処理しかできない（並列処理ができない）のです。  
しかし、非同期処理により外部に処理を任せている間に自身の処理を進めることができます。

#### 同期処理とは
同期処理はコーディングした処理の上から順番に実行されるという意味です。  
上から順番に実行されるのでシンプルですね。  
下記のスクリプトも同期処理で動いているため、アラートは「1」、「2」、「3」と順に表示されます。

{{< tabs groupId="web_6_6" >}}
{{% tab name="index.html" %}}
```html
<script>
  alert(1); // ①
  alert(2); // ②
  alert(3); // ③
</script>
```
{{% /tab %}}
{{< /tabs >}}

#### 非同期処理とは
非同期処理は外部に処理を任せている間に自身の処理を進めることができます。  
先ほどシートの値を取得しようとしたスクリプトで確認してみましょう。

{{< tabs groupId="web_6_7" >}}
{{% tab name="index.html" %}}
```html
<script>
 // 1. スプレッドシートから値を取得する
 var result = google.script.run.getSheetData();
 // 2. 取得した値をアラートで表示する
 console.log(result);
</script>
```
{{% /tab %}}
{{< /tabs >}}

`getSheetData()`でブラウザから Google サーバーに処理を行うように命令をしています。（具体的にはシートから値を取得するように命令しています。）  
しかし、このように外部（Google サーバー）に処理を行うように命令した場合は、その処理結果（戻り値）を待たずにクライアントサイドのJavaScriptは順次処理を続行してしまいます。  
これが**非同期処理**です。

しかし、GAS関数の戻り値を受け取って同期処理を行いたいですよね。  
それを実現するのが`withSuccessHandler`メソッドと`withFailureHandler`メソッドです。

---
### withSuccessHandler について
`withSuccessHandler`メソッドの特徴は **「クライアントサイドからGAS関数を呼び出した後の処理を設定できる」** ことです。  
これらのメソッドを活用することでGAS関数で取得した結果をクライアントサイドに表示することができます。  
しかし、活用するには **コールバック関数** を理解する必要があります。

#### コールバック関数とは
日常生活でコールバックと言いますと、「かかってきた電話に対して電話をかけ直す（折り返し電話をする）」という意味で使われますね。  
JavaScriptでコールバックは「後々呼び出すために定義した関数」という意味で使われます。  
ただ、このコールバックされる関数は特別なことは何もなく、普通のJavaScriptの関数です。  
では、具体的にどのように使用するのかを下記のようにHTMLを修正して確認してみましょう。

{{< tabs groupId="web_6_8" >}}
{{% tab name="index.html" %}}
```html
<script>
  // 数値の2を返す関数（後々呼び出すためにコーディングされた関数）
  function getNumber() {
    return 2;
  }
  // 1. コンソールログに「1」を表示する。
  console.log(1);
  // 2. コンソールログに「getNumber関数の戻り値」を表示する。
  console.log(getNumber());
  // 3. コンソールログに「3」を表示する。
  console.log(3);
</script>
```
{{% /tab %}}
{{< /tabs >}}

上記では`getNumber`関数というコールバック関数をコーディングしています。  
このコールバック関数を`console.log(getNumber());`で呼び出して実行しています。  
このように **即時実行するのではなく、後々実行するための関数を定義することができます。**

これが`withSuccessHandler`メソッドとどのように関係があるのか？といいますと、  
これらのメソッドは　**クライアントサイドからGAS関数を呼び出した後の処理を設定できる** のですが、  
GAS関数を呼び出した後の処理をコールバック関数で定義することができるのです。

#### withSuccessHandlerとは
GAS関数（サーバーサイドの関数）が **正常に完了** して戻り値が返ってきた場合に、  
実行する関数を定義することができます。  
コーディングの仕方は下記の通りです。
```
google.script.run.withSuccessHandler(コールバック関数).GAS関数()
```
それでは、シートから値を取得する`getSheetData()`を同期処理で取得してアラートでその値を表示してみましょう。 
先ほどは`undefined`と返ってきましたが、シートのA1セルの値が表示されれば成功です。

{{< tabs groupId="web_6_9" >}}
{{% tab name="index.html" %}}
```html
<script>
　function outputResult(result) {
    console.log(result);
  }
  google.script.run.withSuccessHandler(outputResult).getSheetData();
</script>
```
{{% /tab %}}
{{< /tabs >}}
上記のコードは下記のようにコールバック関数を`withSuccessHandler`メソッドの引数として設定してコーディングすることができます。  
（少しコードの量が少なくなりますね！）

{{< tabs groupId="web_6_10" >}}
{{% tab name="index.html" %}}
```html
<script>
  google.script.run.withSuccessHandler(function(result){
    console.log(result);
  }).getSheetData();
</script>
```
{{% /tab %}}
{{< /tabs >}}
