---
title: Matplotlib Tutorials - 2. Examples
date: 2020-03-21 05:54:21
updated: 2020-03-21 17:39:14
categories:
  - Drafting
tags:
  - Python
  - Matplotlib
---

[Sample plots in Matplotlib](https://matplotlib.org/3.1.1/tutorials/introductory/sample_plots.html#sphx-glr-tutorials-introductory-sample-plots-py)  
[matplotlib/mpl-data/sample_data](https://github.com/matplotlib/matplotlib/tree/master/lib/matplotlib/mpl-data/sample_data)  


# Line Plot

Use [plot()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot)  
e.g., [Simple Plot](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/simple_plot.html)

```python
# coding: utf8

import matplotlib
import matplotlib.pyplot as plt
import numpy as np

# Data for plotting
t = np.arange(0.0, 2.0, 0.01)
s = 1 + np.sin(2 * np.pi * t)

fig, ax = plt.subplots()
ax.plot(t, s)

ax.plot(t, 1 + np.cos(2 * np.pi * t))
ax.legend(['sin(t)', 'cos(t)'])

ax.set(xlabel='time (s)', ylabel='voltage (mV)',
       title='About as simple as it gets, folks')
ax.grid()

fig.savefig("test.png")
plt.show()
```

<img src="/images/2020-03/0321_Case_Line.png" width="70%">

# Multiple subplots in one figure

Use [subplot()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.subplot.html#matplotlib.pyplot.subplot)  
e.g., [Multiple subplots](https://matplotlib.org/3.1.1/gallery/subplots_axes_and_figures/subplot.html)  

```python
import numpy as np
import matplotlib.pyplot as plt


x1 = np.linspace(0.0, 5.0)
x2 = np.linspace(0.0, 2.0)

y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)
y2 = np.cos(2 * np.pi * x2)

plt.subplot(2, 1, 1)
plt.plot(x1, y1, 'o-')
plt.title('A tale of 2 subplots')
plt.ylabel('Damped oscillation')

plt.subplot(2, 1, 2)
plt.plot(x2, y2, '.-')
plt.xlabel('time (s)')
plt.ylabel('Undamped')

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_subplot_001.png" width="70%">

# Images

Use [imshow()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.imshow.html#matplotlib.pyplot.imshow)  
e.g., [Image Demo](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/image_demo.html)  

## a simple bivariable normal distribution
First we'll generate a simple bivariable normal distribution

```python
import numpy as np
import matplotlib.cm as cm
import matplotlib.pyplot as plt
import matplotlib.cbook as cbook
from matplotlib.path import Path
from matplotlib.patches import PathPatch

delta = 0.025
x = y = np.arange(-3.0, 3.0, delta)
X, Y = np.meshgrid(x, y)
Z1 = np.exp(-X ** 2 - Y ** 2)
Z2 = np.exp(-(X - 1)**2 - (Y - 1)**2)
Z = (Z1 - Z2) * 2

fig, ax = plt.subplots()
im = ax.imshow(Z, interpolation='bilinear', cmap=cm.RdYlGn,
               origin='lower', extent=[-3, 3, -3, 3],
               vmax=abs(Z).max(), vmin=-abs(Z).max())

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_image_demo_001.png" width="70%">

## show images of pictures
It is also possible to show images of pictures.

```python
# A sample image
with cbook.get_sample_data('ada.png') as image_file:
    image = plt.imread(image_file)

fig, ax = plt.subplots()
ax.imshow(image)
ax.axis('off')  # clear x-axis and y-axis

# And another image
w, h = 512, 512

with cbook.get_sample_data('ct.raw.gz') as datafile:
    s = datafile.read()
A = np.frombuffer(s, np.uint16).astype(float).reshape((w, h))
A /= A.max()

fig, ax = plt.subplots()
extent = (0, 25, 0, 25)
im = ax.imshow(A, cmap=plt.cm.hot, origin='upper', extent=extent)

markers = [(15.9, 14.5), (16.8, 15)]
x, y = zip(*markers)
ax.plot(x, y, 'o')

ax.set_title('CT density')
plt.show()
```

Self-modified  
```python
import matplotlib as mpl
mpl.rcParams['examples.directory'] = './Matplotlib'

# A sample image
with cbook.get_sample_data('cat.jpg') as image_file:
    image = plt.imread(image_file)

fig, ax = plt.subplots()
ax.imshow(image)
ax.axis('off')  # clear x-axis and y-axis

# And another image
w, h = 512, 512

with cbook.get_sample_data('cat.jpg') as datafile:
    # s = datafile.read()
    s = plt.imread(datafile)
# A = np.frombuffer(s, np.uint16).astype(float).reshape((w, h))
# A /= A.max()
A = np.asarray(s)
A = A / A.max()

fig, ax = plt.subplots()
extent = (0, 25, 0, 25)
im = ax.imshow(A, cmap=plt.cm.hot, origin='upper', extent=extent)

markers = [(15.9, 14.5), (16.8, 15)]
x, y = zip(*markers)
ax.plot(x, y, 'o')
# x = (15.9, 16.8)
# y = (14.5, 15)

ax.set_title('CT density')
plt.show()
```

<img src="/images/2020-03/0321_Case_Image2a.png" width="45%">
<img src="/images/2020-03/0321_Case_Image2b.png" width="45%">

## Interpolating images

To prevent edge effects when doing interpolation, Matplotlib pads the input array with identical pixels around the edge: [e.g.,](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/image_demo.html#interpolating-images)

```python
A = np.random.rand(5, 5)

fig, axs = plt.subplots(1, 4, figsize=(12, 3))
for ax, interp in zip(axs, ['', 'nearest', 'bilinear', 'bicubic']):
    if not interp:
        ax.imshow(A)
        ax.set_title('Original Data')
        continue
    ax.imshow(A, interpolation=interp)
    ax.set_title(interp.capitalize())
    ax.grid(True)

plt.show()
```

<img src="/images/2020-03/0321_Case_Image3.png" width="100%">

## specify whether images should be

You can specify whether images should be plotted with the array origin x[0,0] in the upper left or lower right by using the origin parameter. You can also control the default setting image.origin in your matplotlibrc file. For more on this topic see the complete guide on origin and extent.  
您可以使用 origin 参数指定是使用数组原点 x[0,0] 在左上还是在右下来绘制图像。 您还可以在 matplotlibrc 文件中控制默认设置 image.origin。 有关此主题的更多信息，请参见有关起源和范围的完整指南。

```python
x = np.arange(120).reshape((10, 12))

interp = 'bilinear'
fig, axs = plt.subplots(nrows=2, sharex=True, figsize=(3, 5))
axs[0].set_title('blue should be up')
axs[0].imshow(x, origin='upper', interpolation=interp)

axs[1].set_title('blue should be down')
axs[1].imshow(x, origin='lower', interpolation=interp)
plt.show()
```

```python
x = plt.imread('./Matplotlib/cat.jpg')

interp = 'bilinear'
fig, axs = plt.subplots(nrows=2, sharex=True, figsize=(5, 4))
axs[0].set_title('blue should be up')
axs[0].imshow(x, origin='upper', interpolation=interp)

axs[1].set_title('blue should be down')
axs[1].imshow(x, origin='lower', interpolation=interp)
plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_image_demo_005.png" width="50%">
<img src="/images/2020-03/0321_Case_Image4b.png" width="50%">

## show an image using a clip path
Finally, we'll show an image using a clip path

```python

delta = 0.025
x = y = np.arange(-3.0, 3.0, delta)
X, Y = np.meshgrid(x, y)
Z1 = np.exp(-X**2 - Y**2)
Z2 = np.exp(-(X - 1)**2 - (Y - 1)**2)
Z = (Z1 - Z2) * 2

path = Path([[0, 1], [1, 0], [0, -1], [-1, 0], [0, 1]])
patch = PathPatch(path, facecolor='none')

fig, ax = plt.subplots()
ax.add_patch(patch)

im = ax.imshow(Z, interpolation='bilinear', # cmap=cm.gray,
               cmap=cm.RdYlGn,
               origin='lower', # extent=[-3, 3, -3, 3],
               extent=[-1.1, 1.1, -1.1, 1.1],
               clip_path=patch, clip_on=True)
im.set_clip_path(patch)

'''
origin = 'lower' # 'upper'
im = ax.imshow(Z, interpolation='bilinear', # cmap=cm.gray,
               cmap=cm.RdYlGn, origin=origin,
               # origin='upper', # extent=[-3, 3, -3, 3],
               extent=[-1.1, 1.1, -1.1, 1.1],
               clip_path=patch, clip_on=True)
im.set_clip_path(patch)
# ax.set_title('origin="upper"')
ax.set_title('origin="{}"'.format(origin))
'''

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_image_demo_006.png" width="25%">
<img src="/images/2020-03/0321_Case_Image5b.png" width="25%">
<img src="/images/2020-03/0321_Case_Image5c.png" width="25%">
<img src="/images/2020-03/0321_Case_Image5d.png" width="25%">


# Contouring and pseudocolor

[Example comparing pcolormesh() and contour() for plotting two-dimensional data](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/pcolormesh_levels.html)  
[pcolormesh()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.pcolormesh.html#matplotlib.pyplot.pcolormesh) 
[contour()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.contour.html#matplotlib.pyplot.contour) 

```python
import matplotlib
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

# contours are *point* based plots, so convert our bounds into point
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

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_pcolormesh_levels_001.png" width="70%">

# Histograms

Using [hist()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.hist.html#matplotlib.pyplot.hist)  
e.g., Histogram Features [Demo of the histogram (hist) function with a few features](https://matplotlib.org/3.1.1/gallery/statistics/histogram_features.html)  

```python
import matplotlib
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(19680801)

# example data
mu = 100  # mean of distribution
sigma = 15  # standard deviation of distribution
x = mu + sigma * np.random.randn(437)

num_bins = 50

fig, ax = plt.subplots()

# the histogram of the data
n, bins, patches = ax.hist(x, num_bins, density=1)

# add a 'best fit' line
# y = ((1 / (np.sqrt(2 * np.pi) * sigma)) *
#     np.exp(-0.5 * (1 / sigma * (bins - mu))**2))
y = 1 / (np.sqrt(2 * np.pi) * sigma) * \
    np.exp(-0.5 * (1 / sigma * (bins - mu))**2)

ax.plot(bins, y, '--')
ax.set_xlabel('Smarts')
ax.set_ylabel('Probability density')
ax.set_title(r'Histogram of IQ: $\mu=100$, $\sigma=15$')

# Tweak spacing to prevent clipping of ylabel
fig.tight_layout()
plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_histogram_features_001.png" width="70%">

```python
>>> # the histogram of the data
... n, bins, patches = ax.hist(x, num_bins, density=1)
>>>
>>> n
array([0.00236158, 0.00236158, 0.        , 0.00118079, 0.        ,
       0.00118079, 0.00236158, 0.        , 0.00472317, 0.00354238,
       0.00590396, 0.00826555, 0.00708475, 0.00944634, 0.00708475,
       0.01298872, 0.00944634, 0.00826555, 0.01653109, 0.02597743,
       0.02597743, 0.02951981, 0.02597743, 0.03542377, 0.03896615,
       0.02479664, 0.02833902, 0.01889268, 0.02597743, 0.02715822,
       0.01771189, 0.01653109, 0.01062713, 0.01889268, 0.00708475,
       0.00826555, 0.00236158, 0.00472317, 0.00354238, 0.00472317,
       0.00590396, 0.00236158, 0.        , 0.        , 0.00118079,
       0.00118079, 0.        , 0.        , 0.        , 0.00118079])
>>> bins
array([ 52.57731858,  54.51527952,  56.45324047,  58.39120142,
        60.32916237,  62.26712331,  64.20508426,  66.14304521,
        68.08100615,  70.0189671 ,  71.95692805,  73.894889  ,
        75.83284994,  77.77081089,  79.70877184,  81.64673278,
        83.58469373,  85.52265468,  87.46061563,  89.39857657,
        91.33653752,  93.27449847,  95.21245942,  97.15042036,
        99.08838131, 101.02634226, 102.9643032 , 104.90226415,
       106.8402251 , 108.77818605, 110.71614699, 112.65410794,
       114.59206889, 116.53002983, 118.46799078, 120.40595173,
       122.34391268, 124.28187362, 126.21983457, 128.15779552,
       130.09575647, 132.03371741, 133.97167836, 135.90963931,
       137.84760025, 139.7855612 , 141.72352215, 143.6614831 ,
       145.59944404, 147.53740499, 149.47536594])
>>> patches
<a list of 50 Patch objects>
>>>
```


# Paths

Using [matplotlib.path](https://matplotlib.org/3.1.1/api/path_api.html#module-matplotlib.path)  
e.g., Path Patch [PathPatch object](https://matplotlib.org/3.1.1/gallery/shapes_and_collections/path_patch.html)  

```python
import matplotlib.path as mpath
import matplotlib.patches as mpatches
import matplotlib.pyplot as plt

fig, ax = plt.subplots()

Path = mpath.Path

path_data = [
    (Path.MOVETO, (1.58, -2.57)),
    (Path.CURVE4, (0.35, -1.1)),
    (Path.CURVE4, (-1.75, 2.0)),
    (Path.CURVE4, (-0.375, 2.0)),
    (Path.LINETO, (0.85, 1.15)),
    (Path.CURVE4, (2.2, 3.2)),
    (Path.CURVE4, (3, 0.05)),
    (Path.CURVE4, (2.0, -0.5)),
    (Path.CLOSEPOLY, (1.58, -2.57)),
]
# Path.CURVE3

codes, verts = zip(*path_data)
path = mpath.Path(verts, codes)
patch = mpatches.PathPatch(path, facecolor='r', alpha=0.5)
ax.add_patch(patch)

# plot control points and connecting lines
x, y = zip(*path.vertices)
line, = ax.plot(x, y, 'go-')

ax.grid()
ax.axis('equal')
plt.show()
```

Path.CURVE4, Path.CURVE3  
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_path_patch_001.png" width="50%">
<img src="/images/2020-03/0321_Case_Path1b.png" width="50%">

```python
>>> Path = mpath.Path
>>> Path
<class 'matplotlib.path.Path'>
>>> Path.MOVETO
1
>>> Path.CURVE4, Path.CURVE3
(4, 3)
>>> Path.LINETO
2
>>> Path.CLOSEPOLY
79
>>> mpath
<module 'matplotlib.path' from 'C:\\Users\\Lenovo\\Anaconda3\\lib\\site-packages\\matplotlib\\path.py'>
>>> mpatches
<module 'matplotlib.patches' from 'C:\\Users\\Lenovo\\Anaconda3\\lib\\site-packages\\matplotlib\\patches.py'>
>>>

>>> codes
(1, 4, 4, 4, 2, 4, 4, 4, 79)
>>> verts
((1.58, -2.57), (0.35, -1.1), (-1.75, 2.0), (-0.375, 2.0), (0.85, 1.15), (2.2, 3.2), (3, 0.05), (2.0, -0.5), (1.58, -2.57))
>>> path
Path(array([[ 1.58 , -2.57 ],
       [ 0.35 , -1.1  ],
       [-1.75 ,  2.   ],
       [-0.375,  2.   ],
       [ 0.85 ,  1.15 ],
       [ 2.2  ,  3.2  ],
       [ 3.   ,  0.05 ],
       [ 2.   , -0.5  ],
       [ 1.58 , -2.57 ]]), array([ 1,  4,  4,  4,  2,  4,  4,  4, 79], dtype=uint8))
>>> patch
<matplotlib.patches.PathPatch object at 0x000001B7C79EA390>
>>>

>>> x, y = zip(*path.vertices)
>>> line, = ax.plot(x, y, 'go-')
>>>
>>> x
(1.58, 0.35, -1.75, -0.375, 0.85, 2.2, 3.0, 2.0, 1.58)
>>> y
(-2.57, -1.1, 2.0, 2.0, 1.15, 3.2, 0.05, -0.5, -2.57)
>>>
>>> path.vertices
array([[ 1.58 , -2.57 ],
       [ 0.35 , -1.1  ],
       [-1.75 ,  2.   ],
       [-0.375,  2.   ],
       [ 0.85 ,  1.15 ],
       [ 2.2  ,  3.2  ],
       [ 3.   ,  0.05 ],
       [ 2.   , -0.5  ],
       [ 1.58 , -2.57 ]])
>>> path.codes
array([ 1,  4,  4,  4,  2,  4,  4,  4, 79], dtype=uint8)
>>>
```

注意会发现，path 的第一部分是左图的绿色点坐标，起始于 (1.58, -2.57) ，顺时针旋转，终于该顶点；而 ax.plot(x, y) 则是绿色的连线，x,y 的终点均与起点相同，故最终是个封闭的图形。  
<img src="/images/2020-03/0321_Case_Path1c.png" width="100%">  
<img src="/images/2020-03/0321_Case_Path1d.png" width="100%">  

# Three-dimensional plotting

The mplot3d toolkit (see [Getting started](https://matplotlib.org/3.1.1/tutorials/toolkits/mplot3d.html#toolkit-mplot3d-tutorial) and [3D plotting](https://matplotlib.org/3.1.1/gallery/index.html#mplot3d-examples-index) )  
e.g., Surface3d [3D surface (color map)](https://matplotlib.org/3.1.1/gallery/mplot3d/surface3d.html)  

```python
# This import registers the 3D projection, but is otherwise unused.
from mpl_toolkits.mplot3d import Axes3D  # noqo: F401 unused import

import matplotlib.pyplot as plt
from matplotlib import cm
from matplotlib.ticker import LinearLocator, FormatStrFormatter
import numpy as np

fig = plt.figure()
ax = fig.gca(projection='3d')

# Make data.
X = np.arange(-5, 5, 0.25)
Y = np.arange(-5, 5, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X**2 + Y**2)
Z = np.sin(R)

# Plot the surface.
surf = ax.plot_surface(X, Y, Z, cmap=cm.coolwarm,
                       linewidth=0, antialiased=False)

# Customize the z axis.
ax.set_zlim(-1.01, 1.01)
ax.zaxis.set_major_locator(LinearLocator(10))
ax.zaxis.set_major_formatter(FormatStrFormatter('%.02f'))

# Add a color bar which maps values to colors.
fig.colorbar(surf, shrink=0.5, aspect=5)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_surface3d_001.png" width="70%">

# Streamplot

Using [streamplot()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.streamplot.html#matplotlib.pyplot.streamplot)  
e.g., Streamplot with various plotting options [Streamplot](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/plot_streamplot.html)  

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec

w = 3
Y, X = np.mgrid[-w:w:100j, -w:w:100j]
# Y.shape = X.shape = (100, 100)

U = -1 - X**2 + Y
V = 1 + X - Y**2
speed = np.sqrt(U**2 + V**2)

fig = plt.figure(figsize=(7, 9))
gs = gridspec.GridSpec(nrows=3, ncols=2, height_ratios=[1, 1, 2])

# Varying density along a streamline
ax0 = fig.add_subplot(gs[0, 0])
ax0.streamplot(X, Y, U, V, density=[0.5, 1])
ax0.set_title('Varying Density')

# Varying color along a streamline
ax1 = fig.add_subplot(gs[0, 1])
strm = ax1.streamplot(X, Y, U, V, color=U, linewidth=2, cmap='autumn')
fig.colorbar(strm.lines)
ax1.set_title('Varying Color')

# Varying line width along a streamline
ax2 = fig.add_subplot(gs[1, 0])
lw = 5*speed / speed.max()
ax2.streamplot(X, Y, U, V, density=0.6, color='k', linewidth=lw)
ax2.set_title('Varying Line Width')

# Controlling the starting points of the streamline
seed_points = np.array([[-2, -1, 0, 1, 2, -1], [-2, -1, 0, 1, 2, 2]])

ax3 = fig.add_subplot(gs[1, 1])
strm = ax3.streamplot(X, Y, U, V, color=U, linewidth=2,
                      cmap='autumn', start_points=seed_points.T)
fig.colorbar(strm.lines)
ax3.set_title('Controlling Starting Points')

# Displaying the starting points with blue symbols.
ax3.plot(seed_points[0], seed_points[1], 'bo')
ax3.set(xlim=(-w, w), ylim=(-w, w))

# Create a mask
mask = np.zeros(U.shape, dtype=bool)
mask[40:60, 40:60] = True
U[:20, :20] = np.nan
U = np.ma.array(U, mask=mask)

ax4 = fig.add_subplot(gs[2:, :])
ax4.streamplot(X, Y, U, V, color='r')
ax4.set_title('Streamplot with Masking')

ax4.imshow(~mask, extent=(-w, w, -w, w), alpha=0.5,
           interpolation='nearest', cmap='gray', aspect='auto')
ax4.set_aspect('equal')

plt.tight_layout()
plt.show()
```

aspect='equal', 'auto'  
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_plot_streamplot_001.png" width="50%">
<img src="/images/2020-03/0321_Case_Stream1b.png" width="50%">

```python
>>> 100j
100j
>>> 100j**2
(-10000+0j)
>>> 100j
100j
>>> 100j**2 <0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<' not supported between instances of 'complex' and 'int'
>>>
```

# Ellipses

refs: [Phoenix](http://www.jpl.nasa.gov/news/phoenix/main.php) [Arc](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.patches.Arc.html#matplotlib.patches.Arc)  
e.g., Ellipse Demo [Ellipse Demo](https://matplotlib.org/3.1.1/gallery/shapes_and_collections/ellipse_demo.html)  

## Ellipse Demo

```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import Ellipse

NUM = 250

ells = [Ellipse(xy=np.random.rand(2) * 10,
                width=np.random.rand(), height=np.random.rand(),
                angle=np.random.rand() * 360)
        for i in range(NUM)]

fig, ax = plt.subplots(subplot_kw={'aspect': 'equal'})
for e in ells:
    ax.add_artist(e)
    e.set_clip_box(ax.bbox)
    e.set_alpha(np.random.rand())
    e.set_facecolor(np.random.rand(3))

ax.set_xlim(0, 10)
ax.set_ylim(0, 10)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_ellipse_demo_001.png" width="70%">

## Ellipse Rotated

```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import Ellipse

# delta = 45.0  # degrees
delta = 30.0 # 60.0

angles = np.arange(0, 360 + delta, delta)
ells = [Ellipse((1, 1), 4, 2, a) for a in angles]

a = plt.subplot(111, aspect='equal')

for e in ells:
    e.set_clip_box(a.bbox)
    e.set_alpha(0.1)
    a.add_artist(e)

plt.xlim(-2, 4)
plt.ylim(-1, 3)

plt.show()
```

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_ellipse_demo_002.png" width="50%">
<img src="/images/2020-03/0321_Case_Ellipse1b.png" width="50%">

# Bar charts

Using [bar()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.bar.html#matplotlib.pyplot.bar), e.g., 
- Barchart Demo [Percentiles as horizontal bar chart](https://matplotlib.org/3.1.1/gallery/statistics/barchart_demo.html)  
- stacked bars [bar_stacked.py](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/bar_stacked.html)  
- horizontal bar charts [barh.py](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/barh.html)

## Percentiles as horizontal bar chart

<img src="/images/2020-03/0321_Case_BarChart1.png" width="100%">

```python
# Demo
import numpy as np
import matplotlib
import matplotlib.pyplot as plt
from matplotlib.ticker import MaxNLocator
from collections import namedtuple

np.random.seed(42)

Student = namedtuple('Student', ['name', 'grade', 'gender'])
Score = namedtuple('Score', ['score', 'percentile'])

# GLOBAL CONSTANTS
testNames = ['Pacer Test', 'Flexed Arm\n Hang', 'Mile Run', 'Agility',
             'Push Ups']
testMeta = dict(zip(testNames, ['laps', 'sec', 'min:sec', 'sec', '']))

def attach_ordinal(num):
    """helper function to add ordinal string to integers
    1 -> 1st
    56 -> 56th
    """
    suffixes = {str(i): v
                for i, v in enumerate(['th', 'st', 'nd', 'rd', 'th',
                                       'th', 'th', 'th', 'th', 'th'])}
    v = str(num)
    # special case early teens
    if v in {'11', '12', '13'}:
        return v + 'th'
    return v + suffixes[v[-1]]

def format_score(scr, test):
    """ Build up the score labels for the right Y-axis by first
    appending a carriage return to each string and then tacking on
    the appropriate meta information (i.e., 'laps' vs 'seconds'). We
    want the labels centered on the ticks, so if there is no meta
    info (like for pushups) then don't add the carriage return to
    the string
    """
    md = testMeta[test]
    if md:
        return '{0}\n{1}'.format(scr, md)
    else:
        return scr

def format_ycursor(y):
    y = int(y)
    if y < 0 or y >= len(testNames):
        return ''
    else:
        return testNames[y]

def plot_student_results(student, scores, cohort_size):
    # create the figure
    fig, ax1 = plt.subplots(figsize=(9, 7))
    fig.subplots_adjust(left=0.115, right=0.88)
    fig.canvas.set_window_title('Eldorado K-8 Fitness Chart')

    pos = np.arange(len(testNames))

    rects = ax1.barh(pos, [scores[k].percentile for k in testNames],
                     align='center',
                     height=0.5,
                     tick_label=testNames)
    
    ax1.set_title(student.name)

    ax1.set_xlim([0, 100])
    ax1.xaxis.set_major_locator(MaxNLocator(11))
    ax1.xaxis.grid(True, linestyle='--', which='major',
                   color='grey', alpha=.25)
    
    # Plot a solid vertical gridline to highlight the median position
    ax1.axvline(50, color='grey', alpha=0.25)

    # Set the right-hand Y-axis ticks and labels
    ax2 = ax1.twinx()

    scoreLabels = [format_score(scores[k].score, k) for k in testNames]

    # set the tick locations
    ax2.set_yticks(pos)
    # make sure that the limits are set equally on both yaxis so the
    # ticks line up
    ax2.set_ylim(ax1.get_ylim())

    # set the tick labels
    ax2.set_yticklabels(scoreLabels)

    ax2.set_ylabel('Test Scores')

    xlabel = ('Percentile Ranking Across {grade} Grade {gender}s\n'
              'Cohort Size: {cohort_size}')
    ax1.set_xlabel(xlabel.format(grade=attach_ordinal(student.grade),
                                 gender=student.gender.title(),
                                 cohort_size=cohort_size))
    
    rect_labels = []
    # Lastly, write in the ranking inside each bar to aid in interpretation
    for rect in rects:
        # Rectangle widths are already integer-valued but are floating
        # type, so it helps to remove the trailing decimal point and 0 by
        # converting width to int type
        width = int(rect.get_width())

        rankStr = attach_ordinal(width)
        # The bars aren't wide enough to print the ranking inside
        if width < 40:
            # Shift the text to the right side of the right edge
            xloc = 5
            # Black against white background
            clr = 'black'
            align = 'left'
        else:
            # Shift the text to the left side of the right edge
            xloc = -5
            # White on magenta
            clr = 'white'
            aligh = 'right'
        
        # Center the text vertically in the bar
        yloc = rect.get_y() + rect.get_height() / 2
        label = ax1.annotate(rankStr, xy=(width, yloc), xytext=(xloc, 0),
                            textcoords="offset points",
                            ha=align, va='center',
                            color=clr, weight='bold', clip_on=True)
        rect_labels.append(label)
    
    # make the interactive mouse over give the bar title
    ax2.fmt_ydata = format_ycursor
    # return all of the artists created
    return {'fig': fig,
            'ax': ax1,
            'ax_right': ax2,
            'bars': rects,
            'perc_labels': rect_labels}

student = Student('Johnny Doe', 2, 'boy')
scores = dict(zip(testNames,
                  (Score(v, p) for v, p in
                   zip(['7', '48', '12:52', '17', '14'],
                        # np.round(np.random.uniform(0, 1,
                        #                         len(testNames)) * 100, 0)))))
                        np.round(
                            np.random.uniform(0, 1, len(testNames))
                            * 100, 0)
                    ))))
cohort_size = 62  # The number of other 2nd grade boys

arts = plot_student_results(student, scores, cohort_size)
plt.show()
```


## 带误差线的分组柱状图

```python
import matplotlib.pyplot as plt

index = np.arange(5)
values = [5, 6, 3, 4, 6]
SD = [0.8, 2, 0.4, 0.9, 1.3]
plt.title('A Bar Chart')
plt.bar(index, values, yerr = SD, error_kw = {'ecolor' : '0.2', 'capsize' :6}, alpha=0.7, label = 'First')
plt.xticks(index+0.2,['a', 'b', 'c', 'd', 'e'])
plt.legend(loc=2)
plt.show()
```

<img src="/images/2020-03/0321_Case_BarChart2b.png" width="70%">

[python绘制带误差线的条形图](https://blog.csdn.net/songyunli1111/article/details/83625639)  
[绘制带有误差线的分组数据](https://zzz5.xyz/2020/01/01/python/matplotlib/python-matplotlib-03/)  
[seaborn：如何在分组的条形图上添加误差线](https://www.thinbug.com/q/42017049)  

绘制格式：   
> plt.bar(index, values, yerr = std, error_kw = {'ecolor' : '0.2', 'capsize' :6}, alpha=0.7)

- **yerr** 关键字参数：可传入包含标准差的列表
- **error_kw={}** , 接收显示误差线的关键字函数
- **eColor**：指定误差线的颜色
- **capsize** ：指定误差线两头横线的宽度
- **alpha**：控制彩色条状图的透明度， 范围 0-1

这里的 SD (Standard Deviation) 为每个 values 对应的标准差，表示个体间变异大小的指标,反映了整个样本对样本平均数的离散程度；还有一个可以选择的值为标准误 SEM (Standard Error of Mean) ，反映样本平均数对总体平均数的变异程度, 从而反映抽样误差的大小。他们之间的关系是：  
![](https://img-blog.csdnimg.cn/20181101193042637.png)


## Stacked Bar Graph

[Matplotlib带标签的分组条形图](https://www.yiibai.com/matplotlib/barchart.html)  
[python——绘制成组柱状图](https://blog.csdn.net/bingningning/article/details/79807345)  
[Matplotlib - 柱状图、直方图、条形图 bar() & barh() 所有用法详解](https://blog.csdn.net/weixin_40683253/article/details/87641416)  
[用单位对条形图分组](https://www.osgeo.cn/matplotlib/gallery/units/bar_unit_demo.html)  

<img src="/images/2020-03/0321_Case_BarChart2a.png" width="100%">

```python
# Stacked Bar Graph
import numpy as np
import matplotlib.pyplot as plt

N = 5

menMeans = (20, 35, 30, 35, 27)
womenMeans = (25, 32, 34, 20, 25)
menStd = (2, 3, 4, 1, 2)
womenStd = (3, 5, 2, 3, 3)

ind = np.arange(N)  # the x locations for the groups
width = 0.35  # the width of the bars: can also be len(x) sequence
'''
p1 = plt.bar(ind, menMeans, width, yerr=menStd)
p2 = plt.bar(ind, womenMeans, width,
            bottom=menMeans, yerr=womenStd)

plt.ylabel('Scores')
plt.title('Scores by group and gender')
plt.xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
plt.yticks(np.arange(0, 81, 10))
plt.legend((p1[0], p2[0]), ('Men', 'Women'))

# plt.show()
'''

# fig = plt.figure(figsize=(12, 7))
# subplot_kw={'aspect': 'equal'}
fig, (ax0, ax1, ax2, ax3) = plt.subplots(ncols=4, figsize=(19, 4))

# plt.subplot(131)
p1 = ax0.bar(ind, menMeans, width, yerr=menStd)
p2 = ax0.bar(ind, womenMeans, width,
            bottom=menMeans, yerr=womenStd)
ax0.set_ylabel('Scores')
ax0.set_title('Scores by group and gender')
ax0.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax0.set_yticks(np.arange(0, 81, 10))
ax0.legend((p1[0], p2[0]), ('Men', 'Women'))

# plt.subplot(132)
p1 = ax1.bar(ind, menMeans, width,
            bottom=womenMeans, yerr=menStd)
p2 = ax1.bar(ind, womenMeans, width, yerr=womenStd)
ax1.set_ylabel('Scores')
ax1.set_title('Scores by group and gender')
ax1.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax1.set_yticks(np.arange(0, 81, 10))
ax1.legend((p1[0], p2[0]), ('Men', 'Women'))

# plt.subplot(133)
rects1 = ax2.bar(ind - width/2, menMeans, width, yerr=menStd, label='Men')
rects2 = ax2.bar(ind + width/2, womenMeans, width, yerr=womenStd, label='Women')
ax2.set_ylabel('Scores')
ax2.set_title('Scores by group and gender')
ax2.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax2.set_yticks(np.arange(0, 81, 10))
ax2.legend() # ax2.legend((p1[0], p2[0]), ('Men', 'Women'))

rects1 = ax3.bar(ind - width/2, menMeans, width, label='Men')
rects2 = ax3.bar(ind + width/2, womenMeans, width, label='Women')
# Add some text for labels, title and custom x-axis tick labels, etc.
ax3.set_ylabel('Scores')
ax3.set_title('Scores by group and gender')
ax3.set_xticks(ind)
ax3.set_xticklabels(('G1', 'G2', 'G3', 'G4', 'G5')) # labels
ax3.legend()
def autolabel(rects):
    """Attach a text label above each bar in *rects*, displaying its height."""
    for rect in rects:
        height = rect.get_height()
        ax3.annotate('{}'.format(height),
                    xy=(rect.get_x() + rect.get_width()/2, height),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
autolabel(rects1)
autolabel(rects2)
ymin, ymax = ax3.get_ylim()
ax3.set_ylim((ymin, ymax + 5))

plt.tight_layout()
plt.show()
```

<img src="/images/2020-03/0321_Case_BarChart2c.png" width="100%">

```python
# fig = plt.figure(figsize=(12, 7))
# subplot_kw={'aspect': 'equal'}
fig, (ax0, ax1, ax2, ax3) = plt.subplots(ncols=4, figsize=(19, 4))#16, 3.5))

# plt.subplot(133)
p1 = ax0.bar(ind - width/2, menMeans, width, yerr=menStd, label='Men')
p2 = ax0.bar(ind + width/2, womenMeans, width, yerr=womenStd, label='Women')
ax0.set_ylabel('Scores')
ax0.set_title('Scores by group and gender')
ax0.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax0.set_yticks(np.arange(0, 81, 10))
ax0.legend() # ax2.legend((p1[0], p2[0]), ('Men', 'Women'))

p1 = ax1.bar(ind - width/2, menMeans, width, yerr=menStd)
p2 = ax1.bar(ind + width/2, womenMeans, width, yerr=womenStd)
ax1.set_ylabel('Scores')
ax1.set_title('Scores by group and gender')
ax1.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax1.set_yticks(np.arange(0, 81, 10))
ax1.legend((p1[0], p2[0]), ('Men', 'Women'))
ax1.autoscale_view()

p1 = ax2.bar(ind - width/2, menMeans, width, yerr=menStd,
            error_kw={'ecolor': '0.2', 'capsize': 6}, alpha=0.7, label='Men')
p2 = ax2.bar(ind + width/2, womenMeans, width, yerr=womenStd,
            error_kw={'ecolor': '0.4', 'capsize': 6}, alpha=0.7, label='Women')
ax2.set_ylabel('Scores')
ax2.set_title('Scores by group and gender')
ax2.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax2.set_yticks(np.arange(0, 81, 10))
ax2.legend()  # ax2.legend((p1[0], p2[0]), ('Men', 'Women'))
ax2.autoscale_view()
from matplotlib.ticker import LinearLocator, FormatStrFormatter
ax2.yaxis.set_major_locator(LinearLocator(10))
ax2.yaxis.set_major_formatter(FormatStrFormatter('%.01f'))

rects1 = ax3.bar(ind - width/2, menMeans, width, label='Men',
                yerr=menStd, error_kw={'capsize': 6})
rects2 = ax3.bar(ind + width/2, womenMeans, width, label='Women',
                yerr=womenStd, error_kw={'capsize': 6})
# Add some text for labels, title and custom x-axis tick labels, etc.
ax3.set_ylabel('Scores')
ax3.set_title('Scores by group and gender')
ax3.set_xticks(ind)
# ax2.set_xticklabels(labels) # labels=('G1', ...)
ax3.set_xticklabels(('G1', 'G2', 'G3', 'G4', 'G5'))
ax3.legend()
def autolabel(rects, minus=0):
    """Attach a text label above each bar in *rects*, displaying its height."""
    for rect in rects:
        height = rect.get_height()
        ax3.annotate('{}'.format(height),
                    # xy=(rect.get_x() + rect.get_width()/2, height),
                    xy = (rect.get_x() + width/2 * minus, height),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')
autolabel(rects1)
autolabel(rects2, minus=2)
ymin, ymax = ax3.get_ylim()
ax3.set_ylim((ymin, ymax + 5))

plt.tight_layout()
plt.show()
```

## Horizontal bar chart

<img src="/images/2020-03/0321_Case_BarChart3.png" width="100%">

```python
# Horizontal bar chart
import matplotlib.pyplot as plt
import numpy as np

# Fixing random state for reproducibility
np.random.seed(19680801)

plt.rcdefaults()
fig, ax = plt.subplots()

# Example data
people = ('Tom', 'Dick', 'Harry', 'Slim', 'Jim')
y_pos = np.arange(len(people))
performance = 3 + 10 * np.random.rand(len(people))
error = np.random.rand(len(people))

'''
ax.barh(y_pos, performance, xerr=error, align='center')
ax.set_yticks(y_pos)
ax.set_yticklabels(people)
ax.invert_yaxis()  # labels read top-to-bottom
ax.set_xlabel('Performance')
ax.set_title('How fast do you want to go today?')

# plt.show()
'''


fig, (ax0, ax1) = plt.subplots(ncols=2, figsize=(14, 4.8))

ax0.barh(y_pos, performance, xerr=error, align='center')
ax0.set_yticks(y_pos)
ax0.set_yticklabels(people)
ax0.invert_yaxis()  # labels read top-to-bottom
ax0.set_xlabel('Performance')
ax0.set_title('How fast do you want to go today?')

ax1.bar(y_pos, performance, yerr=error, align='center',
        error_kw={'ecolor': '0.37', 'capsize': 6}, alpha=0.9, label='Performance')
ax1.set_xticks(y_pos)
ax1.set_xticklabels(people)
ax1.set_ylabel('Performance')
ax1.set_title('How fast do you want to go today?')

plt.show()
```

# Pie charts

Using [pie()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.pie.html#matplotlib.pyplot.pie)  
e.g., Pie Features [Basic pie chart](https://matplotlib.org/3.1.1/gallery/pie_and_polar_charts/pie_features.html)  

<img src="/images/2020-03/0321_Case_Pie.png" width="100%">

```python
import matplotlib.pyplot as plt

# Pie chart, where the slices will be ordered and plotted counter-clockwise:
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10]
explode = (0, 0.1, 0, 0)  # only "explode" the 2nd slice (i.e. 'Hogs')

'''
fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
# plt.show()
'''


fig, (ax0, ax1) = plt.subplots(ncols=2, figsize=(14, 4.8))

ax0.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax0.axis('equal')

ax1.pie(sizes, labels=labels, autopct='%1.1f%%',
        explode=(0, 0.1, 0.15, 0), shadow=False, startangle=0)
ax1.legend()

plt.show()
```


# Tables

Using [table()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.table.html#matplotlib.pyplot.table)  
e.g., Table Demo [Table Demo](https://matplotlib.org/3.1.1/gallery/misc/table_demo.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_table_demo_001.png" width="70%">

```python
import numpy as np
import matplotlib.pyplot as plt

data = [[ 66386, 174296,  75131, 577908,  32015],
        [ 58230, 381139,  78045,  99308, 160454],
        [ 89135,  80552, 152558, 497981, 603535],
        [ 78415,  81858, 150656, 193263,  69638],
        [139361, 331509, 343164, 781380,  52269]]

columns = ('Freeze', 'Wind', 'Flood', 'Quake', 'Hail')
rows = ['%d year' % x for x in (100, 50, 20, 10, 5)]

values = np.arange(0, 2500, 500)
value_increment = 1000

# Get some pastel shades for the colors
colors = plt.cm.BuPu(np.linspace(0, 0.5, len(rows)))
n_rows = len(data)

index = np.arange(len(columns)) + 0.3
bar_width = 0.4

# Initialize the vertical-offset for the stacked bar chart.
y_offset = np.zeros(len(columns))

# Plot bars and create text labels for the table
cell_text = []
for row in range(n_rows):
    plt.bar(index, data[row], bar_width, bottom=y_offset, color=colors[row])
    y_offset = y_offset + data[row]
    cell_text.append(['%1.1f' % (x / 1000.0) for x in y_offset])
# Reverse colors and text labels to display the last value at the top.
colors = colors[::-1]
cell_text.reverse()

# Add a table at the bottom of the axes
the_table = plt.table(cellText=cell_text,
                      rowLabels=rows,
                      rowColours=colors,
                      colLabels=columns,
                      loc='bottom')

# Adjust layout to make room for the table:
plt.subplots_adjust(left=0.2, bottom=0.2)

plt.ylabel("Loss in ${0}'s".format(value_increment))
plt.yticks(values * value_increment, ['%d' % val for val in values])
plt.xticks([])
plt.title('Loss by Disaster')

plt.show()
```

## Steps in Table

whether to use 'zminmax' or not  
<img src="/images/2020-03/0321_Case_Table1b.png" width="100%">  
<img src="/images/2020-03/0321_Case_Table1c.png" width="100%">  

```python
# zminmax = (min(values)*value_increment, (max(values)+100)*value_increment)
zminmax = 2250 * value_increment
rows = ['%d Year' % x for x in (100, 50, 20, 10, 5)]
colors = plt.cm.BuPu(np.linspace(0.15, 0.65, len(rows)))

fig, axs = plt.subplots(ncols=5, figsize=(19, 5))
# fig, (ax0, ax1, ax2, ax3, ax4) = plt.subplots(ncols=5, figsize=(19, 4))
# fig, axs = plt.subplots()

def disaster_table(num, ax, 
                rows=rows, values=values, colors=colors,
                value_increment=value_increment, zminmax=zminmax):
    rows = rows[-num :]
    values = values[: num]
    colors = colors[: num]

    # Initialize the vertical-offset for the stacked bar chart.
    y_offset = np.zeros(len(columns))
    # Plot bars and create text labels for the table
    cell_text = []
    for row in range(num):
        ax.bar(index, data[row], bar_width, bottom=y_offset, color=colors[row])
        y_offset = y_offset + data[row]
        cell_text.append(['%1.1f' % (x / 1000.0) for x in y_offset])
    # Reverse colors and text labels to display the last value at the top.
    colors = colors[::-1]
    cell_text.reverse()

    # Add a table at the bottom of the axes
    the_table = ax.table(cellText=cell_text,
                        rowLabels=rows,
                        rowColours=colors,
                        colLabels=columns,
                        loc='bottom')
    # Adjust layout to make room for the table:
    # plt.subplots_adjust(left=0.2, bottom=0.2)

    ax.set_ylabel("Loss in ${0}'s".format(value_increment))
    # ax.set_yticks(values * value_increment, ['%d' % val for val in values])
    ax.set_yticks(values * value_increment)
    ax.set_yticklabels(['%d' % val for val in values])
    ax.set_xticks([])
    ax.set_title('Loss by Disaster')
    # ax.set_ylim((0, zminmax))

disaster_table(1, axs[0])
disaster_table(2, axs[1])
disaster_table(3, axs[2])
disaster_table(4, axs[3]) #ax3)
disaster_table(5, axs[4]) #ax4)#axs)

plt.tight_layout()
plt.subplots_adjust(bottom=0.2)
plt.show()
```

# Scatter plots

Using [scatter()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.scatter.html#matplotlib.pyplot.scatter)  
e.g., Scatter Demo2 [Scatter Demo2](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/scatter_demo2.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_scatter_demo2_001.png" width="70%">

```python
# Scatter
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.cbook as cbook

import matplotlib as mpl
# import os
mpl.rcParams['examples.directory'] = './Matplotlib'

# Load a numpy record array from yahoo csv data with fields date, open, close,
# volume, adj_close from the mpl-data/example directory. The record array
# stores the date as an np.datetime64 with a day unit ('D') in the date column.
with cbook.get_sample_data('goog.npz') as datafile:
    price_data = np.load(datafile)['price_data'].view(np.recarray)
price_data = price_data[-250:]  # get the most recent 250 trading days

delta1 = np.diff(price_data.adj_close) / price_data.adj_close[:-1]

# Marker size in units of points^2
volume = (15 * price_data.volume[:-2] / price_data.volume[0])**2
close = 0.003 * price_data.close[:-2] / 0.003 * price_data.open[:-2]

fig, ax = plt.subplots()
ax.scatter(delta1[:-1], delta1[1:], c=close, s=volume, alpha=0.5)
# c: color; s: marker size

ax.set_xlabel(r'$\Delta_i$', fontsize=15)
ax.set_ylabel(r'$\Delta_{i+1}$', fontsize=15)
ax.set_title('Volume and percent change')

ax.grid(True)
fig.tight_layout()

plt.show()
```

# GUI widgets

[Slider Demo](https://matplotlib.org/3.1.1/gallery/widgets/slider_demo.html)

形如下图，但是左侧和下侧均可以改变，左侧用于改变线条颜色，下侧用于改变波形，reset 可以恢复原始波形图。

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_slider_demo_001.png" width="70%">

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import Slider, Button, RadioButtons

fig, ax = plt.subplots()
plt.subplots_adjust(left=0.25, bottom=0.25)
t = np.arange(0.0, 1.0, 0.001)
a0 = 5
f0 = 3
delta_f = 5.0
s = a0 * np.sin(2 * np.pi * f0 * t)
l, = plt.plot(t, s, lw=2)
ax.margins(x=0)

axcolor = 'lightgoldenrodyellow'
axfreq = plt.axes([0.25, 0.1, 0.65, 0.03], facecolor=axcolor)
axamp = plt.axes([0.25, 0.15, 0.65, 0.03], facecolor=axcolor)

sfreq = Slider(axfreq, 'Freq', 0.1, 30.0, valinit=f0, valstep=delta_f)
samp = Slider(axamp, 'Amp', 0.1, 10.0, valinit=a0)

def update(val):
    amp = samp.val
    freq = sfreq.val
    l.set_ydata(amp * np.sin(2 * np.pi * freq * t))
    fig.canvas.draw_idle()

sfreq.on_changed(update)
samp.on_changed(update)

resetax = plt.axes([0.8, 0.025, 0.1, 0.04])
button = Button(resetax, 'Reset', color=axcolor, hovercolor='0.975')

def reset(event):
    sfreq.reset()
    samp.reset()
button.on_clicked(reset)

rax = plt.axes([0.025, 0.5, 0.15, 0.15], facecolor=axcolor)
radio = RadioButtons(rax, ('red', 'blue', 'green'), active=0)

def colorfunc(label):
    l.set_color(label)
    fig.canvas.draw_idle()
radio.on_clicked(colorfunc)

plt.show()
```


# Filled curves

Using [fill()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.fill.html#matplotlib.pyplot.fill)  
e.g., Fill [Filled polygon](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/fill.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_fill_001.png" width="100%">  
<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_fill_002.png" width="100%">  

```python
import numpy as np
import matplotlib.pyplot as plt

def koch_snowflake(order, scale=10):
    """
    Return two lists x, y of point coordinates of the Koch snowflake.

    Arguments
    ---------
    order : int
        The recursion depth.
    scale : float
        The extent of the snowflake (edge length of the base triangle).
    """
    def _koch_snowflake_complex(order):
        if order == 0:
            # initial triangle
            angles = np.array([0, 120, 240]) + 90
            return scale / np.sqrt(3) * np.exp(np.deg2rad(angles) * 1j)
        else:
            ZR = 0.5 - 0.5j * np.sqrt(3) / 3

            p1 = _koch_snowflake_complex(order - 1)  # start points
            p2 = np.roll(p1, shift=-1)  # end points
            dp = p2 - p1  # connection vectors

            new_points = np.empty(len(p1) * 4, dtype=np.complex128)
            new_points[::4] = p1
            new_points[1::4] = p1 + dp / 3
            new_points[2::4] = p1 + dp * ZR
            new_points[3::4] = p1 + dp / 3 * 2
            return new_points
    
    points = _koch_snowflake_complex(order)
    x, y = points.real, points.imag
    return x, y

# Basic usage:
x, y = koch_snowflake(order=5)

plt.figure(figsize=(8, 8))
plt.axis('equal')
plt.fill(x, y)
plt.show()

# Use keyword arguments facecolor and edgecolor to modify the the 
# colors of the polygon. Since the linewidth of the edge is 0 in 
# the default Matplotlib style, we have to set it as well for the 
# edge to become visible.
x, y = koch_snowflake(order=2)

fig, (ax1, ax2, ax3) = plt.subplots(1, 3, figsize=(9, 3),
                                    subplot_kw={'aspect': 'equal'})
ax1.fill(x, y)
ax2.fill(x, y, facecolor='lightsalmon', edgecolor='orangered', linewidth=3)
ax3.fill(x, y, facecolor='none', edgecolor='purple', linewidth=3)

plt.show()
```

<img src="/images/2020-03/0321_Case_Fill.png" width="100%">

```python
nrows, ncols = 2, 3
fig, axs = plt.subplots(nrows, ncols, figsize=(15, 9), # (9, 6),
                        subplot_kw={'aspect': 'equal'})
# for order in range(nrows * ncols):
#     ax = axs[order]
for i in range(nrows):
    for j in range(ncols):
        order = i * ncols + j
        xz, yz = koch_snowflake(order=order)
        ax = axs[i][j]
        ax.fill(xz, yz, facecolor='yellow', edgecolor='green', linewidth=3)
plt.tight_layout()
plt.show() 
```


# Date handling

e.g., Date [Date tick labels](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/date.html)  

**Error:** ValueError: Unrecognized character a in format string  
[Python: plt.plot(x,y) ValueError: Unrecognized character S in format string](https://stackoverflow.com/questions/52318672/python-plt-plotx-y-valueerror-unrecognized-character-s-in-format-string)  
[Python 2.7运行时格式字符串中无法识别的字符G.](https://stackoom.com/question/1WiQs/Python-%E8%BF%90%E8%A1%8C%E6%97%B6%E6%A0%BC%E5%BC%8F%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E6%97%A0%E6%B3%95%E8%AF%86%E5%88%AB%E7%9A%84%E5%AD%97%E7%AC%A6G)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_date_001.png" width="70%">

```python
# Date
import matplotlib as mpl
mpl.rcParams['examples.directory'] = './Matplotlib'

import numpy as np
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
import matplotlib.cbook as cbook

years = mdates.YearLocator()  # every year
months = mdates.MonthLocator()  # every month
years_fmt = mdates.DateFormatter('%Y')

# Load a numpy structured array from yahoo csv data with fields date, open,
# close, volume, adj_close from the mpl-data/example directory.  This array
# stores the date as an np.datetime64 with a day unit ('D') in the 'date'
# column.
with cbook.get_sample_data('goog.npz') as datafile:
    # data = np.load(datafile)['price_data']
    data = np.load(datafile)['price_data'].view(np.recarray)

fig, ax = plt.subplots()
# ax.plot('date', 'adj_close', data=data)
ax.plot(data.date, data.adj_close)

# format the ticks
ax.xaxis.set_major_locator(years)
ax.xaxis.set_major_formatter(years_fmt)
ax.xaxis.set_minor_locator(months)

# round to nearest years.
datemin = np.datetime64(data['date'][0], 'Y')
datemax = np.datetime64(data['date'][-1], 'Y') + np.timedelta64(1, 'Y')
ax.set_xlim(datemin, datemax)

# format the coords message box
ax.format_xdata = mdates.DateFormatter('%Y-%m-%d')
ax.format_ydata = lambda x: '$%1.2f' % x  # format the price.
ax.grid(True)

# rotates and right aligns the x labels, and moves the bottom of the
# axes up to make room for them
fig.autofmt_xdate()

plt.show()
```

# Log plots

e.g., Log Demo [Log Demo](https://matplotlib.org/3.1.1/gallery/scales/log_demo.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_log_demo_001.png" width="70%">

```python
import numpy as np
import matplotlib.pyplot as plt

# Data for plotting
t = np.arange(0.01, 20.0, 0.01)

# Create figure
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2)

# log y axis
ax1.semilogy(t, np.exp(-t / 5.0))
ax1.set(title='semilogy')
ax1.grid()

# log x axis
ax2.semilogx(t, np.sin(2 * np.pi * t))
ax2.set(title='semilogx')
ax2.grid()

# log x and y axis
ax3.loglog(t, 20 * np.exp(-t / 10.0), basex=2)
ax3.set(title='loglog base 2 on x')
ax3.grid()

# With errorbars: clip non-positive values
# Use new data for plotting
x = 10.0 ** np.linspace(0.0, 2.0, 20)
y = x ** 2.0

ax4.set_xscale("log", nonposx='clip')
ax4.set_yscale("log", nonposy='clip')
ax4.set(title='Errorbars go negative')
ax4.errorbar(x, y, xerr=0.1 * x, yerr=5.0 + 0.75 * y)
# ylim must be set after errorbar to allow errorbar to autoscale limits
ax4.set_ylim(bottom=0.1)

fig.tight_layout()
plt.show()
```

## 一个函数对应一行，横着看

<img src="/images/2020-03/0321_Case_LogDemo2a.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt
# Data for plotting
t = np.arange(0.01, 20.0, 0.01)
# Create figure
fig, axs = plt.subplots(4, 4, figsize=(12, 9.5))

def autopacking(t, ft, axs, idx, text):
    # idx: {0, 1, 2, 3}

    ax1 = axs[idx][0]
    # log y axis
    ax1.semilogy(t, ft)
    ax1.set(title='semilogy', ylabel=text)
    ax1.grid()

    ax2 = axs[idx][1]
    # log x axis
    ax2.semilogx(t, ft)
    ax2.set(title='semilogx')
    ax2.grid()

    ax3 = axs[idx][2]
    # log x and y axis
    ax3.loglog(t, ft, basex=2)
    ax3.set(title='loglog base 2 on x')
    ax3.grid()

    ax4 = axs[idx][3]
    # With errorbars: clip non-positive values
    # Use new data for plotting
    ax4.set_xscale("log", nonposx='clip')
    ax4.set_yscale("log", nonposy='clip')
    ax4.set(title='Errorbars go negative')
    ax4.errorbar(t, ft, xerr=0.1 * t, yerr=5.0 + 0.75 * ft)
    # ylim must be set after errorbar to allow errorbar to autoscale limits
    # ax4.set_ylim(bottom=0.1)

autopacking(t, np.exp(-t / 5.0), axs, 0, r'$\exp(-t/5)$')
autopacking(t, np.sin(2 * np.pi * t), axs, 1, r'$\sin(2\pi t)$')
autopacking(t, 20 * np.exp(-t / 10.0), axs, 2, r'$\exp(-t/10)$')
autopacking(t * 10, (t * 10) ** 2.0, axs, 3, r'$t^2$')
# t = 10.0 * np.arange(0.0, 20.1, 0.1)
# autopacking(t, t ** 2, axs, 3, r'$t^2$')

fig.tight_layout()
plt.show()
```

## 一个函数对应一列，竖着看

<img src="/images/2020-03/0321_Case_LogDemo2b.png" width="100%">

```python
import numpy as np
import matplotlib.pyplot as plt
# Data for plotting
t = np.arange(0.01, 20.0, 0.01)
# Create figure
fig, axs = plt.subplots(4, 4, figsize=(12, 9.5))

def autopacking(t, ft, axs, idx, text):
    # idx: {0, 1, 2, 3}

    ax1 = axs[0][idx]
    # log y axis
    ax1.semilogy(t, ft)
    # ax1.set(title='semilogy', ylabel=text)
    ax1.set_title(text + '\nsemilogy') # ax1.set(title=r'{}\nsemilogy'.format(text))
    ax1.grid()

    ax2 = axs[1][idx]
    # log x axis
    ax2.semilogx(t, ft)
    ax2.set(title='semilogx')
    ax2.grid()

    ax3 = axs[2][idx]
    # log x and y axis
    ax3.loglog(t, ft, basex=2)
    ax3.set(title='loglog base 2 on x')
    ax3.grid()

    ax4 = axs[3][idx]
    # With errorbars: clip non-positive values
    # Use new data for plotting
    ax4.set_xscale("log", nonposx='clip')
    ax4.set_yscale("log", nonposy='clip')
    ax4.set(title='Errorbars go negative')
    ax4.errorbar(t, ft, xerr=0.1 * t, yerr=5.0 + 0.75 * ft)
    # ylim must be set after errorbar to allow errorbar to autoscale limits
    # ax4.set_ylim(bottom=0.1)

autopacking(t, np.exp(-t / 5.0), axs, 0, r'$\exp(-t/5)$')
autopacking(t, np.sin(2 * np.pi * t), axs, 1, r'$\sin(2\pi t)$')
autopacking(t, 20 * np.exp(-t / 10.0), axs, 2, r'$\exp(-t/10)$')
autopacking(t * 10, (t * 10) ** 2.0, axs, 3, r'$t^2$')
# t = 10.0 * np.arange(0.0, 20.1, 0.1)
# autopacking(t, t ** 2, axs, 3, r'$t^2$')

fig.tight_layout()
plt.show()
```


# Polar plots

Using [polar()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.polar.html#matplotlib.pyplot.polar)  
e.g., Polar Demo [Polar Demo](https://matplotlib.org/3.1.1/gallery/pie_and_polar_charts/polar_demo.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_polar_demo_001.png" width="70%">

```python
# Polar
import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r

ax = plt.subplot(111, projection='polar')
ax.plot(theta, r)
ax.set_rmax(2)
ax.set_rticks([0.5, 1, 1.5, 2])  # Less radial ticks
ax.set_rlabel_position(-22.5)  # Move radial labels away from plotted line
ax.grid(True)

ax.set_title("A line plot on a polar axis", va='bottom')
plt.show()
```

## 对比 ax2, ax3 不设置 rmax 等时

<img src="/images/2020-03/0321_Case_Polar2a.png" width="100%">  
<img src="/images/2020-03/0321_Case_Polar2c.png" width="100%">  

```python
r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
sin = np.sin(theta)
cos = np.cos(theta)
# sin_exp_minus = np.exp(-r) * sin
# cos_exp_minus = np.exp(-r) * cos
# sin_exp = np.exp(r) * sin
# cos_exp = np.exp(r) * cos

# fig, axs = plt.subplots(2, 3, figsize=(12, 5))#, projection='polar')
fig = plt.figure(figsize=(12, 7)) #(12, 5))

def autopacking(r, theta, ft, fig, idx, text):
    # sin, cos

    ax1 = fig.add_subplot(2, 3, idx+1, projection='polar') # ax1 = axs[idx][0]
    # sin / cos
    ax1.plot(theta, ft)
    ax1.set_rmax(2)
    ax1.set_rticks([0.5, 1, 1.5, 2])  # Less radial ticks
    ax1.set_rlabel_position(-22.5)  # Move radial labels away from plotted line
    ax1.grid(True)
    # ax1.set_title("A line plot on a polar axis\n" + text, va='bottom')
    ax1.set_ylabel(text)
    ax1.set_title("trigonometry", va='bottom')

    ax2 = fig.add_subplot(2, 3, idx+2, projection='polar') # ax2 = axs[idx][1]
    # r$\exp(-t)\sin(2\pi t)$
    ax2.plot(theta, np.exp(-r) * ft)
    ax2.set_title(r'$\exp(-t)$' + text)

    ax2.set_rmax(0.8) 
    ax2.set_rticks([0.2, 0.4, 0.6, 0.8]) # [0.25, 0.5, 0.75, 1]
    ax2.set_rlabel_position(-44.5)
    ax2.grid(True)

    ax3 = fig.add_subplot(2, 3, idx+3, projection='polar') # ax3 = axs[idx][2]
    # r$\exp(t)\sin(2\pi t)$
    ax3.plot(theta, np.exp(r) * ft)
    ax3.set_title(r'$\exp(t)$' + text)

    ax3.set_rmax(4)
    ax3.set_rticks([1, 2, 3, 4]) # [0.5, 1, 1.5, 2]
    ax3.set_rlabel_position(-44.5)
    ax3.grid(True)

autopacking(r, theta, sin, fig, 0, r'\sin(2\pi t)')
autopacking(r, theta, sin, fig, 3, r'\cos(2\pi t)')
plt.tight_layout()
plt.show()
```


# Legends

Using [legend()](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)  
e.g., Legend [Legend using pre-defined labels](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/legend.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_legend_001.png" width="70%">

```python
import numpy as np
import matplotlib.pyplot as plt

# Make some fake data.
a = b = np.arange(0, 3, .02)
c = np.exp(a)
d = c[::-1]

# Create plots with pre-defined labels.
fig, ax = plt.subplots()
ax.plot(a, c, 'k--', label='Model length')
ax.plot(a, d, 'k:', label='Data length')
ax.plot(a, c + d, 'k', label='Total message length')

legend = ax.legend(loc='upper center', shadow=True, fontsize='x-large')

# Put a nicer background color on the legend
legend.get_frame().set_facecolor('C0')

plt.show()
```

## 'CN' 颜色对比

<img src="/images/2020-03/0321_Case_Legend.png" width="100%">

```python
fig = plt.figure(figsize=(18, 6)) # (16, 6)) # (12, 5))
fontsize = ['xx-small', 'x-small', 'small', 'medium', 'large', 'x-large', 'xx-large']

def autopacking(a, c, d, idx, color, fontsize=fontsize):
    ax = fig.add_subplot(2, 5, idx)
    ax.plot(a, c, 'k--', label='Model length')
    ax.plot(a, d, 'k:', label='Data length')
    ax.plot(a, c + d, 'b', label='Total message length')
    # {'xx-small', 'x-small', 'small', 'medium', 'large', 'x-large', 'xx-large'}
    # fontsize = 'x-small' if idx <= 5 else 'x-large'
    legend = ax.legend(loc='upper center', fontsize=fontsize[(idx - 1) % 7])
    legend.get_frame().set_facecolor(color)

for i in range(10):
    autopacking(a, c, d, i + 1, 'C'+str(i))

plt.tight_layout()
plt.show()
```


# TeX-notation for text objects

e.g., Mathtext Examples [Mathtext Examples](https://matplotlib.org/3.1.1/gallery/text_labels_and_annotations/mathtext_examples.html)  

<img src="https://matplotlib.org/3.1.1/_images/sphx_glr_mathtext_examples_001.png" width="50%">
<img src="/images/2020-03/0321_Case_Tex1.png" width="50%">

```python
# Tex Mathematical
import matplotlib.pyplot as plt
import subprocess
import sys
import os

# Selection of features following "Writing mathematical expressions" tutorial
mathtext_titles = {
    0: "Header demo",
    1: "Subscripts and superscripts",
    2: "Fractions, binomials and stacked numbers",
    3: "Radicals",
    4: "Fonts",
    5: "Accents",
    6: "Greek, Hebrew",
    7: "Delimiters, functions and Symbols"
}
n_lines = len(mathtext_titles)

# Randomly picked examples
mathext_demos = {
    0: r"$W^{3\beta}_{\delta_1 \rho_1 \sigma_2} = "
    r"U^{3\beta}_{\delta_1 \rho_1} + \frac{1}{8 \pi 2} "
    r"\int^{\alpha_2}_{\alpha_2} d \alpha^\prime_2 \left[\frac{ "
    r"U^{2\beta}_{\delta_1 \rho_1} - \alpha^\prime_2U^{1\beta}_"
    r"{\rho_1 \sigma_2} }{U^{0\beta}_{\rho_1 \sigma_2}}\right]$",

    1: r"$\alpha_i > \beta_i,\ "
    r"\alpha_{i+1}^j = {\rm sin}(2\pi f_j t_i) e^{-5 t_i/\tau},\ "
    r"\ldots$",

    2: r"$\frac{3}{4},\ \binom{3}{4},\ \genfrac{}{}{0}{}{3}{4},\ "
    r"\left(\frac{5 - \frac{1}{x}}{4}\right),\ \ldots$",

    3: r"$\sqrt{2},\ \sqrt[3]{x},\ \ldots$",

    4: r"$\mathrm{Roman}\ , \ \mathit{Italic}\ , \ \mathtt{Typewriter} \ "
    r"\mathrm{or}\ \mathcal{CALLIGRAPHY}$",

    5: r"$\acute a,\ \bar a,\ \breve a,\ \dot a,\ \ddot a, \ \grave a, \ "
    r"\hat a,\ \tilde a,\ \vec a,\ \widehat{xyz},\ \widetilde{xyz},\ "
    r"\ldots$",

    6: r"$\alpha,\ \beta,\ \chi,\ \delta,\ \lambda,\ \mu,\ "
    r"\Delta,\ \Gamma,\ \Omega,\ \Phi,\ \Pi,\ \Upsilon,\ \nabla,\ "
    r"\aleph,\ \beth,\ \daleth,\ \gimel,\ \ldots$",

    7: r"$\coprod,\ \int,\ \oint,\ \prod,\ \sum,\ "
    r"\log,\ \sin,\ \approx,\ \oplus,\ \star,\ \varpropto,\ "
    r"\infty,\ \partial,\ \Re,\ \leftrightsquigarrow, \ \ldots$"
}

def doall():
    # Colors used in mpl online ducumentation.
    mpl_blue_rvb = (191. / 255., 209. / 256., 212. / 255.)
    mpl_orange_rvb = (202. / 255., 121. / 256., 0. / 255.)
    mpl_grey_rvb = (51. / 255., 51. / 255., 51. / 255.)

    # Creating figure and axis.
    plt.figure(figsize=(6, 9)) # (6, 7))
    plt.axes([0.01, 0.01, 0.98, 0.98], facecolor="white", frameon=True)
    plt.gca().set_xlim(0., 1.)
    plt.gca().set_ylim(0.1, 0.98) # 0., 1.)
    # plt.gca().set_title("Matplotlib's math rendering engine",
    #                     color=mpl_grey_rvb, fontsize=14, weight='bold')
    plt.suptitle("Matplotlib's math rendering engine")
    plt.gca().set_xticklabels("", visible=False)
    plt.gca().set_yticklabels("", visible=False)

    # Gap between lines in axes coords
    line_axesfrac = (1. / (n_lines))

    # Plotting header demonstration formula
    full_demo = mathext_demos[0]
    plt.annotate(full_demo,
                xy=(0.5, 1. - 0.59 * line_axesfrac),
                color=mpl_orange_rvb, ha='center', fontsize=20)
    
    # Plotting features demonstration formulae
    for i_line in range(1, n_lines):
        baseline = 1 - (i_line) * line_axesfrac
        baseline_next = baseline - line_axesfrac
        title = mathtext_titles[i_line] + ":"
        fill_color = ['white', mpl_blue_rvb][i_line % 2]
        plt.fill_between([0., 1.], [baseline, baseline],
                        [baseline_next, baseline_next],
                        color=fill_color, alpha=0.5)
        plt.annotate(title,
                    xy=(0.07, baseline - 0.3 * line_axesfrac),
                    color=mpl_grey_rvb, weight='bold')
        demo = mathext_demos[i_line]
        plt.annotate(demo,
                    xy=(0.05, baseline - 0.75 * line_axesfrac),
                    color=mpl_grey_rvb, fontsize=16)
    
    for i in range(n_lines):
        s = mathext_demos[i]
        print(i, s)
    # plt.tight_layout()
    # plt.subplots_adjust(bottom=0.1) # top=0.01)
    plt.show()

if '--latex' in sys.argv:
    # Run: python mathtext_examples.py --latex
    # Need amsmath and amssymb packages.
    fd = open("mathtext_examples.ltx", "w")
    fd.write("\\documentclass{article\n")
    fd.write("\\usepackage{amsmath, amssymb}\n")
    fd.write("\\begin{document}\n")
    fd.write("\\begin{enumerate}\n")

    for i in range(n_lines):
        s = mathext_demos[i]
        s = re.sub(r"(?<!\\)\$", "$$", s)
        fd.write("\\item %s\n" % s)
    
    fd.write("\\end{enumerate}\n")
    fd.write("\\end{document}\n")
    fd.close()

    subprocess.call(["pdflatex", "mathtext_examples.ltx"])
else:
    doall()
```


# Native TeX rendering


# EEG GUI


# XKCD-style sketch plots


# Subplot example

