---
title: 5 - Addressing system (Url) and (Views)
tags:
  - Django
  - Toplearn
  - Urls
  - Views
---

### 📜 List files
```python
1 -> "challenges/views.py"
2 -> "challenges/urls.py"
3 -> "MyProject/urls.py"
4 -> "MyProject/views.py"
```
---


### 💬 add two app new challenges in INSTALLED_APPS
📁 -1 challenges/views.py


```python
from django.shortcuts import render
from django.http import HttpResponse


# Create your views here.

def index(request):
    return HttpResponse("user setting")


def edit_profile(request):
    return HttpResponse("edit profile")


```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


### 💬 urls
📁 -2 challenges/urls.py


```python
from django.urls import path
from . import views

urlpatterns = [
    path('edit-profile/', views.edit_profile),
    path('user-setting/', views.index),
]


```



^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


### 💬 urls MyProject
📁 -3 MyProject/urls.py


```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('user/', include('challenges.urls')),
]
```



![img](http://127.0.0.1:5555/Django/Teach/Toplearn/2.jpg)

![img](http://127.0.0.1:5555/Django/Teach/Toplearn/3.jpg)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 urls MyProject
📁 -4 MyProject/views.py



```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("index page")


```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 urls MyProject
📁 -3 MyProject/urls.py

```python
from django.contrib import admin
from django.urls import path, include
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index),
    path('user/', include('challenges.urls')),
]
```

![img](http://127.0.0.1:5555/Django/Teach/Toplearn/4.png)
