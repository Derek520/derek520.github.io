---
layout: post
title:  Python调用Java方法
categories: Jpype
description: Jpype
keywords: Jpype
comments: true
---

摘要：本文记录了，使用python调用java的jar，从而实现使用python执行java代码，基本安装使用

1. 安装jpype，安装命令如下  

    pip install jpype1　　　　#此明令是python３.6安装名字
    
2. 下来就是调用，使用了：  

    ![](/images/assets/jpype.png)
    
    使用的时候，需要调用java的jvm，问题就在这里，一个是在环境变量中配置，一个是写个绝对路径；网上好多写的是客户端的jvm.dll，问题我们一般用的是Server，linux下是找不到jvm.dll，但我们可以用Server下的libjvm.so
    
    运行结果如下：  
    
    ![](/images/assets/jpype2.png)

