# はじめてのDjangoアプリ作成、その1

1. venvを用いた仮想環境を構築
```pwsh
python3 -m venv venv
```
venvという名前の仮想環境を作成します。
python3の代わりに、pythonやpyを使っても構いません。
-mオプションは、モジュールを指定するためのオプションです。
venvは、Python3.3以降に標準で付属しているモジュールです。
venvの後に続くvenvは、仮想環境の名前です。
例えば、myenvという名前の仮想環境を作成する場合は、以下のようにしてください。
```pwsh
python3 -m venv myenv
```
ここで、pythonのバージョンを指定したい場合は、以下のようにしてください。
```pwsh
python3.8 -m venv venv
```
この場合は、Python3.8を使ってvenvを作成します。しかし、Python3.8がシステムにインストールされていない場合は、エラーが発生します。
今回python3 --versionと入力したところ、Python 3.10.11と表示されたので、仮想環境内のPythonのバージョンは3.10.11になります。

2. venvを有効化
```pwsh
.\venv\bin\Activate
```
もしくは
```pwsh
.\venv\Scripts\Activate
```
binとScriptsのどちらかにActivateがあるはずです。
もし、Activateが見つからない場合は、venvを作り直してください。
仮想環境が有効化されると、コマンドプロンプトの左側に(venv)と表示されます。myenvという名前の仮想璃面を有効化した場合は、(myenv)と表示されます。
pythonのバージョンを確認したい場合は、以下のようにしてください。
```pwsh
python --version
```
今回はPython 3.10.11と表示されたので、仮想環境内のPythonのバージョンは3.10.11になります。

3. Djangoのインストール
```pwsh
pip install django
```
Djangoをインストールします。
pipは、Pythonのパッケージ管理ツールです。
Djangoは、PythonのWebフレームワークです。

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
有効化しているかどうかは、コマンドプロンプトの左側に(venv)と表示されているかどうかで判断できます。
venv部分は、仮想環境の名前になります。myenvという名前の仮想環境を作成した場合は、(myenv)と表示されます。

6. プロジェクトの起動
```pwsh
python manage.py runserver
```
もし、サーバーのポート番号を変更したい場合は、以下のようにしてください。
```pwsh
python manage.py runserver 8080
```
manage.pyは、プロジェクトのための様々な管理コマンドを提供しています。
runserverは、サーバーを起動するためのコマンドです。

7. サーバーは、デフォルトで8000番ポートで起動します。ブラウザで以下のURLにアクセスしてください。
※ポート番号は、コマンドラインに表示されているものを使用してください。
今回の場合、
http://127.0.0.1:8000/
にアクセスします。

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

9. mysiteのディレクトリを確認
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py

manage.pyは、プロジェクトのための様々な管理コマンドを提供しています。
__init__.pyは、そのディレクトリがPythonパッケージであることを示すためのファイルです。
settings.pyは、プロジェクトの設定を管理するファイルです。
urls.pyは、URLのルーティングを行うためのファイルです。
asgi.pyは、ASGI互換のWebサーバーを実行するためのファイルです。
wsgi.pyは、WSGI互換のWebサーバーを実行するためのファイルです。

10. pollsのディレクトリを確認
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py

__init__.pyは、そのディレクトリがPythonパッケージであることを示すためのファイルです。
admin.pyは、管理サイトのための設定を行うファイルです。
apps.pyは、アプリケーションの設定を行うファイルです。
migrations/は、データベースのマイグレーションファイルが格納されるディレクトリです。
models.pyは、データベースのモデルを定義するファイルです。
tests.pyは、テストコードを記述するファイルです。
views.pyは、ビューを定義するファイルです。

11. pollsのviews.pyを編集
```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```
これは、pollsアプリケーションのビューを定義するコードです。
ビューは、Webアプリケーションのビジネスロジックを記述するための場所です。
このビューは、HTTPリクエストを受け取り、HTTPレスポンスを返す関数です。
このビューは、"Hello, world. You're at the polls index."という文字列を含むHTTPレスポンスを返します。

DjangoはMVC（Model-View-Controller）フレームワークとして知られていますが、正確にはMTV（Model-Template-View）パターンに従います。
- **Model（モデル）**: データベースの構造（スキーマ）を定義し、データの操作を行うための場所です。`models.py`ファイルで定義されます。
- **Template（テンプレート）**: ユーザーインターフェースの構造とレイアウトを定義します。HTMLを生成するためのファイルです。
- **View（ビュー）**: ユーザーからのHTTPリクエストを受け取り、テンプレートを使用してHTTPレスポンスを生成します。`views.py`ファイルで定義される関数やクラスによって構成されます。

12. pollsのurls.pyを作成
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
これは、pollsアプリケーションのURLを定義するコードです。
urlpatternsは、URLパターンのリストです。
path()関数は、URLパターンを定義するための関数です。
- 第1引数は、URLパターンを表す文字列です。: これは、空の文字列を指定しています。空の文字列は、ルートURLを表します。今回の場合、ルートURLは、http://127.0.0.1:8000/polls/にマッチします。
- 第2引数は、ビュー関数を指定します。: これは、views.pyファイル内のindex関数を指定しています。
- 第3引数は、URLパターンの名前を指定します。: これは、indexという名前を指定しています。ここで指定した名前は、テンプレート内でURLを参照するために使用されます。参照時の例は、後述します。

13. mysiteのurls.pyを編集
```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
これは、mysiteプロジェクトのURLを定義するコードです。
urlpatternsは、URLパターンのリストです。
path()関数は、URLパターンを定義するための関数です。
- 第1引数は、URLパターンを表す文字列です。: これは、'polls/'という文字列を指定しています。'polls/'は、http://127.0.0.1:8000/polls/にマッチします。
- 第2引数は、include()関数を指定します。: これは、pollsアプリケーションのURLをインクルードするための関数です。
次の行は、adminサイトのURLを定義しています。
- 第1引数は、URLパターンを表す文字列です。: これは、'admin/'という文字列を指定しています。'admin/'は、http://127.0.0.1:8000/admin/にマッチします。
- 第2引数は、admin.site.urlsを指定します。: これは、adminサイトのURLを定義するための関数です。この関数は、adminサイトのURLを有効にするためのものです。これは、Djangoが提供する機能です。
admin.site.urls以外のURLパターンをインクルードする場合は、いつでもinclude()を使うべきです。

14. サーバーを起動
```pwsh
python manage.py runserver
```
ここで、http://127.0.0.1:8000/polls/にアクセスしてください。
これで、pollsアプリケーションのビューが表示されるはずです。