---
title: "for...of文"
date: 2021-05-23T21:49:51+09:00
pre: "<b>6. </b>"
weight: 6
---
## 繰り返し処理をよりシンプルに書く
Chapter2-3の「JavaScriptの制御構文」で for文 に触れましたが、  
ES2015からはよりシンプルに書くことができる**for...of文**を使えるようになりました。  
構文は以下の通りで、宣言した変数の中には配列の要素が代入され、配列の先頭の要素から最後の要素まで繰り返されます。
```js
for (変数名 of 配列) {
  // 繰り返す処理
}
```
以下のサンプルコードでfor...of文を試してみましょう。  
配列の要素が`value`変数に代入されることが確認できます。
```js
function for_of_1() {
  const values = ['A', 'B', 'C'];
  for (const value of values) {
    console.log(value);
  }
}
```Â
```
A
B
C
```
for...of文は原則最後の要素まで繰り返し処理を行いますが、  
`break文`で繰り返し処理を抜けることができます。
```js
function for_of_2() {
  const values = ['A', 'B', 'C'];
  for (const value of values) {
    console.log(value);
    break;
  }
}
```
```
A
```
## index...in文
index...of文とよく似た構文で**index...in文**があります。  
index...of文と同じく、配列の先頭の要素から最後の要素まで繰り返されますが、  
宣言した変数には**インデックス番号**が代入されます。
```js
for (変数名 in 配列) {
  // 繰り返す処理
}
```
以下のサンプルコードで宣言した変数にインデックス番号が代入されていることを確認してみましょう。
```js
function for_in_1() {
  const values = ['A', 'B', 'C'];
  for (const index in values) {
    console.log(index);
    console.log(values[index]);
    console.log('---');
  }
}
```
```
0
A
---
1
B
---
2
C
---
```
また、配列ではなく連想配列を指定すると、宣言した変数にはキー（オブジェクトのプロパティ名）が代入されます。
```js
function for_in_2() {
  const account = {
    id: 1,
    name: 'Taro',
    age: 20
  }
  for (const property in account) {
    console.log(property);
    console.log(account[property]);
    console.log('---');
  }
}
```
```
id
1
---
name
Taro
---
age
20
---
```
