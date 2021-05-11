---
title: PHP安装openssl模块在wordpress中发送邮件
categories: wordpress
abbrlink: 619199573
date: 2021-05-11 11:20:55
tags:
---

 <meta name="referrer" content="no-referrer" />

# 下载WP Mail STMP插件并配置信息

![](https://wx4.sinaimg.cn/large/00724TQEgy1gn4ldjebssj30mz0ett92.jpg)**<font color="#ff0000">STMP密码填写授权码，参考：[https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=1001256](https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=1001256)</font>**


# 发送测试邮件失败


![](https://wx4.sinaimg.cn/large/00724TQEgy1gn4lejpafaj30sg0csteo.jpg)<font color="#ff0000">**这里只是说明连接不上STMP，并没有说明是什么原因造成连接不上，所以模仿发送邮件流程，进行测试**</font>
# 失败原因为缺少"openssl"

![](https://wx1.sinaimg.cn/large/00724TQEgy1gn4lf7vnx3j30f6082aab.jpg)


### **安装"openssl"**

```shell
yum install openssl 
yum install openssl-devel

# 编译php扩展
# /usr/local/php为php安装位置
/usr/local/php/bin/phpize
# 执行后，发现错误 无法找到config.m4 ，config0.m4就是config.m4，复制一份即可
cp /usr/local/php/ext/openssl/config0.m4 /usr/local/php/ext/openssl/config.m4
# 再次出错：Cannot find autoconf. Please check your autoconf installation and the $PHP_AUTOCONF environment variable. Then, rerun this script
# 安装autoconf模块再编译即可
yum install autoconf

# 配置并安装openssl
./configure --with-openssl --with-php-config=/usr/local/php/bin/php-config
make && make install
# 运行完成后最后一行会提示生成的openssl.so文件目录位置：
# Installing shared extensions: /usr/local/php/lib/php/extensions/no-debug-zts-20160303/

# 修改php.ini
vim /usr/local/php/bin/php.ini
# 添加这句：
# extension=/usr/local/php/lib/php/extensions/no-debug-zts-20160303/openssl.so

# 启动php-fpm
./php-fpm
# 依然报错缺少openssl，最后发现虽然php.ini配置完成了，但是启动时并没有用上，所以指定配置文件启动
./php-fpm -c /usr/local/php/bin/php.ini
```