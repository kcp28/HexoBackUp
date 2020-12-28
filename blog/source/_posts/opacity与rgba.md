---
title: opacity&rgba
date: 2020-08-19 16:11:00
categories: 前端基础笔记
tags:
- css
---

opacity 和 rgba 都是css中可以设置透明度的属性。透明度都是0-1之间的小数。

- rgba设置透明度  ：rgba(red,green,blue,透明度)

  ```
  background-color:rgba(12,23,12,.4);
  ```

- opacity设置元素透明度  ：opacity:透明度

  ```
  opacity:.6;
  ```

- 不同：

  1.rgba（）只是一个透明的颜色；opacity设置的是元素的透明度 ，opacity是让整个元素透明。（如rgba无法让图片透明，opacity可以让图片透明）

  2.opacity会使z-index属性失效。对于未设置opacity的元素，那个的z-index大，那个在上面；但是，对于设置了opacity小于1的元素，便按书写顺序排列，后写的会覆盖前边的，即z-index失效。rgba()只是影响背景，不会使元素z-index失效。

  