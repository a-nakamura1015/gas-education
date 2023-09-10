---
title: "class構文"
date: 2021-05-23T02:29:13+09:00
pre: "<b>4. </b>"
weight: 4
---
## クラスとは
クラスを一言で表すと「オブジェクトの雛形（テンプレート）」です。  
クラスはオブジェクトの **属性（プロパティ）** と **機能（メソッド）** を定義することができます。  
例えば、人間をクラスで定義した場合、  
名前や年齢などの情報を持ちますがこれは人間の属性（プロパティ）にあたります。  
属性（プロパティ）は人間によって同じ場合もあれば異なる場合もあります。  
また、人間は挨拶をしたり、食事をしたりしますがこれは機能（メソッド）にあたります。  
皆同じ機能を持ちますが、人間によっては結果が異なる場合がありますね。  
このようにクラスはデータの抽象的な概念を表現する際に活躍します。

クラスはあくまで「オブジェクトの雛形（テンプレート）」であるため、  
実際に動かす際はクラスをもとに **インスタンス（実体）** を生成し、このインスタンスに属性（プロパティ）を設定し機能（メソッド）を実行します。  
これは、人間の設計書（クラス）をもとに人間（インスタンス）を作っているというイメージです。

## クラスの定義
ES2015でクラスを表現するための**class構文**が導入されました。  
class構文では **class** キーワードを用いてクラス名を付けて宣言します。  
また、クラスは **コンストラクター（constructor）** と呼ばれる特殊なメソッドを持ちます。  
コンストラクターはインスタンスが生成されるときに自動的に呼び出されるメソッドであり、  
インスタンスの初期化処理（プロパティの値の設定など）を行うことができます。  
コンストラクターは省略することができますが、この場合は空っぽのコンストラクターが定義されることになります。  
なお、クラスに定義できるコンストラクターは1つまでです。

クラスを宣言する方法は**クラス宣言**と**クラス式**の２種類があります。  
以下はクラス宣言の構文です。
```js
class クラス名 {
  constructor(仮引数名1{, 仮引数名2...}) {
    // 同クラスのインスタンスが生成されるとき、インスタンスごとに自動的に呼び出される
  }
}
```
もう一つの宣言方法のクラス式の構文は以下の通りです。  
クラス式は変数に代入する形式となり、無名関数として扱うことができるためクラス名を省略することができます。
```js
// クラスを値として定義し、変数に代入
const 変数名 = class クラス名 {
  constructor(仮引数名1{, 仮引数名2...}) {}
}
// 無名関数としてクラス名を省略して定義
const 変数名 = class {
  constructor(仮引数名1{, 仮引数名2...}) {}
}
```
{{% notice note %}}
JavaScriptではクラス名の先頭の文字を大文字で書くことが慣習になっています。  
この慣習を守ることで、小文字で書くインスタンス名と大文字で書くクラス名は、一目で区別をつけることができます。
{{% /notice %}}

