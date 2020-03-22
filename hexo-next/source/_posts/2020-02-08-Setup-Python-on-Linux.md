---
title: Setup on Linux (Ubuntu, CentOS 7)
date: 2020-02-08 21:32:59
updated: 
categories:
  - Records
tags:
  - Configure
  - Linux
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
/home/eustomaqua/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/eustomaqua/anaconda3] >>> '/home/eustomaqua/Software/anaconda3
./Anaconda3-5.2.0-Linux-x86_64.sh: eval: line 301: unexpected EOF while looking for matching `''
./Anaconda3-5.2.0-Linux-x86_64.sh: eval: line 302: syntax error: unexpected end of file
PREFIX=/home/eustomaqua/anaconda3
installing: python-3.6.5-hc3d631a_2 ...
Python 3.6.5 :: Anaconda, Inc.
installing: blas-1.0-mkl ...



installing: anaconda-5.2.0-py36_3 ...
installation finished.
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/eustomaqua/.bashrc ? [yes|no]
[no] >>> yes

Appending source /home/eustomaqua/anaconda3/bin/activate to /home/eustomaqua/.bashrc
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

### conda

```bash
~/GitHubLab/ActivityNet/Crawler/Kinetics$ conda env create -f environment.yml
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.5.4
  latest version: 4.8.2

Please update conda by running

    $ conda update -n base conda



Downloading and Extracting Packages
ffmpeg-3.1.3         | 56.6 MB | ###9                                                        |   7%

CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://conda.anaconda.org/menpo/linux-64/ffmpeg-3.1.3-0.tar.bz2>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.



~/GitHubLab/ActivityNet/Crawler/Kinetics$ conda env create -f environment.yml
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.5.4
  latest version: 4.8.2

Please update conda by running

    $ conda update -n base conda



Downloading and Extracting Packages
ffmpeg-3.1.3         | 56.6 MB | 1                                                           |   0% ^Z
[2]+  Stopped                 conda env create -f environment.yml
~/GitHubLab/ActivityNet/Crawler/Kinetics$
~/GitHubLab/ActivityNet/Crawler/Kinetics$ nano ~/.condarc
~/GitHubLab/ActivityNet/Crawler/Kinetics$ nano ~/.condarc
~/GitHubLab/ActivityNet/Crawler/Kinetics$ vim ~/.condarc
~/GitHubLab/ActivityNet/Crawler/Kinetics$
~/GitHubLab/ActivityNet/Crawler/Kinetics$ conda env create -f environment.yml
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.5.4
  latest version: 4.8.2

Please update conda by running

    $ conda update -n base conda



Downloading and Extracting Packages
python-dateutil-2.6. |  232 KB | ########################################################### | 100%
joblib-0.9.4         |  121 KB | ########################################################### | 100%
readline-6.2         |  606 KB | ########################################################### | 100%
blas-1.0             |    6 KB | ########################################################### | 100%
wheel-0.29.0         |   81 KB | ########################################################### | 100%
python-2.7.13        | 11.5 MB | ########################################################### | 100%
tk-8.5.18            |  1.9 MB | ########################################################### | 100%
pip-9.0.1            |  1.6 MB | ########################################################### | 100%
six-1.10.0           |   16 KB | ########################################################### | 100%
pandas-0.19.2        | 15.3 MB | ########################################################### | 100%
numpy-1.12.1         |  6.6 MB | ########################################################### | 100%
ffmpeg-3.1.3         | 56.6 MB | ########################################################### | 100%
setuptools-27.2.0    |  521 KB | ########################################################### | 100%
zlib-1.2.8           |  101 KB | ########################################################### | 100%
mkl-2017.0.1         | 128.2 MB | ########################################################## | 100%
openssl-1.0.2k       |  3.2 MB | ########################################################### | 100%
sqlite-3.13.0        |  4.0 MB | ########################################################### | 100%
pytz-2017.2          |  204 KB | ########################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
Collecting decorator==4.0.11 (from -r /home/eustomaqua/GitHubLab/ActivityNet/Crawler/Kinetics/condaenv.1786bqps.requirements.txt (line 1))
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/00/cc/dd79ea98a0ff5a01d714c37eddd99cd0a71557113f1511921d1ef9a083b8/decorator-4.0.11-py2.py3-none-any.whl
Collecting olefile==0.44 (from -r /home/eustomaqua/GitHubLab/ActivityNet/Crawler/Kinetics/condaenv.1786bqps.requirements.txt (line 2))
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/35/17/c15d41d5a8f8b98cc3df25eb00c5cee76193114c78e5674df6ef4ac92647/olefile-0.44.zip (74kB)
    100% |████████████████████████████████| 81kB 1.1MB/s
Collecting youtube-dl==2017.6.5 (from -r /home/eustomaqua/GitHubLab/ActivityNet/Crawler/Kinetics/condaenv.1786bqps.requirements.txt (line 3))
  Cache entry deserialization failed, entry ignored
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/7d/87/4aa3ab6c0e2c4c0c840153bb311b3e749a4a3fb2ff828d757a456d0293f5/youtube_dl-2017.6.5-py2.py3-none-any.whl (1.6MB)
    100% |████████████████████████████████| 1.6MB 1.0MB/s
Building wheels for collected packages: olefile
  Running setup.py bdist_wheel for olefile ... done
  Stored in directory: /home/eustomaqua/.cache/pip/wheels/87/d1/0a/f210dcd910c1cbf0e20efaa6ab035aa20a5b80c989856a935e
