---
title: Matplotlib Tutorials - 4. 命令查询
date: 2020-03-23 20:32:26
updated: 
categories:
  - Drafting
tags:
  - Notes
  - Python
  - Matplotlib
---

[Matplotlib 使用教程 by黄春林](http://www.bioinfo.org.cn/~casp/temp/spring.lecture/Matplotlib_slides.pdf)  
[matplotlib-tutorial github](https://github.com/rougier/matplotlib-tutorial)  
[Matplotlib中修改坐标轴刻度线的属性](https://blog.csdn.net/HHG20171226/article/details/101289933)  

<!--This is, basically, like Command Query-->



# Matplotlib 使用教程

## 画图的第一种方法
### plot 函数

- 画点或者线
  ```python
  plot(x, y)  #     # plot x and y using default line style and color
  plot(x, y, 'bo')  # plot x and y using blue circle markers
  plot(y)  #        # plot y using x as index array 0..N-1
  plot(y, 'r+')  #  # ditto, but with red plusses
  ```
- 如果 x 或者 y 是二维矩阵，则相当于画列向量
- 可以在一个 plot 函数中画多个点或线
  ```python
  plot(x1, y1, 'g^', x2, y2, 'g-')
  plot(x1, y1, x2, y2, 'g-')
  ```
- 参数有 fmt 形式和 kwargs 形式
  ```python
  'g^-' VS color='g', marker='^', ls='-'
  ```

#### plot 函数的参数

- 可使用Line2D的所有参数
  - [http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot](https://matplotlib.org/api/pyplot_api.html#matplotlib.pyp) 
  - ```python
    class matplotlib.lines.Line2D(xdata, ydata,
        linewidth=None, linestyle=None, color=None,
        marker=None, markersize=None,
        markeredgewidth=None, markeredgecolor=None,
        markerfacecolor=None, markerfacecoloralt=u'none',
        fillstyle=u'full', antialiased=None,
        dash_capstyle=None, solid_capstyle=None,
        dash_joinstyle=None, solid_joinstyle=None,
        pickradius=5, drawstyle=None, markevery=None,
        **kwargs)
    ```

#### Line2D 可指定的参数
<img src="/images/2020-03/0323_Query_huang4a.png" width="100%"><img src="/images/2020-03/0323_Query_huang4b.png" width="100%">

### Markers
<img src="/images/2020-03/0323_Query_huang1.png" width="100%">
### Line styles
<img src="/images/2020-03/0323_Query_huang2.png" width="100%">

### Colors
- 单词，如 red
- 字母，如 r
- 6 个 16 进制数，如 '#FF0000' 或 '#ff0000'
- 含有 三(RGB) 或 四(RGBA) 个元素 (0~1) 的元组，如 (1,0,0) 或 (1,0,0,1) ，只用于 kwargs
- 灰度字符串，如 '0.8'

<img src="/images/2020-03/0323_Query_huang3a.png" width="100%">

#### 一个字母可表示的颜色
- r: 红色
- g: 绿色
- b: 蓝色
- c: cyan
- m: 紫色
- y: 土黄色
- k: 黑色
- w: 白色

### fill style

<img src="/images/2020-03/0323_Query_huang5a.png" width="100%"><img src="/images/2020-03/0323_Query_huang5b.png" width="100%">

### title 函数
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.title(s, \*args, \*\*kwargs)**</td></table>
  - **label: str**
  - **fontdict: dict**
    - 默认为： <!--python--> ```python
      {'fontsize': rcParams['axes.titlesize'],
       'fontweight': rcParams['axes.titleweight'],
       'verticalalignment': 'baseline',
       'horizontalalignment': loc}
      ```

  - **loc : {'center', 'left', 'right'}, str, optional**

- 可使用 Text 的所有参数
  - ```python
    class matplotlib.text.Text(x=0, y=0, text=u'',
        color=None, verticalalignment=u'baseline',
        horizontalalignment=u'left',
        multialignment=None, fontproperties=None,
        rotation=None, linespacing=None,
        rotation_mode=None, **kwargs)
    ```

#### Text 可指定的参数
<img src="/images/2020-03/0323_Query_huang6a.png" width="100%"><img src="/images/2020-03/0323_Query_huang6b.png" width="100%">

### text 函数

- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.text(x, y, s, fontdict=None,
  withdash=False, \*\*kwargs)**</td></table>
  - Add text in string s to axis at location x, y, data coordinates
  - 注意这里的坐标是绝对坐标，与图例不同
  - 可使用 Text 的所有参数

### xlabel, ylabel
- 设置横坐标和纵坐标的名字
- 用法与 title 一样

### 设置坐标轴 (axis)
- 坐标范围设置
  – 设置 x 轴范围： xlim 函数
  – 设置 y 轴范围： ylim 函数
  ```python
  xmin, xmax = xlim()  ## return the current xlim
  xlim( (xmin, xmax) )  # set the xlim to xmin, xmax
  xlim( xmin, xmax )  # # set the xlim to xmin, xmax
  xlim(xmax=3)  #       # adjust the max leaving min unchanged
  xlim(xmin=1)  #       # adjust the min leaving max unchanged
  ```

#### 设置线性坐标系与对数坐标系
- <table><td bgcolor=#E6E6FA>**xscale/yscale(scale, \*\*kwargs)**</td></table>
  – scale 的 3 种取值：**'linear' | 'log' | 'symlog'**

<img src="/images/2020-03/0323_Query_huang7a.png" width="100%">

#### 在对数坐标系下画图
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.semilogx(\*args, \*\*kwargs)**</td></table>
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.semilogy(\*args, \*\*kwargs)**</td></table>
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.loglog(\*args, \*\*kwargs)**</td></table>
- 参数同 plot (Line2D)
- 注意与前面 xscale/yscale 函数的区别
  - xscale/yscale 只设置坐标系，没有画图功能

#### 自定义坐标
- <table><td bgcolor=#E6E6FA>**python matplotlib.pyplot.xticks(\*args, \*\*kwargs)**</td></table>
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.yticks(\*args, \*\*kwargs)**</td></table>
  – 可使用 Text 的参数
  ```python
  # return locs, labels where locs is an array of tick locations and
  # labels is an array of tick labels.
  locs, labels = plt.xticks()

  # set the locations of the xticks
  plt.xticks( np.arange(6) )

  # set the locations and labels of the xticks
  plt.xticks( np.arange(5), ('Tom', 'Dick', 'Harry', 'Sally', 'Sue') )

  plt.xticks( np.arange(12), calendar.month_name[1:13], rotation=17 )

  # 另外一种方法
  plt.gca().set_xticks(np.arange(12))
  plt.gca().set_xticklabels(calendar.month_name[1:13], rotation=17)
  ```

### 图例的用法
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.legend(\*args, \*\*kwargs)**</td></table>
  - **loc: default 0**
  - **fontsize**
  - **numpoints**
  - **shadow**
  - **bbox_to_anchor**
  - ...

<img src="/images/2020-03/0323_Query_huang8a.png" width="100%">

#### 设置图例背景色和阴影
<img src="/images/2020-03/0323_Query_huang8b.png" width="100%">

```python
legend = plt.legend(loc='upper center', shadow=True, fontsize='x-large')
legend.get_frame().set_facecolor('#00FFCC')
```

#### 把图例放在图片以外的地方
<img src="/images/2020-03/0323_Query_huang8c.png" width="100%">

```python
# Place a legend above this legend, expanding
# itself to fully use the given bounding box.
plt.legend(bbox_to_anchor=(0., 1.02, 1., .102),
           loc=3, ncol=2, mode="expand",
           borderaxespad=0.)  # 图例与坐标轴的距离为 0

# Place a legend to the right of this smaller
# figure.
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
```

#### 图例分开放置
<img src="/images/2020-03/0323_Query_huang8d.png" width="100%">

##### Example

```python
import matplotlib.pyplot as plt

line1, = plt.plot([1,2,3], label="Line 1",
linestyle='--')
line2, = plt.plot([3,2,1], label="Line 2",
linewidth=4)

# Create a legend for the first line.
first_legend = plt.legend(handles=[line1], loc=1)

# Add the legend manually to the current Axes.
ax = plt.gca().add_artist(first_legend)

# Create another legend for the second line.
plt.legend(handles=[line2], loc=4)

plt.show()
```

<img src="/images/2020-03/0323_Query_huang8dprime.png" width="60%">

### 保存图片
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.savefig(\*args, \*\*kwargs)**</td></table>
  - 文件名是必需参数
  - <table><td bgcolor=#E6E6FA style="line-height: 1em">**plt.savefig(plot_file, <font color=#FF7F50>bbox_inches='tight'</font>)**</td></table>
    - <font color=black>**bboxinches='tight'**</font> 去掉不需要的白边
    - 输出 ps 格式文件时无法使用这个参数
  - 其他参数
- 如果只想在屏幕上显示出来
  - <table><td bgcolor=#E6E6FA style="line-height: 1em">**plt.show()**</td></table>

### 网格开关
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.grid(b=None, which=u'major', axis=u'both',
  \*\*kwargs)**</td></table>
  - **b: [True | False]**, 是否打网格，默认反转 b
  - **which: ['major' | 'minor' | 'both']**, 在哪种坐标处打网格，默认为 **'major'**
  - **axis: ['both' | 'x' | 'y']**, 横线和竖线|只竖线|只横线，默认为 **'both'**
  - 还可使用 **Line2D** 中的参数
  - 最简单的使用：<font color=black>**plt.grid()**</font>

### 多图

- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.subplot(\*args, \*\*kwargs)**</td></table>
  - <table><td bgcolor=#E6E6FA style="line-height: 1em">**subplot(nrows, ncols, plot\_number)**</td></table>
  - 如果数字都小于 10, 可以写成 subplot(211)

<img src="/images/2020-03/0323_Query_huang9a.png" width="100%"><img src="/images/2020-03/0323_Query_huang9b.png" width="100%">

<!--#### 多图的一个例子-->


### 直方图
- 两种方法
  - **hist**
  - **bar/hbar**

#### hist
<img src="/images/2020-03/0323_Query_huang10a.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt

mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

# the histogram of the data
n, bins, patches = plt.hist(x, 50, normed=1, 
    facecolor='g', edgecolor='black', alpha=0.75)

plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title('Histogram of IQ')

plt.text(60, .025, r'$\mu=100,\ \sigma=15$')

plt.axis([40, 160, 0, 0.03])
plt.grid(True, color='b', linestyle='-.')

plt.show()
```
<img src="/images/2020-03/0323_Query_huang10primea.png" width="60%">

#### hist 函数

- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.hist(x, bins=10, range=None,
  normed=False, weights=None, cumulative=False,
  bottom=None, histtype=u'bar', align=u'mid',
  orientation=u'vertical', rwidth=None, log=False,
  color=None, label=None, stacked=False, hold=None,
  \*\*kwargs)**</td></table>
  - **x**: 一个列表或者多个列表（表示不同数据集，长度可以不一致）
  - **range**: 元组
  - **weights**: x 里每个元素对 bin 高度的贡献 (默认为 1)
  - **bottom**: 数字或者长度为 bins 的列表
  - **histtype: ['bar' | 'barstacked' | 'step' | 'stepfilled']**
  - **align: ['left' | 'mid' | 'right']**
  - **orientation: ['horizontal' | 'vertical']**
  - **rwidth**: bar 相对 bin 的宽度
  - **color**: 一种颜色或者颜色列表（针对不同数据集）

#### 直方图与相应折线图
<img src="/images/2020-03/0323_Query_huang10b.png" width="100%">

```python
import numpy as np
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt

# example data
mu = 100 # mean of distribution
sigma = 15 # standard deviation of distribution
x = mu + sigma * np.random.randn(10000)

num_bins = 50
plt.grid(True, linestyle=':', linewidth=2)
# the histogram of the data
n, bins, patches = plt.hist(x, num_bins, normed=1,
    facecolor='green', edgecolor='k', alpha=0.5)

# add a 'best fit' line
y = mlab.normpdf(bins, mu, sigma)
plt.plot(bins, y, 'r--')

plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title(r'Histogram of IQ: $\mu=100$, $\sigma=15$')

# Tweak spacing to prevent clipping of ylabel
plt.subplots_adjust(left=0.15)
plt.show()
```
<img src="/images/2020-03/0323_Query_huang10primeb.png" width="60%">

#### bar/barh

- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.bar(left, height, width=0.8,
  bottom=None, hold=None, \*\*kwargs)**</td></table>
- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.barh(bottom, width, height=0.8,
  left=None, hold=None, \*\*kwargs)**</td></table>
  - 画 **left, left + width, bottom, bottom + height** 这四条线内的矩形
  - 其他参数（两个函数一样）：**color, edgecolor,
    linewidth, xerr, yerr, ecolor (error bar的颜色),
    capsize (errorbar的大小), error_kw, align (<font color=#9ACD32>*'edge'*</font> or
    'center'), orientation (<font color=#9ACD32>*'vertical'*</font> or 'horizontal'), log**
- 适合在求出数据的概率分布后使用。

#### 使用 bar 的一个例子
<img src="/images/2020-03/0323_Query_huang10c.png" width="100%">

```python
#!/usr/bin/env python
import numpy as np
import matplotlib.pyplot as plt

N = 5
menMeans = (20, 35, 30, 35, 27)
womenMeans = (25, 32, 34, 20, 25)
menStd = (2, 3, 4, 1, 2)
womenStd = (3, 5, 2, 3, 3)
ind = np.arange(N) # the x locations for the groups
width = 0.35 # the width of the bars: can also be len(x) sequence

p1 = plt.bar(ind, menMeans, width, color='r',
            yerr=womenStd,
            edgecolor='k', error_kw={'ecolor': 'b', 'capsize': 8})
p2 = plt.bar(ind, womenMeans, width, color='c',
            bottom=menMeans, yerr=menStd,
            edgecolor='k', error_kw={'ecolor': 'g', 'capsize': 11})

plt.ylabel('Scores')
plt.title('Scores by group and gender')
plt.xticks(ind+width/2., ('G1', 'G2', 'G3', 'G4', 'G5'), rotation=-30) #'vertical'
plt.yticks(np.arange(0,81,10), rotation=30)
plt.legend( (p1[0], p2[0]), ('Men', 'Women') )

plt.show()
```
<img src="/images/2020-03/0323_Query_huang10primec.png" width="60%">

#### errorbar 的画法

- <table><td bgcolor=#E6E6FA>**matplotlib.pyplot.errorbar(x, y, yerr=None, xerr=None, fmt=u'',
  ecolor=None, elinewidth=None, capsize=3, barsabove=False,
  lolims=False, uplims=False, xlolims=False, xuplims=False,
  errorevery=1, capthick=None, hold=None, \*\*kwargs)**</td></table>
  - 可以使用 plot 函数的参数

<img src="/images/2020-03/0323_Query_huang10d.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt

# example data
x = np.arange(0.1, 4, 0.5)
y = np.exp(-x)

plt.errorbar(x, y, xerr=0.2, yerr=0.4,
            ecolor='g', capsize=6)

plt.axis('on')  # 'off': turns off the axis lines and labels
plt.minorticks_on()
plt.tick_params(direction='inout', size=7)  # major
plt.tick_params(which='minor', direction='in')
plt.tick_params(top=True, right=True) # bottom, left

plt.show()
```
<img src="/images/2020-03/0323_Query_huang10primed.png" width="60%">

### 支持中文
涉及到字体问题。略

## 面向对象绘图
### 流程

- matplotlib API 包含有三层，Artist 层处理所有的高层结构，例如处理图表、文字和曲线等的绘制和布局。通常我们只和 Artist 打交道，而不需要关心底层的绘制细节。
- 直接使用 Artists 创建图表的标准流程如下
  - 创建 Figure 对象
  - 用 Figure 对象创建一个或者多个 Axes 或者 Subplot 对象
  - 调用 Axies 等对象的方法创建各种简单类型的 Artists

<img src="/images/2020-03/0323_Query_huang_object1a.png" width="100%">
### subplots 与 axes 的区别
<img src="/images/2020-03/0323_Query_huang_object1b.png" width="100%">

<!--### subplots 与 axes 的区别-->
### 第一个例子
<img src="/images/2020-03/0323_Query_huang_object1c.png" width="100%">

```python
import matplotlib.pyplot as plt
fig = plt.figure()

# first axes
ax1 = fig.add_axes([0.1, 0.1, 0.2, 0.2])
line, = ax1.plot([0,1], [0,1], 'purple')
ax1.set_title("ax1")

##NOT! zmin, zmax = ax1.get_xlim(); ax1.set_xticks((zmin, zmax + 0.2, 0.2))
import matplotlib.ticker as ticker
ax1.xaxis.set_major_locator(ticker.MultipleLocator(0.2))
ax1.yaxis.set_major_locator(ticker.MultipleLocator(0.3))

# second axes
ax2 = fig.add_axes([0.4, 0.3, 0.4, 0.5])
sca = ax2.scatter([1,3,5], [2,1,2], c='k')
ax2.set_title("ax2")

ax2.set_xlim(0., 6.)
ax2.set_ylim(0.8, 2.2)

plt.show()
```
<img src="/images/2020-03/0323_Query_huang_object1primec.png" width="60%">

### figure 类

- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**add_axes(\*args, \*\*kwargs)**</td></table>
  - **rect = l,b,w,h**
  - `fig.add_axes(rect)`
  - `fig.add_axes(rect, frameon=False, axisbg='g')`
  - `fig.add_axes(rect, polar=True)`
  - `fig.add_axes(rect, projection='polar')`
  - `fig.add_axes(ax)`
  - `fig.add_axes(rect, label='axes1')`
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**add_subplots(\*args, \*\*kwargs)**</td></table>
  - `fig.add_subplot(111)`
  - `fig.add_subplot(1,1,1)`
  - `fig.add_subplot(sub)` # sub is an instance
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**gca(\*\*kwargs)**</td></table>
  - Get the current axes, creating one if necessary
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**get_axes()**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**legend(handles, labels, \*args, \*\*kwargs)**</td></table>
  - <span style="background-color: #FFF68F; font-weight: bold;">&nbsp; legend( (line1, line2, line3), ('label1', 'label2', 'label3'), 'upper right')  &nbsp;&nbsp;</span> <!--<pre>底色会变黑</pre>-->
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**savefig(\*args, \*\*kwargs)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**sca(a)**</td></table>
  - Set the current axes to be *a* and return *a*
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**show(warn=True)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**suptitle(t, \*\*kwargs)**</td></table>
  - Add a centered title to the figure.
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**text(x, y, s, \*args, \*\*kwargs)**</td></table>

Others
• get/set_edgecolor()
• get/set_facecolor()
• get/set_figwidth()
• get/set_figheight()
• ....

<img src="/images/2020-03/0323_Query_huang_object2a.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure()
ax1 = fig.add_axes([0.1, 0.1, 0.4, 0.7])
ax2 = fig.add_axes([0.55, 0.1, 0.4, 0.7])

x = np.arange(0.0, 2.0, 0.02)
y1 = np.sin(2*np.pi*x)
y2 = np.exp(-x)
l1, l2 = ax1.plot(x, y1, 'rs-', x, y2, 'go')
l1.set_markeredgecolor('k')

y3 = np.sin(4*np.pi*x)
y4 = np.exp(-2*x)
l3, l4 = ax2.plot(x, y3, 'yd-', x, y4, 'k^')
l3.set_markeredgecolor('b')

fig.legend((l1, l2), ('Line 1', 'Line 2'),
'upper left')
fig.legend((l3, l4), ('Line 3', 'Line 4'),
'upper right')
# plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/0323_Query_huang_object2primea.png" width="60%">

### axes 类

- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**add_artist(a)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**add_line(line)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 1em">**axis(\*v, \*\*kwargs)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 3ex">**bar(left, height, width=0.8, bottom=None,
  \*\*kwargs)**</td></table>
- <table><td bgcolor=#C1FFC1 style="line-height: 3ex">**barh(bottom, width, height=0.8, left=None,
  \*\*kwargs)**</td></table>
- pyplot, figure, axes 很多函数是一样的，axes 在很多函数名称上加了 `set_` 或 `get_` 。

#### axis 类（函数不全）

<!--td  style="font-weight: bold; line-height: 1ex, 2ex, 3ex, 1em" -->
<!--ul style="line-height: 1.5ex" px,em-->
<table><td bgcolor=#C1FFC1 style="font-weight: bold; line-height: 2ex"><ul>
<li> cla(): clear </li>
<li> get_gridlines() </li>
<li> get_label() </li>
<li> get/set_label_text() </li>
<li> get_major/minor_ticks(numticks=None) </li>
<li> get_major/minorticklabels() </li>
<li> get_major/minorticklines() </li>
<li> get/set_ticklabels(minor=False, which=None) </li>
<li> get_ticklines(minor=False) </li>
<li> grid(b=None, which=u'major', \*\*kwargs) </li>
<li> set_ticks(ticks, minor=False) </li>
</ul></td></table>

#### axis 的一些应用

- 选择是否显示刻度值
  - x轴上，1为下，2为上
  - y轴上，1为左，2为右
  ```python
  for tick in ax.xaxis.get_major_ticks():
      tick.label1On = True
      tick.label2On = False
  for tick in ax.yaxis.get_major_ticks():
      tick.label1On = False
      tick.label2On = False
  ```
- 选择如何显示刻度
```python
ax.xaxis.set_ticks_position(‘none’)
ax.yaxis.set_ticks_position(‘right’)
```
- 完全自定义坐标轴刻度及刻度值
```python
ax.set_xticks([-250, -200, -150, -100, -50, 0, 50, 100, 150, 200])
ax.set_xticklabels([‘-250′, ”, ‘-150′, ”, ‘-50′, ”, ’50’, ”, ‘150’, ”])
ax.set_yticks([-40, -20, 0, 20, 40, 60, 80])
ax.set_yticklabels([”, ”, ”, ”, ”, ”, ”])
```
- 分别设置x轴和y轴上刻度值的字体大小
```python
for tick in ax.xaxis.get_major_ticks():
    tick.label1.set_fontsize(18)
for tick in ax.yaxis.get_major_ticks():
    tick.label1.set_fontsize(18)
```
- 对比
  <span style="background-color: #FFF68F; font-weight: bold;">&nbsp; for label in <font color=#FF4500>plt.gca()</font>.xaxis.get_ticklabels():  &nbsp;&nbsp;</span>
```python
for label in plt.gca().xaxis.get_ticklabels():
    label.set_fontsize(18)
for label in plt.gca().yaxis.get_ticklabels():
    label.set_fontsize(18)
```
- 这样也可以设置刻度值字体大小
```python
matplotlib.rc(‘xtick’, labelsize=20)
matplotlib.rc(‘ytick’, labelsize=20)
```

### 一个例子
<img src="/images/2020-03/0323_Query_huang_object2b.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt
plt.subplots_adjust(hspace=0.4)
t = np.arange(0.01, 20.0, 0.01)

# log y axis
plt.subplot(221)
plt.semilogy(t, np.exp(-t/5.0))
plt.title('semilogy')
plt.grid(True)
plt.ylim(10**-2, 1.)

# log x axis
plt.subplot(222)
plt.semilogx(t, np.sin(2*np.pi*t))
plt.title('semilogx')
plt.grid(True)
plt.ylim(-1.0, 1.0)

# log x and y axis
plt.subplot(223)
plt.loglog(t, 20*np.exp(-t/10.0), basex=2)
# plt.grid(True)
plt.title('loglog base 4 on x')

import matplotlib.ticker as ticker
plt.xlim(2.**-7, 2.**5)
plt.gca().xaxis.set_major_locator(ticker.LogLocator(base=2, numticks=15))
plt.ylim(1., 100.)
plt.grid(True, linestyle='-.', lw=2)

# with errorbars: clip non-positive values
ax = plt.subplot(224)
ax.set_xscale("log", nonposx='clip')
ax.set_yscale("log", nonposy='clip')

x = 10.0**np.linspace(0.0, 2.0, 20)
y = x**2.0
plt.errorbar(x, y, xerr=0.1*x, yerr=5.0+0.75*y)
ax.set_ylim(ymin=0.1)
ax.set_title('Errorbars go negative')

plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/0323_Query_huang_object2primeb.png" width="60%">

### 另外两个例子
<img src="/images/2020-03/0323_Query_huang_object2c.png" width="100%"><img src="/images/2020-03/0323_Query_huang_object2d.png" width="100%">

## 用 pylab 模块快速画图
类似于第一种方法  
<img src="/images/2020-03/0323_Query_huang_object3a.png" width="100%">



# Matplotlib tutorial: [<font color=#00FF7F>ref</font>](https://github.com/rougier/matplotlib-tutorial)


- Introduction
  -- IPython and the pylab mode
  -- pyplot
- Simple plot
  -- Using defaults
  -- Instantiating defaults
  -- Changing colors and line widths
  -- Setting limits
  -- Setting ticks
  -- Setting tick labels
  -- Moving spines
  -- Adding a legend
  -- Annotate some points
  -- Devil is in the details

## Figures, Subplots, Axes and Ticks

### Figures

A figure is the windows in the GUI that has "Figure \#" as title. Figures are numbered starting from 1 as opposed to the normal Python way starting from 0. This is clearly MATLAB-style. There are several parameters that determine what the figure looks like:

| Argument | Default | Description |
|---------|--------|------------|
| num | 1 | number of figure |
| figsize | figure.figsize | figure size in in inches (width, height) |
| dpi | figure.dpi | resolution in dots per inch |
| facecolor | figure.facecolor | color of the drawing background |
| edgecolor | figure.edgecolor | color of edge around the drawing background |
| frameon | True |  draw figure frame or not |

The defaults can be specified in the resource file and will be used most of the time. Only the number of the figure is frequently changed.

When you work with the GUI you can close a figure by clicking on the x in the upper right corner. You can also close a figure programmatically by calling close. Depending on the argument it closes (1) the current figure (no argument), (2) a specific figure (figure number or figure instance as argument), or (3) all figures (all as argument).

As with other objects, you can set figure properties with the set_something methods.

### Subplots
With subplot you can arrange plots in a regular grid. You need to specify the number of rows and columns and the number of the plot. Note that the [gridspec](http://matplotlib.sourceforge.net/users/gridspec.html) command is a more powerful alternative.
{% gp 1-3 %}
<img src="/images/2020-03/subplot-grid.png">
<img src="/images/2020-03/gridspec.png">
{% endgp %}
### Axes
Axes are very similar to subplots but allow placement of plots at any location in the figure. So if we want to put a smaller plot inside a bigger one we do so with axes.
{% gp 1-3 %}
<img src="/images/2020-03/axes.png">
<img src="/images/2020-03/axes-2.png">
{% endgp %}


### Ticks

Well formatted ticks are an important part of publishing-ready figures. Matplotlib provides a totally configurable system for ticks. There are tick locators to specify where ticks should appear and tick formatters to give ticks the appearance you want. Major and minor ticks can be located and formatted independently from each other. By default minor ticks are not shown, i.e. there is only an empty list for them because it is as NullLocator (see below).

#### Tick Locators
There are several locators for different kind of requirements:

<img src="/images/2020-03/0323_Query_GitHub_quick5.png" width="80%">

All of these locators derive from the base class matplotlib.ticker.Locator. You can make your own locator deriving from it. Handling dates as ticks can be especially tricky. Therefore, matplotlib provides special locators in matplotlib.dates.


<!--<table width="92%"><tr><td style="width: 12%">Class</td><td style="width: 80%">Description</td></tr><tr><td>NullLocator</td><td>No ticks.</td></tr><tr><td>IndexLocator</td><td>Place a tick on every multiple of some base number of points plotted.</td></tr><tr><td>FixedLocator</td><td>Tick locations are fixed.</td></tr><tr><td>LinearLocator</td><td>Determine the tick locations.</td></tr><tr><td>MultipleLocator</td><td>Set a tick on every integer that is multiple of some base.</td></tr><tr><td>AutoLocator</td><td>Select no more than n intervals at nice locations.</td></tr><tr><td>LogLocator</td><td>Determine the tick locations for log axes.</td></tr></table>-->
<!--
{% gp 1-2 %}
<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/subplot-grid.png">
<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/gridspec.png">
{% endgp %}
{% gp 1-2 %}
<img src="https://raw.githubusercontent.com/rougier/matplotlib-tutorial/master/figures/subplot-grid.png">
{% endgp %}
{% gp 1-2 %}
<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/axes.png">
<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/axes-2.png">
{% endgp %}
-->
<!--
### Ticks Ticks

| Class | Description |
|-------|-------------|
| NullLocator | No ticks. |
| IndexLocator  | Place a tick on every multiple of some base number of points plotted. |
| FixedLocator  | Tick locations are fixed. |
| LinearLocator | Determine the tick locations. |
| MultipleLocator | Set a tick on every integer that is multiple of some base. |
| AutoLocator | Select no more than n intervals at nice locations. |
| LogLocator  | Determine the tick locations for log axes. |
-->

<!--<div style="position: relative; float: left;">--->
<!--
<div>
<table width="80%">
  <tr><td style="width: 15%">Class</td><td style="width: 65%">Description</td></tr>
  <tr>
    <td>NullLocator</td>
    <td>No ticks. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-NullLocator.png"></td>
  </tr>
  <tr>
    <td>IndexLocator</td>
    <td>Place a tick on every multiple of some base number of points plotted. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-IndexLocator.png"></td>
  </tr>
  <tr>
    <td>FixedLocator</td>
    <td>Tick locations are fixed. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-FixedLocator.png"></td>
  </tr>
  <tr>
    <td>LinearLocator</td>
    <td>Determine the tick locations. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LinearLocator.png"></td>
  </tr>
  <tr>
    <td>MultipleLocator</td>
    <td>Set a tick on every integer that is multiple of some base. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-MultipleLocator.png"></td>
  </tr>
  <tr>
    <td>AutoLocator</td>
    <td>Select no more than n intervals at nice locations. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-AutoLocator.png"></td>
  </tr>
  <tr>
    <td>LogLocator</td>
    <td>Determine the tick locations for log axes. <img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LogLocator.png"></td>
  </tr>
</table>
</div>

<table width="92%"><div style="width: 92%"><tr><td style="width: 12%"><div style="width: 12%">Class</div></td><td style="width: 80%"><div style="width: 80%">Description</div></td></tr><tr><td>NullLocator</td><td>No ticks.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-NullLocator.png"></td></tr><tr><td>IndexLocator</td><td>Place a tick on every multiple of some base number of points plotted.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-IndexLocator.png"></td></tr><tr><td>FixedLocator</td><td>Tick locations are fixed.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-FixedLocator.png"></td></tr><tr><td>LinearLocator</td><td>Determine the tick locations.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LinearLocator.png"></td></tr><tr><td>MultipleLocator</td><td>Set a tick on every integer that is multiple of some base.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-MultipleLocator.png"></td></tr><tr><td>AutoLocator</td><td>Select no more than n intervals at nice locations.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-AutoLocator.png"></td></tr><tr><td>LogLocator</td><td>Determine the tick locations for log axes.<img src="https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LogLocator.png"></td></tr></div></table>
-->


## Animation

### Drip drop
### Earthquakes

## Other Types of Plots

### Regular Plots

without and within `plt.axes([left, bottom, weight, height])`
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other1a.png">
<img src="/images/2020-03/0323_Query_rougier_other1b.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

n = 256
X = np.linspace(-np.pi,np.pi,n,endpoint=True)
Y = np.sin(2*X)

# plt.axes([0.025,0.025,0.95,0.95])
plt.axes([0.1, 0.1, 0.8, 0.85]) # (left, bottom, weight, height)

plt.plot (X, Y+1, color='purple', alpha=1.00)
plt.fill_between(X, 1, Y+1, color='blue', alpha=.25)
plt.fill_betweenx(Y, -np.pi/8, x2=np.pi/8,
        # where=((X < np.pi/2) & (X > -np.pi/2)), 
        color='green', alpha=0.47)

plt.plot (X, Y-1, color='black', alpha=1.00)
plt.fill_between(X, -1, Y-1, (Y-1) > -1, color='blue', alpha=.25)
plt.fill_between(X, -1, Y-1, (Y-1) < -1, color='red',  alpha=.25)

plt.xlim(-np.pi,np.pi) #, plt.xticks([])
plt.ylim(-2.5,2.5) #, plt.yticks([])
# plt.savefig('../figures/plot_ex.png',dpi=48)

from matplotlib import ticker
plt.gca().xaxis.set_major_locator(ticker.MultipleLocator(np.pi/4))
# plt.tight_layout()
# plt.subplots_adjust(left=0.18, wspace=0.25, hspace=0.25,
#                     bottom=0.13, top=0.91)
plt.show()
```

### Scatter Plots

using `plt.colorbar()` or `plt.set_cmap('jet'`
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other2a.png">
<img src="/images/2020-03/0323_Query_rougier_other2b.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

n = 1024
X = np.random.normal(0,1,n)
Y = np.random.normal(0,1,n)
T = np.arctan2(Y,X)

# plt.axes([0.025,0.025,0.95,0.95])
plt.scatter(X, Y, s=75, c=T, alpha=.5)

plt.xlim(-1.5,1.5) #, plt.xticks([])
plt.ylim(-1.5,1.5) #, plt.yticks([])
# savefig('../figures/scatter_ex.png',dpi=48)

# plt.colorbar()
# plt.set_cmap('jet') #'hot') # plt.colormaps()
plt.show()
```

### Bar Plots

<img src="/images/2020-03/0323_Query_rougier_other3a.png" width="50%">

```python
import numpy as np
import matplotlib.pyplot as plt

n = 12
X = np.arange(n)
Y1 = (1-X/float(n)) * np.random.uniform(0.5,1.0,n)
Y2 = (1-X/float(n)) * np.random.uniform(0.5,1.0,n)

# plt.axes([0.025,0.025,0.95,0.95])
plt.bar(X, +Y1, facecolor='#9999ff', edgecolor='black')
plt.bar(X, -Y2, facecolor='#ff9999', edgecolor='white')

for x,y in zip(X,Y1):
    plt.text(x+0.0, y+0.05, '%.2f' % y, ha='center', va= 'bottom')

for x,y in zip(X,Y2):
    plt.text(x+0.4, -y-0.05, '%.2f' % y, ha='center', va= 'top')

plt.xlim(-.5,n) #, plt.xticks([])
plt.ylim(-1.25,+1.25) #, plt.yticks([])

# savefig('../figures/bar_ex.png', dpi=48)
plt.show()
```

### Contour Plots

第 13--15 行语句依次执行后的结果分别是
{% gp 1-3 %}
<img src="/images/2020-03/0323_Query_rougier_other4a.png">
<img src="/images/2020-03/0323_Query_rougier_other4b.png">
<img src="/images/2020-03/0323_Query_rougier_other4c.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

def f(x,y):
    return (1-x/2+x**5+y**3)*np.exp(-x**2-y**2)

n = 256
x = np.linspace(-3,3,n)
y = np.linspace(-3,3,n)
X,Y = np.meshgrid(x,y)
# plt.axes([0.025,0.025,0.95,0.95])

plt.contourf(X, Y, f(X,Y), 8, alpha=.75, cmap=plt.cm.hot)
C = plt.contour(X, Y, f(X,Y), 8, colors='black', linewidth=.5)
plt.clabel(C, inline=1, fontsize=10)

# plt.xticks([]), plt.yticks([])
# savefig('../figures/contour_ex.png',dpi=48)
plt.show()
```

若只执行第 14 句；或者执行 14-15 句，而注释掉第 13 句
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other4pa.png">
<img src="/images/2020-03/0323_Query_rougier_other4pb.png">
{% endgp %}

### Imshow

<img src="/images/2020-03/0323_Query_rougier_other5a.png" width="50%">

```python
import numpy as np
import matplotlib.pyplot as plt

def f(x,y):
    return (1-x/2+x**5+y**3)*np.exp(-x**2-y**2)

n = 10
x = np.linspace(-3,3,3.5*n)
y = np.linspace(-3,3,3.0*n)
X,Y = np.meshgrid(x,y)
Z = f(X,Y)

# plt.axes([0.025,0.025,0.95,0.95])
plt.imshow(Z,interpolation='bicubic', cmap='bone', origin='lower')
plt.colorbar(shrink=.92)

# plt.xticks([]), plt.yticks([])
# savefig('../figures/imshow_ex.png', dpi=48)
plt.show()
```

### Pie Charts

<!--no explode and no equal, with both of them-->
- 不设置 explode 参数 (sizes 乘以的系数值越大，图中的看到的饼图块越小)，也不设置 aspect=equal ；  
- 对比两个参数都有的结果图
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other6a.png">
<img src="/images/2020-03/0323_Query_rougier_other6b.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt
'''
n = 20
Z = np.ones(n)
Z[-1] *= 2
plt.axes([0.025, 0.025, 0.95, 0.95])

plt.pie(Z, explode=Z*.05, colors=['%f' % (i/float(n)) for i in range(n)],
        wedgeprops={"linewidth": 1, "edgecolor": "black"})
plt.gca().set_aspect('equal')
plt.xticks([]), plt.yticks([])
'''

n = 4
Z = np.random.randn(n)
Z /= np.sum(Z)
# Z *= 100.
# Z[-1] /= 2

# The slices will be ordered and plotted counter-clockwise.
labels = [r'Rayos X (40.4 %)', r'RMN en solucion (10.6 %)', 
r'Microscopia electronica (20.7 %)', r'Otros (5.3 %)']
sizes = [40.4, 10.6, 20.7, 5.3]
colors = ['yellowgreen', 'gold', 'lightskyblue', 'lightcoral']

patches, texts = plt.pie(sizes, explode=np.array(sizes)*0.005,
        colors=colors, startangle=30)
plt.legend(patches, labels, loc="best")
# Set aspect ratio to be equal so that pie is drawn as a circle.
plt.axis('equal')
plt.title('Sum = {:.2f}'.format(np.sum(sizes)))

# savefig('../figures/pie_ex.png',dpi=48)
plt.show()
```

>     @_preprocess_data(replace_names=["x", "explode", "labels", "colors"],
>                       label_namer=None)
>     def pie(self, x, explode=None, labels=None, colors=None,
>             autopct=None, pctdistance=0.6, shadow=False, labeldistance=1.1,
>             startangle=None, radius=None, counterclock=True,
>             wedgeprops=None, textprops=None, center=(0, 0),
>             frame=False, rotatelabels=False):
> 
>         """Parameters
>         x : array-like
>             The wedge sizes.
> 
>         explode : array-like, optional, default: None
>             If not *None*, is a ``len(x)`` array which specifies the fraction
>             of the radius with which to offset each wedge.
>         """
>

### Quiver Plots

仅执行第 11 句；仅执行第 12 句；两句同时执行
{% gp 1-3 %}
<img src="/images/2020-03/0323_Query_rougier_other7a.png">
<img src="/images/2020-03/0323_Query_rougier_other7b.png">
<img src="/images/2020-03/0323_Query_rougier_other7c.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

n = 8
X,Y = np.mgrid[0:n,0:n]
T = np.arctan2(Y-n/2.0, X-n/2.0)
R = 10+np.sqrt((Y-n/2.0)**2+(X-n/2.0)**2)
U,V = R*np.cos(T), R*np.sin(T)

# plt.axes([0.025,0.025,0.95,0.95])
plt.quiver(X,Y,U,V,R, alpha=.5)
plt.quiver(X,Y,U,V, edgecolor='k', facecolor='None', linewidth=.5)

plt.xlim(-1,n) #, plt.xticks([])
plt.ylim(-1,n) #, plt.yticks([])

# savefig('../figures/quiver_ex.png',dpi=48)
plt.show()
```

### Grids

<img src="/images/2020-03/0323_Query_rougier_other8a.png" width="50%">

```python
import numpy as np
import matplotlib.pyplot as plt

# ax = plt.axes([0.025,0.025,0.95,0.95])
ax = plt.axes()

ax.set_xlim(0,4)
ax.set_ylim(0,3)

ax.xaxis.set_major_locator(plt.MultipleLocator(1.0))
ax.xaxis.set_minor_locator(plt.MultipleLocator(0.1))
ax.yaxis.set_major_locator(plt.MultipleLocator(1.0))
ax.yaxis.set_minor_locator(plt.MultipleLocator(0.1))

ax.grid(which='major', axis='x', linewidth=0.75, linestyle='-', color='b')
ax.grid(which='minor', axis='x', linewidth=0.25, linestyle='-', color='0.75')
ax.grid(which='major', axis='y', linewidth=0.75, linestyle='-', color='r')
ax.grid(which='minor', axis='y', linewidth=0.25, linestyle='-', color='0.25')

ax.set_xticklabels([])
ax.set_yticklabels([])

# savefig('../figures/grid_ex.png',dpi=48)
plt.show()
```

### Multi Plots

注释掉 ``plt.tight_layout()`` ；取消该句的注释
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other9a.png">
<img src="/images/2020-03/0323_Query_rougier_other9b.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure()
# fig.subplots_adjust(bottom=0.025, left=0.025, top = 0.975, right=0.975)
fig.subplots_adjust(bottom=0.125, left=0.125, top=0.875, right=0.875)

plt.subplot(2,1,1)
# plt.xticks([]), plt.yticks([])
plt.yticks([])

plt.subplot(2,3,4)
# plt.xticks([]), plt.yticks([])

plt.subplot(2,3,5)
# plt.xticks([]), plt.yticks([])
plt.xticks([])

plt.subplot(2,3,6)
plt.xticks([]), plt.yticks([])

plt.tight_layout()
# plt.savefig('../figures/multiplot_ex.png',dpi=48)
plt.show()
```

### Polar Axis

- (1) 原例 ``bars = plt.bar(theta, radii, width=width, bottom=0.0)``；   
- (2) x,y 坐标刻度都显示 (edge linewidth=1)；  
- (3-4) edge lw=2, 只显示 x 或 y 轴，第三、四幅图分别是只显示 x 轴或只显示 y 轴时的情形

{% gp 4-3 %}
<img src="/images/2020-03/0323_Query_rougier_other10d.png">
<img src="/images/2020-03/0323_Query_rougier_other10a.png">
<img src="/images/2020-03/0323_Query_rougier_other10bxaxis.png">
<img src="/images/2020-03/0323_Query_rougier_other10cyaxis.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

# ax = plt.axes([0.025,0.025,0.95,0.95], polar=True)
ax = plt.axes(polar=True)

N = 20
theta = np.arange(0.0, 2*np.pi, 2*np.pi/N)
radii = 10*np.random.rand(N)
width = np.pi/4*np.random.rand(N)
# bars = plt.bar(theta, radii, width=width, bottom=0.0)
bars = plt.bar(theta, radii, width=width, bottom=0.0,
        # error_kw={'ecolor': 'k', 'capsize': 6}, # seems no use
        edgecolor='k', linewidth=2)

for r,bar in zip(radii, bars):
    bar.set_facecolor( plt.cm.jet(r/10.))
    bar.set_alpha(0.5)

ax.set_xticklabels([])  ## only show y-axis
ax.set_yticklabels([])  ## only show x-axis
# savefig('../figures/polar_ex.png',dpi=48)
plt.show()
```

### 3D Plots

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = Axes3D(fig)
X = np.arange(-4, 4, 0.25)
Y = np.arange(-4, 4, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X**2 + Y**2)
Z = np.sin(R)

ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap=plt.cm.hot,
        edgecolor='k')
ax.contourf(X, Y, Z, zdir='z', offset=-2, cmap=plt.cm.hot)
ax.set_zlim(-2,2)

# savefig('../figures/plot3d_ex.png',dpi=48)
plt.show()
```

<!--
在第 13--16 句命令中：  
- a) 只执行第 13 句
- b) 只执行第 13 句，且设置 `edgecolor='k'`
- c) 只执行第 15 句
- d) 执行 15-16 句
- e) 执行 13-14,16 句，注释掉第 15 句
- f) 执行 13-15 句
- g) 执行 13-16 句

