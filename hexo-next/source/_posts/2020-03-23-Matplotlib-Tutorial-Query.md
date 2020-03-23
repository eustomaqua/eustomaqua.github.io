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
<img src="/images/2020-03/0323_Query_huang4a.png" width="100%">
<img src="/images/2020-03/0323_Query_huang4b.png" width="100%">

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
- r 红色
- g 绿色
- b 蓝色
- c cyan
- m 紫色
- y 土黄色
- k 黑色
- w 白色

### fill style

<img src="/images/2020-03/0323_Query_huang5a.png" width="100%">
<img src="/images/2020-03/0323_Query_huang5b.png" width="100%">

### title 函数
- ```python
  matplotlib.pyplot.title(s, *args, **kwargs)
  ```
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
- ```python
  xscale/yscale(scale, **kwargs)
  ```
  – scale 的 3 种取值：**'linear' | 'log' | 'symlog'**

<img src="/images/2020-03/0323_Query_huang7a.png" width="100%">

#### 在对数坐标系下画图
- ```python
  matplotlib.pyplot.semilogx(*args, **kwargs)
  ```
- ```python
  matplotlib.pyplot.semilogy(*args, **kwargs)
  ```
- ```python
  matplotlib.pyplot.loglog(*args, **kwargs)
  ```
- 参数同 plot (Line2D)
- 注意与前面 xscale/yscale 函数的区别
  - xscale/yscale 只设置坐标系，没有画图功能

#### 自定义坐标
- ```python matplotlib.pyplot.xticks(*args, **kwargs)```
- ` matplotlib.pyplot.yticks(*args, **kwargs)`
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
- ```matplotlib.pyplot.legend(*args, **kwargs)```
  - ```loc: default 0```
  - ```fontsize```
  - ```numpoints```
  - ```shadow```
  - ```bbox_to_anchor```
  - ...

<img src="/images/2020-03/0323_Query_huang8a.png" width="100%">

#### 设置图例背景色和阴影
```python
legend = plt.legend(loc='upper center', shadow=True, fontsize='x-large')
legend.get_frame().set_facecolor('#00FFCC')
```
<img src="/images/2020-03/0323_Query_huang8b.png" width="100%">

#### 把图例放在图片以外的地方
#### 图例分开放置

### 保存图片
- ```matplotlib.pyplot.savefig(*args, **kwargs)```
  - 文件名是必需参数
  - ```plt.savefig(plot_file, bbox_inches='tight')```
    - <font color=red>```bboxinches='tight'```</font> 去掉不需要的白边
    - 输出 ps 格式文件时无法使用这个参数
  - 其他参数
- 如果只想在屏幕上显示出来
  - ```plt.show()```

### 网格开关
- ```python
  matplotlib.pyplot.grid(b=None, which=u'major', axis=u'both',
  **kwargs)
  ```
  - ```b: [True | False]```, 是否打网格，默认反转 b
  - ```which: ['major' | 'minor' | 'both']```, 在哪种坐标处打网格，默认为 ```'major'```
  - ```axis: ['both' | 'x' | 'y']```, 横线和竖线|只竖线|只横线，默认为 ```'both'```
  - 还可使用 ```Line2D``` 中的参数
  - 最简单的使用：```plt.grid()```
  ```

  ```

### 多图

#### 多图

#### 多图的一个例子


### 直方图
#### hist
#### text 函数
#### 直方图与相应折线图
#### bar/barh
#### 使用 bar 的一个例子
#### errorbar 的画法

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
<img src"/images/2020-03/0323_Query_GitHub_quick1.png" width="100%">
### Line styles
<img src"/images/2020-03/0323_Query_GitHub_quick2.png" width="70%">
### [Markers](https://github.com/rougier/matplotlib-tutorial/blob/master/README.rst#markers)
<img src"/images/2020-03/0323_Query_GitHub_quick3.png" width="83%">
### Colormaps 
All colormaps can be reversed by appending ``` _r```. For instance, ```gray_r``` is the reverse of gray. If you want to know more about colormaps, see [Documenting](https://gist.github.com/2719900)
#### Base
<img src"/images/2020-03/0323_Query_GitHub_quick4a.png" width="100%">
#### GIST
<img src"/images/2020-03/0323_Query_GitHub_quick4b.png" width="100%">
#### Sequential
<img src"/images/2020-03/0323_Query_GitHub_quick4c.png" width="100%">
#### Diverging
<img src"/images/2020-03/0323_Query_GitHub_quick4d.png" width="100%">
#### Qualitative
<img src"/images/2020-03/0323_Query_GitHub_quick4e.png" width="100%">
#### Miscellaneous
<img src"/images/2020-03/0323_Query_GitHub_quick4f.png" width="100%">

# * References

  ```

  ```

  ```

  ```

```

```