Successfully built olefile
Installing collected packages: decorator, olefile, youtube-dl
Successfully installed decorator-4.0.11 olefile-0.44 youtube-dl-2017.6.5
#
# To activate this environment, use:
# > source activate kinetics
#
# To deactivate an active environment, use:
# > source deactivate
#

~/GitHubLab/ActivityNet/Crawler/Kinetics$ conda env list
# conda environments:
#
base                  *  /home/eustomaqua/anaconda3
autovu                   /home/eustomaqua/anaconda3/envs/autovu
kinetics                 /home/eustomaqua/anaconda3/envs/kinetics

~/GitHubLab/ActivityNet/Crawler/Kinetics$
```


### * refs

[Ubuntu安装anaconda 介绍、安装、配置](https://blog.csdn.net/haeasringnar/article/details/82079943)  
[ubuntu16.04安装和使用Anaconda3（详细）](https://blog.csdn.net/ITBigGod/article/details/85690257)  
[Python 环境](https://dl.ypw.io/python-environment/)  
[Python 环境 | 切换 anaconda 源](https://dl.ypw.io/python-environment/)  


## CUDA, cuDNN (NVIDIA Driver)

### check NVIDIA driver

```bash
~/Software$ nvidia-smi
Sat Feb  8 22:19:53 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 440.36       Driver Version: 440.36       CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
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
- // or
- // Download cuDNN v7.4.2 [Dec 14, 2018], for CUDA 10.0


### CUDA

install .run:  
```bash
~/Software$ ls
cuda_10.0.130_410.48_linux.run  cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
~/Software$ chmod +x cuda_10.0.130_410.48_linux.run
~/Software$ ./cuda_10.0.130_410.48_linux.run
Logging to /tmp/cuda_install_14812.log
Using more to view the EULA.
End User License Agreement
--------------------------

Preface
-------
The Software License Agreement in Chapter 1 and the Supplement
in Chapter 2 contain license terms and conditions that govern
the use of NVIDIA software. By accepting this agreement, you
agree to comply with all the terms and conditions applicable
to the product(s) included herein.

NVIDIA Driver
Description
This package contains the operating system driver and
fundamental system software components for NVIDIA GPUs.

NVIDIA CUDA Toolkit
Description



  20. Licensee's use of linmath.h header for CPU functions for
    GL vector/matrix operations from lunarG is subject to the
    Apache License Version 2.0.

-----------------
Do you accept the previously read EULA?
accept/decline/quit:

Do you accept the previously read EULA?
accept/decline/quit:
Do you accept the previously read EULA?
accept/decline/quit: yes
Do you accept the previously read EULA?
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

Installing the CUDA Toolkit in /home/eustomaqua/Software/cuda-10.0 ...
Missing recommended library: libGLU.so
Missing recommended library: libXi.so
Missing recommended library: libXmu.so

Installing the CUDA Samples in /home/eustomaqua/Software/cuda-samples ...
Copying samples to /home/eustomaqua/Software/cuda-samples/NVIDIA_CUDA-10.0_Samples now...
Finished copying samples.

===========
= Summary =
===========

Driver:   Not Selected
Toolkit:  Installed in /home/eustomaqua/Software/cuda-10.0
Samples:  Installed in /home/eustomaqua/Software/cuda-samples, but missing recommended libraries

Please make sure that
 -   PATH includes /home/eustomaqua/Software/cuda-10.0/bin
 -   LD_LIBRARY_PATH includes /home/eustomaqua/Software/cuda-10.0/lib64, or, add /home/eustomaqua/Software/cuda-10.0/lib64 to /etc/ld.so.conf and run ldconfig as root

To uninstall the CUDA Toolkit, run the uninstall script in /home/eustomaqua/Software/cuda-10.0/bin

Please see CUDA_Installation_Guide_Linux.pdf in /home/eustomaqua/Software/cuda-10.0/doc/pdf for detailed information on setting up CUDA.

***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 384.00 is required for CUDA 10.0 functionality to work.
To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
    sudo <CudaInstaller>.run -silent -driver

Logfile is /tmp/cuda_install_14812.log
~/Software$
```

config .bashrc:  
```bash
~/Software$ vim ~/.bashrc
~/Software$ source ~/.bashrc
~/Software$ nvidia-smi
Sat Feb  8 22:55:29 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 440.36       Driver Version: 440.36       CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+
```

end of .bashrc file:  
```bash
# added by Anaconda3 installer
export PATH="/home/eustomaqua/anaconda3/bin:$PATH"
# self added for Nvidia
export PATH=$HOME/Software/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/Software/cuda-10.0/lib64/
```


### cuDNN

