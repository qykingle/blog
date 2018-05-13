---
title: python进阶与强化note3
date: 2018-03-18 15:19:40
tags: [python]
---
# note3
## 拆分字符串
```python
# 普通拆分，可以使用map函数
s = 'ab;cd|efg|hi,jkl|mn\topq;rst,uvw\txyz'
res = s.split(';')
t = []
# 将res中的每一项用|分隔符，分割之后，添加到t列表中去
map(lambda x: t.extend(x.split('|')), res)

#总结为一个函数
def mySplit(s, ds):
    res = [s]
    for d in ds:
        t = []
        map(lambda x: t.extend(x.split(d)), res)
        res = t
    return [x for x in res if x]

s = 'ab;cd|efg|hi,jkl|mn\topq;rst,uvw\txyz'
mySplit(s, ';|,\t')
```
直接使用正则表达式
```python
import re
# 速度慢一些
re.split(r'[,;\t|]+', s)
```

## 如何判断字符串是否以a开头或结尾
`使用s.endswith()和s.startswith()`
```python
import os, stat
#os.listdir('.')
l = [name for name in os.listdir('.') if name.endswith(('.sh', '.py'))]
for f in l:
    # 改变文件权限
    os.chmod(f, os.stat(f).st_mode | stat.S_IXUSR)
```
## 如何调整字符串中文本的格式
```python
import re
log = open('/var/log/dpkg.log').read()
# 将2015-02-28格式转换为02/28/2015
re.sub('(\d{4})-(\d{2})-(\d{2})', r'\2/\3/\1', log)
# 起别名
# print(re.sub('(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})',r'\g<month>/\g<day>/\g<year>',log))
```
## 如何将多个小字符串拼接成一个大的字符串
```python
pl = ["<0112>", "<32>", "<1024*768>", "<10>", "<1>", "<100.0>", "<500.0>"]
s = ''
# 存在浪费
for p in pl:
    s += p
# ';'.join(['abc', '123', 'xyz'])
# 'abc;123;xyz'
# 不存在浪费，推荐
''.join(pl)
# l = ['abc', 123, 45, 'xyz']
# ''.join([str(x) for x in l])
# 元组的括号省略了，生成器比列表解析更节省空间
# ''.join(str(x) for x in l)
```
## 如何对字符串进行左右，居中对齐
`使用str.ljust(), str.rjust(), str.center()`
```python
s.ljust(20, '=')
# 'abc================='
```
`使用format函数`
```python
# 左对齐
format(s, '<20')
# 右对齐
format(s, '>20')
# 居中对齐
format(s, '^20')
```
## 如何去掉字符串中不需要的字符
<div style="text-align: center">
    <img src="http://t.cn/R9vRmyA" width="" height="200px" alt="picture is gone"/>
</div>
`使用strip()`
```python
s = '  abc dd ca '
# 去掉两端的空白，保留中间的空白
s.strip()
s.lstrip()
s.rstrip()
# 去掉符号
s = '----abc+++'
s.strip('-+')
```
`使用切片拼接`
```python
s = 'abc:123'
s[:3] + s[4:]
```
`利用正则表达式`
```python
s = '\tabc\t123\txyz'
# 只能替换一种
s.replace('\t', '')
# 替换多种
import re
s = '\tabc\t123\txyz\r'
re.sub('[\t\r]', '', s)
```
`使用translate()`
```python
s = 'abc1345xyz'
import string 
# 使用string生成映射表
s.translate(string.maketrans('abcxyz', 'xyzabc'))
s = 'abc\tkdjfk\n'
s.translate(None, '\t\n')
```