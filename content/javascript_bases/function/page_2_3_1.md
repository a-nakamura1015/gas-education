---
title: "宣言と呼び出し"
date: 2020-08-10T13:50:55+09:00
pre: "<b>1. </b>"
weight: 1
---

### 関数の呼び出し
おさらいまでに、**関数** とは一連の処理をひとつにまとめたものをいいます。
関数については先ほどご紹介しているので下記を参考にしてください。

[関数とは](../../basic_syntax/page_2_1_2)

これまでは関数を実行する際は、スクリプトエディタのツールバーの「関数を選択」のプルダウンで選択した関数から実行してきました。
実は、関数は「関数を選択」で選択して実行するだけでなく、関数名で **別の関数から呼び出す** ことができます。
```js
関数名()
```
次のサンプルは他の関数を呼び出す例です。`myFunc_1`を実行すると、ログには「おはようございます！」と「こんにちは！」、「こんばんは！」が出力されます。
{{< tabs groupId="function_1" >}}
{{% tab name="コード.gs" %}}
```js
function myFunc_1() {
  console.log('おはようございます！');
  myFunc_2(); // myFunc_2関数を呼び出す
  console.log('こんばんは！');
}
function myFunc_2() {
  console.log('こんにちは！');
}
```
{{% /tab %}}
{{< /tabs >}}
```
おはようございます！
こんにちは！
こんばんは！
```

JavaScriptにおいて関数はオブジェクトとして扱われます。
そのため、他のオブジェクトと同じように引数として関数に渡したり、変数に代入したりすることができます。
重要なポイントとして押さえてほしいのは、関数の「呼び出し」と「参照」がしっかり区別されるということです。
関数名に()をつけることでその関数の呼び出しとなり、関数が実行されて値が返されます。
一方、()をつけずに関数名だけを書くと、その関数を参照しているだけになります。
また、関数は参照されるだけで実行されません。

次の例は`getMessage()`で関数の「呼び出し」を行い、
`getMessage`で関数の「参照」を行っています。
このように関数を呼び出さずに参照することができるのですが、
この関数の「参照」を利用することでオブジェクトとして扱うことができます。
（オブジェクトについては[次章](../../object_mechanism/page_2_4_1)で解説します。）
{{< tabs groupId="function_2" >}}
{{% tab name="コード.gs" %}}
```js
function getMessage() {
  return 'Hello!';
}

console.log(getMessage()); // Hello!
console.log(getMessage);   // [Function: getMessage]
```
{{% /tab %}}
{{< /tabs >}}
続いて、「変数（定数）への代入」を試してみましょう。
関数を変数に代入することで、関数を別の名前で呼び出すことができます。

{{< tabs groupId="function_3" >}}
{{% tab name="コード.gs" %}}
```js
function getMessage() {
  return 'Hello!';
}

var message = getMessage; // 関数をmessage変数に代入
console.log(message());   // Hello!
```
```
{{% /tab %}}
{{< /tabs >}}

{{% notice tip %}}
同じプロジェクト内であれば、別のgsファイルに記述した関数も呼び出すことができます。
{{% /notice %}}
この例でわかるように、関数を呼び出した場合はその呼び出した関数の処理が完了した時点で元の関数に戻ります。
