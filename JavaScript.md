#　javascriptファイルを読み込む
・memo.jsを読み込みたい場合、Rails7dではimportMapを利用する

config/import.rb
```ruby
# Pin npm packages by running ./bin/importmap

pin "application", preload: true
pin "@hotwired/turbo-rails", to: "turbo.min.js", preload: true
pin "@hotwired/stimulus", to: "stimulus.min.js", preload: true
pin "@hotwired/stimulus-loading", to: "stimulus-loading.js", preload: true
pin_all_from "app/javascript/controllers", under: "controllers"
pin "memo", to: "memo.js"  #memo.jsをmemoという名称でインポートできる
```

app/javascript/application.js
```ruby
// Configure your import map in config/importmap.rb. Read more: https://github.com/rails/importmap-rails
import "@hotwired/turbo-rails"
import "controllers"
import "memo" #読み込んだファイルをアプリケーションで動作する
```





# toLocaleString メソッド
　数値をカンマ区切りにする
 ```javascript
var number = 4000000;
var formattedNumber = number.toLocaleString(); // "4,000,000"
 ```


　
