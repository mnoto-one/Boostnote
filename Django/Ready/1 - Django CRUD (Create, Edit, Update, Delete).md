---
title: 1 - Django CRUD (Create, Edit, Update, Delete)
tags:
  - Django
  - CRUD
  - Create
  - Edit
  - Update
  - Delete
  - Forms
  - ModelForm
---

### 📜 List files
```python
1 -> "my_proj/settings.py"
2 -> "books/models.py"
3 -> "books/admin.py"
4 -> "books/views.py"
5 -> "books/urls.py"
6 -> "my_proj/urls.py"
7 -> "books/templates/books/book_list.html"
8 -> "books/templates/books/book_detail.html"
9 -> "books/templates/books/book_form.html"
10 -> "books/templates/books/book_confirm_delete.html"
```
----
* In this post I briefly cover the step needed to create a CRUD app in Django, the steps we will need are:
  * Install Django & start new project
  * Create an App
  * Create the Model
  * Create the Admin Interface (optional)
  * Create the View
  * Define the URLs (i.e. URL to View mapping)
  * Create the Templates

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Install Django and Start New Project
🔰 Terminal
```shell
python3 -m venv crudenv
source crudenv/bin/activate
pip install django
django-admin startproject my_proj
cd my_proj
```
 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Create new App
🔰 Terminal
```shell
python manage.py startapp books
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 INSTALLED_APPS
 📁 -1 my_proj/settings.py
 
```python
...
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'books.apps.BooksConfig',
]
...
 ```
 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Create the Model
 📁 -2 books/models.py
 
```python
from django.db import models
from django.urls import reverse


class Book(models.Model):
    name = models.CharField(max_length=200)
    pages = models.IntegerField()

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return reverse('book_edit', kwargs={'pk': self.pk})
 ```
 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Create the Model
 📁 -2 books/models.py
```shell
python manage.py makemigrations
python manage.py migrate
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Admin Interface (optional)
 📁 -3 books/admin.py
 
```python
from django.contrib import admin
from books.models import Book

admin.site.register(Book)
 ```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Books Views
 📁 - 4 books/views.py
 
```python
from django.views.generic import ListView, DetailView
from django.views.generic.edit import CreateView, UpdateView, DeleteView
from django.urls import reverse_lazy
from books.models import Book


class BookList(ListView):
    model = Book


class BookView(DetailView):
    model = Book


class BookCreate(CreateView):
    model = Book
    fields = ['name', 'pages']
    success_url = reverse_lazy('book_list')


class BookUpdate(UpdateView):
    model = Book
    fields = ['name', 'pages']
    success_url = reverse_lazy('book_list')


class BookDelete(DeleteView):
    model = Book
    success_url = reverse_lazy('book_list')
 ```
 
 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Define the URLs
 📁 - 5 books/urls.py
 
```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.BookList.as_view(), name='book_list'),
    path('view/<int:pk>', views.BookView.as_view(), name='book_view'),
    path('new', views.BookCreate.as_view(), name='book_new'),
    path('view/<int:pk>', views.BookView.as_view(), name='book_view'),
    path('edit/<int:pk>', views.BookUpdate.as_view(), name='book_edit'),
    path('delete/<int:pk>', views.BookDelete.as_view(), name='book_delete'),
]
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 include URLs
 📁 - 6 my_proj/urls.py
 
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('books/', include('books.urls')),
    path('admin/', admin.site.urls),
]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 runserver and insert data books in admin
🔰 Terminal
```shell
python manage.py runserver
```
🔰 Open the browser
```shell
http://127.0.0.1:8000/admin/books/book/
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 book_list.html
 📁 - 7 books/templates/books/book_list.html
 
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
<h1>Books</h1>

<table style="border: 1px solid">
    <thead>
    <tr>
        <th>Name</th>
        <th>Pages</th>
        <th>View</th>
        <th>Edit</th>
        <th>Delete</th>
    </tr>
    </thead>
    <tbody>
    {% for book in object_list %}
        <tr>
            <td>{{ book.name }}</td>
            <td>{{ book.pages }}</td>
            <td><a href="{% url 'book_view' book.id %}">view</a></td>
            <td><a href="{% url 'book_edit' book.id %}">edit</a></td>
            <td><a href="{% url 'book_delete' book.id %}">delete</a></td>
        </tr>
    {% endfor %}
    </tbody>
