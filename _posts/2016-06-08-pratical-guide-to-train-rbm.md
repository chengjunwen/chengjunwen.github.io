---
layout: post
title:  "RBM训练的实用指南"
date:   2016-06-08 16:25:46 +0800
categories: DeepLearning
excerpt:
---

### RBM训练的实用指南

&emsp;这是很久以前，最初学用RBM时候看的Hinton大牛的论文，A Pratical Guide to Training Restricated Boltzmann Machines。趁现在有时间整理一下， 里面讲述了RBM训练过程中各种实用有效的训练tricks。  

#### 1. RBM简介

&emsp;这篇博客不打算具体介绍RBM的结构和推导算法，偏向于介绍训练tricks，所以这一块只会作一些简单的介绍。RBMs经常是被当作生成模型在使用,最重要的一个作用是作为DBN网络的组成部分。RBMs采用CD算法（constrastive divergence）或者PCD（persistent constrastive divergence）算法训练。  
&emsp;在网络构建和网络学习的过程中，有很多的参数都是需要大量的经验来进行抉择， 比方说权重值的初始值、隐藏层单元的数目、学习率的大小、batch size的大小以及动量的大小等等。算法方面还需要选择是二值单元还是高斯单元，网络参数更新采用什么样的算法，SGD还是Adadelta等。还有该如何监控训练过程并相应的调整参数。
&emsp;以下这些tricks，不只是RBM， 也会相应的实用于其他神经网络中。  

#### 2. 调参技巧

* batch size的大小  

&emsp;样本可以一个一个的训练，也可以批量的一个batch一个batch的训练，这个batch的size一般是10——100。batch式的训练可以提升训练速度，网络可以使用矩阵相乘，充分利用GPU的优势。为了避免学习率(lr)受batchsize的影响，一个batch计算出来的梯度最后会除以batchsize。
&emsp;如果batchsize太小，网络训练会比较慢，但如果太大，在使用SGD训练时，每一个梯度估计的权重参数的更新会变小。理想的batchsize的大小一般是数据类别class的大小。每一个batch里，每个类包含一个样本，这样可以减少从整体选取单个batch时的取样误差    

* 学习率 lr的大小  

&emsp;如果 lr 太大，会导致步长增大，梯度下降无法到达(局部)最优，算法上看是重建误差显著增加，最终导致权重参数(weight)可能explode。但如果 lr 过小， 由于小噪声的影响， 会导致训练周期过长。在网络训练的后期，可以适当的降低学习律。训练时可以先设置lr为0.01，观察cost下降情况，来适当的调整，如果cost在下降，可以逐步的增大lr， 如果cost在增加，则需要减少lr。  

* momentum

&emsp;momentum在SGD算法中可以有效的増加学习速度，一般大小设为0.9左右。这个相当于是加入了惯性的思想  
&emsp; v ← m*v − η(∂E/∂wi)  
&emsp; wi ← wi + v  
其中m既是指momentum，v 是速度   

* 2.4 weight-decay  

&emsp;weight decay是指对较大的权重参数值加以惩罚措施， 具体上是指在gradient上就加入一个多余项。最简单的惩罚措施是L2正则化，可以有效的避免过拟合，下面是L2正则化：  

&emsp;wi ← wi − η(∂E/∂wi)−ηλwi  

其中 η 是指学习率 lr, λ则是L2参数, λ的大小一般在0.01——0.00001之间。

#### 3. 监控过拟合  

&emsp;每隔几个epoch则计算一次train data 和 valid data的cost， 并比较，如果valid的cost开始比train的越来越大，则说明模型开始过拟合。过拟合一般情况，train data的错误率越来越低，而valid的责减少缓慢甚至开始不减返増。

#### 4. 网络节点单元类型

&emsp;大多数情况下，节点单元是二值的，但也可是高斯单元，即实值单元。ps，过去大多数网络的参数的权重都是实值的，现在有人开始研究二值权重的网络。


























