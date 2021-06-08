---
title: docker挂载nginx目录及配置
abbrlink: 3587950801
date: 2021-06-08 14:04:40
categories:
tags:
---

<meta name="referrer" content="no-referrer" />

# 挂载命令：

```shell
docker run -p 80:80 -p443:443 --name nginx \
-v /data/nginx/html:/usr/share/nginx/html \
-v /data/nginx/logs:/var/log/nginx \
-v /data/nginx/conf/:/etc/nginx \
-d nginx
```

# 配置：

## 文件配置：

```shell
# 打开文件
	location /a {
	alias /usr/local/test;
	index test.txt;
}

# 打开文件夹
location /b {
	alias /usr/local/test/;
	autoindex on;
}

# 下载文件
location /c {
	alias /usr/local/test/test.txt;
}
```

## SSL配置：

```shell
server {
    listen 443 ssl;
    server_name  www.xxx.com;

    ssl on;
    ssl_certificate      xxx.pem;
    ssl_certificate_key  xxx.key;

    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;

    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers  on;

    location / {
        root   /data/xxx/;
        index  index.html;
    }

}
```

