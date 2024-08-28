# MySQLのエラーが出た場合
以下を追記して、rspecコマンドでテストを実行する。

config/environments/test.rb
```ruby
Rails.application.configure do

 #省略

 config.active_job.queue_adapter = :inline #追記

 #省略
```
config.active_job.queue_adapter = :inline は、Active Job のキュー・アダプターを設定するための設定。
Active JobはRailsの背後でジョブを実行するためのフレームワークで、"inline" アダプターはジョブをすぐに実行する。
つまり、この設定は該当のジョブが非同期でなく、即時に実行されるようにする。
テスト環境では非同期のジョブを待つ時間を持つことが多くないため、ジョブを即座に実行することで、その結果をテストと組み合わせて確認することができる。
furimaアプリでは、ユーザー保存→商品情報保存　からの購入情報保存のテストを実行していたため、テストコードの実行までにユーザー保存というジョブが完了していなかった可能性がある。
よって以下のエラーが表示されていた。https://gyazo.com/6eb9dea692b4db9ad261c060378d35c8
