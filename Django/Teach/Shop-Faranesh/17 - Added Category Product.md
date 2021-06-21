---
title: 17 - Added Category Product
tags:
  - Django
  - Faranesh
  - Category
  - Product
---

### 📜 List files
```python
1 -> "shop/models.py"
```
---

### 💬 models
📁 -1 shop/models.py


```python
class CategoryProduct(models.Model):
    name_category = models.CharField(max_length=60, default='')
    image_category = models.ImageField(upload_to='image/category', default='')

    def __str__(self):
        return self.name_category


class Product(models.Model):
    name = models.CharField(max_length=100)
    ...
    category_product = models.ForeignKey(CategoryProduct, on_delete=models.CASCADE, default='')

    class Meta:
        ordering = ('create_time',)
        verbose_name_plural = 'Products'

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return reverse('shop:product', args=[self.id])
```
