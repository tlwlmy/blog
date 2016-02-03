title: Ubuntu sshpass install
date: 2016-01-21 16:57:21
tags:
---

### 直接安装
```sql
$ sudo apt-get install sshpass
```

### 使用[源安装](http://packages.ubuntu.com/precise/utils/sshpass)
```sql
$ tar -zxvf download/sshpass_1.05.orig.tar.gz
$ cd sshpass-1.05
$ ./configure
$ sudo make && make install
```
