---
title: css之盒子模型、边框、内外边距
date: 2020-08-16 13:17:53
categories: 前端基础笔记
tags:
- css
---

- 盒子模型（框模型 box model）

  - 浏览器渲染页面时，它会将页面中的每一个元素都想象成是一个矩形的盒子。

    想象成盒子之后，布局问题就转换成如何摆放盒子的问题。

  - 每一个盒子从内到外都有以下几部分组成。

    - 内容区(content):放子元素的地方
    - 内边距(padding):内容区到边框之间的距离
    - 边框(border)
    - 外边距(margin):盒子之间的距离

    <span style="color:#345">*content、padding、border决定了盒子的大小*</span>

    <span style="color:#345">*padding决定了盒子的位置*</span>

  <!--more-->

- width、height:默认情况下，width和height设置的是<strong>盒子内容区</strong>的宽高。但可通过box-sizing来修改盒子大小的计算方式，使得width和height直接设置盒子的大小。

  - box-sizing  可选值
    - content-box  默认值，内容盒子（width、height指定盒子内容区的大小）
    - border-box  (width、height指定盒子的大小，当设置padding后，padding会往内挤内容区)（谨慎使用，用js设置样式时可能会有隐患）

- border：边框，是盒子的边界，出了边框就是盒子外部。边框会影响盒子的可见框大小，算盒子大小时需要算上边框。

  - 边框相关的3个样式：

    - border-color  边框颜色（默认颜色为前景色，即字体颜色）
    - border-style  边框样式 （默认值是none,即没有边框） 
      - 边框样式的值：实线:solid ; 点状虚线:dotted ; 虚线:dashed ; 双实线:double
    - border-width  边框宽度  (有默认宽度，一般是3px,（不同浏览器默认值不同）)

  - 以上三个样式的设置规则：

    1. 四个值:上,右,下,左  (顺时针)
    2. 三个值：上,左右,下
    3. 二个值：上下,左右
    4. 一个值：上下左右

  - 注意:当边框十分宽时，四个方向交叉的是一个45度的斜线，每个方向是一个梯形

    ```html
    <head>
    	<meta charset="utf-8">
    	<style type="text/css">
    		div{
    			width:30px;
    			height:30px;
    			background-color: pink;
    			border-style: solid;
    			border-width: 50px;
    			border-color: red green orange blue;
    		}
    	</style>
    </head>
    <body>
    	<div></div>
    </body>
    ```

    {% asset_img 01border.png border example %}

  - 简写border,同时设置四个方向边框：   border:宽度  颜色  样式；  （三个值没有顺序）

  - 设置边框圆角：

    - border-top-left-radius  左上角圆角

    - border-top-right-radius  右上角圆角

    - border-bottom-left-radius  左下角圆角

    - border-bottom-right-radius  右下角圆角

      以上四个属性的值是个长度值
      - 1个值：表示圆角的半径。
      - 2个值：圆角成一个椭圆形，这两个值是椭圆的长短轴

    - 简写：border-radius:顺时针指定值（4个值都一样可以写1个）

    - 当圆角值是元素宽度的一半时，该元素变成一个圆。

      `border-radius:50%;/*指定圆角值为元素宽度的一半*/  `

- 内边距 padding

  边框和内容区之间的距离叫做内边距。<strong>盒子的可见框大小由内容区,内边框和边框共同决定。</strong>

- 外边距 margin

  - 当前盒子和其他盒子之间的距离成为外边距。外边距不会影响盒子的可见框的大小，但是外边距会影响到盒子实际占地的大小，影响盒子的位置。

  - 由于在浏览器中默认情况下，元素是靠左上排列的，所以当设置上左外边距时，会移动元素自身的位置；当设置右下外边距时，会移动其他元素。（上左动自己，下右动别人）

  - 当外边距是`负值`时，元素会向`相反的方向移动`。

- 水平方向的布局规则

  - 子元素在父元素的位置是父元素的内容区。

  - 子元素在父元素中水平方向的布局，*必需*满足以下等式：

    margin-left+border-left+padding-left+width+padding-right+border-right+margin-right=父元素的width

    如果这七个值的和相加不等于父元素的宽度，则属于过渡约束，则浏览器会自动调整*右外边距的值*。

  - 在水平方向，有三个值可以设置为auto：margin-left,width,margin-right。设置为auto后，浏览器会自动计算该属性的值。

    - 三个都不设置或都设置成auto，则使width最大，left和right为0。

    - width为auto时，尽可能使width最大。

    - 当width为一具体值时，如将margin-left或margin-right的其中一个设置为auto,另一个不设置，则设置的那一个会尽可能的大，没设的那一个为0。

    - 当width为具体值时，margin-left和margin-right都设置成auto，则二者宽度相同，元素相对于父元素水平居中。

      ```css
      <!--设置元素水平居中-->
      .box1{
          width:100px;/*确定元素width*/
          margin:0px auto; /*将margin-left和right设置为auto*/
      }
      
      ```

- 竖直方向布局规则

  - margin-top+border-top+padding-top+height+padding-bottom+border-bottom+margin-bottom=父元素height  (不强制满足)
  - 当父元素的height为auto时，父元素的高度由内容的高度（即子元素的高度）决定，父元素会自动适应子元素的高度，确保能容纳所有子元素。若为父元素指定了height，则指定多少是多少，此时若子元素的height超过了父元素，则子元素会从父元素中溢出，溢出的子元素不会影响布局。
  - 设置`margin-top:auto;margin-bottom:auto`使元素垂直位置上居中没用。

