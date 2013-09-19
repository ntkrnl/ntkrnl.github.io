---
author: admin
comments: true
date: 2012-07-02 15:58:20+00:00
layout: post
slug: resolve-upgrade-wordpress-3-4-topic-list-all-topics-even-after-the-disappearance-of
title: 解决升级 WordPress 3.4 后主题列表里所有主题都消失的问题
wordpress_id: 1781
categories:
- wordpress
tags:
- WordPress
- 主题消失
---

升级 WordPress 3.4 之后我的所有主题都从仪表盘的主题管理页面消失了，除了那个正在使用的主题。今天终于找到了原因所在，顺利解决问题。原来是优化服务器的时候将 PHP 的 scandir 函数禁用掉了，而新版 WordPress 引入了 WP_Theme 类来处理主题问题，该类使用 scandir 函数来检测 /wp-content/themes/ 中的所有主题。

我使用的是的 Linode 的 VPS，自己安装的 LAMP 网页服务器，然后按照网上的一些技巧优化性能的时候，修改了 php.ini 文件，在大约 386 行的 disable_functions = 后面列上了一堆 PHP 函数，其中就有 scandir。一直以来都没有什么问题，没想到这次升级 WordPress 就出现这样的事情，好一番测试才找到原因所在。当然解决问题的办法就是再次编辑 php.ini 文件，将 scandir 从那一行里删除，然后重新启动 Apache 服务：

service httpd restart
如果有人不是自己设置的服务器，而是使用共享主机，却碰到了这样的问题，恐怕需要联系管理员来解决了。不过估计一般的主机不会像我设置得这么变态吧。给自己找了麻烦，还不知道这样做有多少好处。

[http://cnzhx.net/blog/solve-problem-of-no-available-themes/](http://cnzhx.net/blog/solve-problem-of-no-available-themes/)