Summary:  
- no limit to ``zlim``
  - only ``ax.plot_surface()``: (a-b)
  - only ``ax.contourf()``: (c)
- ``ax.set_zlim()``
  - with ``ax.contourf()``:(d)-zlim
  - with ``ax.plot_surface()``: (e)-zlim
- both ``plot_surface`` and ``contourf``
  - not including `zlim`: (f)
  - within specific limits: (g)

-->
<!--bgcolor: #FFFACD -->

<!--
<html>
<table style="margin-left: auto; margin-right: auto; line-height: 1em">
  <tr>
    <td>
在第 13--16 句命令中：  
<ol type="a">
  <li> 只执行第 13 句</li>
  <li> 只执行第 13 句，且设置 `edgecolor='k'`</li>
  <li> 只执行第 15 句</li>
  <li> 执行 15-16 句</li>
  <li> 执行 13-14,16 句，注释掉第 15 句</li>
  <li> 执行 13-15 句</li>
  <li> 执行 13-16 句</li>
</ul>
    </td>
    <td bgcolor=#FFF8DC style="line-height: 1em">
**Summary:**  
<ul style="list-style-type: square; line-height: 1ex">
  <li>no limit to ``zlim``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**a-b):**</font> only ``ax.plot_surface()``</li>
    <li><font color="black" style="font-weight: bold;">**c):**</font> only ``ax.contourf()``</li>
  </ul>
  <li>``ax.set_zlim()``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**d)**-zlim:</font> with ``ax.contourf()``</li>
    <li><font color="black" style="font-weight: bold;">**e)**-zlim:</font> with ``ax.plot_surface()``</li>
  </ul>
  <li>both ``plot_surface`` and ``contourf``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**f):**</font> not including `zlim`</li>
    <li><font color="black" style="font-weight: bold;">**g):**</font> within specific limits</li>
  </ul>
