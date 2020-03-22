---
title: Matplotlib Tutorials - 3. matplotlib.pyplot.plot
date: 2020-03-22 18:04:23
updated: 
categories:
  - Drafting
tags:
  - Notes
  - Python
  - Matplotlib
---

[matplotlib.pyplot.plot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)  

[Examples using matplot.pyplot.plot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#examples-using-matplotlib-pyplot-plot)  

# temp

## Marker Path

## Solarized Light stylesheet

## Frame grabbing

## Agg Buffer

## Coords Report

## Custom projection

## Customize Rc

## Findobj.Demo

## Multipage FDF

## Print Stdout
## Set And Get

## Transoffset

## Zorder Demo

## Custom scale


## Rotating custom tick labels

## Tool Manager

## Pdf Fonts
## Pgf Preamble
## Pgf Texsystem

## Simple Legend01

## Buttons

## Rectangle Selector

## Textbox
## Legend guide
## Path effects guide


# Basic Format

基本用法

## Pyplot Simple [ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_simple.html#sphx-glr-gallery-pyplots-pyplot-simple-py)

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.ylabel('some numbers')
plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_simple_001.png" width="41%">

## plot() format string

[ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_formatstr.html#sphx-glr-gallery-pyplots-pyplot-formatstr-py)

```python
#! Plot Format String
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'ro')
plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_formatstr_001.png" width="41%">


## Pyplot Mathtext

[ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_mathtext.html#sphx-glr-gallery-pyplots-pyplot-mathtext-py)

```python
import numpy as np
import matplotlib.pyplot as plt
t = np.arange(0.0, 2.0, 0.01)
s = np.sin(2*np.pi*t)

plt.plot(t,s)
plt.title(r'$\alpha_i > \beta_i$', fontsize=20)
plt.text(1, -0.6, r'$\sum_{i=0}^\infty x_i$', fontsize=20)
plt.text(0.6, 0.6, r'$\mathcal{A}\mathrm{sin}(2 \omega t)$',
         fontsize=20)
plt.xlabel('time (s)')
plt.ylabel('volts (mV)')
plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_mathtext_001.png" width="47%">

## Whats New 0.98.4 Legend

[ref](https://matplotlib.org/3.1.1/gallery/pyplots/whats_new_98_4_legend.html#sphx-glr-gallery-pyplots-whats-new-98-4-legend-py)

```python
#! Whats New Legend
import matplotlib.pyplot as plt
import numpy as np

ax = plt.subplot(111)
t1 = np.arange(0.0, 1.0, 0.01)
for n in [1, 2, 3, 4]:
    plt.plot(t1, t1**n, label="n=%d"%(n,))

leg = plt.legend(loc='best', ncol=2, mode="expand", shadow=True, fancybox=True)
leg.get_frame().set_alpha(0.5)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_whats_new_98_4_legend_001.png" width="47%">

### fancybox=False

> leg = plt.legend(loc='best', ncol=2, mode="expand", shadow=True, fancybox=False)

<img src="/images/2020-03/0322_Pyplot_legend1b.png" width="47%">

### 去掉 mode="expand"

> leg = plt.legend(loc='best', ncol=2, shadow=True, fancybox=True)

<img src="/images/2020-03/0322_Pyplot_legend1c.png" width="47%">

### 去掉 ncol=2

> leg = plt.legend(loc='best', mode="expand", shadow=True, fancybox=True)

<img src="/images/2020-03/0322_Pyplot_legend1d.png" width="47%">

### 重启 restart

> \# leg = plt.legend(loc='best', ncol=2, mode="expand", shadow=True, fancybox=True)
> leg=plt.legend(loc="best")

<img src="/images/2020-03/0322_Pyplot_legend2a.png" width="47%">

- leg=plt.legend(loc="best", ncol=2)  @分成两列
  <img src="/images/2020-03/0322_Pyplot_legend2b.png" width="47%">
- leg=plt.legend(loc="best", mode="expand")  @加宽
  <img src="/images/2020-03/0322_Pyplot_legend2c.png" width="47%">
  <!--宽度变长-->
- leg=plt.legend(loc="best", shadow=True)  @阴影
  <img src="/images/2020-03/0322_Pyplot_legend2d.png" width="47%">
- leg=plt.legend(loc="best", fancybox=True)  @弧度变圆，不再是尖框
  <img src="/images/2020-03/0322_Pyplot_legend2e.png" width="47%">



## Color by y-value

[ref](https://matplotlib.org/3.1.1/gallery/color/color_by_yvalue.html#sphx-glr-gallery-color-color-by-yvalue-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_color_by_yvalue_001.png" width="47%">

```python
import numpy as np
import matplotlib.pyplot as plt

t = np.arange(0.0, 2.0, 0.01)
s = np.sin(2 * np.pi * t)

upper = 0.77
lower = -0.77

supper = np.ma.masked_where(s < upper, s)
slower = np.ma.masked_where(s > lower, s)
smiddle = np.ma.masked_where((s < lower) | (s > upper), s)

fig, ax = plt.subplots()
ax.plot(t, smiddle, t, slower, t, supper)
plt.show()
```


# Line related

## Step Demo

[ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/step_demo.html#sphx-glr-gallery-lines-bars-and-markers-step-demo-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_step_demo_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(14)
y = np.sin(x / 2)

plt.step(x, y + 2, label='pre (default)')
plt.plot(x, y + 2, 'C0o', alpha=0.5)

plt.step(x, y + 1, where='mid', label='mid')
plt.plot(x, y + 1, 'C1o', alpha=0.5)

plt.step(x, y, where='post', label='post')
plt.plot(x, y, 'C2o', alpha=0.5)

plt.legend(title='Parameter where:')
plt.show()
```

## Triinterp Demo

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_triinterp_demo_001.png" width="67%">

```python
#! Tri-interp Demo
import matplotlib.pyplot as plt
import matplotlib.tri as mtri
import numpy as np

# Create triangulation.
x = np.asarray([0, 1, 2, 3, 0.5, 1.5, 2.5, 1, 2, 1.5])
y = np.asarray([0, 0, 0, 0, 1.0, 1.0, 1.0, 2, 2, 3.0])
triangles = [[0, 1, 4], [1, 2, 5], [2, 3, 6], [1, 5, 4], [2, 6, 5], [4, 5, 7],
             [5, 6, 8], [5, 8, 7], [7, 8, 9]]
triang = mtri.Triangulation(x, y, triangles)

# Interpolate to regularly-spaced quad grid.
z = np.cos(1.5 * x) * np.cos(1.5 * y)
xi, yi = np.meshgrid(np.linspace(0, 3, 20), np.linspace(0, 3, 20))

interp_lin = mtri.LinearTriInterpolator(triang, z)
zi_lin = interp_lin(xi, yi)

interp_cubic_geom = mtri.CubicTriInterpolator(triang, z, kind='geom')
zi_cubic_geom = interp_cubic_geom(xi, yi)

interp_cubic_min_E = mtri.CubicTriInterpolator(triang, z, kind='min_E')
zi_cubic_min_E = interp_cubic_min_E(xi, yi)

# Set up the figure
fig, axs = plt.subplots(nrows=2, ncols=2)
axs = axs.flatten()

# Plot the triangulation.
axs[0].tricontourf(triang, z)
axs[0].triplot(triang, 'ko-')
axs[0].set_title('Triangular grid')

# Plot linear interpolation to quad grid.
axs[1].contourf(xi, yi, zi_lin)
axs[1].plot(xi, yi, 'k-', lw=0.5, alpha=0.5)
axs[1].plot(xi.T, yi.T, 'k-', lw=0.5, alpha=0.5)
axs[1].set_title("Linear interpolation")

# Plot cubic interpolation to quad grid, kind=geom
axs[2].contourf(xi, yi, zi_cubic_geom)
axs[2].plot(xi, yi, 'k-', lw=0.5, alpha=0.5)
axs[2].plot(xi.T, yi.T, 'k-', lw=0.5, alpha=0.5)
axs[2].set_title("Cubic interpolation,\nkind='geom'")

# Plot cubic interpolation to quad grid, kind=min_E
axs[3].contourf(xi, yi, zi_cubic_min_E)
axs[3].plot(xi, yi, 'k-', lw=0.5, alpha=0.5)
axs[3].plot(xi.T, yi.T, 'k-', lw=0.5, alpha=0.5)
axs[3].set_title("Cubic interpolation,\nkind='min_E'")

fig.tight_layout()
plt.show()
```

## axhspan Demo

[ref](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/axhspan_demo.html#sphx-glr-gallery-subplots-axes-and-figures-axhspan-demo-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_axhspan_demo_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt

t = np.arange(-1, 2, .01)
s = np.sin(2 * np.pi * t)

plt.plot(t, s)
# Draw a thick red hline at y=0 that spans the xrange
plt.axhline(linewidth=8, color='#d62728')

# Draw a default hline at y=1 that spans the xrange
plt.axhline(y=1)
# Draw a default vline at x=1 that spans the yrange
plt.axvline(x=1)

# Draw a thick blue vline at x=0 that spans the upper quadrant of the yrange
plt.axvline(x=0, ymin=0.75, linewidth=8, color='#1f77b4')

# Draw a default hline at y=.5 that spans the middle half of the axes
plt.axhline(y=.5, xmin=0.25, xmax=0.75)

plt.axhspan(0.25, 0.75, facecolor='0.5', alpha=0.5)
plt.axvspan(1.25, 1.55, facecolor='#2ca02c', alpha=0.5)

plt.show()
```

<img src="/images/2020-03/0322_Pyplot_axhspan.png" width="67%">

改变线条颜色  
> plt.plot(t, s, 'y')  
> plt.axvline(x=0, ymin=0.5, linewidth=8, color='#1f77b4')

注意 axhline 里的 xmin, xmax 和 axvline 里的 ymin, ymax 都指的是比例，意思是距离坐标轴、即图的边界是整个图的百分之多少。

> def axhline(self, y=0, xmin=0, xmax=1, \*\*kwargs):
> 	# Add a horizontal line across the axis.
> 	# Parameters
> 	# ----------
> 	y : scalar, optional, default: 0
> 		y position in data coordinates of the horizontal line
> 	xmin : scalar, optional, default: 0
> 		Should be between 0 and 1, 0 being the far left of the plot, 1 the
> 		far right of the plot.
> 	xmax : scalar, optional, default: 1
> 		Should be between 0 and 1, 0 being the far left of the plot, 1 the
> 		far right of the plot.
> 	# Returns
>


# Axes related

## Shared Axis Demo

[ref](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/shared_axis_demo.html#sphx-glr-gallery-subplots-axes-and-figures-shared-axis-demo-py)

通过将轴实例作为 sharex 或 sharey kwarg 传递，可以共享一个轴的 x 或 y 轴范围。  
更改一个轴上的轴限制将自动反映在另一个轴上，反之亦然，因此，当您使用工具栏导航时，两个轴将在其共享轴上彼此跟随。同理改变轴的缩放比例（例如，对数与线性）。但是，刻度标记可能会有所不同，例如，您可以有选择地关闭一个轴上的刻度标记。  
下例显示了如何自定义各个轴上的刻度线标签。共享的轴共享刻度线定位器，刻度线格式器，视图限制和转换（例如，对数、线性）。但是 ticklabels 标签本身不共享属性。这是一个功能，而不是错误，因为您可能希望使刻度标记在上轴上更小，例如，在下面的示例中。  

如果要关闭给定轴的刻度标签（例如，在 subplot(211) 或 subplot(212) 上），则无法执行标准技巧：  
> setp(ax2, xticklabels=[])

因为这会更改刻度坐标格式器，它在所有轴之间共享。但是您可以更改标签的可见性，这是一个属性：  
> setp(ax2.get_xticklabels(), visible=False)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_shared_axis_demo_001.png" width="67%">

```python
#! Shared Axis
import matplotlib.pyplot as plt
import numpy as np

t = np.arange(0.01, 5.0, 0.01)
s1 = np.sin(2 * np.pi * t)
s2 = np.exp(-t)
s3 = np.sin(4 * np.pi * t)

ax1 = plt.subplot(311)
plt.plot(t, s1)
plt.setp(ax1.get_xticklabels(), fontsize=6)

# share x only
ax2 = plt.subplot(312, sharex=ax1)
plt.plot(t, s2)
# make these tick labels invisible
plt.setp(ax2.get_xticklabels(), visible=False)

# share x and y
ax3 = plt.subplot(313, sharex=ax1, sharey=ax1)
plt.plot(t, s3)
plt.xlim(0.01, 5.0)
plt.show()
```


# Title related

## Titles Demo

[ref](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/titles_demo.html#sphx-glr-gallery-text-labels-and-annotations-titles-demo-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_titles_demo_001.png" width="41%">

```python
#! Title Demo
import matplotlib.pyplot as plt
plt.plot(range(10))
plt.title('Center Title')
plt.title('Left Title', loc='left')
plt.title('Right Title', loc='right')
plt.show()
```

# Legend related

## Align y-labels

Two methods are shown here, one using a short call to Figure.align_ylabels and the second a manual way to align the labels. [ref](https://matplotlib.org/3.1.1/gallery/pyplots/align_ylabels.html#sphx-glr-gallery-pyplots-align-ylabels-py)

```python
import numpy as np
import matplotlib.pyplot as plt

def make_plot(axs):
    box = dict(facecolor='yellow', pad=5, alpha=0.2)

    # Fixing random state for reproducibility
    np.random.seed(19680801)
    ax1 = axs[0, 0]
    ax1.plot(2000*np.random.rand(10))
    ax1.set_title('ylabels not aligned')
    ax1.set_ylabel('misaligned 1', bbox=box)
    ax1.set_ylim(0, 2000)

    ax3 = axs[1, 0]
    ax3.set_ylabel('misaligned 2', bbox=box)
    ax3.plot(np.random.rand(10))

    ax2 = axs[0, 1]
    ax2.set_title('ylabels aligned')
    ax2.plot(2000*np.random.rand(10))
    ax2.set_ylabel('aligned 1', bbox=box)
    ax2.set_ylim(0, 2000)

    ax4 = axs[1, 1]
    ax4.plot(np.random.rand(10))
    ax4.set_ylabel('aligned 2', bbox=box)
```

### Figure.align_ylabels [ref](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.align_ylabels)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_align_ylabels_0011.png" width="47%">

```python
# Plot 1:
fig, axs = plt.subplots(2, 2)
fig.subplots_adjust(left=0.2, wspace=0.6)
make_plot(axs)

# just align the last column of axes:
fig.align_ylabels(axs[:, 1])
plt.show()
```

#### what if: fig.align_ylabels(axs)

> fig.align_ylabels(axs)
>

<img src="/images/2020-03/0322_Pyplot_alignylabel1b.png" width="47%">

### Manually align the labels [ref](https://matplotlib.org/3.1.1/gallery/pyplots/align_ylabels.html#sphx-glr-gallery-pyplots-align-ylabels-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_align_ylabels_002.png" width="47%">

```python
fig, axs = plt.subplots(2, 2)
fig.subplots_adjust(left=0.2, wspace=0.6)

make_plot(axs)

labelx = -0.3  # axes coords

for j in range(2):
    axs[j, 1].yaxis.set_label_coords(labelx, 0.5)

plt.show()
```


# Text (font etc.) related

## Usetex Demo

Shows how to use latex in a plot. [Usetex Demo](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/usetex_demo.html#sphx-glr-gallery-text-labels-and-annotations-usetex-demo-py)  
Also refer to the [Text rendering With LaTeX](https://matplotlib.org/3.1.1/tutorials/text/usetex.html) guide.

执行速度会略有一点儿慢  
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_usetex_demo_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt
plt.rc('text', usetex=True)

# interface tracking profiles
N = 500
delta = 0.6
X = np.linspace(-1, 1, N)
plt.plot(X, (1 - np.tanh(4 * X / delta)) / 2,    # phase field tanh profiles
         X, (1.4 + np.tanh(4 * X / delta)) / 4, "C2",  # composition profile
         X, X < 0, 'k--')                        # sharp interface

# legend
plt.legend(('phase field', 'level set', 'sharp interface'),
           shadow=True, loc=(0.01, 0.48), handlelength=1.5, fontsize=16)

# the arrow
plt.annotate("", xy=(-delta / 2., 0.1), xytext=(delta / 2., 0.1),
             arrowprops=dict(arrowstyle="<->", connectionstyle="arc3"))
plt.text(0, 0.1, r'$\delta$',
         {'color': 'black', 'fontsize': 24, 'ha': 'center', 'va': 'center',
          'bbox': dict(boxstyle="round", fc="white", ec="black", pad=0.2)})

# Use tex in labels
plt.xticks((-1, 0, 1), ('$-1$', r'$\pm 0$', '$+1$'), color='k', size=20)

# Left Y-axis labels, combine math mode and text mode
plt.ylabel(r'\bf{phase field} $\phi$', {'color': 'C0', 'fontsize': 20})
plt.yticks((0, 0.5, 1), (r'\bf{0}', r'\bf{.5}', r'\bf{1}'), color='k', size=20)

# Right Y-axis labels
plt.text(1.02, 0.5, r"\bf{level set} $\phi$", {'color': 'C2', 'fontsize': 20},
         horizontalalignment='left',
         verticalalignment='center',
         rotation=90,
         clip_on=False,
         transform=plt.gca().transAxes)

# Use multiline environment inside a `text`.
# level set equations
eq1 = r"\begin{eqnarray*}" + \
      r"|\nabla\phi| &=& 1,\\" + \
      r"\frac{\partial \phi}{\partial t} + U|\nabla \phi| &=& 0 " + \
      r"\end{eqnarray*}"
plt.text(1, 0.9, eq1, {'color': 'C2', 'fontsize': 18}, va="top", ha="right")

# phase field equations
eq2 = r'\begin{eqnarray*}' + \
      r'\mathcal{F} &=& \int f\left( \phi, c \right) dV, \\ ' + \
      r'\frac{ \partial \phi } { \partial t } &=& -M_{ \phi } ' + \
      r'\frac{ \delta \mathcal{F} } { \delta \phi }' + \
      r'\end{eqnarray*}'
plt.text(0.18, 0.18, eq2, {'color': 'C0', 'fontsize': 16})

plt.text(-1, .30, r'gamma: $\gamma$', {'color': 'r', 'fontsize': 20})
plt.text(-1, .18, r'Omega: $\Omega$', {'color': 'b', 'fontsize': 20})

plt.show()
```

### Steps 分步骤

1. after 19 lines: 显示图例，并标注一个双向箭头
2. after 25 lines: 文字即 text 注解 $\delta$ ，修改横轴的记号标签 (xticklabels)
3. after 29 lines: 修改纵轴说明 (ylabel) 及其记号标签 (yticklabels)
4. after 37 lines: 形如双 y 轴，但是是使用 plt.text 文字注解实现的
5. after 45 lines: plt.text 绿色公式
6. after 53 lines: plt.text 蓝色公式
7. after 55 lines: plt.text 红色 $\gamma$
8. after 56 lines: plt.text 蓝色 $\Omega$

after 19 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line19.png" width="37%">
after 25 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line25.png" width="37%">
after 29 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line29.png" width="37%">
after 37 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line37.png" width="37%">
after 45 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line45.png" width="37%">
after 53 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line53.png" width="37%">
after 55 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line55.png" width="37%">
after 56 lines: <img src="/images/2020-03/0322_Pyplot_Usetex_line56.png" width="37%">


## Controlling style of text and labels using a dictionary

[ref](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/text_fontdict.html#sphx-glr-gallery-text-labels-and-annotations-text-fontdict-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_text_fontdict_001.png" width="67%">

```python
#! Text Font
import numpy as np
import matplotlib.pyplot as plt

font = {'family': 'serif',
        'color':  'darkred',
        'weight': 'normal',
        'size': 16,
        }

x = np.linspace(0.0, 5.0, 100)
y = np.cos(2*np.pi*x) * np.exp(-x)

plt.plot(x, y, 'k')
plt.title('Damped exponential decay', fontdict=font)
plt.text(2, 0.65, r'$\cos(2 \pi t) \exp(-t)$', fontdict=font)
plt.xlabel('time (s)', fontdict=font)
plt.ylabel('voltage (mV)', fontdict=font)

# Tweak spacing to prevent clipping of ylabel
plt.subplots_adjust(left=0.15)
plt.show()
```

## Text Rotation Relative To Line

[ref](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/text_rotation_relative_to_line.html#sphx-glr-gallery-text-labels-and-annotations-text-rotation-relative-to-line-py)

matplotlib 中的文本对象通常相对于屏幕坐标系旋转（即，无论轴如何更改，旋转45度都会沿着水平和垂直之间的直线绘制文本）。 但是，有时人们想相对于绘图中的某物旋转文本。 在这种情况下，正确的角度将不是该对象在绘图坐标系中的角度，而是该对象在屏幕坐标系中显示的角度。 如下面的示例所示，可以通过将绘图中的角度转换为屏幕坐标系来找到该角度。

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_text_rotation_relative_to_line_001.png" width="67%">

```python
#! Text Rotate
import matplotlib.pyplot as plt
import numpy as np

# Plot diagonal line (45 degrees)
h = plt.plot(np.arange(0, 10), np.arange(0, 10))

# set limits so that it no longer looks on screen to be 45 degrees
plt.xlim([-10, 20])

# Locations to plot text
l1 = np.array((1, 1))
l2 = np.array((5, 5))

# Rotate angle
angle = 45
trans_angle = plt.gca().transData.transform_angles(np.array((45,)),
                                                   l2.reshape((1, 2)))[0]

# Plot text
th1 = plt.text(l1[0], l1[1], 'text not rotated correctly', fontsize=16,
               rotation=angle, rotation_mode='anchor')
th2 = plt.text(l2[0], l2[1], 'text rotated correctly', fontsize=16,
               rotation=trans_angle, rotation_mode='anchor')

plt.show()
```


# Multiple related

## Multiple Figs Demo

[ref](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/multiple_figs_demo.html#sphx-glr-gallery-subplots-axes-and-figures-multiple-figs-demo-py)

<img src="/images/2020-03/0322_Pyplot_MultiFigs2a.png" width="47%"><img src="/images/2020-03/0322_Pyplot_MultiFigs2b.png" width="47%">

```python
#! Multiple Figs

## Working with multiple figure windows and subplots
import matplotlib.pyplot as plt
import numpy as np

t = np.arange(0.0, 2.0, 0.01)
s1 = np.sin(2*np.pi*t)
s2 = np.sin(4*np.pi*t)

## Create figure 1
plt.figure(1)
plt.subplot(211)
plt.plot(t, s1)
plt.subplot(212)
plt.plot(t, 2*s1)

## Create figure 2
plt.figure(2)
plt.plot(t, s2)

## Now switch back to figure 1 and make some changes
plt.figure(1)
plt.subplot(211)
plt.plot(t, s2, 's')
ax = plt.gca()
ax.set_xticklabels([])

plt.show()
```

## Multiline

[ref](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/multiline.html#sphx-glr-gallery-text-labels-and-annotations-multiline-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_multiline_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import numpy as np

plt.figure(figsize=(7, 4))
ax = plt.subplot(121)
ax.set_aspect(1)
plt.plot(np.arange(10))
plt.xlabel('this is a xlabel\n(with newlines!)')
plt.ylabel('this is vertical\ntest', multialignment='center')
plt.text(2, 7, 'this is\nyet another test',
         rotation=45,
         horizontalalignment='center',
         verticalalignment='top',
         multialignment='center')
plt.grid(True)
plt.subplot(122)

plt.text(0.29, 0.4, "Mat\nTTp\n123", size=18,
         va="baseline", ha="right", multialignment="left",
         bbox=dict(fc="none"))
plt.text(0.34, 0.4, "Mag\nTTT\n123", size=18,
         va="baseline", ha="left", multialignment="left",
         bbox=dict(fc="none"))
plt.text(0.95, 0.4, "Mag\nTTT$^{A^A}$\n123", size=18,
         va="baseline", ha="right", multialignment="left",
         bbox=dict(fc="none"))

plt.xticks([0.2, 0.4, 0.6, 0.8, 1.],
           ["Jan\n2009", "Feb\n2009", "Mar\n2009", "Apr\n2009", "May\n2009"])
plt.axhline(0.4)
plt.title("test line spacing for multiline text")
plt.subplots_adjust(bottom=0.25, top=0.75)
plt.show()
```


# Mask, NaN related

## Nan Test

[ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/nan_test.html#sphx-glr-gallery-lines-bars-and-markers-nan-test-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_nan_test_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt

t = np.arange(0.0, 1.0 + 0.01, 0.01)
s = np.cos(2 * 2*np.pi * t)
t[41:60] = np.nan

plt.subplot(2, 1, 1)
plt.plot(t, s, '-', lw=2)

plt.xlabel('time (s)')
plt.ylabel('voltage (mV)')
plt.title('A sine wave with a gap of NaNs between 0.4 and 0.6')
plt.grid(True)

plt.subplot(2, 1, 2)
t[0] = np.nan
t[-1] = np.nan
plt.plot(t, s, '-', lw=2)
plt.title('Also with NaN in first and last point')

plt.xlabel('time (s)')
plt.ylabel('more nans')
plt.grid(True)

plt.tight_layout()
plt.show()
```

## Masked Demo

[ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/masked_demo.html#sphx-glr-gallery-lines-bars-and-markers-masked-demo-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_masked_demo_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0, 2*np.pi, 0.02)
y = np.sin(x)
y1 = np.sin(2 * x)
y2 = np.sin(3 * x)
ym1 = np.ma.masked_where(y1 > 0.5, y1)
ym2 = np.ma.masked_where(y2 < -0.5, y2)

lines = plt.plot(x, y, x, ym1, x, ym2, 'o')
plt.setp(lines[0], linewidth=4)
plt.setp(lines[1], linewidth=2)
plt.setp(lines[2], markersize=10)

plt.legend(('No mask', 'Masked if > 0.5', 'Masked if < -0.5'),
            loc='upper right')
plt.title('Masked line demo')
plt.show()
```

## Scatter Masked 

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_scatter_masked_001.png" width="67%">

```python
#! Scatter Masked
import matplotlib.pyplot as plt
import numpy as np

# Fixing random state for reproducibility
np.random.seed(19680801)

N = 100
r0 = 0.6
x = 0.9 * np.random.rand(N)
y = 0.9 * np.random.rand(N)
area = (20 * np.random.rand(N)) ** 2  # 0 to 10 point radii
c = np.sqrt(area)
r = np.sqrt(x ** 2 + y ** 2)
area1 = np.ma.masked_where(r < r0, area)
area2 = np.ma.masked_where(r >= r0, area)
plt.scatter(x, y, s=area1, marker='^', c=c)
plt.scatter(x, y, s=area2, marker='o', c=c)
# Show the boundary between the regions:
theta = np.arange(0, np.pi / 2, 0.01)
plt.plot(r0 * np.cos(theta), r0 * np.sin(theta))

plt.show()
```

# Style related

## Join styles and cap styles

[ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/joinstyle.html#sphx-glr-gallery-lines-bars-and-markers-joinstyle-py)

### Join styles

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_joinstyle_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt

def plot_angle(ax, x, y, angle, style):
    phi = np.radians(angle)
    xx = [x + .5, x, x + .5*np.cos(phi)]
    yy = [y, y, y + .5*np.sin(phi)]
    ax.plot(xx, yy, lw=12, color='tab:blue', solid_joinstyle=style)
    ax.plot(xx, yy, lw=1, color='black')
    ax.plot(xx[1], yy[1], 'o', color='tab:red', markersize=3)

fig, ax = plt.subplots(figsize=(8, 6))
ax.set_title('Join style')

for x, style in enumerate(['miter', 'round', 'bevel']):
    # ax.text(x, 6, style)
    # for y, angle in enumerate([30, 45, 60, 90, 120, 210]):
    ax.text(x, 5, style)
    for y, angle in enumerate([20, 45, 60, 90, 120]):
        plot_angle(ax, x, y, angle, style)
        if x == 0:
            ax.text(-1.3, y, f'{angle} degrees')
ax.text(1, 4.7, '(default)')

ax.set_xlim(-1.5, 2.75)
ax.set_ylim(-.5, 5.5)
ax.xaxis.set_visible(False)
ax.yaxis.set_visible(False)
plt.show()
```

### Cap styles

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_joinstyle_002.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(8, 2))
ax.set_title('Cap style')

for x, style in enumerate(['butt', 'round', 'projecting']):
    ax.text(x, 1, style)
    xx = [x, x + 0.5]
    yy = [0, 0]
    ax.plot(xx, yy, lw=12, color='tab:blue', solid_capstyle=style)
    ax.plot(xx, yy, lw=1, color='black')
    ax.plot(xx, yy, 'o', color='tab:red', markersize=3)
ax.text(2, 0.7, '(default)')

ax.set_ylim(-.5, 1.5)
ax.xaxis.set_visible(False)
ax.yaxis.set_visible(False)
plt.show()
```

# Other Area (Related Domains)

## Psd Demo

Plotting Power Spectral Density (PSD) in Matplotlib. [ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/psd_demo.html#sphx-glr-gallery-lines-bars-and-markers-psd-demo-py) 

### Simple Psd Demo with Matplotlib, MATLAB

The PSD is a common plot in the field of signal processing. NumPy has many useful libraries for computing a PSD. Below we demo a few examples of how this can be accomplished and visualized with Matplotlib.

```python
#@ Psd Demo
import matplotlib.pyplot as plt
import numpy as np
import matplotlib.mlab as mlab
import matplotlib.gridspec as gridspec

# Fixing random state for reproducibility
np.random.seed(19680801)

dt = 0.01
t = np.arange(0, 10, dt)
nse = np.random.randn(len(t))
r = np.exp(-t / 0.05)

cnse = np.convolve(nse, r) * dt
cnse = cnse[: len(t)]
s = 0.1 * np.sin(2 * np.pi * t) + cnse

plt.subplot(211)
plt.plot(t, s)
plt.subplot(212)
plt.psd(s, 512, 1 / dt)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_psd_demo_001.png" width="67%">

Compare this with the equivalent Matlab code to accomplish the same thing:

```matlab
dt = 0.01;
t = [0:dt:10];
nse = randn(size(t));
r = exp(-t/0.05);
cnse = conv(nse, r)*dt;
cnse = cnse(1:length(t));
s = 0.1*sin(2*pi*t) + cnse;

subplot(211)
plot(t,s)
subplot(212)
psd(s, 512, 1/dt)
```

### A more complex one

Below we'll show a slightly more complex example that demonstrates how padding affects the resulting PSD.

```python
dt = np.pi / 100.
fs = 1. / dt
t = np.arange(0, 8, dt)
y = 10. * np.sin(2 * np.pi * 4 * t) + 5. * np.sin(2 * np.pi * 4.25 * t)
y = y + np.random.randn(*t.shape)

# Plot the raw time series
fig = plt.figure(constrained_layout=True)
gs = gridspec.GridSpec(2, 3, figure=fig)
ax = fig.add_subplot(gs[0, :])
ax.plot(t, y)
ax.set_xlabel('time [s]')
ax.set_ylabel('signal')

# Plot the PSD with different amounts of zero padding. This uses the entire
# time series at once
ax2 = fig.add_subplot(gs[1, 0])
ax2.psd(y, NFFT=len(t), pad_to=len(t), Fs=fs)
ax2.psd(y, NFFT=len(t), pad_to=len(t) * 2, Fs=fs)
ax2.psd(y, NFFT=len(t), pad_to=len(t) * 4, Fs=fs)
plt.title('zero padding')

# Plot the PSD with different block sizes, Zero pad to the length of the
# original data sequence.
ax3 = fig.add_subplot(gs[1, 1], sharex=ax2, sharey=ax2)
ax3.psd(y, NFFT=len(t), pad_to=len(t), Fs=fs)
ax3.psd(y, NFFT=len(t) // 2, pad_to=len(t), Fs=fs)
ax3.psd(y, NFFT=len(t) // 4, pad_to=len(t), Fs=fs)
ax3.set_ylabel('')
plt.title('block size')

# Plot the PSD with different amounts of overlap between blocks
ax4 = fig.add_subplot(gs[1, 2], sharex=ax2, sharey=ax2)
ax4.psd(y, NFFT=len(t) // 2, pad_to=len(t), noverlap=0, Fs=fs)
ax4.psd(y, NFFT=len(t) // 2, pad_to=len(t),
        noverlap=int(0.05 * len(t) / 2.), Fs=fs)
ax4.psd(y, NFFT=len(t) // 2, pad_to=len(t),
        noverlap=int(0.2 * len(t) / 2.), Fs=fs)
ax4.set_ylabel('')
plt.title('overlap')

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_psd_demo_002.png" width="100%">

把上面第 3-4 个子图的 NFFT 改变，//2 改为 //3 ，//4 改为 //6 ，可得下图  
<img src="/images/2020-03/0322_Pyplot_Psd2b.png" width="100%">

### Follow-up

This is a ported version of a MATLAB example from the signal processing toolbox that showed some difference at one time between Matplotlib's and MATLAB's scaling of the PSD.

```python
fs = 1000
t = np.linspace(0, 0.3, 301)
A = np.array([2, 8]).reshape(-1, 1)
f = np.array([150, 140]).reshape(-1, 1)
xn = (A * np.sin(2 * np.pi * f * t)).sum(axis=0)
xn += 5 * np.random.randn(*t.shape)

fig, (ax0, ax1) = plt.subplots(ncols=2, constrained_layout=True)

yticks = np.arange(-50, 30, 10)
yrange = (yticks[0], yticks[-1])
xticks = np.arange(0, 550, 100)

ax0.psd(xn, NFFT=301, Fs=fs, window=mlab.window_none, pad_to=1024,
        scale_by_freq=True)
ax0.set_title('Periodogram')
ax0.set_yticks(yticks)
ax0.set_xticks(xticks)
ax0.grid(True)
ax0.set_ylim(yrange)

ax1.psd(xn, NFFT=150, Fs=fs, window=mlab.window_none, pad_to=512, noverlap=75,
        scale_by_freq=True)
ax1.set_title('Welch')
ax1.set_xticks(xticks)
ax1.set_yticks(yticks)
ax1.set_ylabel('')  # overwrite the y-label added by `psd`
ax1.grid(True)
ax1.set_ylim(yrange)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_psd_demo_003.png" width="67%">

This is a ported version of a MATLAB example from the signal processing toolbox that showed some difference at one time between Matplotlib's and MATLAB's scaling of the PSD.

It uses a complex signal so we can see that complex PSD's work properly.

```python
prng = np.random.RandomState(19680801)  # to ensure reproducibility

fs = 1000
t = np.linspace(0, 0.3, 301)
A = np.array([2, 8]).reshape(-1, 1)
f = np.array([150, 140]).reshape(-1, 1)
xn = (A * np.exp(2j * np.pi * f * t)).sum(axis=0) + 5 * prng.randn(*t.shape)

fig, (ax0, ax1) = plt.subplots(ncols=2, constrained_layout=True)

yticks = np.arange(-50, 30, 10)
yrange = (yticks[0], yticks[-1])
xticks = np.arange(-500, 550, 200)

ax0.psd(xn, NFFT=301, Fs=fs, window=mlab.window_none, pad_to=1024,
        scale_by_freq=True)
ax0.set_title('Periodogram')
ax0.set_yticks(yticks)
ax0.set_xticks(xticks)
ax0.grid(True)
ax0.set_ylim(yrange)

ax1.psd(xn, NFFT=150, Fs=fs, window=mlab.window_none, pad_to=512, noverlap=75,
        scale_by_freq=True)
ax1.set_title('Welch')
ax1.set_xticks(xticks)
ax1.set_yticks(yticks)
ax1.set_ylabel('')  # overwrite the y-label added by `psd`
ax1.grid(True)
ax1.set_ylim(yrange)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_psd_demo_004.png" width="67%">


# Not usually used

不太常用的

## Dolphins [ref](https://matplotlib.org/3.1.1/gallery/shapes_and_collections/dolphin.html#sphx-glr-gallery-shapes-and-collections-dolphin-py)

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_dolphin_001.png" width="67%">

```python
import matplotlib.cm as cm
import matplotlib.pyplot as plt
from matplotlib.patches import Circle, PathPatch
from matplotlib.path import Path
from matplotlib.transforms import Affine2D
import numpy as np

# Fixing random state for reproducibility
np.random.seed(19680801)


r = np.random.rand(50)
t = np.random.rand(50) * np.pi * 2.0
x = r * np.cos(t)
y = r * np.sin(t)

fig, ax = plt.subplots(figsize=(6, 6))
circle = Circle((0, 0), 1, facecolor='none',
                edgecolor=(0, 0.8, 0.8), linewidth=3, alpha=0.5)
ax.add_patch(circle)

im = plt.imshow(np.random.random((100, 100)),
                origin='lower', cmap=cm.winter,
                interpolation='spline36',
                extent=([-1, 1, -1, 1]))
im.set_clip_path(circle)

plt.plot(x, y, 'o', color=(0.9, 0.9, 1.0), alpha=0.8)

# Dolphin from OpenClipart library by Andy Fitzsimon
#       <cc:License rdf:about="http://web.resource.org/cc/PublicDomain">
#         <cc:permits rdf:resource="http://web.resource.org/cc/Reproduction"/>
#         <cc:permits rdf:resource="http://web.resource.org/cc/Distribution"/>
#         <cc:permits rdf:resource="http://web.resource.org/cc/DerivativeWorks"/>
#       </cc:License>

dolphin = """
M -0.59739425,160.18173 C -0.62740401,160.18885 -0.57867129,160.11183
-0.57867129,160.11183 C -0.57867129,160.11183 -0.5438361,159.89315
-0.39514638,159.81496 C -0.24645668,159.73678 -0.18316813,159.71981
-0.18316813,159.71981 C -0.18316813,159.71981 -0.10322971,159.58124
-0.057804323,159.58725 C -0.029723983,159.58913 -0.061841603,159.60356
-0.071265813,159.62815 C -0.080250183,159.65325 -0.082918513,159.70554
-0.061841203,159.71248 C -0.040763903,159.7194 -0.0066711426,159.71091
0.077336307,159.73612 C 0.16879567,159.76377 0.28380306,159.86448
0.31516668,159.91533 C 0.3465303,159.96618 0.5011127,160.1771
0.5011127,160.1771 C 0.63668998,160.19238 0.67763022,160.31259
0.66556395,160.32668 C 0.65339985,160.34212 0.66350443,160.33642
0.64907098,160.33088 C 0.63463742,160.32533 0.61309688,160.297
0.5789627,160.29339 C 0.54348657,160.28968 0.52329693,160.27674
0.50728856,160.27737 C 0.49060916,160.27795 0.48965803,160.31565
0.46114204,160.33673 C 0.43329696,160.35786 0.4570711,160.39871
0.43309565,160.40685 C 0.4105108,160.41442 0.39416631,160.33027
0.3954995,160.2935 C 0.39683269,160.25672 0.43807996,160.21522
0.44567915,160.19734 C 0.45327833,160.17946 0.27946869,159.9424
-0.061852613,159.99845 C -0.083965233,160.0427 -0.26176109,160.06683
-0.26176109,160.06683 C -0.30127962,160.07028 -0.21167141,160.09731
-0.24649368,160.1011 C -0.32642366,160.11569 -0.34521187,160.06895
-0.40622293,160.0819 C -0.467234,160.09485 -0.56738444,160.17461
-0.59739425,160.18173
"""

vertices = []
codes = []
parts = dolphin.split()
i = 0
code_map = {
    'M': (Path.MOVETO, 1),
    'C': (Path.CURVE4, 3),
    'L': (Path.LINETO, 1)}

while i < len(parts):
    code = parts[i]
    path_code, npoints = code_map[code]
    codes.extend([path_code] * npoints)
    vertices.extend([[float(x) for x in y.split(',')] for y in
                     parts[i + 1:i + npoints + 1]])
    i += npoints + 1
vertices = np.array(vertices, float)
vertices[:, 1] -= 160

dolphin_path = Path(vertices, codes)
dolphin_patch = PathPatch(dolphin_path, facecolor=(0.6, 0.6, 0.6),
                          edgecolor=(0.0, 0.0, 0.0))
ax.add_patch(dolphin_patch)

vertices = Affine2D().rotate_deg(60).transform(vertices)
dolphin_path2 = Path(vertices, codes)
dolphin_patch2 = PathPatch(dolphin_path2, facecolor=(0.5, 0.5, 0.5),
                           edgecolor=(0.0, 0.0, 0.0))
ax.add_patch(dolphin_patch2)

plt.show()
```


# Refer to previous notes

这些图例之前已经出现过，可参考 Matplotlib 系列第 1-2 篇笔记

- Simple Plot [ref](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/simple_plot.html#sphx-glr-gallery-lines-bars-and-markers-simple-plot-py)
- Multiple subplots [ref](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/subplot.html#sphx-glr-gallery-subplots-axes-and-figures-subplot-py)
- Legend using pre-defined labels [ref](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/legend.html#sphx-glr-gallery-text-labels-and-annotations-legend-py)
- Pyplot Scales [ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_scales.html#sphx-glr-gallery-pyplots-pyplot-scales-py)
- Pyplot Three [ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_three.html#sphx-glr-gallery-pyplots-pyplot-three-py)
- Pyplot Two subplots [ref](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_two_subplots.html#sphx-glr-gallery-pyplots-pyplot-two-subplots-py)
- Symlog Demo [ref](https://matplotlib.org/3.1.1/gallery/scales/symlog_demo.html#sphx-glr-gallery-scales-symlog-demo-py)
- Slider Demo [ref](https://matplotlib.org/3.1.1/gallery/widgets/slider_demo.html#sphx-glr-gallery-widgets-slider-demo-py)
- Usage Guide [ref](https://matplotlib.org/3.1.1/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py)
- Pyplot tutorial [ref](https://matplotlib.org/3.1.1/tutorials/introductory/pyplot.html#sphx-glr-tutorials-introductory-pyplot-py)
- Customizing Matplotlib with style sheets and rcParams [ref](https://matplotlib.org/3.1.1/tutorials/introductory/customizing.html#sphx-glr-tutorials-introductory-customizing-py)

# * References