</table>

<a href="{% url 'book_new' %}">New</a>
</body>
</html>
```
![img](http://127.0.0.1:5555/Django/Ready/CRUD/1.png)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 book_detail.html
 📁 - 8 books/templates/books/book_detail.html
 
```html
<h1>Book Details</h1>
<h2>Name: {{object.name}}</h2>
Pages: {{ object.pages }}
```
![img](http://127.0.0.1:5555/Django/Ready/CRUD/2.png)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 book_form.html
 📁 - 9 books/templates/books/book_form.html
 
```html
<h1>Book Edit</h1>
<form method="post">{% csrf_token %}
    {{ form.as_p }}
    <input type="submit" value="Submit" />
</form>
```
![img](http://127.0.0.1:5555/Django/Ready/CRUD/3.png)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 book_confirm_delete.html
 📁 - 10 books/templates/books/book_confirm_delete.html
 
```html
<h1>Book Delete</h1>
<form method="post">{% csrf_token %}
    Are you sure you want to delete "{{ object }}" ?
    <input type="submit" value="Submit"/>
</form>
```
![img](http://127.0.0.1:5555/Django/Ready/CRUD/4.png)

---
### 💬 Function Based View Version
 📁 🔁 -4 books/views.py
```python
from django.shortcuts import render, redirect, get_object_or_404
from django.forms import ModelForm

from books.models import Book


class BookForm(ModelForm):
    class Meta:
        model = Book
        fields = ['name', 'pages']


def book_list(request, template_name='books/book_list.html'):
    book = Book.objects.all()
    data = {}
    data['object_list'] = book
    return render(request, template_name, data)


def book_view(request, pk, template_name='books/book_detail.html'):
    book = get_object_or_404(Book, pk=pk)
    return render(request, template_name, {'object': book})


def book_create(request, template_name='books/book_form.html'):
    form = BookForm(request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('book_list')
    return render(request, template_name, {'form': form})


def book_update(request, pk, template_name='books/book_form.html'):
    book = get_object_or_404(Book, pk=pk)
    form = BookForm(request.POST or None, instance=book)
    if form.is_valid():
        form.save()
        return redirect('book_list')
    return render(request, template_name, {'form': form})


def book_delete(request, pk, template_name='books/book_confirm_delete.html'):
    book = get_object_or_404(Book, pk=pk)
    if request.method == 'POST':
        book.delete()
        return redirect('book_list')
    return render(request, template_name, {'object': book})

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Define the URLs
 📁 🔁 - 5 books/urls.py
 
```python
from django.urls import path

from books import views

urlpatterns = [
    path('', views.book_list, name='book_list'),
    path('view/<int:pk>', views.book_view, name='book_view'),
    path('new', views.book_create, name='book_new'),
    path('edit/<int:pk>', views.book_update, name='book_edit'),
    path('delete/<int:pk>', views.book_delete, name='book_delete'),
]
```

# ⚠️ Warning

### 💬 If was Upload for create ...
 📁 🔁 -4 books/views.py

```python
def book_create(request, template_name='books/book_form.html'):
    form = BookForm(request.POST or None, request.FILES or None)
    if form.is_valid():
        form.save()
        return redirect('book_list')
    return render(request, template_name, {'form': form})
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 If was Upload for update ...
 📁 🔁 -4 books/views.py
```python
def book_update(request, pk, template_name='books/book_form.html'):
    book = get_object_or_404(Book, pk=pk)
    if request.method == 'POST':
        form = BookForm(request.POST, request.FILES or None, instance=book)
        if form.is_valid():
            form.save()
            return redirect('book_list')
    else:
        form = BookForm(instance=book)
    return render(request, template_name, {'form': form})

```

### 💬 enctype for form
 📁 🔁 -9 books/templates/books/book_form.html
```html
<form method="post" enctype="multipart/form-data">
    ...
</form>
```
