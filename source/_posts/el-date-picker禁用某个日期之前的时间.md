---
title: el-date-picker禁用某个日期之前的时间
categories: element-ui
tags: element-ui
abbrlink: 1302172676
date: 2021-05-10 17:52:17
---

```html
<el-date-picker
　v-model="show.endTime"
　type="date"
　:placeholder="$t('time.endTime')"
　value-format="yyyy-MM-dd"
　:picker-options="pickerOptions"
/>
```

```javascript
data() {
return {
　pickerOptions: {
　　disabledDate: (time) => {
　　　return time.getTime() < new Date(this.startTime).getTime() + 8.64e7
　　}
　}    
}
```

<font color="#ff0000">ps：return&nbsp;time.getTime()&nbsp;<&nbsp;new&nbsp;Date(this.startTime).getTime()&nbsp;+&nbsp;8.64e7</font> 代表只能选择this.startTime之后的时间，并且this.startTime这天不能选择 (8.64e7：科学计数法，代表8.64×10的7次方)