# 気温のモック

今は固定の文字列(hello:world)をmockmockのデバイスが送信してます。もう少し現実的なセンサーのモックとして気温を模した値を送信するようにしましょう。

---

mockmockの管理画面から「グラフ/グラフバリュージェネレータ作成」をクリクします。

![/images/temperature_mock/temperature.jpg](/images/temperature_mock/temperature.jpg)

---

名前を入力します

![/images/temperature_mock/temperature2.jpg](/images/temperature_mock/temperature2.jpg)



| 項目 | 値 |
|--------------------------|----------------|
| グラフバリュージェネレーター名| temperature_gen|


---

擬似的なグラフを設定して値のシミュレートを行います。

具体的な天気情報がほしい場合は検索するか、下記URLを参照してください。

[八代市の1時間天気 tenki.jp](https://tenki.jp/forecast/9/46/8610/43202/1hour.html)

グラフは任意の場所でクリックするとアンカーを追加できます。削除する場合はアンカーを右クリックしてください。

![/images/temperature_mock/temperature3.jpg](/images/temperature_mock/temperature3.jpg)


| 項目(temperature_gen) | 値(例) |
|----------------------|--------|
| 最大値(max)| 28|
| 最小値(min)| 16|
| 周期(T)[sec]| 120|
| 原点の時刻| 2018-08-31T09:00:00+0900|
| ゆらぎ幅| -3 ~ 3|

作成後、**もう一度グラフバリュージェネレータtemperature_gen2**を作成します。

| 項目(temperature_gen2) | 値(例) |
|----------------------|--------|
| 最大値(max)| 24|
| 最小値(min)| 13|
| 周期(T)[sec]| 120|
| 原点の時刻| 2018-08-31T09:00:00+0900|
| ゆらぎ幅| -3 ~ 3|

---

具体的なデータ形式を決めるため、データテンプレートを作成します。

原型となるJSONを登録することで自動的にmockmockが形式を作成してくれます。

![/images/temperature_mock/temperature4.jpg](/images/temperature_mock/temperature4.jpg)

| 項目 | 値 |
|----------------------|--------|
| テンプレート名| temperature sensor default|
| 作成方法| jsonを元にして作成する|

JSONは下記をコピーしてください。

先程グラフバリュージェネレータを2つ作成しましたが、`temperatures`が配列型となっているよう複数のセンサーデータを送信する想定です。

```
{
  "serial_number": "12345",
  "time": "2018-10-15T12:34:56Z",
  "temperature1": "20.5",
  "temperature2": "17.2"
}
```

入力後、「登録」ボタンをクリックしてください。

---

作成完了後、各項目をモック用に調整します。各項目をクリックして修正してください。


|          キー|      型 |  生成タイプ |        field |            format |            name |
|--------------|--------|-----------|--------------|-------------------|-----------------|
| serial_number|  String| mock_const| serial_number|                   |                 |
|          time|  String|       time|              | %Y-%m-%dT%H:%M:%SZ|                 |
|  temperature1|   Float|      graph|              |                   |  temperature_gen|
|  temperature2|   Float|      graph|              |                   | temperature_gen2|


入力後、下記画像のような表示になります。

![/images/temperature_mock/temperature5.jpg](/images/temperature_mock/temperature5.jpg)

---

**mockグループ**を作成します。

![/images/temperature_mock/temperature6.jpg](/images/temperature_mock/temperature6.jpg)


| 項目| 値|
|----|---|
| mockグループ名| temperature sensor|
| 最大稼働時間[sec]| 600|
| mock定数のフィールド| serial_number|

mockステータスから新しく状態を作成します。

![/images/temperature_mock/temperature7.jpg](/images/temperature_mock/temperature7.jpg)

| 項目| 値|
|----|---|
| 状態名| default|
| 初期状態| ☑|
| Topic| hello|
| QoS| 1|
| Retain|  無効|
| 最小データ送信間隔[sec]| 10|
| 最大データ送信間隔[sec]| 10|
| データテンプレート| temperature sensor default|

## モックテスト

一度テスト送信します。

![/images/temperature_mock/temperature8.jpg](/images/temperature_mock/temperature8.jpg)

`serial_number`に適当な文字を入れて送信をクリックします。その後AWS S3にファイルができているか確認してください。

---

## モック作成

Hello Worldのときと同じようにモックを作成します。

「mock作成」をクリックします。

![/images/temperature_mock/temperature9.jpg](/images/temperature_mock/temperature9.jpg)

`serial_number`に適当な文字を入力して、「登録」をクリックします。

![/images/temperature_mock/temperature10.jpg](/images/temperature_mock/temperature10.jpg)


「操作」から「起動」をクリックします。

![/images/temperature_mock/temperature11.jpg](/images/temperature_mock/temperature11.jpg)

起動後、AWS IoTを経由してS3にファイルが作成されます。
それぞれの値が変化しているのを確認してみてください。

