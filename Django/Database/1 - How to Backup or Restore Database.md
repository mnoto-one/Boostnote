---
title: 1 - How to Backup or Restore Database
tags:
  - Django
  - Database
  - Backup
  - Restore
---

### 💬 Command
🔰 Terminal
```shell
python manage.py dumpdata > datadump.json
```

* Next, change your settings.py to the mysql database.

### 💬 Finally :
```
python manage.py loaddata datadump.json
```

### 💬 one or two table 
```
python manage.py dumpdata games.categorygames games.games  > datadumpgames.json
```
