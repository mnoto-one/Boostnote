---
title: 4 - How to run django on openlitespeed
tags: []
---

### 💬 Django Setup

💬 If you haven’t installed Django, please do so through pip3


🔰 Terminal
```sh
pip3 install django
```
📝 Create demo project under the **/var/www/html/** folder.

📝 Create the folder if it doesn’t exist.

```sh
mkdir -p /var/www/html/
cd /var/www/html/
django-admin startproject demo
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Django settings

📝 Edit **settings.py** inside the inner folder (may be demo/demo) to allow hosts
```python
...
ALLOWED_HOSTS = ['*']
...
STATIC_URL = '/python/static/'
STATIC_ROOT = '/var/www/html/demo/public/static'
```
📝 **/python/static/** depends on your context settings

📝 putting the **static** folder under **public** is required

📝 Collect static files in the directory where manage.py exists (may be one level up)

🔰 Terminal
```sh
mkdir -p public/static
python3 manage.py collectstatic
```
📝 Create admin super user

🔰 Terminal
```sh
python3 manage.py migrate
python3 manage.py createsuperuser
Copy
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Change owner

📌 Centos:

🔰 Terminal
```sh
chown -R nobody:nobody /var/www/html/demo
```

📌 ubuntu - debian:

🔰 Terminal
```sh
chown -R nobody:nogroup /var/www/html/demo
```

📝 This example assumes you are using the default document root + URI: /python/

📝 Navigate to **Web Admin > Virtual Hosts > Context > Add**

* **Type =** App Server
* **URI =** /python/
* **Location =** /var/www/html/demo/
* **Binary Path =** /usr/local/lsws/fcgi-bin/lswsgi
* **Application Type =** WSGI
* **Startup File =** demo/wsgi.py

### 💬 Example 1

🔰 Virtual Hosts > new

![img](http://127.0.0.1:5555/LiteSpeed/2021/9.png)

🔰 Virtual Hosts > zPython > General

![img](http://127.0.0.1:5555/LiteSpeed/2021/10.png)


🔰 Virtual Hosts > zPython > context

![img](http://127.0.0.1:5555/LiteSpeed/2021/11.png)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Set up Django with a Virtual Environment
📝 create env

🔰 Terminal
```sh
cd /var/www/html
python3 -m venv demoEnv
source demoEnv/bin/activate
```

📝 install packages

🔰 Terminal
```sh
pip install django
pip install pillow
```

### 💬 Set up Context
📝 This example assumes you are using the default document root + URI: **/**

📝 Navigate to **Web Admin > Virtual Hosts > Context > Add**

* Type = App Server
* URI = /
* Location = /var/www/html/demo/
* Binary Path = /usr/local/lsws/fcgi-bin/lswsgi
* Application Type = WSGI
* Startup File = demo/wsgi.py
* Environment = 


 PYTHONPATH=/var/www/html/lib/python3.8:/var/www/html/demo

LS_PYTHONBIN=/var/www/html/bin/python


![img](http://127.0.0.1:5555/LiteSpeed/2021/12.jpg)
