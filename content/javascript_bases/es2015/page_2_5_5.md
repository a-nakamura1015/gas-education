---
title: "スプレッド構文"
date: 2021-05-23T17:15:08+09:00
pre: "<b>5. </b>"
weight: 5
---
## 配列の値を展開する
ES2015から**スプレッド構文**が使えるようになりました。  
スプレッド構文は配列やオブジェクトなどの反復可能なオブジェクトを展開してくれます。  
構文は配列やオブジェクトが格納されている変数や仮引数の前に`...`をつけることで展開することができます。
```js
...変数または仮引数
```
それでは「配列を展開する」とはどういうことかを確認してみましょう。  
以下のサンプルコードは数値の1、2、3が格納された配列を展開しています。
{{< tabs groupId="es2022_28" >}}
{{% tab name="コード.gs" %}}
```js
function spread_syntax_1() {
  const numbers = [1, 2, 3];
  console.log(numbers);
  // [1, 2, 3]を、1 2 3に展開する
  console.log(...numbers);
}
```
{{% /tab %}}
{{< /tabs >}}
```
[ 1, 2, 3 ]
1 2 3
```
この配列の展開を活用すると、以下のように引数を3つ受け取るSUM関数に対して引数を渡すことができます。  
本来は引数の値を3つ渡す必要があるため、numbers配列の要素を一つずつ取り出す必要があるのですが、  
スプレッド構文を使えばシンプルに書くことができます。
{{< tabs groupId="es2022_29" >}}
{{% tab name="コード.gs" %}}
```js
function spread_syntax_2() {
  const numbers = [1, 2, 3];
  // [1, 2, 3]を、1, 2, 3に展開する
  const result = sum(...numbers);
  console.log(result);
}
function sum(x, y, z) {
  return x + y + z;
}
```
{{% /tab %}}
{{< /tabs >}}
```
6
```
スプレッド構文を使えば、配列同士の結合も以下のように書くことができます。  
本来であれば配列の要素を取り出して結合する必要がありますが、スプレッド構文の場合はその必要がありません。
{{< tabs groupId="es2022_30" >}}
{{% tab name="コード.gs" %}}
```js
function spread_syntax_3() {
  const numbers_1 = [2, 3, 4];
  const numbers_2 = [1, ...numbers_1, 5, 6];
  console.log(numbers_2);
}
```
{{% /tab %}}
{{< /tabs >}}
```
[ 1, 2, 3, 4, 5, 6 ]
```
また、ここまでは配列で解説をしましたが、オブジェクトの要素も同様に展開することができます。
{{< tabs groupId="es2022_31" >}}
{{% tab name="コード.gs" %}}
```js
function spread_syntax_4() {
  const object_1 = {id: 1, name: 'Taro'};
  const object_2 = {...object_1, age: 25};
  console.log(object_2);
}
```
{{% /tab %}}
{{< /tabs >}}
```
{ id: 1, name: 'Taro', age: 25 }
```
