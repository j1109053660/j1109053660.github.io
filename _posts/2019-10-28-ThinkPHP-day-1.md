---
layout: post
title:  "ThinkPHP-day1"
categories: PHP
author: 滑稽兔啊
tags:  web php ThinkPHP
date:  2019-10-28 21:13:45
---

[TOC]

# 第一天，安装和部署













1. 什么是ThinkPHP？
```html
ThinkPHP是一个免费开源的，快速、简单的面向对象的轻量级PHP开发框架```
```
2. ThinkPHP的组织方式？
```html
thinkphp应用基于MVC的方式来组织
```
3. 什么是MVC？
```html
MVC是一个设计模式，由三个核心组成Model-模型，View-视图，controller-控制器
```
4. 什么是框架？
```html
本身不一定完整但可以结局特定问题、可以扩展
```
5. 什么是二层框架？
```html
例如smarty，将逻辑代码与内容分离
```
6. 什么是三层框架？
```html
例如MVC，分为模型模块-视图模块-控制模块三种结构
```
7. 入口文件的访问方式？
```html
单一入口，无论完成什么功能都要通过入口文件访问，统一但不唯一
```
8. 访问模式
```html
pathinfo的访问模式，http://项目地址/入口文件/模块名/控制器名/参数名/参数/参数2/参数2...静态后缀
```
9. 模块化设计思想？
```html
让代码更清晰、更容易重用。默认划分为前台模块和后台模块
```
10. 什么是命名空间？
```html
起个别名，作用是在项目空间中避免重名
```
11. 命名空间的创立？
```html
namespace app\文件名\controller;
```
12. 控制器的定义
```html
采用大驼峰法(首字母大写)其他小写
相同一类的业务都放在一个控制器中
控制器的类文件名与类名一致
```
13. 查看php版本
```php
　<?php
　　Phpinfo();
　　?>
```
14. application下控制器下的Index为什么要大写？
```html
遵循开发规范-类文件采用大驼峰(首字母大写)命名、其他采用小驼峰
```
15. echo与return的区别？
```html
return 直接将值返回出来，并停止程序。echo直接显示程序还可以直接执行容易出错。
```

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191028114731.png)




## 常见的框架：

- [x] think PHP
- [ ] zend framework
- [ ] codelgniter-杭州城市常用
- [ ] yll framework
- [x] [laravel](https://www.golaravel.com/)
- [ ] cakephp



## 关于访问问题
正常模式：域名/控制器入口/文件名/函数名
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191028193611.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191028193523.png)

域名省略方法：
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191028193248.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191028193400.png)