</ul>
    </td>
  </tr>
</table>
</html>
-->

<table style="margin-left: auto; margin-right: auto; line-height: 2em"><tr><td>在第 13--16 句命令中：<ol type="a" style="font-weight: bold;"><li style="font-weight: normal;"> 只执行第 13 句</li><li style="font-weight: normal;"> 只执行第 13 句，且设置 `edgecolor='k'`</li><li style="font-weight: normal;"> 只执行第 15 句</li><li style="font-weight: normal;"> 执行 15-16 句</li><li style="font-weight: normal;"> 执行 13-14,16 句，注释掉第 15 句</li><li style="font-weight: normal;"> 执行 13-15 句</li><li style="font-weight: normal;"> 执行 13-16 句</li></ul></td><td bgcolor=#FFF8DC style="line-height: 2em">**Summary:**<ul style="list-style-type: square; line-height: 2em"><li>no limit to ``zlim``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**a-b):**</font> only ``ax.plot_surface()``</li><li><font color="black" style="font-weight: bold;">**c):**</font> only ``ax.contourf()``</li></ul><li>``ax.set_zlim()``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**d)**-zlim:</font> with ``ax.contourf()``</li><li><font color="black" style="font-weight: bold;">**e)**-zlim:</font> with ``ax.plot_surface()``</li></ul><li>both ``plot_surface`` and ``contourf``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**f):**</font> not including `zlim`</li><li><font color="black" style="font-weight: bold;">**g)-zlim:**</font> within specific limits</li></ul></ul></td></tr></table>

