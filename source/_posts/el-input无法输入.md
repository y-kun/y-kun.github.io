---
title: el-input无法输入
categories: element-ui
tags: element-ui
abbrlink: 3501428516
date: 2021-05-10 17:50:24
---

# 添加_@input_事件

```html
<el-input v-model="show.points" style="width:160px;" @input="change($event)" />
```

# 监听输入事件，在输入时强制刷新

```javascript
change(e) {
	this.$forceUpdate()
}
```