```bash
~/Software$ ls
cuda-10.0                       cudnn-10.0-linux-x64-v7.4.2.24.solitairetheme8
cuda_10.0.130_410.48_linux.run  cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda-samples
~/Software$ cp cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8 cudnn-10.0-linux-x64-v7.6.4.38.tgz
~/Software$ tar -xvf cudnn-10.0-linux-x64-v7.6.4.38.tgz
cuda/include/cudnn.h
cuda/NVIDIA_SLA_cuDNN_Support.txt
cuda/lib64/libcudnn.so
cuda/lib64/libcudnn.so.7
cuda/lib64/libcudnn.so.7.6.4
cuda/lib64/libcudnn_static.a



~/Software$ ls
cuda                            cudnn-10.0-linux-x64-v7.4.2.24.solitairetheme8
cuda-10.0                       cudnn-10.0-linux-x64-v7.6.4.38.solitairetheme8
cuda_10.0.130_410.48_linux.run  cudnn-10.0-linux-x64-v7.6.4.38.tgz
cuda-samples
~/Software$
~/Software$ ls cuda
include  lib64  NVIDIA_SLA_cuDNN_Support.txt
~/Software$ ls cuda/include
cudnn.h
~/Software$ ls cuda/lib64
libcudnn.so  libcudnn.so.7  libcudnn.so.7.6.4  libcudnn_static.a
~/Software$



~/Software$ mv cuda/include/cudnn.h ~/Software/cuda-10.0/include/
~/Software$ mv cuda/lib64/libcudnn* ~/Software/cuda-10.0/lib64
~/Software$ chmod a+r ~/Software/cuda-10.0/include/cudnn.h ~/Software/cuda-10.0/lib64/libcudnn*
~/Software$

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

~/Software$



~/Software$ mv cuda/NVIDIA_SLA_cuDNN_Support.txt cuda-10.0/
~/Software$ rm -r cuda
~/Software$
```


### * refs

