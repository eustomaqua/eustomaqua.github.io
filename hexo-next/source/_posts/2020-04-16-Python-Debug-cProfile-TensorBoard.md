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

## logging v.s. print

<!--Efficiency-->
e.g., Table: Comparison of Time (min) where 
$$Percent = \left(1 - \frac{Time_{\;logger}}{Time_{\;print}} \right)\times 100\%$$

| Example | print | logger | Percent (%) |
|---------|-------|--------|-------------|
| mnist,dnn,b | 192.2485 | 62.3390 | 67.57 |
| mnist,dnn,c | 344.0925 | 77.7800 | 77.40 |
| mnist,dnn,e | 698.8540 | 80.7567 | 88.44 |



# TensorFlow Debug

## tf.logging

## TensorBoard

# PyTorch Debug


# \* References

[Github 中 Markdown 锚点链接如何写](https://my.oschina.net/antsky/blog/1475173)  
