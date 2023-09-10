---
title: "アロー関数"
date: 2021-05-22T23:29:17+09:00
pre: "<b>3. </b>"
weight: 3
---
## 関数宣言の省略
これまで、関数を宣言するときは`function() {}`で表記してきましたが、  
ES2015では「アロー関数」という表記法が追加されて以下の構文で関数を宣言できるようになりました。  
アロー関数は無名関数であり、アロー（矢）のように見える`=>`が特徴的ですね。
```js
() => {};
```
これまでの関数の宣言方法と比べると、以下の違いがあり簡略化ができるようになりました。  
- キーワードの`function`を省略できる。
- 引数がひとつの場合は`()`を省略できる。
- 関数が1行の場合は`{}`と`return`を省略できる。

以下は関数内に通常の記法で宣言した関数（f1）とアロー関数として宣言した関数（f2）を実行するサンプルです。
{{< tabs groupId="es2022_13" >}}
{{% tab name="コード.gs" %}}
```js
function arrow_functions_1() {
  const f1 = function() {
    return 'normal function';
  };
  console.log(f1());
  const f2 = () => 'arrow function';
  console.log(f2());
}
```
{{% /tab %}}
{{< /tabs >}}
```
normal function
arrow function
```
先程のサンプルは関数内の処理が1行のみでしたが、アロー関数で複数行の処理をコーディングしたい場合は`{}`が必要になります。  
また、値を返したい場合は`return`も必要になります。
{{< tabs groupId="es2022_14" >}}
{{% tab name="コード.gs" %}}
```js
function arrow_functions_2() {
  const f3 = () => {
    const str = 'arrow function';
    return str;
  }
  console.log(f3());
}
```
{{% /tab %}}
{{< /tabs >}}
```
arrow function
```
## 関数に仮引数がある場合
関数が呼び出し元から値を受け取れるように仮引数を指定する場合、通常関数は以下のように書いていました。
```js
function(仮引数名1{, 仮引数名2, ...}){};
```
一方、アロー関数は以下のように書きます。仮引数が1つの場合は`()`を省略することができます。
```js
// 仮引数が1つの場合
(仮引数名) => {};
// 仮引数が1つの場合（省略記法）
仮引数名 => {};
// 仮引数が複数の場合
(仮引数名1{, 仮引数名2, ...}) => {};
```
以下のサンプルを実行し、通常の関数もアロー関数もともに値を受け取れることを確認してみましょう。
{{< tabs groupId="es2022_15" >}}
{{% tab name="コード.gs" %}}
```js
function arrow_functions_3() {
  const name = 'Taro';
  const f1 = function(str) {
    console.log(`My name is ${str}.`);
  }
  f1(name);
  const f2 = str => console.log(`His name is ${str}.`);
  f2(name);
}
```
{{% /tab %}}
{{< /tabs >}}
```
My name is Taro.
His name is Taro.
```
通常の関数と同じく、アロー関数も仮引数を複数指定することができます。  
しかし、仮引数が1つのときと違って`()`が必要になります。
{{< tabs groupId="es2022_17" >}}
{{% tab name="コード.gs" %}}
```js
function arrow_functions_4() {
  const num1 = 1;
  const num2 = 2;
  const f1 = function(a, b) {
    console.log(`normal function: ${a + b}`);
  }
  f1(num1, num2);
  const f2 = (a, b) => console.log(`arrow function: ${a + b}`);
  f2(num1, num2);
}
```
{{% /tab %}}
{{< /tabs >}}
```
normal function: 3
arrow function: 3
```
## 通常の関数とアロー関数の違い
ここまではアロー関数を通常の関数と同様に使えると述べてきましたが、  
ここではアロー関数が通常の関数と異なる点について説明します。
### アロー関数に名前をつけることができない
アロー関数は無名関数のため、名前をつけることができません。  
そのため、アロー関数を実行するには変数に代入し、変数の後ろに`()`をつけて関数として実行する必要があります。  
名前付きの関数が必要な場合はこれまで通り通常の関数として宣言するようにしましょう。
### this の振る舞いが異なる
通常の関数の場合 thisはオブジェクトを指しますが、  
アロー関数のthis はグローバル領域に宣言したthisを指します。(もし、グローバル領域にthisがない場合、this は undefined になります。)
{{< tabs groupId="es2022_18" >}}
{{% tab name="コード.gs" %}}
```js
// グローバル領域にthis.nameを宣言
this.name = 'Ichiro';
function arrow_functions_5() {
  const person1 = {
    name: 'Taro',
    greet: function() {
      console.log(`Hello. My name is ${this.name}.`);
    }
  }
  person1.greet();
  const person2 = {
    name: 'Hanako',
    greet: () => console.log(`Hello. My name is ${this.name}.`)
  }
  person2.greet();
}
```
{{% /tab %}}
{{< /tabs >}}
```
Hello. My name is Taro.
Hello. My name is Ichiro.
```
先程の例はメソッドをアロー関数にすると this はグローバル領域を指してしまうという例でしたが、  
メソッドを通常の関数として宣言するとその関数内の this はオブジェクトを指してくれます。
{{< tabs groupId="es2022_19" >}}
{{% tab name="コード.gs" %}}
```js
function arrow_functions_6() {
  const person3 = {
    name: 'Hanako',
    greet: function() {
      // 通常関数内であればアロー関数でもthisはperson3オブジェクトを指してくれます。
      const getName = () => this.name;
      console.log(`My name is ${getName()}.`);
    }
  }
  person3.greet();
}
```
{{% /tab %}}
{{< /tabs >}}
```
Hello. My name is Hanako.
```

上記以外にも違いがあるので、詳細は以下リンク先の公式リファレンスを確認してみましょう。  
[アロー関数式 - MDN Web Docs](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
