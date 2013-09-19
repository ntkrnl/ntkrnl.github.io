---
author: admin
comments: true
date: 2013-03-20 03:53:48+00:00
layout: post
slug: was-convinced-by-gfw-intelligent-recognition
title: 被GFW的智能识别折服了
wordpress_id: 1587
categories:
- vps
- 安全
tags:
- tor
---

还是Host1Free的免费VPS，这次是用来搭建TOR网桥。

启动TOR，绑定bridge在26端口上

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor1.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor1.png)
<!-- more -->
telnet测试测试

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor2.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor2.png)
一切正常

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor3.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor3.png)
[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor4.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor4.png)
TOR去连的时候竟然卡主了

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor5.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor5.png)
Advor同理

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor6.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor6.png)
过几分钟再次telnet

[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor7.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2013/03/tor7.png)
26端口已经被封，说明GFW能够自动分析TOR协议判断是否是TOR通信，如果是的话则临时切断并封禁一段时间端口，如果被封端口的次数多可能会导致封IP。我天朝大功夫网的技术果然不是盖的..........
