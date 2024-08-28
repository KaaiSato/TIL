# 環境変数の設定
アプリケーションのダッシュボード　Environmentより設定

Environment Variables / Add Environment Variableで項目追加

ex)Basic認証の場合

　・【ID】　Key：　BASIC＿AUTH_USER　　　　Value：任意
 
　・【Password】　Key：　BASIC＿AUTH_PASSWORD　　Value：任意
 
 




# データベース(PostgreSQL)のリセット
render-build.sh
```ruby
#　bundle exec rake db:migrate　
DISABLE_DATABASE_ENVIRONMENT_CHECK=1 bundle exec rake db:migrate:reset  
```
以上記述した後、commmit,pushを行う
リセットされた後は、コメントアウトを戻し、resetの記述を削除しておかないと毎回リセットされるので注意する