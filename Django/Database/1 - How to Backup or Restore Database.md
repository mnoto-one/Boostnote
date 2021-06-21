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
```sh
python manage.py dumpdata > datadump.json
```

* Next, change your settings.py to the mysql database.

### 💬 Finally :
🔰 Terminal
```sh
python manage.py loaddata datadump.json
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 one or two table 
🔰 Terminal
```sh
python manage.py dumpdata games.categorygames games.games  > datadumpgames.json
```

Or 


### 💬 one or two table 
🔰 Terminal
```sh
python manage.py dumpdata games > datadumpgames.json
```

### 💬 one or two table with multi apps 
🔰 Terminal
```sh
python manage.py dumpdata games website dashboard > datadumpgames.json
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### dumpdata (--exclude)
🔰 Terminal
```sh
python manage.py dumpdata --exclude auth.permission > db.json
```

# ⚠️ Warning
### 💬 Backup Pro
🔰 Terminal
```sh
print manage.py dumpdata --exclude auth.permission --exclude contenttypes > db.json
```
