---
layout: post
title:  Tensorflow安装
categories: Tensorflow
description: Tensorflow
keywords: Tensorflow
comments: true
---

> 摘要：Tensorflow安装学习


1. Tensorflow安装：anaconda3 python3.6;

windows安装以管理员权限打开命令窗口;linux/MAX直接执行下面命令   

```mysql
pip install --upgrade --ignore-installed tensorflow
```

2. 如果没有安装anaconda3，系统是python3.5或者2.7　安装如下：    

```mysql
Linux/ubuntu:
python2.7: pip install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.1-cp27-none-linux_x86_64.whl 
python3.5: pip3 install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.1-cp35-cp35m-linux_x86_64.whl 

Maxos:
python2: pip install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.1-py2-none-any.whl
python3: pip3 install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.1-py3-none-any.whl

```
### 清华镜像站提供各版本下载安装
#### Contos7
<https://mirrors.tuna.tsinghua.edu.cn/help/tensorflow/>

