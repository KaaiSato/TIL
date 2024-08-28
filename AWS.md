# S3で画像を保存する  
 IaC(Infrastructure as Code) サーバーなどのインフラ環境ををCLIを用いて管理すること  
## AWS CloudShellを用いてバケットを作成し、セキュリティ対策をする(ex,バケット名：furima40467)  
- バケットを作成する
  $ aws s3 mb s3://furima40467
- バケットが作成できたか確認する  
  $ aws s3 ls
- 所有者を確認する
  $ aws s3api get-bucket-ownership-controls --bucket furima40467
- AWSにアップロードするときに暗号化する（サーバーサイド暗号化）
  $ aws s3api get-bucket-encryption --bucket furima40467
- 外部からのアクセスは全てブロックする
  $ aws s3api get-public-access-block --bucket furima40467
- アクセスを許可する（ファイルをアップロードできるようにする）
  $ aws s3api put-public-access-block --bucket furima40467 --public-access-block-configuration '
{
    "BlockPublicAcls": true,
    "IgnorePublicAcls": true,
    "BlockPublicPolicy": false,
    "RestrictPublicBuckets": false

}'  
- IAMユーザー一覧を取得する(arn:aws:iam::xxxxxxxxxxx:user/ユーザー名をコピーする)
  $ aws iam list-users
- ホームディレクトリ/s3/polisy.jsonに以下を記載し、それをコピペしてコマンドに打ち込み、バケットポリシーを設定する
  $ aws s3api put-bucket-policy --bucket furima40467 --policy "$(cat << EOF
{
   "Version": "2012-10-17",
   "Id": "Policy1544152951996",
   "Statement": [
       {
           "Sid": "Stmt1544152948221",
           "Effect": "Allow",
           "Principal": {
               "AWS": "arn:aws:iam::905418298931:user/Satoka_tech_camp"
           },
           "Action": "s3:*",
           "Resource": "arn:aws:s3:::furima40467"
       }
   ]
}
EOF

)"  

- バケットポリシーを取得して設定を確認する
  $ aws s3api get-bucket-policy --bucket furima40467

## 画像の保存先の指定
- まずはｚｓｈに環境変数を設定する

- config/storage.yml
```ruby
test:
  service: Disk
  root: <%= Rails.root.join("tmp/storage") %>

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>

amazon:
  service: S3
  region: ap-northeast-1
  bucket:  （自身のバケット名が記載されている状態です）
  access_key_id: <%= ENV['AWS_ACCESS_KEY_ID'] %>
  secret_access_key:  <%= ENV['AWS_SECRET_ACCESS_KEY'] %>
```

- ローカル環境

config/envrionments/develpoment.rb
```ruby
config.active_storage.service = :amazon
```

- 本番環境  
config/envrionments/develpoment.rb
```ruby
config.active_storage.service = :amazon
```



## git-secrets
AWSが公開しているツール。commitするコードにパスワードが含まれていると、警告が出て処理が行われないようにする。

## secret key  base

secret_key_base は、Ruby on Railsアプリケーションにおいて、セキュリティのために使用される重要な設定項目。
- セッションデータの暗号化:Railsでは、ユーザーのセッションデータ（ログイン状態やその他のセッション情報）をクライアント側（ブラウザ）に保存します。その際のデータの暗号化や署名に使用される。
- CSRF（クロスサイトリクエストフォージェリ）保護:CSRFトークンの生成にも使用されます。CSRF攻撃からアプリケーションを守るために、リクエストごとに一意の認証トークンを生成する
- Cookieの署名:署名付きCookieを使う場合、secret_key_baseはその署名の生成にも使用される。

## ポート一覧
- HTTP (ポート番号: 80) 
  種類: TCP
  役割: ウェブサーバーへの通常のHTTPトラフィック（未暗号化）を許可。

- HTTPS (ポート番号: 443)
  種類: TCP
  役割: ウェブサーバーへの安全なHTTストラフィック（暗号化）を許可。

- SSH (ポート番号: 22)
  種類: TCP
  役割: サーバーへの安全なシェルアクセスを許可します。主に管理者がリモート接続に使用。

- MySQL/Aurora (ポート番号: 3306)
  種類: TCP
  役割: MySQLデータベースへの接続を許可。RDSでのMySQLやAuroraで使用。

- PostgreSQL (ポート番号: 5432)
  種類: TCP
  役割: PostgreSQLデータベースへの接続を許可。

- RDP (ポート番号: 3389)
  種類: TCP
  役割: Windowsサーバーへのリモートデスクトップ接続を許可。

- SMTP (ポート番号: 25)
  種類: TCP
  役割: メール送信サーバー（SMTPプロトコル）のトラフィックを許可します。

- Custom TCP/UDP 
  種類: TCP/UDP
  役割: 任意のアプリケーションやサービスが使用するポート。



