---
title: el-date-picker设置默认日期
categories: element-ui
tags: element-ui
abbrlink: 3812763588
date: 2021-05-11 11:12:50
---

```javascript
// js变量
start_date: [new Date(Date.now()), new Date(Date.now())]
```


```html
<el-date-picker
　v-model="defaultDate"
　type="daterange"
　align="right"
　unlink-panels
　range-separator="--"
　start-placeholder="开始日期"
　end-placeholder="结束日期"
　:picker-options="pickerOptions"
　format="yyyy-MM-dd"
/>
```


```javascript
// 把yyyy/MM/dd转为yyyy-MM-dd
start_date[1].toLocaleDateString().replace(/\//g, '-')
```