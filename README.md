# README
# What's HappySky?

- Purpose
  HappySkyは、主にbeatmaniaIIDXというゲームにおいて、友人同士でスコアアタック大会を開催したい時に利用しやすいことを想定した、スコア管理やチャットができるWebアプリケーションです。
  beatmaniaIIDXに限らず、様々なゲームのスコアを競うような場面において有効活用できるものと期待しています。
  
- Function
  ユーザー新規登録、編集機能
  グループ設定(大会設定)機能
  チャット、画像投稿機能
  新規メンバー招待機能
  スコア登録、編集、削除機能

# HappySkyのDB設計

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|mail|string|null: false|
|password|string|null: false|

### Association
- has_many :messages
- has_many :groups, through: :groups_users
- has_many :groups_users
- has_many :scores

## groupsテーブル

|Column|Type|Options|
|------|----|-------|
|groupname|string|null: false|
|user_id|integer|null: false, foreign_key: true|

### Association
- has_many :messages
- has_many :users, through: :groups_users
- has_many :groups_users
- has_many :scores

## groups_usersテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user

## massagesテーブル

|Column|Type|Options|
|------|----|-------|
|content|text|null: false|
|image|string||
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user


## Scoresテーブル
|Column|Type|Options|
|------|----|-------|
|title|text|null: false|
|score|integer|null: false|
|user_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user