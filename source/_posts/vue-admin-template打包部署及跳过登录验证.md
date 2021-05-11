---
title: vue-admin-template打包部署及跳过登录验证
categories: vue
tags:
  - vue
  - element-ui
abbrlink: 1908717661
date: 2021-05-11 10:55:27
---

<meta name="referrer" content="no-referrer" />

# 修改vue.config.js

![](https://wx4.sinaimg.cn/large/00724TQEgy1gn4nm3pr2yj30eu08sjrp.jpg)
<font color="#ff0000">**将publicPath的值改为'./'(设置打包后的静态资源为相对路径,避免加载不到css、js导致页面白屏)**  
**outputDir：打包后的文件夹名**</font>**<font color="#ff0000">
assetsDir：打包后的静态资源文件夹名</font>**


# 三个文件中的<font color="#ff0000">VUE_APP_BASE_API</font>改为自己的请求地址

![](https://wx1.sinaimg.cn/large/00724TQEgy1gn4nmw56m1j30l3098wet.jpg)
# 修改登录请求接口

![](https://wx3.sinaimg.cn/large/00724TQEgy1gn4nng5mvoj30jt0ekt9q.jpg)

# 注释掉<font color="#ff0000">src/main.js</font>中此段代码

![](https://wx4.sinaimg.cn/large/00724TQEgy1gn4nnzxf4hj30gm08f0t0.jpg)
<span style="color:#ff0000">不使用mock数据，使用自己的接口数据</span>

# 修改<font color="#ff0000">util/request.js</font>中的code判断，改为自己后端返回的code

![](https://wx1.sinaimg.cn/large/00724TQEgy1gn4nol5glsj30gv0a4t95.jpg)

# 如需跳过登录直接进入dashboard页面，将<font color="#ff0000">/src/permission.js</font>**中的**<font color="#ff0000">hasToken</font>直接赋值为<font color="#ff0000">true</font>即可(即if判断为true)

![](https://wx1.sinaimg.cn/large/00724TQEgy1gn4np3q6d2j30gb0aiaaj.jpg)