---
layout: post
title:  "阿里云OSS+PicGo组键图床"
categories: Web
author: 滑稽兔啊
tags:  web 阿里云OSS PicGo 图床
date:  2019-10-24 17:53:23
eye:  12
---



## 前言
> 写博客经常插入一些说明图片，使用绝对路径或者相对路径地址的图片不是很方便。
> 到目前为止博客一直用的网络图床。常见的微博图床、七牛图床、又拍云图床、腾讯云COS、阿里云OSS等。一直以来我所使用的是喵素图床https://miao.su/  直到昨天该图床的网站证书过期导致警告访问，不能正常显示图片，博客还有网站中的显示图片的链接都以挂掉。这免费图床让我感到不安图片说不定哪天就怪掉，不如就自己来搞一个私人图床。

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024181303.jpg)











## 第一步，寻找储存服务器

>最为一个长时间使用的服务推荐使用阿里云OSS或者腾讯云COS

<span style="color:yellow">参考价格</span>
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024185224.png)



> 对象储存不仅可以用来当图床，还可以当作云盘使用，缺点是操作没有百度云盘方便



## 第二步，创建专用用户 

<img src="https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024191454.png" style="zoom:80%;" />

输入 ```登录名称``` 和 ```显示名称``` 访问方式选择 ```编程方式``` 
进入 ```权限管理``` ，点击 ```新增授权``` ，搜索 ```AliyunOSSFullAccess```，确认。
选择 ```认证管理``` ，点击 ```创建新的AccessKey```，会生成 ```AccessKeyID``` 和 ```AccessKeySecret```,AccessKeySecret是无法找回的请妥善保存。

## 第三步，创建Bucket

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024193527.png)

> Bucket名称要全局唯一
>区域最好选择离你近的
>权限选择公共读，这样子图片别人才能访问得到

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024194011.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024194015.png)



## 第四步，安装PicGo



>PicGo是一个支持多种图床的客户端图片上传工具
>可以实现快速上传图片到指定图床，并将链接保存到剪贴板。



Github地址：https://github.com/Molunerfinn/PicGo



链接设置如下：

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191024195154.png)



>PicGo设置上传快捷键： 
>当使用截图工具截图后，会保存到剪贴板，这时按下快捷键，PicGo就会自动上传图片，然后将指定格式的链接地址放到剪贴板，直接粘贴到Markdown文档即可。 






>其他待补充...
