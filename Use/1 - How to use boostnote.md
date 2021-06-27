---
title: 1 - How to use boostnote
tags:
  - Use
---

### 📜 List files
```python
1 -> "products/views.py"
2 -> "shop/urls.py"
```
---
### 💬 def product_list_view
 📁 -1 products/views.py
```python
from django.shortcuts import render

from .models import Product


def product_list_view(request):
    products = Product.objects.all()
    context = {
        "object_list": products
    }

    return render(request, "products/product_list.html", context)

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 class ProductListView
 📁 🔁 -1 products/views.py
```python
from django.shortcuts import render
from django.views.generic.list import ListView
from .models import Product


class ProductListView(ListView):
    queryset = Product.objects.all()
    template_name = "products/product_list.html"


def product_list_view(request):
    ...
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Result
 📁 -2 shop/urls.py
```python
print('Hi how are you ?')
```

▶️ Result in Terminal

```shell
Hi how are you ?
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Command
🔰 Terminal
```shell
pip freeze > requirements.txt
```
#### 💬 Useful attributes on {{ field }} include:

- 📌 {{ field.label }}
```
Description ...
```

- 📌 {{ field.html_name }}
```
Description ...
```
- 📌 {{ field.help_text }}

```
Description ...
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Group Group
```python
{{ request.get_host }}
```

▶️ Result

```shell
http://127.0.0.1:8000
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Link
[Link Address](https://docs.djangoproject.com/en/3.0/topics/auth/default/)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Note
📝 Lorem Ipsum is simply dummy tex

📝 Lorem Ipsum is simply dummy tex

📝 Lorem Ipsum is simply dummy tex

📝 Lorem Ipsum is simply dummy tex


# ⚠️ Warning
### 💬 Result
 📁 -2 shop/urls.py
```python
print('Hi how are you ?')
```
