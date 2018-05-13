---
title: 'Debian8-Server安装LEMP-nginx,MySQL/MariaDB,PHP'
date: 2017-05-28 22:29:29
tags: [Debian, nginx, mysql, php]
---
转载自linux大神博客

[原文链接](https://www.linuxdashen.com/debian8-jessie)
>LNMP是一组用于搭建网站的开源软件。LNMP代表Linux操作系统、Ngnix HTTP服务器(发音为Engine X)、MySQL/MariaDB数据库和PHP。在这篇教程中，我将介绍如何在Debian 8 服务器上安装LNMP。数据库选择MariaDB, 并安装最新的PHP7. 以下命令在Debian服务器上执行。

## 安装Nginx

相对于Apache，Nginx是一个轻量级的高性能web服务器并在近年来越来越流行。Nginx也可以同时作为一个反向代理。在Debian8上安装Nginx, 输入下面的命令。

```bash
sudo apt-get install nginx -y
```

安装完成后，Nginx会自动运行。
```bash
$ sudo service nginx status
[ ok ] nginx is running.
```

查看Nginx版本
```bash
$ nginx -v
nginx version: nginx/1.6.2
```

在浏览器地址栏中输入Debian服务器的IP, 回车。如果你看到下面的文字，说明Nginx正确地安装好了。

<div style="text-align: center">
    <img src="https://static.jedsk.com/wp-content/uploads/Selection_642.png" width="" height="200px" alt="picture is gone"/>
</div>

你可以使用下面的命令查看服务器的IP。
```bash
curl http://icanhazip.com
```

## 安装MariaDB

MariaDB是MySQL的一个替代品。使用下面的命令安装：
```bash
sudo apt-get install -y mariadb-server mariadb-client
```

在安装过程中会要求你为MariaDB root用户设置一个密码。输入密码后按回车。记住，MariaDB root用户是数据库的管理员，与Linux的root用户是不同的。

<div style="text-align: center">
<img src="https://static.jedsk.com/wp-content/uploads/Selection_645.png" width="" height="200px" alt="picture is gone"/>
</div>

再次输入密码并回车。
<div style="text-align: center">
    <img src="https://static.jedsk.com/wp-content/uploads/Selection_646.png" width="" height="200px" alt="picture is gone"/>
</div>


查看MariaDB版本

```bash
$ mysql --version
mysql Ver 15.1 Distrib 10.0.22-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2
```

运行安全脚本

```bash
sudo mysql_secure_installation
```

输入MariaDB root用户密码。当它问你是否要更改root密码时，选择n. 然后你可以一路按回车键来回答其他所有的问题。

MariaDB数据库安装完成。

`或者安装mysql`
```bash
sudo apt-get install mysql-server mysql-client
```
过程中会提示你设置Mysql的密码，就跟平时的密码设置一样，一 次输入，一次确认。密码确认完毕后基本等一会就安装好了。尝试
```bash
mysql -u root -p
```
如果登录成功，那Mysql就正确安装了.

----

## 安装PHP7

在/etc/apt/sources.list文件中添加下面两行文字以安装dotdeb.org软件源。
```bash
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```

下载并安装GnuPG key
```bash
wget https://www.dotdeb.org/dotdeb.gpg
sudo apt-key add dotdeb.gpg
```


更新本地软件包索引并安装PHP7
```bash
sudo apt-get update

sudo apt-get install php7.0-fpm php7.0-mysql php7.0-common php7.0-gd php7.0-json php7.0-cli php7.0-curl
```

-----

配置PHP7

编辑php.ini文件
```bash
sudo vi /etc/php/7.0/fpm/php.ini
```

找到如下一行
```bash
;cgi.fix_pathinfo=1
```

去掉前面的分号，并将1改为0

```bash
cgi.fix_pathinfo=0
```

保存文件后重启php7.0-fpm
```bash
sudo service php7.0-fpm restart
```

----

## 配置Nginx Virtual Host

在/etc/nginx/sites-available目录下创建一个新的virtual host配置文件

```bash
sudo vi /etc/nginx/sites-available/yourdomain.conf
```

将yourdomain替换成你实际的域名。然后在文件中添加下面的配置。
```bash
server {
listen 80;
server_name yourdoman.com www.yourdomain.com;
root /var/www/html;
index index.php index.html index.htm index.nginx-debian.html;

location / {
try_files $uri $uri/ =404;
}

error_page 404 /404.html;
error_page 500 502 503 504 /50x.html;

location = /50x.html {
root /var/www/html;
}

location ~ \.php$ {
try_files $uri =404;
fastcgi_pass unix:/run/php/php7.0-fpm.sock;
fastcgi_index index.php;
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
include fastcgi_params;
}
}
```
注意，上面第4行 root /var/www/html; 中的root是指网站的根目录，而不是指Linux系统的root用户。

保存文件后，创建一个软链接。
```bash
sudo ln -s /etc/nginx/sites-available/yourdomain.conf /etc/nginx/sites-enabled/yourdomain.conf
```
测试Nginx配置
```bash
sudo nginx -t
```

测试成功：
```bash
 nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
 nginx: configuration file /etc/nginx/nginx.conf test is successful
```

重新加载Nginx配置
```bash
sudo service nginx reload
```

将/var/www/html目录的所有者更改为Nginx用户www-data
```bash
sudo chown www-data:www-data /var/www/* -R
```

测试PHP

在/var/www/html/目录下新建一个文件info.php
```bash
sudo vi /var/www/html/info.php
```

将下面的内容粘贴到info.php文件中。
```php
<?php
   phpinfo();
?>
```

保存文件。然后在浏览器的地址栏输入下面的地址。
```bash
yourdomain.com/info.php
```

用你的实际域名替换yourdomain.com. 如果你看见下面的文字，说明PHP运行正常。

<div style="text-align: center">
    <img src="https://static.jedsk.com/wp-content/uploads/arch_Selection_001.png" width="" height="200px" alt="picture is gone"/>
</div>

请确保你已经为你的域名设置好了一个A记录。

info.php文件只是用于测试的。为了安全起见，你可以删除它。好了！现在你应该成功地在Debian 8 Jessie上搭建好了LNMP.

`502 Bad Gateway`
如果你在测试PHP时网页显示502 Bad Gateway错误。那么很有可能是nginx服务器fastcgi_pass的值与PHP www.conf文件中 listen的值不一致造成的。

打开你的virtual host文件。
```bash
sudo vi /etc/nginx/sites-available/yourdomain.conf
```

查看fastcgi_pass的值。

<div style="text-align: center">
    <img src="https://www.linuxdashen.com/wp-content/uploads/2016/01/Selection_653.png" width="" height="200px" alt="picture is gone"/>
</div>

再打开php的www.conf文件。
```bash
sudo vi /etc/php/7.0/fpm/pool.d/www.conf
```

<div style="text-align: center">
    <img src="https://static.jedsk.com/wp-content/uploads/Selection_654.png" width="" height="200px" alt="picture is gone"/>
</div>

找到文件中的listen这一行，我们需要让nginx fastcgi_pass的值与php listen的值一致。修改完后重启nginx进程和php-fpm进程，这时502 bad gateway错误应该就解决了，可以正常打开网页了。

另外/run/php/php7.0-dpm.sock文件的所有者要与nginx进程用户www-data一致．
```bash
ls /run/php/php7.0-fpm.sock -lh

srw-rw---- 1 www-data www-data 0 Mar 19 03:31 /run/php/php7.0-fpm.sock
```

