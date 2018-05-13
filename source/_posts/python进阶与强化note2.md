---
title: python进阶与强化note2
date: 2017-03-22 15:19:37
tags:
---
# note2
## 如何实现可迭代对象和迭代器对象
应用场景:
- 延时访问(用时访问)
- 封装成一个对象
- for 循环逐条显示
```python
import requests
from collections import Iterable, Iterator

# 继承迭代器对象，并重写__next__方法(next，对于pyton2) 
class WeatherIterator(Iterator):
    def __init__(self, cities):
        self.cities = cities
        self.index = 0
    def getWeather(self, city):
        r = requests.get(u'http://wthrcdn.etouch.cn/weather_mini?city=' + city)
        data = r.json()['data']['forecast'][0]
        return '%s: %s, %s' % (city, data['low'], data['high'])

    def __next__(self):
        if self.index == len(self.cities):
            raise StopIteration
        city = self.cities[self.index]
        self.index += 1
        return self.getWeather(city)

# 继承可迭代对象, 并重写__iter__
class WeatherIterable(Iterable):
    def __init__(self, cities):
        self.cities = cities

    def __iter__(self):
        return WeatherIterator(self.cities)

for x in WeatherIterable([u'北京', u'上海', u'广州', u'长春']):
    print(x)
```
## 使用生成器函数实现可迭代对象
- 应用场景:实现一个可迭代对象的类，它能迭代出给定范围内所有素数：

代码：
```python
class PrimeNumbers:
    def __init__(self, start, end):
        self.start = start
        self.end = end
    def isPrimeNum(self, k):
        if k < 2:
            return False

        for i in range(2, k):
            if k % i == 0:
                return False
        return True

    def __iter__(self) :
        for k in range(self.start, self.end + 1):
            if self.isPrimeNum(k):
                yield k

for x in PrimeNumbers(1, 100):
    print(x)
```

## 反向迭代
可以使用：
```python
l = [1, 2, 3, 4, 5]
l.reverse() # 缺点，改变了原来的值

l[::-1] # 浪费了空间

reversed(l) # 得到一个可迭代的对象
```
实例
```python
class FloatRange:
    def __init__(self, start, end, step = 0.1):
        self.start = start
        self.end = end
        self.step = step 
    def __iter__(self):
        t = self.start
        while t <= self.end:
            yield t
            t += self.step

    def __reversed__(self):
        t = self.end
        while t >= self.start:
            yield t
            t -= self.step

# 正向迭代
for x in FloatRange(1.0, 4.0, 0.5):
    print(x)

# 反向迭代 
for x in reversed(FloatRange(1.0, 4.0, 0.5)):
    print(x)

```
## 如何对迭代器做切片操作
针对日志文件，可以使用
```python
# 缺点，如果文件过大，容易导致内存不足
f = open('/var/log/system.log')
l = l.readlines()
l[100:300]

for line in f:
    print(line)

```

## 可迭代对象
islice会消耗之前申请的迭代器对象
```python
from itertools import islice

## 初始到500  for x in islice(f, 500)
##  100到末尾 for x in islice(f, 100, None) 
for x in islice(f, 100, 300):
    print(x)
```

## 如何在一个for语句中迭代迭代多个可迭代对象
```python
# 并行
from random import randint
chinese = [randint(60, 100) for _ in range(40)]
english = [randint(60, 100) for _ in range(40)]
math = [randint(60, 100) for _ in range(40)]
for i in range(len(math)):
    print(chinese[i] + math[i] + english[i])

# 使用内置函数zip
for c, m, e in zip(chinese, math, english):
    print(c + m + e)

# 串行
# 使用chain函数
from itertools import chain
for s in chain(chinese, english, math):
    if s > 90:
        count += 1
```
