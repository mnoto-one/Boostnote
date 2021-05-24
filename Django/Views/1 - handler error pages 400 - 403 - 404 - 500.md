---
title: 1 - handler error pages 400 - 403 - 404 - 500
tags:
  - Django
  - Views
  - error404
  - error400
  - error403
  - error500
---

### 📜 List files
```python
1 -> "urls.py"
2 -> "views.py"
```
---

### 💬 added handler in file url
 📁 -1 urls.py
```python
handler400 = 'myresume_app.views.error_400_view'
handler403 = 'myresume_app.views.error_403_view'
handler404 = 'myresume_app.views.error_404_view'
handler500 = 'myresume_app.views.error_500_view'
```
### 💬 code views for handler
 📁 -2 views.py
```python
from django.shortcuts import render

def error_400_view(request, exception):
    return render(request, 'storefront/errors/error-400.html', status=400)


def error_403_view(request, exception):
    return render(request, 'storefront/errors/error-403.html', status=403)


def error_404_view(request, exception):
    return render(request, 'storefront/errors/error-404.html', status=404)


def error_500_view(request):
    return render(request, 'storefront/errors/error-500.html', status=500)
```

### 💬 If the two templates are separate
 📁 -2 views.py
```python
from django.shortcuts import render


def error_400_view(request, exception):
    if request.path.startswith('/dashboard'):
        return render(request, 'Dashboard/errors/error-400.html', status=400)
    else:
        return render(request, 'website/errors/error-400.html', status=400)


def error_403_view(request, exception):
    if request.path.startswith('/dashboard'):
        return render(request, 'Dashboard/errors/error-403.html', status=403)
    else:
        return render(request, 'website/errors/error-403.html', status=403)


def error_404_view(request, exception):
    if request.path.startswith('/dashboard'):
        return render(request, 'Dashboard/errors/error-404.html', status=404)
    else:
        return render(request, 'website/errors/error-404.html', status=404)


def error_500_view(request):
    if request.path.startswith('/dashboard'):
        return render(request, 'Dashboard/errors/error-500.html', status=500)
    else:
        return render(request, 'website/errors/error-500.html', status=500)

```
