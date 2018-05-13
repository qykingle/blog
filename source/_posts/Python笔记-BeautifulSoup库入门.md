---
title: Python笔记-BeautifulSoup库入门
date: 2017-03-14 13:36:40
tags: [python, BeautifulSoup]
---
## Beautiful Soup库的安装
Win平台: “以管理员身份运行”cmd 执行
```bash    
pip install beautifulsoup4
```
## 最简单的测试：
```python
import requests
from bs4 import BeautifulSoup
r = requests.get("http://www.baidu.com")
demo = r.text
soup = BeautifulSoup(demo, 'html.parser')
print(soup.prettify())
```
## Beautiful Soup库解析器：

## BeautifulSoup类的基本元素

- Tag标签：任何存在于HTML语法中的标签都可以用soup.<tag>访问获得 当HTML文档中存在多个相同<tag>对应内容时，soup.<tag>返回第一个
- Tag的name(名字)：每个<tag>都有自己的名字，通过<tag>.name获取，字符串类型
- Tag的attrs(属性)：一个<tag>可以有0或多个属性，字典类型
- Tag的NavigableString：NavigableString可以跨越多个层次
- Tag的Comment：Comment是一种特殊类型，可以读取代码中的注释
----

## 标签树的下行遍历

```python
#遍历儿子节点
for child in soup.body.children:
    print(child)

## 遍历子孙节点
for child in soup.body.descendants:
    print(child)
```
## 标签树的上行遍历
- .parent:节点的父亲标签
- .parents:节点先辈标签的迭代类型，用于循环遍历先辈节点

## 标签树的平行遍历

## bs4库的prettify()方法
    prettify()为HTML文本<>及其内容增加更加'\n' .prettify()可用于标签，方法:<tag>.prettify()
