---
title: 1 - how to config for upload website
tags:
  - Django
  - Teach
  - Upload
---

models.py

```python
class Slider(models.Model):
    name = models.CharField(max_length=100)
    image = models.ImageField(upload_to='upload/%Y/%m')
    url = models.URLField(blank=True)

    def __str__(self):
        return self.name
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

admin.py

```python
from django.contrib import admin
from . import models

# Register your models here.

admin.site.register(models.Slider)

```
