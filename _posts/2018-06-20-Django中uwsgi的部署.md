---
layout: post
title: Django中uwsgi的部署
categories:
  - Django
description: Django中uwsgi的部署
keywords: django,uwsgi
comments: true
---


# Django中uwsgi的部署

在django项目的setting.py文件的同级目录下，新建一个配置文件　uwsgi.ini并配置文件，内容如下
```
[uwsgi]
# 配置服务器的监听ip和端口，让uWSGI作为nginx的支持服务器的话，设置socke就行；如果要让uWSGI作为单独的web-server，用http
http = 0.0.0.0:80
#socket = 0.0.0.0:80
# 配置项目目录（此处设置为项目的根目录）
chdir = /mnt/Project/ML/KnowledgeGraph/KGGraph 
# 配置入口模块 (django的入口函数的模块，即setting同级目录下的wsgi.py)
wsgi-file = KGGraph/wsgi.py
# 开启master, 将会多开一个管理进程, 管理其他服务进程
master = True
# 服务器开启的进程数量
processes = 2
# 以守护进程方式提供服, 输出信息将会打印到log中
daemonize = wsgi.log
# 服务器进程开启的线程数量
threads = 4
# 退出的时候清空环境变量
vacuum = true
# 进程pid
pidfile = uwsgi.pid
# 配uWSGI搜索静态文件目录（及django项目下我们存放static文件的目录，用uWSGI作为单独服务器时才需要设置）
check-static = /mnt/Project/ML/KnowledgeGraph/KGGraph/templates/RuisiGraph
```

启动uwsgi服务器
```
uwsgi --ini uwsgi.ini
```
重启uwsgi服务
```
uwsgi --reload uwsgi.pid
```
停止uwsgi服务
```
uwsgi --stop uwsgi.pid
```


结果如下所示
![uwsgi00](/images/posts/Django/uwsgi00.png)

