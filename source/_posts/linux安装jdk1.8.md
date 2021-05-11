---
title: linux安装jdk1.8
categories: java
tags: [java,linux]
abbrlink: 3542552830
date: 2021-05-10 16:38:07
---

```powershell
# 进入到local目录，创建java文件夹并把jdk解压到该目录下
[root@shmily ~]# cd /usr/local
[root@shmily local]# mkdir java
[root@shmily local]# tar -zxvf jdk-8u161-linux-x64.tar.gz -C java
# 配置环境变量
[root@shmily local]# vim /etc/profile
# 文件末尾添加内容：

export JAVA_HOME=/usr/local/java/jdk1.8.0_161
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
export PATH=$PATH:${JAVA_PATH}

# 执行命令使配置生效：
[root@shmily local]# source /etc/profile
# 查看jdk是否安装完成：
[root@shmily local]# java -version
```