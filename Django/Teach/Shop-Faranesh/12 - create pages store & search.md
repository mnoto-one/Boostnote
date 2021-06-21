---
title: 12 - create pages store & search
tags:
  - Django
  - Faranesh
  - Store
  - Search
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/store.html"
3 -> "shop/templates/base.html"
4 -> "shop/templates/searched_products.html"
```
---

### 💬 shop views for store - search
📁 -1 shop/views.py

```python
...
from . import models
from django.db.models import Q

...

def store(request):
    products = models.Product.objects.order_by('-create_time')
    return render(request, 'store.html', {'products': products})


def search(request):
    query = request.GET.get('q')
    queryset_list = []
    if query:
        queryset_list = models.Product.objects.filter(Q(name__icontains=query)).distinct()
    elif query == '':
        queryset_list = models.Product.objects.all()
    products = queryset_list
    return render(request, 'searched_products.html', {'products': products})

...

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 templates store.html
📁 -2 shop/templates/store.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Home{% endblock %}
{% block content %}
    <div class="uk-child-width-1-5@m" uk-grid>
        {% for product in products %}
            <div>
                <div class="uk-card uk-card-default">
                    <div class="uk-card-media-top">
                        <img src="{{ product.image.url }}" alt="" style="height: 500px;object-fit: contain;">
                    </div>
                    <div class="uk-card-body">
                        <a href="{{ product.get_absolute_url }}">
                            <h3 class="uk-card-title">{{ product.name }}</h3>
                        </a>
                        <h4 class="uk-card-title">${{ product.price }}</h4>
                        <a class="uk-button uk-button-primary" href="{{ product.get_absolute_url }}">Show</a>
                    </div>
                </div>
            </div>
        {% endfor %}
    </div>
{% endblock %}
```

![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/2.png)


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 add Form Search in navbar
📁 -3 shop/templates/base.html

```html
<!doctype html>
{% load static %}
<html lang="en">
<head>
    ...
</head>
<body>
<nav class="uk-navbar-container" uk-navbar>
    <div class="uk-navbar-left">
        ...
    </div>
    <div class="uk-navbar-right">
        <div>
            <a class="uk-navbar-toggle" uk-search-icon href="#"></a>
            <div class="uk-drop" uk-drop="mode: click; pos: left-center; offset: 0">
                <form action="{% url 'shop:search' %}" method="get" class="uk-search uk-search-navbar uk-width-1-1">
                    <input name="q" value="{{ request.GET.q }}" title="search" class="uk-search-input" type="search" placeholder="Search" autofocus>
                </form>
            </div>
        </div>
    </div>
</nav>
{% block content %}{% endblock %}
</body>
</html>
```
 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Searched products html
📁 -4 shop/templates/searched_products.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Home{% endblock %}
{% block content %}
    <div class="uk-child-width-1-5@m" uk-grid>
        {% for product in products %}
            <div>
                <div class="uk-card uk-card-default">
                    <div class="uk-card-media-top">
                        <img src="{{ product.image.url }}" alt="" style="height: 500px;object-fit: contain;">
                    </div>
                    <div class="uk-card-body">
                        <a href="{{ product.get_absolute_url }}">
                            <h3 class="uk-card-title">{{ product.name }}</h3>
                        </a>
                        <h4 class="uk-card-title">${{ product.price }}</h4>
                        <a class="uk-button uk-button-primary" href="{{ product.get_absolute_url }}">Show</a>
                    </div>
                </div>
            </div>
        {% endfor %}
    </div>
{% endblock %}
```

![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/3.png)
