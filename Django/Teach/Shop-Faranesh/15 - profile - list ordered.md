---
title: 15 - profile - list ordered
tags:
  - Django
  - Faranesh
  - Profile
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/profile.html"
3 -> "shop/templates/orders.html"
```
---

### 💬 profile - orders
📁 -1 shop/views.py

```python
...
def profile(request):
    return render(request, 'profile.html')


def orders(request):
    orders = models.Order.objects.order_by('-order_date')
    return render(request, 'orders.html', {'orders': orders})
...

```


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 profile.html
📁 -2 shop/templates/profile.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Profile{% endblock title %}
{% block content %}
    <div uk-grid>
        <div class="uk-width-1-2">
            <div class="uk-card-body">
                <h1>Profile</h1>
                <div>
                    <a class="uk-button uk-button-secondary" href="{% url 'account_email' %}">
                        Add Email
                    </a>
                    <br>
                    <br>
                    <a class="uk-button uk-button-secondary" href="{% url 'account_change_password' %}">
                        Password Change
                    </a>
                    <br>
                    <br>
                    <a class="uk-button uk-button-secondary" href="{% url 'account_reset_password' %}">
                        Password Reset
                    </a>
                    <br>
                    <br>
                    <a class="uk-button uk-button-secondary" href="{% url 'shop:orders' %}">
                        Your Orders
                    </a>
                    <br>
                    <br>
                </div>
            </div>
        </div>
    </div>
{% endblock content %}
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 orders.html
📁 -3 shop/templates/orders.html

```html
{% extends 'website/base.html' %}
{% load static %}
{% block title %}Orders{% endblock title %}
{% block content %}
    <br>
    <div uk-grid>
        <div class="uk-width-1-1">
            <div class="uk-card-body">
                <h1>Your Orders</h1>
                <div>
                    <div class="uk-text-center">
                        {% for order in orders %}
                            {% if order.payed %}
                                <div>
                                    <div class="uk-card uk-card-default uk-card-body">
                                        <p style="background: #00803e;color: white">Payed : {{ order.payed }}</p>
                                        <p>Order id :{{ order.id }}</p>
                                        <p class="btn">Address :{{ order.address.name }}
                                            , {{ order.address.mobile }}</p>
                                    </div>
                                </div>
                            {% else %}
                                <div>
                                    <div class="uk-card uk-card-default uk-card-body">
                                        <p style="background: #970123;color: white">Payed : {{ order.payed }}</p>
                                        <p>Order id :{{ order.id }}</p>
                                        <p class="btn">Address :{{ order.address.name }}
                                            , {{ order.address.mobile }}</p>
                                        <hr>
                                    </div>
                                </div>
                            {% endif %}
                        {% empty %}
                            <p>No Orders Yet</p>
                        {% endfor %}
                    </div>
                </div>
            </div>
        </div>
    </div>
{% endblock content %}
```


![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/7.png)


![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/8.png)
