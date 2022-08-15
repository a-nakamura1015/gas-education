---
title: "配列"
date: 2020-08-10T13:30:37+09:00
pre: "<b>6. </b>"
weight: 6
---

## 配列とは
これまでは変数や定数に値を一つずつ代入して扱ってきましたが、複数のデータを1つにまとめたくなるケースもあります。
例えば、果物の名前を変数で管理したい場合は下記の通りになります。
```js
var fruitsName_1 = 'apple';
var fruitsName_2 = 'grape';
var fruitsName_3 = 'orange';
```
このように一つずつ変数を初期化して扱うことは可能ですが、非常に管理がしづらい問題が発生します。

さらに果物の名前の変数を作りたいとなった場合、fruiteName_Xの形式で変数名を作ることになりますが、
今回の果物が何個目の果物なのかをわざわざ確認しないといけないですよね。

このように、複数のデータをまとめて集合として扱うことができるデータを **配列** といいます。

配列はカンマで値と区切り、全体を角括弧（[]）で囲むことで表現することができます。（これを **配列リテラル** といいます。）
```js
[値1, 値2, ...]
```
配列は下記の図のように、複数の箱が連結しているような構造になっています。
それぞれの入れ物には番号が順番に割りふられており、番号は「0」から始まります。
この番号は **インデックス** といい、配列に格納されている値を **要素** といいます。
また、配列は変数に代入することもできます。

下記のサンプルは果物の名前を配列で管理した場合のコードとなります。
{{< tabs groupId="value_2_22" >}}
{{% tab name="コード.gs" %}}
```js
function outputArray_1() {
  var fruits = ['apple', 'grape', 'orange'];
  console.log(fruits);
}
```
{{% /tab %}}
{{< /tabs >}}
```
'apple', 'grape', 'orange'
```

### 配列の特徴
配列には以下の3つの特徴があります。
- 配列の各要素は添字（インデックス）をもっており、先頭が0から始まる数字が割り当てられている。
- JavaScriptの配列には異なる型の要素を入れることができる。
- 配列の最後の要素の添字（インデックス）よりも大きな添字を使って代入を行うと、
配列が自動的に大きくなり、値が指定されていない要素にはundefinedが暗黙的に代入される。

#### 配列の要素の参照と代入
配列から特定の要素を取り出す場合はインデックスを用います。
```js
配列名[インデックス]
```

下記のサンプルは配列fruitsからインデックスが1の要素をログに出力しています。
インデックスは0から始まるため、インデックスが1の要素は先頭から2番目の要素なので、「grape」が出力されます。
{{< tabs groupId="value_2_23" >}}
{{% tab name="コード.gs" %}}
```js
function outputArray_2() {
  var fruits = ['apple', 'grape', 'orange'];
  console.log(fruits[1]); // 'grape'
}
```
{{% /tab %}}
{{< /tabs >}}
また、配列内の特定の要素を代入で更新することもできます。
```js
配列名[インデックス] = 値;
```
配列内に指定したインデックスの要素が存在する場合は上書きされます。
逆に、配列内に指定したインデックスの要素が存在しない場合は要素の追加がなされます。
{{< tabs groupId="value_2_24" >}}
{{% tab name="コード.gs" %}}
```js
function outputArray_3() {
  var fruits = ['apple', 'grape', 'orange'];
  fruits[4] = 'peach';
  console.log(fruits); // 'apple', 'grape', 'orange', null, peach
  fruits[3] = 'berry';
  console.log(fruits); // 'apple', 'grape', 'orange', berry, peach
}
```
{{% /tab %}}
{{< /tabs >}}