[How to check NVIDIA driver version on your Linux system](https://linuxconfig.org/how-to-check-nvidia-driver-version-on-your-linux-system)  
[2 Ways to Install Nvidia Driver on Ubuntu 18.04 (GUI & Command Line)](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)  


## Install Python Packages


### Expected packages

with Anaconda:  
```python
jupyter == 1.0.0
numpy == 1.14.3
pandas == 0.23.0
scikit-learn == 0.19.1
matplotlib == 2.2.2
Pillow == 5.1.0
seaborn == 0.8.1
```
custom:  
```python
opencv-python
tqdm
torch
torchvision
tensorflow-gpu
# keras
tensorboardX
```

### Before custom installation

```bash
~/Software$ cd ..
~$
~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import jupyter
>>> import numpy as np
>>> import pandas as pd
>>> import sklearn
>>> import matplotlib
>>> from PIL import Image
>>> import seaborn
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/matplotlib/font_manager.py:278: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
  'Matplotlib is building the font cache using fc-list. '
>>>
>>> np.__version__
'1.14.3'
>>> pd.__version__
'0.23.0'
>>> seaborn.__version__
'0.8.1'
>>>
[4]+  Stopped                 python
~$
~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import seaborn
>>>
[5]+  Stopped                 python
~$
```

### pip install

```bash
$
```

#### custom

```bash
~$ pip config global.index-url  # same as: pip config
Need an action (edit, get, list, set, unset) to perform.
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
~$ pip config list global.index-url
Got unexpected number of arguments, expected 0. (example: "pip config list")
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
~$
~$ pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
Writing to /home/eustomaqua/.config/pip/pip.conf
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.



~$ pip install opencv-python
Requirement already satisfied: numpy>=1.11.3 in ./anaconda3/lib/python3.6/site-packages (from opencv-python) (1.14.3)
distributed 1.21.8 requires msgpack, which is not installed.
Installing collected packages: opencv-python
Successfully installed opencv-python-4.2.0.32

~$ pip install tqdm
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Successfully installed tqdm-4.42.1
```


#### pytorch

```bash
~$ # pip install torch torchvision
~$ # pip install tensorboardX


~$ pip install torch==1.2.0 torchvision==0.4.0
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting torch==1.2.0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/30/57/d5cceb0799c06733eefce80c395459f28970ebb9e896846ce96ab579a3f1/torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl (748.8MB)
    100% |████████████████████████████████| 748.9MB 146kB/s
Collecting torchvision==0.4.0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/06/e6/a564eba563f7ff53aa7318ff6aaa5bd8385cbda39ed55ba471e95af27d19/torchvision-0.4.0-cp36-cp36m-manylinux1_x86_64.whl (8.8MB)
    100% |████████████████████████████████| 8.8MB 3.4MB/s
Requirement already satisfied: numpy in ./anaconda3/lib/python3.6/site-packages (from torch==1.2.0) (1.16.2)
Requirement already satisfied: pillow>=4.1.1 in ./anaconda3/lib/python3.6/site-packages (from torchvision==0.4.0) (5.1.0)
Requirement already satisfied: six in ./anaconda3/lib/python3.6/site-packages (from torchvision==0.4.0) (1.11.0)
Installing collected packages: torch, torchvision
Successfully installed torch-1.2.0 torchvision-0.4.0
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.


~$ pip install tensorboardX
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting tensorboardX
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/35/f1/5843425495765c8c2dd0784a851a93ef204d314fc87bcc2bbb9f662a3ad1/tensorboardX-2.0-py2.py3-none-any.whl (195kB)
    100% |████████████████████████████████| 204kB 2.4MB/s
Requirement already satisfied: six in ./anaconda3/lib/python3.6/site-packages (from tensorboardX) (1.11.0)
Requirement already satisfied: protobuf>=3.8.0 in ./anaconda3/lib/python3.6/site-packages (from tensorboardX) (3.11.3)
Requirement already satisfied: numpy in ./anaconda3/lib/python3.6/site-packages (from tensorboardX) (1.16.2)
Requirement already satisfied: setuptools in ./anaconda3/lib/python3.6/site-packages (from protobuf>=3.8.0->tensorboardX) (45.1.0)
Installing collected packages: tensorboardX
Successfully installed tensorboardX-2.0
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.


~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> import torchvision
>>> torch.cuda.is_available()
True
>>> from tensorboardX import SummaryWriter
>>>
[12]+  Stopped                 python
```



#### tensorflow-gpu

tensorflow-gpu 2.0.0-beta0  

(1) failed due to "install msgpack, wrapt"

```bash
~$ # pip install tensorflow-gpu  # keras
~$ pip install tensorflow-gpu==2.0.*
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting tensorflow-gpu==2.0.*
  Could not find a version that satisfies the requirement tensorflow-gpu==2.0.* (from versions: 0.12.1, 1.0.0, 1.0.1, 1.1.0rc1, 1.1.0rc2, 1.1.0, 1.2.0rc0, 1.2.0rc1, 1.2.0rc2, 1.2.0, 1.2.1, 1.3.0rc0, 1.3.0rc1, 1.3.0rc2, 1.3.0, 1.4.0rc0, 1.4.0rc1, 1.4.0, 1.4.1, 1.5.0rc0, 1.5.0rc1, 1.5.0, 1.5.1, 1.6.0rc0, 1.6.0rc1, 1.6.0, 1.7.0rc0, 1.7.0rc1, 1.7.0, 1.7.1, 1.8.0rc0, 1.8.0rc1, 1.8.0, 1.9.0rc0, 1.9.0rc1, 1.9.0rc2, 1.9.0, 1.10.0rc0, 1.10.0rc1, 1.10.0, 1.10.1, 1.11.0rc0, 1.11.0rc1, 1.11.0rc2, 1.11.0, 1.12.0rc0, 1.12.0rc1, 1.12.0rc2, 1.12.0, 1.12.2, 1.12.3, 1.13.0rc0, 1.13.0rc1, 1.13.0rc2, 1.13.1, 1.13.2, 1.14.0rc0, 1.14.0rc1, 1.14.0, 2.0.0a0, 2.0.0b0, 2.0.0b1)
No matching distribution found for tensorflow-gpu==2.0.*
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.


~$ pip install tensorflow-gpu==2.0.0b0
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting tensorflow-gpu==2.0.0b0
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/e8/7e/87c4c94686cda7066f52cbca4c344248516490acdd6b258ec6b8a805d956/tensorflow_gpu-2.0.0b0-cp36-cp36m-manylinux1_x86_64.whl (348.8MB)
Collecting protobuf>=3.6.1 (from tensorflow-gpu==2.0.0b0)
  Downloading protobuf-3.11.3-cp36-cp36m-manylinux1_x86_64.whl (1.3MB)
Collecting absl-py>=0.7.0 (from tensorflow-gpu==2.0.0b0)
  Downloading absl-py-0.9.0.tar.gz (104kB)
Collecting google-pasta>=0.1.6 (from tensorflow-gpu==2.0.0b0)
  Downloading google_pasta-0.1.8-py3-none-any.whl (57kB)
Collecting termcolor>=1.1.0 (from tensorflow-gpu==2.0.0b0)
  Downloading termcolor-1.1.0.tar.gz
Collecting keras-preprocessing>=1.0.5 (from tensorflow-gpu==2.0.0b0)
  Downloading Keras_Preprocessing-1.1.0-py2.py3-none-any.whl (41kB)
Collecting gast>=0.2.0 (from tensorflow-gpu==2.0.0b0)
  Downloading gast-0.3.3-py2.py3-none-any.whl
Collecting astor>=0.6.0 (from tensorflow-gpu==2.0.0b0)
  Downloading astor-0.8.1-py2.py3-none-any.whl
Collecting wrapt>=1.11.1 (from tensorflow-gpu==2.0.0b0)
  Downloading wrapt-1.11.2.tar.gz
Collecting keras-applications>=1.0.6 (from tensorflow-gpu==2.0.0b0)
  Downloading Keras_Applications-1.0.8-py3-none-any.whl (50kB)
Collecting grpcio>=1.8.6 (from tensorflow-gpu==2.0.0b0)
  Downloading grpcio-1.27.1-cp36-cp36m-manylinux1_x86_64.whl (2.7MB)
Collecting tf-estimator-nightly<1.14.0.dev2019060502,>=1.14.0.dev2019060501 (from tensorflow-gpu==2.0.0b0)
  Downloading tf_estimator_nightly-1.14.0.dev2019060501-py2.py3-none-any.whl (496kB)
Requirement already satisfied: wheel>=0.26 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.31.1)
Collecting tb-nightly<1.14.0a20190604,>=1.14.0a20190603 (from tensorflow-gpu==2.0.0b0)
  Downloading tb_nightly-1.14.0a20190603-py3-none-any.whl (3.1MB)
Collecting numpy<2.0,>=1.14.5 (from tensorflow-gpu==2.0.0b0)
  Downloading numpy-1.18.1-cp36-cp36m-manylinux1_x86_64.whl (20.1MB)
Requirement already satisfied: six>=1.10.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.11.0)
Requirement already satisfied: setuptools in ./anaconda3/lib/python3.6/site-packages (from protobuf>=3.6.1->tensorflow-gpu==2.0.0b0) (39.1.0)
Requirement already satisfied: h5py in ./anaconda3/lib/python3.6/site-packages (from keras-applications>=1.0.6->tensorflow-gpu==2.0.0b0) (2.7.1)
Collecting markdown>=2.6.8 (from tb-nightly<1.14.0a20190604,>=1.14.0a20190603->tensorflow-gpu==2.0.0b0)
  Downloading Markdown-3.2-py2.py3-none-any.whl (88kB)
Requirement already satisfied: werkzeug>=0.11.15 in ./anaconda3/lib/python3.6/site-packages (from tb-nightly<1.14.0a20190604,>=1.14.0a20190603->tensorflow-gpu==2.0.0b0) (0.14.1)
Building wheels for collected packages: absl-py, termcolor, wrapt
  Running setup.py bdist_wheel for absl-py ... done
  Stored in directory: /home/eustomaqua/.cache/pip/wheels/55/fd/b5/4db4cce08516c3aaa68ee4c843439f45c7fcf177320ba63d9f
  Running setup.py bdist_wheel for termcolor ... done
  Stored in directory: /home/eustomaqua/.cache/pip/wheels/e3/d8/fc/50ab6e66e3dead21d5afff006dc5298913a3064be2b1105359
  Running setup.py bdist_wheel for wrapt ... done
  Stored in directory: /home/eustomaqua/.cache/pip/wheels/48/31/f6/4ebf38e9000388204ef6f1931a0cd48f9d75a12a9c6a328cfd
Successfully built absl-py termcolor wrapt
distributed 1.21.8 requires msgpack, which is not installed.
tb-nightly 1.14.0a20190603 has requirement setuptools>=41.0.0, but you'll have setuptools 39.1.0 which is incompatible.
Installing collected packages: protobuf, absl-py, google-pasta, termcolor, numpy, keras-preprocessing, gast, astor, wrapt, keras-applications, grpcio, tf-estimator-nightly, markdown, tb-nightly, tensorflow-gpu
  Found existing installation: numpy 1.14.3
    Uninstalling numpy-1.14.3:
      Successfully uninstalled numpy-1.14.3
  Found existing installation: wrapt 1.10.11
Cannot uninstall 'wrapt'. It is a distutils installed project and thus we cannot accurately determine which files belong to it which would lead to only a partial uninstall.
```

(2) succeed install, faile import

```bash
~$ pip install msgpack
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting msgpack
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/3d/a8/e01fea81691749044a7bfd44536483a296d9c0a7ed4ec8810a229435547c/msgpack-0.6.2-cp36-cp36m-manylinux1_x86_64.whl (249kB)
    100% |████████████████████████████████| 256kB 3.6MB/s
Installing collected packages: msgpack
Successfully installed msgpack-0.6.2
~$ pip install --ignore-installed wrapt
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting wrapt
Installing collected packages: wrapt
Successfully installed wrapt-1.11.2
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
~$
```

```bash
~$ pip install tensorflow-gpu==2.0.0b0
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting tensorflow-gpu==2.0.0b0
  Downloading tensorflow_gpu-2.0.0b0-cp36-cp36m-manylinux1_x86_64.whl (348.8MB)
    100% |████████████████████████████████| 348.9MB 296kB/s
Collecting grpcio>=1.8.6 (from tensorflow-gpu==2.0.0b0)
  Downloading grpcio-1.27.1-cp36-cp36m-manylinux1_x86_64.whl (2.7MB)
    100% |████████████████████████████████| 2.7MB 13.3MB/s
Requirement already satisfied: google-pasta>=0.1.6 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.1.8)
Requirement already satisfied: gast>=0.2.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.3.3)
Requirement already satisfied: numpy<2.0,>=1.14.5 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.18.1)
Collecting tb-nightly<1.14.0a20190604,>=1.14.0a20190603 (from tensorflow-gpu==2.0.0b0)
  Downloading tb_nightly-1.14.0a20190603-py3-none-any.whl (3.1MB)
    100% |████████████████████████████████| 3.1MB 34.7MB/s
Requirement already satisfied: protobuf>=3.6.1 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (3.11.3)
Requirement already satisfied: termcolor>=1.1.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.1.0)
Requirement already satisfied: absl-py>=0.7.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.9.0)
Collecting keras-applications>=1.0.6 (from tensorflow-gpu==2.0.0b0)
  Downloading Keras_Applications-1.0.8-py3-none-any.whl (50kB)
    100% |████████████████████████████████| 51kB 27.3MB/s
Requirement already satisfied: wheel>=0.26 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.31.1)
Requirement already satisfied: six>=1.10.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.11.0)
Requirement already satisfied: astor>=0.6.0 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (0.8.1)
Requirement already satisfied: wrapt>=1.11.1 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.11.2)
Requirement already satisfied: keras-preprocessing>=1.0.5 in ./anaconda3/lib/python3.6/site-packages (from tensorflow-gpu==2.0.0b0) (1.1.0)
Collecting tf-estimator-nightly<1.14.0.dev2019060502,>=1.14.0.dev2019060501 (from tensorflow-gpu==2.0.0b0)
  Downloading tf_estimator_nightly-1.14.0.dev2019060501-py2.py3-none-any.whl (496kB)
    100% |████████████████████████████████| 501kB 12.7MB/s
Collecting markdown>=2.6.8 (from tb-nightly<1.14.0a20190604,>=1.14.0a20190603->tensorflow-gpu==2.0.0b0)
  Downloading Markdown-3.2-py2.py3-none-any.whl (88kB)
    100% |████████████████████████████████| 92kB 16.3MB/s
Collecting setuptools>=41.0.0 (from tb-nightly<1.14.0a20190604,>=1.14.0a20190603->tensorflow-gpu==2.0.0b0)
  Downloading setuptools-45.1.0-py3-none-any.whl (583kB)
    100% |████████████████████████████████| 593kB 28.1MB/s
Requirement already satisfied: werkzeug>=0.11.15 in ./anaconda3/lib/python3.6/site-packages (from tb-nightly<1.14.0a20190604,>=1.14.0a20190603->tensorflow-gpu==2.0.0b0) (0.14.1)
Requirement already satisfied: h5py in ./anaconda3/lib/python3.6/site-packages (from keras-applications>=1.0.6->tensorflow-gpu==2.0.0b0) (2.7.1)
Installing collected packages: grpcio, setuptools, markdown, tb-nightly, keras-applications, tf-estimator-nightly, tensorflow-gpu
  Found existing installation: setuptools 39.1.0
    Uninstalling setuptools-39.1.0:
      Successfully uninstalled setuptools-39.1.0
Successfully installed grpcio-1.27.1 keras-applications-1.0.8 markdown-3.2 setuptools-45.1.0 tb-nightly-1.14.0a20190603 tensorflow-gpu-2.0.0b0 tf-estimator-nightly-1.14.0.dev2019060501
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

```bash
~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/h5py/__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
>>>
[7]+  Stopped                 python
```

(3) warning import

```bash
~$ pip install numpy==1.16.2
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting numpy==1.16.2
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/35/d5/4f8410ac303e690144f0a0603c4b8fd3b986feb2749c435f7cdbb288f17e/numpy-1.16.2-cp36-cp36m-manylinux1_x86_64.whl (17.3MB)
    100% |████████████████████████████████| 17.3MB 2.2MB/s
Installing collected packages: numpy
  Found existing installation: numpy 1.18.1
    Uninstalling numpy-1.18.1:
      Successfully uninstalled numpy-1.18.1
Successfully installed numpy-1.16.2
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.

~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
/home/eustomaqua/anaconda3/lib/python3.6/site-packages/h5py/__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
>>>
[8]+  Stopped                 python
```

(4) succeed import, failed no cuda

```bash
~$ pip install -U h5py
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting h5py
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/60/06/cafdd44889200e5438b897388f3075b52a8ef01f28a17366d91de0fa2d05/h5py-2.10.0-cp36-cp36m-manylinux1_x86_64.whl (2.9MB)
    100% |████████████████████████████████| 2.9MB 13.5MB/s
Requirement not upgraded as not directly required: numpy>=1.7 in ./anaconda3/lib/python3.6/site-packages (from h5py) (1.16.2)
Requirement not upgraded as not directly required: six in ./anaconda3/lib/python3.6/site-packages (from h5py) (1.11.0)
Installing collected packages: h5py
  Found existing installation: h5py 2.7.1
    Uninstalling h5py-2.7.1:
      Successfully uninstalled h5py-2.7.1
Successfully installed h5py-2.10.0
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.

~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> tf.test.is_gpu_available()
2020-02-08 23:52:36.691031: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2020-02-08 23:52:36.706948: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcuda.so.1
2020-02-08 23:52:36.853793: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-08 23:52:36.854165: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55f4173381e0 executing computations on platform CUDA. Devices:
2020-02-08 23:52:36.854183: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): GeForce RTX 2070 SUPER, Compute Capability 7.5
2020-02-08 23:52:36.873251: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3600000000 Hz
2020-02-08 23:52:36.873745: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55f417727de0 executing computations on platform Host. Devices:
2020-02-08 23:52:36.873759: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): <undefined>, <undefined>
2020-02-08 23:52:36.873898: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-08 23:52:36.874134: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1640] Found device 0 with properties:
name: GeForce RTX 2070 SUPER major: 7 minor: 5 memoryClockRate(GHz): 1.8
pciBusID: 0000:01:00.0
2020-02-08 23:52:36.874223: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcudart.so.10.0'; dlerror: libcudart.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874269: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcublas.so.10.0'; dlerror: libcublas.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874312: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874353: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874395: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcusolver.so.10.0'; dlerror: libcusolver.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874435: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcusparse.so.10.0'; dlerror: libcusparse.so.10.0: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874476: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Could not dlopen library 'libcudnn.so.7'; dlerror: libcudnn.so.7: cannot open shared object file: No such file or directory
2020-02-08 23:52:36.874484: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1663] Cannot dlopen some GPU libraries. Skipping registering GPU devices...
2020-02-08 23:52:36.874494: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1181] Device interconnect StreamExecutor with strength 1 edge matrix:
2020-02-08 23:52:36.874499: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1187]      0
2020-02-08 23:52:36.874504: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1200] 0:   N
False
>>>
[9]+  Stopped                 python
```

(5) succeed


**错因：** 之前的 LD_LIBRARY_PATH 误写成 LD_LIBARAY_PATH 了  
错误写法：  export LD_LIBARAY_PATH=$LD_LIBRARY_PATH:$HOME/Software/cuda-10.0/lib64/  
正确写法：  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/Software/cuda-10.0/lib64/  



```bash
~$ LD_LIBRARY_PATH
LD_LIBRARY_PATH: command not found
~$ source ~/.bashrc
~$ vim ~/.bashrc
~$ source ~/.bashrc
~$ LD_LIBRARY_PATH
LD_LIBRARY_PATH: command not found
~$
~$
~$
~$ vim ~/.bashrc
~$ source ~/.bashrc
~$ PATH
PATH: command not found
~$ echo PATH
PATH
~$ echo $PATH
/home/eustomaqua/Software/cuda-10.0/bin:/home/eustomaqua/anaconda3/bin:/home/eustomaqua/Software/cuda-10.0/bin:/home/eustomaqua/anaconda3/bin:/home/eustomaqua/Software/cuda-10.0/bin:/home/eustomaqua/anaconda3/bin:/home/eustomaqua/Software/cuda-10.0/bin:/home/eustomaqua/anaconda3/bin:/home/eustomaqua/Software/cuda-10.0/bin:/home/eustomaqua/anaconda3/bin:/home/eustomaqua/anaconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
~$ echo $LD_LIBRARY_PATH
:/home/eustomaqua/Software/cuda-10.0/lib64/:/home/eustomaqua/Software/cuda-10.0/lib64/

