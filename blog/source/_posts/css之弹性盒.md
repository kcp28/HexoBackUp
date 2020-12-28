---
title: css之弹性盒
date: 2020-08-27 13:59:17
categories: 前端基础笔记
tags:
- css
mathjax: true
---

弹性盒：又名伸缩盒。弹性盒是css3种新增的一种布局方式，通过弹性盒，可以使一个盒子自动适应其容器的大小，通过弹性盒可以创造出十分灵活的布局。

## 弹性容器   弹性元素(弹性子元素、弹性项)

### 弹性容器

弹性元素的父元素就是弹性容器，要使用弹性盒，必需先将元素设置为弹性容器。设置弹性容器方式：

1.`display:flex;`     块级弹性容器 (独占一行，宽度默认是父元素的宽)（常用）

2.`display:inline-flex;`     行内弹性容器(不独占一行，宽度被内容撑开)

<!--more-->

### 弹性元素(弹性子元素、弹性项)

弹性容器内的<b>子元素</b>(孙子元素不行)就是弹性元素

## 弹性容器的属性

### flex-direction

用来设置弹性容器的*主轴*方向（子元素是横向排列还是纵向排列）。可选值：

- row  主轴是横向的，<b>自左向右</b>
- row-reverse  主轴是横向的，<b>自右向左</b>
- column  主轴是纵向的，<b>自上向下</b>
- column-reverse  主轴是纵向的，<b>自下向上</b>

弹性容器有主轴，还有辅轴(侧轴)。主轴是横向的，辅轴就是纵向的；主轴是纵向的，辅轴就是横向的。

### flex-wrap

设置弹性容器内的弹性元素是否自动换行。可选值：

- nowrap   默认，不换行
- wrap   自动换行。
- wrap-reverse  反转换行

- flex-flow  是一个简写属性，可以同时设置 flex-direction  和  flex-wrap

```css
/*弹性容器主轴是纵向，子元素自动换行*/
flex-flow:column wrap;
```

### justify-content

弹性元素在主轴上的对齐方式。可选值：

- flex-start  元素沿*主轴的起边* 对齐
- flex-end   元素沿*主轴的终边* 对齐
- center  元素在主轴  中间  
- space-between   将空白区域平均分配到弹性元素 *之间*（容器两边相邻的弹性元素没有空白）
- space-around   将空白区域设置到弹性元素的前后
- space-evenly   将空白区域设置到弹性元素一侧。这个能保证元素之间是等距的。
- stretch   拉伸元素，使之在主轴方向上充满盒子。各元素拉伸的宽度相同

### align-items

设置辅轴上元素的对齐方式。可选值

- flex-start  元素沿*辐轴的起边* 对齐
- flex-end   元素沿*辐轴的终边* 对齐
- center  元素在辐轴  中间
- stretch   拉伸元素，使之在辅轴方向上充满盒子。各元素拉伸的宽度相同

### align-content

设置辅轴上的空白的分布方式。可选值：

- flex-start  元素沿着辅轴起边对齐（空白区域跑终边）
- flex-end   元素沿着主轴终边对齐（空白区域跑起边）
- center   元素在辅轴中间（空白区域跑到两边）
- space-between   将空白区域平均分配到弹性元素 *之间*（容器两边相邻的弹性元素没有空白）
- space-around   将空白区域设置到弹性元素的前后
- space-evenly   将空白区域设置到弹性元素一侧。这个能保证元素之间是等距的。

## 弹性元素的属性

### flex-grow

用来指定弹性子元素的增长的系数（当父元素留有空白时设置）。值是一个数字:`flex-frow:1；`

当子元素没有充满父元素时，即父元素留有空白时，子元素会按照自己flex-grow的值增长一定的量来充满父元素。此时，
$$
第i个元素的增长量=父元素空白区域的量*\frac{第i个元素flex-grow的值}{\sum_{k=1}^{n}{第k个元素的flex-grow的值}}
$$
默认情况下，子元素的flex-grow的值为0。即，默认情况下，子元素不会拉长去填充父元素。若只有1个子元素设置了flex-grow的值，则只有该元素会拉长填满空白。若都设置了flex-grow的值，且值一样，则每个子元素都会拉长去填满空白，且拉长的长度一样。

### flex-shrink

用来指定弹性子元素的收缩系数。(当父元素放不下子元素时)。值也是一个数字。

每个子元素缩短多少，由子元素的flex-basis和flex-shrink共同决定。
$$
第i个元素缩减大小=该元素的flexBasis*flexShrink*\frac{溢出的大小}{\sum_{k=1}^{n}{第k个元素的flexBasis*flexShrink}}
$$

### flex-basis

指定弹性元素的标准大小，即子元素不增长不缩短的情况下，子元素的大小。如：`flex-basis:100px;`

一旦设置了这个值，则width自动失效(主轴是纵轴的话，则height失效)。默认值auto,按照弹性容器的长度来设置子元素大小。

### flex

简写属性(常用)，可以同时设置三个值：`flex:flex-grow flex-shrink flex-basis`  注意该属性是给弹性元素设置的。

```css
flex:1 0 100px;/*flex-grow:1;flex-shrink:0;flex-basis:100px*/
```

- `flex:initial;`初始值，相当于flex:0 1 auto,所以默认情况下，子元素只会缩不会伸


- `flex:auto;`初始值，相当于flex:1 1 auto


- `flex:none;`初始值，相当于flex:0 0 auto

### align-self 

用于设置 *弹性元素自身* 在 *辅轴* 上的对齐方式。用于覆盖元素上align-items的属性。可选值和align-items相同。

### order

用来指定弹性元素的排列顺序

```html
<style>
    .outer{
        display:flex;
    }
    .outer div{
        width: 100px;
        height: 100px;
        font-size: 20px;
        text-align: center;  
    }
    .outer div:nth-child(1){
        background-color: red;
        order:2;
    }
    .outer div:nth-child(2){
        background-color: yellow;
        order:3;
    }
    .outer div:nth-child(3){
        background-color: blue;
        order:1;
    }
</style>
<body>
    <div class="outer">
        <div>1</div>
        <div>2</div>
        <div>3</div>
    </div>
</body>
```

效果：{% asset_img 1.png %}

