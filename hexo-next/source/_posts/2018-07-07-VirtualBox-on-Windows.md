---
title: 虚拟机配置 (Ubuntu, Python)
date: 2018-07-07 16:51:10
updated:
categories:
  - Records
tags:
  - Configure
  - Linux
---


# VirtualBox 安装 Ubuntu 16.04

## 准备 

**软件版本**

> **Windows:** Win 7/10  
> **VirtualBox:** e.g., VirtualBox 5.2.6/5.1.16  
> **Ubuntu:** ubuntu-16.04.4-desktop-amd64.iso  

**在 bios 开启 Virtualization Technology (VTx) 选项**  
其目的是：可以安装 64 位 linux 操作系统，并且可以开启虚拟机多 CPU 配置。  
机器不同，BIOS 配置不同，有些机器是默认打开 VTx 选项的，无需此步。如果没有打开 VTx，在 BIOS 打开即可。  
如：  
[thinkpad t460 开启虚拟化](https://bbs.thinkpad.com/thread-4406091-1-1.html)  
[如何开启笔记本的 VT-x 虚拟化技术功能](http://iknow.lenovo.com/app/detail/dc_C183451.html)  
[联想 ThinkPad 使用虚拟机时遇到要求打开 CPU 中 VT 的方法](https://blog.csdn.net/liynet/article/details/7232599)  

## 安装

新建虚拟机  
- “新建”虚拟机电脑，选择“现在创建虚拟磁盘”，其中内存设为 2048 GB（自定义）  
- 创建虚拟磁盘，文件大小设为 40 GB（自定义），‘虚拟磁盘文件类型’使用 vdi 或 vmdb 均可，‘存储在物理磁盘上’选择“动态分配”  

开始安装  
- 点击“启动”，选择光盘文件开始安装  
- 选择语言，中英均可  
- 安装时下载更新  
- 清除整个磁盘并安装  
- 设置时区  
- 设置键盘语言  
- 设置用户名和密码  
- 等待……  
- 安装完成后重启，重启前要移除安装光盘  

安装增强功能  
- “设备” -> “安装增强功能”  
- 重启  

设置共享文件夹  
- “控制” -> “设置” -> “共享文件夹”，点击右侧的添加按钮  
- 一定要选中“自动挂载”和“固定分配”  
- 添加共享文件夹权限  
  > sudo usermod -G vboxsf username
- 一定要重启。重启完成后再查看，发现每个文件夹前都多了"sf_"，在"/media"文件夹下。

## 解决问题

- 设置 root 密码  
  > sudo passwd   

```html
    安装 ubuntu 成功后，都是普通用户权限，并没有最高 root 权限。如果需要使用 root 权限，通常都会在命令前面加上 sudo 。有时候这样比较麻烦。  
    我们一般使用 su 命令来直接切换到 root 用户，但是会抛出 su: Authentication failure 这样的问题。这是因为：ubuntu 默认 root 密码是随机的，即每次开机都有一个新密码。  
    给 root 用户设置一个初始密码只需要输入 sudo passwd 命令，输入一般用户密码并设定 root 用户密码。  
    设定 root 密码成功后，输入 su 命令，并输入刚才设定的 root 密码，就可以切换成 root 了。  
    提示符 $ 代表一般用户，提示符 # 代表 root 用户。  
    输入 exit 命令，可退出 root 并返回一般用户。  
```

- username 不在 sudoer 文件中。此事将被报告  
  > gedit /etc/sudoers 在 “# User privilege specification” 下增加一行 usernameALL=(ALL:ALL) ALL

- **无法进入root权限，却又需要root权限才能解决问题，的死循环**  
  ***出错原因：***  
  设置root密码时把命令错输成 su passwd，再输正确命令时就提示不在sudoers文件中了。  
  此时，root密码随机，无法进入root权限；而更改sudoers文件又需要root权限，因此陷入死循环。  

  ***更正办法：***  [sudoers修改不能在终端使用sudo 和su的解决方法](https://blog.csdn.net/u011277123/article/details/78011983)  

  - 重启电脑，一直按着 esc 键，进入 "高级模式 -> recovery mode -> root" ，回车，这时会进入root目录，相当于单用户模式  
  - 在root终端输入    # mount -o remount rw /  
  - 修改/etc/sudoers的权限为777（默认权限是440）    # chmod 777 /etc/sudoers  
  - \# vi /etc/sudoers 回车，然后在后端加入 %admin ALL=(ALL) ALL 回车 sudo ALL=(ALL:ALL) ALL 保存  
  - 修改完保存退出后将/etc/sudoers权限恢复成默认的440权限，然后重启。这样你的问题解决！ 
  > \# chmod 440 /etc/sudoers  
  > \# reboot


- E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。

  在“设置”下的“软件和更新”里，去掉“更新”下的“不支持的更新”  
  然后更新一下  
  > sudo apt-get update



参考  
1. Ubuntu 的选择， i386 还是 amd64 ？  
  [UBUNTU amd64 和 i386有什么区别](http://forum.ubuntu.org.cn/viewtopic.php?t=80409)    
  i386是32位，amd64是64位。
  64位支持的内存一般更大（但如果只有1-2G内存的话，没必要装64位的）；且性能会高些，如果是数值计算，性能会高很多，整数运算上同频率64位的效率是32位的4倍左右。
  不过用的人少，问题略多（没有64位的flash支持，只能先用32位的，还有一些软件默认不提供64位包，不过可以自己编译。图省事的，还是用32位的吧）。

2. VirtualBox 安装 虚拟机 Ubuntu 16.04   
  [VirtualBox安装部署Ubuntu 16.04 图文详解](https://www.linuxidc.com/Linux/2016-08/134580.htm)  
  [基于VirtualBox虚拟机安装Ubuntu图文教程](https://blog.csdn.net/u012732259/article/details/70172704)  

3. ubuntu 设置 root 密码   
  [ubuntu 16.04 设置root用户初始密码](https://blog.csdn.net/u012301841/article/details/73692426)  
  [ubuntu 首次登陆设置root密码](https://blog.csdn.net/weixin_36210698/article/details/72857366)  

4. ubuntu 不在 sudoers 文件中。此事将被报告。  
  [用户名 不在 sudoers文件中，此事将被报告。](https://blog.csdn.net/lincyang/article/details/21020295)  
  [解决 用户不在 sudoers 文件中 的问题](https://blog.csdn.net/byzhang19900624/article/details/8813396)  



## 常用命令

ref:  [如何查看ubuntu的内核版本和发行版本号](https://blog.csdn.net/debug_cpp/article/details/2687067)

查看 Ubuntu 的内核和发行版本号

```bash
cat /etc/issue
sudo lsb_release -a
```



# Ubuntu 16.04 下 Python 的使用

## 默认

ref:  [linux 查看python安装路径,版本号](https://blog.csdn.net/jenyzhang/article/details/49646641) 

Ubuntu 16.04 自带两个版本的 Python，分别为 2.7 和 3.5 。
```bash
python2
python3
python  //默认为 2
```

查看 Ubuntu 中安装的 Python 路径
```sh
whereis python
which python
```

查看 Ubuntu 中安装的 Python 版本号
```shell
python --version
python
```

## pip 相关

### 管理员安装

程序“pip”尚未安装。如需运行‘pip’，请要求管理员安装 ‘python-pip’ 软件包。

安装 
```bash
sudo apt-get install python-pip
sudo apt-get install python3-pip  //pip3
```

更新
```bash
pip install --upgrade pip  //bug! 会更新到 10.x
pip install --upgrade pip==9.0.3
```

查看
```bash
pip 8.1.1:	pip list
pip 9.0.1:	pip list --format=columns
pip 10.0.1:	pip list
```

### virtualenv 与 virtualenvwrapper

ref: [python 虚拟环境[virtualenv/virtualenvwrapper]设置](https://www.jianshu.com/p/44ab75fbaef2)

安装
```bash
pip install virtualenv
pip install virtualenvwrapper
```

创建新环境
```bash
virtualenv [新环境名]
virtualenv [新环境名] --python=/usr/bin/python3
```

e.g.,  
> mkdir VirtualEnv  
> virtualenv py27env --python=/usr/bin/python2  
> virtualenv py35env --python=/usr/bin/python3

虚拟环境的进入和退出  
> cd VirtualEnv  
> source py27env/bin/activate  
> deactivate  
> source py35env/bin/activate  
> deactivate

## 安装所需包

### 通用

```bash
pip install numpy
pip install scipy
pip install scikit-learn

pip install matplotlib
pip install pandas
pip install pillow

pip install pathos
pip install lmdb
pip install requests
```

### Python 2.7.12+

```bash
pip install theano
pip install keras

pip install tensorflow==1.4.1

pip install http://download.pytorch.org/whl/cpu/torch-0.4.0-cp27-cp27mu-linux_x86_64.whl
pip install torchvision
```

如果有 GPU，比如服务器
```bash
pip install tensorflow-gpu==1.4.*
pip install torch torchvision
//pip uninstall tensorflow tensorboard
```

### Python 3.5.2+

```bash
pip install tensorflow==1.4.1
pip install http://download.pytorch.org/whl/cpu/torch-0.3.1-cp35-cp35m-linux_x86_64.whl
pip install torchvision==0.2.0
pip install keras

pip install pymongo
pip install photinia
```

服务器如有 GPU
```bash
pip install tensorflow-gpu==1.4.*
//pip3 install torch torchvision
pip install http://download.pytorch.org/whl/cu80/torch-0.3.1-cp35-cp35m-linux_x86_64.whl
pip install torchvision==0.2.0
```

注意：  
使用 lmdb 需要安装 python3-dev  
使用 matplotlib 需要安装 python3-tk  
> sudo apt-get install python3-dev  
> sudo apt-get install python3-tk

### 使用

```python
import numpy as np
import scipy
import sklearn
# import matplotlib
# matplotlib.use('Agg')
import matplotlib.pyplot as plt
import pandas
from PIL import Image

import tensorflow as tf
#No need: import tensorboard
import torch
import torchvision
import theano
import keras

import pathos
import requests
import lmdb
import pymongo
import photinia as ph
```

# 安装开发环境


## sublime, texstudio, texlive 

[Ubuntu 16.04安装sublime text3](https://jingyan.baidu.com/article/64d05a023cd849de55f73be4.html)  

sudo add-apt-repository ppa:webupd8team/sublime-text-3  
sudo apt-get update  
sudo apt-get install sublime-text-installer  
subl    # 启动


[Linux系统 Ubuntu更新sublime-text3的正确方法](http://wuguowei.com/wordpress/archives/1578)  

wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -   
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list   
sudo apt-get update  
sudo apt-get install sublime-text   


[sublime-text3无法输入中文的解决方法(linux环境)](http://wuguowei.com/wordpress/archives/1585)   
[sublime text3 安装 配置 以及常见问题汇总](http://blog.51cto.com/xiumu/1766052)   


[Ubuntu16.04中使用texlive+texstudio搭建Latex环境](https://blog.csdn.net/DreamHome_S/article/details/77920303)   

sudo apt install texlive  
sudo apt install latex-cjk-all  
sudo apt install texstudio  

安装 texlive, 中文字体包, texstudio  


## LanguageTool, Inkscape


TexStudio 配置语法检查 LanguageTool  
[对TexStudio配置拼写和语法检查LanguageTool功能](https://blog.csdn.net/yinqingwang/article/details/54583541)  
[折腾TeXstudio&拼写语法检查工具-LanguageTool](http://regulus.cc/2018/01/30/%E6%8A%98%E8%85%BETeXstudio/)  
[【Latex】如何在texstudio中进行语法检测](https://zhuanlan.zhihu.com/p/38209314)


矢量画图工具 Inkscape  
[ubuntu使用PPA安装Inkscape 0.91](https://www.linuxdashen.com/ubuntu%E4%BD%BF%E7%94%A8ppa%E5%AE%89%E8%A3%85inkscape-0-91)  
[Linux for Ubuntu安装Inkscape开源矢量图工具](https://blog.csdn.net/tydyz/article/details/76166224)  
[Ubuntu安装Inkscape开源矢量图工具及基本使用](http://www.linuxdiyf.com/linux/32143.html)  
[inkscape安装（ubuntu 16.04）](https://blog.csdn.net/lxlong89940101/article/details/86497925)

sudo add-apt-repository ppa:inkscape.dev/stable  
sudo apt update  
sudo apt-get install inkscape  
sudo apt-get remove inkscape  # 删除



## 安装 Python 开发环境

### 安装 Spyder

ref: [在Ubuntu-16.04中安装Python可视化IDE——Spyder](http://blog.51cto.com/tong707/1970182)

安装Spyder之前，安装以下python常用库和依赖（如果安装过会跳过）:  
```bash
sudo apt-get install python-dev python-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev
sudo pip install scrapy
sudo apt-get install libzmq-dev
sudo pip install pyzmq #here
sudo pip install pygments
sudo apt-get install qt4-dev-tools qt4-doc qt4-qtconfig qt4-demos qt4-designer
sudo pip install qtconsole
sudo pip install ipython
```

安装 Spyder  
> sudo apt install spyder  
> 我用的是 sudo apt-get install spyder

安装成功后，命令行输入 spyder 可打开 IDE  
> spyder

spyder 使用当前虚拟环境中的 python  
> 虚拟环境的设置还可以通过 tools > preferences > python interpreter 来自定义 

- Tools > Preferences  
- Step 1: Run > Console > 默认第一项改成第二项  
- Step 2: Console > Advanced settings > Python executable 的默认第一项改成第二项  
- Step 3: 把上一步中第二项的默认 "/usr/bin/python" 改成 "/home/ubuntu/VirtualEnv/py35env/bin/python"

参考  
[在Ubuntu-16.04中安装Python可视化IDE——Spyder](http://blog.51cto.com/tong707/1970182)  
[Ubuntu16.04下面spyder切换虚拟环境下面的python版本](https://blog.csdn.net/appleyuchi/article/details/78354694)  
废弃  
[conda 虚拟环境下配置spyder解释器为指定解释器](https://www.jianshu.com/p/1d33547f9f05)  
[anaconda /spyder 多虚拟环境](https://www.jianshu.com/p/de68016087c4) 

### 安装 PyCharm

> sudo add-apt-repository ppa:mystic-mirage/pycharm  
> sudo apt update  
> sudo apt install pycharm  
> \# 我后面两个用的是  
> \# sudo apt-get update

### 安装 Anaconda


## 安装 OpenCV

### 安装 opencv 3.0.0

ref: [手把手教你，在Ubuntu上安装OpenCV 3.0 和 Python 2.7+](http://nooverfit.com/wp/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E4%BD%A0%EF%BC%8C%E5%9C%A8ubuntu%E4%B8%8A%E5%AE%89%E8%A3%85opencv-3-0-%E5%92%8C-python-2-7/)

(1) 打开终端窗口，更新 apt-get 包管理器，升级所有预安装包  
> $ sudo apt-get update  
> $ sudo apt-get upgrade  

(2) 安装我们的开发工具和包  
> $ sudo apt-get install build-essential cmake git pkg-config  

(3) OpenCV 需要从磁盘中加载不同格式的图片，如  JPEG, TIFF, PNG 等等．所以我们需要安装我们的图像 I/O 工具包  
> $ sudo apt-get install libjpeg-dev libtiff-dev libjasper-dev libpng-dev  

(4) 另外，OpenCV 是用 GTK 开发包来显示 GUI,  即用户图形界面，所以我们要安装这个开发包  
> $ sudo apt-get install libgtk2.0-dev  

(5) OpenCV 还必须处理视频流和单个帧，下面就是我们需要的安装包  
> $ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  

(6) OpenCV 还包含一些内部优化工具  
> $ sudo apt-get install libatlas-base-dev gfortran  

(7) 安装 python 包管理器 pip  
(8) 步骤8  
+ 安装 virtualenv 和 virtualenvwrapper. 用来分割 python 虚拟环境. 这不是必须的, 但是强烈推荐  
> $ sudo pip install virtualenv virtualenvwrapper  
> $ sudo rm -rf ~/.cache/pip  

+ 现在我们有了 virtualenv 和 virtualenvwrapper, 我们要更新我们的 ~/.bashrc 文件  
> \# virtualenv and virtualenvwrapper  
> export WORKON_HOME=$HOME/.virtualenvs  
> source /usr/local/bin/virtualenvwrapper.sh  

+ 为了使 ~/.bashrc 文件生效 , 你可以用以下这些方法的其中之一  
  (1) 注销后重新登录, (2) 关闭终端开一个新终端, (3) 直接使得 ~/.bashrc 文件在当前生效:  
> $ source ~/.bashrc  

+ 最后我们生成名字叫 cv 的虚拟开发环境:  
> $ mkvirtualenv cv  

(9) 步骤9  
+ 安装 python 开发工具  
> $ sudo apt-get install python2.7-dev  

+ 安装 numpy   
> $ pip install numpy   

(10) 步骤10   
+ 预备环境终于都搞定啦, 我们进入正题, 安装 OpenCV 3.0.0  
> $ cd ~  
> $ git clone https://github.com/Itseez/opencv.git  
> $ cd opencv  
> $ git checkout 3.0.0   

+ 你也可以在这里使用 3.1.0, 但是别忘了去 OpenCV.org 官网看看有什么变动.  
+ 有一些牛叉的算法如 SIFT, SURF, 等等 在 opencv_contrib 里面, 所以我们要安装它来支持 OpenCV:  
> $ cd ~  
> $ git clone https://github.com/Itseez/opencv_contrib.git  
> $ cd opencv_contrib  
> $ git checkout 3.0.0  

+ 注意: opencv_contrib 和 OpenCV 版本要一致  
+ 是时候 build OpenCV 辣:  
> $ cd ~/opencv  
> $ mkdir build  
> $ cd build  
> $ cmake -D CMAKE_BUILD_TYPE=RELEASE \  
>   -D CMAKE_INSTALL_PREFIX=/usr/local \  
>   -D INSTALL_C_EXAMPLES=ON \  
>   -D INSTALL_PYTHON_EXAMPLES=ON \  
>   -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \  
>   -D BUILD_EXAMPLES=ON ..  

+ **如果要装 OpenCV 3.1.0, 你需要设置 DINSTALL_C_EXAMPLES=OFF**   
+ 最后, 编译! :  
> $ make -j4  

注意  
cmake -D CMAKE_BUILD_TYPE=RELEASE  -D CMAKE_INSTALL_PREFIX=/usr/local  -D INSTALL_C_EXAMPLES=ON  -D INSTALL_PYTHON_EXAMPLES=ON  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules  -D BUILD_EXAMPLES=ON .. 

即  
```bash
cmake -D CMAKE_BUILD_TYPE=RELEASE  -D CMAKE_INSTALL_PREFIX=/usr/local  -D INSTALL_C_EXAMPLES=ON  -D INSTALL_PYTHON_EXAMPLES=ON  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules  -D BUILD_EXAMPLES=ON .. 
```


### 卸载重装

ref: [ubuntu卸载opencv并重装opencv3.0.0](https://www.cnblogs.com/txg198955/p/5990295.html)

```bash
一、 卸载opencv2.4.9： Going to the "build" folder directory of opencv from terminal, and execute the following：
1. $ sudo make uninstall
2. $ cd ..
3. $ sudo rm -r build
4. $ sudo rm -r /usr/local/include/opencv2 /usr/local/include/opencv /usr/include/opencv /usr/include/opencv2 /usr/local/share/opencv /usr/local/share/OpenCV /usr/share/opencv /usr/share/OpenCV /usr/local/bin/opencv* /usr/local/lib/libopencv*
```

### 安装 opencv 3.2.0

ref: [ubuntu 16.04 安装opencv 3.2.0](https://blog.csdn.net/yudiemiaomiao/article/details/72780790)

1. 安装 opencv 依赖包   
2. 下载 opencv3.2.0   
  这里需要下载 opencv 和 opencv_contrib (后者会在 cmake 配置的时候用到)，这是因为 opencv3 以后 SIFT 和 SURF 之类的属性被移到了 contrib 中。   
> $ wget https://github.com/opencv/opencv/archive/3.2.0.zip  #从github上直接下载或者clone也可   
> $ wget https://github.com/opencv/opencv_contrib/archive/3.2.0.zip   

3. 安装 opencv3.2.0   

cd VirtualEnv/opencv  
cd opencv  
git checkout 3.2.0  
cd ../opencv_contrib  
git checkout 3.2.0  
cd ..  

cd opencv  
mkdir build  
cd build  
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..  


CMAKE_INSTALL_PREFIX：安装的python目录前缀，指定了python模块的安装路径：CMAKE_INSTALL_PREFIX/lib/python2.7/dist-packages，获取该路径的方式可以用： 

python -c "import sys; print sys.prefix"  


在安装过程中，很有可能会出现错误：ICV: Downloading ippicv_linux_20151201.tgz 超时，据说此部分可有可无，可自行搜索文件名进行下载，然后替换opencv-3.2.0/3rdparty/ippicv/downloads/linux-*目录下的同名文件，重新cmake。

optional(显示指定一些编译内容），我在安装时未显示指定：

cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D ENABLE_FAST_MATH=1 -D WITH_CUDA=ON -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 -D CUDA_GENERATION=Auto -D WITH_GSTREAMER_0_10=OFF ..  


在 build 目录下：  

make -j4  

-j4 表示四核运算，可根据电脑配置选择。

然后  
编译没问题的话, 就可以安装了:

sudo make install  
sudo ldconfig -v  


(11) 步骤11：  
如果安装无误, OpenCV 现在已经安装在 /usr/local/lib/python2.7/site–packages 中了. 但是考虑到我们的虚拟环境 cv 还没有 OpenCV, 我们需要建立一个软链:

```bash
cd ~  
cd VirtualEnv/py27env  
cd lib/python2.7/site-packages  
ln -s /usr/local/lib/python2.7/dist-packages/cv2.so cv2.so  
```

(12) 步骤 12:  
恭喜 ! 你完成了在 Ubuntu 上安装 OpenCV 3.0 和 Python 2.7+  
所有剩下的就是验证一下啦：   

```bash
$ workon cv
$ python
>>> import cv2
>>> cv2.__version__
>>> '3.0.0'
```


参考  
[ubuntu 16.04 安装opencv 3.2.0](https://blog.csdn.net/yudiemiaomiao/article/details/72780790)  
[手把手教你，在Ubuntu上安装OpenCV 3.0 和 Python 2.7+](http://nooverfit.com/wp/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E4%BD%A0%EF%BC%8C%E5%9C%A8ubuntu%E4%B8%8A%E5%AE%89%E8%A3%85opencv-3-0-%E5%92%8C-python-2-7/)  
[python 虚拟环境[virtualenv/virtualenvwrapper]设置](https://www.jianshu.com/p/44ab75fbaef2)  
[ubuntu卸载opencv并重装opencv3.0.0](https://www.cnblogs.com/txg198955/p/5990295.html)  
[Ubuntu下安装opencv 2.4.11](https://blog.csdn.net/u013453604/article/details/49781771)


## spyder 切换环境

cd VirtualEnv

source py35env/bin/activate  
pip install ipython  

### 安装 PyQt4

sudo apt-get install libxext6 libxext-dev libqt4-dev libqt4-gui libqt4-sql  //delete "libqt4-gui"   
sudo apt-get install qt4-dev-tools qt4-doc qt4-qtconfig qt4-demos qt4-designer   
sudo apt-get install python-qt4   
sudo apt-get install python-qt4-*   
sudo apt-get install python-qscintilla2   

sudo apt-get install python3-pyqt4   
sudo apt-get install python3-pyqt4.qsci  
sudo apt-get install python3-pyqt4.qtsql  
sudo apt-get install python3-pyqt4.phonon  

[Ubuntu：Unable to locate package（无法定位安装包）](https://blog.csdn.net/baidu_33850454/article/details/78225155)  
[Desktop Ubuntu 14.04LTS/16.04科学计算环境配置](https://www.bbsmax.com/A/obzbX1Y15E/)  
[在ubuntu 14.04 64bit下配置安装PyQt4(python2.7和python3.4)](https://blog.csdn.net/tao_627/article/details/46529587)  

### 安装 PySide

sudo apt-get install build-essential  
sudo apt-get install qt4-dev-tools qt4-doc qt4-qtconfig qt4-demos qt4-designer qtcreator  
sudo pip3 install pyside  

[Ubuntu下安装PySide](https://blog.csdn.net/u011008379/article/details/55299371)  
[PySide Installation error with Command “python setup.py egg_info” failed with error code 1](https://stackoverflow.com/questions/46723857/pyside-installation-error-with-command-python-setup-py-egg-info-failed-with-er)  

### 安装 ipython, pyside

cd ~/VirtualEnv  
source py35env/bin/activate  
pip install pyside  



## summary

- python2: ....   
- python3: ....   
- virtualenv, virtualenvwrapper   
- sublime text 3   
- texlive, texstudio (inkscape)  
- pycharm   
- spyder, spyder3  

