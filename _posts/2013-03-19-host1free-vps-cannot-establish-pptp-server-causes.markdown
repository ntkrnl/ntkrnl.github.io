---
author: admin
comments: true
date: 2013-03-19 05:51:53+00:00
layout: post
slug: host1free-vps-cannot-establish-pptp-server-causes
title: Host1Free VPS无法建立PPTP服务器的原因
wordpress_id: 1584
categories:
- vps
---

申请了一个Host1Free的免费VPS一直不知道来做什么好，几次试图建立VPN服务器都没成功，拨过去就是619错误。今天才知道是服务商禁掉了<del>奸商</del> 在安装pptp服务之前先运行下面命令，如果像下面这样是正常的


> cat /dev/ppp cat: /dev/ppp: No such device or address cat /dev/net/tun cat: /dev/net/tun: File descriptor in bad state


如果返回“Permission denied”就是被禁用了
