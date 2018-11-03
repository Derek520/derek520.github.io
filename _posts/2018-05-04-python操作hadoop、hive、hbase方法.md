---
layout: post
title:  Python操作hadoop、hive、hbase方法
categories: 大数据
description: 大数据
keywords: 大数据
comments: true
---

>摘要：基于业务需要，需要对hadoop、hive、hbase操作，平时都是在命令行或图形界面操作，现在需要在代码块中连接操作，第一次装遇到不少坑，记录下正确的方法
   

>系统：deepin15.7
python版本：python3.5;   

>连接hive方法，采用pyhive连接
需要安装的依赖，好多实在安装依赖时卡主了
按照以下步骤安装，顺利完成
    
```python
sudo apt-get install sasl2-bin
sudo apt-get install libsasl2-dev
pip install pyhs2
pip install pyhive
pip install thrift_sasl

from pyhive import hive
conn = hive.Connection(host="xxxxx", port=10000, username='xxxx', database='default')
正常操作就ｏｋ
```
    
 
   
2. 连接hbase方法，当你hive连接没问题，那连接hbase没什么问题
    
> 需要安装依赖关系，按照一下步骤安装，　
    　
```python
pip install thrift　　　＃这一步，就是上面　pip install thrift_sasl，如果装了，就不用再装
pip install happybase　　#happybase　连接跟我们正常连接数据库一样

from happybase import Connection
connection = Connection(host="192.168.0.156",port=9090,timeout=None,autoconnect=True,table_prefix=None,table_prefix_separator=b'_',compat='0.98', transport='buffered',protocol='binary')

host：主机名
port：端口
timeout：超时时间
autoconnect：连接是否直接打开
table_prefix：用于构造表名的前缀
table_prefix_separator：用于table_prefix的分隔符
compat：兼容模式
transport：运输模式
protocol：协议
```
            

3. 连接hdfs方法，  

```python

安装 pip install hdfs   

from hdfs import Client
Client("url",root="/",proxy=None,timeout=None,session=None)
url：ip：端口
root：制定的hdfs根目录
proxy：制定登陆的用户身份
timeout：设置的超时时间
session:连接标识
```
    
4. python 操作hadoop，进行分词统计　　

````python
mapper.py  
    
        import sys
        for line in sys.stdin:      # 接收屏幕的值
            words = line.split()    # 以空格切割
            for word in words:      # 输出信息
                print('{}:{}'.format(word, 1))  # 用：号隔开
    reducer.py  
        
        import sys
        curr_word = None
        curr_count = 0
        
        for line in sys.stdin:
            word, count = line.split(':')   # 因为mapper中用：隔开，这里用：分割
            count = int(count)              # 获取数量是字符串，需要转换成int
            if word == curr_word:           # 统计个数
                curr_count += count
            else:
                if curr_word:
                    print('{}\t{}'.format(curr_word, curr_count))
                curr_word = word
                curr_count = count
        
        if curr_word == word:
            print('{}\t{}'.format(curr_word, curr_count))

    同一个目录下，创建123.txt文件，执行一下命令　　
    
        cat 123.txt | python mapper.py | sort -t 1 | python reducer.py 
        这条命令的意思，将123.txt文件内容输出到屏幕，将结果作为参数，给mapper.py，输出的结果进行排序，间隔符１；将输出的结果再出作为参数给reducer.py
        
````
        
    