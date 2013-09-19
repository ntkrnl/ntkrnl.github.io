---
author: admin
comments: true
date: 2012-06-18 02:14:18+00:00
layout: post
slug: compiling-under-linux-install-protobuf
title: LINUX下编译安装PROTOBUF
wordpress_id: 1118
categories:
- linux
- 程序
tags:
- linux
- protobuf
---

如果出现错误：
protoc: error while loading shared libraries: libprotobuf.so.0: cannot open shared object file: No such file or directory The issue is that Ubuntu 8.04 doesn't include /usr/local/lib in library paths.

To fix it for your current terminal session, just type in
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
