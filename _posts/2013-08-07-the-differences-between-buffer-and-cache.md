---
layout: post
title: Buffer和Cache的区别
image: http://pic.yupoo.com/ecchanger/D4Ubu6k8/medium.jpg
date: '2013-08-02 11:48:17'
author: 唐三
author_img: http://pic.yupoo.com/ecchanger/D4B7Qmib/medish.jpg
weibo: http://weibo.com/ecchanger
comments : true
type: 原创
categories: ["Coding", "Working"]
tags: 
- buffer
- cache
- linux
---

作中经常谈到Cache和Buffer，但二者有什么区别呢？今天突然想到这个，就Google下，找了一下答案，记录下…

网上找到一篇[《Difference between Cache and Buffer》](http://www.differencebetween.info/difference-between-cache-and-buffer)，文中这样描述：

>Both cache and buffer are types of temporary storage that are utilized in computer science. However, they differ in the methods and the capabilities in which they are used. A cache transparently stores data so that future requests for that data can be served faster. A buffer, on the other hand, temporarily stores data while the data is the process of moving from one place to another, i.e. the input device to the output device.

首先两者都是计算机中临时保存数据的方法，但二者有如下不同：

**缓存**（Cached）是把读取过的数据保存起来，当再次需要读取这个数据时，如果命中就不要去回源了，若没有命中就回源读硬盘或者RPC；  

**缓冲**（Buffer）是根据磁盘的读写设计的，把分散的写操作集中进行，减少磁盘碎片和硬盘的反复寻道，从而提高系统性能。  



**参考资料**：  
[Difference between Cache and Buffer](http://www.differencebetween.info/difference-between-cache-and-buffer)  
[Buffer和Cache的区别](http://yoozhu.com/?p=23)