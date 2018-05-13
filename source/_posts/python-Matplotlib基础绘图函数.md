---
title: python-Matplotlib基础绘图函数
date: 2017-05-13 16:48:37
tags: [python, Matplotlib]
---
## pyplot的基础图标函数列表
一共有16种
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.1.png" width="" height="" alt="picture is gone"/>
</div>
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.2.png" width="" height="" alt="picture is gone"/>
</div>
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.3.png" width="" height="" alt="picture is gone"/>
</div>

----

## pyplot饼图的绘制
`plt.pie()`
代码：
```python
import matplotlib.pyplot as plt

labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10]
explode = (0, 0.1, 0, 0)

plt.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=False, startangle=90)

plt.axis('equal')
plt.show()
```
效果：
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.4.png" width="500px" height="400px" alt="picture is gone"/>
</div>

## pyplot直方图的绘制
`plt.hist()`
代码：
```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)
mu, sigma = 100, 20 #均值和标准差
a = np.random.normal(mu, sigma, size = 100)

# 20可以控制区间分级的数量,即直方图的个数
plt.hist(a, 20, normed = 1, histtype = 'stepfilled', facecolor='b', alpha=0.75)
plt.title('Histogram')
plt.show()
```
效果：
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.5.png" width="500px" height="400px" alt="picture is gone"/>
</div>

## pyplot极坐标图的绘制
代码：
```python
import numpy as np
import matplotlib.pyplot as plt

N = 20
theta = np.linspace(0.0, 2 * np.pi, N, endpoint = False)
radii = 10 * np.random.rand(N)
width = np.pi / 4 * np.random.rand(N)

ax = plt.subplot(111, projection='polar')
bars = ax.bar(theta, radii, width=width, bottom=0.0) #分别对应left, height, width
for r, bar in zip(radii, bars):
    bar.set_facecolor(plt.cm.viridis(r / 10.))
    bar.set_alpha(0.5)

plt.show()
```
效果:
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.6.png" width="500px" height="400px" alt="picture is gone"/>
</div>

## pyplot散点图的绘制
代码：
```python
import numpy as np
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.plot(10 * np.random.randn(100), 10 * np.random.randn(100), 'o')
ax.set_title('Simple Scatter')

plt.show()
```
<div style="text-align: center">
    <img src="http://ojlmcfp94.bkt.clouddn.com/image/pyplot2.7.png" width="500px" height="400px" alt="picture is gone"/>
</div>


