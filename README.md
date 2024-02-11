# django-tutorial

## 実行手順書(pwsh)

1. venvを用いた仮想環境を構築
```pwsh
python3 -m venv venv
```

2. venvを有効化
```pwsh
.\venv\bin\Activate
```

3. Djangoのインストール
```pwsh
pip install django
```

4. Djangoプロジェクトの作成
```pwsh
django-admin startproject mysite
```
このコマンドの意味は、`mysite`という名前のプロジェクトを作成するという意味です。
具体的には、以下の通りです。
・django-adminコマンドは、Djangoのプロジェクトを作成するためのコマンドです。
・startprojectは、プロジェクトを作成するためのコマンドです。
・mysiteは、プロジェクトの名前です。

5. プロジェクトのディレクトリに移動
```pwsh
cd mysite
```
※これはvenvを有効化した状態で行ってください。

6. プロジェクトの起動
```pwsh
python manage.py runserver
```

7. サーバーは、デフォルトで8000番ポートで起動します。ブラウザで以下のURLにアクセスしてください。
http://{ポート番号}/
※ポート番号は、コマンドラインに表示されているものを使用してください。

8. アプリケーションの作成
```pwsh
python manage.py startapp polls
```
このコマンドの意味は、`polls`という名前のアプリケーションを作成するという意味です。
具体的には、以下の通りです。
・startappは、アプリケーションを作成するためのコマンドです。
・pollsは、アプリケーションの名前です。
なぜ、manage.pyを使ってアプリケーションを作成するのかというと、manage.pyは、プロジェクトのための様々な管理コマンドを提供しているためです。
manage.pyは、コマンドライン引数を受け取り、それに応じた処理を行います。

## 参考文献
https://docs.djangoproject.com/ja/3.2/intro/tutorial01/