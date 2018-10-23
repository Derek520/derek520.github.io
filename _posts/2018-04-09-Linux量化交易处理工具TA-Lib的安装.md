---
layout: post
title: Linux量化交易处理工具TA-Lib的安装
categories: [Linux,Jupyter]
description: Linux量化交易处理工具TA-Lib的安装
keywords: Linux,MACD,TA-Lib
comments: true
---



## Linux量化交易处理工具TA-Lib的安装

> 适用系统Ubuntu,Deepin,Debain，OSX

#### pip 指令安装
> 通过终端执行指令进行安装

##### Deepin,Ubuntu 
```
pip install TA-Lib
```
##### MacOS
```
brew install ta-lib
```

### 解决因依赖文件造成的报错情况
在Linux系统下会报如下错误
![Wrong00](/images/posts/Linux/TA-Lib-001.png)
解决方法：
1 安装依赖文件ta-lib
```
sudo apt-get install ta-lib
```
如果此时报如下错误则进行第2步：

![Wrong01](/images/posts/Linux/TA-Lib-002.png)

2 继续安装依赖文件python3-dev
```
sudo apt-get install python3-dev
```
如果已经安装过该依赖文件的会显示如下：
![Wrong02](/images/posts/Linux/TA-Lib-003.png)

3 前两步完成后，使用pip重新安装TA-Lib,安装执行后进入终端尝试导入该模块 import ta-lib如果仍然不能导入，则进行4步

4 [点击下载安装包](http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz)
> 1 解压压缩包

> 2 cd 进入当前文件夹

> 3 执行 ./configure --prefix=/usr

> 4 make

> 5 sudo make install

安装编译并安装完成后，重装执行指令即可
```
pip install TA-Lib
```



