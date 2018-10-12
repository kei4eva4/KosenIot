# リソース削除

今回のハンズオンで作成したリソースは以下になります。  
基本的に無料となる範囲のリソースを指定してますが、将来的に無料を保証するものではないため不要なものは削除してください。


また、Elasticsearch Serviceに関しては公開状態のためハンズオン終了後**必ず**削除してください。

## リソース一覧

AWSリソース

- AWS IoT
    - 管理/タイプ(helloIotType)
        - 先に廃止をして、削除する必要あり
    - 安全性/証明書(helloIotPolicy)
    - ポリシー
    - ACT(helloIotRule)
- S3
    - バケット(helloiot-namae)
- Elasticsearch Service
    - ドメイン(hello-iot)
        - 「ドメインの削除」をクリック
- IAM
    - Role各種

mockmock

- mockグループ
    - hello iot group
    - temperature sensor
- データテンプレート
    - temperature sensor default
- グラフバリュージェネレータ
    - temperature_gen
    - temperature_gen2
