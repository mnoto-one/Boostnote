---
title: 2 - How to use file manager with  scp
tags:
  - SSH
  - Scp
  - FileManger
---

### 💬 SCP Command Syntax

📝 The **scp** command syntax take the following form:

🔰 Terminal
```shell
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* 📌 Copy a Local File to a Remote System with the scp Command

🔰 Terminal
```shell
scp file.txt remote_username@10.10.0.2:/remote/directory
```

* 📌  If you want to save the file under a different name, you need to specify the new file name:

🔰 Terminal
```shell
scp file.txt remote_username@10.10.0.2:/remote/directory/newfilename.txt
```

* 📌  If SSH on the remote host is listening on a port other than the default 22 then you can specify the port using the -P argument:

🔰 Terminal
```shell
scp -P 2322 file.txt remote_username@10.10.0.2:/remote/directory
```

* 📌  To copy a directory from a local to remote system, use the -r option:

🔰 Terminal
```shell
scp -r /local/directory remote_username@10.10.0.2:/remote/directory
Co
```
