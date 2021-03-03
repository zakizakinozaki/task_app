# テーブル設計

## usersテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| nickname           | string     | null :false               |
| email              | string     | null :false, unique: true |
| encrypted_password | string     | null :false               |

### Association

- has_many :room_users
- has_many :rooms, through: room_users
- has_many :messages
- has_many :outputs
- has_many :questions
- has_many :comments
- has_many :tasks
- has_many :boards

## rooms テーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| name               | string     | null :false               |

### Association

- has_many :room_users
- has_many :users, through: room_users
- has_many :messages
- has_many :questions

## room_users テーブル

| Column       | Type       | Options                        |
| ------------ | ---------- | ------------------------------ |
| user_id      | references | null: false, foreign_key: true |
| room_id      | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user

## messages テーブル

| Column       | Type       | Options                        |
| ------------ | ---------- | ------------------------------ |
| content      | text       | null: false                    |
| user_id      | references | null: false, foreign_key: true |
| room_id      | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user

## boardsテーブル

| Column             | Type       | Options                   |
| ------------------ | ---------- | ------------------------- |
| project            | text       | null: false               |
| user_id            | references | foreign_key :true         |

### Association

- has_many   :lists
- belongs_to :user

## listsテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| program            | text       | null :false               |
| board_id           | references | foreign_key :true         |

### Association

- has_many :cards
- belongs_to :board

## cardsテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| task               | text       | null :false               |
| memo               | text       |                           |
| list_id            | references | foreign_key :true         |

### Association

- belongs_to :list

## outputsテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| heading            | text       | null :false               |
| description        | text       | null :false               |
| user_id            | references | foreign_key :true         |

### Association

- belongs_to :user

## questionsテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| title              | text       | null :false               |
| quest              | text       | null :false, unique: true |
| user_id            | references | foreign_key :true         |
| room_id            | references | foreign_key :true         |

### Association

- belongs_to :user
- belongs_to :room
- has_many :comments

## commentsテーブル

| Column             | Type       | Option                    |
| ------------------ | ---------- | ------------------------- |
| text               | text       | null :false               |
| user_id            | references | foreign_key :true         |
| question_id        | references | foreign_key :true         |

### Association

- belongs_to :user
- belongs_to :question