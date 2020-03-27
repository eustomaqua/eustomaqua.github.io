---
title: Seaborn Tutorial Examples
date: 2020-03-25 23:29:29
updated: 2020-03-26 23:45:12
categories:
  - Drafting
tags:
  - Notes
  - Seaborn
---

<!--
updated: 2020-03-27 1:14:06  (true, 1:13?)
-->
[Seaborn: Statistical data visualization](http://seaborn.pydata.org/index.html)  
[mwaskom / seaborn-data](https://github.com/mwaskom/seaborn-data)  


# Seaborn official
Seaborn is a Python data visualization library based on [matplotlib](https://matplotlib.org/). It provides a high-level interface for drawing attractive and informative statistical graphics.

## Homepage

### Scatterplot Matrix
[Scatterplot Matrix](http://seaborn.pydata.org/examples/scatterplot_matrix.html)
<img src="http://seaborn.pydata.org/_images/scatterplot_matrix.png" width="100%">

```python
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style="ticks")

df = sns.load_dataset("iris")
sns.pairplot(df, hue="species")
plt.show()  # saveas 'homepage1plt.png'

# sns_fig = sns.pairplot()
# sns_fig.savefig('homepage1.png')
```

上面那张图是 `seaborn.version == 0.10.0` 的效果，下面两张图是 `sns.__version__ = 0.8.1` 的效果 
<!--
<img src="/images/2020-03/0326_seaborn_homepage1.png" width="100%"><img src="/images/2020-03/0326_seaborn_homepage1sns.png" width="100%">
-->
{% gp 1-2 %}
<img src="/images/2020-03/0326_seaborn_homepage1.png">
<img src="/images/2020-03/0326_seaborn_homepage1sns.png">
{% endgp %}

### Timeseries plot with error bands
[Timeseries plot with error bands](http://seaborn.pydata.org/examples/errorband_lineplots.html)
<img src="http://seaborn.pydata.org/_images/errorband_lineplots.png" width="60%">

```python
import seaborn as sns
sns.set(style="darkgrid")

# Load an example dataset with long-form data
fmri = sns.load_dataset("fmri")

# Plot the responses for different events and regions
sns.lineplot(x="timepoint", y="signal",
                hue="region", style="event",
                data=fmri)
plt.show()
```

下面这两种写法都不能保存图片
```python
fig = sns.lineplot()
fig.savefig('homepage2.png')

sns.lineplot()
sns.plt.savefig('homepage2.png')
```

### Scatterplot with categorical and numerical semantics
[Scatterplot with categorical and numerical semantics](http://seaborn.pydata.org/examples/different_scatter_variables.html)
<img src="http://seaborn.pydata.org/_images/different_scatter_variables.png" width="60%">

```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="whitegrid")

# Load the example diamonds dataset
diamonds = sns.load_dataset("diamonds")

# Draw a scatter plot while assigning point colors and sizes to different
# variables in the dataset
f, ax = plt.subplots(figsize=(6.5, 6.5))
sns.despine(f, left=True, bottom=True)
clarity_ranking = ["I1", "SI2", "SI1", "VS2", "VS1", "VVS2", "VVS1", "IF"]
sns.scatterplot(x="carat", y="price",
                hue="clarity", size="depth",
                palette="ch:r=-.2,d=.3_r",
                hue_order=clarity_ranking,
                sizes=(1, 8), linewidth=0,
                data=diamonds, ax=ax)
plt.show()
```

### Horizontal boxplot with observations
[Horizontal boxplot with observations](http://seaborn.pydata.org/examples/horizontal_boxplot.html)
<img src="http://seaborn.pydata.org/_images/horizontal_boxplot.png" width="70%" >

```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="ticks")

# Initialize the figure with a logarithmic x axis
f, ax = plt.subplots(figsize=(9, 6))  # figsize=(7, 6))
ax.set_xscale("log")

# Load the example planets dataset
planets = sns.load_dataset("planets")

# Plot the orbital period with horizontal boxes
sns.boxplot(x="distance", y="method", data=planets,
            whis="range", palette="vlag")

# Add in points to show each observation
sns.swarmplot(x="distance", y="method", data=planets,
            size=2, color=".3", linewidth=0)

# Tweak the visual presentation
ax.xaxis.grid(True)
# ax.set(ylabel="")
sns.despine(trim=True, left=True)

plt.tight_layout()
plt.show()
```
<img src="/images/2020-03/0326_seaborn_homepage4.png" width="80%">

### Linear regression with marginal distributions
[Linear regression with marginal distributions](http://seaborn.pydata.org/examples/regression_marginals.html)
<img src="http://seaborn.pydata.org/_images/regression_marginals.png" width="60%">

```python
import seaborn as sns
sns.set(style="darkgrid")

import pandas as pd
df = pd.read_csv('./Seaborn/tips.csv')
if df.iloc[-1].isnull().all():
        df = df.iloc[:-1]
# Set some columns as a categorical type with ordered levels
# if name == "tips":
df["day"] = pd.Categorical(df["day"], ["Thur", "Fri", "Sat", "Sun"])
df["sex"] = pd.Categorical(df["sex"], ["Male", "Female"])
df["time"] = pd.Categorical(df["time"], ["Lunch", "Dinner"])
df["smoker"] = pd.Categorical(df["smoker"], ["Yes", "No"])
tips = df

# tips = sns.load_dataset("tips")
g = sns.jointplot("total_bill", "tip", data=tips,
                kind="reg", truncate=False,
                xlim=(0, 60), ylim=(0, 12),
                color="m", height=7)

plt.show()
```

### Plotting on a large number of facets
[Plotting on a large number of facets](http://seaborn.pydata.org/examples/many_facets.html)
<img src="http://seaborn.pydata.org/_images/many_facets.png" width="80%">

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
sns.set_style("ticks")

# Create a dataset with many short random walks
rs = np.random.RandomState(4)
pos = rs.randint(-1, 2, (20, 5)).cumsum(axis=1)
pos -= pos[:, 0, np.newaxis]
step = np.tile(range(5), 20)
walk = np.repeat(range(20), 5)
df = pd.DataFrame(np.c_[pos.flat, step, walk],
                columns=["position", "step", "walk"])

# Initalize a grid of plots with an Axes for each walk
grid = sns.FacetGrid(df, col="walk", hue="walk", palette="tab20c",
                    col_wrap=4, height=1.5)

# Draw a horizontal line to show the starting point
grid.map(plt.axhline, y=0, ls=":", c=".5")

# Draw a line plot to show the trajectory of each random walk
grid.map(plt.plot, "step", "position", marker="o")

# Adjust the tick positions and labels
grid.set(xticks=np.arange(5), yticks=[-3, 3],
        xlim=(-.5, 4.5), ylim=(-3.5, 3.5))

# Adjust the arrangement of the plots
grid.fig.tight_layout(w_pad=1)

plt.show()
```

分解第 16--28 行:  
1. after `grid = sns.FaceGrid`
2. after `grid.map(plt.axhline)`
3. after `grid.map(plt.plot)`
4. after `grid.set()`

{% gp 4-3 %}
<img src="/images/2020-03/0326_seaborn_homepage6a.png">
<img src="/images/2020-03/0326_seaborn_homepage6b.png">
<img src="/images/2020-03/0326_seaborn_homepage6c.png">
<img src="/images/2020-03/0326_seaborn_homepage6d.png">
{% endgp %}

### Installation
尝试了上面前两种之后，把 seaborn 版本升级到当前最新
```bash
λ python
Python 3.6.5 |Anaconda, Inc.| (default, Mar 29 2018, 13:32:41) [MSC v.1900 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import seaborn as sns
>>> sns.__version__
'0.8.1'
>>> ^Z
>>> 

λ pip install seaborn -U
Collecting seaborn
  Downloading https://files.pythonhosted.org/packages/70/bd/5e6bf595fe6ee0f257ae49336dd180768c1ed3d7c7155b2fdf894c1c808a/seaborn-0.10.0-py3-none-any.whl (215kB)
    66% |█████████████████████▎          | 143kB 8.7kB/s eta 0:00:0
    71% |██████████████████████▊         | 153kB 10.0kB/s eta 0:00
    75% |████████████████████████▎       | 163kB 8.3kB/s eta 0:0
    80% |█████████████████████████▉      | 174kB 8.9kB/s eta 0:
    85% |███████████████████████████▎    | 184kB 8.5kB/s eta
    90% |████████████████████████████▉   | 194kB 8.4kB/s eta
    94% |██████████████████████████████▍ | 204kB 8.1kB/s e
    99% |███████████████████████████████▉| 215kB 9.0kB/s
    100% |████████████████████████████████| 225kB 10kB/s

Requirement not upgraded as not directly required: numpy>=1.13.3 in c:\users\lenovo\anaconda3\lib\site-packages (from seaborn) (1.17.2)
Requirement not upgraded as not directly required: scipy>=1.0.1 in c:\users\lenovo\anaconda3\lib\site-packages (from seaborn) (1.4.1)
Requirement not upgraded as not directly required: pandas>=0.22.0 in c:\users\lenovo\anaconda3\lib\site-packages (from seaborn) (0.23.0)
Requirement not upgraded as not directly required: matplotlib>=2.1.2 in c:\users\lenovo\anaconda3\lib\site-packages (from seaborn) (2.2.2)
Requirement not upgraded as not directly required: pytz>=2011k in c:\users\lenovo\anaconda3\lib\site-packages (from pandas>=0.22.0->seaborn) (2018.4)
Requirement not upgraded as not directly required: python-dateutil>=2.5.0 in c:\users\lenovo\anaconda3\lib\site-packages (from pandas>=0.22.0->seaborn) (2.7.3)
Requirement not upgraded as not directly required: cycler>=0.10 in c:\users\lenovo\anaconda3\lib\site-packages (from matplotlib>=2.1.2->seaborn) (0.10.0)
Requirement not upgraded as not directly required: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in c:\users\lenovo\anaconda3\lib\site-packages (from matplotlib>=2.1.2->seaborn) (2.2.0)
Requirement not upgraded as not directly required: six>=1.10 in c:\users\lenovo\anaconda3\lib\site-packages (from matplotlib>=2.1.2->seaborn) (1.14.0)
Requirement not upgraded as not directly required: kiwisolver>=1.0.1 in c:\users\lenovo\anaconda3\lib\site-packages (from matplotlib>=2.1.2->seaborn) (1.0.1)
Requirement not upgraded as not directly required: setuptools in c:\users\lenovo\anaconda3\lib\site-packages (from kiwisolver>=1.0.1->matplotlib>=2.1.2->seaborn) (45.0.0)
Installing collected packages: seaborn
  Found existing installation: seaborn 0.8.1
    Uninstalling seaborn-0.8.1:
      Successfully uninstalled seaborn-0.8.1
Successfully installed seaborn-0.10.0
You are using pip version 10.0.1, however version 20.0.2 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```

## Example gallery
ref: [Example gallery](http://seaborn.pydata.org/examples/index.html)

# \#\# Tutorial
ref: [Official seaborn tutorial](http://seaborn.pydata.org/tutorial.html)

## Plotting functions

### [<font color=#8470FF>Visualizing statistical relationships</font>](http://seaborn.pydata.org/tutorial/relational.html)
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style("darkgrid")
```
#### [<font color=#87CEFA>Relating variables with scatter plots</font>](http://seaborn.pydata.org/tutorial/relational.html#relating-variables-with-scatter-plots)
```python
def load_dataset_tips(fpath='./Seaborn/'):
    df = pd.read_csv(fpath + 'tips.csv')
    if df.iloc[-1].isnull().all():
        df = df.iloc[:-1]
    # Set some columns as a categorical type with ordered levels
    # if name == "tips":
    df["day"] = pd.Categorical(df["day"], ["Thur", "Fri", "Sat", "Sun"])
    df["sex"] = pd.Categorical(df["sex"], ["Male", "Female"])
    df["time"] = pd.Categorical(df["time"], ["Lunch", "Dinner"])
    df["smoker"] = pd.Categorical(df["smoker"], ["Yes", "No"])
    return df

tips = load_dataset_tips()
# tips = sns.load_dataset("tips")

sns.relplot(x="total_bill", y="tip", data=tips)
sns.relplot(x="total_bill", y="tip", hue="smoker", data=tips)
sns.relplot(x="total_bill", y="tip", hue="smoker", style="smoker", data=tips)
sns.relplot(x="total_bill", y="tip", hue="smoker", style="time", data=tips)
sns.relplot(x="total_bill", y="tip", hue="size", data=tips)
sns.relplot(x="total_bill", y="tip", hue="size", palette="ch:r=-.5,l=.75", data=tips)
sns.relplot(x="total_bill", y="tip", size="size", data=tips)
sns.relplot(x="total_bill", y="tip", size="size", sizes=(15, 200), data=tips)

plt.show()
```

`sns.relplot(x, y="tip")` with `hue="smoker`
{% gp 1-2%}
<img src="http://seaborn.pydata.org/_images/relational_4_0.png">
<img src="http://seaborn.pydata.org/_images/relational_6_0.png">
{% endgp %}
`sns.relplot(x, y, hue="smoker", style={"smoker" | "time"})`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/relational_8_0.png">
<img src="http://seaborn.pydata.org/_images/relational_10_0.png">
{% endgp %}
with `hue="size"`, different `palette`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/relational_12_0.png">
<img src="http://seaborn.pydata.org/_images/relational_14_0.png">
{% endgp %}
using `size="size"`, different `sizes=?`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/relational_16_0.png">
<img src="http://seaborn.pydata.org/_images/relational_18_0.png">
{% endgp %}

<!--
`sns.relplot(x, y="tip")` with `hue="smoker`
{% gp 1-2%}
<img src="/images/2020-03/0326_sns_plot_visual_1a.png">
<img src="/images/2020-03/0326_sns_plot_visual_1b.png">
{% endgp %}
`sns.relplot(x, y, hue="smoker", style={"smoker" | "time"})`
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual_1c.png">
<img src="/images/2020-03/0326_sns_plot_visual_1d.png">
{% endgp %}
with `hue="size"`, different `palette`
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual_1e.png">
<img src="/images/2020-03/0326_sns_plot_visual_1f.png">
{% endgp %}
using `size="size"`, different `sizes=?`
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual_1g.png">
<img src="/images/2020-03/0326_sns_plot_visual_1h.png">
{% endgp %}
-->

#### [<font color=#87CEFA>Emphasizing continuity with line plots</font>](http://seaborn.pydata.org/tutorial/relational.html#emphasizing-continuity-with-line-plots)

```python
df = pd.DataFrame(dict(time=np.arange(500),
                    value=np.random.randn(500).cumsum()))
g = sns.relplot(x="time", y="value", kind="line", data=df)
g.fig.autofmt_xdate()
# f = sns.relplot(x="time", y="value", kind="line", data=df)
```
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual2_a1.png">
<img src="/images/2020-03/0326_sns_plot_visual2_a2.png">
{% endgp %}

```python
df = pd.DataFrame(np.random.randn(500, 2).cumsum(axis=0),
                columns=["x", "y"])
sns.relplot(x="x", y="y", sort=False, kind="line", data=df)
sns.relplot(x="x", y="y", sort=True, kind="line", data=df)
```
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual2_b1.png">
<img src="/images/2020-03/0326_sns_plot_visual2_b2.png">
{% endgp %}

##### Aggregation and representing uncertainty

```python
fmri = sns.load_dataset("fmri")
sns.relplot(x="timepoint", y="signal", kind="line", data=fmri)
sns.relplot(x="timepoint", y="signal", ci=None, kind="line", data=fmri)
sns.relplot(x="timepoint", y="signal", kind="line", ci="sd", data=fmri)
sns.relplot(x="timepoint", y="signal", estimator=None, kind="line", data=fmri)
plt.show()
```

{% gp 4-3 %}
<img src="http://seaborn.pydata.org/_images/relational_25_0.png">
<img src="http://seaborn.pydata.org/_images/relational_27_0.png">
<img src="http://seaborn.pydata.org/_images/relational_29_0.png">
<img src="http://seaborn.pydata.org/_images/relational_31_0.png">
{% endgp %}

<!--
{% gp 4-3 %}
<img src="/images/2020-03/0326_sns_plot_visual2_ca.png">
<img src="/images/2020-03/0326_sns_plot_visual2_cb.png">
<img src="/images/2020-03/0326_sns_plot_visual2_cc.png">
<img src="/images/2020-03/0326_sns_plot_visual2_cd.png">
{% endgp %}
-->

##### Plotting subsets of data with semantic mappings

```python
fmri = sns.load_dataset("fmri")

sns.relplot(x="timepoint", y="signal", hue="event", kind="line", data=fmri)
sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            kind="line", data=fmri)
sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            dashes=False, markers=True, kind="line", data=fmri)

# First one: dashes=False, markers=True
f = sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            dashes=True, markers=True, kind="line", data=fmri)
g = sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            dashes=False, markers=False, kind="line", data=fmri)

sns.relplot(x="timepoint", y="signal", hue="event", style="event",
            kind="line", data=fmri)
f2 = sns.relplot(x="timepoint", y="signal", hue="event", style="region",
            kind="line", data=fmri)
f3 = sns.relplot(x="timepoint", y="signal", hue="region", style="event",
            kind="line", data=fmri)
f4 = sns.relplot(x="timepoint", y="signal", hue="region", style="region",
            kind="line", data=fmri)

sns.relplot(x="timepoint", y="signal", hue="region",
            units="subject", estimator=None,
            kind="line", data=fmri.query("event == 'stim'"))
f = sns.relplot(x="timepoint", y="signal", hue="region",
            units="subject", estimator=None,
            kind="line", data=fmri.query("event != 'stim'"))

plt.show()
```

`hue="event"` | `hue="region", style="event` with different dashes/markers
{% gp 1-3 %} 
<img src="http://seaborn.pydata.org/_images/relational_33_0.png">
<img src="http://seaborn.pydata.org/_images/relational_35_0.png">
<img src="http://seaborn.pydata.org/_images/relational_37_0.png">
{% endgp %}

`hue="region", style="event"` with different dashes/markers  
(in source codes, default: `dashes=True, markers=False`)
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/relational_37_0.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dc2.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dc3.png">
{% endgp %}

`hue="event | region", style="region | region"`
{% gp 4-3 %}
<img src="http://seaborn.pydata.org/_images/relational_39_0.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd2.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd3.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd4.png">
{% endgp %}

`data=fmri.query("event == 'stim'")` or not
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/relational_41_0.png">
<img src="/images/2020-03/0326_sns_plot_visual2_de2.png">
{% endgp %}

<!--
`hue="event"` | `hue="region", style="event` with different dashes/markers
{% gp 1-3 %}
<img src="/images/2020-03/0326_sns_plot_visual2_da.png">
<img src="/images/2020-03/0326_sns_plot_visual2_db.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dc.png">
{% endgp %}

`hue="region", style="event"` with different dashes/markers  
(in source codes, default: `dashes=True, markers=False`)
{% gp 1-3 %}
<img src="/images/2020-03/0326_sns_plot_visual2_dc.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dc2.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dc3.png">
{% endgp %}

`hue="event | region", style="region | region"`
{% gp 4-3 %}
<img src="/images/2020-03/0326_sns_plot_visual2_dd.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd2.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd3.png">
<img src="/images/2020-03/0326_sns_plot_visual2_dd4.png">
{% endgp %}

`data=fmri.query("event == 'stim'")` or not
{% gp 1-2 %}
<img src="/images/2020-03/0326_sns_plot_visual2_de.png">
<img src="/images/2020-03/0326_sns_plot_visual2_de2.png">
{% endgp %}
-->

```python
import os
def load_dataset(name, cache=True, data_home=None, **kws):
    """Load a dataset from the online repository (requires internet).

    Parameters
    ----------
    name : str
        Name of the dataset (`name`.csv on
        https://github.com/mwaskom/seaborn-data).  You can obtain list of
        available datasets using :func:`get_dataset_names`
    cache : boolean, optional
        If True, then cache data locally and use the cache on subsequent calls
    data_home : string, optional
        The directory in which to cache data. By default, uses ~/seaborn-data/
    kws : dict, optional
        Passed to pandas.read_csv

    """
    # path = ("https://raw.githubusercontent.com/"
    #         "mwaskom/seaborn-data/master/{}.csv")
    path = './Seaborn/{}.csv'
    full_path = path.format(name)
    '''
    if cache:
        cache_path = os.path.join(get_data_home(data_home),
                                  os.path.basename(full_path))
        if not os.path.exists(cache_path):
            urlretrieve(full_path, cache_path)
        full_path = cache_path
    '''
    df = pd.read_csv(full_path, **kws)
    if df.iloc[-1].isnull().all():
        df = df.iloc[:-1]

    # Set some columns as a categorical type with ordered levels

    if name == "tips":
        df["day"] = pd.Categorical(df["day"], ["Thur", "Fri", "Sat", "Sun"])
        df["sex"] = pd.Categorical(df["sex"], ["Male", "Female"])
        df["time"] = pd.Categorical(df["time"], ["Lunch", "Dinner"])
        df["smoker"] = pd.Categorical(df["smoker"], ["Yes", "No"])

    if name == "flights":
        df["month"] = pd.Categorical(df["month"], df.month.unique())

    if name == "exercise":
        df["time"] = pd.Categorical(df["time"], ["1 min", "15 min", "30 min"])
        df["kind"] = pd.Categorical(df["kind"], ["rest", "walking", "running"])
        df["diet"] = pd.Categorical(df["diet"], ["no fat", "low fat"])

    if name == "titanic":
        df["class"] = pd.Categorical(df["class"], ["First", "Second", "Third"])
        df["deck"] = pd.Categorical(df["deck"], list("ABCDEFG"))

    return df

dots = load_dataset("dots").query("align == 'dots'")
```
```python
# dots = sns.load_dataset("dots").query("align == 'dots'")
sns.relplot(x="time", y="firing_rate",
            hue="coherence", style="choice",
            kind="line", data=dots)

palette = sns.cubehelix_palette(light=.8, n_colors=6)
sns.relplot(x="time", y="firing_rate",
            hue="coherence", style="choice",
            palette=palette,
            kind="line", data=dots)

from matplotlib.colors import LogNorm
palette = sns.cubehelix_palette(light=.7, n_colors=6)
sns.relplot(x="time", y="firing_rate",
            hue="coherence", style="choice",
            hue_norm=LogNorm(),
            kind="line", data=dots)

sns.relplot(x="time", y="firing_rate",
            size="coherence", style="choice",
            kind="line", data=dots)

sns.relplot(x="time", y="firing_rate",
            hue="coherence", size="choice",
            palette=palette,
            kind="line", data=dots)

plt.show()
```
{% gp 5-3 %}
<img src="http://seaborn.pydata.org/_images/relational_43_0.png">
<img src="http://seaborn.pydata.org/_images/relational_45_0.png">
<img src="http://seaborn.pydata.org/_images/relational_47_0.png">
<img src="http://seaborn.pydata.org/_images/relational_49_0.png">
<img src="http://seaborn.pydata.org/_images/relational_51_0.png">
{% endgp %}
<!--
{% gp 5-3 %}
<img src="/images/2020-03/0326_sns_plot_visual2_ea.png">
<img src="/images/2020-03/0326_sns_plot_visual2_eb.png">
<img src="/images/2020-03/0326_sns_plot_visual2_ec.png">
<img src="/images/2020-03/0326_sns_plot_visual2_ed.png">
<img src="/images/2020-03/0326_sns_plot_visual2_ee.png">
{% endgp %}
-->

##### Plotting with date data

```python
df = pd.DataFrame(dict(time=pd.date_range("2017-1-1", periods=500),
                    value=np.random.randn(500).cumsum()))
g = sns.relplot(x="time", y="value", kind="line", data=df)
g.fig.autofmt_xdate()

plt.show()
```
<img src="/images/2020-03/0326_sns_plot_visual2_f.png" width="50%">

#### [<font color=#87CEFA>Showing multiple relationships with facets</font>](http://seaborn.pydata.org/tutorial/relational.html#showing-multiple-relationships-with-facets)

```python
tips = load_dataset("tips")
# tips = sns.load_dataset("tips")
sns.relplot(x="total_bill", y="tip", hue="smoker",
            col="time", data=tips)

fmri = sns.load_dataset("fmri")
sns.relplot(x="timepoint", y="signal", hue="subject",
            col="region", row="event", height=3,
            kind="line", estimator=None, data=fmri)

sns.relplot(x="timepoint", y="signal", hue="event", style="event",
            col="subject", col_wrap=5,
            height=3, aspect=.75, linewidth=2.5,
            kind="line", data=fmri.query("region == 'frontal'"))

plt.show()
```
<img src="http://seaborn.pydata.org/_images/relational_55_0.png"><img src="/images/2020-03/0327_sns_plot_visual_3b.png"><img src="http://seaborn.pydata.org/_images/relational_59_0.png">
<!--
<img src="/images/2020-03/0327_sns_plot_visual_3a.png"><img src="/images/2020-03/0327_sns_plot_visual_3b.png"><img src="/images/2020-03/0327_sns_plot_visual_3c.png">
-->

### [<font color=#8470FF>Plotting with categorical data</font>](http://seaborn.pydata.org/tutorial/categorical.html)

It’s helpful to think of the different categorical plot kinds as belonging to three different families, which we’ll discuss in detail below. They are:
- Categorical scatterplots:
  - stripplot() (with kind="strip"; the default)
  - swarmplot() (with kind="swarm")
- Categorical distribution plots:
  - boxplot() (with kind="box")
  - violinplot() (with kind="violin")
  - boxenplot() (with kind="boxen")
- Categorical estimate plots:
  - pointplot() (with kind="point")
  - barplot() (with kind="bar")
  - countplot() (with kind="count")

These families represent the data using different levels of granularity. When deciding which to use, you’ll have to think about the question that you want to answer.
```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="ticks", color_codes=True)
```

#### [<font color=#87CEFA>Categorical scatterplots</font>](http://seaborn.pydata.org/tutorial/categorical.html#categorical-scatterplots)

```python
tips = load_dataset("tips")
# tips = sns.load_dataset("tips")

sns.catplot(x="day", y="total_bill", data=tips)
sns.catplot(x="day", y="total_bill", jitter=False, data=tips)
sns.catplot(x="day", y="total_bill", kind="swarm", data=tips)
sns.catplot(x="day", y="total_bill", hue="sex", kind="swarm", data=tips)

sns.catplot(x="size", y="total_bill", kind="swarm",
            data=tips.query("size != 3"))
sns.catplot(x="smoker", y="tip", order=["No", "Yes"], data=tips)

sns.catplot(x="total_bill", y="day", hue="time", kind="swarm", data=tips)

plt.show()
```

`x="day", y="total_bill"`
{% gp 4-3 %}
<img src="http://seaborn.pydata.org/_images/categorical_4_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_6_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_8_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_10_0.png">
{% endgp %}
`x=?, y=?` and `x="total_bill", y="day"`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_12_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_14_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_16_0.png">
{% endgp %}

<!--
{% gp 4-3 %}
<img src="/images/2020-03/0327_sns_plot_category1_aa.png">
<img src="/images/2020-03/0327_sns_plot_category1_ab.png">
<img src="/images/2020-03/0327_sns_plot_category1_ac.png">
<img src="/images/2020-03/0327_sns_plot_category1_ad.png">
{% endgp %}
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category1_ba.png">
<img src="/images/2020-03/0327_sns_plot_category1_bb.png">
<img src="/images/2020-03/0327_sns_plot_category1_bc.png">
{% endgp %}
-->
<!--Hello World-->

#### [<font color=#87CEFA>Distributions of observations within categories</font>](http://seaborn.pydata.org/tutorial/categorical.html#distributions-of-observations-within-categories)

##### Boxplots

```python
tips = load_dataset("tips")
# tips = sns.load_dataset("tips")

sns.catplot(x="day", y="total_bill", kind="box", data=tips)
sns.catplot(x="day", y="total_bill", hue="smoker", kind="box", data=tips)

tips["weekend"] = tips["day"].isin(["Sat", "Sun"])
sns.catplot(x="day", y="total_bill", hue="weekend",
            kind="box", dodge=False, data=tips)
# f = sns.catplot(x="day", y="total_bill", hue="weekend",
#             kind="box", dodge=True, data=tips)

plt.show()
```
`x,y` with or without `hue="smoker"`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_18_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_20_0.png">
{% endgp %}
different `dodgo`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_22_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_ac2.png">
{% endgp %}

```python
diamonds = sns.load_dataset("diamonds")
sns.catplot(x="color", y="price", kind="boxen",
            data=diamonds.sort_values("color"))
# f = sns.catplot(x="color", y="price", kind="box",
#             data=diamonds.sort_values("color"))

plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_24_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_b2.png">
{% endgp %}
<!--
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_aa.png">
<img src="/images/2020-03/0327_sns_plot_category2_ab.png">
{% endgp %}
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_ac.png">
<img src="/images/2020-03/0327_sns_plot_category2_ac2.png">
{% endgp %}

{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_b.png">
<img src="/images/2020-03/0327_sns_plot_category2_b2.png">
{% endgp %}
-->
<!--Hello World-->

##### Violinplots

```python
tips = load_dataset("tips")
# tips = sns.load_dataset("tips")

sns.catplot(x="total_bill", y="day", hue="sex",
            kind="violin", data=tips)
# f1 = sns.catplot(x="day", y="total_bill", hue="sex",
#             kind="violin", data=tips)

sns.catplot(x="total_bill", y="day", hue="sex",
            kind="violin", bw=.15, cut=0,
            data=tips)
sns.catplot(x="day", y="total_bill", hue="sex",
            kind="violin", split=True, data=tips)
# f2 = sns.catplot(x="day", y="total_bill", hue="sex",
#             kind="violin", split=False, data=tips) # default: split=False

sns.catplot(x="day", y="total_bill", hue="sex",
            kind="violin", inner="stick", split=True,
            palette="pastel", data=tips)

g = sns.catplot(x="day", y="total_bill", kind="violin", inner=None, data=tips)
sns.swarmplot(x="day", y="total_bill", color="k", size=3, data=tips, ax=g.ax)

plt.show()
```
exchange `x` and `y`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_26_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_ca2cc2.png">
{% endgp %}
`bw=.15, cut=0` and `split=True (default: False)`
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/categorical_28_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_30_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_ca2cc2.png">
{% endgp %}
including param `inner`
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_32_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_34_0.png">
{% endgp %}
<!--
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_ca.png">
<img src="/images/2020-03/0327_sns_plot_category2_ca2cc2.png">
{% endgp %}
{% gp 1-3 %}
<img src="/images/2020-03/0327_sns_plot_category2_cb.png">
<img src="/images/2020-03/0327_sns_plot_category2_cc.png">
<img src="/images/2020-03/0327_sns_plot_category2_ca2cc2.png">
{% endgp %}
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_cd.png">
<img src="/images/2020-03/0327_sns_plot_category2_ce.png">
{% endgp %}
-->
<!--Hello World-->

#### [<font color=#87CEFA>Statistical estimation within categories</font>](http://seaborn.pydata.org/tutorial/categorical.html#statistical-estimation-within-categories)

##### Bar plots

```python
titanic = load_dataset("titanic")
# titanic = sns.load_dataset("titanic")

sns.catplot(x="sex", y="survived", hue="class", kind="bar", data=titanic)
sns.catplot(x="deck", kind="count", palette="ch:.25", data=titanic)
# f = sns.catplot(x="deck", kind="count", palette="ch:25", data=titanic)
sns.catplot(y="deck", hue="class", kind="count",
            palette="pastel", edgecolor=".6",
            data=titanic)

plt.show()
```
{% gp 7-3 %}
<img src="http://seaborn.pydata.org/_images/categorical_36_0.png">
<img src="">
<img src="http://seaborn.pydata.org/_images/categorical_38_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_db2.png">
<img src="http://seaborn.pydata.org/_images/categorical_40_0.png">
<img src="">
{% endgp %}
<!--
<img src="http://seaborn.pydata.org/_images/categorical_36_0.png" width="50%">
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_38_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_db2.png">
{% endgp %}
<img src="http://seaborn.pydata.org/_images/categorical_40_0.png" width="50%">
-->
<!--Hello World-->
<!--
<img src="/images/2020-03/0327_sns_plot_category2_da.png" width="50%">
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_db.png">
<img src="/images/2020-03/0327_sns_plot_category2_db2.png">
{% endgp %}
<img src="/images/2020-03/0327_sns_plot_category2_dc.png" width="50%">
-->
<!--Hello World-->

##### Point plots

```python
titanic = load_dataset("titanic")
# titanic = sns.load_dataset("titanic")

sns.catplot(x="sex", y="survived", hue="class", kind="point", data=titanic)
f = sns.catplot(x="class", y="survived", hue="sex", kind="point", data=titanic)

sns.catplot(x="class", y="survived", hue="sex",
            palette={"male": "g", "female": "m"},
            marker=["^", "o"], linestyles=["-", "--"],
            kind="point", data=titanic)

plt.show()
```
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/categorical_42_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_ea2eb2.png">
<img src="http://seaborn.pydata.org/_images/categorical_44_0.png">
{% endgp %}
<!--
{% gp 1-3 %}
<img src="/images/2020-03/0327_sns_plot_category2_ea.png">
<img src="/images/2020-03/0327_sns_plot_category2_ea2eb2.png">
<img src="/images/2020-03/0327_sns_plot_category2_eb.png">
{% endgp %}
-->
<!--Hello World-->

#### [<font color=#87CEFA>Plotting "wide-form" data</font>](http://seaborn.pydata.org/tutorial/categorical.html#plotting-wide-form-data)

```python
iris = sns.load_dataset("iris")

#! Part 1
sns.catplot(data=iris, orient="h", kind="box")
# g = sns.catplot(data=iris, kind="box")

#! Part 2
sns.violinplot(x=iris.species, y=iris.sepal_length)

#! Part 3
titanic = load_dataset("titanic")
# titanic = sns.load_dataset("titanic")
f, ax = plt.subplots(figsize=(7, 3))
sns.countplot(y="deck", data=titanic, color="c")

plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_46_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_fa2.png">
{% endgp %}
<img src="http://seaborn.pydata.org/_images/categorical_48_0.png" width="50%"><img src="http://seaborn.pydata.org/_images/categorical_50_0.png" width="70%">
<!--
{% gp 1-2 %}
<img src="/images/2020-03/0327_sns_plot_category2_fa.png">
<img src="/images/2020-03/0327_sns_plot_category2_fa2.png">
{% endgp %}
<img src="/images/2020-03/0327_sns_plot_category2_fb.png" width="50%"><img src="/images/2020-03/0327_sns_plot_category2_fc.png" width="70%">
-->
<!--Hello World-->

#### [<font color=#87CEFA>Showing multiple relationships with facets</font>](http://seaborn.pydata.org/tutorial/categorical.html#showing-multiple-relationships-with-facets)

```python
tips = load_dataset("tips")
# tips = sns.load_dataset("tips")
sns.catplot(x="day", y="total_bill", hue="smoker",
            col="time", aspect=.6,
            kind="swarm", data=tips)

titanic = load_dataset("titanic")
# titanic = sns.load_dataset("titanic")
g = sns.catplot(x="fare", y="survived", row="class",
                kind="box", orient="h", height=1.5, aspect=4,
                data=titanic.query("fare > 0"))
g.set(xscale="log")

plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/categorical_52_0.png">
<img src="http://seaborn.pydata.org/_images/categorical_54_0.png">
{% endgp %}

### [<font color=#8470FF>Visualizing the distribution of a dataset</font>](http://seaborn.pydata.org/tutorial/distributions.html)

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats
sns.set(color_codes=True)
```

#### [<font color=#87CEFA>Plotting univariate distributions</font>](http://seaborn.pydata.org/tutorial/distributions.html#plotting-univariate-distributions)

```python
x = np.random.normal(size=100)
sns.distplot(x)
plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/distributions_6_0.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_a.png">
{% endgp %}

##### Histograms

```python
sns.distplot(x, kde=False, rug=True)
# f2 = sns.distplot(x, kde=False, rug=False)
# f3 = sns.distplot(x, kde=True, rug=True)
# f4 = sns.distplot(x, kde=True, rug=False)  # default
```
{% gp 4-3 %}
<img src="/images/2020-03/0327_sns_plot_distrib1_b.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_b2.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_b3.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_b4.png">
{% endgp %}

```python
sns.distplot(x, bins=20, kde=False, rug=True)
# f2 = sns.distplot(x, bins=10, kde=False, rug=True)
# f3 = sns.distplot(x, bins=40, kde=False, rug=True)
```
{% gp 1-3 %}
<img src="/images/2020-03/0327_sns_plot_distrib1_c.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_c2.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_c3.png">
{% endgp %}

##### Kernel density estimation

```python
x = np.random.normal(size=100)
sns.distplot(x, hist=False, rug=True)
plt.show()
```
<!--
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/distributions_12_0.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_d.png">
{% endgp %}
-->
<img src="http://seaborn.pydata.org/_images/distributions_12_0.png" width="50%">

```python
x = np.random.normal(0, 1, size=30)
bandwidth = 1.06 * x.std() * x.size ** (-1 / 5.)
support = np.linspace(-4, 4, 200)

kernels = []
for x_i in x:
    kernel = stats.norm(x_i, bandwidth).pdf(support)

    kernels.append(kernel)
    plt.plot(support, kernel, color="r")

sns.rugplot(x, color=".2", linewidth=3)

plt.show()
```
<!--
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/distributions_14_0.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_e.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_e2.png">
{% endgp %}
-->
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/distributions_14_0.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_e2.png">
{% endgp %}

```python
x = np.random.normal(0, 1, size=30)
bandwidth = 1.06 * x.std() * x.size ** (-1 / 5.)
support = np.linspace(-4, 4, 200)
kernels = []
for x_i in x:
    kernel = stats.norm(x_i, bandwidth).pdf(support)
    kernels.append(kernel)

from scipy.integrate import trapz
density = np.sum(kernels, axis=0)
density /= trapz(density, support)
plt.plot(support, density)

plt.show()
```
<!--
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/distributions_16_0.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_f.png">
{% endgp %}
-->
<img src="http://seaborn.pydata.org/_images/distributions_16_0.png" width="50%">

```python

x = np.random.normal(0, 1, size=30)
sns.kdeplot(x, shade=True)
# sns.kdeplot(x, shade=False)  # default
plt.show()
```
<!--
<img src="/images/2020-03/0327_sns_plot_distrib1_g.png">
<img src="/images/2020-03/0327_sns_plot_distrib1_g2.png">
-->
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/distributions_18_0.png">
<img src="http://seaborn.pydata.org/_images/distributions_16_0.png">
{% endgp %}

```python
x = np.random.normal(0, 1, size=30)

sns.kdeplot(x)
sns.kdeplot(x, bw=.2, label="bw: 0.2")
sns.kdeplot(x, bw=2, label="bw: 2")
plt.legend()

plt.show()
```
<img src="http://seaborn.pydata.org/_images/distributions_20_0.png" width="50%">

```python
sns.kdeplot(x, shade=True, cut=0)
sns.rugplot(x)
plt.show()
#i.e.,


fig, axs = plt.subplots(2, 3, figsize=(9, 6))

plt.subplot(2, 3, 1)
sns.kdeplot(x, shade=True, cut=0)
sns.rugplot(x)
plt.title('Original')

plt.subplot(2, 3, 2)
sns.kdeplot(x, shade=True, cut=0)
plt.title('Only kdeplot')

plt.subplot(2, 3, 3)
sns.rugplot(x)
plt.title('Only rugplot')

plt.subplot(2, 3, 4)
sns.kdeplot(x, shade=False, cut=0)
sns.rugplot(x)
plt.title('shade=False')

plt.subplot(2, 3, 5)
sns.kdeplot(x, shade=True, cut=1)
sns.rugplot(x)
plt.title('cut=1')

plt.subplot(2, 3, 6)
sns.kdeplot(x, shade=True, cut=2)
sns.rugplot(x)
plt.title('cut=2')

plt.tight_layout()
plt.show()
```
<img src="http://seaborn.pydata.org/_images/distributions_22_0.png" width="50%"><img src="/images/2020-03/0327_sns_plot_distrib1_h2.png" width="100%">

##### Fitting parametric distributions

```python
x = np.random.gamma(6, size=200)
sns.distplot(x, kde=False, fit=stats.gamma)
plt.show()
#! i.e.,


fig, axs = plt.subplots(1, 2, figsize=(8, 4))

plt.subplot(1, 2, 1)
sns.distplot(x, kde=False, fit=stats.gamma)
plt.title('Original')

plt.subplot(1, 2, 2)
sns.distplot(x, kde=True, fit=stats.gamma)
plt.title('kde=True')
plt.legend()

plt.tight_layout()
plt.show()
```
<img src="http://seaborn.pydata.org/_images/distributions_24_0.png" width="50%"><img src="/images/2020-03/0327_sns_plot_distrib1_i3.png" width="100%">

#### [<font color=#87CEFA>Plotting bivariate distributions</font>](http://seaborn.pydata.org/tutorial/distributions.html#plotting-bivariate-distributions)

```python
mean, cov = [0, 1], [(1, .5), (.5, 1)]
data = np.random.multivariate_normal(mean, cov, 200)
df = pd.DataFrame(data, columns=["x", "y"])
```

##### Scatterplots

```python
sns.jointplot(x="x", y="y", data=df)
plt.show()
```
<img src="http://seaborn.pydata.org/_images/distributions_28_0.png" width="60%">

##### Hexbin plots

```python
x, y = np.random.multivariate_normal(mean, cov, 1000).T
with sns.axes_style("white"):
    sns.jointplot(x=x, y=y, kind="hex", color="k")
plt.show()
```
<img src="http://seaborn.pydata.org/_images/distributions_30_0.png" width="60%">

##### Kernel density estimation

```python
sns.jointplot(x="x", y="y", data=df, kind="kde")
plt.show()

f, ax = plt.subplots(figsize=(6, 6))
sns.kdeplot(df.x, df.y, ax=ax)
sns.rugplot(df.x, color="g", ax=ax)
sns.rugplot(df.y, vertical=True, ax=ax)
plt.show()

f, ax = plt.subplots(figsize=(6, 6))
cmap = sns.cubehelix_palette(as_cmap=True, dark=0, light=1, reverse=True)
sns.kdeplot(df.x, df.y, cmap=cmap, n_levels=60, shade=True)
plt.show()

g = sns.jointplot(x="x", y="y", data=df, kind="kde", color="m")
g.plot_joint(plt.scatter, c="w", s=30, linewidth=1, marker="+")
g.ax_joint.collections[0].set_alpha(0)
g.set_axis_labels("$X$", "$Y$")
plt.show()
```

{% gp 4-3 %}
<img src="http://seaborn.pydata.org/_images/distributions_32_0.png">
<img src="http://seaborn.pydata.org/_images/distributions_34_0.png">
<img src="http://seaborn.pydata.org/_images/distributions_36_0.png">
<img src="http://seaborn.pydata.org/_images/distributions_38_0.png">
{% endgp %}

#### [<font color=#87CEFA>Visualizing pairwise relationships in a dataset</font>](http://seaborn.pydata.org/tutorial/distributions.html#visualizing-pairwise-relationships-in-a-dataset)

```python
iris = sns.load_dataset("iris")

sns.pairplot(iris)
plt.show()

sns.pairplot(iris, hue="species")
plt.show()

g = sns.PairGrid(iris)
g.map_diag(sns.kdeplot)
g.map_offdiag(sns.kdeplot, n_levels=6)
plt.show()
```

<img src="http://seaborn.pydata.org/_images/distributions_40_0.png" width="100%"><img src="http://seaborn.pydata.org/_images/distributions_42_0.png" width="100%"><img src="http://seaborn.pydata.org/_images/distributions_44_0.png" width="100%">

### [<font color=#8470FF>Visualizing linear relationships</font>](http://seaborn.pydata.org/tutorial/regression.html)

```python
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

sns.set(color_codes=True)
```

#### [<font color=#87CEFA>Functions to draw linear regression models</font>](http://seaborn.pydata.org/tutorial/regression.html#functions-to-draw-linear-regression-models)

```python
# tips = sns.load_dataset("tips")
tips = load_dataset("tips")

sns.regplot(x="total_bill", y="tip", data=tips)
sns.lmplot(x="total_bill", y="tip", data=tips)

sns.lmplot(x="size", y="tip", data=tips)
sns.lmplot(x="size", y="tip", data=tips, x_jitter=.05)
sns.lmplot(x="size", y="tip", data=tips, x_estimator=np.mean)

plt.show()
```

{% gp 5-3 %}
<img src="http://seaborn.pydata.org/_images/regression_7_0.png">
<img src="http://seaborn.pydata.org/_images/regression_8_0.png">
<img src="http://seaborn.pydata.org/_images/regression_10_0.png">
<img src="http://seaborn.pydata.org/_images/regression_12_0.png">
<img src="http://seaborn.pydata.org/_images/regression_14_0.png">
{% endgp %}

#### [<font color=#87CEFA>Fitting different kinds of models</font>](http://seaborn.pydata.org/tutorial/regression.html#fitting-different-kinds-of-models)

```python
anscombe = sns.load_dataset("anscombe")

sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'I'"),
            ci=None, scatter_kws={"s": 80})

sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'II'"),
            ci=None, scatter_kws={"s": 80})
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'II'"),
            order=2, ci=None, scatter_kws={"s": 80})

sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'III'"),
            ci=None, scatter_kws={"s": 80})
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'III'"),
           robust=True, ci=None, scatter_kws={"s": 80})

plt.show()
```
<!--
<img src="http://seaborn.pydata.org/_images/regression_17_0.png" width="50%">
{% gp 4-3 %}
<img src="">
<img src="http://seaborn.pydata.org/_images/regression_19_0.png">
<img src="http://seaborn.pydata.org/_images/regression_21_0.png">
<img src="http://seaborn.pydata.org/_images/regression_23_0.png">
<img src="http://seaborn.pydata.org/_images/regression_25_0.png">
{% endgp %}
-->
<!--Hello World-->
{% gp 8-7 %}
<img src="http://seaborn.pydata.org/_images/regression_17_0.png">
<img src="http://seaborn.pydata.org/_images/regression_19_0.png">
<img src="http://seaborn.pydata.org/_images/regression_21_0.png">
<img src="">
<img src="http://seaborn.pydata.org/_images/regression_23_0.png">
<img src="http://seaborn.pydata.org/_images/regression_25_0.png">
{% endgp %}

```python
tips["big_tip"] = (tips.tip / tips.total_bill) > .15
sns.lmplot(x="total_bill", y="big_tip", data=tips,
           y_jitter=.03)

sns.lmplot(x="total_bill", y="big_tip", data=tips,
           logistic=True, y_jitter=.03)

sns.lmplot(x="total_bill", y="tip", data=tips,
           lowess=True)

plt.show()
```
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/regression_27_0.png">
<img src="http://seaborn.pydata.org/_images/regression_29_0.png">
<img src="http://seaborn.pydata.org/_images/regression_31_0.png">
{% endgp %}

```python
sns.residplot(x="x", y="y", data=anscombe.query("dataset == 'I'"),
              scatter_kws={"s": 80})
plt.show()

sns.residplot(x="x", y="y", data=anscombe.query("dataset == 'II'"),
              scatter_kws={"s": 80})
plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/regression_33_0.png">
<img src="http://seaborn.pydata.org/_images/regression_35_0.png">
{% endgp %}

#### [<font color=#87CEFA>Conditioning on other variables</font>](http://seaborn.pydata.org/tutorial/regression.html#conditioning-on-other-variables)

```python
sns.lmplot(x="total_bill", y="tip", hue="smoker", data=tips)

sns.lmplot(x="total_bill", y="tip", hue="smoker", data=tips,
           markers=["o", "x"], palette="Set1")

sns.lmplot(x="total_bill", y="tip", hue="smoker", col="time", data=tips)

sns.lmplot(x="total_bill", y="tip", hue="smoker",
           col="time", row="sex", data=tips)

plt.show()
```
{% gp 1-2 %}
<img src="http://seaborn.pydata.org/_images/regression_37_0.png">
<img src="http://seaborn.pydata.org/_images/regression_39_0.png">
{% endgp %}
<img src="http://seaborn.pydata.org/_images/regression_41_0.png" width="90%"><img src="http://seaborn.pydata.org/_images/regression_42_0.png" width="90%"> <!--50%, 100%-->

#### [<font color=#87CEFA>Controlling the size and shape of the plot</font>](http://seaborn.pydata.org/tutorial/regression.html#controlling-the-size-and-shape-of-the-plot)

```python
f, ax = plt.subplots(figsize=(5, 6))
sns.regplot(x="total_bill", y="tip", data=tips, ax=ax)

sns.lmplot(x="total_bill", y="tip", col="day", data=tips,
           col_wrap=2, height=3)

sns.lmplot(x="total_bill", y="tip", col="day", data=tips,
           aspect=.5)

plt.show()
```
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/regression_44_0.png">
<img src="http://seaborn.pydata.org/_images/regression_46_0.png">
<img src="http://seaborn.pydata.org/_images/regression_47_0.png">
{% endgp %}

#### [<font color=#87CEFA>Plotting a regression in other contexts</font>](http://seaborn.pydata.org/tutorial/regression.html#plotting-a-regression-in-other-contexts)

```python
sns.jointplot(x="total_bill", y="tip", data=tips, kind="reg")

sns.pairplot(tips, x_vars=["total_bill", "size"], y_vars=["tip"],
             height=5, aspect=.8, kind="reg")

sns.pairplot(tips, x_vars=["total_bill", "size"], y_vars=["tip"],
             hue="smoker", height=5, aspect=.8, kind="reg")

plt.show()
```
{% gp 1-3 %}
<img src="http://seaborn.pydata.org/_images/regression_49_0.png">
<img src="http://seaborn.pydata.org/_images/regression_51_0.png">
<img src="http://seaborn.pydata.org/_images/regression_53_0.png">
{% endgp %}



## Multi-plot grids

### [<font color=#40E0D0>Building structured multi-plot grids</font>](http://seaborn.pydata.org/tutorial/axis_grids.html)
#### [<font color=#66CDAA>Conditional small multiples</font>](http://seaborn.pydata.org/tutorial/axis_grids.html#conditional-small-multiples)
#### [<font color=#66CDAA>Using custom functions</font>](http://seaborn.pydata.org/tutorial/axis_grids.html#using-custom-functions)
#### [<font color=#66CDAA>Plotting pairwise data relationships</font>](http://seaborn.pydata.org/tutorial/axis_grids.html#plotting-pairwise-data-relationships)


## Plot aesthetics

### [<font color=#40E0D0>Controlling figure aesthetics</font>](http://seaborn.pydata.org/tutorial/aesthetics.html)
#### [<font color=#66CDAA>Seaborn figure styles</font>](http://seaborn.pydata.org/tutorial/aesthetics.html#seaborn-figure-styles)
#### [<font color=#66CDAA>Removing axes spines</font>](http://seaborn.pydata.org/tutorial/aesthetics.html#removing-axes-spines)
#### [<font color=#66CDAA>Temporarily setting figure style</font>](http://seaborn.pydata.org/tutorial/aesthetics.html#temporarily-setting-figure-style)
#### [<font color=#66CDAA>Overriding elements of the seaborn styles</font>](http://seaborn.pydata.org/tutorial/aesthetics.html#overriding-elements-of-the-seaborn-styles)
#### [<font color=#66CDAA>Scaling plot elements</font>](http://seaborn.pydata.org/tutorial/aesthetics.html#scaling-plot-elements)

### [<font color=#40E0D0>Choosing color palettes</font>](http://seaborn.pydata.org/tutorial/color_palettes.html)
#### [<font color=#66CDAA>Building color palettes</font>](http://seaborn.pydata.org/tutorial/color_palettes.html#building-color-palettes)
#### [<font color=#66CDAA>Qualitative color palettes</font>](http://seaborn.pydata.org/tutorial/color_palettes.html#qualitative-color-palettes)
#### [<font color=#66CDAA>Sequential color palettes</font>](http://seaborn.pydata.org/tutorial/color_palettes.html#sequential-color-palettes)
#### [<font color=#66CDAA>Diverging color palettes</font>](http://seaborn.pydata.org/tutorial/color_palettes.html#diverging-color-palettes)
#### [<font color=#66CDAA>Setting the default color palette</font>](http://seaborn.pydata.org/tutorial/color_palettes.html#setting-the-default-color-palette)


# Valuable examples
ref: [深度好文 | Matplotlib可视化最有价值的 50 个图表（附完整 Python 源代码）](http://liyangbit.com/pythonvisualization/matplotlib-top-50-visualizations/)  

<ol style="line-height: 1ex; list-style-type: lower-roman;">
  <li>关联 (Correlation)
    <ol style="line-height: 1em; list-style-type: decimal;">
      <li>散点图 (Scatter plot)</li>
      <li>带边界的气泡图 (Bubble plot with Encircling)</li>
      <li>带线性回归最佳拟合线的散点图 (Scatter plot with linear regression line of best fit)</li>
      <li>抖动图 (Jittering with stripplot)</li>
      <li>计数图 (Counts Plots)</li>
      <li>边缘直方图 (Marginal Histogram)</li>
      <li>边缘箱型图 (Marginal Boxplot)</li>
      <li>相关图 (Correllogram)</li>
      <li>矩阵图 (Pairwise Plot)</li>
    </ol>
  </li>
  <li>偏差 (Deviation)
    <ol style="line-height: 1em; list-style-type: decimal;" start="10">
      <li>发散性条形图 (Diverging Bars)</li>
      <li>发散性文本 (Diverging Texts)</li>
      <li>发散性包点图 (Diverging Dot Plot)</li>
      <li>带标记的发散性棒棒糖图 (Diverging Lollipop Chart with Markers)</li>
      <li>面积图 (Area Chart)</li>
    </ol>
  </li>
  <li>排序 (Ranking)
    <ol style="line-height: 1em; list-style-type: decimal;" start="15">
      <li>有序条形图 (Ordered Bar Chart)</li>
      <li>棒棒糖图 (Lollipop Chart)</li>
      <li>包点图 (Dot Plot)</li>
      <li>坡度图 (Slope Chart)</li>
      <li>哑铃图 (Dumbbell Plot)</li>
    </ol>
  </li>
  <li>分布 (Distribution)
    <ol style="line-height: 1em; list-style-type: decimal;" start="20">
      <li>连续变量的直方图 (Histogram for Continuous Variable)</li>
      <li>类型变量的直方图 (Histogram for Categorical Variable)</li>
      <li>密度图 (Density Plot)</li>
      <li>直方密度线图 (Density Curves with Histogram)</li>
      <li>Joy Plot</li> <!--欢欣图-->
      <li>分布式包点图 (Distributed Dot Plot)</li>
      <li>箱形图 (Box Plot)</li>
      <li>包点+箱形图 (Dot + Box Plot)</li>
      <li>小提琴图 (Violin Plot)</li>
      <li>人口金字塔 (Population Pyramid)</li>
      <li>分类图 (Categorical Plots)</li>
    </ol>
  </li>
  <li>组成 (Composition)
    <ol style="line-height: 1em; list-style-type: decimal;" start="31">
      <li>华夫饼图 (Waffle Chart)</li>
      <li>饼图 (Pie Chart)</li>
      <li>树形图 (Treemap)</li>
      <li>条形图 (Bar Chart)</li>
    </ol>
  </li>
  <li>变化 (Change)
    <ol style="line-height: 1em; list-style-type: decimal;" start="35">
      <li>时间序列图 (Time Series Plot)</li>
      <li>带波峰波谷标记的时序图 (Time Series with Peaks and Troughs Annotated)</li>
      <li>自相关和部分自相关图 (Autocorrelation (ACF) and Partial Autocorrelation (PACF) Plot)</li>
      <li>交叉相关图 (Cross Correlation plot)</li>
      <li>时间序列分解图 (Time Series Decomposition Plot)</li>
      <li>多个时间序列 (Multiple Time Series)</li>
      <li>使用辅助 Y 轴来绘制不同范围的图形 (Plotting with different scales using secondary Y axis)</li>
      <li>带有误差带的时间序列 (Time Series with Error Bands)</li>
      <li>堆积面积图 (Stacked Area Chart)</li>
      <li>未堆积的面积图 (Area Chart UnStacked)</li>
      <li>日历热力图 (Calendar Heat Map)</li>
      <li>季节图 (Seasonal Plot)</li>
    </ol>
  </li>
  <li>分组 (Groups)
    <ol style="line-height: 1em; list-style-type: decimal;" start="47">
      <li>树状图 (Dendrogram)</li>
      <li>簇状图 (Cluster Plot)</li>
      <li>安德鲁斯曲线 (Andrews Curve)</li>
      <li>平行坐标 (Parallel Coordinates)</li>
    </ol>
  </li>
</ol>


# \*References

**seaborn 保存图片**  
[python 通过seaborn,matplotlib 画出的图如何通过代码保存或调用？](https://www.zhihu.com/question/54659030)  
[匿名用户的回答](https://www.zhihu.com/question/54659030/answer/637680015)  
[Jupyter example](https://nbviewer.jupyter.org/github/ipython/ipython/blob/4.0.x/examples/IPython%20Kernel/Rich%20Output.ipynb)  

*下面这种写法 `seaborn.version == 0.8.1` 可行*  
1. 存储为 `.png`, e.g.,
```python
g3 = sns.jointplot("N", "H", data=data_all, kind="reg", 
            scatter_kws=dict(s=45, linewidths=.5, edgecolors='black'),
            robust=True, annot_kws='rrrrrrr')
g3.savefig("n_H_R.png",dpi = 300)
```
写给跟我一样的新手的补充说明:  
(1) 上面一行括号里有的没的不用看，反正就是画个图的意思。  
(2) 下面一行dpi是设置像素的意思，可以不写。  
2. 存储为 `.pdf`, e.g.,
```python
ax = sns.violinplot( x="PA", y="Score", data = data_oneline, palette= c, inner="quartile")
plt.savefig('./p_5.pdf', format='pdf', dpi = 300)
```

**seaborn 展示图片**  
[十分钟掌握Seaborn，进阶Python数据可视化分析](https://cloud.tencent.com/developer/news/354998)  
[seaborn.pairplot绘图不显示问题](https://blog.csdn.net/god_wot/article/details/85100586)  
[seaborn如何显示图？](http://sofasofa.io/forum_main_post.php?postid=1000953)  
[Seaborn 和 Matplotlib 数据可视化](https://www.jianshu.com/p/4b925654f506)  
[seaborn如何将多个图片同时显示出来?](https://www.zhihu.com/question/268942778)  
[解决seaborn在pycharm中绘图不出图的问题](https://www.jb51.net/article/140733.htm)  