{% gp 8-5 %}
<img src="/images/2020-03/0323_Query_rougier_other11a.png">
<img src="/images/2020-03/0323_Query_rougier_other11b.png">
<img src="/images/2020-03/0323_Query_rougier_other11c.png">
<img src="/images/2020-03/0323_Query_rougier_other11d.png">
<img src="/images/2020-03/0323_Query_rougier_other11e.png">
<img src="/images/2020-03/0323_Query_rougier_other11f.png">
<img src="/images/2020-03/0323_Query_rougier_other11g.png">
{% endgp %}

### Text

原版示例 v.s. 注释掉第 11 句
{% gp 1-2 %}
<img src="/images/2020-03/0323_Query_rougier_other12a.png">
<img src="/images/2020-03/0323_Query_rougier_other12b.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt

eqs = []
eqs.append((r"$W^{3\beta}_{\delta_1 \rho_1 \sigma_2} = U^{3\beta}_{\delta_1 \rho_1} + \frac{1}{8 \pi 2} \int^{\alpha_2}_{\alpha_2} d \alpha^\prime_2 \left[\frac{ U^{2\beta}_{\delta_1 \rho_1} - \alpha^\prime_2U^{1\beta}_{\rho_1 \sigma_2} }{U^{0\beta}_{\rho_1 \sigma_2}}\right]$"))
eqs.append((r"$\frac{d\rho}{d t} + \rho \vec{v}\cdot\nabla\vec{v} = -\nabla p + \mu\nabla^2 \vec{v} + \rho \vec{g}$"))
eqs.append((r"$\int_{-\infty}^\infty e^{-x^2}dx=\sqrt{\pi}$"))
eqs.append((r"$E = mc^2 = \sqrt{{m_0}^2c^4 + p^2c^2}$"))
eqs.append((r"$F_G = G\frac{m_1m_2}{r^2}$"))