#### 多次元配列
先ほどは配列の要素をインデックスで指定して値を取り出したり、上書きしたりしました。
実はこの要素には配列を設定することができ、配列の中に配列がある **二次元配列** を作ることができます。
このように配列が入れ子になっている配列を **多次元配列** といいます。
二次元配列は下記のように記述することで初期化することができます。
```js
var foods = [['beef', 'pork', 'chicken'], ['apple', 'grape'], ['tuna']];
```
二次元配列は要素が多くなるほど構造が複雑になりイメージがしづらいかもしれません。
そのようなときは下図のように箱の中に箱があるとイメージすると考えやすくなるでしょう。
{{% notice note %}}
二次元配列に対して、「入れ子」になっていない通常の配列を一次元配列といいます。
{{% /notice %}}
二次元配列から特定の要素を取り出す場合もインデックスを用います。
{{< tabs groupId="value_2_25" >}}
{{% tab name="コード.gs" %}}
```js
function outputArray_4() {
  var foods = [['beef', 'pork', 'chicken'], ['apple', 'grape'], ['tuna']];
  console.log(foods[0]); // 'beef', 'pork', 'chicken'
  foods[2] = ['carrot'];
  console.log(foods); // ['beef', 'pork', 'chicken'], ['apple', 'grape'], ['carrot']
}
```
{{% /tab %}}
{{< /tabs >}}

二次元配列の内側の要素を取り出すには、外側のインデックスに続けて内側のインデックスも指定します。
```js
配列名[インデックス1][インデックス2]
```
```js
配列名[インデックス1][インデックス2] = 値;
```
二次元配列の内側の要素の参照、代入および追加は下記のサンプルのように記述することができます。
{{< tabs groupId="value_2_26" >}}
{{% tab name="コード.gs" %}}
```js
function outputArray_5() {
  var number = [[1, 2, 3], [10, 20], [100]];
  console.log(number[0][0]); // 1
  console.log(number[1][0]); // 10
  console.log(number[1][1]); // 20
}

function outputArray_6() {
  var number = [[1, 2, 3], [10, 20], [100]];
  number[0][0] = 0;   // 要素への代入
  number[2][1] = 200; // 要素の追加
  console.log(number); // [0, 2, 3], [10, 20], [100, 200]
}
```
{{% /tab %}}
{{< /tabs >}}

GASではスプレッドシートのシートの行列のデータを利用する際にこの二次元配列を扱いますので、
一次元配列だけでなく多次元配列についても理解しておく必要があります。

### 配列要素の操作
配列の要素を操作するメソッドは多々ありますが、
「配列内の要素を変更してしまうメソッド」と「新しい配列を返すメソッド」の２種類に分けられます。

#### 先頭の要素を操作する
配列の先頭は`arr[0]`と表現します。
先頭の要素を操作する関数は下記の2つで、それぞれ配列そのものを変更します。
`shiftメソッド`: 先頭の要素を削除する。削除した要素を返す。
`unshiftメソッド`: 先頭に要素を追加する。追加後の配列の長さを返す。
{{< tabs groupId="value_2_27" >}}
{{% tab name="コード.gs" %}}
```js
var arr = ['b', 'c', 'd'];
console.log(arr.shift());      // b
console.log(arr);              // [ 'c', 'd' ]
console.log(arr.unshift('a')); // 3
console.log(arr);              // [ 'a', 'c', 'd' ]
```
{{% /tab %}}
{{< /tabs >}}

#### 最後の要素を操作する
配列の最後は`arr[arr.length - 1]`と表現します。
最後の要素を操作する関数は下記の2つで、それぞれ配列そのものを変更します。
`pushメソッド`：最後に要素を追加する。追加後の配列の長さを返す。
`popメソッド`:最後の要素を削除する。削除した要素を返す。
{{< tabs groupId="value_2_28" >}}
{{% tab name="コード.gs" %}}
```js
var arr = ['b', 'c', 'd'];
console.log(arr.push('e')); // 4
console.log(arr);           //[ 'b', 'c', 'd', 'e' ]
console.log(arr.pop());     // e
console.log(arr);           // [ 'b', 'c', 'd' ]
```
{{% /tab %}}
{{< /tabs >}}

