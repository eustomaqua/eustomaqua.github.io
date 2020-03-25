---
title: Matplotlib Tutorials - 3. matplotlib.pyplot.plot
date: 2020-03-22 18:04:23
updated: 
categories:
  - Drafting
tags:
  - Notes
  - Matplotlib
---

[matplotlib.pyplot.plot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)  

[Examples using matplot.pyplot.plot](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#examples-using-matplotlib-pyplot-plot)  



# Basic Format

<font color=#8A2BE2>Say Hello to Pyplot:</font> 基本用法

## Pyplot Simple
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_simple.html#sphx-glr-gallery-pyplots-pyplot-simple-py) 
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_simple_001.png" width="41%">

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.ylabel('some numbers')
plt.show()
```

## plot() format string
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_formatstr.html#sphx-glr-gallery-pyplots-pyplot-formatstr-py) 
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_formatstr_001.png" width="41%">

```python
#! Plot Format String
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'ro')
plt.show()
```


## Pyplot Mathtext
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/pyplots/pyplot_mathtext.html#sphx-glr-gallery-pyplots-pyplot-mathtext-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pyplot_mathtext_001.png" width="67%">
<!--width="47%"-->

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

## Pgf: Fonts, Preamble, Texsystem

### Pgf Fonts
[ref](https://matplotlib.org/3.1.1/gallery/userdemo/pgf_fonts.html#sphx-glr-gallery-userdemo-pgf-fonts-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pgf_fonts_001.png" width="67%">

```python
import matplotlib.pyplot as plt
plt.rcParams.update({
    "font.family": "serif",
    "font.serif": [],                    # use latex default serif font
    "font.sans-serif": ["DejaVu Sans"],  # use a specific sans-serif font
})

plt.figure(figsize=(4.5, 2.5))
plt.plot(range(5))
plt.text(0.5, 3., "serif")
plt.text(0.5, 2., "monospace", family="monospace")
plt.text(2.5, 2., "sans-serif", family="sans-serif")
plt.text(2.5, 1., "comic sans", family="Comic Sans MS")
plt.xlabel("µ is not $\\mu$")
plt.tight_layout(.5)

plt.savefig("pgf_fonts.pdf")
plt.savefig("pgf_fonts.png")
```

{% gp 1-3 %}
<img src="/images/2020-03/0322_Pyplot_pgf1a.png">
<img src="/images/2020-03/pgf_fonts.png">
{% endgp %}

### Pgf Preamble

[ref](https://matplotlib.org/3.1.1/gallery/userdemo/pgf_preamble_sgskip.html#sphx-glr-gallery-userdemo-pgf-preamble-sgskip-py)

- default mainfont
  <img src="/images/2020-03/0322_Pyplot_pgfpreamble_none.png" width="67%">
- DejaVu Serif
  <img src="/images/2020-03/0322_Pyplot_pgfpreamble_DejaVu.png" width="67%">
- Times New Roman
  <img src="/images/2020-03/0322_Pyplot_pgfpreamble_Times.png" width="67%">
- Latin Modern Mono
  <img src="/images/2020-03/0322_Pyplot_pgfpreamble_Latin.png" width="67%">

```python
import matplotlib as mpl
mpl.use("pgf")
import matplotlib.pyplot as plt
plt.rcParams.update({
    "font.family": "serif",  # use serif/main font for text elements
    "text.usetex": True,     # use inline math for ticks
    "pgf.rcfonts": False,    # don't setup fonts from rc parameters
    "pgf.preamble": [
         "\\usepackage{units}",          # load additional packages
         "\\usepackage{metalogo}",
         "\\usepackage{unicode-math}",   # unicode math setup
         ## r"\setmathfont{xits-math.otf}",
         r"\setmainfont{DejaVu Serif}",  # serif font via preamble
         # r"\setmainfont{Times New Roman}",
         # r"\setmainfont{Latin Modern Mono}",
         ]
})

plt.figure(figsize=(4.5, 2.5))
plt.plot(range(5))
plt.xlabel("unicode text: я, ψ, €, ü, \\unitfrac[10]{°}{µm}")
plt.ylabel("\\XeLaTeX")
plt.legend(["unicode math: $λ=∑_i^∞ μ_i^2$"])
plt.tight_layout(.5)

plt.savefig("pgf_preamble.pdf")
plt.savefig("pgf_preamble.png")
```

### Pgf Texsystem

[ref](https://matplotlib.org/3.1.1/gallery/userdemo/pgf_texsystem.html#sphx-glr-gallery-userdemo-pgf-texsystem-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pgf_texsystem_001.png">

```python
import matplotlib.pyplot as plt
plt.rcParams.update({
    "pgf.texsystem": "pdflatex",
    "pgf.preamble": [
         r"\usepackage[utf8x]{inputenc}",
         r"\usepackage[T1]{fontenc}",
         r"\usepackage{cmbright}",
         ]
})

plt.figure(figsize=(4.5, 2.5))
plt.plot(range(5))
plt.text(0.5, 3., "serif", family="serif")
plt.text(0.5, 2., "monospace", family="monospace")
plt.text(2.5, 2., "sans-serif", family="sans-serif")
plt.xlabel(r"µ is not $\mu$")
plt.tight_layout(.5)

plt.savefig("pgf_texsystem.pdf")
plt.savefig("pgf_texsystem.png")
# plt.show()
```

{% gp 1-3 %}
<img src="/images/2020-03/0322_Pyplot_pgftexsystem1a.png">
<img src="/images/2020-03/pgf_texsystem.png">
{% endgp %}


## Color by y-value
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/color/color_by_yvalue.html#sphx-glr-gallery-color-color-by-yvalue-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_color_by_yvalue_001.png" width="67%">

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
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/step_demo.html#sphx-glr-gallery-lines-bars-and-markers-step-demo-py)
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
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/triinterp_demo.html#sphx-glr-gallery-images-contours-and-fields-triinterp-demo-py)
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
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/axhspan_demo.html#sphx-glr-gallery-subplots-axes-and-figures-axhspan-demo-py)
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
>     # Add a horizontal line across the axis.
>     # Parameters
>     # ----------
>     y : scalar, optional, default: 0
>         y position in data coordinates of the horizontal line
>     xmin : scalar, optional, default: 0
>         Should be between 0 and 1, 0 being the far left of the plot, 1 the
>         far right of the plot.
>     xmax : scalar, optional, default: 1
>         Should be between 0 and 1, 0 being the far left of the plot, 1 the
>         far right of the plot.
>     # Returns
>

## Marker Path
[ref](https://matplotlib.org/3.1.1/gallery/shapes_and_collections/marker_path.html#sphx-glr-gallery-shapes-and-collections-marker-path-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_marker_path_001.png" width="67%">

```python
#! Marker Path
import matplotlib.pyplot as plt
import matplotlib.path as mpath
import numpy as np

star = mpath.Path.unit_regular_star(6) # 代表 N 角星
circle = mpath.Path.unit_circle()
# concatenate the circle with an internal cutout of the star
verts = np.concatenate([circle.vertices, star.vertices[::-1, ...]])
codes = np.concatenate([circle.codes, star.codes])
cut_star = mpath.Path(verts, codes)

plt.plot(np.arange(10)**2, '--r', marker=cut_star, markersize=15)
plt.show()
```

## Solarized Light stylesheet
[ref](https://matplotlib.org/3.1.1/gallery/style_sheets/plot_solarizedlight2.html#sphx-glr-gallery-style-sheets-plot-solarizedlight2-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_plot_solarizedlight2_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import numpy as np
x = np.linspace(0, 10)
with plt.style.context('Solarize_Light2'):
    plt.plot(x, np.sin(x) + x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 2 * x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 3 * x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 4 + np.random.randn(50))
    plt.plot(x, np.sin(x) + 5 * x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 6 * x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 7 * x + np.random.randn(50))
    plt.plot(x, np.sin(x) + 8 * x + np.random.randn(50))
    # Number of accent colors in the color scheme
    plt.title('8 Random Lines - Line')
    plt.xlabel('x label', fontsize=14)
    plt.ylabel('y label', fontsize=14)
plt.show()
```

### style.available

> @contextlib.contextmanager
> def context(style, after_reset=False):
>     """Context manager for using style settings temporarily.
>     Parameters
>     ----------
>     style : str, dict, or list
>         A style specification. Valid options are:
>         +------+-------------------------------------------------------------+
>         | str  | The name of a style or a path/URL to a style file. For a    |
>         |      | list of available style names, see `style.available`.       |
>         +------+-------------------------------------------------------------+
>         | dict | Dictionary with valid key/value pairs for                   |
>         |      | `matplotlib.rcParams`.                                      |
>         +------+-------------------------------------------------------------+
>         | list | A list of style specifiers (str or dict) applied from first |
>         |      | to last in the list.                                        |
>         +------+-------------------------------------------------------------+
>     etc.
>     """
>

```python
>>> plt.style.available
['bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'seaborn', 'Solarize_Light2', 'tableau-colorblind10', '_classic_test']
```

### changing 'style' param

e.g., with plt.style.context('presentation'):

```python
def auto_sub_pack(style, ax):
    with plt.style.context(style):
        ax.plot(x, np.sin(x) + x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 2 * x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 3 * x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 4 + np.random.randn(50))
        ax.plot(x, np.sin(x) + 5 * x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 6 * x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 7 * x + np.random.randn(50))
        ax.plot(x, np.sin(x) + 8 * x + np.random.randn(50))
        # Number of accent colors in the color scheme
        ax.set_title('8 Random Lines - Line')
        ax.set_xlabel('x label', fontsize=14)
        ax.set_ylabel('y label', fontsize=14)
        ax.legend((style,))

x = np.linspace(0, 10)  # len(plt.style.available) = 26
style_set = plt.style.available + ['presentation']  # 27 = 3x9 = 4x8 = 5x6
for fid in range(3):
    fstyle = style_set[fid * 9: (fid + 1) * 9]
    fig, axs = plt.subplots(3, 3, figsize=(12, 8)) # (15, 9))
    for i in range(3):
        for j in range(3):
            k = i * 3 + j
            auto_sub_pack(fstyle[k], axs[i, j])
    fig.tight_layout()
plt.show()
```

