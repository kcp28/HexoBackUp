---
title: matplotlib学习笔记
date: 2020-11-22 16:10:34
tags:
- matplotlib
categories: 学习笔记
---

## 基础操作

matplotlib许多操作都来自pyplot库

```python
import matplotlib.pyplot as plt
import numpy as np

#用numpy生成线性的范围在（-1，1）的50个点
x=np.linspace(-1,1,50)
y=x**2  #y=x^2
#生成图
plt.plot(x,y)# x:横坐标 y:纵坐标
#图显示出来
plt.show()
```

## figure

一个figure就是一个显示窗口

 一个plot算是一个图 ，在plot中设置图中线的颜色、形状、长宽等

```python
import matplotlib.pyplot as plt
import numpy as np

#用numpy生成线性的范围在（-1，1）的50个点
x=np.linspace(-1,1,50)
y1=2*x+1
y2=x**2

plt.figure()
plt.plot(x,y1)#这个plot属于上面那个figure

#num=1:设置figure的序号，figsize(长，宽)
plt.figure(num=1,figsize=(8,4))
#color：设置颜色  linewidth：设置线宽  linestyle="--"设置线形 线状为虚线
plt.plot(x,y2,color="blue",linewidth=2.0,linestyle="--")# x:横坐标 y:纵坐标

#图显示出来
plt.show()
```

## axis 坐标轴

```python
import matplotlib.pyplot as plt
import numpy as np

x=np.linspace(-2,3,100)
y1=2*x+1
y2=x**2

plt.figure()
plt.plot(x,y1)
plt.plot(x,y2,color="blue",linewidth=2.0,linestyle="--")

plt.xlim((-1,2))#x轴取值范围[-1,2]
plt.ylim((-2,3))#y轴取值范围

plt.xlabel("x_axix")#x轴标签
plt.ylabel("y_axix")#y轴标签

new_ticks=np.linspace(-1,2,5)

plt.xticks(new_ticks)#设置x轴刻度
plt.yticks([-2,-1.8,-1,1.22,3],#设置y轴
           [r"$really\  Bad$",r"$bad$",r"$normal$",r"$good$",r"$really\ good$"]
           )

#图显示出来
plt.show()
```