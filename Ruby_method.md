# evenメソッド 

対象の要素の値が偶数であれば真を返し、そうでない場合は偽を返す

      ```ruby
      10.even? #=> true

       5.even?  #=> false
       ```
       
[evenメソッド](https://docs.ruby-lang.org/ja/latest/method/Integer/i/even=3f.html)

# .floorメソッド 

小数点を切り捨てる

      ```ruby
    irb(main):001:0> 3.1.floor　=> 3
　　irb(main):002:0> 3.9.floor => 3
      ```
      

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

# sliceメソッド 
配列や文字列から指定した要素を取り出すことができる

   ```ruby
array = [0,1,2,3,4,5,6]
ele1 = array.slice(1)
puts ele1
#=> 1
ele2 = array.slice(-4,4)
puts ele2
#=> 3, 4, 5, 6
puts array 
#=> [0,1,2,3,4,5,6]
 ```
       
[sliceメソッド](https://docs.ruby-lang.org/ja/latest/method/String/i/slice=21.html)


# whileメソッド 
指定された条件が真（true）である間、繰り返し処理（ループ）を行う

   ```ruby
i = 0
while i < 5
  puts i
  i += 1
end
 ```
       
[whileメソッド](https://docs.ruby-lang.org/en/3.0/syntax/control_expressions_rdoc.html#label-while+Loop)


# 範囲演算子（..）
   ```ruby
# 1～6までの範囲を指定して、繰り返し表示
(1..6).each do |num|
  puts num
end
 ```
