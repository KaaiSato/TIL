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

# ~省略~
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




