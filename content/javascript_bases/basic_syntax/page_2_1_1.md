---
title: "ステートメント"
date: 2020-08-10T13:21:08+09:00
pre: "<b>1. </b>"
weight: 1
---

## ステートメントについて

JavaScriptはスクリプトを実行すると、原則上から順に1行ずつ処理が実行されていきます。

この処理の最小単位をステートメントと呼びます。

ステートメントは単語の途中でない限り、改行を入れることができます。

（あくまで、改行と入れることができるという話であり、コードの可読性が下がるようであれば無闇に改行を入れることはお勧めできません。）

```js
function myFunction() {
  console.log(
    'Hello GAS!'
  );
}
```

また、ステートメントの最後にはセミコロン（;）をつけることがルールとなっていますが、
セミコロンをつけなくても大抵のコードは実行されます。

ただし、稀にセミコロンをつけなかったためにエラーが発生するケースもあるため、
***ステートメントの最後にはセミコロン（;）をつける*** ようにしましょう。