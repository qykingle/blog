---
title: Python-numpy库
date: 2017-04-17 13:43:15
tags: [python, numpy]
---
## 列表和数组
区别:
- 列表：数据类型可以不同
- 数组：数据类型相同
## NumPy简介
NumPy是一个开源的Python科学计算基础库，包含：
一个强大的N维数组对象 ndarray
- 广播功能函数
- 整合C/C++/Fortran代码的工具
- 线性代数、傅里叶变换、随机数生成等功能

### ndarray对象的属性
- .ndim: 秩，即轴的数量或纬度的数量
- .shape: ndarray对象的尺度，对于矩阵，n行m列
- .size : ndarray对象的个数，相当于.shape中n*m的值
- dtype: ndarray对象的元素类型
- itemsize: ndarray对象中每个元素的大小，以字节为单位

----

### ndarray的元素类型
- bool: 布尔类型，True或False
- intc:  与C语言中的int类型一致，一般是int32或int64
- intp:用于索引的整数，与C语言中ssize_t一致，int32或int64
- int8, int16, int32, int64
- uint8, uint16, uint32, uint64,无符号位
- float16, float32, float64
- complex64, complex128: 实部和虚部都是32 / 64位浮点数

**ndarray数组可以由非同质对象构成非,同质ndarray元素为对象类型,非同质ndarray对象无法有效发挥NumPy优势，尽量避免使用**

----  

### ndarray数组的创建方法
(1)从Python中的列表、元组等类型创建ndarray数组:
- x = np.array(list/tuple)
 - x = np.array(list/tuple, dtype=np.float32)

(2)使用NumPy中函数创建ndarray数组，如:arange, ones, zeros等:
- np.arange(n):类似range()函数，返回ndarray类型，元素从0到n‐1
- np.ones(shape): 根据shape生成一个全1数组，shape是元组类型
- np.zeros(shape): 根据shape生成一个全0数组，shape是元组类型
- np.full(shape, val): 根据shape生成一个数组，每个元素值都是val
- np.eye(n): 创建一个正方的n*n单位矩阵，对角线为1，其余为0
- np.ones_like(a): 根据数组a的形状生成一个全1数组
- np.zeros_like(a): 根据数组a的形状生成一个全0数组
- np.full_like(a): 根据数组a的形状生成一个数组，每个元素值都是val

(3)使用NumPy中其他函数创建ndarray数组
- np.linspace(): 根据起止数据等间距地填充数据，形成数组,有endpoint参数，可以设置成False
- np.concatenate(): 将两个或多个数组合并成一个新的数组

----

### ndarray数组的维度变换
- .reshape(shape): 不改变数组元素，返回一个shape形状的数组，原数组不变
- .resize(shape): 与.reshape()功能一样，但是修改原数组
- .swapaxes(ax1, ax2): 将数组n个维度中两个维度进行调换
- .flatten(): 对数组进行降维，返回折叠后的一维数组，原数组不变

### ndarray数组的类型变换
new_a = a.astype(new_type)
```python
b = a.astype(np.float)
```
ndarray数组向列表的转换: ls = a.tolist()

### 数组的索引和切片
索引:获取数组中特定位置元素的过程,一般以逗号分隔
切片:获取数组元素子集的过程，一般以分号分隔


### 数组与标量之间的运算
数组与标量之间的运算作用于数组的每一个元素
NumPy一元函数
- np.abs(x) np.fab(x):计算数组各元素的绝对值
- np.sqrt(x): 计算数组各元素的平方根
- np.square(x): 计算数组各元素的平方
- np.log(x) np.log10(x) np.log2(x): 计算数组各元素的自然对数、10底对数和2底对数
- np.ceil(x) np.floor(x): 计算数组各元素的ceiling值 或 floor值
- np.rint(x): 计算数组各元素的四舍五入值
- np.modf(x): 将数组各元素的小数和整数部分以两个独立数组形式返回
- np.cos(x) np.cosh(x) np.sin(x) np.sinh(x) np.tan(x) np.tanh(x): 计算数组各元素的普通型和双曲型三角函数
- np.exp(x): 计算数组各元素的指数值
- np.sign(x): 计算数组各元素的符号值，1(+), 0, ‐1(‐)
** 注意数组是否被真实改变**

NumPy二元函数:
- np.maximum(x,y) np.fmax() np.minimum(x,y) np.fmin(): 元素级的最大值/最小值计算
- np.mod(x, y): 元素级的模运算
- np.copysign(x,y): 将数组y中各元素值的符号赋值给数组x对应元素
