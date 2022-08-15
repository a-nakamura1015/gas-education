---
title: "テンプレート文字列"
date: 2021-05-22T21:04:21+09:00
pre: "<b>2. </b>"
weight: 2
---
## 文字列に挿入する
ES2015までは変数の値と文字列を`console.log()`で出力したい場合は、以下のように`+記号`で結合をする必要がありました。
```js
const name = 'Taro';
console.log('My name is ' + name +'.');
```
ES2015からは`テンプレート文字列`で文字列の中にプレースホルダを挿入することができます。  
＊）プレースホルダとは変数の中身を置き換えることができる文字列のことです。  
構文は以下の通りで　\`（バッククォート）で囲み、$（ドル記号）と{}（波括弧）で作ることができます。  
\`（バッククォート）と '（シングルクォート）は全く別の文字になるため注意が必要です。
```js
`${変数名や計算式などのリテラル}`
```
では、サンプルコードで確認をしてみましょう。  
波括弧の中に変数名を指定することで、変数に格納されている値を文字列に挿入することができます。
{{< tabs groupId="es2022_10" >}}
{{% tab name="コード.gs" %}}
```js
function template_literals_1() {
  const name = 'Taro';
  console.log(`My name is ${name}.`);
}
```
{{% /tab %}}
{{< /tabs >}}
```
My name is Taro.
```
波括弧の中には値や変数だけでなく四則演算子も指定できます。  
そのため、以下のように計算式を指定することもできます。
{{< tabs groupId="es2022_11" >}}
{{% tab name="コード.gs" %}}
```js
function template_literals_2() {
  const num1 = 1;
  const num2 = 2;
  console.log(`Result:${num1 + num2}`);
}
```
{{% /tab %}}
{{< /tabs >}}
```
Result:3
```
また、テンプレート文字列内で改行をすると、文字列を複数行にすることもできます。
{{< tabs groupId="es2022_12" >}}
{{% tab name="コード.gs" %}}
```js
function template_literals_3() {
  console.log(`1行目
2行目`);
}
```
{{% /tab %}}
{{< /tabs >}}
```
1行目
2行目
```
