---
title: css之轮廓和阴影
date: 2020-08-18 11:31:02
categories: 前端基础笔记
tags:
- css
---

轮廓和阴影是css3新增的一个内容

- 轮廓  outline
  - 轮廓就是不占空间的边框，设置轮廓不会影响元素的布局
  - 语法：`outline: 1px solid red;`

- 阴影 box-shadow

  - 阴影和轮廓一样，不会影响元素布局
  - 语法：box-shadow:[inset] 水平偏移量  垂直偏移量  模糊半径  颜色；
  - 值：
    - inset  内部阴影（写上表示该阴影是内部阴影）
    - 1.第一个值，阴影的水平偏移量。正值向右移动，负值向左移动
    - 2.第二个值，阴影的垂直偏移量。正值向下移动，负值向上移动
    - 3.第三个值，阴影的模糊半径。
    - 4.第四个值，阴影的颜色。
  - 多层阴影：设置多组值，每组之间用 ‘ , ’隔开。

  ```css
  .box1{
      box-shadow:5px 3px 4px #123;/*单层阴影*/
  }
  .box2{
      box-shadow:0px 0px 5px rgba(12,34,55,.3);/*四周都设阴影*/
  }
  .box3{
      box-shadow:5px 3px 4px #123,
          8px 5px 4px #223,
          10px 7px 4px #323;/*多层阴影*/
  }
  ```

  