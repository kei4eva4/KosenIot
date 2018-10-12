# Elaticsearch Service

Elaticsearch Serviceを利用してデータをグラフ化します。

AWS IoTのルールの`HelloIotRule`を開きます。

![/images/elasticsearch/elasticsearch1.jpg](/images/elasticsearch/elasticsearch1.jpg)

「アクションの追加」ボタンをクリックします。

![/images/elasticsearch/elasticsearch2.jpg](/images/elasticsearch/elasticsearch2.jpg)

「Amazon Elasticsearch Serviceにメッセージを送信する」にチェックします。

![/images/elasticsearch/elasticsearch3.jpg](/images/elasticsearch/elasticsearch3.jpg)


まだElasticsearch Serviceを起動していないため新しく作成します。
「新しいリソースを作成する」をクリックします。

![/images/elasticsearch/elasticsearch4.jpg](/images/elasticsearch/elasticsearch4.jpg)

新しくElasticsearch Serviceのページが開きます。
「新しいドメインの作成」をクリックします。

![/images/elasticsearch/elasticsearch5.jpg](/images/elasticsearch/elasticsearch5.jpg)

Elasticserach Serviceのウィザードが開かれます。

ドメイン名を`hello-iot`として「次へ」をクリックします。

![/images/elasticsearch/elasticsearch6.jpg](/images/elasticsearch/elasticsearch6.jpg)


画像の用に値を設定します。

![/images/elasticsearch/elasticsearch7.jpg](/images/elasticsearch/elasticsearch7.jpg)

![/images/elasticsearch/elasticsearch8.jpg](/images/elasticsearch/elasticsearch8.jpg)

インスタンスサイズを`t2.small`にしたことを確認したら「次へ」をクリックします。


Elasticsearch Serviceを運用するネットワーク環境を設定します。  
今回は作業簡易化するためだれでもアクセス可能な公開状態で設定します。  
本番利用する場合は、VPCのネットワークを新規で作成して配置してください。

「パブリックアクセス」にチェックしてください。

![/images/elasticsearch/elasticsearch9.jpg](/images/elasticsearch/elasticsearch9.jpg)


アクセスポリシーを選択します。
「テンプレート選択」から「ドメインへのオープンアクセス許可」をクリックします。

![/images/elasticsearch/elasticsearch10.jpg](/images/elasticsearch/elasticsearch10.jpg)

ダイアログが表示されるため、「リスクに同意します」をチェックして「OK」をクリックします。

![/images/elasticsearch/elasticsearch11.jpg](/images/elasticsearch/elasticsearch11.jpg)

画像のようなJSONが入力されたことを確認して「次へ」をクリックします。

![/images/elasticsearch/elasticsearch12.jpg](/images/elasticsearch/elasticsearch12.jpg)

確認画面が表示されるので「確認」をクリックします。

![/images/elasticsearch/elasticsearch13.jpg](/images/elasticsearch/elasticsearch13.jpg)


Elasticserach Serviceが起動して作成中になります。
アクティブになるまで数分かかるので待ちます。

![/images/elasticsearch/elasticsearch14.jpg](/images/elasticsearch/elasticsearch14.jpg)


アクティブ表示になったら、AWS IoTの画面に戻ります。
更新ボタンを押して`hello-iot`を指定します。

![/images/elasticsearch/elasticsearch15.jpg](/images/elasticsearch/elasticsearch15.jpg)

その後表示された入力項目を埋めます。　

|           ID|       索引|        タイプ|
|-------------|----------|-------------|
| ${newuuid()}| hello-iot| temperatures|

これらはElasticsearch Serviceのための設定です。  
Elasticsearch Serviceでデータを一意にするよう`newuuid`関数を利用しています。  
索引とタイプはRDBでいう、データベースとテーブルの関係になります。  

AWS IoTからElastic Searchserviceにデータを登録できるようにロールを作成します。
「新しいロールの作成」をクリックします。

![/images/elasticsearch/elasticsearch16.jpg](/images/elasticsearch/elasticsearch16.jpg)

