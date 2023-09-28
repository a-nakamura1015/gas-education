---
title: "予定を操作しよう"
date: 2022-08-15T13:19:11+09:00
pre: "<b>4. </b>"
weight: 4
---
### 予定を作成しよう
いよいよカレンダーの予定を作ってみましょう。  
カレンダーの予定を作るには、まず予定を作成するカレンダーを取得する必要があります。
カレンダーを取得できたら、Calendarクラスの [createEvent メソッド]で予定を作りましょう。  
Calendar.createEventメソッドを実行するには以下の３つの引数を指定する必要があります。
- 予定のタイトル
- 予定の開始日時
- 予定の終了日時

以下のサンプルコードは「タイトルが New Event」で、「予定の時間が2022年9月1日の9時〜10時」の予定を作成しています。  
サンプルコードの **'カレンダーのID'** には任意のカレンダーのIDを指定しましょう。  
サンプルコードを実行したら、Google カレンダー上に予定が作成されているかを確認してみましょう。
{{< tabs groupId="calendar_4_1" >}}
{{% tab name="コード.gs" %}}
```js
function createEvent() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  const title = 'New Event';
  const startTime = new Date('2022-09-01 09:00:00');
  const endTime = new Date('2022-09-01 10:00:00');
  calendar.createEvent(title, startTime, endTime);
}
```
{{% /tab %}}
{{< /tabs >}}
#### Calendar クラスのメソッド
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| createEvent | [String] 予定のタイトル、[Date] 予定の開始日時、[Date] 予定の終了日時 | [CalendarEvent] 作成されたイベント | 新しいイベントを作成します。 |
---
### 予定の情報を取得しよう
続いて、先ほど作成した予定を GAS で取得してみましょう。  
Calendarクラスの [getEvents メソッド](https://developers.google.com/apps-script/reference/calendar/calendar#geteventsstarttime,-endtime)で、対象のカレンダーの予定を取得することができます。  
Calendar.getEvents メソッドは **パラメータで取得する予定の範囲を指定する**ことができ、開始日時と終了日時を指定します。

以下のサンプルコードを実行すると、2022年9月1日の予定を取得することができます。  
サンプルコードの **'カレンダーのID'** には任意のカレンダーのIDを指定しましょう。  
{{< tabs groupId="calendar_4_2" >}}
{{% tab name="コード.gs" %}}
```js
function getEvents() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  // 2022年9月1日のカレンダーの予定を取得する
  const events = calendar.getEvents(new Date('2022-09-01 00:00:00'), new Date('2022-09-01 23:59:59'));
  for (let i = 0; i < events.length; i++) {
    const event = events[i];
    const title = event.getTitle();
    const startTime = event.getStartTime();
    const endTime = event.getEndTime();
    const location = event.getLocation();
    const description = event.getDescription();
    console.log(event, title, startTime, endTime, location, description);
  }
}
```
{{% /tab %}}
{{< /tabs >}}
#### Calendar クラスのメソッド
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| getEvents | [Date] 取得する予定の範囲の開始日時、[Date] 取得する予定の範囲の終了日時 | [CalendarEvent[]] 指定した時間範囲内で作成されたイベント | 特定の時間範囲内に発生するすべてのイベントを取得します。 |

#### CalendarEvent クラスのメソッド
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| getTitle | なし | [String] 取得したイベントのタイトル | イベントのタイトルを取得します。 |
| getStartTime | なし | [Date] 取得したイベントの開始時刻 | イベントの開始時刻を取得します。 |
| getEndTime | なし | [Date] 取得したイベントの終了時刻 | イベントの終了時刻を取得します。 |
| getLocation | なし | [String] 取得したイベントの場所 | イベントの場所を取得します。 |
| getDescription | なし | [String] 取得したイベントの説明 | イベントの説明を取得します。 |
---
### 予定の情報を更新しよう
取得した予定はその内容を更新することができます。  
更新対象の予定を特定できたのであれば、各メソッドで予定の内容を変更することができます。  
以下のサンプルコードを実行すると、2022年9月1日の予定のうち、タイトルが New Event の予定の内容が更新されます。  
サンプルコードの **'カレンダーのID'** には任意のカレンダーのIDを指定しましょう。 
{{< tabs groupId="calendar_4_3" >}}
{{% tab name="コード.gs" %}}
```js
function updateEvent() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  // 2022年9月1日のカレンダーの予定を取得する
  const events = calendar.getEvents(new Date('2022-09-01 00:00:00'), new Date('2022-09-01 23:59:59'));
  for (let i = 0; i < events.length; i++) {
    // カレンダーの予定を取得する
	const event = events[i];
    if (event.getTitle() === 'New Event') {
	    event.setTitle('Updated Event');
	    event.setTime(new Date('2022-09-01 15:00:00'), new Date('2022-09-01 16:00:00'));
	    event.setLocation('Tokyo');
	    event.setDescription('This is updated by gas.');
    }
  }
}
```
{{% /tab %}}
{{< /tabs >}}
#### CalendarEvent クラスのメソッド
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| setTitle | [String] イベントの新しいタイトル | なし | イベントのタイトルを設定します。 |
| setTime | [Date] イベントの新しい開始時刻、[Date] イベントの新しい終了時刻 | なし | イベントの開始時刻を設定します。 |
| setLocation | [String] イベントの新しい場所 | なし | イベントの場所を設定します。 |
| setDescription | [String] イベントの新しい説明 | なし | イベントの説明を設定します。 |
--- 
### 予定を削除しよう
最後に GAS で予定を削除してみましょう。  
Calendarクラスの [deleteEvent メソッド](https://developers.google.com/apps-script/reference/calendar/calendar-event#deleteevent)を実行すると、対象の予定を削除することができます。  
以下のサンプルコードは2022年9月1日の予定のうち、タイトルが Updated Event の予定が削除されます。  
サンプルコードの **'カレンダーのID'** には任意のカレンダーのIDを指定しましょう。 
{{< tabs groupId="calendar_4_3" >}}
{{% tab name="コード.gs" %}}
```js
function deleteEvent() {
  // IDが一致するカレンダーを取得する
  const calendar = CalendarApp.getCalendarById('カレンダーのID');
  // 2022年9月1日のカレンダーの予定を取得する
  const events = calendar.getEvents(new Date('2022-09-01 00:00:00'), new Date('2022-09-01 23:59:59'));
  for (let i = 0; i < events.length; i++) {
    // カレンダーの予定を取得する
	const event = events[i];
    if (event.getTitle() === 'Updated Event') {
	    event.deleteEvent();
    }
  }
}
```
{{% /tab %}}
{{< /tabs >}}
#### CalendarEvent クラスのメソッド
| メソッド名 | パラメータ | 戻り値 | 説明 |
| --- |  --- | --- | ---------- |
| deleteEvent | なし | なし | イベントを削除します。 |
