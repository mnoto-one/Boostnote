---
title: 14 - create page cart - ordering
tags:
  - Django
  - Faranesh
  - Cart
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/order_detail.html"
3 -> "shop/templates/detail.html"
```
---

### 💬 order_detail
📁 -1 shop/views.py



```python
...

def orders(request):
    pass


def order_detail(request, order_id):
    order = get_object_or_404(models.Order, id=order_id)
    return render(request, 'order_detail.html', {'order': order})


def to_bank(request, order_id):
    pass

...

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 order_detail
📁 -2 shop/templates/order_detail.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %} Order Detail {% endblock title %}
{% block content %}
    <br>
    <div uk-grid>
        <div class="uk-width-1-2">
            <div class="uk-card-body">
                <h1>Thank you!</h1>
                <div>
                    <p>You order was successfuly completed.</p>
                    <p>Your Order Number : {{ order.id }}</p>
                    <p><a href="{% url 'shop:to_bank' order.id %}" class="btn btn-primary">Online Payment</a></p>
                </div>
            </div>
        </div>
    </div>
{% endblock content %}
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 detail
📁 -3 shop/templates/detail.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Detail{% endblock title %}
{% block content %}
    <br>
    <div uk-grid>
        <div class="uk-width-1-1">
            <div class="uk-card-body">
                <h2>Your Order</h2>
                <div>
                    <table class="uk-table uk-table-divider">
                        <thead>
                        <tr>
                            <th>Image</th>
                            <th>Product</th>
                            <th>Price</th>
                            <th>Quantity</th>
                            <th>Total</th>
                            <th>Remove</th>
                        </tr>
                        </thead>
                        <tbody>
                        {% for item in cart %}
                            {% with product=item.product %}
                                <tr>
                                    <td class="product-thumbnail">
                                        <a href="{{ product.get_absolute_url }}">
                                            <img src="{{ product.image.url }}" alt="Image" style="width: 100px">
                                        </a>
                                    </td>
                                    <td class="product-name">
                                        <h2>{{ product.name }}</h2>
                                    </td>
                                    <td>${{ item.price }}</td>
                                    <td>
                                        <form action="{% url 'cart:cart_add' product.id %}" method="post">
                                            {{ item.update_product_count_form.product_count }}
                                            {{ item.update_product_count_form.update }}
                                            {% csrf_token %}
                                            <input type="submit" value="Update">
                                        </form>
                                    </td>
                                    <td>${{ item.total_price }}</td>
                                    <td>
                                        <a href="{% url 'cart:cart_remove' product.id %}"
                                           class="btn btn-primary btn-sm">X</a>
                                    </td>
                                </tr>
                            {% endwith %}
                        {% endfor %}
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
    <div class="uk-card-body">
        <div uk-grid>
            <div class="uk-width-1-2">
                <a href="{% url 'shop:store' %}">
                    <button class="uk-button uk-button-primary">Continue Shopping</button>
                </a>
            </div>
            <div class="uk-width-1-2">

                <span>Total</span>
                <span>${{ cart.get_total_price }}</span>
                <br>
                <a href="{% url 'shop:checkout' %}">
                    <button class="uk-button uk-button-secondary">Checkout</button>
                </a>
            </div>
        </div>
    </div>
{% endblock content %}


```

![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/5.png)


![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/6.png)
