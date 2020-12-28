---
title: css之过渡
date: 2020-08-24 14:37:31
categories: 前端基础笔记
tags:
- css
---

过渡，可以使一个属性的值经过一段时间变成另一个值。过渡相关的属性：

- transition-property   指定要过渡的属性，可以同时指定多个值，多个值之间用“ , ”隔开。

  ```css
  /*指定width、height属性过渡*/
  transition-property:width,height;
  /*所有属性都指定过渡*/
  transition-property:all;
  ```

  <!--more-->

- transition-duration   过渡持续时间 

  ```css
  /*过渡时间单位：s 秒 ；ms 毫秒（注意时间不宜过长）*/
  transition-property:2s;
  /*为各属性分开指定过渡时间*/
  transition-property:2s,50ms;
  ```

- transition-delay  延迟过渡

  ```css
  transition-delay:2s/*延迟2s后开始过渡*/
  ```

- transition-timing-function   指定过渡时间函数。可选值：

  - ease  慢-快-慢    默认

  - linear  匀速

  - ease-in  慢-快

  - ease-out  快-慢

  - ease-in-out  先加速后减速

  - steps(n,end/start): n 表示分n步。start:开始就动   end：时间结束时动

  - 可以通过贝塞尔曲线来指定元素的运动方式。`cubic-bezier(p1,p2,p3,p4)`(https://cubic-bezier.com)

    `transition-timing-function:cubic-bezier(.46,1.21,.86,1.61);`

- transition  过渡相关的简写属性。

```html
<!--过渡demo-->
<style type="text/css">
    .box1{
        height: 100px;
        width: 100px;
        background-color: red;
        transition-property: all;
        transition-duration: 2s;
        transition-timing-function: ease-in-out;

    }
    .box1:hover{
        height: 200px;
        width: 200px;
        background-color: purple;
    }
</style>
<body>
	<div class="box1">鼠标放上看效果</div>
</body>
```

demo效果：

<style type="text/css">
    .box1{
        height: 100px;
        width: 100px;
        background-color: red;
        transition-property: all;
        transition-duration: 2s;
        transition-timing-function: ease-in-out;

}
.box1:hover{
    height: 200px;
    width: 200px;
    background-color: purple;
}

</style>

<div class="box1">鼠标放上看效果</div>