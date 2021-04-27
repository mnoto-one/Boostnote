---
title: " 1 - How to add icon desktop in Launchers"
tags:
  - Linux
  - Launchers
  - Icon
  - Desktop
  - Apps
---

### 📜 List files
```python
1 -> "namefile.desktop"
```
---


### 💬 Create file desktop
🔰 Terminal
```shell
touch namefile.desktop
```
### 💬 Code example Desktop 1
 📁 -1 namefile.desktop
```
[Desktop Entry]
Categories=Utility;
Exec="/opt/Boost Note/boostnote.next" --no-sandbox
Icon=boostnote.next
Name=Boost Note
StartupWMClass=Boost Note
Terminal=false
Type=Application
```
### 💬 Code example Desktop 1
 📁 -1 namefile.desktop
```
[Desktop Entry]
Categories=Utility;
Exec=charm
Icon=/home/mnoto/Apps/pycharm-2020.2/bin/pycharm.svg
Name=Pycharm
Terminal=false
Type=Application
```

### 💬 Add file desktop in Launchers
🔰 Terminal
```shell
sudo su
cp namefile.desktop /usr/share/applications
```
