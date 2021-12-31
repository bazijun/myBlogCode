---
title: html-高级
layout: post
sticky: 0
hide: false
categories:
  - 前端
tags:
  - html
date: 2021-12-31 13:49:02
---
# HTML 高级

### 1. img 标签 引入 二维码

> 二维码都是 base64编码的

所以 **src** 属性该这样写

```html
<img src="data:image/png;base64,qrCode"/>
```
