---
author: admin
comments: true
date: 2012-06-10 20:11:00+00:00
layout: post
slug: warning-wp-super-cache-caching-broken-the-script-advanced-cache-php-could-not-load-wp-cache-phase1-php
title: Warning! WP Super Cache caching broken! The script advanced-cache.php could
  not load wp-cache-phase1.php.
wordpress_id: 1526
categories:
- wordpress
tags:
- WordPress
- WP Super Cache
---

解决方式：
删除wp-content/advanced-cache.php文件，WP Super Cache将会自动生成该文件，该错误可能是因为复制或移动了SuperCache文件夹导致的。
