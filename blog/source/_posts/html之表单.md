---
title: html之表单
date: 2020-08-21 13:52:18
categories: 前端基础笔记
tags:
- html
---

- form 表单。元素属性：
  - action  表单提交的目标地址。
  - method  提交方式  post/get

  <b>像input、img等替换元素，和行内块(display为inline-block)，可用文本居中的方式让他们居中</b>

form中的表单项都属于行内块，可以设置宽高，不独占一行。所以表单项默认是不换行的。

- 文本框   `<input type="text" />`

- 密码框   `<input type="password" />`

  <!--more-->

- 单选按钮 

  ````html
  <input type="radio" name="sex" value="男">
  <input type="radio" name="sex" value="女" checked>
  <!--实现单选功能需要把同组的单选按钮设置相同的name。-->
  ````

  checked 可以将单选按钮设置为默认选中。

- 多选按钮

  ```html
  <input type="checkbox" name="hobby" value="swim">游泳
  <input type="checkbox" name="hobby" value="run">跑步
  <input type="checkbox" name="hobby" value="pingpang" checked>乒乓球
  ```

  checked 可以将多选按钮设置为默认选中。

- 下拉列表

  ```html
  <!--select定义下拉列表-->
  <select name="city">
  <!--optgroup 为下拉选项分组。注意是用label定义分组名-->
      <optgroup label="国内城市">
  <!--option 定义下拉选项.selected属性将当前选项设置为默认值-->
          <option value="beijing" selected>北京</option>
      	<option value="shanghai">上海</option>
      	<option value="shenzhen">深圳</option>
      </optgroup>
      <optgroup label="国外城市">
      	<option value="NewYork">纽约</option>
      	<option value="Pairs">巴黎</option>
      </optgroup>
  </select>
  ```

- 按钮 

  ```html
  提交按钮<input type="submit" value="提交"/>
  		<button type="submit">提交</button>
  重置按钮<input type="reset" value="重置"/>
  		<button type="reset">重置</button>
  普通按钮<input type="button" value="点我呀~"/>
  		<button type="button">点我呀~</button>
  ```

- 上传文件  `<input type="file"/>`

- 隐藏的文本框  `<input type="hidden" />`

- 表单项属性

  - name：当指定name属性后，表单才会提交该表单项的值。表单中的数据默认情况下，都是以查询字符串(query string)的形式发送给服务器的。查询字符串：如  username=abc&password=123456。

  - autofocus   自动获取焦点  `<input type="text" autofocus \>`

  - required  必填项  `<input type="text" required \>`

  - value  指定表单项的值  `<input type="text" value="XXX" \>`

  - readonly   只读属性  `<input type="text" readonly \>`

  - disabled   禁用表单项  `<input type="text" disabled \>`

  - autocomplete  自动填写，默认值是on,即开启自动填写(autocomplete="on")。  

    关闭自动填写：`<input type="text" autocomplete="off" \>`

