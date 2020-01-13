---
layout: post
title:  "ThinkPHP-day11"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2020-1-09 12:00:10
---

# 第11天，模型层









* content
{:toc}


## Db与模型的区别

Db查询返回的数据类型为`数组`

模型查询返回类型的是`模型对象实例`



## 模型定义

> 写法:

```
<?php	
namespace app\index\model;
use think\Model;
class User extends Model{
}
```



### 模型定义的要素：

* 通常会继承 ` think\Model(或者子类) `，虚拟模型除外；
* 一个模型可以一对一，一对多；
* (一个模型类对应操作的数据是一张表，模型类实例化对象就是表里的一条数据)
* 模型名和数据表名可以不是直接对应关系
* 空模型与Db类功能一样，但意义不用。



### 模型定义的目的

* 定义数据表（默认就是模型类名）
* 定义数据表主键（默认会自动获取）
* 定义数据库连接（默认使用数据库配置）
* 定义数据处理逻辑（包括属性和方法）
* 定义业务逻辑（方法）



### 模型定义不支持

* 数据表字段（不需要，会自动获取，并支持缓存机制）
* 数据表前缀（不支持，模型不关心前缀）

|模型名|对应数据表|
|:--|:--|
|User|user|
|UserType|user_type|
|User|think_user|
|UserType|think_user_type|



## 模型调用

模型支持实例化调用和静态调用（主要是查询，查询后会返回一个模型对象实例）。



**实例化调用**

```
$user = new \app\index\model\User();
```

**静态调用**

```
$user = \app\index\model\User::get(1);
```

**助手函数**

```
$user = model('User');
```



tp中表名都是按照小写加下划线的命名规则命名，表名转成类文件名和类名去掉表前缀，用驼峰法





:one: ：

:two: ：重用度高

:three: ：先整体后局部