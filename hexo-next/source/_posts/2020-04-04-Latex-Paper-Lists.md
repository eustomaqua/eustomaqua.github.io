---
title: Tips of LaTeX and GitHub Badges
date: 2020-04-03 23:44:18
updated: 2020-04-03 23:44:18
categories:
  - Writing
tags: 
  - LaTeX
  - Git
  - Configure
---

<!--
Tips of Lists and Codes in Papers (列表 etc.)
Created: 2020-04-01 23:14:51
Updated:
2020-04-03 23:44:18
2020-04-12 01:36:29
-->


\# Tips of Lists and Codes in Papers (列表 etc.)  
latex 数学符号: [常用数学符号的 LaTeX 表示方法](https://www.mohu.org/info/symbols/symbols.htm)


# LaTeX: Functions

## eumerate, itemize

### enumerate 起始编号定义
[Latex,enumerate环境下起始编号定义(How can I make an enumerate list](http://blog.sina.com.cn/s/blog_a0e53bf70102vtwz.html)

```latex
\begin{enumerate}
\setcounter{enumi}{3}
\item[4.] Question?
\begin{enumerate}
    \item[1)] Item A
    \item[2)] Item B
    \item[3)] Item C
\end{enumerate}
\end{enumerate}
```

## ?

# LaTeX: Others


# GitHub repos

## using git to control versions

```bash
$ git clone [repo-address]
$ cd [repo-name]

$ git config user.name eustomaqua
$ git config user.email [your-email-address]
$ git config push.default simple
#                         simple  
## only pushes the current branch to the corresponding
## remote branch that 'git pull' uses to update the 
## current branch
#$ git config push.default matching

$ git help config
# q: quit
```

```bash
$ git branch

# to begin with
$ git checkout -b adanet
$ git push --set-upstream origin adanet

# next
$ git status
$ git add .
$ git commit -m "messages"
$ git push

# switch over
$ git checkout [branch-name]
```

## 徽章 / CI bots

### Travis CI (build passing)

\#\#\#\# Public [https://travis-ci.org/](https://travis-ci.org/)  
\#\#\#\# Private [https://travis-ci.com/](https://travis-ci.com/)  

**私有仓库**  
1. start with
  1. 进入 [Dashboard](https://travis-ci.com/dashboard)  
  2. 选择相应的仓库，点击右侧 `Trigger a build`  
    然后网页上方就会弹出提示 *Hooray! You're successfully triggered a build for eustomaqua/repo. Hold tight, it might take a moment to show up.*  
  3. 刷新网页后进入该仓库，此时它的徽章仍是 `build unknown`  
  4. 点击右方 `More options` --> `Settings`
2. 在项目根目录下创建 `.travis.yml` 文件，添加源代码
  ```yaml
env:
  global:
    - CODACY_PROJECT_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    - CODECOV_TOKEN = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  ```

**公开仓库**  
1. 暂略

**徽章:** 进入 build 页面，鼠标左键单击徽章，则可见 `Status Image`，选择 FORMAT 复制 RESULT 即可。

### Coveralls (coverage)
\#\#\#\# public repos

官网 [https://coveralls.io/](https://coveralls.io/)  
只支持公开仓库

1. 用 GitHub 账号登入，点击左侧 `ADD REPOS`
2. 选择仓库。若仓库显示不全，就点击右上角 `SYNC REPOS`

此时还是 `只支持公开仓库` 的状态；若想支持私有仓库 **[尝试失败]**，
- 在页面最下方找到 Need to Access Un-Publicized Organization Memberships，
- 点击其右的 `ENABLE PRIVATE REPO ACCESS`，则显示 *SYNCING...*
- 稍等片刻后出现授权页面 "Anthorize Coveralls Pro"，确定授权 `Anthorize Iemurheavy`
- 回到自动重定向后的页面，发现此时仍然只有公开库，找到页面最下方的 "Refresh Your Private Repos"，点击右侧 `REFRESH PRIVATE REPOS`，出现 *SYNCING...*
- 发现还是只有公开仓库
- 注：最下方的 `GITHUB SETTINGS` 点进去是授权页面，需要时可 `Revoke Access`

*COVERALLS 示意图*
1. UN-PUBLICIZED 授权之前
  <img src="/images/2020-04/0404_GitHubCI_Coveralls_1public.png" width="97%">
2. UN-PUBLICIZED 授权之后
  <img src="/images/2020-04/0404_GitHubCI_Coveralls_2private.png" width="97%">

### Codecov (codecov)
\#\#\#\# public repos  
\#\#\#\# private repos  

官网 [https://codecov.io/](https://codecov.io/)

1. 使用 GitHub (/ GitLab / Bitbucket) 账号登入
2. 右上角点击自己的头像，在新进入的页面点击右方 `Add new repository`  
3. 页面 Choose a new repository below: 在下方选择仓库  
4. 页面 Let's get your project covered  
  1. Copy Token, 把代码填入 `.travis.yml` 的 "env: global" 部分  
  ```yaml
env:
  global:
    - CODECOV_TOKEN = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  ```
  3. 将测试覆盖率报告上传给 Codecov
  ```yaml
after_success:
  - codecov --token="$CODECOV_TOKEN"
  - bash <(curl -s https://codecov.io/bash)
  ```
5. 在官网上查看报告

- Overview
- Settings
  Badge -> Markdown

第一次成功上传后找到
- Branches: 可查看对应分支的报告 
- Settings: 
  - General: 改变 `Default Branch`，输入对应分支名，然后 `Update`
  - Badge: 页面多刷新几次之后，发现徽章的 Markdown 代码改变，对应更新 readme 即可
  - 其实两个徽章的代码里面也就只有 [branch-name] 不一样，其他都一样

### Codacy (code quality, coverage)
\#\#\#\# public repos  
\#\#\#\# private repos  

官网 [https://www.codacy.com](https://www.codacy.com)  

1. Click `Add repository`  
  用 GitHub 账号 (也可使用 GitLab, Bitbucket) 进入[官网](https://app.codacy.com/projects)，添加自己的仓库。  
  注意此时能 access 到的仓库都是 Public 的。要想 access 到私有仓库，需授权

2. `Give access on GitHub`  
  点击后按页面说明进行，需要输入 GitHub 账号密码。  
  授权后可 access 到 Private 仓库。

3. 指定仓库 Click `Add`  
  找到想要 review 的仓库，点击右方 `Add`。  
  等待：*Checking permissions...*, *Reviewing...*  
  其中 Reviewing 这一步需要等一会儿，时间不定


进入 My Repositories --> Settings 
- Branches
  - `ANALYSIS` 可以设置对哪个分支进行分析
  - `Select Main Branch` 可以把默认分支从 master 移到其他分支
- General
  - Codacy Badge

回到 Dashboard ，进入 Coverage: `Set up your coverage here` 
- Copy the Repository Token ，修改 `.travis.yml` 文件
  ```yaml
env:
  global:
    - CODACY_PROJECT_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  ```
- 生成测试覆盖率的报告文件
- 上传报告
- *Notice:* 此时再回到 Settings -> General, 会发现 Codacy Badge 已经从一个 code quality 变到了两个，即增加了 coverage 

## refs

github 自动 travis  
[Github集成TravisCI：自动发布](https://github.com/levy9527/blog/issues/1)  
[手把手教你使用Travis CI自动部署你的Hexo博客到Github上](https://www.jianshu.com/p/e22c13d85659)  
[给github项目加上持续集成（travis-ci）与自动release发布软件功能](https://www.chenxublog.com/2019/01/29/github-travis-ci-auto-release.html)  
[如何使用Travis CI来做GitHub的Release自动发布](https://www.liesauer.net/blog/post/github-auto-release-with-travis-ci.html)  

github 使用 codacy  
[徽章系列7： codacy 的使用](https://www.jianshu.com/p/ed46ceca0654)  
[聊聊GITHUB上的那些小工具01——代码质量](https://zhuanlan.zhihu.com/p/30780998)  
[聊聊Code Review](https://www.cnblogs.com/shengulong/p/8866681.html)  
[徽章系列7： codacy 的使用](https://blog.csdn.net/gdky005/article/details/73330343)  

**孤独狂饮 | 简书**  
[徽章系列3： Travis CI 的使用](https://www.jianshu.com/p/226b4d8007e5)  
[徽章系列4： Circle CI 的使用](https://www.jianshu.com/p/1a0225eca32f)  
[徽章系列5： Codecov 的使用](https://www.jianshu.com/p/c0fc577407a6)  
[徽章系列7： codacy 的使用](https://www.jianshu.com/p/ed46ceca0654)  
[徽章系列8：生成个性徽章](https://www.jianshu.com/p/7e176d1fb583)  
[打造一个高逼格的android开源项目——小白全攻略](https://www.jianshu.com/p/f973eb1de56a)  
[开源徽章系列](https://www.jianshu.com/nb/13467652)  

## pytest

在 conda 虚拟环境下使用 pytest 会调用主环境的 python
```bash
$ source activate adanet
$ pip install -r requirements.txt
$ pip install pytest
$ #    python -m pytest 
$ # or pytest #tests
```

**pytest**
- pytest 设置 python 路径  
  [【Pytest】pytest的基本设置](https://blog.csdn.net/liuchunming033/article/details/46506131)  
  [<font color="green">Pytest-配置文件</font>](https://blog.csdn.net/weixin_43743725/article/details/85048235)  
  The command "coverage run --source=./ -m pytest" exited with 5.  
  [No documentation on exit code 5](https://github.com/pytest-dev/pytest/issues/2239)  
- pytest, deselected 什么情形  
  [<font color="green">pytest docs: 标记函数</font>](https://learning-pytest.readthedocs.io/zh/latest/doc/test-function/mark.html)  
  [pytest 执行测试用例的几种方法](https://www.jianshu.com/p/ec2663524d86)  
  [Pytest - 使用介绍](https://www.jianshu.com/p/a754e3d47671)  
  [pytest教程之分组测试](https://blog.csdn.net/df0128/article/details/91040953)  
  [Play Python Library之pytest--mark篇](https://cuyu.github.io/python/2016/09/21/Play-Python-Library%E4%B9%8Bpytest-mark%E7%AF%87)  
- 虚拟环境 pytest  
  [<font color="green">在conda虛擬環境下使用py.test會調用主環境的Python</font>](https://blog.csdn.net/keineahnung2345/article/details/86080914)  
  [python笔记41-虚拟环境virtualenv](https://www.cnblogs.com/yoyoketang/p/11427362.html)  


# Remote Servers

## VSCode
Visual Studio Code 安装插件  
- Remote - SSH
- \# Remote Development

### ssh 配置文件

`Remote - SSH` 可以点击左下角连接远程服务器，它的配置文件是 `C:\Users\Lenovo\.ssh\config`
```bash
C:\Users\Lenovo\.ssh
λ ls
config  id_rsa  id_rsa.pub  known_hosts

C:\Users\Lenovo\.ssh
λ vim config
# Esc + :q or :wq
```
```bash
# ControlPath ~/.ssh/%r@%h_%p
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
# Host alias
#     HostName hostname
#     User user
#
Host eustomaqua
    HostName        127.0.0.1
    Port            22
    User            eustomaqua
    IdentityFile    ~/.ssh/id_rsa  # C:\Users\Lenovo\.ssh\id_rsa
    IdentitiesOnly  yes
```

### 设置免密登录

VSCode 每次远程连接都要输入密码，很麻烦，所以还需要设置一下 ssh 的免密登录。

1. **在本地 PC 生成 SSH 的公钥和私钥**
  ```bash
  λ ssh-keygen -t rsa
  ```
  这样会在当前目录生成名为 `id_rsa` 的私钥文件和名为 `id_rsa.pub` 的公钥文件，`-t` 表示密钥类型是 rsa。  
  如果只输入 ssh-keygen 生成的 RSA 密钥长度为 2048，如果你对安全性要求比较高可以指定 4096 位的长度，这里 `-b` 就是多少位：
  ```bash
  λ ssh-keygen -b 4096 -t rsa
  ```
  当你在生成 SSHKEY 的时候在命令行下会提示你 Enter file in which to save the key，让你确认密钥文件保存的路径，一般回车即可（一般默认会在当前用户家目录下的 .ssh 目录下）。  
  第二个提示是 Enter passphrase (empty for no passphrase) 让你输入一个密钥的密码，如果不输入则留空；回车生成公私钥完毕 。（这里建议密码留空）

2. **手动上传公钥文件**  
  将本地的公钥文件上传到服务器上，然后在服务器需要免密登录的用户家目录下查看是否有 `~/.ssh/authorized_keys` 这个文件，如果没有手动创建一个:
  ```bash
  $ # cd ~/.ssh
  $ touch ~/.ssh/authorized_keys
  $ # cat authorized_keys 为空
  ```
  然后将公钥内容写入到 `authorized_keys` 文件中，因为这个文件可能已经有内容了，所以可以使用如下方式
  ```bash
  $ cat -n ~/.ssh/rsa.pub ~/.ssh/authorized_keys
  ```
  也可以使用 `vim` 打开这个文件，然后把本地公钥内容粘贴到文件末端 (另起一行，粘贴公钥)

### 内网穿透 (暂略)

使用 autossh 进行内网穿透  
设想这样的场景，你在公司或者学校有一台用于炼丹的服务器，但是只能在内网访问。我在家里使用笔记本也想连接到远程的服务器中，这时我们应该怎么办呢。  
答案是我们需要一台具有公网 ip 的服务器作为中继，使用 autossh 将公网服务器作为代理服务器。假设公网服务器为主机 A，内网炼丹炉为主机 B，我们的笔记本为 C 则

### 其它设置

[设置VsCode自动换行](https://sherlockgy.github.io/2018/09/01/%E8%AE%BE%E7%BD%AEVsCode%E8%87%AA%E5%8A%A8%E6%8D%A2%E8%A1%8C/)  

## PyCharm

## Refs

vscode 远程 一直输入密码  
[使用vscode进行远程炼丹](https://zhuanlan.zhihu.com/p/89662757)  
[vscode remote开发ssh免密登陆失败](https://blog.csdn.net/hchhbbcxl/article/details/101429447)  
[VS Code Remote SSH配置](https://zhuanlan.zhihu.com/p/68577071)  

ubuntu 查看目录权限  
[linux文件权限查看及修改-chmod ------入门的一些常识](https://blog.csdn.net/haydenwang8287/article/details/1753883)  
[ubuntu 文件及子文件夹的权限的查看及修改](https://blog.csdn.net/qq_22605739/article/details/46722161)  


# \*References
