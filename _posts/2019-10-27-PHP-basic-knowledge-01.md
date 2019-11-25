---
layout: post
title:  "PHP测试题基础篇01期"
categories: PHP
author: 滑稽兔啊
tags:  web php 测试题
date:  2019-10-27 20:42:24
---

## 前言

>PHP必须掌握的基本知识
>及时记录遇到过的习题，知识点

* content
{:toc}













## 一.什么是post

通过 HTTP POST 方法传递给当前脚本的变量的数组。

## 二.文件上传处理错误信息说明

0. 文件上传成功
1. 上传文件超过php限制
2. 上传文件超过HTML限制
3. 文件部分上传
4. 没有文件被上传
6. 找不到临时文件
7. 没有写入权限

## 三.PHP的错误信息

notice通知,
warning警告，
fatal error致命错误，
parse error语法错误

## 四.session和cookie的区别和联系

>1.不同的访问方法
>2.不同的隐私政策
>3.有效期的差异
>4.不同的服务器压力
>5.不同的浏览器支持
>6.跨域支持的差异Cookie支持跨域访问。


<span style="color:red;">区别:</span>

1. session安全cookie不安全
2. session存在服务器cookie存在客户端
3. session速度快cookie速度慢
4. session容量大cookie受浏览器限制2-4k

<span style="color:blue;">联系:</span>

1. session_id储存在cookie中
2. 手动关闭浏览器cookie，session失效

## 五.数据库的三大范式
1. 不能没有主键
2. 每个属性不可再分
3. 不能有属性传递依赖


## 六.ajax状态码
```
输入状态码：console.log(xhr,readyState)
ajax的状态码：0初始值，1数据发送成功，2服务端已返回数据，3浏览器正在解析数据，4完成
http的状态码:200成功，404路径错误
```
ajax的流程：
1.创建ajax对象
2.Ajax初始化
3.设置头格式 发送请求方式为 键值对
4.设置回调函数  返回才调用的函数
5.执行ajax发送数据

----------------------------------------------------
## 七.jq的ajax语法
1.$.ajax-写法复杂，功能全面
2.$.post-写法简单，功能简单
3.$,get-写法简单，功能简单

```
ajax一个json参数(8个属性):$.ajax({
async:是否异步,url:提交地址,data:提交的数据,
type:提交方式,dataType:预期的服务端返回的类型,
success:成功的回调函数形参为返回的数据,
error:失败的回调函数,beforeSend:等待的回调函数})

post有4个参数:$.post("文件地址",{act:'del',uid=uid},funtion(data){ },"html")
1.发送地址 2.发送数据 3.成功的回调 4. 服务端返回的数据类型
```
```
ajax属性
$.ajax({
	async:true,//是否异步
	url:''//提交地址
	data:{name:admin,act:'check'}//提交的数据
	type:'post',//提交类型
	dataType:'html',//(json,xml,html)预期的服务端返回的类型
	success:function(data自定义名){
		//成功的回调函数 形参为返回的数据
	}，
	error:function(){//失败的回调函数},
	beforeSend:function(){//等待的回调函数},	
});
```

在一个server.php页面红处理多个ajax
if($act=='check'){//业务1}
if($act=='name'){//业务2}
...

============================================
## 八.封装
类的三种封装类型：
public公共的,无限访问修饰符
protected受保护的,类的外部无法使用
private私有的,类的外部无法使用，不能被继承

```
16种魔术方法（方法必须是public function）
构造方法1. __construct (new的时候自动执行)
public function __construct($参数1，$参数2...){}
析构方法2. __destruct()(对象被销毁之前执行，不能传参)
public function __destruct(){}	
销毁 unset(对象名)
方法3. __set (类的外部不可调用的属性赋值时自动执行,固定两个形参1.属性名2.值)
方法4. __get(类的外部对不可调用的属性取值时自动执行，一个参数，1.属性名)
方法5. __isset(类的外部判断不可调用的属性赋值时自动执行)
方法6. __unset(类的外部判断不可调用的属性赋值时自动执行)
方法7. __toString(当你把对象当成字符串去使用时自动执行)
方法8. __clone(在对象被克隆时自动执行)
方法9. __sleep(序列化对象时自动执行)
方法10. __wakeup(反序列化时自动执行)
方法11. __call(调用不存在的方法时自动执行，两个参数1.不存在的方法名2.传入的参数-数组)
方法12. __callStatic(用静态方式中调用一个不可访问方式时调用)
方法13. __autoload(尝试加载未定义的类)
方法14. __invoke(调用函数的方式调用一个对象时的回应方法)
方法15. __set_state(调用var_export()导出类时，此静态方法会被调用)
方法16. __debugInfo(打印所需调试信息)
```
> 构造方法在new的时候自动执行，设置了形参要在new的同时传入实参
> 栗子：
> public function __construct($name,$age,$sex){....}
> $zh=new 类名('小张','18','男')
<hr style="color:gray;">

> 析构方法在对象被销毁之前执行的方法（不可传参）
> 如果没有手动销毁，则在页面执行之后执行
> 栗子：
> public function __destruct(){echo "<hr>";}
> 如果没有unset()销毁对象，那么这个分隔符永远在页面最下面

->  对像的连接符号
=> 数组的连接符号

self 用来调用静态属性和方法
:: 范围解析操作符 用来调用静态属性和静态属性方法

serialize()方法通过序列化表单值，创建URL编码文本字符串


JSON的一般写法：
{name:'xiaozhang',age:'18'}
或者
O:6:"Person":{s:3:"sex";s:3:"男"；}

## 九.类的三大特性

封装(将函数和变量结合在了一起)
继承(类是可以继承的)
多态(多种形态)同一个父类 有多个子类 他们调用同一个方法 得到的结果



继承规则：
一个父类可以有多个子类 一个子类只能有一个父类
子类可以继承父类的所有非私有的成员

```php+HTML
<?php
class 名{
	//属性
    public $a;	//公共的,无限访问修饰符
	protected $b;	//受保护的,类的外部无法使用
	private $c;	//私有的,类的外部无法使用，不能被继承
    //方法
    public function __construct($max,值2,值3){
        $this->max=$max;
        $this->...
        $this->...
    }
}
?>
```



## 十.Class的普通属性和静态属性

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191027203125.png)
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191027203142.png)