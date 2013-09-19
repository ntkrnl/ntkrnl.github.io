---
author: admin
comments: true
date: 2012-06-11 00:06:21+00:00
layout: post
slug: 512m-vps-performance-following-small-memory-optimization-and-security
title: 512M内存以下的小内存VPS性能优化和安全防护
wordpress_id: 1085
categories:
- linux
- vps
tags:
- linux
- lnmp
- vps
- vps优化
---

<!-- more -->
**优化开始（本文所有参数可以根据自己内存情况进行微调）：**

建议先看 **LNMP** 配置一文，这次优化的方法是基于lnmp的配置，lnmp Web环境配置方法在这里就不在重复了。

**1.关闭不需要的服务，（这是我所关闭的服务，请看清每个服务，根据自己情况而定）**



> chkconfig --level 3 acpid off
chkconfig --level 3 anacron off
chkconfig --level 3 apmd off
chkconfig --level 3 mdmonitor off
chkconfig --level 3 xinetd off
chkconfig --level 3 Sendmail off
chkconfig --level 3 rpcgssd off
chkconfig --level 3 rawdevices off
chkconfig --level 3 messagebus off
chkconfig --level 3 atd off
chkconfig --level 3 gpm off
chkconfig --level 3 autofs off
chkconfig --level 3 cpuspeed off
chkconfig --level 3 haldaemon off
chkconfig --level 3 nfslock off
chkconfig --level 3 portmap off
chkconfig --level 3 xfs off
chkconfig --level 3 netfs off
chkconfig --level 3 smartd off
chkconfig --level 3 ip6tables off
chkconfig --level 3 isdn off
chkconfig --level 3 rpcidmapd off
chkconfig --level 3 microcode_ctl off

service acpid stop
service anacron stop
service apmd stop
service mdmonitor stop
service xinetd stop
service sendmail stop
service rpcgssd stop
service rawdevices stop
service messagebus stop
service atd stop
service gpm stop
service autofs stop
service cpuspeed stop
service haldaemon stop
service nfslock stop
service portmap stop
service xfs stop
service netfs stop
service smartd stop
service ip6tables stop
service isdn stop
service rpcidmapd stop
service microcode_ctl stop




**2. 删除CentOS自带的sendmail，改用postfix。
**# yum remove sendmail
# yum install postfix

**3.增加SWAP分区大小（一般是内存的2倍）
**# cd /var/
# dd if=/dev/zero of=swapfile bs=1024 count=524288
# /sbin/mkswap swapfile
# /sbin/swapon swapfile

注意：增加SWAP分区只能在Xen VPS上操作，OpenVZ的VPS不行。感谢网友：（角落bujinshuo.com）的提醒

让系统自动引导：
# echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab

**4.MySQL的配置文件优化（适用于mysql版本为：mysql-5.1.57）**

编译安装参数：


> ./configure --prefix=/usr/local/webserver/mysql/
--enable-assembler
--with-extra-charsets=complex
--enable-thread-safe-client
--with-big-tables --with-readline
--with-SSL 
--with-embedded-server
--enable-local-infile


my.cnf文件参数：




> [root@MyVPS2524 ~]# cat /etc/my.cnf | grep -v "#"

