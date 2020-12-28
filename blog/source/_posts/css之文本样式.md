---
title: css之文本样式
date: 2020-08-20 15:54:17
categories: 前端基础笔记
tags:
- css
---

- text-align  用来设置文本水平对齐方式。可选值：

  - left  默认  靠左对齐
  - right   靠右对齐
  - center   居中对齐
  - justify   两端对齐  通过调整空格大小，使得左右都对齐

- vertical-align  设置文本垂直对齐方式。

  - 可选值：

    - baseline   基线对齐

    - top    元素顶端与父元素顶端对齐

    - bottom    元素底部与父元素底部对齐

    - super  上标

      <!--more-->

    - sub   下标

    - middle  居中对齐（这个有点向下）

    - 数值  1.像素值   2.百分比（相对于行高计算）总之：正值往上调整，负值往下调整

  - 用处：当一个div包一个img图片时，图片和div最下端不是紧挨着，会有个缝，这是由于图片默认是按字体基线对齐的方式对齐的,会把div撑高。想要去掉这个缝，法一：设置div中`font-size:0;` 法二：将图片垂直对齐设置为bottom`vertical-align:bottom;`

    ```html
    <style type="text/css">
        div{
            background-color: red;
            border:1px solid blue;
        }
        img{
            width: 100px;
        }
    </style>
    <div>
    	<img src="./bg.jpg">
    </div>
    ```

    默认情况下，div和图片底部之间有个缝：{% asset_img 01.png 有缝 %}

    ```css
    div{
        background-color: red;
        border:1px solid blue;
        /*设置字体大小为0，这样处理有风险，不建议*/
        /*font-size: 0px;*/
    }
    img{
        width: 100px;
        /*给图片设置垂直对齐方式*/
        vertical-align: bottom;
    }
    ```

    设置垂直对齐方式后，没有缝了：{% asset_img 02.png 没缝 %}

- text_decoration   设置文本修饰。语法：text_decoration: 类型  线形   颜色；

  - 类型可选值：
    - underline   下划线
    - line-through   删除线
    - overline  上划线
    - none  没有线
  - 线形可选值：
    - solid  默认  实线
    - double  双下划线
    - dotted  点状线
    - dashed  虚线
    - wavy  波浪线

- text-indent   首行缩进

  - `text-indent:40px;`  缩进40px   （正数向左缩进，负数向右缩进。也可用这种方式隐藏元素）
  - `text-indent:2em;`  缩进2个字

- white-space  如何处理空白内容。可选值：

  - normal   默认，正常自动换行
  - nowrap  不换行
  - pre   保留文本编辑时的格式（空格、换行都保留了）

- text-overflow  如何处理溢出的文本。可选值：

  - ellipsis   使用省略号来表示溢出内容

  容器一行显示不了所有字，设置字不换行，超出容器多余的部分用省略号表示：

  ```html
  <style type="text/css">
  	p{
          width: 100px;
          background-color: green;
          /*设置文字不换行*/
          white-space: nowrap;
          /*隐藏溢出的内容*/
          overflow: hidden;
          /*设置用省略号代替溢出文本*/
          text-overflow: ellipsis;
      }
  </style>
  <body>
  	<p>这里有好多好多好多的字</p>
  </body>
  ```

  效果：{% asset_img 03.png %}

- letter-spacing   字母间距   值越大，间距越大

- word-spacing   单词间距    值越大，间距越大

  