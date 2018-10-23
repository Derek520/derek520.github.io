---
layout: post
title:  Django中使用celery完成异步任务
categories: Django
description: Django中使用celery完成异步任务
keywords: Django, celery
comments: true
---


# Django中使用celery完成异步任务 
​                   
>摘要: 本文主要介绍如何在django中用celery完成异步任务，web项目中为了提高用户体验可以对一些耗时操作放到异步队列中去执行，例如激活邮件，后台计算操作等等 当前项目环境为：django==1.11.8   celery==3.1.25   redis==2.10.6  pip==9.0.1  python3==3.5.2django-celery==3.1.17                

### 一，创建Django项目及celery配置

#### 1，创建Django项目

1>打开终端输入：django-admin startproject TestCelery 创建django项目('TestCelery'是项目名称)

2>进行TestCelery在终端输入指令：django-admin startapp testcelery 创建应用('testcelery为应用名称')

#### 2， 为celery设置环境变量

1>项目中在TestCelery中创建celery.py文件(与setting.py同级)输入以下内容：          

```
from celery import Celery
from django.conf import settings
import os

# 为celery设置环境变量
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'TestCelery.settings')

# 创建应用
app = Celery('testcelery')

# 酸配置应用
app.conf.update(
    
    # 本地Redis服务器
    BROKER_URL='redis://127.0.0.1:6379/2',
)

app.autodiscover_tasks(settings.INSTALLED_APPS)
```

2>当前项目目录如下图所示：
​                                  ![img](https://static.oschina.net/uploads/space/2018/0122/175836_zWTN_2728740.png)

 

### 二,创建任务tasks,编写视图View及urls

#### 1, 在testcelery应用中新建tasks.py文件，并写入要进行处理的任务：          

```
from TestCelery.celery import app
from time import sleep


@app.task
def start_running(nums):

    print('***>%s<***' %nums)
    print('--->>开始执行任务<<---')
    for i in range(10):

        print('>>'*(i+1))
        sleep(1)
    print('>---任务结束---<')
```

#### 2，编写view视图，并写入调用client的方法

```
from django.views import View
from django.http import HttpResponse
from .tasks import start_running
from time import sleep

# Create your views here.


class IdexView(View):

    def get(self, request):

        print('>=====开始发送请求=====<')
        for i in range(10):

            print('>>',end='')
            sleep(0.1)

        start_running.delay('》》》》》我是传送过来的《《《《《')
        return HttpResponse('<h2> 请求已发送 </h2>')


```

#### 3，编写testcelery应用的usrls

```
from django.conf.urls import url
from .views import *

urlpatterns = [

    url(r'^$', IdexView.as_view()),
]

```

#### 4，当前项目目录如下图所示：

![img](https://static.oschina.net/uploads/space/2018/0122/180557_BGnz_2728740.png)

### 三，运行项目，开启worker

#### 1, 运行项目在当前项目下输入启动服务指令：python manager.py runserver，出现如下图所示即代表运行成功：

![img](https://static.oschina.net/uploads/space/2018/0122/191744_eRlF_2728740.png)

#### 2，开启worker另在当前项目下另打开一个终端，输入指令: celery -A TestCelery worker --loglevel=DEBUG,启动后如下如示：

![img](https://static.oschina.net/uploads/space/2018/0122/192210_uG4I_2728740.png)

#### 3，调用任务

1>打开浏览器，输入http://127.0.0.1:8000/send/  进行访问![img](https://static.oschina.net/uploads/space/2018/0122/192503_0dWG_2728740.png)

2> woker监听到任务请求时，就会执行耗时任务，如下图所示：

​        ![img](https://static.oschina.net/uploads/space/2018/0122/192710_mRg1_2728740.png)