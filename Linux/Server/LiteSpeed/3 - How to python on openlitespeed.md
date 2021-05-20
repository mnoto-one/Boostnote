---
title: 3 - How to python on openlitespeed
tags: []
---

### 💬 Python WSGI Apps with LSAPI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Install Python3 Library

📌 1 - CentOS

🔰 Terminal
```sh
yum install python3-devel
yum install python3-pip
```

💬 You may need to use:

🔰 Terminal
```sh
yum install python36-devel
yum install python36-pip
```


📌 2 - ubuntu

🔰 Terminal
```sh
apt install build-essential
apt-get install python3-dev
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Install WSGI

💬 The easiest and fastest way to run web applications with LiteSpeed Web Server is to install and compile [wsgi-lsapi.](https://www.litespeedtech.com/open-source/litespeed-sapi/download)

```sh
curl -O http://www.litespeedtech.com/packages/lsapi/wsgi-lsapi-1.6.tgz
tar xf wsgi-lsapi-1.6.tgz
cd wsgi-lsapi-1.6
python3 ./configure.py
make
cp lswsgi /usr/local/lsws/fcgi-bin/
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 How to Verify WSGI Script

🔰 Virtual Hosts > new

![img](http://127.0.0.1:5555/LiteSpeed/2021/6.png)

🔰 Virtual Hosts > TonyTeachesTech > General

![img](http://127.0.0.1:5555/LiteSpeed/2021/7.png)


Set up Context
This example assumes you are using the default document root + URI: /python/

Navigate to **Web Admin > Virtual Hosts > Context > Add**

* **Type =** App Server
* **URI =** /python/
* **Location =** /usr/local/lsws/Example/python/
* **Binary Path =** /usr/local/lsws/fcgi-bin/lswsgi
* **Application Type =** WSGI


### 💬 Example 1
![img](http://127.0.0.1:5555/LiteSpeed/2021/8.png)

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Create wsgi.py script

Create a **python** directory under your document root.

🔰 Then, create a wsgi.py file with the following content:

```python

import os
import sys
sys.path.insert(0, os.path.dirname(__file__))

def application(environ, start_response):
    start_response('200 OK', [('Content-Type', 'text/plain')])
    message = 'It works!\n'
    version = 'Python %s\n' % sys.version.split()[0]
    response = '\n'.join([message, version])
    return [response.encode()]
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Verification
💬 Visit http://Server_IP:Port/python/ in your browser 

▶️ Result in Browser
```
It works!

Python x.x.x
```