## クラスを使うメリット
これまではオブジェクトが必要になった際は、以下のようにその都度プロパティやメソッドを定義していました。  
しかし、このコーディング方法はほとんど同じ内容のコードを書かないといけない上、  
メソッドを増やすことになった場合は非常に手間がかかります。
{{< tabs groupId="es2022_20" >}}
{{% tab name="コード.gs" %}}
```js
function object_pattern() {
  const human1 = {
    name: 'Taro',
    greet: function() {
      console.log(`Hello. My name is ${this.name}`);
    }
  }
  const human2 = {
    name: 'Hanako',
    greet: function() {
      console.log(`Hello. My name is ${this.name}`);
    }
  }
  human1.greet(); // Hello. My name is Taro
  human2.greet(); // Hello. My name is Hanako
}
```
{{% /tab %}}
{{< /tabs >}}
一方、クラスはこの問題を解消してくれます。  
以下は先ほどのサンプルをclass構文を使って書き直したサンプルです。  
仮にメソッドを増やすことになったとしても、Humanクラスにメソッド追加することで、  
各インスタンスは共通のメソッドを呼び出すことができます。  
また、クラス内でthisはクラスを元に生成されたインスタンスのことを指します。  
以下のサンプルには**名前がTaroの人間クラスのインスタンス**と**名前がHanakoの人間クラスのインスタンス**が生成されています。  
インスタンスを生成するには **new クラス名()** と記述します。  
※) クラスは変数や関数と同様にグローバル領域に定義することができます。
{{< tabs groupId="es2022_21" >}}
{{% tab name="コード.gs" %}}
```js
class Human {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello. My name is ${this.name}`);
  }
}
function classes_pattern_1() {
  const human1 = new Human('Taro');
  const human2 = new Human('Hanako');
  human1.greet(); // Hello. My name is Taro
  human2.greet(); // Hello. My name is Hanako
}
```
{{% /tab %}}
{{< /tabs >}}
## アクセッサプロパティ
通常、クラスに定義したメソッドは **インスタンス.メソッド名()** で実行することができますが、  
インスタンスのプロパティの参照（getter）と代入（setter）をする特殊なメソッドは **インスタンス.プロパティ名** で実行することができます。  
このようにプロパティを制御するメソッドを**アクセッサプロパティ**といいます。  
アクセッサプロパティは対象のメソッド名の前に`get`または`set`をつけることで定義できます。  
`get`をつけたメソッドはプロパティの参照ができるようになり、仮引数は不要ですが必ず値を返す必要があります。  
一方、`set`を付けたメソッドはプロパティに代入ができるようになり、値を返す必要はありませんが仮引数は必要になります。
```js
class クラス {
  get プロパティ名() {
    return 値;
  }
  set プロパティ名(仮引数) {
    // プロパティの代入などのsetterの処理
  }
}
```
先ほどのサンプルコードのHumanクラスをアクセッサプロパティでコーディングすると以下の通りになります。  
クラス内のプロパティを指している`this.name`を`this._name`としているのには理由があります。  
`this.name`が呼ばれるとgetterが動くのですが、このgetterもまた`this.name`を呼んでいるのです。  
そのため、同じ関数がひたすら呼ばれることにより`RangeError: Maximum call stack size exceeded`が発生してしまいます。  
このエラーを回避するため、プロパティを`this._name`とコーディングする必要があるのです。
{{< tabs groupId="es2022_22" >}}
{{% tab name="コード.gs" %}}
```js
class Human {
  constructor(name) {
    this._name = name;
  }
  greet() {
    console.log(`Hello. My name is ${this.name}`);
  }
  get name() {
    return this._name;
  }
  set name(name) {
    this._name = name;
  }
}
function classes_pattern_2() {
  const human = new Human('Yamada Taro');
  human.name = 'Suzuki Taro'; // setterでYamada TaroからSuzuki Taroに改名
  console.log(human.name); // getterで改名後の名前を取得
}
```
{{% /tab %}}
{{< /tabs >}}
```
Suzuki Taro
```
## プロトタイプ
全ての関数はprototypeと呼ばれる特別なプロパティを持っています。  
このprototypeの仕組みにより、クラスに対して定義したメソッドは各インスタンスで利用できるメソッドになります。  
このように各インスタンスで共有で利用できるメソッドは **プロトタイプメソッド（インスタンスメソッド）** と呼ばれています。  
先ほどのサンプルコードではgreetメソッドを定義していましたが、  
このメソッドを各インスタンスが利用できるのはプロトタイプメソッドとして定義しているためです。  
プロトタイプメソッドは以下のように定義して呼び出すことができます。
```js
class クラス名 {
  メソッド名() {
  }
}
const インスタンス名 = new クラス名();
インスタンス名.メソッド名();
```
また、生成したインスタンスに対してメソッドやプロパティを定義することができます。  
同じ名前のメソッドやプロパティを宣言すると、プロトタイプメソッドよりもインスタンス生成後にインスタンスに対して追加したメソッドやプロパティが優先されます。  
追加したメソッドやプロパティは対象のインスタンスのみで利用可能で、同クラスの別インスタンスでは利用することはできません。
{{< tabs groupId="es2022_23" >}}
{{% tab name="コード.gs" %}}
```js
class Human {
  constructor(name) {
    this._name = name;
  }
  greet() {
    console.log(`Hello. My name is ${this.name}`);
  }
  get name() {
    return this._name;
  }
  set name(name) {
    this._name = name;
  }
}
function classes_pattern_3() {
  const human1 = new Human('Taro');
  const human2 = new Human('Hanako');
  // human1にメソッドを再定義・追加する
  human1.greet = function() { console.log(`I am ${human1.name}`); }
  human1.shout = function() { console.log('Hello!!!'); }
  // 各インスタンスのメソッドを実行する
  human1.greet(); // I am Taro
  human1.shout(); // Hello!!!
  human2.greet(); // Hello. My name is Hanako
  human2.shout(); // TypeError: human2.shout is not a function
}
```
{{% /tab %}}
{{< /tabs >}}

## 静的メソッド（クラスメソッド）
ここまで紹介したメソッドはインスタンスごとに実行することができる**インスタンスメソッド**でしたが、  
ここではクラスをインスタンス化せずに使用する **静的メソッド（クラスメソッド）** を紹介します。  
静的メソッドは特定のインスタンスに関わることなく、クラスに関係する処理を実行することができるメソッドです。  
静的メソッドの定義方法はメソッド名の前に**static**をつけるだけで、  
静的メソッドはインスタンス名.メソッド名ではなく**クラス名.メソッド名**で呼び出すことができます。
```js
class クラス名 {
  static メソッド名() {
    // 静的メソッドの処理
  }
}
// 静的メソッドの呼び出し
クラス名.メソッド名();
```
それでは、静的メソッドがどのような場面で活躍するかを紹介します。  
例えば、Humanクラスから生成されたインスタンスの数を管理したい場合、  
各インスタンスではなくクラスでインスタンスの数を管理する必要があります。  
以下のサンプルコードではHumanクラスのインスタンスが生成されるたびに静的メソッドを実行してインスタンスの数をカウントしています。
{{< tabs groupId="es2022_24" >}}
{{% tab name="コード.gs" %}}
```js
class Human {
  constructor(name) {
    this._name = name;
    // インスタンスが生成されるたびに静的メソッドを実行
    Human.getCounter();
  }
  // Human.countプロパティを加算する静的メソッド
  static getCounter() {
    return Human.count++;
  }
  greet() {
    console.log(`Hello. My name is ${this.name}`);
  }
  get name() {
    return this._name;
  }
  set name(name) {
    this._name = name;
  }
}
// クラス共通のプロパティを設定
Human.count = 0;
function classes_pattern_4() {
  new Human('Taro');
  new Human('Hanako');
  new Human('Ichiro');
  console.log(Human.count);
}
```
{{% /tab %}}
{{< /tabs >}}
```
3
```

## 継承
クラスのインスタンスを生成すると、クラスのプロトタイプがもつ機能を「継承」します。  
継承とは、クラスの構造や機能を引き継いだ新しいクラスを定義することです。

仮にオブジェクトのプロトタイプに呼び出そうとしたメソッドが見つからない場合は、  
同クラスが継承している **スーパークラス（親クラス）** で同じ名前のメソッドがないかを探します。  
同じ名前のメソッドが見つかるまでスーパークラス（親クラス）を遡っていき、一番上まで遡っても見つからない場合はエラーとなります。  
このようにオブジェクト自身のプロトタイプを追っていくことは**プロトタイプチェーン**と呼ばれています。
このプロトタイプチェーンにより、クラスの間に階層関係を構築することができます。  

**extends**キーワードを使い、以下の構文で書くことで既存のクラスを継承することができます。  
class構文の右辺にextendsキーワードで継承元となるスーパークラス（親クラス）を指定することで、 スーパークラスを継承した **サブクラス（子クラス）** を定義できます。  
サブクラスのインスタンスは、通常のインスタンスの作成方法と同じく**new演算子**をクラス名の前に記述することで作成することができます。
```js
class 子クラス名 extends 親クラス名 {
}
const child = new 子クラス名();
```
以下のサンプルコードはスーパークラスである Animal クラスと、  
Animalクラスを継承するサブクラス（子クラス）のDogクラスとCatクラスをコーディングしています。  
サブクラスのコンストラクタに **super()** が実行されていますが、  
このsuper()でextendsを使って定義したサブクラスからスーパークラスを参照することができます。  
サンプルコードではスーパークラスのコンストラクタを参照して実行しています。
{{< tabs groupId="es2022_25" >}}
{{% tab name="コード.gs" %}}
```js
class Animal {
  constructor(categoryName) {
    this.category = categoryName;
    this.name;
    console.log(`${this.category}が産まれた`);
  }
  walk() {
    console.log(`${this.name}が歩いた`);
  }
  // 吠える・鳴くメソッド
  bark() {
    console.log(`${this.name}が吠えた`);
  }
}

