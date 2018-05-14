---
title: Pandas库入门笔记.md
date: 2017-05-27 16:27:24
tags: [python , pandas] 
---

## [Pandas](http://pandas.pydata.org)库的介绍
**Pandas是- 第三方库，提供高性能易用数据类型和分析工具**
```python 
import pandas as pd
#Pandas基于NumPy实现，常与NumPy和Matplotlib一同使用
```

## Pandas库的理解
`默认对列进行操作`
两个数据类型:`Series`, `DataFrame`
基于上述数据类型的各类操作
- 基本操作
- 运算操作
- 特征类操作
- 关联类操作

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas1.png" width="" height="200px" alt="picture is gone"/>
</div>

## Pandas库的Series类型
**Series类型由一组数据及与之相关的数据索引组成**
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas2.png" width="" height="200px" alt="picture is gone"/>
</div>

----

Series类型由一组数据及与之相关的数据索引组成
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas3.png" width="" height="200px" alt="picture is gone"/>
</div>

Series类型可以由如下类型创建:
- 列表 
- 标量值
- 字典 
- ndarray
- 其他函数

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas4.png" width="" height="200px" alt="picture is gone"/>
</div>

-----

**从字典类型创建**
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas5.png" width="" height="200px" alt="picture is gone"/>
</div>

Series类型的基本操作
- Series类型包括index和values两部分
- Series类型的操作类似ndarray类型 
- Series类型的操作类似Python字典类型

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas6.png" width="" height="200px" alt="picture is gone"/>
</div>

Series类型的操作类似ndarray类型:
- 索引方法相同索引方法相同，采用[]
- NumPy中运算和操作可用于Series类型
- 可以通过自定义索引的列表进行切片
- 可以通过自动索引进行切片，如果存在自定义索引，则一同被切片

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas7.png" width="" height="200px" alt="picture is gone"/>
</div>

-----

切片
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas8.png" width="" height="200px" alt="picture is gone"/>
</div>

Series类型的操作类似Python字典类型:
- 通过自定义索引访问 
- 保留字in操作
- 使用.get()方法

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas9.png" width="" height="200px" alt="picture is gone"/>
</div>

## DataFrame类型
DataFrame类型由共用相同索引的一组列组成
> DataFrame是一个表格型的数据类型，每列值类型可以不同 DataFrame既有行索引、也有列索引DataFrame常用于表达二维数据，但可以表达多维数据

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas10.png" width="" height="200px" alt="picture is gone"/>
</div>

DataFrame类型可以由如下类型创建:
- 二维ndarray对象
- 由一维ndarray、列表、字典、元组或Series构成的字典 
- Series类型
- 其他的DataFrame类型

**从二维ndarray对象创建**
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas11.png" width="" height="200px" alt="picture is gone"/>
</div>

-----

**从一维ndarray对象字典创建**
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas12.png" width="" height="300px" alt="picture is gone"/>
</div>

----

**从列表类型的字典创建**
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas13.png" width="" height="200px" alt="picture is gone"/>
</div>


## Pandas库的数据类型操作
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas14.png" width="" height="300px" alt="picture is gone"/>
</div>

索引类型的常用方法
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas15.png" width="" height="200px" alt="picture is gone"/>
</div>

----

示例：
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas16.png" width="" height="300px" alt="picture is gone"/>
</div>

.drop()能够删除Series和DataFrame指定行或列索引

## Pandas库的数据类型运算

- 算术运算根据行列索引，补齐后运算，运算默认产生浮点数 
- 补齐时缺项填充NaN (空值)
- 二维和一维、一维和零维间为广播运算 
- 采用+ ‐ * /符号进行的二元运算产生新的对象

数据类型的算术运算
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas17.png" width="" height="200px" alt="picture is gone"/>
</div>

----

示例：
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/pandas18.png" width="" height="300px" alt="picture is gone"/>
</div>

比较运算法则:
- 比较运算只能比较相同索引的元素，不进行补齐 
- 二维和一维、一维和零维间为广播运算
- 采用> < >= <= == !=等符号进行的二元运算产生布尔对象