plt.axes([0.025,0.025,0.95,0.95])

for i in range(24):
    index = np.random.randint(0,len(eqs))
    eq = eqs[index]
    size = np.random.uniform(12,32)
    x,y = np.random.uniform(0,1,2)
    alpha = np.random.uniform(0.25,.75)
    plt.text(x, y, eq, ha='center', va='center', color="#11557c", alpha=alpha,
             transform=plt.gca().transAxes, fontsize=size, clip_on=True)

plt.xticks([]), plt.yticks([])
# savefig('../figures/text_ex.png',dpi=48)
plt.show()
```

## Beyond this tutorial
[ref id](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#id9): [ref](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#beyond-this-tutorial)  

### Tutorials
- [Pyplot tutorial](http://matplotlib.sourceforge.net/users/pyplot_tutorial.html)
- [Image tutorial](http://matplotlib.sourceforge.net/users/image_tutorial.html)
- [Text tutorial](http://matplotlib.sourceforge.net/users/index_text.html)
- [Artist tutorial](http://matplotlib.sourceforge.net/users/artists.html)
- [Path tutorial](http://matplotlib.sourceforge.net/users/path_tutorial.html)
- [Transforms tutorial](http://matplotlib.sourceforge.net/users/transforms_tutorial.html)

### Matplotlib documentation
- [User guide](http://matplotlib.sourceforge.net/users/index.html)
- [FAQ](http://matplotlib.sourceforge.net/faq/index.html)
- [Screenshots](http://matplotlib.sourceforge.net/users/screenshots.html)

### Code documentation
### Galleries
The [matplotlib gallery](https://matplotlib.org/gallery.html) is also incredibly useful when you search how to render a given graphic. Each example comes with its source.  
A smaller gallery is also available [here](https://www.labri.fr/).

## Quick references
[ref id](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#id10): [ref](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#quick-references)

### [Line properties](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#line-properties)
<img src="/images/2020-03/0323_Query_GitHub_quick1.png" width="100%">

### Line styles
<img src="/images/2020-03/0323_Query_GitHub_quick2.png" width="70%">

### [Markers](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#markers)
<img src="/images/2020-03/0323_Query_GitHub_quick3.png" width="83%">

### Colormaps 

<!--All colormaps can be reversed by appending **\_r**. For instance, **gray\_r** is the reverse of gray. -->
All colormaps can be reversed by appending `_r`. For instance, ``gray_r`` is the reverse of gray. If you want to know more about colormaps, see [Documenting](https://gist.github.com/2719900)

#### Base
<img src="/images/2020-03/0323_Query_GitHub_quick4a.png" width="100%">
#### GIST
<img src="/images/2020-03/0323_Query_GitHub_quick4b.png" width="100%">
#### Sequential
<img src="/images/2020-03/0323_Query_GitHub_quick4c.png" width="100%">
#### Diverging
<img src="/images/2020-03/0323_Query_GitHub_quick4d.png" width="100%">
#### Qualitative
<img src="/images/2020-03/0323_Query_GitHub_quick4e.png" width="100%">
#### Miscellaneous
<img src="/images/2020-03/0323_Query_GitHub_quick4f.png" width="100%">

# * References

<!--
## Useful
## List
-->
## Useful

[Matplotlib中修改坐标轴刻度线的属性](https://blog.csdn.net/HHG20171226/article/details/101289933)  
[使用table标签，会出现大面积空白](https://github.com/iissnan/hexo-theme-next/issues/114)  
[html table compressed into a row](https://tool.oschina.net/jscompress?type=2)  
[Matplotlib Gallery](https://matplotlib.org/gallery.html)  

## Solution of blanks before ``<table>``

若要解决 ``<table>`` 表格前方出现的大片空白问题，需要将相应代码压缩。但是需要注意的一点是，若 ``<td>`` 内有列表元素，那么设置 ``line-height`` 时，压缩后的值大约应是压缩前值的 2 倍。例如本文相应位置的代码写法是

```markdown
<html>
<table style="margin-left: auto; margin-right: auto; line-height: 1em">
  <tr>
    <td>
