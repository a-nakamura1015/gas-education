---
title: "HTMLを学ぼう"
date: 2021-06-07T03:01:16+09:00
pre: "<b>3. </b>"
weight: 3
---
### HTMLとは
本章では、先ほどWeb画面を表示するのに使用したHTMLファイルについて掘り下げていきます。  
HTMLは Hyper Text Markup Language の略で、Webページの構造に作ることができます。  
ChromeをはじめとするブラウザはこのHTMLを読み取って画面を形成して表示します。  

また、HTMLは要素で様々な項目を表現することができ、この要素を **タグ** で記述することができます。  
HTMLには様々なタグがあるのですが、今回はその中で代表的なタグの使い方を学んでいきましょう。  

まずは、既に作成している以下のHTMLファイルに登場しているタグから確認していきましょう。  
{{< tabs groupId="web_2_4" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    Web画面を変更しました!
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}

### htmlタグ
HTMLの文章であることを指定するタグであり、このタグで囲われた部分がHTMLを記述することができる範囲になります。  
この範囲に様々なタグを記述することができます。

### headタグ
文書のヘッダ部分を意味するタグで、このタグで囲われた範囲でHTMLファイルの情報を宣言することができます。  
後ほど学ぶことになる装飾の情報であるCSSはこの範囲で定義することになります。  

### bodyタグ
ブラウザの画面上に表示する内容を指定するタグです。このタグの中に書かれた内容が画面に表示されます。

ここからはbodyタグ内に書くことができるタグを学んでいきましょう。  
サンプルコードを書いて、Web画面で確認しながら進めていきましょう。

### divタグ
単体では意味をなさないタグですが、同タグで囲った部分をグループ化することができます。  
divタグで囲むことで文章の改行を表現することもできます。  
{{< tabs groupId="web_2_5" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <div>1つ目</div>
    <div>2つ目</div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_1.png](../img/page_3_1.png)

### brタグ
「Break」の略で、文章を改行することができるタグです。終了タグが必要ないことが特徴です。
{{< tabs groupId="web_2_6" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    1行目<br>2行目
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_2.png](../img/page_3_2.png)

### pタグ
「Paragraph」の略で、このタグに囲まれた文章は1つの段落（文章の塊）になります。  
pタグによってできる改行と、brタグによってできる改行とでは見た目が若干異なるのでうまく使い分けましょう。  
{{< tabs groupId="web_2_7" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <p>こんにちは、山田太郎です！</p>
    <p>好きなものはプログラミングで、<br>嫌いなものは静電気です。</p>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_3.png](../img/page_3_3.png)

### tableタグ、thタグ、trタグ、tdタグ
Web画面に表を作りたい場合はtableタグ内にthタグやtrタグ、tdタグを記述することで作ることができます。  
それぞれのタグは以下の意味を持ちます。
| 名称 | タグの意味 |
| --- | --------- |
| thタグ | ヘッダー行（テーブルの先頭行） |
| trタグ | 表の1行分のデータ |
| tdタグ | 表の1セル分のデータ |

各タグを以下のように記述することで表を作ることができます。  
```html
<table>
  <tr>
    <th>ヘッダー１</th>
    <th>ヘッダー２</th>
    <th>ヘッダー３</th>
  </tr>
  <tr>
    <td>A1</td>
    <td>B1</td>
    <td>C1</td>
  </tr>
  <tr>
    <td>A2</td>
    <td>B2</td>
    <td>C2</td>
  </tr>
</table>
```

それでは、以下のサンプルコードを書いて、表を作ってみましょう。
{{< tabs groupId="web_2_7" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <table>
      <tr>
        <th>ヘッダー１</th>
        <th>ヘッダー２</th>
        <th>ヘッダー３</th>
      </tr>
      <tr>
        <td>A1</td>
        <td>B1</td>
        <td>C1</td>
      </tr>
      <tr>
        <td>A2</td>
        <td>B2</td>
        <td>C2</td>
      </tr>
    </table>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_4.png](../img/page_3_4.png)

### inputタグ
ここまでは画面に表示する項目を作ってきましたが、inputタグはテキストの入力欄やボタンなどユーザーが操作することができるアイテムを作ることができます。  
type属性に設定された値によって表示されるアイテムは変わります。
また、これらのinputタグは **formタグ** でグループ化することができます。

#### text属性
type属性に`text`を指定するとテキストの入力欄（テキストボックス）を作ることができます。  
また、value属性に値を入れると、入れた値が初期値として設定されます。
{{< tabs groupId="web_2_8" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <form>
      <input type="text" value="初期値">
    </form>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_5.png](../img/page_3_5.png)

#### password属性
type属性に`password`を指定するとパスワードを入力するための入力欄を作ることができます。  
入力した文字が確認できないのが特徴です。
{{< tabs groupId="web_2_9" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <form>
      <input type="password" value="abc123">
    </form>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_6.png](../img/page_3_6.png)

#### radio属性
type属性に`radio`を指定すると、複数の選択肢から1つだけを選択できるラジオボタンを作ることができます。 
{{< tabs groupId="web_2_10" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <form>
      <input type="radio" value="A">Aコース
      <input type="radio" value="B">Bコース
    </form>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_7.png](../img/page_3_7.png)

#### checkbox属性
type属性に`checkbox`を指定すると、複数の選択肢から複数を選択できるチェックボックスを作ることができます。 
{{< tabs groupId="web_2_11" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <form>
      <input type="checkbox" value="A">Aコース
      <input type="checkbox" value="B">Bコース
    </form>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_8.png](../img/page_3_8.png)

#### button属性
type属性に`button`を指定すると、クリックできるボタンを作ることができます。 
value属性に値を設定すると、その値がボタンの名前として表示されます。
{{< tabs groupId="web_2_12" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <form>
      <input type="button" value="ボタン">
    </form>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_3_9.png](../img/page_3_9.png)

### コメント
HTMLでも、JavaScriptと同様にコメントを残すことができます。  しかし、コメントの記法がJavaScriptとは異なるため注意が必要です。  
`<!-- -->`で囲まれた部分はブラウザには表示されないため、残しておきたいメモ書きやタグの一時的な無効化などをしたいときに活用できます。
```html
<!-- １行分のコメント -->
<!--
1行目のコメント
2行目のコメント
-->
```
