---
layout: post
title: Anaconda创建虚拟环境及Django的安装
categories:
  - Django
  - Anacoda
  - Linux
description: Anaconda创建虚拟环境及Django的安装
keywords: Linux,Anaconda,虚拟环境,Django
comments: true
---

# Anaconda创建虚拟环境及Django的安装
>适用系统： Deepin、Ubuntu、Mac OS、Windows、Raspberry Pi Linux
>调试环境： Deepin 15.5

本篇文章主要讲解如何使用Anaconda进行虚拟环境的创建、调用、删除等功能，并完成Django的安装与使用
### [Django介绍](#)
Django是一个开放源代码的Web应用框架，由Python写成。运用了MVT模式（Model,View,Template)，主要目标是使得开发复杂的、数据库驱动网站变得简单，Django注重组件的重用性和“可插拔性”，敏捷开发和DRY法则（Don't Repeat Yourself)。Django还提供了可选的创建、阅读、更新、删除界面。
### Anaconda安装Django1.8.2
使用Anaconda之前，请先安装Anaconda安装方法此处不再赘述。Anaconda安装完成后，输入以下命令可以查看当前已创建过的虚拟环境。
```
conda info --envs
```
![Anaconda00](/images/posts/Anaconda/Anaconda03.png)
#### 创建虚拟环境安装Django
```
conda create --name Django_3_1.8.2 python=3
```
>也可以写成conda create -n Django_3_1.8.2 python=3,其中python=3代表python版本为3

![Anaconda01](/images/posts/Anaconda/Anaconda01.png)
安装过程中会提示是否安装（y/n)?输入y进行安装
![Anaconda02](/images/posts/Anaconda/Anaconda00.png)

#### 访问新环境
```
source activate Django_3_1.8.2
```
安装完成后就中以进行Django的安装了，此处使用pip进行安装
```
pip install django==1.8.2
```
![Anaconda03](/images/posts/Anaconda/Anaconda02.png)
#### 测试是否安装完成
```
python -c 'import django;print(django.get_version())'
```
#### 退出环境
```
source deactivate
```
#### 卸载环境
```
conda remove --name Django_3_1.8.2 --all
```
> windows环境下，流程基本一样，唯一的区别是，不使用source，直接用activate 虚拟环境名称即可
