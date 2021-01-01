---
title: Tips of LaTeX and Badges, Remote Server
date: 2020-04-03 23:44:18
updated: 2021-01-01 20:58:34
categories:
  - Writing
tags: 
  - LaTeX
  - Git
  - Configure
  - Remote Server
---

<!--
Tips of Lists and Codes in Papers (列表 etc.)
Created: 2020-04-01 23:14:51
Updated:
2020-04-03 23:44:18
2020-04-12 01:36:29

Tips of LaTeX and Badges, Usage of Remote Server
Tag: Remote Server / Linux
-->


\# Tips of Lists and Codes in Papers (列表 etc.)  
latex 数学符号: [常用数学符号的 LaTeX 表示方法](https://www.mohu.org/info/symbols/symbols.htm)

[MATLAB: 绘制出版级论文插图的经验](https://zhuanlan.zhihu.com/p/85068748)  
[Beamer Theme Matrix](https://hartwork.org/beamer-theme-matrix/)  

Useful:  
[Adobe Color 取色器](https://color.adobe.com/zh/create/color-wheel)  
[RGB 十六进制 常用对照表](https://tool.oschina.net/commons?type=3)  
[Color 颜色渐变主题](https://uigradients.com/#Rastafari)  
[RGB颜色值与十六进制颜色码转换工具](https://www.sioe.cn/yingyong/yanse-rgb-16/)  


# LaTeX: Functions

## 分条列举

### eumerate, itemize

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

## 分支函数

```latex
\begin{enumerate}
f(x) = 
\begin{cases}
1, & x>0\,;\\
0, & x<0\,.
\end{cases}
\end{enumerate}
```

## 算法清单

{% gp 1-2 %}
<img src="/images/2021-01/0101_algorithmic.png">
<img src="/images/2021-01/0101_algorithm2e.png">
{% endgp %}

### algorithmic

```markdown
\usepackage{algorithm}
\usepackage{algorithmic}
\renewcommand{\algorithmicrequire}{\textbf{Input:}} %输入
\renewcommand{\algorithmicensure}{\textbf{Output:}} %输出

\begin{algorithm}[H]
\caption{Caption 算法标题}
\label{alg:my_label}
\begin{algorithmic}[1]
\REQUIRE 输入参数
\ENSURE 输出参数
\STATE 执行命令
\FORALL{0 < i < n}
    \IF{a > b}
        \STATE a += 1;
        \STATE b -= 1;
    \ELSE
        \STATE a = 3;
    \ENDIF
\ENDFOR
\end{algorithmic}
\end{algorithm}
```

### algorithm2e

```markdown
\usepackage[ruled,linesnumbered]{algorithm2e}

\begin{algorithm}[H]
\caption{Caption 算法标题}
\label{alg:my_label}
\LinesNumbered
\KwIn{输入参数}
\KwOut{输出参数}
\For{i = 1 : n}{
    \eIf{a > b}{
        a += 1;\\
        b -= 1;
    }{
        j++;
    }
}
\end{algorithm}
```

# LaTeX: Packages

[beamer 的常见设置汇总](http://blog.sina.com.cn/s/blog_6aee843a0101l2vu.html)  
[LaTeX Beamer数理报告设计精通：主题制作](https://www.liangye.site/2019/10/25/latex-beamer-theme-tutorial/)  

## 论文其他, i.e., Article

公式
```markdown
% *** MATH PACKAGES ***
\usepackage{bm}
\usepackage{amsmath}
\usepackage{amssymb} %\mathbf{}
\usepackage{amsthm}
\newtheorem{thm}{Theorem}
\newtheorem{lemma}{Lemma}
\newtheorem{defin}{Definition}
\newtheorem{axiom}{Axiom}
\newtheorem{prop}{Proposition}
\newtheorem{corol}{Corollary}
\newtheorem{remark}{Remark}
\usepackage{rotating}

% \newtheorem{thm}{Theorem}
\newenvironment{thmbis}[1]
  {\renewcommand{\thethm}{\ref{#1}$'$}%
   \addtocounter{thm}{-1}%
   \begin{thm}}
  {\end{thm}}

\DeclareMathOperator*{\argmax}{argmax}
\DeclareMathOperator*{\argmin}{argmin}
\DeclareMathOperator*{\minimize}{minimize}
\DeclareMathOperator*{\maximize}{maximize}
\newcommand{\defineq}{\overset{\text{def}}{=}} % \hat{=}
```

算法
```markdown
% *** SPECIALIZED LIST PACKAGES ***
\usepackage{algorithm}
\usepackage{algorithmic}
\renewcommand{\algorithmicrequire}{\textbf{Input:}}
\renewcommand{\algorithmicensure}{\textbf{Output:}}

\usepackage{color} % /xcolor
\usepackage{enumerate}
```

列表
```markdown
% *** SPECIALIZED LIST PACKAGES ***
\usepackage{booktabs} %三线表
\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}

% *** ALIGNMENT PACKAGES ***
\usepackage{array}
\usepackage{threeparttable}
\usepackage{multirow}
```

画图
```markdown
% *** GRAPHICS RELATED PACKAGES ***
\ifCLASSINFOpdf
  \usepackage[pdftex]{graphicx}
\else
  \usepackage[dvips]{graphicx}
\fi

% *** SUBFIGURE PACKAGES ***
\ifCLASSOPTIONcompsoc
  \usepackage[caption=false,font=normalsize,labelfont=sf,textfont=sf]{subfig}
\else
  \usepackage[caption=false,font=footnotesize]{subfig}
\fi
\graphicspath{{imgs/}{newfigs/}}

\usepackage{tikz}
```

引用
```markdown
% *** CITATION PACKAGES ***
\usepackage{cite}

% *** FLOAT PACKAGES ***
% *** PDF, URL AND HYPERLINK PACKAGES ***
\usepackage{url}

\newcommand{\citet}[1]{\citeauthor{#1} \shortcite{#1}}
\newcommand{\citep}{\cite} 
\newcommand{\citealp}[1]{\citeauthor{#1} \citeyear{#1}}

\def\etal{\emph{et al.}}
\def\ie{i.e.,}
\def\eg{e.g.,}
```

特殊
```markdown
\def\sign{\mathop{\rm{sign}}}
\newcommand{\entitle}{Title of This Paper}
\newcommand{\full}{????}
\newcommand{\abbr}{\emph{????}}
```

## 报告设置, i.e., Beamer

```markdown
% 主题颜色
% \usetheme{default}% Madrid}
% \usecolortheme{dove}

\usepackage{xeCJK} %支持中文，须用 XeLaTeX 编译
% \usefonttheme[onlymath]{serif} %数学公式字体
\usefonttheme{professionalfonts} %%公式里的字体

% 相关编号
% \setbeamertemplate{theorems}[numbered] %定理编号
\setbeamertemplate{caption}[numbered] %图表编号

\usepackage[numbers,sort&compress]{natbib} %参考文献
\usepackage{hyperref} %让文档支持超链接
```

```markdown
% 行文颜色
\usepackage{xcolor}
\textcolor{red}{Hello}
% 系统定义好的颜色
% red/blue/green/black/white/cyan/magenta/yellow

% 定义颜色
\definecolor{aggiemaroon}{cmyk}{1.0,0.8,0,0}
\definecolor{blendothers}{rgb}{0.7,0.2,0.2} %[0-1]
\definecolor{blendremind}{RGB}{0,97,255} %[0,255]
```

改变列表编号计数器
```markdown
\begin{enumerate}
    \addtocounter{enumi}{3}  % 改变列表标号计数器
  \item[在这里输入你的符号] test
\end{enumerate}
```

## Beamer 本地编译

```markdown
%\usepackage[UTF8]{ctex}    %中文
\usepackage{xeCJK}    %中文

\setCJKmainfont{楷体}   %字体
\setmainfont{Times New Roman}

\usepackage{xcolor}   %颜色
\usepackage{hyperref}   %书签
%\usepackage[colorlinks]{hyperref}      %书签目录
\usepackage[numbers, sort&compress]{natbib} %参考文献
```

```markdown
%\usepackage{indentfirst} %添加首行缩进，两个字符
%\setlength{\parindent}{2em}
\def\indent{\hspace{2em}}

\usepackage{multimedia} %让文档支持多媒体
%\usepackage{graphics}  %让文档支持图片
\usepackage{subfig}
\usepackage{hyperref} %让文档支持超链接
\hypersetup{CJKbookmarks=true}
```

```markdown
\setbeamertemplate{navigation symbols}{} % 取消导航条
%\setbeamertemplate{footline}[frame number]{}   %右下角显示页码
%\setbeamertemplate{footline}{\insertframenumber/\inserttotalframenumber} %左下角

% \logo{\includegraphics[height=0.25\textwidth]{../ustc_logo_fig_new.eps}}
% \titlegraphic{\includegraphics[scale=0.5]{simtlogo.png}} %仅标题页

\definecolor{beamer@blendedblue}{rgb}{0.2,0.2,0.7} % use structure theme to change
\definecolor{mycolor}{rgb}{0.75,0.75,1.0}
\definecolor{mytitle}{rgb}{0.6,0.6,0.9}
%定制区块环境
\setbeamertemplate{blocks}[rounded][shadow=true]
\setbeamercolor{block title}{fg=white,bg=blue!40}%beamer@blendedblue}
\setbeamercolor{block body}{bg=blue!5}%mycolor}
```

## 改变字体 (固定了主题结构)

```markdown
%\usetheme{default}
\usetheme{Madrid}
\definecolor{aggiemaroon}{cmyk}{1.0,0.8,0,0}
\usecolortheme[named=aggiemaroon]{structure}
\useoutertheme{shadow}
\useinnertheme{rounded}
\setbeamertemplate{navigation symbols}{} %取消导航条
\setbeamerfont{structure}{family=\rmfamily,series=\bfseries}
\usefonttheme{serif}
```

## 定理环境 (影响标题背景色)

设定结构的前景色
```markdown
% uiGradients: Blu
\definecolor{myblues}{RGB}{0,65,106}
\definecolor{mywhite}{RGB}{228,229,230}
\setbeamercolor{structure}{fg=myblues}
\setbeamercolor{structure}{bg=mywhite}
```
使用继承方式来批量改变block标题颜色和block主干颜色，利用“<颜色>!<数字>!<颜色>”来进行混合
```markdown
\setbeamercolor{block title}{use=structure,fg=structure.fg,bg=structure.fg!20!bg}
\setbeamercolor{block title alerted}{use=alerted text,fg=alerted text.fg,bg=alerted text.fg!20!bg}
\setbeamercolor{block title example}{use=example text,fg=example text.fg,bg=example text.fg!20!bg}
\setbeamercolor{block body}{parent=normal text,use=block title,bg=block title.bg!50!bg}
\setbeamercolor{block body alerted}{parent=normal text,use=block title alerted,bg=block title alerted.bg!50!bg}
\setbeamercolor{block body example}{parent=normal text,use=block title example,bg=block title example.bg!50!bg}
\setbeamercolor{titlelike}{parent=structure,bg=white!90!red}
```


# LaTeX: Others

## ?

## Refs

[Beamer Theme Gallery](https://deic-web.uab.cat/~iblanes/beamer_gallery/index.html)  
[在 Beamer 中添加计时器和 Logo](https://amito.me/2019/Adding-Timer-and-Logo-in-Beamer/)  
[Time clock with XeLaTeX](https://tex.stackexchange.com/questions/219415/time-clock-at-the-footline-of-a-beamer-slide-is-not-adjusted-in-the-middle-if-co/407730#407730)  
[LaTeX笔记|基本功能（七）](https://zhuanlan.zhihu.com/p/24841513)  
[beamer模板设计（七）titlepage、logo和目录页](https://zhuanlan.zhihu.com/p/137427360)  

latex algorithm2e, state  
[Latex之使用algorithm2e包来写算法](https://blog.csdn.net/yq_forever/article/details/89815562)  
[latex 算法，算法包 algorithm， algorithm2e](https://blog.csdn.net/robert_chen1988/article/details/71512914?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1)  
[algorithm2e document](https://download.nus.edu.sg/mirror/ctan/macros/latex/contrib/algorithm2e/doc/algorithm2e.pdf)  

beamer 数学公式字体  
[在 Beamer 中如何使用标准数学字体](http://sealhuang.github.io/beamer-math-font)  
[Beamer中数学符号字体](https://blog.csdn.net/cclethe/article/details/78866721)  
[Latex中Beamer修改公式字体以及文本半透明显示技巧](https://blog.csdn.net/weixin_30613433/article/details/97109011)  

beamer 定理环境  
[beamer模板设计（九）beamer中的列表和环境](https://zhuanlan.zhihu.com/p/138021900)  
beamer 字体颜色  
[Latex中如何设置字体颜色（三种方式）](https://www.cnblogs.com/tsingke/p/7457236.html)  
latex beamer 设置字体族  
[LaTeX制作幻灯片](https://www.jianshu.com/p/e1746a64aa04)  



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

```bash
# 查看配置信息:  system级别, global 用户级别, 和local 当前仓库
# 设置先从 system->global->local  底层配置会覆盖顶层配置
$ git config --local --list
$ git config --global --list
$ git config --system --list
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
1. 打开主页 [https://travis-ci.org/](https://travis-ci.org/)
2. 点击 页面左上方 `My Repositories` 的右侧的 `+` 加号，
  然后可以看到许多仓库，都是公开的
3. 选择相关仓库，如果找不到就先 ``Sync account``，还不行就在 `Legacy Services Integration` 中直接搜
4. 打开该仓库的右侧开关，然后点击仓库名进入，此时仍显示 `build unknown` 
5. 点击 Badge 本身就可获得它对应的代码；若想换成别的分支，把 master 改成相关的分支名就行。
1. 其他类似。暂略

**徽章:** 进入 build 页面，鼠标左键单击徽章，则可见 `Status Image`，选择 FORMAT 复制 RESULT 即可。

### Coveralls (coverage)
\#\#\#\# public repos

官网 [https://coveralls.io/](https://coveralls.io/)  
只支持公开仓库

1. 用 GitHub 账号登入，点击左侧 `ADD REPOS`
2. 选择仓库。若仓库显示不全，就点击右上角 `SYNC REPOS`

3. `OFF --> ON` ，然后点击 repo 名进入该仓库 
4. Click 左侧的 `Setting`
5. `.coveralls.yml`
```yaml
repo_token: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

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
  *Notice:* 如果想找的仓库不显示，就点击 `Add repository` 页面最下方的 `Sync team list` ，
  即 "头像 -> Account -> Repositories -> Sync team repository list"
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

***出现问题:***  
若配置了公钥之后本机 ssh 仍然提示需要输入密码的话，可以考虑给服务器上 ~/.ssh 目录加权限来解决
```bash
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys
```
参考 [解决SSH免密登录配置成功后不生效问题](https://blog.csdn.net/lisongjia123/article/details/78513244)

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


## 出现问题
有时候明明已经设置了 `authorized_keys` 文件，并加入了自己的公钥，但是仍然会一直提示输入密码信息。因为自己是非 root 用户，无法在服务器上改 ssh\_config 文件或是重启 ssh 服务，所以没有尝试下面这些所提出的解决方法。

*References:*  
ssh authorized_keys 不生效  
[SSH authorized_keys 无效问题](https://blog.csdn.net/xexiyong/article/details/77742994)  
[解决SSH免密登录配置成功后不生效问题](https://blog.csdn.net/lisongjia123/article/details/78513244)  
ssh_config 文件  
[使用 SSH config 文件](https://daemon369.github.io/ssh/2015/03/21/using-ssh-config-file)  
[ssh配置文件ssh_config和sshd_config区别](https://www.cnblogs.com/xiaochina/p/5802008.html)  

# \*References
