---
title: css之字体
date: 2020-08-19 19:16:01
categories: 前端基础笔记
tags:
- css
---

## 字体的分类（家族）

### 衬线字体  serif

- 字体宽度各异，有衬线
- 如：Times、宋体

### 无衬线字体  sans-serif

- 字体宽度各异，无衬线
- 如：Helvetica、Arial、微软雅黑

### 等宽字体  monospace

- 字体等宽一样，一般用于代码或表格
- 如：Courier New、Consolas

<!--more-->

## font-family 

用来指定字体的家族，可以指定一个字体的分类，也可以指定一个特定的字体

```css
font-family:serif;/*指定一个字体的分类，不过这样不同浏览器可能有不同的效果*/
font-family:'微软雅黑';/*指定一个特定的字体*/
```

font-family 也可同时指定多个字体，各字体之间用 “  ，”隔开。

```css
font-family:Arial,华文彩云,serif;
```

​	只有当计算机安装了字体才可使用，指定多个字体则如果第一种字体电脑没有，用第二种字体；第二种字体没有，用第三个。等等，以此类推。

## font-face   (用这种方式注意版权)

font-face用来引入字体，使用户的计算机即使没有该字体，浏览器也能正常显示该字体。

```css
@font-face{
    font-family:'字体名称';/*这个名称是自己起的*/
    src:url('字体文件路径');/*字体必需是本地的字体，在自己的服务器内*/
}
```

然后就可以在其他选择器中使用该字体：`font-family:'字体名称';`

## 图标字体

图标字体使图标能像字体一样使用。Font Awesome 网站提供了许多图标字体。

### 图标字体使用步骤：

1. 从官网下载。将下载的css和font文件夹放到项目目录中
2. 引入css文件：`<link rel="stylesheet" href="./css/font-awesome.min.css">`

```html
<head>
    <meta charset="UTF-8">
    <!-- 引入字体图标的css文件 -->
    <link rel="stylesheet"  href="./css/font-awesome.css">
</head>
<body>
    <!-- 使用字体图标 -->
    <i class="fa fa-camera-retro fa-lg"></i> fa-lg
    <i class="fa fa-camera-retro fa-2x"></i> fa-2x
    <i class="fa fa-camera-retro fa-3x"></i> fa-3x
    <i class="fa fa-camera-retro fa-4x"></i> fa-4x
    <i class="fa fa-camera-retro fa-5x"></i> fa-5x
</body>
```

字体图标可以像字体一样使用`font-size`设置字体大小，用`color`设置颜色。字体图标再放大也不会失真。

### iconfont  国内的一个图标库

#### 使用步骤：

1. 在网站中选择要用的图标，把他们加入购物车  

2. 在购物车中下载代码，把下载 的内容放到项目中。e

3. 在页面引入css:`<link rel="stylesheet" href="./iconfont.css">`

4. 使用 :

   1. 用Unicode (字体图标的Unicode可从给的demo中找)挑选相应图标并获取字体编码，应用于页面:

      ```html
      <span class="iconfont">&#x33;</span>
      ```

   2. 通过类。挑选相应图标并获取类名，应用于页面：

      ```html
      <span class="iconfont icon-xxx"></span>
      ```

   3. 在伪类中使用

      ```css
      p::before{
          content:"\33";/*找到图标编码，\图标编码  */
          font-family:iconfont;
          font-size:15px;/*指定图标大小*/
      }
      ```

## em单位

em也是css中的一个单位。1em=1 font-size;可使用em，使容器大小随字体大小改变。

```css
.box{
	font-size:100px;
	width:2em;/*元素宽度是200px*/
}
```
## rem单位

rem也是css中的一个单位。  1rem=html的 1 font-size.

<b>em相对于自己元素的字体大小；rem相对于根元素`<html>`的字体大小</b>

注意：<b>html的font-size默认是16px；font-size最小是12px，若设置的字体大小小于12px，则浏览器自动将字体大小该成12px</b>

## 行高 line-height

文本在网页中显示时，css会为每一个文本行都设置一个文本框，以容纳这些文字。行内元素是被内容撑开的，当文字只有一行时,撑起的高度就是行高。

### 通过line-height来设置行高。

- `line-height:100px;`   指定行高有几像素
- `line-height:1;`   指定行高等于几倍的字体大小(默认行高是字体大小的1.33倍)

注意：行内元素不能设置宽高，它的背景高度默认是行高的字体大小的1.33倍，改变行高背景高度也不变。行内元素的border的高度，和背景高度一样默认是字体大小的1.33倍，且不会改变。

```html
<style type="text/css">
    *{
        padding:0;
        margin: 0;
    }
    div{
        width: 500px;
        margin: 50px auto;
    }
    span{
        font-size: 55px;
        line-height:2;
        background-color: yellow;
        border: 1px solid red;
    }
</style>
<body>
	<div>
		<hr />
			<span>这是一些文字</span>
		<hr />
	</div>
</body>
```

效果如图：（灰线是行高，红色是边框，黄色是背景）{% asset_img 01.png%}

- 文字基本是在行高中居中的（看起来有点偏下）。设置文字在父元素内垂直居中：将行高设置成父元素的高度。

- 通过行高可以设置行间距：行间距 = 行高 - 字体；

## 字重  font-weight

字体是否加粗。可选值：

- 100-900之间的值。值越大，字越粗.(注意：200比一定比100粗，也有肯和100一样；)
- `font-weight:bold;`   直接设置字体加粗（常用）  bold相当于700（默认是normal，相当于400）

## font-style

用来设置字体的样式(斜体)。可选值：

- normal  默认 正常
- italic    斜体         oblique  倾斜

## font-variant

字体变形。可选值：small-caps  小型大写字母

## font

字体简写属性，可以同时设置字体相关的所有样式。

- 语法：(注意：前三个有无都行，且顺序随意。后两个必有，且顺序不变)

`font:[font-weight] [font-style] [font-variant] font-size[/line-height] font-family;   `​
