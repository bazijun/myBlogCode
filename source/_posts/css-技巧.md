---
title: css-技巧
layout: post
categories:
  - 前端
tags:
  - css
  - 技巧
date: 2021-12-31 10:13:07

---


# css 技巧


### 隐藏input 输入后的背景色


![如图](https://cdn.bazijun.top/img/20211231103838.png)
* **方法一**
在html中为form标签添加属性 autocomplete="off"

> `autocomplete` 属性适用于 `<form>`，以及 `<input>`中以下 类型：text, search, url, telephone, email, password, datepickers, range 以及 color。
>* ` 就是控制是否显示 账号密码的历史记录下拉菜单`

 ``` html
<form method="post" autocomplete="off">

/* 或在 input 中设置 */

<input autocomplete="off" type="text" name="username" placeholder="请输入用户名">
```

* **方法二**
设置 css
``` css

input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill{
  -webkit-box-shadow: 0 0 0px 1000px #fff inset /* 背景色是什么，设置相同颜色，这里body的默认背景色是白色 */
}
```


### icon(图标动效)

效果为 点击 图标 旋转方向。需要动态绑定 class实现。

``` css
.arrow-up{ // 图标向上
  transform: rotate(180deg);
  transition: all 0.5s;
}
.arrow-up:hover{
  cursor: pointer;
}
.arrow-down{ // 图标向下
  transform: rotate(360deg);
  transition: all 0.5s;
}
.arrow-down:hover{
  cursor: pointer;
}
```


