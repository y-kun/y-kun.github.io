---
title: vue-element-template登录流程
categories: vue
tags: [vue,element-ui]
abbrlink: 1374621978
date: 2021-05-11 09:09:57
---

<meta name="referrer" content="no-referrer" />

# src/view/login/index.vue

```javascript
handleLogin() {
　this.$refs.loginForm.validate(valid => {
　　if (valid) {
　　　this.loading = true
　　　this.$store.dispatch('user/login', this.loginForm).then(() => {
　　　　　this.$router.push({ path: this.redirect '' '/' })
　　　　　this.loading = false
　　　　}).catch(() => {
　　　　　this.loading = false
　　　　})
　　} else {
　　　console.log('error submit!!')
　　　return false
　　}
　})
}
```


# this.$store.dispatch('user/login', this.loginForm)　--->　src/store/modules/user.js

```javascript
import { Login, logout, getUserInfo } from '@/api/user'
login({ commit }, userInfo) {
　const { username, password } = userInfo
　return new Promise((resolve, reject) => {
　　login({ username: username.trim(), password: password }).then(response => {
　　　const { data } = response
　　　commit('SET_TOKEN', data.token)
　　　setToken(data.token)
　　　resolve()
　　}).catch(error => {
　　　reject(error)
　　})
　})
}
```

# import { Login, logout, getUserInfo } from '@/api/user'　--->　src/api/user.js

```javascript
export function login(data) {
　return request({
　　url: '/user/login',
　　method: 'post',
　　data
　})
}
```

# src/utils/request.js
### 注意：**<font color="#ff0000">if (res.code !== 20000)</font>**　code需改为后端返回的值

```javascript
response => { 
　const res = response.data 
	// if the custom code is not 20000, it is judged as an error. 
　　if (res.code !== 20000) {   
　　　Message({     
　　　　message: res.message '' 'Error',     
　　　　type: 'error',     
　　　　duration: 5 * 1000   
　　　})   
　　　// 50008: Illegal token; 50012: Other clients logged in; 50014: Token expired;  
　　　if (res.code === 50008 '' res.code === 50012 '' res.code === 50014) {     
　　　　// to re-login     
　　　　MessageBox.confirm('You have been logged out, you can cancel to stay on this page, or log in again', 'Confirm logout', {       
　　　　　confirmButtonText: 'Re-Login',       
　　　　　cancelButtonText: 'Cancel',       
　　　　　type: 'warning'     
　　　　}).then(() => {       
　　　　　store.dispatch('user/resetToken').then(() => {         
　　　　　　location.reload()       
　　　　　})     
　　　　})   
　　　}   
　　　return Promise.reject(new Error(res.message '' 'Error')) 
　　} else {   
　　　return res 
　　} 
　}, 
　error => { 
　console.log('err' + error) // for debug 
　Message({ message: error.message, 
　　type: 'error', 
　　duration: 5 * 1000 
　}) 
　return Promise.reject(error) 
}
```