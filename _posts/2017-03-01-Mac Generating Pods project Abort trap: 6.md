---
layout: post
title: Mac Generating Pods project Abort trap
categories: Bug
description: Mac Generating Pods project Abort trap
keywords: mac,Pods
comments: true
---








# Mac Generating Pods project Abort trap: 6

作者:**AustinKuture**

```
摘要: 使用cocoapods为项目添加pod库时,发现未产生.xcworkspace文件,
     同时终端上显示"Generating Pods project Abort trap: 6",本篇文
     章主要分析可能产生的原因并找出最适合的方法解决此类问题.
```

- 为项目添加cocoapods如果产生此种错误时,主要有以下几点原因:

## 1,cocoapods版本过低:

> 打开终端在终端输入:pod --version,目前最新版本是1.2.0(2017年3月),如果发现版本过低,则可以在终端输入以下命令:gem install cocoapods 更新cocoapods工具然后 pod install即可

![img](https://static.oschina.net/uploads/space/2017/0301/164513_oA5x_2728740.png)

## 2,ruby版本过低:

- 在终端输入:rvm list known查看所有ruby版本 

![img](https://static.oschina.net/uploads/space/2017/0301/163404_bYHq_2728740.png)                             

- 输入ruby -v 查看当前版本

![img](https://static.oschina.net/uploads/space/2017/0301/163450_lQoy_2728740.png)

- 如果不是最新的则输入ruby 2.3.0 install  (注:2.30为版本号)

## 3,使用了过期的ruby镜像:

- 终端输入:gem sources -l查看当前镜像源

![img](https://static.oschina.net/uploads/space/2017/0301/163756_bzuQ_2728740.png)

> 2017年之前国内镜像源一直是 <https://ruby.taobao.org/>,目前镜像源已由淘宝改为<https://gems.ruby-china.org/>
>
> ![img](https://static.oschina.net/uploads/space/2017/0301/164048_rMB6_2728740.png)

- 更改方法:

> 1>移除旧的镜像源 , gem sources --remove https://ruby.taobao.org/
>
> 2>添加新的镜像源, gem sources --add https://gems.ruby-china.org/

- 完成后查看一下,gem sources -l

## 4,排除前两种后,更改ruby 镜像源时报错,错误原因为请求拒绝:

- 当遇见修改镜像遭到拒绝时,说明在安装或者产生根目录时使用了管理员身份进行的操作,解决方法如下:
- 打开终端输入: sudo -s 以管理员身份运行![img](https://static.oschina.net/uploads/space/2017/0301/164938_Kzt7_2728740.png)           
- 输入sudo -s 后系统要求输入密码,密码输入时为不可见状态,直接输入并回车即可.成功获得超级管理员身份后用户名称会变为以下状态:![img](https://static.oschina.net/uploads/space/2017/0301/165246_bph4_2728740.png)

此时以超级管理员的身份,重复操作步骤3即可修改镜像源.

## 5,当以上4种情况皆不可行时,卸载ruby环境和cocoapods,并重新安装,安装教程:<http://www.jianshu.com/p/6d8604f0b94c>