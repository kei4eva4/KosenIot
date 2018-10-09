# デバイスの作成

## AWS IoTのエンドポイントを取得
- AWS IoT管理画面のサイドバーの設定を選択
- カスタムエンドポイントをコピーしておく
![/images/handson/device2.jpg](/images/handson/device2.jpg)

## mockmockのコンソールからプロジェクトを作成
- [mockmockのコンソール](https://console.mock-mock.com/)を開く
- 「プロジェクトを作成」をクリック
![/images/handson/device1.jpg](/images/handson/device1.jpg)

- 送信先ホストは先ほど管理画面からコピーしたものを入力
- 証明書ファイル、秘密鍵ファイル、Root証明書ファイルは先ほどダウンロードしたものを添付
- すべての項目を入力後「登録」ボタンをクリック
![/images/handson/device3.jpg](/images/handson/device3.jpg)

## データテンプレートを作成
- サイドバーのデータテンプレート→データテンプレート作成をクリック
- テンプレート名を入力し、「登録」をクリック
![/images/handson/device4.jpg](/images/handson/device4.jpg)

## mockグループを作成
- サイドバーのmockグループ作成をクリック
- mockグループ名、最大稼働時間を入力し、「登録」をクリック
![/images/handson/device5.jpg](/images/handson/device5.jpg)

## mockステータスを作成
- タブのmockステータスをクリック
- 「mockステータス作成」をクリック
![/images/handson/device6.jpg](/images/handson/device6.jpg)
- すべての項目を入力後「登録」ボタンをクリック
![/images/handson/device7.jpg](/images/handson/device7.jpg)

## テスト送信
- テスト送信の「送信」をクリック
![/images/handson/device8.jpg](/images/handson/device8.jpg)
- 下記のように表示されれば成功
![/images/handson/device9.jpg](/images/handson/device9.jpg)
- AWS IoT管理画面のモニタリングをクリック、下記のように表示される
![/images/handson/device10.jpg](/images/handson/device10.jpg)

## mockを起動
- タブのmock管理をクリック
- 「mock作成」をクリック
![/images/handson/device11.jpg](/images/handson/device11.jpg)
- 「登録」をクリック
![/images/handson/device12.jpg](/images/handson/device12.jpg)
- mock一覧→操作から「起動」をクリック
![/images/handson/device13.jpg](/images/handson/device13.jpg)

## S3でデータを確認
- AWSコンソールからS3を開く
![/images/handson/device14.jpg](/images/handson/device14.jpg)
- バケットの一覧から先ほど作成したバケットを選択
![/images/handson/device15.jpg](/images/handson/device15.jpg)
- データを確認
![/images/handson/device17.jpg](/images/handson/device17.jpg)