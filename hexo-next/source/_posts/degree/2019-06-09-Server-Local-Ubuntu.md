---
title: 远程服务器与本地机的使用 (Ubuntu 16.04)
date: 2019-06-09 23:02:59
updated: 2019-06-09 23:02:59
categories: 
  - Records
tags: 
  - Configuration
  - Linux
  - Git
  - Remote Server
---
<!--
date: 2019-06-09 23:02:59
updated: 

Modified: 24 Mar 2020 10:05:57
Configure: 4 Dec 2021 15:22:08
-->


# Server

前提条件： 
1. 无 root 权限
2. Ubuntu 16.04
3. CUDA 9.0 (not necessary)

## 非 root 用户安装 cuda, cudnn

### 1. 下载安装 cuda

- 下载 TensorFlow 对应版本的 CUDA [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads) 
- 选择 linux 及对应系统之后，选择 runfile(local) 下载，*即 ``linux -> x86_64 -> Ubuntu -> 16.04 -> runfile (local)''*
- 给文件运行权限 **chmod +x filename.run** 然后运行 **./filename.run**
- 在协议中选择同意 (accept)，不安装 driver installation (no)，然后在安装 cuda 时选择个人用户的家目录，如 **/home/yourname/cuda90**，link 选择 no，samples 自己设定 (yes or no) 及安装目录，sudo 选择 no
- 修改个人用户的环境变量，环境变量文件 **~/.bashrc** 位于家目录，即 **/home/yourname/.bashrc** (可用 **vim ~/.bashrc** 编辑)，末尾添加如下语句  ；修改之后需 **source ~/.bashrc** 使环境变量生效，或另开终端
```shell
export PATH=$HOME/VirtualEnv/cuda90/bin:$PATH
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/VirtualEnv/cuda90/lib64/
```


### 2. 查看 cuda 安装状态

- **nvidia-smi** 查看显卡驱动运行状态
- **nvcc -V** 查看 cuda-toolkit 安装是否成功

### 3. 安装 cudnn