ロール名として`aws-iot-to-elasticsearch-role`と入力します。  
「新しいロールの作成」をクリックします。

![/images/elasticsearch/elasticsearch17.jpg](/images/elasticsearch/elasticsearch17.jpg)


先程作った`aws-iot-to-elasticsearch-role`を設定して「アクションの追加」をクリックします。

![/images/elasticsearch/elasticsearch18.jpg](/images/elasticsearch/elasticsearch18.jpg)


ここまでで、AWS IoTでの設定作業は終了です。
mockmockで温度のモックを起動して、AWS IoT経由でElasticsearch Serviceにデータを送信しましょう。

---

AWSでElasticearch Serviceを起動するとビジュアライズするためのKibanaを一緒に利用できるようになります。  
画像の箇所のURLをクリックしてKibanaを起動しましょう。

![/images/elasticsearch/elasticsearch19.jpg](/images/elasticsearch/elasticsearch19.jpg)


サイドバーの「Management」から最初のKibanaの設定をします。

![/images/elasticsearch/elasticsearch20.jpg](/images/elasticsearch/elasticsearch20.jpg)


「Index Patterns」をクリックします。

![/images/elasticsearch/elasticsearch21.jpg](/images/elasticsearch/elasticsearch21.jpg)

Kibanaにどんなデータが入ってるかを教えるためIndex patternを登録します。  
ここでは先程AWS IoTで設定した`hello-iot*`を入力して「> Next Step」をクリックします。

![/images/elasticsearch/elasticsearch22.jpg](/images/elasticsearch/elasticsearch22.jpg)

タイムに関するプロパティを指定します。ここでは`time`を選択して「Create index pattern」をクリックします。

![/images/elasticsearch/elasticsearch23.jpg](/images/elasticsearch/elasticsearch23.jpg)

インデックスの作成が完了すると画像のような画面になります。すでに登録されたデータを解析して自動で型を設定してくれます。

![/images/elasticsearch/elasticsearch24.jpg](/images/elasticsearch/elasticsearch24.jpg)

サイドバーからDiscoverをクリックしてデータが入っているか確認しましょう。  
問題なければ画像のような画面になります。

![/images/elasticsearch/elasticsearch24_2.jpg](/images/elasticsearch/elasticsearch24_2.jpg)

---

入ってきているデータをビジュアライズしましょう。  

サイドバーの「Visualize」ボタンをクリックします。

![/images/elasticsearch/elasticsearch25.jpg](/images/elasticsearch/elasticsearch25.jpg)

ラインチャートを組むため「Line」をクリックします。

![/images/elasticsearch/elasticsearch26.jpg](/images/elasticsearch/elasticsearch26.jpg)

`hello-iot*`をクリックします。

![/images/elasticsearch/elasticsearch27.jpg](/images/elasticsearch/elasticsearch27.jpg)

チャートを設定と表示する画面になります。
サイドバーからチャート設定を行います。  
Y-Axisを開きます。

![/images/elasticsearch/elasticsearch28.jpg](/images/elasticsearch/elasticsearch28.jpg)


画像のようにY軸にtemperature1/2を表示するように設定します。

![/images/elasticsearch/elasticsearch29.jpg](/images/elasticsearch/elasticsearch29.jpg)

次にX軸を設定します。
「X-Axis」をクリックします。

![/images/elasticsearch/elasticsearch30.jpg](/images/elasticsearch/elasticsearch30.jpg)

X軸を時間にするため、画像のように設定します。

![/images/elasticsearch/elasticsearch31.jpg](/images/elasticsearch/elasticsearch31.jpg)


再生ボタンをクリックすると、設定が反映されてチャートが表示されます。
X軸の設定を変えたり、Aggregationを変更したりしてみてください。

![/images/elasticsearch/elasticsearch32.jpg](/images/elasticsearch/elasticsearch32.jpg)

---

以上で、ハンズオンの資料は終了です。  
おつかれさまでした🍵
