---
title: vue脚手架搭建项目
categories: vue
abbrlink: 1451956170
date: 2021-05-11 11:17:25
tags:
---

vue init webpack <font color="#ff0000">demo</font>（项目名小写）

```shell
Project name # 项目名：默认为上一步"webpack demo"中的demo

Project description # 项目介绍：默认 A Vue.js project

Author # 作者名

Vue build（Use arrow keys）
　Runtime + Compiler：recommended for most users # 运行加编译
　Runtime-only：about 6KB lighter min+gzip，but templaters（or any Vue-spcific HTML）are ONLY allowed in .Vue files - render functions are required elsewhere # 仅运行

Install vue-router ? （Y/n） # 安装Vue路由

Use ESLint to lint your code ? （Y/n） # 使用ESlint对代码进行校验

Pick an ESLint preset (Use arrow keys) # 选择ESLint预设，编写vue项目时的代码风格
　Standard (https://github.com/standard/standard)　# Standard
　Airbnb (https://github.com/airbnb/javascript) # Airbnb
　none (configure it yourself) # 自己配置

Set up unit tests （Y/n） # 使用单元测试

Setup e2e tests with Nightwatch？ （Y/n） # 使用e2e测试

Should we run npm install fr you after the project has been created?（recommended）（Use arrow keys）
　Yes，use Npm # 使用npm
　Yes，use Yarn # 使用yarn
　No，I whill handle that myself # 自己配置
```


cd demo


npm install


安装element-ui，可选

```shell
npm install element-ui -S
```


安装scss，可选

```shell
# 安装node-sass
npm install node-sass --save-dev
# 安装sass-loader
npm install sass-loader --save-dev
# 在build/webpack.base.conf.js文件中的rules模块中添加：
{
　test: /\.scss$/,
　loaders: ['style', 'css', 'sass']
}
```


安装scss后启动报错：
<font color="#ff0000">Node Sass version 5.0.0 is incompatible with ^4.0.0.</font>
解决：

```shell
# 卸载原sass
npm uninstall node-sass
# 重新安装 4.X.X 版本的sass
npm install node-sass@4.14.1

```