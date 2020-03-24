---
title: Git, Markdown, Linux, Vim 常用命令汇总
date: 2018-07-08 13:44:55
updated: 2018-07-08 23:41:52
categories:
  - Records
tags:
  - Commands
  - Linux
  - Git
  - Markdown
---

[comment]: <> (updated: Git, Markdown, Linux, Vim 常用命令汇总)
[comment]: <> (2018-07-08-Git-Markdown-Linux-Vim.md)
[comment]: <> (/images/2018-07/09_git_commit_a.png)



# Git & GitHub


## 问题汇总

\#\#\# **git 为不同的项目设置不同的用户名** 

ref: [git为不同的项目设置不同的用户名](https://blog.csdn.net/xiaoliu665114/article/details/66969957)

不能采用通用配置时，就要单独设置每个项目的 git 配置。

(a). 每个 git 项目下都会有一个隐藏的 .git 文件夹 ，  
将终端的工作目录设置到相应的项目根目录下，执行 ls -a 命令，显示所有文件，即可看到 .git 的隐藏文件夹。  
通过 cd .git 进入该目录，发现该目录下有个 config 文件，采用 open config 命令打开，添加如下配置：  
```bash
[user]
    name = XXX(自己的名称英文)
    email = XXXX(邮箱)
```
保存，command+s 即可。  
这时候就为该项目配置了独立的用户名和邮箱。提交代码时，提交日志上显示的就是设置的名称，当然 github 这种会根据设置的邮箱来设置对应的用户名。

(b). 通过命令行的方式 (即要去掉 --global 参数) 去设置单独的 git 配置，只需要在 .git 文件夹下。 例如执行如下命令，就可以修改当前项目提交代码时用到的用户名。  
```shell
git  config  user.name  "xxxxx"
```

如果全局的配置和当前项目的单独配置中出现相同的配置选项，比如全局和项目都设置了 user.name ，那么在该项目中进行 git 操作时，会默认采用该项目配置的用户名。


\#\#\# **^X 离开**

ref: [sudo 简介](https://blog.csdn.net/YQXLLWY/article/details/55214943)

```bash
$ git commit -a
```
出现问题，该界面无法离开  
<img src="/images/2018-07/09_git_commit_a.png">

这些命令的执行方式是：Esc，然后命令中的 ^ 代表 Alt，如离开 ^X ，就需要依次按 Esc, Alt x ，这样才会退出，有点像 vim。



\#\#\# **next**


## 常用 Git 命令清单

ref: [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

日常使用的 6 个命令  
![git](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

专有名词：  
- Workspace：工作区  
- Index / Stage：暂存区  
- Repository：仓库区（或本地仓库）  
- Remote：远程仓库  

### 一、新建代码库 

```bash
# 在当前目录新建一个Git代码库
$ git init

# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]

# 下载一个项目和它的整个代码历史
$ git clone [url]
```

### 二、配置 

Git 的设置文件为 .gitconfig ，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。  
```bash
# 显示当前的Git配置
$ git config --list

# 编辑Git配置文件
$ git config -e [--global]

# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

### 三、增加/删除文件

```bash
# 添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录的所有文件到暂存区
$ git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p

# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...

# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```

### 四、代码提交

```bash
# 提交暂存区到仓库区
$ git commit -m [message]

# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
```

### 五、分支

```
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

### 六、标签

```bash
# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```

### 七、查看信息

```bash
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log

# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat

# 搜索提交历史，根据关键词
$ git log -S [keyword]

# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature

# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]

# 显示指定文件相关的每一次diff
$ git log -p [file]

# 显示过去5次提交
$ git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
$ git blame [file]

# 显示暂存区和工作区的差异
$ git diff

# 显示暂存区和上一个commit的差异
$ git diff --cached [file]

# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD

# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]

# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"

# 显示某次提交的元数据和内容变化
$ git show [commit]

# 显示某次提交发生变化的文件
$ git show --name-only [commit]

# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]

# 显示当前分支的最近几次提交
$ git reflog
```

### 八、远程同步

```bash
# 下载远程仓库的所有变动
$ git fetch [remote]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
```

### 九、撤销

```bash
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
```

### 十、其他

```bash
# 生成一个可供发布的压缩包
$ git archive
```








# Markdown

**编辑器**  
[Atom](https://atom.io/)  
[Mou](http://25.io/mou/)  
[typora](https://typora.io/)

**png 图片在线压缩**  
[PNG压缩](https://compresspng.com/zh/)  
[调整单个图像文件](https://www.iloveimg.com/zh-cn/resize-image)  
[压缩图](https://www.yasuotu.com/png)

## 基本语法

参考  
[Markdown 书写风格指南](http://einverne.github.io/markdown-style-guide/zh.html)  
[Intro to Markdown, 代码块和语法高亮](http://xianbai.me/learn-md/article/extension/code-blocks-and-highlighting.html)  
[Markdown 书写建议](https://sspai.com/post/37271)

\#\#\# **通用规则**

文件名建议使用如下的风格:  
- 用小写代替大写  
- 把开头 the, a, an 除去  
- 用连字符代替标点和空格  
- 用一个连字符代替连续多个连字符，当多个连字符出现时，只使用一个  
- 不在文件名前后使用连字符

引用：在符号 > 后面接一个空格。不要在单独的引用中使用空行。  
列表：  
(1) 无序使用连字符 "-"，不建议使用 "\*" (可能和加粗和斜体符号产生混淆) 和 "+" (不流行)  
(2) 有序尽量选用 "1."，除非打算通过数字在相同 Markdown 文件或者外部文件中引用他们。  
(3) 尽量使用无序列表，除非有通过数字引用的需求。最佳则是从来不通过符号来引用它们。  

\#\#\# **常用语法**

(1) 段落与换行  
段落前后：空行，即行内什么都没有或只有空白符 (空格或制表符)  
段落内加入换行 (\<br>): 可在前一行末尾加入至少两个空格，然后换行写其它文字  
Markdown 中的多数区块都需要在两个空行之间。

(2) 标题  
Setext 形式 (多个 = 或 -，分别支持 h1,h2 两种标题)  
atx 形式 (\#: 对称形式，或只在左边使用)，注意 \# 左侧不可有任何空白，内侧可以

(3) 引用  
引用内容：段落或内容前使用 \> 符号  
多行引用：每行前加，或仅在第一行使用 (后面相邻行可省略)；如需换行，可行尾添加两个空格，或在引用内容中加一个空行  
嵌套使用：
```markdown
>也可以在引用中
>>使用嵌套的引用
```
其他 Markdown：引用中可使用其他任何 Markdown 语法

(4) 列表  
无序列表项的开始：符号('\*', '\+', 或 '\-') 空格；  
有序列表项的开始：数字 . 空格；  
空格至少为一个，多个空格将被解析为一个，如果仅需要在行前显示数字和 '.' ：  
```markdown
05\. 可以使用：数字\. 来取消显示为列表
```
嵌套的列表：
```markdown
1. 第一层
  + 1-1
  + 1-2
```
> \* 的语法专门用来显示 Markdown 语法中使用的特殊字符，参考 [字符转义](http://xianbai.me/learn-md/article/syntax/blackslash-escapes.html)

(5) 代码  

(6) 分隔线  
一行内使用三个或更多，增加分隔线 (\<hr>)  
```markdown
***
------
___ 	//下划线
```
多个字符之间可以有空格 (空白符)，但不能有其他字符  
```markdown
* * *
- - -
```

(7) 超链接  
行内式：title 可以使用 ' 或 "  
```markdown
[title text](URL 'link text')
```
参考式：(1) 能尽量保持文章结构的简单，也方便统一管理 URL； (2) 优点：可以在多个不同的位置引用同一个 URL  
```markdown
[Google][link]
[link]: http://www.google.com/ "Google"
识别符可以是字母、数字、空白或标点符号，不区分大小写
格式：  [识别符]: URL 'title'

[Google][]
[Google]: http://scholar.google.com/ "Google"
省略识别符，使用链接文本作为识别符
```
自动链接：适合行内较短的链接，会使用 URL 作为链接文字。邮箱地址会自动编码，以逃避抓取机器人。
```markdown
<http://www.google.com/>
<123@email.com>
```

(8) 图片  
```markdown
![Name](https://...)
```
同插入超链接的语法基本一致，也分行内式和参考式两种  
```markdown
![GitHub](https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding")
方括号中的部分是图片的替代文本，括号中的 'title' 部分和链接一样，是可选的。

![GitHub][github]
[github]: https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding"
```
指定图片的显示大小  
```html
Markdown 不支持指定图片的显示大小，不过可以通过直接插入<img />标签来指定相关属性：
<img src="https://avatars2.githubusercontent.com/u/3265208?v=3&s=100" alt="GitHub" title="GitHub,Social Coding" width="50" height="50" />
```

(9) 强调  
*斜体*    **粗体**    ***强调***  

(10) 字符转义  

\#\#\# **扩展语法**

(1) 删除线
```markdown
这就是 \~~删除线\~~
这就是 ~~删除线~~
```
这就是 ~~删除线~~

(2) 代码块和语法高亮

(3) 表格 和对齐
```markdown
|    name    | age |
| ---------- | --- |
| LearnShare |  12 |
| Mike       |  32 |

| left | center | right |
| :--- | :----: | ----: |
| aaaa | bbbbbb | ccccc |
| a    | b      | c     |
```

(4) Task List
```markdown
- [ ] Eat
- [x] Code
  - [x] HTML
  - [x] CSS
  - [x] JavaScript
- [ ] Sleep
```





## 常见问题

\#\#\# **代码块加入行号和支持语言**

加入行号只需用三个 "`" 框入即可

[前端：给你的 Markdown 文章添加代码高亮及行号](https://www.jianshu.com/p/aaad9a3f619b)  
[重构 Markdown 代码块文档结构以支持行号显示](https://blog.bluerain.io/p/markdown-code-block-line-number.html)  
[Markdown 入门](http://www.dongye.tk/2014/10/11/markdown-intro/)

[Markdown代码高亮支持的语言](https://www.jianshu.com/p/f02d5a3736ba)  
[markdown代码块支持的语言](http://www.cnblogs.com/qyf404/p/5019631.html)

\#\#\# **显示 bash/shell 代码**

ref: [在 markdown 中突出显示 bash/shell 代码](https://codeday.me/bug/20170706/34249.html)

取决于 markdown 渲染引擎和 markdown 的味道。没有标准。如果你的意思是 github flavored markdown 例如，shell 应该工作正常。别名是 sh，bash 或 zsh。您可以找到可用的语法词法列表 [here](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)

\#\#\# **显示 颜色块**

ref:  
[为什么 markdown 不支持字号和字体颜色？](https://www.zhihu.com/question/22504694)  
[Markdown 使用技巧总结](https://blog.csdn.net/u010177286/article/details/50358720)  

```html
<font color=red>内容</font>
<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>
```
但是字体颜色和颜色块都显示不出来



# Linux

- 参考手册：Linux 命令大全  
- Linux 教程  
- Shell 教程  

ref: [Linux 命令大全](http://www.runoob.com/linux/linux-command-manual.html)


## 文件

\#\#\# **1、文件管理**

cat 命令用于连接文件并打印到标准输出设备上。  
Linux/Unix 的文件调用权限分为三级 : 文件拥有者、群组、其他。利用 chmod 可以藉以控制文件如何被他人所调用。  
chown 将指定文件的拥有者改为指定的用户或组。使用权限是 root。  
locate 命令用于查找符合条件的文档，它会去保存文档和目录名称的数据库内，查找合乎范本样式条件的文档或目录。  
cp 命令主要用于复制文件或目录。  
mv 命令用来为文件或目录改名、或将文件或目录移入其它位置。  
rm 命令用于删除一个文件或者目录。  
which 命令用于查找文件。该指令会在环境变量 $PATH 设置的目录里查找符合条件的文件。  
whereis 命令用于查找文件。该指令会在特定目录中查找符合条件的文件。这些文件应属于原始代码、二进制文件，或是帮助文件。该指令只能用于查找二进制文件、源代码文件和 man 手册页，一般文件的定位需使用 locate 命令。  
rcp 命令用于复制远程文件或目录。rcp 指令用在远端复制文件或目录，如同时指定两个以上的文件或目录，且最后的目的地是一个已经存在的目录，则它会把前面指定的所有文件或目录复制到该目录中。  
scp 命令用于 Linux 之间复制文件和目录。scp 是 secure copy的缩写,scp 是 linux 系统下基于 ssh 登陆进行安全的远程文件拷贝命令。  

cmp 命令用于比较两个文件是否有差异。  
cut 命令用于显示每行从开头算起 num1 到 num2 的文字。
diff 命令用于比较文件的差异。逐行比较文本异同，如指定比较目录，则比较相同文件名的文件，但不比较其中的子目录。  
diffstat 命令根据diff的比较结果，显示统计数字。  
file 命令用于辨识文件类型。  
find 命令用来在指定目录下查找文件。如不指定参数，则在当前目录下查找子目录与文件。  
git 命令是文字模式下的文件管理员。  
less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。  
more 命令类似 cat ，不过会以一页一页的形式显示，更方便使用者逐页阅读，而最基本的指令就是按空白键（space）就往下一页显示，按 b 键就会往回（back）一页显示，而且还有搜寻字串的功能（与 vi 相似），使用中的说明文件，请按 h 。  
od 命令用于输出文件内容。它读取所给予的文件的内容，并将其内容以八进制字码呈现出来。  
paste 命令用于合并文件的列。  
patch 命令用于修补文件。  
touch 命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。 ls -l 可以显示档案的时间记录。  
slocate 命令查找文件或目录，本身有一个数据库，里面存放了系统中文件与目录的相关信息。  
split 命令用于将大文件分割成较小的文件，在默认情况下按照每 1000 行切割。  
tee 命令用于读取标准输入的数据，并将内容输出到标准输出设备，同时保存成文件。  
read  命令用于从标准输入读取数值。  

\#\#\# **2、文档编辑**

grep 命令用于查找文件里符合条件的字符串。
egrep 命令用于在文件内查找指定的字符串。其表达比 grep 更规范。  
rgrep 命令用于递归查找文件里符合条件的字符串。  
sort 命令用于将文本文件内容加以排序。可针对文本文件的内容，以行为单位来排序。  

join 命令用于将两个文件中，指定栏位内容相同的行连接起来。  
look 命令用于查询单词。  
spell 命令可建立拼写检查程序。可从标准输入设备读取字符串，结束后显示拼错的词汇。  
uniq 命令用于检查及删除文本文件中重复出现的行列。  
let 命令是 BASH 中用于计算的工具，用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量。如果表达式中包含了空格或其他特殊字符，则必须引起来。  
wc命令用于计算字数。可以计算文件的 Byte 数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则 wc 指令会从标准输入设备读取数据。  

\#\#\# **3、文件传输**

ftp 命令设置文件系统相关功能。FTP 是 ARPANet 的标准文件传输协议，该网络就是现今 Internet 的前身。  
bye 命令用于中断 FTP 连线并结束程序。在 ftp 模式下，输入 bye 即可中断目前的连线作业，并结束 ftp 的执行。  
tftp 命令用于传输文件。  

## 磁盘

\#\#\# **4、磁盘管理**

cd 命令用于切换当前工作目录至 dirName (目录参数)。  
mkdir 命令用于建立名称为 dirName 之子目录。  
ls 命令用于显示指定工作目录下之内容（列出目前工作目录所含之文件及子目录)。  

df 命令用于显示目前在 Linux 系统上的文件系统的磁盘使用情况统计。  
mount 命令是经常会使用到的命令，它用于挂载 Linux 系统外的文件。  
mount 命令是经常会使用到的命令，它用于挂载 Linux 系统外的文件。  

stat 命令用于显示 inode 内容。  
lndir 命令用于连接目录内容。  

\#\#\# **5、磁盘维护**

sync 命令用于数据同步，在关闭 Linux 系统时使用。  

## 网络

\#\#\# **6、网络通讯**

ifconfig 命令用于显示或设置网络设备。  
ping 命令用于检测主机。执行 ping 指令会使用 ICMP 传输协议，发出要求回应的信息，若远端主机的网络功能没有问题，就会回应该信息，因而得知该主机运作正常。  

## 系统

\#\#\# **7、系统管理**

exit 命令用于退出目前的 shell。  
kill 命令用于删除执行中的程序或工作。  
su 命令用于变更为其他使用者的身份，除 root 外，需要键入该使用者的密码。  
sudo 命令以系统管理者的身份执行指令，也就是说，经由 sudo 所执行的指令就好像是 root 亲自执行。  
shutdown 命令可以用来进行关机程序。  
reboot 命令用于用来重新启动计算机。  

date 命令可以用来显示或设定系统的日期与时间。  
id 命令用于显示用户的 ID，以及所属群组的 ID。  
who 命令用于显示系统中有哪些使用者正在上面，显示的资料包含了使用者 ID、使用的终端机、从哪边连上来的、上线时间、呆滞时间、CPU 使用量、动作等等。  
logout 命令用于退出系统。  
free 命令用于显示内存状态。会显示内存的使用情况，包括实体内存，虚拟的交换文件内存，共享内存区段，以及系统核心使用的缓冲区等。  

useradd 命令用于建立用户帐号。  
userdel 命令用于删除用户帐号。  
usermod 命令用于修改用户帐号。  
userconf 命令用于用户帐号设置程序。  
uname 命令用于显示系统信息。  
skill 命令送个讯号给正在执行的程序，预设的讯息为 TERM (中断)，较常使用的讯息为 HUP、INT、KILL、STOP、CONT 和 0。  

\#\#\# **8、系统设置**

clear 命令用于清除屏幕。  
alias 命令用于设置指令的别名。  
export 命令用于设置或显示环境变量。  
ulimit 命令用于控制shell程序的资源。  

enable 命令用于启动或关闭 shell 内建指令。  
time 命令的用途，在于量测特定指令执行时所需消耗的时间及系统资源等资讯。  
reset 命令其实和 tset 是一同个命令，它的用途是设定终端机的状态。  

## 设备

\#\#\# **9、备份压缩**

tar 命令用于备份文件。  
zip 命令用于压缩文件。  

\#\#\# **10、设备管理**

loadkeys 命令可以根据一个键盘定义表改变 linux 键盘驱动程序转译键盘输入过程。  

## 其他

\#\#\# **其他命令 - Linux bc 命令**

ref: [Linux bc 命令](http://www.runoob.com/linux/linux-comm-bc.html)

bc 命令是任意精度计算器语言，通常在 linux 下当计算器用。  
它类似基本的计算器, 使用这个计算器可以做基本的数学运算。

\#\#\# **其他命令 - Linux tail 命令**

ref: [Linux tail 命令](http://www.runoob.com/linux/linux-comm-tail.html)

tail 命令可用于查看文件的内容，有一个常用的参数 **-f** 常用于查阅正在改变的日志文件。  
**tail -f filename** 会把 filename 文件里的最尾部的内容显示在屏幕上，并且不断刷新，只要 filename 更新就可以看到最新的文件内容。



# Vim

ref: [Linux vi/vim](http://www.runoob.com/linux/linux-vim.html)


## vi/vim 的使用

(1)  vi/vim 刚启动时，进入命令模式 

**i** 切换到输入模式，以输入字符。  
**x** 删除当前光标所在处的字符。  
**:** 切换到底线命令模式，以在最低一行输入命令。  

(2)  输入模式 (也称为编辑模式) 

**字符按键以及 Shift 组合**，输入字符  
**Enter**，回车键，换行  
**Back space**，退格键，删除光标前一个字符  
**Del**，删除键，删除光标后一个字符  
**方向键**，在文本中移动光标  
**Home/End**，移动光标到行首/行尾  
**Page Up/Page Down**，上/下翻页  
**Insert**，切换光标为输入/替换模式，光标将变成竖线/下划线  
**Esc**，退出输入模式，切换到命令模式  

(3)  底线命令模式 

在命令模式下按下:（英文冒号）就进入了底线命令模式。  
底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。  
在底线命令模式中，基本的命令有（已经省略了冒号）： 

- **q** 退出程序  
- **w** 保存文件  

按 ESC 键可随时退出底线命令模式。  
简单地说，我们可以将这三个模式想成底下的图标来表示：

![Vim/Vi 工作模式](http://www.runoob.com/wp-content/uploads/2014/07/vim-vi-workmodel.png)


## vi/vim 按键说明

除了上面简易范例的 i, Esc, :wq 之外，其实 vim 还有非常多的按键可以使用。

第一部分：一般模式可用的光标移动、复制粘贴、搜索替换等

第二部分：一般模式切换到编辑模式的可用的按钮说明

第三部分：一般模式切换到指令行模式的可用的按钮说明

特别注意，在 vi/vim 中，数字是很有意义的！数字通常代表重复做几次的意思！ 也有可能是代表去到第几个什么什么的意思。

举例来说，要删除 50 行，则是用 『50dd』 对吧！ 数字加在动作之前，如我要向下移动 20 行呢？那就是『20j』或者是『20↓』即可。


## 什么是 vim?

vim 键盘图  
![vim 键盘图](http://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch.gif)

