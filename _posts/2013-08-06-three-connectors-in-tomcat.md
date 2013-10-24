---
layout: post
title: Tomcat中三种Connector的配置方式
image: http://cdn.okaythemes.com/pocket/files/2012/10/iphone21.jpg
date: '2013-08-06 20:22'
author: 唐三
author_img: http://pic.yupoo.com/ecchanger/D4B7Qmib/medish.jpg
weibo: http://weibo.com/ecchanger
comments : true
type: 原创
categories: ["Coding", "Working"]
tags: 
- tomcat
- connector
- nio
- bio
- apr
---

年初做Tomcat和Jetty和Jboss对比性能测试时，遇到一个问题就是Tomcat的Connector修改的问题，发现无论怎么修改都不行，后来看源码才知道怎么回事，今天又有人问到这个问题，就记录下，以免自己忘记了。  

Tomcat的运行模式有3种：  
1. BIO：默认的模式，没有经过任何优化处理和支持，性能比较低下；  
2. NIO：No-blocking I/O，利用java的异步IO技术，提供一个基于缓冲区，并能提供非阻塞I/O操作，在某些场景下性能有较大提升；  
3. APR：APR(Apache Portable Runtime)是一个高可移植库，它是Apache HTTP Server 2.x的核心。包括访问高级IO功能(例如sendfile，epoll和OpenSSL)，OS级别功能(随机数生成，系统状态等等)，本地进程管理(共享内存，NT管道和UNIX sockets)。它采用C语言编写，需要在操作系统上安装包，才可以使用，无疑，这是性能最高的方式。  

如何查看当时Tomcat运行在哪个模式下呢？看看启动日志就知道了！（看配置文件不一定准，往下看…）  

    2013-7-22 11:32:42 org.apache.coyote.AbstractProtocol init
    信息: Initializing ProtocolHandler ["http-apr-8080"]  
    2013-7-22 11:32:42 org.apache.coyote.AbstractProtocol init  
    信息: Initializing ProtocolHandler ["ajp-apr-8009"]  
    2013-7-22 11:32:42 org.apache.catalina.startup.Catalina load  

由于我们线上孝已经安装了相应的APR包，所以我们是运行在APR模式下的，不过我按照网上的教程，修改了成BIO和NIO模式，却怎么也不好用，看了Tomcat源码才发现，原来是在判断BIO和NIO模式之前，先判调用了一下`isAPRAvailable（）`方法来优先取APR模式。那如何我们强制想把模式改成NIO和BIO如何改呢？可以直接修改conf/tomcat-server.xml里面的conector的属性，把protocol属性修改成`org.apache.coyote.http11.Http11Protocol`就是强制指定BIO了，如果想修改成NIO的改成`org.apache.coyote.http11.Http11NioProtocol`。
