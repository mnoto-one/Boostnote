---
title: 16 - pay online
tags:
  - Django
  - Faranesh
  - Pay
  - Online
---

### 📜 List files
```python
1 -> "shop/views.py"
2 -> "shop/templates/callback.html"
```
---

### 💬 profile - orders
📁 -1 shop/views.py

```python
...
from zeep import Client
from django.http import HttpResponse
...
MERCHANT = '25502853-c878-4047-b804-9002d05a7cfd'
client = Client('https://www.zarinpal.com/pg/services/WebGate/wsdl')


def to_bank(request, order_id):
    order = get_object_or_404(models.Order, id=order_id)
    amount = 0
    order_items = models.OrderItem.objects.filter(order=order)
    for item in order_items:
        amount += item.product_cost
    callbackUrl = 'http://127.0.0.1:8000/callback/'
    mobile = ''
    email = ''
    description = 'Test'
    result = client.service.PaymentRequest(MERCHANT, amount, description, email, mobile, callbackUrl)
    if result.Status == 100 and len(result.Authority) == 36:
        x = []
        for item in order_items:
            x.append(item)
        models.Invoice.objects.create(order=order,
                                      order_items=x,
                                      authority=result.Authority)
        return redirect('https://www.zarinpal.com/pg/StartPay/' + result.Authority)
    else:
        return HttpResponse('Error code' + str(result.Status))


def callback(request):
    if request.GET.get('Status') == 'OK':
        authority = request.GET.get('Authority')
        invoice = get_object_or_404(models.Invoice, authority=authority)
        amount = 0
        order = invoice.order
        order_items = models.OrderItem.objects.filter(order=order)
        for item in order_items:
            amount += item.product_cost
        result = client.service.PaymentVerification(MERCHANT, authority, amount)
        if result.Status == 100:
            order.payed = True
            order.save()
            return render(request, 'callback.html', {'invoice': invoice})
        else:
            return HttpResponse('error' + str(result.Status))
    else:
        return HttpResponse('error')
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 callback.html
📁 -2 shop/templates/callback.html

```python
{% extends 'base.html' %}
{% load static %}
{% block title %}Callback{% endblock title %}
{% block content %}
    <h1 class="text-center"> Payment Detail</h1>
    <div class="section">
    <div class="container">
        <div class="row">
            <div class="col-md-12 order-detail">
                <div class="section-title text-center">
                    <h3 class="title">Thank You</h3>

                </div>
                <div class="order-summary">
                    <p>Your Invoice Number : {{ invoice.id }}</p>
                </div>
            </div>
        </div>
    </div>

    </div>
{% endblock content %}
```