~$ python
Python 3.6.5 |Anaconda, Inc.| (default, Apr 29 2018, 16:14:56)
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> tf.test.is_gpu_available()
2020-02-09 00:08:17.326460: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2020-02-09 00:08:17.343444: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcuda.so.1
2020-02-09 00:08:17.381171: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.381486: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55d5564a5150 executing computations on platform CUDA. Devices:
2020-02-09 00:08:17.381501: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): GeForce RTX 2070 SUPER, Compute Capability 7.5
2020-02-09 00:08:17.405235: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3600000000 Hz
2020-02-09 00:08:17.405621: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55d556894ab0 executing computations on platform Host. Devices:
2020-02-09 00:08:17.405633: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): <undefined>, <undefined>
2020-02-09 00:08:17.405743: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.405958: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1640] Found device 0 with properties:
name: GeForce RTX 2070 SUPER major: 7 minor: 5 memoryClockRate(GHz): 1.8
pciBusID: 0000:01:00.0
2020-02-09 00:08:17.406103: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcudart.so.10.0
2020-02-09 00:08:17.406736: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcublas.so.10.0
2020-02-09 00:08:17.407325: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcufft.so.10.0
2020-02-09 00:08:17.407470: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcurand.so.10.0
2020-02-09 00:08:17.408220: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcusolver.so.10.0
2020-02-09 00:08:17.408804: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcusparse.so.10.0
2020-02-09 00:08:17.410651: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcudnn.so.7
2020-02-09 00:08:17.410718: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.410960: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.411148: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1763] Adding visible gpu devices: 0
2020-02-09 00:08:17.411170: I tensorflow/stream_executor/platform/default/dso_loader.cc:42] Successfully opened dynamic library libcudart.so.10.0
2020-02-09 00:08:17.411687: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1181] Device interconnect StreamExecutor with strength 1 edge matrix:
2020-02-09 00:08:17.411696: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1187]      0
2020-02-09 00:08:17.411700: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1200] 0:   N
2020-02-09 00:08:17.414113: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.414336: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1006] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-02-09 00:08:17.414546: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1326] Created TensorFlow device (/device:GPU:0 with 7014 MB memory) -> physical GPU (device: 0, name: GeForce RTX 2070 SUPER, pci bus id: 0000:01:00.0, compute capability: 7.5)
True
>>>
[13]+  Stopped                 python
```

### refs

[安装Tensorlayer报错“Cannot uninstall 'xxx'"的解决方案](https://blog.csdn.net/u012654847/article/details/80875838)  
[FutureWarning: Deprecated numpy API calls in tf.python.framework.dtypes](https://github.com/tensorflow/tensorflow/issues/30427)  
[FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated](https://github.com/h5py/h5py/issues/961)  

[TensorFlow Official: GPU support](https://www.tensorflow.org/install/gpu)  
[ImportError: libcudnn.so.7: cannot open shared object file: No such file or directory](https://github.com/tensorflow/tensorflow/issues/20271)  
[【UBUNTU深度学习环境】ImportError: libcudnn.so.7: cannot open shared object file: No such file or directory](https://blog.csdn.net/weixin_40298200/article/details/79420758)  

[PyTorch使用tensorboardX](https://zhuanlan.zhihu.com/p/35675109)  
[Pytorch使用tensorboardX可视化。超详细！！！](https://www.jianshu.com/p/46eb3004beca)  
[官方总结 tensorboardX 使用教程](https://blog.csdn.net/qq_39575835/article/details/89160828)  

[ubuntu 18.04 + Tensorflow-gpu 2.0环境搭建](https://zhuanlan.zhihu.com/p/77385238)  
[TensorFlow 2.0 Alpha的初步尝试：安装及填坑小记](https://zhuanlan.zhihu.com/p/61296818)  



## Issue: ssh 新终端必须先 source .bashrc 才能正常用自己的 python

important:  
[社区环境搭建 使用ssh登入ubuntu不执行.bashrc解决方法](https://qjzd.net/topic/56777682984f90d869bd23fc)  

open a terminal:  
```bash
vim ~/.bash_profile
```

in .bash_profile file:  
```bash
# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
        . "$HOME/.bashrc"
    fi
