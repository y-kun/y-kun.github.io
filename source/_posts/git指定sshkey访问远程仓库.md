---
layout: git
title: git指定sshkey访问远程仓库
date: 2021-05-11 09:12:16
categories: git
tags:
---

<meta name="referrer" content="no-referrer" />

### **在_/.ssh_目录下新建config文件，添加内容：**

```sh
# 远程仓库地址
Host "dev.wizarpos.com"
# 提供给git使用
User "git"
# 私钥文件路径
IdentityFile "C:/Users/demo/.ssh/id_rsa_wizarpos"
# 远程端口
port 30022
# 为true代表使用此配置
IdentitiesOnly yes
```

![](https://tva1.sinaimg.cn/large/00724TQEgy1gqe7xh1bk1j30cl07175z.jpg)