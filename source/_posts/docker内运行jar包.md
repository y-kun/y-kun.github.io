---
title: docker内运行jar包
abbrlink: 368443741
date: 2021-06-08 14:56:58
categories:
tags:
---

<meta name="referrer" content="no-referrer" />

创建一个自定义网络（单机项目可以不需要创建，自定义网络用于feign调用时走内网）：

```shell
docker network create --subnet=172.18.0.0/16 docker-net(自定义网络名称)
```

运行jar包：

```shell
docker run -d -p 8108:8108 -e TZ=Asia/Shanghai \
-v /home/jar/xxx.jar:/home/xxx.jar \
-v /data/jar/logs:/data/logs \
--name xxx \
--net docker-net --ip 172.18.0.2 java:8 java -jar /home/jar/xxx.jar
# 如果未创建自定义网络，--net docker-net可以去掉
```

