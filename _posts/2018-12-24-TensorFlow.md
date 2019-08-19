---
layout: post
title: TensorFlow
categories: AI
description: 人工智能
keywords: AI
---



1.安装py 

sudo apt-get install python-pip python-dev

2.安装tf 

```
sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl

之后升级到1.12
pip install --upgrade tensorflow 

安装路径在usr/local/lib/python2.7/dist-packages/tensorflow

```
> apt-get 是ubuntu自带的管理工具，centos默认是yum 

```
查看操作系统版本的linux命令
head -n 1 /etc/issue 
```

```
看到以下信息，表示安装成功

The directory '/home/blockchain/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
The directory '/home/blockchain/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting tensorflow==0.8.0 from https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl
  Downloading https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl (22.2MB)
    100% |████████████████████████████████| 22.2MB 78kB/s 
Collecting numpy>=1.8.2 (from tensorflow==0.8.0)
  Downloading numpy-1.13.1-cp27-cp27mu-manylinux1_x86_64.whl (16.6MB)
    100% |████████████████████████████████| 16.6MB 97kB/s 
Requirement already up-to-date: six>=1.10.0 in /usr/local/lib/python2.7/dist-packages (from tensorflow==0.8.0)
Requirement already up-to-date: protobuf==3.0.0b2 in /usr/local/lib/python2.7/dist-packages (from tensorflow==0.8.0)
Requirement already up-to-date: wheel in /usr/lib/python2.7/dist-packages (from tensorflow==0.8.0)
Collecting setuptools (from protobuf==3.0.0b2->tensorflow==0.8.0)
  Downloading setuptools-36.2.4-py2.py3-none-any.whl (477kB)
    100% |████████████████████████████████| 481kB 961kB/s 
Installing collected packages: numpy, tensorflow, setuptools
  Found existing installation: numpy 1.12.0
    Uninstalling numpy-1.12.0:
      Successfully uninstalled numpy-1.12.0
  Found existing installation: tensorflow 0.8.0
    Uninstalling tensorflow-0.8.0:
      Successfully uninstalled tensorflow-0.8.0
  Found existing installation: setuptools 34.3.1
    Uninstalling setuptools-34.3.1:
      Successfully uninstalled setuptools-34.3.1
Successfully installed numpy-1.13.1 setuptools-36.2.4 tensorflow-0.8.0

```

3. 两个最简单的例子

```
>>> import tensorflow as tf
>>> hello =tf.constant('hello,commando!')
>>> sess=tf.Session()
>>> print sess.run(hello)

>>> a=tf.constant(10)
>>> b=tf.constant(32)
>>> print sess.run(a+b)
42

```


```
>>> import tensorflow as rf
>>> sess=rf.InteractiveSession()
>>> x=rf.Variable([1.0,2.0])
>>> a=rf.constant([3.0,3.0])
>>> x.initializer.run()
>>> sub=rf.sub(x,a)
>>> print sub.eval()
[-2. -1.]
```


4. TensorBoard

下载mnist_with_summaries.py文件
https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/tutorials/mnist

执行 python mnist_with_summaries.py

启动 python tensorboard.py --logdir=/tmp/mnist_logs
>1.12版本 tensorboard --logdir=/tmp/tensorflow/mnist/input_data

访问 http://192.168.50.120:6006/

5. tensorboard log目录应该是event文件所在的目录
```
root@iZ2zeb5n81znirjwr3s29iZ:/tmp/tensorflow/mnist/logs/mnist_with_summaries/train# ls
events.out.tfevents.1545619242.iZ2zeb5n81znirjwr3s29iZ
root@iZ2zeb5n81znirjwr3s29iZ:/tmp/tensorflow/mnist/logs/mnist_with_summaries/train# pwd
/tmp/tensorflow/mnist/logs/mnist_with_summaries/train

```


![image](http://note.youdao.com/yws/public/resource/782c672e0460504523345c9301875789/xmlnote/47D91BEAFB7449118D819F48C3379F3A/1061)