>     
>     [client]
>     port            = 3306
>     socket          = /tmp/mysql.sock
>     
>     [mysqld]
>     user            = mysql
>     port            = 3306
>     socket          = /tmp/mysql.sock
>     basedir         = /usr/local/webserver/mysql
>     datadir         = /data/mysqldata/database
>     log-error       = /data/mysqldata/log/mysql_error.log
>     pid-file        = /data/mysqldata/pid/mysql.pid
>     skip-external-locking
>     skip-name-resolve
>     default_table_type = MyISAM
>     transaction_isolation = READ-UNCOMMITTED
>     open_files_limit = 600
>     back_log = 40
>     key_buffer_size = 4M
>     max_allowed_packet = 16M
>     thread_stack = 192K
>     table_cache = 60
>     external-locking = FALSE
>     sort_buffer_size = 256K
>     read_buffer_size = 1M
>     join_buffer_size = 256K
>     read_rnd_buffer_size = 4M
>     bulk_insert_buffer_size = 2M
>     myisam_sort_buffer_size = 4M
>     myisam_repair_threads = 1
>     myisam_recover
>     
>     thread_cache = 128
>     thread_cache_size = 10
>     query_cache_size = 0M
>     query_cache_limit = 2M
>     query_cache_min_res_unit = 4K
>     tmp_table_size = 512K
>     max_heap_table_size = 32M
>     long_query_time = 1
>     log-short-format
>     max_connections = 200
>     wait_timeout = 30
>     max_connect_errors = 200
>     expire_logs_days = 7
>     thread_concurrency = 8
>     
>     server-id       = 1
>     
>     [mysqldump]
>     quick
>     max_allowed_packet = 16M
>     
>     [mysql]
>     no-auto-rehash


说明：mysql是默认支持4种存储引擎：CSV，MRG_MYISAM，MEMORY，MyISAM，默认不支持InnoDB存储引擎（消耗内存比较大）。由于内存很小，推荐使用MyISAM存储引擎。

**5.Nginx配置优化
**nginx主配文件nginx.conf参数：




> #user options
user www www;
#CPU Core options  //本应该开启至少2个nginx进程，由于内存太小，只能节约一点了。 worker_processes 1;
#nginx Process options
pid /usr/local/webserver/nginx/nginx.pid;
# [ debug | info | notice | warn | error | crit ]
error_log /data/wslogs/nginx_error.log crit;
#Specifies the value for maximum file descriptors that can be opened by this process.
worker_rlimit_nofile 51200;

events
{
 use epoll;
 #maxclient = worker_processes * worker_connections / cpu_number
 worker_connections 51200;
}

http
{
 include mime.types;
 default_type application/octet-stream;
 #charset gb2312;

 #General options
 server_names_hash_bucket_size 128;
 client_header_buffer_size 32k;
 large_client_header_buffers 4 32k;

 sendfile on;

 #timeouts
 keepalive_timeout 60;

 #TCP options
 tcp_nopush on;
 tcp_nodelay on;

 #fastcgi options
 fastcgi_connect_timeout 300;
 fastcgi_send_timeout 300;
 fastcgi_read_timeout 300;

 fastcgi_buffer_size 64k;
 fastcgi_buffers 4 64k;
 fastcgi_busy_buffers_size 128k;
 fastcgi_temp_file_write_size 128k;  #gzip  compression  //对html、CSS、JS、XML等文件启用gzip压缩，减少数据传输量，提高访问速度。 gzip on;
 gzip_min_length 1k;
 gzip_buffers 4 16k;
 gzip_http_version 1.0;
 gzip_comp_level 2;
 gzip_types text/plain text/css application/x-javascript application/xml;
 gzip_vary on;

 #limit_zone  crawler  $binary_remote_addr  10m;

 #virtual hosts options
 include vhosts.conf;
}


虚拟主机配置文件参数优化（这里我是把虚拟主机配置文件和nginx.conf分开的）：




