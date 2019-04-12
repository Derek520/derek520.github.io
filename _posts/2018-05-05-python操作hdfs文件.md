---
layout: post
title:  Python操作hdfs
categories: 
    - 大数据
    - 读取hdfs文件
description: 大数据
keywords: 大数据,hdfs
comments: true
---

> 摘要：python读取hdfs数据方法

1. 安装hdfs
```python
pip install hdfs
```
2. 连接hdfs
```python
import hdfs
client = hdfs.Client("http://127.0.0.1:50070")
其他参数说明：

classhdfs.client.Client(url,root=None,proxy=None,timeout=None,session=None)
url：ip：端口
root：制定的hdfs根目录
proxy：制定登陆的用户身份
timeout：设置的超时时间
seesion：requests.Session instance, used to emit all requests
```

3. dir:查看支持的方法  
```python
print dir(client)
#输出结果 
['__class__', '__delattr__', '__dict__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__module__', '__new__', '__reduce__', '__reduce_ex__', '__registry__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_append', '_create', '_delete', '_get_acl_status', '_get_content_summary', '_get_file_checksum', '_get_file_status', '_get_home_directory', '_get_trash_root', '_list_status', '_lock', '_mkdirs', '_modify_acl_entries', '_open', '_proxy', '_rename', '_request', '_session', '_set_acl', '_set_owner', '_set_permission', '_set_replication', '_set_times', '_timeout', '_urls', 'acl_status', 'checksum', 'content', 'delete', 'download', 'from_options', 'list', 'makedirs', 'parts', 'read', 'rename', 'resolve', 'root', 'set_acl', 'set_owner', 'set_permission', 'set_replication', 'set_times', 'status', 'upload', 'url', 'urls', 'walk', 'write']
```
4. status:获取路径的具体信息  
```python
print client.status("/")
# 输出结果
{u'group': u'supergroup', u'permission': u'755', u'blockSize': 0, u'accessTime': 0, u'pathSuffix': u'', u'modificationTime': 1538207487671, u'replication': 0, u'length': 0, u'childrenNum': 4, u'owner': u'hdfs', u'storagePolicy': 0, u'type': u'DIRECTORY', u'fileId': 16385}

其他参数：status(hdfs_path,strict=True)
hdfs_path：就是hdfs路径
strict：设置为True时，如果hdfs_path路径不存在就会抛出异常，如果设置为False，如果路径为不存在，则返回None
```

5. list:获取指定路径的子目录信息  
```python
print client.list("/")
```
6. makedirs:创建目录
```python
client.makedirs("/test")
```
7.rename:重命名
```python
client.rename("/test","/new_name")
```
8. delete:删除
```python
client.delete("/new_name")
```
9. upload:上传数据
```python
client.upload("/test","/opt/bigdata/hadoop/NOTICE.txt")
其他参数：upload(hdfs_path,local_path,overwrite=False,n_threads=1,temp_dir=None,
chunk_size=65536,progress=None,cleanup=True,**kwargs)

overwrite：是否是覆盖性上传文件

n_threads：启动的线程数目

temp_dir：当overwrite=true时，远程文件一旦存在，则会在上传完之后进行交换

chunk_size：文件上传的大小区间

progress：回调函数来跟踪进度，为每一chunk_size字节。它将传递两个参数，文件上传的路径和传输的字节数。一旦完成，-1将作为第二个参数

cleanup：如果在上传任何文件时发生错误，则删除该文件
```
10. download:下载
```python
client.download("/test/test.txt","/home")
其他参数：download(hdfs_path,local_path,overwrite=False,n_threads=1,temp_dir=None,**kwargs)
```
11. read:读取文件
```python
with client.read("/test/test.txt") as reader:
     print reader.read()

其他参数：read(*args,**kwds)
hdfs_path：hdfs路径

offset：设置开始的字节位置

length：读取的长度（字节为单位）

buffer_size：用于传输数据的字节的缓冲区的大小。默认值设置在HDFS配置。

encoding：制定编码

chunk_size：如果设置为正数，上下文管理器将返回一个发生器产生的每一chunk_size字节而不是一个类似文件的对象

delimiter：如果设置，上下文管理器将返回一个发生器产生每次遇到分隔符。此参数要求指定的编码。

progress：回调函数来跟踪进度，为每一chunk_size字节（不可用，如果块大小不是指定）。它将传递两个参数，文件上传的路径和传输的字节数。称为一次与- 1作为第二个参数。

```