/**
 * 犬は動物のサブクラス
 */
class Dog extends Animal {
  constructor() {
    // スーパークラス（Animalクラス）のコンストラクタを呼び出す
    super('犬');
    this.name;
  }
　setName(name) {
    this.name = name;
  }
  // スーパークラス（Animalクラス）のメソッドを上書き
  bark() {
    console.log('ワン！');
  }
  // サブクラス固有のメソッドを追加
  bite() {
    console.log(`${this.name}は噛み付いた`);
  }
}

/**
 * 猫は動物のサブクラス
 */
class Cat extends Animal {
  constructor() {
    // スーパークラス（Animalクラス）のコンストラクタを呼び出す
    super('猫');
    this.name;
  }
　setName(name) {
    this.name = name;
  }
  // スーパークラス（Animalクラス）のメソッドを上書き
  bark() {
    console.log('ニャ〜');
  }
  // サブクラス固有のメソッドを追加
  scratch() {
    console.log(`${this.name}は引っ掻いた`);
  }
}
```
{{% /tab %}}
{{< /tabs >}}

先ほどのDogクラスとCatクラスからインスタンスを生成し、メソッドを実行しているのが以下のサンプルコードです。  
Dogクラスから生成したインスタンスにはPochiという名前を、Catクラスから生成したインスタンスにはTamaという名前をつけ、  
それぞれのメソッドを実行しています。
{{< tabs groupId="es2022_26" >}}
{{% tab name="コード.gs" %}}
```js
function classes_pattern_5() {
  const dog = new Dog();
  const cat = new Cat();
  // スーパークラスの共通のメソッドを呼び出す
  dog.setName('Pochi');
  dog.walk();
  cat.setName('Tama');
  cat.walk();
  // 上書きされたスーパークラスの共通メソッドを呼び出す
  dog.bark();
  cat.bark();
  // 各クラスの固有のメソッドを呼び出す
  dog.bite();
  cat.scratch();
}
```
{{% /tab %}}
{{< /tabs >}}
```
犬が産まれた
猫が産まれた
Pochiが歩いた
Tamaが歩いた
ワン！
ニャ〜
Pochiは噛み付いた
Tamaは引っ掻いた
```

このように、継承によりオブジェクトなどのデータ型に関する操作が統一的であることを**ポリモーフィズム**と呼びます。  
また、JavaScriptには**instanceof演算子**で左辺の値が右辺のクラスのインスタンスであるかを真偽値で返してくれます。  
instanceof演算子は右辺にスーパークラスが指定された場合はtrueを返します。
{{< tabs groupId="es2022_27" >}}
{{% tab name="コード.gs" %}}
```js
function classes_pattern_6() {
  const dog = new Dog(); // 犬が産まれた
  const cat = new Cat(); // 猫が産まれた
  console.log(dog instanceof Dog); // true
  console.log(cat instanceof Cat); // true
  console.log(dog instanceof Cat); // false
  console.log(cat instanceof Dog); // false
  console.log(dog instanceof Animal); // true
  console.log(cat instanceof Animal); // true
}
```
{{% /tab %}}
{{< /tabs >}}
```
犬が産まれた
猫が産まれた
true
true
false
false
true
true
```
{{% notice note %}}
JavaScriptのすべてのオブジェクトはルートクラスであるObjectのインスタンスになります。  
そのため、任意のオブジェクト o に対し、`o instanceof Object`の結果はtrueになります。
{{% /notice %}}
