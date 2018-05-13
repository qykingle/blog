---
title: python-Matplotlib库入门笔记
date: 2017-05-12 21:33:28
tags: [python, Matplotlib]
---
http://matplotlib.org/

Matplotlib库由各种可视化类构成，内部结构复杂，受Matlab启发 matplotlib.pyplot是绘制各类可视化图形的命令子库，相当于快捷方式

```python
#引入模块的别名
import matplotlib.pyplot as plt
```

## Matplotlib库小测
```python
import matplotlib.pyplot as plt

plt.plot([3, 1, 4, 5, 2])
plt.ylabel("Grade")
plt.show()
```
<div style="text-align: center;">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot1.png" width="500px" height="400px" alt="picture is gone"/>
</div>

----

```python
import matplotlib.pyplot as plt

plt.plot([3, 1, 4, 5, 2])
plt.ylabel("Grade")
plt.savefig('test', dpi=600) #PNG文件
plt.show()
```
>plt.savefig()将输出图形存储为文件，默认PNG格式，可以通过dpi修改输出质量

```python
import matplotlib.pyplot as plt
plt.plot([0, 2, 4, 6, 8], [3, 1, 4, 5, 2])
plt.ylabel("Grade")
plt.axis([-1, 10, 0, 6]) #x, y的取值范围
plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.png" width="500px" height="400px" alt="picture is gone"/>
</div>

> plt.plot(x,y)当有两个以上参数时，按照X轴和Y轴顺序绘制数据点

----

## pyplot的绘图区域
```python
plt.subplot(nrows, ncols, plot_number)
```
在全局绘图区域中创建一个 分区体系，并定位到一个子 绘图区域
```python
plt.subplot(3,2,4)
#plt.subplot(324)
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot3.png" width="500px" height="400px" alt="picture is gone"/>
</div>

----

```python
import numpy as np
import matplotlib.pyplot as plt

def f(t):
    return np.exp(-t) * np.cos(2 * np.pi * t)
a = np.arange(0.0, 5.0, 0.02)
plt.subplot(211)
plt.plot(a, f(a))

plt.subplot(2, 1, 2)
plt.plot(a, np.cos(2 * np.pi * a), 'g--')
plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot4.png" width="500px" height="400px" alt="picture is gone"/>
</div>

----

## pyplot的plot()函数
```python
plt.plot(x, y, format_string, **kwargs)
```
- `x`: X轴数据，列表或数组，可选
- `y`: Y轴数据，列表或数组
- `format_string`: 控制曲线的格式字符串，可选
- `**kwargs`: 第二组或更多(x,y,format_string)

> 当绘制多条曲线时，各条曲线的x不能省略

```python
import matplotlib.pyplot as plt
import numpy as np

a = np.arange(10)
plt.plot(a, a*1.5, a, a*2,5, a, a*3.5, a, a*4.5)
plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot5.png" width="500px" height="" alt="picture is gone"/>
</div>

----

format_string: 控制曲线的格式字符串，可选 由颜色字符、风格字符和标记字符组成

|颜色字符|说明|颜色字符|说明|
|:--------:|:-------:|:----:|:---------:|
|'b'|蓝色|'m'|洋红色 magenta|
|'g'|绿色|'y'|黄色|
|'r'|红色|'k'|黑色|
|'c'|青绿色cyan|'w'|白色|
|'#008000'|RGB某颜色|'0.8'|灰度字符串|

|风格字符|说明|
|:----:|:------:|
|'-'|实现|
|'--'|破折线|
|'-.'|点画线|
|':'|虚线|
|'' ''|无线条|

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot6.png" width="100%" height="" alt="picture is gone"/>
</div>

---- 

## pyplot的中文显示
> pyplot并不默认支持中文显示，需要rcParams修改字体实现

```python
import matplotlib.pyplot as plt
import matplotlib

matplotlib.rcParams['font.family'] = 'SimHei'
plt.plot([3, 1, 4, 5, 2])
plt.ylabel("纵轴值")
plt.savefig('test', dpi=600)
plt.show()
```
但是在Mac上依旧有些中文字体不支持，所以可以通过`字体册`软件，找到对应的字体，然后添加进来，如下：
```python
import matplotlib.pyplot as plt
import matplotlib
from matplotlib.font_manager import FontProperties
fonts = FontProperties(fname = "/System/Library/Fonts/STHeiti Light.ttc", size = 14)
plt.plot([3, 1, 4, 5, 2])
plt.ylabel("纵轴值", FontProperties = fonts)
plt.savefig('test', dpi = 600)

plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot7.png" width="500px" height="400px" alt="picture is gone"/>
</div>

----

## pyplot的文本显示函数

<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot8.png" width="600px" height="" alt="picture is gone"/>
</div>

`实例`
```python
import numpy as np
import matplotlib.pyplot as plt
from  matplotlib.font_manager import FontProperties
fonts = FontProperties(fname = "/System/Library/Fonts/STHeiti Light.ttc", size = 14)

a = np.arange(0.0, 5.0, 0.02)
plt.plot(a, np.cos(2 * np.pi * a), 'r--')

plt.xlabel('横轴：时间', fontproperties = fonts, color = 'green')
plt.ylabel('纵轴：振幅', fontproperties = fonts)
plt.title(r'正玄波实例$y = cos(2\pi x)$', FontProperties =fonts, fontsize = 25)
plt.text(2, 1, r'$\mu = 100$') #Latex，2，1表示位置

plt.axis([-1, 6, -2, 2])
plt.grid(True) #显示网格
plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot9.png" width="500px" height="400px" alt="picture is gone"/>
</div>

----

## pyplot的子绘图区域
```python
plt.subplot2grid(GridSpec, CurSpec, colspan=1, rowspan=1)
```
> 理念:设定网格，选中网格，确定选中行列区域数量，编号从0开始

```python
plt.subplot2grid((3,3), (1,0), colspan=2) # rowspan
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot10.png" width="300px" height="" alt="picture is gone"/>
</div>

`GridSpec类`
```python
import matplotlib.gridspec as gridspec

gs = gridspec.GridSpec(3, 3)

ax1 = plt.subplot(gs[0, :])
ax1 = plt.subplot(gs[1, :-1])
ax1 = plt.subplot(gs[1:, -1])
ax1 = plt.subplot(gs[2, 0])
ax1 = plt.subplot(gs[2, 1])
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot11.png" width="300px" height="" alt="picture is gone"/>
</div>