在第 13--16 句命令中：  
<ol type="a">
  <li> 只执行第 13 句</li>
  <li> 只执行第 13 句，且设置 `edgecolor='k'`</li>
  <li> 只执行第 15 句</li>
  <li> 执行 15-16 句</li>
  <li> 执行 13-14,16 句，注释掉第 15 句</li>
  <li> 执行 13-15 句</li>
  <li> 执行 13-16 句</li>
</ul>
    </td>
    <td bgcolor=#FFF8DC style="line-height: 1em">
**Summary:**  
<ul style="list-style-type: square; line-height: 1ex">
  <li>no limit to ``zlim``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**a-b):**</font> only ``ax.plot_surface()``</li>
    <li><font color="black" style="font-weight: bold;">**c):**</font> only ``ax.contourf()``</li>
  </ul>
  <li>``ax.set_zlim()``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**d)**-zlim:</font> with ``ax.contourf()``</li>
    <li><font color="black" style="font-weight: bold;">**e)**-zlim:</font> with ``ax.plot_surface()``</li>
  </ul>
  <li>both ``plot_surface`` and ``contourf``</li>
  <ul style="line-height: 2ex">
    <li><font color="black" style="font-weight: bold;">**f):**</font> not including `zlim`</li>
    <li><font color="black" style="font-weight: bold;">**g):**</font> within specific limits</li>
  </ul>
