# データベース(PostgreSQL)のリセット
render-build.sh
```ruby
#　bundle exec rake db:migrate　
DISABLE_DATABASE_ENVIRONMENT_CHECK=1 bundle exec rake db:migrate:reset  
```
以上記述した後、commmit,pushを行う
リセットされた後は、コメントアウトを戻し、resetの記述を削除しておかないと毎回リセットされるので注意する
