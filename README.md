# README
test
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

## user(顧客)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false, primary key|
|nickname|string|null: false|
|mail|string|null: false|
|password|string|null: false|
|name_cc|string|null: false|
|name_kc|string|null: false|
|birthday|integer|null: false|
|robot_y_n|string|null: false|
|phone number|string|null: false|
|image|string|null: false|
|introduction|string|null: false|
### Association
- has_many :card
- has_many :evaluation(評価)
- has_many :to_do
- has_many :infomation
- has_many :address
- has_many :account(口座)
- has_many :point
- has_many :transfer_application_resume(振込申請履歴)
- has_many :transaction_message(取引メッセージ)
- has_many :reading_attention_resume(閲覧履歴)
- has_many :nice(いいね)

- has_many :user-transaction(顧客-取引)
- has_many :user-product(顧客-商品)
- has_many :before_message(事前メッセージ)

## transaction(取引)テーブル
|Column|Type|Options|
|------|----|-------|
|transaction_id(取引ID)|integer|null: false, primary key|
|product_id(商品ID)|integer|null: false,foreign_key: true|
|user_id|integer|null: false,foreign_key: true|
|address_id|integer|null: false,foreign_key: true|
|date|integer|null: false|
|transaction_situation_id(取引状況ID)|integer|null: false,foreign_key: true|
### Association
- has_many :to_do
- has_many :transaction_message(取引メッセージ)
- has_many :transaction_situation(取引状況)
- has_many :user-transaction(顧客-取引)
- has_many :user-product(顧客ー商品)
- belongs_to :point
- belongs_to :transfer_application_resume(振込申請履歴)

## product(商品)テーブル
|Column|Type|Options|
|------|----|-------|
|product_id(商品ID)|integer|null: false, primary key|
|image|string|null: false|
|value|integer|null: false|
|product_name|string|null: false|
|product_explanation(商品説明)|integer||
|category|integer|null: false|
|product_situation(商品状態)|string||
|postage_burden(送料負担者)|integer|null: false|
|shipping_origin(発送元)|integer|null: false|
|arrival_days(到着日数)|integer||
### Association
- has_many :reading_attention_resume(閲覧履歴)
- has_many :nice(いいね)
- has_many :before_message(事前メッセージ)
- has_many :user-product(顧客-商品)


## user_transaction(顧客-取引)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false, foreign_key: true|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
### Association
- belongs_to :user
- belongs_to :transaction

## user_product(顧客-商品)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false, foreign_key: true|
|product_id(商品ID)|integer|null: false,foreign_key: true|
### Association
- belongs_to :user
- belongs_to :product


## cardsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|card_number|integer|null: false|
|expiration_date(有効期限)|integer|null: false|
|securitycord|integer|null: false|
### Association
- belongs_to :user

## evaluation(評価)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|evaluation(評価)|integer|null: false|
|user_id(評価してくれた人ID)|integer|null: false,foreign_key: true|
|comment|integer||
### Association
- belongs_to :user

## to_doテーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
|text|string|null: false|
### Association
- belongs_to :user
- belongs_to :transaction

## infomationテーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|text|string|null: false|
### Association
- belongs_to :user

## addressテーブル
|Column|Type|Options|
|------|----|-------|
|address_id(お届け先ID)|integer|null: false,primary key|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|name_cc|string|null: false|
|name_kc|string|null: false|
|postal_cord|integer|null: false|
|prefectures(都道府県)|string|null: false|
|municipalities(市町村)|string|null: false|
|house_number(番地)|integer|null: false|
|building_name(建物名)|string|null: false|
|phone number|integer|null: false|
### Association
- has_many :transaction
- belongs_to :user

## account(口座)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|bank|integer|null: false|
|account_type|string|null: false|
|branch_cord(支店コード)|integer|null: false|
|account_cord(口座番号)|integer|null: false|
|account_fa_name(口座名義(セイ))|string|null: false|
|account_fi_name(口座名義(メイ))|string|null: false|
|address(住所)|integer|null: false|
### Association
- belongs_to :user

## pointテーブル
|Column|Type|Options|
|------|----|-------|
|point_id(pointID)|integer|null: false,primary key|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
|point|integer|null: false|
|point_date|integer|null: false|
## Association
- has_many :transaction
- belongs_to :user

## transfer_application_resume(振込申請履歴)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
|transfer_application_date(振込申請日時)|integer|null: false|
|value|integer|null: false|
### Association
- has_many :transaction
- belongs_to :user

## transaction_message(取引メッセージ)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
|transaction_date(取引日時)|integer|null: false|
|text|string||
### Association
- has_many :users
- has_many :transaction

## reading_attention_resume(閲覧履歴)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|product_id(商品ID)|integer|null: false,foreign_key: true|
|reading_date(閲覧日時)|integer|null: false|
### Association
- belongs_to :users
- belongs_to :products

## nice(いいね)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|product_id(商品ID)|integer|null: false,foreign_key: true|
|number|integer|null: false|
### Association
- belongs_to :users
- belongs_to :products

## before_message(前メッセージ)テーブル
|Column|Type|Options|
|------|----|-------|
|user_id(顧客ID)|integer|null: false,foreign_key: true|
|product_id(商品ID)|integer|null: false,foreign_key: true|
user_id(相手ID)|integer|null: false,foreign_key: true|
|before_message_date|integer|null: false|
|text|string||
### Association
- belongs_to :users
- belongs_to :products

## transaction_situation(取引状況)テーブル
|Column|Type|Options|
|------|----|-------|
|transaction_situation_id(取引状況ID)|integer|null: false, primary key|
|transaction_id(取引ID)|integer|null: false,foreign_key: true|
|transaction_situation_date(取引状況日時)|integer|null: false|
|situation|string|null: false|
### Association
- belongs_to :transaction
