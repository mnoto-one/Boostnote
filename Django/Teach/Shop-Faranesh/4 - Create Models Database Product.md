---
title: 4 - Create Models Database Product
tags:
  - Django
  - Faranesh
  - Models
---

### 📜 List files
```python
1 -> "shop/models.py"
2 -> "shop/urls.py"
3 -> "cart/urls.py"
```
---

### 💬 models
📁 -1 shop/models.py

```python
from django.db import models
from django.contrib.auth.models import User
from django.urls import reverse


class Product(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField(max_length=3000)
    create_time = models.DateTimeField(auto_now_add=True)
    update_time = models.DateTimeField(auto_now=True)
    image = models.ImageField(upload_to='image/product/%Y/%m/%d')
    price = models.DecimalField(max_digits=10, decimal_places=0)

    class Meta:
        ordering = ('create_time',)
        verbose_name_plural = 'Products'

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return reverse('shop:product', args=[self.id])


class Order(models.Model):
    customer = models.ForeignKey(User, on_delete=models.CASCADE)
    order_date = models.DateTimeField(auto_now_add=True)
    payed = models.BooleanField(default=False)
    address = models.ForeignKey('Address', on_delete=models.SET_NULL, null=True)

    def __str__(self):
        return f'{self.address}'

    class Meta:
        ordering = ('order_date',)
        verbose_name_plural = 'Orders'


class Address(models.Model):
    name = models.CharField(max_length=20)
    mobile = models.CharField(max_length=11)
    address = models.CharField(max_length=50)
    user = models.ForeignKey(User, on_delete=models.CASCADE)

    def __str__(self):
        return f'{self.address} , {self.name} , {self.mobile} , {self.user}'

    class Meta:
        verbose_name_plural = 'Addresses'


class OrderItem(models.Model):
    order = models.ForeignKey(Order, related_name='orderitem', on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.SET_NULL, null=True)
    product_price = models.DecimalField(max_digits=10, decimal_places=0)
    product_count = models.PositiveIntegerField()
    product_cost = models.DecimalField(max_digits=10, decimal_places=0)

    def __str__(self):
        return str(self.product.name)

    class Meta:
        verbose_name_plural = 'OrderItems'


class Invoice(models.Model):
    order = models.ForeignKey(Order, on_delete=models.SET_NULL, null=True)
    order_items = models.CharField(max_length=400, )
    invoice_date = models.DateTimeField(auto_now_add=True)
    authority = models.CharField(max_length=200, blank=True, null=True)

    def __str__(self):
        return str(self.id)

    class Meta:
        verbose_name_plural = 'Invoices'


class Transaction(models.Model):
    STATUS_CHOICES = (
        ('pending', 'Pending'),
        ('failed', 'Failed'),
        ('completed', 'Completed'),
    )
    invoice = models.ForeignKey(Invoice, on_delete=models.SET_NULL, null=True)
    transaction_date = models.DateTimeField(auto_now_add=True)
    amount = models.DecimalField(max_digits=10, decimal_places=0)
    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='pending')

    def __str__(self):
        return str(self.id)

    class Meta:
        verbose_name_plural = 'Transactions'

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 urls
📁 -2 shop/urls.py
```python
app_name = 'shop'

urlpatterns = [
]
```

### 💬 urls
📁 -3 cart/urls.py

```python
app_name = 'cart'

urlpatterns = [
]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Makemigrations & Migrate

🔰 Terminal

```shell
python manage.py makemigrations
python manage.py migrate
```
