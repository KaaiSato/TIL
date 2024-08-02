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

# Application Record
Rails 5から導入されたクラスで、自分たちが作るすべてのモデルが継承する親クラス。ActiveRecord::Baseを継承している。
ApplicationRecordとそのサブクラス（作るモデル全て）にActive Recordの機能が提供される
例えば、全モデルに共通するスコープやバリデーション、コールバックなどはApplicationRecordに定義し、
個々のモデル固有のものは各モデルのクラスに定義する。
ApplicationRecordを継承していれば**saveメソッド**や**createメソッド**は、設定したバリデーションが実行される。


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

# exists?
モデル（テーブル）の中に対応するレコードが存在するかを調べるActiveRecordメソッドの一つ。引数にキーとバリューを持つ。

ex)Orderテーブルに対応するitemが存在するかどうか？
```html
<% if Order.exists?(item_id: item.id) %> 
  <div class='sold-out'>
    <span>Sold Out!!</span>
  </div>
<% end %>
```
  ※ただし、実装上のパフォーマンス等を考慮すると、ビューで直接データベースの操作をするのではなく、コントローラで事前に必要な情報を取得・計算しておくと良い。
  
  ※ もしモデル（テーブル）に存在しないことを確認する場合は、否定形を用いる
  ```ruby
  !Order.exists?(item_id: item.id)
  ```

# git-secrets
Gitリポジトリに機密情報（秘密鍵、パスワード、APIキーなど）が誤ってコミットされるのを防ぐためのツール。  
開発の際に機密情報がリポジトリに含まれないようにする。


# turbo機能
TurboはRailsの一部であるHotwireの機能の一つで、ページ遷移を高速化するために使用される。Turboにより、全ページのリロードを行わずに、部分的なページの更新（HTMLの一部を切り替える）が可能になり、高速なページ遷移を実現する。
しかし、全てのケースでTurboが有効に機能するわけではなく、特定のJavaScriptのイベントやライブラリが正常に動作しない場合など、Turboとの互換性に問題があるケースがある。
data: { turbo: false }は、特定のリンクまたはフォームに対してTurbo機能を無効化し、そのリンクやフォームは従来のページのフルリロードを行う。



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
validates :prefecture, numericality: { other_than: 0, message: "can't be blank" }  # 都道府県のプルダウンを選択。０：ーー　を選択するとエラーになる
```



＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

# requireメソッド　とpresence: trueのバリデーションについて
requireメソッドとpresence: trueバリデーションは、どちらも「値がない場合」に対する処理を行うものではあるが、その対象となる値と処理のタイミングが異なる

- requireメソッドはコントローラーでリクエストパラメーターを取り扱う際に利用します。ここでは、指定したキーがパラメーター群（params）中に存在することを保証します。存在しないときにはエラーActionController::ParameterMissingを発生させます。このチェックはモデルにデータが渡される前、つまりデータベースに保存される前の初期段階で行われます。
- presence: trueバリデーションはモデルに定義され、モデルのインスタンスがデータベースに保存される前にその属性値が存在すること（nilや""（空文字）でないこと）をチェックします。もし存在しない場合、そのデータはデータベースに保存されず、Railsはそのデータが無効であることを通知します。

したがって、requireメソッドはパラメータが送られてくることを、presence: trueはそのパラメータ（あるいは他の方法で設定された属性）が存在する値であることを保証する。

