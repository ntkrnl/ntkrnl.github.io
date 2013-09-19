---
author: admin
comments: true
date: 2012-06-08 06:24:23+00:00
layout: post
slug: force-google-chrome-to-use-https
title: chrome强制google使用https
wordpress_id: 1067
categories:
- 未分类
tags:
- chrome
- google
- https
---

先关掉chrome Vista和win7用户可以到 %LOCALAPPDATA%GoogleChromeUser Data 下面（就是C:用户用户名application datagooglechromeuser data 下） 用记事本打开Local State文件 找到“"last_known_google_url” 和 “last_prompted_google_url”这两行，修改为[https://www.google.com](https://www.google.com/)，保存重启即可。
另外使用google.com可以修改一下搜索设置，关掉SafeSearch filters，在languages里面添加中文。