- 使用 `overflow `来设置溢出内容的处理方式。（溢出：元素内容超过父元素）可选值：

  - `overflow:visible`  默认值，溢出内容不会被剪裁，直接在父元素外部显示。
  - `overflow:hidden ` 溢出的内容会被裁剪，超过父元素的内容不会显示。
  - `overflow:scroll`  生成滚动条，可以通过滚动条查看完整内容。溢出与否都有滚动条。
  - `overflow:auto`  根据需要生成滚动条。那个方向溢出，那个方向生成滚动条。

- 外边距的折叠

  - 垂直方向相邻的外边距，会发生外边距折叠现象。
  - 兄弟间相邻的外边距
    - 两个都是`正值`时，会取两个外边距间的`最大值`。
    - 两个都是`负值`时，则取`绝对值大`的。
    - 两个外边距`一正一负`时，取`两个的和`。
  - 父子元素的`相邻垂直外边距`
    - 子元素的外边距会传递给父元素
      - 解决方法：
        1. 不给子元素设置外边距，给他设置内边距，然后改变父元素的高度。

        2. 隔开父子元素，不让他们相邻：

           法一：给父元素设置一个1px的内边距padding或border，用这个内边距或border让父子的外边距margin不再相邻，然后修改盒子大小。

           法二：在父子元素之间加一个table（只有table可以隔开父子元素）

           ```html
           <div class="father">
           	<table></table>
           	<div class="son"></div>
           </div>
           ```

           用伪元素加table，隔开父子元素(最完美的方式):

           ```css
           .father::before{
               content:'';
               display:table;/*让这一部分以table的方式显示*/
           }
           <div class="father">
           	<div class="son"></div>
           </div>
           ```

        3. (最完美的方式)父元素开启BFC。给父元素overflow属性设置为hidden。（BFC详见{% post_link css之浮动 css之浮动%}）

          父元素中：`overflow:hidden;`

- 文档流（标准流  常规流）

  - 文档（document）,文档就是网页
  - 文档流是网页中的一个位置，默认情况页面中的所有元素都在文档流中排列。
  - 块元素在文档流中的特点
    1. 自上向下排列，独占一行。
    2. 默认宽度和父元素一样(width值是auto，效果是和父元素宽度一样)
    3. 默认高度被内容撑开。
  - 行内元素在文档流中的特点
    1. 自左向右水平排列，没用独占一行。一行中放不下，自动换行。
    2. 默认高度和宽度都被内容撑开。

- 块元素和行内元素的作用

  - 块元素（block）主要用于页面布局。如，div、p

  - 行内元素（inline）主要用于选中文字。如，span

  - 一般情况下，只会在块中放行内元素，不会在行内元素中放块元素。

    特殊：1.  p元素中不能放任何的块元素。

    ​	    2.  a元素中可以放任何的元素，处理它自己。

- 行内元素的盒模型

  - 内联元素不支持设置宽度和高度。
  - 内联元素可以设置padding，但垂直方向的padding不会影响页面的布局。
  - 内联元素可以设置border，但垂直方向的border不会影响页面的布局。
  - 内联元素支持水平方向上的margin，但不支持垂直方向的margin。
  - 水平方向上的外边距不会折叠，二者求和。

  总结：<strong>内联元素不支持设置宽高。仅在水平方向支持padding、border、margin（水平方向设置会影响布局）；垂直方向可以设置边框和内边距，但都不影响页面布局。</strong>

- display属性

  - display用来指定元素所生产的框的类型，可选值：
    - inline  元素作为行内元素显示
    - block  元素作为块元素显示
    - inline-block  行内块元素（可设宽高，不独占一行）（不常用）
    - none  元素不在页面中显示
    - table 元素作为一个表格显示
    - flex 元素作为一个弹性容器显示
    - inline-flex 元素作为行内弹性容器显示

- visibility属性

  - 设置元素的显示状态，可选值：
    - visible  默认，元素正常显示。
    - hidden  不显示元素，但是元素依然占据位置

  <strong>display:none和visibility:hidden的区别：二者都不显示元素，none不占位置，hidden依旧留有元素位置。</strong>

```
<!--练习：二级菜单，当鼠标移到一级菜单时显示二级菜单-->
<head>
	<meta charset="utf-8">
	<style type="text/css">
		.inner{
			display: none;
		}
		.outer > li:hover .inner{
			display:block;
		}
	</style>
</head>
<body>
	<ul class="outer">
		<li>
			<a href="#">1</a>
			<ul class="inner">
				<li><a href="#">1.1</a></li>
				<li><a href="#">1.2</a></li>
				<li><a href="#">1.3</a></li>
				<li><a href="#">1.4</a></li>
			</ul>
		</li>
		<li>
			<a href="#">2</a>
			<ul class="inner">
				<li><a href="#">2.1</a></li>
				<li><a href="#">2.2</a></li>
				<li><a href="#">2.3</a></li>
			</ul>
		</li>
		<li>
			<a href="#">3</a>
			<ul class="inner">
				<li><a href="#">3.1</a></li>
				<li><a href="#">3.2</a></li>
			</ul>
		</li>
	</ul>
</body>
```

- 默认样式

  浏览器为元素设置的默认样式，不同的浏览器设置的默认样式不同。这些默认样式对开发没用，去除默认样式：

  ```css
  body{
      margin:0;/*浏览器默认8px*/
  }
  p{
      margin:0;
  }
  ul{
      margin:0;
      padding:0;
      list-style:none;/*去除无序列表中的项目符号*/
      /*list-style的可选值：
      	square:方块
      	circle:原点
      */
  }
  ```

  

