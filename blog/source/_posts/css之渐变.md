---
title: css之渐变
date: 2020-08-26 15:43:03
categories: 前端基础笔记
tags:
- css
---

渐变不是颜色，是图片。我们需要通过 `background-image`或`background`设置渐变的效果。

渐变有两种：1.linear-gradient() 线性渐变  2.radial-gradient() 径向渐变

<!--more-->

- linear-gradient 线性渐变

  - 语法：linear-gradient(角度，颜色 位置，颜色 位置，颜色 位置)

  - 角度的值可以是top等，也可以上 度数(单位：deg)

    to bottom  或  180deg    自上向下（默认）

    to top  或  0deg    自下向上

    to left  或  90deg    自右向左

    to right     自左向右

    to right top  从左下到右上
    to left bottom  从右上到左下...

    `background-image:linear-gradient(red,yellow); `

    默认情况，效果：{% asset_img 1.png %}

    ` background-image:linear-gradient(to right top,red,yellow); `

    效果：{% asset_img 2.png %}

    ` background-image:linear-gradient(65deg,red,yellow); `

    效果：{% asset_img 3.png %}

  - 默认情况下，渐变颜色是平均分配的。可以在颜色后，指定颜色的范围.语法： 开始位置  结束位置（注意这种语法兼容性不好）

    ```css
    /*0-20px位置颜色是red,80-100px是黄色，20-80px之间渐变*/
    background-image:linear-gradient(red 0 20px,yellow 80px 100px);
    ```

    效果：{% asset_img 4.png %}

  - 颜色后边可以指定一个长度(px或百分比)，用来指定颜色的起始位置：

    ```css
    /*0-10px位置颜色是red,70px以下开始是黄色，10-70px之间渐变*/  
    background-image:linear-gradient(red 10px,yellow 70px); 
    ```

    效果：{% asset_img 5.png %}          

    ```css
    /*位置也可以是百分比，相对于该元素的高度*/
    background-image:linear-gradient(red 20%,yellow 60%); 
    ```

    效果：{% asset_img 6.png %}

  - repeating-linear-gradient  重复现象渐变

    `background-image:repeating-linear-gradient(red 10px,yellow 30px);`

    效果：{% asset_img 7.png %}

- radial-gradient()  径向渐变

  该渐变默认上下左右对称。渐变默认形状是根据元素形状来的：元素是方块的，渐变是圆形的；元素是长方形，渐变是椭圆形的。

  ` background-image:radial-gradient(#abc,skyblue,blue);`

  默认情况，效果：{% asset_img 8.png %}

  - 设置渐变的形状：
    设置圆形的径向渐变：`background-image:radial-gradient(circle,#abc,skyblue,blue);`

    设置椭圆形的径向渐变：`background-image:radial-gradient(ellipse,#abc,skyblue,blue);`
    设置渐变的宽高(单位px):`background-image:radial-gradient(宽 高,#abc,skyblue,blue);`

    ```css
    background-image:radial-gradient(50px 80px,#abc,skyblue,blue);
    ```

    效果：{% asset_img 9.png %}

  -  设置渐变中心的位置：at 横向位置  垂直位置 （横向：top/bottom  垂直：left/center/right  也可以写具体的像素值）

     ```css
    /*渐变的中心在上方中间*/
    background-image:radial-gradient(at top center,#abc,skyblue,blue);
     ```

    效果：{% asset_img 10.png %}

    ```css
    /*渐变的中心距左边30px，距上边50px*/
    background-image:radial-gradient(at 30px 50px,#abc,skyblue,blue);
    ```

    效果：{% asset_img 11.png %}

  - 调整渐变的范围：

     closest-side:渐变的效果到离圆心最近的边
     farthest-side:渐变的效果到离圆心最远的边
     closest-corner:渐变到离圆心最近的角
     farthest-corner:渐变的效果到离圆心最近的边

    `background-image:radial-gradient(closest-side at 30px center,#abc,skyblue,blue);`

    效果：{% asset_img 12.png %}       

  -   重复的径向渐变，注意要设置渐变种各颜色的范围
     `background-image:repeating-radial-gradient(#abc 20%,skyblue 40%,blue 60%);`

    效果：{% asset_img 13.png %}

- 渐变和背景图片一样，可以用background-position改变位置