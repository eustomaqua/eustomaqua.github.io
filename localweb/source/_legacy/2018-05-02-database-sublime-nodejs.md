---
title: 数据库 (lmdb, mongodb) 的安装与使用，附 Sublime 插件配置
date:        2018-05-02 14:11:01
updated: 2018-07-07 19:06:27
categories:
  - Records
tags:
  - Configuration
---

<!-- Configure -->

[comment]: <> (updated: 2018-05-02 15:03:36)
[comment]: <> ("updated: 2018-05-02 15:14:48")

[comment]: <> (https://github.com/eustomaqua/eustomaqua.github.io/blob/master/images/2018-05-02/lmdb_img1.png?raw=true)
[comment]: <> (https://github.com/eustomaqua/eustomaqua.github.io/blob/master/images/2018-05-02/lmdb_img2.png?raw=true)
[comment]: <> (../_images_my/2018-07/05_02_lmdb_img1.png)
[comment]: <> (../_images_my/2018-07/05_02_lmdb_img2.png)
[comment]: <> (https://github.com/eustomaqua/eustomaqua.github.io/raw/master/_images_self/2018-07/05_02_lmdb_img1.png)
[comment]: <> (https://github.com/eustomaqua/eustomaqua.github.io/raw/master/_images_self/2018-07/05_02_lmdb_img2.png)


# lmdb

## Intro

lmdb 数据库是一个非关系型数据库。  
caffe 先支持 leveldb，后支持 lmdb 的，lmdb 读取的效率更高，而且支持不同程序同时读取，而 leveldb 只允许一个程序读取。这一点在使用同样的数据跑不同的配置程序时很重要。  
lmdb 有利于提高磁盘 IO 利用率。

[comment]: <> (# Setting)
## Install

> pip install lmdb

## Apply

LMDB 和 SQLite/MySQL 等关系型数据库不同，属于 key-value 数据库（把 LMDB 想成 dict 会比较容易理解），键 key 与值 value 都是字符串。

\#\#\# **操作流程**

> 安装    pip install lmdb   
> 使用时    import lmdb   
> 概括地讲，操作 LMDB 的流程是：
> - 打开环境    env = lmdb.open()
> - 建立事务    txn = env.begin()
> - 插入和修改  txn.put(key, value)
> - 进行删除    txn.delete(key)
> - 进行查询    txn.get(key)
> - 进行遍历    txn.cursor()
> - 提交更改    txn.commit()
>   注意上次 commit() 之后要用 env.begin() 更新 txn 。

简单示例：  
<img src="/images/2018-07/05_02_lmdb_img1.png" height="60%" width="60%">  
<img src="/images/2018-07/05_02_lmdb_img2.png" height="60%" width="60%">


## References

<font color=Magenta> important </font>
[Python操作SQLite/MySQL/LMDB/LevelDB](https://www.jianshu.com/p/66496c8726a1)  

[lmdb 安装](http://www.voidcn.com/article/p-badyeacd-ty.html)  
[lmdb 安装](https://blog.csdn.net/yuanchheneducn/article/details/52934746)  
[Python lmdb](http://www.voidcn.com/article/p-uvbflary-bes.html)  
[lmdb -- python](http://www.voidcn.com/article/p-qeyubiym-dq.html)  
[python lmdb 使用](http://www.voidcn.com/article/p-npjzqwyd-sc.html)  

[lmdb 简介](https://www.jianshu.com/p/yzFf8j)  
[caffe 为什么要使用 lmdb 数据库？](https://www.zhihu.com/question/41854215)  


# MongoDB

ref: [MongoDB 简介](http://www.runoob.com/mongodb/mongodb-intro.html)  

MongoDB 是一个基于分布式文件存储的开源数据库系统，由 C++ 语言编写。  
在高负载的情况下，添加更多的节点，可以保证服务器性能。  
MongoDB 旨在为 Web 应用提供可扩展的高性能数据存储解决方案。  
MongoDB 将数据存储为一个文档，数据结构由键值 (key=>value) 对组成。  
MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。  
<!-- <img src="http://www.runoob.com/wp-content/uploads/2013/10/crud-annotated-document.png" height="60%" width="60%"> -->
<img src="/images/2024-12/crud-annotated-document.png" height="60%" width="60%">

**主要特点**：  
- 面向文档存储，安装简单，操作容易，且支持多种编程语言 (如：RUBY，PYTHON，JAVA，C++，PHP，C# 等)  
- 可通过本地或网络创建数据镜像，有更强的扩展性  
- 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。  
- GridFS是其中一个内置功能，可用于存放大量小文件。  
- 允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。  
- 索引可以是任意属性，以实现更快的排序，如 FirstName="Sameer",Address="8 Gandhi Road"  
- 支持丰富的查询表达式。  
  - 查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。  
  - 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。  
  - Map/reduce 主要是用来对数据进行批量处理和聚合操作，使用Javascript编写，并可通过db.runCommand或mapreduce命令来执行MapReduce操作  
  - Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。  


## Mongodb 安装

```bash
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927 
$ echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list 
$ sudo apt-get update
$ sudo apt-get install -y mongodb-org
```

> mongo -version  
> mongod  
> pgrep mongo -l  
> sudo systemctl start mongod  
> sudo systemctl status mongod  
> sudo systemctl enable mongod  

<img src="/images/2018-07/07_mongodb_img1.png" height="60%" width="60%">  
<img src="/images/2018-07/07_mongodb_img2.png" height="60%" width="60%">

参考  
[Ubuntu 安装 Mongodb](https://www.jianshu.com/p/5598f1dcbb98)  
[Ubuntu 下 MongoDB 安装与使用教程](http://dblab.xmu.edu.cn/blog/mongodb/)

## Robomongo 安装

[Robomongo 官网](https://robomongo.org/download)  
Robomongo is now Robo 3T 

```bash
wget https://download.robomongo.org/0.9.0/linux/robomongo-0.9.0-linux-x86_64-0786489.tar.gz 
tar -xvf robomongo-0.9.0-linux-x86_64-0786489.tar.gz 
sudo mkdir /usr/local/bin/robomongo
sudo mv robomongo-0.9.0-linux-x86_64-0786489/* /usr/local/bin/robomongo
cd /usr/local/bin/robomongo/bin
./robomongo
```

<img src="/images/2018-07/07_robo3t_img1.png" height="60%" width="60%">  
<img src="/images/2018-07/07_robo3t_img2.png" height="60%" width="60%">  
<img src="/images/2018-07/07_robo3t_img3.png" height="60%" width="60%">

参考  
[How to Install MongoDB on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04)  
[How to install Robomongo from tar.gz file as a program in Ubuntu 15.10](https://stackoverflow.com/questions/35547860/how-to-install-robomongo-from-tar-gz-file-as-a-program-in-ubuntu-15-10)  
[How to install robomongo on Ubuntu](https://askubuntu.com/questions/739297/how-to-install-robomongo-on-ubuntu/781793)

## mongodb 使用

> mongod  
> mongo  
> locate mongo  

开启服务
```bash
$ mongo --dbpath /home/ubuntu/VirtualEnv/mongodb/data/db
```

另一个终端
```bash
$ mongo
```

<img src="/images/2018-07/07_use_db_img1.png" height="60%" width="60%">  
<img src="/images/2018-07/07_use_db_img5.png" height="60%" width="60%">

## pymongo 使用

ref: [pymongo 简易教程](https://zhuanlan.zhihu.com/p/20500518)

**利用 Python 操作 MongoDB 的步骤：**  
(1) 安装 MongoDB  
(2) 在 Python 上装入 pymongo 库  
(3) 在终端中配置数据库   
  > $ mongod --dbpath ~/data  

(4) 浏览器中输入 localhost:27017/ 测试  
  > hocalhost: 27017/  
  > "It looks like you are trying to access MongoDB over HTTP on the native driver port."  
  > 出现 ↑ 信息，说明已经成功，可以开始使用  

(5) 使用 pymongo

**使用 pymongo**  
(1) 连接 MongoClient  
(2) 获取数据库 (database)  
(3) 获取 Collection  
(4) 存储数据  
(5) 从 MongoDB 中调用数据  
(6) 更新数据  
(7) 删除数据  
(8) 计数

### (1) 连接 MongoClient  
使用 pymongo 的第一步首先是连接 Client 来使用服务：
```python
from pymongo import MongoClient
Client = MongoClient()
```

### (2) 获取数据库 (database)  
在 MongoDB 中一个实例能够支持多个独立的数据库，你可以用点取属性的方式来获取数据库，或者通过字典的方式获取：  
```python
db = Client.test_database
db = Client['test_database']
```
(注：'test' 可以换成你想要用的名字，比如 "python_database")

### (3) 获取 Collection  
Collection 是存储在 MongoDB 中的一组文件，同获取 database 一样，你可以用点取属性的方式或者字典的方法获取：  
```python
collection = db.test_collection
collection = db['test_collection']
```

### (4) 存储数据  
在 MongoDB 中，数据是以 BSON 的类型存储的。见下面的 post:  
```python
import datetime
post = ['type':'BSON',
           'date':datetime.datetime.utcnow()]
```
了解完 MongoDB 的数据格式后，你可以通过以下的方式插入数据 (其中 .inserted_id 将返回 ObjectId 对象)：  
```python
document1 = ｛'x':1｝
document2 = ｛'x':2｝
posts = db.posts     #你也可以不这样做，每次通过 db.posts 调用
post_1 = posts.insert_one(document1).inserted_id
post_2 = posts.insert_one(document2).inserted_id
```
每个插入的数据对应一个 ObjectId，可直接查看：  
```python
>>> post_1
ObjectId(...)
>>> post_2
ObjectId(...)
```
你还可以用 insert_many() 插入多个文档：  
```python
new_document = [{'x':3},
                             {'x':4}]
result = posts.insert_many(new_document)

>>> result.inserted_ids
[ObjectId(...),ObjectId(...)]
```

### (5) 从 MongoDB 中调用数据  
find_one() 函数能够从数据库中调出已存储的数据：  
```python
>>> posts.find_one()
['x':'1']
```
但用 find_one() 的方法只能获取一个数据，如果数据库中存在多个数据时，它返回的是第一个的值。你也可以通过 ObjectId 来请求数据，效果和上面是一样的。如果你想打印出全部数据，可以通过迭代的方式获取：  
```python
>>> for data in posts.find():
            data
>>> 
{u'x':1,
u'x':2,
u'x':3,
u'x':4}
```
你也可以加入限制性因素来获取特定的数据：  
```python
>>> for post in posts.find({'x':1}):
>>>      post
>>>
{u'x':1}
```
查找条件中也可以用正则匹配来匹配 value。

### (6) 更新数据  
在 pymongo 中可以用 update_one() 来更新数据：  
```python
>>> posts.update_one({'x':4},{'$set':{'x':3}})
```
其中传入的第一个参数是你想要更新的数据，第二个是你想要更新的最新数据。其中 $set 部分是必要元素，如果没有会报出错误。除了 $set 外还有很多其它的比如 $inc，对应着不同的功能，在此先不赘述。  
上面只是更新匹配到的第一个数据，同样地，也可以用 update_many() 一次更新多个值。

### (7) 删除数据  
同上，可以用 delete_one() 和 delete_many() 方法来删除数据，括号中是筛选条件：  
```python
>>> posts.delete_one({'x':3})
>>> posts.delete_one({'x':2})
```

### (8) 计数  
如果想知道 collection 中有多少文档，可以用 .count() 请求来获取符合条件的文档。  
```python
>>> posts.count()
4
>>> posts.find({'x':1})
1
```


# Sublime Text 3 插件配置

ref: [左侧显示目录树](https://www.zhihu.com/question/23427839)  
```bash
(1) Open folder
(2) 安装 SideBarEnhancements 插件后，View -> Side Bar -> Show Side Bar
```

安装 Sublime text 3 插件很方便，可以直接下载安装包解压到 Packages 目录 (菜单 -> Preferences -> Browse Packages)；也可以安装 package control 组件，然后直接在线安装。

## 安装 package control 

按 Ctrl+`(此符号位于 tab 按键上面)调出 console (注：避免热键冲突)   
粘贴以下代码到命令行并回车：  
```bash
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
下载完成之后重启 Sublime Text 3。  
如果在 Perferences -> 中看到 package control 这一项，则安装成功。

**用 Package Control 安装插件的方法**  
按下 Ctrl+Shift+P 调出命令面板；  
输入 install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。

**安装 常用插件**  
utf8  
EMMET  
sidebarenhancements  
ctags  自动补全代码  

参考  
[让你用sublime写出最完美的python代码--windows环境](https://www.cnblogs.com/zhaof/p/8126306.html)  
[Ubuntu16.04下使用sublime text3搭建Python IDE](https://www.cnblogs.com/unflynaomi/p/5704293.html)  
[Sublime Text 3安装及常用插件安装](https://blog.csdn.net/wxl1555/article/details/69941451)  
[sublime 跳转到函数定义: ctags](https://blog.csdn.net/mxdzchallpp/article/details/80054026)


## 安装常用插件

### (1) 代码分析:  SublimeLinter-flake8 

功能：  
(1) 分析语法错误；
(2) 分析代码结构问题 (如使用没有定义的变量)；
(3) 分析不符合规范和美观的代码 

Flake8 是一个需要独立安装的命令行工具。在安装 Flake8 之后，再为 Sublime 安装 SublimeLinter 和 SublimeLinter-flake8 插件。  
```bash
$ pip install flake8
$ flake8 --help
//$ pip install --upgrade flake8  #升级插件
$ pip3 install flake8
```

SublimeLinter 是 Sublime 的代码框架，它可以集成 Flake8 这样的 linter 引擎来检查我们的代码，
并可以把它们的消息转换成 Sublime Text 然后把它们显示在我们代码旁边。  
SublimeLinter 可以让 Flake8 和 Sublime Text 成为一个非常完美的搭档，可以直接在代码编辑器里看到 Flake8 的消息。 

所以首先我们需要安装 SublimeLinter，然后我们将安装连接 Flake8 和 SublimeLinter 的 SublimeLinter-flake8  
```bash
(1) 通过 ctrl+shift+p 进入，并输入 install package，然后回车
(2) 初次会慢点，然后出现提示
(3) 输入要安装的 SublimeLinter，选择并安装
(4) 插件安装完成后会出现一个 Package Control Messages 提示，重启 Sublime 后生效
```

现在需要将 SublimeLinter 和 Flake8 集成连接起来，这里就通过 SublimeLinter-flake8 插件来完成
同样的,和上一个插件安装方法类似也是通过 ctrl+shift+p 进入，并输入 Flake8：  
安装完成后重启生效。  
为了让它更好用，还需要对 SublimeLinter-flake8 做一些简单配置

"mark_style": "outline" -> "squiggly_underline"  
"lint_mode": "background" -> "load_save"

### (2) 代码自动补全:  Anaconda 

功能：  
(1) 代码的自动补全  
(2) 显示 python 类、方法或者函数的使用方法  
(3) 检查导入模块是否有效  
(4) 按照 PEP8 规范自动化格式我们的代码  
(5) 可以跳转到函数的定义或者类的定义  
(6) ……

**Install the Anaconda Package**  
安装同上，重启后生效。  
简单配置：  
```python
{
  "anaconda_linting": false,
  "pep8": false,
  "python_interpreter": "/usr/bin/python3",
  "suppress_word_completions": true,
  "suppress_explicit_completions": true,
  "complete_parameters": false,
}
```
上述配置是因为这个插件和 flake8 插件的功能相互冲突，这里最好使用 flake8 的配置就可以了

## 建立新的运行环境

ref: [Ubuntu 16.04下指定Sublime Text 3 默认python编译版本](https://www.jianshu.com/p/d612f8da3ffa)

\#\#\# **安装 PackageResourceViewer 插件**

> 1. 输入 Ctrl+Shift+P  
> 2. 输入 install，选择 Package Control:  Install Package  
> 3. 选择 PackageResourceViewer，安装

\#\#\# **设置默认的 Python.sublime-build**

> 1. 输入 Ctrl+Shift+P  
> 2. 输入 resource，选择 PackageResourceViewer: Open Resource  
> 3. 再选择 Python，再再选择 Python.sublime-build  
> 4. 编辑 Python.sublime-build 将 "shell_cmd": "python -u \"$file\"", 改为以下之一：  
```python
"shell_cmd": "python3 -u \"$file\"", //指定python3为.py默认编译器
"shell_cmd": "python2 -u \"$file\"", //指定python2为.py默认编译器
"shell_cmd": "python -u \"$file\"", //根据Ubuntu系统设置，看/usr/bin/python链接哪儿(ln)
"shell_cmd": "指定版本python的绝对路径 -u \"$file\"", //指定路径下的python编译器
```
> 5. 使用 python3 的配置文件示例 (Python.sublime-build)  
```python
{
  //"shell_cmd":"python -u \"$file\"",
  "shell_cmd":"python3 -u \"$file\"",  //指定python3为.py默认编译器
  "file_regex":"^[ ]*File \"(...*?)\", line ([0-9]*)",
  "selector":"source.python",
  "env":{"PYTHONIOENCODING":"utf-8"},
  "variants":[{
      "name":"Syntax Check",
      "shell_cmd":"python -m py_compile \"${file}\"",
    }
  ]
}
```
> 6. Ctrl+S 保存配置文件  
>   注：有关 .sublime-build 的配置信息说明，可参见  
> 7. 重启 Sublime Text 3  
> 8. 打开 .py 文件，Ctrl + B 即可编译执行
>   方便、顺眼多了

\#\#\# **与其他方法的使用比较**

网上也有其他变通方法，可参考以下链接  
[ubuntu 下 sublime text 3 加入 python3 环境支持]()  
[指定 ubuntu 下的 python 运行版本](http://www.cnblogs.com/vingi/articles/2997043.html)

前者，每次编译时选择麻烦  
后者，改系统默认配置，可能引发其他依赖异常  
本文 ctrl+b 可直接编译运行，又不改系统默认配置，简单方便，是合适的解决办法

## Tools > Build System > Python2/3

安装 Package Control  
<img src="/images/2018-07/07_sublime_img1.png" height="60%" width="60%">  

更改 Python.sublime-build  
<img src="/images/2018-07/07_sublime_img2.png" height="60%" width="60%">  

建立新的运行环境  
<img src="/images/2018-07/07_sublime_img3.png" height="60%" width="60%">  

存储位置在 Browse Package > User 中  
<img src="/images/2018-07/07_sublime_img4.png" height="60%" width="60%">  

参考  
[sublime text 3 如何配置自己的 build-system，在命令行中运行 python ](https://www.yalewoo.com/sublime_text_3_python_build_system.html)  
[Sublime 编辑器中集成多个 python 版本](http://qihoo.pro/sublime-with-multiversion-python.html)  
[sublime 运行 python 文件简单配置与安装](https://blog.csdn.net/u012905422/article/details/52526640)  
[Sublime 深度定制：build system 的妙用](https://www.jianshu.com/p/c9d76fe898c8)  


## anaconda 不能自动补全第三方库

参考  
[Sublime Text 3 配置 python 开发环境遇见的问题](http://www.voidcn.com/article/p-owbfoovb-ue.html)  
[mac sublime anaconda 不能自动补全第三方库](http://blog.5ibc.net/p/30141.html)  

错因是系统有两个 Python，所以使用 anaconda 插件的 Go to definition 功能时，会跳转到系统自带的 python 那里去，也就是说，这个时候的 anaconda 能够对系统自带的库 work well，但是对我想使用的 python3(非系统路径python) 的库就不行。   
其原因在于，anaconda 依赖于 sublime 的 Python inerpreter，sublime 调用什么 Python，anaconda 就搜寻这个 Python 的库。  
这时就需要更改 sublime 的 Python interpreter，不同环境下使用不同的 Python，解决方法有三种：  
(1) 更改 python.sublime-build  
(2) 更改 project configuration  
注：sublime 的 project 很重要，很多插件都是在 project 下才有用的，比如侧边栏增强的那个插件，你的文件要是不在 project 里，装了跟没装一样。其实我现在也没搞明白这个 project 的配置，anaconda 是推荐在 project 里配置，这样不同的 project 有不同的配置，但是我发现在里面写没作用。   
(3) 改全局配置，打开 anaconda 的 user 配置  
我的解决方案是 (1,3) 双管齐下才有效




# Node.js 

ref: [Node.js 教程](http://www.runoob.com/nodejs/nodejs-tutorial.html)

简单的说 Node.js 就是运行在服务端的 JavaScript。  
Node.js 是一个基于 Chrome JavaScript 运行时建立的一个平台。  
Node.js 是一个事件驱动 I/O 服务端 JavaScript 环境，基于 Google 的 V8 引擎，V8 引擎执行 Javascript 的速度非常快，性能非常好。

什么情况下 Node.js 是个非常好的选择？  
对于前端程序员，不懂得像 PHP、Python 或 Ruby 等动态编程语言，但是想创建自己的服务，……  
对于后端程序员，想部署一些高性能的服务，……

\#\# **安装 (failed)**

```bash
$ sudo apt-get install nodejs
$ sudo apt-get install npm
$ nodejs --version
v4.2.6
$ npm --version
3.5.2
```
但是这个版本太低了，安装 electron 失败。

于是升级。
```bash
$ sudo npm install npm@latest -g
$ sudo apt-get install node-legacy
$ node --version         #$ node -v
v4.2.6
$ sudo npm install -g n  #failed!
$ sudo n stable          #找不到命令
```
但是这个还是原来的旧版本，没有升级成功。

\#\# **安装** 

ref: [官网说明](https://nodejs.org/zh-cn/download/package-manager/#debian-and-ubuntu-based-linux-distributions)

```bash
$ sudo apt-get install curl
$ curl 
$ sudo apt-get install -y nodejs
$ node -v
v10.6.0
$ npm -v
6.1.0
```

安装 electron
```bash
$ git clone https://github.com/electron/electron-quick-start
$ cd electron-quick-start
$ npm install
$ npm start
```

<img src="/images/2018-07/07_weibo_img1.png" height="60%" width="60%">  
<img src="/images/2018-07/07_weibo_img2.png" height="60%" width="60%">  
<img src="/images/2018-07/07_weibo_img3.png" height="60%" width="60%">



# 其它问题

ref: [无法锁定管理目录(/var/lib/dpkg/)，是否有其他进程正占用它？](https://blog.csdn.net/ping523/article/details/54945083)

Error:  
E: 无法获得锁 /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)  
E: 无法锁定管理目录(/var/lib/dpkg/)，是否有其他进程正占用它？ 

解决方法一：  
\#:ps -aux (列出进程，形式如)  
root 5765 0.0 1.0 18204 15504 ? SN 04:02 0:00 apt-get -qq -d  
找到最后一列以apt-get 开头的进程  
\#:sudo kill -9 该进程的PID 

解决方法二：  
\#:sudo rm /var/cache/apt/archives/lock  
\#:sudo rm /var/lib/dpkg/lock 
