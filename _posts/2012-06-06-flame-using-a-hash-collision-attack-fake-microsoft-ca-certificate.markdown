---
author: admin
comments: true
date: 2012-06-06 11:54:01+00:00
layout: post
slug: flame-using-a-hash-collision-attack-fake-microsoft-ca-certificate
title: Flame利用哈希碰撞攻击伪造微软CA证书
wordpress_id: 1478
categories:
- 未分类
---

软安全专家称，Flame的幕后攻击者[利用了](http://arstechnica.com/security/2012/06/flame-wields-rare-collision-crypto-attack/)罕见的[碰撞攻击方法](http://en.wikipedia.org/wiki/Collision_attack)伪造微软的数字证书。碰撞攻击在理论上是可行的，但在实践中却是闻所未闻。2008年，研究人员利用200台PS3[碰撞攻击MD5算法](http://it.solidot.org/article.pl?sid=09/01/01/050232&tid=70)，创造了一个伪造的CA证书。微软本周一承认，Flame利用了旧哈希函数弱点伪造Terminal Server产品的证书。微软安全响应中心高级主管Mike Reavey说，Flame恶意程序利用了加密碰撞攻击结合使用Terminal Server授权服务证书去签名其代码，但他没有对此详细描述。一位加密技术专家认为，微软的意思可能是Terminal Server中弱点允许攻击者伪造证书，而碰撞攻击则让他们能隐藏身份。
