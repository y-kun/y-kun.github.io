---
title: el-table使用sort-method进行排序
categories: element-ui
tags: element-ui
abbrlink: 1600405551
date: 2021-05-11 11:11:44
---

# 由于sort-method在Table-column Attributes中，所以应使用<font color="#ff0000">:sort-method</font>而不是@sort-method，且必须添加<font color="#ff0000">sortable</font>属性

```html
<el-table-column sortable label="客单价(元)" :sort-method="sortByPrice" min-width="100" align="center">
　<template slot-scope="scope">
　　<span v-if="scope.row.collection_amount!==0">{{ (scope.row.collection_amount/scope.row.collection_num)/100 ' moneyFilter }}　 
　　</span>
　　<span v-else>0.00</span>
　</template>
</el-table-column>
```


# 判断大小并返回 
<font color="#ff0000">踩坑：返回值应为数值，而不是boolean</font>

```javascript
// 根据客单价排序
sortByPrice(row, row1) {
　if (row.collection_amount === 0) {
　　return -1
　}
　if ((row.collection_amount / row.collection_num) < (row1.collection_amount / row1.collection_num)) {
　　return -1
　} else {
　　return 1
　}
}
```