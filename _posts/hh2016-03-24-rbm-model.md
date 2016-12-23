---
layout: post
title:  "RBM 模型的理解与分析"
date:   2016-03-24 21:00:35
categories: DeepLearning
excerpt: RBM 模型的简单理解
---

### RBM, Restricted Boltzmann Machines

&emsp;RBM, 受限波尔兹曼机， 是一种能量模型， 可以用于深度神经网络模型的预训练， 也可以用作高维数据的降维。  

#### 1. RBM的网络结构  

&emsp;RBM是一种特殊形式的log-linear马尔可夫随机场
其网络结构如下图所示：  
<p align ="center"><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/RBM_zpsygtmw2by.png" heighzgt="200" width="400"></p>
$emsp; 由图可知，RBM分为可见层(visible layer) 和隐藏层(hidden layer)，隐藏层可以看成是可见层的编码， 因此可以用RBM对数据进行降维。另外，还可以利用RBM对 BP网络的参数权重进行预训练，直接对BP网络进行训练容易得到网络的局部最优解，而用RBM训练所得的参数权重作为BP网络的初始值，再进行调偕训练可以得到更好的结果。作为一种能量模型，其能量函数 E(v,h) 如下所示：  



