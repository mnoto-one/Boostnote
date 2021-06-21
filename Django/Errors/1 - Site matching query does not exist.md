---
title: 1 - Site matching query does not exist
tags:
  - Error
  - Django
  - Site
  - DoesNotExist
---

▶️  Error

```
DoesNotExist at /admin/login/
Site matching query does not exist.
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Solve problem
 📁 🔁 -1 settings.py
 ```python
SITE_ID=1
```
