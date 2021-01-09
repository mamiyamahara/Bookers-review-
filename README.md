# README

①カラム　指定できる型

string : 文字列
text : 長い文字列
integer : 整数
float : 浮動小数
decimal : 精度の高い小数
datetime : 日時
timestamp : タイムスタンプ
time : 時間
date : 日付
binary : バイナリデータ
boolean : Boolean


②rootパスの設定
root to: 'コントローラー名#アクション名'


③null制約
migrateファイルに以下記載
「 t.データ型 "カラム名", null: false 」
rails db:migrateで反映


④validates
モデルに以下記載する。(空欄でない制約)
「 validates :カラム名, presence: true 」


⑤flashメッセージ
・コントローラーで表示したいメッセージを設定
「 flash[notice] = "表示したいメッセージを記載" 」
・Viewページの表示したい場所に以下記載。
  <%= flash[:notice] %>


⑥文字色について
HTML直書きのものがCSSに書いたものより優先される。
pタグ直書きで反映されない場合、spanタグに変更すると反映された。


⑦form_for　フォームのサイズ指定
f,text_area :カラム名, size: "大きさ(ヨコ)x大きさ(タテ)"

fieldは小さめのテキストBox
areaは大きめのテキストBox

⑧一覧表示の順番を変更する
@変数名s = モデル名.all.order(created_at: :desc) #=>新しい順の投稿一覧
#created_atは作成日時　descは降順
@変数名s = モデル名.all.order(created_at: :asc)#=> 古い順の投稿一覧
#created_atは作成日時　ascは昇順

⑨エラーメッセージの表示
・複数箇所にエラーメッセージを表示させたい場合は、
　エラーメッセージ用のビューファイルを作成し、以下記述してrenderで使い回す。
・一箇所だけしか使わない場合は、表示させたいビューファイルに以下を直書きしても使える。

<% if @変数名.errors.any? %>
  <div class="alert alert-warning">(Bootstrapの装飾)
    <ul>
        <%= @変数名.errors.count %>errors prohibited this obj from being saved:
        <br>
        <% @変数名.errors.full_messages.each do |message| %>
            <li><%= message %></li>
      <% end %>
    </ul>
  </div>
<% end %>

・@変数名.errors.any?で全ての属性のうち１つでもエラーがあったかどうかをチェック。
・エラーメッセージはエラーが発生すると、「error.full_message」内に格納される。
・複数エラーが出ている場合もあるので、each doで回して全て表示させる。
・失敗時のviewの読み込みはrenderを使用する。
　※redirect_toにすると新しいviewページが呼ばれてしまい、ページに書いたif文が反応しない。
　redirect_to…ルーティングを通り、新たにviewページを呼び出す。
　render…ルーティングを通らず、viewページに飛ぶ。


・renderでエラーメッセージのビューファイルを呼び出す時は、以下のように記述する。

<%= render 'layouts/error_messages(エラーメッセージのファイル名)', model: f.object %>

f.objectは、form_for (中略) do |f|のf部分にあたる。
ここで変数を使うより、f.objectとしておけばどのページでも使えるのでこのまま覚える。