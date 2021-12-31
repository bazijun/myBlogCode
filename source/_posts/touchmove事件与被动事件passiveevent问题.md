---
title: touchmove事件与被动事件passiveevent问题
layout: post
sticky: 0
hide: false
categories:
  - 前端
tags:
  - javascript
  - 踩坑
date: 2021-12-31 15:40:53
---

# touchmove事件 与 被动事件(passive event) 问题

[TOC]

![报错信息](https://cdn.bazijun.top/img/20211231154153.png)




**产生原因：**

1. 条件1：使用监听事件时候，第三个参数配置了passive为true(说明指定了这个监听为一个被动监听)

   ```javascript
   window.addEventListener("touchmove", handler, { passive: true });
   ```

2. 条件2：上条件中的被动监听的handler中调用了

```javascript
    
    function handler() {
        //阻止默认事件，如点击<a>标签阻止其默认跳转事件
        event.preventDefault();
        //其他逻辑...
    }
```
**上述两个条件同时成立的时候，就会报标题中错误或警告。**

 

**本质：**
谷歌浏览器对event.preventDefault()（默认事件阻止）的检测机制变化导致的（听不懂？直接看下面）。

`老版本`：当用户触发我们定义的监听事件时候（如条件1中的“touchmove”事件），浏览器会主动检测对应的handler代码中是否有event.preventDefault(),以便进行默认事件阻止。但是这样做会增加响应时间，用户体验受到影响；

`新版本`： 

>  默认不再检测event.preventDefault()，直接响应用户操作。这相当于把我们定义的事件监听都设置成了被动事件监听。具体代码就是：

```javascript
window.addEventListener("touchmove", handler);
window.addEventListener("touchmove", handler, { passive: true });
```


上面两个代码效果相同，我们经常用第一条，不知不觉中定义了一个被动监听事件。

那么问题就来了，**我们不知道我们的事件已经默认被定义为了被动事件监听。结果我们在这个事件监听中调用了event.preventDefault()，浏览器就不高兴了，导致报错**，告诉你：

“你定义的事件不是一个被动事件监听吗？不就是告诉我为了提高响应速度不要处理event.preventDefault()吗？为啥你还要调用event.preventDefault()！”

看了我们已经找到问题所在了。

**总结：** 被动事件监听不能调用event.preventDefault()。

值得说的是： Passive Event Listeners特性当前仅支持mousewheel/touch相关事件。

---



#### 解决办法：
1、声明事件监听的时候设置为主动事件监听：

```javascript
window.addEventListener(‘touchmove’, handler, { passive: false})；
```

2、设置监听事件绑定的dom的CSS为：

``` css
touch-action:none
```

表示当触控事件发生在绑定的dom上时，不进行任何操作。

#### 引申：

在解决下图出现的警告时，通常使用 *default-passive-events* 包。可以解决。

> 该问题主要是因为 chrome51后 google为了滚动等事件的性能，所有的事件都需要默认绑定 被动监听器了，但element中并没有绑定，所有会抛出警告。


​	*default-passive-events* 包，可以通过修改事件的 passive 设置为 true, 解决这个警告。又因为element是在事件监听器的callback(handler)中使用`event.preventDefault()`清除默认事件的。所有就完全成全了上述的 `报错的产生原因`，导致上述的**报错**。所以在使用element组件时不建议再用 *default-passive-events* 包。警告就警告吧。





**ps:**

关于touch-action还有很多设置，我也在学习中。

本文参考了https://blog.csdn.net/lijingshan34/article/details/88350456和https://juejin.im/post/5ad804c1f265da504547fe68。理解上不对之处欢迎指出。
