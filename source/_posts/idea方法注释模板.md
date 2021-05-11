---
title: idea方法注释模板
categories: java
tags: 开发工具
abbrlink: 3159180473
date: 2021-05-10 17:28:14
---

<meta name="referrer" content="no-referrer" />

<font color="#ff0000">File-->Settings-->Editor-->Live Templates</font>
![在这里插入图片描述](https://tvax1.sinaimg.cn/large/00724TQEgy1gqdgvm388zj30yp0jzq54.jpg)
<font color="#ff0000">新建组名</font>
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdgvyow1oj30ag041mx1.jpg)
<font color="#ff0000">设置模板内容</font>![在这里插入图片描述](https://tva3.sinaimg.cn/large/00724TQEgy1gqdgw6w0ccj30yp0jz76v.jpg)

```bash
 * 
 * TODO
 * 
 * @param $param$
 * @return $return$
 * @author $USER$
 * @since $DATE$ $TIME$
 **/
```
<font color="#ff0000">设置模板的应用场景</font>
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdgweg1ozj30yp0jzn0g.jpg)
<font color="#ff0000">设置参数的获取方式</font>
![在这里插入图片描述](https://tva1.sinaimg.cn/large/00724TQEgy1gqdgwjre9dj307t053mx2.jpg)
![在这里插入图片描述](https://tva3.sinaimg.cn/large/00724TQEgy1gqdgwsqhnjj30fd07k3yy.jpg)
<font color="#ff0000">使用这种方法生成的注释参数类型为：</font>
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdgx30jx3j307s057jrd.jpg)
<font color="#ff0000">如果想去除中括号，修改：</font>
![在这里插入图片描述](https://tvax3.sinaimg.cn/large/00724TQEgy1gqdgx8ydusj30ff07m3yz.jpg)

```bash
groovyScript("def result=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList(); for(i = 0; i < params.size(); i++) {
if(i!=params.size()-1) result+= params[i]+',';
else{result+= params[i];return result;}
}; return result", methodParameters())
```