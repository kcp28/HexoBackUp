---
title: css之定位position
date: 2020-08-19 13:42:10
categories: 前端基础笔记
tags:
- css
---

通过定位，可以将元素放到页面中的任意位置。使用position属性来设置元素的定位。

- position
  - 属性值：
    - static  默认  不开启定位
    - relative 开启相对定位
    - absolute 开启决对定位
    - fixed 开启固定定位
- 当<b>元素开启定位 后（开启定位，即position的值不是static）</b>，我们可以通过四个方向的偏移量来控制元素的位置：top、bottom、left、right
  - top 元素与其定位位置的顶部距离
  - bottom 元素与其定位位置的底部距离
  - left 元素与其定位位置的左侧距离
  - right 元素与其定位位置的右侧距离

<!--more-->

- 定位的层级

  - <b>开启定位</b>以后，元素都会提升一个层级。定位元素的层级,可以通过<b>z-index</b>属性来设置。
  - z-index的属性值是一个数，数字越大，层级越高。
  - 层级高的可以盖住层级低的。层级相同，则在结构上靠后的盖住靠前的。
  - 祖先元素层级再高，也盖不住后代元素。（如父元素层级再高，也盖不住子元素。）

- 相对定位   

  - 通过 ` position:relative;`,将元素定位设置为相对定位。
  - 相对定位特点：
    - 开启相对定位后，元素不会发生任何变化
    - 开启相对定位后，元素<b>不会脱离文档流</b>，
    - 相对定位的元素，是*相对于*其在<b>文档流中的位置</b>进行定位的。(即是 *相对于*  它没开启定位时的 *原来位置*  来定位的)
    - 相对定位会使元素*提高一个层级* 。（开启定位的元素会盖住没开定位的元素）
    - 相对定位不会像浮动那样改变元素的性质，块元素和行内元素的性质不变。

- 绝对定位 

  - 通过` position:absolute; ` 开启元素的绝对定位。

  - 绝对定位特点：

    - 绝对定位会使元素完全脱离文档流

    - 绝对定位会像浮动一样，改变元素性质：行内元素变成块元素，块元素宽高被内容撑起。

    - 开启绝对定位后，如果不设置偏移量，则元素位置不会发生变化。

    - 决对定位是相对于  <b>离他最近的 *开启了定位*  的祖先元素</b>  进行定位的。如果所有祖先元素都没有开启定位，则绝对定位相对于`<html>`进行定位。

      所以一般情况下，我们为一个元素开启了绝对定位后，会同时为它的父元素开启相对定位。

      总结：<b>绝对定位元素是相对于它的  *包含块*  进行定位的。</b >

    - 开启绝对定位，会使元素提升一个层级。

- 包含块

  - 对于绝对定位元素，包含块就是<b>离它最近的开启了定位的块元素</b>。
  - 没有开启定位的祖先元素，则其包含块是网页中的初始包含块，即`<html>`

- 让开启绝对定位的元素相对于包含块左右居中：

  - top、left、bottom、right的默认值都是auto

  - 开启绝对定位后水平方向布局规则：

    left+margin-left+border-left+padding-left+width+padding-right+border-right+margin-right+right=包含块的width

    此时有五个值可以设置为auto:left、margin-left、width、margin-right、right

  - 当开启绝对定位，没有设置left和right时和左右margin时，为了使元素位置不变，会指定左右margin为0，调整left和right。

  - 当开启绝对定位，且left=0,right=0时，水平布局规则就和正常情况下一样了（详见{% post_link css之盒子模型等 css之盒子模型、边框、内外边距 %}）。

  - 使元素相对于包含块左右居中：设置left=0,right=0,左右margin设置为auto:

    ```css
    .son_box{
        widht:200px;/*左右居中，元素要指定宽度*/
        height:200px;
        position:absolute;/*开启绝对定位*/
        left:0;
        right:0;
        margin:0 auto;/*让元素相对于包含块左右居中*/
    }
    ```

- 让元素相对于包含块垂直居中：

  ```css
  .son_box{
      width:200px;
      height:200px;/*垂直居中，元素要指定高度*/
      position:absolute;
      top:0;
      bottom:0;
      margin-top:auto;
      margin-bottom:auto;
  }
  ```

- 让元素相对于包含块左右垂直居中：

  ```css
  .son_box{
      width:200px;
      height:200px;
      position:absolute;
      left:0;
      right:0;
      top:0;
      bottom:0;
      margin:auto;
  }
  ```

- 固定定位

  - 通过  `position:fixed` ，开启元素的固定定位。

  - 固定定位的特点大部分和绝对定位一样：

    - 开启固定定位的元素会脱离文档流
    - 开启固定定位的元素的性质会发生改变：行内元素变块元素，块元素宽高由内容撑起。
    - 开启固定定位的元素会提升一个层级。
    - 固定定位的元素是总是相对于浏览器窗口（视口）进行定位的。视口是固定不动的，会动的是网页。

    {% asset_img 视口与html页面.png 视口与html页面 %}

- 粘滞定位（新加的 兼容性不好）

  - 通过 `position:sticky`