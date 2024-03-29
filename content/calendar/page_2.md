---
title: "Calendarサービス"
date: 2022-08-15T09:24:16+09:00
pre: "<b>2. </b>"
weight: 2
---
### Calendarサービスとは
**Calendarサービス** は Google App Script で Google カレンダーを操作するためのメソッドを提供しています。
Calendarサービスでは以下のクラスを活用することで Google カレンダーを操作することができます。

| クラス名 | 概要 |
| --- | --- |
| CalendarApp | Calendar サービスのグローバルオブジェクト |
| Calendar | カレンダーを操作（カレンダーの情報の取得・更新・削除）する |
| CalendarEvent | 予定を操作（予定の取得・更新・削除）する |

Calendar サービスの各クラスは CalendarApp → Calendar → CalendarEvent という階層構造になっています。
各クラスにはそのオブジェクトを操作するメンバーとともに、その配下のオブジェクトを取得するメンバーが用意されています。
これは Google カレンダー に限らず、他のサービスでもオブジェクトを操作する際の基本的な流れとなります。
また、GAS のクラスに対して new 演算子でインスタンスを生成することはありません。

{{% notice tip %}}
GASのオブジェクト操作の基本動作は、グローバルオブジェクトから辿って目的のオブジェクトを取得し、操作をしていきます。  
Google カレンダーの場合は **CalendarApp** がグローバルオブジェクトになります。
{{% /notice %}}

![page_2_1.png](../img/page_2_1.png)
