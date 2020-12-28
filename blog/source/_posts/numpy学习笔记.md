---
title: numpy学习笔记
date: 2020-10-07 15:42:13
tag:
- numpy
categories: 学习笔记系列
---

numpy官网：https://numpy.org/

## 1. 安装

### 1.1 安装numpy

```python
pip install numpy
```

### 1.2 引入numpy

```python
import numpy as np
```

## 2. numpy数组

### 2.1 创建数组

1.`np.array([列表]/range(first,end,step))`

2.`np.arange(first,end,step)`   np.arange()方法就相当于np.array(range())

用以上两种方式创建的数组都是`numpy.ndarray`类型的。<!--more-->

```python
import numpy as np
t1 = np.array([1,2,3,4])
print(t1)
print(type(t1)) #查看对象的类型：type(对象)
t2 = np.array(range(10))
print(t2)
t3 = np.arange(10)
print(t3)
print(type(t3))
```

执行结果：

```
[1 2 3 4]
<class 'numpy.ndarray'>
[0 1 2 3 4 5 6 7 8 9]
[0 1 2 3 4 5 6 7 8 9]
<class 'numpy.ndarray'>
```

3.创建时指定数组数据的类型--dtype="数据类型"

数据类型的值可为：int8、int32、int64；(整型)

​				   uint8、uint32、uint64；（无符号整型）

​				   float16、float32(单精度浮点型)、float64(双精度浮点型)、float128;

​				   complex64、complex128、complex256;（用64、128、256位浮点数表示复数）

​				   bool（布尔类型，值为true/false）

```python
t6=np.array(range(5),dtype="float32")
print(t6)
print(t6.dtype)
```

执行结果：

```
[0. 1. 2. 3. 4.]
float32
```

### 2.2数组中数据的类型

#### 2.2.1 查看数组中数据的类型-dtype

数组对象.dtype

```python
t4 = np.arange(1,10,2)
print(t4)
print(t4.dtype)
```

执行结果:

```
[1 3 5 7 9]
int32
```

#### 2.2.2 改变数组中数据的类型-astype

数组对象.astype("数据类型")

```python
t5 = t4.astype("float32")
print(t5)
print(t5.dtype)
```

执行结果:

```
[1. 3. 5. 7. 9.]
float32
```

### 2.3  数组形状

#### 2.3.1 查看数组形状--shape

numpy数组对象.shape

```python
import numpy as np
t1=np.arange(10)
t2=np.array([[1,2,3],[4,5,6]])
print(t1.shape)  #输出：(10,)
print(t2.shape)  #输出：(2, 3)
t3=np.array([
                [[1,2,3,4],[5,6,7,8]],
                [[9,1,13,14],[15,16,17,18]],
                [[21,22,23,24],[25,26,27,28]],
             ])
print(t3.shape)  #输出：(3, 2, 4)
```

#### 2.3.2 改变数组形状--reshape()、flatten()

1) 对象.reshape(tuple)

  参数为表示形状的元组，能改就改，不能改就报错

```python
t4=t1.reshape((2,5))
print(t4) 
```

执行结果：

```
[[0 1 2 3 4]
 [5 6 7 8 9]]
```

2) 对象.flatten()

  flatten() ：把数组变成一维的返回

```python
t5=t3.flatten()
print(t5)#输出：[ 1  2  3  4  5  6  7  8  9  1 13 14 15 16 17 18 21 22 23 24 25 26 27 28]
```

### 2.4 数组转置

1> 对象.transpose()

2> 对象.T

3> 对象.swapaxes(1,0)  交换数组的0，1轴

(以上三种方式效果相同)

```python
import numpy as np
t1=np.array([
    [1,2,3,4,5,6],
    [7,8,9,10,11,12],
    [13,14,15,16,17,18]
])
t2=t1.transpose()
print(t2)
print("*"*19)
print(t1.T)
print("*"*19)
t4=t1.swapaxes(1,0)
print(t4)
```

