---
author: admin
comments: true
date: 2012-12-25 06:59:26+00:00
layout: post
slug: tor-ramdisk
title: tor-ramdisk
wordpress_id: 1005
categories:
- 安全
---

[tor-ramdisk](http://opensource.dyc.edu/tor-ramdisk)是一个只运行[tor](https://www.torproject.org/)节点的系统映像，特点：



	
  * 完全在内存中运行，断电以后完全不会存留任何数据在硬盘，从而保证了安全性；

	
  * iso的大小才5.3mb


缺点是不支持Hidden Service，因为Hidden Service需要一些别的服务比如HTTP等等，作者没有加，[下载地址](http://opensource.dyc.edu/pub/tor-ramdisk/images/)
