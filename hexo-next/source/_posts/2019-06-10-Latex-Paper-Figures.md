---
title: Tips of Tables and Figures in Papers (论文图表小技巧)
date: 2019-06-10 21:49:03
updated: 2019-07-06 13:16:49
categories:
  - Records
tags: 
  - LaTeX
---


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

**导入 enumerate 后设置项目符号**  

待补充....

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


# Resources

## Beautiful ``Feather''

[Feather](https://feathericons.com/)

均是矢量图，风格简约；想修改成自己想要的图形也很方便

## Awesome ``TEXamples''

[Tikz examples](http://www.texample.net/tikz/examples/)  
<img src="http://www.texample.net/media/img/logo.png" alt="texamples">


### Features

#### Absolute positioning (4 items)

[Exam sheet](http://www.texample.net/tikz/examples/exam-sheet/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/exam-sheet.png" width="150">

[Fancy chapter headings](http://www.texample.net/tikz/examples/fancy-chapter-headings/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/fancy-chapter-headings.png" width="150">

[Modifying the current page node](http://www.texample.net/tikz/examples/modifying-current-page-node/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/modifying-current-page-node.png" width="150">

[Transparent PNG overlay](http://www.texample.net/tikz/examples/transparent-png-overlay/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/transparent-png-overlay.png" width="150">

#### Angles (1 item)

[Drawing angles using the PG 3.0 angles and quotes libraries](http://www.texample.net/tikz/examples/angles-quotes/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/angles-quotes.png" width="150">

#### Arcs (4 items)

[Circular arrows with text](http://www.texample.net/tikz/examples/circular-arrows-text/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/circular-arrows-text.png" width="150">

[PDCA cycle](http://www.texample.net/tikz/examples/pdca-cycle/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/pdca-cycle.png" width="150">

[Poincare Diagram, Classification of Phase Portraits](http://www.texample.net/tikz/examples/poincare/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/poincare.png" width="150">

[Steradian cone in sphere](http://www.texample.net/tikz/examples/steradian-cone-sphere/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/steradian-cone-sphere.png" width="150">

#### Arrows (18 items)

[3D cone](http://www.texample.net/tikz/examples/3d-cone/)
<img src="http://www.texample.net/media/tikz/examples/PNG/3d-cone.png" width="150">

[Actor Transaction Diagram](http://www.texample.net/tikz/examples/actor-transaction-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/actor-transaction-diagram.png" width="150">

[An example of tikz and listings jointly used](http://www.texample.net/tikz/examples/tikz-listings/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tikz-listings.png" width="150">

[Beamer arrows](http://www.texample.net/tikz/examples/beamer-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/beamer-arrows.png" width="150">

[Borrowers and lenders](http://www.texample.net/tikz/examples/borrowers-and-lenders/)
<img src="http://www.texample.net/media/tikz/examples/PNG/borrowers-and-lenders.png" width="150">

[Chains with labeled edges](http://www.texample.net/tikz/examples/labeled-chain/)
<img src="http://www.texample.net/media/tikz/examples/PNG/labeled-chain.png" width="150">

[Circular arrows with text](http://www.texample.net/tikz/examples/circular-arrows-text/)
<img src="http://www.texample.net/media/tikz/examples/PNG/circular-arrows-text.png" width="150">

[Double Arrows a la Chef](http://www.texample.net/tikz/examples/double-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/double-arrows.png" width="150">

[Drawing a graph](http://www.texample.net/tikz/examples/graph/)
<img src="http://www.texample.net/media/tikz/examples/PNG/graph.png" width="200">

[Energy level diagram](http://www.texample.net/tikz/examples/energy-level-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/energy-level-diagram.png" width="150">

[Fancy arrows drawn with the PGF 3.0 arrows.meta library](http://www.texample.net/tikz/examples/fancy-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fancy-arrows.png" width="150">

[Intersection of](http://www.texample.net/tikz/examples/intersection-of/)
<img src="http://www.texample.net/media/tikz/examples/PNG/intersection-of.png" width="150">

[Marketing distribution channel](http://www.texample.net/tikz/examples/marketing-distribution-channel/)
<img src="http://www.texample.net/media/tikz/examples/PNG/marketing-distribution-channel.png" width="150">

[Overlapping arrows](http://www.texample.net/tikz/examples/overlapping-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/overlapping-arrows.png" width="150">

[Putting a diagrams in chains](http://www.texample.net/tikz/examples/diagram-chains/)
<img src="http://www.texample.net/media/tikz/examples/PNG/diagram-chains.png" width="150">

[Refraction - Snell’s Law](http://www.texample.net/tikz/examples/refraction/)
<img src="http://www.texample.net/media/tikz/examples/PNG/refraction.png" width="150">

[Snake Lemma](http://www.texample.net/tikz/examples/snake-lemma/)
<img src="http://www.texample.net/media/tikz/examples/PNG/snake-lemma.png" width="150">

[Table in the shape of an arrow](http://www.texample.net/tikz/examples/arrow-table/)
<img src="http://www.texample.net/media/tikz/examples/PNG/arrow-table.png" width="150">

#### Automata and Petri nets (5 items)

[A Petri-net for Hagen](http://www.texample.net/tikz/examples/nodetutorial/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/nodetutorial.png" width="150">

[Automata](http://www.texample.net/tikz/examples/automata/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/automata.png" width="300">

[EPC flow charts](http://www.texample.net/tikz/examples/epc-flow-charts/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/epc-flow-charts.png" width="150">

[Mobile ad-hoc network](http://www.texample.net/tikz/examples/manet/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/manet.png" width="250">

[State machine](http://www.texample.net/tikz/examples/state-machine/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/state-machine.png" width="150">

#### Background (12 items)

[A Petri-net for Hagen](http://www.texample.net/tikz/examples/nodetutorial/)
<img src="http://www.texample.net/media/tikz/examples/PNG/nodetutorial.png" width="150">

[Actor Transaction Diagram](http://www.texample.net/tikz/examples/actor-transaction-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/actor-transaction-diagram.png" width="150">

[Bode plot](http://www.texample.net/tikz/examples/bode-plot/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bode-plot.png" width="150">

[Fibonacci spiral](http://www.texample.net/tikz/examples/fibonacci-spiral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fibonacci-spiral.png" width="150">

[Network Topology](http://www.texample.net/tikz/examples/network-topology/)
<img src="http://www.texample.net/media/tikz/examples/PNG/network-topology.png" width="150">

[Nice shaded/framed paragraphs using tikz and framed](http://www.texample.net/tikz/examples/framed-tikz/)
<img src="http://www.texample.net/media/tikz/examples/PNG/framed-tikz.png" width="150">

[Random city](http://www.texample.net/tikz/examples/city/)
<img src="http://www.texample.net/media/tikz/examples/PNG/city.png" width="150">

[Rectangle node with diagonal fill](http://www.texample.net/tikz/examples/rectangle-node-with-diagonal-fill/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rectangle-node-with-diagonal-fill.png" width="150">

[Rules](http://www.texample.net/tikz/examples/rules/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rules.png" width="150">

[Schema of Labs on a class](http://www.texample.net/tikz/examples/labs-schema/)
<img src="http://www.texample.net/media/tikz/examples/PNG/labs-schema.png" width="150">

[System Combination](http://www.texample.net/tikz/examples/system-combination/)
<img src="http://www.texample.net/media/tikz/examples/PNG/system-combination.png" width="150">

[Timing diagram with the tikz-timing package](http://www.texample.net/tikz/examples/tikz-timing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tikz-timing.png" width="150">

#### Blending (2 items)

[A Venn diagram with PDF blending](http://www.texample.net/tikz/examples/venn/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/venn.png" width="150">

[Venn diagramm with PGF 3.0 blend mode](http://www.texample.net/tikz/examples/venn-diagram-blended/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/venn-diagram-blended.png" width="150">

#### Calendar library (5 items)

[A calendar for doublesided DIN-A4](http://www.texample.net/tikz/examples/a-calender-for-doublesided-din-a4/)
<img src="http://www.texample.net/media/tikz/examples/PNG/a-calender-for-doublesided-din-a4.png" width="150">

[A calendar of circles](http://www.texample.net/tikz/examples/calendar-circles/)
<img src="http://www.texample.net/media/tikz/examples/PNG/calendar-circles.png" width="150">

[Birthday calendar](http://www.texample.net/tikz/examples/birthday-calendar/)
<img src="http://www.texample.net/media/tikz/examples/PNG/birthday-calendar.png" width="150">

[Changing the default calendar layout](http://www.texample.net/tikz/examples/changing-the-default-calendar-layout/)
<img src="http://www.texample.net/media/tikz/examples/PNG/changing-the-default-calendar-layout.png" width="150">

[Foldable dodecahedron with Calendar](http://www.texample.net/tikz/examples/foldable-dodecahedron-with-calendar/)
<img src="http://www.texample.net/media/tikz/examples/PNG/foldable-dodecahedron-with-calendar.png" width="150">

#### Callouts (1 item)

[Energy level diagrams - illustrating Hund’s rule](http://www.texample.net/tikz/examples/energy-levels/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/energy-levels.png" width="150">

#### Chains (12 items)

[AC drive components](http://www.texample.net/tikz/examples/ac-drive-components/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/ac-drive-components.png" width="150">

[Assignment structure](http://www.texample.net/tikz/examples/assignment-structure/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/assignment-structure.png" width="150">

[BER measurement on fibre optical system](http://www.texample.net/tikz/examples/BER-measurement/)
<img src="http://www.texample.net/media/tikz/examples/PNG/BER-measurement.png" width="150">

[Chains with labeled edges](http://www.texample.net/tikz/examples/labeled-chain/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/labeled-chain.png" width="150">

[Digital Signal Processing Library](http://www.texample.net/tikz/examples/fir-filter/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/fir-filter.png" width="150">

[Overlapping arrows](http://www.texample.net/tikz/examples/overlapping-arrows/) 
<img src="http://www.texample.net/media/tikz/examples/PNG/overlapping-arrows.png" width="150">

[Purdue Enterprise Reference Architecture Model](http://www.texample.net/tikz/examples/pera-model/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pera-model.png" width="150">

[Putting a diagrams in chains](http://www.texample.net/tikz/examples/diagram-chains/)
<img src="http://www.texample.net/media/tikz/examples/PNG/diagram-chains.png" width="150">

[Python if-then-else syntax diagram](http://www.texample.net/tikz/examples/python-if-then-else-syntax-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/python-if-then-else-syntax-diagram.png" width="150">

[TikZ and PGF version 2.00](http://www.texample.net/tikz/examples/pgf-version-2/)
<img src="http://texample.net/media/tikz/examples/extra/pgf-version-2/mpgf2001.png" width="150">

[Turing Machine](http://www.texample.net/tikz/examples/turing-machine-2/)
<img src="http://www.texample.net/media/tikz/examples/PNG/turing-machine-2.png" width="150">

[Turing machine](http://www.texample.net/tikz/examples/turing-machine/)
<img src="http://www.texample.net/media/tikz/examples/PNG/turing-machine.png" width="150">

#### Circuits (3 items)

[18W MOSFET amplifier with npn transistor](http://www.texample.net/tikz/examples/mosfet/)
<img src="http://www.texample.net/media/tikz/examples/PNG/mosfet.png" width="150">

[Block Diagram for TTL IC Multiplexer 74HC153](http://www.texample.net/tikz/examples/multiplexer/)
<img src="http://www.texample.net/media/tikz/examples/PNG/multiplexer.png" width="150">

[Circuit example](http://www.texample.net/tikz/examples/circuit/)
<img src="http://www.texample.net/media/tikz/examples/PNG/circuit.png" width="150">

#### Clipping (18 items)

[Animated illustration of the convolution of two functions](http://www.texample.net/tikz/examples/convolution-of-two-functions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/convolution-of-two-functions.png" width="150">

[Borromean rings](http://www.texample.net/tikz/examples/borromean-rings/)
<img src="http://www.texample.net/media/tikz/examples/PNG/borromean-rings.png" width="150">

[Energy levels of a fluor molecule](http://www.texample.net/tikz/examples/fluor-energy-levels/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fluor-energy-levels.png" width="150">

[Focused ion beam system](http://www.texample.net/tikz/examples/focused-ion-beam-system/)
<img src="http://www.texample.net/media/tikz/examples/PNG/focused-ion-beam-system.png" width="150">

[Hidden and exposed terminal problems in Wi-Fi](http://www.texample.net/tikz/examples/terminals/)
<img src="http://www.texample.net/media/tikz/examples/PNG/terminals.png" width="150">

[Intersecting rings](http://www.texample.net/tikz/examples/intersecting-rings/)
<img src="http://www.texample.net/media/tikz/examples/PNG/intersecting-rings.png" width="150">

[Projectile](http://www.texample.net/tikz/examples/projectile/)
<img src="http://www.texample.net/media/tikz/examples/PNG/projectile.png" width="150">

[Puzzle](http://www.texample.net/tikz/examples/puzzle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/puzzle.png" width="150">

[RGB color mixing](http://www.texample.net/tikz/examples/rgb-color-mixing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rgb-color-mixing.png" width="150">

[Rusting Iron](http://www.texample.net/tikz/examples/rusting-iron/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rusting-iron.png" width="150">

[Safe fusion](http://www.texample.net/tikz/examples/safe-fusion/)
<img src="http://www.texample.net/media/tikz/examples/PNG/safe-fusion.png" width="200">

[Set operations illustrated with Venn diagrams](http://www.texample.net/tikz/examples/set-operations-illustrated-with-venn-diagrams/)
<img src="http://www.texample.net/media/tikz/examples/PNG/set-operations-illustrated-with-venn-diagrams.png" width="150">

[Smooth maps](http://www.texample.net/tikz/examples/smooth-maps/)
<img src="http://www.texample.net/media/tikz/examples/PNG/smooth-maps.png" width="150">

[Sunset](http://www.texample.net/tikz/examples/sunset/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sunset.png" width="150">

[Temperature and rain sparklines](http://www.texample.net/tikz/examples/temperature-and-rain-sparklines/)
<img src="http://www.texample.net/media/tikz/examples/PNG/temperature-and-rain-sparklines.png" width="300">

[The Olympic rings](http://www.texample.net/tikz/examples/the-olympic-rings/)
<img src="http://www.texample.net/media/tikz/examples/PNG/the-olympic-rings.png" width="150">

[Venn diagram](http://www.texample.net/tikz/examples/venn-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/venn-diagram.png" width="150">

[Yin and yang](http://www.texample.net/tikz/examples/yin-and-yang/)
<img src="http://www.texample.net/media/tikz/examples/PNG/yin-and-yang.png" width="150">

#### Coordinate calculations (30 items)

[Actor Transaction Diagram](http://www.texample.net/tikz/examples/actor-transaction-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/actor-transaction-diagram.png" width="150">

[Assignment structure](http://www.texample.net/tikz/examples/assignment-structure/)
<img src="http://www.texample.net/media/tikz/examples/PNG/assignment-structure.png" width="150">

[Asymmetric information](http://www.texample.net/tikz/examples/asymmetric-information/)
<img src="http://www.texample.net/media/tikz/examples/PNG/asymmetric-information.png" width="150">

[Credit rationing](http://www.texample.net/tikz/examples/credit-rationing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/credit-rationing.png" width="150">

[Escher Brick and Penrose Triangle](http://www.texample.net/tikz/examples/escher-brick-penrose-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/escher-brick-penrose-triangle.png" width="150">

[Falling dominoes](http://www.texample.net/tikz/examples/dominoes/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dominoes.png" width="150">

[Hierarchical diagram](http://www.texample.net/tikz/examples/hierarchical-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/hierarchical-diagram.png" width="250">

[Homotopy of paths](http://www.texample.net/tikz/examples/homotopy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/homotopy.png" width="150">

[IS-LM diagram](http://www.texample.net/tikz/examples/is-lm-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/is-lm-diagram.png" width="250">

[J-Curve](http://www.texample.net/tikz/examples/j-curve/)
<img src="http://www.texample.net/media/tikz/examples/PNG/j-curve.png" width="150">

[LR constraints - Drawing and filling with arcs and Bezier curves](http://www.texample.net/tikz/examples/draw-fill-bezier-curves/)
<img src="http://www.texample.net/media/tikz/examples/PNG/draw-fill-bezier-curves.png" width="150">

[Lambert-Beer law parameters drawing](http://www.texample.net/tikz/examples/lambert-beer-law/)
<img src="http://www.texample.net/media/tikz/examples/PNG/lambert-beer-law.png" width="150">

[Lune of Hippocrates](http://www.texample.net/tikz/examples/lune-of-hippocrates/)
<img src="http://www.texample.net/media/tikz/examples/PNG/lune-of-hippocrates.png" width="150">

[Metapost style ncbar connection](http://www.texample.net/tikz/examples/myncbar/)
<img src="http://media.texample.net/tikz/examples/extra/myncbar/mnodeconnections1.png" width="150">

[Morley’s triangle](http://www.texample.net/tikz/examples/morleys-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/morleys-triangle.png" width="150">

[Nine points circle of a triangle](http://www.texample.net/tikz/examples/nine-points-circle-of-a-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/nine-points-circle-of-a-triangle.png" width="150">

[Periodic Table of Chemical Elements](http://www.texample.net/tikz/examples/periodic-table-of-chemical-elements/)
<img src="http://www.texample.net/media/tikz/examples/PNG/periodic-table-of-chemical-elements.png" width="150">

[Perpendicular bisectors of a triangle](http://www.texample.net/tikz/examples/bisector/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bisector.png" width="150">

[Polarization state of light](http://www.texample.net/tikz/examples/polarization-state-of-light/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polarization-state-of-light.png" width="150">

[Puzzle](http://www.texample.net/tikz/examples/puzzle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/puzzle.png" width="150">

[Pythagorean triangle with the squares of its sides and labels](http://www.texample.net/tikz/examples/pythagoras-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pythagoras-triangle.png" width="150">

[Rainbows - Sun ray entering a rain drop](http://www.texample.net/tikz/examples/raindrop/)
<img src="http://www.texample.net/media/tikz/examples/PNG/raindrop.png" width="150">

[Random city](http://www.texample.net/tikz/examples/city/)
<img src="http://www.texample.net/media/tikz/examples/PNG/city.png" width="150">

[Replicating triangles](http://www.texample.net/tikz/examples/triangles/)
<img src="http://www.texample.net/media/tikz/examples/PNG/triangles.png" width="150">

[Rooty helix](http://www.texample.net/tikz/examples/rooty-helix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rooty-helix.png" width="150">

[Shake and Rattle on a planar pendulum example](http://www.texample.net/tikz/examples/shake-rattle-pendulum/)
<img src="http://www.texample.net/media/tikz/examples/PNG/shake-rattle-pendulum.png" width="150">

[Sine and Cosine functions animation](http://www.texample.net/tikz/examples/sine-and-cosine-functions-animation/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sine-and-cosine-functions-animation.png" width="150">

[Sunflower pattern (Phyllotaxy)](http://www.texample.net/tikz/examples/phyllotaxy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/phyllotaxy.png" width="150">

[TCP state machine](http://www.texample.net/tikz/examples/tcp-state-machine/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tcp-state-machine.png" width="150">

[TikZ and PGF version 2.00](http://www.texample.net/tikz/examples/pgf-version-2/)
<img src="http://texample.net/media/tikz/examples/extra/pgf-version-2/mpgf2001.png" width="150">


#### Coordinate systems (8 items)

[Credit rationing](http://www.texample.net/tikz/examples/credit-rationing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/credit-rationing.png" width="250">

[Gajski-Kuhn Y-chart](http://www.texample.net/tikz/examples/gajski-kuhn-y-chart/)
<img src="http://www.texample.net/media/tikz/examples/PNG/gajski-kuhn-y-chart.png" width="150">

[Intersecting lines](http://www.texample.net/tikz/examples/intersecting-lines/)
<img src="http://www.texample.net/media/tikz/examples/PNG/intersecting-lines.png" width="150">

[Intersection of](http://www.texample.net/tikz/examples/intersection-of/)
<img src="http://www.texample.net/media/tikz/examples/PNG/intersection-of.png" width="150">

[Phasor diagram](http://www.texample.net/tikz/examples/phasor-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/phasor-diagram.png" width="150">

[Polar coordinates template](http://www.texample.net/tikz/examples/polar-coordinates-template/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polar-coordinates-template.png" width="150">

[Sine and Cosine functions animation](http://www.texample.net/tikz/examples/sine-and-cosine-functions-animation/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sine-and-cosine-functions-animation.png" width="150">

[Smooth maps](http://www.texample.net/tikz/examples/smooth-maps/)
<img src="http://www.texample.net/media/tikz/examples/PNG/smooth-maps.png" width="150">


#### Decorations (45 items)

[Box and whisker plot](http://www.texample.net/tikz/examples/box-and-whisker-plot/)
<img src="http://www.texample.net/media/tikz/examples/PNG/box-and-whisker-plot.png" width="150">

[Christmas fractal tree](http://www.texample.net/tikz/examples/christmas-tree-2/)
<img src="http://www.texample.net/media/tikz/examples/PNG/christmas-tree-2.png" width="150">

[Christmas tree with balls, candles and snowflakes](http://www.texample.net/tikz/examples/christmas-tree-3/)
<img src="http://www.texample.net/media/tikz/examples/PNG/christmas-tree-3.png" width="150">

[Circular arrows with text](http://www.texample.net/tikz/examples/circular-arrows-text/)
<img src="http://www.texample.net/media/tikz/examples/PNG/circular-arrows-text.png" width="150">

[Difference quotient](http://www.texample.net/tikz/examples/difference-quotient/)
<img src="http://www.texample.net/media/tikz/examples/PNG/difference-quotient.png" width="150">

[Direct torque control of AC drive](http://www.texample.net/tikz/examples/ac-drive-dtc/)
<img src="http://www.texample.net/media/tikz/examples/PNG/ac-drive-dtc.png" width="150">

[Double Arrows a la Chef](http://www.texample.net/tikz/examples/double-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/double-arrows.png" width="150">

[Drawing trees with the PG 3.0 pic feature](http://www.texample.net/tikz/examples/tree-pic/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tree-pic.png" width="150">

[Electric circuit decorations](http://www.texample.net/tikz/examples/circuit-decorations/)
<img src="http://www.texample.net/media/tikz/examples/PNG/circuit-decorations.png" width="150">

[Envelope](http://www.texample.net/tikz/examples/envelope/)
<img src="http://www.texample.net/media/tikz/examples/PNG/envelope.png" width="150">

[Excised, Horizon-Penetrating Coordinates for Black Hole Spacetime](http://www.texample.net/tikz/examples/spacetime/)
<img src="http://www.texample.net/media/tikz/examples/PNG/spacetime.png" width="150">

[Fancy arrows drawn with the PGF 3.0 arrows.meta library](http://www.texample.net/tikz/examples/fancy-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fancy-arrows.png" width="150">

[Feynman diagram](http://www.texample.net/tikz/examples/feynman-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/feynman-diagram.png" width="150">

[Focused ion beam system](http://www.texample.net/tikz/examples/focused-ion-beam-system/)
<img src="http://www.texample.net/media/tikz/examples/PNG/focused-ion-beam-system.png" width="150">

[Gamma interaction](http://www.texample.net/tikz/examples/gamma-interaction/)
<img src="http://www.texample.net/media/tikz/examples/PNG/gamma-interaction.png" width="150">

[Growing wave decoration](http://www.texample.net/tikz/examples/growing-wave-decoration/)
<img src="http://www.texample.net/media/tikz/examples/PNG/growing-wave-decoration.png" width="150">

[Hidden and exposed terminal problems in Wi-Fi](http://www.texample.net/tikz/examples/terminals/)
<img src="http://www.texample.net/media/tikz/examples/PNG/terminals.png" width="150">

[Homotopy of paths](http://www.texample.net/tikz/examples/homotopy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/homotopy.png" width="150">

[Kalman Filter System Model](http://www.texample.net/tikz/examples/kalman-filter/)
<img src="http://www.texample.net/media/tikz/examples/PNG/kalman-filter.png" width="150">

[Lipid vesicle](http://www.texample.net/tikz/examples/lipid-vesicle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/lipid-vesicle.png" width="150">

[Mechanism of Scanning electron microscopy](http://www.texample.net/tikz/examples/scanning-electron-microscopy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/scanning-electron-microscopy.png" width="150">

[Model of a throttle valve](http://www.texample.net/tikz/examples/throttle-valve/)
<img src="http://www.texample.net/media/tikz/examples/PNG/throttle-valve.png" width="250">

[Motivation model diagram Heckhausen Rheinberg](http://www.texample.net/tikz/examples/model-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/model-diagram.png" width="150">

[Nested Grids in SWAN and WAM coupling](http://www.texample.net/tikz/examples/nested-grids-in-swan-and-wam-coupling/)
<img src="http://www.texample.net/media/tikz/examples/PNG/nested-grids-in-swan-and-wam-coupling.png" width="150">

[Nice shaded/framed paragraphs using tikz and framed](http://www.texample.net/tikz/examples/framed-tikz/)
<img src="http://www.texample.net/media/tikz/examples/PNG/framed-tikz.png" width="150">

[Oblique Incidence](http://www.texample.net/tikz/examples/oblique-incidence/)
<img src="http://www.texample.net/media/tikz/examples/PNG/oblique-incidence.png" width="150">

[Observer/Estimator](http://www.texample.net/tikz/examples/observer-estimator/)
<img src="http://www.texample.net/media/tikz/examples/PNG/observer-estimator.png" width="150">

[PDCA cycle](http://www.texample.net/tikz/examples/pdca-cycle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pdca-cycle.png" width="150">

[PGF 2.0 title page](http://www.texample.net/tikz/examples/pgf2-titlepage/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pgf2-titlepage.png" width="150">

[Phasor diagram](http://www.texample.net/tikz/examples/phasor-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/phasor-diagram.png" width="150">

[Physical pendulum](http://www.texample.net/tikz/examples/physical-pendulum/)
<img src="http://www.texample.net/media/tikz/examples/PNG/physical-pendulum.png" width="150">

[Principle of X-ray photoelectron spectroscopy (XPS)](http://www.texample.net/tikz/examples/principle-of-x-ray-photoelectron-spectroscopy-xps/)
<img src="http://www.texample.net/media/tikz/examples/PNG/principle-of-x-ray-photoelectron-spectroscopy-xps.png" width="150">

[Principle of separated control and safety systems](http://www.texample.net/tikz/examples/sontrol-safety-system/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sontrol-safety-system.png" width="150">

[Rainbows - Sun ray entering a rain drop](http://www.texample.net/tikz/examples/raindrop/)
<img src="http://www.texample.net/media/tikz/examples/PNG/raindrop.png" width="150">

[Refraction - Snell’s Law](http://www.texample.net/tikz/examples/refraction/)
<img src="http://www.texample.net/media/tikz/examples/PNG/refraction.png" width="150">

[Semiconductor pn junction diagram](http://www.texample.net/tikz/examples/junction-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/junction-diagram.png" width="150">

[Simulating hand-drawn lines with TikZ](http://www.texample.net/tikz/examples/hand-drawn-lines/)
<img src="http://www.texample.net/media/tikz/examples/PNG/hand-drawn-lines.png" width="150">

[Splitting of Hydrogen in different strong magnetic fields](http://www.texample.net/tikz/examples/hydrogen-splitting/)
<img src="http://www.texample.net/media/tikz/examples/PNG/hydrogen-splitting.png" width="150">

[Standard model of physics](http://www.texample.net/tikz/examples/model-physics/)
<img src="http://www.texample.net/media/tikz/examples/PNG/model-physics.png" width="150">

[Sunset](http://www.texample.net/tikz/examples/sunset/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sunset.png" width="150">

[Table in the shape of an arrow](http://www.texample.net/tikz/examples/arrow-table/)
<img src="http://www.texample.net/media/tikz/examples/PNG/arrow-table.png" width="150">

[The Perrin - Jablonski diagram](http://www.texample.net/tikz/examples/the-perrin-jablonski-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/the-perrin-jablonski-diagram.png" width="150">

[TikZ and PGF version 2.00](http://www.texample.net/tikz/examples/pgf-version-2/)
<img src="http://texample.net/media/tikz/examples/extra/pgf-version-2/mpgf2001.png" width="150">

[Title graphics](http://www.texample.net/tikz/examples/title-graphics/)
<img src="http://www.texample.net/media/tikz/examples/PNG/title-graphics.png" width="150">

[Torn paper with matching torn edges](http://www.texample.net/tikz/examples/torn-paper/)
<img src="http://www.texample.net/media/tikz/examples/PNG/torn-paper.png" width="150">

#### Fadings (12 items)

[Coffee cup](http://www.texample.net/tikz/examples/coffee-cup/)
<img src="http://www.texample.net/media/tikz/examples/PNG/coffee-cup.png" width="150">

[Fading text](http://www.texample.net/tikz/examples/text-fading/)
<img src="http://www.texample.net/media/tikz/examples/PNG/text-fading.png" width="150">

[Fireworks](http://www.texample.net/tikz/examples/fireworks/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fireworks.png" width="150">

[High harmonics](http://www.texample.net/tikz/examples/high-harmonics/)
<img src="http://www.texample.net/media/tikz/examples/PNG/high-harmonics.png" width="300">

[Mandala](http://www.texample.net/tikz/examples/mandala/)
<img src="http://www.texample.net/media/tikz/examples/PNG/mandala.png" width="150">

[Poppy flower](http://www.texample.net/tikz/examples/poppy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/poppy.png" width="150">

[RGB triangle](http://www.texample.net/tikz/examples/rgb-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rgb-triangle.png" width="150">

[Sunset](http://www.texample.net/tikz/examples/sunset/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sunset.png" width="150">

[Transmission Electron Microscope System](http://www.texample.net/tikz/examples/transmission-electron-microscope/)
<img src="http://www.texample.net/media/tikz/examples/PNG/transmission-electron-microscope.png" width="150">

[Windshield wiper](http://www.texample.net/tikz/examples/windshield-wiper/)
<img src="http://www.texample.net/media/tikz/examples/PNG/windshield-wiper.png" width="150">

#### Fit (6 items)

[BER measurement on fibre optical system](http://www.texample.net/tikz/examples/BER-measurement/)
<img src="http://www.texample.net/media/tikz/examples/PNG/BER-measurement.png" width="150">

[Computer diagram](http://www.texample.net/tikz/examples/computer-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/computer-diagram.png" width="150">

[Fitting text to a shape](http://www.texample.net/tikz/examples/text-shape/)
<img src="http://www.texample.net/media/tikz/examples/PNG/text-shape.png" width="150">

[Flowchart](http://www.texample.net/tikz/examples/flowchart/)
<img src="http://www.texample.net/media/tikz/examples/PNG/flowchart.png" width="150">

[Highlighting elements in matrices](http://www.texample.net/tikz/examples/highlighting-matrix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/highlighting-matrix.png" width="150">

[Quantum circuit](http://www.texample.net/tikz/examples/quantum-circuit/)
<img src="http://www.texample.net/media/tikz/examples/PNG/quantum-circuit.png" width="150">

#### Foreach (96 items)

[A complete graph](http://www.texample.net/tikz/examples/complete-graph/)
<img src="http://www.texample.net/media/tikz/examples/PNG/complete-graph.png" width="150">

[A simple cycle](http://www.texample.net/tikz/examples/cycle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/cycle.png" width="150">

[A simple graph-model in 3D](http://www.texample.net/tikz/examples/3d-graph-model/)
<img src="http://www.texample.net/media/tikz/examples/PNG/3d-graph-model.png" width="150">

[Airfoil profiles](http://www.texample.net/tikz/examples/airfoil-profiles/)
<img src="http://www.texample.net/media/tikz/examples/PNG/airfoil-profiles.png" width="150">

[Andler optimal lot-size](http://www.texample.net/tikz/examples/andler-optimal-lot-size/)
<img src="http://www.texample.net/media/tikz/examples/PNG/andler-optimal-lot-size.png" width="150">

[Animated illustration of the convolution of two functions](http://www.texample.net/tikz/examples/convolution-of-two-functions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/convolution-of-two-functions.png" width="250">

[Animated set intersection](http://www.texample.net/tikz/examples/animated-set-intersection/)
<img src="http://www.texample.net/media/tikz/examples/PNG/animated-set-intersection.png" width="150">

[Arithmetic mean as center of mass](http://www.texample.net/tikz/examples/balance/)
<img src="http://www.texample.net/media/tikz/examples/PNG/balance.png" width="150">

[Arithmetic of the clock](http://www.texample.net/tikz/examples/arithmetic-of-the-clock/)
<img src="http://www.texample.net/media/tikz/examples/PNG/arithmetic-of-the-clock.png" width="150">

[Atoms and orbitals](http://www.texample.net/tikz/examples/atoms-and-orbitals/)
<img src="http://www.texample.net/media/tikz/examples/PNG/atoms-and-orbitals.png" width="150">

[Automata](http://www.texample.net/tikz/examples/automata/)
<img src="http://www.texample.net/media/tikz/examples/PNG/automata.png" width="250">

[Block diagram line junctions](http://www.texample.net/tikz/examples/line-junctions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/line-junctions.png" width="150">

[C(n,4) points of intersection](http://www.texample.net/tikz/examples/cn4-points-of-intersection/)
<img src="http://www.texample.net/media/tikz/examples/PNG/cn4-points-of-intersection.png" width="150">

[Circular arrows with text](http://www.texample.net/tikz/examples/circular-arrows-text/)
<img src="http://www.texample.net/media/tikz/examples/PNG/circular-arrows-text.png" width="150">

[Clusters of atoms](http://www.texample.net/tikz/examples/clusters-of-atoms/)
<img src="http://www.texample.net/media/tikz/examples/PNG/clusters-of-atoms.png" width="150">

[Coffee cup](http://www.texample.net/tikz/examples/coffee-cup/)
<img src="http://www.texample.net/media/tikz/examples/PNG/coffee-cup.png" width="150">

[Coloring diagrams - linear relaxation](http://www.texample.net/tikz/examples/colored-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/colored-diagram.png" width="250">

[Combinatorial graphs](http://www.texample.net/tikz/examples/combinatorial-graphs/)
<img src="http://www.texample.net/media/tikz/examples/PNG/combinatorial-graphs.png" width="200">

[Computer diagram](http://www.texample.net/tikz/examples/computer-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/computer-diagram.png" width="150">

[D flip-flops and shift register](http://www.texample.net/tikz/examples/d-flip-flops-and-shift-register/)
<img src="http://www.texample.net/media/tikz/examples/PNG/d-flip-flops-and-shift-register.png" width="250">

[Dartboard](http://www.texample.net/tikz/examples/dartboard/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dartboard.png" width="150">

[Database decimation process](http://www.texample.net/tikz/examples/database-decimation-process/)
<img src="http://www.texample.net/media/tikz/examples/PNG/database-decimation-process.png" width="200">

[Degree wheel](http://www.texample.net/tikz/examples/degree-wheel/)
<img src="http://www.texample.net/media/tikz/examples/PNG/degree-wheel.png" width="150">

[Difference quotient](http://www.texample.net/tikz/examples/difference-quotient/)
<img src="http://www.texample.net/media/tikz/examples/PNG/difference-quotient.png" width="200">

[Dipolar magnetic field](http://www.texample.net/tikz/examples/dipolar-magnetic-field/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dipolar-magnetic-field.png" width="150">

[Distance, velocity and acceleration vectors](http://www.texample.net/tikz/examples/dva-vectors/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dva-vectors.png" width="150">

[Distributed processing](http://www.texample.net/tikz/examples/distributed-processing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/distributed-processing.png" width="200">

[Drawing lattice points and vectors](http://www.texample.net/tikz/examples/lattice-points/)
<img src="http://www.texample.net/media/tikz/examples/PNG/lattice-points.png" width="150">

[Energy level diagrams - illustrating Hund’s rule](http://www.texample.net/tikz/examples/energy-levels/)
<img src="http://www.texample.net/media/tikz/examples/PNG/energy-levels.png" width="200">

[Falling dominoes](http://www.texample.net/tikz/examples/dominoes/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dominoes.png" width="150">

[Fibonacci spiral](http://www.texample.net/tikz/examples/fibonacci-spiral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fibonacci-spiral.png" width="200">

[Genaille and Lucas sticks for multiplication and division](http://www.texample.net/tikz/examples/genaille-and-lucas-sticks/)
<img src="http://www.texample.net/media/tikz/examples/PNG/genaille-and-lucas-sticks.png" width="150">

[Guitar chords](http://www.texample.net/tikz/examples/guitar-chords/)
<img src="http://www.texample.net/media/tikz/examples/PNG/guitar-chords.png" width="150">

[H-tree and b-tree](http://www.texample.net/tikz/examples/h-tree/)
<img src="http://www.texample.net/media/tikz/examples/PNG/h-tree.png" width="150">

[Hypercycle](http://www.texample.net/tikz/examples/hypercycle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/hypercycle.png" width="150">

[Idealised directional spectrum](http://www.texample.net/tikz/examples/idealised-directional-spectrum/)
<img src="http://www.texample.net/media/tikz/examples/PNG/idealised-directional-spectrum.png" width="150">

[Lambert-Beer law parameters drawing](http://www.texample.net/tikz/examples/lambert-beer-law/)
<img src="http://www.texample.net/media/tikz/examples/PNG/lambert-beer-law.png" width="150">

[Line Plot Example](http://www.texample.net/tikz/examples/line-plot-example/)
<img src="http://www.texample.net/media/tikz/examples/PNG/line-plot-example.png" width="150">

[Linear regression](http://www.texample.net/tikz/examples/linear-regression/)
<img src="http://www.texample.net/media/tikz/examples/PNG/linear-regression.png" width="150">

[Logarithmic spiral](http://www.texample.net/tikz/examples/logarithmic-spiral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/logarithmic-spiral.png" width="150">

[Mandala](http://www.texample.net/tikz/examples/mandala/)
<img src="http://www.texample.net/media/tikz/examples/PNG/mandala.png" width="150">

[Map of a HiSPARC detector inside the KASCADE experiment](http://www.texample.net/tikz/examples/kascade-map/)
<img src="http://www.texample.net/media/tikz/examples/PNG/kascade-map.png" width="150">

[Membrane and Ions](http://www.texample.net/tikz/examples/membrane-ions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/membrane-ions.png" width="150">

[More tikz-timing examples](http://www.texample.net/tikz/examples/more-tikz-timing-examples/)
<img src="http://www.texample.net/media/tikz/examples/PNG/more-tikz-timing-examples.png" width="150">

[Mosaic from Pompeii](http://www.texample.net/tikz/examples/mosaic-from-pompeii/)
<img src="http://www.texample.net/media/tikz/examples/PNG/mosaic-from-pompeii.png" width="150">

[Neural network](http://www.texample.net/tikz/examples/neural-network/)
<img src="http://www.texample.net/media/tikz/examples/PNG/neural-network.png" width="200">

[Optical Fiber Polarization Controller](http://www.texample.net/tikz/examples/polarization-controller/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polarization-controller.png" width="150">

[P2P system topology](http://www.texample.net/tikz/examples/p2p-topology/)
<img src="http://www.texample.net/media/tikz/examples/PNG/p2p-topology.png" width="150">

[Parameterised pig](http://www.texample.net/tikz/examples/parameterised-pig/)
<img src="http://www.texample.net/media/tikz/examples/PNG/parameterised-pig.png" width="150">

[Parameterized plots](http://www.texample.net/tikz/examples/parameterized-plots/)
<img src="http://www.texample.net/media/tikz/examples/PNG/parameterized-plots.png" width="150">

[Pascal triangle](http://www.texample.net/tikz/examples/pascal-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pascal-triangle.png" width="150">

[Pascal’s triangle and Sierpinski triangle](http://www.texample.net/tikz/examples/pascals-triangle-and-sierpinski-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pascals-triangle-and-sierpinski-triangle.png" width="150">

[Periodic boundaries conditions](http://www.texample.net/tikz/examples/periodic-boundaries-conditions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/periodic-boundaries-conditions.png" width="150">

[Perpendicular bisectors of a triangle](http://www.texample.net/tikz/examples/bisector/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bisector.png" width="150">

[Perpendicular bissector](http://www.texample.net/tikz/examples/perpendicular-bissector/)
<img src="http://www.texample.net/media/tikz/examples/PNG/perpendicular-bissector.png" width="150">

[Pie chart](http://www.texample.net/tikz/examples/pie-chart/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pie-chart.png" width="150">

[Pie chart with colors](http://www.texample.net/tikz/examples/pie-chart-color/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pie-chart-color.png" width="150">

[Poincare Diagram, Classification of Phase Portraits](http://www.texample.net/tikz/examples/poincare/)
<img src="http://www.texample.net/media/tikz/examples/PNG/poincare.png" width="200">

[Polar coordinates template](http://www.texample.net/tikz/examples/polar-coordinates-template/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polar-coordinates-template.png" width="150">

[Polygon division](http://www.texample.net/tikz/examples/polygon-division/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polygon-division.png" width="150">

[Prim’s algorithm](http://www.texample.net/tikz/examples/prims-algorithm/)
<img src="http://www.texample.net/media/tikz/examples/PNG/prims-algorithm.png" width="150">

[Principle of X-ray photoelectron spectroscopy (XPS)](http://www.texample.net/tikz/examples/principle-of-x-ray-photoelectron-spectroscopy-xps/)
<img src="http://www.texample.net/media/tikz/examples/PNG/principle-of-x-ray-photoelectron-spectroscopy-xps.png" width="150">

[Projection of circles onto a spherical surface](http://www.texample.net/tikz/examples/dome/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dome.png" width="150">

[Puzzle](http://www.texample.net/tikz/examples/puzzle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/puzzle.png" width="150">

[RGB color mixing](http://www.texample.net/tikz/examples/rgb-color-mixing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rgb-color-mixing.png" width="150">

[RNA codons table](http://www.texample.net/tikz/examples/rna-codons-table/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rna-codons-table.png" width="150">

[RPM disc](http://www.texample.net/tikz/examples/rpm-disc/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rpm-disc.png" width="150">

[Radix-2 FFT signal flow](http://www.texample.net/tikz/examples/radix2fft/)
<img src="http://www.texample.net/media/tikz/examples/PNG/radix2fft.png" width="150">

[Regular polygons](http://www.texample.net/tikz/examples/regular-polygons/)
<img src="http://www.texample.net/media/tikz/examples/PNG/regular-polygons.png" width="150">

[Replicating triangles](http://www.texample.net/tikz/examples/triangles/)
<img src="http://www.texample.net/media/tikz/examples/PNG/triangles.png" width="150">

[Representation of a geometric series](http://www.texample.net/tikz/examples/geometric-series/)
<img src="http://www.texample.net/media/tikz/examples/PNG/geometric-series.png" width="150">

[Rooty helix](http://www.texample.net/tikz/examples/rooty-helix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rooty-helix.png" width="150">

[Rose rhodonea curve](http://www.texample.net/tikz/examples/rose-rhodonea-curve/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rose-rhodonea-curve.png" width="150">

[Rotated polygons](http://www.texample.net/tikz/examples/rotated-polygons/)
<img src="" width="150">

[Rotated squares](http://www.texample.net/tikz/examples/rotated-squares/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rotated-squares.png" width="150">

[Rotated triangle](http://www.texample.net/tikz/examples/rotated-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rotated-triangle.png" width="150">

[Rusting Iron](http://www.texample.net/tikz/examples/rusting-iron/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rusting-iron.png" width="150">

[Scatterplot](http://www.texample.net/tikz/examples/scatterplot/)
<img src="http://www.texample.net/media/tikz/examples/PNG/scatterplot.png" width="150">

[Seismic focal mechanism in 3D view.](http://www.texample.net/tikz/examples/seismic-focal-mechanism-in-3d-view/)
<img src="http://www.texample.net/media/tikz/examples/PNG/seismic-focal-mechanism-in-3d-view.png" width="150">

[Semiconductor pn junction diagram](http://www.texample.net/tikz/examples/junction-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/junction-diagram.png" width="150">

[Skype network topology](http://www.texample.net/tikz/examples/skype-topology/)
<img src="http://www.texample.net/media/tikz/examples/PNG/skype-topology.png" width="150">

[Smooth maps](http://www.texample.net/tikz/examples/smooth-maps/)
<img src="http://www.texample.net/media/tikz/examples/PNG/smooth-maps.png" width="150">

[Spiderweb diagram](http://www.texample.net/tikz/examples/spiderweb-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/spiderweb-diagram.png" width="150">

[Stacked discs in 3d](http://www.texample.net/tikz/examples/disc/)
<img src="http://www.texample.net/media/tikz/examples/PNG/disc.png" width="150">

[Standard deviation](http://www.texample.net/tikz/examples/standard-deviation/)
<img src="http://www.texample.net/media/tikz/examples/PNG/standard-deviation.png" width="250">

[Sudoku](http://www.texample.net/tikz/examples/sudoku/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sudoku.png" width="250">

[Symmetries of the plane](http://www.texample.net/tikz/examples/symmetries/)
<img src="http://www.texample.net/media/tikz/examples/PNG/symmetries.png" width="150">
<img src="http://texample.net/media/tikz/examples/thumbs/symmetry17.jpg" width="250">

[System Combination](http://www.texample.net/tikz/examples/system-combination/)
<img src="http://www.texample.net/media/tikz/examples/PNG/system-combination.png" width="150">

[The Olympic rings](http://www.texample.net/tikz/examples/the-olympic-rings/)
<img src="http://www.texample.net/media/tikz/examples/PNG/the-olympic-rings.png" width="150">

[The Perrin - Jablonski diagram](http://www.texample.net/tikz/examples/the-perrin-jablonski-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/the-perrin-jablonski-diagram.png" width="150">

[The electric dipole moment (p) in the water molecule](http://www.texample.net/tikz/examples/electric-dipole/)
<img src="http://www.texample.net/media/tikz/examples/PNG/electric-dipole.png" width="150">

[Time course of events in an experiment](http://www.texample.net/tikz/examples/events/)
<img src="http://www.texample.net/media/tikz/examples/PNG/events.png" width="150">

[Towers of Hanoi](http://www.texample.net/tikz/examples/towers-of-hanoi/)
<img src="http://www.texample.net/media/tikz/examples/PNG/towers-of-hanoi.png" width="150">

[Turing machine](http://www.texample.net/tikz/examples/turing-machine/)
<img src="http://www.texample.net/media/tikz/examples/PNG/turing-machine.png" width="150">

[Ulam spiral](http://www.texample.net/tikz/examples/ulam-spiral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/ulam-spiral.png" width="150">

[Unit circle](http://www.texample.net/tikz/examples/unit-circle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/unit-circle.png" width="150">

#### Forest (1 item)

[Hierarchical diagram](http://www.texample.net/tikz/examples/hierarchical-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/hierarchical-diagram.png" width="250">

#### Intersections (7 items)

[Biconcave lens](http://www.texample.net/tikz/examples/biconcave-lens/)
<img src="http://www.texample.net/media/tikz/examples/PNG/biconcave-lens.png" width="150">

[Conics - Polars and Tangents](http://www.texample.net/tikz/examples/polars-tangents-conic/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polars-tangents-conic.png" width="150">

[Energy levels of a fluor molecule](http://www.texample.net/tikz/examples/fluor-energy-levels/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fluor-energy-levels.png" width="150">

[Handling the crossover of intersecting lines](http://www.texample.net/tikz/examples/line-junction/)
<img src="http://www.texample.net/media/tikz/examples/PNG/line-junction.png" width="150">

[Shake and Rattle on a planar pendulum example](http://www.texample.net/tikz/examples/shake-rattle-pendulum/)
<img src="http://www.texample.net/media/tikz/examples/PNG/shake-rattle-pendulum.png" width="150">

[Steradian cone in sphere](http://www.texample.net/tikz/examples/steradian-cone-sphere/)
<img src="http://www.texample.net/media/tikz/examples/PNG/steradian-cone-sphere.png" width="150">

[Supersonic nozzle technical drawing](http://www.texample.net/tikz/examples/supersonic-nozzle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/supersonic-nozzle.png" width="150">

#### Layers (17 items)

[Animated illustration of the convolution of two functions.](http://www.texample.net/tikz/examples/convolution-of-two-functions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/convolution-of-two-functions.png" width="200">

[Atoms and orbitals](http://www.texample.net/tikz/examples/atoms-and-orbitals/)
<img src="http://www.texample.net/media/tikz/examples/PNG/atoms-and-orbitals.png" width="150">

[Bode plot](http://www.texample.net/tikz/examples/bode-plot/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bode-plot.png" width="200">

[Difference quotient](http://www.texample.net/tikz/examples/difference-quotient/)
<img src="http://www.texample.net/media/tikz/examples/PNG/difference-quotient.png" width="200">

[Distributed processing](http://www.texample.net/tikz/examples/distributed-processing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/distributed-processing.png" width="150">

[Inertial navigation system](http://www.texample.net/tikz/examples/inertial-navigation-system/)
<img src="http://www.texample.net/media/tikz/examples/PNG/inertial-navigation-system.png" width="150">

[Kalman Filter System Model](http://www.texample.net/tikz/examples/kalman-filter/)
<img src="http://www.texample.net/media/tikz/examples/PNG/kalman-filter.png" width="150">

[More tikz-timing examples](http://www.texample.net/tikz/examples/more-tikz-timing-examples/)
<img src="http://www.texample.net/media/tikz/examples/PNG/more-tikz-timing-examples.png" width="150">

[Nice shaded/framed paragraphs using tikz and framed](http://www.texample.net/tikz/examples/framed-tikz/)
<img src="http://www.texample.net/media/tikz/examples/PNG/framed-tikz.png" width="150">

[Pascal’s triangle and Sierpinski triangle](http://www.texample.net/tikz/examples/pascals-triangle-and-sierpinski-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pascals-triangle-and-sierpinski-triangle.png" width="150">

[Prim’s algorithm](http://www.texample.net/tikz/examples/prims-algorithm/)
<img src="http://www.texample.net/media/tikz/examples/PNG/prims-algorithm.png" width="150">

[Quantum circuit](http://www.texample.net/tikz/examples/quantum-circuit/)
<img src="http://www.texample.net/media/tikz/examples/PNG/quantum-circuit.png" width="150">

[Rooty helix](http://www.texample.net/tikz/examples/rooty-helix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rooty-helix.png" width="150">

[Rules](http://www.texample.net/tikz/examples/rules/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rules.png" width="150">

[Scientific interactions](http://www.texample.net/tikz/examples/scientific-interactions/)
<img src="http://www.texample.net/media/tikz/examples/PNG/scientific-interactions.png" width="150">

[System Combination](http://www.texample.net/tikz/examples/system-combination/)
<img src="http://www.texample.net/media/tikz/examples/PNG/system-combination.png" width="150">

[Timing diagram with the tikz-timing package](http://www.texample.net/tikz/examples/tikz-timing/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tikz-timing.png" width="150">

#### LuaTeX (2 items)

[Enderman](http://www.texample.net/tikz/examples/enderman/)
<img src="http://www.texample.net/media/tikz/examples/PNG/enderman.png" width="150">

[Plot of the Brillouin Function](http://www.texample.net/tikz/examples/brillouin-function/)
<img src="http://www.texample.net/media/tikz/examples/PNG/brillouin-function.png" width="150">

#### Markings (5 items)

[Direct torque control of AC drive](http://www.texample.net/tikz/examples/ac-drive-dtc/)
<img src="http://www.texample.net/media/tikz/examples/PNG/ac-drive-dtc.png" width="150">

[Poincare Diagram, Classification of Phase Portraits](http://www.texample.net/tikz/examples/poincare/)
<img src="http://www.texample.net/media/tikz/examples/PNG/poincare.png" width="150">

[Principle of separated control and safety systems](http://www.texample.net/tikz/examples/sontrol-safety-system/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sontrol-safety-system.png" width="150">

[Rainbows - Sun ray entering a rain drop](http://www.texample.net/tikz/examples/raindrop/)
<img src="http://www.texample.net/media/tikz/examples/PNG/raindrop.png" width="150">

[Refraction - Snell’s Law](http://www.texample.net/tikz/examples/refraction/)
<img src="http://www.texample.net/media/tikz/examples/PNG/refraction.png" width="150">

#### Mathematical engine (41 items)

[Andler optimal lot-size](http://www.texample.net/tikz/examples/andler-optimal-lot-size/)
<img src="http://www.texample.net/media/tikz/examples/PNG/andler-optimal-lot-size.png" width="150">

[Animated definite integral](http://www.texample.net/tikz/examples/animated-definite-integral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/animated-definite-integral.png" width="150">

[Annotated 3D box](http://www.texample.net/tikz/examples/annotated-3d-box/)
<img src="http://www.texample.net/media/tikz/examples/PNG/annotated-3d-box.png" width="150">

[Archimedes’s approximation of pi](http://www.texample.net/tikz/examples/archimedess-approximation-of-pi/)
<img src="http://www.texample.net/media/tikz/examples/PNG/archimedess-approximation-of-pi.png" width="150">

[Arithmetic of the clock](http://www.texample.net/tikz/examples/arithmetic-of-the-clock/)
<img src="http://www.texample.net/media/tikz/examples/PNG/arithmetic-of-the-clock.png" width="150">

[C(n,4) points of intersection](http://www.texample.net/tikz/examples/cn4-points-of-intersection/)
<img src="http://www.texample.net/media/tikz/examples/PNG/cn4-points-of-intersection.png" width="150">

[Database decimation process](http://www.texample.net/tikz/examples/database-decimation-process/)
<img src="http://www.texample.net/media/tikz/examples/PNG/database-decimation-process.png" width="150">

[Dipolar magnetic field](http://www.texample.net/tikz/examples/dipolar-magnetic-field/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dipolar-magnetic-field.png" width="150">

[Fibonacci spiral](http://www.texample.net/tikz/examples/fibonacci-spiral/)
<img src="http://www.texample.net/media/tikz/examples/PNG/fibonacci-spiral.png" width="150">

[Ford circle](http://www.texample.net/tikz/examples/ford-circle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/ford-circle.png" width="150">

[Genaille and Lucas sticks for multiplication and division](http://www.texample.net/tikz/examples/genaille-and-lucas-sticks/)
<img src="http://www.texample.net/media/tikz/examples/PNG/genaille-and-lucas-sticks.png" width="150">

[Highlighting elements in matrices](http://www.texample.net/tikz/examples/highlighting-matrix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/highlighting-matrix.png" width="150">

[Karnaugh diagram](http://www.texample.net/tikz/examples/karnaugh-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/karnaugh-diagram.png" width="150">

[Morley’s triangle](http://www.texample.net/tikz/examples/morleys-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/morleys-triangle.png" width="150">

[Nine points circle of a triangle](http://www.texample.net/tikz/examples/nine-points-circle-of-a-triangle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/nine-points-circle-of-a-triangle.png" width="150">

[Parameterized plots](http://www.texample.net/tikz/examples/parameterized-plots/)
<img src="http://www.texample.net/media/tikz/examples/PNG/parameterized-plots.png" width="150">

[Perpendicular bisectors of a triangle](http://www.texample.net/tikz/examples/bisector/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bisector.png" width="150">

[Perpendicular bissector](http://www.texample.net/tikz/examples/perpendicular-bissector/)
<img src="http://www.texample.net/media/tikz/examples/PNG/perpendicular-bissector.png" width="150">

[Pie chart with colors](http://www.texample.net/tikz/examples/pie-chart-color/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pie-chart-color.png" width="150">

[Plane Sections of the Cylinder - Dandelin Spheres](http://www.texample.net/tikz/examples/dandelin-spheres/)
<img src="http://www.texample.net/media/tikz/examples/PNG/dandelin-spheres.png" width="150">

[Polarizing microscope](http://www.texample.net/tikz/examples/polarizing-microscope/)
<img src="http://www.texample.net/media/tikz/examples/PNG/polarizing-microscope.png" width="250">

[Projectile](http://www.texample.net/tikz/examples/projectile/)
<img src="http://www.texample.net/media/tikz/examples/PNG/projectile.png" width="150">

[RNA codons table](http://www.texample.net/tikz/examples/rna-codons-table/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rna-codons-table.png" width="150">

[Rainbows - Sun ray entering a rain drop](http://www.texample.net/tikz/examples/raindrop/)
<img src="http://www.texample.net/media/tikz/examples/PNG/raindrop.png" width="150">

[Spherical and cartesian grids](http://www.texample.net/tikz/examples/spherical-and-cartesian-grids/)
<img src="http://www.texample.net/media/tikz/examples/PNG/spherical-and-cartesian-grids.png" width="150">

[Spherical polar pots with 3dplot](http://www.texample.net/tikz/examples/spherical-polar-pots-with-3dplot/)
<img src="http://www.texample.net/media/tikz/examples/PNG/spherical-polar-pots-with-3dplot.png" width="150">

[Sunflower pattern (Phyllotaxy)](http://www.texample.net/tikz/examples/phyllotaxy/)
<img src="http://www.texample.net/media/tikz/examples/PNG/phyllotaxy.png" width="150">

[TCP state machine](http://www.texample.net/tikz/examples/tcp-state-machine/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tcp-state-machine.png" width="150">

[The Earth’s orbit around the Sun](http://www.texample.net/tikz/examples/earth-orbit/)
<img src="http://www.texample.net/media/tikz/examples/PNG/earth-orbit.png" width="150">

[Unit circle](http://www.texample.net/tikz/examples/unit-circle/)
<img src="http://www.texample.net/media/tikz/examples/PNG/unit-circle.png" width="150">

[Using signed distance functions to embed contours in discrete grids](http://www.texample.net/tikz/examples/contours-grids/)
<img src="http://www.texample.net/media/tikz/examples/PNG/contours-grids.png" width="150">

[Venn diagram with magnifier](http://www.texample.net/tikz/examples/venn-diagram-with-magnifier/)
<img src="http://www.texample.net/media/tikz/examples/PNG/venn-diagram-with-magnifier.png" width="200">

#### Matrices (25 items)

[A CONSORT-style flowchart of a randomized controlled trial](http://www.texample.net/tikz/examples/consort-flowchart/)
<img src="http://www.texample.net/media/tikz/examples/PNG/consort-flowchart.png" width="150">

[BER measurement on fibre optical system](http://www.texample.net/tikz/examples/BER-measurement/)
<img src="http://www.texample.net/media/tikz/examples/PNG/BER-measurement.png" width="150">

[Butterfly Lemma](http://www.texample.net/tikz/examples/butterfly-lemma/)
<img src="http://www.texample.net/media/tikz/examples/PNG/butterfly-lemma.png" width="150">

[Chains with labeled edges](http://www.texample.net/tikz/examples/labeled-chain/)
<img src="http://www.texample.net/media/tikz/examples/PNG/labeled-chain.png" width="200">

[Commutative diagram](http://www.texample.net/tikz/examples/commutative-diagram-tikz/)
<img src="http://www.texample.net/media/tikz/examples/PNG/commutative-diagram-tikz.png" width="150">

[Commutative diagram with crossing edges](http://www.texample.net/tikz/examples/commutative-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/commutative-diagram.png" width="150">

[Data flow diagram](http://www.texample.net/tikz/examples/data-flow-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/data-flow-diagram.png" width="150">

[Free body diagrams](http://www.texample.net/tikz/examples/free-body-diagrams/)
<img src="http://www.texample.net/media/tikz/examples/PNG/free-body-diagrams.png" width="150">

[Kalman Filter System Model](http://www.texample.net/tikz/examples/kalman-filter/)
<img src="http://www.texample.net/media/tikz/examples/PNG/kalman-filter.png" width="150">

[Logic diagram](http://www.texample.net/tikz/examples/logic-matrix/)
<img src="http://www.texample.net/media/tikz/examples/PNG/logic-matrix.png" width="150">

[Matrix multiplication](http://www.texample.net/tikz/examples/matrix-multiplication/)
<img src="http://www.texample.net/media/tikz/examples/PNG/matrix-multiplication.png" width="150">

[Mnemonic rule for matrix determinant](http://www.texample.net/tikz/examples/mnemonic-rule-for-matrix-determinant/)
<img src="http://www.texample.net/media/tikz/examples/PNG/mnemonic-rule-for-matrix-determinant.png" width="150">

[Observer/Estimator](http://www.texample.net/tikz/examples/observer-estimator/)
<img src="http://www.texample.net/media/tikz/examples/PNG/observer-estimator.png" width="200">

[PGF version 1.18](http://www.texample.net/tikz/examples/pgf-version-118/)
<img src="http://www.texample.net/media/tikz/examples/PNG/pgf-version-118.png" width="200">

[Python if-then-else syntax diagram](http://www.texample.net/tikz/examples/python-if-then-else-syntax-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/python-if-then-else-syntax-diagram.png" width="250">

[Sequence diagram](http://www.texample.net/tikz/examples/sequence-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sequence-diagram.png" width="150">

[Snake Lemma](http://www.texample.net/tikz/examples/snake-lemma/)
<img src="http://www.texample.net/media/tikz/examples/PNG/snake-lemma.png" width="150">

[Table in the shape of an arrow](http://www.texample.net/tikz/examples/arrow-table/)
<img src="http://www.texample.net/media/tikz/examples/PNG/arrow-table.png" width="150">

#### Mindmaps (4 items)

#### Node positioning (21 items)

[Bayesian Probability Illustration Diagram](http://www.texample.net/tikz/examples/bayes/)
<img src="http://www.texample.net/media/tikz/examples/PNG/bayes.png" width="150">

[Borrowers and lenders](http://www.texample.net/tikz/examples/borrowers-and-lenders/)
<img src="http://www.texample.net/media/tikz/examples/PNG/borrowers-and-lenders.png" width="150">

[Class diagram](http://www.texample.net/tikz/examples/class-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/class-diagram.png" width="150">

[Commutative diagram](http://www.texample.net/tikz/examples/commutative-diagram-tikz/)
<img src="http://www.texample.net/media/tikz/examples/PNG/commutative-diagram-tikz.png" width="150">

[Double Arrows a la Chef](http://www.texample.net/tikz/examples/double-arrows/)
<img src="http://www.texample.net/media/tikz/examples/PNG/double-arrows.png" width="150">

[Drawing a graph](http://www.texample.net/tikz/examples/graph/)
<img src="http://www.texample.net/media/tikz/examples/PNG/graph.png" width="150">

[Entity-Relationship diagram](http://www.texample.net/tikz/examples/entity-relationship-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/entity-relationship-diagram.png" width="150">

[Example for tkz-orm v0.1 2010/01/25](http://www.texample.net/tikz/examples/tkz-orm-example/)
<img src="http://www.texample.net/media/tikz/examples/PNG/tkz-orm-example.png" width="150">

[Flowchart](http://www.texample.net/tikz/examples/flowchart/)
<img src="http://www.texample.net/media/tikz/examples/PNG/flowchart.png" width="150">

[Marketing distribution channel](http://www.texample.net/tikz/examples/marketing-distribution-channel/)
<img src="http://www.texample.net/media/tikz/examples/PNG/marketing-distribution-channel.png" width="150">

[Merge sort recursion tree](http://www.texample.net/tikz/examples/merge-sort-recursion-tree/)
<img src="http://www.texample.net/media/tikz/examples/PNG/merge-sort-recursion-tree.png" width="150">

[Observer/Estimator](http://www.texample.net/tikz/examples/observer-estimator/)
<img src="http://www.texample.net/media/tikz/examples/PNG/observer-estimator.png" width="150">

[P2P system topology](http://www.texample.net/tikz/examples/p2p-topology/)
<img src="http://www.texample.net/media/tikz/examples/PNG/p2p-topology.png" width="150">

[Periodic Table of Chemical Elements](http://www.texample.net/tikz/examples/periodic-table-of-chemical-elements/)
<img src="http://www.texample.net/media/tikz/examples/PNG/periodic-table-of-chemical-elements.png" width="150">

[Porter model](http://www.texample.net/tikz/examples/porter-model/)
<img src="http://www.texample.net/media/tikz/examples/PNG/porter-model.png" width="150">

[Rules](http://www.texample.net/tikz/examples/rules/)
<img src="http://www.texample.net/media/tikz/examples/PNG/rules.png" width="150">

[Sequence diagram](http://www.texample.net/tikz/examples/sequence-diagram/)
<img src="http://www.texample.net/media/tikz/examples/PNG/sequence-diagram.png" width="150">

[Skype network topology](http://www.texample.net/tikz/examples/skype-topology/)
<img src="http://www.texample.net/media/tikz/examples/PNG/skype-topology.png" width="150">

[Timetable](http://www.texample.net/tikz/examples/timetable/)
<img src="http://www.texample.net/media/tikz/examples/PNG/timetable.png" width="150">

[Visualisation of Two’s complement for a 4-bit-value](http://www.texample.net/tikz/examples/complement/)
<img src="http://www.texample.net/media/tikz/examples/PNG/complement.png" width="150">

#### Nodes and shapes (15 items)

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">



<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

#### Layers (17 items)

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

#### LuaTeX (2 items)

#### Markings (5 items)

#### Mathematical engine (41 items)

#### Matrices (25 items)

#### Mindmaps (4 items)

#### Node positioning (21 items)



#### Overlays (10 items)

#### Paper folding (1 item)

#### Patterns (1 item)

#### Pic (5 items)

#### Plotting (20 items)

#### Postactions (2 items)

#### Quotes (1 item)

<img src="" width="150">

#### Remember picture (8 items)

#### Scopes (18 items)

#### Shadings (34 items)

#### Shadows (3 items)

#### Shapes (1 item)

<img src="" width="150">

#### Smartdiagram (6 items)

#### Snakes (5 items)

#### Spy library (5 items)

#### Styles (36 items)

#### To paths (14 items)

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

<img src="" width="150">

#### Transformations (31 items)

#### Transparency (20 items)

#### Trees (16 items)



### Tags



