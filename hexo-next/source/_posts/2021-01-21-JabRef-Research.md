---
title: 好用的科研小工具 (个人喜好)
date: 2021-01-21 20:01:28
updated: 2021-01-21 20:01:28
categories:
  - Efficiency
tags:
  - Kindle
mathjax: false
---

<!--
极简之梦中情“屋”
tags: Life,
tags: iOS, Windows

2021/1/31 17:04pm Sun, Productivity
-->


# LaTeX

不用讲了吧，磕盐民工码文必备利器。本地机用的是 texlive + texstudio, 其中 texstudio 可以配置语法自动检查，提示高亮。以前配置过，当时没记录。不过我现在都转到 overleaf 然后云端备份了。  

Overleaf 里我建了几个不同的文件夹，感觉它的文件夹相当于是标签，一个项目可以同时属于两个标签。比如说为了方便分类，可以用 In Progress / Under Review / Reject & Resubmit / Prepare A Major Revision / Accepted 等来区分。Overleaf 文件夹的颜色是默认生成的，无法自定义改变，觉得颜色不满意只能删掉重新创建了，碰运气看能不能碰出个喜欢的。此外 overleaf 时不时就会来个掉线也是有点烦

参考文献用 .bib ，整理时推荐使用 JabRef 3.8.2, 表用最新版 5.2, 不好使。安装后设置：
- Perferences
  - Groups: Initially show groups tree expanded 取消勾选
  - Entry editor: 勾选 Show BibTeX source by default
  - Entry table columns: 勾选 Show priority (将之移动到 ranking 之前)
- 点选图标使之显示 groups tree
- Groups Setting
  - 选择 Intersection
  - 选择 Hide non-hits
  - 勾选 Show number of elements contained in each group
  - 勾选 Automatically assign new entry to selected groups

JabRef 3.8.2 有个缺点是重新安装后 groups tree 不会自动生成，但是可以 move to group; 相比之下 JabRef 5.2 不停提示有别的程序改动文件，且 saving library 极慢，不能自如移动分组 (只能手动输入)，不能显示颜色等问题烦人得多了。所以我最后又卸了最新版回到了 3.8.2. 其实早些年我用 3.8.2 也存在有点反应迟钝的问题，但是我记不太清楚是当时版本是 4 的问题，还是 3.8 也有，不过现在基本已经没有反应迟钝了。而且 3.8.2 还可以自动提示有重复项 (方便合并)。我最新装的是 Java 8, 其实以前也是，不知道有没有关系。而且老版搜索、添加项、合并项等都十分方便，反而衬得最新版界面胖得有些臃肿，搜索和添加项都不是很顺手。最关键的是保存实在是太烦人了。

习惯 latex 之后再看 word 就十分不顺眼，可能我太过强迫症…… 所以这就遗留下一个问题就是我得学会怎么写 .cls 格式，不然用 word 真的又烦又难看


# Servers

推荐 Bitvise SSH Client 和 Cmder 结合使用，当然要在本地配好 ssh 免密登录。  
Bitvise SSH Client 方便查看服务器端代码执行后产生的结果，下载文件也不会影响其最后修改时间。否则就只能在服务器端 zip 压缩文件后下载本地再解压。  
Cmder 更方便于直接 ssh 免密登录，这样不过需要在服务器上执行命令的话，不需要每次都用 Bitvise SSH Client 客户端。

调试代码的话，可以直接用 VSCode 连接到服务器上调试，我认为这种方法 debug 起来是最方便的。PyCharm 可以在本地写好测试完，自动上传到服务器，也可以远程调试 (但是方便程度略有不如)。  
也可以用 git, 在本地改好代码后 git push 上传，然后在服务器端 git pull, 最后用 .sh 脚本执行命令。

代码执行过程中常用的命令有：
```shell
$ htop
$ watch -n 10 nvidia-smi
$ ps -ef | grep xxxx
```

实验数据结果推荐用 Google Docs 里的表格存储到 Google Drive, 我一般会用 Google Slices 记录下工作进度和计划等，都放到一个文件夹里，方便日后查阅。  
每一次新提交的论文，实验结果等相关资料都创建一个新的文件夹，overleaf 创建一个新的项目，这样相当于人工分成若干个分支，便于后续查找不同的版本记录。


# Chrome

插件我推荐这些
- Pinned
  - AdBlock: 屏蔽广告
  - OneTab: 存储希望关掉的页面以备后续查看
  - Google Gmail Checker
  - Google Calendar
  - Worldtime: 跨时区查看时间, 可同时显示
  - FireShot - Capture page: 捕捉网页截图
- Enabled
  - Find Code for Research Papers - CatalyzeX
  - Free Download Manager
  - Google 文档的离线功能
  - // Google 翻译
  - // Google 学术搜索按钮
  - Keepa - Amazon Price Tracker
  - Proxy SwitchyOmega

应用 url `chrome://apps`
- Awesome
  - 马克飞象
  - Google 绘图
  - Google Keep
- Laptop
  - Any.do
  - Readium
  - Google Keep
  - Evernote Web
  - StackEdit
  - Gantter
  - Google 协作平台
- Desktop
  - 有道云笔记网页版
  - Telegram
  - Google Drive
  - TensorFlow
  - Asana


# Kindle

打开 Goodreads, 记录阅读进度。  
自己邮箱传送的电子书，除非是非常好的书籍可以反复阅读的，其他的读完后全部永久删除。备份邮箱都有，不需要额外占用空间，找起书来也麻烦。  
购买的免费书可以适当删除，真金白银买的书就最好删掉本地文件就可以了，想再阅读时再下载。
