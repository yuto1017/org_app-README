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
- Basic認証パスワード：
- Basic認証ID：admin

# 利用方法
## 新規登録
1．ログイン画面の左下の「Sign up」から新規登録ページへ進む。<br>
2．ファイル選択のボタンを押して登録するアカウント画像を選択する。br>
3．「Nickname」、「Email」、「Password」を入力する。<br>
4．「Authority」は必要に応じて選択する。 ※<br>
5．「Create Account」ボタンを押して新規登録が完了する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;※「管理者」は全権限を有し、担当者は、タスクの新規作成、編集、削除以外の機能を使用することができる。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;閲覧者はタスクの情報などの閲覧のみが可能である。<br>

## タスクの作成
1．サイドバーの「タスクの作成」をクリックしてタスクの新規作成ページへ進む。<br>
2．「タスクの名称」、「タスクの説明」、「開始日」、「完了日」、「担当者」、「管理者」を入力する。<br>
3．「Create Task」ボタンを押してタスクの新規作成を完了する。<br>
&nbsp;&nbsp;&nbsp;&nbsp;※作成後に遷移したタスクの詳細表示ページにて、タスクの情報が表示される。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;「リマインダーの作成」、「進捗報告」、「チャットの作成」をクリックすることで各機能の作成ページへ遷移するとができる。<br>

## リマインダーの作成
1．タスクの詳細表示ページにて、「リマインダーの作成」をクリックしてリマインダーの作成ページへ進む。<br>
2．「リマインダーの日付」、「リマインダーの時刻」、「リマインダーのメッセージ」を入力する。<br>
3．「Create Remainder」ボタンを押してリマインダーの作成を完了する。<br>
4．作成後に遷移したタスクの詳細表示ページにて、「リマインダーの日時」、「リマインダーの編集」、「リマインダーの削除」が<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;表示される。<br>

## 進捗報告の作成
1．タスクの詳細表示ページにて、「進捗報告」をクリックして進捗報告の作成ページへ進む。<br>
2．「進捗状況」を選択し、「進捗率」、「進行時間」、「振り返り」、「その他、コメントなど」（任意）を入力する。<br>
3．「Create Report」ボタンを押して進捗報告の作成を完了する。<br>
4．作成後に遷移したタスクの詳細表示ページにて、「タスクの進捗状況」が「未着手」から入力した内容に変更され、<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;「進捗報告一覧」が表示される。「進捗報告一覧」をクリックして進捗報告の詳細情報を確認することができる。<br>

## チャットの作成
1．サイドバーの「チャットの作成」をクリックしてチャットの作成ページへ進む。<br>
2．「タスク」、「ユーザー」を選択する。<br>
3．「Create Chat」ボタンを押してチャットの作成を完了する。<br>
4．作成後に遷移したタスクの詳細表示ページにて、「チャット」が表示され、メッセージを入力して「送信」ボタンを<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;押すことでメッセージが表示される。<br>

# アプリケーションを作成した背景
タスク管理は、作業の最小単位であるタスクを細分化し、タスクに優先順位を設けて適切な順序で実施できるように管理することであるが、タスク管理を行うために、用途に応じてツールを使い分けているケースがあり、その場合は「タスクの進捗状況」や「タスクの情報共有」などのタスクの一元管理が困難であると仮説を立てた。同様の問題を抱えている方はいると考え、これらの課題解決を図ってタスクの一元管理ができるアプリケーションを開発することにした。<br>
また、タスクの進捗などに対して他のユーザーとチャット形式でに相談できるようにプラスαの機能を用いることで他のタスク管理のアプリケーションとの差別化を図る。

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

