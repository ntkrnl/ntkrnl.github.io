---
author: admin
comments: true
date: 2013-12-13 22:38:00+00:00
layout: post
slug: gyp-binding-gyp-not-found
title: binding.gyp not found错误解决
wordpress_id: 174
categories:
- node.js 
tags:
- node-gyp
---
编译node.js的sqlite3，从官网下载下来的居然编译出错，提示：

    make: Entering directory `/home/ntkrnl/ghost/node_modules/sqlite3/build'
    make: Warning: File `../deps/sqlite3.gyp' has modification time 2.1e+06 s in the future
      ACTION Regenerating Makefile
    gyp: binding.gyp not found (cwd: /home/ntkrnl/ghost/node_modules/sqlite3/build) while trying to load binding.gyp
    
试验了各种方法挨个把build文件夹下的文件都看了也还是搞不定，最后发现这句：

    make: Warning: File `../deps/sqlite3.gyp' has modification time 2.1e+06 s in the future 

WTF？！！！ 时间不对？  原来是虚拟机里面好久没更新时间了............
