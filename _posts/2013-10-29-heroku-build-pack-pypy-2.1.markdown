---
author: admin
comments: true
date: 2013-10-29 01:00:00+00:00
layout: post
slug: heroku-build-pack-pypy-2.1
title: 让Heroku支持PyPy-2.1
wordpress_id: 173
categories:
- Python 
tags:
- Heroku
- PyPy
---
Heroku只支持PyPy-1.9，由于greenlet在早期的pypy版本上比较慢，PyPy-2.1还能支持个gevent，所以顺手搞了一个Heroku的PyPy-2.1 build pack

这个fork版本支持的Python Runtime：

- Python-2.7.4
- Python-3.3.1 
- PyPy-1.9 (experimental)
- PyPy-2.1 (experimental)

使用方法：

- 创建新项目的时候：`heroku create --stack cedar --buildpack git://github.com/ntkrnl/heroku-buildpack-pypy2.1.git`


- 对于已经存在的项目：`heroku config:set BUILDPACK_URL=git://github.com/ntkrnl/heroku-buildpack-pypy2.1.git`

- 在`runtime.txt`里面，写`pypy-2.1`

使用Tornado hello world， `ab -n 10000 -c 300`做了下性能测试

- Python-2.7.4
 ![](http://ww3.sinaimg.cn/large/7dea1af1tw1ea1f2snxvuj20ge0ghjt8.jpg)
- PyPy-1.9
 ![](http://ww2.sinaimg.cn/large/7dea1af1tw1ea1f2r6q37j20g80g5gnc.jpg)
- PyPy-2.1
![](http://ww4.sinaimg.cn/large/7dea1af1tw1ea1f2nn5hyj20gc0gcq48.jpg)

可以看出和PyPy-2.1相比，Python-2.7.4和PyPy-1.9都是渣渣

值得注意的是PyPy占用的内存颇多，Python-2.7.4大概启动的时候使用30mb的内存，PyPy则至少150mb。而Heroku的一个free instance只有500mb的内存，所以如果用Supervisor启动多个进程的时候，要注意设置[PYPY_GC_MAX](http://doc.pypy.org/en/latest/gc_info.html)，防止内存溢出。