---
title: html之表格
date: 2020-08-21 12:52:28
categories: 前端基础笔记
tags:
- html
---

- table  定义表格
  - table也是块元素，独占一行，但它的宽高是被内容撑开的。
  - table的css样式：
    - border-spacing  设置单元格间距
    - border-collaps:collapse   合并相邻单元格之间的边框

- tr  行

  <!--more-->

- td  单元格

```html
<table>
	<tr>
    	<td>1.1</td>
        <td>1.2</td>
    </tr>
    <tr>
    	<td>2.1</td>
        <td>2.2</td>
    </tr>
</table>
```

- 横向合并单元格  colspan

  ```html
  <td colspan="2"></td><!--这个单元格就占据2个横向单元格的位置-->
  ```

- 纵向合并单元格  rowspan

  ```html
  <td rowspan="2"></td><!--这个单元格就占据2个纵向单元格的位置-->
  ```

- thead  表格头部

  - th  表示表头的单元格

- tbody  表格内容

  - 创建表格时，如果没有使用tbody，浏览器会自动添加tbody，并把所有的tr都添加到tbody中，所以tr的父元素并不是table而是tbody

- tfoot   表格底部

  ```html
  <style>
          table{
              margin:50px auto;
              border: 1px solid grey;
              /*单元格间距设为0*/
              /*border-spacing: 0px;*/
              /*合并相邻单元格之间的边框*/
              border-collapse: collapse;
          }
          td,th{
              border:1px solid grey;
          }
      </style>
  </head>
  <body>
      <table>
          <thead>
              <tr>
                  <th>序号</th>
                  <th>姓名</th>
                  <th>住址</th>
              </tr>
          </thead>
          <tbody>
              <tr>
                  <td>1</td>
                  <td>沈周</td>
                  <td>应天府</td>
              </tr>
              <tr>
                  <td>2</td>
                  <td>唐僧</td>
                  <td>苏州府</td>
              </tr>
              <tr>
                  <td>3</td>
                  <td>汤显祖</td>
                  <td>苏州府</td>
              </tr>
          </tbody>
          <tfoot>
              <tr>
                  <td>合计</td>
                  <td colspan="2">4人</td>
              </tr>
          </tfoot>
      </table> 
  </body>
  ```

- 运用表格，使子块元素在父元素中垂直居中

  在表格的td中,运用`vertical-align:middle`使子元素居中很有效。但在div中，用该属性让元素居中就不行。所以在父元素中运用`display:table-cell`，将父元素的显示方式改编为单元格，然后再用vertical-align使子元素居中。

  ```css
   .father_box{
      width: 300px;
      height: 300px;
      background-color: yellow;
      /*改变父元素显示方式:让div以表格单元格的方式显示*/
      display: table-cell;
      /*让子元素垂直居中*/
      vertical-align:middle;
  }
  .son_box{
      width: 100px;
      height: 100px;
      background-color:green;
      /*子元素相对于父元素水平居中*/
      margin: 0px auto;
  }
  <div class="father_box">
      <div class="son_box"></div>
  </div>
  ```

  <b>注意：在表格td中，或将display设置为table-cell时，margin会失效，但依旧可用padding</b>