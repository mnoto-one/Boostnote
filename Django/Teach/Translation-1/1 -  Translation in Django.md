---
title: 1 -  Translation in Django
tags:
  - Translation
  - Language
  - Django
---

### 📜 List files
```python
1 -> "translation_example/settings.py"
2 -> "example/views.py"
3 -> "example/templates/index.html"
4 -> "translation_example/urls.py"
5 -> "example/locale/es/LC_MESSAGES/django.po"
```
---

### 💬 Create project
🔰 Terminal

```sh
django-admin startproject translation_example
cd translation_example
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Create startapp
🔰 Terminal

```sh
python manage.py startapp example
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


### 💬 settings
📁 -1 translation_example/settings.py

```python
INSTALLED_APPS = [
    ...
    'example.apps.ExampleConfig'
]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 views index
📁 -2 example/views.py

```python
from django.shortcuts import render


# Create your views here.

def index(request):
    context = {
        'hello': 'Hello'
    }
    return render(request, 'index.html', context)

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Create folder templates and file index.html
🔰 Terminal

```sh
mkdir example/templates
touch example/templates/index.html
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 html index
📁 -3 example/templates/index.html

```html
<!doctype html>
<html lang="en">
<head>
   ...
</head>
<body>
<h1>{{ hello }}</h1>
<h2>My name is Alex</h2>
</body>
</html>
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 views index
📁 -4 translation_example/urls.py

```python
from django.contrib import admin
from django.urls import path
from example import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index),
]

```

![img](http://127.0.0.1:5555/Django/Teach/Translation-1/1.png)


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 views index
📁 🔁 -2 example/views.py

```python
from django.shortcuts import render
from django.utils.translation import gettext as _


# Create your views here.

def index(request):
    context = {
        'hello': _('Hello')
    }
    return render(request, 'index.html', context)

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 i18n - trans
📁 🔁 -3 example/templates/index.html

```html
<!doctype html>
{% load i18n %}
<html lang="en">
<head>
    ...
</head>
<body>
<h1>{{ hello }}</h1>
<h2>{% trans "My name is Alex" %}</h2>
</body>
</html>
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Install gettext in linux
🔰 Terminal

```sh
sudo apt install gettext
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Create folder locale translation
🔰 Terminal

```sh
mkdir example/locale
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 makemessages
🔰 Terminal

```sh
python manage.py makemessages -l es
```


💬 if error  Unable to find a locale path to store translations for file

📁 🔁 -1 translation_example/settings.py
```python
LOCALE_PATHS = [
    BASE_DIR / 'locale',
]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 edit file po for translation
📁 -5 example/locale/es/LC_MESSAGES/django.po

```
#: example/templates/index.html:13
msgid "My name is Alex"
msgstr "Me llamo Alex"

#: example/views.py:9
msgid "Hello"
msgstr "Hola"
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 compilemessages
🔰 Terminal

```sh
python manage.py compilemessages
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 compilemessages
🔰 Terminal

```sh
python manage.py compilemessages
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


### 💬 settings change lanuage
📁 🔁 -1 translation_example/settings.py

```python
...
LANGUAGE_CODE = 'es'
...
```

![img](http://127.0.0.1:5555/Django/Teach/Translation-1/2.png)



^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


### 💬 MIDDLEWARE
📁 🔁 -1 translation_example/settings.py

```python
...
MIDDLEWARE = [
    ...
    'django.middleware.common.CommonMiddleware',
    'django.middleware.locale.LocaleMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    ...
]
...
```
