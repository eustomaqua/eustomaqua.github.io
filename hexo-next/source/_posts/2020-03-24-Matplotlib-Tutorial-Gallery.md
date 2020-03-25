---
title: Matplotlib Tutorials - 5. Gallery
date: 2020-03-24 23:31:03
updated: 
categories:
  - Drafting
tags:
  - Notes
  - Matplotlib
  - Seaborn
---


[Official Tutorials](https://matplotlib.org/3.1.1/tutorials/index.html)  
[Official Gallery](https://matplotlib.org/gallery.html)  
[Seaborn: statistical data visualization](http://seaborn.pydata.org/index.html)  
[深度好文 | Matplotlib可视化最有价值的 50 个图表（附完整 Python 源代码）](http://liyangbit.com/pythonvisualization/matplotlib-top-50-visualizations/)  



# 预备知识

## boxplot v.s. violinplot

### boxplot 箱型图
ref: [Matplotlib学习---用matplotlib画箱线图（boxplot）](https://www.cnblogs.com/HuZihu/p/9481071.html) 

箱线图通过数据的四分位数来展示数据的分布情况。例如：数据的中心位置，数据间的离散程度，是否有异常值等。  
把数据从小到大进行排列并等分成四份，第一分位数 (Q1) ，第二分位数 (Q2) 和第三分位数 (Q3) 分别为数据的第 25%, 50% 和 75% 的数字。  
```markdown
I-------------I o I-------------I o I-------------I o I-------------I  
                  Q1                Q2                 Q3  
    (lower quartile)      (median)     (upper quartile)  
```
四分位间距 (Interquartile range, IQR) = 上分位数 (upper quartile) - 下分位数 (lower quartile) 

箱线图分为两部分，分别是箱 (box) 和须 (whisker)。箱 (box) 用来表示从第一分位到第三分位的数据，须 (whisker) 用来表示数据的范围。   
箱线图从上到下各横线分别表示：数据上限 (通常是 Q3+1.5\*IQR) ，第三分位数 (Q3) ，第二分位数 (中位数)，第一分位数 (Q1)，数据下限 (通常是 Q1-1.5\*IQR) 。有时还有一些圆点，位于数据上下限之外，表示异常值 (outliers)。  
（注：如果数据上下限特别大，那么 whisker 将显示数据的最大值和最小值。）

下图展示了箱线图各部分的含义。摘自 [https://datavizcatalogue.com/methods/box_plot.html](https://datavizcatalogue.com/methods/box_plot.html)  
<!--<img src="https://images2018.cnblogs.com/blog/1247570/201808/1247570-20180820171027180-29907435.png" width="47%">-->
{% gp 1-2 %}
<img src="/images/2020-03/box_plot.png">
<img src="/images/2020-03/box_plot2.png">
{% endgp %}


### violinplot 小提琴图

[关于使用python seaborn库绘制violinplot小提琴图的一些小坑](https://www.cnblogs.com/xc-123456/p/11096964.html)  
[Python：matplotlib 和 Seaborn 之热图、小提琴图和箱线图 (三十四)](http://www.digtime.cn/articles/70/python-matplotlib-he-seaborn-zhi-re-tu-xiao-ti-qin-tu-he-xiang-xian-tu-san-shi-si)  
[深度好文 | Matplotlib可视化最有价值的 50 个图表（附完整 Python 源代码）](http://liyangbit.com/pythonvisualization/matplotlib-top-50-visualizations/)  


ref: [matplotlib 小提琴图（violin plot）](https://cloud.tencent.com/developer/article/1486970)

小提琴图 (Violin Plot) 用于显示数据分布及其概率密度。  
<!--<img src="https://ask.qcloudimg.com/http-save/yehe-6021899/6ku32q2uug.png?imageView2/2/w/1620" width="47%">  -->
<img src="/images/2020-03/6ku32q2uug.png" width="47%">  
这种图表结合了箱形图和密度图的特征，主要用来显示数据的分布形状。中间白点为中位数，中间的黑色粗条表示四分位数范围。上下贯穿小提琴图的黑线代表最小非异常值 min 到最大非异常值 max 的区间，线上下端分别代表上限和下限，超出此范围为异常数据。（或者，从黑色粗条延伸的细黑线代表 95% 置信区间）  
Matplotlib 库中，使用 violinplot() 函数来绘制小提琴图。  

ref: [seaborn画小提琴图(violin plot)](https://www.bobobk.com/206.html)

小提琴图是用来展示多组数据的分布状态以及概率密度。跟箱线图类似，但是可以密度层面展示更好。在数据量非常大不方便一个一个展示的时候小提琴图特别适用。而python里面的seaborn包可以很方便的画出小提琴图。  
小提琴图各位置对应参数，中间一条就是箱线图数据，25%，50%，75% 位置，细线区间为 95% 置信区间。  
<!--<img src="https://www.bobobk.com/wp-content/uploads/2019/01/violin.webp" width="43%">-->
<img src="/images/2020-03/violin.webp" width="57%"><!--43%-->

ref: [盒图与小提琴图比较](https://www.osgeo.cn/matplotlib/gallery/statistics/boxplot_vs_violin.html) 

请注意，尽管小提琴图与 Tukey (1977) 的盒形图密切相关，但它们添加了有用的信息，如样本数据的分布 (密度迹线)。  
默认情况下，方框图显示的数据点超出 1.5\* 四分位范围，作为胡须上方或下方的异常值，而小提琴图显示的是整个数据范围。  
关于箱线图及其历史的一个很好的一般参考资料可以在这里找到 [http://vita.had.co.nz/papers/boxplots.pdf](http://vita.had.co.nz/papers/boxplots.pdf)  
小提琴绘图需要 matplotlib>1.4。
有关小提琴绘图的更多信息，SciKit 学习文档有一个很好的部分 [http://scikit-learn.org/stable/modules/density.html](http://scikit-learn.org/stable/modules/density.html)  

### ViolinPlots: more

violin plot (search picture)  
[Original Picture](https://www.bobobk.com/wp-content/uploads/2019/01/violin.webp)  
[Google Search](https://www.google.com/search?newwindow=1&safe=active&tbs=simg:CAQSpQIJtz2-onKcgFEamQILELCMpwgaYgpgCAMSKLQBgBP2H4ET8hL3H5kI2xPBE_1MSoj6YPqcopD6XPqo2oT7SP5opiSsaMJLWwL6Bw0vGxexO4SVbahcbUmez5fJrpK6pXmYVkWfRAOjUJwIcetRTBu746hAPBCAEDAsQjq7-CBoKCggIARIETVGHagwLEJ3twQkakQEKGgoHZGlhZ3JhbdqliPYDCwoJL20vMDJ2MG0yChgKBHBsb3TapYj2AwwKCi9tLzA0cTM0N3kKGwoIbGluZSBhcnTapYj2AwsKCS9tLzA5MTlyeAofCgxjb2xvcmZ1bG5lc3PapYj2AwsKCS9tLzAzMHpsZgobCghwYXJhbGxlbNqliPYDCwoJL20vMDMwemZuDA&sxsrf=ALeKk030JGuj8YjzfCHHqnNJ9SWltbXPcg:1585082037899&q=violin+plot&tbm=isch&sa=X&ved=2ahUKEwj267ve-rPoAhWUPXAKHdNSCakQwg4oAHoECAoQKA&biw=1246&bih=668)  

[Twitter ViolinPlots](https://twitter.com/Dustin_Michels/status/1044454953652109312/photo/1)  
[Medium: Medidas centrais e Boxplot](https://medium.com/@bulcao1998/medidas-centrais-e-boxplot-2a5330d0b331)  
[ViolinPlots](http://frag.mohammedshrine.org/violin-parts-diagram.html), i.e., 
[Violin Plots 101: Visualizing Distribution and Probability Density](https://mode.com/blog/violin-plot-examples)  
[如何解读决策树和随机森林的内部工作机制](http://www.qingpingshan.com/bc/jsp/331216.html)  


#### [如何解读决策树和随机森林的内部工作机制](http://www.qingpingshan.com/bc/jsp/331216.html)
**附 violin 图基础**

violin 图是绘制数字数据的方法，它和箱线图十分相似，但其另外展示了分布的概率密度。下面我们先了解箱线图：
<img src="/images/2020-04/1031362924-12.png" width="53%"><!--47%-->
上图这一组数据表明：
- 最小值等于 5
- 最大值等于 10
- 平均值为 8
- 下四分位数为 7，即第一四分位数 (Q1)，等于该样本中所有数值由小到大排列后第 25% 的值。
- 中位数为 8.5，即第二四分位数 (Q2)，等于该样本中所有数值由小到大排列后第 50% 的值。
- 上四分位数为 9，即第三四分位数 (Q3)，等于该样本中所有数值由小到大排列后第 75% 的值。
- 四分位距为 2 (即 ΔQ=Q3-Q1)。

上述是箱线图的基本参数，箱线图只显示诸如平均值/中值和四分位数范围的汇总统计数据，violin 图显示了数据的完整分布。
<img src="/images/2020-04/1031362T7-13.jpg" width="57%">
violin 图概括了箱线图所表达的统计量：
- 上图白点代表中位数
- 灰色的矩形代表 Q3 和 Q1 之间的四分位距
- 灰线代表 95% 的置信区间

两边的灰色曲线代表核密度估计，其展示了数据的分布形状。其中两边间距较宽的曲线段代表样本总体取给定值有较高的概率，较窄的曲线段表明取给定值有较小的概率。

#### [Medium: Medidas centrais e Boxplot](https://medium.com/@bulcao1998/medidas-centrais-e-boxplot-2a5330d0b331)
Author: ViníciusRibeiro

在本文中，我将解释和分析有关数据科学中的中心度量的一些信息。
1. **四分位数：**  
将有序数据集划分为四个相等的部分时，每个部分代表 25％，即总数据的 1/4。
因此，我们有：
-- 第一四分位数 (下四分位数) 代表样本的 25％ 。 (符号= Q1)
-- 第二个四分位数 (中位数) 代表样本的 50％ 。 (符号= Q2)
-- 第三四分位数 (上四分位数) 的值占订购样本的 75％ 。 (符号= Q3)
2. **箱图**  
它是一种图形工具，显示有序数据集的四分位数之间的差异。
<img src="/images/2020-04/violin-boxplot1.png" width="57%">

3. **四分位间距 (IIQ)：**  
IIQ 或 IQR (四分位数间距) 是上下四分位数之间的差，IQR = Q3-Q1 。围绕中位数的分布代表了 50％ 的样本。
<img src="/images/2020-04/violin-boxplot2.png" width="63%">

4. **小提琴图**  
小提琴或小提琴曲线图与箱形图非常相似，不同之处在于它还通过镜像密度图显示了概率密度。
<img src="/images/2020-04/violin2.png" width="57%">

5. ***让我们练习一下：***
``git clone https://github.com/Kaioh95/Aula_Boxplot.git``

-- **中央措施/中心度量：**    
  在统计中，集中趋势的度量是概率分布的中心值。最常见的中心度量是算术平均值，时尚度和中位数，既可以计算有限数量的值，也可以计算理论分布（例如正态分布）的中心趋势。

-- **平均为收支平衡点：**
  <img src="/images/2020-04/violin-boxplot3.png" width="87%">

-- **通过代数定义平均值：**
  假设分布为 `[x1，x2，x3，...，xn]`，则平均值由希腊字母 μ 表示，并由以下公式定义。
  <img src="/images/2020-04/violin-box-eq1.png" width="57%">

-- **中位数：**
  在某些情况下，依靠平均值不是最佳选择，当我们拥有非常不同的数据时（例如，最小值和最大值之间的幅度（范围）非常宽泛），就会发生这种情况。  
  为了不使我们的模型与这些极端值（与大多数观测值略有不同）产生偏差，我们使用中位数，这是将分布的下半部分与上半部分分开的值。  
  示例：`pd.Series([[1,333,345,355,400,377,392,366,367,348,100000])`。中位数 ()
  中位数结果是：366.0  
  该向量的平均结果约为：9389. 45. 巨大的差异！  

-- **方差：**
  它是离散度的一种度量，表示一组数据与该数据集的期望值 E(x) 可以相距多远。
  <img src="/images/2020-04/violin-box-eq2.png" width="77%">
  注意：平方差可避免将正值添加到负值的问题。

-- **标准差：**
通常用希腊字母 sigma 表示的标准偏差是对均值周围数据分散程度的度量。高标准偏差表示数据从均值散布得更广，而低标准偏差表示更多数据与均值对齐。在一系列数据分析方法中，标准偏差可用于快速确定数据点的离散度。
陷阱：
与平均值一样，如果单独使用，标准偏差也会产生误导。例如，如果数据具有非常奇怪的模式，例如非正态曲线或大量离群值，则标准偏差将无法提供所有必要的信息。

-- **定义标准差：**
如下所示，标准偏差是方差的平方根。
<img src="/images/2020-04/violin-box-eq3.png" width="77%">
高值表示偏离均值，而低值表示分布均值的近似值。

-- **标准偏差-图表：**
<img src="/images/2020-04/violin-boxplot4.png" width="63%"><!--87-->
在水平轴（上图中两个最靠近中心轴的阴影区域）的任何方向上均值的标准差占该组人口的 68％ 。与平均值的两个标准差（最靠近中心区域的四个区域）代表约95％的人口。三个标准差（所有阴影区域）代表约 99％ 的人。

-- **示例-标准偏差：**
在某些限制结果的情况下，例如在产品制造和质量控制中，小的标准偏差可能是目标。直径必须为 2 厘米才能正确安装的特定类型的汽车零件在制造过程中不应具有很大的标准偏差。在这种情况下，较大的标准偏差将意味着许多零件由于无法正确装配在一起而最终进入了垃圾箱。否则汽车将在未来遇到问题。  
但是，在仅观看和记录数据的情况下，较大的标准偏差不一定是一件坏事；它只是反映了正在研究的群体的巨大差异。例如，如果您查看特定公司中每个人的薪水，包括从学生实习生到首席执行官的每个人的薪水，则标准差可能会很大。另一方面，如果仅通过查看寄宿生来限制组，则标准偏差会较小，因为该组中的人员薪水变动较小。第二组数据不是更好，只是可变性较小。

-- **属性-标准偏差：**
以下是一些在解释标准偏差时可以帮助您的属性：
> -由于标准偏差的计算方式以及测量距离的事实，因此标准偏差永远不能为负数（距离绝不是负数）。
> -标准偏差的最小可能值为 0，并且仅在计划的情况下才会发生，其中数据集中的每个数字都完全相同（无偏差）。
> -标准偏差受异常值（数据集中的极低或极高数字）的影响。这是因为标准差基于与均值的距离。请记住，平均值也受异常值的影响。
> -标准偏差的单位与原始数据相同。

-- **离群值：**
离群值是与所有其他数据截然不同的数据，它们是曲线外的点。换句话说，离群值是偏离正态性的值，并且可能（可能会）导致通过算法和分析系统获得的结果异常。  
至少在两个方面，了解异常值是数据分析的基础：
> -离群值会对整个分析结果产生负面影响；
> -异常值的行为可能正是所寻求的。

<img src="/images/2020-04/violin-box-eq4.png" width="87%"> &uarr;\_\_<!--&larr;--> 使用小型数据集时，查找距离其他数据太远的数据会更容易。在这种情况下，只需查看电子表格或表格中的数据，即可轻松找到异常值。
<img src="/images/2020-04/violin-box-eq5.png" width="87%"> &uarr;\_\_<!--&larr;--> 当您拥有更大的数据集时，电子表格可能变得难以发现不一致之处。在这种情况下，找到异常值的一种好方法是**绘制图表**。通过这样做，分析人员可以快速识别出采样有所不同。

-- **自然异常值：**
在找到治疗离群值的最佳方法之前，我们需要了解原因。从这个意义上讲，我们有两种类型的离群值：自然值和人工值。
顾名思义，自然离群值代表所有情况下数据的差异。一些示例是：
> -分析给定地区的预期寿命时，年龄要高一些；
> -损益表，当某人的经济状况比您的团队中其他人做得更好（或更差）时；
> -一家特定商店的销售额比其他连锁店要多得多；
> -远远低于当月目标的销售人员。

-- **人工离群值：**
尽管它们很常见，但大多数异常值都是人为造成的-也就是说，它们来自错误。导致这些离群值的主要错误有 5 个：
> -***输入错误 （数据输入）：***键入或信息收集错误；
> -***抽样错误：***例如，当评估零售连锁店 X 的平均票证时，也会包括 Y 商店的平均票证；
> -***测量错误：***当测量仪器损坏或使用不当时发生；
> -***处理数据*** *时* ***出错：***在预处理数据时发生，可以使用创建异常值的方法；
> -***故意错误：***故意欺骗某些信息而导致的错误。

-- **使用异常值进行操作：**
> -***消除值：***如果您的数据集足够大，则可以简单地排除异常值而不会对数据分析造成重大损害。
> -***单独处理：***如果离群值数量较大，则可以选择仅使用此数据进行单独的分析。可以将它们分为两组，并创建特定的模型进行分析。该解决方案对于调查极端情况非常有用，例如即使在危机时期仍继续销售并获利的公司。
> -***对数转换：对数转换*** 数据是一种可以减少由极端和异常值引起的变化的技术。
> -***聚类方法：***使用这些方法可以找到一种纠正方法，并为异常值赋予新的价值。例如，如果离群值是由输入错误引起的，而不是消除并丢失整个记录行，则一种解决方案是使用聚类算法。这些算法找到最接近异常值的观测值的行为，并干扰最佳近似值。

-- **计算离群值：**
Sup\_out = μ + 1.5 x IQR
Inf\_out = μ - 1.5 x IQR
记住 IQR 是四分位距离
IQR = Q3 - Q1

参考文献：
> 离群值
> [https://www.bixtecnologia.com/home/index.php/5215/outliers-descubra-o-que-sao-e-como-contorna-los-em-sua-analise-de-dados/](https://www.bixtecnologia.com/home/index.php/5215/outliers-descubra-o-que-sao-e-como-contorna-los-em-sua-analise-de-dados/)
> [https://www.aquare.la/o-que-sao-outliers-e-como-trata-los-em-uma-analise-de-dados/](https://www.aquare.la/o-que-sao-outliers-e-como-trata-los-em-uma-analise-de-dados/)
标准偏差
> [https://www.dummies.com/education/math/statistics/how-to-interpret-standard-deviation-in-a-statistical-data-set/](https://www.dummies.com/education/math/statistics/how-to-interpret-standard-deviation-in-a-statistical-data-set/)
> [https://www.bigskyassociates.com/blog/bid/356764/5-Most-Important-Methods-For-Statistical-Data-Analysis](https://www.bigskyassociates.com/blog/bid/356764/5-Most-Important-Methods-For-Statistical-Data-Analysis)
方差
> [https://statistics.laerd.com/statistical-guides/measures-of-spread-range-quartiles.php](https://statistics.laerd.com/statistical-guides/measures-of-spread-range-quartiles.php)
> [https://hbr.org/2019/08/do-you-understand-the-variance-in-your-data](https://hbr.org/2019/08/do-you-understand-the-variance-in-your-data)

<!--
ViníciusRibeiro
撰写者

ViníciusRibeiro
跟随
写下第一个回应
更多来自中型
中等偏上
冠状病毒：锤子和舞蹈
托马斯·普约（Tomas Pueyo）
托马斯·普约（Tomas Pueyo）
年03月20 · 29 分钟读取
83K
中等偏上
您是否不知道有冠状病毒？
万锦海德
马卡姆HEID 的元素
年03月20 · 4 分钟读
12.3千
中等偏上
这是冠状病毒爆发期间您的身体需要的锻炼
科视Christie Aschwanden
克里斯蒂Aschwanden 的元素
年03月21 · 6 分钟读
7.2千
探索中
欢迎来到话语重要的地方。在Medium上，聪明的声音和原始想法成为中心焦点-看不到广告。观看
让您成为中型
关注您关心的所有主题，我们将为您提供最佳故事到您的主页和收件箱。探索
成为会员
无限制地访问Medium 上的最佳故事-并在写作过程中为作家提供支持。只需$ 5 /月。升级版
关于
帮助
法律
-->


#### Violin Plots 101: Visualizing Distribution and Probability Density
[Violin Plots 101: Visualizing Distribution and Probability Density](https://mode.com/blog/violin-plot-examples)  
[Pareto Chart 101: Visualizing the 80-20 Rule](https://mode.com/blog/pareto-chart-101?utm_medium=recommended&utm_source=blog&utm_content=violin_plot)  
Author: JOEL CARRON, DATA SCIENTIST AT MOOE

有时中位数和均值不足以理解数据集。大多数值都集中在中位数附近吗？还是它们聚集在最小值和最大值之间，而中间什么也没有？当您有这样的问题时，分布图就是您的朋友。  
该箱形图是一个老待命可视化的基本分布。比较摘要统计信息（例如范围和四分位数）很方便，但是它不能让您看到数据的变化。对于多峰分布（具有多个峰的分布），这可能会特别受限制。  
但是，不用担心 -这是小提琴图的用处。小提琴图是箱形图和籽粒密度图的混合体，后者显示数据中的峰值。

**The anatomy of a violin plot (小提琴图剖析)**
<img src="/images/2020-04/violin-plots-101-visualizing-distribution-and-probability-density.png" width="57%">
小提琴图具有许多与箱形图相同的摘要统计量：  
--- 白点代表中位数
--- 中间的灰色粗条表示四分位间距
--- 灰色细线代表分布的其余部分，但使用四分位数间距函数的方法确定为“异常值”的点除外。
灰线的每一侧都有一个核密度估计值，以显示数据的分布形状。小提琴图的较宽部分表示人口成员采用给定值的可能性较高；较细的部分表示较低的可能性。
<img src="/images/2020-04/violin-plot-02.png" width="57%">
理论上足够了。让我们看一些例子。我们将使用 Seaborn，这是一个 Python 库，专门用于进行统计可视化。


## 带线性回归最佳拟合线的散点图
Scatter plot with linear regression line of best fit (回归线图)  
如果你想了解两个变量如何相互改变，那么最佳拟合线就是常用的方法。 下图显示了数据中各组之间最佳拟合线的差异。 要禁用分组并仅为整个数据集绘制一条最佳拟合线，请从下面的sns.lmplot() 调用中删除 hue ='cyl' 参数。  
[https://raw.githubusercontent.com/selva86/datasets/master/mpg_ggplot2.csv](https://raw.githubusercontent.com/selva86/datasets/master/mpg_ggplot2.csv)

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Import Data
df = pd.read_csv("./Matplotlib/mpg_ggplot2.csv")
df_select = df.loc[df.cyl.isin([4, 8]), :]

# Plot
sns.set_style("white")
gridobj = sns.lmplot(x="displ", y="hwy", hue="cyl", data=df_select,
                    # height=7, 
                    aspect=1.6, robust=True, palette='tab10',
                    scatter_kws=dict(s=60, linewidths=.7, edgecolors='black'))

# Decorations
gridobj.set(xlim=(0.5, 7.5), ylim=(0, 50))
plt.title("Scatterplot with line of best fit grouped by number of "
        "cylinders", fontsize=14)
plt.tight_layout()
plt.show()
```

<!--
<img src="/images/2020-03/0324_Gallery_regression1a.png">
<img src="/images/2020-03/0324_Gallery_regression1b.png">
-->
{% gp 1-2 %}
<img src="/images/2020-03/0324_Gallery_regress1a.png">
<img src="/images/2020-03/0324_Gallery_regress1b.png">
{% endgp %}

### 针对每列绘制线性回归线
或者，可以在其每列中显示每个组的最佳拟合线。 可以通过在 ``sns.lmplot()`` 中设置 ``col=groupingcolumn`` 参数来实现，如下所示：

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Import Data
df = pd.read_csv("./Matplotlib/mpg_ggplot2.csv")
df_select = df.loc[df.cyl.isin([4, 8]), :]

# Each line in its own column
sns.set_style("white")
gridobj = sns.lmplot(x="displ", y="hwy", data=df_select,
                    robust=True, palette='Set1', col="cyl",
                    scatter_kws=dict(s=60, linewidths=.7, edgecolors='purple'))

# Decorations
gridobj.set(xlim=(0.5, 7.5), ylim=(0, 50))
plt.tight_layout()
plt.show()
```

<!--
<img src="/images/2020-03/0324_Gallery_regression1a.png">
<img src="/images/2020-03/0324_Gallery_regression1b.png">
-->
{% gp 2-1 %}
<img src="/images/2020-03/0324_Gallery_regress2a.png">
<img src="/images/2020-03/0324_Gallery_regress2b.png">
{% endgp %}




# Important

## Statistical plots

### boxplot_color_demo
[statistics example code: boxplot_color_demo.py](https://matplotlib.org/examples/statistics/boxplot_color_demo.html) 
<img src="https://matplotlib.org/_images/boxplot_color_demo.png" width="87%">

```python
import matplotlib.pyplot as plt
import numpy as np

# Random test data
np.random.seed(123)
all_data = [np.random.normal(0, std, 100) for std in range(1, 4)]

fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(9, 4))

# rectangular box plot
bplot1 = axes[0].boxplot(all_data,
                         vert=True,   # vertical box aligmnent
                         patch_artist=True)   # fill with color

# notch shape box plot
bplot2 = axes[1].boxplot(all_data,
                         notch=True,  # notch shape
                         vert=True,   # vertical box aligmnent
                         patch_artist=True)   # fill with color

# fill with colors
colors = ['pink', 'lightblue', 'lightgreen']
for bplot in (bplot1, bplot2):
    for patch, color in zip(bplot['boxes'], colors):
        patch.set_facecolor(color)

# adding horizontal grid lines
for ax in axes:
    ax.yaxis.grid(True)
    ax.set_xticks([y+1 for y in range(len(all_data))], )
    ax.set_xlabel('xlabel')
    ax.set_ylabel('ylabel')

# add x-tick labels
plt.setp(axes, xticks=[y+1 for y in range(len(all_data))],
         xticklabels=['x1', 'x2', 'x3', 'x4'])

plt.show()
```


### boxplot\_demo
[statistics example code: boxplot\_demo.py](https://matplotlib.org/examples/statistics/boxplot_demo.html) 

> 可视化离散变量数据可使用常见的条形图和饼图，可视化数值型变量可使用箱线图、直方图、折线图、面积图、散点图等。先来考虑数值型变量的箱线图绘制。箱线图一般用来展现数据的分布（如上下四分位值、中位数等），同时，也可以用箱线图来反映数据的异常情况。  
> 箱形图又称为盒须图、盒式图或箱线图。是一种用作显示一组数据分散情况资料的统计图。  
>
> 箱线图，又称箱形图（boxplot）或盒式图，不同于一般的折线图、柱状图或饼图等传统图表，只是数据大小、占比、趋势等等的呈现，其包含一些统计学的均值、分位数、极值等等统计量，因此，该图信息量较大，不仅能够分析不同类别数据平均水平差异（需在箱线图中加入均值点），还能揭示数据间离散程度、异常值、分布差异等等。  
> 箱线图一般用来看数据的分布，比如四分位数，异常点等。简单的数据信息也可以用 DataFrame.describe() 进行查看。  
>

[Python可视化 | Seaborn5分钟入门(三)——boxplot和violinplot](https://www.jianshu.com/p/96977b9869ac)  
[Python-matplotlib统计图之箱线图漫谈](https://www.jianshu.com/p/b2f70f867a4a)  
[图文并茂的Python箱型图教程](https://blog.csdn.net/hustqb/article/details/77717026)  
[matplotlib可视化箱线图](https://zhuanlan.zhihu.com/p/38199913)  
[画箱形图 boxplot](https://blog.csdn.net/You_are_my_dream/article/details/53435733)  
[从零开始学Python【3】--matplotlib(箱线图)](https://www.kesci.com/home/project/59f6ec6dc5f3f511952c228e)  
[matplotlib：boxplot箱线图](https://amberwest.github.io/2018/12/12/matplotlib%EF%BC%9Aboxplot%E7%AE%B1%E5%BD%A2%E5%9B%BE/)  

```python
import numpy as np
import matplotlib.pyplot as plt

# fake data
np.random.seed(937)
data = np.random.lognormal(size=(37, 4), mean=1.5, sigma=1.75)
labels = list('ABCD')
fs = 10  # fontsize
```
{% gp 1-2 %}
<img src="https://matplotlib.org/_images/boxplot_demo_00_001.png">
<img src="https://matplotlib.org/_images/boxplot_demo_01_001.png">
{% endgp %}

#### toggle the display of different elements
```python
# demonstrate how to toggle the display of different elements:
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(6, 6), sharey=True)
axes[0, 0].boxplot(data, labels=labels)
axes[0, 0].set_title('Default', fontsize=fs)

axes[0, 1].boxplot(data, labels=labels, showmeans=True)
axes[0, 1].set_title('showmeans=True', fontsize=fs)

axes[0, 2].boxplot(data, labels=labels, showmeans=True, meanline=True)
axes[0, 2].set_title('showmeans=True,\nmeanline=True', fontsize=fs)

axes[1, 0].boxplot(data, labels=labels, showbox=False, showcaps=False)
tufte_title = 'Tufte Style \n(showbox=False,\nshowcaps=False)'
axes[1, 0].set_title(tufte_title, fontsize=fs)

axes[1, 1].boxplot(data, labels=labels, notch=True, bootstrap=10000)
axes[1, 1].set_title('notch=True,\nbootstrap=10000', fontsize=fs)

axes[1, 2].boxplot(data, labels=labels, showfliers=False)
axes[1, 2].set_title('showfliers=False', fontsize=fs)

for ax in axes.flatten():
    ax.set_yscale('log')
    ax.set_yticklabels([])

fig.subplots_adjust(hspace=0.4)
plt.show()
```

#### customize the display different elements
```python
# demonstrate how to customize the display different elements:
boxprops = dict(linestyle='--', linewidth=3, color='darkgoldenrod')
flierprops = dict(marker='o', markerfacecolor='green', markersize=12,
                  linestyle='none')
medianprops = dict(linestyle='-.', linewidth=2.5, color='firebrick')
meanpointprops = dict(marker='D', markeredgecolor='black',
                      markerfacecolor='firebrick')
meanlineprops = dict(linestyle='--', linewidth=2.5, color='purple')

fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(6, 6), sharey=True)
axes[0, 0].boxplot(data, boxprops=boxprops)
axes[0, 0].set_title('Custom boxprops', fontsize=fs)

axes[0, 1].boxplot(data, flierprops=flierprops, medianprops=medianprops)
axes[0, 1].set_title('Custom medianprops\nand flierprops', fontsize=fs)

axes[0, 2].boxplot(data, whis='range')
axes[0, 2].set_title('whis="range"', fontsize=fs)

axes[1, 0].boxplot(data, meanprops=meanpointprops, meanline=False,
                   showmeans=True)
axes[1, 0].set_title('Custom mean\nas point', fontsize=fs)

axes[1, 1].boxplot(data, meanprops=meanlineprops, meanline=True,
                   showmeans=True)
axes[1, 1].set_title('Custom mean\nas line', fontsize=fs)

axes[1, 2].boxplot(data, whis=[15, 85])
axes[1, 2].set_title('whis=[15, 85]\n#percentiles', fontsize=fs)

for ax in axes.flatten():
    ax.set_yscale('log')
    ax.set_yticklabels([])

fig.suptitle("I never said they'd be pretty")
fig.subplots_adjust(hspace=0.4)
plt.show()
```

### boxplot\_vs\_violin\_demo
[statistics example code: boxplot\_vs\_violin\_demo.py](https://matplotlib.org/examples/statistics/boxplot_vs_violin_demo.html) 
<img src="https://matplotlib.org/_images/boxplot_vs_violin_demo.png" width="87%">

```python
import matplotlib.pyplot as plt
import numpy as np

fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(9, 4))

# generate some random test data
all_data = [np.random.normal(0, std, 100) for std in range(6, 10)]

# plot violin plot
axes[0].violinplot(all_data,
                   showmeans=False,
                   showmedians=True)
axes[0].set_title('violin plot')

# plot box plot
axes[1].boxplot(all_data)
axes[1].set_title('box plot')

# adding horizontal grid lines
for ax in axes:
    ax.yaxis.grid(True)
    ax.set_xticks([y+1 for y in range(len(all_data))])
    ax.set_xlabel('xlabel')
    ax.set_ylabel('ylabel')

# add x-tick labels
plt.setp(axes, xticks=[y+1 for y in range(len(all_data))],
         xticklabels=['x1', 'x2', 'x3', 'x4'])
plt.show()
```

### bxp\_demo
[statistics example code: bxp\_demo.py](https://matplotlib.org/examples/statistics/bxp_demo.html)

[关于使用python seaborn库绘制violinplot小提琴图的一些小坑](https://blog.csdn.net/weixin_30537451/article/details/97924074)  
[10分钟python图表绘制 | seaborn入门（三）：Boxplot与Violinplot](https://zhuanlan.zhihu.com/p/25800237)  
[Python可视化 | Seaborn5分钟入门(三)——boxplot和violinplot](https://zhuanlan.zhihu.com/p/34059825)  
[Matplotlib盒图与小提琴图](https://blog.csdn.net/xzy53719/article/details/82803438)  
[十分钟掌握Seaborn，进阶Python数据可视化分析](https://www.python51.com/jc/4144.html)  
[Python数据处理学习笔记 - seaborn统计数据可视化篇](https://blog.mazhangjing.com/2018/03/29/learn_seaborn/#233-%E5%A4%9A%E5%8F%98%E9%87%8F%E5%A4%9A%E5%9B%BE%E5%BD%A2%E6%8B%9F%E5%90%88%E5%8F%A0%E5%8A%A0)  

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.cbook as cbook

# fake data
np.random.seed(937)
data = np.random.lognormal(size=(37, 4), mean=1.5, sigma=1.75)
labels = list('ABCD')

# compute the boxplot stats
stats = cbook.boxplot_stats(data, labels=labels, bootstrap=10000)
# After we've computed the stats, we can go through and change anything.
# Just to prove it, I'll set the median of each set to the median of all
# the data, and double the means
for n in range(len(stats)):
    stats[n]['med'] = np.median(data)
    stats[n]['mean'] *= 2

print(stats[0].keys())

fs = 10  # fontsize
```
{% gp 1-2 %}
<img src="https://matplotlib.org/_images/bxp_demo_00_001.png">
<img src="https://matplotlib.org/_images/bxp_demo_01_001.png">
{% endgp %}

#### toggle the display of different elements
```python
# demonstrate how to toggle the display of different elements:
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(6, 6), sharey=True)
axes[0, 0].bxp(stats)
axes[0, 0].set_title('Default', fontsize=fs)

axes[0, 1].bxp(stats, showmeans=True)
axes[0, 1].set_title('showmeans=True', fontsize=fs)

axes[0, 2].bxp(stats, showmeans=True, meanline=True)
axes[0, 2].set_title('showmeans=True,\nmeanline=True', fontsize=fs)

axes[1, 0].bxp(stats, showbox=False, showcaps=False)
tufte_title = 'Tufte Style\n(showbox=False,\nshowcaps=False)'
axes[1, 0].set_title(tufte_title, fontsize=fs)

axes[1, 1].bxp(stats, shownotches=True)
axes[1, 1].set_title('notch=True', fontsize=fs)

axes[1, 2].bxp(stats, showfliers=False)
axes[1, 2].set_title('showfliers=False', fontsize=fs)

for ax in axes.flatten():
    ax.set_yscale('log')
    ax.set_yticklabels([])

fig.subplots_adjust(hspace=0.4)
plt.show()
```

#### customize the display different elements
```python
# demonstrate how to customize the display different elements:
boxprops = dict(linestyle='--', linewidth=3, color='darkgoldenrod')
flierprops = dict(marker='o', markerfacecolor='green', markersize=12,
                  linestyle='none')
medianprops = dict(linestyle='-.', linewidth=2.5, color='firebrick')
meanpointprops = dict(marker='D', markeredgecolor='black',
                      markerfacecolor='firebrick')
meanlineprops = dict(linestyle='--', linewidth=2.5, color='purple')

fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(6, 6), sharey=True)
axes[0, 0].bxp(stats, boxprops=boxprops)
axes[0, 0].set_title('Custom boxprops', fontsize=fs)

axes[0, 1].bxp(stats, flierprops=flierprops, medianprops=medianprops)
axes[0, 1].set_title('Custom medianprops\nand flierprops', fontsize=fs)

axes[1, 0].bxp(stats, meanprops=meanpointprops, meanline=False,
               showmeans=True)
axes[1, 0].set_title('Custom mean\nas point', fontsize=fs)

axes[1, 1].bxp(stats, meanprops=meanlineprops, meanline=True,
               showmeans=True)
axes[1, 1].set_title('Custom mean\nas line', fontsize=fs)

for ax in axes.flatten():
    ax.set_yscale('log')
    ax.set_yticklabels([])

fig.suptitle("I never said they'd be pretty")
fig.subplots_adjust(hspace=0.4)
plt.show()
```

### customized\_violin\_demo
[statistics example code: customized\_violin\_demo.py](https://matplotlib.org/examples/statistics/customized_violin_demo.html) 
<img src="https://matplotlib.org/_images/customized_violin_demo.png" width="87%">

```python
import matplotlib.pyplot as plt
import numpy as np


def adjacent_values(vals, q1, q3):
    upper_adjacent_value = q3 + (q3 - q1) * 1.5
    upper_adjacent_value = np.clip(upper_adjacent_value, q3, vals[-1])

    lower_adjacent_value = q1 - (q3 - q1) * 1.5
    lower_adjacent_value = np.clip(lower_adjacent_value, vals[0], q1)
    return lower_adjacent_value, upper_adjacent_value


def set_axis_style(ax, labels):
    ax.get_xaxis().set_tick_params(direction='out')
    ax.xaxis.set_ticks_position('bottom')
    ax.set_xticks(np.arange(1, len(labels) + 1))
    ax.set_xticklabels(labels)
    ax.set_xlim(0.25, len(labels) + 0.75)
    ax.set_xlabel('Sample name')


# create test data
np.random.seed(123)
data = [sorted(np.random.normal(0, std, 100)) for std in range(1, 5)]

fig, (ax1, ax2) = plt.subplots(nrows=1, ncols=2, figsize=(9, 4), sharey=True)

ax1.set_title('Default violin plot')
ax1.set_ylabel('Observed values')
ax1.violinplot(data)

ax2.set_title('Customized violin plot')
parts = ax2.violinplot(
        data, showmeans=False, showmedians=False,
        showextrema=False)

for pc in parts['bodies']:
    pc.set_facecolor('#D43F3A')
    pc.set_edgecolor('black')
    pc.set_alpha(1)

quartile1, medians, quartile3 = np.percentile(data, [25, 50, 75], axis=1)
whiskers = np.array([
    adjacent_values(sorted_array, q1, q3)
    for sorted_array, q1, q3 in zip(data, quartile1, quartile3)])
whiskersMin, whiskersMax = whiskers[:, 0], whiskers[:, 1]

inds = np.arange(1, len(medians) + 1)
ax2.scatter(inds, medians, marker='o', color='white', s=30, zorder=3)
ax2.vlines(inds, quartile1, quartile3, color='k', linestyle='-', lw=5)
ax2.vlines(inds, whiskersMin, whiskersMax, color='k', linestyle='-', lw=1)

# set style for the axes
labels = ['A', 'B', 'C', 'D']
for ax in [ax1, ax2]:
    set_axis_style(ax, labels)

plt.subplots_adjust(bottom=0.15, wspace=0.05)
plt.show()
```

### errorbar

**Helpful:**  
[误差条形图中的上限和下限](https://www.matplotlib.org.cn/gallery/statistics/errorbar_limits.html)  
[指定误差线的不同方法](https://www.osgeo.cn/matplotlib/gallery/statistics/errorbar_features.html)  
[Matplotlib学习---用matplotlib画误差线（errorbar）](https://www.cnblogs.com/HuZihu/p/9418903.html)  
[matplotlib可视化番外篇errorbar()--误差棒图](https://www.jianshu.com/p/5973680a1542)  
[Matplotlib学习---用matplotlib画误差线（errorbar）](https://blog.csdn.net/weixin_33787529/article/details/94304997)  
[plt.errorbar()函数解析（最清晰的解释）](https://blog.csdn.net/TeFuirnever/article/details/89847505)  
[matplotlib 误差棒图](https://cloud.tencent.com/developer/article/1486829)  

**Useless:**  
[matplotlib散点图、频次直方图与误差线图](https://zhuanlan.zhihu.com/p/34900932)  
[python误差棒图errorbar()函数实例解析](https://www.jb51.net/article/180092.htm)  
[Matplotlib画图系列(二)误差曲线(errorbar)](https://blog.csdn.net/The_lastest/article/details/79829046)  
[用-matplotlib-绘制误差棒图(Errorbar）](https://blog.csdn.net/CoderPai/article/details/80441300)  

#### errorbar\_demo
[statistics example code: errorbar\_demo.py](https://matplotlib.org/examples/statistics/errorbar_demo.html) 
<img src="https://matplotlib.org/_images/errorbar_demo1.png" width="43%">

```python
import numpy as np
import matplotlib.pyplot as plt

# example data
x = np.arange(0.1, 4, 0.5)
y = np.exp(-x)

fig, ax = plt.subplots()
ax.errorbar(x, y, xerr=0.2, yerr=0.4)
plt.show()
```

#### errorbar\_demo\_features
[statistics example code: errorbar\_demo\_features.py](https://matplotlib.org/examples/statistics/errorbar_demo_features.html) 
<img src="https://matplotlib.org/_images/errorbar_demo_features.png" width="43%">

```python
import numpy as np
import matplotlib.pyplot as plt

# example data
x = np.arange(0.1, 4, 0.5)
y = np.exp(-x)

# example error bar values that vary with x-position
error = 0.1 + 0.2 * x

fig, (ax0, ax1) = plt.subplots(nrows=2, sharex=True)
ax0.errorbar(x, y, yerr=error, fmt='-o')
ax0.set_title('variable, symmetric error')

# error bar values w/ different -/+ errors that
# also vary with the x-position
lower_error = 0.4 * error
upper_error = error
asymmetric_error = [lower_error, upper_error]

ax1.errorbar(x, y, xerr=asymmetric_error, fmt='o')
ax1.set_title('variable, asymmetric error')
ax1.set_yscale('log')
plt.show()
```

#### errorbar\_limits
[statistics example code: errorbar\_limits.py](https://matplotlib.org/examples/statistics/errorbar_limits.html) 
<img src="https://matplotlib.org/_images/errorbar_limits.png" width="43%"><img src="/images/2020-03/0324_Gallery_errorbar3a.png" width="47%">

```python
import numpy as np
import matplotlib.pyplot as plt

# example data
x = np.array([0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0])
y = np.exp(-x)
xerr = 0.1
yerr = 0.2

# lower & upper limits of the error
lolims = np.array([0, 0, 1, 0, 1, 0, 0, 0, 1, 0], dtype=bool)
uplims = np.array([0, 1, 0, 0, 0, 1, 0, 0, 0, 1], dtype=bool)
ls = 'dotted'

fig, ax = plt.subplots(figsize=(7, 4))

# standard error bars
ax.errorbar(x, y, xerr=xerr, yerr=yerr, linestyle=ls,
            label='Line y')

# including upper limits
ax.errorbar(x, y + 0.5, xerr=xerr, yerr=yerr, uplims=uplims,
            linestyle=ls, label='Line y+0.5')

# including lower limits
ax.errorbar(x, y + 1.0, xerr=xerr, yerr=yerr, lolims=lolims,
            linestyle=ls, label='Line y+1.0')

# including upper and lower limits
ax.errorbar(x, y + 1.5, xerr=xerr, yerr=yerr,
            lolims=lolims, uplims=uplims,
            marker='o', markersize=8,
            linestyle=ls, label='Line y+1.5')

# Plot a series with lower and upper limits in both x & y
# constant x-error with varying y-error
xerr = 0.2
yerr = np.zeros(x.shape) + 0.2
yerr[[3, 6]] = 0.3

# mock up some limits by modifying previous data
xlolims = lolims
xuplims = uplims
lolims = np.zeros(x.shape)
uplims = np.zeros(x.shape)
lolims[[6]] = True  # only limited at this index
uplims[[3]] = True  # only limited at this index

# do the plotting
ax.errorbar(x, y + 2.1, xerr=xerr, yerr=yerr,
            xlolims=xlolims, xuplims=xuplims,
            uplims=uplims, lolims=lolims,
            marker='o', markersize=8,
            linestyle='none', label='Line y+2.1')

ax.legend(loc='center right', bbox_to_anchor=(1.14, 1), borderaxespad=0.7)
plt.tight_layout()

# tidy up the figure
ax.set_xlim((0, 5.5))
ax.set_title('Errorbar upper and lower limits')
plt.show()
```

#### errorbars\_and\_boxes
[statistics example code: errorbars\_and\_boxes.py](https://matplotlib.org/examples/statistics/errorbars_and_boxes.html) 
<img src="https://matplotlib.org/_images/errorbars_and_boxes.png" width="43%">

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.collections import PatchCollection
from matplotlib.patches import Rectangle

# Number of data points
n = 5
# Dummy data
np.random.seed(10)
x = np.arange(0, n, 1)
y = np.random.rand(n) * 5.
# Dummy errors (above and below)
xerr = np.random.rand(2, n) + 0.1
yerr = np.random.rand(2, n) + 0.2


def make_error_boxes(ax, xdata, ydata, xerror, yerror, facecolor='r',
                     edgecolor='None', alpha=0.5):
    # Create list for all the error patches
    errorboxes = []

    # Loop over data points; create box from errors at each point
    for x, y, xe, ye in zip(xdata, ydata, xerror.T, yerror.T):
        rect = Rectangle((x - xe[0], y - ye[0]), xe.sum(), ye.sum())
        errorboxes.append(rect)

    # Create patch collection with specified colour/alpha
    pc = PatchCollection(errorboxes, facecolor=facecolor, alpha=alpha,
                         edgecolor=edgecolor)
    # Add collection to axes
    ax.add_collection(pc)

    # Plot errorbars
    artists = ax.errorbar(xdata, ydata, xerr=xerror, yerr=yerror,
                          fmt='None', ecolor='k')
    return artists


# Create figure and axes
fig, ax = plt.subplots(1)
# Call function to create error boxes
_ = make_error_boxes(ax, x, y, xerr, yerr)
plt.show()
```

### histogram

[matplotlib.pyplot中的hist函数简单使用](https://blog.csdn.net/u014525494/article/details/80157402)  
[matplotlib可视化直方图](https://zhuanlan.zhihu.com/p/37959111)  

直方图 (histogram) 是为了表明数据分布情况。通俗地说就是哪一块数据所占比例或者出现次数较高，哪一块出现概率低。如下图，横轴是数据，纵轴是出现的次数 (也就是频数)。从这个图看 4.1-4.3 这块数据出现次数最高。可以看出直方图能够反映数据的分布状况。  
<img src="/images/2020-04/2018050116394561.png" width="47%"><!--47%-->
<!--
<img src="https://img-blog.csdn.net/2018050116394561?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQ1MjU0OTQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="47%">
-->

#### histogram\_demo\_cumulative
[statistics example code: histogram\_demo\_cumulative.py](https://matplotlib.org/examples/statistics/histogram_demo_cumulative.html) 
<img src="https://matplotlib.org/_images/histogram_demo_cumulative.png" width="63%"><!--43%-->

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import mlab

np.random.seed(0)

mu = 200
sigma = 25
n_bins = 50
x = np.random.normal(mu, sigma, size=100)

fig, ax = plt.subplots(figsize=(8, 4))

# plot the cumulative histogram
n, bins, patches = ax.hist(x, n_bins, normed=1, histtype='step',
                           cumulative=True, label='Empirical',
                           )  ##BUG! color='g', alpha=0.15)

# Add a line showing the expected distribution.
y = mlab.normpdf(bins, mu, sigma).cumsum()
y /= y[-1]

ax.plot(bins, y, 'k--', linewidth=1.5, label='Theoretical')

# Overlay a reversed cumulative histogram.
ax.hist(x, bins=bins, normed=1, histtype='step', cumulative=-1,
        label='Reversed emp.',
        )  ##BUG! color='r', alpha=0.05)

# tidy up the figure
ax.grid(True)
ax.legend(loc='right')
ax.set_title('Cumulative step histograms')
ax.set_xlabel('Annual rainfall (mm)')
ax.set_ylabel('Likelihood of occurrence')

plt.show()
```

#### histogram\_demo\_features
[statistics example code: histogram\_demo\_features.py](https://matplotlib.org/examples/statistics/histogram_demo_features.html) 
<img src="https://matplotlib.org/_images/histogram_demo_features2.png" width="43%">

```python
import numpy as np
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt

np.random.seed(0)

# example data
mu = 100  # mean of distribution
sigma = 15  # standard deviation of distribution
x = mu + sigma * np.random.randn(437)

num_bins = 50

fig, ax = plt.subplots()

# the histogram of the data
n, bins, patches = ax.hist(x, num_bins, normed=1)

# add a 'best fit' line
y = mlab.normpdf(bins, mu, sigma)
ax.plot(bins, y, '--')
ax.set_xlabel('Smarts')
ax.set_ylabel('Probability density')
ax.set_title(r'Histogram of IQ: $\mu=100$, $\sigma=15$')

# Tweak spacing to prevent clipping of ylabel
fig.tight_layout()
plt.show()
```

#### histogram\_demo\_histtypes
[statistics example code: histogram\_demo\_histtypes.py](https://matplotlib.org/examples/statistics/histogram_demo_histtypes.html) 
<img src="https://matplotlib.org/_images/histogram_demo_histtypes.png" width="87%">

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)

mu = 200
sigma = 25
x = np.random.normal(mu, sigma, size=100)

fig, (ax0, ax1) = plt.subplots(ncols=2, figsize=(8, 4))

ax0.hist(x, 20, normed=1, histtype='stepfilled', facecolor='g', alpha=0.75)
ax0.set_title('stepfilled')

# Create a histogram by providing the bin edges (unequally spaced).
bins = [100, 150, 180, 195, 205, 220, 250, 300]
ax1.hist(x, bins, normed=1, histtype='bar', rwidth=0.8)
ax1.set_title('unequal bins')

fig.tight_layout()
plt.show()
```

#### histogram\_demo\_multihist
[statistics example code: histogram\_demo\_multihist.py](https://matplotlib.org/examples/statistics/histogram_demo_multihist.html) 
<img src="https://matplotlib.org/_images/histogram_demo_multihist.png" width="47%">

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)

n_bins = 10
x = np.random.randn(1000, 3)

fig, axes = plt.subplots(nrows=2, ncols=2)
ax0, ax1, ax2, ax3 = axes.flatten()

colors = ['red', 'tan', 'lime']
ax0.hist(x, n_bins, normed=1, histtype='bar', color=colors, label=colors)
ax0.legend(prop={'size': 10})
ax0.set_title('bars with legend')

ax1.hist(x, n_bins, normed=1, histtype='bar', stacked=True)
ax1.set_title('stacked bar')

ax2.hist(x, n_bins, histtype='step', stacked=True, fill=False)
ax2.set_title('stack step (unfilled)')

# Make a multiple-histogram of data-sets with different length.
x_multi = [np.random.randn(n) for n in [10000, 5000, 2000]]
ax3.hist(x_multi, n_bins, histtype='bar')
ax3.set_title('different sample sizes')

fig.tight_layout()
plt.show()
```

#### multiple\_histograms\_side\_by\_side
[statistics example code: multiple\_histograms\_side\_by\_side.py](https://matplotlib.org/examples/statistics/multiple_histograms_side_by_side.html) 
<img src="https://matplotlib.org/_images/multiple_histograms_side_by_side.png" width="43%">

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)
number_of_bins = 20

# An example of three data sets to compare
number_of_data_points = 387
labels = ["A", "B", "C"]
data_sets = [np.random.normal(0, 1, number_of_data_points),
             np.random.normal(6, 1, number_of_data_points),
             np.random.normal(-3, 1, number_of_data_points)]

# Computed quantities to aid plotting
hist_range = (np.min(data_sets), np.max(data_sets))
binned_data_sets = [
    np.histogram(d, range=hist_range, bins=number_of_bins)[0]
    for d in data_sets
]
binned_maximums = np.max(binned_data_sets, axis=1)
x_locations = np.arange(0, sum(binned_maximums), np.max(binned_maximums))

# The bin_edges are the same for all of the histograms
bin_edges = np.linspace(hist_range[0], hist_range[1], number_of_bins + 1)
centers = 0.5 * (bin_edges + np.roll(bin_edges, 1))[:-1]
heights = np.diff(bin_edges)

# Cycle through and plot each histogram
fig, ax = plt.subplots()
for x_loc, binned_data in zip(x_locations, binned_data_sets):
    lefts = x_loc - 0.5 * binned_data
    ax.barh(centers, binned_data, height=heights, left=lefts)

ax.set_xticks(x_locations)
ax.set_xticklabels(labels)

ax.set_ylabel("Data values")
ax.set_xlabel("Data sets")

plt.show()
```

#### violinplot\_demo
[statistics example code: violinplot\_demo.py](https://matplotlib.org/examples/statistics/violinplot_demo.html) 
<img src="https://matplotlib.org/_images/violinplot_demo.png" width="47%">

```python
import random
import numpy as np
import matplotlib.pyplot as plt

# fake data
fs = 10  # fontsize
pos = [1, 2, 4, 5, 7, 8]
data = [np.random.normal(0, std, size=100) for std in pos]

fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(6, 6))

axes[0, 0].violinplot(data, pos, points=20, widths=0.3,
                      showmeans=True, showextrema=True, showmedians=True)
axes[0, 0].set_title('Custom violinplot 1', fontsize=fs)

axes[0, 1].violinplot(data, pos, points=40, widths=0.5,
                      showmeans=True, showextrema=True, showmedians=True,
                      bw_method='silverman')
axes[0, 1].set_title('Custom violinplot 2', fontsize=fs)

axes[0, 2].violinplot(data, pos, points=60, widths=0.7, showmeans=True,
                      showextrema=True, showmedians=True, bw_method=0.5)
axes[0, 2].set_title('Custom violinplot 3', fontsize=fs)

axes[1, 0].violinplot(data, pos, points=80, vert=False, widths=0.7,
                      showmeans=True, showextrema=True, showmedians=True)
axes[1, 0].set_title('Custom violinplot 4', fontsize=fs)

axes[1, 1].violinplot(data, pos, points=100, vert=False, widths=0.9,
                      showmeans=True, showextrema=True, showmedians=True,
                      bw_method='silverman')
axes[1, 1].set_title('Custom violinplot 5', fontsize=fs)

axes[1, 2].violinplot(data, pos, points=200, vert=False, widths=1.1,
                      showmeans=True, showextrema=True, showmedians=True,
                      bw_method=0.5)
axes[1, 2].set_title('Custom violinplot 6', fontsize=fs)

for ax in axes.flatten():
    ax.set_yticklabels([])

fig.suptitle("Violin Plotting Examples")
fig.subplots_adjust(hspace=0.4)
plt.show()
```

## Images, contours, and fields

- \#\#\# image\_demo
- \#\#\# image\_demo\_clip\_path
- \#\#\# streamplot\_demo\_features
- \#\#\# streamplot\_demo\_features
- \#\#\# streamplot\_demo\_masking
- \#\#\# streamplot\_demo\_start\_points

### contourf\_log
[images\_contours\_and\_fields example code: contourf\_log.py](https://matplotlib.org/examples/images_contours_and_fields/contourf_log.html) 
<img src="https://matplotlib.org/_images/contourf_log.png" width="47%">

```python
'''Demonstrate use of a log color scale in contourf
'''
import matplotlib.pyplot as plt
import numpy as np
from numpy import ma
from matplotlib import colors, ticker, cm
from matplotlib.mlab import bivariate_normal

N = 100
x = np.linspace(-3.0, 3.0, N)
y = np.linspace(-2.0, 2.0, N)

X, Y = np.meshgrid(x, y)

# A low hump with a spike coming out of the top right.
# Needs to have z/colour axis on a log scale so we see both hump and spike.
# linear scale only shows the spike.
z = (bivariate_normal(X, Y, 0.1, 0.2, 1.0, 1.0)
     + 0.1 * bivariate_normal(X, Y, 1.0, 1.0, 0.0, 0.0))

# Put in some negative values (lower left corner) to cause trouble with logs:
z[:5, :5] = -1

# The following is not strictly essential, but it will eliminate
# a warning.  Comment it out to see the warning.
z = ma.masked_where(z <= 0, z)


# Automatic selection of levels works; setting the
# log locator tells contourf to use a log scale:
fig, ax = plt.subplots()
cs = ax.contourf(X, Y, z, locator=ticker.LogLocator(), cmap=cm.PuBu_r)

# Alternatively, you can manually set the levels
# and the norm:
#lev_exp = np.arange(np.floor(np.log10(z.min())-1),
#                    np.ceil(np.log10(z.max())+1))
#levs = np.power(10, lev_exp)
#cs = P.contourf(X, Y, z, levs, norm=colors.LogNorm())

# The 'extend' kwarg does not work yet with a log scale.

cbar = fig.colorbar(cs)

plt.show()
```

### interpolation\_methods
[images\_contours\_and\_fields example code: interpolation\_methods.py](https://matplotlib.org/examples/images_contours_and_fields/interpolation_methods.html) 
<img src="https://matplotlib.org/_images/interpolation_methods.png" width="100%">

```python
'''
Show all different interpolation methods for imshow
'''

import matplotlib.pyplot as plt
import numpy as np

# from the docs:

# If interpolation is None, default to rc image.interpolation. See also
# the filternorm and filterrad parameters. If interpolation is 'none', then
# no interpolation is performed on the Agg, ps and pdf backends. Other
# backends will fall back to 'nearest'.
#
# http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.imshow

methods = [None, 'none', 'nearest', 'bilinear', 'bicubic', 'spline16',
           'spline36', 'hanning', 'hamming', 'hermite', 'kaiser', 'quadric',
           'catrom', 'gaussian', 'bessel', 'mitchell', 'sinc', 'lanczos']

np.random.seed(0)
grid = np.random.rand(4, 4)

fig, axes = plt.subplots(3, 6, figsize=(12, 6),
                         subplot_kw={'xticks': [], 'yticks': []})

fig.subplots_adjust(hspace=0.3, wspace=0.05)

for ax, interp_method in zip(axes.flat, methods):
    ax.imshow(grid, interpolation=interp_method, cmap='viridis')
    ax.set_title(interp_method)

plt.show()
```

### pcolormesh\_levels
[images\_contours\_and\_fields\ example\ code: pcolormesh\_levels.py](https://matplotlib.org/examples/images_contours_and_fields/pcolormesh_levels.html) 
<img src="https://matplotlib.org/_images/pcolormesh_levels.png" width="47%">

```python
"""
Shows how to combine Normalization and Colormap instances to draw
"levels" in pcolor, pcolormesh and imshow type plots in a similar
way to the levels keyword argument to contour/contourf.

"""

import matplotlib.pyplot as plt
from matplotlib.colors import BoundaryNorm
from matplotlib.ticker import MaxNLocator
import numpy as np


# make these smaller to increase the resolution
dx, dy = 0.05, 0.05

# generate 2 2d grids for the x & y bounds
y, x = np.mgrid[slice(1, 5 + dy, dy),
                slice(1, 5 + dx, dx)]

z = np.sin(x)**10 + np.cos(10 + y*x) * np.cos(x)

# x and y are bounds, so z should be the value *inside* those bounds.
# Therefore, remove the last value from the z array.
z = z[:-1, :-1]
levels = MaxNLocator(nbins=15).tick_values(z.min(), z.max())


# pick the desired colormap, sensible levels, and define a normalization
# instance which takes data values and translates those into levels.
cmap = plt.get_cmap('PiYG')
norm = BoundaryNorm(levels, ncolors=cmap.N, clip=True)

fig, (ax0, ax1) = plt.subplots(nrows=2)

im = ax0.pcolormesh(x, y, z, cmap=cmap, norm=norm)
fig.colorbar(im, ax=ax0)
ax0.set_title('pcolormesh with levels')


# contours are *point* based plots, so convert our bound into point
# centers
cf = ax1.contourf(x[:-1, :-1] + dx/2.,
                  y[:-1, :-1] + dy/2., z, levels=levels,
                  cmap=cmap)
fig.colorbar(cf, ax=ax1)
ax1.set_title('contourf with levels')

# adjust spacing between subplots so `ax1` title and `ax0` tick labels
# don't overlap
fig.tight_layout()

plt.show()
```

## Pie and polar charts

**Helpful:**  
[【Python】Matplotlib画图（九）——饼图](https://blog.csdn.net/roguesir/article/details/78178365)  
[python 画图--饼图](https://blog.csdn.net/jenyzhang/article/details/52047999)  
[Python中使用matplotlib画饼图详解](https://blog.csdn.net/u012111465/article/details/72797032)  

**Nearly Useless:**  
[matplotlib命令与格式：图例legend语法及设置](https://blog.csdn.net/helunqu2017/article/details/78641290)  
[Seaborn为什么要绘制两个图例，我如何删除一个并修复另一个图例？](https://stackoom.com/question/3sXFu/Seaborn%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%BB%98%E5%88%B6%E4%B8%A4%E4%B8%AA%E5%9B%BE%E4%BE%8B-%E6%88%91%E5%A6%82%E4%BD%95%E5%88%A0%E9%99%A4%E4%B8%80%E4%B8%AA%E5%B9%B6%E4%BF%AE%E5%A4%8D%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%9B%BE%E4%BE%8B)  
[关于python：如何将图例放出情节](https://www.codenong.com/4700614/)  

### pie\_demo\_features
[pie\_and\_polar\_charts example code: pie\_demo\_features.py](https://matplotlib.org/examples/pie_and_polar_charts/pie_demo_features.html)
<img src="https://matplotlib.org/_images/pie_demo_features1.png" width="47%">

```python
import matplotlib.pyplot as plt

# Pie chart, where the slices will be ordered and plotted counter-clockwise:
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10]
explode = (0, 0.1, 0, 0)  # only "explode" the 2nd slice (i.e. 'Hogs')

fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.

plt.show()
```

### polar\_bar\_demo
[pie\_and\_polar\_charts example code: polar\_bar\_demo.py](https://matplotlib.org/examples/pie_and_polar_charts/polar_bar_demo.html)
<img src="https://matplotlib.org/_images/polar_bar_demo.png" width="47%">

```python
"""
=======================
Pie chart on polar axis
=======================
Demo of bar plot on a polar axis.
"""
import numpy as np
import matplotlib.pyplot as plt

# Compute pie slices
N = 20
theta = np.linspace(0.0, 2 * np.pi, N, endpoint=False)
radii = 10 * np.random.rand(N)
width = np.pi / 4 * np.random.rand(N)

ax = plt.subplot(111, projection='polar')
bars = ax.bar(theta, radii, width=width, bottom=0.0)

# Use custom colors and opacity
for r, bar in zip(radii, bars):
    bar.set_facecolor(plt.cm.viridis(r / 10.))
    bar.set_alpha(0.5)

plt.show()
```

### polar\_scatter\_demo
[pie\_and\_polar\_charts example code: polar\_scatter\_demo.py](https://matplotlib.org/examples/pie_and_polar_charts/polar_scatter_demo.html) 
<img src="https://matplotlib.org/_images/polar_scatter_demo.png" width="47%">

```python
"""
==========================
Scatter plot on polar axis
==========================
Demo of scatter plot on a polar axis.
Size increases radially in this example and color increases with angle
(just to verify the symbols are being scattered correctly).
"""
import numpy as np
import matplotlib.pyplot as plt

# Compute areas and colors
N = 150
r = 2 * np.random.rand(N)
theta = 2 * np.pi * np.random.rand(N)
area = 200 * r**2
colors = theta

ax = plt.subplot(111, projection='polar')
c = ax.scatter(theta, r, c=colors, s=area, cmap='hsv', alpha=0.75)

plt.show()
```

# Tricks

## Lines, bars, and markers
## Shapes and collections
## Color

## Text, labels, and annotations

## Ticks and spines

### spines\_demo\_dropped
[ticks\_and\_spines example code: spines\_demo\_dropped.py](https://matplotlib.org/examples/ticks_and_spines/spines_demo_dropped.html) 
<img src="https://matplotlib.org/_images/spines_demo_dropped.png" width="47%">

```python
"""
==============
Dropped spines
==============
Demo of spines offset from the axes (a.k.a. "dropped spines").
"""
import numpy as np
import matplotlib.pyplot as plt
fig, ax = plt.subplots()

image = np.random.uniform(size=(10, 10))
ax.imshow(image, cmap=plt.cm.gray, interpolation='nearest')
ax.set_title('dropped spines')

# Move left and bottom spines outward by 10 points
ax.spines['left'].set_position(('outward', 10))
ax.spines['bottom'].set_position(('outward', 10))

# Hide the right and top spines
ax.spines['right'].set_visible(False)
ax.spines['top'].set_visible(False)

# Only show ticks on the left and bottom spines
ax.yaxis.set_ticks_position('left')
ax.xaxis.set_ticks_position('bottom')

plt.show()
```

### tick-formatters
[ticks\_and\_spines example code: tick-formatters.py](https://matplotlib.org/examples/ticks_and_spines/tick-formatters.html) 
<img src="https://matplotlib.org/_images/tick-formatters.png" width="67%">

```python
"""
===============
Tick formatters
===============

Show the different tick formatters.
"""

import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker


# Setup a plot such that only the bottom spine is shown
def setup(ax):
    ax.spines['right'].set_color('none')
    ax.spines['left'].set_color('none')
    ax.yaxis.set_major_locator(ticker.NullLocator())
    ax.spines['top'].set_color('none')
    ax.xaxis.set_ticks_position('bottom')
    ax.tick_params(which='major', width=1.00, length=5)
    ax.tick_params(which='minor', width=0.75, length=2.5, labelsize=10)
    ax.set_xlim(0, 5)
    ax.set_ylim(0, 1)
    ax.patch.set_alpha(0.0)


plt.figure(figsize=(8, 5))
n = 6

# Null formatter
ax = plt.subplot(n, 1, 1)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(1.00))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.25))
ax.xaxis.set_major_formatter(ticker.NullFormatter())
ax.xaxis.set_minor_formatter(ticker.NullFormatter())
ax.text(0.0, 0.1, "NullFormatter()", fontsize=16, transform=ax.transAxes)

# Fixed formatter
ax = plt.subplot(n, 1, 2)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(1.0))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.25))
majors = ["", "0", "1", "2", "3", "4", "5"]
ax.xaxis.set_major_formatter(ticker.FixedFormatter(majors))
minors = [""] + ["%.2f" % (x-int(x)) if (x-int(x))
                 else "" for x in np.arange(0, 5, 0.25)]
ax.xaxis.set_minor_formatter(ticker.FixedFormatter(minors))
ax.text(0.0, 0.1, "FixedFormatter(['', '0', '1', ...])",
        fontsize=15, transform=ax.transAxes)


# Func formatter
def major_formatter(x, pos):
    return "[%.2f]" % x


ax = plt.subplot(n, 1, 3)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(1.00))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.25))
ax.xaxis.set_major_formatter(ticker.FuncFormatter(major_formatter))
ax.text(0.0, 0.1, 'FuncFormatter(lambda x, pos: "[%.2f]" % x)',
        fontsize=15, transform=ax.transAxes)


# FormatStr formatter
ax = plt.subplot(n, 1, 4)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(1.00))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.25))
ax.xaxis.set_major_formatter(ticker.FormatStrFormatter(">%d<"))
ax.text(0.0, 0.1, "FormatStrFormatter('>%d<')",
        fontsize=15, transform=ax.transAxes)

# Scalar formatter
ax = plt.subplot(n, 1, 5)
setup(ax)
ax.xaxis.set_major_locator(ticker.AutoLocator())
ax.xaxis.set_minor_locator(ticker.AutoMinorLocator())
ax.xaxis.set_major_formatter(ticker.ScalarFormatter(useMathText=True))
ax.text(0.0, 0.1, "ScalarFormatter()", fontsize=15, transform=ax.transAxes)

# StrMethod formatter
ax = plt.subplot(n, 1, 6)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(1.00))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.25))
ax.xaxis.set_major_formatter(ticker.StrMethodFormatter("{x}"))
ax.text(0.0, 0.1, "StrMethodFormatter('{x}')",
        fontsize=15, transform=ax.transAxes)

# Push the top of the top axes outside the figure because we only show the
# bottom spine.
plt.subplots_adjust(left=0.05, right=0.95, bottom=0.05, top=1.05)

plt.show()
```

### tick-locators
[ticks\_and\_spines example code: tick-locators.py](https://matplotlib.org/examples/ticks_and_spines/tick-locators.html) 
<img src="https://matplotlib.org/_images/tick-locators.png" width="67%">

```python
"""
=============
Tick locators
=============

Show the different tick locators.
"""

import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker


# Setup a plot such that only the bottom spine is shown
def setup(ax):
    ax.spines['right'].set_color('none')
    ax.spines['left'].set_color('none')
    ax.yaxis.set_major_locator(ticker.NullLocator())
    ax.spines['top'].set_color('none')
    ax.xaxis.set_ticks_position('bottom')
    ax.tick_params(which='major', width=1.00)
    ax.tick_params(which='major', length=5)
    ax.tick_params(which='minor', width=0.75)
    ax.tick_params(which='minor', length=2.5)
    ax.set_xlim(0, 5)
    ax.set_ylim(0, 1)
    ax.patch.set_alpha(0.0)


plt.figure(figsize=(8, 6))
n = 8

# Null Locator
ax = plt.subplot(n, 1, 1)
setup(ax)
ax.xaxis.set_major_locator(ticker.NullLocator())
ax.xaxis.set_minor_locator(ticker.NullLocator())
ax.text(0.0, 0.1, "NullLocator()", fontsize=14, transform=ax.transAxes)

# Multiple Locator
ax = plt.subplot(n, 1, 2)
setup(ax)
ax.xaxis.set_major_locator(ticker.MultipleLocator(0.5))
ax.xaxis.set_minor_locator(ticker.MultipleLocator(0.1))
ax.text(0.0, 0.1, "MultipleLocator(0.5)", fontsize=14,
        transform=ax.transAxes)

# Fixed Locator
ax = plt.subplot(n, 1, 3)
setup(ax)
majors = [0, 1, 5]
ax.xaxis.set_major_locator(ticker.FixedLocator(majors))
minors = np.linspace(0, 1, 11)[1:-1]
ax.xaxis.set_minor_locator(ticker.FixedLocator(minors))
ax.text(0.0, 0.1, "FixedLocator([0, 1, 5])", fontsize=14,
        transform=ax.transAxes)

# Linear Locator
ax = plt.subplot(n, 1, 4)
setup(ax)
ax.xaxis.set_major_locator(ticker.LinearLocator(3))
ax.xaxis.set_minor_locator(ticker.LinearLocator(31))
ax.text(0.0, 0.1, "LinearLocator(numticks=3)",
        fontsize=14, transform=ax.transAxes)

# Index Locator
ax = plt.subplot(n, 1, 5)
setup(ax)
ax.plot(range(0, 5), [0]*5, color='White')
ax.xaxis.set_major_locator(ticker.IndexLocator(base=.5, offset=.25))
ax.text(0.0, 0.1, "IndexLocator(base=0.5, offset=0.25)",
        fontsize=14, transform=ax.transAxes)

# Auto Locator
ax = plt.subplot(n, 1, 6)
setup(ax)
ax.xaxis.set_major_locator(ticker.AutoLocator())
ax.xaxis.set_minor_locator(ticker.AutoMinorLocator())
ax.text(0.0, 0.1, "AutoLocator()", fontsize=14, transform=ax.transAxes)

# MaxN Locator
ax = plt.subplot(n, 1, 7)
setup(ax)
ax.xaxis.set_major_locator(ticker.MaxNLocator(4))
ax.xaxis.set_minor_locator(ticker.MaxNLocator(40))
ax.text(0.0, 0.1, "MaxNLocator(n=4)", fontsize=14, transform=ax.transAxes)

# Log Locator
ax = plt.subplot(n, 1, 8)
setup(ax)
ax.set_xlim(10**3, 10**10)
ax.set_xscale('log')
ax.xaxis.set_major_locator(ticker.LogLocator(base=10.0, numticks=15))
ax.text(0.0, 0.1, "LogLocator(base=10, numticks=15)",
        fontsize=15, transform=ax.transAxes)

# Push the top of the top axes outside the figure because we only show the
# bottom spine.
plt.subplots_adjust(left=0.05, right=0.95, bottom=0.05, top=1.05)

plt.show()
```

## Axis scales
## Subplots, axes, and figures

## Style sheets

### plot\_bmh
[style\_sheets example code: plot\_bmh.py](https://matplotlib.org/examples/style_sheets/plot_bmh.html) 
<img src="https://matplotlib.org/_images/plot_bmh.png" width="47%">

```python
"""
========================================
Bayesian Methods for Hackers style sheet
========================================

This example demonstrates the style used in the Bayesian Methods for Hackers
[1]_ online book.

.. [1] http://camdavidsonpilon.github.io/Probabilistic-Programming-and-Bayesian-Methods-for-Hackers/

"""
from numpy.random import beta
import matplotlib.pyplot as plt


plt.style.use('bmh')


def plot_beta_hist(ax, a, b):
    ax.hist(beta(a, b, size=10000), histtype="stepfilled",
            bins=25, alpha=0.8, normed=True)


fig, ax = plt.subplots()
plot_beta_hist(ax, 10, 10)
plot_beta_hist(ax, 4, 12)
plot_beta_hist(ax, 50, 12)
plot_beta_hist(ax, 6, 55)
ax.set_title("'bmh' style sheet")

plt.show()
```

### plot\_ggplot
[style\_sheets example code: plot\_ggplot.py](https://matplotlib.org/examples/style_sheets/plot_ggplot.html) 
<img src="https://matplotlib.org/_images/plot_ggplot.png" width="47%">

```python
"""
==================
ggplot style sheet
==================

This example demonstrates the "ggplot" style, which adjusts the style to
emulate ggplot_ (a popular plotting package for R_).

These settings were shamelessly stolen from [1]_ (with permission).

.. [1] http://www.huyng.com/posts/sane-color-scheme-for-matplotlib/

.. _ggplot: http://ggplot2.org/
.. _R: https://www.r-project.org/

"""
import numpy as np
import matplotlib.pyplot as plt

plt.style.use('ggplot')

fig, axes = plt.subplots(ncols=2, nrows=2)
ax1, ax2, ax3, ax4 = axes.ravel()

# scatter plot (Note: `plt.scatter` doesn't use default colors)
x, y = np.random.normal(size=(2, 200))
ax1.plot(x, y, 'o')

# sinusoidal lines with colors from default color cycle
L = 2*np.pi
x = np.linspace(0, L)
ncolors = len(plt.rcParams['axes.prop_cycle'])
shift = np.linspace(0, L, ncolors, endpoint=False)
for s in shift:
    ax2.plot(x, np.sin(x + s), '-')
ax2.margins(0)

# bar graphs
x = np.arange(5)
y1, y2 = np.random.randint(1, 25, size=(2, 5))
width = 0.25
ax3.bar(x, y1, width)
ax3.bar(x + width, y2, width,
        color=list(plt.rcParams['axes.prop_cycle'])[2]['color'])
ax3.set_xticks(x + width)
ax3.set_xticklabels(['a', 'b', 'c', 'd', 'e'])

# circles with colors from default color cycle
for i, color in enumerate(plt.rcParams['axes.prop_cycle']):
    xy = np.random.normal(size=2)
    ax4.add_patch(plt.Circle(xy, radius=0.3, color=color['color']))
ax4.axis('equal')
ax4.margins(0)

plt.show()
```

### plot\_grayscale
[style\_sheets example code: plot\_grayscale.py](https://matplotlib.org/examples/style_sheets/plot_grayscale.html) 
<img src="https://matplotlib.org/_images/plot_grayscale.png" width="47%">

```python
"""
=====================
Grayscale style sheet
=====================

This example demonstrates the "grayscale" style sheet, which changes all colors
that are defined as rc parameters to grayscale. Note, however, that not all
plot elements default to colors defined by an rc parameter.

"""
import numpy as np
import matplotlib.pyplot as plt


def color_cycle_example(ax):
    L = 6
    x = np.linspace(0, L)
    ncolors = len(plt.rcParams['axes.prop_cycle'])
    shift = np.linspace(0, L, ncolors, endpoint=False)
    for s in shift:
        ax.plot(x, np.sin(x + s), 'o-')


def image_and_patch_example(ax):
    ax.imshow(np.random.random(size=(20, 20)), interpolation='none')
    c = plt.Circle((5, 5), radius=5, label='patch')
    ax.add_patch(c)


plt.style.use('grayscale')

fig, (ax1, ax2) = plt.subplots(ncols=2)
fig.suptitle("'grayscale' style sheet")

color_cycle_example(ax1)
image_and_patch_example(ax2)

plt.show()
```

{% gp 1-2 %}
<img src="/images/2020-03/0324_Gallery_grayscale2a.png">
<img src="/images/2020-03/0324_Gallery_grayscale2b.png">
{% endgp %}

# 3D Plots

## mplot3d toolkit
## axes\_grid toolkit


# FYI (For your information)

## Specialty plots
## Miscellaneous examples

## pylab examples

### animation\_demo
[pylab\_examples example code: animation\_demo.py](https://matplotlib.org/examples/pylab_examples/animation_demo.html)
<img src="https://matplotlib.org/_images/animation_demo.png" width="47%">

```python
"""
Pyplot animation example.

The method shown here is only for very simple, low-performance
use.  For more demanding applications, look at the animation
module and the examples that use it.
"""

import matplotlib.pyplot as plt
import numpy as np

x = np.arange(6)
y = np.arange(5)
z = x * y[:, np.newaxis]

for i in range(5):
    if i == 0:
        p = plt.imshow(z)
        fig = plt.gcf()
        plt.clim()   # clamp the color limits
        plt.title("Boring slide show")
    else:
        z = z + 2
        p.set_data(z)

    print("step", i)
    plt.pause(0.5)
```
### animation\_demo2
[pylab\_examples example code: annotation\_demo2.py](https://matplotlib.org/examples/pylab_examples/annotation_demo2.html)
{% gp 1-2 %}
<img src="https://matplotlib.org/_images/annotation_demo2_00.png">
<img src="https://matplotlib.org/_images/annotation_demo2_01.png">
{% endgp %}

```python
import matplotlib.pyplot as plt
from matplotlib.patches import Ellipse
import numpy as np


fig = plt.figure(1, figsize=(8, 5))
ax = fig.add_subplot(111, autoscale_on=False, xlim=(-1, 5), ylim=(-4, 3))

t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2*np.pi*t)
line, = ax.plot(t, s, lw=3)

ax.annotate('straight',
            xy=(0, 1), xycoords='data',
            xytext=(-50, 30), textcoords='offset points',
            arrowprops=dict(arrowstyle="->"))

ax.annotate('arc3,\nrad 0.2',
            xy=(0.5, -1), xycoords='data',
            xytext=(-80, -60), textcoords='offset points',
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="arc3,rad=.2"))

ax.annotate('arc,\nangle 50',
            xy=(1., 1), xycoords='data',
            xytext=(-90, 50), textcoords='offset points',
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="arc,angleA=0,armA=50,rad=10"))

ax.annotate('arc,\narms',
            xy=(1.5, -1), xycoords='data',
            xytext=(-80, -60), textcoords='offset points',
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="arc,angleA=0,armA=40,angleB=-90,armB=30,rad=7"))

ax.annotate('angle,\nangle 90',
            xy=(2., 1), xycoords='data',
            xytext=(-70, 30), textcoords='offset points',
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="angle,angleA=0,angleB=90,rad=10"))

ax.annotate('angle3,\nangle -90',
            xy=(2.5, -1), xycoords='data',
            xytext=(-80, -60), textcoords='offset points',
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="angle3,angleA=0,angleB=-90"))

ax.annotate('angle,\nround',
            xy=(3., 1), xycoords='data',
            xytext=(-60, 30), textcoords='offset points',
            bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="angle,angleA=0,angleB=90,rad=10"))

ax.annotate('angle,\nround4',
            xy=(3.5, -1), xycoords='data',
            xytext=(-70, -80), textcoords='offset points',
            size=20,
            bbox=dict(boxstyle="round4,pad=.5", fc="0.8"),
            arrowprops=dict(arrowstyle="->",
                            connectionstyle="angle,angleA=0,angleB=-90,rad=10"))

ax.annotate('angle,\nshrink',
            xy=(4., 1), xycoords='data',
            xytext=(-60, 30), textcoords='offset points',
            bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="->",
                            shrinkA=0, shrinkB=10,
                            connectionstyle="angle,angleA=0,angleB=90,rad=10"))

# You can pass an empty string to get only annotation arrows rendered
ann = ax.annotate('', xy=(4., 1.), xycoords='data',
                  xytext=(4.5, -1), textcoords='data',
                  arrowprops=dict(arrowstyle="<->",
                                  connectionstyle="bar",
                                  ec="k",
                                  shrinkA=5, shrinkB=5))


fig = plt.figure(2)
fig.clf()
ax = fig.add_subplot(111, autoscale_on=False, xlim=(-1, 5), ylim=(-5, 3))

el = Ellipse((2, -1), 0.5, 0.5)
ax.add_patch(el)

ax.annotate('$->$',
            xy=(2., -1), xycoords='data',
            xytext=(-150, -140), textcoords='offset points',
            bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="->",
                            patchB=el,
                            connectionstyle="angle,angleA=90,angleB=0,rad=10"))

ax.annotate('arrow\nfancy',
            xy=(2., -1), xycoords='data',
            xytext=(-100, 60), textcoords='offset points',
            size=20,
            # bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="fancy",
                            fc="0.6", ec="none",
                            patchB=el,
                            connectionstyle="angle3,angleA=0,angleB=-90"))

ax.annotate('arrow\nsimple',
            xy=(2., -1), xycoords='data',
            xytext=(100, 60), textcoords='offset points',
            size=20,
            # bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="simple",
                            fc="0.6", ec="none",
                            patchB=el,
                            connectionstyle="arc3,rad=0.3"))

ax.annotate('wedge',
            xy=(2., -1), xycoords='data',
            xytext=(-100, -100), textcoords='offset points',
            size=20,
            # bbox=dict(boxstyle="round", fc="0.8"),
            arrowprops=dict(arrowstyle="wedge,tail_width=0.7",
                            fc="0.6", ec="none",
                            patchB=el,
                            connectionstyle="arc3,rad=-0.3"))

ann = ax.annotate('bubble,\ncontours',
                  xy=(2., -1), xycoords='data',
                  xytext=(0, -70), textcoords='offset points',
                  size=20,
                  bbox=dict(boxstyle="round",
                            fc=(1.0, 0.7, 0.7),
                            ec=(1., .5, .5)),
                  arrowprops=dict(arrowstyle="wedge,tail_width=1.",
                                  fc=(1.0, 0.7, 0.7), ec=(1., .5, .5),
                                  patchA=None,
                                  patchB=el,
                                  relpos=(0.2, 0.8),
                                  connectionstyle="arc3,rad=-0.1"))

ann = ax.annotate('bubble',
                  xy=(2., -1), xycoords='data',
                  xytext=(55, 0), textcoords='offset points',
                  size=20, va="center",
                  bbox=dict(boxstyle="round", fc=(1.0, 0.7, 0.7), ec="none"),
                  arrowprops=dict(arrowstyle="wedge,tail_width=1.",
                                  fc=(1.0, 0.7, 0.7), ec="none",
                                  patchA=None,
                                  patchB=el,
                                  relpos=(0.2, 0.5)))

plt.show()
```

### fill\_between\_demo
[pylab\_examples example code: fill\_between\_demo.py](https://matplotlib.org/examples/pylab_examples/fill_between_demo.html)
{% gp 1-3 %}
<img src="https://matplotlib.org/_images/fill_between_demo_001.png">
<img src="https://matplotlib.org/_images/fill_between_demo_011.png">
<img src="https://matplotlib.org/_images/fill_between_demo_021.png">
{% endgp %}

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0.0, 2, 0.01)
y1 = np.sin(2*np.pi*x)
y2 = 1.2*np.sin(4*np.pi*x)

fig, (ax1, ax2, ax3) = plt.subplots(3, 1, sharex=True)

ax1.fill_between(x, 0, y1)
ax1.set_ylabel('between y1 and 0')

ax2.fill_between(x, y1, 1)
ax2.set_ylabel('between y1 and 1')

ax3.fill_between(x, y1, y2)
ax3.set_ylabel('between y1 and y2')
ax3.set_xlabel('x')

# now fill between y1 and y2 where a logical condition is met.  Note
# this is different than calling
#   fill_between(x[where], y1[where],y2[where]
# because of edge effects over multiple contiguous regions.
fig, (ax, ax1) = plt.subplots(2, 1, sharex=True)
ax.plot(x, y1, x, y2, color='black')
ax.fill_between(x, y1, y2, where=y2 >= y1, facecolor='green', interpolate=True)
ax.fill_between(x, y1, y2, where=y2 <= y1, facecolor='red', interpolate=True)
ax.set_title('fill between where')

# Test support for masked arrays.
y2 = np.ma.masked_greater(y2, 1.0)
ax1.plot(x, y1, x, y2, color='black')
ax1.fill_between(x, y1, y2, where=y2 >= y1, facecolor='green', interpolate=True)
ax1.fill_between(x, y1, y2, where=y2 <= y1, facecolor='red', interpolate=True)
ax1.set_title('Now regions with y2>1 are masked')

# This example illustrates a problem; because of the data
# gridding, there are undesired unfilled triangles at the crossover
# points.  A brute-force solution would be to interpolate all
# arrays to a very fine grid before plotting.

# show how to use transforms to create axes spans where a certain condition is satisfied
fig, ax = plt.subplots()
y = np.sin(4*np.pi*x)
ax.plot(x, y, color='black')

# use the data coordinates for the x-axis and the axes coordinates for the y-axis
import matplotlib.transforms as mtransforms
trans = mtransforms.blended_transform_factory(ax.transData, ax.transAxes)
theta = 0.9
ax.axhline(theta, color='green', lw=2, alpha=0.5)
ax.axhline(-theta, color='red', lw=2, alpha=0.5)
ax.fill_between(x, 0, 1, where=y > theta, facecolor='green', alpha=0.5, transform=trans)
ax.fill_between(x, 0, 1, where=y < -theta, facecolor='red', alpha=0.5, transform=trans)


plt.show()
```

### broken\_bath
[pylab\_examples example code: broken\_barh.py](https://matplotlib.org/examples/pylab_examples/broken_barh.html)
<img src="https://matplotlib.org/_images/broken_barh1.png" width="47%">

### boxplot\_demo2
[pylab\_examples example code: boxplot\_demo2.py](https://matplotlib.org/examples/pylab_examples/boxplot_demo2.html)
<img src="https://matplotlib.org/_images/boxplot_demo2.png" width="87%">

## Showcase

### colorbar\_basics
[api example code: colorbar\_basics.py](https://matplotlib.org/examples/api/colorbar_basics.html)
<img src="https://matplotlib.org/_images/colorbar_basics.png" width="87%">

### span\_regions
[api example code: span\_regions.py](https://matplotlib.org/examples/api/span_regions.html)
<img src="https://matplotlib.org/_images/span_regions.png" width="47%">

### skewt
[api example code: skewt.py](https://matplotlib.org/examples/api/skewt.html)
<img src="https://matplotlib.org/_images/skewt1.png" width="47%">

## API
## widget


# \* References

