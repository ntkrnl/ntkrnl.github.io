---
author: admin
comments: true
date: 2012-06-08 03:27:59+00:00
layout: post
slug: under-iis-using-wp-super-cache-and-memcached
title: IIS环境下使用WP Super Cache和Memcached
wordpress_id: 1046
categories:
- 网站优化
tags:
- IIS
- Memecached
- WordPress
- WP Super Cache
- 网站优化
---

**安装IIS Rewrite插件**
因为WP Super Cache需要使用apache下的htacess文件来实现url重写，所以IIS不能直接使用。需要先下载IIS上的URL重写插件[rewrite.rar](http://www.cngeek.info/wp-content/uploads/2012/06/rewrite.rar)，在IIS管理器中选择网站，右键--->属性--->ISAPI筛选器--->添加，筛选器名称随便写一个，路径就选刚才那个rar文件里的dll，然后把httpd.ini放到网站的根目录，重启网站完成了第一步。
<!-- more -->
[![](http://www.cngeek.info/wp-content/uploads/2012/06/Unnamed-QQ-Screenshot20120608113439.jpg)](http://www.cngeek.info/wp-content/uploads/2012/06/Unnamed-QQ-Screenshot20120608113439.jpg)
**安装SuperCache**
然后安装WP Super Cache插件，要选中的几个选项是：



	
  * Caching On (Recommended)

	
  * Compress pages so they’re served more quickly to visitors. _(Recommended)_

	
  * _304 Not Modified browser caching. Indicate when a page has not been modified since last requested. __(Recommended)_


**安装Memcached**
这样就初步设置好了，由于WP Super Cache现在也支持内存缓存了，我们再来设置一下memcached插件，这样会更快。



	
  * 首先下载[php的memcache插件（5.2版本）](http://www.cngeek.info/wp-content/uploads/2012/06/php_memcache.zip)和[memcached](http://www.cngeek.info/wp-content/uploads/2012/06/memcached.zip)

	
  * 将php_memcache.dll放到php主目录下的ext文件夹，修改php.ini填加这样一行：extension=php_memcache.dll

	
  * 解压memcached.zip到任意路径，执行memcached -d install和memcached -d start

	
  * 下载[WordPress Memcached Object Cache插件](http://downloads.wordpress.org/plugin/memcached.2.0.1.zip)，解压将object-cache.php放到wp-content文件夹下


这些都设置好了以后，到后台--->设置--->WP Super Cache--->高级选项，开启“使用缓存对象来储存缓存的文件”  这个选项，至此使用Memcached的WP Super Cache就设置完成了。
