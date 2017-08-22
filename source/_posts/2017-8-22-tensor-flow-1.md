---
title: TensorFlow学习笔记(1)
date: 2017-08-22 
tags: 技术
categories: AI
---
# TensorFlow(来源于百度百科)
1. TensorFlow是谷歌基于DistBelief进行研发的第二代人工智能学习系统，其命名来源于本身的运行原理。Tensor（张量）意味着N维数组，Flow（流）意味着基于数据流图的计算，TensorFlow为张量从流图的一端流动到另一端计算过程。TensorFlow是将复杂的数据结构传输至人工智能神经网中进行分析和处理过程的系统。
2. TensorFlow可被用于语音识别或图像识别等多项机器深度学习领域，对2011年开发的深度学习基础架构DistBelief进行了各方面的改进，它可在小到一部智能手机、大到数千台数据中心服务器的各种设备上运行。TensorFlow将完全开源，任何人都可以用。
3. 我个人理解 TensorFlow 更像一个集成了AI开发的平台，协助把大规模的数据运算分散到大规模的设备中去，这其中融入了Google对于AI的一个理解，在这个框架内引入了第三方的库，让AI开发有一个统一的标准

# Windows安装TensorFlow
TensorFlow 是目前来说，对于个人开发者来说，是一个唯一可靠的平台，鉴于目前各方面文档都不全，普通的小白开发者入门极其困难；从最开始的安装解决就有很多坑，大部分人在第一步就掉坑里爬不上来；不管学习什么都要持之以恒，只要确定了这门技术有意义，就要有一门心思走到底的决心；下面介绍一下Window上面安装TensorFlow的步骤，以及遇到的问题

参考网址[点击查看](http://blog.csdn.net/u010099080/article/details/53418159)

该教程中指出了大体的步骤，但是在实际操作中可能还会有其它的问题！

1. 安装文件准备（涉及到的资源会上传 百度云盘）
    * TensorFlow 1.3 whl文件（pip安装文件）
    * Python 3.6 和 pip
    * CUDA 8.0 和 cuDNN 6.0
    * 其它的第三方库
    * 链接：http://pan.baidu.com/s/1jHJN3ts 密码：yw1z
    
2. 安装Python和Pip
   * Python是一种跨平台的脚本开发语言
   * Pip 基于Python的第三方库管理平台
   * 直接下载资源里面的Python文件，Python3.6里面已经集成了Pip，点击安装即可，安装过程中勾选 “Add To Path” ，会自动加入到路径中去
   * 安装完成后 执行 python --version 和 pip --version 查看是否成功
    
3. 安装TensorFlow
 
**在线安装命令（网络状况比较好的话）**

```
# GPU版本
pip3 install --upgrade tensorflow-gpu

# CPU版本
pip3 install --upgrade tensorflow
```

**离线安装** 
    
因为国内墙的原因，正常情况下都是无法安装成功的，在安装过程中会不断的发现某一个第三方库下载超时，我把这里全部的稍微大一点的包 都已经下载好，直接执行命令进行
    
```
pip install numpy-1.12.1-cp36-none-win_amd64.whl
pip install scipy-0.19.0-cp36-cp36m-win_amd64.whl
pip install tensorflow_tensorboard-0.1.4-py3-none-any.whl
pip install tensorflow-1.3.0-cp36-cp36m-win_amd64.whl

//把上面四个命令都执行完毕后，再执行下面这个命令，基本上都能一次性成功
pip install tensorflow_gpu-1.3.0-cp36-cp36m-win_amd64.whl 

```
    
4. 安装Cuba 和 cuDnn
    * Cuba 直接打开可执行文件，安装即可
    * cuDnn 解压后，把bin加入系统的Path中
    * 注意cuDnn下载需要注册账号，并且注意选择正确的版本（也可以直接使用资源里面的）

5. 安装完成后出现的错误 
  
**numpy 库无法使用**
一般会伴随着“ImportError: DLL load failed: 找不到指定的模块。”
如果是在线安装，或者使用pypi提供的库，好像都是有问题的，解决的方法就是使用我提供的numpy库，采用离线的方式安装 numpy

**ImportError: No module named '_pywrap_tensorflow_internal'问题**
一般都是cuDnn的库版本错误，或者设置Path错误，这里注意，设置过环境变量后，需要退出cmd，重新进入才会生效

**某一个库下载超时**

把下载失败的文件名复制下来，在这个网址里面搜索
https://pypi.python.org/pypi/

6. 执行结果

```
import tensorflow as tf
a = tf.random_normal((100, 100))
b = tf.random_normal((100, 500))
c = tf.matmul(a, b)
//产生a，b两个矩阵，两个矩阵相乘，在GPU中并行处理
sess = tf.InteractiveSession()
sess.run(c)
```

![image](http://lovemingnuo.oss-cn-beijing.aliyuncs.com/blog/tensor_flow.png)



   