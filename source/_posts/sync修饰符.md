---
title: sync修饰符
layout: post
sticky: 0
hide: false
categories:
  - 前端
tags:
  - vue
date: 2021-12-31 14:59:53
---
## sync修饰符

>主要用于**双向绑定父子组件的props**，简化其代码量。子组件只用$emit，父组件不必绑定自定义事件，只需在传递的props后加上 .sync修饰符即可响应子组件的变化。

- [sync修饰符](#sync修饰符)
    - [子组件](#子组件)
      - [注意！](#注意)
    - [父组件](#父组件)
      - [参考:](#参考)
    - [子组件](#子组件)
      - [注意！](#注意)
    - [父组件](#父组件)
      - [参考: 使用.sync修饰符【Vue小技巧】](#参考-使用sync修饰符vue小技巧)

#### 子组件
* template
``` html
<div class="box">
  <div>当前标题： {{name}}</div>
  <div>当前内容： {{content}}</div>
  <div>||</div>
  <button @click="changeName">点击改变标题</button>
  <button @click="changeContent">点击改变内容</button>
</div>
```
* methods
``` javaScript
methods: {
    changeName () {
      this.$emit('update:name', '标题已改变')
    },
    changeContent () {
      this.$emit('update:content', '内容已改变')
    }
  }

```
  
 ##### 注意！
  
> 子组件的 `$emit` 绑定的事件名，不能随意命名，必须使用 `update:props` 的方式
<br/>

#### 父组件
* 绑定事件再改变props的值
``` html
<csync
  :name="name"
  :content="content"
  @update:name="name = $event"
  @update:content="content = $event"
></csync>
```

* 使用 `.sync` 修饰符，同样的效果！一步到位！
``` html
<div>
  <csync
  :name.sync="name"
  :content.sync="content"
  ></csync>
</div>
```
* 在传递的props为**对象**的时候 `sync` 由为巴适，例如在父组件中使用事件绑定的方式:
``` html
<csync
  :name="obj.name"
  :content="obj.content"
  @update:name="obj.name = $event"
  @update:content="obj.content = $event"
></csync>
```
* 而使用  `v-bind` 加 `sync` 修饰符，就是一步到位，同样的效果
``` html
<csync v-bind.sync="obj"></csync>
```
子组件是一直未有改变的，子组件中没有接收名为 obj 的 props， 接收的仅是 obj 的属性。

---
##### 参考: 
[使用.sync修饰符《Vue小技巧》](https://www.bilibili.com/video/BV1iL411J76u)

