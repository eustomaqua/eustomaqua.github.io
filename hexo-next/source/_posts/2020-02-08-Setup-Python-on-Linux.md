---
title: Setup on Linux (Ubuntu, CentOS 7)
date: 2020-02-08 21:32:59
updated: 
categories:
  - Records
tags:
  - Configure
---


[TOC]


```bash
$ cd ~
$ ls
$
$ mkdir Software
$ # upload Anaconda*.sh
```

## Operation System

### Ubuntu

```bash
$ # 发行版本号 (a,b)
$ cat /etc/issue
Ubuntu 18.04.3 LTS \n \l
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.3 LTS
Release:        18.04
Codename:       bionic
$ # 查看内核版本号
$ uname -r
5.0.0-37-generic
```

```bash
$ cat /etc/issue
Ubuntu 16.04.4 LTS \n \l

$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.4 LTS
Release:    16.04
Codename:   xenial
$ uname -r
4.15.0-55-generic
$ uname -a
Linux ubuntu-VirtualBox 4.15.0-55-generic #60~16.04.2-Ubuntu SMP Thu Jul 4 09:03:09 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
$ getconf LONG_BIT
64
```

### Cent OS

```bash
$ # 查看 Cent OS 系统版本
$ cat /etc/redhat-release
CentOS release 6.10 (Final)
$ # 1) 查看内核版本
$ cat  /proc/version
Linux version 2.6.32-754.14.2.el6.x86_64 (mockbuild@x86-01.bsys.centos.org) (gcc version 4.4.7 20120313 (Red Hat 4.4.7-23) (GCC) ) #1 SMP Tue May 14 19:35:42 UTC 2019
$ # 2) 显示系统名、节点名称、操作系统的发行版号、操作系统版本、运行系统的机器 ID 号
$ uname -a
Linux ubri01 2.6.32-754.14.2.el6.x86_64 #1 SMP Tue May 14 19:35:42 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
$ # 3) 显示操作系统的发行版号
$ uname -r
2.6.32-754.14.2.el6.x86_64

$ # 查看linux版本
$ # 1) 列出所有版本信息
$ # 注: 这个命令适用于所有的linux，包括Redhat、SuSE、Debian等发行版。
$ lsb_release -a
LSB Version:    :base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
Distributor ID: CentOS
Description:    CentOS release 6.10 (Final)
Release:        6.10
Codename:       Final
$ cat /etc/issue
CentOS release 6.10 (Final)
Kernel \r on an \m
$ cat /etc/redhat-release
CentOS release 6.10 (Final)

$ # 查看系统是64位还是32位
$ getconf LONG_BIT
64
$ file /bin/ls
/bin/ls: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.18, stripped

$ # centos查看系统cpu个数、核心数、线程数
$ # 1. 查看物理cpu个数
$ grep 'physical id' /proc/cpuinfo | sort -u | wc -l
2
$ # 2. 查看核心数量，即每个物理CPU中core的个数(即核数)
$ grep 'core id' /proc/cpuinfo | sort -u | wc -l
14
$ # 3. 查看线程数（逻辑CPU的个数）
$ grep 'processor' /proc/cpuinfo | sort -u | wc -l
56
$ # 4.查看cpu型号
$ dmidecode -s processor-version
/dev/mem: Permission denied
$ # 5.查看内存方法
$ grep MemTotal /proc/meminfo
MemTotal:       132067272 kB
```

### * refs

