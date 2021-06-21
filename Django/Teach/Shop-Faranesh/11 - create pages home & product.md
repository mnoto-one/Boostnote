---
title: 11 - create pages home & product
tags:
  - Django
  - Faranesh
  - Templates
  - Home
  - Product
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/base.html"
3 -> "shop/templates/index.html"
4 -> "shop/templates/product.html"
```
---

### 💬 shop views
📁 -1 shop/views.py
```python
from django.shortcuts import render, get_object_or_404
from cart.forms import CartAddProductForm
from . import models


def index(request):
    product_list = models.Product.objects.order_by('-create_time')[:10]
    return render(request, 'index.html', {'product_list': product_list})


def product(request, id):
    product_detail = get_object_or_404(models.Product, id=id)
    cart_add_product_form = CartAddProductForm()
    return render(request, 'product.html', {'product_detail': product_detail, 'cart_add_product_form': cart_add_product_form})


def store(request):
    pass


def search(request):
    pass


def checkout(request):
    pass


def profile(request):
    pass


def orders(request):
    pass


def order_detail(request, order_id):
    pass


def to_bank(request, order_id):
    pass


def callback(request):
    pass

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 templates base.html
📁 -2 shop/templates/base.html


```html
<!doctype html>
{% load static %}
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!---- CSS ---->
    <link rel="stylesheet" href="{% static 'global/css/uikit.min.css' %}"/>
    <!---- JS ---->
    <script src="{% static 'global/js/uikit.min.js' %}"></script>
    <script src="{% static 'global/js/uikit-icons.min.js' %}"></script>
</head>
<body>
<nav class="uk-navbar-container" uk-navbar>
    <div class="uk-navbar-left">

        <ul class="uk-navbar-nav">
            <li class="uk-active"><a href="#">Active</a></li>
            <li>
                <a href="#">Parent</a>
                <div class="uk-navbar-dropdown">
                    <ul class="uk-nav uk-navbar-dropdown-nav">
                        <li class="uk-active"><a href="#">Active</a></li>
                        <li><a href="#">Item</a></li>
                        <li><a href="#">Item</a></li>
                    </ul>
                </div>
            </li>
            <li><a href="#">Item</a></li>
        </ul>

    </div>
</nav>

</body>
</html>
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Title / Content
📁 🔁 -2 shop/templates/base.html

```html
<!doctype html>
{% load static %}
<html lang="en">
<head>
    ...
    <title>{% block title %} {% endblock %}</title>
    <!---- CSS ---->
    ...
</head>
<body>
<nav class="uk-navbar-container" uk-navbar>
    ...
</nav>
{% block content %}{% endblock %}
</body>
</html>
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

🔰 Copy all files static in folder static_files

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Header Menu Navbar
📁 🔁 -2 shop/templates/base.html

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

        <ul class="uk-navbar-nav">
            <li class="uk-active"><a href="#">Active</a></li>
            <li>
                <a href="#">Account</a>
                <div class="uk-navbar-dropdown">
                    <ul class="uk-nav uk-navbar-dropdown-nav">
                        {% if user.is_authenticated %}
                            <li><a href="{% url 'account_logout' %}">Logout</a></li>
                            <li><a href="{% url 'shop:profile' %}">Profile</a></li>
                        {% else %}
                            <li><a href="{% url 'account_login' %}">Login</a></li>
                            <li><a href="{% url 'account_signup' %}">Signup</a></li>
                        {% endif %}
                    </ul>
                </div>
            </li>
            <li><a href="#">Item</a></li>
        </ul>

    </div>
</nav>
{% block content %}{% endblock %}
</body>
</html>
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 templates index
📁 -3 shop/templates/index.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Home{% endblock %}
{% block content %}
    <div class="uk-child-width-1-3@m" uk-grid>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
        <div>
            <div class="uk-card uk-card-default">
                <div class="uk-card-media-top">
                    <img src="{% static 'website/images/products/product-laptop-1.jpg' %}" alt="">
                </div>
                <div class="uk-card-body">
                    <h3 class="uk-card-title">Media Top</h3>
                    <h4 class="uk-card-title">5000 T</h4>
                    <a class="uk-button uk-button-primary" href="#">Show</a>
                </div>
            </div>
        </div>
    </div>
{% endblock %}     
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Dynamic Product in index
📁 🔁 -3 shop/templates/index.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Home{% endblock %}
{% block content %}
    <div class="uk-child-width-1-5@m" uk-grid>
        {% for product in product_list %}
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

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

🔰 Go to panel admin insert a product

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 templates product
📁 -4 shop/templates/product.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Home{% endblock %}
{% block content %}
    <br>
    <div uk-grid>
        <div class="uk-width-1-3 uk-text-center">
            <div class="uk-card uk-card-default uk-card-body">
                <img src="{{ product_detail.image.url }}" alt="Image">
            </div>
        </div>
        <div class="uk-width-2-3">
            <div class="uk-card uk-card-default uk-card-body">
                <h2 class="text-black">{{ product_detail.name }}</h2>
                <p>{{ product_detail.description }}</p>
                <p><strong class="uk-h4">${{ product_detail.price }}</strong></p>
                <form action="{% url 'cart:cart_add' product_detail.id %}" method="post">
                    {% csrf_token %}
                    {{ cart_add_product_form }}
                    <hr>
                    <input type="submit" class="btn btn-block btn-primary" value="Add To Cart">
                </form>
            </div>
        </div>
    </div>
{% endblock %}
```
