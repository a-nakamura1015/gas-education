---
title: "コメント"
date: 2020-08-10T13:27:43+09:00
pre: "<b>3. </b>"
weight: 3
---

## コメントとは

***コメント*** とは、スクリプト内のメモ書きのことをいいます。

このコメントはスクリプトの実行時には無視されるため、実行されることはありません。

では、どのようなときにこのコメントを使うのでしょうか？

例えばですが、しばらく期間をあけてコードを読み返した際に、自身がどのような考えで実装したのか思い出すのは大変です。

そのようなときにコメントが書かれているとこのような苦労をせずに済みます。

同様に、自身ではなく他の人にソースを読んでもらうことがあった場合も、
自身がどのような考えで実装したのかを伝えることができます。

1行のみコメントにしたい場合は、その文頭に「//」を入れることでコメントにすることができます。

```js
function myFunction() {
  // 実行されないので半角英数字や半角記号以外の文字を入れることができます。
  console.log('Hello GAS!'); // 行の後ろにも入れることができます。
}
```

また、複数行をコメントにしたい場合は「/\*」と「\*/」で囲います。

```js
function muFunction() {
  /*
   1行目
   2行目
  */
  console.log('Hello GAS!');
}
```

## コメントの活用方法

コーディングをしていて、「このステートメントは実行したくないな」というときにもコメントは活躍します。

このように一時的にコメントにすることを「コメントアウト」といいます。

```js
 // 2回目のconsole.log()は実行したくない場合
function myFunction() {
  console.log('Hello GAS!');
  // 2回目のconsole.log()をコメントアウト
  // console.log('Hello GAS!');
}
```

{{% notice note %}}
コメントアウトはショートカットキーがあり、コメントアウトしたい行を選択した上で、Windonwsは`Ctrl + /`、Macは`control + /`でコメントアウトをすることができます。逆に、コメントを解除したい場合も同じ手順で行うことができます。
{{% /notice %}}