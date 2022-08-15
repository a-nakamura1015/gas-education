---
title: "カレンダーを操作しよう"
date: 2022-08-15T10:33:18+09:00
pre: "<b>3. </b>"
weight: 3
---
### カレンダーを作成しよう
Google カレンダーでは複数のカレンダーを作ることができます。(この機能により、用途によってカレンダーを使い分けることができます。)  
GAS でカレンダーを作るには、GoogleAppsクラスの [createCalendar メソッド](https://developers.google.com/apps-script/reference/calendar/calendar-app#createcalendarname)を活用します。
このメソッドはパラメータとして **カレンダー名** を指定する必要があります。
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| createCalendar | [String] カレンダーの名前 | [Calendar] 作成したカレンダー | ユーザーが所有する新しいカレンダーを作成します。 |

今回は以下のサンプルコードを実行して、旅行用のカレンダーを作成してみましょう。
{{< tabs groupId="calendar_3_1" >}}
{{% tab name="コード.gs" %}}
```js
function createCalendar() {
  const myCalendar = CalendarApp.createCalendar('旅行用');
}
```
{{% /tab %}}
{{< /tabs >}}

サンプルコードが無事実行ができたら、Google カレンダーを再読み込みしてみましょう。  
すると、マイカレンダーの中に旅行用カレンダーが作成されていることが確認できます。

---
### カレンダーの情報を取得しよう
カレンダーに予定を作るには、まずカレンダーを取得する必要があります。
CalendarAppクラスの [getAllCalendars メソッド](https://developers.google.com/apps-script/reference/calendar/calendar-app#getallcalendars)を実行することで、Google カレンダー内にある全てのカレンダーを取得することができます。  
このメソッドは Calendarクラスのオブジェクトを配列で返します。
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| getAllCalendars | なし | [Calendar[]] 取得したカレンダーの配列 | ユーザーが所有または購読しているすべてのカレンダーを取得します。 |

以下のサンプルコードは CalendarApp.getAllCalendar() の戻り値をループ処理で一つずつ取得して処理をしています。

{{< tabs groupId="calendar_3_2" >}}
{{% tab name="コード.gs" %}}
```js
function getAllCalendar() {
  // 全てのカレンダーを取得する
  const allCalendar = CalendarApp.getAllCalendars();
  for (let i = 0; i < allCalendar.length; i++) {
    // カレンダーを一つずつ取得して、カレンダーの情報をログで出力する
    const calendar = allCalendar[i];
    const id = calendar.getId();
    const name = calendar.getName();
    const descripion = calendar.getDescription();
    console.log(id, name, descripion);
  }
}
```
{{% /tab %}}
{{< /tabs >}}

サンプルコードの変数**calendar**には Calendarクラスのオブジェクトが格納されています。  
Calendarクラスはカレンダーの情報を取得するためのメソッドを提供しています。  
サンプルコードを実行すると、カレンダーのID、名前、説明をログで表示されますので確認してみましょう。

| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| getId | なし | [String] 取得したカレンダーの ID | カレンダーの ID を取得します。 |
| getName | なし | [String] 取得したカレンダーの名前 | カレンダーの名前を取得します。 |
| getDescription | なし | [String] 取得したカレンダーの説明 | カレンダーの説明を取得します。 |

{{% notice note %}}
**カレンダーの説明の確認方法**
カレンダーの説明はカレンダーの設定画面で確認することができます。  
対象のカレンダーにマウスカーソルを合わせると3点リーダーが表示され、クリックするとメニューが表示されます。 
このメニュー内の「設定と共有」を選択すると、カレンダーの設定画面を表示することができます。
![page_3_1.png](../img/page_3_1.png)
{{% /notice %}}

また、ある特定のカレンダーのみを取得することもできます。  
CalendarAppクラスの [getCalendarById メソッド](https://developers.google.com/apps-script/reference/calendar/calendar-app#getcalendarbyidid) で特定のカレンダーを取得できます。  
このメソッドはパラメータに**カレンダーのID**を指定するため、特定のカレンダーを取得するには事前にカレンダーのIDを確認する必要があります。

以下のサンプルコードはカレンダーを特定し、そのカレンダーの情報を取得してログに出力しています。  
**'カレンダーのID'** には先ほど作成した旅行用のカレンダーのIDを指定しましょう。
{{< tabs groupId="calendar_3_3" >}}
{{% tab name="コード.gs" %}}
```js
function getCalendarById() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  // 取得したカレンダーの情報を取得する
  const id = calendar.getId();
  const name = calendar.getName();
  const descripion = calendar.getDescription();
  console.log(id, name, descripion);
}
```
{{% /tab %}}
{{< /tabs >}}

| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| getCalendarById | [String] カレンダーのID | [Calendar] 取得したカレンダー | 指定された ID のカレンダーを取得します。 |

{{% notice note %}}
**カレンダーのIDの確認方法**
カレンダーのIDはカレンダーの設定画面で確認することができます。  
対象のカレンダーにマウスカーソルを合わせると3点リーダーが表示され、クリックするとメニューが表示されます。 
このメニュー内の「設定と共有」を選択すると、カレンダーの設定画面を表示することができます。
![page_3_2.png](../img/page_3_2.png)
{{% /notice %}}

---
### カレンダーの情報を更新しよう
カレンダーを特定することができれば、カレンダーの情報を更新することができるようになります。
Calendarクラスの [setName メソッド](https://developers.google.com/apps-script/reference/calendar/calendar#setnamename)はカレンダーの名前を、  
Calendarクラスの [setDescription メソッド](https://developers.google.com/apps-script/reference/calendar/calendar#setdescriptiondescription)はカレンダーの説明を更新することができます。  

以下のサンプルコードはカレンダーを取得した後にカレンダーの名前と説明を更新しています。  
サンプルコードを実行したのち、期待通りに Google カレンダーが更新されているかを確認してみましょう。
{{< tabs groupId="calendar_3_4" >}}
{{% tab name="コード.gs" %}}
```js
function updateCalendar() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  calendar.setName('Updated Calendar');
  calendar.setDescription('This is updated by gas.');
}
```
{{% /tab %}}
{{< /tabs >}}

| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| setName | [String] カレンダーの名前 | なし | カレンダーの名前を設定します。 |
| setDescription | [String] カレンダーの説明 | なし | カレンダーの説明を設定します。 |
---
### カレンダーを削除しよう
カレンダーを特定することができれば、カレンダーを削除することもできます。 
Calendarクラスの [deleteCalendar メソッド](https://developers.google.com/apps-script/reference/calendar/calendar#deletecalendar)  はカレンダーを削除することができます。  

以下のサンプルコードを実行すると特定したカレンダーを削除されます。 
**'カレンダーのID'** には先ほど更新した **Updated Calendar** カレンダーのIDを指定しましょう。
{{< tabs groupId="calendar_3_5" >}}
{{% tab name="コード.gs" %}}
```js
function deleteCalendar() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  calendar.deleteCalendar();
}
```
{{% /tab %}}
{{< /tabs >}}

| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| deleteCalendar | なし | なし | カレンダーを完全に削除します。自分が所有するカレンダーのみを削除できます。 |
