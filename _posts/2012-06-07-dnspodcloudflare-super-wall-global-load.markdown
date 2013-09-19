---
author: admin
comments: true
date: 2012-06-07 17:32:03+00:00
layout: post
slug: dnspodcloudflare-super-wall-global-load
title: DNSPod+CloudFlare=超级穿墙+全球负载
wordpress_id: 1027
categories:
- 网站优化
tags:
- CDN
- CloudFlare
- DNSPod
- 网站优化
---

博主实在太穷买不起linode服务器，这个博客所在的服务器位于美国西海岸，国内电信ping的延迟大概160ms左右，网通延迟很高，加上服务器配置不行，刚安装完的时候加载一个wordpress初始页面都要10s，于是我毅然决然的开始了折腾之旅。既然要提速，肯定要用CDN了，免费CDN里面有[cloudflare](https://www.cloudflare.com)、、[webluker](http://www.webluker.com/)、[incapsula](http://www.incapsula.com/)等，webluker需要备案，incapsula导入域名一直解析出错，所以只能用cloudflare了。

首先注册cloudflare，随便填了一通以后我们来到这个界面：
<!-- more -->
[![](http://bitcn.org/wp-content/uploads/2012/06/DNS-Settings-CloudFlare-The-web-performance-security-company-651x1024.png)](http://bitcn.org/wp-content/uploads/2012/06/DNS-Settings-CloudFlare-The-web-performance-security-company.png)

但是cloudflare经过我的测试被墙了好多节点，怎么用呢？

我们来看一下cloudflare都有哪些IP，官方在[这里](https://www.cloudflare.com/wiki/What_are_the_CloudFlare_IP_address_ranges)有说明


> CloudFlare uses the following IPv4 address ranges:

204.93.240.0/24 (204.93.240.0 - 204.93.240.255)
204.93.177.0/24 (204.93.177.0 - 204.93.177.255)
199.27.128.0/21 (199.27.128.0 - 199.27.135.255)
173.245.48.0/20 (173.245.48.0 - 173.245.63.255)
103.22.200.0/22 (103.22.200.0 - 103.22.203.255)
141.101.64.0/18 (141.101.64.0 - 141.101.127.255)
108.162.192.0/18 (108.162.192.0 - 108.162.255.255)
190.93.240.0/20 (190.93.240.0-190.93.255.255)

CloudFlare uses the following IPv6 address ranges:

2400:CB00:/32 (2400:CB00:0000:0000 - 2400:CB00:FFFF:FFFF)
2606:4700:/32 (2606:4700:0000:0000 - 2606::4700:FFFF:FFFF)
2803:f800:/32 (2803:f800:0:0:0:0:0:0 -2803:f800:FFFF:FFFF)


其中103开头的位于香港，173和108开头的位于美国西海岸，141开头的位于瑞典，190开头的位于中美洲…… 经过测试联通到香港节点103.22.200.18的速度最快，电信则是到美国节点190.93.240.5速度最快，国外只要一律用173.245.48.11即可，cloudflare好像能自动平衡。我们只需要用DNSPod将域名针对不同的地区解析到这些CloudFlare的节点上，Cloudflare就会自动帮我们转到刚才填的A记录站点。

DNSPod也是胡乱填一下， 来到这里：
[![](http://bitcn.org/wp-content/uploads/2012/06/DNSPod1.png)](http://bitcn.org/wp-content/uploads/2012/06/DNSPod1.png)

然后就到的你域名服务商那里把NS记录转到DNSPod就行：
[![](http://bitcn.org/wp-content/uploads/2012/06/Domain-Manager-Domain-Details.png)](http://bitcn.org/wp-content/uploads/2012/06/Domain-Manager-Domain-Details.png)

如果你用google的8.8.8.8的话可能半个小时就初步见效了，大概得等至少五六个小时吧DNS才能全球都刷新完。 这招儿对付被墙的网站可能会管用，只是不知道cloudflare的节点被封的会不会越来越多……
