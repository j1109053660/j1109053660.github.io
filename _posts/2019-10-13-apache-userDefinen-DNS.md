---
layout: post
title:  "apache自定义域名解析"
categories: PHP
author: 滑稽兔啊
tags:  PHP apache 域名解析 phpStudy
date:  2019-10-13 20:39:11
---

## 前言
> 在进行本地测试php时碰到的问题，在预览web网站时打开的都是localhost/项目根目录/index.php  域名栏里的项目路径越多那地址就越长，想要缩短或者简化路径更美观 。我所用的环境是phpStudy集成环境，内置apache(阿帕奇)。在apache进行自定义域名指向本地地址设置。

* content
{:toc}










## 过程

1. 打开 ```C:\Windows\System32\drivers\etc\hosts``` 文本。

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025192306.png)

2. 在最后添加信息 ```127.0.0.1	qwq.top``` 保存

3. 打开 ```D:\phpStudy\Apache\conf\httpd.conf``` 文本

4. 查找 ```vhosts``` 大约在470行取消前面的#

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025192406.png)

5. 打开```D:\phpStudy\Apache\conf\extra\httpd-vhosts.conf```文本

6. 清除所有，添加以下代码:
```conf
没有这个代码网页无法加载原localhost/www下的路径
<VirtualHost *:80>
	DocumentRoot "D:\phpStudy\WWW"
	ServerName localhost
</VirtualHost>
```
```cinf
同过自定义域名打开多级路径下的项目
<VirtualHost *:80>
	DocumentRoot "D:\phpStudy\WWW\2019-10-10\q"
	ServerName qwq.top
</VirtualHost>
```
>注意：上面代码中绝对路径“D:\phpStudy\WWW\2019-10-10\q”是项目地址(index.php所在目录)

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025192430.png)

------





