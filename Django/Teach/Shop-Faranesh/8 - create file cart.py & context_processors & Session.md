---
title: 8 - create file cart.py & context_processors & Session
tags:
  - Django
  - Faranesh
  - Cart
  - Context_Processor
  - Session
---

### 📜 List files
```python
1 -> "django_project/cart/cart.py"
2 -> "django_project/cart/context_processor.py"
3 -> "django_project/django_project/settings.py"
```
---

### 💬 cart
📁 -1 django_project/cart/cart.py

```python

class Cart(request):
    pass
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 context_processor
📁 -2 django_project/cart/context_processor.py

```python
from .cart import Cart


def cart(request):
    return {'cart': Cart(request)}

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 context_processor.cart
📁 -2 django_project/django_project/settings.py

```python
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            'context_processors': [
                ...
                'cart.context_processor.cart'
            ],
        },
    },
]
```

### 💬 cart
📁 -1 django_project/cart/cart.py
```python
from django.conf import settings
from shop.models import Product
from decimal import Decimal


class Cart(object):

    def __init__(self, request):

        self.session = request.session
        cart = self.session.get(settings.CART_SESSION_ID)
        if not cart:
            cart = self.session[settings.CART_SESSION_ID] = {}
        self.cart = cart

    def add(self, product, product_count=1, update_count=False):

        product_id = str(product.id)
        if product_id not in self.cart:
            self.cart[product_id] = {'product_count': 0,
                                     'price': str(product.price)}

        if update_count:
            self.cart[product_id]['product_count'] = product_count
        else:
            self.cart[product_id]['product_count'] += product_count
        self.save()

    def save(self):
        self.session[settings.CART_SESSION_ID] = self.cart
        self.session.modified = True

    def remove(self, product):
        product_id = str(product.id)
        if product_id in self.cart:
            del self.cart[product_id]
            self.save()

    def __iter__(self):
        product_ids = self.cart.keys()
        products = Product.objects.filter(id__in=product_ids)
        for product in products:
            self.cart[str(product.id)]['product'] = product

        for item in self.cart.values():
            item['price'] = Decimal(item['price'])
            item['total_price'] = item['price'] * item['product_count']
            yield item

    def __len__(self):
        return sum(item['product_count'] for item in self.cart.values())

    def get_total_price(self):
        return sum(Decimal(item['price']) * item['product_count'] for item in self.cart.values())

    def clear(self):
        self.session[settings.CART_SESSION_ID] = {}
        self.session.modified = True

    def cart_item_count(self):
        a = []
        for item in self.cart.values():
            a.append(item)
        b = len(a)
        return b
```
