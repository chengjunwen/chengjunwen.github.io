---
layout: post
title:  "背包问题及其空间优化"
date:   2016-01-02 19:06:05
categories: 算法
excerpt: 动态规划。
---

### 问题描述

输入：  
有一个背包，容量大小为V，n件物品，每件物品有一下两种属性：  

* 价值 value, ![value][1]
* 大小 size， ![size](http://7xppp2.com1.z0.glb.clouddn.com/wi.gif)

输出：  
选取能放入背包中的物品的组合子集，![subset](http://7xppp2.com1.z0.glb.clouddn.com/subset.gif)，子集大小之和不超过背包容量，使得子集物品的价值之和![allvalue](http://7xppp2.com1.z0.glb.clouddn.com/allvalue.gif)最大。  


### 问题解析

在所有n件物品中选取子集，假设对于背包容量为 x 的前 i 件 物品的最优解为(![value](http://7xppp2.com1.z0.glb.clouddn.com/ui.gif),x),则前i 件物品的最优解有下面两种情况：  

1. i 不属于最优子集，则最优解为 (![value](http://7xppp2.com1.z0.glb.clouddn.com/ui_1.gif), x)  
2. i 属于子集，则最优解为 ![value](http://7xppp2.com1.z0.glb.clouddn.com/vi.gif)+(![value](http://7xppp2.com1.z0.glb.clouddn.com/ui_1.gif), x-![size](http://7xppp2.com1.z0.glb.clouddn.com/wi.gif))  

如果![size](http://7xppp2.com1.z0.glb.clouddn.com/wi.gif)>x,则只考虑第一种情况。
算法:  
对于所有可能的物品 i=1,2,3，..,n  
对于所有可能的背包容量 x=0,1,2,..,V 
首先初始化一个二维数组A表示最优解，对任意x，有A[0,x]=0， 


	for i= 1,2,..,n
    	for x=w[i],1,2,..V
	    	    A[i,x]=max{ A[i-1,x], A[i-1,x-w[i]] + v[i] }

时间和空间复杂度均是 O(nw)  

### 空间优化  
上面采用的是用二维数组，如果V很大时，数组会非常大，于是，就想到能不能减少存储，用一个一维数组就存储完呢。其实由上面的伪码里的最后一行计算式可以看出来，每一次A[i,x]都是依赖于A[i-1，x]和A[i-1，x-w[i]]的，第一维完全可以去掉,A[i-1,]就是上一轮的A[i,]，所以完全可以替换成A[x]依赖于A[x]和A[x-w[i]]，但是有个问题，计算A[i,x+1]时，要用到A[i-1,x+1-w[i]],可是这个时候A[i-1,]已经被更新为A[i]，于是想到可以将X的遍历反过来，这样计算完A[i,x],再计算A[i,x-1]时用到的是A[i-1,j-1]而不会用到A[i-1,x]。  
只需要一维数组 A， 数组大小为 V,A的所有元素初始化为0

	for i= 1,2,..,n
		for x=V,V-1,..,w[i]
			A[x]=max{ A[x], A[x-w[i]] + v[i] }

### 背包完全装满

这种情况下，初始化时，只有A[0]=0，是恰好装满，A[i],i=1,2..V初始化为 -inf表示没有合法解。  
其他计算过程就与上面的一样。  
[1]: http://7xppp2.com1.z0.glb.clouddn.com/vi.gif
[2]: http://7xppp2.com1.z0.glb.clouddn.com/wi.gif
[3]: http://7xppp2.com1.z0.glb.clouddn.com/subset.gif
[4]: http://7xppp2.com1.z0.glb.clouddn.com/allvalue.gif
