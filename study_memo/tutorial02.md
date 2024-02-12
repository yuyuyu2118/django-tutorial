# はじめてのDjangoアプリ作成、その2

1. Databaseの設定
mysite/settings.pyを開きます。
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```
ENGINEは、データベースの種類を指定します。データベースの種類は、SQLite3、PostgreSQL、MySQL、Oracleなどがあります。デフォルトでは、SQLite3が指定されています。
NAMEは、データベースのファイル名を指定します。デフォルトでは、db.sqlite3が指定されています。
複数のデータベースを使いたい場合は、以下のようにしてください。
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    },
    'users': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_database_name',
        'USER': 'your_username',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```
usersという名前のデータベースを作成し、PostgreSQLを使う場合は、上記のようにしてください。
他のDBを使いたい場合は、データベースバインディングをインストールしてください。
```pwsh
pip install psycopg2
```

2. mysite/settings.pyの他の設定
```python
LANGUAGE_CODE = 'ja'
TIME_ZONE = 'Asia/Tokyo'
```
LANGUAGE_CODEは、言語コードを指定します。デフォルトでは、en-usが指定されています。jaを指定すると、日本語になります。
TIME_ZONEは、タイムゾーンを指定します。デフォルトでは、UTCが指定されています。Asia/Tokyoを指定すると、日本時間になります。

3. データベースの作成
```pwsh
python manage.py migrate
```
データベースを作成します。
migrateとは、データベースのスキーマを作成するためのコマンドです。
```pwsh
(venv) PS C:\Users\sasar\OneDrive\デスクトップ\practice\django-practice\mysite>sqlite3 db.sqlite3 ".schema"
CREATE TABLE IF NOT EXISTS "django_migrations" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "app" varchar(255) NOT NULL, "name" varchar(255) NOT NULL, "applied" datetime NOT NULL);
CREATE TABLE sqlite_sequence(name,seq);
CREATE TABLE IF NOT EXISTS "auth_group_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "group_id" integer NOT NULL REFERENCES "auth_group" ("id") DEFERRABLE INITIALLY DEFERRED, "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE TABLE IF NOT EXISTS "auth_user_groups" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED, "group_id" integer NOT NULL REFERENCES "auth_group" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE TABLE IF NOT EXISTS "auth_user_user_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED, "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE UNIQUE INDEX "auth_group_permissions_group_id_permission_id_0cd325b0_uniq" ON "auth_group_permissions" ("group_id", "permission_id");    
CREATE INDEX "auth_group_permissions_group_id_b120cbf9" ON "auth_group_permissions" ("group_id");
CREATE INDEX "auth_group_permissions_permission_id_84c5c92e" ON "auth_group_permissions" ("permission_id");
CREATE UNIQUE INDEX "auth_user_groups_user_id_group_id_94350c0c_uniq" ON "auth_user_groups" ("user_id", "group_id");
CREATE INDEX "auth_user_groups_user_id_6a12ed8b" ON "auth_user_groups" ("user_id");
CREATE INDEX "auth_user_groups_group_id_97559544" ON "auth_user_groups" ("group_id");
```
データベースが作成されました。

4. モデルの作成
```python
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
これは、Questionという名前のモデルを作成するコードです。
モデルは、データベースのテーブルに対応します。
Questionモデルは、question_textとpub_dateという2つのフィールドを持っています。
Choiceモデルは、questionとchoice_textとvotesという3つのフィールドを持っています。
それぞれのフィールドについて、以下のように説明します。
- **Questionモデル**
    - question_text: 質問の内容を格納するフィールドです。
    - pub_date: 質問の公開日時を格納するフィールドです。
- **Choiceモデル**
    - question: 質問に対する選択肢を格納するフィールドです。
    - choice_text: 選択肢の内容を格納するフィールドです。
    - votes: 選択肢の投票数を格納するフィールドです。

5. INSTALLED_APPSにアプリケーションの設定を加える
```python
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
PollsConfigクラスは、polls/apps.pyにあるので、パスの指定ではpolls.apps.PollsConfigとなる。

6. 再度migrationを行う。
```pwsh
py manage.py makemigrations polls
```
どのようなSQLが実行されるかの確認
```pwsh
py manage.py sqlmigrate polls 0001
```

makemigrations後に再度migrateを行う
```pwsh
py manage.py migrate
```

これで更新が完了する。

7. shell内でdatabadeの操作を行う。
以下のコマンドを実行してみる

```pwsh
py manage.py shell
```
```python
from polls.models import Question, Choice
from django.utils import timezone
q = Question(question_text="What's new?", pub_date=timezone.now())