
# テーブル設計

## users テーブル

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

## tasks テーブル

| Column             | Type       | Options                                        |
| -------------------| ---------- | ---------------------------------------------- |
| user               | references | null: false, foreign_key: true                 |
| title              | string     | null: false                                    |
| description        | text       | null: false                                    |
| start_date         | date       | null: false                                    |
| completion_date    | date       | null: false                                    |
| worker             | references | null: false                                    |
| worker_nickname    | string     | null: false, foreign_key: { to_table: :users } |
| admin              | references | null: false                                    |
| admin_nickname     | string     | null: false, foreign_key: { to_table: :users } |

### Association

- belongs_to :user
- belongs_to :assignee, class_name: "User"
- belongs_to :admin, class_name: "User"
- has_one :reminder
- has_many :reports
- has_one :chat

## reminders テーブル

| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| task               | references | null: false, foreign_key: true |
| reminder_date      | date       | null: false                    |
| reminder_time      | time       | null: false                    |
| message            | text       |                                |
| displayed          | boolean    | default: false                 |

### Association

- belongs_to :task

## reports テーブル

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

## chats テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| task      | references | null: false, foreign_key: true |
| user      | references | null: false, foreign_key: true |

### Association

- belongs_to :task
- belongs_to :user
- has_many :sendmessages

## sendmessages テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| chat      | references | null: false, foreign_key: true |
| user      | references | null: false, foreign_key: true |
| content   | text       | null: false                    |

### Association

- belongs_to :chat
- belongs_to :user


## 今後実装したい機能
- プロジェクト管理機能
- タスクの検索機能
- カレンダー表示機能
