---
title: Numpy数据存取与函数
date: 2017-04-29 14:07:43
tags: [numpy, python]
---
## [](#数据的CSV文件存取 "数据的CSV文件存取")数据的CSV文件存取

CSV (Comma‐Separated Value, 逗号分隔值) CSV是一种常见的文件格式，用来存储批量数据

*   frame : 文件、字符串或产生器，可以是.gz或.bz2的压缩文件
*   array : 存入文件的数组
*   array : 存入文件的数组
*   array : 存入文件的数组

*   frame : 文件、字符串或产生器，可以是.gz或.bz2的压缩文件
*   dtype : 数据类型，可选
*   delimiter : 分割字符串，默认是任何空格
*   unpack : 如果True，读入属性将分别写入不同变量

> CSV只能有效存储一维和二维数组 np.savetxt() np.loadtxt()只能有效存取一维和二维数组

* * *

## [](#任意维度如何存取呢？ "任意维度如何存取呢？")任意维度如何存取呢？

*   frame : 文件、字符串
*   dtype : 读取的数据类型
*   count : 读入元素个数，‐1表示读入整个文件
*   sep : 数据分割字符串，如果是空串，写入文件为二进制

> 该方法需要读取时知道存入文件时数组的维度和元素类型 a.tofile()和np.fromfile()需要配合使用 可以通过元数据文件来存储额外信息

## [](#Numpy的便捷文件存取 "Numpy的便捷文件存取")Numpy的便捷文件存取

*   fname: 文件名，以.npy为扩展名，压缩扩展名为.npz
*   array: 数组变量

*   fname: 文件名，以.npy为扩展名，压缩扩展名为.npz

## [](#NumPy的随机函数子库 "NumPy的随机函数子库")NumPy的随机函数子库

np.random

*   rand(do, d1, …, dn): 根据d0‐dn创建随机数数组，浮点数，[0,1)，均匀分布
*   randn(do, d1, .., dn): 根据d0‐dn创建随机数数组，标准正态分布
*   randint(low[, high, shape]): 根据shape创建随机整数或整数数组，范围是[low, high)
*   sdde(s): 随机数种子，s是给定的种子值

*   shuffle(a): 根据数组a的第1轴进行随排列，改变数组x

*   permutation(a): 根据数组a的第1轴产生一个新的乱序数组，不改变数组x
*   choice(a[, size, replace, p]): 从一维数组a中以概率p抽取元素，形成size形状新数组 replace表示是否可以重用元素，默认为False

*   uniform(low, high, size): 产生具有均匀分布的数组,low起始值,high结束值,size形状

*   normal(loc, scale, size): 产生具有正态分布的数组,loc均值,scale标准差,size形状
*   poisson(lam, size): 产生具有泊松分布的数组,lam随机事件发生率,size形状

## [](#NumPy的统计函数 "NumPy的统计函数")NumPy的统计函数

*   sum(a, axis = None): 根据给定轴axis计算数组a相关元素之和， axis整数或元组
*   mean(a, axis = None): 根据给定轴axis计算数组a相关元素的期望， axis整数或元组
*   average(a, axis = None, weights=None): 根据给定轴axis计算数组a相关元素的加权平均值
*   std(a, axis = None): 根据给定轴axis计算数组a相关元素的标准差
*   var(a, axis = None): 根据给定轴axis计算数组a相关元素的方差

*   min(a) max(a):计算数组a中元素的最小值、最大值

*   argmin(a) argmax(a): 计算数组a中元素最小值、最大值的降一维后下标
*   unravel_index(index, shape): 根据shape将一维下标index转换成多维下标
*   ptp(a): 计算数组a中元素最大值与最小值的差
*   median(a): 计算数组a中元素的中位数（中值）

*   np.gradient(f): 计算数组f中元素的梯度，当f为多维时，返回每个维度梯度

    > 梯度：连续值之间的变化率，即斜率XY坐标轴连续三个X坐标对应的Y轴值：a, b, c，其中，b的梯度是： (c‐a)/2
