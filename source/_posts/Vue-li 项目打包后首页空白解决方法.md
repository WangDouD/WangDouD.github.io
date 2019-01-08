---
title: Vue-li 项目打包后首页空白解决方法
date:  2018/4/12
tags: [Web,技术]

---

> 也不知道是Vue-li的坑还是webpack的坑，简单粗暴的解决这个问题吧

<!--more-->

## 现象
打包后打开`index.html`文件，网页显示空白，打开chrome调试工具，发现css，js等文件都找不到。

## 解决方法
### 1. 打开项目下的config/index.js文件
文件中有两个`assetsPublicPath`属性，找到`build`下的，更改为下图所示。

[![build里的assetsPublicPath属性](https://i.loli.net/2018/04/12/5aceb7d71d42a.jpg)](https://i.loli.net/2018/04/12/5aceb7d71d42a.jpg)

assetsPublicPath属性作用是指定编译发布的根目录，'/'指的是项目的根目录，'./'指的是当前目录。

### 2.打开项目下的build/utils.js文件
找到图中的相应位置，添加上`publicPath:'../../'`，如图所示。

[![utils.js文件](https://i.loli.net/2018/04/12/5acebbfba4cd2.jpg)](https://i.loli.net/2018/04/12/5acebbfba4cd2.jpg)

修改完后重新打包生成，问题解决。

