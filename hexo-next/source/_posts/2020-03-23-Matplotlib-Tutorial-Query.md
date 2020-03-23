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
    - 默认为： ```python
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
  - <table><td bgcolor=#E6E6FA>**plt.savefig(plot_file, <font color=#FF7F50>bbox_inches='tight'</font>)**</td></table>
    - <font color=black>**bboxinches='tight'**</font> 去掉不需要的白边
    - 输出 ps 格式文件时无法使用这个参数
  - 其他参数
- 如果只想在屏幕上显示出来
  - <table><td bgcolor=#E6E6FA>**plt.show()**</td></table>

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
  - <table><td bgcolor=#E6E6FA>**subplot(nrows, ncols, plot\_number)**</td></table>
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
    capsize (errorbar的大小), error_kw, align ('edge' or
    'center'), orientation ('vertical' or 'horizontal'), log
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

### subplots 与 axes 的区别

### 第一个例子

### figure 类

### axes 类

### axis 的一些应用

### 一个例子


## 用 pylab 模块快速画图
类似于第一种方法




# Matplotlib tutorial: [<font color=#00FF7F>ref</font>](https://github.com/rougier/matplotlib-tutorial)


## Introduction

### IPython and the pylab mode

### pyplot

## Simple plot

### Using defaults
### Instantiating defaults
### Changing colors and line widths
### Setting limits
### Setting ticks
### Setting tick labels
### Moving spines
### Adding a legend
### Annotate some points
### Devil is in the details

## Figures, Subplots, Axes and Ticks

### Figures
### Subplots
### Axes
### Ticks
#### Tick Locators

## Animation

### Drip drop
### Earthquakes

## Other Types of Plots

### Regular Plots
### Scatter Plots
### Bar Plots
### Contour Plots
### Imshow
### Pie Charts
### Quiver Plots
### Grids
### Multi Plots
### Polar Axis
### 3D Plots
### Text

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

## Useful

[Matplotlib中修改坐标轴刻度线的属性](https://blog.csdn.net/HHG20171226/article/details/101289933)  


## List

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


