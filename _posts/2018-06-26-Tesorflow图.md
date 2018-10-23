---
layout: post
title:  Tensorflow(图)
categories: Tensorflow
description: Tensorflow
keywords: Tensorflow
comments: true
---



### 图
Tensorflow图默认已经注册，一组表示 tf.Operation计算单位的对象和tf.Tensor
表示操作之间流动的数据单元的对象

获取调用默认图对象：
tf.get_default_graph()
op、sess或者tensor 的graph属性

#### 创建新图
```mysql
tf.Graph()


使用新创建的图

	g = tf.Graph() 
	with g.as_default(): 
	        a = tf.constant(1.0) 
	        assert c.graph is g

```

#### 测试代码
```mysql
import tensorflow as tf
import os

# 关闭警告
os.environ['TF_CPP_MIN_LOG_LEVEL']='2'


def test():
    """
    python中加法运算
    :return:
    """
    a = 1
    b = 2
    c = a+b
    print(c)

def test2():
    """
    tensorflow中做加法运算
    在tensorflow中运算，不能直接得到结果
    :return:
    """
    a = tf.constant(value=10)
    b = tf.constant(value=20)
    c = tf.add(a,b)
    print(c)
    # 如果要得出结果，需要开启会话，在会话状态下，计算结果
    # tensorflow这样设计，可达到在不同的计算机上运行，他是一个分布式框架
    with tf.Session() as sess:
        ret = sess.run(c)
        print(ret)


def test3():
    """
    图
    :return:
    """
    a = tf.constant(value=10)
    b = tf.constant(value=20)
    c = tf.add(a, b)
    print(c)

    # 获取默认的图对象
    default_graph = tf.get_default_graph()
    print(default_graph)
    print(a.graph)
    print(b.graph)


    # 也可以创建新的图
    newgraph = tf.Graph()
    print(newgraph)

    with tf.Session() as sess:
        print(sess.graph)


def test4():
    """
    图
    :return:
    """


    # 也可以创建新的图
    newgraph = tf.Graph()
    print(newgraph)

    # 将新创建的图作为默认图对象,同时要将运算的放在默认图下面
    with newgraph.as_default():
        a = tf.constant(value=10)
        b = tf.constant(value=20)
        c = tf.add(a, b)
        print(c)

        print(a.graph)
        print(b.graph)
        print(c.graph)

    # 会话设置图对象，不设置是默认图对象
    with tf.Session(graph=newgraph) as sess:
        print(sess.graph)
        print(sess.run(a))
        print(sess.run(c))

if __name__ == '__main__':
    # test()
    # test2()
    # test3()
    test4()
```

#### 会话

- tf.Session()
运行TensorFlow操作图的类，使用默认注册的图（可以指定运行图）

- 会话资源
会话可能拥有很多资源，如 tf.Variable，tf.QueueBase
和tf.ReaderBase，会话结束后需要进行资源释放

1. sess = tf.Session()     sess.run(...)      sess.close() 
2. 使用上下文管理器
with tf.Session() as sess: 
	sess.run(...)

- config=tf.ConfigProto(log_device_placement=True)
3. 应用命令行，ipython
- 交互式：tf.InteractiveSession()  


#### 会话run()方法
run(fetches, feed_dict=None,graph=None)
	运行ops和计算tensor
嵌套列表，元组，
namedtuple，dict或OrderedDict(重载的运算符也能运行)

feed_dict 允许调用者覆盖图中指定张量的值,提供给
placeholder使用

返回值异常
	RuntimeError：如果它Session处于无效状态（例如已关闭）。
	TypeError：如果fetches或feed_dict键是不合适的类型。
	ValueError：如果fetches或feed_dict键无效或引用 Tensor不存在。

```mysql
import tensorflow as tf

def session_test():
    a = tf.constant(value=10)
    b = tf.constant(value=20)
    c = tf.add(a, b)

    # tf.ConfigProto(log_device_placement=True),加入这个［配置，可以打印运算所自爱的设备信息
    with tf.Session(config=tf.ConfigProto(log_device_placement=True)) as sess:
        print(sess.run(c))
    # 定义占位符，可以在run的时候传入值
    # ph = tf.placeholder(dtype=tf.int64,shape=(2,3))
    # 可以不指定形状，但类型不可缺少
    ph = tf.placeholder(dtype=tf.int64)
    with tf.Session() as sess:
        # run()可以传入多个值，列表或元组，得到的结果也是列表或元组
        print(sess.run([a,b,c]))
        # 不指定形状也可以输出
        print(sess.run(ph,feed_dict={ph:[[1,2,3],[4,5,6]]}))
if __name__ == '__main__':
    session_test()
```
### op
![op](/images/ai/op.png)

### 张量

- 一个类型化的N维度数组（tf.Tensor）
- 有三部分组成：名字，形状，数据类型
```mysql
# 张量的三要素：
# 名称：默认，也可以自己指定
# shape:和numpy的维度相似，这里称为阶
# 类型：和numpy的类型类似，也有自己特殊的类型
```
#### 张量阶
![img](/images/ai/zl_1.png)
#### 张量数据类型
![img](/images/ai/zl_2.png)

```mysql
ef tensor_test():
    """
    张量的学习
    :return:
    """
    # 张量的三要素：
    # 名称：默认，也可以自己指定
    # shape:和numpy的维度相似，这里称为阶
    # 类型：和numpy的类型类似，也有自己特殊的类型
    a = tf.constant(10,name="c1")
    print(a)
    b = tf.constant(20,dtype=tf.float32)
    print(b)

    print(b.dtype)
    a = tf.cast(a,dtype=tf.float32)
    # 两个数据类型不一样不能运算，需要转换
    c = tf.add(a,b)
    print(c.name)
    print(c.shape)
    print("*"*20)
    print(c.op)
if __name__ == '__main__':
    # session_test()
    tensor_test()
```