---
layout: post
title:  "convolution和deconvolution"
date:   2016-12-22 17:01:57 +0800
categories:	DeepLearning
excerpt:
---

### 卷积

&emsp;首先简单的介绍一下卷积的定义，如下图，f 和 g 卷积， 相当于把 g 翻转之后沿着 x 轴滑动来累计两函数的积分值。如下图所示：
![convolution](/images/conv/Convolution.png)

### 图像卷积(convolution)的三种形式

大家看CNN(卷积网络)时肯定有注意到有个参数padding可以设置成 full , same, valid三种，不同参数的卷积形式略有不同。  

1. full卷积  
&emsp;full卷积很像上述所提到的卷积， iamge(A)和kernel filter(B)卷积（A\*B），就是把B翻转然后滑动累积和A的积分指。由于A是图片，这样就意味着要对A进行padding，卷积计算从B和A的最边缘有交集就开始计算，所以也叫 full convolution。full conv之后图片的大小会比 A图大。如下图所示(盗图，懒得画图了).  
	![/images/conv/full.png)
    
2. same 卷积  
&emsp;将图 A 和 B 进行 same 卷积，卷积之后 A 图的大小不变，所以就叫 same 卷积。s卷积计算的起始点是从 B 图的中心和 A 图有交集开始，same 卷积如下图所示，所以 same 卷积也会对 A 图进行padding。  
    ![/images/conv/same.png)

3. valid 卷积  
&emsp;valid 卷积不需要对图 A 进行padding， 也就是大家平常看CNN 网络讲解图时常用的卷积形式，卷积计算从 B 被 A 完全交集开始计算， 如下图所示：  
    ![/images/conv/valid.png)

%emsp;关于 三种卷积对于输出map大小的影响，假设 输入 iamge 大小是 N\*N ,kernel filter大小是 M\*M,卷积时步长为s，如果padding的长度是p，则卷积之后map大小是 [ (N-M+2\*p)/s +1 ] \* [ (N-M+2\*p)/s +1 ]，这个公式可以套到下面三种卷积里面。  

* valid 卷积，步长为1 时，输出大小 (N-M +1) \* (N-M +1)  
* same 卷积，步长为1 时， 输出map大小 N \* N。pad的长度是 (M-1)/2, M 一般是奇数。  
* full 卷积，步长为1 时， 输出map大小 (N+M-1) \* (N+M-1)。pad的长度是 M-1  

### 图像反卷积 ,deconvolution
	
&emsp;其实关于图像的反卷积并不是真正意义上的反卷积，用反卷积命名是错误的，成为 转置卷积（transposed convolution ）更为准确。反卷积可以让输出图比输入图大，CNN网络用反卷积通常是为了重构出原图的大小(经过conv之后图片一般会变小)，这个在 full CNN 里面就用来重构出原图的大小，从而进行pixel 级别的语义分割。反卷积有两种形式，   

1. 上面提到的 full convolution 其实就是一种反卷积，如果步长为一，如下图所示，蓝色部分是原图 2\*2， 白色部分是 padding的：  

	![deconv1](/images/conv/YyCu2.gif)
2. 还有一种，并不是直接在原图四周padding，而是一种插入时的padding，如下，蓝色部分是原图 2\*2， 白色部分是 padding的:  

	![deconv2](/images/conv/f2RiP.gif)

