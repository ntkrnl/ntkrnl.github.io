---
author: admin
comments: true
date: 2011-05-18 08:13:00+00:00
layout: post
slug: lpk-fail-to-load-under-win7-solution
title: win7下lpk加载失败的解决
wordpress_id: 106
categories:
- 调试
---

####现象

在xp下能正常运行的lpk补丁放到win7运行，程序一运行就卡死，通过调试发现其中在oleaut32.dll中执行DllMain中一句RegisterWindowMessage发生了错误，程序崩溃，然后在seh中不断循环。


####原理

作为一个lpk补丁，有个很重要的问题就是不能在一开始加载过多的dll，因为你加载的dll如果太复杂会反过来调用lpk的函数，但此时lpk并没有初始化成功。在这个例子中gdi32.dll里面有部分代码是加载lpk.dll，然后寻找lpk的几个函数的地址，此时gdi并没有完成初始化，但是后面运行RegisterWindowMessage这个显然和消息窗口有关。

####解决

使用连接器提供的延迟加载参数/DelayLoad，把大多数非核心dll都放到后面加载，让lpk先初始化完成。

