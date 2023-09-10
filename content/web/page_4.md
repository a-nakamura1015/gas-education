---
title: "CSSを学ぼう"
date: 2021-06-07T05:05:23+09:00
pre: "<b>4. </b>"
weight: 4
---
### CSSとは
CSSはWebページの装飾をすることができます。これまでは質素なデザインのWebページしか作ることができませんでしたが、  
CSSを活用すると自由にWebページのレイアウトを設定できるようになります。
CSSは Cascading Style Sheetsの略で、以下のいずれかの方法でCSSを書くことができます。  
- 外部ファイルのCSSファイルを作成して書く
- styleタグの範囲内に書く

GASプロジェクトではGSファイルか、HTMLファイルしか作れないため、  
必然的に「styleタグの範囲内に書く」ことになります。
styleタグは以下のようにheadタグ内に書くことができます。
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
    </style>
  </head>
  <body>
  </body>
</html>
```

CSSを活用するにあたり、HTMLのidとclassの使い分けを理解する必要があります。  
colorプロパティで実際に文字の色を変えながら確認してみましょう。

### HTMLのid属性
id属性は任意の1つのタグを特定するために使用します。そのため、HTMLファイル内でid属性は重複しないようにすることが望ましいです。
以下のサンプルコードでは、Aコースは赤色、Bコースは青色となるようにCSSを設定しています。  
id属性を指定してCSSを設定する場合は、id属性の前に **#** を付けます。
{{< tabs groupId="web_4_1" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      #A {
        color: red;
      }
      #B {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div id="A">
      Aコース
    </div>
    <div id="B">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_1.png](../img/page_4_1.png)

### HTMLのclass属性
class属性は複数のタグをグループ化するために使用します。そのため、HTMLファイル内でclass属性が重複しても問題はありません。  
以下のサンプルコードでは、AコースもBコースも同じclass属性のため同じCSSが適用されます。  
class属性を指定してCSSを設定する場合は、class属性の前に **.** を付けます。
{{< tabs groupId="web_4_2" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      .course {
        color: red;
      }
    </style>
  </head>
  <body>
    <div class="course">
      Aコース
    </div>
    <div class="course">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_2.png](../img/page_4_2.png)

{{% notice note %}}
1つのタグにid属性とclass属性の両方を設定することもできますが、この場合はclass属性よりもid属性の方が優先されます。
{{% /notice %}}

それでは代表的なCSSを実際に書いてみましょう。

### colorプロパティ
テキストの色を指定することができるプロパティです。  
色の種類は英字で指定することができますが、カラーコードで指定することもできます。  
カラーコードは # の後ろに6文字の英数字の形式で書くことができます。
{{< tabs groupId="web_4_3" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      .course {
        color: #4b0082;
      }
    </style>
  </head>
  <body>
    <div class="course">
      Aコース
    </div>
    <div class="course">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_3.png](../img/page_4_3.png)

### background-colorプロパティ
背景の色を指定することができるプロパティです。  
色の指定方法はcolorプロパティと同じです。
{{< tabs groupId="web_4_4" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      #A {
        background-color: #fa8072;
      }
      #B {
        background-color: #6495ed;
      }
    </style>
  </head>
  <body>
    <div id="A">
      Aコース
    </div>
    <div id="B">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_4.png](../img/page_4_4.png)

### font-sizeプロパティ
文字の大きさを指定することができるプロパティです。  
大きさの指定方法は 数値+単位(px, %, pt, em) です。
{{< tabs groupId="web_4_5" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      #A {
        font-size: 20px;
      }
      #B {
        font-size: 50px;
      }
    </style>
  </head>
  <body>
    <div id="A">
      Aコース
    </div>
    <div id="B">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_5.png](../img/page_4_5.png)

### widthプロパティ、heightプロパティ
widthプロパティで幅を、heigthプロパティで高さを設定することができます。  
大きさの指定方法はfont-sizeプロパティと同じく、 数値+単位(px, %, pt, em) です。  
※ 目視でわかりやすいように背景色も設定しています。 複数のプロパティを設定する場合は、プロパティの最後をセミコロンにする必要があります。 
{{< tabs groupId="web_4_6" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      #A {
        background-color: #fa8072;
        width: 100px;
      }
      #B {
        background-color: #6495ed;
        height: 50px;
      }
    </style>
  </head>
  <body>
    <div id="A">
      Aコース
    </div>
    <div id="B">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_6.png](../img/page_4_6.png)

### marginプロパティ、paddingプロパティ
marginプロパティは内側の余白、paddingプロパティは外側の余白を設定することができます。  
大きさの指定方法はfont-sizeプロパティと同じく、 数値+単位(px, %, pt, em) です。
{{< tabs groupId="web_4_6" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      .course {
        margin: 100px;
        padding: 50px;
      }
    </style>
  </head>
  <body>
    <div class="course">
      Aコース
    </div>
    <div class="course">
      Bコース
    </div>
  </body>
</html>
```
{{% /tab %}}
{{< /tabs >}}
![page_4_7.png](../img/page_4_7.png)

{{% notice info %}}
Web画面で右クリックして、メニュー内の「検証」を選択すると要素に設定されている余白を確認できます。
![page_4_8.png](../img/page_4_8.png)
{{% /notice %}}

### borderプロパティ
表の上下左右のボーダーラインの太さ、色などを一括でまとめて指定することができるプロパティです。  
プロパティ名を指定したのち、ボーダーラインの太さ・ボーダーラインの種類・ボーダーラインの色の順に指定します。
| 設定の種類 | 指定方法 |
| --------- | ------ |
| ボーダーラインの太さ | 数値+単位(px, pt, em) |
| ボーダーラインの種類 | solid : 実線　double：二重線　dotted：点線 dashed：破線 など|
| ボーダーラインの色 | 文字の色の英字やカラーコード |

また、borderプロパティのみで、テーブルのレイアウトを設定すると線と線の間に隙間ができてしまいます。  
隙間を無くして1つの線にしたい場合はtableに **border-collapse: collapse** を指定する必要があります。

これまではid属性もしくはclass属性を使用してCSSを適用してきましたが、実はタグ名で指定することもできます。  
以下のように「tableのth」の場合は`table th`、「tableのtd」の場合は`table td`と指定します。  
また、複数の要素に対して同じCSSを適用する場合は要素間をカンマで区切ります。

{{< tabs groupId="web_4_9" >}}
{{% tab name="index.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <style>
      table {
        border-collapse: collapse;
      }
      table th, table td {
        border: 3px solid red
      }
    </style>
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
![page_4_9.png](../img/page_4_9.png)

### コメント  
CSSもJavaScriptと同様にコメントを書くことができます。  
記法はJavaScriptと同じで、1行のみの場合は `//`、複数行の場合は`/** **/`で記述することができます。
```html
<style>
  // テーブルの線を1つにまとめる
  table {
    border-collapse: collapse;
  }
  /**
    * テーブルのヘッダーとデータに以下のスタイルを設定する
    * ・太さは3px
    * ・種類は実線
    * ・色は赤色
    */
  table th, table td {
    border: 3px solid red
  }
</style>
```
