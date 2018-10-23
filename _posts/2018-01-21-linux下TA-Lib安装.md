---
layout: post
title:  Linux安装TA-Lib
categories: Linux
description: TA-lib
keywords: Linux
comments: true
---

摘要： linux安装TA-Lib报错，无法安装的问题，进行记录

pip install TA-Lib
报一下错
![](/images/assets/talib.png)

安装注意事项：

1. 下载安装包：ta-lib-0.4.0-src.tar.gz

2.解压文件并进入ta-lib目录，执行以下语句

    ./configure --prefix=/usr

3. 执行make

4. 执行sudo make install

5. 再次安装pip install TA-Lib

按以上步骤执行，将会安装成功!