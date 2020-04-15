---
title: Logging in Python (日志处理)
date: 2018-09-18 16:26:21
updated: 2018-09-18 16:26:21
categories:
  - Programming
tags:
  - Commands
  - Python
  - Notes
---

[comment]: <> (title: Python 之日志处理 —— Logging;  tags: Python)



[Python日志功能详解](https://blog.igevin.info/posts/python-log/)  
[Python中的logging模块](http://python.jobbole.com/86887/)


# Why: 为什么要使用 logging?

代码调试时常使用 print 函数输出一些中间变量的值或者相关信息，这样虽然简便，但是在程序调试完之后需要逐个删除或注释 print 语句，比较麻烦。  
logging 模块能很好地解决这个问题，通过设置 severity level，容易控制在控制台打印的信息，也可以同时把日志信息输出到多个目的地，如控制台、日志文件、网络位置等。  

# How: 怎么使用 logging?

## 日志基本用法

### 默认

```Python
#!/usr/local/bin/python
# -*- coding: utf-8 -*-

import logging

logging.debug('debug message')
logging.info('info message')
logging.warn('warn message')
#or logging.warning('warn message')
logging.error('error message')
logging.critical('critical message')
# 注意：debug, info 不会输出结果
```

默认情况下，日志将会被打印到屏幕上，日志级别为 WARNING (即只有日志级别等于或高于 WARNING 的日志信息才会输出)，日志格式为 *warning level:instance name:warning message*

### 记录到文件

```python
import logging

# 配置日志文件和日志级别
logging.basicConfig(filename='logger.log', level=logging.INFO)

logging.debug('debug message')
...
```

需要注意的是，配置应在代码文件开头设置，否则不会改变初始的设置 (即代码文件开头的原始设置)。

## 完善日志功能

想要更灵活地使用日志模块，就要了解它是如何工作的。  
Logger, Handler, Formatter 和 Filter 是日志模块的几个基本概念，其工作原理也要从这四个基本概念说起。  

- Logger 记录器，提供日志相关功能的调用接口
- Handler 处理器，将 (记录器产生的) 日志记录发送至合适的目的地。
- Filter 过滤器，提供更好的粒度控制，可决定输出哪些日志记录。
- Formatter 格式化器，指明最终输出中日志记录的格式

### 基本概念
#### Logger
Logger 记录器，其对象实例是日志记录功能的载体，如 

```python
import logging

logger = logging.getLogger('simple_example_name')

logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')
```

注意：Logger 对象从不直接实例化，而是通过模块级的功能 *logging.getLogger(name)* 来创建 Logger 实例。调用 *logging.getLogger(name)* 功能时，如果传入的 name 参数值相同，则总是返回同一个 Logger 对象实例的引用。

如果没有显式进行创建，则默认创建一个 root logger，并应用默认的日志级别 (WARN)、默认的处理器 Handler (StreamHandler, 即将日志信息打印输出到标准输出上)、和默认的格式化器 Formatter (默认的格式即为第一个简单使用程序中输出的格式，即 *warning level:instance name:warning message*)

#### Handler

Handler 将日志信息发送到设定位置，可通过 Logger 对象的 *addHandler()* 方法为 Logger 对象添加 0 或多个 handler。日志的一种典型应用场景是：系统希望将所有的日志信息保存到 log 文件中，其中日志等级等于或高于 ERROR 的消息还要在屏幕标准输出上显示，日志等级为 CRITICAL 的还需要发送邮件通知；这种场景就需要 3 个独立的 handler 来实现需求，分别与指定的日志等级或日志位置做响应。

注意：为 Logger 配置的 handler 不能是 Handler 基类对象，而是 Handler 的子类对象。常用的 Handler 有 StreamHandler, FileHandler, 和 NullHandler。

#### Formatter

Formatter 用于设置日志输出的格式，与 Logger/Handler 不同，它可以直接初始化对象，即 *formatter=logging.Formatter(fmt=None, datefmt=None)*。创建时分别传入两个参数来修改日志格式和时间格式，默认的日志格式为 *%(asctime)s - %(levelname)s - %(message)s*, 默认的时间格式为 *%Y-%m-%d %H:%M:%S*.

#### Filter

Filter 可用于 Logger 对象或 Handler 对象，用于提供比日志等级更加复杂的日志过滤方式。默认的 filter 只允许在指定 logger 层级下的日志消息通过过滤。  
举个栗子，若把 filter 设置为 *filter=logging.Filter('A.B')*, 则 logger 'A.B', 'A.B.C', 'A.B.C.D', 'A.B.D' 产生的日志信息可以通过过滤，但 'A.BB', 'B.A.B' 均不行。若以空字符串初始化 filter ，则所有的日志消息都可以通过过滤。  
Filter 在日志功能配置中是非必须的，只在对日志消息过滤需求比较复杂时配置使用即可。

### 日志产生流程

日志产生的流程逻辑参考图  
<img src="/images/2018-09/logging_flow.png" alt="avatar" height="95%" width="95%">

### 日志模块的使用

日志模块使用的关键是“日志的配置”。配置好之后，只需调用 logger.INFO(), logger.ERROR() 等方法即可创建日志内容。

配置日志模块有三种方法：  
1. 在代码中显式创建 loggers, handlers, formatters 甚至 filters，并调用这几个对象中的各个配置函数来完成日志配置  
2. 将配置信息写到配置文件中，然后读取配置文件信息来完成日志配置  
3. 将配置信息写到一个字典 dict 中，然后读取这个配置字典来完成日志配置

#### 代码配置和使用

通过代码配置日志模块胜在方便简单，但不推荐在大型项目中使用，因为修改配置就需要修改代码。  
这种方法可帮助我们理解日志模块的工作原理，因此用作案例。  

```python
import logging

## 创建 Logger
# Create logger
logger = logging.getLogger('test')
# Set default log level
logger.setLevel(logging.DEBUG)

## 创建 Handler
# Create console handler and set level to warn
ch = logging.StreamHandler()
ch.setLevel(logging.WARN)

## 创建 Formatter
# Create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

## 配置 Logger
# add formatter to ch
ch.setFormatter(formatter)
# add ch to logger
logger.addHandler(ch)
# The final log level is the higher one between the default and the one in handler

## 使用日志模块
logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')

## >>> logger.debug('debug')
## >>> logger.warn('warn')
## 2018-09-18 04:40:21,474 - test - WARNING - warn
## >>> logger.critical('critical message')
## 2018-09-18 04:42:01,788 - test - CRITICAL - critical message
## >>> 

ch2 = logging.FileHandler('logger.log')
ch2.setLevel(logging.INFO)
ch2.setFormatter(formatter)
logger.addHandler(ch2)
# 'application' code
```

这个 logger.log 文件的写入是追加的，不是重新写入的形式。如这个例子中， logger.log 的文件内容是 (前三行是之前的测试内容):  
```python
INFO:root:info
ERROR:root:error
WARNING:root:warn
2018-09-18 04:44:33,129 - test - INFO - info message
```

#### 文件配置和使用

通过配置文件配置日志模块时，配置文件通常使用 *.ini* 格式，日志模块需要调用 *fileConfig* ，即 *logging.config.fileConfig('logging_config.ini')* ，然后 logger 的使用方法同上。 

```python
import logging
import logging.config

logging.config.fileConfig('logging_config.ini')

# create logger
logger = logging.getLogger('root')

# 'application' code
logger.debug('....')
```

其中，*logging_config.ini* 文件内容为 

```vim
[loggers]
keys=root,simpleExample

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_simpleExample]
level=INFO
handlers=consoleHandler
qualname=simpleExample
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[formatter_simpleFormatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
```

通过配置文件配置日志模块，逻辑与代码中的配置一样，也是把 logger, handler 和 formatter 定义好，然后组装到一起。只是 ini 配置与代码配置的语法不通，可参考上例做相应修改。

#### 字典配置和使用

基于 Dict 对象配置日志模块在 Python 中应用广泛，很多 Django 或 Flask 项目都采用这种方式。以下是一个使用样例，可参考用于修改。

```python
import logging
import logging.config

config = {
  'version': 1,
  'formatters': {
    'simple': {
      'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s', 
    },
  },
  'handlers': {
    'console': {
      'class': 'logging.StreamHandler',
      'level': 'DEBUG',
      'formatter': 'simple'
    },
    'file': {
      'class': 'logging.FileHandler',
      'filename': 'logging.log',
      'level': 'DEBUG',
      'formatter': 'simple'
    },
  },
  'loggers': {
    'root': {
      'handlers': ['console'],
      'level': 'DEBUG',
      # 'propagate': True,
    },
    'simple': {
      'handlers': ['console', 'file'],
      'level': 'WARN',
    }
  }
}

logging.config.dictConfig(config)

print 'logger:'
logger = logging.getLogger('root')

logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')

print 'logger2:'
logger2 = logging.getLogger('simple')

logger2.debug('debug message updated')
logger2.info('info message updated')
logger2.warn('warn message updated')
logger2.error('error message updated')
logger2.critical('critical message updated')
```

### *日志的严重等级

Log Level 如下，
```vim
CRITICAL: 50
ERROR: 40
WARNING: 30
INFO: 20
DEBUG: 10
NOTSET: 0
```

等级包括 NOTSET, DEBUG, INFO, WARNING, ERROR, CRITICAL, 严重程度依次递增。


# Which: 查阅

## 示例

```python
# -*- coding: utf-8 -*-
import logging
import sys

# 获取logger实例，如果参数为空则返回root logger
logger = logging.getLogger("AppName")

# 指定logger输出格式
formatter = logging.Formatter('%(asctime)s %(levelname)-8s%: %(message)s')

# 文件日志
file_handler = logging.FileHandler("test.log")
file_handler.setFormatter(formatter)  # 可以通过setFormatter指定输出格式

# 控制台日志
console_handler = logging.StreamHandler(sys.stdout)
console_handler.formatter = formatter  # 也可以直接给formatter赋值

# 为logger添加的日志处理器
logger.addHandler(file_handler)
logger.addHandler(console_handler)

# 指定日志的最低输出级别，默认为WARN级别
logger.setLevel(logging.INFO)

# 输出不同级别的log
logger.debug('this is debug info')
logger.info('this is information')
logger.warn('this is warning message')
logger.error('this is error message')
logger.fatal('this is fatal message, it is same as logger.critical')
logger.critical('this is critical message')

# 移除一些日志处理器
logger.removeHandler(file_handler)
```

## 格式化输出日志

```python
# 格式化输出

service_name = "Booking"
logger.error('%s service is down!' % service_name) 			  #使用Python自带的字符串格式化，不推荐
logger.error('%s service is down!', service_name) 			  #使用logger的格式化，推荐
logger.error('%s service is %s!', service_name, 'down') 	  #多参数格式化
logger.error('{} service is {}'.format(service_name, 'down')) #使用format函数，推荐

# 2018-09-18 21:11:34,493 ERROR   : Booking service is down!
```

## 记录异常信息

当使用logging模块记录异常信息时，不需要传入该异常对象，直接调用 logger.error() 或 logger.exception() 就可以将当前异常记录下来。

```python
# 记录异常信息

try:
  1 / 0
except:
  # 等同于error级别，但是会额外记录当前抛出的异常堆栈信息
  logger.exception('this is an exception message')

# 2016-10-08 21:59:19,493 ERROR   : this is an exception message
# Traceback (most recent call last):
#   File "D:/Git/py_labs/demo/use_logging.py", line 45, in 
#     1 / 0
# ZeroDivisionError: integer division or modulo by zero
```

<!-- <table border="1">
  <tr>
    <th> Value   </th><th> Meaning </th>
  </tr>
  <tr><td> %(name)s            </td><td> Logger 的名字 </td></tr>
  <tr><td> %(levelno)s         </td><td> 数字形式的日志级别 </td>
  </tr>
  <tr><td> %(levelname)s       </td><td> 文本形式的日志级别 </td>
  </tr>
  <tr><td> %(message)s         </td><td> 用户输出的消息 </td>
  </tr>
  <tr>
    <td> %(created)f         </td><td> 当前时间，用 UNIX 标准的表示时间的浮点数表示 </td>
  </tr>
  <tr>
    <td> %(relativeCreated)d </td><td> 输出日志信息时的，自 Logger 创建以来的毫秒数 </td>
  </tr>
  <tr>
    <td> %(asctime)s         </td>
    <td> 字符串形式的当前时间。默认格式是 "2003-07-08 16:49:45,896"。逗号后面的是毫秒 </td>
  </tr>
  <tr>
    <td> %(pathname)s        </td><td> 调用日志输出函数的模块的完整路径名，可能没有 </td>
  </tr>
  <tr><td> %(filename)s        </td><td> 调用日志输出函数的模块的文件名 </td></tr>
  <tr>
    <td> %(module)s          </td><td> 调用日志输出函数的模块名，filename 的名字部分 </td>
  </tr>
  <tr><td> %(funcName)s        </td><td> 调用日志输出函数的函数名 </td></tr>
  <tr><td> %(lineno)d          </td><td> 调用日志输出函数的语句所在代码行 </td></tr>
  <tr><td> %(thread)d          </td><td> 线程 ID ，可能没有 </td></tr>
  <tr><td> %(threadName)s      </td><td> 线程名，可能没有 </td></tr>
  <tr><td> %(process)d         </td><td> 进程 ID ，可能没有 </td></tr>
  <tr><td> %(processName)s     </td><td> 进程名，可能没有 </td></tr>
</table>
-->

## 修改日志消息的格式

**Formatter 日志格式**  
Formatter 对象定义了 log 信息的结构和内容，构造时需要带两个参数：  
- 一个是格式化的模板 fmt ，默认会包含最基本的 level 和 message 信息  
- 一个是格式化的时间样式 datefmt ，默认为 2003-07-08 16:49:45,896 (%Y-%m-%d %H:%M:%S)

fmt 中允许使用的变量可参考下表  

| Value               | Meaning                                  |
| ------------------- | ---------------------------------------- |
| %(name)s            | Logger 的名字                               |
| %(levelno)s         | 数字形式的日志级别                                |
| %(levelname)s       | 文本形式的日志级别                                |
| %(message)s         | 用户输出的消息                                  |
| %(created)f         | 当前时间，用 UNIX 标准的表示时间的浮点数表示                |
| %(relativeCreated)d | 输出日志信息时的，自 Logger 创建以来的毫秒数               |
| %(asctime)s         | 字符串形式的当前时间。默认格式是 "2003-07-08 16:49:45,896"。逗号后面的是毫秒 |
| %(pathname)s        | 调用日志输出函数的模块的完整路径名，可能没有                   |
| %(filename)s        | 调用日志输出函数的模块的文件名                          |
| %(module)s          | 调用日志输出函数的模块名，filename 的名字部分              |
| %(funcName)s        | 调用日志输出函数的函数名                             |
| %(lineno)d          | 调用日志输出函数的语句所在代码行                         |
| %(thread)d          | 线程 ID ，可能没有                              |
| %(threadName)s      | 线程名，可能没有                                 |
| %(process)d         | 进程 ID ，可能没有                              |
| %(processName)s     | 进程名，可能没有                                 |


## 跌过的坑不要再爬一遍

logging 全局设一个就够了，否则会重复输出

使用同名 logger 会拿到同一实例，这样可以实现跨模块调用同样的 logger 来记录日志；另外也可以通过日志名称来区分同一程序的不同模块。


# 参考链接

[logging - Logging facility for Python](https://docs.python.org/2/library/logging.html#logrecord-attributes)  
[time.strftime(format[, t])](https://docs.python.org/2/library/time.html#time.strftime)    
[Python 中 Logging 模块使用方法](http://zhangzhk.com/2018/01/13/python-logging-module/)  
[Python日志输出——logging模块](https://blog.csdn.net/chosen0ne/article/details/7319306)  
[Python之日志处理(logging模块)](https://www.cnblogs.com/yyds/p/6901864.html)  
[Python logging 模块使用指南](http://www.codebelief.com/article/2017/05/python-logging-module-tutorial/)  

# \* Example

目标场景：比如说两个模块，在其中一个模块中引用另外一个模块，并存在某一日志文件中

- test.py
  ```python
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import logging
logging.basicConfig(level=logging.INFO)

import os
if os.path.exists('logger.log'):
    os.remove('logger.log')

logger = logging.getLogger('youruser')
ch2 = logging.FileHandler('logger.log')
ch2.setLevel(logging.NOTSET)
formatter = logging.Formatter('%(asctime)s %(name)s/%(levelname)s: %(message)s')
# formatter = logging.Formatter('%(created)f - %(name)s - %(levelno)s - %(message)s')
# formatter = logging.Formatter('%(relativeCreated)s - %(module)s/%(funcName)s | %(message)s')
ch2.setFormatter(formatter)
logger.addHandler(ch2)
logger.info('')
logger.info('2\n')
logger.info('\n3')
logger.info('\t4')
logger.warning('hello')
logger.warn('world')
logger.warn('main Test {}'.format(4))

from testa import funcA
funcA(logger)
  ```
- testa.py
  ```python
# import logging

def funcA(logger):
    logger.warn('Test A')
  ```

- print `logger.log`
  ```txt
2020-04-15 04:53:45,247 youruser/INFO: 
2020-04-15 04:53:45,247 youruser/INFO: 2

2020-04-15 04:53:45,248 youruser/INFO: 
3
2020-04-15 04:53:45,248 youruser/INFO:  4
2020-04-15 04:53:45,248 youruser/WARNING: hello
2020-04-15 04:53:45,248 youruser/WARNING: world
2020-04-15 04:53:45,249 youruser/WARNING: main Test 4
2020-04-15 04:53:45,250 youruser/WARNING: Test A

  ```
