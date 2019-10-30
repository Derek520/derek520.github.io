---
layout: post
title:  Tensorflow安装
categories: Tensorflow
description: Tensorflow
keywords: Tensorflow
comments: true
---

> 摘要：Tensorflow安装学习


1. Tensorflow安装：anaconda3 python3.6;

windows安装以管理员权限打开命令窗口;linux/MAX直接执行下面命令   

```mysql
pip install --upgrade --ignore-installed tensorflow
```

2. 如果没有安装anaconda3，系统是python3.5或者2.7　安装如下：    

```mysql
Linux/ubuntu:
python2.7: pip install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.1-cp27-none-linux_x86_64.whl 
python3.5: pip3 install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.1-cp35-cp35m-linux_x86_64.whl 

Maxos:
python2: pip install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.1-py2-none-any.whl
python3: pip3 install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.1-py3-none-any.whl

```
### 清华镜像站提供各版本下载安装
#### Contos7
<https://mirrors.tuna.tsinghua.edu.cn/help/tensorflow/>

### anaconda3 +python3.7 +Tensorflow-gpu安装

1. 检查是否安装
```python
lspci | grep -i nvidia
```

2. 检查N卡驱动
<https://www.nvidia.com/Download/index.aspx>

3. 查看N卡是否支持GPU
<https://developer.nvidia.com/cuda-gpus>

4. 安装nvidia-smi,查看GPU信息
```python
sudo apt-get install nvidia-smi
```

5. Tensorflow-gpu,cuda,cudnn版本对应关系图
![](/images/tensorflow/cuda.png)
![linux](/images/tensorflow/gpu_linux.png)
![windows](/images/tensorflow/gpu_windows.png)

官方连接
<https://www.tensorflow.org/install/install_sources#tested_source_configurations>

5. 安装cuda,下载有点慢
```python
sudo apt-get install nvidia-cuda-dev nvidia-cuda-toolkit nvidia-nsight nvidia-visual-profiler
```

7. 安装cudnn,下载对应的版本,我的系统是deepin 选择linux版，具体根据自己的系统选择，例如：cundd7.1.3 for linux
<https://developer.nvidia.com/search/site/cudnn-7.0-linux-x64-v4.0>
<https://developer.nvidia.com/rdp/cudnn-archive>

![cudnn](/images/tensorflow/cudnn.png)

8. 下载完毕cudnn,解压cudnn包,把解压得到的文件夹cuda复制到/usr/local/目录下:
```python
tar -zxvf cudnn-9.1-linux-x64-v7.1.tgz
sudo mv cuda/ /usr/local/
```
9. 设置环境变量
```python
vi ~/.bashrc 
#cuda
export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
```

10. 在anaconda3+python3.6.5环境下,安装:tensorflow-gpu==1.8
```python
pip install tensorflow-gpu==1.8
```

> 目前,官网tensorflow支持cuda9,不支持9.0以上的,我的是9.1版本,需要下载被编译过的支持9.1的版本tensorflow-gpu
<https://github.com/mind/wheels/releases?>
我下载了tensorflow-gpu==1.8


11. 下载完编译过的tensorflow-gpu==1.8,进行安装
```python
pip install /home/derek/Desktop/tensorflow-1.8.0-cp36-cp36m-linux_x86_64.whl
```

12. 运行，测试代码：
```python
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```
![](/images/tensorflow/tenrort_erre.png)  

运行没问题,报了告警,解决方法是： 

    出错位置h5py\_init_.py:26 
    
解决办法  

    对h5py进行更新升级
    pip install h5py==2.8.0
    
    
13. 最终运行结果:  
![](/images/tensorflow/tensort_suc.png)


### 最新linux对应版本  

![](/images/tensorflow/tf.png)
