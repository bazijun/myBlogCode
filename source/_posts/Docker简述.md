---
title: Docker简述
layout: post
sticky: 0
hide: false
categories:
  - 网络
tags:
  - 服务器
date: 2021-12-31 16:10:30
---

## docker

> docker可以理解成一个集装箱，里面有各种服务和环境。不必考虑里面装了什么，只在要有docker的主机上，就可以运行docker镜像，移植性强。

[CentOS中安装docker](https://www.jianshu.com/p/3771b155283b)

### node.js 和 nginx 和 docker 的区别

* node.js 是js的运行环境，跑js代码的。“Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行时”

* nginx用来做代理和静态资源托管，可以代理node.js起的http服务。


* docker可以认为是虚拟机，虚拟机里可以安装node.js或者nginx。**是一种类似容器的东西**，里面可以配置各种nginx和node.js此类的服务。拥有移植性。


> 联系：写了一个node.js项目，提供api;写了一个vue项目，打包成静态资源（需要api接口）。nginx做代理，将node.js提供的api和vue的静态资源整合到一个域名底下。
可以将node.js项目打包成一个docker镜像（有node.js环境和代码的一个虚拟机），这样我拿着这镜像可以随意的部署到任何一台有安装过docker的机子上。不需要考虑我这机子上有没有安装过node.js。

### 命令
启动 docker =>  **sudo** 表示  允许普通用户使用root的超级权限以及命令的工具。

``` shell
sudo systemctl start docker
```
查看下载的 docker 镜像
``` shell
docker image
```
搜索 镜像资源
``` shell
docker search 镜像关键字
```
拉取镜像
``` shell
docker pull 镜像name
```
查看所有运行的容器
``` shell
docker ps
```

### docker 中启动 nginx
> -d 后台运行
> -p 端口映射 => 本机端口(服务器的端口)`:`容器端口(nginx的端口)
``` shell
docker run -d -p 8080:80 --name my-nginx  nginx
```
关闭服务
``` shell
docker stop 容器名/容器id
```
