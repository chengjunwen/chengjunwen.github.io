---
layout: post
title:  "Ubuntu库路径和环境变量设置"
date:   2016-01-23 20:42:05
categories: ubuntu
excerpt: 不同的Ubuntu版本，安装caffe时要安装的库不同
---

## 库路径添加

在`/etc/ld.so.conf`文件中添加库的绝对路径，或者在`/etc/ld.so.conf.d/`目录下新建一个`.conf`文件，并在该文件中写入库的绝对路径，如: 

> /usr/lib 
> /usr/local/hdf5/lib 

然后执行 `sudo ldconfig`, ldconfig的作用是将`/etc/ld.so.conf`列出的路径下的所有库文件缓存到`/etc/ld.so.cache`中，才能使用。

## 环境变量设置
	
环境变量设置分为系统环境变量设置和用户环境变量设置，

### 系统环境变量设置
所有用户都可以使用，一般在存储下列文件中：

* /etc/environment 
* /etc/profile 
* /etc/bash.bashrc 

添加系统环境变量则在着几个文件之一中添加相应的环境变量路径，如写入: 

	export PATH=$PATH:/opt/intel/composer_xe_2013/bin

然后执行 `source /etc/profile` 生效

### 用户环境变量设置
当前用户才可以使用， 一般存储在一下文件中：

* ～/.bashrc
* ~/.bash_profile
* ~/.profile

加入环境变量的方式与系统环境变量相同，在上述文件之一中写入即可。
