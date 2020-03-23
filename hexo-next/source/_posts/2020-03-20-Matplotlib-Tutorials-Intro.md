---
title: Matplotlib Tutorials - 1. Introductory
date: 2020-03-20 23:20:29
updated: 
categories:
  - Drafting
tags:
  - Python
  - Matplotlib
  - Notes
---

[TOC]

References:  
[matplotlib.pyplot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.html)  
[Tutorials](https://matplotlib.org/3.1.1/tutorials/index.html)  
[Matplotlib 使用教程](http://www.bioinfo.org.cn/~casp/temp/spring.lecture/Matplotlib_slides.pdf)  
[matplotlib的backend浅析](http://vra.github.io/2017/06/13/mpl-backend/)  
[RGB 颜色对照表](https://tool.oschina.net/commons?type=3)  

[matplotlib调整子图间距，调整整体空白](https://blog.csdn.net/GAN_player/article/details/78543643)  
[4.9Python数据处理篇之Matplotlib系列(九)---子图分布](https://www.cnblogs.com/zyg123/p/10517711.html)  
[指定颜色](https://www.osgeo.cn/matplotlib/tutorials/colors/colors.html)  
[在Matplotlib绘图中添加Latex风格公式](https://www.cnblogs.com/chaosimple/p/4031421.html)  



***Tutorials: Introductory***

# User Guide

通用概念  
```python
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
# import numpy as np
```

图片的各个组成部分  
![Parts of a Figure](https://matplotlib.org/3.1.1/_images/anatomy.png)  

Types of inputs to plotting functions  
```python
>>> import pandas as pd
>>> import numpy as np
>>> 
>>> a = pd.DataFrame(np.random.rand(4,5), columns=list('abcde'))
>>> a
          a         b         c         d         e
0  0.777797  0.368171  0.816256  0.821103  0.922983
1  0.350432  0.771138  0.764347  0.550587  0.009030
2  0.544528  0.328576  0.814329  0.148863  0.801908
3  0.662106  0.542827  0.143121  0.746108  0.104796
>>> a.values
array([[0.77779745, 0.3681715 , 0.8162556 , 0.82110297, 0.922983  ],
       [0.35043196, 0.7711383 , 0.7643467 , 0.55058725, 0.00903032],
       [0.54452813, 0.32857608, 0.81432872, 0.14886258, 0.80190761],
       [0.66210608, 0.54282728, 0.14312097, 0.74610766, 0.10479626]])
>>>
>>> b = np.matrix(np.random.rand(2,2))
>>> b
matrix([[0.59049461, 0.11964552],
        [0.79433021, 0.71548013]])
>>> np.asarray(b)
array([[0.59049461, 0.11964552],
       [0.79433021, 0.71548013]])
```

一个简单的例子  
```python
x = np.linspace(0, 2, 100)  # shape: (100,)

plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')

plt.xlabel('x label')
plt.ylabel('y label')

plt.title("Simple Plot")

plt.legend()

plt.show()
```
![User Guide: Simple Plot](https://matplotlib.org/3.1.1/_images/sphx_glr_usage_003.png)  

## 性能 Performance

无论是以交互方式浏览数据还是以编程方式保存大量绘图，渲染性能都可能成为管道中的一个痛苦瓶颈。 Matplotlib提供了几种方法，以稍微改变绘制外观（达到可设置的公差）为代价，大大减少了渲染时间。减少渲染时间的可用方法取决于所创建绘图的类型。

### **Line segment simplification** 线段简化  
对于具有线段的图（例如，典型的线图，多边形的轮廓等），可以通过matplotlibrc文件中的path.simplify和path.simplify_threshold参数来控制渲染性能（有关更多信息，请参见有关matplotlibrc文件，使用样式表和rcParams来自定义Matplotlib）。 path.simplify参数是一个布尔值，指示是否完全简化线段。 path.simplify_threshold参数控制简化的线段数量；阈值越高，渲染越快。  
以下脚本将首先显示数据而不进行任何简化，然后以简化方式显示相同的数据。尝试与他们两个进行交互：  

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib as mpl

# Setup, and create the data to plot
y = np.random.rand(100000)
y[50000:] *= 2
y[np.logspace(1, np.log10(50000), 400).astype(int)] = -1
mpl.rcParams['path.simplify'] = True

mpl.rcParams['path.simplify_threshold'] = 0.0
plt.plot(y)
plt.show()

mpl.rcParams['path.simplify_threshold'] = 1.0
plt.plot(y)
plt.show()
```

Matplotlib当前默认为保守简化阈值1/9。如果要更改默认设置以使用其他值，则可以更改matplotlibrc文件。另外，您可以创建一种新样式（用于最大程度简化）进行交互式绘图，并创建另一种样式（用于最小程度进行简化）的出版物质量绘图，并根据需要激活它们。有关如何执行这些操作的说明，请参见使用样式表和rcParams自定义Matplotlib。  
通过将线段迭代合并为单个矢量，直到下一个线段到矢量的垂直距离（在显示坐标空间中测量）大于path.simplify_threshold参数，简化了工作。  
注意：在版本2.1中进行了有关简化线段的更改。在2.1之前的版本中，这些参数仍将改善渲染时间，但是在2.1及更高版本中，某些类型数据的渲染时间将得到极大的改善。

### **Marker simplification** 标记简化  
标记也可以简化，尽管不如线段健壮。简化标记仅适用于Line2D对象（通过markevery属性）。传递Line2D构造参数的任何地方（例如matplotlib.pyplot.plot()和matplotlib.axes.Axes.plot()），都可以使用markevery参数：

```python
plt.plot(x，y，markevery = 10)
```

markevery参数允许进行简单的二次采样，或尝试均匀间隔（沿x轴）采样。有关更多信息，请参见Markevery演示。

### **Splitting lines into smaller chunks** 将行分成较小的块  
如果使用的是Agg后端（请参阅什么是后端？），则可以使用agg.path.chunksize rc参数。这使您可以指定块的大小，任何大于多个顶点的线都将被拆分为多行，每行最多包含agg.path.chunksize个顶点。 （除非agg.path.chunksize为零，否则不进行分块。）对于某些类型的数据，将行分块为合理的大小可以大大减少渲染时间。

以下脚本将首先显示没有任何块大小限制的数据，然后显示块大小为10,000的相同数据。当数字很大时，最好看到最大的区别，请尝试最大化GUI并与之交互：

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib as mpl
mpl.rcParams['path.simplify_threshold'] = 1.0

# Setup, and create the data to plot
y = np.random.rand(100000)
y[50000:] *= 2
y[np.logspace(1,np.log10(50000), 400).astype(int)] = -1
mpl.rcParams['path.simplify'] = True

mpl.rcParams['agg.path.chunksize'] = 0
plt.plot(y)
plt.show()

mpl.rcParams['agg.path.chunksize'] = 10000
plt.plot(y)
plt.show()
```

### **Legends** 图例  
轴的默认图例行为会尝试查找覆盖最少数据点的位置（loc = "best"）。 如果有很多数据点，这可能是非常昂贵的计算。 在这种情况下，您可能需要提供一个特定的位置。

### **Using the *fast* style** 使用快速样式  
快速样式可用于将简化和分块参数自动设置为合理的设置，以加快绘制大量数据的速度。 只需运行以下命令即可使用它：

```python
import matplotlib.style as mplstyle
mplstyle.use('fast')
```

它的重量很轻，因此可以与其他样式很好地配合，只要确保最后应用快速样式即可，这样其他样式就不会覆盖设置：

```python
mplstyle.use(['dark_background', 'ggplot', 'fast'])
```


# Pyplot tutorial

```python
plt.plot([1, 2, 3, 4], 'ro')  # plot: y = [1,2,3,4], x = [0, len(y)-1]
plt.plot([1, 2, 3, 4], [1, 4, 9, 16])  # plot: x, y
plt.axis([0, 6, 0, 20])  # [xmin, xmax, ymin, ymax]

t = np.arange(0., 5., 0.2)  # [0., 0.2, ..., 4.8]  shape=(25,)
plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_004.png)  

## Formatting the style of your plot
line styles and format strings [plot()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)  

**Format Strings** 格式字符串 通常由 color, marker, line 组成，如
```python
fmt = '[marker][line][color]'
```
也支持其他形式如 [color][marker][line] ，但是可能会存在歧义。

**Markers**
<img src="/images/2020-03/20200320_Pyplot1a.png" width="50%">

**Line Styles**
<img src="/images/2020-03/20200320_Pyplot1b.png" width="50%">

**Colors**
<img src="/images/2020-03/20200320_Pyplot1c.png" width="100%">

## Controlling line properties

Lines 有许多可以设置的属性，如 linewidth, dash style, antialiased 等 [see matplotlib.lines.Line2D](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)  
设置方法：  
1. keyword args
```python
plt.plot(x, y, linewidth=2.0)
```
2. setter methods
```python
line, = plt.plot(x, y, '-')
line.set_antialiased(False)  # turn off antialiasing
```
3. 'setp()' command
```python
lines = plt.plot(x1, y1, x2, y2)
# use keyword args
plt.setp(lines, color='r', linewidth=2.0)
# or MATLAB style string value pairs
plt.setp(lines, 'color', 'r', 'linewidth', 2.0)
```

## Plotting with keyword strings

```python
data = {'a': np.arange(50),
        'c': np.random.randint(0, 50, 50),
        'd': np.random.randn(50)}
data['b'] = data['a'] + 10 * np.random.randn(50)
data['d'] = np.abs(data['d']) * 100

plt.scatter('a', 'b', c='c', s='d', data=data)
plt.xlabel('entry a')
plt.ylabel('entry b')
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_005.png)  

其中 c 参数代表颜色，s 代表标记大小 marker size，即 [plt.scatter()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.scatter.html#matplotlib.pyplot.scatter)

## Plotting with categorical variables

```python
names = ['group_a', 'group_b', 'group_c']
values = [1, 10, 100]
plt.figure(figsize=(9, 3))

plt.subplot(131)
plt.bar(names, values)
plt.subplot(132)
plt.scatter(names, values)
plt.subplot(133)
plt.plot(names, values)
plt.suptitle('Categorical Plotting')
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_006.png)

## Working with multiple figures and axes

```python
def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

plt.figure()
plt.subplot(211)
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')

plt.subplot(212)
plt.plot(t2, np.cos(2*np.pi*t2), 'r--')
plt.show()

def hb(t):
    return np.exp(-t) * np.sin(2 * np.pi * t)
def ha(t):
    return np.exp(t) * np.sin(2 * np.pi * t)
def hc(t):
    return np.exp(t) * np.cos(2 * np.pi * t)

fig = plt.figure(figsize=(11.5, 6.7))
plt.subplot(325)
plt.plot(t2, np.cos(2 * np.pi * t2), 'r--', label='cos')
plt.legend()
plt.subplot(326)
plt.plot(t2, np.sin(2 * np.pi * t2), 'r--', label='sin')
plt.legend()

plt.subplot(323)
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')
plt.title(r'$\exp(-t)\cdot\cos(2\pi t)$')
plt.subplot(324)
plt.plot(t1, hb(t1), 'bo', t2, hb(t2), 'k')
plt.title(r'$\exp(-t)\cdot\sin(2\pi t)$')

plt.subplot(321)
plt.plot(t1, hc(t1), 'bo', t2, hc(t2), 'k')
plt.title(r'$\exp(t)\cdot\cos(2\pi t)$')
plt.subplot(322)
plt.plot(t1, ha(t1), 'bo', t2, ha(t2), 'k')
plt.title(r'$\exp(t)\cdot\sin(2\pi t)$')

plt.tight_layout()  # fig.tight_layout()
plt.show()
```
<img src="/images/2020-03/20200320_Pyplot2b.png" width="100%">

您可以使用 clf() 清除当前图形，并使用 cla() 清除当前轴。如果您发现在后台为您维护状态（特别是当前图像，图形和轴）很烦人，请不要绝望：这只是面向对象API的薄状态包装，您可以使用它（参见艺术家教程）  
如果要制作大量图形，则还需要注意一件事：在使用 close() 显式关闭图形之前，图形所需的内存不会完全释放。删除对图形的所有引用，和/或使用窗口管理器杀死图形在屏幕上出现的窗口是不够的，因为pyplot会保留内部引用，直到调用 close() 为止。

## Working with text

```python
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

# the histogram of the data
n, bins, patches = plt.hist(x, 50, density=1, facecolor='g', alpha=0.75)

plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title('Histogram of IQ')
plt.text(60, .025, r'$\mu=100,\ \sigma=15$')
plt.axis([40, 160, 0, 0.03])
plt.grid(True)
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_008.png)

自定义 text() 的性质 [matplotlib.text.Text](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_008.png)  
[Text properties and layout](https://matplotlib.org/3.1.1/tutorials/text/text_props.html)  
可类似用 keyword arguments 或 setp() 的方式来设置其属性，如  
```python
t = plt.xlabel('my data', fontsize=14, color='red')
```

**Using mathematical expressions in text** 使用数学表达式  
```python
plt.title(r'$\sigma_i=15$')
```

**Annotating text** 批注/注释  
```python
ax = plt.subplot(111)

t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2 * np.pi * t)
line, = plt.plot(t, s, lw=2)

plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
            arrowprops=dict(facecolor='black', shrink=0.05),)

plt.ylim(-2, 2)
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_009.png)

[Basic annotation](https://matplotlib.org/3.1.1/tutorials/text/annotations.html#annotations-tutorial)  
[Advanced Annotation](https://matplotlib.org/3.1.1/tutorials/text/annotations.html#plotting-guide-annotation)  
[Annotating Plots](https://matplotlib.org/3.1.1/tutorials/text/annotations.html#plotting-guide-annotation)  

## **Logarithmic and other nonlinear axes** 对数和其他非线性轴  

[matplotlib.pyplot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot) 支持线性轴尺度 (linear axis scales)、对数和逻辑斯特回归轴 (logarithmic and logit scales)、以及 symmetric log (symlog)  
改变坐标轴尺度很简单，只需要  
```python
plt.xscale('log')  # {"linear", "log", "symlog", "logit"}
```
示例图形：
[Symlog Demo](https://matplotlib.org/3.1.1/gallery/scales/symlog_demo.html#sphx-glr-gallery-scales-symlog-demo-py) 
[Pyplot Scales](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_scales.html#sphx-glr-gallery-pyplots-pyplot-scales-py)

### Pyplot Scales

```python
from matplotlib.ticker import NullFormatter  # useful for 'logit' scale

# Fixing random state for reproducibility
np.random.seed(19680801)

# make up some data in the interval [0, 1]
y = np.random.normal(loc=0.5, scale=0.4, size=1000)
y = y[(y > 0) & (y < 1)]
y.sort()

x = np.arange(len(y))

# plot with various axes scales
plt.figure()

# linear
plt.subplot(221)
plt.plot(x, y)
plt.plot(x, y - y.mean(), 'r')
plt.yscale('linear')
plt.title('linear')
plt.grid(True)

# log
plt.subplot(222)
plt.plot(x, y)
plt.plot(x, y - y.mean(), 'r')
plt.yscale('log')
plt.title('log')
plt.grid(True)

# symmetric log
plt.subplot(223)
plt.plot(x, y - y.mean())
plt.plot(x, y, 'g')
plt.yscale('symlog', linthreshy=0.01)
# plt.yscale('symlog', lintreshy=0.1)
plt.title('symlog')
plt.grid(True)

# logit
plt.subplot(224)
plt.plot(x, y)
plt.plot(x, y - y.mean(), 'r')
plt.yscale('logit')
plt.title('logit')
plt.grid(True)
# Format the minor tick labels of the y-axis into empty strings with
# `NullFormatter`, to avoid cumbering the axis with too many labels.
plt.gca().yaxis.set_minor_formatter(NullFormatter())
# Adjust the subplot layout, because the logit one may take more space
# than usual, due to y-tick labels like "1 - 10^{-3}"
plt.subplots_adjust(top=0.92, bottom=0.08, left=0.10, right=0.95, hspace=0.25,
                    wspace=0.35)

plt.show()
```
<img src="/images/2020-03/20200320_Pyplot3a.png" width="100%">

### Symlog Demo

```python
dt = 0.01
x = np.arange(-50.0, 50.0, dt)
y = np.arange(0, 100.0, dt)

plt.subplot(221)#311)
plt.plot(x, y)
plt.xscale('symlog')
plt.ylabel('symlogx')
plt.grid(True)
plt.gca().xaxis.grid(True, which='minor')  # minor grid on too

plt.subplot(222)#312)
plt.plot(y, x)
plt.yscale('symlog')
plt.ylabel('symlogy')

plt.subplot(223)#313)
plt.plot(x, np.sin(x / 3.0))
plt.xscale('symlog')
plt.yscale('symlog', linthreshy=0.015)
plt.grid(True)
plt.ylabel('symlog both')

plt.subplot(224)
plt.plot(x, y)
plt.grid(True)
plt.ylabel('linear both')

plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/20200320_Pyplot3b.png" width="100%">


# Sample plots in Matplotlib

详见另一篇

# Image tutorial

1. Startup commands
2. Importing image data into Numpy arrays
3. Plotting numpy arrays as images
  - Applying pseudocolor schemes to image plots
  - Color scale reference
  - Examining a specific data range
  - Array Interpolation schemes

```python
# %matplotlib inline
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

# img = mpimg.imread('../../doc/_static/stinkbug.png')
img = mpimg.imread('./cat.jpg')
print(img)  # ndarray, uint8

imgplot = plt.imshow(img)
plt.show()

lum_img = img[:, :, 0]
# This is array slicing.  You can read more in the `Numpy tutorial
# <https://docs.scipy.org/doc/numpy/user/quickstart.html>`_.
plt.imshow(lum_img)
plt.show()
```
<img src="/images/2020-03/20200320_Image1a.png" width="70%">

## **Applying pseudocolor schemes to image plots**  
```python
plt.figure(figsize=(17, 2))#)
plt.subplot(141)#221)
plt.imshow(img)
plt.title('Original Image')
plt.subplot(142)#222)
plt.imshow(img[:, :, 0])
plt.title('img[:, :, 0]')

plt.subplot(143)#223)
plt.imshow(img[:, :, 1])
plt.title('img[:, :, 1]')
plt.subplot(144)#224)
plt.imshow(img[:, :, 2])
plt.title('img[:, :, 2]')
plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/20200320_Image1c.png" width="100%">

## **Color scale reference**  
i.e., colorbar()  
```python
plt.figure(figsize=(20, 2))
plt.subplot(151)
plt.imshow(img)
plt.title('Original Image')

plt.subplot(152)
plt.imshow(lum_img)
plt.title('lum_img = img[:, :, 0]')

plt.subplot(153)
plt.imshow(lum_img, cmap="hot")
plt.title('lum_img, cmap="hot"')

plt.subplot(154)
imgplot = plt.imshow(lum_img)
imgplot.set_cmap('nipy_spectral')
plt.title('lum_img, set_cmap, nipy_spectral')

plt.subplot(155)
imgplot = plt.imshow(lum_img)
plt.colorbar()
plt.title('lum_img, colorbar()')

plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/20200320_Image1d.png" width="100%">

## **Examining a specific data range**  

```python
img = mpimg.imread('./Matplotlib/cat.jpg')
print(img)  # ndarray, uint8
lum_img = img[:, :, 0]

fig = plt.figure(figsize=(13, 7)) #10, 5))
plt.subplot2grid((3,4), (0,0), colspan=1,rowspan=1)
plt.imshow(img)
plt.title('Original img')
plt.subplot2grid((3,4), (0,1), colspan=1,rowspan=1)
plt.imshow(lum_img)
plt.title('lum_img = img[:,:,0]')

plt.subplot2grid((3,4), (0,2), colspan=1,rowspan=1)
plt.imshow(img / 256.)
plt.subplot2grid((3,4), (0,3), colspan=1,rowspan=1)
plt.imshow(lum_img / 256.)

plt.subplot2grid((3,4), (1,0), colspan=2,rowspan=2)
plt.hist(lum_img.ravel() / 256, bins=256, range=(0.0, 1.0), fc='k', ec='k')
plt.title('A good tool to find interesting regions is the histogram.')
plt.subplot2grid((3,4), (1,2), colspan=1,rowspan=2)
plt.plot(lum_img.ravel() / 256, '.')

plt.subplot2grid((3,4), (1,3), colspan=1,rowspan=1)
imgplot = plt.imshow(lum_img / 256., clim=(0.0, 0.7))
plt.title('Specify the clim in the call to plot')
plt.subplot2grid((3,4), (2,3), colspan=1,rowspan=1)
plt.imshow(lum_img / 256.)

plt.show()
```
<img src="/images/2020-03/20200320_Image2a.png" width="100%">

```python
# img e.g. ...[210, 208, 209]]], dtype=uint8)
fig = plt.figure()
a = fig.add_subplot(2, 2, 1)
imgplot = plt.imshow(lum_img)
a.set_title('Before')
plt.colorbar(ticks=[0.1, 0.3, 0.5, 0.7], orientation='horizontal')
a = fig.add_subplot(2, 2, 2)
imgplot = plt.imshow(lum_img)
imgplot.set_clim(0.0, 0.7)
a.set_title('After')
plt.colorbar(ticks=[0.1, 0.3, 0.5, 0.7], orientation='horizontal')

lum_img = lum_img / 256.
b = fig.add_subplot(2, 2, 3)
imgplot = plt.imshow(lum_img)
b.set_title('Before')
plt.colorbar(ticks=[0.1, 0.3, 0.5, 0.7], orientation='horizontal')
b = fig.add_subplot(2, 2, 4)
imgplot = plt.imshow(lum_img)
imgplot.set_clim(0.0, 0.7)
b.set_title('After')
plt.colorbar(ticks=[0.1, 0.3, 0.5, 0.7], orientation='horizontal')

plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/20200320_Image2b.png" width="100%">

## **Array Interpolation schemes**  

插值根据不同的数学方案计算“应该”像素的颜色或值。 发生这种情况的一个常见地方是调整图像大小时。 像素数会变化，但是您需要相同的信息。 由于像素是离散的，因此缺少空间。 插值法是您填充该空间的方式。 这就是为什么当您炸毁图像时有时会显得像素化的原因。 当原始图像和扩展图像之间的差异更大时，效果会更加明显。 让我们来缩小形象。 我们实际上是在丢弃像素，只保留少数像素。 现在，当我们绘制它时，该数据将爆炸到屏幕上的大小。 旧的像素不再存在，计算机必须提取像素来填充该空间。  
我们将使用用于加载图像的Pillow库来调整图像的大小。

```python
from PIL import Image
img = Image.open('./Matplotlib/cat.jpg')
img.thumbnail((64, 64), Image.ANTIALIAS)  # resizes image in-place
imgplot = plt.imshow(img)

# Image.open:
# <PIL.JpegImagePlugin.JpegImageFile image mode=RGB size=340x148 at 0x..>
# img.thumbnail:
# <PIL.JpegImagePlugin.JpegImageFile image mode=RGB size=64x27 at 0x..>
plt.show()
```
<img src="/images/2020-03/20200320_Image3a.png" width="70%">

由于没有给imshow()任何插值参数，因此这里有默认的插值法，即双线性。  
让我们尝试其他一些。 如“最近”，即不进行插值。  
```python
imgplot = plt.imshow(img, interpolation="nearest")
```

和 bicubic  
```python
imgplot = plt.imshow(img, interpolation="bicubic")
```
放大照片时经常使用双三次插值法-人们倾向于模糊而不是像素化。  


```python
fig = plt.figure(figsize=(14, 7.5))
plt.subplot(221)
img = Image.open('./cat.jpg')
plt.imshow(img)
plt.title('RGB 340x148')
plt.subplot(222)
img.thumbnail((64, 64), Image.ANTIALIAS)  # resizes image in-place
imgplot = plt.imshow(img)
plt.title('RGB 64x27')
plt.subplot(223)
plt.imshow(img, interpolation="nearest")
plt.title("interpolation: nearest")
plt.subplot(224)
plt.imshow(img, interpolation="bicubic")
plt.title("interpolation: bicubic")
plt.show()
```
<img src="/images/2020-03/20200320_Image3d.png" width="100%">


# The Lifecycle of a plot

```python
# coding: utf8
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.ticker import FuncFormatter

# Our data
data = {'Barton LLC': 109438.50,
        'Frami, Hills and Schmidt': 103569.59,
        'Fritsch, Russel and Anderson': 112214.71,
        'Jerde-Hilpert': 112591.43,
        'Keeling LLC': 100934.30,
        'Koepp Ltd': 103660.54,
        'Kulas Inc': 137351.96,
        'Trantow-Barrows': 123381.38,
        'White-Trantow': 135841.99,
        'Will LLC': 104437.60}
group_data = list(data.values())
group_names = list(data.keys())
group_mean = np.mean(group_data)

# Getting started
## fig, ax = plt.subplots()
## plt.show()

fig, ax = plt.subplots()
ax.barh(group_names, group_data)
plt.show()

# Controlling the style
print(plt.style.available)

plt.style.use('fivethirtyeight')
fig, ax = plt.subplots()
ax.barh(group_names, group_data)
plt.show()
```
['bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'seaborn', 'Solarize_Light2', 'tableau-colorblind10', '_classic_test']

## Customizing the plot
```
# Customizing the plot
fig, ax = plt.subplots()
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')
plt.show()

plt.rcParams.update({'figure.autolayout': True})
fig, ax = plt.subplots()
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')
plt.show()

fig, ax = plt.subplots()
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')
ax.set(xlim=[-10000, 140000], xlabel='Total Revenue', ylabel='Company',
       title='Company Revenue')
plt.show()

fig, ax = plt.subplots(figsize=(8, 4))
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')
ax.set(xlim=[-10000, 140000], xlabel='Total Revenue', ylabel='Company',
       title='Company Revenue')
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_lifecycle_008.png)

```python
def currency(x, pos):
    """The two args are the value  and tick position"""
    if x >= 1e6:
        s = '${:1.1f}M'.format(x*1e-6)
    else:
        s = '${:1.0f}K'.format(x*1e-3)
    return s

formatter = FuncFormatter(currency)

fig, ax = plt.subplots(figsize=(6, 8))
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')

ax.set(xlim=[-10000, 140000], xlabel='Total Revenue', ylabel='Company',
       title='Company Revenue')
ax.xaxis.set_major_formatter(formatter)
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_lifecycle_009.png)

## Combining multiple visualizations

```python
plt.style.use('fivethirtyeight')
plt.rcParams.update({'figure.autolayout': True})

fig, ax = plt.subplots(figsize=(8, 8))
ax.barh(group_names, group_data)
labels = ax.get_xticklabels()
plt.setp(labels, rotation=45, horizontalalignment='right')

# Add a vertical line, here we set the style in the function call
ax.axvline(group_mean, ls='--', color='r')

# Annotate new companies
for group in [3, 5, 8]:
    ax.text(145000, group, "New Company", fontsize=10,
            verticalalignment="center")

# Now we'll move our title up since it's getting a little cramped
ax.title.set(y=1.05)

ax.set(xlim=[-10000, 140000], xlabel='Total Revenue', ylabel='Company',
       title='Company Revenue')
ax.xaxis.set_major_formatter(formatter)
ax.set_xticks([0, 25e3, 50e3, 75e3, 100e3, 125e3])
fig.subplots_adjust(right=.1)

# plt.savefig('20200320_Lifecycle3.png', dpi=300)
plt.show()
```
![](https://matplotlib.org/3.1.1/_images/sphx_glr_lifecycle_010.png)

3a. plt.setp() 
<img src="/images/2020-03/20200320_Lifecycle3a.png" width="50%">  
3b. ax.axvline() 
<img src="/images/2020-03/20200320_Lifecycle3b.png" width="50%">  
3c. for group in 
<img src="/images/2020-03/20200320_Lifecycle3c.png" width="50%">  
3d. ax.title
<img src="/images/2020-03/20200320_Lifecycle3d.png" width="50%">  
3e. ax.set 
<img src="/images/2020-03/20200320_Lifecycle3e.png" width="50%">  
3f. ax.xaxis 
<img src="/images/2020-03/20200320_Lifecycle3f.png" width="50%">  
3g. ax.set_xticks 
<img src="/images/2020-03/20200320_Lifecycle3g.png" width="50%">  

## Saving our plot

现在我们对绘图的结果感到满意，我们希望将其保存到磁盘。 我们可以在Matplotlib中保存许多文件格式。 要查看可用选项的列表，请使用：  
```python
print(fig.canvas.get_supported_filetypes())
```

> **fig** 
> Figure size 800x800 with 1 Axes
> 
> **fig.canvas**
> <matplotlib.backends.backend_qt5agg.FigureCanvasQTAgg object at Ox...>
>
> **fig.canvas.get_supported_filetypes()**
> {'eps': 'Encapsulated Postscript', 'jpeg': 'Joint Photographic ...rts Group', 'jpg': 'Joint Photographic ...rts Group', 'pdf': 'Portable Document Format', 'pgf': 'PGF code for LaTeX', 'png': 'Portable Network Graphics', 'ps': 'Postscript', 'raw': 'Raw RGBA bitmap', 'rgba': 'Raw RGBA bitmap', 'svg': 'Scalable Vector Graphics', 'svgz': 'Scalable Vector Graphics', 'tif': 'Tagged Image File Format', 'tiff': 'Tagged Image File Format'}
>
> **fig.canvas.get_supported_filetypes_grouped()**
> {'Encapsulated Postscript': ['eps'], 'Joint Photographic ...rts Group': ['jpeg', 'jpg'], 'PGF code for LaTeX': ['pgf'], 'Portable Document Format': ['pdf'], 'Portable Network Graphics': ['png'], 'Postscript': ['ps'], 'Raw RGBA bitmap': ['raw', 'rgba'], 'Scalable Vector Graphics': ['svg', 'svgz'], 'Tagged Image File Format': ['tif', 'tiff']


然后，我们可以使用Figure.Figure.savefig()来将图形保存到磁盘。 请注意，我们将在下面显示几个有用的标志：  
- transparent = True ，如果格式支持，则使保存的图形的背景透明。
- dpi = 80 ，控制输出的分辨率（每平方英寸的点数）。
- bbox_inches = “tight" ，使图形的边界适合我们的绘图。

```python
# Uncomment this line to save the figure.
# fig.savefig('sales.png', transparent=False, dpi=80, bbox_inches="tight")
```


# Customizing Matplotlib with style

[Tips for customizing the properties and default styles of Matplotlib.](https://matplotlib.org/3.1.1/tutorials/introductory/customizing.html#sphx-glr-tutorials-introductory-customizing-py)  

## Customizing Matplotlib with style sheets and rcParams 

### Using style sheets

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib as mpl
plt.style.use('ggplot')
data = np.random.randn(50)

print(plt.style.available)
# ['bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'seaborn', 'Solarize_Light2', 'tableau-colorblind10', '_classic_test']
```

### Defining your own style

可以创建自定义样式并使用样式表的路径或URL调用style.use来使用它们。 此外，如果将 <style-name>.mplstyle 文件添加到 mpl_configdir/stylelib ，则可以通过调用 style.use(<style-name>) 重用自定义样式表。 默认情况下，mpl_configdir 应该为 ~/.config/matplotlib ，但也可以使用matplotlib.get_configdir() 来检查您的位置。 您可能需要创建此目录。 您还可以通过设置 MPLCONFIGDIR 环境变量来更改 matplotlib 在其中查找 stylelib/ 文件夹的目录，请参见 matplotlib 配置和缓存目录位置。  
请注意，如果样式具有相同的名称，则 mpl_configdir/stylelib 中的自定义样式表将覆盖由 matplotlib 定义的样式表。  
例如，您可能要使用以下命令创建 mpl_configdir/stylelib/presentation.mplstyle：  
```txt
axes.titlesize : 24
axes.labelsize : 20
lines.linewidth : 3
lines.markersize : 10
xtick.labelsize : 16
ytick.labelsize : 16
```

例如我的原默认目录为：  
```python
>>> import matplotlib as mpl
>>> mpl.get_configdir()
'C:\\Users\\Lenovo\\.matplotlib'
```
<img src="/images/2020-03/20200320_Stylesheet1a.png" width="80%">  
<img src="/images/2020-03/20200320_Stylesheet1b.png" width="80%">  

创建后即可使用  
<img src="/images/2020-03/20200320_Stylesheet1c.png" width="80%">  

```python
# Defining your own style
>>> import matplotlib.pyplot as plt
>>> plt.style.use('presentation')
```

### Composing styles

```python
>>> import matplotlib.pyplot as plt
>>> plt.style.use(['dark_background', 'presentation'])
```

### Temporary styling

如果您只想为特定的代码块使用样式，而又不想更改全局样式，则样式包提供了一个上下文管理器，用于将更改限制在特定范围内。 为了隔离样式更改，您可以编写如下内容：  
```python
# Temporary styling
with plt.style.context('dark_background'):
    plt.plot(np.sin(np.linspace(0, 2 * np.pi)), 'r-o')
plt.show()
```
<!--![](https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_001.png)-->
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_001.png" width="57%">

## matplotlib rcParams

**Important**  
下面两种改法其实只能改变 lines.linewidth ，改变不了 lines.color  
若想改变 lines.color ，需要 [matplotlib.rcParams](https://matplotlib.org/3.1.1/api/matplotlib_configuration_api.html#matplotlib.rcParams)  
```python
>>> type(mpl.rcParams)
<class 'matplotlib.RcParams'>
>>> for k,v in mpl.rcParams.items():
...     if k.startswith('lines'):
...             print('{:20s} {}'.format(k, v))
...
lines.antialiased     True
lines.color           C0
lines.dash_capstyle   butt
lines.dash_joinstyle  round
lines.dashdot_pattern [6.4, 1.6, 1.0, 1.6]
lines.dashed_pattern  [3.7, 1.6]
lines.dotted_pattern  [1.0, 1.65]
lines.linestyle       -
lines.linewidth       1.5
lines.marker          None
lines.markeredgewidth 1.0
lines.markersize      6.0
lines.scale_dashes    True
lines.solid_capstyle  projecting
lines.solid_joinstyle round
>>>
>>> mpl.rcParams['lines.color']
'C0'
>>> type(mpl.rcParams['lines.color'])
<class 'str'>
```
这是 "CN”颜色规格，即 'C' 后跟一个数字，这是默认属性循环的索引 (matplotlib.rcParams['axes.prop_cycle'] ）；索引发生在艺术家创建时，如果循环不包括颜色，则默认为黑色。

```python
>>> mpl.rcParams['axes.prop_cycle']
cycler('color', ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd', '#8c564b', '#e377c2', '#7f7f7f', '#bcbd22', '#17becf'])

data = np.random.randn(50)

mpl.rcParams['lines.linewidth'] = 8
mpl.rcParams['lines.color'] = 'C4'
plt.plot(data)
plt.show()

mpl.rc('lines', linewidth=4, color='C0')
plt.plot(data)
plt.show()

th = np.linspace(0, 2*np.pi, 128)


def demo(sty):
    mpl.style.use(sty)
    fig, ax = plt.subplots(figsize=(3, 3))

    ax.set_title('style: {!r}'.format(sty), color='C0')

    ax.plot(th, np.cos(th), 'C1', label='C1')
    ax.plot(th, np.sin(th), 'C2', label='C2')
    ax.legend()
    plt.show()

demo('default')
demo('seaborn')
```
用下面的 demo 确认了 C1--C9 与 C0 并不相同，确认了 mpl.rcParams['lines.color'] 确实无法起到作用。**参考**  
[指定颜色](https://www.osgeo.cn/matplotlib/tutorials/colors/colors.html)  

其他备用：  
[matplotlib颜色表](https://www.jianshu.com/p/d0b789ba5be9)  
[Python-Matplotlib 9 颜色和样式](https://www.cnblogs.com/zsr0401/p/6405677.html)  
[python中matplotlib的颜色及线条控制](https://www.cnblogs.com/darkknightzh/p/6117528.html)  

另外备注：  
```python
fig.tight_layout() # 调整整体空白
plt.subplots_adjust(wspace =0, hspace =0) # 调整子图间距
```

### Dynamic rc settings

您还可以在python脚本中动态更改默认的rc设置，或者从python shell交互式更改默认的rc设置。 所有的rc设置都存储在类似字典的变量matplotlib.rcParams中，该变量是matplotlib软件包的全局变量。 rcParams可以直接修改，例如：  
```python
mpl.rcParams['lines.linewidth'] = 2
mpl.rcParams['lines.color'] = 'r'
plt.plot(data)

plt.show()
```
<!--![](https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_002.png)-->
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_002.png" width="57%">

Matplotlib还提供了一些方便的功能来修改rc设置。 使用关键字参数，可以使用 matplotlib.rc()) 命令一次修改单个组中的多个设置：  
```python
mpl.rc('lines', linewidth=4, color='g')
plt.plot(data)
plt.show()
```
<!--![](https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_003.png)-->
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_customizing_003.png" width="57%">

## The *matplotlibrc* file

略




# * Outline

```markdown
# Tutorials: Intro


# Tutorials: Intermediate

## Artist tutorial
## Legend guide
## Styling with cycler
## Customizing Figure Layouts Using GridSpec and Other Functions
## Constrained Layout Guide
## Tight Layout guide
## origin and extend in imshow


# Tutorials: Advanced

## Path Tutorial
## Path effects guide
## Transformations Tutorial


# Colors

## Specifying Colors
## Customized Colorbars Tutorial
## Creating Colormaps in Matplotlib
## Colormap Normalization
## Choosing Colormaps in Matplotlib


# Text

## Text in Matplotlib Plots
## Text properties and layout
## Annotations
## Writing mathematical expressions
## Typesetting With XeLaTeX/LuaLaTeX
## Text rendering With LaTeX


# Toolkits

## Overview of axes_grid1 toolkit
## Overview of axisartist toolkit
## The mplot3d Toolkit
```

