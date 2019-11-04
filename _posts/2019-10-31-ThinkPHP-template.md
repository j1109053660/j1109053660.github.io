---
layout: post
title:  "ThinkPHP-template"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-10-31 17:45:11
---


# 模板











* content
{:toc}
**普通标签**

{$name}
>普通标签的定界符被修改成<{}>，输出要<{$name}>才生效

## 变量输出

$view=new View();
$view->name='thinkphp';
return $view->fetch();
模板使用：hello,{$name}!

$data['name']='Thinkphp'
$data['email']='thinkphp@qq.com'
$view->assign('data',$data);
模板使用：Name:{$data.name}  或者 Email:{$data['email']}
如果data变量是一个对象：{$data:name}或者{$data->email}

## 系统变量

> 通常以 ```{$Think```打头

{$Think.server.script_name} // 输出$_SERVER['SCRIPT_NAME']变量
{$Think.session.user_id} // 输出$_SESSION['user_id']变量
{$Think.get.pageNumber} // 输出$_GET['pageNumber']变量
{$Think.cookie.name} // 输出$_COOKIE['name']变量

支持输出 ```$_SERVER```  、 ``` $_ENV``` 、 ```$_POST``` 、 ```$_GET``` 、 ```$_REQUEST``` 、 ```$_SESSION``` 和```$_COOKIE``` 变量。

**常量输出**
```{$Think.APP_PATH}```

**配置输出**
```{$Think.config.default_module}```
```{$Think.config.default_controller}```

## 请求参数

>代补



## 使用函数

模板输出变量使用函数
```{$data.name|md5}```
编译后的结果：```<?php echo (md5($data['name'])); ?>```

函数有多个参数需要调用
```{$create_time|date="y-m-d",###}```
编译后的结果：```<?php echo (date("y-m-d",$create_time)); ?>```

果前面输出的变量在后面定义的函数的第一个参数
```{$data.name|substr=0,3}``` 或者 ```{$data.name|substr=###,0,3} ```
编译后的结果：```<?php echo (substr($data['name'],0,3)); ?>```


以支持多个函数过滤，多个函数之间用“|”分割
```{$name|md5|strtoupper|substr=0,3}```
编译后的结果：```<?php echo (substr(strtoupper(md5($name)),0,3)); ?>```
>函数会按照从左到右的顺序依次调用
>可以使用冒号{:substr(strtoupper(md5($name)),0,3)}



## 默认值default
> ThinkPHP day-4内容


## 运算符

{$a+$b}
<!--
在使用运算符的时候，不再支持常规函数用法，例如：
{$user.score+10} //正确的
{$user['score']+10} //正确的
{$user['score']*$user['level']} //正确的
{$user['score']|myFun*10} //错误的
{$user['score']+myFun($user['level'])} //正确的
-->

## 三元运算
> ThinkPHP day-4内容



## 原样输出literal
> ThinkPHP day-4内容
> 

## 模板注释
> ThinkPHP day-4内容