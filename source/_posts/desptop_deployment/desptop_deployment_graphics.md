layout: posd
title: ubuntu14.04系统Nvidia显卡安装
date: 2016-04-02 19:53:00
tags:
---

### 1.根据显卡型号下载驱动
- 显卡型号：Nvidia GeForce GTX 750 ( 2 GB / 技嘉 )
- Nvidia官方显卡下载地址（http://www.geforce.cn/drivers)，选择对应的显卡型号下载，由于点击同意并下载，是跳到链接文件，需要采用wget方式下载，如下
```
wget http://cn.download.nvidia.com/XFree86/Linux-x86_64/361.42/NVIDIA-Linux-x86_64-361.42.run
```

### 2.卸载Nvidia显卡，屏蔽其他显卡
- 卸载显卡
```
sudo apt-get remove --purge nvidia-*
```
- 将其他显卡加入黑名单列表，编辑/etc/modprobe.d/blacklist.conf文件，添加
```
blacklist vga16fb 
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
```
- 保存文件，执行命令使黑名单列表生效
```
sudo update-initramfs -u
```

### 3.显卡安装
- 进入系统，ctrl+alt+f1进入tty， 关闭lightdm
```
sudo service lightdm stop
```
- 安装显卡,安装期间会遇到报错the distribution-provided pre-install script failed!不必理会，继续安装
```
chmod +x NVIDIA-Linux-*-.run
./NVIDIA-Linux-*-.run
```
- 重新启动lightdm
```
sudo service lightdm start
```
- 重启电脑
```
sudo reboot
```

### 4.总结
- 每次安装显卡都是一个蛋疼的过程，第一次安装成功显卡，都是重装系统十多次才搞定的。
- 从ubuntu15.04装到14.04，用装15.04安装，直接花屏，进入连tty都是花屏，根本看不起输入的命令，连登陆用户都不可以，换了14.04后，有点花，但是还是可以看的清。
- 有时候安装过程会出现无线网卡驱动没安装成功，只能用网线链接上网，sudo apt-get update一下才能用无线连上网。
- 这次是第二次安装，重装了四，五次才成功，还是用14.04比较稳定，尝试使用nvidia-340安装驱动显卡，结果花屏，导致有重新用对应的显卡安装。
- 每次使用ubuntu测试模式，显卡和无线网卡都是能正常使用，但是安装完总一个是有问题的。
