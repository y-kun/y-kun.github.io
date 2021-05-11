---
title: jmeter address already in use
abbrlink: 2408300312
date: 2021-05-11 11:16:01
categories:
tags:
---

<font color="#ff0000">原因：windows本身提供的端口访问机制问题  
windows提供给TCP/IP链接的端口为1024-5000，并且要四分钟来循环回收他们。就导致在短时间内跑大量请求将端口占满。</font>

解决：

 1. cmd中，用regedit打开注册表
2.  在HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters下：
	1. 右击parameters，添加一个新的DWORD，名字为MaxUserPort
	2. 然后双击MaxUserPort，输入数值数据为65534，基数选择十进制如果是分布式运行的话，控制机器和负载机器都需要这样操作哦）
	3. 修改配置完毕之后记得重启机器才会生效

<font color="#ff0000">tips：另一个 TCPTimedWaitDelay 注册表参数确定关闭的端口等待多长时间才能重用关闭的端口。</font>

windows官方链接：[https://docs.microsoft.com/zh-cn/troubleshoot/windows-client/networking/connect-tcp-greater-than-5000-error-wsaenobufs-10055](https://docs.microsoft.com/zh-cn/troubleshoot/windows-client/networking/connect-tcp-greater-than-5000-error-wsaenobufs-10055)