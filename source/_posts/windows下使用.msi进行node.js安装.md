---
title: windows下使用.msi进行node.js安装
abbrlink: 2673616333
date: 2021-05-10 16:13:55
---

<meta name="referrer" content="no-referrer" />

nodejs下载

Node.js 安装包及源码下载地址为：[https://nodejs.org/en/download/](https://nodejs.org/en/download/)
![在这里插入图片描述](https://tvax4.sinaimg.cn/large/00724TQEgy1gqdf3weg4uj30rp0emmym.jpg)
你可以根据不同平台系统选择你需要的 Node.js 安装包。
此文章介绍windows环境下的安装：

一直执行next到安装完成：
![在这里插入图片描述](https://tva4.sinaimg.cn/large/00724TQEgy1gqdf48sui8j30h60df74x.jpg)

Node.js runtime 表示运行环境
npm package manager表示npm包管理器
online documentation shortcuts 在线文档快捷方式
Add to PATH添加到环境变量
![在这里插入图片描述](https://tva4.sinaimg.cn/large/00724TQEgy1gqdf4gyyeij30h60dfq3y.jpg)
在键盘按下【win+R】键，输入cmd，然后回车，打开cmd窗口验证：
显示版本号代表安装完成：
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdf4o0vavj30r90efdg7.jpg)
安装完成后在安装目录创建node_global及node_cache文件夹：
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdf4u0fz4j30si0fggne.jpg)
创建完两个空文件夹之后，打开cmd命令窗口，输入：
`npm config set prefix "E:\nodejs\node_global"`
`npm config set cache "E:\nodejs\node_cache"`

设置环境变量：
*进入环境变量对话框，在系统变量下新建NODE_PATH，输入E:\nodejs\node_global\node_modules，将用户变量下Path中的C:\Users\XXX\AppData\Roaming\npm修改为E:\nodejs\node_global*

安装模块进行测试：
`npm install express -g     # -g意思为全局安装`

<font color=#FF0000>报错：npm install rollbackFailedOptional: verb npm-session</font>
cmd执行`npm config set registry http://registry.npm.taobao.org`命令；

安装全局vue-cli脚手架：
cmd执行：
`cnpm install -g vue-cli  #  等待安装`
`vue   #  若出现vue信息说明表示成功`

<font color=#FF0000>cnpm不是内部命令的解决办法：</font>

系统变量中的path里加：E:\nodejs\node_global
然后退出重新打开cmd，输入`cnpm -v`

<font color=#FF0000>cnpm : 无法加载文件 E:\nodejs\node_global\cnpm.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies 解决方法：</font>
以管理员身份运行windows powershell，运行命令set-ExecutionPolicy RemoteSigned

至此，node.js安装完成。