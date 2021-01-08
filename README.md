# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

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