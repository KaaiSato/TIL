# test
- user単体
- trainer単体

# 実装中
reservationのnew.html.erb
trainer_idを渡す

エURLがhttp://localhost:3000/reservations/new?trainer_id=8のようになっているのは、リンク生成時にtrainer_idがクエリパラメータとして渡されているためです。これは意図した動作ですが、フォームでその値を受け取って正しく処理するための追加の手順が必要です。


1. newアクションでのtrainer_idの受け取り

まず、newアクションでparams[:trainer_id]を受け取り、それをフォームに渡す必要があります。


def new
  @reservation_address = ReservationAddress.new(trainer_id: params[:trainer_id])
end

2. フォームでの隠しフィールドの追加

フォームに隠しフィールドを追加し、trainer_idをフォームデータとして送信できるようにします。


フォームの修正 (reservations/new.html.erb)

<%= form_with model: @reservation_address, url: reservations_path do |f| %>
  <!-- フォームの他のフィールド -->
  <%= f.hidden_field :trainer_id, value: @reservation_address.trainer_id %>

  <div class="actions">
    <%= f.submit "予約する" %>
  </div>
<% end %>

3. ReservationAddressモデルのコンストラクタの修正

もし必要であれば、ReservationAddressモデルにtrainer_idをコンストラクタで正しく受け取れるように設定します。


class ReservationAddress
  include ActiveModel::Model
  attr_accessor :trainer_id, :user_id, :last_name, :first_name, :last_name_reading, :first_name_reading, :date, :time_id, :request, :prefecture_id, :city, :addresses, :phone_number

  validates :trainer_id, presence: true  # 必要ならバリデーションを追加
  # 既存のバリデーションとメソッド

  def save
    reservation = Reservation.create(trainer_id: trainer_id, user_id: user_id, last_name: last_name, first_name: first_name, last_name_reading: last_name_reading, first_name_reading: first_name_reading, date: date, time_id: time_id, request: request)
    Address.create(prefecture_id: prefecture_id, city: city, addresses: addresses, phone_number: phone_number, reservation_id: reservation.id)
  end
end

全体の流れ


trainers/show.html.erbから正しくリンクを生成し、trainer_idをクエリパラメータとして渡す。

newアクションでtrainer_idを受け取り、ReservationAddressモデルのインスタンスに含める。

フォームに隠しフィールドを追加し、trainer_idを含める。

createアクションでtrainer_idを含んだパラメータを受け取り、処理する。


これらの手順を踏むことで、trainer_idが正しくフォームに渡され、保存されることを確認できます。


引き続き頑張ってください！応援しています。問題があればまた質問してくださいね。

