---
title: Error response from daemon service endpoint with name xxx already exists.
categories: docker
abbrlink: 710246348
date: 2021-05-11 11:14:27
tags:
---

<font color="#ff0000">原因：容器被删除，网络仍在占用</font>


解决：

```shell
# 删除容器
docker rm -f 容器ID
# 查看容器的网络占用情况
docker network inspect 网络模式（例：bridge）
# 清理此容器的网络占用
docker network disconnect --force 网络模式（例：bridge） 容器名称（例：mysql）
# 检查是否还有同名容器占用
docker network inspect 网络模式
# 重新构建容器
```