执行结果

```
[[ 1  7 13]
 [ 2  8 14]
 [ 3  9 15]
 [ 4 10 16]
 [ 5 11 17]
 [ 6 12 18]]
*******************
[[ 1  7 13]
 [ 2  8 14]
 [ 3  9 15]
 [ 4 10 16]
 [ 5 11 17]
 [ 6 12 18]]
*******************
[[ 1  7 13]
 [ 2  8 14]
 [ 3  9 15]
 [ 4 10 16]
 [ 5 11 17]
 [ 6 12 18]]
```

### 2.5 数组切片

#### 2.5.1 用[]切片

1）取行，列   `t1[行，列]`  

2）确定行列的范围  [start,end,step]  范围是[start,end)

​      若指定第几行或第几列，需要用[]。如，`t1[[2,3],[5,2]]`读取第2行的第5列,第3行的第2列，即坐标为(2,5) (3,2)位置的数据。

```python
import numpy as np
#loadtxt()方法读取文本文件
use_file_path="youtube_video_data/GB_video_data_numbers.csv"
t1=np.loadtxt(use_file_path,delimiter=",",dtype="int64")

#取行，列：t1[行，列]，所有切片操作中，传的都是下标索引值，从0开始，左闭右开
print(t1[1500:])#读取从第1500行到最后一行
print("*"*99)

print(t1[1:10])#读取从第1行到第10-1行
print("*"*99)

print(t1[1:10,1:3])#读取从第1行到第10-1行的第1到第3-1列
print("*"*99)

print(t1[:,1:3])#读取所有行的第1到第3-1列
print("*"*99)

print(t1[[2,4,5],1:3])#读取索引为2，4，5行中第1到第3-1列
print("*"*99)

print(t1[:,[0,2]]) #读取所有行中0,2列
print("*"*99)

print(t1[[0,2,2],[0,1,3]])#读取（0.0）（2，1）（2，3）位置上的点
```

#### 2.5.2 条件筛选

数组对象[条件]   筛选出符合条件的数据，如`t1[t1>10]` 选出t1中值大于10的数。

```python
import numpy as np
t1=np.arange(24).reshape(4,6)
print(t1)
print("*"*16)
print(t1[t1>10])#以列表形式输出数组中大于10的元素
```









## 3. numpy中的小数

np.round(array,n)：保存n位小数，四舍五入array数组中的小数

```python
import numpy as np
import random
#用random.random()函数随机生成0-1的小数
t1=[random.random() for i in range(10)]
print(t1)
#生成npmpy数组
t2=np.array(t1)
print(t2)
print(t2.dtype)
#保存两位小数，四舍五入数组中的数字
t3=np.round(t2,2)
print(t3)
```

执行结果：

```
[0.34400530572233423, 0.8859044542162572, 0.05467702147742037, 0.1980902143297847, 0.72136720116339, 0.4999993907724136, 0.04363670323857349, 0.5925288225564053, 0.32436435785693607, 0.7071094017058672]
[0.34400531 0.88590445 0.05467702 0.19809021 0.7213672  0.49999939
 0.0436367  0.59252882 0.32436436 0.7071094 ]
float64
[0.34 0.89 0.05 0.2  0.72 0.5  0.04 0.59 0.32 0.71]
```

## 4. numpy读取文件

loadtxt()  方法读取文本文件。参数：fname  文件路径；delimiter 分隔符；dtype 数据类型；unpack 是否转置，默认是false，若设为true,则数据转置

```python
import numpy as np
#loadtxt()方法读取文本文件，fname:文件路径,delimiter：分隔符，dtype：数据类型 unpack:默认是false，若sheweitrue,则数据转置
use_file_path="youtube_video_data/GB_video_data_numbers.csv"
t1=np.loadtxt(use_file_path,delimiter=",",dtype="int64")
print(t1.shape)
print("*"*99)
```

