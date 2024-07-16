# ActiveModel::Model モジュール
このモジュールをincludeすると、そのクラスはモデルが持つ機能を持つことができる。Formオブジェクト作成の際に用いる。
・属性の読み書き
・デフォルトのバリデーション（validatesメソッドなど）
・アクティブレコードとの親和性（フォームヘルパーやurlヘルパー）といった機能が提供される
ActiveModel::Modelを使用した例
```ruby
class Person
  include ActiveModel::Model

  attr_accessor :name, :age
  validates :name, presence: true
  validates :age, numericality: { only_integer: true }
end
```
Personクラスはデータベースとは独立しており、一時的にモデルとして振舞う。

# attr_accessor
Rubyの組み込みメソッド。特定のクラスインスタンス変数に対するgetterとsetterを一度に定義。毎回手作業でgetterとsetterを書く手間を省くことができる

・getter：インスタンス変数の値を読み出すメソッド。

・setter：インスタンス変数に値を設定するメソッド。

```ruby
class Car
  attr_accessor :color
end

car = Car.new
car.color = "Red"  # setterを使用して値を設定
puts car.color     # getterを使用して値を取得 => "Red"
```
上記のattr_accessor :colorは以下のコードと等価
```ruby
def color
  @color
end

def color=(value)
  @color = value
end
```



# index: true
マイグレーションファイルでカラム名の後に記述する。指定したカラムに対してデータベースのインデックスを作成するという意味です。データベースのインデックスは、データ検索を高速化する役割を果たす。
一般的に、頻繁に検索や絞り込みに使われるカラムにはインデックスを設けると良い。

# numericality
バリデーションを設定する際、指定されたカラムに対して数値かどうかを検証するヘルパー。エラーメッセージも組み込むことができる。
```ruby
validates :price, numericality: true #値が数値であることを要求
validates :quantity, numericality: { only_integer: true }  #数値が整数であることを要求
validates :age, numericality: { greater_than_or_equal_to: 13, less_than_or_equal_to: 120, message: "is invalid"} #数値が特定の範囲に含まれていることを要求
validates :investment, numericality: { greater_than: 0 } #数値が特定の値より大きい（もしくは小さい）ことを要求
```

