---
author: admin
comments: true
date: 2010-01-23 00:45:00+00:00
layout: post
slug: zlib-problem
title: zlib的一个问题
wordpress_id: 155
categories:
- 程序
---

在zlib的官方网站上找了一个1.2.3的版本，把头文件和lib文件加进我的工程，调用uncompress函数，出现redifinition错误，大概是“malloc already defined in libcd.lib.” 按照网上的说法，可以忽略掉libcd.lib再编译，不过去掉以后会导致new方式分配内存无法使用，确实挠头，总不能不用new 吧..........

无奈最后只能用了个蹩脚的办法，动态调用zlib1.dll = =! 不知道有没有更好的办法


![](https://blogger.googleusercontent.com/tracker/3559482437792289304-6012650949965466612?l=cctvsmg.blogspot.com)
