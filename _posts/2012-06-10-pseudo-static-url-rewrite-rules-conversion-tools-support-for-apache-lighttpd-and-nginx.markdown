---
author: admin
comments: true
date: 2012-06-10 20:15:19+00:00
layout: post
slug: pseudo-static-url-rewrite-rules-conversion-tools-support-for-apache-lighttpd-and-nginx
title: URL Rewrite伪静态规则转换工具，支持Apache、Lighttpd和Nginx
wordpress_id: 1527
categories:
- linux
tags:
- apache
- lighttpd
- linux
- nginx
- WordPress
---


URL RewriteRule conversion tool | URL伪静态规则转换工具
[http://www.onexin.net/rewrite.php](http://www.onexin.net/rewrite.php)

Apache

    RewriteRule ^store-([0-9]+).html$ store.php?id=$1 [L,NC]
    

IIS rewrite (WordPress)


    [ISAPI_Rewrite]
    CacheClockRate 3600
    RepeatLimit 32

    RewriteRule ^index.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]


Apache rewrite

    
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]


Nginx rewrite


    location / {
    index index.html index.php;
    if (-f $request_filename/index.html){
    rewrite (.*) $1/index.html break;
    }
    if (-f $request_filename/index.php){
    rewrite (.*) $1/index.php;
    }
    if (!-f $request_filename){
    rewrite (.*) /index.php;
    }
    }


来源：http://www.onexin.net/rewrite-rules-for-pseudo-static-conversion-tools-support-apache-lighttpd-and-nginx/
