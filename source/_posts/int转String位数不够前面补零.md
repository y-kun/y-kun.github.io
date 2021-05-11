---
title: int转String位数不够前面补零
categories: java
abbrlink: 421069899
date: 2021-05-11 09:08:33
tags:
---

**<font color="#ff0000">String.format("%09d", 25);</font>** 
0代表前面要补的字符
9代表字符串长度
d表示参数为整数类型
运行结果为：000000025