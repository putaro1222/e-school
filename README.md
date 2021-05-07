# README

アプリケーション名	

アプリケーション概要	このアプリケーションでできることを記述。

URL	デプロイ済みのURLを記述。デプロイが済んでいない場合は、デプロイが完了次第記述すること。

テスト用アカウント	ログイン機能等を実装した場合は、ログインに必要な情報を記述。またBasic認証等を設けている場合は、そのID/Passも記述すること。

利用方法	このアプリケーションの利用方法を記述。

目指した課題解決	このアプリケーションを通じて、どのような人の、どのような課題を解決しようとしているのかを記述。

洗い出した要件	スプレッドシートにまとめた要件定義を記述。

実装した機能についての画像やGIFおよびその説明	実装した機能について、それぞれどのような特徴があるのかを列挙する形で記述。画像はGyazoで、GIFはGyazoGIFで撮影すること。

実装予定の機能	洗い出した要件の中から、今後実装予定の機能がある場合は、その機能を記述。

データベース設計	ER図等を添付。

ローカルでの動作方法

# テーブル設計

## users テーブル

| Column             | Type   | Options                   |
| ------------------ | ------ | --------------------------|
| nickname           | string | null: false               |
| email              | string | null: false, unique: true |
| encrypted_password | string | null: false               |
| age                | integer| null: false               |
| sex_id             | integer| null: false               |
| area_id            | integer| null: false               |

### Association

- has_many :lectures
- has_many :curriculums
- has_one  :address


## curriculums テーブル

| Column      | Type       | Options                        |
| ----------- | ---------- | ------------------------------ |
| category_id | integer    | null: false                    |
| class_name  | string     | null: false                    |
| class_info  | text       | null: false                    |
| class_url   | string     |                                |
| user        | references | null: false, foreign_key: true |

### Association

- has_one    :lecture
- belongs_to :user


## lectures テーブル

| Column     | Type       | Options                        |
| -----------| ---------- | ------------------------------ |
| user       | references | null: false, foreign_key: true |
| curriculum | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :lecture


## address テーブル

| Column          | Type            | Options                  |
| ----------------| --------------- | ------------------------ |
| last_name       | string    | null: false                    |
| first_name      | string    | null: false                    |
| last_name_kana  | string    | null: false                    |
| first_name_kana | string    | null: false                    |
| birthday        | date      | null: false                    |
| postal_code     | string    | null: false                    |
| prefecture_id   | integer   | null: false                    |
| city            | string    | null: false                    |
| block           | string    | null: false                    |
| building        | string    |                                |
| phone_number    | string    | null: false                    |
| user            | references| null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one    :card


## card テーブル

| Column         | Type       | Options                        |
| ---------------| ---------- | ------------------------------ |
| card_token     | string     | null: false                    |
| customer_token | string     | null: false                    |
| address        | references | null: false, foreign_key: true |

### Association

- belongs_to :address
