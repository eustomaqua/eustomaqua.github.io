---
title: 卷积神经网络中的卷积和池化操作
date:    2018-04-22 16:03:49
updated: 2018-07-7 18:43:51
categories:
  - Deep Learning
tags:
  - CNN
  - TensorFlow
---

[comment]: <> (updated: 2018-04-22 22:23:23)
[comment]: <> (updated: 2018-04-22 21:16:32)
[comment]: <> (updated: 2018-04-22 16:04:09)
[comment]: <> (updated: 2018-04-23 15:32:31)


# What is CNNs?

卷积神经网络（ Convolutional Neural Networks, CNNs/ConvNets ），是神经网络的一种。

整个网络仍然表示一个单独的可微分的得分函数：从原始图像像素到类别。
最后的（全连接）层也仍然存在一个损失函数（如：SVM/Softmax）。

不同点在于：ConvNet 结构做出了显式的假设，即输入为图片。
这个假设允许我们把确定的性质编码进网络结构中。
而卷积网络的结构也使得前馈函数能够更加有效地实现，并大量地缩减了网络中所需要的参数。


# How to use it in TF?

## tf.nn.conv2d
> tf.nn.conv2d(input, filter, strides, padding, use_cudnn_on_gpu=None, data_format=None, name=None)

params:
- **input** :  [batch, in_height, in_width, in_channels]
- **filter**  :  [filter_height, filter_width, in_channels, out_channels]
- **strides** :  [1, stride_height, stride_width, 1]
- **padding** :  'SAME', 'VALID'
- data_format :  'NHWC', 'NCHW'

return:  
- [batch, out_height, out_width, out_channels]  

(1) if padding='SAME',  
out_height = ceil(in_height / stride_height)  
out_width  = ceil(in_width / stride_width)  
(2) if padding='VALID',  
out_height = ceil((in_height - filter_height + 1) / stride_height)  
out_width = ceil((in_width - filter_width + 1) / stride_width)

## tf.nn.max_pool, tf.nn.avg_pool
> **tf.nn.max_pool**(value, ksize, strides, padding, data_format='NHWC', name=None)  
> **tf.nn.avg_pool**(value, ksize, strides, padding, data_format='NHWC', name=None)  

params:
- **value** :  [batch, in_height, in_width, in_channels]
- **ksize** :   [1, ksize_height, ksize_widht, 1]
- **strides** :  [1, stride_height, stride_width, 1]
- **padding** :  'SAME', 'VALID'
- data_format :  'NHWC', 'NCHW'

return:
- [batch, out_height, out_width, in_channels]

(1) if padding='SAME',  
out_height = ceil(in_height / stride_height)  
out_width  = ceil(in_width  / stride_width )  
(2) if padding='VALID',  
out_height = ceil((in_height - ksize_height + 1) / stride_height)  
out_width  = ceil((in_width  - ksize_width  + 1) / stride_width )

## Same Params
[comment]: <> (Params in common)

- strides 代表切边移动的步长，4 个方向；而 padding 是切片是否可以越过边缘，有两种方式，SAME 为越过，VALID 为不越过，它的意义是决定切片中心是否经过图的边缘。

- data_format 表示输入数据的格式，需要跟输入数据的格式保持一致。有 'NHWC' 和 'NCHW' 两种，默认是 'NHWC' ，即 [batch, in_height, in_width, in_channels]
- padding 表示是否填充。有两个格式。  
    + 'SAME'  得到的输出特征图，跟输入特征图**相同**  
    + 'VALID' 得到的输出特征图，跟输入特征图**不相同**


# More details about CNNs...

## tf.nn.conv2d
> **tf.nn.conv2d(input, filter, strides, padding, use_cudnn_on_gpu=None, data_format=None, name=None)**  

五个**参数**：
1. input ，指需要做卷积的输入图像，是一个 4 维 tensor ，要求类型为 float32 或 float64 其中之一。  
  其 shape= [batch, in_height, in_width, in_channels]，具体含义是 [训练时一个 batch 的图片数量, 图片高度, 图片宽度, 图像通道数]  
2. filter ，相当于 CNN 中的卷积核，要求类型与参数 input 相同。  
  注意第三维 in_channels ，就是参数 input 的第四维。  
  其 shape= [filter_height, filter_width, in_channels, out_channels] ，具体含义是 [卷积核的高度, 卷积核的宽度, 图像通道数, 卷积核个数]  
3. strides ，卷积时在图像每一维的步长，这是一个一维的向量，长度为 4.  
  strides.shape = [1, stride_height, stride_width, 1]  
  注：必须有 strides[0]=strides[3]=1. 绝大多数情况下，水平的 stride 和竖直的 stride 一样，即 strides = [1, stride, stride, 1]。
4. padding ，是一个 string 类型的量，只能是 'SAME', 'VALID' 其中之一，这个值决定了不同的卷积方式
5. use_cudnn_on_gpu ，bool 类型，是否使用 cudnn 加速，默认为 true 

**返回**：  
  一个 tensor ，这个输出就是我们常说的 feature map 。

**计算过程**：  
1. 展平 filter 成如下 2-D matrix ，其 shape= [filter_height * filter_width * in_channels, out_channels]  
2. 从 input tensor 中提取 patches 构成一个 virtual tensor ，其 shape= [batch, out_height, out_width, filter_height * filter_width * in_channels]  
3. 对于每一个 patch ，右乘上 (1) 中的 filter matrix 。即 [batch, out_height, out_width, filter_height * filter_width * in_channels] x [filter_height * filter_width * in_channels, out_channels] ，其结果的 shape 就是 [batch, out_height, out_width, out_channels]  
4. 输出结果的 shape 计算 （ceil 表示向上取整）   
    - padding = 'SAME'  
      out_height = ceil( in_height / stride_height )  
      out_width  = ceil( in_width / stride_width )  
    - padding = 'VALID'  
      out_height = ceil( (in_height - filter_height + 1) / stride_height )  
      out_width  = ceil( (in_width - filter_width + 1) / stride_width )  


## tf.nn.max_pool, tf.nn.avg_pool
> **tf.nn.max_pool**(value, ksize, strides, padding, data_format='NHWC', name=None)  
> **tf.nn.avg_pool**(value, ksize, strides, padding, data_format='NHWC', name=None)  

四个**参数**：  
1. value ，需要池化的输入。一般池化层接在卷积层后面，所以输入通常是 feature map ，依然是 [batch, in_height, in_width, in_channels] 这样形式的 shape   
2. ksize ，池化窗口的大小，取一个四维向量，一般是 [1, height, width, 1] 。因为我们不想在 batch 和 channels 上做池化，所以这两个维度设为 1   
3. strides ，和卷积类似，窗口在每一维度上滑动的步长，一般也是 [1, stride, stride, 1]   
4. padding ，和卷积类似，可以取 'VALID' 或 'SAME'   

**返回**：   
 一个 tensor ，类型不变，shape 仍为 [batch, height, width, channels] 的形式


# References

1. conv2d, pool in TensorFlow  

2. Convolutional Neural Networks, CNNs/ConvNets   
  [CS231n Convolutional Neural Networks for Visual Recognition](http://cs231n.github.io/convolutional-networks/)  
  [深度学习笔记整理系列之七](https://blog.csdn.net/zouxy09/article/details/8781543)  
  [CNN 笔记：通俗理解卷积神经网络](https://blog.csdn.net/v_july_v/article/details/51812459)  
