---
title: 2 - How to multi website openlitespeed
tags:
  - Litespeed
  - Multi
  - Website
  - Teach
---

### 📜 List files
```python
1 -> "TonyTeachesTech/html/index.html"
2 -> "etc/hosts"
```
---
### 💬 Create folder and file for start project
🔰 Terminal

```ssh
cd /usr/local/lsws/
ls
sudo su
sudo mkdir TonyTeachesTech
cd TonyTeachesTech
mkdir html
cd html
nano index.html
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 html
 📁 -1 TonyTeachesTech/html/index.html
```html
<h1>Hello welcome to My webite 1</h1>
<p>TonyTeachesTech</p>
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

🔰 Virtual Hosts > new

![img](http://127.0.0.1:5555/LiteSpeed/2021/1.png)

* $SERVER_ROOT
/usr/local/lsws/
* $VH_NAME
Virtual Host Name *


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

🔰 Virtual Hosts > TonyTeachesTech > General

![img](http://127.0.0.1:5555/LiteSpeed/2021/2.png)

save

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

🔰 Listener Default > Virtual Host Mappings 

![img](http://127.0.0.1:5555/LiteSpeed/2021/3.png)

save

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


 📁 -2 etc/hosts
```
192.168.2.128 tonyteachestech.xyz
```

test

▶️ Result in Terminal

tonyteachestech.xyz


# ⚠️ Warning
### 💬 If you want to upload a regular project folder

🔰 Virtual Hosts > ... > Basic

![img](http://127.0.0.1:5555/LiteSpeed/2021/4.png)

🔰 Virtual Hosts > ... > General

![img](http://127.0.0.1:5555/LiteSpeed/2021/5.png)
