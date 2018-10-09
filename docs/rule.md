# ルールを作成

## AWS IoTの管理画面でルールを作成する
- サイドバーからACTを選択し、「作成」をクリック
![/images/handson/rule1.jpg](/images/handson/rule1.jpg)

- 名前、SQLバージョン、ルールクエリステートメントを入力
- 「アクションの追加」をクリック
![/images/handson/rule2.jpg](/images/handson/rule2.jpg)

- Amazon S3バケットにメッセージを格納するにチェックを入れて、「アクションの設定」をクリック
![/images/handson/rule3.jpg](/images/handson/rule3.jpg)

- 「新しいリソースを作成する」をクリック
![/images/handson/rule4.jpg](/images/handson/rule4.jpg)

- 「バケットを作成する」をクリック
![/images/handson/rule5.jpg](/images/handson/rule5.jpg)

- 「バケット名」を入力（この名前はAWS全体でユニークである必要があります）
- 「作成」をクリック
![/images/handson/rule6.jpg](/images/handson/rule6.jpg)

- S3バケットとキーを入力
    - S3バケットが表示されない場合は更新ボタンを押してください
    - キーは「data-${timestamp()}」と入力
- 「新しいロールの作成」をクリック
![/images/handson/rule7.jpg](/images/handson/rule7.jpg)

- IAMロール名を入力し、「新しいロールの作成」をクリック
![/images/handson/rule8.jpg](/images/handson/rule8.jpg)

- 「アクションの追加」をクリック
![/images/handson/rule9.jpg](/images/handson/rule9.jpg)

- 「ルールの作成」をクリック
![/images/handson/rule10.jpg](/images/handson/rule10.jpg)
