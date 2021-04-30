---
title: 1 - How to use HTML5 color picker in Django
tags:
  - Django
  - Forms
  - Color
  - Input
---

### 📜 List files
```python
1 -> "model.py"
2 -> "form.py"
3 -> "admin.py"
```
---
### 💬 def Model
 📁 -1 model.py
```python
#model.py
...

class Category(models.Model):
    ...
    color = models.CharField(max_length=7)

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Forms
 📁  -2 form.py
```python
from django.forms import ModelForm, TextInput
from .models import Category

class CategoryForm(ModelForm):
    class Meta:
        model = Category
        fields = ['name_category', 'txt_color', 'color']
        widgets = {
            'name_category': TextInput(...),
            'txt_color': TextInput(...),
            'color': TextInput(attrs={'type': 'color'}),
        }

class CategoryAdminForm(ModelForm):
    form = CategoryForm

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Admin
 📁  -3 admin.py
```python
...
from .forms import CategoryAdminForm

...
class CategoryAdmin(admin.ModelAdmin):
    form = forms.CategoryAdminForm
    
admin.site.register(models.Category, CategoryAdmin)
```
