# アプリケーション名
タスク管理アプリ  TAMT（タント）<br>
&nbsp;&nbsp;※TAMTは&nbsp;&nbsp;&nbsp;&nbsp;Task Auxiliary Management Tool（タスク補助管理ツール）の各単語の頭文字をとった略称

# アプリケーションの概要
複数のツールを用いることなく、下記のメリットから効率的にタスク管理が行うことができる。<br>
&nbsp;&nbsp;・タスクの可視化によってタスクの見落としがなくなる<br>
&nbsp;&nbsp;・進捗状況の把握が可能で担当者と管理者間でタスクの情報共有<br>
&nbsp;&nbsp;・単一ツールで一元管理することで複数のツールを必要としない

# URL
https://org-app-40428.onrender.com

# テスト用アカウント


# 利用方法


# アプリケーションを作成した背景

# 洗い出した要件

#


# 実装予定の機能
- プロジェクト管理機能
- タスクの検索機能
- カレンダー表示機能

# データベース設計



# 画面遷移図



# テーブル設計

### users テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| nickname           | string  | null: false               |
| email              | string  | null: false, unique: true |
| encrypted_password | string  | null: false               |
| authority_id       | integer | null: false               |

### Association

- has_many :tasks
- has_many :reports
- has_many :sendmessages
- has_many :personaltasks

### tasks テーブル

| Column             | Type       | Options                                        |
| -------------------| ---------- | ---------------------------------------------- |
| user               | references | null: false, foreign_key: true                 |
| title              | string     | null: false                                    |
| description        | text       | null: false                                    |
| start_date         | date       | null: false                                    |
| completion_date    | date       | null: false                                    |
| assignee           | references | null: false                                    |
| assignee_nickname  | string     | null: false, foreign_key: { to_table: :users } |
| admin              | references | null: false                                    |
| admin_nickname     | string     | null: false, foreign_key: { to_table: :users } |

### Association

- belongs_to :user
- belongs_to :assignee, class_name: "User"
- belongs_to :admin, class_name: "User"
- has_one :reminder
- has_many :reports
- has_one :chat
- has_many :personaltasks

### reminders テーブル

| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| task               | references | null: false, foreign_key: true |
| reminder_date      | date       | null: false                    |
| reminder_time      | time       | null: false                    |
| message            | text       |                                |
| displayed          | boolean    | default: false                 |

### Association

- belongs_to :task

### reports テーブル

| Column              | Type       | Options                        |
| --------------------| ---------- | ------------------------------ |
| task                | references | null: false, foreign_key: true |
| user                | references | null: false, foreign_key: true |
| progress_status_id  | integer    | null: false                    |
| progress_percentage | integer    | null: false                    |
| progress_time       | time       | null: false                    |
| think_back          | text       | null: false                    |
| comment             | text       |                                |

### Association

- belongs_to :task
- belongs_to :user

### chats テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| task      | references | null: false, foreign_key: true |
| user      | references | null: false, foreign_key: true |

### Association

- belongs_to :task
- belongs_to :user
- has_many :sendmessages

### sendmessages テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| chat      | references | null: false, foreign_key: true |
| user      | references | null: false, foreign_key: true |
| content   | text       | null: false                    |

### Association

- belongs_to :chat
- belongs_to :user

### personaltasks テーブル

| Column    | Type       | Options                        |
| ----------| ---------- | ------------------------------ |
| task      | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :task


## 開発環境

| カテゴリー                | 名称           | バージョン  |
| -------------------------| -------------- | -----------|
| プログラミング言語（※）   | Ruby           | 3.2.0     |
| フレームワーク            | Ruby on Rails  | 7.0.8.4    |
| データベース              | MySQL          | 5.7.44     |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;※一部の機能でJava Scriptを使用


## ローカルでの動作方法

以下のコマンドを順に実行。<br>
% git clone [https://github.com/yuto1017/org_app](https://github.com/yuto1017/org_app)<br>
% cd org_app<br>
% bundle install<br>
% yarn install<br>

## 工夫したポイント

