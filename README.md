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