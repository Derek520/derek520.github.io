---
layout: post
title:  Python操作oracle数据库
categories: 
    - Oracle
    - Python
description: Oracle
keywords: Oracle
comments: true
---

摘要：由于公司的数据库是oracle，之前都是用java连接操作，现在改用python操作,增删改查

#### 刚开始安装的时候，费了一番功夫，因为我的电脑系统deepin,网上多数都是windows下的

1.　下载安装cx_oracle，linux很简单的，直接使用下面命令安装：  

   
```python
pip install cx_oracle      #不存在版本问题，我试过默认是最高版本
```
        
2.  安装后以后，虽然能导入，但是用不了,需要下载oracle客户端：  

<http://www.oracle.com/technetwork/database/database-technologies/instant-client/downloads/index.html>　
        
```python
instantclient-jdbc-linux.x64-11.2.0.4.0
instantclient-sdk-linux.x64-11.2.0.4.0
instantclient-sqlplus-linux.x64-11.2.0.4.0
instantclient-basic-linux.x64-11.2.0.4.0.zip
将以上的三个文件解压
　instantclient_11_2　　＃这个对应数据库的版本，和自己系统

instantclient-basic-linux.x64-11.2.0.4.0.zip 解压这一个也可以用

```

3. 下载下来解压，放在自己知道目录，一般/opt/oracle/目录下，没有需要新建  
 
4. 需要配置系统变量  
        
````python
export ORACLE_HOME=/hoem/derek/app/oracle
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export PATH=$ORACLE_HOME/bin:$PATH 
        
````  
      
5. 请将Instant Client永久添加到运行时链接路径  

```python
sudo sh -c "echo /home/derek/app/oracle/instantclient_11_2 > /etc/ld.so.conf.d/oracle-instantclient.conf"
sudo sudo ldconfig
    
```

        

    


