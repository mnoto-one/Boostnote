---
title: 4 - django modules
tags:
  - Django
  - StartApp
  - Toplearn
---

### 📜 List files
```python
1 -> "MyProject/settings.py"
```
---


### 💬 Startapp

🔰 Terminal

```shell
python manage.py startapp challenges
```

```shell
python manage.py startapp challenges_2
```


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 add two app new challenges in INSTALLED_APPS
 📁 -1 MyProject/settings.py


```python
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'challenges',
    'challenges_2'
]
...
```
