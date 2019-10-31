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

### cuda 10.0 下载地址
<https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal>

![](/images/tensorflow/tf_2.jpg)

![](/images/tensorflow/tf_3.jpg)


### 下载需要nvidia 账户  
![](/images/tensorflow/tf_4.jpg)

### 安装cuda 10.0  ,

```angular2
sudo sh cuda_10.0.130_410.48_linux.run
```

### 需要安装 NVIDIA 410.93, CUDA 10.0, cudnn 7.4

系统：deepin
显卡：Quadro M2000M

#### deepin自带的显卡管理器，切换后的版本是：390 不满足需求,需要自己去官网下载；不能下载最新版本，下载历史版本

**[NVIDIA历史版本下载地址](https://www.nvidia.cn/Download/Find.aspx?lang=cn)**  
**[CUDA历史版本下载地址](https://developer.nvidia.com/cuda-toolkit-archive)**   
**[cudnn历史版本下载地址](https://developer.nvidia.com/rdp/cudnn-archive)** 
### 下载好软件后,进行安装,方法基本和网上一样，要注意细节，不然进不了图形页面，就需要折腾一番

#### 1. 禁用nouveau   
```angular2
# 这个文件名字不一定就是这样，但是肯定是blacklist开头的文件
vi /etc/modprobe.d/blacklist-bcm43.conf
# 在后面加入下面两行
blacklist nouveau
options nouveau modeset=0
```
保存后立即生效：    
```angular2
sudo update-initramfs -u 
``` 

#### 2. 卸载之前的NVIDIA 
```angular2
# 要是没有安装，也不会有问题，一定要保证卸载完成，不要报错;
sudo apt-get --purge remove nvidia-*    
# 不要使用 sudo apt-get autoremove
```

#### 3. 重启电脑，哈哈，这好多人都着了道；

```angular2
#说说为什么要重启,重启是为了释放nouveau资源占用问题
# 重启后执行
lsmod |grep -i nouveau  
``` 
如果进不了图形界面，看下面步骤

> 下来就是网上说的要重启电脑，我重启后就进不了图形界面，在这坑大了，看网上有的人都能进去；
> 重点：进不去就会卡在logo或黑窗口界面，如果到了这一步，别乱折腾，

在安装NVIDIA的时候需要关闭 Secure Boot 值改成Disabled。每个厂家进去bios都不一样，需要自己查，我的是F1。    

如果进不了图形界面，我们就进入无界面窗口，用过服务器的人都知道，服务器基本都是无界面. 
继续开机后,显示 deepin 15.XX 直接按键盘：e  

> 在linux   /boot/vm***   在这一行最后面：systemd.unit=multi-user.target

按键盘：Ctrl+x 等待进入无界面窗口，入下面的动态图

![](/images/tensorflow/deepin.gif)


