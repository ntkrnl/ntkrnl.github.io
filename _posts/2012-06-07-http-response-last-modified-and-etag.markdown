---
author: admin
comments: true
date: 2012-06-07 09:39:08+00:00
layout: post
slug: http-response-last-modified-and-etag
title: http响应Last-Modified和ETag
wordpress_id: 1484
categories:
- 未分类
- 网站优化
---

文章来源：[http://www.iwms.net/n2029c12.aspx](http://www.iwms.net/n2029c12.aspx)

基础知识
**1) 什么是”Last-Modified”?
**　　在浏览器第一次请求某一个URL时，服务器端的返回状态会是200，内容是你请求的资源，同时有一个Last-Modified的属性标记此文件在服务期端最后被修改的时间，格式类似这样：
Last-Modified: Fri, 12 May 2006 18:53:33 GMT
客户端第二次请求此URL时，根据 HTTP 协议的规定，浏览器会向服务器传送 If-Modified-Since 报头，询问该时间之后文件是否有被修改过：
If-Modified-Since: Fri, 12 May 2006 18:53:33 GMT
如果服务器端的资源没有变化，则自动返回 HTTP 304 （Not Changed.）状态码，内容为空，这样就节省了传输数据量。当服务器端代码发生改变或者重启服务器时，则重新发出资源，返回和第一次请求时类似。从而保证不向客户端重复发出资源，也保证当服务器有变化时，客户端能够得到最新的资源。
**2) 什么是”Etag”?
**　　HTTP 协议规格说明定义ETag为“被请求变量的实体值” （参见 —— 章节 14.19）。 另一种说法是，ETag是一个可以与Web资源关联的记号（token）。典型的Web资源可以一个Web页，但也可能是JSON或XML文档。服务器单独负责判断记号是什么及其含义，并在HTTP响应头中将其传送到客户端，以下是服务器端返回的格式：
ETag: "50b1c1d4f775c61:df3"
客户端的查询更新格式是这样的：
If-None-Match: W/"50b1c1d4f775c61:df3"
如果ETag没改变，则返回状态304然后不返回，这也和Last-Modified一样。本人测试Etag主要在断点下载时比较有用。
**Last-Modified和Etags如何帮助提高性能?
**　　聪明的开发者会把Last-Modified 和ETags请求的http报头一起使用，这样可利用客户端（例如浏览器）的缓存。因为服务器首先产生 Last-Modified/Etag标记，服务器可在稍后使用它来判断页面是否已经被修改。本质上，客户端通过将该记号传回服务器要求服务器验证其（客户端）缓存。
过程如下:



	
  1. 客户端请求一个页面（A）。

	
  2. 服务器返回页面A，并在给A加上一个Last-Modified/ETag。

	
  3. 客户端展现该页面，并将页面连同Last-Modified/ETag一起缓存。

	
  4. 客户再次请求页面A，并将上次请求时服务器返回的Last-Modified/ETag一起传递给服务器。

	
  5. 服务器检查该Last-Modified或ETag，并判断出该页面自上次客户端请求之后还未被修改，直接返回响应304和一个空的响应体。


