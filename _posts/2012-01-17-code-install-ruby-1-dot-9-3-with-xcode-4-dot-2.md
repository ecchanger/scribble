---
layout: post
title: rvm 安装 Ruby 1.9.3时错误： compiler cannot create executables
image: http://pic.yupoo.com/ecchanger/D4Zviznb/medium.jpg
date: '2012-01-17 14:32'
author: 唐三
author_img: http://pic.yupoo.com/ecchanger/D4B7Qmib/medish.jpg
weibo: http://weibo.com/ecchanger
comments : true
type: 原创
categories: ["Coding", "Studying"]
tags:
- ruby
- tip
---

rvm 安装 Ruby 1.9.3时错误： 

	compiler cannot create executables，rvm install 1.9.3
	Installing yaml to /Users/ecchanger/.rvm/usr
	ruby-1.9.3-p0 - #configuring
	ERROR: Error running ' ./configure --prefix=/Users/ecchanger/.rvm/rubies/ruby-1.9.3-p0
	 	--enable-shared --disable-install-doc --with-libyaml-dir=/Users/ecchnager/.rvm/usr ',
	 	please read /Users/ecchanger/.rvm/log/ruby-1.9.3-p0/configure.log
	ERROR: There has been an error while running configure. Halting the installation.

看日志也没看出来是什么问题，后来上网查到的答案，原因是xcode 4.2移除了 non-LLVM 版本的 GCC，而1.9.3安装时要这个版本的gcc才能编译。安装4.1版本的xcode没有问题。用以下方式安装就可以了。

	rvm install 1.9.3 --with-gcc=clang

参考：[http://stackoverflow.com/questions/8032824/cant-install-ruby-under-lion-with-rvm-gcc-issues](http://stackoverflow.com/questions/8032824/cant-install-ruby-under-lion-with-rvm-gcc-issues)