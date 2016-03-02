layout: posd
title: python2、pyhton3和nc命令共享本地文件
date: 2015-10-15 15:18:10
tags:
---
### python2
```bash
python -m SimpleHTTPServer 20000
```

### python3
```bash
python3 -m http.server 20000
```
### nc命令
> 远程拷贝文件 从A服务器拷贝到B服务器上
```bash
A服务器：nc -l 1234 > text.txt
B服务器：nc 192.168.10.11 1234 < text.txt
```
