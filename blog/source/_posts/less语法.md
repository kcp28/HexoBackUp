---
title: less语法
date: 2020-08-27 10:36:43
categories: 前端基础笔记
tags:
- css
- less
---

- less的注释

less的注释有两种。一种是css的多行注释 : /**/  ;  一种是less自己的多行注释：//

```less
/*这是原版的css的注释，它里面的内容会被编译到css文件中去*/
//这是less的单行注释，这个里面的内容不会被编译到css文件中
```

- 运算

+加法；-减法；*乘法；/除法。注意加单位，单位和数值之间不要有空格

<!--more-->

```less
width:100px+100px;   //生成css结果是  width:200px;
width:100+100px;   //生成css结果是  width:200px;
width:100+100 px;   //生成css结果是  width:200 px;此时css语法错误,px和数值之间不能有空格
width:2*100;   //生成css结果是  width:200;此时css语法错误，没有单位
```

- $样式名    直接引用指定样式的值

```less
.box1{
    width:200px;
    height:$width;//height的值也是200px
}
```

此时也可以计算：

```less
.box1{
    width:200px;
    height:$width * .2;//height的值是200*0.2px,是40px
}
```

- 变量

  - 定义变量    @变量名

  ```less
  @a:10px;  //定义变量a,并给它赋值10px
  ```

  - 使用变量

  ```less
  width:@a;   //使用变量a,widht:10px;
  ```

  命名变量时，最好采用驼峰命名法。驼峰命名法，变量名首字母小写，每一个单词的开头字母大写。

  - 可以将变量名的值作为选择器使用，语法：@{变量名}

  ```less
  @className:box1;   //定义变量className,并给它赋值box1
  @classId:mybox;
  .@{className}{}   //将变量className的值作为选择器使用，相当于 .box1{}
  #@{classId}{}   //相当于  #mybox{}
  ```

  - 在路径中使用变量： @{变量名} 

  ```less
  .@{className}{
      background-image:url('@{className}/img/1.png');//相当于box1/img/1.png
  }
  ```

  less变量的作用域遵循局部变量、全局变量的规则。

  - 把变量作为另一个变量的变量值

  ```less
  @w:50px;
  @a:w; //变量a的值是变量w
  .box{
  	width:@@a;  //@a相当于w,@@a相当于@w。width:50px;
  }
  ```

总结：<b>1.属性作为变量：$属性名;   2.自定义变量  @变量名:值</b>

- Mixins  通过Mixins可以将不同类的样式进行混合使用，复用样式(元素选择器不能被复用)

```less
.box1{...}
.box2{
    .box1();  //.box2中使用.box1中的内容。.box1{...} .box2{...}
    .box3{...}//.box3为.box2的后代元素，相当于 .box2 .box3{...}  后代选择器
}
.box4{
    .box2 .box3();  //在.box4中复用.box3中定义的样式
}
```

定义Mixins，如果在名字后添加了  ()   ,则mixins中的样式不会被编译到css文件中去。

```less
.hello(){...}  //.hello不会被编译到css文件中
.box{
    .hello();  //复用 .hello 中定义的样式
}
```

定义时，可以在()中指定参数，相当于形参，具体的参数值在复用时指定：

```less
.hello(@w,@mycolor){  //定义样式的同时，定义形参
    width:@w;
    height:$width;
    background-color:@mycolor;
}
.box{
    //.hello(100px,#bfa); //使用 .hello 中定义的样式并传入实参,这样写实参要与形参顺序一致
    .hello(@mycolor:#bfa,@w:100px)//指定参数名传参，实参形参顺序无要求
}
```

可以给形参指定默认值。当使用时没有传实参时，该形参的值就为默认值：

```less
.hello(@w:10px,@mycolor:#fff){  //指定变量@w的默认值是10px，变量@mycolor的默认值是#fff
    width:@w;
    height:$width;
    background-color:@mycolor;
}
.box{
    .hello();  //不传递实参，就使用默认值
}
//编译结果：
.box{
    width:10px;
    height:10px;
    background-color:#fff;
}
```

- extend()  可以将其他的选择器上的样式，扩展到当前的选择器上。和Mixins不同，Mixins是全部复制，而extend()是通过选择器分组的形式来对样式进行扩展。(元素选择器也行)

语法    选择器:extend(被扩展的选择器){该元素中独有的样式}

```less
.box1{        
    ...
    .box2{...}  
}
.box3:extend(.box1){/*box3独有的样式*/}
//以上less编译出的css的结果是：
.box1,.box3{...}
.box1 .box2{...}
.box3{/*box3独有的样式*/}
```

可在extend()中使用all，将所有含有box1的都扩展：

```less
.box1{        
    ...
    .box2{...}  
}
.box3:extend(.box1 all){/*box3独有的样式*/}
//以上less编译出的css的结果是：
.box1,.box3{...}
.box1 .box2,.box3 .box2{...}
.box3{/*box3独有的样式*/}
```

- &  表示外层选择器

```less
.box1{
    &{...} //& 代表 .box1
    .box2{
        &{...}//& 代表 .box2
    }
}
.box3 .box4{
    &{...} //& 代表 .box3 .box4
}
```

可以用&实现子元素选择器：

```less
ul{
    &>li{...}  //相当于  ul>li{...}
}
```

- import 导入。可以把外部的less文件中的代码，导入到当前的less文件中

```less
@import "外部less文件路径/less文件名.less"；//less文件后缀 .less 可以不写
```

- darken(颜色，百分度)  函数。用于加深颜色。把指定颜色加深指定的百分度：

```less
//把背景颜色黄色加深20%
background-color:darken(yellow,20%);
```