- cudnn 的安装，官网下载 [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn) (需注册账号)，解压到 cuda 所在的文件夹，**tar -xzvf cuda-9.0-linux-x64-v7.4.2.24.tgz** (输入自己下载的安装包名)
- 拷贝过去 cudnn -> cuda (cuda90 是个人用户家目录下的 /home/yourname/VirtualEnv/cuda90 )，注意路径正确  
  **cp cuda/include/cudnn.h ~/VirtualEnv/cuda90/include/**   
  **cp cuda/lib64/libcudnn* ~/VirtualEnv/cuda90/lib64**   
  **chmod a+r ~/VirtualEnv/cuda90/include/cudnn.h ~/VirtualEnv/cuda90/lib64/libcudnn* **  


### 4. 查看 cudnn 安装状态

**cat ~/VirtualEnv/cuda90/include/cudnn.h | grep CUDNN_MAJOR -A5**  
显示
```python
$ cat ~/VirtualEnv/cuda90/include/cudnn.h | grep CUDNN_MAJOR -A5
#define CUDNN_MAJOR 7
#define CUDNN_MINOR 4
#define CUDNN_PATCHLEVEL 2

#define CUDNN_VERSION (CUDNN_MAJOR * 1000 + CUDNN_MINOR * 100 + CUDNN_PATCHLEVEL)

#include "driver_types.h"
#include <cuda_runtime.h>

#ifndef CUDNNWINAPI
```
则 cudnn 版本为 7.4.2  
然后就可以安装自己想要安装的框架了

后续：编译框架的时候提示无 lcuda.so 动态库   
解决办法：在 /usr/lib64/nvidia 中有，创建软链接到自己的安装 cuda 的目录 /home/liuao/cuda91/lib64 (i.e., /home/username/VirtualEnv/cuda90/lib64) 即可。


### * 安装过程 (所用到的命令)

```shell
# install cuda
$ cd ~/VirtualEnv
$ chmod +x cuda_9.0.176_384.81_linux.run
$ ./cuda_9.0.176_384.81_linux.run
[EULA] accept
[install Driver] no
[install CUDA 9.0 Toolkit] yes
[Toolkit location] /home/yourname/VirtualEnv/cuda90
[symbolic link at /usr/local/cuda] no
[install CUDA 9.0 Samples] yes
[Samples location] /home/yourname/VirtualEnv/cudasamples
$ nvidia-smi
$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2017 NVIDIA Corporation
Built on Fri_Sep__1_21:08:03_CDT_2017
Cuda compilation tools, release 9.0, V9.0.176
#
# install cudnn
$ cd ~/VirtualEnv
$ tar -xzvf cudnn-9.0-linux-x64-v7.4.2.24.tgz
$ cp cuda/include/cudnn.h ~/VirtualEnv/cuda90/include/
$ ls cuda/lib64
$ cp cuda/lib64/libcudnn* ~/VirtualEnv/cuda90/lib64/
$ chmod a+r ~/VirtualEnv/cuda90/include/cudnn.h ~/VirtualEnv/cuda90/lib64/libcudnn*
$ cat ~/VirtualEnv/cuda90/include/cudnn.h | grep CUDNN_MAJOR -A5
#define CUDNN_MAJOR 7
#define CUDNN_MINOR 4
#define CUDNN_PATCHLEVEL 2

#define CUDNN_VERSION (CUDNN_MAJOR * 1000 + CUDNN_MINOR * 100 + CUDNN_PATCHLEVEL)

#include "driver_types.h"
#include <cuda_runtime.h>

#ifndef CUDNNWINAPI
```


## 非 root 用户安装自己的 Python

我的习惯是  
- virtualenv 创建的虚拟环境都放在 **VirtualEnv** 文件夹下，命名格式 e.g., **py36env**, **py35gnn**, etc 
- 家目录安装的不同版本 Python 都放在 **software** 文件夹下 (同时存放软件下载包)，命名格式 e.g., **python27**, etc

```shell
$ mkdir software
$ cd software
# 
# install Python
$ wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
$ tar -zxvf Python-3.6.1.tgz
$ cd Python-3.6.1
$ ./configure --prefix=/home/userrname/software/python36
$ make -j
$ make install
# or: make -j && make install
# 注意如果 make && make install 会失败，应该是权限问题
# 
# pip3 install package
$ cd ../python36
$ bin/python3
$ bin/pip3 list
$ cd bin
$ ./pip3 install packagename
```


## 非 root 用户安装 Python 包库

两种方法：
> pip install --user package-name
> virtualenv, virtualenvwrapper

方法一的卸载，pip uninstall package-name 即可，会先卸载个人目录下的包。如果个人目录和系统目录有同名包，随后使用 sudo 卸载系统包即可。

方法二更方便环境隔离，可以自行配置多个环境。

方法三是用 docker，暂未尝试。


非 root 用户在服务器上配置自己的环境，使用 pip install --user package 设置自己的虚拟环境
```perl
$ pip install --user virtualenv virtualwrapper
#
# create virtual environment (not necessary)
$ cd ~
$ mkdir VirtualEnv
$ cd VirtualEnv
$ virtualenv py36env --python=/usr/bin/python3.6
$ source py36env/bin/activate
$ pip list
$ pip install packagename....
$ deactivate
```


# Remote (Local - Server)

## TensorBoard 远程访问


### 远程连接

在本地/虚拟机 (Ubuntu 16.04) 中 

1. 终端 
```shell
ssh -L 16006:127.0.0.1:6006 yourname@server.address
```
  其中 16006:127.0.0.1 代表自己机器上的 16006 号端口，6006 是服务器上 TensorBoard 使用的端口
2. 在浏览器中打开 http://127.0.0.1:16006
3. 服务器上 ctrl+c 关闭后，本地即无法连接
4. 本地终端 exit
```powershell
ubuntu@VirtualBox:~$ ssh -L 16006:127.0.0.1:6006 yourname@server.address
yourname@server.address's password: 
Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 4.4.0-141-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

79 packages can be updated.
4 updates are security updates.

New release '18.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


*** System restart required ***
Last login: Thu Feb  7 15:46:49 2019 from 10.231.238.49
yourname@server.address:~$ exit
logout
Connection to server.address closed.
ubuntu@VirtualBox:~$ 
```

### 使用
Usage: ``$ tensorboard --logdir=folder_path``

1. between Local Steps 1 & 2
2. 在服务器上开启 TensorBoard
  ```shell
  tensorboard --logdir=./network
  ```

e.g.,
```powershell
ubuntu@VirtualBox:~$ ssh -L 16006:127.0.0.1:6006 yourname@server.address
yourname@server.address's password: 
Last login: Wed Feb 27 11:08:00 2019 from 10.230.167.212
yourname@server.address:~$ source VirtualEnv/py35env/bin/activate
(py35env) yourname@server.address:~$ cd yourfolder
(py35env) yourname@server.address:~/yourfolder$ ls
(py35env) yourname@server.address:~/yourfolder$ tensorboard --logdir=folder_of_your_model
W0227 12:16:59.123035 Reloader tf_logging.py:120] Found more than one graph event per run, or there was a metagraph containing a graph_def, as well as one or more graph events.  Overwriting the graph with the newest event.
TensorBoard 1.12.1 at http://yourserver:6006 (Press CTRL+C to quit)
^C(py35env) yourname@server.address:~/yourfolder$ 
```


##  Jupyter notebook 远程访问

仍以非 root 用户身份安装

1, 安装步骤  
(1) 登录服务器  
```perl
~$ source ~/VirtualEnv/py36env/bin/activate
(py36env) ~$ jupyter notebook
jupyter: command not found
```
(2) 检查是否有安装 jupyter notebook  
终端输入 jupyter nootbook ，如果报错就是没有安装，用下列命令安装
```perl
(py36env) ~$ #pip install pyzmq tornado jinja2 jsonschema
(py36env) ~$ pip install jupyter
```
(3) 生成配置文件
```perl
(py36env) ~$ jupyter notebook --generate-config
Writing default config to: /home/username/.jupyter/jupyter_notebook_config.py
```
(4) 生成密码 （后续写配置文件、登录 Jupyter notebook 时需要）   
打开Python终端，我输入的密码是 1234
```perl
(py36env) ~$ python
Python 3.6.7 (default, Oct 21 2018, 04:56:05)
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from IPython.lib import passwd
>>> passwd()
Enter password:
Verify password:
'sha1:afc40e4de2b5:69f901707c23fde938709612d49424fab065c3b1'
>>>
[12]+  Stopped                 python
```
(5) 修改默认配置文件
```perl
(py36env) ~$ vim ~/.jupyter/jupyter_notebook_config.py
```
进行如下修改（这里可以自行配置）：
```vim
c.NotebookApp.ip = '*'  #允许所有ip访问
c.NotebookApp.password = u'sha1:afc40e4de2b5:69f901707c23fde938709612d49424fab065c3b1'  #刚才复制的那个密文
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888  #随便指定一个端口
c.IPKernelApp.pylab = 'inline'
```

(6) 启动 Jupyter notebook
```perl
(py36env) ~$ jupyter notebook
[I 12:16:27.663 NotebookApp] Serving notebooks from local directory: /home/username
[I 12:16:27.663 NotebookApp] The Jupyter Notebook is running at:
[I 12:16:27.664 NotebookApp] http://server.address:8888/
[I 12:16:27.664 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
^C[I 12:23:05.617 NotebookApp] interrupted
Serving notebooks from local directory: /home/username
0 active kernels
The Jupyter Notebook is running at:
http://username:8888/
Shutdown this notebook server (y/[n])? y
[C 12:23:08.408 NotebookApp] Shutdown confirmed
[I 12:23:08.409 NotebookApp] Shutting down 0 kernels
(py36env) ~$
```

注意：服务器的 ip，不需要加自己的用户名，即 'server.address' 即可，若写成 'username@server.address' 会报错，说其并非是一个 ip 地址
```perl
Traceback (most recent call last):
  File "/home/username/VirtualEnv/py36env/lib/python3.6/site-packages/notebook/notebookapp.py", line 864, in _default_allow_remote
    addr = ipaddress.ip_address(self.ip)
  File "/usr/lib/python3.6/ipaddress.py", line 54, in ip_address
    address)
ValueError: 'username@server.address' does not appear to be an IPv4 or IPv6 address
```
注意：c.NotebookApp.ip 的问题及报错
```vim
#(1) c.NotebookApp.ip = 'username@server.address'
ValueError: 'username@server.address' does not appear to be an IPv4 or IPv6 address

#(2) c.NotebookApp.ip = 'server.address'
http://server.address:8888
无法访问此网站
server.address 的响应时间过长

#(3) c.NotebookApp.ip = '*'
ValueError: '' does not appear to be an IPv4 or IPv6 address

#(4) c.NotebookApp.ip = '0.0.0.0'
http://(server or 127.0.0.1):8888/
无法访问此网站 (4a/4b)
(4a) 找不到 server 的服务器 IP 地址
(4b) 127.0.0.1 拒绝了我们的连接请求
```

(7) 远程访问  
此时应该可以直接从本地浏览器直接访问 http://address_of_remote:8888 就可以看到 jupyter 的登录页面。（注意服务器上的 Jupyter notebook 不要关）



## PyCharm

### Deployment

**Tools -> Deployment -> Configuration**  
+server, and remember to "Save password"

**Tools -> Deployment -> Options**  
click "Create empty directions"

### Python interpreter

**File -> Settings**  
**Project: your_name -> Project Interpreter**  
add the python path on the server, remember to "**Move this server to IDE settings**" instead of "Create copy of this deployment server in IDE settings"   
**Edit Sync Folders** (Local Path, Remote Path)

### 其它配置

#### autopep8

**File -> Settings -> Tools -> External Tools -> +**  
> Program：C:\Python35\Scripts\autopep8.exe   
> Parameters：--in-place --ignore=E123,E133,E50 "\$FilePath\$"  
> Working directory：\$FileDir\$

[在PyCharm环境配置Autopep8到菜单栏](https://blog.csdn.net/yannanxiu/article/details/54598404)  
[PyCharm 使用 autopep8 按 PEP8 风格自动排版 Python 代码](https://wsgzao.github.io/post/autopep8/)



# Local

## Ubuntu 16.04 (alongside Win 7)

我双系统安装失败了，现在只能用 Ubuntu，一启动 Win 7 就花屏



## Windows 10

Bitvise SSH Client

可以写个 .sh 然后 nohup 执行。  
如果不用 nohup，一旦关闭终端/连接断掉，这个脚本就会停止执行 
```shell
$ vim yourtask.sh
$ chmod +x ./yourtask.sh
$ nohup ./yourtask.sh
# 查看使用空间
$ du -h --max-depth=1
```




# GitHub

```shell
$ git checkout branchname
$ git pull upstream branchname
$ git rebase upstream/branchname

$ git log    # q (exit)
$ git config --list
```



