---
author: admin
comments: true
date: 2013-10-23 5:35:00+00:00
layout: post
slug: windows-install-gevent
title: windows下安装gevent
wordpress_id: 172
categories:
- python
tags:
- gevent
---
Python 2.7 会搜索 Visual Studio 2008.如果你电脑上没有这个版本的话,比如只有:

- Visual Studio 2010,在cmd里面执行: `SET VS90COMNTOOLS=%VS100COMNTOOLS%`
- Visual Studio 2012 的话:`SET VS90COMNTOOLS=%VS110COMNTOOLS%`

然后就可以正常了