fi
```

new terminal:
```bash
python
```

refs:  
[ubuntu 用户修改.bashrc之后，每次登录需要运行source命令才生效](https://blog.51cto.com/xjhznick/1399938)  
[解决.bashrc文件每次打开终端都需要source的问题](https://www.jianshu.com/p/c4946024b946)  
[ubuntu12.04 .bashrc设置后无效](https://blog.csdn.net/heybob/article/details/8899703)  



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



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git add .
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git commit -m "annotations"  # 注释
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ cd ..
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 1 个提交。
  （使用 "git push" 来发布您的本地提交）
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git checkout -- <文件>..." 丢弃工作区的改动）

  修改：     hexo-next/source/_posts/2020-02-08-Setup-Python-on-Linux.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git add .
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git commit -m "config done on gpu"
[hexo-next 10c854a] config done on gpu
 1 file changed, 724 insertions(+), 18 deletions(-)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
warning: push.default 尚未设置，它的默认值在 Git 2.0 已从 'matching'
变更为 'simple'。若要不再显示本信息并保持传统习惯，进行如下设置：

  git config --global push.default matching

若要不再显示本信息并从现在开始采用新的使用习惯，设置：

  git config --global push.default simple

当 push.default 设置为 'matching' 后，git 将推送和远程同名的所有
本地分支。

从 Git 2.0 开始，Git 默认采用更为保守的 'simple' 模式，只推送当前
分支到远程关联的同名分支，即 'git push' 推送当前分支。

参见 'git help config' 并查找 'push.default' 以获取更多信息。
（'simple' 模式由 Git 1.7.11 版本引入。如果您有时要使用老版本的 Git，
为保持兼容，请用 'current' 代替 'simple'）

Username for 'https://github.com': eustomaqua
Password for 'https://eustomaqua@github.com': 
对象计数中: 13, 完成.
Delta compression using up to 2 threads.
压缩对象中: 100% (13/13), 完成.
写入对象中: 100% (13/13), 15.88 KiB | 0 bytes/s, 完成.
Total 13 (delta 8), reused 0 (delta 0)
remote: Resolving deltas: 100% (8/8), completed with 4 local objects.
To https://github.com/eustomaqua/eustomaqua.github.io.git
   480734a..10c854a  hexo-next -> hexo-next
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config
用法：git config [<选项>]

配置文件位置
    --global              使用全局配置文件
    --system              使用系统级配置文件
    --local               使用仓库级配置文件
    -f, --file <文件>     使用指定的配置文件
    --blob <数据对象 ID>  从给定的数据对象读取配置

操作
    --get                 获取值：name [value-regex]
    --get-all             获得所有的值：key [value-regex]
    --get-regexp          根据正则表达式获得值：name-regex [value-regex]
    --get-urlmatch        获得 URL 取值：section[.var] URL
    --replace-all         替换所有匹配的变量：name value [value_regex]
    --add                 添加一个新的变量：name value
    --unset               删除一个变量：name [value-regex]
    --unset-all           删除所有匹配项：name [value-regex]
    --rename-section      重命名小节：old-name new-name
    --remove-section      删除一个小节：name
    -l, --list            列出所有
    -e, --edit            打开一个编辑器
    --get-color           获得配置的颜色：配置 [默认]
    --get-colorbool       获得颜色设置：配置 [stdout-is-tty]

类型
    --bool                值是 "true" 或 "false"
    --int                 值是十进制数
    --bool-or-int         值是 --bool or --int
    --path                值是一个路径（文件或目录名）

其它
    -z, --null            终止值是 NUL 字节
    --name-only           只显示变量名
    --includes            查询时参照 include 指令递归查找

ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config push.default
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config --global push.default simple
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
```

