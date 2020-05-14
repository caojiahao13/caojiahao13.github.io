---
layout: default
title: "Jiahao Cao's homepage"
description: useful tools
theme: jekyll-theme-cayman
---

This note is mainly for helping myself remember how to use colab, so it is written in chinese.

[Google Colaboratory](https://colab.research.google.com/notebooks/intro.ipynb)是一个十便捷并且计算自愿种类丰富的平台。

##  入门

Colab 笔记本是由 Colab 托管的 Jupyter 笔记本，也叫做：**Colab笔记本**。

和jupyter notebook类似，它可以运行代码(python,R,shell,c++...)，嵌入文本，html等。

这些笔记本存储在用户的谷歌云盘下，易于分享和合作。

## python和深度学习的相关设置

我自己使用了```!pip list```，看到colab笔记本已经内置了大部分常用的包，如：

* tensorflow               2.2.0     
* numpy                    1.18.4   

但是我发现没有pytorch，下面主进行一些相关配置。


这里主要参考了这篇[文章](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)

> 谷歌colab提供了免费的 Tesla K80 GPU 来使用Keras,tensorflow以及PyTorch等


* 设置GPU：打开一个笔记本，左上角```修改```>```笔记本设置```>```硬件加速器```选择GPU。这时我们已经默认启用GPU了。
* 配置谷歌colab和谷歌drive的连接从而可以读取google drive中的文件：
```
from google.colab import drive
drive.mount('/content/drive/')
```
期间会让你登录google并且完成授权。完成后会显示：
```Enter your authorization code:
··········
Mounted at /content/drive/
```
也就是说你的drive上的内容已经挂在了```/content/drive/```目录下了。
* 更改家目录到drive下的```app```文件夹
```
import os
os.chdir("drive/app")
```
* 安装Keras
```
!pip install -q keras
```
* 安装pytorch
```
pip install torch torchvision
```

#### 抓取一些配置信息

* 查看目前的GPU情况
```
import tensorflow as tf
tf.test.gpu_device_name()
```
如果有返回```'/device:GPU:0'```，则GPU已经启用了。
* 用的什么GPU？
```
from tensorflow.python.client import device_lib
device_lib.list_local_devices()
```
可以看到返回的信息有``` name: Tesla K80```
* RAM信息查询
```
!cat /proc/meminfo
```
我得到了
```
MemTotal:       13333540 kB
MemFree:         2270528 kB
MemAvailable:   11932508 kB
Buffers:           91424 kB
Cached:          9505336 kB
```
* CPU信息查询
```
!cat /proc/cpuinfo
```
我得到了
```
processor	: 0
vendor_id	: GenuineIntel
cpu family	: 6
model		: 63
...
```
#### 一个mnist数据集合的GPU训练：
* 下载[训练代码](https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py)
* 将文件upload到你的drive上
* ```!python3 "/content/drive/My Drive/.../mnist_cnn.py"```运行代码
我得到的运行结果是：

```
Using TensorFlow backend.
2020-05-14 16:28:34.107188: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcudart.so.10.1
Downloading data from https://s3.amazonaws.com/img-datasets/mnist.npz
11493376/11490434 [==============================] - 2s 0us/step
x_train shape: (60000, 28, 28, 1)
60000 train samples
10000 test samples

...

Epoch 12/12
60000/60000 [==============================] - 8s 136us/step - loss: 0.0284 - accuracy: 0.9915 - val_loss: 0.0299 - val_accuracy: 0.9914
Test loss: 0.0299225880630853
Test accuracy: 0.9914000034332275
```
可以看到在GPU训练很快。在我的笔记本电脑上，运行了半分钟还没有一个epoch的三分之一。
#### 用链接下载csv文件斌给加入drive
```
!wget https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/datasets/Titanic.csv -P "/content/drive/My Drive/app"
```
或者
```
!wget https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/datasets/Titanic.csv -P drive/app
```
读取前五行：
```
import pandas as pd
titanic = pd.read_csv(“/content/drive/My Drive/app/Titanic.csv”)
titanic.head(5)
```
