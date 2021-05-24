---
title: 1 - render a html page without views.py
tags:
  - Django
  - Urls
  - Lambda
  - Render
---

### 📜 List files
```python
1 -> "urls.py"
```
---

### 💬 lambda in path url
 📁 -1 urls.py

```python
from django.shortcuts import render

urlpatterns = [
    path('', lambda request: render(request, 'homepage.html'))
]   
```
