---
title: Python笔记-Requests库网络爬取实战
date: 2017-03-07 13:34:48
tags: [python, Requests]
---
## 实例1:京东商品页面的爬取
代码：
```python
import requests
url = "https://item.jd.com/2967929.html"
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:1000]
except:
print("爬取失败")
```
----
## 实例2:亚马逊商品页面的爬取
因为亚马逊自带防爬虫技术，故而我们可以将爬虫假装成一个浏览器去访问，代码如下：
```python
import requests
url = "https://www.amazon.cn/gp/product/B01M8L5Z3Y"
try:
    kv = {"user-agent":"Mozilla/5.0"}
    r = requests.get(url, headers=kv)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[1000:2000])
except:
    print("爬取失败")
```
----
## 实例3:百度/360搜索关键字提交
百度的关键词接口: http://www.baidu.com/s?wd=keyword
360的关键词接口: http://www.so.com/s?q=keyword
代码如下：
```python
import requests
keyword = "Python"
try:
    kv = {'wd': keyword}
    r = requests.get("http://www.baidu.com/s", params = kv)
    print(r.requests.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print("爬取失败")
```
## 实例4:网络图片的爬取和存储
网络图片链接的格式: http://www.example.com/picture.jpg
国家地理:http://www.nationalgeographic.com.cn/
选择一个图片Web页面: http://www.nationalgeographic.com.cn/photography/photo_of_the_ day/3921.html
图片地址:http://image.nationalgeographic.com.cn/2017/ 0211/20170211061910157.jpg
```python
import requests
import os
url = "http://image.nationalgeographic.com.cn/2017/ 0211/20170211061910157.jpg"
root = "D://pics//"
path = root + url.split('/')[-1]
try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path, 'wb') as f:
            f.write(r.content)
            f.close()
            print("文件保存成功")
    else:
        print("文件已经存在")
except:
    print("爬取失败")
```
