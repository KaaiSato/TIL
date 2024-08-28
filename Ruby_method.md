# absメソッド

数値オブジェクト（整数、小数点数など）に対して、その数値の絶対値を取得できる。

```ruby
n = -10 
n.abs
# => 10
```



# downcaseメソッド

大文字を小文字に変換する
```ruby
# 大文字を含んだ文字列を定義
irb(main):001:0> name = "Hiabc"
=> "Hiabc"

# downcaseメソッドを使用し、小文字に変換
irb(main):002:0> name.downcase
=> “hiabc”
```

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


# randメソッド

０から指定した数未満の数値をランダムに生成する  

      ``ruby
     num = rand(100)
     puts num
     => 32  # 0~99の範囲でランダムな数字が生成された

     num = rand(100)
     puts num
     => 74  # 0~99の範囲でランダムな数字が生成された

       ```
　　
　　　　　　　


# scanメソッド 

対象の要素から引数で指定した文字列を数え、配列として返す

      ```ruby
      "foobarbazfoobarbaz".scan("ba")
       => ["ba", "ba", "ba", "ba"]
       ```
       
[scanメソッド](https://docs.ruby-lang.org/ja/latest/method/String/i/scan.html)


# shuffleメソッド
配列の要素をランダムにシャッフルし、その結果を配列として返す
  ```ruby
# shuffleメソッドで配列をシャッフルし、変数animalsに代入
animals = ["cat", "dog", "rabbit"].shuffle

puts animals
# => ["rabbit", "cat", "dog"]
  ```
[shuffleメソッド](https://docs.ruby-lang.org/ja/latest/method/Array/i/shuffle.html)

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


# バイナリーサーチ
ソート済みのリストや配列に入ったデータ（同一の値はないものとする）に対する検索を行うときに用いられる手法。
まず、中央の値を確認し、検索したい値との大小関係を用いて、検索したい値が中央の値の右にあるか、左にあるかを判断します。
それを繰り返し、片側には存在しないことを確かめながら検索していく。

ex)
```ruby
def binary_search(array ,target_num ,number_of_elements)
  left_index = 0
  right_index = number_of_elements - 1
  
  while left_index <= right_index do
    center_index = (left_index + right_index) / 2 
    if array[center_index] == target_num
    return center_index
    elsif  array[center_index] < target_num
      left_index = center_index + 1
    else 
      right_index = center_index - 1
    end
  end
  return -1
end

array=[1,3,5,6,9,10,13,20,26,31]
puts "検索したい数字を入力して下さい"
target = gets.to_i
number_of_elements = array.length
result = binary_search(array ,target ,number_of_elements)

if result == -1
  puts "#{target}は配列内に存在しません"
else 
  puts "#{target}は配列の#{result}番目に存在します"
end
```


# 範囲演算子（..）
   ```ruby
# 1～6までの範囲を指定して、繰り返し表示
(1..6).each do |num|
  puts num
end
 ```