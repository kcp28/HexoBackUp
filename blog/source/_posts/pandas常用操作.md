---
title: pandas常用操作
date: 2021-08-15 16:17:55
tags:
- pandas
categories: 学习笔记系列
---

## 文件读写

读取csv文件：

```python
data=pd.read_csv(filepath,header=None,low_memory=False,dtype=np.float)
```

read_csv()	读取csv（逗号分隔）文件，返回DataFrame。参数为：

- filepath:文件路径，字符串类型
- header:指定行数做列名。可以是int类型，此数为数据开始行数；可以是list,如[1,2,3,4],次数用list中的内容做列名。当`header=None`时，不指定行数做列名
- low_memory:分块加载到内存，再低内存消耗中解析。但是可能出现类型混淆。确保类型不被混淆需要设置为False。或者使用dtype 参数指定类型。默认是True
- dtype:指定每列数据的数据类型
- sep:指定分隔符，默认 ‘ , ’

写入csv文件：

```python
data.to_csv("test.csv",index=False,sep=',')
```

to_csv()	将DataFrame写入到csv文件中。参数为：

- 必写参数为文件路径

- index：是否显示行名，默认True

- sep:指定分隔符,默认 ' . '

- header:列名，默认True

- mode:写入模式，默认‘w’

  r : 只能读, 必须存在, 可在任意位置读取

  w : 只能写, 可以不存在, 必会擦掉原有内容从头写

  a : 只能写, 可以不存在, 必不能修改原有内容, 只能在结尾追加写, 文件指针无效

  r+ : 可读可写, 必须存在, 可在任意位置读写, 读与写共用同一个指针

  w+ : 可读可写, 可以不存在, 必会擦掉原有内容从头写

  a+ : 可读可写, 可以不存在, 必不能修改原有内容, 只能在结尾追加写, 文件指针只对读有效 (写操作会将文件指针移动到文件尾)

### 删除行

删除指定行：

```python
#删除第一行：
data = data.drop([0],axis=0)#axis=0 删除行 axis=1 删除列

data=data.drop(dropList)#dropList:要删去的行的索引的List
```

删除含有Nan数据的行：

```python
data = data.dropna(axis=0, how='any') #how=any 只要有就删 how=all 全部为Nan才删
```

删除含有inf数据的行：

```python
dropList=data.index[np.isinf(data).any(1)].tolist()
data=data.drop(dropList)
```

## 查看数据

显示数据时，不省略显示：

```python
# 显示所有列
pd.set_option('display.max_columns', None)
# 显示所有行
pd.set_option('display.max_rows', None)
```

查看数据维度：

```python
data.shape #（75，25）数据维度为75行 25列  
data.shape[0] #data的行数
data.shape[1] #data的列数
```

查看变量类型：

```python
type(data)
```

查看数据每列的数据类型：

```python
data.dtypes
```

查看前n行数据：

```python
data.head(5)#查看前5行数据
```

查看后n行数据：

```
data.tail(5)#查看后5行数据
```

获取指定行列数据：

```python
features=data.iloc[:,:data.shape[1]-1]
labels=data.iloc[:,data.shape[1]-1:]
data.iloc[行索引,列索引]#索引可以是一个list
data.iloc[[2,4,5,8],2:5] #查看第2，4，5，8行的[2，4]列
```

检查是否含有nan/inf:

```python
np.isnan(data).any()#data中含有nan则为True
np.isnan(data).all()#data中全为nan则为True

np.isinf(data).any()
np.isinf(data).all()

#注意：当csv文件中含有文字型的标题头时，用read_csv()读出的DataFrame的每列都是Object类型，此时无法用np.isinf()方法，该方法的参数要是数字类型。此时，可以把标题删了，重新存一个csv再重新读新csv，当不含文字数据时，read_csv()读出的DataFrame中的列就是数字类型。
```

参考：

pandas.read_csv()参数详解：https://www.cnblogs.com/datablog/p/6127000.html

pandas to_csv()写入函数参数详解:https://blog.csdn.net/weixin_50220061/article/details/109232688