[如何查看ubuntu的内核版本和发行版本号？](https://blog.csdn.net/debug_cpp/article/details/2687067)  
[centos系统查看系统版本、内核版本、系统位数、cpu个数、核心数、线程数](https://blog.csdn.net/u011630575/article/details/51426429)


## Anaconda, Python

### Anaconda

Download:  
[mirrors.thu](https://mirrors.tuna.tsinghua.edu.cn/news/restore-anaconda/)  
[Anaconda3-5.2.0-Linux-x86_64.sh](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)

Install:  
```bash
~$ cd ~/Software
~/Software$ ./Anaconda3-5.2.0-Linux-x86_64.sh
-bash: ./Anaconda3-5.2.0-Linux-x86_64.sh: Permission denied
$ bash ./Anaconda3-5.2.0-Linux-x86_64.sh

Welcome to Anaconda3 5.2.0

In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
>>>



>>> Please answer 'yes' or 'no':'
>>> yes

Anaconda3 will now be installed into this location:
/home/yjbian/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/yjbian/anaconda3] >>> '/home/yjbian/Software/anaconda3
./Anaconda3-5.2.0-Linux-x86_64.sh: eval: line 301: unexpected EOF while looking for matching `''
./Anaconda3-5.2.0-Linux-x86_64.sh: eval: line 302: syntax error: unexpected end of file
PREFIX=/home/yjbian/anaconda3
installing: python-3.6.5-hc3d631a_2 ...
Python 3.6.5 :: Anaconda, Inc.
installing: blas-1.0-mkl ...



installing: anaconda-5.2.0-py36_3 ...
installation finished.
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/yjbian/.bashrc ? [yes|no]
[no] >>> yes

Appending source /home/yjbian/anaconda3/bin/activate to /home/yjbian/.bashrc
A backup will be made to: /home/yjbian/.bashrc-anaconda3.bak


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
>>> yes
Proceeding with installation of Microsoft VSCode
VSCode is already installed!
~/Software$



~/Software$
~/Software$ python
Python 2.7.17 (default, Nov  7 2019, 10:07:09)
[GCC 7.4.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
[1]+  Stopped                 python
~/Software$ source ~/.bashrc
~/Software$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
[2]+  Stopped                 python
~/Software$
~/Software$ pip list
Package                            Version
---------------------------------- ---------
alabaster                          0.7.10
anaconda-client                    1.6.14
anaconda-navigator                 1.8.7
anaconda-project                   0.8.2
asn1crypto                         0.24.0
astroid                            1.6.3
astropy                            3.0.2
attrs                              18.1.0
Babel                              2.5.3
backcall                           0.1.0
backports.shutil-get-terminal-size 1.0.0
beautifulsoup4                     4.6.0
bitarray                           0.8.1
bkcharts                           0.2
blaze                              0.11.3
bleach                             2.1.3
bokeh                              0.12.16
boto                               2.48.0
Bottleneck                         1.2.1
certifi                            2018.4.16
cffi                               1.11.5
chardet                            3.0.4
click                              6.7
cloudpickle                        0.5.3
clyent                             1.2.2
colorama                           0.3.9
conda                              4.5.4
conda-build                        3.10.5
conda-verify                       2.0.0
contextlib2                        0.5.5
cryptography                       2.2.2
cycler                             0.10.0
Cython                             0.28.2
cytoolz                            0.9.0.1
dask                               0.17.5
datashape                          0.5.4
decorator                          4.3.0
distributed                        1.21.8
docutils                           0.14
entrypoints                        0.2.3
et-xmlfile                         1.0.1
fastcache                          1.0.2
filelock                           3.0.4
Flask                              1.0.2
Flask-Cors                         3.0.4
gevent                             1.3.0
glob2                              0.6
gmpy2                              2.0.8
greenlet                           0.4.13
h5py                               2.7.1
heapdict                           1.0.0
html5lib                           1.0.1
idna                               2.6
imageio                            2.3.0
imagesize                          1.0.0
ipykernel                          4.8.2
ipython                            6.4.0
ipython-genutils                   0.2.0
ipywidgets                         7.2.1
isort                              4.3.4
itsdangerous                       0.24
jdcal                              1.4
jedi                               0.12.0
Jinja2                             2.10
jsonschema                         2.6.0
jupyter                            1.0.0
jupyter-client                     5.2.3
jupyter-console                    5.2.0
jupyter-core                       4.4.0
jupyterlab                         0.32.1
jupyterlab-launcher                0.10.5
kiwisolver                         1.0.1
lazy-object-proxy                  1.3.1
llvmlite                           0.23.1
locket                             0.2.0
lxml                               4.2.1
MarkupSafe                         1.0
matplotlib                         2.2.2
mccabe                             0.6.1
mistune                            0.8.3
mkl-fft                            1.0.0
mkl-random                         1.0.1
more-itertools                     4.1.0
mpmath                             1.0.0
msgpack-python                     0.5.6
multipledispatch                   0.5.0
navigator-updater                  0.2.1
nbconvert                          5.3.1
nbformat                           4.4.0
networkx                           2.1
nltk                               3.3
nose                               1.3.7
notebook                           5.5.0
numba                              0.38.0
numexpr                            2.6.5
numpy                              1.14.3
numpydoc                           0.8.0
odo                                0.5.1
olefile                            0.45.1
openpyxl                           2.5.3
packaging                          17.1
pandas                             0.23.0
pandocfilters                      1.4.2
parso                              0.2.0
partd                              0.3.8
path.py                            11.0.1
pathlib2                           2.3.2
patsy                              0.5.0
pep8                               1.7.1
pexpect                            4.5.0
pickleshare                        0.7.4
Pillow                             5.1.0
pip                                10.0.1
pkginfo                            1.4.2
pluggy                             0.6.0
ply                                3.11
prompt-toolkit                     1.0.15
psutil                             5.4.5
ptyprocess                         0.5.2
py                                 1.5.3
pycodestyle                        2.4.0
pycosat                            0.6.3
pycparser                          2.18
pycrypto                           2.6.1
pycurl                             7.43.0.1
pyflakes                           1.6.0
Pygments                           2.2.0
pylint                             1.8.4
pyodbc                             4.0.23
pyOpenSSL                          18.0.0
pyparsing                          2.2.0
PySocks                            1.6.8
pytest                             3.5.1
pytest-arraydiff                   0.2
pytest-astropy                     0.3.0
pytest-doctestplus                 0.1.3
pytest-openfiles                   0.3.0
pytest-remotedata                  0.2.1
python-dateutil                    2.7.3
pytz                               2018.4
PyWavelets                         0.5.2
PyYAML                             3.12
pyzmq                              17.0.0
QtAwesome                          0.4.4
qtconsole                          4.3.1
QtPy                               1.4.1
requests                           2.18.4
rope                               0.10.7
ruamel-yaml                        0.15.35
scikit-image                       0.13.1
scikit-learn                       0.19.1
scipy                              1.1.0
seaborn                            0.8.1
Send2Trash                         1.5.0
setuptools                         39.1.0
simplegeneric                      0.8.1
singledispatch                     3.4.0.3
six                                1.11.0
snowballstemmer                    1.2.1
sortedcollections                  0.6.1
sortedcontainers                   1.5.10
Sphinx                             1.7.4
sphinxcontrib-websupport           1.0.1
spyder                             3.2.8
SQLAlchemy                         1.2.7
statsmodels                        0.9.0
sympy                              1.1.1
tables                             3.4.3
tblib                              1.3.2
terminado                          0.8.1
testpath                           0.3.1
toolz                              0.9.0
tornado                            5.0.2
traitlets                          4.3.2
typing                             3.6.4
unicodecsv                         0.14.1
urllib3                            1.22
wcwidth                            0.1.7
webencodings                       0.5.1
Werkzeug                           0.14.1
wheel                              0.31.1
widgetsnbextension                 3.2.1
wrapt                              1.10.11
xlrd                               1.1.0
XlsxWriter                         1.0.4
xlwt                               1.3.0
zict                               0.1.3
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
~/Software$
```


### Python

```bash
~/Software$ rm -r Anaconda3-5.2.0-Linux-x86_64.sh
$
$ pip install packages
$ pip install -U packages # pip install packages --upgrade
$ pip uninstall packages
```

```bash
$ # 使用 Anaconda 创建其他 Python 环境
$ conda create -n python2 python=2.7
$ source activate python2
$
$ # 切换 pip 源
$ # 如果遇到网络问题，可以使用清华大学的镜像：
$ pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```


### * refs

[Ubuntu安装anaconda 介绍、安装、配置](https://blog.csdn.net/haeasringnar/article/details/82079943)  
[ubuntu16.04安装和使用Anaconda3（详细）](https://blog.csdn.net/ITBigGod/article/details/85690257)  
[Python 环境](https://dl.ypw.io/python-environment/)  


## CUDA, cuDNN (NVIDIA Driver)

### check NVIDIA driver

```bash
~/Software$ nvidia-smi
Sat Feb  8 22:19:53 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 440.36       Driver Version: 440.36       CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce RTX 207...  Off  | 00000000:01:00.0 Off |                  N/A |
|  0%   37C    P8    20W / 215W |    386MiB /  7979MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1155      G   /usr/lib/xorg/Xorg                            57MiB |
|    0      1505      G   /usr/lib/xorg/Xorg                            24MiB |
|    0      6744      G   /usr/bin/gnome-shell                         220MiB |
|    0     28250      G   /usr/bin/gnome-shell                          81MiB |
+-----------------------------------------------------------------------------+
~/Software$
```


### Download

**Download CUDA Archive:**  
[CUDA Toolkit 10.0 Archive](https://developer.nvidia.com/cuda-10.0-download-archive)  

*Select Target Platform:*  
Click: Operating System, Architecture, Distribution, Version, Installer Type  
1) Linux, x86_64, Ubuntu, 18.04, runfile (local)  
2) Linux, x86_64, CentOS, 7, runfile (local)  

*Download Installers for Linux ....:*  
Base Installer (Download)

**Download cuDNN Archive:**  
[cuDNN latest](https://developer.nvidia.com/cudnn)  
[cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)  

Download cuDNN v7.6.4 [September 27, 2019], for CUDA 10.0  
- cuDNN Library for Linux

### CUDA

### cuDNN


### * refs

[How to check NVIDIA driver version on your Linux system](https://linuxconfig.org/how-to-check-nvidia-driver-version-on-your-linux-system)  
[2 Ways to Install Nvidia Driver on Ubuntu 18.04 (GUI & Command Line)](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)  


## Install Python Packages

### pip install

```bash
$
```


## References

### update posts

save codes

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支与上游分支 'origin/hexo-next' 一致。
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git checkout -- <文件>..." 丢弃工作区的改动）

    修改：     hexo-next/source/_posts/2019-07-20-Kindle-SignIn-WordWise.md

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

    hexo-next/source/_posts/2020-02-08-Setup-Python-on-Linux.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
```

post notes

```bash

```

