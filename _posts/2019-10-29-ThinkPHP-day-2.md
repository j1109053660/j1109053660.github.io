---
layout: post
title:  "ThinkPHP-day2"
categories: PHP
author: 滑稽兔啊
tags:  web php ThinkPHP
date:  2019-10-29 22:29:45
---

# 第二天、控制器和视图











* content
{:toc}
## 第一部分：常识
1. 什么是面向对象
```html
例如，计算过程不算只要结果
```
1.1 什么面向对象过程
```html
例如，封装函数就是面向对象的过程
```
2. MVC的各层功能
```html
Model是应用程序中处理应用程序数据逻辑的部分
View 是应用程序中处理数据显示的部分
controller是应用程序中处理用户交互的部分
```
3. MVC的优缺点
```html
优点:
代码更加清晰，适合于二次开发或者持续的迭代开发
适合与多人开发
用这种结构开发项目的底层和代码更加安全
缺点：
代码结构更加复杂，执行效率偏低》解决办法：增加缓存
大型项目比较适合使用，而小项目降低了效率》解决办法：小项目不使用MVC结构
```
4. 查看PHP版本的四种方式
```php+html
①命令行查询：php -v(version)
②使用预定义常量PHP_VERSION查询：<?php echo PHP_VERION;?>
③使用phpversion()函数查询: <?php echo phpversion();?>
④使用phpinfo()函数查询：<?php echo phpinfo();?>
```
5. 什么命名规范
```html
请查看《ThinkPHP介绍》这篇介绍
```
6. 八种类型中简单类型叫什么？
```html
八种数据类型其中简单类型4种叫做标量，判断是否为标量is_scalar();
```
7. 五种赋值方式
```html
赋值字符串到模板、
赋值一维数组到模板(索引和关联)、
批量赋值(最好使用一维关联数组，一般常用与修改时在模板显示原数据)、
赋值二维数组调用到模板、
赋值对象到模板
```
8. tp中<{foreach}>各种参数叫什么
```html
name是数据源，item表示循环变量，默认key是键
数据源：将赋值过来的变量去掉$就是数据源
```
9. 怎么修改赋值到模板的定界符号
```html
config.php文件'模板设置'中tpl_begin\tpl_end修改定界符
```
10. PHP内置空对象？怎么实例化空对象
```html
stdClass()   
new \stdClass();
//斜杆的意思是前面没有任何别名
```

11.控制器的职责

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191224133147.png)

## 第二部分：代码

**1. 第七题：五种赋值方法**

> 控制器

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029221949.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222102.png)

> 视图

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222233.png)

2. 控制鸡偶行数0.0 变色

> 网页浏览

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222828.png)

> 控制器

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222340.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222413.png)

> 视图

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029222507.png)

-----

3. 继承和渲染

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191029223601.png)