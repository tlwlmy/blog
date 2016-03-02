title: sentry
date: 2016-03-01 16:46:44
tags: sentry,log,python,django
---

Sentry 是一款基于 Django 实现的日志管理工具，Disqus 团队对其代码贡献不少。虽然 Sentry 本身是 Python 实现的，但是其日志监控功能却不局限于 python，对诸如 Node.js, php, ruby, C#, java 等语言的项目都可以做到无缝集成，甚至可以用来对 iOS, Android 移动客户端以及 Web前端异常进行跟踪。主动上报的方式将错误信息等进行收集汇总和提醒，以帮助我们及时发现项目中的问题。

### 1.安装环境

 - python2.7
 - python-setuptools, python-pip, python-dev, libxslt1-dev, libxml2-dev, libz-dev, libffi-dev, libssl-dev, libpq-dev, libyaml-dev
 - redis >= 2.8.9
 - nginx
 - mysql

### 2.python环境配置

 - 虚拟环境安装

 ```bash
 pip install virtualenv
 pip install virtualenvwrapper
 ```
 - 虚拟环境配置

 ```bash
 export WORKON_HOME=~/.virtualenvs
 mkdir $WORKON_HOME
 echo "export WORKON_HOME=$WORKON_HOME" >> ~/.bashrc
 echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
 echo "export PIP_VIRTUALENV_BASE=$WORKON_HOME" >> ~/.bashrc
 source ~/.bashrc
 ```
 
 - 基本命令
 ```bash
 mkvirtualenv test
 workon test
 deactivate
 rmvirtualenv test
 ```

### 3.sentry安装

 - 新建虚拟环境
 ```bash
 mkvirtualenv sentry
 ```
 - 安装
 ```bash
 pip install sentry
 pip install MYSQL-python
 ```
### 4.sentry配置

 - 初始化
 ```bash
 sentry init /etc/sentry
 ```
 - 修改/etc/sentry/sentry.conf.py数据库配置
 ```python
 DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'sentry',
        'USER': 'sentry',
        'PASSWORD': '',
        'HOST': '',
        'PORT': '3306',
    }
}

 ```
 - sentry启动,upgrade过程可以创建超级用户
 ```bash
 sentry --config=/etc/sentry/sentry.conf.py upgrade
 sentry --config=/etc/sentry/sentry.conf.py start
 ```
 - sentry三个主要模块：web，worker，cron，用supervisor启动的
 ```bash
 [program:sentry-web]
 directory=/home/ymserver
 command=/home/ymserver/virtualenv/sentry/bin/sentry --config=/etc/sentry/sentry.conf.py start
 autostart=true
 autorestart=true
 redirect_stderr=true
 stdout_logfile=/data/log/supervisor/sentry-web.log

 [program:sentry-worker]
 directory=/home/ymserver
 command=/home/ymserver/virtualenv/sentry/bin/sentry --config=/etc/sentry/sentry.conf.py celery worker
 autostart=true
 autorestart=true
 redirect_stderr=true
 stdout_logfile=/data/log/supervisor/sentry-worker.log
 user=ymserver

 [program:sentry-cron]
 directory=/home/ymserver
 command=/home/ymserver/virtualenv/sentry/bin/sentry --config=/etc/sentry/sentry.conf.py celery beat
 autostart=true
 autorestart=true
 redirect_stderr=true
 stdout_logfile=/data/log/supervisor/sentry-cron.log
 ```
 - [nginx配置](http://www.tlwlmy.com/2016/03/01/sentry-nginx/)
 - [sentry.conf.py配置](http://www.tlwlmy.com/2016/03/01/sentry-conf/)

### 5.sentry应用python
 - python安装raven库就可以直接调用了
 ```bash
 pip install raven --upgrade
 ```
 - 例子
 ```python
 from raven import Client
 client = Client('https://<key>:<secret>@app.getsentry.com/<project>')
 try:
     1 / 0
 except ZeroDivisionError:
     client.captureException()
 ```

### 6.参考
 -  https://docs.getsentry.com/on-premise/server/installation/
 -  https://docs.getsentry.com/hosted/clients/python/
 -  http://blog.gaoyuan.xyz/2013/12/18/deploy-sentry-in-product/

