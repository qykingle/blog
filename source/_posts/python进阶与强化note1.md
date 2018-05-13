---
title: python进阶与强化note1
date: 2017-03-18 15:19:30
tags: [python]
---

## note1
## 过滤
`list`过滤
```python
#生成-10到10范围内的十个数
data = [randint(-10, 10) for _ in range(10)]

#过滤
filter(lambda x: x >= 0, data)

# 列表解析过滤 更快
[x for x in data if x >= 0]
```
`dict`过滤
```python
# 生成一个1-20号，分数为60-100的成绩
student = {x: randint(60, 100) for x in range(1, 21)}

#迭代键和值并过滤
{k:v for k, v in d.items() if v > 90}
```

## 命名
`tuple`增加可读性
```python
NAME, AGE, SEX, EMAIL = range(4)
student = ('Jim', 16, 'male', 'jim@qq.com')
#name
print(student[NAME])

#age
if student[AGE] >= 18:
    pass
#sex
if student[SEX] == 'male':
    pass
```
`使用namedtuple`
```python
from collections import namedtuple
Student = namedtuple('Student', ['name', 'age', 'sex', 'email'])
s = Student(name='Jim', age=16, sex='male', email='jim@qq.com')
s.age
```

## 统计
`统计数字出现的次数`
```python
from random import randint
data = [randint(0, 20) for _ in range(30)]
# 生成起始值为0的字典
c = dict.fromkeys(data, 0)
for x in data:
    c[x] += 1
```
`使用内置函数`
```python
from collections import Counter
# 统计数组出现次数，并生产字典c2
c2 = Counter(data)
#选出出现频率最高的三个元组
c2.most_common(3)
```
`统计单词出现频率`
```python
import re
from collections import Counter
txt = open('CodingStyle').read()
# 按照非字母进行分割
data = re.split('\W+', txt)
# 统计单词出现频次
c3 = Counter(data)
c3.most_common(3)
```
## 字典按值排序
```python
from random import randint
# 字典解析生成
data = {x: randint(60, 100) for x in 'xyzabc'}
# 通过zip函数连接生成一个列表，列表由一系列的元组构成
data2 = zip(data.values(), data.keys())
# 排序
sort = sorted(data2)
```
或者
```python
sorted(d.items(), key = lambda x: x[1])
```

## 公共键
```python
from random import randint, sample
# 先取样，后生成字典
s1 = {x: randint(1, 4) for x in sample('abcefg', randint(3, 6))}
s2 = {x: randint(1, 4) for x in sample('abcefg', randint(3, 6))}
s3 = {x: randint(1, 4) for x in sample('abcefg', randint(3, 6))}
res = []
for k in s1:
    if k in s2 and k in s3:
        res.append(k)
```
或者
```python
# 通过集合的方式(交集)
res = s1.keys() & s2.keys() & s3.keys()
```
`使用map, reduce进行N轮操作`
```python
reduce(lambda a, b: a & b, map(dict.keys, [s1, s2, s3]))
```

## 让字典保持有序
默认的字典是没有顺序的,但可以使用OrderedDict
```python
from collections import OrderedDict
d = OrderedDict()
d['jim'] = (1, 35)
d['leo'] = (2, 36)
d['bob'] = (3, 39)
```
`实例`
```python
from time import time
from random import randint
from collections import OrderedDict

d = OrderedDict()
players = list("ABCDEFGH")
start = time()

for i in range(8):
    input()
    p = players.pop(randint(0, 7 - i))
    end = time()
    print(i+1, p, end - start)
    d[p] = (i + 1, end - start)
print('*' * 20)
for i in d:
    print(i, d[i])
```
## 历史记录
```python
import os
from collections import deque
from random import randint
import pickle
N = randint(0, 100)
# 构造一个队列
history = deque([], 5)
# 判断当前路径中是否有history文件
if os.path.isfile('history'):
    history = pickle.load(open('history', 'rb'))
def guess(k):
    if k == N:
        print('right')
        return True
    if k < N:
        print('%s is less than N' % k)
    else:
        print('%s is greater than N' % k)
    return False

while True:
    line = input('please input a number: ')
    if line.isdigit():
        k = int(line)
        history.append(k)
        if guess(k):
            break
    elif line == 'history' or line == 'h?':
        print(list(history))
# 将history存储到本地文件中，方便下次打开历史记录仍然存在
pickle.dump(history, open('history', 'wb'))
```

