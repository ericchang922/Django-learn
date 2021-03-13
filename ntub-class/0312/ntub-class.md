# 3/12 class
開始先建立資料夾並且git init
1. 建立gitignore  
2. 可以在github的github底下找到適合各種語言的gitignore的檔案   
[github/gitignore](https://github.com/github/gitignore)
3. 在gitignore裡面新增以下內容，避免git將設定檔上傳
    ```
    # macOS
    .DS_Store

    # VSCode
    .vscode/

    # Pycharm
    .idea/
    ```
4. 安裝python~~~(第二新的版本)
5. 安裝虛擬環境
    mac:
    ```
    pip3 install --user pipenv

    python3 -m pipenv install
    ```

    windows-git bash:
    ```
        # --user 只安裝在當前使用者的資料夾
        $ pip install --user pipenv

        # 設定讀取使用者環境變數
        $ setx PATH "%PATH%;%USERPROFILE%\AppData\Roaming\Python\Python38\Scripts"

        $ pipenv --version
        pipenv, version 2020.11.15

        # 建立虛擬環境
        $ pipenv install

        # 移除虛擬環境
        $ pipenv --rm

        # 開啟虛擬環境
        $ pipenv shell

        # 關閉虛擬環境
        $ exit

        # 確認使用虛擬環境的 Python
        $ which python
        /c/Users/User/.virtualenvs/django-ntub-class-pGb9Kqx9/Scripts/python
    ```
6. 安裝程式碼排版工具 - Flake8
    **安裝時加上--dev為開發工具，不會部署在伺服器**
    ```
    python3 -m pipenv install --dev flake8 flake8-commas
    ```
    安裝完成之後在pycharm 中的Pipfile檔案中的[dev-packages]裡面可以看到：
    ```
    flake8 = "*"
    flake8-commas = "*"
    ```
    檢查檔案不需要包括套件等檔案：
    ```
    flake8 --show-source --statistics --exclude venv,.venv,migrations .
    ```
7. 安裝Django
    ```
    python3 -m pipenv install django
    ```
8. 新建專案
    ```
    python3 -m pipenv shell
    django-admin startproject core .
    ```
9. 新增app  
    1. 在專案根目錄建立一個python project 叫app  
    2. 在app中新建一個空的tutorial資料夾  
    3. 
        ```
        python manage.py startapp tutorial app/tutorial
        ```
10. 在tutorial 中的 veiws.py 可以新增程式  
    如：
    ```python
    from django.http import HttpRequest, HttpResponse
    from django.shortcuts import render

    # Create your views here.
    def hello_world(request: HttpRequest) -> HttpResponse:
        return HttpResponse('<h1>Hello, world!</h1>')
    ```
11. 在tutorial新增一個 urls.py
    如：
    ```python
    from django.contrib import admin
    from django.urls import path

    from . import views

    urlpatterns = [
        path('hello-world/', views.hello_world),
    ]

    ```
12. 原本core 的 url.py
    則是：
    ```python
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('',include('app.tutorial.urls')),
        path('admin/', admin.site.urls),
    ]
    ```
13. 執行專案
    ```
    python3 manage.py runserver
    ```
14. 剛才的 server 在 localhost:8000
15. control+c可停止伺服器，exit可以離開虛擬環境