<img src="/images/2020-03/0322_Pyplot_stylesheet2a.png" width="100%"><img src="/images/2020-03/0322_Pyplot_stylesheet2b.png" width="100%"><img src="/images/2020-03/0322_Pyplot_stylesheet2c.png" width="100%">


# Axes related

## Shared Axis Demo
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/shared_axis_demo.html#sphx-glr-gallery-subplots-axes-and-figures-shared-axis-demo-py)

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

## Coords Report

覆盖/重写默认的坐标报告。 [ref](https://matplotlib.org/3.1.1/gallery/misc/coords_report.html#sphx-glr-gallery-misc-coords-report-py)
<!--<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_coords_report_001.png" width="67%">-->

[plt.subplots()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots)  
[ax: axes.Axes](https://matplotlib.org/3.1.1/api/axes_api.html#matplotlib.axes.Axes)  
<img src="/images/2020-03/0322_Pyplot_coordsreport.png" width="67%">

```python
import matplotlib.pyplot as plt
import numpy as np

def millions(x):
    return '$%1.1fM' % (x*1e-6)
# Fixing random state for reproducibility
np.random.seed(19680801)
x = np.random.rand(20)
y = 1e7 * np.random.rand(20)
fig, ax = plt.subplots()
ax.plot(x, y, 'o')

# ax.fmt_ydata = millions
from matplotlib.ticker import FormatStrFormatter
# ax.yaxis.set_major_formatter(FormatStrFormatter('%.01f'))
class Millions(FormatStrFormatter):
    def __init__(self, fmt='$%1.1fM'):
        self.fmt = fmt
    def __call__(self, x, pos=None):
        return self.fmt % (x * 1e-6)
ax.yaxis.set_major_formatter(Millions())

plt.show()
```

## Transoffset

这说明了使用 transforms.offset_copy 进行的变换，该变换将诸如文本字符串之类的绘图元素定位在屏幕坐标（点或英寸）相对于任何坐标中给定位置的指定偏移处。  
每个 Artist（即派生出诸如 Text 和 Line 之类的 mpl 类）都具有一个转换，可以在创建 Artist 时进行设置，例如通过相应的 pyplot 命令。 默认情况下，这通常是 Axes.transData 转换，从数据单位到屏幕点。 我们可以使用 offset_copy 函数来制作此变换的修改后副本，其中修改包含偏移量。

[ref](https://matplotlib.org/3.1.1/gallery/misc/transoffset.html#sphx-glr-gallery-misc-transoffset-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_transoffset_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import matplotlib.transforms as mtransforms
import numpy as np

xs = np.arange(7)
ys = xs**2

fig = plt.figure(figsize=(5, 10))
ax = plt.subplot(2, 1, 1)

# If we want the same offset for each text instance,
# we only need to make one transform.  To get the
# transform argument to offset_copy, we need to make the axes
# first; the subplot command above is one way to do this.
trans_offset = mtransforms.offset_copy(ax.transData, fig=fig,
                                       x=0.05, y=0.10, units='inches')

for x, y in zip(xs, ys):
    plt.plot(x, y, 'ro')
    plt.text(x, y, '%d, %d' % (int(x), int(y)), transform=trans_offset)

# offset_copy works for polar plots also.
ax = plt.subplot(2, 1, 2, projection='polar')

trans_offset = mtransforms.offset_copy(ax.transData, fig=fig,
                                       y=6, units='dots')

for x, y in zip(xs, ys):
    plt.polar(x, y, 'ro')
    plt.text(x, y, '%d, %d' % (int(x), int(y)),
             transform=trans_offset,
             horizontalalignment='center',
             verticalalignment='bottom')

plt.show()
```

## Custom scale
[ref](https://matplotlib.org/3.1.1/gallery/scales/custom_scale.html#sphx-glr-gallery-scales-custom-scale-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_custom_scale_001.png" width="67%">

```python
import numpy as np
from numpy import ma
from matplotlib import scale as mscale
from matplotlib import transforms as mtransforms
from matplotlib.ticker import Formatter, FixedLocator
from matplotlib import rcParams


# BUG: this example fails with any other setting of axisbelow
rcParams['axes.axisbelow'] = False


class MercatorLatitudeScale(mscale.ScaleBase):
    """
    Scales data in range -pi/2 to pi/2 (-90 to 90 degrees) using
    the system used to scale latitudes in a Mercator projection.

    The scale function:
      ln(tan(y) + sec(y))

    The inverse scale function:
      atan(sinh(y))

    Since the Mercator scale tends to infinity at +/- 90 degrees,
    there is user-defined threshold, above and below which nothing
    will be plotted.  This defaults to +/- 85 degrees.

    source:
    http://en.wikipedia.org/wiki/Mercator_projection
    """

    # The scale class must have a member ``name`` that defines the string used
    # to select the scale.  For example, ``gca().set_yscale("mercator")`` would
    # be used to select this scale.
    name = 'mercator'

    def __init__(self, axis, *, thresh=np.deg2rad(85), **kwargs):
        """
        Any keyword arguments passed to ``set_xscale`` and ``set_yscale`` will
        be passed along to the scale's constructor.

        thresh: The degree above which to crop the data.
        """
        super().__init__()  #!@NOTICE! axis)
        if thresh >= np.pi / 2:
            raise ValueError("thresh must be less than pi/2")
        self.thresh = thresh

    def get_transform(self):
        """
        Override this method to return a new instance that does the
        actual transformation of the data.

        The MercatorLatitudeTransform class is defined below as a
        nested class of this one.
        """
        return self.MercatorLatitudeTransform(self.thresh)

    def set_default_locators_and_formatters(self, axis):
        """
        Override to set up the locators and formatters to use with the
        scale.  This is only required if the scale requires custom
        locators and formatters.  Writing custom locators and
        formatters is rather outside the scope of this example, but
        there are many helpful examples in ``ticker.py``.

        In our case, the Mercator example uses a fixed locator from
        -90 to 90 degrees and a custom formatter class to put convert
        the radians to degrees and put a degree symbol after the
        value::
        """
        class DegreeFormatter(Formatter):
            def __call__(self, x, pos=None):
                return "%d\N{DEGREE SIGN}" % np.degrees(x)

        axis.set_major_locator(FixedLocator(
            np.radians(np.arange(-90, 90, 10))))
        axis.set_major_formatter(DegreeFormatter())
        axis.set_minor_formatter(DegreeFormatter())

    def limit_range_for_scale(self, vmin, vmax, minpos):
        """
        Override to limit the bounds of the axis to the domain of the
        transform.  In the case of Mercator, the bounds should be
        limited to the threshold that was passed in.  Unlike the
        autoscaling provided by the tick locators, this range limiting
        will always be adhered to, whether the axis range is set
        manually, determined automatically or changed through panning
        and zooming.
        """
        return max(vmin, -self.thresh), min(vmax, self.thresh)

    class MercatorLatitudeTransform(mtransforms.Transform):
        # There are two value members that must be defined.
        # ``input_dims`` and ``output_dims`` specify number of input
        # dimensions and output dimensions to the transformation.
        # These are used by the transformation framework to do some
        # error checking and prevent incompatible transformations from
        # being connected together.  When defining transforms for a
        # scale, which are, by definition, separable and have only one
        # dimension, these members should always be set to 1.
        input_dims = 1
        output_dims = 1
        is_separable = True
        has_inverse = True

        def __init__(self, thresh):
            mtransforms.Transform.__init__(self)
            self.thresh = thresh

        def transform_non_affine(self, a):
            """
            This transform takes an Nx1 ``numpy`` array and returns a
            transformed copy.  Since the range of the Mercator scale
            is limited by the user-specified threshold, the input
            array must be masked to contain only valid values.
            ``matplotlib`` will handle masked arrays and remove the
            out-of-range data from the plot.  Importantly, the
            ``transform`` method *must* return an array that is the
            same shape as the input array, since these values need to
            remain synchronized with values in the other dimension.
            """
            masked = ma.masked_where((a < -self.thresh) | (a > self.thresh), a)
            if masked.mask.any():
                return ma.log(np.abs(ma.tan(masked) + 1.0 / ma.cos(masked)))
            else:
                return np.log(np.abs(np.tan(a) + 1.0 / np.cos(a)))

        def inverted(self):
            """
            Override this method so matplotlib knows how to get the
            inverse transform for this transform.
            """
            return MercatorLatitudeScale.InvertedMercatorLatitudeTransform(
                self.thresh)

    class InvertedMercatorLatitudeTransform(mtransforms.Transform):
        input_dims = 1
        output_dims = 1
        is_separable = True
        has_inverse = True

        def __init__(self, thresh):
            mtransforms.Transform.__init__(self)
            self.thresh = thresh

        def transform_non_affine(self, a):
            return np.arctan(np.sinh(a))

        def inverted(self):
            return MercatorLatitudeScale.MercatorLatitudeTransform(self.thresh)

# Now that the Scale class has been defined, it must be registered so
# that ``matplotlib`` can find it.
mscale.register_scale(MercatorLatitudeScale)


if __name__ == '__main__':
    import matplotlib.pyplot as plt

    t = np.arange(-180.0, 180.0, 0.1)
    s = np.radians(t)/2.

    plt.plot(t, s, '-', lw=2)
    plt.gca().set_yscale('mercator')

    plt.xlabel('Longitude')
    plt.ylabel('Latitude')
    plt.title('Mercator: Projection of the Oppressor')
    plt.grid(True)

    plt.show()
```

## Rotating custom tick labels
Demo of custom tick-labels with user-defined rotation. 
[ref](https://matplotlib.org/3.1.1/gallery/ticks_and_spines/ticklabels_rotation.html#sphx-glr-gallery-ticks-and-spines-ticklabels-rotation-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_ticklabels_rotation_001.png" width="67%">

> plt.xticks(x, labels, rotation=45)
> <img src="/images/2020-03/0322_Pyplot_rotateticklabels.png" width="67%">


```python
#! Rotating custom tick labels
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 9, 6]
labels = ['Frogs', 'Hogs', 'Bogs', 'Slogs']

plt.plot(x, y)
# You can specify a rotation for the tick labels in degrees or with keywords.
plt.xticks(x, labels, rotation='vertical')
# Pad margins so that markers don't get clipped by the axes
plt.margins(0.2)
# Tweak spacing to prevent clipping of tick-labels
plt.subplots_adjust(bottom=0.15)
plt.show()
```

## Path effects guide

[ref](https://matplotlib.org/3.1.1/tutorials/advanced/patheffects_guide.html#sphx-glr-tutorials-advanced-patheffects-guide-py) Defining paths that objects follow on a canvas.

Matplotlib 的 patheffects 模块提供了将多重绘制阶段应用于可以通过路径渲染的任何Artist的功能。  
可以应用路径效果的艺术家包括 Patch、Line2D、Collection 甚至 Text 。每个艺术家的路径效果都可以通过 set_path_effects 方法（set_path_effects）进行控制，该方法采用了 AbstractPathEffect 实例的迭代方法。  

最简单的路径效果是“普通”效果，该效果只是简单地绘制了艺术家而没有任何效果：  
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_patheffects_guide_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects

fig = plt.figure(figsize=(5, 1.5))
text = fig.text(0.5, 0.5, 'Hello path effects world!\nThis is the normal '
                          'path effect.\nPretty dull, huh?',
                ha='center', va='center', size=20)
text.set_path_effects([path_effects.Normal()])
plt.show()
```

下面两张图是对比 "使用第8行 text.set_path_effects()" 和 "注释掉该行"   
（画图顺序：在执行过程中，先生成了第二张图，然后再生成第一张图）  
{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_guidepath1a.png">
<img src="/images/2020-03/0322_Pyplot_guidepath1b.png">
{% endgp %}

### Adding a shadow

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_patheffects_guide_002.png" width="67%">

```python
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects

text = plt.text(0.5, 0.5, 'Hello path effects world!',
                path_effects=[path_effects.withSimplePatchShadow()])

plt.plot([0, 3, 2, 5], linewidth=5, color='blue',
         path_effects=[path_effects.SimpleLineShadow(),
                       path_effects.Normal()])
plt.show()
```

### Making an artist stand out

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_patheffects_guide_003.png" width="67%">

```python
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects

fig = plt.figure(figsize=(7, 1))
text = fig.text(0.5, 0.5, 'This text stands out because of\n'
                          'its black border.', color='white',
                          ha='center', va='center', size=30)
text.set_path_effects([path_effects.Stroke(linewidth=3, foreground='black'),
                       path_effects.Normal()])
plt.show()
```

### Greater control of the path effect artist

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_patheffects_guide_004.png" width="67%">

```python
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects

fig = plt.figure(figsize=(8, 1))
t = fig.text(0.02, 0.5, 'Hatch shadow', fontsize=75, weight=1000, va='center')
t.set_path_effects([path_effects.PathPatchEffect(offset=(4, -4), hatch='xxxx',
                                                 facecolor='gray'),
                    path_effects.PathPatchEffect(edgecolor='white', linewidth=1.1,
                                                 facecolor='black')])
plt.show()
```


## Set And Get

[ref](https://matplotlib.org/3.1.1/gallery/misc/set_and_get.html#sphx-glr-gallery-misc-set-and-get-py)  
The pyplot interface allows you to use setp and getp to set and get object properties, as well as to do introspection on the object.

### set, get

#### set

If you want to know the valid types of arguments, you can provide the name of the property you want to set without a value:
```python
>>> plt.setp(line, 'linestyle')
    linestyle: [ '-' | '--' | '-.' | ':' | 'steps' | 'None' ]
```

If you want to see all the properties that can be set, and their possible values, you can do:
```python
>>> plt.setp(line)
```

#### get

get returns the value of a given attribute. You can use get to query the value of a single attribute:
```python
>>> plt.getp(line, 'linewidth')
    0.5
```

or all the attribute/value pairs:
```python
>>> plt.getp(line)
    aa = True
    alpha = 1.0
    antialiased = True
    c = b
    clip_on = True
    color = b
    ... long listing skipped ...
```

#### e.g.,

```python
>>> line, = plt.plot([1,2,3])
>>> plt.setp(line, linestyle='--')

>>> x = np.arange(0,1.0,0.01)
>>> y1 = np.sin(2*np.pi*x)
>>> y2 = np.sin(4*np.pi*x)
>>> lines = plt.plot(x, y1, x, y2)
>>> plt.setp(lines, linewidth=2, color='r')
```

### Aliases

To reduce keystrokes in interactive mode, a number of properties have short aliases, e.g., 'lw' for 'linewidth' and 'mec' for 'markeredgecolor'. When calling set or get in introspection mode, these properties will be listed as 'fullname or aliasname'.

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_set_and_get_001.png" width="67%">

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0, 1.0, 0.01)
y1 = np.sin(2*np.pi*x)
y2 = np.sin(4*np.pi*x)
lines = plt.plot(x, y1, x, y2)
l1, l2 = lines
plt.setp(lines, linestyle='--')       # set both to dashed
plt.setp(l1, linewidth=2, color='r')  # line1 is thick and red
plt.setp(l2, linewidth=1, color='g')  # line2 is thinner and green


print('Line setters')
plt.setp(l1)
print('Line getters')
plt.getp(l1)

print('Rectangle setters')
plt.setp(plt.gca().patch)
print('Rectangle getters')
plt.getp(plt.gca().patch)

t = plt.title('Hi mom')
print('Text setters')
plt.setp(t)
print('Text getters')
plt.getp(t)

plt.show()
```


# Title related

## Titles Demo
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/titles_demo.html#sphx-glr-gallery-text-labels-and-annotations-titles-demo-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_titles_demo_001.png" width="67%"> <!--"41%"-->

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

## Legend guide

Generating legends fiexibly in Matplotlib. [ref](https://matplotlib.org/3.1.1/tutorials/intermediate/legend_guide.html#sphx-glr-tutorials-intermediate-legend-guide-py)

### Controlling the legend entries

{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_guide1a.png">
<img src="/images/2020-03/0322_Pyplot_guide1b.png">
{% endgp %}

```python
# Legend guide
import matplotlib.pyplot as plt
# handles, labels = ax.get_legend_handles_labels()
# ax.legend(handles, labels)

line_up, = plt.plot([1,2,3], label='Line 2')
line_down, = plt.plot([3,2,1], label='Line 1')
plt.legend(handles=[line_up, line_down])
plt.show()

line_up, = plt.plot([1,2,3], label='Line 2')
line_down, = plt.plot([3,2,1], label='Line 1')
plt.legend([line_up, line_down], ['Line Up', 'Line Down'])
plt.show()
```

### Creating artists specifically for adding to the legend (aka. Proxy artists)

{% gp 1-2 %}
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_legend_guide_001.png">
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_legend_guide_002.png">
{% endgp %}

```python
import matplotlib.patches as mpatches
import matplotlib.pyplot as plt
red_patch = mpatches.Patch(color='red', label='The red data')
plt.legend(handles=[red_patch])
plt.show()

import matplotlib.lines as mlines
blue_line = mlines.Line2D([], [], color='blue', marker='*',
                          markersize=15, label='Blue stars')
plt.legend(handles=[blue_line])
plt.show()
```

### Legend location

图例的位置可以通过关键字参数 loc 来指定。 有关更多详细信息，请参见 legend() 上的文档。  
bbox_to_anchor 关键字为手动图例放置提供了很大程度上的控制。 例如，如果您希望轴图例位于图形的右上角而不是轴的角，则只需指定角的位置以及该位置的坐标系即可：
```python
plt.legend(bbox_to_anchor=(1, 1),
           bbox_transform=plt.gcf().transFigure)
```

下方代码中有三处 \#\# 的注释，其中，这两张图分别来源于：  
1. 第一处注释，第二、三处取消注释
2. 第一处注释，第二、三处亦注释，并按下方代码修改对应位置

{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_guide2a.png">
<img src="/images/2020-03/0322_Pyplot_guide3.png">
{% endgp %}

备注，原版来自于 [comes from Legend Guide](https://matplotlib.org/3.1.1/tutorials/intermediate/legend_guide.html#sphx-glr-tutorials-intermediate-legend-guide-py)  
3. 第二、三处均为原版，即不注释，第一处也不注释
4. 第二、三处均为原版，即不注释，而第一处则注释掉

{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_guide4a.png">
<img src="/images/2020-03/0322_Pyplot_guide4b.png">
{% endgp %}

```python
import matplotlib.pyplot as plt
## plt.legend(bbox_to_anchor=(1, 1),
##            bbox_transform=plt.gcf().transFigure)

plt.subplot(211)
plt.plot([1, 2, 3], '--', label="test1")
plt.plot([3, 2, 1], '--', label="test2")

# Place a legend above this subplot, expanding itself to
# fully use the given bounding box.
## plt.legend(bbox_to_anchor=(0., 1.02, 1., .102), loc='lower left',
##            ncol=2, mode="expand", borderaxespad=0.)
plt.legend(bbox_to_anchor=(0.02, 0.12, 0.7, .262),
           bbox_transform=plt.gcf().transFigure)

plt.subplot(223)
plt.plot([1, 2, 3], c='C3', label="test3")
plt.plot([3, 2, 1], c='C4', label="test4")
# Place a legend to the right of this smaller subplot.
## plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
plt.legend(bbox_to_anchor=(0.75, 0.8),
           bbox_transform=plt.gcf().transFigure)

plt.show()
```


## Simple Legend01

[ref](https://matplotlib.org/3.1.1/gallery/userdemo/simple_legend01.html#sphx-glr-gallery-userdemo-simple-legend01-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_simple_legend01_001.png" width="67%">

```python
import matplotlib.pyplot as plt

plt.subplot(211)
plt.plot([1, 2, 3], label="test1")
plt.plot([3, 2, 1], label="test2")
# Place a legend above this subplot, expanding itself to
# fully use the given bounding box.
plt.legend(bbox_to_anchor=(0., 1.02, 1., .102), loc='lower left',
           ncol=2, mode="expand", borderaxespad=0.)

plt.subplot(223)
plt.plot([1, 2, 3], label="test1")
plt.plot([3, 2, 1], label="test2")
# Place a legend to the right of this smaller subplot.
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)

plt.show()
```

### bbox_to_anchor

其中 bbox_to_anchor 代表的是 (xloc, yloc, xlen, ylen) ，这四个数值其实都是相对于 x-axis, y-axis 的比例；如果只有两个量，那么就代表 (xloc, yloc) ，后面的长度取默认值。

- (1) pgf texsystem
  <img src="/images/2020-03/0322_Pyplot_legend1a.png" width="57%">
  备注，原设置是  
  > ```python
  plt.legend(bbox_to_anchor=(0., 1.02, 1., .102), 
             loc='lower left', ncol=2, mode="expand", borderaxespad=0.)
  plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
  ```

- (2) 调整子图一、二的图例 <!--height="4px-->
> <table><td bgcolor=#7FFFD4 style="font-weight: bold; text-align: left;">
    plt.legend(bbox_to_anchor=(0.1, 1.02, 0.6, .102), loc='lower left', ncol=2, mode="expand", borderaxespad=0.)
    plt.legend(bbox_to_anchor=(1.05, 0.7), loc='upper left', borderaxespad=0.)
</td></table>
> 
> <img src="/images/2020-03/0322_Pyplot_legend1b.png" width="57%">

- (3) 调整子图二的图例 <!--height="1px"-->
> <table><td bgcolor=#7FFFD4 style="font-weight: bold;">
    plt.legend(bbox_to_anchor=(1.55, 0.7), loc='upper left', borderaxespad=0.)
</td></table>
>
> <img src="/images/2020-03/0322_Pyplot_legend1f.png" width="57%">

- (4) 调整子图一，四元组 + 去掉 mode="expand"
> <table><td bgcolor=#7FFFD4>plt.legend(bbox_to_anchor=(0.1, 1.02, 0.6, 0.302), loc='lower left', ncol=2, borderaxespad=0., fancybox=True, shadow=True)</td></table>
>
> <img src="/images/2020-03/0322_Pyplot_legend1c.png" width="57%">

- (4) 调整子图一，二元组 + 包含 mode="expand" + 分成两列呈现
> <table><td bgcolor=#7FFFD4>plt.legend(bbox_to_anchor=(0.1, 1.02), loc='lower left', ncol=2, mode="expand", borderaxespad=0., fancybox=True, shadow=True)</td></table>
>
> <img src="/images/2020-03/0322_Pyplot_legend1d.png" width="57%">

- (5) 调整子图一，二元组 + 包含 mode="expand" + 只有一列呈现
> <table><td bgcolor=#7FFFD4>plt.legend(bbox_to_anchor=(0.1, 1.02), loc='lower left', ncol=1, mode="expand", borderaxespad=0., fancybox=True, shadow=True)</td></table>
>
> <img src="/images/2020-03/0322_Pyplot_legend1e.png" width="57%">


### 'bbox_to_anchor' param

>     @docstring.dedent_interpd
>     def legend(self, *args, **kwargs):
>         """
>         Places a legend on the axes.
>         Other Parameters
>         ----------------
>         loc : int or string or pair of floats, default: 'upper right'
>             The location of the legend. Possible codes are:
>                 ===============   =============
>                 Location String   Location Code
>                 ===============   =============
>                 'best'            0
>                 'upper right'     1
>                 'upper left'      2
>                 'lower left'      3
>                 'lower right'     4
>                 'right'           5
>                 'center left'     6
>                 'center right'    7
>                 'lower center'    8
>                 'upper center'    9
>                 'center'          10
>                 ===============   =============
>             Alternatively can be a 2-tuple giving ``x, y`` of the lower-left
>             corner of the legend in axes coordinates (in which case
>             ``bbox_to_anchor`` will be ignored).
>         
>         bbox_to_anchor : `.BboxBase` or pair of floats
>             Specify any arbitrary location for the legend in `bbox_transform`
>             coordinates (default Axes coordinates).
>             For example, to put the legend's upper right hand corner in the
>             center of the axes the following keywords can be used::
>                loc='upper right', bbox_to_anchor=(0.5, 0.5)
>         
>         ncol : integer
>             The number of columns that the legend has. Default is 1.
>         
>         prop : None or :class:`matplotlib.font_manager.FontProperties` or dict
>             The font properties of the legend. If None (default), the current
>             :data:`matplotlib.rcParams` will be used.
>         
>         etc."""
>

### class Legend

> class Legend(Artist):
>     """ Place a legend on the axes at location loc. """
>     def __str__(self):
>         return "Legend"
>     
>     @docstring.dedent_interpd
>     def __init__(self, parent, handles, labels,
>                  loc=None,
>                  numpoints=None,    # the number of points in the legend line
>                  markerscale=None,  # the relative size of legend markers
>                                     # vs. original
>                  markerfirst=True,  # controls ordering (left-to-right) of
>                                     # legend marker and label
>                  scatterpoints=None,    # number of scatter points
>                  scatteryoffsets=None,
>                  prop=None,          # properties for the legend texts
>                  fontsize=None,        # keyword to set font size directly
>                  # spacing & pad defined as a fraction of the font-size
>                  borderpad=None,      # the whitespace inside the legend border
>                  labelspacing=None,   # the vertical space between the legend
>                                       # entries
>                  handlelength=None,   # the length of the legend handles
>                  handleheight=None,   # the height of the legend handles
>                  handletextpad=None,  # the pad between the legend handle
>                                       # and text
>                  borderaxespad=None,  # the pad between the axes and legend
>                                       # border
>                  columnspacing=None,  # spacing between columns
>                  ncol=1,     # number of columns
>                  mode=None,  # mode for horizontal distribution of columns.
>                              # None, "expand"
>                  fancybox=None,  # True use a fancy box, false use a rounded
>                                  # box, none use rc
>                  shadow=None,
>                  title=None,  # set a title for the legend
>                  framealpha=None,  # set frame alpha
>                  edgecolor=None,  # frame patch edgecolor
>                  facecolor=None,  # frame patch facecolor
>                  bbox_to_anchor=None,  # bbox that the legend will be anchored.
>                  bbox_transform=None,  # transform for the bbox
>                  frameon=None,  # draw frame
>                  handler_map=None,
>                  ):
>         """
>         Notes
>         -----
>         Users can specify any arbitrary location for the legend using the
>         *bbox_to_anchor* keyword argument. bbox_to_anchor can be an instance
>         of BboxBase(or its derivatives) or a tuple of 2 or 4 floats.
>         See :meth:`set_bbox_to_anchor` for more detail.
>         The legend location can be specified by setting *loc* with a tuple of
>         2 floats, which is interpreted as the lower-left corner of the legend
>         in the normalized axes coordinate.
>         """
>         
>     def set_bbox_to_anchor(self, bbox, transform=None):
>         """
>         Set the bbox that the legend will be anchored to.
>         *bbox* can be
>         - A `.BboxBase` instance
>         - A tuple of ``(left, bottom, width, height)`` in the given transform
>           (normalized axes coordinate if None)
>         - A tuple of ``(left, bottom)`` where the width and height will be
>           assumed to be zero.
>         """
>


## Whats New 0.98.4 Legend
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/pyplots/whats_new_98_4_legend.html#sphx-glr-gallery-pyplots-whats-new-98-4-legend-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_whats_new_98_4_legend_001.png" width="67%">

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

### call off in 'plt.legend'
#### fancybox=False

> leg = plt.legend(loc='best', ncol=2, mode="expand", shadow=True, fancybox=False)

<img src="/images/2020-03/0322_Pyplot_legendprime1b.png" width="41%">

#### 去掉 mode="expand"

> leg = plt.legend(loc='best', ncol=2, shadow=True, fancybox=True)

<img src="/images/2020-03/0322_Pyplot_legendprime1c.png" width="41%">

#### 去掉 ncol=2

> leg = plt.legend(loc='best', mode="expand", shadow=True, fancybox=True)

<img src="/images/2020-03/0322_Pyplot_legendprime1d.png" width="41%">

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

### Figure.align_ylabels
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.align_ylabels)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_align_ylabels_0011.png" width="57%"> <!--"47%"-->

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

<img src="/images/2020-03/0322_Pyplot_alignylabel1b.png" width="57%">

### Manually align the labels

[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/pyplots/align_ylabels.html#sphx-glr-gallery-pyplots-align-ylabels-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_align_ylabels_002.png" width="57%">

```python
fig, axs = plt.subplots(2, 2)
fig.subplots_adjust(left=0.2, wspace=0.6)

make_plot(axs)

labelx = -0.3  # axes coords

for j in range(2):
    axs[j, 1].yaxis.set_label_coords(labelx, 0.5)

plt.show()
```

## Zorder Demo

轴的默认绘制顺序是补丁 patch、线条 line、文本 text。 此顺序由 zorder 属性确定。 默认值如下表所示。  
您可以通过设置 zorder 更改单个艺术家的顺序。 任何单独的 plot() 调用都可以为该特定项目的 zorder 设置一个值。  
在下面的第一个子图中，线是从散点图的补丁集合上方绘制的，这是默认设置。在下面的子图中，顺序相反。第二个图显示了如何控制单个线条的 zorder。

<img src="/images/2020-03/0322_Pyplot_zorder.png" width="100%">

[ref](https://matplotlib.org/3.1.1/gallery/misc/zorder_demo.html#sphx-glr-gallery-misc-zorder-demo-py)

{% gp 1-2 %}
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_zorder_demo_001.png">
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_zorder_demo_002.png">
{% endgp %}

```python
import matplotlib.pyplot as plt
import numpy as np
## Fixing random state for reproducibility
np.random.seed(19680801)
x = np.random.random(20)
y = np.random.random(20)

# Lines on top of scatter
plt.figure()
plt.subplot(211)
plt.plot(x, y, 'C3', lw=3)
plt.scatter(x, y, s=120)
plt.title('Lines on top of dots')
## Scatter plot on top of lines
plt.subplot(212)
plt.plot(x, y, 'C3', zorder=1, lw=3)
plt.scatter(x, y, s=120, zorder=2)
plt.title('Dots on top of lines')
plt.tight_layout()

# A new figure, with individually ordered items
x = np.linspace(0, 2*np.pi, 100)
plt.rcParams['lines.linewidth'] = 10
plt.figure()
plt.plot(x, np.sin(x), label='zorder=10', zorder=10)  # on top
plt.plot(x, np.sin(1.1*x), label='zorder=1', zorder=1)  # bottom
plt.plot(x, np.sin(1.2*x), label='zorder=3',  zorder=3)
plt.axhline(0, label='zorder=2', color='grey', zorder=2)
plt.title('Custom order of elements')
l = plt.legend(loc='upper right')
l.set_zorder(20)  # put the legend on top

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
[<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/text_rotation_relative_to_line.html#sphx-glr-gallery-text-labels-and-annotations-text-rotation-relative-to-line-py)

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
{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_MultiFigs2a.png">
<img src="/images/2020-03/0322_Pyplot_MultiFigs2b.png">
{% endgp %}
<!--
<img src="/images/2020-03/0322_Pyplot_MultiFigs2a.png" width="47%"><img src="/images/2020-03/0322_Pyplot_MultiFigs2b.png" width="47%">
-->

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

## Tool Manager

Toolbar (tools) [ref](https://matplotlib.org/3.1.1/gallery/user_interfaces/toolmanager_sgskip.html#sphx-glr-gallery-user-interfaces-toolmanager-sgskip-py)

```python
import matplotlib.pyplot as plt
plt.rcParams['toolbar'] = 'toolmanager'
from matplotlib.backend_tools import ToolBase, ToolToggleBase


class ListTools(ToolBase):
    '''List all the tools controlled by the `ToolManager`'''
    # keyboard shortcut
    default_keymap = 'm'
    description = 'List Tools'

    def trigger(self, *args, **kwargs):
        print('_' * 80)
        print("{0:12} {1:45} {2}".format(
            'Name (id)', 'Tool description', 'Keymap'))
        print('-' * 80)
        tools = self.toolmanager.tools
        for name in sorted(tools):
            if not tools[name].description:
                continue
            keys = ', '.join(sorted(self.toolmanager.get_tool_keymap(name)))
            print("{0:12} {1:45} {2}".format(
                name, tools[name].description, keys))
        print('_' * 80)
        print("Active Toggle tools")
        print("{0:12} {1:45}".format("Group", "Active"))
        print('-' * 80)
        for group, active in self.toolmanager.active_toggle.items():
            print("{0:12} {1:45}".format(str(group), str(active)))


class GroupHideTool(ToolToggleBase):
    '''Show lines with a given gid'''
    default_keymap = 'G'
    description = 'Show by gid'
    default_toggled = True

    def __init__(self, *args, gid, **kwargs):
        self.gid = gid
        super().__init__(*args, **kwargs)

    def enable(self, *args):
        self.set_lines_visibility(True)

    def disable(self, *args):
        self.set_lines_visibility(False)

    def set_lines_visibility(self, state):
        for ax in self.figure.get_axes():
            for line in ax.get_lines():
                if line.get_gid() == self.gid:
                    line.set_visible(state)
        self.figure.canvas.draw()


# (cont.)```
​```python
fig = plt.figure()
plt.plot([1, 2, 3], gid='mygroup')
plt.plot([2, 3, 4], gid='unknown')
plt.plot([3, 2, 1], gid='mygroup')

# Add the custom tools that we created
fig.canvas.manager.toolmanager.add_tool('List', ListTools)
fig.canvas.manager.toolmanager.add_tool('Show', GroupHideTool, gid='mygroup')

# Add an existing tool to new group `foo`.
# It can be added as many times as we want
fig.canvas.manager.toolbar.add_tool('zoom', 'foo')

# Remove the forward button
fig.canvas.manager.toolmanager.remove_tool('forward')

# To add a custom tool to the toolbar at specific location inside
# the navigation group
fig.canvas.manager.toolbar.add_tool('Show', 'navigation', 1)

#!@NOTICE! fig.canvas.manager.toolbar.add_tool('List', 'navigation', 2)
plt.show()
```

### Steps 分步骤

注意这里的 line loc 是上一小节的第二部分，但是这两个部分本应在同一个文件内的，这里分开只是为了方便分步骤查看哪些命令起到了什么作用。

1. after line 04: 画出原始图像，即未修改前的 GUI 图形
2. after line 08: 仍与上图相同
3. after line 12: 导航栏最后面多了一个搜索图标，这两个点击其中任意一个，都会与另一个同步
4. after line 15: 导航栏去掉前向箭头
5. after line 19: 导航栏的位置下标为 1 处，增加自定义 Show 按钮，取消点击则绿色和蓝色线条消失
6. after line 21: 导航栏上增加自定义 List 按钮，点击后在终端显示相关信息 (详见下一小节) ，此外这里取消了 Show 的点击状态

after 04 lines: <img src="/images/2020-03/0322_Pyplot_toolbar_line4.png" width="37%">
after 12 lines: <img src="/images/2020-03/0322_Pyplot_toolbar_line12.png" width="37%">
after 15 lines: <img src="/images/2020-03/0322_Pyplot_toolbar_line15.png" width="37%">
after 19 lines: <img src="/images/2020-03/0322_Pyplot_toolbar_line19.png" width="37%">
after 21 lines: <img src="/images/2020-03/0322_Pyplot_toolbar_addlist.png" width="37%">

### add 'List' and cancel 'Show' click

> <table><td bgcolor=#00FA9A style="font-weight: bold;">
    fig.canvas.manager.toolbar.add_tool('List', 'navigation', 2)
    plt.show()
</td></table>
> 

```shell
________________________________________________________________________________
Name (id)    Tool description                              Keymap
--------------------------------------------------------------------------------
List         List Tools                                    m
Show         Show by gid                                   G
allnav       Enables all axes toolmanager                  a
back         Back to previous view                         backspace, c, left
fullscreen   Toogle Fullscreen mode                        ctrl+f, f
grid         Toogle major grids                            g
grid_minor   Toogle major and minor grids
home         Reset original view                           h, home, r
nav          Enables one axes toolmanager                  1, 2, 3, 4, 5, 6, 7, 8, 9
pan          Pan axes with left mouse, zoom with right     p
quit         Quit the figure                               cmd+w, ctrl+w, q
quit_all     Quit all figures                              Q, W, cmd+W
save         Save the figure                               ctrl+s, s
subplots     Configure subplots
xscale       Toogle Scale X axis                           L, k
yscale       Toogle Scale Y axis                           l
zoom         Zoom to rectangle                             o
________________________________________________________________________________
Active Toggle tools
Group        Active
--------------------------------------------------------------------------------
default      None
None         {'Show'}
PS C:\Users\Lenovo\Documents\> 
```

## Buttons

Constructing a simple button GUI to modify a sine wave.  
The ***next*** and ***previous*** button widget helps visualize the wave with new frequencies.

[ref](https://matplotlib.org/3.1.1/gallery/widgets/buttons.html#sphx-glr-gallery-widgets-buttons-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_buttons_001.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import Button

freqs = np.arange(2, 20, 3)

fig, ax = plt.subplots()
plt.subplots_adjust(bottom=0.2)
t = np.arange(0.0, 1.0, 0.001)
s = np.sin(2*np.pi*freqs[0]*t)
l, = plt.plot(t, s, lw=2)


class Index(object):
    ind = 0

    def next(self, event):
        self.ind += 1
        i = self.ind % len(freqs)
        ydata = np.sin(2 * np.pi * freqs[i] * t)
        l.set_ydata(ydata)
        plt.draw()

    def prev(self, event):
        self.ind -= 1
        i = self.ind % len(freqs)
        ydata = np.sin(2 * np.pi * freqs[i] * t)
        l.set_ydata(ydata)
        plt.draw()

callback = Index()
axprev = plt.axes([0.7, 0.05, 0.1, 0.075])
axnext = plt.axes([0.81, 0.05, 0.1, 0.075])
bnext = Button(axnext, 'Next')
bnext.on_clicked(callback.next)
bprev = Button(axprev, 'Previous')
bprev.on_clicked(callback.prev)

plt.show()
```

## Rectangle Selector

鼠标单击某处，将鼠标移至某个位置，然后释放按钮。 此类提供单击和释放事件，并且从单击点到实际鼠标位置（在同一轴上）绘制一条线或一个框，直到释放按钮为止。 在方法 "self.ignore()" 中，检查 eventpress 和 eventrelease 中的按钮是否相同。

[ref](https://matplotlib.org/3.1.1/gallery/widgets/rectangle_selector.html#sphx-glr-gallery-widgets-rectangle-selector-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_rectangle_selector_001.png" width="67%">

```python
from matplotlib.widgets import RectangleSelector
import numpy as np
import matplotlib.pyplot as plt


def line_select_callback(eclick, erelease):
    'eclick and erelease are the press and release events'
    x1, y1 = eclick.xdata, eclick.ydata
    x2, y2 = erelease.xdata, erelease.ydata
    print("(%3.2f, %3.2f) --> (%3.2f, %3.2f)" % (x1, y1, x2, y2))
    print(" The button you used were: %s %s" % (eclick.button, erelease.button))


def toggle_selector(event):
    print(' Key pressed.')
    if event.key in ['Q', 'q'] and toggle_selector.RS.active:
        print(' RectangleSelector deactivated.')
        toggle_selector.RS.set_active(False)
    if event.key in ['A', 'a'] and not toggle_selector.RS.active:
        print(' RectangleSelector activated.')
        toggle_selector.RS.set_active(True)


fig, current_ax = plt.subplots()                 # make a new plotting range
N = 100000                                       # If N is large one can see
x = np.linspace(0.0, 10.0, N)                    # improvement by use blitting!

plt.plot(x, +np.sin(.2*np.pi*x), lw=3.5, c='b', alpha=.7)  # plot something
plt.plot(x, +np.cos(.2*np.pi*x), lw=3.5, c='r', alpha=.5)
plt.plot(x, -np.sin(.2*np.pi*x), lw=3.5, c='g', alpha=.3)

print("\n      click  -->  release")

# drawtype is 'box' or 'line' or 'none'
toggle_selector.RS = RectangleSelector(current_ax, line_select_callback,
                                       drawtype='box', useblit=True,
                                       button=[1, 3],  # don't use middle button
                                       minspanx=5, minspany=5,
                                       spancoords='pixels',
                                       interactive=True)
plt.connect('key_press_event', toggle_selector)
plt.show()
```

### 鼠标点击各情形

1. 鼠标点击左键，拖动可得一个粉红色窗口
2. 注意屏幕上同时出现以下几行，其中 Key pressed. 出现两行代表截图一次，这里有四行，也就意味着截此张图时其实已经是第二次截图了
  >     click  -->  release
  >     (3.14, -0.00) --> (6.38, 0.71)
  >     The botton you used were: 1 1
3. 换个地方重新拖动，可得
  > (1.36, -0.61) --> (7.53, 0.20)
  >  The button you used were: 1 1
4. 注意 button 一行的数字，如果是鼠标右键点击该矩形则出现 3 3 ，若是左键点击则显示 1 1

<!--width="67%"-->
<!--gp 1-5, 8-7 5-3-->

{% gp 4-3 %}
<img src="/images/2020-03/0322_Pyplot_rect1a.png">
<img src="/images/2020-03/0322_Pyplot_rect1b.png">
<img src="/images/2020-03/0322_Pyplot_rect1c.png">
<img src="/images/2020-03/0322_Pyplot_rect1d.png">
{% endgp %}

## Textbox

Allowing text input with the Textbox widget.  
You can use the Textbox widget to let users provide any text that needs to be displayed, including formulas. You can use a submit button to create plots with the given input.

[ref](https://matplotlib.org/3.1.1/gallery/widgets/textbox.html#sphx-glr-gallery-widgets-textbox-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_textbox_001.png" width="67%">

最下方的文本框可输入公式，输入后回车可得相应的图象，如
{% gp 1-2 %}
<img src="/images/2020-03/0322_Pyplot_textbox3.png">
<img src="/images/2020-03/0322_Pyplot_textbox4.png">
{% endgp %}

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import TextBox
fig, ax = plt.subplots()
plt.subplots_adjust(bottom=0.2)
t = np.arange(-2.0, 2.0, 0.001)
s = t ** 2
initial_text = "t ** 2"
l, = plt.plot(t, s, lw=2)


def submit(text):
    ydata = eval(text)
    l.set_ydata(ydata)
    ax.set_ylim(np.min(ydata), np.max(ydata))
    plt.draw()

axbox = plt.axes([0.1, 0.05, 0.8, 0.075])
text_box = TextBox(axbox, 'Evaluate', initial=initial_text)
text_box.on_submit(submit)

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

## Custom projection

通过减轻 Matplotlib 的许多功能来展示 Hammer 投影。 
[ref](https://matplotlib.org/3.1.1/gallery/misc/custom_projection.html#sphx-glr-gallery-misc-custom-projection-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_custom_projection_001.png" width="67%">

```python
#! Hammer projection

import matplotlib
from matplotlib.axes import Axes
from matplotlib.patches import Circle
from matplotlib.path import Path
from matplotlib.ticker import NullLocator, Formatter, FixedLocator
from matplotlib.transforms import Affine2D, BboxTransformTo, Transform
from matplotlib.projections import register_projection
import matplotlib.spines as mspines
import matplotlib.axis as maxis
import numpy as np

rcParams = matplotlib.rcParams

# This example projection class is rather long, but it is designed to
# illustrate many features, not all of which will be used every time.
# It is also common to factor out a lot of these methods into common
# code used by a number of projections with similar characteristics
# (see geo.py).


class GeoAxes(Axes):
    """
    An abstract base class for geographic projections
    """
    class ThetaFormatter(Formatter):
        """
        Used to format the theta tick labels.  Converts the native
        unit of radians into degrees and adds a degree symbol.
        """
        def __init__(self, round_to=1.0):
            self._round_to = round_to

        def __call__(self, x, pos=None):
            degrees = np.round(np.rad2deg(x) / self._round_to) * self._round_to
            if rcParams['text.usetex'] and not rcParams['text.latex.unicode']:
                return r"$%0.0f^\circ$" % degrees
            else:
                return "%0.0f\N{DEGREE SIGN}" % degrees

    RESOLUTION = 75

    def _init_axis(self):
        self.xaxis = maxis.XAxis(self)
        self.yaxis = maxis.YAxis(self)
        # Do not register xaxis or yaxis with spines -- as done in
        # Axes._init_axis() -- until GeoAxes.xaxis.cla() works.
        # self.spines['geo'].register_axis(self.yaxis)
        self._update_transScale()

    def cla(self):
        Axes.cla(self)

        self.set_longitude_grid(30)
        self.set_latitude_grid(15)
        self.set_longitude_grid_ends(75)
        self.xaxis.set_minor_locator(NullLocator())
        self.yaxis.set_minor_locator(NullLocator())
        self.xaxis.set_ticks_position('none')
        self.yaxis.set_ticks_position('none')
        self.yaxis.set_tick_params(label1On=True)
        # Why do we need to turn on yaxis tick labels, but
        # xaxis tick labels are already on?

        self.grid(rcParams['axes.grid'])

        Axes.set_xlim(self, -np.pi, np.pi)
        Axes.set_ylim(self, -np.pi / 2.0, np.pi / 2.0)

    def _set_lim_and_transforms(self):
        # A (possibly non-linear) projection on the (already scaled) data

        # There are three important coordinate spaces going on here:
        #
        #    1. Data space: The space of the data itself
        #
        #    2. Axes space: The unit rectangle (0, 0) to (1, 1)
        #       covering the entire plot area.
        #
        #    3. Display space: The coordinates of the resulting image,
        #       often in pixels or dpi/inch.

        # This function makes heavy use of the Transform classes in
        # ``lib/matplotlib/transforms.py.`` For more information, see
        # the inline documentation there.

        # The goal of the first two transformations is to get from the
        # data space (in this case longitude and latitude) to axes
        # space.  It is separated into a non-affine and affine part so
        # that the non-affine part does not have to be recomputed when
        # a simple affine change to the figure has been made (such as
        # resizing the window or changing the dpi).

        # 1) The core transformation from data space into
        # rectilinear space defined in the HammerTransform class.
        self.transProjection = self._get_core_transform(self.RESOLUTION)

        # 2) The above has an output range that is not in the unit
        # rectangle, so scale and translate it so it fits correctly
        # within the axes.  The peculiar calculations of xscale and
        # yscale are specific to a Aitoff-Hammer projection, so don't
        # worry about them too much.
        self.transAffine = self._get_affine_transform()

        # 3) This is the transformation from axes space to display
        # space.
        self.transAxes = BboxTransformTo(self.bbox)

        # Now put these 3 transforms together -- from data all the way
        # to display coordinates.  Using the '+' operator, these
        # transforms will be applied "in order".  The transforms are
        # automatically simplified, if possible, by the underlying
        # transformation framework.
        self.transData = \
            self.transProjection + \
            self.transAffine + \
            self.transAxes

        # The main data transformation is set up.  Now deal with
        # gridlines and tick labels.

        # Longitude gridlines and ticklabels.  The input to these
        # transforms are in display space in x and axes space in y.
        # Therefore, the input values will be in range (-xmin, 0),
        # (xmax, 1).  The goal of these transforms is to go from that
        # space to display space.  The tick labels will be offset 4
        # pixels from the equator.
        self._xaxis_pretransform = \
            Affine2D() \
            .scale(1.0, self._longitude_cap * 2.0) \
            .translate(0.0, -self._longitude_cap)
        self._xaxis_transform = \
            self._xaxis_pretransform + \
            self.transData
        self._xaxis_text1_transform = \
            Affine2D().scale(1.0, 0.0) + \
            self.transData + \
            Affine2D().translate(0.0, 4.0)
        self._xaxis_text2_transform = \
            Affine2D().scale(1.0, 0.0) + \
            self.transData + \
            Affine2D().translate(0.0, -4.0)

        # Now set up the transforms for the latitude ticks.  The input to
        # these transforms are in axes space in x and display space in
        # y.  Therefore, the input values will be in range (0, -ymin),
        # (1, ymax).  The goal of these transforms is to go from that
        # space to display space.  The tick labels will be offset 4
        # pixels from the edge of the axes ellipse.
        yaxis_stretch = Affine2D().scale(np.pi*2, 1).translate(-np.pi, 0)
        yaxis_space = Affine2D().scale(1.0, 1.1)
        self._yaxis_transform = \
            yaxis_stretch + \
            self.transData
        yaxis_text_base = \
            yaxis_stretch + \
            self.transProjection + \
            (yaxis_space +
             self.transAffine +
             self.transAxes)
        self._yaxis_text1_transform = \
            yaxis_text_base + \
            Affine2D().translate(-8.0, 0.0)
        self._yaxis_text2_transform = \
            yaxis_text_base + \
            Affine2D().translate(8.0, 0.0)

    def _get_affine_transform(self):
        transform = self._get_core_transform(1)
        xscale, _ = transform.transform_point((np.pi, 0))
        _, yscale = transform.transform_point((0, np.pi / 2.0))
        return Affine2D() \
            .scale(0.5 / xscale, 0.5 / yscale) \
            .translate(0.5, 0.5)

    def get_xaxis_transform(self, which='grid'):
        """
        Override this method to provide a transformation for the
        x-axis tick labels.

        Returns a tuple of the form (transform, valign, halign)
        """
        if which not in ['tick1', 'tick2', 'grid']:
            raise ValueError(
                "'which' must be one of 'tick1', 'tick2', or 'grid'")
        return self._xaxis_transform

    def get_xaxis_text1_transform(self, pad):
        return self._xaxis_text1_transform, 'bottom', 'center'

    def get_xaxis_text2_transform(self, pad):
        """
        Override this method to provide a transformation for the
        secondary x-axis tick labels.

        Returns a tuple of the form (transform, valign, halign)
        """
        return self._xaxis_text2_transform, 'top', 'center'

    def get_yaxis_transform(self, which='grid'):
        """
        Override this method to provide a transformation for the
        y-axis grid and ticks.
        """
        if which not in ['tick1', 'tick2', 'grid']:
            raise ValueError(
                "'which' must be one of 'tick1', 'tick2', or 'grid'")
        return self._yaxis_transform

    def get_yaxis_text1_transform(self, pad):
        """
        Override this method to provide a transformation for the
        y-axis tick labels.

        Returns a tuple of the form (transform, valign, halign)
        """
        return self._yaxis_text1_transform, 'center', 'right'

    def get_yaxis_text2_transform(self, pad):
        """
        Override this method to provide a transformation for the
        secondary y-axis tick labels.

        Returns a tuple of the form (transform, valign, halign)
        """
        return self._yaxis_text2_transform, 'center', 'left'

    def _gen_axes_patch(self):
        """
        Override this method to define the shape that is used for the
        background of the plot.  It should be a subclass of Patch.

        In this case, it is a Circle (that may be warped by the axes
        transform into an ellipse).  Any data and gridlines will be
        clipped to this shape.
        """
        return Circle((0.5, 0.5), 0.5)

    def _gen_axes_spines(self):
        return {'geo': mspines.Spine.circular_spine(self, (0.5, 0.5), 0.5)}

    def set_yscale(self, *args, **kwargs):
        if args[0] != 'linear':
            raise NotImplementedError

    # Prevent the user from applying scales to one or both of the
    # axes.  In this particular case, scaling the axes wouldn't make
    # sense, so we don't allow it.
    set_xscale = set_yscale

    # Prevent the user from changing the axes limits.  In our case, we
    # want to display the whole sphere all the time, so we override
    # set_xlim and set_ylim to ignore any input.  This also applies to
    # interactive panning and zooming in the GUI interfaces.
    def set_xlim(self, *args, **kwargs):
        raise TypeError("It is not possible to change axes limits "
                        "for geographic projections. Please consider "
                        "using Basemap or Cartopy.")

    set_ylim = set_xlim

    def format_coord(self, lon, lat):
        """
        Override this method to change how the values are displayed in
        the status bar.

        In this case, we want them to be displayed in degrees N/S/E/W.
        """
        lon, lat = np.rad2deg([lon, lat])
        if lat >= 0.0:
            ns = 'N'
        else:
            ns = 'S'
        if lon >= 0.0:
            ew = 'E'
        else:
            ew = 'W'
        return ('%f\N{DEGREE SIGN}%s, %f\N{DEGREE SIGN}%s'
                % (abs(lat), ns, abs(lon), ew))

    def set_longitude_grid(self, degrees):
        """
        Set the number of degrees between each longitude grid.

        This is an example method that is specific to this projection
        class -- it provides a more convenient interface to set the
        ticking than set_xticks would.
        """
        # Skip -180 and 180, which are the fixed limits.
        grid = np.arange(-180 + degrees, 180, degrees)
        self.xaxis.set_major_locator(FixedLocator(np.deg2rad(grid)))
        self.xaxis.set_major_formatter(self.ThetaFormatter(degrees))

    def set_latitude_grid(self, degrees):
        """
        Set the number of degrees between each longitude grid.

        This is an example method that is specific to this projection
        class -- it provides a more convenient interface than
        set_yticks would.
        """
        # Skip -90 and 90, which are the fixed limits.
        grid = np.arange(-90 + degrees, 90, degrees)
        self.yaxis.set_major_locator(FixedLocator(np.deg2rad(grid)))
        self.yaxis.set_major_formatter(self.ThetaFormatter(degrees))

    def set_longitude_grid_ends(self, degrees):
        """
        Set the latitude(s) at which to stop drawing the longitude grids.

        Often, in geographic projections, you wouldn't want to draw
        longitude gridlines near the poles.  This allows the user to
        specify the degree at which to stop drawing longitude grids.

        This is an example method that is specific to this projection
        class -- it provides an interface to something that has no
        analogy in the base Axes class.
        """
        self._longitude_cap = np.deg2rad(degrees)
        self._xaxis_pretransform \
            .clear() \
            .scale(1.0, self._longitude_cap * 2.0) \
            .translate(0.0, -self._longitude_cap)

    def get_data_ratio(self):
        """
        Return the aspect ratio of the data itself.

        This method should be overridden by any Axes that have a
        fixed data ratio.
        """
        return 1.0

    # Interactive panning and zooming is not supported with this projection,
    # so we override all of the following methods to disable it.
    def can_zoom(self):
        """
        Return *True* if this axes supports the zoom box button functionality.
        This axes object does not support interactive zoom box.
        """
        return False

    def can_pan(self):
        """
        Return *True* if this axes supports the pan/zoom button functionality.
        This axes object does not support interactive pan/zoom.
        """
        return False

    def start_pan(self, x, y, button):
        pass

    def end_pan(self):
        pass

    def drag_pan(self, button, key, x, y):
        pass


class HammerAxes(GeoAxes):
    """
    A custom class for the Aitoff-Hammer projection, an equal-area map
    projection.

    https://en.wikipedia.org/wiki/Hammer_projection
    """

    # The projection must specify a name. This will be used by the
    # user to select the projection,
    # i.e. ``subplot(111, projection='custom_hammer')``.
    name = 'custom_hammer'

    class HammerTransform(Transform):
        """
        The base Hammer transform.
        """
        input_dims = 2
        output_dims = 2
        is_separable = False

        def __init__(self, resolution):
            """
            Create a new Hammer transform.  Resolution is the number of steps
            to interpolate between each input line segment to approximate its
            path in curved Hammer space.
            """
            Transform.__init__(self)
            self._resolution = resolution

        def transform_non_affine(self, ll):
            longitude, latitude = ll.T

            # Pre-compute some values
            half_long = longitude / 2
            cos_latitude = np.cos(latitude)
            sqrt2 = np.sqrt(2)

            alpha = np.sqrt(1 + cos_latitude * np.cos(half_long))
            x = (2 * sqrt2) * (cos_latitude * np.sin(half_long)) / alpha
            y = (sqrt2 * np.sin(latitude)) / alpha
            return np.column_stack([x, y])

        def transform_path_non_affine(self, path):
            # vertices = path.vertices
            ipath = path.interpolated(self._resolution)
            return Path(self.transform(ipath.vertices), ipath.codes)

        def inverted(self):
            return HammerAxes.InvertedHammerTransform(self._resolution)

    class InvertedHammerTransform(Transform):
        input_dims = 2
        output_dims = 2
        is_separable = False

        def __init__(self, resolution):
            Transform.__init__(self)
            self._resolution = resolution

        def transform_non_affine(self, xy):
            x, y = xy.T
            z = np.sqrt(1 - (x / 4) ** 2 - (y / 2) ** 2)
            longitude = 2 * np.arctan((z * x) / (2 * (2 * z ** 2 - 1)))
            latitude = np.arcsin(y*z)
            return np.column_stack([longitude, latitude])

        def inverted(self):
            return HammerAxes.HammerTransform(self._resolution)

    def __init__(self, *args, **kwargs):
        self._longitude_cap = np.pi / 2.0
        GeoAxes.__init__(self, *args, **kwargs)
        self.set_aspect(0.5, adjustable='box', anchor='C')
        self.cla()

    def _get_core_transform(self, resolution):
        return self.HammerTransform(resolution)


# Now register the projection with Matplotlib so the user can select it.
register_projection(HammerAxes)


if __name__ == '__main__':
    import matplotlib.pyplot as plt
    # Now make a simple example using the custom projection.
    plt.subplot(111, projection="custom_hammer")
    p = plt.plot([-1, 1, 1], [-1, -1, 1], "o-")
    plt.grid(True)

    plt.show()
```



# Not usually used

不太常用的


## Findobj.Demo

Recursively find all objects that match some criteria. [ref](https://matplotlib.org/3.1.1/gallery/misc/findobj_demo.html#sphx-glr-gallery-misc-findobj-demo-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_findobj_demo_001.png" width="67%">

如果只要前 19 行，则可得图形，即在没有使用 findobj 改变颜色和字体之前  
<img src="/images/2020-03/0322_Pyplot_findobj.png" width="67%">

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.text as text

a = np.arange(0, 3, .02)
b = np.arange(0, 3, .02)
c = np.exp(a)
d = c[::-1]

fig, ax = plt.subplots()
plt.plot(a, c, 'k--', a, d, 'k:', a, c + d, 'k')
plt.legend(('Model length', 'Data length', 'Total message length'),
           loc='upper center', shadow=True)
plt.ylim([-1, 20])
plt.grid(False)
plt.xlabel('Model complexity --->')
plt.ylabel('Message length --->')
plt.title('Minimum Message Length')
# plt.show()

# match on arbitrary function
def myfunc(x):
    return hasattr(x, 'set_color') and not hasattr(x, 'set_facecolor')

for o in fig.findobj(myfunc):
    o.set_color('blue')

# match on class instances
for o in fig.findobj(text.Text):
    o.set_fontstyle('italic')

plt.show()
```

## Customize Rc
[ref](https://matplotlib.org/3.1.1/gallery/misc/customize_rc.html#sphx-glr-gallery-misc-customize-rc-py)
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_customize_rc_001.png" width="67%">

```python
#! Customize Rc
'''
def set_pub():
    rc('font', weight='bold')    # bold fonts are easier to see
    rc('tick', labelsize=15)     # tick labels bigger
    rc('lines', lw=1, color='k') # thicker black lines
    rc('grid', c='0.5', ls='-', lw=0.5)  # solid gray grid lines
    rc('savefig', dpi=300)       # higher res outputs

>>> set_pub()
>>> subplot(111)
>>> plot([1,2,3])
>>> savefig('myfig')
>>> rcdefaults()  # restore the defaults
'''

import matplotlib.pyplot as plt

plt.subplot(311)
plt.plot([1, 2, 3])

# the axes attributes need to be set before the call to subplot
plt.rc('font', weight='bold')
plt.rc('xtick.major', size=5, pad=7)
plt.rc('xtick', labelsize=15)

# using aliases for color, linestyle and linewidth; gray, solid, thick
plt.rc('grid', c='0.5', ls='-', lw=5)
plt.rc('lines', lw=2, color='g')
plt.subplot(312)

plt.plot([1, 2, 3])
plt.grid(True)

plt.rcdefaults()
plt.subplot(313)
plt.plot([1, 2, 3])
plt.grid(True)
plt.show()
```

## Multipage FDF

[ref](https://matplotlib.org/3.1.1/gallery/misc/multipage_pdf.html#sphx-glr-gallery-misc-multipage-pdf-py)
这是一个创建具有多个页面的 pdf 文件以及向 pdf 文件添加元数据和注释的演示。  
如果要通过 LaTeX 使用多页 pdf文件，则需要使用从 matplotlib.backends.backend_pgf 导入 PdfPages。 但是，此版本不支持 ***attach_note***。

下面的代码最终生成一个名为 ***multipage_pdf.pdf*** 的文件，里面是 3 个图形，即 
{% gp 1-3 %}
<img src="/images/2020-03/0322_Pyplot_multipdf1.png">
<img src="/images/2020-03/0322_Pyplot_multipdf2.png">
<img src="/images/2020-03/0322_Pyplot_multipdf3.png">
{% endgp %}

```python
import datetime
import numpy as np
from matplotlib.backends.backend_pdf import PdfPages
import matplotlib.pyplot as plt

# Create the PdfPages object to which we will save the pages:
# The with statement makes sure that the PdfPages object is closed properly at
# the end of the block, even if an Exception occurs.
with PdfPages('multipage_pdf.pdf') as pdf:
    plt.figure(figsize=(3, 3))
    plt.plot(range(7), [3, 1, 4, 1, 5, 9, 2], 'r-o')
    plt.title('Page One')
    pdf.savefig()  # saves the current figure into a pdf page
    plt.close()

    # if LaTeX is not installed or error caught, change to `usetex=False`
    plt.rc('text', usetex=True)
    plt.figure(figsize=(8, 6))
    x = np.arange(0, 5, 0.1)
    plt.plot(x, np.sin(x), 'b-')
    plt.title('Page Two')
    pdf.attach_note("plot of sin(x)")  # you can add a pdf note to
                                       # attach metadata to a page
    pdf.savefig()
    plt.close()

    plt.rc('text', usetex=False)
    fig = plt.figure(figsize=(4, 5))
    plt.plot(x, x ** 2, 'ko')
    plt.title('Page Three')
    pdf.savefig(fig)  # or you can pass a Figure object to pdf.savefig
    plt.close()

    # We can also set the file's metadata via the PdfPages object:
    d = pdf.infodict()
    d['Title'] = 'Multipage PDF Example'
    d['Author'] = 'Jouni K. Sepp\xe4nen'
    d['Subject'] = 'How to create a multipage pdf file and set its metadata'
    d['Keywords'] = 'PdfPages multipage keywords author title subject'
    d['CreationDate'] = datetime.datetime(2009, 11, 13)
    d['ModDate'] = datetime.datetime.today()

```

## Print Stdout

print png to standard out. [ref](https://matplotlib.org/3.1.1/gallery/misc/print_stdout_sgskip.html#sphx-glr-gallery-misc-print-stdout-sgskip-py)

```python
# usage: python print_stdout.py > somefile.png

import sys
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

plt.plot([1, 2, 3])
plt.savefig(sys.stdout.buffer)
```


## Frame grabbing

[ref](https://matplotlib.org/3.1.1/gallery/animation/frame_grabbing_sgskip.html#sphx-glr-gallery-animation-frame-grabbing-sgskip-py) 直接使用 MovieWriter 抓取单个帧并将其写入文件。这避免了任何事件循环集成，因此即使在Agg后端也可以使用。不建议在交互式设置中使用它。

## Agg Buffer

[ref](https://matplotlib.org/3.1.1/gallery/misc/agg_buffer.html#sphx-glr-gallery-misc-agg-buffer-py) 使用后端agg作为RGB字符串访问图形画布，然后将其转换为数组并将其传递给Pillow进行渲染。

第一次执行时图片出错，第二次就可以了  
<img src="/images/2020-03/0322_Pyplot_aggbuffer.png" width="87%">

```python
#! Frame grabbing
#! Agg Buffer

import numpy as np

from matplotlib.backends.backend_agg import FigureCanvasAgg
import matplotlib.pyplot as plt

plt.plot([1, 2, 3])

canvas = plt.get_current_fig_manager().canvas

agg = canvas.switch_backends(FigureCanvasAgg)
agg.draw()
s, (width, height) = agg.print_to_buffer()

# Convert to a NumPy array.
X = np.frombuffer(s, np.uint8).reshape((height, width, 4))

# Pass off to PIL.
from PIL import Image
im = Image.frombytes("RGBA", (width, height), s)

# Uncomment this line to display the image using ImageMagick's `display` tool.
im.show()
```

## Dolphins [<font color=#8A2BE2>ref</font>](https://matplotlib.org/3.1.1/gallery/shapes_and_collections/dolphin.html#sphx-glr-gallery-shapes-and-collections-dolphin-py)

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

[markdown 中改变字体的颜色和背景色](https://blog.csdn.net/u010177286/article/details/50358720)  
具体颜色分类及标记可参照 [各种颜色](https://blog.csdn.net/testcs_dn/article/details/45719357/)  
[markdown编辑器语法——文字颜色、大小、字体与背景色的设置](https://blog.csdn.net/manjianchao/article/details/53668280)  


matplotlib.backends.backend_pgf.LatexError: LaTeX returned an error, probably missing font or error in preamble:  
[Source code for matplotlib.backends.backend_pgf](https://matplotlib.org/3.1.1/_modules/matplotlib/backends/backend_pgf.html)  
[PGF backend (LaTeX) on macOS: font-not-found](https://github.com/matplotlib/matplotlib/issues/10307)  
[PGF backend tests failing](https://github.com/matplotlib/matplotlib/issues/2403)  
[LaTeX 字体设置](https://www.jianshu.com/p/a67dbcd064d5)  


[如何在td中控制字体右对齐 且加粗](https://bbs.csdn.net/topics/350167336)  
[HTML <td> 标签的 height 属性](https://www.w3school.com.cn/tags/att_td_height.asp)  
[HTML中怎么去掉table中th的默认粗体](https://blog.csdn.net/u013718120/article/details/42077303)  

