---
title: Debug Tips - cProfile in Python, TensorBoard
date: 2020-04-16 05:08:51
updated: 
categories:
  - Programming
tags:
  - Debug
  - Python
  - TensorFlow
mathjax: true
---

<!--
date: 2020-04-16 05:08:51
-->


# Python Debug: cProfile

## cProfile in Python
**refs:**  
- [使用cProfile分析Python程序性能](https://blog.csdn.net/asukasmallriver/article/details/74356771)  
- [python性能分析工具：cProfile使用](https://blog.csdn.net/u010453363/article/details/78415553)  

为了优化 Python 脚本，使用 cProfile 和 pstats 对其进行性能分析。  
思路：  
1. 使用 cProfile 模块生成脚本执行的统计信息文件
2. 使用 pstats 格式化统计信息，并根据需要做排序分析处理

Step 1, 使用 cProfile 生成脚本执行的统计信息文件
```shell
$ python -m cProfile -o cPro_output.txt script.py -params
```

> 参数说明：
> - 使用模块当做脚本运行： `-m cProfile`
> - 输出参数： `-o cPro_output.txt`
> - 测试的 python 脚本： `script.py`
> - 其余为 python 脚本的输入参数

Step 2, 使用 pstats 查看格式化后的统计信息，可以根据自身需求做排序  
```shell
$ python profiler.py > cProfiler_output.txt
```
其中，profiler.py 文件内容为
```python
import pstats
p=pstats.Stats('./cPro_output.txt')
p.print_stats()
#根据调用次数排序
p.sort_stats('calls').print_stats()
#根据调用总时间排序
p.sort_stats('cumulative').print_stats()
```

> \*Stats类 (pstats.Stats) 说明

| def Function | Illustration |
|----------|--------------|
| strip_dirs() | 用以除去文件名前的路径信息。 |
| add(filename,[…]) | 把 profile 的输出文件加入 Stats 实例中统计 |
| dump_stats(filename) | 把 Stats 的统计结果保存到文件 |
| sort_stats(key,[…]) | 最重要的一个函数，用以排序 profile 的输出 |
| reverse_order() | 把 Stats 实例里的数据反序重排 |
| print_stats([restriction,…]) | 把 Stats 报表输出到 stdout |
| print_callers([restriction,…]) | 输出调用了指定的函数的函数的相关信息 |
| print_callees([restriction,…]) | 输出指定的函数调用过的函数的相关信息 |

> sort_stats 支持以下参数：

| 参数 | 含义 |
|--------|--------|
| ‘calls’           | call count |
| ‘cumulative’ | cumulative time |
| ‘file’          | file name |
| ‘filename’ | file name |
| ‘module’   | module name |
| ‘ncalls’     | call count |
| ‘pcalls’     | primitive call count |
| ‘line’         | line number |
| ‘name’      | function name |
| ‘nfl’           | name/file/line |
| ‘stdname’ | standard name |
| ‘time’     | internal time |
| ‘tottime’ | internal time |

- \* 一个比较典型的输出结果：
```shell
197 function calls (192 primitive calls) in 0.002 seconds
Ordered by: standard name
ncalls tottime percall cumtime percall filename:lineno(function)
1 0.000 0.000 0.001 0.001 :1()
1 0.000 0.000 0.001 0.001 re.py:212(compile)
1 0.000 0.000 0.001 0.001 re.py:268(_compile)
1 0.000 0.000 0.000 0.000 sre_compile.py:172(_compile_charset)
1 0.000 0.000 0.000 0.000 sre_compile.py:201(_optimize_charset)
4 0.000 0.000 0.000 0.000 sre_compile.py:25(_identityfunction)
3/1 0.000 0.000 0.000 0.000 sre_compile.py:33(_compile)
```

- 输出结果说明：
```shell
共有197次函数调用，原始调用为192次，原始调用说明不包含递归调用。
以standard name进行排序。3/1表示发生了递归调用，1为原始调用次数，3为递归调用次数
ncalls 函数的被调用次数
tottime 函数总计运行时间，除去函数中调用的函数运行时间
percall 函数运行一次的平均时间，等于tottime/ncalls
cumtime 函数总计运行时间，含调用的函数运行时间
percall 函数运行一次的平均时间，等于cumtime/ncalls
filename:lineno(function) 函数所在的文件名，函数的行号，函数名
```

## logging v.s. print

代码中若想获知中间结果，使用 print 输出耗时过于巨大。下表是我将对应的 print 都换成 logging 信息后，程序的耗时对比。注意其他代码可认为基本没改。  
我本来也是不知道 print 会对性能有如此之大的影响的，刚换成 logger 后也没有太在意，直到我把两个数值放在一起比较了之后……

<!--Efficiency-->
e.g., Table: Comparison of Time (min) where 
$$Percent = \left(1 - \frac{Time_{\;logger}}{Time_{\;print}} \right)\times 100\%$$

| Example | print | logger | Percent (%) |
|---------|-------|--------|-------------|
| mnist,dnn,b | 192.2485 | 62.3390 | 67.57 |
| mnist,dnn,c | 344.0925 | 77.7800 | 77.40 |
| mnist,dnn,d | 376.3242 | 80.7567 | 78.54 |
| mnist,dnn,e | 698.8540 | 86.6952 | 87.59 |

<!--
typo:
| mnist,dnn,e | 698.8540 | 80.7567 | 88.44 |
fact:
        dnn,d      dnn,e      dnn,d   ERROR
-->

### Example
***Example:***  
- cProfile
```shell
python -m cProfile -o prt_1h.txt compare.py -n 100 -run print
python -m cProfile -o log_1h.txt compare.py -n 100 -run logger
python -m cProfile -o log_1hd.txt compare.py -n 100 -run logger -fmt default
python -m cProfile -o log_1ht.txt compare.py -n 100 -run logger -fmt time

python -m cProfile -o prt_1k.txt compare.py -n 1000 -run print
python -m cProfile -o log_1k.txt compare.py -n 1000 -run logger
python -m cProfile -o log_1kd.txt compare.py -n 1000 -run logger -fmt default
python -m cProfile -o log_1kt.txt compare.py -n 1000 -run logger -fmt time

python -m cProfile -o prt_1m.txt compare.py -n 1000000 -run print
python -m cProfile -o log_1m.txt compare.py -n 1000000 -run logger
python -m cProfile -o log_1md.txt compare.py -n 1000000 -run logger -fmt default
python -m cProfile -o log_1mt.txt compare.py -n 1000000 -run logger -fmt time
```
- pstat
```shell
python cprofiler.py -o prt_1h.txt > cp_prt1h.txt
python cprofiler.py -o log_1h.txt > cp_log1h.txt
python cprofiler.py -o log_1hd.txt > cp_log1hd.txt
python cprofiler.py -o log_1ht.txt > cp_log1ht.txt

python cprofiler.py -o prt_1k.txt > cp_prt1k.txt
python cprofiler.py -o log_1k.txt > cp_log1k.txt
python cprofiler.py -o log_1kd.txt > cp_log1kd.txt
python cprofiler.py -o log_1kt.txt > cp_log1kt.txt

python cprofiler.py -o prt_1m.txt > cp_prt1m.txt
python cprofiler.py -o log_1m.txt > cp_log1m.txt
python cprofiler.py -o log_1md.txt > cp_log1md.txt
python cprofiler.py -o log_1mt.txt > cp_log1mt.txt
```
- `cp_*.txt` 中耗时最多的 tottime  \| 对比表 (seconds)

| `cp_{row}1{col}.txt` | 1h | 1k | 1m |
|----------------------|----|----|----|
| prt | 0.005 | 0.005 | 3.431 |
| log | 0.004 | 0.007 | 0.740 |
| log (default) | 0.006 | 0.006 | 0.934 |
|log (asciitime)| 0.004 | 0.007 | 0.804 |

- Time Cost (s)
```shell
python compare.py -n 5000 -run print
python compare.py -n 5000 -run logger
python compare.py -n 5000 -run logger -fmt default
python compare.py -n 5000 -run logger -fmt time

python compare.py -n 1000000 -run print
python compare.py -n 1000000 -run logger
python compare.py -n 1000000 -run logger -fmt default
python compare.py -n 1000000 -run logger -fmt time
```

| `-n {col} -run {col}` | 5k | 1m |
|-------------|----|----|
| prt         | 0.017555952072143555 | 3.732201337814331  |
| log         | 0.007807493209838867 | 2.201814651489258  |
|log (default)| 0.012686729431152344 | 1.920773983001709  |
| log (time)  | 0.01854419708251953  | 2.5776114463806152 |

### Codes

- compare.py
```shell
# coding: utf-8
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import argparse
import logging
import sys
import os
import time

logging.basicConfig(level=logging.INFO)


def testPrint(n, txt='cmpPrint.log'):
    saveout = sys.stdout
    fsock = open(txt, "w")
    sys.stdout = fsock
    #
    for i in range(n):
        print("No. ", i)
    #
    fsock.close()
    sys.stdout = saveout


def testLogger(n, txt='cmpLogger.log', formatter=None):
    logger = logging.getLogger('compare')
    logtxt = logging.FileHandler(txt)  # 'compareLogger.log')
    logtxt.setLevel(logging.DEBUG)
    if not formatter:
        logtxt.setFormatter(formatter)
    logger.addHandler(logtxt)
    #
    for i in range(n):
        logger.debug("No. {}".format(i))
    #


def deleteFiles(txt):
    if os.path.exists(txt):
        os.remove(txt)



parser = argparse.ArgumentParser()
parser.add_argument('-n', '--number', type=int,
    default=1000, help='Number of Output')
parser.add_argument('-run', '--execute', type=str,
    default="print", choices=['print', 'logger'],
    help="Print or Logger?")
parser.add_argument('-fmt', '--format', type=str,
    default='', help='Formatter in Logger')


# txt_prt = 'txtPrint.log'
# txt_log = 'txtLogger.log'

args = parser.parse_args()
n = args.number

if args.execute.startswith('p'):
    txt = 'txtPrint.log'
    deleteFiles(txt)
    testPrint(n, txt)

else:
    txt = 'txtLogger.log'
    deleteFiles(txt)

    fmt = args.format
    formatter = None
    if not fmt:
        pass
    elif fmt == 'default':
        formatter = logging.Formatter(logging.BASIC_FORMAT, None)
    elif fmt == 'time':
        formatter = logging.Formatter(
            '%(asctime)s - %(name)s:%(levelname)s | %(message)s')

    testLogger(n, txt, formatter)

```
- cprofiler.py
```shell
# coding: utf8
import argparse

import pstats
"""
p=pstats.Stats('./cProfile_output.txt')
p.print_stats()
p.sort_stats('calls').print_stats()  #    # 根据调用次数排序
p.sort_stats('cumulative').print_stats()  # 根据调用总时间排序
"""


parser = argparse.ArgumentParser()
parser.add_argument('-o', '--output', type=str,
    default='./cProfile_output.txt',
    help='Filename of Outputs')


args = parser.parse_args()
t = args.output

p = pstats.Stats(t)
p.sort_stats('tottime').print_stats()

```
- compare.py (Time Cost)
```shell
...

args = parser.parse_args()
n = args.number
# since = time.time()

if args.execute.startswith('p'):
    ...
else:
    ...

time_elapsed = time.time() - since
print("{:6s} n={} fmt={}".format(args.execute, args.number, args.format))
print("Time Cost: {} s".format(time_elapsed))
```


# TensorFlow Debug

## tf.logging

```python
import logging

# http://landcareweb.com/questions/26327/ru-he-jiang-tensorflowri-zhi-ji-lu-zhong-ding-xiang-dao-wen-jian
# get TF logger
log = logging.getLogger('tensorflow')
log.setLevel(logging.DEBUG)
# create formatter and add it to the handlers
#formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
# create file handler which logs even debug messages
fh = logging.FileHandler('tensorflow.log')
fh.setLevel(logging.DEBUG)
#fh.setFormatter(formatter)
log.addHandler(fh)
```

## TensorBoard

Same Terminal, Different Machines
```shell
# Local
$ ssh -L 16006:127.0.0.1:6006 yourname@server.address

# Server
$ cd expected-folder-path
$ tensorboard --logdir=./network

$ # Open http://127.0.0.1:16006 in Local browser
$ # Ctrl+C close on the same Terminal
```

# PyTorch Debug
ref: [点赞收藏：PyTorch常用代码段整理合集](https://yq.aliyun.com/articles/716950?spm=a2c4e.11153959.teamlist.33.4bd85a18ZHZchy)


# \* References

[Github 中 Markdown 锚点链接如何写](https://my.oschina.net/antsky/blog/1475173)  