post notes

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ hexo g
Usage: hexo <command>

Commands:
  help     Get help on a command.
  init     Create a new Hexo folder.
  version  Display version information.

Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ ls
hexo-next  README.md
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ cd hexo-next
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g  # 生成
INFO  Start processing
INFO  Files loaded in 3.29 s
INFO  Generated: search.xml
INFO  Generated: categories/index.html
INFO  Generated: ....
INFO  114 files generated in 5.96 s
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo s  # 本地预览
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
^CINFO  Farewell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo d  # 发布

ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
INFO  Files loaded in 5.74 s
INFO  Generated: 2020/2020-02-08-Setup-Python-on-Linux/index.html
INFO  Generated: search.xml
INFO  Generated: index.html
INFO  3 files generated in 9.83 s
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git add .
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git commit -m "backup history"
[hexo-next 2b17507] backup history
 1 file changed, 51 insertions(+)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ cd hex*
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ ls
_config.yml  debug.log     package.json       public     source
db.json      node_modules  package-lock.json  scaffolds  themes
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
INFO  Files loaded in 2.62 s
INFO  Generated: search.xml
INFO  Generated: 2020/2020-02-08-Setup-Python-on-Linux/index.html
INFO  Generated: index.html
INFO  3 files generated in 6.39 s
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo d
INFO  Deploying: git
INFO  Clearing .deploy_git folder...
INFO  Copying files from public folder...
INFO  Copying files from extend dirs...
[master c64205a] updated on Sat, 02/08/2020
 36 files changed, 3796 insertions(+), 79 deletions(-)
 create mode 100644 2020/2020-02-08-Setup-Python-on-Linux/index.html
 create mode 100644 archives/2020/02/index.html
 create mode 100644 archives/2020/index.html
Username for 'https://github.com': eustomaqua
Password for 'https://eustomaqua@github.com': 
To https://github.com/eustomaqua/eustomaqua.github.io.git
   df22d0c..c64205a  HEAD -> master
分支 master 设置为跟踪来自 https://github.com/eustomaqua/eustomaqua.github.io.git 的远程分支 master。
INFO  Deploy done: git
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

