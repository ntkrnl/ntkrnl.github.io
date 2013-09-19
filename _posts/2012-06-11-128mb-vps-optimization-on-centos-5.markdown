---
author: admin
comments: true
date: 2012-06-11 00:17:05+00:00
layout: post
slug: 128mb-vps-optimization-on-centos-5
title: 128MB VPS 上优化 CentOS 5
wordpress_id: 1091
categories:
- linux
- vps
tags:
- centos
- linux
- vps
- vps优化
---

CentOS 是一个构建在 Red Hat Enterprise Linux (RHEL) 源代码上的 Linux 发行版，并且从二进制的角度100%兼容 RHEL 软件包，简单的说 RHEL上 可以运行的软件包在 CentOS 上不需要编译就可以直接安装运行。除了少量的版权信息外，CentOS 和 RHEL 基本上一样。CentOS 是免费的，并且有着 RHEL 的稳定，因此深受各大 hosting 服务商支持，几乎所有 Linux VPS 都支持 CentOS。

一般来说如果 VPS 配置较高我会选 CentOS，配置低的话就选 Debian，当然这是个人偏好，大多数 Linux VPS 服务商也会提供 Gentoo，不过每次安装程序，升级都要编译会消耗很多资源，耗时，而且性能没有明显提高，不推荐给配置低的 VPS。VPS 服务商一般给的操作系统版本都是最小安装版本，或者优化过的版本。每个 VPS 服务商提供的版本都可能不同，安装 CentOS 的系统最低要求至少 64MB 内存（纯文字界面），1GB 硬盘空间。
<!-- more -->
安装和升级系统

1、登录 VPS 安装 CentOS 5。
2、安装完毕后马上升级整个系统。


> yum update


有了一个干净的系统以后，剩下来就是加强和优化 Linux。除不必要的软件包，服务，用户，文件等

3、删除不需要的软件包。


> yum remove Deployment_Guide-en-US finger cups-libs cups
bluez-libs desktop-file-utils ppp rp-pppoe wireless-tools irda-utils
nfs-utils nfs-utils-lib rdate fetchmail eject ksh mkbootdisk mtools
syslinux tcsh startup-notification talk apmd rmt dump setserial portmap yp-tools
ypbind



rpm -qa (列出所有安装了的包)
rpm -e package (删除某个包)
rpm -qi package (查询某个包)
rpm -qf command (根据程序查询包的名字)
rpm -ql package (查询某个包所有的安装文件)

4、删除一些不安全的软件包，并且用相应安全的软件替代，如: ssh/sftp/scp 替代 telnet, rsh, ftp, rcp
注意系统需要一个默认的 MAT，删除 Sendmail MAT 之前必须先安装一个，如: Postfix。


> yum remove telnet rsh ftp rcp
yum install postfix
yum remove sendmail
/sbin/chkconfig postfix off


5、停掉并且删除一些不需要的 xinetd 服务。


> /sbin/service xinetd stop; /sbin/chkconfig xinetd off
rm -rf /etc/xinetd.d


6、禁止一些 /etc/init.d/ 下面不需要的服务，更多信息请参考 Understanding your (Red Hat Enterprise Linux) daemons, by Len DiMaggio 和 Hardening Tips For Default Installation of Red Hat Enterprise Linux 5.


> /sbin/chkconfig --list

for a in acpid anacron apmd atd autofs avahi-daemon bluetooth cpuspeed
cups firstboot gpm haldaemon hidd ip6tables irqbalance isdn kdump
kudzumcstrans messagebus microcode_ctl netfs nfs nfslock pcscd portmap
readahead_early readahead_later rpcgssd rpcidmapd sendmail
setroublesshoot smartd xfs xinetd yum-updatesd;
do /sbin/chkconfig $a off; done


7、重启系统后，检查一下正在运行中的服务，看看是不是都是必须的。


> netstat -an | grep LISTEN
netstat -atunp


8、为了安全起见，删除一些不需要的用户。


