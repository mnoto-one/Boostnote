---
title: 13 - create page checkout
tags:
  - Django
  - Faranesh
  - Checkout
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/checkout.html"
```
---

### 💬 shop views for checkout login_required
📁 -1 shop/views.py

```python
from django.shortcuts import render, get_object_or_404, redirect
from cart.forms import CartAddProductForm
from django.contrib.auth.decorators import login_required
from .forms import AddressForm
from . import models
from cart.cart import Cart
from django.db.models import Q
from decimal import Decimal


...


@login_required()
def checkout(request):
    cart = Cart(request)
    if not cart:
        return redirect('shop:store')
    if request.method != 'POST':
        form = AddressForm()
    else:
        form = AddressForm(request.POST)
        if form.is_valid():
            address = models.Address.objects.create(
                name=request.POST.get('name'),
                mobile=request.POST.get('mobile'),
                address=request.POST.get('address'),
                user=request.user
            )

            order = models.Order.objects.create(customer=request.user, address=address)
            for item in cart:
                models.OrderItem.objects.create(
                    order=order,
                    product=item['product'],
                    product_price=item['price'],
                    product_count=item['product_count'],
                    product_cost=Decimal(item['product_count']) * Decimal(item['price'])
                )
        cart.clear()
        return redirect('shop:order_detail', order.id)
    return render(request, 'checkout.html', {'form': form})


...

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 checkout.html
📁 -1 shop/templates/checkout.html



```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Checkout{% endblock title %}
{% block content %}
    <br>
    <div uk-grid>
        <div class="uk-width-1-2">
            <div class="uk-card-body">
                <h2>Adress</h2>
                <div>
                    <div>
                        <form action="{% url 'shop:checkout' %}" method="post">
                            {% csrf_token %}
                            {{ form.as_p }}
                            <button type="submit" class="btn btn-primary btn-lg py-3 btn-block">Place Order</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
        <div class="uk-width-1-2">
            <div class="uk-card-body">
                <h2>Your Order</h2>
                <div>
                    <table class="uk-table uk-table-divider">
                        <thead>
                        <tr>
                            <th>Product</th>
                            <th>Total</th>
                        </tr>
                        </thead>
                        <tbody>
                        {% for item in cart %}
                            <tr>
                                <td>{{ item.product_count }} X {{ item.product.name }}</td>
                                <td>${{ item.total_price }}</td>
                            </tr>
                        {% endfor %}
                        </tbody>
                    </table>
                    <strong>Order Total : </strong>
                    <strong>${{ cart.get_total_price }}</strong>
                </div>
            </div>
        </div>
    </div>
{% endblock content %}
```

![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/4.png)