> server {
 listen 80;
 server_name www.linuxde.net linuxde.net;
 access_log /data/wslogs/linuxde_www_access.log combined;
 index index.html index.htm index.php;
 root /data/wsdata/wwwroot/linuxde/www; #这是对网站的301重定向，当用linuxde.net地址访问，会跳转到www.linuxde.net if ($host !~ "^www.linuxde.net$") {
  rewrite ^(.*) http://www.linuxde.net$1 permanent;
 }
 location ~ .*.(php|php5)?$ {  #nginx与phpfcgi的通信方式
  #用Unix Socket通行方式比TCP通信方式速度快，但是TCP在高并发的时候比Unix Socket稳定。  fastcgi_pass  unix:/tmp/php-cgi.sock;
  #fastcgi_pass   127.0.0.1:9000;
  fastcgi_index   index.php;
  include enable_fcgi.conf;
 } #将gif|jpg|jpeg|png|bmp|swf文件在本地浏览器缓存30天，这个时间自己看情况决定！ location ~ .*.(gif|jpg|jpeg|png|bmp|swf)$ {
  access_log      off;
  expires 30d;
 } #同上，这个不用解释 location ~ .*.(js|css)$ {
  access_log      off;
  expires 1d;
 } #wordpress的伪静态 location / {
  if (-f $request_filename/index.html){
   rewrite (.*) $1/index.html break;
  }
  if (-f $request_filename/index.php){
   rewrite (.*) $1/index.php;
  }
  if (!-f $request_filename){
   rewrite (.*) /index.php;
  }
 }
}


**6.PHP的配置优化
**php-fpm.conf配置文件优化参数：
将php-fpm.conf文件下面一行参数值修改为5，就是开启5个php-cgi进程，这是系统占内存最多进程




> <value name="max_children">5</value>
> 
> 
补充：这条命令是查看phpcgi进程数，如果接近预设值，说明不够用，需要增加，小内存VPS不够用也没办法。
netstat -anpo | grep "php-cgi" | wc -l

修改nginx和phpfcgi的通信方式，修改下面一行参数：

>     
>     <value name="listen_address">/tmp/php-cgi.sock</value>
> 
> 
应为改用了postfix，所以下面参数需要修改：

>     
>     <value name="sendmail_path">/usr/sbin/sendmail.postfix -t</value>
> 
> 
eAccelerator的优化（添加在php.ini文件中）：

>     
>     [eaccelerator]
>     zend_extension="/usr/local/webserver/php/lib/php/extensions/no-debug-non-zts-20060613/eaccelerator.so"
>     eaccelerator.shm_size="8"
>     eaccelerator.cache_dir="/usr/local/webserver/eaccelerator_cache"
>     eaccelerator.enable="1"
>     eaccelerator.optimizer="1"
>     eaccelerator.check_mtime="1"
>     eaccelerator.debug="0"
>     eaccelerator.filter=""
>     eaccelerator.shm_max="0"
>     eaccelerator.shm_ttl="3600"
>     eaccelerator.shm_prune_period="3600"
>     eaccelerator.shm_only="0"
>     eaccelerator.compress="1"
>     eaccelerator.compress_level="9"
>     eaccelerator.keys = "disk_only"
>     eaccelerator.sessions = "disk_only"
>     eaccelerator.content = "disk_only"


说明：只使用1M共享内存，删除所有在最后3600秒内无法存取的脚本缓存，用磁盘辅助进行缓存。

**7.系统内核的优化
**在文件末尾添加以下参数：
vim /etc/sysctl.conf


> #add
>     net.ipv4.conf.all.send_redirects = 0
>     net.ipv4.conf.all.accept_redirects = 0
> 
> 
#/sbin/sysctl -p



**8.最后是安全相关
**使用iptables关闭不需要对外开放的端口
iptables脚本内容（对外只开放22和80端口）：


> #清除iptables记录
>     iptables -F; iptables -X; iptables -Z
>     #开启SSH登录端口
>     iptables -A INPUT -p tcp --dport 22 -j ACCEPT
>     iptables -P INPUT DROP
>     iptables -P OUTPUT ACCEPT
>     iptables -P FORWARD ACCEPT
>     iptables -A INPUT -i lo -j ACCEPT
>     #开启80端口
>     iptables -A INPUT -p tcp --dport 80 -j ACCEPT
>     iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
>     iptables -A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT
>     # 防止DDOS //不知道有效果没。
>     iptables -A FORWARD -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 1/s -j ACCEPT
>     service iptables save
>     service iptables restart


是不是觉得少了FTP端口，是的，为了安全考虑，推荐使用WinSCP代替FTP，WinSCP使用的是22端口。
