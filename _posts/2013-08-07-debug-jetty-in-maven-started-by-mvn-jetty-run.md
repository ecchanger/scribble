---
layout: post
title: 在Maven中的Jetty插件中进行Debug
image: http://pic.yupoo.com/ecchanger/D4TM2RoY/medish.jpg
date: '2013-08-07 15:22:10'
author: 唐三
author_img: http://pic.yupoo.com/ecchanger/D4B7Qmib/medish.jpg
weibo: http://weibo.com/ecchanger
comments : true
type: 原创
categories: ["Coding"]
tags: 
- jetty
- maven
- debug
---

　　WebX默认工程安装了Maven Jetty插件，用起来很方便，做简单测试时不用总往Tomcat里跑了，不过因为没法设置启动参数，无法Debug，今天搜索了一下，找到了一个方法：

1.Set environment variable MAVEN_OPTS to:  

```
-Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n
```
2.Then in Eclipse 3 click Run > Debug Configurations > create New Remote Java Application. Remember to attach sources. Invoke Maven by mvn jetty:run and start Debug in Eclipse.

Idea中也一样，启动一个Reomte，然后监听8000端口就可以了....


**来源**：[http://gaertig.pl/blog/en/2009/03/debug-jetty-in-maven-started-by-mvn-jetty-run.html](http://gaertig.pl/blog/en/2009/03/debug-jetty-in-maven-started-by-mvn-jetty-run.html)