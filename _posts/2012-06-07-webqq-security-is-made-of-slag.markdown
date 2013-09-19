---
author: admin
comments: true
date: 2012-06-07 17:56:45+00:00
layout: post
slug: webqq-security-is-made-of-slag
title: WebQQ安全真是做的渣一样的
wordpress_id: 1040
categories:
- 安全
tags:
- Miranda
- QQ
- SSL
- WebQQ
- 安全
---

由于要修改[Miranda](http://code.google.com/p/miranda/)QQ插件的协议，看到有人写了一个[基于WebQQ的协议插件](http://studiokuma.googlecode.com)，一翻代码吓尿了——**腾讯的WebQQ根本丝毫没有加密，全部是明文传输！** 用HTTPAnalyzer抓包了下全都是很简单的json格式，连解密都不用随便sniffer一下数据全部到手。
腾讯就懒到连一个SSL都不加么，还是本来就没考虑过安全因素？ 反正我看到国外很多很小的站，凡是涉及到一丁点敏感数据都要SSL传输的，本土的IT企业战斗力真的不到5的感觉。
