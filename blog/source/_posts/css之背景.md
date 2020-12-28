---
title: css之背景
date: 2020-08-21 10:06:53
categories: 前端基础笔记
tags:
- css
---

- background-color  设置背景区域

- background-clip  设置背景显示的区域。可选值：

  - border-box   默认，背景会延伸到边框的下边
  - padding-box   背景会设置到内边距
  - content-box   背景只会设置到内容区中

- background-image  设置背景图片

  - 语法：` background-image:url('图片路径');` 注意：路径都是相对于当前文件的。

  - 注意：背景图片和背景颜色可以同时设置。这样，颜色会成为图片的底色。（开发时通常在指定背景图片的同时也指定一个背景颜色，确保图片不显示的情况下，页面也能正常看。）

    <!--more-->

  - 设置背景图片时，如果图片大小小于元素大小，则图片默认会从左上角开始平铺；如果图片大于元素，则图片多余部分不会显示。（可用background-size设置背景图片显示的大小）

- background-repeat   设置背景图片的重复方式。可选值：
  - repeat   默认，图片水平垂直双方向重复，直至充满容器
  - repeat-x  水平方向平铺（重复）
  - repeat-y   垂直方向平铺（重复）
  - no-repeat   不平铺（不重复）

- background-size   设置图片尺寸  

  - 语法：`background-size:背景图片显示宽度  背景图片显示高度；`

  - `background-size:100%;`或`background-size:100% auto;`    宽度与父元素一样,高度等比例缩放;

    `background-size:auto 100%;`   高度与父元素一样，宽度等比例缩放。

  - `background-size:cover`  确保图片比例不变，缩放背景图片，使之充满整个元素。（图片可能显示不全）

  - `background-size:contain`   完整显示图片。可能会有位置没有图片。

- background-position   设置背景图片的位置（用处：雪碧图）

  - 设置方式：

    1. 通过位置关键字来设置位置：top  left  right  bottom  center

       `background-position:top left;`  左上角开始显示图片

       `background-position:top right;`  右上角开始显示图片

       `background-position:bottom left;`  左下角开始显示图片

       `background-position:top center;`  顶部中间开始显示图片

       `background-position:center center;`  元素中间开始显示图片

       如果只写一个值，则第二个值默认是center;

    2. 通过指定偏移量来设置背景图片的位置，需要两个值:1.水平方向偏移量(正值：背景向右移动；负值向左移动)； 2.竖直方向偏移量(正值：背景向下移动；负值：向上移动)

       如：`background-position:20px 40px;`

- background-origin  设置图片从哪里开始定位。可选值：

  - border-box、content-box、padding-box(默认)

- background-attachment   设置图片是否相对于body固定。可选值：

  - scroll  滚动。背景图片会随着页面滚动
  - fixed   背景在视口中固定

- background  以上背景样式的简写属性，所有的背景相关的都可以写，且没有顺序的要求。（注意：要设置background-size 必需先写 background-position;要先写origin再写clip）