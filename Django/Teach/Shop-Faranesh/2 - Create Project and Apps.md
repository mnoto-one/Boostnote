---
title: 2 - Create Project and Apps
tags:
  - Django
  - Faranesh
  - StartProject
  - StartApp
---

### 📜 List files
```python
1 -> "django_project/settings.py"
```
---

### 💬 Start Project

🔰 Terminal

```shell
django-admin startproject django_project .
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Start Apps shop cart

🔰 Terminal

```shell
django-admin startapp shop
django-admin startapp cart
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 INSTALLED_APPS
📁 -1 django_project/settings.py
```python
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'shop.apps.ShopConfig',
    'cart.apps.CartConfig',
]
...
```
