---
title: Atom无法安装插件的解决方案
date: 2018-04-15 17:20:30
tags: [atom, 插件]
---
众所周知 Atom安装插件经常失败，全局SS也没什么用。终于找到了两个可靠的方法，分享一下。

## 第一种
以Linter为例，到[Atom官方插件库](https://atom.io/packages)中搜索出Linter，点击[插件详情页](https://atom.io/packages/linter)中的Repo，进入该插件的[Github仓库](https://github.com/steelbrain/linter)，clone该项目到你的Atom插件目录（Win： C:\Users\你的用户名\.atom\packages，Mac： ~/.atom/packages），然后cd到该插件目录下，执行 npm install，安装完成。


这也是网上比较常见的手动安装插件的做法，但是实际安装完后经常出现再次打开Atom时崩溃的现象，建议尝试第二种方式。

## 第二种

切换到Atom安装目录下（Win： `C:\Users\你的用户名\.atom`，Mac： `~/.atom`），编辑`.atomrc`文件（如果没有就新建一个）。
将该文件内容改为
```bash
registry = https://registry.npm.taobao.org
```
或者
```bash
strict-ssl = false
http_proxy = socks5://127.0.0.1:1080
https_proxy = socks5://127.0.0.1:1080
```
将http_proxy和https_proxy修改为你自己的代理。
然后再去Atom中正常安装（File-Setting-Install）即可
