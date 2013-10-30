---
author: admin
comments: true
date: 2013-09-27 22:45:34+00:00
layout: post
slug: gae-mongodb
title: GAE外接免费的Mongodb数据库突破Datastore读写次数限制
wordpress_id: 170
categories:
- GAE
---
Google给的Datastore读写数量限制很坑爹，这直接导致了很多开发者逃离GAE。现在有了一种新的解决方案——GAE外接免费的Mongodb数据库

####特性


- Mongolab提供的数据库完全免费，用的是Google Compute Engine服务器，与GAE之间的延迟极低，500mb大小，对于个人使用已经完全足够了


- 高性能，经测试Mongodb接口的读写速度和Datastore几乎持平


- 容易移植，只需要改几行代码，以前运行在Datastore上的程序，就能无缝桥接到Mongodb，笔者已经测试过V2ex Babel 2、Doodle blog均能正常运转

####使用方法


- 首先申请一个Mongolab免费数据库，注册好以后，在新建那里选Google Cloud Platform 
![](http://ww2.sinaimg.cn/large/7dea1af1tw1e91fmx1x8jj20kq0n2wgb.jpg)


- 新建一个以你appid命名的数据库


- git clone https://github.com/ntkrnl/gae-mongodb


- 将gae-mongodb下文件夹一块复制到要迁移的项目文件夹


- 在工程主文件的头部，或者model.py头部加入如下几句代码，'mongodb://xxxxxx'是刚才申请得到的mongodb uri，port是连接端口

    	import os
    	import datastore_mongodb_stub
    	from google.appengine.api import apiproxy_stub_map
    
    	mongodb = datastore_mongodb_stub.DatastoreMongoDBStub(os.environ['APPLICATION_ID'], False, 'datastore_v3', None, None, 'mongodb://xxxxxx', port)
    	apiproxy_stub_map.apiproxy.ReplaceStub('datastore_v3', mongodb)

	![](http://ww3.sinaimg.cn/large/7dea1af1tw1e91fmvcf2oj20n20os0vp.jpg)


- update到GAE测试是否运行成功



