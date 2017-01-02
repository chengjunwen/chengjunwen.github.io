---
layout: post
title:  "汇编之Data Movement Instructions"
date:   2017-01-02 16:29:33 +0800
categories:
excerpt:
---

#### 汇编的数据类型
	
&emsp;在汇编的指令里，最常用的就是copy data 的指令，可以将汇编的所有指令汇总成 instruction classes， 每个class里的所有指令做的数据类型不同的同一种操作。比如 mov ，基于不同的数据类型，有不同的指令。首先，关于64位系统里的汇编的数据类型与C++ 对照如下：  
<p><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/ComputerSysterm/datatype_zpsho9uqdo6.png" wight="500" height="250"></p>  

#### data movement instruction

将数据从一个location(源地址) copy到另一个 location(目的地址)，称之为 move，  
1. 源地址， 可以是 immediate(常数)，register，memory  
2. 目的地址， 可以是 register， memory

不过 ，在 x86-64的系统里禁止从 memory到memory的mov。  

##### MOV

基于不同的数据类型， MOV 指令集有以下几个指令：  
<p><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/ComputerSysterm/mov_zpsgcl0nvlz.png" wight="500" height="200"></p>  

关于以上的mov指令，有一个需要注意的是 movl指令， 当目的地址是 register时，movl会register的高位的4个byte置 0 。(源数据 4个byte， register是 8个byte)。不过，对于movb，movw，即使目的地址是register，并不会将高位置 0 ，而是保留原值。举个小例子如下:  
<p><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/ComputerSysterm/movexample_zpscjkfk0ka.png" wight="400" height="150"></p>  

上图里的数据是16进制表示的，可以发现 ，对于 1-3行的mov指令，高位的字节是保留原字节的，但是第 4 行的 movl指令将高位的4 个byte置 0 了。
对于MOV指令集 ，除了以上提到的，还有两大类，MOVZ和MOVS  
1. MOVZ， 补零扩展的 MOV。  
2. MOVS， 符号位扩展的 MOV。  

##### MOVZ

关于 MOVZ的指令集如下所示，  
<p><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/ComputerSysterm/movz_zpsrlydyrss.png" wight="500" height="200"></p>  

可以发现，这个指令集里没有从 double word 到 quad word 的mov，逻辑上可以写成movzlq指令，其实是因为这个指令其实和movl一样，都是高位 4 byte为0.  

##### MOVS

MOVS 是指符号位扩展，也就是将空缺的高位补成符号位。关于 MOVS的指令集如下所示，  
<p><img src="http://i1156.photobucket.com/albums/p568/chengjunwen/ComputerSysterm/movs_zpsz0a4r9eh.png" wight="500" height="270"></p>  

和MOVZ相比，MOVS里就有 movslq指令。另外，MOVS里还有一个指令 cltq，其实这个指令并不是一个真正的mov指令， 而是对 32位的寄存器 %eax符号位拓展成 64位的寄存器 %rax，所以这个指令的源地址和目的地址分别固定为 %eax 和 %rax。这个指令的效果和 $$$ movslq \ \%eax,\%rax $$$ 相同