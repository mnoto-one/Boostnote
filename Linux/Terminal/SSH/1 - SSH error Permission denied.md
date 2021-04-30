---
title: 1 - SSH error Permission denied
tags:
  - Linux
  - SSH
  - Error
  - Permission
  - Denied
---

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Command
🔰 Terminal
```shell
sudo nano etc/ssh/sshd_config
```
🔰  Before it will be like this:
```
#LoginGraceTime 2m
#PermitRootLogin prohibit-password
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
```
🔰  Make it to :
```
#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
```
🔰  Save it and use ssh restart command

```shell
systemctl restart sshd
```
