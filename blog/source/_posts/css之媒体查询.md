---
title: css之媒体查询
date: 2020-08-29 12:30:25
categories: 前端基础笔记
tags:
- css
---

## 1. 媒体查询（media query）

通过媒体查询我们可以为不同的设备，不同的屏幕大小设置不同的样式。比如，根据视口的宽度，屏幕宽高比和和朝向等，来改变页面中元素的样式。

## 2. 媒体查询语法

@media 查询条件{样式}

<!--more-->

### 2.1 查询条件

#### 2.1.1 媒体类型

- all		适用于所有的设备,它里面的样式会应用于所有设备上
- print        适用于打印样式,它里面的样式会应用于打印样式上
- screen     适用于屏幕,它里面的样式会应用到屏幕上
- speech    适用于阅读器,它里面的样式会应用到阅读器上

```css
/*媒体查询例子：*/
@media screen,print{/多个查询条件之间用 , 隔开/
    .box{
        width:100px;
        height:100px;
        background-color:#bfa;
    }
}
/*一般媒体查询都会以only screen开头，表示仅仅对显示屏应用该样式。
only主要用于解决兼容性的问题：对于不支持媒体查询的浏览器，让它忽略媒体查询中设置的样式；让媒体查询中设置的样式只在支持媒体查询的浏览器中应用*/
@media only screen{/*样式*/}
```

#### 2.1.2 媒体功能

- width、min-width、max-width   视口宽度（常用）
- height、min-height、max-height  视口高度（不常用）
- aspect-ratio  宽高比
- orientation  视口方向（portrait 纵向  landscape  横向）
- resolution  像素密度

```css
/*指定屏幕最小宽度，当 屏幕宽度>=最小宽度 时应用样式  min >=   max <=*/
@media only screen and (min-width:800px){...}
```

#### 2.1.3 运算符

- and  多个条件同时满足时应用样式

```css
/*注意：and两边有空格*/
@media only screen and (max-width:800px) and (min-width:600px){...}
```

- ​    ,    一个条件满足即可应用样式
- not  对所有结果取反，如果所有条件 都满足 则不应用样式（必须写在开头）

```css
/*not是对后面所有条件的整体结果取反。若后面条件成立，不应用样式；后面条件不成立，应用样式*/
@media not sereen and (orientation:portrait){...}
```

- only 只有新版浏览器才识别能识别的关键字，用于区分不支持的浏览器

## 3. 断点

断点，即屏幕变化的临界点，跨过这个点页面布局会发生显著的变化。

- 超小屏幕		768以下
- 小屏幕		>=768
- 中等屏幕		>=992
- 大屏幕		>=1200