---
title: 7 - Config Urls.py
tags:
  - Django
  - Faranesh
  - Urls
---

### 📜 List files
```python
1 -> "django_project/shop/urls.py"
2 -> "django_project/cart/urls.py"
```
---

### 💬 urls shop
📁 -1 django_project/shop/urls.py

```python
from . import views
from django.urls import path

app_name = 'shop'
urlpatterns = [
    path('', views.index, name='index'),
    path('checkout/', views.checkout, name='checkout'),
    path('product/<int:id>/', views.product, name='product'),
    path('store/', views.store, name='store'),
    path('to_bank/<int:order_id>/', views.to_bank, name='to_bank'),
    path('callback/', views.callback, name='callback'),
    path('profile/', views.profile, name='profile'),
    path('orders/', views.orders, name='orders'),
    path('searched_products/', views.search, name='search'),
    path('order_detail/<int:order_id>/', views.order_detail, name='order_detail')
]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 urls shop
📁 -2 django_project/cart/urls.py

```python
from django.urls import path
from . import views

app_name = 'cart'
urlpatterns = [
    path('', views.cart_detail, name='cart_detail'),
    path('add/<int:product_id>/', views.cart_add, name='cart_add'),
    path('remove/<int:product_id>/', views.cart_remove, name='cart_remove'),
]
```