</ul>
    </td>
  </tr>
</table>
</html>
```

```markdown
<table style="margin-left: auto; margin-right: auto; line-height: 2em"><tr><td>在第 13--16 句命令中：<ol type="a"><li> 只执行第 13 句</li><li> 只执行第 13 句，且设置 `edgecolor='k'`</li><li> 只执行第 15 句</li><li> 执行 15-16 句</li><li> 执行 13-14,16 句，注释掉第 15 句</li><li> 执行 13-15 句</li><li> 执行 13-16 句</li></ul></td><td bgcolor=#FFF8DC style="line-height: 2em">**Summary:**<ul style="list-style-type: square; line-height: 2em"><li>no limit to ``zlim``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**a-b):**</font> only ``ax.plot_surface()``</li><li><font color="black" style="font-weight: bold;">**c):**</font> only ``ax.contourf()``</li></ul><li>``ax.set_zlim()``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**d)**-zlim:</font> with ``ax.contourf()``</li><li><font color="black" style="font-weight: bold;">**e)**-zlim:</font> with ``ax.plot_surface()``</li></ul><li>both ``plot_surface`` and ``contourf``</li><ul style="line-height: 4ex"><li><font color="black" style="font-weight: bold;">**f):**</font> not including `zlim`</li><li><font color="black" style="font-weight: bold;">**g):**</font> within specific limits</li></ul></ul></td></tr></table>
```

**References:**  
- markdown 文字两列  
  -- [markdown 左右分栏 css](https://blog.csdn.net/zhangyu4863/article/details/83504008)  
  -- [关于 Markdown 的一些奇技淫巧](https://zhuanlan.zhihu.com/p/28987530)  
  -- [【进阶】还在担心排版？你常见的Markdown书写问题都在这里](https://www.jianshu.com/p/b36c4f06dcb1)  
- ul 标签  
  -- [HTML 5 `<ul>` 标签, W3school](https://www.w3school.com.cn/html5/tag_ul.asp)  
  -- [HTML `<ul>` 标签, 菜鸟](https://www.runoob.com/tags/tag-ul.html)  
  -- [HTML `<ul>` 标签, w3school](https://www.w3school.com.cn/tags/tag_ul.asp)  
- 有序列表 html 标签  
  -- [HTML `<ol>` 标签](https://www.w3school.com.cn/tags/tag_ol.asp)  
  -- [HTML 列表, w3school](https://www.w3school.com.cn/html/html_lists.asp)  
- 有序列表嵌套 html 标签  
  -- [html列表嵌套](https://blog.csdn.net/GUOSJIA/article/details/79055609)  
  -- [html无序有序列表嵌套](https://blog.csdn.net/u010383937/article/details/72231982)  
- `<ol>` 加粗 标签  
  -- [html - html使ABC有序列表項具有粗體](https://hant-kb.kutu66.com/html/post_12404878)  
  -- [HTML+CSS基础](https://cloud.tencent.com/developer/article/1016715)  
  -- [html的字体标签、列表、表格和表单](https://zhuanlan.zhihu.com/p/26368149)  
  -- [html li加粗](https://cloud.tencent.com/developer/information/html%20li%E5%8A%A0%E7%B2%97)  


## List of Refs

plt.hist 边框  
[matplotlib绘制直方图、条形图和饼图](https://blog.csdn.net/hohaizx/article/details/79101322)  

plt grid 虚线  
[Python绘图库Matplotlib.pyplot之网格线设置 i.e., plt.grid()](https://blog.csdn.net/weixin_41789707/article/details/81035997)  

plt 坐标轴刻度  
[matplotlib命令与格式：pyplot api坐标轴刻度常用命令](https://blog.csdn.net/helunqu2017/article/details/78736415)  
[matplotlib画图系列之设置坐标轴（精度、范围，标签，中文字符显示）](https://blog.csdn.net/weixin_34613450/article/details/81633350)  

plt 坐标轴 右侧上侧 显示刻度  
[Matplotlib中修改坐标轴刻度线的属性](https://blog.csdn.net/HHG20171226/article/details/101289933)  
[Matplotlib中修改坐标轴刻度线的属性](https://zhuanlan.zhihu.com/p/32088843)  
[设置坐标轴2 | 莫烦](https://morvanzhou.github.io/tutorials/data-manipulation/plt/2-4-axis2/)  


plt 刻度 间隔  
[用Python设置matplotlib.plot的坐标轴刻度间隔以及刻度范围](https://www.cnblogs.com/djw12333/p/11049981.html)  
[matplotlib横轴密度修改](https://blog.csdn.net/cdqn10086/article/details/77828609)  
[Python设置matplotlib.plot的坐标轴刻度间隔以及刻度范围](https://www.jb51.net/article/163842.htm)  
[matplotlib命令与格式：pyplot api坐标轴刻度常用命令](https://blog.csdn.net/helunqu2017/article/details/78736415)  

plt marker edgecolor  
[Marker edge color](http://scipy-lectures.org/intro/matplotlib/auto_examples/options/plot_mec.html)  
[matplotlib.pyplot.scatter](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.scatter.html)  

plt grid 间距  
[了解LogLocator中的subs参数](https://xbuba.com/questions/51930055)  
[python - PyPlot-设置绘图的网格线间距](https://www.coder.work/article/1248716)  
[PyPlot - 为绘图设置网格线间距](https://qa.1r1g.com/sf/ask/2133790921/)  
[matplotlib - PyPlot设置 plot的网格线间距](https://kb.kutu66.com/python/post_4418548)  
plt  loglocator 间距  
[如何减少matplotlib对数图上的主刻度线间距](https://www.thinbug.com/q/48403484)  
[matplotlib基础1：绘图基本属性设置 -- xticks(loc,labels)格式化转义标记](https://blog.csdn.net/weixin_40040404/article/details/81185564)  
[数据可视化(matplotilb)](https://www.lagou.com/lgeduarticle/34243.html)  
[客户端码农学习ML —— Matplotlib基本用法](http://qianhk.com/2018/03/%E5%AE%A2%E6%88%B7%E7%AB%AF%E7%A0%81%E5%86%9C%E5%AD%A6%E4%B9%A0ML-Matplotlib%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95/)  
plt  loglocator 刻度间距  
[【matplotlib】设置纵坐标刻度为10^n](https://blog.csdn.net/u012509485/article/details/82895651)  
[【Matplotlib】 刻度设置(2): Tick locating and formatting](https://www.cnblogs.com/nju2014/p/5633768.html)  

table 字体加粗  
[如何在td中控制字体右对齐 且加粗](https://bbs.csdn.net/topics/350167336)  
table 里 列表  
[HTML 表格](https://www.w3school.com.cn/html/html_tables.asp)  
[想用一个列表和table并排，如何让列表里的项优先占满显示?](https://segmentfault.com/q/1010000007049455)  
[HTML 列表 | 菜鸟](https://www.runoob.com/html/html-lists.html)  
[HTML 列表 | W3school](https://www.w3school.com.cn/html/html_lists.asp)  
html 列表 间隔太宽  
[HTML字体行间距太大解决办法！](https://blog.csdn.net/lu12077/article/details/81203538)  
html table 间隔太宽  
[HTML中的属性 1.外间距和2.内间距（详解） （表格属性）](https://blog.csdn.net/Ameir_yang/article/details/60603277)  
[table中设置tr行间距](https://blog.csdn.net/itmyhome1990/article/details/50475616)  


html table 列宽  
[HTML `<td>` 标签的 width 属性](https://www.w3school.com.cn/tags/att_td_width.asp)  
[table以及td宽度设置细节](https://www.jianshu.com/p/0b027c877a0d)  
[html - table 表格不被撑开，td某些列宽度固定某些列自适应](https://www.cnblogs.com/jying/p/6289981.html)  

html table 前大片空白  
[HTML出现异常空格现象(table外,上方出现空白)](https://blog.csdn.net/qq_16552753/article/details/86100423)  
[`<table>`表格大片空白行的问题](https://github.com/ghosert/cmd-editor/issues/868)  
html 浮动体  
[html实现简单的浮动框](https://blog.csdn.net/zhengyikuangge/article/details/90901423)  
[CSS浮动、定位](https://www.jianshu.com/p/c80f18803a17)  
[css浮动(float)及清除浮动的几种实用方法](https://juejin.im/post/5a6feb2af265da3e393ab42d)  
html table 之前 空白  
[使用table标签，会出现大面积空白](https://github.com/iissnan/hexo-theme-next/issues/114)  
[Writing on GitHub](https://help.github.com/en/github/writing-on-github#tables)  
[html table compressed into a row](https://tool.oschina.net/jscompress?type=2)  


matplotlib layout 显示不全  
[matplotlib y轴标注显示不全以及subplot调整的问题](https://www.itdaan.com/blog/2016/12/23/ae75f9a47f32080af31b062d49be7fe9.html)  
[matplotlib 进阶之Tight Layout guide](https://blog.csdn.net/mtandhj/article/details/90300417)  
[matplotlib 进阶之Tight Layout guide](https://blog.csdn.net/weixin_33757911/article/details/94027770)  

np.arctan2 用法  
[numpy.arctan2](http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.arctan2.html)  
[python中 math模块下 atan 和 atan2的区别](https://blog.csdn.net/songyunli1111/article/details/81145971)  

> numpy.arctan2(x1, x2[, out])
> x1/x2 的元素平方倒圆切线正确选择象限。
> 选择象限（即分支）使得 arctan2(x1,x2) 是以弧度原点并通过点 (1,0) ，并且光线在原点结束并通过点 (x2,x1)。（注意角色颠倒：“y -coordinate” 是第一个函数参数，“x -coordinate” 是第二个。根据 IEEE 约定，该函数定义为 x2 = +/- 0，并且 x1 和 x2 = +/- inf （具体值见注）。
> 这个函数没有为复值参数定义；对于复杂值的所谓参数，使用 angle.

plt.pie legend  
[How to add a legend to matplotlib pie chart?](https://stackoverflow.com/questions/19852215/how-to-add-a-legend-to-matplotlib-pie-chart)  
[Labeling a pie and a donut](https://matplotlib.org/3.1.1/gallery/pie_and_polar_charts/pie_and_donut_labels.html)  
[Pie Chart in Python with Legends](http://www.datasciencemadesimple.com/pie-chart-in-python-with-legends/)  

