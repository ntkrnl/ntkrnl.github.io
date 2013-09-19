---
author: admin
comments: true
date: 2012-06-10 20:20:24+00:00
layout: post
slug: chmod-recursive-subdirectories
title: chmod递归子目录
wordpress_id: 8
categories:
- linux
tags:
- centos
- chmod
- linux
- vps
---

有两种方式：
1.将一个目录下的所有子目录和文件修改属性可以用：chmod mode dir -R
2.如果对子目录要修改的属性和文件不同的话，可以用：
find dir -type d -exec chmod 755 {} ;  find dir -type f -exec chmod 644 {} ;

（其中dir为你要修改的目录）
