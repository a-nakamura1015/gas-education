---
title: "処理を繰り返し行う"
date: 2020-08-10T13:43:49+09:00
pre: "<b>2. </b>"
weight: 2
---
## while文
唐突ですが、「1から10の数値を加算した結果を求めるスクリプトを書いてみましょう！」となったとき、どのようにコーディングしますか？
ここまで学習してきた皆さんであれば、下記のようにコーディングすることができると思います。
```js
var num = 0;
num += 1;
num += 2;
~
num += 10;
```
そして、コーディングの途中で「これ同じことを繰り返していない？」と気づくと思います。
繰り返す処理の数だけ行数が増えていき、コーディングをするのも大変ですし、後々コードを修正するときも大変です。
実際にプログラミングをしているとこのように同じ処理を繰り返す場面が多々あります。
実は、JavaScriptには繰り返し処理を実現する構文が用意されています。
そのうちの1つが **while文** です。
while文は条件式を用いた繰り返しを実現することができます。
```js
while (条件式) {
  // 条件式がtrueの間は実行される処理
}
```
while文を使いますと、条件式の結果がtrueの間はブロック内の処理を繰り返し実行し、条件式がfalseになったときにループ処理から抜けます。
下記のサンプルを実行して、while文の処理の流れを確認しましょう。
{{< tabs groupId="value_2_2_1_11" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop() {
  var x = 1;
  var sum = 0;
  while(x <= 10) {
    sum += x;
    x++;
  }
  console.log(sum);
}
```
{{% /tab %}}
{{< /tabs >}}
```
55
```
#### 無限ループ
繰り返し処理を行う際には **無限ループ** に気をつける必要があります。
下記のサンプルを実行すると無限ループが発生します。
{{< tabs groupId="value_2_2_1_12" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_2() {
  var x = 1;
  var sum = 0;
  while(x <= 10) {
    sum += x;
  }
  console.log(sum);
}
```
{{% /tab %}}
{{< /tabs >}}
このサンプルを実行するとスクリプトエディタの上部に「関数outLoop_2を実行中...」というメッセージが表示されたまま処理が完了しません。
このサンプルは変数xを初期化して1を代入していますが、while文の条件式が`x <= 10`となっているのにもかかわらず変数xが更新されずにずっと1のままのため、
while文の中をグルグル回り続けてしまっています。
このように、while文の条件式がfalseとなることがなく、永遠に同じループが繰り返されてしまう状態を無限ループといいます。
GASでは無限ループが発生した場合は「関数〇〇を実行中...」に続く、キャンセルをクリックすることでスクリプトを停止させることができます。
繰り返し処理をコーディングする際は、必ずループが終了するようになっているかを確認するようにしましょう。

{{% notice warning %}}
while文による繰り返しでは無限ループに気を付けましょう。
{{% /notice %}}

## for文
while文は条件式がtrueの間は処理を繰り返すという構文でしたが、処理を繰り返す回数があらかじめ決まっているのであれば **for文** を使用しましょう。
```js
for (①カウンタ変数の初期化; ②条件式; ④増減式) {
  // ③条件式がtrueの間は実行される処理
}
```
for文では **カウンタ変数** と呼ばれる変数を用います。
for文を使用すると決められた回数の繰り返し処理をとてもシンプルにコーディングすることができます。
for文の処理の流れは以下の通りです。

**①カウンタ変数の初期化**
　カウンタ変数に値を代入して初期化します。

**②条件式**
　条件式の結果を求めて判定を行います。この判定で true と判定された場合は {} の中の処理を実行します。
　false と判定された場合は {} の中の処理を実行せずにループ処理を抜けます。

**③条件式がtrueの間は実行される処理**
　for文の {} の中の処理を実行します。

**④増減式**
　最後に計算式を実行し、カウント変数の増減を行います。
　計算後は②条件式に戻ります。

次のサンプルを実行してfor文の処理の流れを確認しましょう。
{{< tabs groupId="value_2_2_1_13" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_3() {
  var sum = 0;
  for (var index = 1; index <= 10; index++) {
    sum += index;
  }
  console.log(sum);
}
```
{{% /tab %}}
{{< /tabs >}}
```
55
```

#### continue文
いまのループを中断して次のループに進みたい（要約するとスキップしたい）場合は`continue文`を活用します。
continue文が実行されると、そのループは中断され増減式が実行されます。
次のサンプルではカウンタ変数のindex変数が２の倍数の場合は、continue文以降の処理をスキップしています。
{{< tabs groupId="value_2_2_1_13" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_4() {
  for (var index = 0; index <= 10; index++) {
    if (index % 2 === 0) {
      // index が２の倍数の場合はスキップする
      continue;
    }
    console.log(index);
  }
}
```
{{% /tab %}}
{{< /tabs >}}
```js
1
3
5
7
9
```

### 繰り返し処理と配列
これまでは配列の要素を取得しようとすると下記のようにコーディングする必要がありました。
{{< tabs groupId="value_2_2_1_14" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_5() {
  var fruits = ['apple', 'banana', 'orange'];
  console.log(fruits[0]);
  console.log(fruits[1]);
  console.log(fruits[2]);
}
```
{{% /tab %}}
{{< /tabs >}}
```js
apple
banana
orange
```
上記の例では取り出す要素が3つだけのため問題ありませんが、
この要素の数が10、100と増えていくとそれに比例してコーディング量が増えてしまいます。
そのような時に繰り返し処理を活用するとコーディング量を減らすことができます。
{{< tabs groupId="value_2_2_1_15" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_6() {
  var fruits = ['apple', 'banana', 'orange'];
  for (var index = 0; index < fruits.length; index++) {
    console.log(fruits[index]);
  }
}
```
{{% /tab %}}
{{< /tabs >}}
```js
apple
banana
orange
```
先ほどの例は配列の要素を取得しましたが、多次元配列から要素を取得するときも活躍します。
以下のサンプルでは繰り返し処理を活用して２次元配列の要素を取得しています。
{{< tabs groupId="value_2_2_1_16" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_7() {
  var foods = [['apple', 'banana', 'orange'], ['beef', 'pork', 'chicken']];
  for (var i = 0; i < foods.length; i++) {
    console.log(foods[i]);
  }
}
```
{{% /tab %}}
{{< /tabs >}}
```
['apple', 'banana', 'orange']
['beef', 'pork', 'chicken']
```
２次元配列から配列（要素）を取得することができましたが、さらにその配列の要素を取得したい場合もあります。
その場合は繰り返し処理の中でさらに繰り返し処理を行う２重ループを行うことで実現できます。
1回目のループ（カウント変数がi変数のループ）では配列（要素）を取得して、
2回目のループ（カウント変数がj変数のループ）で要素を取得しています。
{{< tabs groupId="value_2_2_1_17" >}}
{{% tab name="コード.gs" %}}
```js
function outputLoop_8() {
  var foods = [['apple', 'banana', 'orange'], ['beef', 'pork', 'chicken']];
  for (var i = 0; i < foods.length; i++) {
    for (var j = 0; j < foods[i].length; j++) {
      console.log(foods[i][j]);
    }
  }
}
```
{{% /tab %}}
{{< /tabs >}}
```js
apple
banana
orange
beef
pork
chicken
```
