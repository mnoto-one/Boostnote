---
title: 2 - Django blog open source
tags:
  - Django
  - Ready
  - Blog
  - Category
  - OpenSource
---

### 📜 List files
```python
1 -> "blog/models.py"
2 -> "blog/urls.py"
3 -> "blog/views.py"
```
---
### 💬 Model Database Category - Blog
 📁 -1 blog/models.py

```python
from django.db import models

# Create your models here.

from django.db import models
from django.contrib.auth.models import User

STATUS = (
    (0, "Draft"),
    (1, "Publish")
)


class Category(models.Model):
    title = models.CharField(max_length=200, unique=True)

    def __str__(self):
        return self.title


class Blog(models.Model):
    title = models.CharField(max_length=200, unique=True)
    slug = models.SlugField(max_length=200, unique=True)
    cover = models.ImageField(upload_to='images/blog/%Y/%m', default='')
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name='blog_posts')
    updated_on = models.DateTimeField(auto_now=True)
    excerpt = models.TextField(max_length=300, default='', help_text='Small description of this post')
    content = models.TextField()
    created_on = models.DateTimeField(auto_now_add=True)
    status = models.IntegerField(choices=STATUS, default=1)
    category_blog = models.ForeignKey(Category, on_delete=models.CASCADE, default='')

    class Meta:
        ordering = ['-created_on']

    def __str__(self):
        return self.title
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 urls
 📁 -2 blog/urls.py

```python
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.home, name="home"),
    path('show/<slug:str>', views.show, name="show"),
]
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 views
 📁 -3 blog/views.py

```python
from django.shortcuts import render, get_object_or_404
from django.core.paginator import Paginator
from . import models


# Create your views here.

def home(request):
    contact_list = models.Blog.objects.all()
    paginator = Paginator(contact_list, 25)  # Show 25 contacts per page.
    page_number = request.GET.get('page')
    page_obj = paginator.get_page(page_number)
    array = {'blogs': page_obj}
    return render(request, 'website/pages/blog-pages.html', array)


def show(request, str):
    blog = get_object_or_404(models.Blog, slug=str)
    array = {'blog': blog}
    return render(request, 'website/pages/blog-show.html', array)

```
