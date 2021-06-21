---
title: 6 - panel admin
tags:
  - Django
  - Faranesh
  - Admin
---

### 📜 List files
```python
1 -> "shop/admin.py"
```
---

### 💬 Admin
📁 -1 shop/admin.py

```python
from django.contrib import admin
from . import models


# Register your models here.
class ProductAdmin(admin.ModelAdmin):
    list_display = ('name', 'create_time', 'price')


class OrderAdmin(admin.ModelAdmin):
    list_display = ('id', '__str__', 'customer', 'order_date', 'payed')


class OrderItemAdmin(admin.ModelAdmin):
    list_display = ('id', 'order', 'product')


class InvoiceAdmin(admin.ModelAdmin):
    list_display = ('id', 'order', 'invoice_date', 'authority', 'order_items')


class AddressAdmin(admin.ModelAdmin):
    list_display = ('id', 'name', 'mobile', 'address', 'user')


class TransactionAdmin(admin.ModelAdmin):
    list_display = ('id', 'invoice', 'amount', 'transaction_date', 'status')


admin.site.register(models.Product, ProductAdmin)
admin.site.register(models.Order, OrderAdmin)
admin.site.register(models.Address, AddressAdmin)
admin.site.register(models.OrderItem, OrderItemAdmin)
admin.site.register(models.Invoice, InvoiceAdmin)
admin.site.register(models.Transaction, TransactionAdmin)

```


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Create Account Admin
🔰 Terminal

```python
python manage.py createsuperuser
```

![img](http://127.0.0.1:5555/Django/Teach/Shop-Faranesh/1.png)
