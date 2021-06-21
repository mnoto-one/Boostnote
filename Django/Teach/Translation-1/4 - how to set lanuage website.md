---
title: 4 - how to set lanuage website
tags:
  - Change
  - Set
  - Language
  - Website
---

### 💬 set and switch language

[link](https://docs.djangoproject.com/en/3.2/topics/i18n/translation/#the-set-language-redirect-view)



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
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 i18n
 📁 -4 translation_example/urls.py
```python
...
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('i18n/', include('django.conf.urls.i18n')),
    path('', views.index),
]
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


<form action="{% url 'set_language' %}" method="post">{% csrf_token %}
    <input name="next" type="hidden" value="{{ redirect_to }}">
    <select title="language" name="language">
        {% get_current_language as LANGUAGE_CODE %}
        {% get_available_languages as LANGUAGES %}
        {% get_language_info_list for LANGUAGES as languages %}
        {% for language in languages %}
            <option value="{{ language.code }}"{% if language.code == LANGUAGE_CODE %} selected{% endif %}>
                {{ language.name_local }} ({{ language.code }})
            </option>
        {% endfor %}
    </select>
    <input type="submit" value="Go">
</form>
...
</body>
</html>
```
### 💬 Or
### 💬 Static
```html
<form action="{% url 'set_language' %}" method="post">{% csrf_token %}
    <input name="next" type="hidden" value="{{ redirect_to }}">
    <select title="language" name="language">
            <option value="en">
                English (en)
            </option>
            <option value="es">
                español (es)
            </option>
    </select>
    <input type="submit" value="Go">
</form>
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Standard code language
```html
<option value="en" selected>
    English (en)
</option>

<option value="fa">
    فارسی (fa)
</option>
```
