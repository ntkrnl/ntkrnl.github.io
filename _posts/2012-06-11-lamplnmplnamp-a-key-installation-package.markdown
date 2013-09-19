---
author: admin
comments: true
date: 2012-06-11 00:01:40+00:00
layout: post
slug: lamplnmplnamp-a-key-installation-package
title: lamp|lnmp|lnamp|一键安装包
wordpress_id: 1082
categories:
- linux
- vps
tags:
- apache
- centos
- linux
- mysql
- nginx
- php
- vps
---

wdcp (WDlinux Control Panel) 是一套用PHP开发的Linux服务器管理系统,旨在易于使用和管理Linux服务器,通过web页面操作就可以管理服务器和虚拟主机.简单,方便,易操作.只有Linux版本,没有windows版本,让你方便地使用和管理Linux服务器,让不懂Linux的人也可以用Linux做服务器了.支持CentOS/RedHat版本,其它Linux版本尚未测试,欢迎测试!

<!-- more -->
功能列表
包括网站管理,服务器管理两大功能
服务器管理
1 支持apache,nginx. nginx+apache,目录访问限制,完美解决利用脚本跨站访问的问题,提高安全性.
2 在线查看系统资源,运行时间,系统负载,内存使用率,top信息
3 在线连接数管理,连接数统计,单IP连接数,连接状态统计,web连接数,mysql连接数
4 在线管理系统服务,停止,启动,设置随系统启
5 在线端口管理,可检测开通端口,关闭端口
6 在线管理进程,查看进程,终止进程KILL
7 在线设置IP地址,增加,删除
8 在线内存管理,查看内存使用情况,可在线释放内存
9 在线设置服务器所使用的DNS IP地址
10 在线执行shell命令,如ifconfig,ls,date等
11 在线查看磁盘使用率
12 在线文件管理,可编辑,修改,打包,解压,修改属性(详细介绍见下)
13 在线查看系统日志,ssh登录日志,ftp日志等
14 在线重起服务器,关机,重启相关应用服务,如web,mysql,ftp,ssh
15 在线设置mysql,php常用参数,也可直接在线编辑配置文件
16 在线设置防火墙(iptables),可增加规则,开通IP,端口,限制IP访问等
17 在线设置selinux安全配置
18 在线管理ssh,端口修改,限制root用户登录,是否DNS解释(ssh连接很慢,很可能是开启了此DNS解释)
19 在线设置可ping值,一定程度上保护服务器安全
20 在线后台直接升级,方便易操作
21 增加普通用户管理(可修改FTP用户密码,mysql数据库密码,域名邦定)
更多功能,敬请后续关注...

网站管理功能
1 新建网站,修改,删除,设置默认首页,日志记录,域名邦定,二级域名邦定等(网站文件上传至FTP主目录下的public_html目录下)
2 支持在线设置rewrite规则,增加,修改,删除
3 支持在线定制400,401,403,404,405,500,503错误定向页(此页面内容在FTP主目录的public_html/errpage/下,可自行修改)
4 可在线邦定二级域名
5 FTP用户管理,可单独建立FTP用户,修改密码,删除，限制FTP空间大小
6 mysql用户管理,可建独立mysql数据库,密码修改,删除等.可以限制mysql使用大小，更多的功能,可使用phpmyadmin
7 后台整合phpmyadmin,更好地管理mysql
8 支持网站,数据库,FTP在线打包备份

在线文件管理器
1 可编辑,修改,删除,打包,解压,修改权限/属性,所有者,所有组
2 在线打包/解压(支持.tar,tar.gz,tgz,bz2,zip格式),下载
3 支持在线文件编辑
4 使用回收站功能增加安全性,所有删除的文件都将暂存回收站里,以防误删,误操作等
5 可定制清理回收站(使用ssh,scp,WinSCP3等)

演示
[http://demo.wdlinux.cn:8080](http://demo.wdlinux.cn:8080/)
用户密码:admin/wdlinux.cn

更新20120407
1 修复登录验证BUG(严重)
2 增加文件管理器全选功能
3 调整绑定www主机名为可选
4 登录验证码调整为可选是否启用，默认不启用
5 优化在线解压，网站解压后自动设置权限
6 调整http的默认缓存设置
7 不限置特别字符密码的设置
8 修复lnmp环境301跳转默认IP也跳转的问题
9 修复后台重起功能部分系统无效的问题
10 修复在线更新不能更新的问题
11 增加mysql,ftp的备份，之前更换模板时把这两个给漏了
12 修复默认站点问题
13 增加修改wdcp数据库用户的密码修改

下载安装
wget [http://dl.wdlinux.cn:5180/lanmp_v2.2.tar.gz](http://dl.wdlinux.cn:5180/lanmp_v2.2.tar.gz)
tar zxvf lanmp_v2.2.tar.gz
sh in.sh
可选安装lnamp,lamp,lnmp三个中任一个

wdcp管理系统后台访问地址
http://ip:8080
默认用户密码
admin
wdlinux.cn

mysql默认的用户密码
root
wdlinux.cn

部分组件的可选安装，如memcache,mysqli,pdo_mysql,innodb等
具体的安装方法可见[http://www.wdlinux.cn/bbs/thread-1356-1-1.html](http://www.wdlinux.cn/bbs/thread-1356-1-1.html)

安装说明
有比较多的朋友说在安装mysql时会“卡住”，其实不然，只不过是因为mysql的编译时间比较长，10至30分钟不等，具体看机器的硬件配置，所以请耐心等待，但有些是网络中断就真像卡住了一样，到底是不是真卡住，可以看这里的说明
[http://www.wdlinux.cn/bbs/thread-65-1-1.html](http://www.wdlinux.cn/bbs/thread-65-1-1.html)

升级
1.X版本
wget [http://down.wdlinux.cn/down/wdcp1t2_up.sh](http://down.wdlinux.cn/down/wdcp1t2_up.sh)
sh wdcp1t2_up.sh

2.0/2.1版本升级
wget [http://down.wdlinux.cn/down/wdcp2021_up.sh](http://down.wdlinux.cn/down/wdcp2021_up.sh)
sh wdcp2021_up.sh

2.2的直接在后台升级即可
(2.0/2.1/2.2强烈建议升级)

**相关说明**
所有软件安装目录/www/wdlinux
站点配置文件
/www/wdlinux/nginx/conf/vhost
/www/wdlinux/apache/conf/vhost

数据库配置文件/www/wdlinux/etc/my.cnf
数据库文件目录 /www/wdlinux/mysql/var

**卸载或重装**
sh in.sh un
即可卸载，并且自动重起
启动完登录后，再次运行
sh in.sh
便可重装
重装后重新打开IE，否则会有session错误提示的问题**
****卸载或重装请备份好数据，否则数据丢失后果自负**

**相关软件版本**
httpd-2.2.22
nginx-1.0.12
php-5.2.17
mysql-5.1.61
phpmyadmin-3.3.7
zend-3.3.3
eAccelerator-0.9.5.3
pure-ftpd-1.0.35


原文： [http://www.wdlinux.cn/bbs/thread-1788-1-1.html](http://www.wdlinux.cn/bbs/thread-1788-1-1.html)
