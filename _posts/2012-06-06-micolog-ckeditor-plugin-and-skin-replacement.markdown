---
author: admin
comments: true
date: 2012-06-06 12:33:08+00:00
layout: post
slug: micolog-ckeditor-plugin-and-skin-replacement
title: micolog的ckeditor插件及皮肤更换
wordpress_id: 1480
categories:
- 未分类
---

用惯了wordpress的ck-and-syntaxhighlighter，xheditor没有blockquote很麻烦，micolog的ckeditor插件下载地址[点这里](http://micolog.appspot.com/plugins/view?key=agdtaWNvbG9nchsLEgZQbHVnaW4iD0NLRWRpdG9yIHBsdWdpbgw)

改皮肤的方法有两种：


> A.config.js里面加入一行config.skin = 'office2003';这里office2003是你要改的皮肤名字，当然ckeditor自带的皮肤只有三种kama、office2003、v2；

B.修改ckeditor.js，找到skin:'kama'，把皮肤替换成自己想要的即可。
