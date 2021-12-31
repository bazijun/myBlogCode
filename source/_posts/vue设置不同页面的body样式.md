---
title: vue设置不同页面的body样式
layout: post
sticky: 0
hide: false
categories:
  - 前端
tags:
  - vue
date: 2021-12-31 15:01:20
---
### vue设置不同 页面的 body样式

> 由于vue 是单页面应用，所有想要不同页面不同背景色，只能可以组件中动态设置

##### 方法一 (推荐)
* 使用组件独享路由钩子来设置 当前path下页面的 body样式
``` javascript
//... 组件实例中
  beforeRouteEnter (to, from, next) {
    // 添加背景色，此钩子无法获取实例this
    document.querySelector('body').setAttribute('style', 'background-color:#F4F4F4')
    next()
  },
  beforeRouteLeave (to, from, next) {
    // 去除背景色
    document.querySelector('body').setAttribute('style', '')
    next()
  },
```
##### 方法二
* 在组件生命周期中设置
``` javascript
beforeCreate () { 
    document.querySelector('body').setAttribute('style','background-color:rgb(245,245,245)')
},

beforeDestroy () { 
    document.querySelector('body').setAttribute('style', "background-color:''")
}
```
