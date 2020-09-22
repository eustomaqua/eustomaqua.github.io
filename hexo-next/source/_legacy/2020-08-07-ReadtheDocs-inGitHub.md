---
title: ReadtheDocs 创建文档 in GitHub
date: 2020-08-07 15:28:19
updated: 2020-08-07 15:28:19
categories:
  - Records
tags:
  - ReadtheDocs
  - GitHub
mathjax: false
---


**Prepare:** 
[https://readthedocs-demo-zh.readthedocs.io/zh_CN/latest/%E6%96%87%E4%BB%B6%E6%89%98%E7%AE%A1%E7%B3%BB%E7%BB%9F-ReadtheDocs.html](https://readthedocs-demo-zh.readthedocs.io/zh_CN/latest/%E6%96%87%E4%BB%B6%E6%89%98%E7%AE%A1%E7%B3%BB%E7%BB%9F-ReadtheDocs.html)



# 环境搭建

## Step by Step

```shell
cd ~/Software
ls
git clone https://github.com/sphinx-doc/sphinx
cd sphinx
pip install .
```

## Details

### Previously

```shell
ubuntu@ubuntu-VirtualBox:~$ cd VirtualEnv
ubuntu@ubuntu-VirtualBox:~/VirtualEnv$ ls
electron-quick-start  opencv   py35env  richinfoai
mongodb               py27env  py36env  sources.list
ubuntu@ubuntu-VirtualBox:~/VirtualEnv$ source py36env/bin/activate
(py36env) ubuntu@ubuntu-VirtualBox:~/VirtualEnv$ pip list
Package             Version
------------------- -------
absl-py             0.6.1  
astor               0.7.1  
gast                0.2.0  
grpcio              1.17.1 
h5py                2.9.0  
Keras-Applications  1.0.6  
Keras-Preprocessing 1.0.5  
Markdown            3.0.1  
numpy               1.15.4 
pip                 18.1   
protobuf            3.6.1  
setuptools          40.6.3 
six                 1.12.0 
tensorboard         1.12.2 
tensorflow          1.12.0 
termcolor           1.1.0  
Werkzeug            0.14.1 
wheel               0.32.3 
You are using pip version 18.1, however version 20.2.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(py36env) ubuntu@ubuntu-VirtualBox:~/VirtualEnv$ 

(py36env) ubuntu@ubuntu-VirtualBox:~/Software/sphinx$ python
Python 3.6.5 (default, Jun  7 2018, 21:37:43) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> ^Z
[1]+  已停止               python
(py36env) ubuntu@ubuntu-VirtualBox:~/Software/sphinx$ 
```

### Environment

```shell
(py36env) ubuntu@ubuntu-VirtualBox:~/VirtualEnv$ cd ~/Software
(py36env) ubuntu@ubuntu-VirtualBox:~/Software$ ls
fonts.dir  fonts.scale  install-tl-20200703
(py36env) ubuntu@ubuntu-VirtualBox:~/Software$ git clone https://github.com/sphinx-doc/sphinx
正克隆到 'sphinx'...
remote: Enumerating objects: 81, done.
remote: Counting objects: 100% (81/81), done.
remote: Compressing objects: 100% (66/66), done.
remote: Total 110523 (delta 47), reused 34 (delta 15), pack-reused 110442
接收对象中: 100% (110523/110523), 43.43 MiB | 487.00 KiB/s, 完成.
处理 delta 中: 100% (84248/84248), 完成.
检查连接... 完成。
(py36env) ubuntu@ubuntu-VirtualBox:~/Software$ cd sphinx
(py36env) ubuntu@ubuntu-VirtualBox:~/Software/sphinx$ pip install .
Processing /home/ubuntu/Software/sphinx
Collecting sphinxcontrib-applehelp (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/dc/47/86022665a9433d89a66f5911b558ddff69861766807ba685de2e324bd6ed/sphinxcontrib_applehelp-1.0.2-py2.py3-none-any.whl (121kB)
    100% |████████████████████████████████| 122kB 211kB/s 
Collecting sphinxcontrib-devhelp (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/c5/09/5de5ed43a521387f18bdf5f5af31d099605c992fd25372b2b9b825ce48ee/sphinxcontrib_devhelp-1.0.2-py2.py3-none-any.whl (84kB)
    100% |████████████████████████████████| 92kB 1.7MB/s 
Collecting sphinxcontrib-jsmath (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/c2/42/4c8646762ee83602e3fb3fbe774c2fac12f317deb0b5dbeeedd2d3ba4b77/sphinxcontrib_jsmath-1.0.1-py2.py3-none-any.whl
Collecting sphinxcontrib-htmlhelp (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/36/62/8222554b29b3acde8420128d6d3999c5904d40922ef4b6ccb370e2be7421/sphinxcontrib_htmlhelp-1.0.3-py2.py3-none-any.whl (96kB)
    100% |████████████████████████████████| 102kB 2.0MB/s 
Collecting sphinxcontrib-serializinghtml (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/9a/ca/bfad79b79b3821d0c6361c431f0ef4aec16ee248338b2c2013008b34d345/sphinxcontrib_serializinghtml-1.1.4-py2.py3-none-any.whl (89kB)
    100% |████████████████████████████████| 92kB 938kB/s 
Collecting sphinxcontrib-qthelp (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/2b/14/05f9206cf4e9cfca1afb5fd224c7cd434dcc3a433d6d9e4e0264d29c6cdb/sphinxcontrib_qthelp-1.0.3-py2.py3-none-any.whl (90kB)
    100% |████████████████████████████████| 92kB 2.1MB/s 
Collecting Jinja2>=2.3 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/30/9e/f663a2aa66a09d838042ae1a2c5659828bb9b41ea3a6efa20a20fd92b121/Jinja2-2.11.2-py2.py3-none-any.whl (125kB)
    100% |████████████████████████████████| 133kB 1.9MB/s 
Collecting Pygments>=2.0 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/2d/68/106af3ae51daf807e9cdcba6a90e518954eb8b70341cee52995540a53ead/Pygments-2.6.1-py3-none-any.whl (914kB)
    100% |████████████████████████████████| 921kB 2.7MB/s 
Collecting docutils>=0.12 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/81/44/8a15e45ffa96e6cf82956dd8d7af9e666357e16b0d93b253903475ee947f/docutils-0.16-py2.py3-none-any.whl (548kB)
    100% |████████████████████████████████| 552kB 3.3MB/s 
Collecting snowballstemmer>=1.1 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/7d/4b/cdf1113a0e88b641893b814e9c36f69a6fda28cd88b62c7f0d858cde3166/snowballstemmer-2.0.0-py2.py3-none-any.whl (97kB)
    100% |████████████████████████████████| 102kB 9.0MB/s 
Collecting babel>=1.3 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/15/a1/522dccd23e5d2e47aed4b6a16795b8213e3272c7506e625f2425ad025a19/Babel-2.8.0-py2.py3-none-any.whl (8.6MB)
    100% |████████████████████████████████| 8.6MB 1.4MB/s 
Collecting alabaster<0.8,>=0.7 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/10/ad/00b090d23a222943eb0eda509720a404f531a439e803f6538f35136cae9e/alabaster-0.7.12-py2.py3-none-any.whl
Collecting imagesize (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/31/b2/b5522a0c8d11e4aff83f8342f3f0dea68c2fb25aa44403e420587f0ce204/imagesize-1.2.0-py2.py3-none-any.whl
Collecting requests>=2.5.0 (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/45/1e/0c169c6a5381e241ba7404532c16a21d86ab872c9bed8bdcd4c423954103/requests-2.24.0-py2.py3-none-any.whl (61kB)
    100% |████████████████████████████████| 71kB 8.7MB/s 
Requirement already satisfied: setuptools in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from Sphinx==3.2.0.dev20200807) (40.6.3)
Collecting packaging (from Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/46/19/c5ab91b1b05cfe63cccd5cfc971db9214c6dd6ced54e33c30d5af1d2bc43/packaging-20.4-py2.py3-none-any.whl
Collecting MarkupSafe>=0.23 (from Jinja2>=2.3->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/b2/5f/23e0023be6bb885d00ffbefad2942bc51a620328ee910f64abe5a8d18dd1/MarkupSafe-1.1.1-cp36-cp36m-manylinux1_x86_64.whl
Collecting pytz>=2015.7 (from babel>=1.3->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/4f/a4/879454d49688e2fad93e59d7d4efda580b783c745fd2ec2a3adf87b0808d/pytz-2020.1-py2.py3-none-any.whl (510kB)
    100% |████████████████████████████████| 512kB 8.0MB/s 
Collecting idna<3,>=2.5 (from requests>=2.5.0->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/a2/38/928ddce2273eaa564f6f50de919327bf3a00f091b5baba8dfa9460f3a8a8/idna-2.10-py2.py3-none-any.whl (58kB)
    100% |████████████████████████████████| 61kB 13.7MB/s 
Collecting certifi>=2017.4.17 (from requests>=2.5.0->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/5e/c4/6c4fe722df5343c33226f0b4e0bb042e4dc13483228b4718baf286f86d87/certifi-2020.6.20-py2.py3-none-any.whl (156kB)
    100% |████████████████████████████████| 163kB 6.1MB/s 
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 (from requests>=2.5.0->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/9f/f0/a391d1463ebb1b233795cabfc0ef38d3db4442339de68f847026199e69d7/urllib3-1.25.10-py2.py3-none-any.whl (127kB)
    100% |████████████████████████████████| 133kB 7.1MB/s 
Collecting chardet<4,>=3.0.2 (from requests>=2.5.0->Sphinx==3.2.0.dev20200807)
  Using cached https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl
Collecting pyparsing>=2.0.2 (from packaging->Sphinx==3.2.0.dev20200807)
  Downloading https://files.pythonhosted.org/packages/8a/bb/488841f56197b13700afd5658fc279a2025a39e22449b7cf29864669b15d/pyparsing-2.4.7-py2.py3-none-any.whl (67kB)
    100% |████████████████████████████████| 71kB 10.2MB/s 
Requirement already satisfied: six in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from packaging->Sphinx==3.2.0.dev20200807) (1.12.0)
Building wheels for collected packages: Sphinx
  Running setup.py bdist_wheel for Sphinx ... done
  Stored in directory: /tmp/pip-ephem-wheel-cache-4vrdpaha/wheels/6e/66/5c/025df57f9259947510a7d5206e1115114ba3e051e812813297
Successfully built Sphinx
Installing collected packages: sphinxcontrib-applehelp, sphinxcontrib-devhelp, sphinxcontrib-jsmath, sphinxcontrib-htmlhelp, sphinxcontrib-serializinghtml, sphinxcontrib-qthelp, MarkupSafe, Jinja2, Pygments, docutils, snowballstemmer, pytz, babel, alabaster, imagesize, idna, certifi, urllib3, chardet, requests, pyparsing, packaging, Sphinx
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Pygments-2.6.1 Sphinx-3.2.0.dev20200807 alabaster-0.7.12 babel-2.8.0 certifi-2020.6.20 chardet-3.0.4 docutils-0.16 idna-2.10 imagesize-1.2.0 packaging-20.4 pyparsing-2.4.7 pytz-2020.1 requests-2.24.0 snowballstemmer-2.0.0 sphinxcontrib-applehelp-1.0.2 sphinxcontrib-devhelp-1.0.2 sphinxcontrib-htmlhelp-1.0.3 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.3 sphinxcontrib-serializinghtml-1.1.4 urllib3-1.25.10
You are using pip version 18.1, however version 20.2.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(py36env) ubuntu@ubuntu-VirtualBox:~/Software/sphinx$ 
```


# 项目创建

## Step by Step


## Details

### HelloWorld

```shell
(py36env) ubuntu@ubuntu-VirtualBox:~/Software/sphinx$ cd ~
(py36env) ubuntu@ubuntu-VirtualBox:~$ cd /media/sf_GitHubLab
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab$ cd ReadTheDocs
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs$ mkdir docs
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs$ cd docs
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ sphinx-quickstart
欢迎使用 Sphinx 3.2.0 快速配置工具。

Please enter values for the following settings (just press Enter to
accept a default value, if one is given in brackets).

Selected root path: .

You have two options for placing the build directory for Sphinx output.
Either, you use a directory "_build" within the root path, or you separate
"source" and "build" directories within the root path.
> 独立的源文件和构建目录（y/n） [n]: y

The project name will occur in several places in the built documentation.
> 项目名称: helloworld
> 作者名称: eustomaqua
> 项目发行版本 []: 0.1.1

If the documents are to be written in a language other than English,
you can select a language here by its language code. Sphinx will then
translate text that it generates into that language.

For a list of supported codes, see
https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
> 项目语种 [en]: zh_CN

创建文件 /media/sf_GitHubLab/ReadTheDocs/docs/source/conf.py。
创建文件 /media/sf_GitHubLab/ReadTheDocs/docs/source/index.rst。
创建文件 /media/sf_GitHubLab/ReadTheDocs/docs/Makefile。
创建文件 /media/sf_GitHubLab/ReadTheDocs/docs/make.bat。

完成：已创建初始目录结构。

You should now populate your master file /media/sf_GitHubLab/ReadTheDocs/docs/source/index.rst and create other documentation
source files. Use the Makefile to build the docs, like so:
   make builder
where "builder" is one of the supported builders, e.g. html, latex or linkcheck.

(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ make html
正在运行 Sphinx v3.2.0
正在加载翻译 [zh_CN]... 完成
创建输出目录... 完成
构建 [mo]： 0 个 po 文件的目标文件已过期
构建 [html]： 1 个源文件的目标文件已过期
更新环境: [新配置] 已添加 1，0 已更改，0 已移除
阅读源... [100%] index                                                             
查找当前已过期的文件... 没有找到
pickling环境... 完成
检查一致性... 完成
准备文件... 完成
写入输出... [100%] index                                                            
generating indices...  genindex完成
writing additional pages...  search完成
复制静态文件... ... 完成
copying extra files... 完成
dumping search index in Chinese (code: zh)... 完成
dumping object inventory... 完成
构建 成功.

HTML 页面保存在 build/html 目录。
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ 
```

### Theme Configure

```shell
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ pip install sphinx_rtd_theme
Collecting sphinx_rtd_theme
  Downloading https://files.pythonhosted.org/packages/c3/86/1addf25a238bbd8466bb099f23d9a9f13494b22b37b44f6c41a778b8730f/sphinx_rtd_theme-0.5.0-py2.py3-none-any.whl (10.8MB)
    100% |████████████████████████████████| 10.8MB 2.3MB/s 
Requirement already satisfied: sphinx in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx_rtd_theme) (3.2.0.dev20200807)
Requirement already satisfied: imagesize in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.2.0)
Requirement already satisfied: setuptools in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (40.6.3)
Requirement already satisfied: alabaster<0.8,>=0.7 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (0.7.12)
Requirement already satisfied: requests>=2.5.0 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (2.24.0)
Requirement already satisfied: sphinxcontrib-jsmath in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.0.1)
Requirement already satisfied: sphinxcontrib-qthelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.0.3)
Requirement already satisfied: sphinxcontrib-devhelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.0.2)
Requirement already satisfied: docutils>=0.12 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (0.16)
Requirement already satisfied: sphinxcontrib-serializinghtml in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.1.4)
Requirement already satisfied: Jinja2>=2.3 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (2.11.2)
Requirement already satisfied: snowballstemmer>=1.1 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (2.0.0)
Requirement already satisfied: sphinxcontrib-htmlhelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.0.3)
Requirement already satisfied: packaging in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (20.4)
Requirement already satisfied: Pygments>=2.0 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (2.6.1)
Requirement already satisfied: sphinxcontrib-applehelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (1.0.2)
Requirement already satisfied: babel>=1.3 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx->sphinx_rtd_theme) (2.8.0)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx->sphinx_rtd_theme) (1.25.10)
Requirement already satisfied: chardet<4,>=3.0.2 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx->sphinx_rtd_theme) (3.0.4)
Requirement already satisfied: idna<3,>=2.5 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx->sphinx_rtd_theme) (2.10)
Requirement already satisfied: certifi>=2017.4.17 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx->sphinx_rtd_theme) (2020.6.20)
Requirement already satisfied: MarkupSafe>=0.23 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from Jinja2>=2.3->sphinx->sphinx_rtd_theme) (1.1.1)
Requirement already satisfied: pyparsing>=2.0.2 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from packaging->sphinx->sphinx_rtd_theme) (2.4.7)
Requirement already satisfied: six in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from packaging->sphinx->sphinx_rtd_theme) (1.12.0)
Requirement already satisfied: pytz>=2015.7 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from babel>=1.3->sphinx->sphinx_rtd_theme) (2020.1)
Installing collected packages: sphinx-rtd-theme
Successfully installed sphinx-rtd-theme-0.5.0
You are using pip version 18.1, however version 20.2.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ 
```

```shell
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ make html
正在运行 Sphinx v3.2.0
正在加载翻译 [zh_CN]... 完成
加载 pickled环境... 完成
构建 [mo]： 0 个 po 文件的目标文件已过期
构建 [html]： 1 个源文件的目标文件已过期
更新环境: 已添加 0，0 已更改，0 已移除
查找当前已过期的文件... 没有找到
准备文件... 完成
写入输出... [100%] index                                                            
generating indices...  genindex完成
writing additional pages...  search完成
复制静态文件... ... 完成
copying extra files... 完成
dumping search index in Chinese (code: zh)... 完成
dumping object inventory... 完成
构建 成功.

HTML 页面保存在 build/html 目录。
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ 
```

### Markdown Conf

```shell
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ pip install recommonmark
Collecting recommonmark
  Downloading https://files.pythonhosted.org/packages/94/de/334aaf73df8c0e77fb07f883d1e274344526196c137ef3479cb5e5aef086/recommonmark-0.6.0-py2.py3-none-any.whl
Collecting commonmark>=0.8.1 (from recommonmark)
  Downloading https://files.pythonhosted.org/packages/b1/92/dfd892312d822f36c55366118b95d914e5f16de11044a27cf10a7d71bbbf/commonmark-0.9.1-py2.py3-none-any.whl (51kB)
    100% |████████████████████████████████| 51kB 167kB/s 
Requirement already satisfied: docutils>=0.11 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from recommonmark) (0.16)
Requirement already satisfied: sphinx>=1.3.1 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from recommonmark) (3.2.0.dev20200807)
Requirement already satisfied: sphinxcontrib-devhelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.0.2)
Requirement already satisfied: snowballstemmer>=1.1 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (2.0.0)
Requirement already satisfied: babel>=1.3 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (2.8.0)
Requirement already satisfied: imagesize in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.2.0)
Requirement already satisfied: sphinxcontrib-applehelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.0.2)
Requirement already satisfied: sphinxcontrib-jsmath in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.0.1)
Requirement already satisfied: packaging in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (20.4)
Requirement already satisfied: Jinja2>=2.3 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (2.11.2)
Requirement already satisfied: requests>=2.5.0 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (2.24.0)
Requirement already satisfied: sphinxcontrib-qthelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.0.3)
Requirement already satisfied: Pygments>=2.0 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (2.6.1)
Requirement already satisfied: alabaster<0.8,>=0.7 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (0.7.12)
Requirement already satisfied: setuptools in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (40.6.3)
Requirement already satisfied: sphinxcontrib-serializinghtml in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.1.4)
Requirement already satisfied: sphinxcontrib-htmlhelp in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from sphinx>=1.3.1->recommonmark) (1.0.3)
Requirement already satisfied: pytz>=2015.7 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from babel>=1.3->sphinx>=1.3.1->recommonmark) (2020.1)
Requirement already satisfied: pyparsing>=2.0.2 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from packaging->sphinx>=1.3.1->recommonmark) (2.4.7)
Requirement already satisfied: six in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from packaging->sphinx>=1.3.1->recommonmark) (1.12.0)
Requirement already satisfied: MarkupSafe>=0.23 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from Jinja2>=2.3->sphinx>=1.3.1->recommonmark) (1.1.1)
Requirement already satisfied: chardet<4,>=3.0.2 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx>=1.3.1->recommonmark) (3.0.4)
Requirement already satisfied: idna<3,>=2.5 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx>=1.3.1->recommonmark) (2.10)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx>=1.3.1->recommonmark) (1.25.10)
Requirement already satisfied: certifi>=2017.4.17 in /home/ubuntu/VirtualEnv/py36env/lib/python3.6/site-packages (from requests>=2.5.0->sphinx>=1.3.1->recommonmark) (2020.6.20)
Installing collected packages: commonmark, recommonmark
Successfully installed commonmark-0.9.1 recommonmark-0.6.0
You are using pip version 18.1, however version 20.2.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(py36env) ubuntu@ubuntu-VirtualBox:/media/sf_GitHubLab/ReadTheDocs/docs$ 
```


# MkDocs

```shell
(py36env) ubuntu@ubuntu-VirtualBox:~$ pip install mkdocs
Collecting mkdocs
  Downloading https://files.pythonhosted.org/packages/5d/89/ed04b217404bbba031c4e2e084f36ef840b8663fce0b80302b547e651e4d/mkdocs-1.1.2-py3-none-any.whl (6.4MB)
    100% |████████████████████████████████| 6.4MB 232kB/s 
Collecting Markdown>=3.2.1 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/a4/63/eaec2bd025ab48c754b55e8819af0f6a69e2b1e187611dd40cbbe101ee7f/Markdown-3.2.2-py3-none-any.whl (88kB)
    100% |████████████████████████████████| 92kB 288kB/s 
Collecting PyYAML>=3.10 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/64/c2/b80047c7ac2478f9501676c988a5411ed5572f35d1beff9cae07d321512c/PyYAML-5.3.1.tar.gz (269kB)
    100% |████████████████████████████████| 276kB 322kB/s 
Collecting lunr[languages]==0.5.8 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/15/a4/3043c019613a1d60abb6e150b7665761bdd236a0d915d447d21c4415fddd/lunr-0.5.8-py2.py3-none-any.whl (2.3MB)
    100% |████████████████████████████████| 2.3MB 135kB/s 
Collecting tornado>=5.0 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/95/84/119a46d494f008969bf0c775cb2c6b3579d3c4cc1bb1b41a022aa93ee242/tornado-6.0.4.tar.gz (496kB)
    100% |████████████████████████████████| 501kB 178kB/s 
Collecting click>=3.3 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/d2/3d/fa76db83bf75c4f8d338c2fd15c8d33fdd7ad23a9b5e57eb6c5de26b430e/click-7.1.2-py2.py3-none-any.whl (82kB)
    100% |████████████████████████████████| 92kB 134kB/s 
Requirement already satisfied: Jinja2>=2.10.1 in ./VirtualEnv/py36env/lib/python3.6/site-packages (from mkdocs) (2.11.2)
Collecting livereload>=2.5.1 (from mkdocs)
  Downloading https://files.pythonhosted.org/packages/bd/60/6640b819e858562ef6684abac60593b7369fe0a8a064df426d3ab0ab894d/livereload-2.6.3.tar.gz
Collecting importlib-metadata; python_version < "3.8" (from Markdown>=3.2.1->mkdocs)
  Downloading https://files.pythonhosted.org/packages/8e/58/cdea07eb51fc2b906db0968a94700866fc46249bdc75cac23f9d13168929/importlib_metadata-1.7.0-py2.py3-none-any.whl
Requirement already satisfied: six>=1.11.0 in ./VirtualEnv/py36env/lib/python3.6/site-packages (from lunr[languages]==0.5.8->mkdocs) (1.12.0)
Collecting future>=0.16.0 (from lunr[languages]==0.5.8->mkdocs)
  Downloading https://files.pythonhosted.org/packages/45/0b/38b06fd9b92dc2b68d58b75f900e97884c45bedd2ff83203d933cf5851c9/future-0.18.2.tar.gz (829kB)
    100% |████████████████████████████████| 829kB 168kB/s 
Collecting nltk>=3.2.5; python_version > "2.7" and extra == "languages" (from lunr[languages]==0.5.8->mkdocs)
  Downloading https://files.pythonhosted.org/packages/92/75/ce35194d8e3022203cca0d2f896dbb88689f9b3fce8e9f9cff942913519d/nltk-3.5.zip (1.4MB)
    100% |████████████████████████████████| 1.4MB 279kB/s 
Requirement already satisfied: MarkupSafe>=0.23 in ./VirtualEnv/py36env/lib/python3.6/site-packages (from Jinja2>=2.10.1->mkdocs) (1.1.1)
Collecting zipp>=0.5 (from importlib-metadata; python_version < "3.8"->Markdown>=3.2.1->mkdocs)
  Downloading https://files.pythonhosted.org/packages/b2/34/bfcb43cc0ba81f527bc4f40ef41ba2ff4080e047acb0586b56b3d017ace4/zipp-3.1.0-py3-none-any.whl
Collecting joblib (from nltk>=3.2.5; python_version > "2.7" and extra == "languages"->lunr[languages]==0.5.8->mkdocs)
  Downloading https://files.pythonhosted.org/packages/51/dd/0e015051b4a27ec5a58b02ab774059f3289a94b0906f880a3f9507e74f38/joblib-0.16.0-py3-none-any.whl (300kB)
    100% |████████████████████████████████| 307kB 238kB/s 
Collecting regex (from nltk>=3.2.5; python_version > "2.7" and extra == "languages"->lunr[languages]==0.5.8->mkdocs)
  Downloading https://files.pythonhosted.org/packages/3e/eb/85f375a102e95cde14a184ee985a35e1a20c4ceb3fe7f57fa128a9326283/regex-2020.7.14-cp36-cp36m-manylinux1_x86_64.whl (660kB)
    100% |████████████████████████████████| 665kB 229kB/s 
Collecting tqdm (from nltk>=3.2.5; python_version > "2.7" and extra == "languages"->lunr[languages]==0.5.8->mkdocs)
  Downloading https://files.pythonhosted.org/packages/28/7e/281edb5bc3274dfb894d90f4dbacfceaca381c2435ec6187a2c6f329aed7/tqdm-4.48.2-py2.py3-none-any.whl (68kB)
    100% |████████████████████████████████| 71kB 214kB/s 
Building wheels for collected packages: PyYAML, tornado, livereload, future, nltk
  Running setup.py bdist_wheel for PyYAML ... done
  Stored in directory: /home/ubuntu/.cache/pip/wheels/a7/c1/ea/cf5bd31012e735dc1dfea3131a2d5eae7978b251083d6247bd
  Running setup.py bdist_wheel for tornado ... done
  Stored in directory: /home/ubuntu/.cache/pip/wheels/93/84/2f/409c7b2bb3afc3aa727f7ee8787975e0793f74d1165f4d0104
  Running setup.py bdist_wheel for livereload ... done
  Stored in directory: /home/ubuntu/.cache/pip/wheels/f2/a1/fa/00775311351a48f78b4a0e40588eefdd6f2731cc8115d6957d
  Running setup.py bdist_wheel for future ... done
  Stored in directory: /home/ubuntu/.cache/pip/wheels/8b/99/a0/81daf51dcd359a9377b110a8a886b3895921802d2fc1b2397e
  Running setup.py bdist_wheel for nltk ... done
  Stored in directory: /home/ubuntu/.cache/pip/wheels/ae/8c/3f/b1fe0ba04555b08b57ab52ab7f86023639a526d8bc8d384306
Successfully built PyYAML tornado livereload future nltk
Installing collected packages: zipp, importlib-metadata, Markdown, PyYAML, future, click, joblib, regex, tqdm, nltk, lunr, tornado, livereload, mkdocs
  Found existing installation: Markdown 3.0.1
    Uninstalling Markdown-3.0.1:
      Successfully uninstalled Markdown-3.0.1
Successfully installed Markdown-3.2.2 PyYAML-5.3.1 click-7.1.2 future-0.18.2 importlib-metadata-1.7.0 joblib-0.16.0 livereload-2.6.3 lunr-0.5.8 mkdocs-1.1.2 nltk-3.5 regex-2020.7.14 tornado-6.0.4 tqdm-4.48.2 zipp-3.1.0
You are using pip version 18.1, however version 20.2.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(py36env) ubuntu@ubuntu-VirtualBox:~$ 
```


# References
