title: VirtualBox Usb设备
date: 2016-01-05 10:44:57
tags:
---
### Ubuntu 14.04 VirtualBox虚拟机win7支持Usb设备
需要从[官网](https://www.virtualbox.org/wiki/Downloads)下载Oracle VM VirtualBox Extension Pac
扩展插件需要安装对应的版本，不然可能会报错,查看VirtualBox 版本
```sql
dpkg -l | grep virtualbox
```
下载完成后点击安装，在USB设置添加USB筛选器
查询自己当前用户
```sql
whoami
```
将当前用户加入vboxusers组
```sql
usermod -a -G vboxusers $(whoami)
```
重启Ubuntu系统，再启动虚拟机win7

### 参考
* http://www.cnblogs.com/wanqieddy/archive/2012/03/06/2382408.html
* http://www.cnblogs.com/westfly/archive/2013/04/19/3031330.html
