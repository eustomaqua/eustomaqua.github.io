---
title: NVIDIA TensorRT Installation
date: 2020-04-03 08:21:30
updated: 2020-04-03 08:21:30
categories:
  - Records
tags: 
  - Configure
  - Linux
  - NVIDIA TensorRT
---

<!--
Created: 2020-04-03 02:31:04
-->


# Installation
\# Ubuntu 18.04 or 16.04  
- Anaconda3-5.2.0-Linux-x86_64.sh
- CUDA 10.0.130
- cuDNN v7.6.4 for CUDA 10.0

## Anaconda

### 卸载

[Ubuntu 卸载 anaconda](https://blog.csdn.net/lqp888888/article/details/79807885)   
[linux上anaconda的卸载](https://blog.csdn.net/qq_22474567/article/details/54984257)  
[Ubuntu上 anaconda的卸载](https://blog.csdn.net/lixintong1992/article/details/67654753)  

```bash
$ # 1. 进入安装 Anaconda 目录，用下面这个命令 即可删除文件夹。
$ cd ~/VirtualEnv
$ rm -r anaconda3

$ # 2. 更新路径。输入命令
$ gedit ~/.bashrc
$ ## 注释掉或者删除“ export PATH=/home/usr/anaconda3/bin:$PATH ”，保存文档。

$ # 3. 可使之立即生效；也可关闭当前终端，新开终端即可生效.
$ source ~/.bashrc
```

### 安装

Anaconda3-5.2.0-Linux-x86_64.sh [\[mirrors.thu\]](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)  

```bash
$ cd ~
$ mv software Software
$ cd ~/Software
$ bash ./Anaconda3-5.2.0-Linux-x86_64.sh

In order to continue the installation process, please review the license agreement.
Please, press ENTER to continue
>>>


Do you accept the license terms? [yes|no]
[no] >>>
Please answer 'yes' or 'no':'
>>> yes


Anaconda3 will now be installed into this location:
/home/eustomaqua/anaconda3
  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below
[/home/eustomaqua/anaconda3] >>> /home/eustomaqua/VirtualEnv/anaconda3

PREFIX=/home/eustomaqua/VirtualEnv/anaconda3
installing: python-3.6.5-hc3d631a_2 ...
Python 3.6.5 :: Anaconda, Inc.
installing: blas-1.0-mkl ...


installation finished.
WARNING:
    You currently have a PYTHONPATH environment variable set. This may cause
    unexpected behavior when running the Python interpreter in Anaconda3.
    For best results, please verify that your PYTHONPATH only points to
    directories of packages that are compatible with the Python interpreter
    in Anaconda3: /home/eustomaqua/VirtualEnv/anaconda3
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/eustomaqua/.bashrc ? [yes|no]
[no] >>> yes

Appending source /home/eustomaqua/VirtualEnv/anaconda3/bin/activate to /home/eustomaqua/.bashrc
A backup will be made to: /home/eustomaqua/.bashrc-anaconda3.bak
For this change to become active, you have to open a new terminal.
Thank you for installing Anaconda3!


===========================================================================

Anaconda is partnered with Microsoft! Microsoft VSCode is a streamlined
code editor with support for development operations like debugging, task
running and version control.
To install Visual Studio Code, you will need:
  - Administrator Privileges
  - Internet connectivity
Visual Studio Code License: https://code.visualstudio.com/license
Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]
>>> no
$
```

### 检查

```bash
~/software$ python
Python 2.7.12 (default, Nov 12 2018, 14:36:49)
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
[1]+  Stopped(SIGTSTP)        python
~/software$

~/software$ source ~/.bashrc
~/software$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
[2]+  Stopped(SIGTSTP)        python
~/software$
~/software$ pip list
```

## 显卡驱动

```bash
$ nvidia-smi
```

## CUDA

### 卸载

[Win10中CUDA、cuDNN的安装与卸载](https://blog.csdn.net/XunCiy/article/details/89070315)  
[Ubuntu安装和卸载CUDA和CUDNN](https://blog.csdn.net/qq_33200967/article/details/80689543)  

```bash
$ # 先卸载原来的 cuda, cudnn
$ cd ~/VirtualEnv
$ ./cuda90/bin/uninstall_cuda_9.0.pl
$ rm -r cuda90

$ rm -r cuda  ## cudnn
$ rm -r cudasamples
```

> 为什么一开始我就要卸载CUDA呢，这是因为笔者是换了显卡RTX2070，原本就安装了CUDA 8.0 和 CUDNN 7.0.5不能够正常使用，笔者需要安装CUDA 10.0 和 CUDNN 7.4.2，所以要先卸载原来的CUDA。注意以下的命令都是在root用户下操作的。  
> 卸载CUDA很简单，一条命令就可以了，主要执行的是CUDA自带的卸载脚本，读者要根据自己的cuda版本找到卸载脚本：
> ``sudo /usr/local/cuda-8.0/bin/uninstall_cuda_8.0.pl``
> 卸载之后，还有一些残留的文件夹，之前安装的是CUDA 8.0。可以一并删除：
> ``sudo rm -rf /usr/local/cuda-8.0/``
> 这样就算卸载完了CUDA。

### 安装

```bash
~$ cd Software
~/Software$ ls
Anaconda3-5.2.0-Linux-x86_64.sh  cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda_10.0.130_410.48_linux.run   Python-3.6.1.tgz
~/Software$ chmod +x cuda_10.0.130_410.48_linux.run
~/Software$ ls
Anaconda3-5.2.0-Linux-x86_64.sh  cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda_10.0.130_410.48_linux.run   Python-3.6.1.tgz
~/Software$ ./cuda_10.0.130_410.48_linux.run
Logging to /tmp/cuda_install_25104.log
Using more to view the EULA.
End User License Agreement
--------------------------


  20. Licensee's use of linmath.h header for CPU functions for
    GL vector/matrix operations from lunarG is subject to the
    Apache License Version 2.0.
-----------------
Do you accept the previously read EULA?
accept/decline/quit: Do you accept the previously read EULA?
accept/decline/quit: accept

Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 410.48?
(y)es/(n)o/(q)uit: no

Install the CUDA 10.0 Toolkit?
(y)es/(n)o/(q)uit: yes

Enter Toolkit Location
 [ default is /usr/local/cuda-10.0 ]: /home/eustomaqua/Software/cuda-10.0

Do you want to install a symbolic link at /usr/local/cuda?
(y)es/(n)o/(q)uit: no

Install the CUDA 10.0 Samples?
(y)es/(n)o/(q)uit: yes

Enter CUDA Samples Location
 [ default is /home/eustomaqua ]: /home/eustomaqua/Software/cuda-samples


$
```

### 配置

```bash
~/Software$ vim ~/.bashrc
~/Software$ # Esc + ':wq'
~/Software$ source ~/.bashrc
```

修改 `~/.bashrc` 文件
```bash
## cuda 9.0: 5-May-2019 central time
# export PATH=$HOME/VirtualEnv/cuda90/bin:$PATH
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/VirtualEnv/cuda90/lib64/
# export CPATH=$HOME/VirtualEnv/cuda90/include:$CPATH
# export DYLD_LIBRARY_PATH=$HOME/VirtualEnv/cuda90/lib:$DYLD_LIBRARY_PATH
## cuda 10.0: 3-Dec-2019 beijing time
# export PATH=/usr/local/cuda/bin:$PATH
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64/
# export CPATH=/usr/local/cuda/include:$CPATH
# export DYLD_LIBRARY_PATH=/usr/local/cuda/lib:$DYLD_LIBRARY_PATH
# alias python='/home/eustomaqua/VirtualEnv/py36env/bin/python3'
export PYTHONPATH=/home/eustomaqua/VirtualEnv/py36env/bin/python3
export PYTHONPATH="${PYTHONPATH}:/home/eustomaqua/GitHubLab/ml-fairness-gym"


# added by Anaconda3 installer
export PATH="/home/eustomaqua/VirtualEnv/anaconda3/bin:$PATH"
# self added for Nvidia
export PATH=$HOME/Software/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/Software/cuda-10.0/lib64/
```

### 检查

```bash
~/Software$ nvidia-smi

~/Software$ cat /usr/local/cuda/version.txt
CUDA Version 10.2.89
~/Software$ cat cuda-10.0/version.txt
CUDA Version 10.0.130
~/Software$

~/Software$ ls /usr/local/cuda/lib64 | grep cudnn
~/Software$ ls cuda-10.0/lib64 | grep cudnn
~/Software$ # 检查表示尚未安装 cuDNN
```

## CUDNN

### 安装

```bash
~/Software$ ls
Anaconda3-5.2.0-Linux-x86_64.sh  cuda-samples
cuda-10.0                        cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda_10.0.130_410.48_linux.run   Python-3.6.1.tgz
~/Software$ cp cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8 cudnn-10.0-linux-x64-v7.6.4.38.tgz
~/Software$ tar -xvf cudnn-10.0-linux-x64-v7.6.4.38.tgz
cuda/include/cudnn.h
cuda/NVIDIA_SLA_cuDNN_Support.txt
cuda/lib64/libcudnn.so
cuda/lib64/libcudnn.so.7
cuda/lib64/libcudnn.so.7.6.4
cuda/lib64/libcudnn_static.a
~/Software$

~/Software$ ls
Anaconda3-5.2.0-Linux-x86_64.sh  cuda-samples
cuda                             cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda-10.0                        cudnn-10.0-linux-x64-v7.6.4.38.tgz
cuda_10.0.130_410.48_linux.run   Python-3.6.1.tgz
~/Software$ rm cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
~/Software$ cd cuda
:~/Software/cuda$ ls
include  lib64  NVIDIA_SLA_cuDNN_Support.txt
~/Software/cuda$ cd ..

~/Software$ mv cuda/include/cudnn.h ~/Software/cuda-10.0/include/
~/Software$ mv cuda/lib64/libcudnn* ~/Software/cuda-10.0/lib64
~/Software$ chmod a+r ~/Software/cuda-10.0/include/cudnn.h ~/Software/cuda-10.0/lib64/libcudnn*
~/Software$
~/Software$ rm -r cuda
rm: remove write-protected regular file 'cuda/NVIDIA_SLA_cuDNN_Support.txt'? y
~/Software$
```

### 检查

```bash
~/Software$ cat ~/Software/cuda-10.0/version.txt
CUDA Version 10.0.130
~/Software$ cat ~/Software/cuda-10.0/include/cudnn.h | grep CUDNN_MAJOR -A5
#define CUDNN_MAJOR 7
#define CUDNN_MINOR 6
#define CUDNN_PATCHLEVEL 4

#define CUDNN_VERSION (CUDNN_MAJOR * 1000 + CUDNN_MINOR * 100 + CUDNN_PATCHLEVEL)

#include "driver_types.h"
#include <cuda_runtime.h>
#include <stdint.h>

~/Software$ ls ~/Software/cuda-10.0/lib64 | grep cudnn
libcudnn.so
libcudnn.so.7
libcudnn.so.7.6.4
libcudnn_static.a
~/Software$
```

# Python related

## virtualenv

安装
```bash
$ pip install virtualenv
$ pip install virtualenvwrapper
```

创建新环境
```bash
$ virtualenv [新环境名] --python=/usr/bin/python3
```
e.g.,
> cd ~
> mkdir VirtualEnv
> virtualenv py27env --python=/usr/bin/python2
> virtualenv py35env --python=/usr/bin/python3

虚拟环境的进入和退出
```bash
$ cd ~/VirtualEnv
$ source py35env/bin/activate
$ deactivate
```

删除环境
```bash
$ # 直接删除虚拟环境 (venv) 所在的文件夹即可
$ rm -r py27env
```

[python 虚拟环境 virtualenv/virtualenvwrapper 设置](https://www.jianshu.com/p/44ab75fbaef2)  
[虚拟环境virtualenv简单操作](https://www.jianshu.com/p/0d3c91f13d68)  
[Python的虚拟环境virtualenv sina](http://blog.sina.com.cn/s/blog_4ddef8f80101eu0w.html)  

## conda env

[Anaconda创建环境、删除环境、激活环境、退出环境](https://blog.csdn.net/H_O_W_E/article/details/77370456)

```bash
~/Software$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
[3]+  Stopped(SIGTSTP)        python
~/Software$ conda env list
# conda environments:
#
base                  *  /home/eustomaqua/VirtualEnv/anaconda3

~/Software$ source activate base
(base) ~/Software$ source deactivate
~/Software$

~/Software$ conda create -n py36env python=3.6
~/Software$ conda remove -n py36env --all
~/Software$ conda activate adanet
~/Software$ conda deactivate
```

## Packages

# TensorRT

官方文档  
[Deep Learning SDK Documentation](https://docs.nvidia.com/deeplearning/sdk/tensorrt-archived/index.html#trt_7)  
[NVIDIA TensorRT](https://developer.nvidia.com/tensorrt)  
[TensorRT Installation Guide - NVIDIA Developer Documentation](https://docs.nvidia.com/deeplearning/sdk/tensorrt-install-guide/index.html)  

## First Attempt: Failed

[深度学习 TensorRT安装](https://zhuanlan.zhihu.com/p/64053177)  
[TensorRT安装及使用教程](https://blog.csdn.net/zong596568821xp/article/details/86077553)  
[Ubuntu16.04 安装 TensorRT](https://blog.csdn.net/wgshun616/article/details/81019601)  

### 下载

在 Nvidia 官网注册，填写调查问卷之后可下载 TensorRT  
[NVIDIA TensorRT](https://developer.nvidia.com/tensorrt)  Click `Download Now`  
下载前先检查下自己的开发环境 —— 系统和 CUDA 版本

- ```bash
  ~$ cat /etc/issue
  Ubuntu 18.04.3 LTS \n \l

  ~$ cat /usr/local/cuda/version.txt
  cat: /usr/local/cuda/version.txt: No such file or directory
  ~$ cat ~/Software/cuda-10.0/version.txt
  CUDA Version 10.0.130
  ~$
  ```
- ```bash
  ~/Software$ cat /etc/issue
  Ubuntu 16.04.6 LTS \n \l

  ~/Software$ cat /usr/local/cuda/version.txt
  CUDA Version 10.2.89
  ~/Software$ cat ~/Software/cuda-10.0/version.txt
  CUDA Version 10.0.130
  ~/Software$
  ```

[NVIDIA TensorRT 7.x Download](https://developer.nvidia.com/nvidia-tensorrt-7x-download)  
选择最新版 `TensorRT 7.0 for Linux`
- Debian and RPM Install Packages for Linux x86
  - [TensorRT 7.0.0.11 for Ubuntu 1804 and CUDA 10.0 DEB local repo packages](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/7.0/7.0.0.11/local_repo/nv-tensorrt-repo-ubuntu1804-cuda10.0-trt7.0.0.11-ga-20191216_1-1_amd64.deb)
  - [TensorRT 7.0.0.11 for Ubuntu 1604 and CUDA 10.0 DEB local repo packages](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/7.0/7.0.0.11/local_repo/nv-tensorrt-repo-ubuntu1604-cuda10.0-trt7.0.0.11-ga-20191216_1-1_amd64.deb)
- Tar File Install Packages For Linux x86
  - [TensorRT 7.0.0.11 for Ubuntu 18.04 and CUDA 10.0 tar package](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/7.0/7.0.0.11/tars/TensorRT-7.0.0.11.Ubuntu-18.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz)
  - [TensorRT 7.0.0.11 for Ubuntu 16.04 and CUDA 10.0 tar package](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/7.0/7.0.0.11/tars/TensorRT-7.0.0.11.Ubuntu-16.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz)

这里使用基于 deb 文件的安装，但是建议还是下载一个 tar 文件，这样在安装完成后，如果报错发现一些依赖包缺失，便于安装依赖包，在之后就会看到这样的操作。  
同时需要注意的是，英伟达自己的几个 GPU 平台是有不一样的安装指南的。比如你用 Drive PX2，就要使用 DriveInstall 来安装 TensorRT 了。  
<img src="https://pic2.zhimg.com/80/v2-262e209917537c0f699cc1a5eb803b2d_720w.png" width="100%">

### 安装

#### 使用 deb 包安装

\#\#\# 添加环境变量
\#\#\# 检查

#### prelim

先在 Ubuntu 16.04 系统上使用 tar 安装 TensorRT，安装完后可导入 tensorrt，但是 uff 导入失败。错因是没有 tensorflow 模块

```bash
$ conda remove -n adanet --all
$ conda create -n adanet python=3.6
$ source activate adanet
$ pip install tensorrt uff # as follows in `tar`
# numpy=1.18.2; setuptools=46.1.3.post20200330
Package    Version
---------- -------------------
certifi    2019.11.28
numpy      1.18.2
pip        20.0.2
protobuf   3.11.3
setuptools 46.1.3.post20200330
six        1.14.0
tensorrt   7.0.0.11
uff        0.6.5
wheel      0.34.2

$ pip install adanet
# Successfully installed 
# absl-py-0.9.0  adanet-0.8.0
# colorama-0.4.3 coverage-4.5.4
# mock-3.0.5     nose-1.3.7
# rednose-1.3.0  termstyle-0.1.11

$ pip install tensorflow-gpu
# Successfully installed
# astor-0.8.1 cachetools-4.0.0 chardet-3.0.4 gast-0.2.2
# google-auth-1.13.1 google-auth-oauthlib-0.4.1 google-pasta-0.2.0
# grpcio-1.27.2 h5py-2.10.0 idna-2.9
# keras-applications-1.0.8 keras-preprocessing-1.1.0
# markdown-3.2.1 oauthlib-3.1.0 opt-einsum-3.2.0
# pyasn1-0.4.8 pyasn1-modules-0.2.8
# requests-2.23.0 requests-oauthlib-1.3.0 rsa-4.0
# scipy-1.4.1
# tensorboard-2.1.1 tensorflow-estimator-2.1.0 tensorflow-gpu-2.1.0
# termcolor-1.1.0 urllib3-1.25.8 werkzeug-1.0.1 wrapt-1.12.1
```

**导入错误**

Cannot dlopen some TensorRT libraries.  
["Could not load dynamic library 'libnvinfer.so.6'" when installing from WSL 2](https://github.com/tensorflow/tensorflow/issues/36201)  
[Could not load dynamic library 'libnvinfer_plugin.so.6'](https://github.com/tensorflow/tensorflow/issues/35968)  
[Installation errors with tensorflow 2.1.0](https://stackoverflow.com/questions/59954265/installation-errors-with-tensorflow-2-1-0)  

Could not find .pgm in data directories, TensorRT  
[Keras vs. TensorRT Incorrect Results](https://github.com/NVIDIA/TensorRT/issues/375)  
[Bug for TF2.x + TensorRT(7) failing when minimum_segment_size=2](https://github.com/tensorflow/tensorflow/issues/36724)  

[Tensorflow TensorRT: Could not load dynamic library 'libnvinfer.so.5'](https://github.com/tensorflow/tensorflow/issues/34329)  

**tensorflow-gpu 2.1.0 需要 libnvinfer.so.6 ，不是 TensorRT 7.x**  
**必须重新安装 TensorRT 6.0** 

#### 使用 tar 包安装

首先下载 tar 版本的安装包，下载地址需要登陆 NVIDIA。  
安装 TensorRT 前需要安装 CUDA 和 cuDNN 
```bash
~$ # 1. 打开下载路径，解压 tar 文件 
~$ cd Software
~/Software$ ls
Anaconda3-5.2.0-Linux-x86_64.sh
cuda-10.0
cuda_10.0.130_410.48_linux.run
cuda-samples
cudnn-10.0-linux-x64-v7.6.4.38.tgz
nv-tensorrt-repo-ubuntu1604-cuda10.0-trt7.0.0.11-ga-20191216_1-1_amd64.deb
Python-3.6.1.tgz
TensorRT-7.0.0.11.Ubuntu-16.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz
~/Software$ tar -xvf TensorRT-7.0.0.11.Ubuntu-16.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz

~/Software$ # 此时多了一个 `TensorRT-7.0.0.11` 文件夹
~/Software$ # 2. 解压好添加环境变量
~/Software$ vim ~/.bashrc  # 打开环境变量文件

## # 将下面三个环境变量写入环境变量文件并保存
## export LD_LIBRARY_PATH=TensorRT解压路径/lib:$LD_LIBRARY_PATH
## export CUDA_INSTALL_DIR=/usr/local/cuda-9.0
## export CUDNN_INSTALL_DIR=/usr/local/cuda-9.0
i.e,,
export LD_LIBRARY_PATH=$HOME/Software/TensorRT-7.0.0.11/lib:$LD_LIBRARY_PATH
export CUDA_INSTALL_DIR=$HOME/Software/cuda-10.0
export CUDNN_INSTALL_DIR=$HOME/Software/cuda-10.0

~/Software$ source ~/.bashrc  # 使刚刚修改的环境变量文件生效
```

下面是安装 Python 的 TensorRT 包
```bash
~/Software$ # 3. 进入解压后的 TensorRT 目录下的 python 文件夹
~/Software$ cd TensorRT-7.0.0.11
~/Software/TensorRT-7.0.0.11$ ls
bin   doc           include  python   targets                     uff
data  graphsurgeon  lib      samples  TensorRT-Release-Notes.pdf
~/Software/TensorRT-7.0.0.11$ cd Python
-sh: cd: Python: No such file or directory
~/Software/TensorRT-7.0.0.11$ cd python
~/Software/TensorRT-7.0.0.11/python$ ls
tensorrt-7.0.0.11-cp27-none-linux_x86_64.whl  tensorrt-7.0.0.11-cp36-none-linux_x86_64.whl
tensorrt-7.0.0.11-cp34-none-linux_x86_64.whl  tensorrt-7.0.0.11-cp37-none-linux_x86_64.whl
tensorrt-7.0.0.11-cp35-none-linux_x86_64.whl
~/Software/TensorRT-7.0.0.11/python$

~/Software/TensorRT-7.0.0.11/python$ # 安装。
# 注意刚刚 source ~/.bashrc 后自动退出虚拟环境，需重新进入
~/Software/TensorRT-7.0.0.11/python$ conda activate adanet
~/Software/TensorRT-7.0.0.11/python$ pip install tensorrt-7.0.0.11-cp36-none-linux_x86_64.whl
Processing ./tensorrt-7.0.0.11-cp36-none-linux_x86_64.whl
Installing collected packages: tensorrt
Successfully installed tensorrt-7.0.0.11
(adanet) ~/Software/TensorRT-7.0.0.11/python$ pip list
Package    Version
---------- -------------------
certifi    2019.11.28
pip        20.0.2
setuptools 46.1.3.post20200330
tensorrt   7.0.0.11
wheel      0.34.2
(adanet) ~/Software/TensorRT-7.0.0.11/python$
```

测试 TensorRT 是否安装成功，能正确输出版本号即可
```bash
(adanet) ~/Software/TensorRT-7.0.0.11/python$ python
Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorrt
>>> tensorrt.__version__
'7.0.0.11'
>>>
[5]+  Stopped(SIGTSTP)        python
```

然后转到 uff 目录下安装 uff 包
```bash
(adanet) ~/Software/TensorRT-7.0.0.11/python$ cd ../uff
(adanet) ~/Software/TensorRT-7.0.0.11/uff$ ls
uff-0.6.5-py2.py3-none-any.whl
(adanet) ~/Software/TensorRT-7.0.0.11/uff$ pip install uff-0.6.5-py2.py3-none-any.whl
Processing ./uff-0.6.5-py2.py3-none-any.whl
Collecting protobuf>=3.3.0
  Downloading protobuf-3.11.3-cp36-cp36m-manylinux1_x86_64.whl (1.3 MB)
     |████████████████████████████████| 1.3 MB 562 kB/s
Collecting numpy>=1.11.0
  Downloading numpy-1.18.2-cp36-cp36m-manylinux1_x86_64.whl (20.2 MB)
     |████████████████████████████████| 20.2 MB 2.3 MB/s
Requirement already satisfied: setuptools in /home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/lib/python3.6/site-packages (from protobuf>=3.3.0->uff==0.6.5) (46.1.3.post20200330)
Collecting six>=1.9
  Downloading six-1.14.0-py2.py3-none-any.whl (10 kB)
Installing collected packages: six, protobuf, numpy, uff
Successfully installed numpy-1.18.2 protobuf-3.11.3 six-1.14.0 uff-0.6.5
(adanet) ~/Software/TensorRT-7.0.0.11/uff$

# 测试，会输出 uff 的安装路径
(adanet) ~/Software/TensorRT-7.0.0.11/uff$ which convert-to-uff
/home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/bin/convert-to-uff

# 拷贝 lenet5.uff 到 python 相关目录进行验证
(adanet) ~/Software/TensorRT-7.0.0.11/uff$ cd ..
(adanet) ~/Software/TensorRT-7.0.0.11$ mkdir python/data
(adanet) ~/Software/TensorRT-7.0.0.11$ mkdir python/data/mnist
(adanet) ~/Software/TensorRT-7.0.0.11$ cp ./data/mnist/lenet5.uff ./python/data/mnist/lenet5.uff
(adanet) ~/Software/TensorRT-7.0.0.11$ cd ./samples/sampleMNIST
(adanet) ~/Software/TensorRT-7.0.0.11/samples/sampleMNIST$ ls
Makefile  README.md  sampleMNIST.cpp
(adanet) ~/Software/TensorRT-7.0.0.11/samples/sampleMNIST$ make clean
(adanet) ~/Software/TensorRT-7.0.0.11/samples/sampleMNIST$ make
(adanet) ~/Software/TensorRT-7.0.0.11/samples/sampleMNIST$ cd ../../bin
(adanet) ~/Software/TensorRT-7.0.0.11/bin$ ./sample_mnist
# 若命令执行顺利则/即安装成功
# Could not find 3.pgm in data directories: &&&& FAILED
```

Current optimization profile is: 0. Please ensure there are no enqueued operations pending in this context prior to switching profiles   
[Please ensure there are no enqueued operations pending in this context prior to switching profiles” warning](https://forums.developer.nvidia.com/t/please-ensure-there-are-no-enqueued-operations-pending-in-this-context-prior-to-switching-profiles-warning/111189)  

## Second Attempt: Work

### 下载
[NVIDIA TensorRT 6.x Download](https://developer.nvidia.com/nvidia-tensorrt-6x-download)  
TensorRT 6.0 GA for Linux
- Debian and RPM Install Packages for Linux x86
  - TensorRT 6.0.1.5 GA for Ubuntu 1804 and CUDA 10.0 DEB local repo packages
- Tar File Install Packages For Linux x86
  - TensorRT 6.0.1.5 GA for Ubuntu 18.04 and CUDA 10.0 tar package
  - TensorRT 6.0.1.5 GA for Ubuntu 16.04 and CUDA 10.0 tar package

### 使用 tar 包安装

卸载 TensorRT  
[（原）Ubuntu安装TensorRT](https://www.cnblogs.com/darkknightzh/p/11129472.html)  
[Ubuntu16.04 安装tensorRT 全过程](https://blog.csdn.net/calmuse/article/details/93616720)  
[ubuntu安装tensorRT](https://blog.csdn.net/weixin_37669089/article/details/85255760)  

先卸载
```bash
$ source activate adanet
$ pip uninstall uff  # y
$ pip uninstall tensorrt  # y
$ cd ~/Software
$ rm -r TensorRT-7.0.0.11
```

再安装
```bash
(adanet) ~$ cd ~/Software 
$ tar -xzvf TensorRT-6.0.1.5.Ubuntu-16.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz
$ vim ~/.bashrc

# added by Anaconda3 installer
export PATH="/home/eustomaqua/VirtualEnv/anaconda3/bin:$PATH"
# self added for Nvidia
export PATH=$HOME/Software/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=$HOME/Software/cuda-10.0/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$HOME/Software/TensorRT-6.0.1.5/lib:$LD_LIBRARY_PATH
export CUDA_INSTALL_DIR=$HOME/Software/cuda-10.0
export CUDNN_INSTALL_DIR=$HOME/Software/cuda-10.0
```

新开终端以便使 `~/.bashrc` 文件生效
```bash
(adanet) ~$ cd ~/Software
$ cd TensorRT-6.0.1.5

$ cd python
$ pip install tensorrt-6.0.1.5-cp36-none-linux_x86_64.whl
Successfully installed tensorrt-6.0.1.5
>>> import tensorrt
>>> tensorrt.__version__

$ cd ../uff
$ pip install uff-0.6.5-py2.py3-none-any.whl
Successfully installed uff-0.6.5
```

检查 tensorflow, adanet, uff 的导入情况
```python
Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
2020-04-03 07:02:35.550509: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libnvinfer.so.6
2020-04-03 07:02:35.552571: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libnvinfer_plugin.so.6
>>> import adanet
WARNING:tensorflow:From /home/eustomaqua/VirtualEnv/anaconda3/envs/adapruning/lib/python3.6/site-packages/adanet/core/tpu_estimator.py:39: The name tf.estimator.tpu.TPUEstimator is deprecated. Please use tf.compat.v1.estimator.tpu.TPUEstimator instead.

>>>
>>> import tensorrt
>>> import uff
Traceback (most recent call last):
  File "/home/eustomaqua/VirtualEnv/anaconda3/envs/adapruning/lib/python3.6/site-packages/uff/converters/tensorflow/conversion_helpers.py", line 18, in <module>
    from tensorflow import GraphDef
ImportError: cannot import name 'GraphDef'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/eustomaqua/VirtualEnv/anaconda3/envs/adapruning/lib/python3.6/site-packages/uff/__init__.py", line 2, in <module>
    from uff.converters.tensorflow.conversion_helpers import from_tensorflow  # noqa
  File "/home/eustomaqua/VirtualEnv/anaconda3/envs/adapruning/lib/python3.6/site-packages/uff/converters/tensorflow/conversion_helpers.py", line 23, in <module>
    https://www.tensorflow.org/install/""".format(err))
ImportError: ERROR: Failed to import module (cannot import name 'GraphDef')
Please make sure you have TensorFlow installed.
For installation instructions, see:
https://www.tensorflow.org/install/
>>>
```

ImportError: cannot import name 'GraphDef'  
[ImportError: cannot import name 'Graph'](https://stackoverflow.com/questions/50031584/importerror-cannot-import-name-graph)  
[TensorRT 6 : import uff error](https://forums.developer.nvidia.com/t/tensorrt-6-import-uff-error/108008)  
> It seems to be due to Tensorflow version.
> UFF converter not supporting TF version 2.0.
> Please check the tensorflow version and install tensorflow version 1.15 or 1.14.

检查 uff 的安装情况
```bash
$ pip uninstall uff  # y
$ deactivate

$ conda env list
$ conda create -n adanet python=3.6
$ source activate adanet
$ pip install tensorflow-gpu==1.*
# Successfully installed
# absl-py-0.9.0 astor-0.8.1 gast-0.2.2
# google-pasta-0.2.0 grpcio-1.27.2 h5py-2.10.0
# keras-applications-1.0.8 keras-preprocessing-1.1.0
# markdown-3.2.1 numpy-1.18.2 opt-einsum-3.2.0
# protobuf-3.11.3 six-1.14.0
# tensorboard-1.15.0 tensorflow-estimator-1.15.1
# tensorflow-gpu-1.15.2
# termcolor-1.1.0 werkzeug-1.0.1 wrapt-1.12.1
$ pip install adanet
# Successfully installed
# adanet-0.8.0 colorama-0.4.3 coverage-4.5.4
# mock-3.0.5 nose-1.3.7 rednose-1.3.0 termstyle-0.1.11

Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorrt
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'tensorrt'
>>> import tensorflow as tf
>>> import adanet
WARNING:tensorflow:From /home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/tf_compat/__init__.py:87: The name tf.losses.Reduction is deprecated. Please use tf.compat.v1.losses.Reduction instead.
WARNING:tensorflow:From /home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/core/tpu_estimator.py:39: The name tf.estimator.tpu.TPUEstimator is deprecated. Please use tf.compat.v1.estimator.tpu.TPUEstimator instead.
>>>

$ cd ~/Software/TensorRT-6.0.1.5
$ cd python
$ pip install tensorrt-6.0.1.5-cp36-none-linux_x86_64.whl
$ cd ../uff
$ pip install uff-0.6.5-py2.py3-none-any.whl

Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorrt
>>> import uff
>>> import tensorflow as tf
>>> import adanet
WARNING:tensorflow:From /home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/tf_compat/__init__.py:87: The name tf.losses.Reduction is deprecated. Please use tf.compat.v1.losses.Reduction instead.

WARNING:tensorflow:From /home/eustomaqua/VirtualEnv/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/core/tpu_estimator.py:39: The name tf.estimator.tpu.TPUEstimator is deprecated. Please use tf.compat.v1.estimator.tpu.TPUEstimator instead.

>>>
[6]+  Stopped(SIGTSTP)        python
(adanet) ~/Software/TensorRT-6.0.1.5/uff$
```

### 使用 deb 包安装

创建环境
```bash
$ conda env list
$ conda create -n adanet python=3.6  # tensorflow-gpu==2.1.0 adanet=0.8.0
$ source activate adanet
$ source deactivate
$ conda remove -n adanet -all

$ conda create -n adanet python=3.6
$ source activate adanet
$ pip list
Package    Version
---------- -------------------
certifi    2019.11.28
pip        20.0.2
setuptools 46.1.3.post20200330
wheel      0.34.2

$ pip install tensorflow-gpu==1.*
# Successfully installed
# absl-py-0.9.0 astor-0.8.1 gast-0.2.2
# google-pasta-0.2.0 grpcio-1.27.2 h5py-2.10.0
# keras-applications-1.0.8 keras-preprocessing-1.1.0
# markdown-3.2.1 numpy-1.18.2 opt-einsum-3.2.0
# protobuf-3.11.3 six-1.14.0
# tensorboard-1.15.0 tensorflow-estimator-1.15.1
# tensorflow-gpu-1.15.2
# termcolor-1.1.0 werkzeug-1.0.1 wrapt-1.12.1
$ pip install adanet
# Successfully installed
# adanet-0.8.0 colorama-0.4.3 coverage-4.5.4
# mock-3.0.5 nose-1.3.7 rednose-1.3.0 termstyle-0.1.11

Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> import adanet
WARNING:tensorflow:From /home/eustomaqua/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/tf_compat/__init__.py:87: The name tf.losses.Reduction is deprecated. Please use tf.compat.v1.losses.Reduction instead.
WARNING:tensorflow:From /home/eustomaqua/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/core/tpu_estimator.py:39: The name tf.estimator.tpu.TPUEstimator is deprecated. Please use tf.compat.v1.estimator.tpu.TPUEstimator instead.
>>>
[1]+  Stopped                 python
```

安装 TensorRT
```bash
$ cd ~/Software
$ ls
cuda-10.0
cuda-samples
nv-tensorrt-repo-ubuntu1804-cuda10.0-trt6.0.1.5-ga-20190913_1-1_amd64.deb
nv-tensorrt-repo-ubuntu1804-cuda10.0-trt7.0.0.11-ga-20191216_1-1_amd64.deb
TensorRT-6.0.1.5.Ubuntu-18.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz
TensorRT-7.0.0.11.Ubuntu-18.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz

$ dpkg -i nv-tensorrt-repo-ubuntu1804-cuda10.0-trt6.0.1.5-ga-20190913_1-1_amd64.deb
dpkg: error: requested operation requires superuser privilege
```

放弃 deb 安装，回到 tar 方式
```bash
$ cd ~/Software
$ tar -xvaf TensorRT-6.0.1.5.Ubuntu-18.04.x86_64-gnu.cuda-10.0.cudnn7.6.tar.gz
$ cd TensorRT-6.0.1.5
$ cd python
$ pip install tensorrt-6.0.1.5-cp36-none-linux_x86_64.whl
$ cd ../uff
$ pip install uff-0.6.5-py2.py3-none-any.whl

$ vim ~/.bashrc

# added by Anaconda3 installer
export PATH="/home/eustomaqua/anaconda3/bin:$PATH"
# self added for Nvidia
export PATH="$HOME/Software/cuda-10.0/bin:$PATH"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$HOME/Software/cuda-10.0/lib64/"
# TensorRT
export LD_LIBRARY_PATH=$HOME/Software/TensorRT-6.0.1.5/lib:$LD_LIBRARY_PATH
export CUDA_INSTALL_DIR=$HOME/Software/cuda-10.0
export CUDNN_INSTALL_DIR=$HOME/Software/cuda-10.0
```
新开终端使 `.bashrc` 生效
```bash
$ source activate adanet
$ cd ~/Software/TensorRT-6.0.1.5

Python 3.6.10 |Anaconda, Inc.| (default, Mar 25 2020, 23:51:54)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorrt
>>> import uff
>>> import tensorflow as tf
>>> import adanet
WARNING:tensorflow:From /home/eustomaqua/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/tf_compat/__init__.py:87: The name tf.losses.Reduction is deprecated. Please use tf.compat.v1.losses.Reduction instead.

WARNING:tensorflow:From /home/eustomaqua/anaconda3/envs/adanet/lib/python3.6/site-packages/adanet/core/tpu_estimator.py:39: The name tf.estimator.tpu.TPUEstimator is deprecated. Please use tf.compat.v1.estimator.tpu.TPUEstimator instead.

>>>
[1]+  Stopped                 python
```

检查 tensorrt, uff 是否安装成功
```bash
$ python
>>> import tensorrt
>>> tensorrt.__version__

$ cd ~/Software/TensorRT-6.0.1.5
$ which convert-to-uff
/home/eustomaqua/anaconda3/envs/adanet/bin/convert-to-uff
$
$ mkdir python/data
$ mkdir python/data/mnist
$ cp ./data/mnist/lenet5.uff ./python/data/mnist/lenet5.uff
$ cd ./samples/sampleMNIST
$ make clean
$ make
$ cd ../../bin
$ ./sample_mnist
&&&& RUNNING TensorRT.sample_mnist # ./sample_mnist
[03/03/2020-07:47:01] [I] Building and running a GPU inference engine for MNIST
[03/03/2020-07:47:07] [I] [TRT] Detected 1 inputs and 1 output network tensors.
Could not find 8.pgm in data directories:
        data/mnist/
        data/samples/mnist/
&&&& FAILED
```

### 检查 uff 的安装情况

Could not find 8.pgm in data directories:  
[Depreciated MNIST Sample](https://github.com/NVIDIA/TensorRT/issues/256)  
[TensorRT(2)-基本使用：mnist手写体识别](https://arleyzhang.github.io/articles/c17471cb/)  
[【代码分析】TensorRT sampleMNIST 详解](https://blog.csdn.net/HaoBBNuanMM/article/details/102841685)  

[TensorRT-sample-support-guide NVIDIA](https://docs.nvidia.com/deeplearning/sdk/tensorrt-sample-support-guide/index.html)  
[Getting started with PyTorch and TensorRT | IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.1/navigation/wmlce_getstarted_tensorrt.html)  

[Could not find 0.pgm in data directories: ](https://github.com/NVIDIA/TensorRT/issues/165)  
Answer: [Answer in other thread:](https://github.com/NVIDIA/TensorRT/issues/256#issuecomment-568382745)  
> By running the download_pgms.py in the /TensorRT-7.0.0.11/data/mnist, I can already get the *.pgm files.
>

generate_pgms.py  
[tensorrt-release-notes NVIDIA](https://docs.nvidia.com/deeplearning/sdk/tensorrt-release-notes/tensorrt-6.html)  
[深度学习算法优化系列十七 | TensorRT介绍，安装及如何使用？](https://zhuanlan.zhihu.com/p/110934202)  

```bash
~/Software/TensorRT-6.0.1.5/bin$ dpkg -l | grep TensorRT
$ cd ../data/mnist
$ cat README.md
```

## 总结

在安装 tensorrt, uff 之前，需先创建虚拟环境，并安装 tensorflow-gpu==1.*   
注意 tensorflow-gpu 不能是 2.x 版本，因为 uff 与 tf2.0 不兼容  

此外使用 tensorflow-gpu==2.1.0 时，发现它调用的是 TensorRT 6.x ，不能用 TensorRT 7.x；  
把 tensorflow-gpu 版本降级为 1.15.2 后，仍然可以使用 TensorRT 6.x

# \*References

[GitHub、GitLab与BitBucket应该怎么选?](http://tech.it168.com/a2017/1026/3176/000003176180.shtml)  
[利用 SSH 的用户配置文件 Config 管理 SSH 会话](https://www.hi-linux.com/posts/14346.html)  
