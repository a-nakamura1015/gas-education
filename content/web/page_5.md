---
title: "クライアントサイドのJavaScriptを学ぼう"
date: 2021-06-07T05:05:37+09:00
pre: "<b>5. </b>"
weight: 5
---
### クライアントサイドのJavaScript
ここまではGSファイルにJavaScriptを書いてきましたが、実はHTMLファイルにもJavaScritを書くことができます。  
HTMLファイルでJavaScriptを書ける場所は決まっており、**scriptタグ** の中に書くことができます。  
また、このscriptタグも書くことができる場所が決まっています。  
#### JavaScriptを書くことができる場所
scriptタグを書くことができるのは主に以下の2つの場所になります。
1つ目はheadタグの中でstyleタグと同様の場所に書くことができます。
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      // CSSを記述する
    </style>
    <script>
      // JavaScriptを記述する
    </script>
  </head>
  <body>
  </body>
</html>
```

2つ目はbodyタグの中です。
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      // CSSを記述する
    </style>
  </head>
  <body>
    <div>Sample</div>
    <script>
      // JavaScriptを記述する
    <script>
  </body>
</html>
```

それでは、早速クライアントサイドの JavaScript をコーディングしてみましょう。  
今回は Google Chrome のコンソールログに「Hello!」と表示をしてみます。
```js
console.log('Hello!');
```

{{< tabs groupId="web_5_1" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      console.log('Hello!');
    </script>
  </head>
  <body>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}

Google Chrome のコンソールログは以下の手順で確認できます。  
1. ブラウザ右上「︙」をクリックします。
1. 表示されたメニューから[その他のツール]→[デベロッパーツール]をクリックします。
1. デベロッパーツール内の「Console」タブを選択します。

![page_5_1.png](../img/page_5_1.png)

続いて、ボタンをクリックした際にコンソールログに「Hello!」と表示をしてみましょう。
任意のタイミングで処理をさせたい場合は関数として定義する必要があります。  
次のサンプルではボタンをクリックした際に`viewMessage()`が実行されるように、  
inputタグの `onclick` に`viewMessage()`を設定しています。

{{< tabs groupId="web_5_2" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function viewMessage() {
        console.log('ボタンをクリックしました！');
      }
    </script>
  </head>
  <body>
    <input type="button" value="メッセージを表示する" onclick="viewMessage()">
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}

![page_5_2_1.png](../img/page_5_2_1.png)
![page_5_2_2.png](../img/page_5_2_2.png)

### サーバーサイドのJavaScriptとの違い
クライアントサイドもサーバーサイドも同じ JavaScript をコーディングしていますが、  
コーディングできる処理はそれぞれ異なります。  

サーバーサイドはGoogle の各種サービスを操作する Google Apps Script を実行することはできますが、  
画面の値や色を変えたりなどの画面側の処理を行うことができません。  
画面側の処理を行いたい場合は .gs ではなくHTMLのスクリプトタグ内にコーディングをしていきます。

### HTMLの要素を操作する
クライアントサイドのJavaScriptで画面を操作するには対象の画面の部品を特定する必要があります。  
画面の各部品には`id`を設定することができるため、この`id`で部品を特定することができます。  
以下のサンプルでは`viewMessage()`でテキストボックスの入力した値を取得してコンソールログに出力していますが、  
`document.getElementById()`で対象のテキストボックスを取得しています。

{{< tabs groupId="web_5_3" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function viewMessage() {
        // idが’textBox’の要素を取得します。
        const textBox = document.getElementById('textBox');
        // 取得した要素から値を取得します。
        const value = textBox.value;
        // コンソールログで取得した値を表示します。
        console.log(value);
      }
    </script>
  </head>
  <body>
    <input type="text" id="textBox">
    <input type="button" value="メッセージを表示する" onclick="viewMessage()">
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_5_3_1.png](../img/page_5_3_1.png)
![page_5_3_2.png](../img/page_5_3_2.png)

クライアントサイドの JavaScript は画面から情報取得することだけでなく、  
画面を変化させることもできます。  
以下のサンプルではテキストボックスに入力した内容を画面に出力しています。

{{< tabs groupId="web_5_4" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function viewMessage() {
        // idが’textBox’の要素を取得します。
        const textBox = document.getElementById('textBox');
        // 取得した要素から値を取得します。
        const value = textBox.value;
        // 取得した値を太字にします。
        const output = `<b>${value}</b>`;
        // 出力先の要素を取得します。
        const outputArea = document.getElementById('outputArea');
        // 出力先の要素に値を追加します。
        outputArea.innerHTML = output;
      }
    </script>
  </head>
  <body>
    <input type="text" id="textBox">
    <input type="button" value="メッセージを表示する" onclick="viewMessage()">
    <div id="outputArea"></div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_5_4.png](../img/page_5_4.png)

### CSSを操作する
クライアントサイドの JavaScript は画面の見た目も変えることができます。  
以下のサンプルでは CSS の設定を JavaScript で変えています。

{{< tabs groupId="web_5_5" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      #colorBtn {
        background-color: blue;
        color: white;
        font-size: 15px;
      }
    </style>
    <script>
      function changeColor() {
        // idが'colorBtn'の要素を取得する。
        const colorBtn = document.getElementById('colorBtn');
        // 取得した要素の背景色を赤色に変更する。
        colorBtn.style.backgroundColor = 'red';
      }
    </script>
  </head>
  <body>
    <input type="button" id="colorBtn" value="色を変える" onclick="changeColor()">
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
＜ボタンのクリック前＞
![page_5_5_1.png](../img/page_5_5_1.png)
＜ボタンのクリック後＞
![page_5_5_2.png](../img/page_5_5_2.png)

### 画面にダイアログを表示する
画面上にポップアップでメッセージを表示したい場合は`dialogタグ`を使いましょう。  
以下のサンプルでは画面表示時に閉じるボタン付きのダイアログを表示しています。

{{< tabs groupId="web_5_6" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <dialog id="alert">
      <p id="alert-message"></p>
      <div>
        <button id="alert-closeBtn" value="閉じる">
      </div>
    </dialog>
    <script>
      function showAlert() {
        var dialog = document.getElementById('alert');
        var dialogMsg = document.getElementById('alert-message');
        var dialogCloseBtn = document.getElementById('alert-closeBtn');
        dialogMsg.innerHTML = 'こんにちは！';
        // 閉じるボタンをクリックした時の処理
        var closedFnc = function() {
          dialog.close();
        }
        dialogCloseBtn.addEventListener('click', closedFnc);
      }
    </script>
  </body>
</html>

```
{{% /tab %}}
{{% tab name="コード.gs" %}}
```js
function doGet() {
  return HtmlService.createTemplateFromFile('index').evaluate();
}
```
{{% /tab %}}
{{< /tabs >}}

![page_5_6.png](../img/page_5_6.png)
