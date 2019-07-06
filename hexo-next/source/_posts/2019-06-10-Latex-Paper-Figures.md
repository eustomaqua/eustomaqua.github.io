---
title: Tips of Tables and Figures in Papers (论文图表小技巧)
date: 2019-06-15 16:52:13
updated: 2019-07-06 22:14:21
categories:
  - Records
tags: 
  - LaTeX
---

[comment]: <> (2019-07-06 18:39:54)


# Contents

## template

英文用 pdfLatex 编译
```erlang
\documentclass{article}
\usepackage[utf8]{inputenc}
% 导言区
\begin{document}
% 正文区
\end{document}
```

中文用 XeLaTeX 编译
```erlang
\documentclass[UTF8]{article}
\usepackage[fontset=ubuntu]{ctex}
% or local: \usepackage{xeCJK}
\usepackage[left=2.17cm, right=2.17cm, top=1.7cm, bottom=1.7cm]{geometry}
\begin{document}
\end{document}
```


## Tables

### 三线表

[【LaTeX Tips】各种表格的绘制](https://liam.page/2013/08/04/LaTeX-table/)  
```erlang
% 导言区
\usepackage{booktabs}
% 正文区
\begin{table}[htbp]
\centering
\caption{Table Caption}
\label{tab:?}
\begin{tabular}{ccc}
    \toprule
    Data set & Treatment group & Control group \\
    \midrule
    Image & & \\
    Text  & & \\
    \bottomrule
\end{tabular}
\end{table}
```

### 跨行跨列 

跨列，横向合并  
在 tabular 中，可以用 \multicolumn{cols}{pos}{text} 来使得 text 占据 cols 个 cells, 并遵照 pos 中指示的位置。其中 pos 中支持竖线 | 的使用，以在合并后的 cells 两侧绘制竖线。  
注意如果横向合并 cells 之后，改行的列数会相应增加。亦即在上述例子中，第一行的 cell 占据了 3 列的空间，如果在其后添加 & 符号（表示希望将接下来的内容添加在下一列），则会提示列数过多。  
```text
\begin{table}%[htbp]
\centering
\caption{Table Caption}
\label{tab:}
\begin{tabular}{c|r|r}
    \toprule
    Data set & \multicolumn{2}{c}{Treatment and control} \\
    \midrule
    Image & 11111 & 2 \\
    Text  & 3 & 44444 \\
    \bottomrule
\end{tabular}
\end{table}
```

跨行，纵向合并  
纵向合并 cells 需要 multirow 宏包的支持。该宏包提供的 \multirow{rows}{width}{text} 命令能够实现我们的需求。其中若 width 参数中填入 *, 则占据的宽度会根据需要自动增减。  
注意该命令仅仅是将目标位置的 text 扩展到了包括目标位置所在的 rows 行。因此，在其下的若干行，必须用 & 符号空出相应的位置，不然就会导致文字重叠。例如编译下面的代码  
```text
\begin{table}%[htbp]
\centering
\caption{Table Caption}
\label{tab:}
\begin{tabular}{c|r|r}
    \toprule
    \multirow{2}{*}{Data set} & Parameter & Models \\
    & layers & network \\
    \midrule
    Image & 11111 & 2 \\
    Text  & 3 & 44444 \\
    \bottomrule
\end{tabular}
\end{table}
```

既跨行又跨列  
显见，实现这样的需求需要将上述两个命令结合起来使用。但是只能用 \multicolumn{cols}{pos}{\multirow{rows}{width}{text}} 这样的形式，而不能反过来嵌套。具体原因不明。  
```text
\begin{table}%[htbp]
\centering
\caption{Table Caption}
\label{tab:}
\begin{tabular}{c|rr}
    \toprule
    \multirow{2}{*}{Data set} & \multicolumn{2}{c}{Parameter \& Models} \\
    & layers & network \\
    \midrule
    Image & 11111 & 2 \\
    Text  & 3 & 44444 \\
    \bottomrule
\end{tabular}
\end{table}
```

### scalebox

[Scalebox - knowing how much it scales](https://tex.stackexchange.com/questions/13460/scalebox-knowing-how-much-it-scales)  
[Quickest way to include graphics](https://tex.stackexchange.com/questions/10966/quickest-way-to-include-graphics/10970#10970)  
\resizebox{<width>}{<height>}{<content>}   
\rotatebox   
\includegraphics[height=<height>, width=<width>, angle=<angle>, keepaspectratio]{<filename>}  
\adjustbox{height=<height>, width=<width>, angle=<angle>, keepaspectratio}{<TeX content>}  

[8.1 scalebox  命令](http://www.ctex.org/documents/latex/graphics/node22.html)  
\scalebox 命令对其作用的对象进行缩放，使缩放后的对象的宽度为原始 宽度与水平缩放因子之积，高度为原始高度与垂直缩放因子之积。如果垂直缩放 因子没有给出，那么将按照给定的水平缩放因子，保持原始宽高的比例进行缩放。 如果缩放因子为负值，则对对象进行反射。  
```text
% 导言区
\usepackage{graphicx}
% 正文区
\scalebox{水平缩放因子}[垂直缩放因子]{对象}
```

### footnote in tables

**一个不太好的 solution**  
[Footnote in tabular environment](https://tex.stackexchange.com/questions/109467/footnote-in-tabular-environment)  
[Footnotes for tables in LaTeX](https://stackoverflow.com/questions/2888817/footnotes-for-tables-in-latex)  
[Footnotes in tables?](https://tex.stackexchange.com/questions/1583/footnotes-in-tables)  
```text
% 导言区
\usepackage{footnote}
\makesavenoteenv{tabular}
\makesavenoteenv{table}
% 正文区
\begin{table}
\begin{tabular}{l}
    \hline
    Content\footnote{footnote text} \\
    \hline
\end{tabular}
\end{table}
\begin{tabular}{l}
Content\footnote{footnote text}
\end{tabular}
```

**表格下方显示脚注**  
[Latex给表格加脚注](https://blog.csdn.net/ShuqiaoS/article/details/86230367)  
[题 LaTeX中表格的脚注](http://landcareweb.com/questions/4442/latexzhong-biao-ge-de-jiao-zhu)  
```text
% 导言区
\usepackage{threeparttable}
% 正文区

% A table with footnotes appearing at the bottom of the page:
\begin{table}
    \centering
    \begin{tabular}{llll}
        \hline
        column 1 & column 2 & column 3\footnotemark[1] & column 4\footnotemark[2] \\
        \hline
        row 1 & data 1 & data 2 & data 3 \\
        row 2 & data 1 & data 2 & data 3 \\
        row 3 & data 1 & data 2 & data 3 \\
        \hline
    \end{tabular}
    \caption{Table with footnotes at the bottom of the page}
    \label{tab:test1}
\end{table}
\footnotetext[1]{table footnote 1}
\footnotetext[2]{table footnote 2}

\clearpage

% A table with footnotes appearing at the bottom of the table:
\begin{table}
    \centering
    \begin{threeparttable}[b]
        \caption{Table with footnotes after the table}
        \label{tab:test2}
        \begin{tabular}{llll}
            \hline
            column 1 & column 2 & column 3\tnote{1} & column 4\tnote{2} \\
            \hline
            row 1 & data 1 & data 2 & data 3 \\
            row 2 & data 1 & data 2 & data 3 \\
            row 3 & data 1 & data 2 & data 3 \\
            \hline
        \end{tabular}
        \begin{tablenotes}
            \item[1] tablefootnote 1
            \item[2] tablefootnote 2
        \end{tablenotes}
    \end{threeparttable}
\end{table}
```
<img src="/images/2018-09/2019_06_15_example_table_b.png" width="60%">

### 单元格内换行

[LaTeX之表格中强制换行](https://blog.csdn.net/dazuo01/article/details/22821935)  
[Latex 表格内文字过长自动换行](https://blog.csdn.net/virhuiai/article/details/7886265)  
[Latex 中 Table中不显示 footnote, 表格强制分行, 解决方法](https://blog.csdn.net/dannyPolyu/article/details/8667403)  
```text
% 导言区
\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}
% 正文区
\tabincell{c}{.... \\ ....}
```

### e.g., 

```text
\begin{table}[h]
\small
\caption{%\small
Illustration. 
}\label{tab:multi}
\centering
\scalebox{0.89}[0.89]{
\setlength{\tabcolsep}{1.7mm}{
\begin{tabular}{l|cccc|cccc}
    \toprule
    Data set & \multicolumn{4}{c|}{Criterion 1} & \multicolumn{4}{c}{Criterion 2} \\
    \midrule
    ~ & Model 1 & Model 2 & Model 3 & Model 4 & Model 1 & Model 2 & Model 3 & Model 4 \\
    Dataset 1 & & & & & & & & \\
    Dataset 2 & & & & & & & &  \\
    \midrule % \hline %\cline{2-9}
    ~ & Model 1 & Model 2 & Model 3 & Model 4 & Model 1 & Model 2 & Model 3 & Model 4 \\
    Dataset 1 & & & & & & & &  \\
    Dataset 2 & & & & & & & &  \\
    \bottomrule
\end{tabular}
}}
\end{table}
```
<img src="/images/2018-09/2019_06_15_example_table_a.png" width="60%">

### 分页或横置表格

```text
\usepackage{longtable}
\usepackage{rotating} %表格就会产生旋转，若是想让页面横置，需要Landscape  环境  
```

[Latex的分页表格与longtable宏包](https://my.oschina.net/u/1037903/blog/224146)  
[LaTeX技巧476：LaTeX如何将表格如何旋转（2）](http://blog.sina.com.cn/s/blog_5e16f1770100oavx.html)  
[【LaTeX Tips】各种表格的绘制](https://liam.page/2013/08/04/LaTeX-table/)  


## Figures

### Tikz Examples

```text
% 导言区
\usepackage{tikz}
% 正文区
\begin{figure}[p]
\begin{tikzpicture}
    \filldraw[black] (0,0) circle (2pt) node[anchor=west] {Intersection point};
    \draw[gray, thick] (-1,2) -- (2,-4);
    \draw[gray, thick] (-1,-1) -- (2,2);
\end{tikzpicture}
\end{figure}
```

```text
% 导言区
\usepackage{tikz}
\usetikzlibrary{positioning}
% 正文区
% Diagram
\begin{figure}
\begin{tikzpicture}[
    roundnode/.style={circle, draw=green!60, fill=green!5, very thick, minimum size=7mm},
    squarednode/.style={rectangle, draw=red!60, fill=red!5, very thick, minimum size=5mm},
]
% Nodes
\node[squarednode]  (maintopic)                          {2};
\node[roundnode]    (uppercircle)   [above=of maintopic] {1};
\node[squarednode]  (rightsquare)   [right=of maintopic] {3};
\node[roundnode]    (lowercircle)   [below=of maintopic] {4};
% Lines
\draw[->] (uppercircle.south) -- (maintopic.north);
\draw[->] (maintopic.east) -- (rightsquare.west);
\draw[->] (rightsquare.south) .. controls +(down:7mm) and +(right:7mm) .. (lowercircle.east);
\end{tikzpicture}
\end{figure}
```

### Matlab 导出更清晰的图

大小：宽度 7  
渲染：分辨率 300  
导出 eps 文件  

### GSview 裁剪 eps

File -> PS to EPS -> "Automatically calculate Bounding Box"  


# Others


## Packages


### enumitem

**类似''导入 enumerate 后设置项目符号''**  

[comment]: <> (待补充....)

```erlang
% \usepackage{enumerate}  % 与 enumitem 不兼容
\usepackage{enumitem}
\setenumerate[1]{itemsep=-1pt, partopsep=0pt, parsep=0pt, topsep=0pt}
\setitemize[1]{itemsep=0pt, partopsep=0pt, parsep=0pt, topsep=0pt}
% \setdescription{itemsep=0pt, partopsep=0pt, parsep=0pt, topsep=0pt}
\newlist{subquestion}{enumerate}{1}
% \setlist[subquestion,1]{label=(\alph*)}  % options
% \setlist[subquestion,1]{label=[\roman*]}  % options
\setlist[subquestion,1]{label=[\arabic*]}  % options
```


### enumerate

**itemize 间距大小**  
[latex调整itemize的间距大小](https://blog.csdn.net/fandroid/article/details/54644966)  
[latex调整itemize的间距大小](http://www.voidcn.com/article/p-sdcrpatl-re.html)  

```text
% 单独设置
\begin{itemize}
\setlength{\itemsep}{0pt}
\setlength{\parsep}{0pt}
\setlength{\parskip}{0pt}
\item ...
\item ...
\end{itemize}
```

```text
% 全局设置
\usepackage{enumitem}
\setenumerate[1]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=5pt}
\setitemize[1]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=5pt}
\setdescription{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=5pt}
```

**项目列表符号**  

[Lists](https://www.overleaf.com/learn/latex/Lists)  
[LaTeX: Roman numbers in enumerate list and adjust space between list items](http://blog.chapagain.com.np/latex-roman-numbers-in-enumerate-list-and-adjust-space-between-list-items/)  
[enumerate – Enumerate with redefinable labels](https://ctan.org/pkg/enumerate)  
[Using lower-case roman numerals in enumerate lists](https://tex.stackexchange.com/questions/54055/using-lower-case-roman-numerals-in-enumerate-lists)  

[Latex插入项目列表符号](https://www.cnblogs.com/shenxiaolin/p/7244423.html)  
[【latex】itemize, enumerate枚举，编号使用](https://blog.csdn.net/qqxx6661/article/details/53930286)  
[itemize,enumerate,description 用法【LaTeX 使用】](http://blog.sina.com.cn/s/blog_77f5a65c0101fmjl.html)  
[在Latex使用條列式清單itemize , enumerate , description](https://www.cnblogs.com/dearjustine/archive/2010/04/05/1704508.html)  
[在Latex使用條列式清單itemize , enumerate , description [转]](https://www.cnblogs.com/longdouhzt/archive/2012/09/28/2706995.html)  
[itemize,enumerate,description 用法【LaTeX 使用】](https://www.cnblogs.com/zhaoyang10/p/4518781.html)  

```text
\begin{itemize}
    \item[-] good morning...
    \item[-] good morning....
\end{itemize}

\begin{enumerate}[(a)]%[Step 1]
    \item good morning...
    \item good morning....
\end{enumerate}
```


### marvosym

[The MarVoSym Font Package](https://mirror-hk.koddos.net/CTAN/fonts/marvosym/doc/fonts/marvosym/marvodoc.pdf)  
[marvosym – Martin Vogel's Symbols (marvosym) font](https://ctan.org/pkg/marvosym)  
[Direc­tory fonts/marvosym](https://ctan.org/tex-archive/fonts/marvosym)  
[The MarVoSym Font Package](http://texdoc.net/texmf-dist/doc/fonts/marvosym/marvodoc.pdf)  

### listings 显示代码

[使用 listings 宏包，如何设置代码的字体 #7](https://github.com/CTeX-org/forum/issues/7)  
[在LaTeX里实现最专业的程序源代码排版](https://qiuxing.wordpress.com/2010/12/30/latex-listings/)  
[【转载】latex listings宏包使用](https://www.jianshu.com/p/aff46a14ba9b)  
[LaTeX使用listings宏包插入代码时，将代码字体设为 Monaco](https://www.jianshu.com/p/9f23ca23c04b)  
[LaTex：插入代码的listings包和lstlisting环境](https://blog.csdn.net/quantumpo/article/details/26854289)  
[listings 是专用于代码排版的 LaTeX宏包（及使用xltxtra进行中文支持）](https://blog.csdn.net/yumengkk/article/details/8080530)  
[LaTeX 使用 listings 宏包插入代码时，如何将代码的字体设定为 Monaco?](https://www.zhihu.com/question/30957600)  

```text
% 导言区
\usepackage{listings}
% 正文区

% 1) inline, 适合在正常的一段话中引用一个函数
\lstset{language=C}
the call \lstinline!socket()! creates a socket.

% 2) enviroment, 适合在 LaTeX 源文档里插入一段中等长度的代码
\lstset{language=c++}
\begin{lstlisting}[frame=tb]{somecode}
    for(i = 0; i &amp;lt; 10; i++){
        // increment the pointer
        *p++ = i;
    }
\end{lstlisting}

% 3) 直接调用外部源代码文件
\lstinputlisting[language=Python]{source_filename.py}
```

### listings example

```text
% 导言区
\usepackage{listings}

\lstset{
	columns=fixed,       
	numbers=left,                                      % 在左侧显示行号
	numberstyle=\tiny\color{gray},                     % 设定行号格式
	frame=none,                                        % 不显示背景边框
	backgroundcolor=\color[RGB]{245,245,233},          % 设定背景颜色
	keywordstyle=\color[RGB]{60,60,255},               % 设定关键字颜色
	numberstyle=\footnotesize\color{darkgray},           
	commentstyle=\it\color[RGB]{0,96,96},              % 设置代码注释的格式
	stringstyle=\rmfamily\slshape\color[RGB]{128,0,0}, % 设置字符串格式
	showstringspaces=false,                            % 不显示字符串中的空格
	language=python,                                   % 设置语言， 让LaTeX排版时将关键字突出显示
	breaklines,                                        % 让LaTeX自动将长的代码行换行排版
	extendedchars=false,                               % 解决代码跨页时，章节标题，页眉等汉字不显示的问题
}

% 正文区
\begin{lstlisting}
def func():
    # function
    pass
\end{lstlisting}
```

### indentfirst

```text
\usepackage{indentfirst}
\setlength{\parindent}{2em}
```


## Ubuntu 16.04 下编译

待补充....

### 参考 

我忘了自己当时怎么用的生成命令了，所以暂时先放一个参考  
[Bibtex使用方法简要说明（linux）](https://my.oschina.net/fenglinwansu/blog/79009)

```latex
% 1. 建立 .bib 文件，即 references.bib
% 2. 建立 .tex 文件，即 paper.tex ，并在文中引用 .bib 文件
% 3. 编译
latex paper.tex
bibtex paper.tex 
latex paper.tex
latex paper.tex
% 4. 得到生成的 .pdf 文件，即 paper.pdf
```



# Resources

## Beautiful ``Feather''

[Feather](https://feathericons.com/)

均是矢量图，风格简约；想修改成自己想要的图形也很方便

## Awesome ``TEXamples''

[Tikz examples](http://www.texample.net/tikz/examples/)  
<img src="http://www.texample.net/media/img/logo.png" alt="texamples">

图片示例详见另一篇续吧，不然太长了……感觉加载反应迟钝……

[comment]: <> "Tips of Tables and Figures in Papers (cont.) 续  https://eustomaqua.github.io/2019/2019-06-10-Latex-Paper-Figures-cont/"