####  複数の要素を追加する
`concatメソッド`は複数の要素を配列に追加し、戻り値として配列のコピーを返します。
引数として渡された配列の全ての要素を対象の配列の最後に追加します。
{{< tabs groupId="value_2_29" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = ['a', 'b', 'c'];
var arr2 = arr1.concat('d', 'e');
console.log(arr1); // [ 'a', 'b', 'c' ]
console.log(arr2); // [ 'a', 'b', 'c', 'd', 'e' ]
```
{{% /tab %}}
{{< /tabs >}}

`concatメソッド`は引数として配列を指定することもできます。
{{< tabs groupId="value_2_30" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = ['a', 'b', 'c'];
var arr2 = arr1.concat(['d', 'e']);
console.log(arr1); // [ 'a', 'b', 'c' ]
console.log(arr2); // [ 'a', 'b', 'c', 'd', 'e' ]
```
{{% /tab %}}
{{< /tabs >}}

引数に多次元配列を指定することもできますが、その場合は内側の配列はそのまま追加されます。
{{< tabs groupId="value_2_31" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = ['a', 'b', 'c'];
var arr2 = arr1.concat(['d', ['e', 'f']]);
console.log(arr1); // [ 'a', 'b', 'c' ]
console.log(arr2); // [ 'a', 'b', 'c', 'd', [ 'e', 'f' ] ]
```
{{% /tab %}}
{{< /tabs >}}

#### 配列内の要素を部分的に取り出す
配列の要素のうち一部のみを取り出したい場合は`sliceメソッド`を使います。
`sliceメソッド`は２個の引数を渡します。
1つめは「要素を取得する開始位置（インデックス）」、2つめは「要素を取得する終了直前の位置（インデックス）」を指定します。
第２引数を省略すると最後の要素まで取得することになります。
また、第2引数に負の値を指定すると最後の要素から数えた場所を指定することになります。
{{< tabs groupId="value_2_31" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [1, 2, 3];
var arr2 = arr1.slice(1);
// 元の配列に変化はない
console.log(arr1); // [ 1, 2, 3 ]
// インデックスが１以降の要素が表示される。
console.log(arr2); // [ 2, 3 ]
```
{{% /tab %}}
{{< /tabs >}}

{{< tabs groupId="value_2_32" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [1, 2, 3];
var arr2 = arr1.slice(1, 3);
// 元の配列に変化はない
console.log(arr1); // [ 1, 2, 3 ]
// インデックスが１の要素からインデックスが3の直前の要素までが表示される。
console.log(arr2); // [ 2, 3 ]
```
{{% /tab %}}
{{< /tabs >}}

{{< tabs groupId="value_2_33" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [1, 2, 3];
var arr2 = arr1.slice(1, -1);
// 元の配列に変化はない
console.log(arr1); // [ 1, 2, 3 ]
// インデックスが１の要素から最後のインデックスが１つ前の要素までが表示される。
console.log(arr2); // [ 2 ]
```
{{% /tab %}}
{{< /tabs >}}

#### 途中の要素の削除や追加
`spliceメソッド`を使うと配列の任意の場所を指定して内容を変更することができます。
第1引数には変更を開始する添字（インデックス）、第2引数には削除する要素の数、
第3引数以降に追加する要素を指定します。
戻り値として削除された要素からなる配列を返します。
{{< tabs groupId="value_2_34" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [1, 4, 5];
var arr2 = arr1.splice(1, 0, 2, 3); // インデックス1の要素に3と4を追加
// 元の配列に要素が追加される
console.log(arr1); // [ 1, 2, 3, 4, 5 ]
// 要素は削除されていないため要素は返されない
console.log(arr2); // []
```
{{% /tab %}}
{{< /tabs >}}

{{< tabs groupId="value_2_35" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [1, 4, 5];
var arr2 = arr1.splice(1, 2, 2, 3); // インデックス1の要素に3と4を追加
// 元の配列の要素が削除された上で要素が追加される
console.log(arr1); // [ 1, 2, 3 ]
// 削除された要素が返される
console.log(arr2); // [ 4, 5 ]
```
{{% /tab %}}
{{< /tabs >}}

#### 配列内の要素の逆転とソート
配列の要素を逆順で並び替える場合は`reversseメソッド`を使用します。
{{< tabs groupId="value_2_36" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [5, 4, 3, 2, 1];
arr1.reverse();
console.log(arr1); // [ 1, 2, 3, 4, 5 ]
```
{{% /tab %}}
{{< /tabs >}}

また、`sortメソッド`は配列の要素のソート（並び替え）をします。
既定のソート順は昇順で、要素を文字列に変換してからUTF-16コード単位の値の並びとして比較します。
{{< tabs groupId="value_2_37" >}}
{{% tab name="コード.gs" %}}
```js
var arr1 = [3, 4, 2, 1, 5];
arr1.sort();
console.log(arr1); // [ 1, 2, 3, 4, 5 ]
```
{{% /tab %}}
{{< /tabs >}}

`sortメソッド`で配列内のオブジェクトも並び替えることができるのですが、
その際にプロパティ値で並び替えることができます。

#### 配列内の要素の検索
配列内の要素を検索する方法をいくつかあります。
##### indexOfメソッド
指定した値に厳密に等しい要素（===で等しい要素）をもつ最初の添字を返すメソッドです。
また、`lastIndexOfメソッド`は同様に最後の添字を返します。
配列の一部だけを検索対象としたい場合は引数に開始位置を指定します。
ちなみに、要素が見つからなかった場合は-1を返します。
{{< tabs groupId="value_2_38" >}}
{{% tab name="コード.gs" %}}
```js
var arr = [1, 2, 3, 4, 1];
console.log(arr.indexOf(1));      // 0
console.log(arr.lastIndexOf(1));  // 4
console.log(arr.indexOf(5));      // -1
console.log(arr.lastIndexOf(-1)); // -1
```
{{% /tab %}}
{{< /tabs >}}
上記のサンプルの通り、見つかった場合は添字番号（インデックス）を返し、見つからなかった場合は-1を返します。

##### mapとfilter
`mapメソッド`は配列内の要素に対して、引数で指定した関数を呼び出してその結果から新しい配列を生成します。
{{< tabs groupId="value_2_39" >}}
{{% tab name="コード.gs" %}}
```js
var fruits = [{name: 'apple', price: 300}, {name: 'banana', price: 400}];
//  オブジェクトから名前のみ抽出して配列を生成する。
var names = fruits.map(function(fruit) {
  return fruit.name;
});
//  オブジェクトから価格のみ抽出して配列を生成する。
var prices = fruits.map(function(fruit) {
  return fruit.price;
});
console.log(fruits); // [ { name: 'apple', price: 300 }, { name: 'banana', price: 400 } ]
console.log(names); // ['apple', 'banana']
console.log(prices); // [330, 440]
```
{{% /tab %}}
{{< /tabs >}}

上記のサンプルでは要素（fruit）を1つずつ取り出し、その要素のプロパティ（name, price）を取得しています。
`mapメソッド`の引数に関数を渡して、取得した要素を第1仮引数に設定して関数内の処理を行っています。
関数に渡した第1仮引数は要素そのものですが、第2仮引数と第3仮引数も指定することできます。
第２仮引数は添字（インデックス）が渡され、第３仮引数はメソッドを実行した配列そのものが渡されます。
{{< tabs groupId="value_2_40" >}}
{{% tab name="コード.gs" %}}
```js
var fruits = [{name: 'apple', price: 300}, {name: 'banana', price: 400}];
// 第1引数は要素そのもの、第2引数は添字、第3引数は配列そのものが設定されます。
var values = fruits.map(function(fruit, index, _fruits) {
  // ※第1引数の要素そのものを使用して、fruit.name でも名前を取得できます。
  return {index: index, name: _fruits[index].name};
});
console.log(values); // [ { index: 0, name: 'apple' }, { index: 1, name: 'banana' } ]
```
{{% /tab %}}
{{< /tabs >}}

`filterメソッド`は配列の内容を特定の条件を絞り込むメソッドです。
fiterはその名前の通り、配列から不要な要素を取り除く（フィルタリングする）ことができます。

{{< tabs groupId="value_2_41" >}}
{{% tab name="コード.gs" %}}
```js
var fruits = [{name: 'apple', price: 300}, {name: 'banana', price: 400}];
//  オブジェクトから価格が300よりも大きい要素抽出して配列を生成する。
var _fruits = fruits.filter(function(fruit){
  return fruit.price > 300;
});
console.log(fruits); // [ { name: 'apple', price: 300 }, { name: 'banana', price: 400 } ]
console.log(_fruits); // [ { name: 'banana', price: 400 } ]
```
{{% /tab %}}
{{< /tabs >}}
