---
title: 基于LNMP搭建wordpress博客系统
categories: wordpress
tags:
  - linux
  - mysql
  - nginx
abbrlink: 3665250559
date: 2021-05-10 17:43:46
---

## 总体依赖安装：

```powershell
yum install -y pcre pcre-devel zlib zlib-devel openssl openssl-devel gcc gcc-c++ zlib zlib-devel openssl openssl-devel pcre pcre-devel libaio-devel libxml2 libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel libzip-devel pcre-devel
```

# 安装nginx
```shell
# 进入/usr/local目录并下载nginx安装包
cd /usr/local
wget http://nginx.org/download/nginx-1.12.1.tar.gz

# 解压、修改文件名并进入nginx目录
tar -zxvf nginx-1.12.1.tar.gz
mv nginx-1.12.1 nginx
cd nginx

# 配置
./configure --with-http_ssl_module --prefix=/usr/local/nginx

# 安装并编译
make && make install

# 创建软连接并启动
ln -s /usr/local/nginx/sbin/nginx
./nginx
```
# 安装mysql

```shell
# 下载mysql安装包
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.26-linux-glibc2.12-x86_64.tar.gz

# 解压
tar -xvf mysql-5.7.26-linux-glibc2.12-x86_64.tar

# 重命名
mv mysql-5.7.26-linux-glibc2.12-x86_64 /usr/local/mysql

# 添加用户组mysql和用户mysql,并将其添加到mysql用户组中
# useradd -r参数表示mysql用户是系统用户，不可用于登录系统 
# useradd -g参数表示把mysql用户添加到mysql用户组中
groupadd mysql
useradd -r -g mysql mysql

# 创建数据目录并赋予权限
mkdir -p /data/mysql
chown mysql:mysql -R /data/mysql

# 配置my.cnf
vim /etc/my.cnf
# 将内容修改为：
[mysqld]
bind-address=0.0.0.0
port=3306
user=mysql
basedir=/usr/local/mysql
datadir=/data/mysql
socket=/tmp/mysql.sock

[mysqld_safe]
user=mysql
log-error=/data/mysql/mysql.err
pid-file=/data/mysql/mysql.pid

# 进入mysql的bin目录并初始化（需记住输出日志末尾的密码）
cd /usr/local/mysql/bin/
./mysqld --defaults-file=/etc/my.cnf --basedir=/usr/local/mysql/ --datadir=/data/mysql/ --user=mysql --initialize

# 将mysql.server放置到/etc/init.d/mysql中
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql

# 启动mysql服务
service mysql start

# 进入mysql（密码为初始化时生成的临时密码）
mysql -u root -p 临时密码
```

如运行报错：<font color="#ff0000">Access denied for user 'root'@'localhost'</font>：
修改_/etc/my.cnf：[mysqld]中添加 skip-grant-tables 即可（此命令为跳过权限验证）

```shell
# 修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;

# 创建用户并添加权限提供给远程连接使用
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;

# 刷新权限
flush privileges;
```


# 安装PHP

```shell
# 下载PHP安装包
wget https://www.php.net/distributions/php-7.3.3.tar.gz

# 解压重命名并进入php目录
tar -zxzf php-7.3.3.tar.gz
mv php-7.3.3 php
cd php-7.3.3

# 配置
./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-config-file-scan-dir=/usr/local/php/etc/php.d --with-mcrypt=/usr/include --enable-mysqlnd --with-mysqli --with-pdo-mysql --enable-fpm --with-fpm-user=nginx --with-fpm-group=nginx --with-gd --with-iconv --with-zlib --enable-xml --enable-shmop --enable-sysvsem --with-curl

# 编译并安装
make && make install

# 复制配置文件并修改文件名
cp php.ini-production /usr/local/php/bin/php.ini
cd /usr/loacl/php/etc/
cp php-fpm.conf.default php-fpm.conf
cd /usr/local/php/etc/php-fpm.d
cp www.conf.default www.conf

# 修改用户和用户组
vim /usr/local/php/etc/php-fpm.d/www.conf
user = 当前用户
group = 当前用户组

# 配置nginx，使其支持php
location ~ .php$ {
root html;
fastcgi_pass 127.0.0.1:9000;
fastcgi_index index.php;
fastcgi_param SCRIPT_FILENAME /$document_root$fastcgi_script_name;
include fastcgi_params;
}

# 创建软连接并启动
ln -s /usr/local/php/sbin/php-fpm
./php-fpm
```


# 安装wordpress

```shell
# 下载wordpress
wget https://cn.wordpress.org/wordpress-5.4-zh_CN.tar.gz

# 解压并复制wordpress到nginx根目录下
tar -zxvf wordpress-4.8.1-zh_CN.tar.gz
cp -R wordpress /nginx/html

# 复制配置文件
cd nginx/html/wordpress/
cp wp-config-sample.php wp-config.php

# 修改配置文件
vim wp-config.php
# 配置数据库信息：
/** WordPress数据库的名称 */
define('DB_NAME', 'wpdb');
/** MySQL数据库用户名 */
define('DB_USER', 'wpadmin');
/** MySQL数据库密码 */
define('DB_PASSWORD', 'pass');
/** MySQL主机 */
define('DB_HOST', 'localhost');
/** 创建数据表时默认的文字编码 */
define('DB_CHARSET', 'utf8');

# 进入mysql并创建wordpress数据库及用户
mysql -u root -p
create database wpdb character set utf8;
grant all privileges on wpdb.* to 'wpadmin'@'localhost' identified by 'pass';
flush privileges;
```
## 打开浏览器完成wordpress配置：xxx.xxx.xxx.xxx/wordpress/wp-admin/install.php，输入网站名称、管理帐号、密码、邮箱

安装报错：<font color="#ff0000">无法建立目录wp-content/uploads/2020/04。有没有上级目录的写权限？</font>
设置wordpress目录下wp-content的权限即可：

```shell
chmod 777 -R /usr/local/nginx/html/wordpress/wp-content/
```


#### 安装插件需要ftp服务解决方法：

```shell
# wordpress安装目录 ==> wp-config.php,文件末尾添加以下代码：
vim /usr/local/nginx/html/wordpress/wp-config.php

define("FS_METHOD","direct"); 
define("FS_CHMOD_DIR", 0777); 
define("FS_CHMOD_FILE", 0777);
```

<font color="#ff0000">Tips：如想去掉xx.xx.xx.xx/wordpress的wordpress：</font>

```shell
# 复制wordpress目录下的index.php到nginx/html目录下，
# 修改nginx/html/index.php：
require DIR . '/wp-blog-header.php';
# 改为
require DIR . '/wordpress/wp-blog-header.php';
```