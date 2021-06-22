---
title: 2 - How to create date and update date in model
tags:
  - Django
  - Database
  - Models
  - Date
  - Update
  - Create
  - auto_now
---

### 📜 List files
```python
1 -> "app/models.py"
```
---
### 💬 create_time update_time
 📁 -1 app/models.py

```python
...
create_time = models.DateTimeField(auto_now_add=True)
update_time = models.DateTimeField(auto_now=True)
```
