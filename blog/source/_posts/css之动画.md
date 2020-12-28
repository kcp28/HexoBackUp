---
title: css之动画
date: 2020-08-24 15:56:37
categories: 前端基础笔记
tags:
- css
---

动画：可以通过动画实现一些更复杂的交互效果。要实现css动画，必需要先设置关键帧。

- @keyframes   用来设置关键帧

  ```css
  @keyframes 关键帧名称 {
    /* from指定动画开始的位置，相当于0%*/  
      from{}
      /*to指定动画结束的位置，相当于100%*/
      to{}
  }
  ```

  <!--more-->

  关键帧中用百分比指定动画每一时刻的位置：

  ```css
  @keyframes 关键帧名称 {
      0%,50%{}
      /*to指定动画结束的位置，相当于100%*/
      20%,100%{}
  }
  ```

- 需要在执行动画的元素上，设置动画细节。用animation相关属性来实现。

  - animation-name  指定动画的名称  

  - animation-duration   指定动画的持续时间

  - animation-delay   指定动画的延迟

  - animation-timing-function  指定动画的时间函数（ease、linear、steps...）

  - animation-iteration-count  指定动画执行的次数  

    ```css
    /*动画执行无限次,即动画循环执行*/
    animation-iteration-count:infinite;
    ```

例子：

```html
<style type="text/css">
		@keyframes a1 {
			from{
				background-position: 0 0;
			}
			to{
				background-position: 1536px 0;
			}
		}
		.box1{
			height: 256px;
			/*calc()是一个可以计算px值的函数，要带单位*/
			width: calc(1536px / 6);
			background-image: url(./img/bg2.png);
			animation-name: a1;
			animation-duration: 5s;
			animation-timing-function: steps(6,end);
			animation-iteration-count: infinite;
		}
	</style>
<body>
	<div class="box1"></div>
</body>
```

- animation-play-state  动画的播放状态。可选值：
  - paused  动画暂停
  - running  动画运行（默认）
- animation-direction  动画运动的方向。可选值：
  - normal  默认，动画从0%-100%执行
  - reverse  反转执行，动画从100%-0%执行
  - alternate  0%-100%-0%
  - alternate-reverse  100%-0%-100%

