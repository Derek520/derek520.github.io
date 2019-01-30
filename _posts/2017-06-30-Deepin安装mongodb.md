---
layout: post
title: Deepin安装Mongodb
categories: Mongodb
description: Mongodb
keywords: Mongodb
comments: true
---

摘要： Deepin 15.8系统安装mongodb数据库方法，整理好安装步骤和方法，只需要按照步骤安装即可。

安装网址：[https://docs.mongodb.com/manual/administration/install-on-linux/](https://docs.mongodb.com/manual/administration/install-on-linux/)

#### 1. 导入MongoDB public GPG Key   
   
```python
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
# 如果添加公钥时，报错，没有dirmngr,执行下面的安装命令，再添加
sudo apt install dirmngr
```

#### 2. 添加软件源   

```python
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
```

#### 3. 更新本地软件包  

```python
sudo apt-get update
```

#### 4. 安装MongoDB
```python
sudo apt-get install -y mongodb-org
```

#### 基本使用：  

```python
mongo -version
#查看帮助
mongod –help  
#启动
sudo service mongod start  
#停止
sudo service mongod stop  
#重启
sudo service mongod restart  
#查看是否启动成功
ps ajx|grep mongod  
#配置文件的位置
sudo vi /etc/mongod.conf
# 默认端⼝
27017  
# 日志的位置
/var/log/mongodb/mongod.log  

#启动本地客户端:
mongo  
#查看帮助：
mongo –help  
#退出：
exit或者ctrl+c  
```

创建账号之后，如果没有登录而使用，则会报错，只有先登录后才可以使用

#### 卸载moogdb:

```
一、卸载只是 mongodb
这将删除只是 mongodb 包本身。

sudo apt-get remove mongodb


二、卸载 mongodb 和它的依赖项。
这将删除 mongodb 软件包和不再需要的任何其他受养人包

sudo apt-get remove --auto-remove mongodb


三、清除您的配置数据
如果你还想要删除您的本地/config 文件为 mongodb，那么这将工作。

sudo apt-get purge mongodb
或者
sudo apt-get purge --auto-remove mongodb
```

#### ubuntu 16.0.4 源码安装mongodb

1. 下载文件，解压文件  

[https://www.mongodb.com/download-center/community](https://www.mongodb.com/download-center/community)

2. 解压文件  

```python
tar -zxvf mongodb-linux-x86_64-ubuntu1604-4.0.1.tgz
mv mongodb-linux-x86_64-ubuntu1604-4.0.1 /usr/local/mongodb
```
3. 创建文件夹　　

```python
mkdir -p /data/mongodb
mkdir -p /data/logs/mongodb
mkdir -p /data/conf/mongodb
touch /data/logs/mongodb/mongodb.log
touch /data/conf/mongodb/mongodb.conf
```

4. 执行命令

```python
dbpath=/data/mongodb logpath=/data/logs/mongodb/mongodb.log port=27017 fork=true nohttpinterface=true
```

5. vi编辑mongodb.conf,添加一下内容 

```python
#端口号
port = 27017 
#数据目录
dbpath = /data/mongodb
#日志目录
logpath = /data/logs/mongodb/mongodb.log
#设置后台运行
fork = true
#日志输出方式
logappend = true
#开启认证
#auth = true
#本地ip
#bind_ip=127.0.0.1
```

6. 启动mongo

```python
cd /usr/local/mongodb/bin/

./mongod --config /data/conf/mongodb/mongodb.conf
```

7. 进入mongo数据库  

```python
/usr/local/mongodb/bin/mongo
```

8. 将mongo加入环境变量中

```python
vi ~/.bashrc
export PATH=$PATH:/usr/local/mongodb-linux-x86_64-rhel70-3.6.6/bin
source .bashrc
```

#### 报错处理  

报错1:  

```python

./mongod: error while loading shared libraries: libcurl.so.4: cannot open shared object file: No such file or directory 
在启动./mongod 的时候缺少 libcurl.so 库
安装libcurl4-openssl-dev
apt-get install libcurl4-openssl-dev
```  
报错2：  

```python

./mongod: error while loading shared libraries: libnetsnmpmibs.so.30: cannot open shared object file: No such file or directory
安装
apt-get install snmpd snmp snmp-mibs-downloader
```