---
layout: post
title:  Tensorflow(形状)
categories: Tensorflow
description: Tensorflow
keywords: Tensorflow
comments: true
---

Tensorflowx形状，分为动态形状和静态形状

形状：
动态形状和静态形状



```mysql
import tensorflow as tf

def shape_test():
    """
    改变形状
    :return:
    """
    a = tf.constant(value=[[1,2,3],[4,5,6]],shape=(2,3))
    print(a)
    # 设置不固定的形状，用None表示
    # b = tf.constant(shape=(None,3))
    # 指定形状
    ph1 = tf.placeholder(dtype=tf.int32,shape=(2,3))
    ph2 = tf.placeholder(dtype=tf.int32,shape=(None,3))
    # print(ph1)
    # print(ph2)

    # 改变形状
    # Tensor.set_shape用于没有固定形状的tensor做形状改变
    tf.Tensor.set_shape(ph2,(1,3))
    # 一旦形状固定后，就不能再调用set_shape方法了
    # tf.Tensor.set_shape(ph2, (2, 3))
    # 对已固定形状的tensor,可以调用reshape来改变形状
    # reshape:可以改变已经固定形状的tensor,但是会重新创建一个tensor对象,有返回值需要接收
    ph1 = tf.reshape(ph1,(3,2))
    print(ph1)

    ph3 = tf.placeholder(dtype=tf.int32, shape=(None, None,3))
    tf.Tensor.set_shape(ph3,(None,1,3))
    print(ph3)


    with tf.Session() as sess:
        ret= sess.run(ph2,feed_dict={ph2:[[1,2,3]]})
        # print(ret)
        # print(ph2)


if __name__ == '__main__':
    shape_test()
```

