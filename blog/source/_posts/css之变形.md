---
title: css之变形
date: 2020-08-24 17:34:27
categories: 前端基础笔记
tags:
- css
---

变形：transform  可以通过变形对元素进行平移、旋转、放大、缩小拉伸等操作，即改变元素的形状、位置、大小、角度等。

- transform  变形,变形不会影响布局。可选值：

  - translate()  水平/垂直/前后移动

    - translateX()   沿x轴方向平移  元素水平移动（负往左，正往右）

    - translateY()   沿y轴方向平移  元素垂直移动（负往上，正往下）

      括号中填移动的偏移量，偏移量可以是具体的像素值，也可以是百分比。百分比是相对自己的宽度高度计算的。

      <!--more-->

      ```html
      <!--绝对定位元素宽高不定时水平垂直居中（IE9及以上）-->
      <style type="text/css">
          .box1{
              width: 500px;
              height: 500px;
              position: relative;
              margin: 0 auto;
              background-color: red;
          }
          .box2{
              position: absolute;
              background-color: #aad;	
              /*元素左端对齐到父元素中线上*/
              left: 50%;
              /*元素上端对齐到父元素中线上*/
              top:50%;
              /*让元素向左移（上移）自己宽度（高度）的一半，实现水平（垂直）居中*/
              /*transform:translateX(-50%) translateY	(-50%);*/
              transform: translate(-50%,-50%);
          }
      </style>
      <body>
      	<div class="box1">
      		<div class="box2">aaadddddddddddddddddd</div>
      	</div>
      </body>
      ```

    - translateZ()   沿z轴方向平移  元素距离人的距离 (x,y,z轴遵守左手法则)

      默认情况下，浏览器显示不出来该属性，因为浏览器不支持近大远小。要显示效果需要先设置视距。

      视距 perspective,即人的眼睛和网页之间的距离，最好设置在800px~1000px之间。一般在html元素中设置：		

      ```css
      html{
          perspective:800px;
      }
      ```

  - rotate()  旋转  
    - rotateX()   沿X轴旋转 ` transform: rotateX(90deg);/*沿x轴旋转90度*/`
    - rotateY()   沿Y轴旋转 ` transform: rotateY(90deg);/*沿y轴旋转90度*/`
    - rotateZ()   沿Z轴旋转 ` transform: rotateZ(90deg);/*沿z轴旋转90度,看起来是沿着中心转*/`

  - scale()  缩放（只在2d平面有效）

    - scaleX()   沿X轴缩放`transform:scaleX(1.2);/*沿X轴缩放1.2倍*/`
    - scaleY()   沿Y轴缩放`transform:scaleX(2);/*沿Y轴缩放2倍*/`

  - skew()  倾斜

    - skewX()   X方向倾斜`transform:skewX(90deg);/*X轴方向倾斜90度*/`
    - skewY()   Y方向倾斜`transform:skewY(45deg);/*Y轴方向倾斜45度*/`

- transform-style  设置变形时效果

  `transform-style:preserve-3d;`  设置变形时3d效果

- transform-origin  指定变形的原点。可选值：top/bottom;left/right/center

  - center    中心  默认
  - top left  左上角
  - 50px 50px  

  