---
title: 9 - Config Forms
tags:
  - Django
  - Faranesh
  - Forms
---

### 📜 List files
```python
1 -> "shop/forms.py"
2 -> "cart/forms.py"
```
---
### 💬 shop forms
📁 -1 shop/forms.py

```python
from django import forms
from .models import Address


class AddressForm(forms.ModelForm):
    class Meta:
        model = Address
        fields = ['name', 'mobile', 'address']

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 cart forms
📁 -2 cart/forms.py
```python
from django import forms

PRODUCT_COUNT_CHOICES = [(i, str(i)) for i in range(1, 6)]


class CartAddProductForm(forms.Form):
    product_count = forms.TypedChoiceField(choices=PRODUCT_COUNT_CHOICES, coerce=int)
    update = forms.BooleanField(required=False,
                                initial=False,
                                widget=forms.HiddenInput)

```
