---
layout: post
title:  "程序编译,链接"
date:   2016-12-28 12:31:16 +0800
categories: ComputerSystem
excerpt:
---

###  简介

&emsp; 一般我们写的编程语言 eg. C\+\+ ,C 等都是高级编程语言，并不能倍机器直接认识，高级语言需要先转换成低级的机器语言指令，才能被机器执行。将这些指令打包到一个 executable object program里面，这个executable object program 就是我们常说的可执行文件 executable object file。  
&emsp;关于 GNU , GNU 是一种编译工具，支持的语言有 C，C\+\+ ，java ，fortran，pascal object-C，Ada等。  

### 编译过程

以helloword为例子， hello.c:

	#include <stdio.h>
	int main()
	{
		printf( 11 hello, world\n 11 ) ;
		return O;
	}
    
&emsp;在linux系统上，把一个源文件(hello.c) 转换成 可执行文件(hello)需要四个步骤:

1. 预处理 ，preprocessing   
 	预处理是处理 ‘#’开头的代码行，例如 #include <stdio.h> ,预处理器会读取系统头文件 stdio.h里面的全部文件 并插入到hello.c里,这一步生成的文件还是文本的 program，后缀  .i 。    

```
    	gcc -E hello.c -o test.i
```        

2. 编译 ， compilation   
	编译是指将文本的程序代码(hello.i)编译成汇编语言的程序代码(hello.s)。hello.s也是text file.汇编语言以一种人能理解的方式描述了机器语言指令。对于不同的编译器和不同的语言， 汇编语言提供了一种通用的语言模式。  

```
    	gcc -S hello.i -o test.s
```

```
	main:
		sub'q 	$8, %rsp
		movl 	$.LCO, %edi
		call	puts
		movl 	$0, %eax
    	addq	$8, %rsp
		ret 
```

3. 汇编， assembly   
	汇编将汇编语言(hello.s)转换成机器语言指令，并打包成可重定位的目标代码(relocatable object program)，存储成二进制的目标文件(hello.o)  

```
   gcc -c hello.s -o test.o     
```

4. 链接， linking  
	链接是将 程序的目标文件和其他所需的目标文件链接起来生成最后的可执行文件。  
    关于其他所需的目标文件， 可能是调用的自己项目里的其他目标文件，也可能是调用的第三方库文件，以及系统库文件。例如helloword里用到的printf函数，其实现方法是在一个printf.o 的目标文件里， 链接需要将 hello.o 和 printf.o 链接起来生成 可执行文件(hello) 。  

```
    gcc hello.o  -o hello
```

#### 静态库(.a) 和 动态库(.so)

##### 1. 静态库：  

* 在程序编译的时加载到程序里，所以程序运行时删掉.a文件也可以运行。  
* 编译时需要指定库文件路径(通过-L参数传递)，也要指定库名(-l)，  
	eg，Makefile里通常用LDFLAGS指定库路径，LIBS指定库名：  
	
    	LDFLAGS=-L/usr/lib -L/path/to/your/lib
    	LIBS = -lpthread -liconv
  关于编译过程，假设libhello.a和main.c在一个目录下：  
		gcc -c main.c
		gcc -o hello main.o libhello.a
    	//gcc -o hello main.o -L. -lhello  //可替代上句
		//gcc -o hello main.c -L. -lhello  //可替代一二句
  编译时，非系统库不能放在main文件之前，否则会报错未定义。  
  
##### 2. 动态库

* 在程序运行时才加载到程序中，所以运行时也需要库文件的存在
* 编译时，和静态库一样，需要指定动态库库路径和库名

静态库函数改变后，调用静态库的源码也需要重新编译
动态库函数改变后，调用动态库的源码不需要重新编译









