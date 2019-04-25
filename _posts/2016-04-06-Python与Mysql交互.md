---
layout: post
title:  Python 连接Mysql
categories: Python
description: python
keywords: Python
comments: true
---


### python3 连接mysql:



1、导入 pymysql 包： from pymysql import \*

2、进行连接：

conn = connect\(host='localhost',port=3306,database='jing\_dong',user='root',password='mysql',charset='utf8'\) \#这是创建Connection连接，连接数据库必须要有的， host：就是ip地址，port:端口 database：数据库名字

3、获取数据库对象： cs = conn.cursor\(\)

4、这一步就可以操作数据库的增删改查：

count = cs.execute\('insert into students values\(0,“周杰”,34,176.00,2,5,0\)'\) \# 这句意思就是今后sql语句都在execute\(\)函数括号里面写，必须用单引号或双引号引起来。

db.rollback\(\) 回滚

cur.fetchone\(\) 获取下一行数据

cur.fetchall\(\) 获取结果集的所有行，一行构成一个元组



5、对数据库增删改完后，需要进行提交：conn.commit\(\)；查不需要

6、提交完后，需要关闭数据库 关闭数据库之前，先关闭对象：cs.close\(\)

7、关闭完对象后，关闭数据库：conn.close\(\)



例子：

```py
from pymysql import connect
import multiprocessing
import threading
import gevent
from gevent import monkey
monkey.patch_all()
import time

class Sql_class:
    def __init__(self):
    self.db = connect(host = "192.168.113.146",database = "python3",port = 3306,user = "root",password = "yuan121423",charset = "utf8")
        self.cur = self.db.cursor()
        
        def __del__(self):
        self.cur.close()
        self.db.close()
    
    def update(self):
    
        sql = """insert into goods_cates(name) values('小学生')"""
        # sql = """delete from goods_cates WHERE name = '小学生'"""
        # sql = """update goods_cates set name = 'hahaha' WHERE name = '小学生'"""
        try:
            data = self.cur.execute(sql)
            # sleep(1)
        except Exception as e:
            print("更新失败")
            self.db.rollback()
        else:
            self.db.commit()
            print("更新成功")

    def select(self):
    
        # sql = """select g.name as a,c.name as e,b.name as t,abc.max_price from goods as g
        # inner join goods_cates as c on g.cate_id=c.id inner join goods_brands as b on
        # g.brand_id=b.id inner join ( select cc.name as ss,max(gg.price) as max_price from goods as gg
        # inner join goods_cates as cc on gg.cate_id = cc.id group by cc.name) as abc on abc.ss = c.name and abc.max_price = g.price;"""
        sql = """select * from students"""
        data = self.cur.execute(sql)
        for i in range(data):
            name = self.cur.fetchone()
            print(name[0],name[1])
            
        # self.cur.close()
        # self.db.close()

    def main():
        #port=3306,database='python3',user='root',password='yuan121423',charset='utf8'
        # db = connect(host = "192.168.113.146",database = "python3",port = 3306,user = "root",password = "yuan121423",charset = "utf8")
        # cur =db.cursor()
        start = time.time()
        dx = Sql_class()
        # g1 = gevent.spawn(dx.update())
        # g2 = gevent.spawn(dx.select())
        # gevent.joinall([g1,g2])
        
        # thd1 = threading.Thread(target=dx.select())
        # thd2 = threading.Thread(target=dx.update())
        # thd1.start()
        # thd2.start()
        # pro1 = multiprocessing.Process(target=dx.update())
        # pro2 = multiprocessing.Process(target=dx.select())
        # pro2.start()
        # pro1.start()
        # update(cur,db)
        # select(cur,db)
        dx.select()
        dx.update()
        stop = time.time()
        print(stop-start)
if __name__ == '__main__':
    main()
```

### python2 连接mysql

> import MySQLdb  python2使用的包和python3不一样
> pip install MySQLdb-python 容易失败

centos 安装MySQLdb方法:  

```python
sudo yum install MySQL-python
```
ubuntu 安装MySQLdb方法:  

```python
sudo apt-get install libmysqlclient-dev libmysqld-dev python-dev python-setuptools

pip install MySQL-python
如果报错可能是pip版本问题，更新pip版本
```
