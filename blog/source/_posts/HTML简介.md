---
title: HTML简介
date: 2020-08-11 18:53:22
categories: 前端基础笔记
tags:
- html
---

<!DOCTYPE html>
- 文档声明，告诉浏览器网页的版本

`<html lang="zh"> ...</html>`
- lang属性用来指定语言

`<meta charset="UTF-8">`
- meta 标签用来设置网页的元数据，它里面的内容不被用户查看，一般用来告诉浏览器如何解析网页，或者告诉搜索引擎网页的主要内容。
- 可选属性：
  - name="description" content="描述内容"  ：descprition表示描述网页的内容，content中写具体的描述。
  - name="Keywords" content="关键字" ：Keywords表示描述网页的关键字，content中写具体的关键字。
  - charset用来指定浏览器编码
  - http-equiv="refresh" content=“3;url=XXX” ：用来设置请求的重定向。3表示3秒，后面接重定向的url
- 块元素(block element) :块元素会在网页中独占一行。如，div、p、blockquote
- 内联元素（行内元素）：在网页中不会独占一行。
- p: 块元素，它里面不能放任何的块元素。
- span:span标签是一个文本标签，但它没有语义。主要作用就是选中文中。

<!--more-->

- img:图片标签，用来引入外部图片
  - src:图片路径
  - alt:图片的描述。该属性的值在图片正常显示时不会显示，当图片无法加载出的时候显示。搜索引擎会根据alt的值来判断图片内容，若没有alt属性，搜索引擎不会对图片进行收录。
  - width:图片宽度。height:图片高度。当宽度和高度只设置一个时，则另一个会等比例缩放。所以一般只设置宽。但开发时，宽高最好不设置，直接改图片大小。
  - 浏览器加载（请求资源）顺序：页面->按顺序请求图片(每次1张)。
  - 相对路径：相对于当前文件夹所在路径     ./当前目录    ../上一级目录

- iframe:内联框架,用来引入外部的网页。(开发中不推荐使用，iframe中内容不会被爬虫抓取。)
  - src:外部网页路径  
  - frameborder:显示外部网页时，边框的大小。width:宽 height:高
  -  title:提示文字，当鼠标放在元素上时，显示的提示文字。（其他标签一般也有这个属性）

- audio:引入外部音频。一般情况下音频都是mp3。

  ​	默认情况下音频不会在页面中显示和播放，想要显示和播放用controls属性

  - controls:用来设置是否允许用户控制音频的播放。该属性没有属性值，允许就加。

    `<audio src="音频路径" controls></audio>`  

  - autoplay:用来设置音频是否自动播放(一般浏览器默认不会自动播放)，用法和controls属性一样。

  ```
  <!--一般情况下可使用source标签解决浏览器的兼容问题。文本信息只在都不兼容时显示。-->
  <audio controls>
      对不起，该浏览器不支持该标签
      <source src="音频1.mp3" />
      <source src="音频1.ogg" />
      <embed src="音频1.mp3" type="audio/mp3" />
      <!--embed是用来兼容ie8的，其它情况不推荐使用。type属性用来指定资源类型-->
  </audio>
  
  ```

- video:视频标签，用法和audio一样

  ```
  <video controls>
      对不起，该浏览器不支持该标签
      <source src="视频1.mp4" />
      <source src="视频1.webm" />
      <embed src="视频1.mp4" type="video/mp4" />
      <!--embed是用来兼容ie8的，其它情况不推荐使用。type属性用来指定资源类型-->
  </video>
  <!--开发时，我们一般不把视频资源放在本地服务器上，
  因为1.视频太大，占用内存较多 2.在线播放占用较大的带宽。如果购买的服务器，则这样会产生较大的费用。
  方法1:我们可以购买专门放视频的平台的服务器，把视频放在这些平台上，平台返回视频的链接，我们用video引用该链接来引入自己的视频。
  方法2：把视频放在优酷、腾讯等视频平台上，用iframe标签引入。写个人博客用这个方法还行，否则不推荐使用，因为视频样式等不好控制。
  在视频网站分享->复制通用地址->在自己html中引入
  <iframe frameborder="0" src="https://v.qq.com/txp/iframe/player.html?vid=d0034k9roij" allowFullScreen="true"></iframe>
  -->
  ```

  ==像img、iframe、video、audio等，这些标签属于替换元素。==

- a:超链接。用于跳转页面。

  - href:跳转的url 。

  ```
  <!--回到顶部，#表示页面顶部-->
  <a href="#">回到顶部</a>  
  <!--回到某个元素所在位置，需要给该元素设置id属性。-->
  <a href="#bottom">回到顶部</a>  <!--跳转到id为bottom的元素的位置-->
  ```

  - target：可以设置是否在新页面打开链接。可选值：
    - _self:默认值，在当前窗口打开网页
    - _blank:在新窗口打开。

- 列表

  - 有序列表 ol

  - 无序列表ul  （常用）

  - 定义列表dl，主要对于一些内容下定义

    - dt 表示定义项
    - dd描述定义项

    ```
    <dl>
    	<dt>HTML</dt>
    	<dd>HTML负责网页结构</dd>
    </dl>
    ```

  