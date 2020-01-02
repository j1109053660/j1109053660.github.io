---
layout: post
title:  "ThinkPHP-day5"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-11-01 14:50:21
---



## 请求接参数











* content
{:toc}

**接收请求参数**

静态调用》$request = Request::instance(); //use think\Request;
助手函数》$request=request();

> Request::instance();//单例的设计模式，始终保证内存中只有一个类的实例化对象；


**获取请求参数**

//变量类型方法([变量名],[/变量修饰符],['‘默认值'],[过滤方法])

<span style="color:#B1173C;font-weight:bold;">
参数1：变量类型方法，根据请求的类型来使用相应的方法param(parameter,核心目标获取的是pathinfo的参数)、get、post;<br>
参数2：变量名，可选，如果写，可以直接接到对应参数的值，不写为获取全部参数的数组，相当于$_GET  $_POST；
</span>

```
$param=$request->param('');<br>
$get=$request->get();<br>
//指定参数接值或者不指定参数接值<br>
```
<span style="color:#B1173C;font-weight:bold;">
参数3：变量修饰符，对接收的变量进行强制的类型转换，复选框命名要加[]并且接收参需要加/a进行强制类型转换
</span>

| 修饰符 |         作用         |
| :----: | :------------------: |
|   /s   | 强制转换为字符串类型 |
|   /d   |  强制转换为整型类型  |
|   /b   |  强制转换为布尔类型  |
|   /a   |  强制转换为数组类型  |
|   /f   |  强制转换为浮点类型  |

<span style="color:#B1173C;font-weight:bold;">
参数4：默认值。当接收的参数数没有设置的接参变量的时候（没给传递的时候），会将默认值赋给接收的变量
</span>
> 注意：pathinfo方式传参时参数名存在，参数值不存在，那么认为该参数没有传，默认值就起效果了
> get和post方式如果参数名存在，那么就认为参数存在，认为是默认赋值了空字符串的值，request接参时默认值 是没有效果的

> 数组特殊-例如复选框一个不选，走默认值。

<span style="color:#B1173C;font-weight:bold;">
参数5：过滤方法，执行的顺序是从左向右；其实就是一个参数的函数；只是执行了一个函数而已，函数可以不是过滤的效果，如：md5；
</span>

>常用的过滤函数有trim(去除两端空格),
>htmlspecialchars(特殊字符转义)
>strip_tags(滤掉NUL，HTML和PHP的标签)

```
<!--参考代码--><br>
$param = $request->param();<br>
$get   = $request->get();<br>
$post  = $request->post();<br>
$id    = $request->param('id/d','1');//参数是否传值<br>
$ids   = $request->get('ids',2);//参数是否存在<br>
$vip   = $request->post('vip/a',[22]);//复选框特殊<br>
$username  = $request-post('username','default','trim,htmlspecialchars,strip_tags');//参数是否存在<br>
$usernamee = $request->post('username','default','md5');//参数是否存在<br>
// 赋值到模版<br>
$this->assign('name','zhuoxiang');
```



**使用PHP函数对变量进行比较**

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191224134304.png)



-----

> sql注释 <br>
> 在索引栏中输入一下代码：<br>
>select * from user where username='admin' or 1=1;--' and upwd='123456';//--注释后面的代码将屏蔽掉不在执行。<br>
>select * from user where username='admin' or 1=1;drop 表名//删除表

-----

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1572600887329&di=e4b3e049453205489866a6d2fb46d174&imgtype=0&src=http%3A%2F%2Fimg.mp.itc.cn%2Fupload%2F20170220%2F46becb84e4eb4aae94260f6eb6a5eeaf.jpg)