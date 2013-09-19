---
author: admin
comments: true
date: 2012-12-25 06:59:49+00:00
layout: post
slug: sina-sae-keep-alive-in-how-to-modify-the-host-header
title: 新浪SAE如何修改主机头中的keep-alive？
wordpress_id: 1009
categories:
- 未分类
---

去[webpagetest](http://www.webpagetest.org/)测试加载速度的时候，被告知`keep-alive`参数没有设置好，在sae的选项里面找了半天没找到在哪儿改…… `htaccess`不让用就算了，那个防火墙形同虚设就算了，连`http header`都不能有完全的修改控制权，这尼玛坑爹呢！
