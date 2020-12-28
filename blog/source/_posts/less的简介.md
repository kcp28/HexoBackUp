---
title: less的简介、安装和使用
date: 2020-08-26 17:05:46
categories: 前端基础笔记
tags:
- css
- less
---

​    less是一门css预处理语言，less是一个css的增强版，增加了变量、Mixin、函数等特性，使css更易维护和扩展。

使用less:

1. 安装node.js ： 官网下载安装包(.msi)，然后运行，一直点下一步。

   在命令行中输入：node -v 查看安装node.js的版本。如果没有报错，证明node.js安装成功

node.js中有一个NPM(node package manage 即node包管理器)，可以用npm下载安装用node编写的包、文件等。

<!--more-->

但是存放下载资源的服务器在美国，下载速度较慢，所以用之前要配置镜像服务器，从镜像服务器上下载资源。

- 配置淘宝的镜像服务器

  npm install -g cnpm --registry=https://registry.npm.taobao.org

2. 装less的编译器

   命令行中：npm install -g less

   用淘宝镜像服务器下载：cnpm install -g less

   安装完成后，在命令行中输入：lessc     

   如果没有报错，则证明less安装成功

3. less编译器使用方法

- 命令行中输入：lessc xxx.less xxx.css  将xxx.less编译为xxx.css

自动编译：在IDE中使用插件整合less,这样就不用手动编译。在用less插件时，每次编译时会自动输出一个 xxx.css .map  类型的文件(可以设置输出与否)。该文件的作用时将css文件和less文件相关联，使我们可以直接调试less文件2。

在html页面还是引入 生成的css文件。

 `<link rel="stylesheet" href="css/XXX.css">`

- 在网页中对less进行编译

在页面引入less.min.js文件对less编译。此时，页面可直接引入less文件。

```html
<!--引入less文件-->
<link rel="stylesheet/less" href="css/xxx.less">
<!--引入外部js文件：less.js。注意要先引入less文件-->
<script src="script/less.min.js"></script>
```

