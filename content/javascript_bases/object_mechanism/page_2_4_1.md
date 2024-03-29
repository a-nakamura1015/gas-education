---
title: "オブジェクト"
date: 2020-08-10T13:58:59+09:00
pre: "<b>1. </b>"
weight: 1
---

## オブジェクトとは
オブジェクトは「物」や「対象」という意味ですが、  
プログラミングの世界では情報（属性）や機能を持ったデータの集合体という意味になります。  
配列もオブジェクトの一種になります。

本章ではJavaScriptの「オブジェクト指向」の入り口にあたる部分について解説していきます。  
「オブジェクト指向」というと難しく見えてしまい、できれば避けたいと思うかもしれませんが、  
GASの各サービスはこのオブジェクトの仕組みに忠実に構成されています。  

つまり、JavaScriptのオブジェクトの仕組みが理解できているのとそうでないのとでは、これからのJavaScriptとGASの習得スピードと理解度に明らかな差が出てきます。

## プロパティとメソッドとは
オブジェクトはプロパティと呼ばれるデータを持つことができます。
プロパティは属性とも呼ばれ、データを管理する役割を果たすことができます。

プロパティを理解するために、まずはオブジェクトの書式について確認してみましょう。  
オブジェクトは次のようなプロパティと値の組み合わせのデータの集合体です。  
以下のようなデータの集合体を`JSON（JavaScript Object Notation）`といいます。  
```js
{
  プロパティ１:値１,
  プロパティ２:値２
}
```
プロパティに設定した値は以下のようにして取得することができます。
```js
オブジェクト名.プロパティ
```

実際にJSONを作ってみましょう。次の例は学業の成績データをオブジェクトにしてみました。  
成績データ（result）は各科目の点数を格納しており、  
国語（japanese）・数学（math）・英語（english）の点数を持っています。
{{< tabs groupId="object_1" >}}
{{% tab name="コード.gs" %}}
```js
function object_1() {
  var result = {
    japanese: 100,
    math: 80,
    english: 90
  }
  console.log(result.japanese);
  console.log(result.math);
  console.log(result.english);
}
```
{{% /tab %}}
{{< /tabs >}}
```
100
80
90
```

プロパティは変数と同様に再代入することができます。  
次の例は成績データ（result）の国語（japanese）に0を再代入しています。
{{< tabs groupId="object_2" >}}
{{% tab name="コード.gs" %}}
```js
function object_2() {
  var result = {
    japanese: 100,
    math: 80,
    english: 90
  }
  console.log(result.japanese);
  result.japanese = 0;
  console.log(result.japanese);
}
```
{{% /tab %}}
{{< /tabs >}}
```
100
0
```

{{% notice tip %}}  
おそらく、プログラミング初心者にとっては`オブジェクト名.プロパティ`という記法が難しく感じられるかもしれません。  
そのような時は、`.`を`の`に置き換えるとしっくりくると思います。  
例えば、先程の例の成績データ（result）の国語（japanese）の点数を取得する際に`result.japanese`とコーディングしましたが、  
`resultのjapanase`と置き換えるとどうでしょう？  
こうすると、`成績データ（result）の国語（japanese）`と読めるようになると思います。  
{{% /notice %}}

実は、JSONにはオブジェクトの値として関数を持たせることができます。  
このように、オブジェクトの要素として関数を指定した場合は、その要素をプロパティとは呼ばずに **メソッド** と呼びます。  
以下のような要素がオブジェクトに含まれていれば、それがメソッドとなります。
```js
メソッド: function(仮引数１, 仮引数２, ...) {
  // 処理
  return 戻り値;
}
```
{{% notice note %}}
メソッドとは、関数が格納されたプロパティのことです。
{{% /notice %}}

プロパティを呼び出す場合と同様に、メソッドは以下のようにして呼び出すことができます。  
メソッドは関数のため、いくつかの引数を持つこともできます。
```js
オブジェクト名.メソッド(引数１, 引数２)
```

では、下記のサンプルで確認していきましょう。myGreetオブジェクトのsayHelloというメソッドを用意して呼び出しています。
{{< tabs groupId="object_3" >}}
{{% tab name="コード.gs" %}}
```js
var myGreet = {
  sayHello: function() {
    return 'Hello!';
  }
}
function outputObj_1() {
  console.log(myGreet.sayHello());
}
```
{{% /tab %}}
{{< /tabs >}}
```
Hello!
```

つまり、オブジェクトは **「情報」としてのプロパティ** だけでなく、**「機能」としてのメソッド** を持つことができるのです。  
なお、プロパティとメソッドを総じて、オブジェクトの **メンバー** と呼びます。

{{% notice note %}}
オブジェクトは、メンバーとしてプロパティとメソッドを持つことができます。
{{% /notice %}}

## メソッドの代入と追加
プロパティと同じく、メソッドも次のように代入することができます。オブジェクトに存在しないメソッドを代入すると、メソッドの追加になります。
```js
オブジェクト名.メソッド = function(仮引数１, 仮引数２, ...) {
  // 処理
  return 戻り値;
}
```
myGreetオブジェクトにsayGoodByeメソッドを追加する処理を加えたものが次のサンプルです。  
実行すると、ログには「Good bye!」も出力され、追加したsayGoodByeメソッドが動作していることが確認できます。
{{< tabs groupId="object_4" >}}
{{% tab name="コード.gs" %}}
```js
var myGreet = {
  sayHello: function() {
    return 'Hello!';
  }
}
myGreet.sayGoodBye = function() {
  return 'Good bye!'
}
function outputObj_2() {
  console.log(myGreet.sayHello());
  console.log(myGreet.sayGoodBye());
}
```
{{% /tab %}}
{{< /tabs >}}
```
Hello!
Good bye!
```
