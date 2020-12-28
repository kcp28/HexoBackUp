---
title: css之响应式布局
date: 2020-08-26 15:23:00
categories: 前端基础笔记
tags:
- css
---

- 响应式左右布局

```html
<style>
    .outer{
        width:80%;
        /*设置最小宽度*/
        min-width: 800px;
        /* height: 500px; */
        margin: 0 auto;
        background-color: rgb(255, 170, 188);
        /* 开启bfc，解决子元素浮动，父元素高度塌陷的问题 */
        overflow: hidden;
    }
    .left{
        width: 20%;
        height: 500px; 
        background-color: rgb(102, 212, 148);
        float: left;
    }
    .right{
        width:80%;
        height: 500px; 
        background-color: rgb(29, 30, 94);
        float: left; 
    } 
</style>
<body>
    <div class="outer">
        <div class="left"></div>
        <div class="right"></div>
    </div>
</body>
```

<!--more-->

- 左侧固定右侧自适应

```html
<style>
    .outer{
        width:80%;
        /* height: 500px; */
        margin: 0 auto;
        background-color: rgb(255, 170, 188);
        /* 开启bfc，解决子元素浮动，父元素高度塌陷的问题 */
        overflow: hidden;
    }
    .left{
        width: 200px;
        height: 500px; 
        background-color: rgb(102, 212, 148);
        float: left;
        /* 使用margin移动元素位置 */
        margin-left:-100%;
    }
    .right{
        width:100%;
        height: 500px; 
        background-color: rgb(117, 118, 206);
        float: left; 
    } 
    .right_inner{
        /* 不设置宽度，宽度就是auto，会根据margin大小改变。二者相加大小始终等于父元素 */
        margin-left: 200px;
    }
</style>
 <body>
     <div class="outer">
         <div class="right">
             <div class="right_inner">
                 右侧的主要内容
             </div>
         </div>
         <div class="left">左侧菜单</div>
     </div>
</body>
```

- 左右固定中间自适应

```html
<style>
    .outer{
        width:90%;
        /* 指定最小宽度，防止中间变得很小 */
        min-width: 650px;
        margin:0 auto;
        background-color: #bfa;
    }
    .main{
        width: 100%;
        height: 500px;
        background-color: rgb(245, 160, 160);
        float: left;
    }
    .main_inner{
        margin:0 200px;
    }
    .left{
        width: 200px;
        height: 500px;
        background-color: rgb(240, 205, 111);
        float: left;
        margin-left: -100%;
    }
    .right{
        width: 200px;
        height: 500px;
        background-color: rgb(92, 199, 218);
        float: left;
        margin-left: -200px;
    }
</style>
 <body>
     <div class="outer">
         <div class="main">
             <div class="main_inner">
                 主要内容
             </div>
         </div>
         <div class="left">
             左侧菜单
         </div>
         <div class="right">
             右侧菜单
         </div>
     </div>
</body>
```

- 左右固定中间自适应之圣杯布局

```html
<style>
    .outer{
        width:90%;
        /* 指定最小宽度，防止中间变得很小 */
        min-width: 850px;
        margin:0 auto;
        background-color: #bfa;
        position: relative;
    }
    .main{
        height: 500px;       
        background-color: rgb(245, 160, 160);
        /* 指定左右外边距，将两侧位置空出来 */
        margin: 0 200px;
    }
    .left{
        width: 200px;
        height: 500px;
        background-color: rgb(240, 205, 111);
        /* 用定位将左侧元素放到左侧 */
        position: absolute;
        left: 0px;
        top:0;
    }
    .right{
        width: 200px;
        height: 500px;
        background-color: rgb(92, 199, 218);
        /* 用定位将右侧元素放到右侧 */
        position: absolute;
        right: 0;
        top:0;
    }
</style>
<body>
    <div class="outer">
        <div class="left">
            左侧菜单
        </div>
        <div class="main">
            主要内容
        </div>
        <div class="right">
            右侧菜单
        </div>
    </div>
</body>
```

- 左右固定中间自适应之现在的做法

```html
 <style>
     .outer{
         width:90%;
         /* 指定最小宽度，防止中间变得很小 */
         min-width: 850px;
         margin:0 auto;
         background-color: #bfa;
     }
     .main{
         /* 用公式计算宽度 不兼容ie8及以下 */
         width:calc(100% - 400px);
         height: 500px;       
         background-color: rgb(245, 160, 160);
         float: left;
     }
     .left{
         width: 200px;
         height: 500px;
         background-color: rgb(240, 205, 111);
         float: left;
     }
     .right{
         width: 200px;
         height: 500px;
         background-color: rgb(92, 199, 218);
         float: left;
     }
</style>
 <body>
     <div class="outer">
         <div class="left">
             左侧菜单
         </div>
         <div class="main">
             主要内容
         </div>
         <div class="right">
             右侧菜单
         </div>
     </div>
</body>
```

