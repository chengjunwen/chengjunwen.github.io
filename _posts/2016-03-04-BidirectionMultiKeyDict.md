---                                                                             
layout: post
title:  "建立python的双向可以多重key值的dict"
date:   2016-03-04 20:42:05
categories: python
excerpt: 双向 多重key值的 dict 
---

### 建立python的双向, 多重key值的dict
前端时间用python做音乐生成，需要用到可以双向查找的字典， 同时还希望词典中有重复的key值， 因而参考了stackoverflow上的代码， 将二者结合完成了所需  

	class Dictlist(dict):
		def __setitem__(self, key, value):
			try:
				self[key]
			except KeyError:
				super(Dictlist, self).__setitem__(key, [])
			self[key].append(value)
	class BidirectionaDict(Dictlist):
		def __setitem__(self, key, val):
			Dictlist.__setitem__(self, key, val)
			Dictlist.__setitem__(self, val, key)
		def __delitem__(self, key):
			Dictlist.__delitem__(self, self[key])
			Dictlist.__delitem__(self, key)


`Dictlist` 完成多重key值实现  
`BidirectionDict` 实现key和value的双向访问  
测试：

> \> d = BidirectionalDict()  
\> d['test'] = 1  
\> d['test'] = 2  
\> d['test'] = 3  
\> d['train'] = 1  
\> d['train'] = 2  
\> d['test']  
[1, 2, 3]  
\> d[1]  
['test', 'train']    

