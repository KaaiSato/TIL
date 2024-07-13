# evenメソッド 

対象の要素の値が偶数であれば真を返し、そうでない場合は偽を返す

      ```ruby
      10.even? #=> true

       5.even?  #=> false
       ```
       
[evenメソッド](https://docs.ruby-lang.org/ja/latest/method/Integer/i/even=3f.html)


# include?メソッド 

指定した値が、配列中に含まれているかを判定する。指定した値が含まれている場合はtrueを、含まれていない場合はfalseを返り値として返す。

      ```ruby
      array = ["foo", "bar"]　
      　puts array.include?("bar")　　#=> true
　　　　puts array.include?("hoge")　#=> false
       ```



# indexメソッド 

文字列や配列の中に指定した文字列が含まれていた場合、その文字列の開始位置を整数の値で返す

      ```ruby
      str.index(検索したい文字列, [検索を開始する位置])
       ```
       
[indexメソッド](https://docs.ruby-lang.org/ja/latest/method/String/i/index.html)


# scanメソッド 

対象の要素から引数で指定した文字列を数え、配列として返す

      ```ruby
      "foobarbazfoobarbaz".scan("ba")
       => ["ba", "ba", "ba", "ba"]
       ```
       
[scanメソッド](https://docs.ruby-lang.org/ja/latest/method/String/i/scan.html)
