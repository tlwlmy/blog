layout: posd
title: ubuntu14.04系统基本配置
date: 2016-04-02 19:53:00
tags:
---

# 1.浏览器
* 使用ubuntu默认库安装Chrome和Pepper Flash Player
```
sudo apt-get update
sudo apt-get install chromium-browser
sudo add-apt-repository ppa:skunk/pepper-flash
sudo apt-get update
sudo apt-get install pepflashplugin-installer
sudo update-pepperflashplugin-nonfree --install

```
# 2.输入法
* 搜狗输入法，选择对应的操作系统位数下载，点击deb包安装
```
http://pinyin.sogou.com/linux/?r=pinyin

```
# 3.终端
* [linux终端选择参考](http://blog.jobbole.com/59165/)
* ubuntu下是使用Terminator和Guake，mac下使用iTerm2，安装后自行配置终端颜色，字体，透明度，快捷键
```
sudo apt-get install terminator
sudo apt-get install guake
```

# 4.Consolas字体添加
* 添加consolas字体，修改终端Terminator和Guake字体，选择consolas字体，退出重新打开终端即可以生效
* 下载：http://pan.baidu.com/s/1pLlCY5l
```
sudo mkdir /usr/share/fonts/winfonts
sudo cp consola.ttf /usr/share/fonts/winfonts/
cd /usr/share/fonts/winfonts/
sudo mkfontscale    # 创建字体的fonts.scale文件，它用来控制字体旋转缩放
sudo mkfontdir      # 创建字体的fonts.dir文件，它用来控制字体粗斜体产生
sudo fc-cache -fv   # 建立字体缓存信息，也就是让系统认识认识新字体
```
# 5.Awesome桌面环境安装
* awesome是一款平铺式窗口管理器，将所有打开的窗口设置成各种平铺方式，让它们之间无间隙的平铺于桌面上。awesome可以全部使用键盘来操作窗口。安装完后，注销用户，然后在登录时选择awesome即可。
```
sudo apt-get install awesome awesome-extra
cp /etc/xdg/awesome/rc.lua ~/.config/awesome
```
* Gnome Do能根据用户键入的内容进行自动匹配，从而快速打开系统中已有的程序、文件、书签等
```
sudo apt-get install gnome-do
```

# 6.使用VirtualBox安装虚拟环境windows
* 在ubuntu安装虚拟机windows，装一些windows常用的工具，抓包工具feddle，聊天工具qq
* 网络使用桥接模式，使用增强功能，传输文件使用共享文件夹
* https://www.virtualbox.org/wiki/Linux_Downloads
```
wget http://download.virtualbox.org/virtualbox/5.1.18/virtualbox-5.1_5.1.18-114002~Ubuntu~trusty_amd64.deb
sudo dpkg -i virtualbox-5.1_5.1.18-114002~Ubuntu~trusty_amd64.deb
```
