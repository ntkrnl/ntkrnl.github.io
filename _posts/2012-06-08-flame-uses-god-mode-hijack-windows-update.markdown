---
author: admin
comments: true
date: 2012-06-08 03:56:42+00:00
layout: post
slug: flame-uses-god-mode-hijack-windows-update
title: Flame利用“上帝模式”劫持Windows Update
wordpress_id: 1058
categories:
- 安全
tags:
- Flame
- 安全
- 病毒
---

卡巴斯基研究人员称，Flame恶意程序使用了多种方法自我复制，其中最令人感兴趣的是[利用微软Windows更新服务](https://www.securelist.com/en/blog/208193566/Flame_Replication_via_Windows_Update_MITM_proxy_server)，局域网中的其它机器在更新时会连接到被感染的计算机，病毒因此能在局域网中蔓延。Flame包含三大模块：“SNACK”、“MUNCH”和“GADGET”，其行为通过恶意程序的全局注册控制，它的数据库中有数以千计的可配置选项。SNACK可嗅探网络中的数据包，而MUNCH是Flame的HTTP服务器，它们能设置一个假的服务器，伪装成Windows updates的合法源。为了让代理能工作，它需要微软Root权限密钥的批准，这就是为什么它需要一个伪造的证书。攻击者利用Terminal Server的弱点创造了假证书，让恶意代码能被验证为合法代码。但光有证书还没用，因为微软在Vista之后版本中在证书信息中加入了Hydra扩展，如果证书验证通过，它会将其标记为“critical”，否则会被拒绝接受。因此攻击者需要[利用碰撞攻击](http://blogs.technet.com/b/srd/archive/2012/06/06/more-information-about-the-digital-certificates-used-to-sign-the-flame-malware.aspx?Redirected=true)移除Hydra数据。此后，Flame就能工作在所有Windows机器上。卡巴斯基研究人员将之称为[开启了“上帝模式”作弊码](http://arstechnica.com/security/2012/06/flames-god-mode-cheat-code-wielded-to-hijack-windows-7-server-2008/)。
