---
title: "let・const キーワード"
date: 2021-04-03T23:54:33+09:00
pre: "<b>1. </b>"
weight: 1
---
## 新しい変数の宣言
これまで変数を宣言する際は var キーワードを使用してきましたが、es2015からは let キーワードと const キーワードで宣言することができるようになりました。  
ここでは、それぞれのキーワードで宣言した場合の違いに学んでいきましょう。

## 変数宣言の種類
これから var ・ let ・ const の違いを確認していきますが、今後のコーディングは以下の前提で行うようにしましょう。
- 原則 const で宣言しましょう。
- ループ処理などの変数を更新する場合限っては let で宣言しましょう。
- var では宣言しないようにしましょう。

以下の表は、var ・ let ・ const の違いを一覧にまとめたものです。

||  var  |  let  |  const  |
| ---- | ---- | ---- | ---- |
|  再宣言  |  可  |  不可  |  不可  |
|  再代入  |  可  |  可  |  不可  |
|  スコープの種類  |  関数スコープ  |  ブロックスコープ  |  ブロックスコープ  |
|  変数の巻き上げ  |  undefined  |  ReferenceError が発生する  | ReferenceError が発生する |

### var キーワード
#### var キーワードでの変数の再宣言・再代入
varキーワードで宣言した変数は再宣言・再代入をすることができます。
```js
function var_pattern_1() {
  // var での再宣言
  var value = 1;
  var value = 2;
}
function var_pattern_2() {
  // var での再代入
  var value = 1;
  value = 2;
}
```
#### var キーワードでの変数のスコープ
varキーワードで宣言したローカル変数は `関数スコープ` となります。  
関数スコープの場合は関数内であれば宣言したブロックが異なっていても参照することができます。
```js
function var_pattern_3() {
  let isLoop = true;
  while(isLoop){
    // value 変数を宣言したのちループ処理を抜ける
    var value = 1;
    isLoop = false;
  }
  // ブロックスコープが適用されないため value 変数を参照できる
  console.log(value); // 1
}
```
#### var キーワードでの変数の巻き上げ
先述の通り、 var キーワードで宣言されたローカル変数は同関数内であれば参照することができます。
実は宣言の前からでも参照することができるのです。  
この事象は「巻き上げ（hosting）」と呼ばれています。  
以下のサンプルコードをでは、1回目の`console.log()`でパラメーターに value 変数を渡していますが、実行時点では value 変数は宣言されていません。  
実行してもエラーは発生しませんが、1回目の`console.log()`でログに表示されるのは`undefined`となります。  
```js
function var_pattern_4() {
  console.log(value); // undefined
  var value = 1;
  console.log(value); // 1
}
```
変数の巻き上げで注意すべきは巻き上げが発生してもエラーとして扱われない点です。  
変数の巻き上げに気づかず、そのまま処理を実行することにより期待しない処理が行われる可能性があります。  
一方、後述する let・const キーワードでローカル変数を宣言した場合は変数の巻き上げは発生せずエラーが発生します。  
**変数の巻き上げを未然に防ぐためにも、変数は let・const キーワードで宣言するようにしましょう。**  
{{% notice warning %}}
JavaScriptでは関数内で宣言されたローカル変数は、すべてその関数の先頭で宣言されたものとみなされます。
{{% /notice %}}

### let キーワード
#### let キーワードの再宣言・再代入
letキーワードで宣言したローカル変数は再宣言することはできませんが、再代入することはできます。  
letキーワードで宣言したローカル変数を再宣言するようにコーディングすると、保存する際に JavaScript の文法が間違っているという意味の`構文エラー（SyntaxError）`が発生します。
```js
function let_pattern_1() {
  // let での再宣言
  // 保存時にエラー発生　構文エラー: SyntaxError: Identifier 'value' has already been declared
  let value = 1;
  //let value = 2;
}
function let_pattern_2() {
  // let での再代入
  let value = 1;
  value = 2;
}
```
#### let キーワードのスコープ
letキーワードで宣言したローカル変数は `ブロックスコープ` となります。  
ブロックスコープの場合はブロック内であれば宣言したローカル変数を参照することができますが、同じ関数であってもブロック外からは参照することができません。
```js
function let_pattern_3() {
  let isLoop = true;
  while(isLoop) {
    // value 変数を宣言したのちループ処理を抜ける
    let value = 1;
    isLoop = false;
  }
  // ブロックスコープが適用されるため value 変数を参照できない
  // 実行時にエラー発生 ReferenceError: value is not defined
  console.log(value);
}
```
#### let キーワードの変数の巻き戻し
let キーワードでローカル変数を宣言した場合は変数の巻き戻しは発生しません。  
代わりに実行する際に参照する変数が見つからないという意味の `参照エラー（ReferenceError）`が発生します。
```js
function let_pattern_4() {
  console.log(value);
  let value = 1;
  // 実行時にエラー発生 ReferenceError: Cannot access 'value' before initialization
  console.log(value);
}
```
### const キーワード
#### const キーワードの再宣言・再代入
constキーワードで宣言したローカル変数は再宣言・再代入ができません。
```js
function const_pattern_3() {
  let isLoop = true;
  while(isLoop) {
    // value 変数を宣言したのちループ処理を抜ける
    const value = 1;
    isLoop = false;
  }
  // ブロックスコープが適用されるため value 変数を参照できない
  // 実行時にエラー発生 ReferenceError: value is not defined
  console.log(value);
}
```
#### const キーワードのスコープ
constキーワードで宣言したローカル変数は、letキーワードと同じく `ブロックスコープ` となります。  
そのため、ブロック内であれば宣言したローカル変数を参照することができますが、同じ関数であってもブロック外からは参照することができません。
```js
function const_pattern_4() {
  console.log(value);
  const value = 1;
  // 実行時にエラー発生 ReferenceError: Cannot access 'value' before initialization
  console.log(value);
}
```
#### const キーワードの変数の巻き戻し
let キーワードと同様に、const キーワードでローカル変数を宣言した場合は変数の巻き戻しは発生しません。  
代わりに実行する際に参照する変数が見つからないという意味の `参照エラー（ReferenceError）`が発生します。
```js
function const_pattern_4() {
  console.log(value);
  const value = 1;
  // 実行時にエラー発生 ReferenceError: Cannot access 'value' before initialization
  console.log(value);
}
```
