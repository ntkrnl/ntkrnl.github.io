---
author: admin
comments: true
date: 2012-06-26 12:05:09+00:00
layout: post
slug: autocad-design-drawings-of-worms-to-steal-back-to-china
title: AutoCAD蠕虫偷窃设计图纸，发回中国
wordpress_id: 1269
categories:
- 安全
tags:
- autocad
- 木马
- 蠕虫
---

安全研究人员[发现了](http://threatpost.com/en_us/blogs/autocad-worm-stealing-designs-blueprints-062512)一种窃取AutoCAD软件制作的图纸和设计文档的新蠕虫。该蠕虫被称为[ACAD/Medre.A](http://blog.eset.com/?p=13194)，通过被感染的AutoCAD模板传播，将窃取到的数以万计的文档发送回中国的电邮地址。安全专家称，病毒的感染率正在下降，表示它不属于一个有针对性的攻击活动。蠕虫于六个月前进入安全研究人员的视野，他们注意到病毒似乎针对的是秘鲁的机器。ACAD/Medre.A用AutoCAD脚本语言AutoLISP编写，作者还试图让病毒能支持未来发布的AutoCAD版本。病毒配置发送图纸到23个163.com和21个qq.com邮箱，邮箱都已爆满，返回出错信息。它还会寻找机器上的Outlook 11.0、12.0、13.0或Foxmail，然后试图发送Outlook的.PST文件。除了发送图纸外，ACAD/Medre.A还会创建一个密码为“1”的加密rar压缩文件，包含Acad.fas和趣味机械图.dxf两个文件。