> cp /etc/passwd /etc/passwd.sav
cp /etc/group /etc/group.sav
for a in adm lp sync news uucp operator games gopher mailnull nscd rpc;
do /usr/sbin/userdel $a -f; done
for a in lp news uucp games gopher users floopy nscd rpc rpcuser nfsnobody;
do /usr/sbin/groupdel $a -f; done



加固和优化系统

9、打开防火墙。


> system-config-securitylevel-tui


10、检查和禁止全局可写的 SUID 文件。


> find / -perm +4000 -user root -type f -print
find / -perm +2000 -group root -type f -print
chmod u-s /full/path/to/filename
chmod g-s /full/path/to/filename


11、只允许 root 在一个 terminal 上登录，如: tty1。


> vi /etc/securetty


12、避免其他用户按 Ctrl+Alt+Del 重启。


> vi /etc/inittab


注释掉


> #ca::ctrlaltdel:/sbin/shutdown -t3 -r now


13、/etc/security/console.apps/ 下面有 root 用户登录 console 后可以运行的程序，全部删除。


> rm -f /etc/security/console.apps/*


14、删除一些登录信息。


> vi /etc/issue (warning at login prompt)
vi /etc/motd (warning after successful login)


15、只运行一个 virtual terminal，如果是 VPS 的话，自己不可能物理登录终端，可以全部禁止掉。


> vi /etc/inittab
# Run gettys in standard runlevels
#1:2345:respawn:/sbin/mingetty tty1
#2:2345:respawn:/sbin/mingetty tty2
...


16、加固 SSH 安全。


> vi /etc/ssh/sshd_config
Port 2222
Protocol 2
PermitRootLogin no
PermitEmptyPasswords no
X11Forwarding no
UsePAM no
UseDNS no
AllowUsers vpsee
Banner /etc/issue


17、安装 Bastille 软件包帮助加固。


> rpm -Uvh perl-Curses-1.15-1.el5.rf.i386.rpm
rpm -ivh Bastille-3.0.9-1.0.noarch.rpm
/usr/sbin/bastille -c


18、优化 Linux 内核。


> vi /etc/sysctl.conf
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.all.accept_redirects = 0



定制 Linux 内核

19、定制，编译，安装 Linux 内核。


> yum install rpm-build ncurses ncurses-devel
rpm -ivh kernel-2.6.18-8.1.1.el5.src.rpm
cd /usr/src/redhat/SPECS
rpmbuild -bp --target i686 kernel-2.6.spec
cd /usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.i686
sed -i 's/EXTRAVERSION = -prep/EXTRAVERSION = -8.1.1.custom.el5/' Makefile
make menuconfig
make rpm
cd /usr/src/redhat/RPMS/i686
rpm -ivh kernel-2.6.18prep-1.rpm
/sbin/mkinitrd /boot/initrd-2.6.18-prep.img 2.6.18-prep (2.6.18-prep -> /lib/modules)
vi /boot/grub/menu.1st


20、修改 iptables，只允许 ssh，http 和 https 端口打开。


> /sbin/iptables -F
/sbin/iptables -A INPUT -i lo -j ACCEPT
/sbin/iptables -A INPUT -i ! lo -d 127.0.0.0/8 -j REJECT
/sbin/iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
/sbin/iptables -A OUTPUT -j ACCEPT
/sbin/iptables -A INPUT -p tcp --dport 80 -j ACCEPT
/sbin/iptables -A INPUT -p tcp --dport 443 -j ACCEPT
/sbin/iptables -A INPUT -p tcp -m state --state NEW --dport 22 -j ACCEPT
/sbin/iptables -A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT
/sbin/iptables -A INPUT -j REJECT
/sbin/iptables -A FORWARD -j REJECT


然后查看一下 iptables：


> iptables -L


更多信息


> 10 Realistic Steps to a Faster Web Site
Understanding your (Red Hat Enterprise Linux) daemons, by Len DiMaggio
Linux Server Security (2nd Edition), by Michael D. Bauer, O’Reilly
Hardening Linux, by James Turnbull, Apress
RHEL 5.0 Deployment Guide, by RedHat
RHEL 5.0 Installation Guide, by RedHat
Hardening Tips For Default Installation of Red Hat Enterprise Linux 5, by NSA
