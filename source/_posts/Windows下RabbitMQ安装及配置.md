---
title: Windows下RabbitMQ安装及配置
categories: java
abbrlink: 1589426423
date: 2021-05-10 17:41:49
tags:
---

<meta name="referrer" content="no-referrer" />

<div id="article_content" class="article_content clearfix">
            <link rel="stylesheet" href="https://csdnimg.cn/release/phoenix/template/css/ck_htmledit_views-211130ba7a.css">
            <br/>
           <div>本文转自：<a href="https://blog.csdn.net/zhm3023/article/details/82217222">https://blog.csdn.net/zhm3023/article/details/82217222</a></div>
                       <br/>
           <div/>
                            <div class="htmledit_views" id="content_views">
                                            <p>rabbitMQ是一个在AMQP协议标准基础上完整的，可服用的企业消息系统。它遵循Mozilla Public License开源协议，采用 Erlang 实现的工业级的消息队列(MQ)服务器，Rabbit MQ 是建立在Erlang OTP平台上。</p>


<p>1、安装Erlang</p>

<p>下载地址：<a href="https://www.erlang.org/downloads" rel="nofollow">https://www.erlang.org/downloads</a>，本文选择<a href="http://erlang.org/download/otp_win64_21.0.1.exe" rel="nofollow">OTP 21.0.1 Windows 64-bit Binary File&nbsp;</a>(91707927)</p>

<p>设置环境变量，新建ERLANG_HOME</p>

<p><img alt="" class="has" height="134" src="https://img-blog.csdn.net/2018083010261937?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="350"></p>

<p>修改环境变量path，增加Erlang变量至path，%ERLANG_HOME%\bin;</p>

<p>打开cmd命令框，输入erl</p>

<p><img alt="" class="has" height="184" src="https://img-blog.csdn.net/20180830102843667?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="489"></p>

<p>至此，Erlang 安装完成</p>

<p>2、安装rabbitmq</p>

<p>下载地址：<a href="http://www.rabbitmq.com/download.html" rel="nofollow">http://www.rabbitmq.com/download.html</a></p>

<p>exe安装地址：<a href="http://www.rabbitmq.com/install-windows.html" rel="nofollow">http://www.rabbitmq.com/install-windows.html</a></p>

<p>解压缩安装地址：<a href="http://www.rabbitmq.com/install-windows-manual.html" rel="nofollow">http://www.rabbitmq.com/install-windows-manual.html</a></p>

<p>本文选择解压缩安装<a href="https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.7/rabbitmq-server-windows-3.7.7.zip" rel="nofollow">rabbitmq-server-windows-3.7.7.zip</a></p>

<p>将<a href="https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.7/rabbitmq-server-windows-3.7.7.zip" rel="nofollow">rabbitmq-server-windows-3.7.7.zip</a>解压缩至D:\Program Files目录下</p>

<p>设置环境变量，新建RABBITMQ_SERVER</p>

<p><img alt="" class="has" height="139" src="https://img-blog.csdn.net/20180830103603987?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="350"></p>

<p>修改环境变量path，增加rabbitmq变量至path，%RABBITMQ_SERVER%\sbin;</p>

<p>打开cmd命令框，切换至D:\Program Files\rabbitmq_server-3.7.7\sbin目录下，输入rabbitmqctl status</p>

<p><img alt="" class="has" height="602" src="https://img-blog.csdn.net/20180830103803858?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="664"></p>

<p>说明rabbmitmq未启动，继续下面操作。</p>

<p>安装插件，命令：rabbitmq-plugins.bat enable rabbitmq_management,出现：</p>

<p><img alt="" class="has" height="231" src="https://img-blog.csdn.net/20180830104340321?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="669"></p>

<p>解决方法：&nbsp;<br>
将 C:\Users\Administrator\.erlang.cookie 同步至C:\Windows\System32\config\systemprofile\.erlang.cookie&nbsp;</p>

<p>同时删除：C:\Users\Administrator\AppData\Roaming\RabbitMQ目录</p>

<p>输入命令：rabbitmq-plugins.bat enable rabbitmq_management ，出现下面信息表示插件安装成功：</p>

<p><img alt="" class="has" height="332" src="https://img-blog.csdn.net/20180830104802723?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="676"></p>

<p>输入命令：rabbitmq-server.bat</p>

<p><img alt="" class="has" height="293" src="https://img-blog.csdn.net/20180830105821133?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="673"></p>

<p>rabbitmq启动成功，浏览器中<a href="http://localhost:15672" rel="nofollow">http://localhost:15672</a>，</p>

<p><img alt="" class="has" height="475" src="https://img-blog.csdn.net/20180830104928623?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="962"></p>

<p>输入guest,guest进入rabbitMQ管理控制台：</p>

<p><img alt="" class="has" height="794" src="https://img-blog.csdn.net/20180830105034225?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="1200"></p>

<p>打开cmd，再次输入命令：rabbitmqctl status</p>

<p><img alt="" class="has" height="1010" src="https://img-blog.csdn.net/20180830105147926?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pobTMwMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="664"></p>

<p>至此，rabbitMQ安装部署完成。</p>