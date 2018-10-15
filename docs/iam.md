# IAM作成

## IAMについて

AWS Identity and Access Management（以下、IAM）は認証を管理するサービスです。アカウント作成でログインできるようになるユーザはルートユーザと呼びすべての権限を保持しています。そのままでは開発者やアプリケーションの権限としては大きすぎるため一般的にIAMを使ってアカウントを新しく発行し権限を付与します。

IAMで発行できるものにはユーザの他にもユーザをグルーピングできるグループや、サービスに対して権限を定義できるロールなどがあります。

## 利用ユーザの作成

基本的にルートユーザは利用しないようにすることが良いとされています。AWSなどのクラウドサービスはアカウントを盗られると多額の請求をされてしまう場合があります。基本的に2段階認証の設定をおすすめします。

参考: [https://aws.amazon.com/jp/iam/details/mfa/](https://aws.amazon.com/jp/iam/details/mfa/)


これから、普段の開発用ユーザをIAMで作成して権限を付与していきます。

---

以下のURLからログイン画面を表示します。

[https://console.aws.amazon.com/console/home](https://console.aws.amazon.com/console/home)

![/images/iam/signin.jpg](/images/iam/signin.jpg)

1. アカウント作成で入力したメールアドレスを入力して「次へ」をクリック
2. パスワードを入力してサインイン

もし画像のような表示の場合は赤枠のリンクをクリックしてください

![/images/iam/signin2.jpg](/images/iam/signin2.jpg)

---

ログインするとAWSのコンソール画面が表示されます。

![/images/iam/dashboard.jpg](/images/iam/dashboard.jpg)

簡単に画面を説明をします。

![/images/iam/dashboard2.jpg](/images/iam/dashboard2.jpg)

1. ①を押すとAWSのサービス一覧が表示されます。ここから各サービスページへアクセスできます。
2. ②は利用したいサービス名を検索して表示することができます。
3. ③にログインしてるユーザ名が表示されます。ここからアカウント情報ページや請求ダッシュボードにいけます。
4. ④は選択しているリージョンが表示されます。AWSではサービスはリージョン（地域）ごとに提供されます。

---

IAMサービスページに移動します。

![/images/iam/iam.jpg](/images/iam/iam.jpg)

入力欄に「IAM」を入力して、出てきたセレクトボックスをクリックして移動します。

---

![/images/iam/iam2.jpg](/images/iam/iam2.jpg)

「ユーザ」をクリックします。

---

![/images/iam/iam3.jpg](/images/iam/iam3.jpg)

「ユーザの追加」をクリックします。

---

![/images/iam/iam4.jpg](/images/iam/iam4.jpg)

1. ① 新しくログインに使用するユーザ名を入力します。ここでは `iot_user` とします
2. コマンドラインなどでこのアカウントを使用する場合、②にチェックします
3. コンソール画面にログインするユーザの場合、③にチェックします
4. ④で新しいユーザのパスワードを設定
5. パスワードのリセットが必要のチェックは外す
6. 「次のステップ:アクセス権限」をクリック

---

作成するユーザに権限を付与します。  
今回は利便性のために管理者向けの機能を除いたすべてのAWSサービスが利用できるPowerUserAccessを付与します。
またあとでロール作成のためIAMFullAccessも付与します。

![/images/iam/iam5.jpg](/images/iam/iam5.jpg)

1. ① 「既存のポリシーを直接アタッチ」を選択
2. ② 「PowerUserAccess」で検索
3. ③ 「PowerUserAccess」にチェックする

![/images/iam/iam5_2.jpg](/images/iam/iam5_2.jpg)

1. ② 「IAMFullAccess」で検索
2. ③ 「IAMFullAccess」にチェックする
3. 「次のステップ:確認」ボタンをクリック

![/images/iam/iam6.jpg](/images/iam/iam6.jpg)

`PowerUserAccess`と`IAMFullAccess`がついていることを確認して「ユーザの作成」をクリックします。

---

![/images/iam/iam7.jpg](/images/iam/iam7.jpg)

1. CSV(①)またはメール(①')でアクセスキーをバックアップします
2. IAMユーザのログインURLを開きます

---

![/images/iam/iam8.jpg](/images/iam/iam8.jpg)

先ほど作成したIAMユーザでログインします。最初から入力されている数字はAWSのアカウントIDになります。  
ログインに成功するとAWSコンソール画面が表示されます。

---

以上で、IAMの説明とIAMユーザ作成が終わりました。

注意点として今回作成したIAMユーザではIAMユーザの編集権限はありません。  
AWSではIAMと他のサービスで別の権限として扱われています。IAM編集機能を持たせたい場合はルートユーザでログインユーザに `IAMFullAccess` の権限（または個別のIAM権限）を付与してください。
