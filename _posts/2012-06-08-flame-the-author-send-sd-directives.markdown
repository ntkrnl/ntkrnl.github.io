---
author: admin
comments: true
date: 2012-06-08 04:18:49+00:00
layout: post
slug: flame-the-author-send-sd-directives
title: Flame作者发送自毁指令
wordpress_id: 1062
categories:
- 安全
tags:
- Flame
- 安全
---

赛门铁克安全研究人员在官方博客[报告](http://www.symantec.com/connect/blogs/flamer-urgent-suicide)，Flame间谍软件作者发出了自毁指令，命令被感染的机器移除程序，抹掉痕迹避免被进一步分析。Flame内置了名叫SUICIDE的模块，能用于在被感染机器上卸载程序。但上周末Flame作者通过仍被其控制的命令控制服务器释放了新的自毁模块browse32.ocx。SUICIDE能从机器上移除大部分文件，而browse32.ocx则能定位和移除所有与Flame相关的文件，然后用随机字符覆盖，防止被感染机器被人分析，抹掉了它的一切踪迹。它没有用无意义字符复写整个硬盘，而仅仅是与Flame有关的文件。
