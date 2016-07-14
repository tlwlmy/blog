title: phpmyadmin链接多个数据库
date: 2016-07-14 16:31:46
tags: mysql,服务器
---

### 查看phpmyadmin安装目录
```bash
$ whereis phpmyadmin
phpmyadmin: /etc/phpmyadmin /usr/share/phpmyadmin
```

### 方法一
- 修改/usr/share/phpmyadmin/libraries/config.default.php
```php
/** 
 * allow login to any user entered server in cookie based authentication 
 * 
 * @global boolean $cfg['AllowArbitraryServer'] 
 */  
$cfg['AllowArbitraryServer'] = true; //默认是false,改成true 
```
### 方法二
- 复制/usr/share/phpmyadmin/config.sample.inc.php，命名为config.inc.php
```bash
 $ cd /usr/share/phpmyadmin
 $ sudo cp config.sample.inc.php config.inc.php
```
- 修改config.inc.php文件，在第一个Servers配置下加多一个数据库配置
```php
$i++;
$cfg['Servers'][$i]['verbose'] = 'tlwlmy';    // 链接名字
$cfg['Servers'][$i]['host'] = '192.168.0.1';
$cfg['Servers'][$i]['port'] = '';
$cfg['Servers'][$i]['socket'] = '';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['AllowNoPassword'] = false;
```

### 方法三
- 修改/etc/phpmyadmin/config.inc.php，在第一个Servers配置下加多一个数据库配置
```php
$i++;
$cfg['Servers'][$i]['verbose'] = 'tlwlmy';    // 链接名字
$cfg['Servers'][$i]['host'] = '192.168.0.1';
$cfg['Servers'][$i]['port'] = '';
$cfg['Servers'][$i]['socket'] = '';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['AllowNoPassword'] = false;
```

### 总结
- 使用第一种方法，需要自己填写host，切换数据库比较麻烦
- 第二种方法是网上大多数查到的，但是修改配置很多次都不成功
- 第三种方法，成功配置了，其实效果是和第二种一样的
- 第二种方法不成功可能是因为读取的配置文件可能是使用/etc/phpmyadmin/config.inc.php，而不是/usr/share/phpmyadmin/config.inc.php下的

### 参考
- http://blog.51yip.com/mysql/1250.html（方法一和方法二）
- http://www.onlinehowto.net/config-multiple-servers-in-phpmyadmin/1405（方法二）
- http://www.linuxfunda.com/2013/10/06/how-to-manage-multiple-mysql-server-using-one-phpmyadmin/（方法三）

