title: ubuntu14.04系统redis多实例运行
date: 2016-11-25 17:03:23
tags: redis多实例
---

### 一、安装最新的redis版本
```bash
apt-get remove redis-server    # 删除旧版
apt-get autoremove
sudo apt-get install -y python-software-properties
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:rwky/redis
sudo apt-get update
sudo apt-get install -y redis-server
```

### 二、redis配置文件
``` bash
/etc/init.d/redis-server-------------redis的可执行程序
/etc/redis/redis.conf----------------redis的配置文件
/usr/bin/redis-server---------------redis的自启动文件
```

### 三、redis默认配置的端口号是6379，添加多配置一个6380端口
* 复制redis配置文件
```bash
cp /etc/redis/redis.conf /etc/redis/redis6380.conf
```
* 修改redis6380.conf文件，vim /etc/redis/redis6380.conf
```bash
pidfile /var/run/redis/redis-server6380.pid
port 6380
logfile /var/log/redis/redis-server6380.log
dbfilename dump6380.rdb
bind 0.0.0.0    # 允许其他服务器访问
```

### 四、添加redis6380执行文件
* 复制redis执行文件
```bash
sudo cp /etc/init.d/redis-server /etc/init.d/redis-server6380
```
* 修改redis-server6380配置文件对应位置
```bash
DAEMON=/usr/bin/redis-server
DAEMON_ARGS=/etc/redis/redis_6380.conf
NAME=redis-server
DESC=redis-server6380

RUNDIR=/var/run/redis
PIDFILE=$RUNDIR/redis-server6380.pid
```

### 五、启动redis6380
```bash
sudo service redis-server6380 (start|stop|restart)
```

### 六、添加redis6380开机启动设置
* 开机启动设置
```bash
sudo update-rc.d redis-server6380 defaults 20    # 开机启动
```
* 取消开启启动设置
```
sudo update-rc.d -f redis-server6380 remove
```
* 测试开机启动，redis6380是否运行
```bash
sudo reboot    # 重启
ps axu | grep redis    # 查询redis进程
```

### 参考
* http://www.cnblogs.com/limx/p/5690604.html
* https://makandracards.com/makandra/7965-run-multiple-redis-servers-on-ubuntu
