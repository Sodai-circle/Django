# Django

- Nginx + Django + uWSGI + Mysqlの環境です

  

## DjangoDock

1. リポジトリからクローン

   ```
   git clone https://github.com/Sodai-circle/Django.git django_app/djangodock
   ```

2. djangodock階層で

   ```
   cp env-example .env
   ```

   必要に応じて編集する

3. 同じくdjangodock階層で

   ```
   docker-compose build workspace nginx mysql
   ```

4. djangoアプリ作成

   ```
   docker-compose run workspace django-admin startproject app .
   ```

5. settings.pyに以下を追加

   ```
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': 'default',
           'USER': 'default',
           'PASSWORD': 'secret',
           'HOST': 'mysql',
           'PORT': '3306',
       }
   }
   ```

6. マイグレーションの実行

   ```
   docker-compose run workspace bash -c "python ./manage.py makemigrations && python ./manage.py migrate"
   ```

7. Settings.pyに追加

   ```
   import os
   
   STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
   ```

8. ```
   docker-compose run workspace ./manage.py collectstatic
   ```

9. コンテナ起動  **必ずmysqlを先に起動**

   ```
   docker-compose up -d mysql && docker-compose up -d workspace nginx
   ```

10. [ここに](http:localhost)アクセスし、うまくいっているか確認

## 使い方

- 始めるとき djangodockの階層で
   ```bash
   docker-compose up -d mysql && docker-compose up -d workspace nginx
   ```
- 終わるとき
   ```bash
   docker-compose down
   ```

