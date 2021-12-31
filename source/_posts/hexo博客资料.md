---
title: hexo博客资料
layout: post
sticky: 0
hide: false
categories:
  - 网络
tags:
- 资料
date: 2021-12-31 15:20:36
---


#### 资源

>[`教程`](https://blog.csdn.net/sinat_37781304/article/details/82729029?spm=1001.2014.3001.5506)
> [官网](https://hexo.io/zh-cn/)

* 插件

>[fluid主题库](https://github.com/fluid-dev/hexo-theme-fluid) ==》 [配套文档](https://hexo.fluid-dev.com/docs/guide/#%E5%85%B3%E4%BA%8E%E6%8C%87%E5%8D%97) ==》 该ui框架已经集成搜索组件  hexo-generator-search，不要重复添加。

>[评论组件](https://valine.js.org/quickstart.html#npm)


>搜索组件 ：`npm install hexo-generator-json-content`


#### hexo deploy 的 说明
>hexo deploy 命令可以根据 `__config.yml` 中的 deploy 下的 repo 指定的仓库地址来部署网站，并且会自动连接该仓库，并自动push文件。

[Gitee(码云)、Github同时配置ssh key](https://blog.csdn.net/qq_40323256/article/details/104091775)
[论git中使用https和ssh协议的区别](https://blog.csdn.net/jfkidear/article/details/90376815)

#### 注意点
* 公司的只支持 ssh协议的连接，所以 repo只能写 ssh地址
* hexo 部署到 仓库的不是hexo源代码，就是和普通push不一样，而是整理打包后的html+css+img+静态资源，其实就是一个启动网站的真实代码。
* hexo 部署 老实使用 `hexo clean` + `hexo g` + `hexo d`  不然容易资源不同步, 但也可能是缓存问题。稍等片刻

#### 知识点
* hexo 使用 `hexo new bolg` 后一定要使用 生成器 `hexo -g`渲染博客，不然部署后啥都没变。
* hexo 有三种 layout 布局方式, 主要的是 post， 通过 `hexo new blogname` 就会自动在`source/_posts` 下创建md。然后就是 `page` 使用 `hexo new page pagename` 会在 `source/` 单独创建 page 文件夹。访问会通过 `域名url/pagename`  **一般侧边栏和导航栏的选项会使用到 page**， 还有一种 layout 是草稿 
draft, 不介绍
* `scaffolds` 模板中 可以预置各layout创建后 **Front-matter**  
* 主题配置完后 需要 重新开启一次服务器 (`hexo s`)。


