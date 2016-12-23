---
layout: post
title:  "在Ubuntu14.04或者12.04安装caffe"
date:   2016-01-01 22:42:05
categories: DeepLearning
excerpt: 不同的Ubuntu版本，安装caffe时要安装的库不同
---

## 安装准备

* cuda 版本6.0以上
* BLAS via ATLAS, MKL, or OpenBLAS
* Boost >= 1.55
* protobuf, glog, gflags, hdf5
* Camke 版本 >= 2.8.7,（最好是更加新的版本）

### 1. 依赖库安装

#### 1.1 通用 ：

	sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler  
	sudo apt-get install --no-install-recommends libboost-all-dev  

#### 1.2 14.04版本需要：

>sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev  

#### 1.3 12.04版本需要：

glog安装:  

>wget https://google-glog.googlecode.com/files/glog-0.3.3.tar.gz  
>tar zxvf glog-0.3.3.tar.gz  
>cd glog-0.3.3  
>./configure  
>make && make install  

gflags安装:  

>wget https://github.com/schuhschuh/gflags/archive/master.zip  
unzip master.zip  
cd gflags-master  
mkdir build && cd build  
export CXXFLAGS="-fPIC" && cmake .. && make VERBOSE=1  
make && make install  

lmdb库:  

>git clone https://github.com/LMDB/lmdb  
cd lmdb/libraries/liblmdb  
make && make install  

### 2 编译安装：

Adjust Makefile.config (for example, if using Anaconda Python)  
更改makefile文件的BLAS为安装的对应的mkl或者ALTAS，然后执行下列安装:  

>make all  
make test  
make runtest  
 
或者cmake安装:  

>mkdir build  
cd build  
cmake ..  
make all  
make runtest  
