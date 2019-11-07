---
layout: post
title:  "ThinkPHP-day8"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-11-07 11:45:10
---

# 第八天，数据库连接-3









* content
{:toc}


## 【查询构造器】查询语句：表达式查询

表达式查询，三个参数，其中如果是等于的条件，可以省略等于的条件直接写两个参数

```
$result=Db::table('ecm_goods')
	->field(true)
	->where('descriptopn','null','')//select * from 'ecm_goods' where 'descriptopn' is null
	->where('descriptopn','')// 'descriptopn' = ''
	//特殊表达式
	//->where("left(goods_name,2)='杰记'",'exp','')//expression  引号内可以写原生表达式 ，left是从左截取
	->select();
```

```
$result=Db:table('ecm_users')->where('add_time','> time',13570128000)-select();
$result=Db:table('ecm_users')->where('add_time','> time','2015/11/12')-select();
```


**时间比较（字符串或者数字）常用的符号**

&gt;  time<br>
&lt;  time<br>
&gt;=  time<br>
&lt;=  time<br>
between  time<br>
notbetween  time<br>



## 【查询构造器】查询语句：数组查询

不推荐使用
['字段名1' =>['表达式'],\['值']，'字段名2'=>['表达式','值']]

```
$where=[
	'goods_id'=>['>',10],
	'price'	=>['<',50]
];

$map=[
	'goods_id'=>['>',20],
	'goods_name'=>['like','%杰记%']
];
$result=Db::table('ecm_goods')
	->where($where)
	->whereOr($map)
	->select();
//执行的sql语句
SELECT * FROM `ecm_goods` WHERE `goods_id` > 10 AND `price` < 50 OR `goods_id` > 20 OR `goods_name` LIKE '%杰记%'
```



## 【查询构造器】查询语句：闭包查询

闭包查询（匿名函数），可以使用一次闭包就代表了加了一次括号

```
$result=Db::table('ecm_goods')
	->where(function($query){
	$query->where('goods_id','between',[10,50])
	->whereOr('price','<',50);	
	})
	->where('goods_name','like','%杰记%')->select();
	
//执行的sql语句
SELECT * FROM `ecm_goods` WHERE ( `goods_id` BETWEEN 10 AND 50 OR `price` < 50 ) AND `goods_name` LIKE '%杰记%' 
```

> ->where(function($query){
>	$query->where(function($q){
>	$q->where('1=1')
>	})
>	})
> 闭包里还可以继续套闭包	



**在闭包中使用变量**

需要在括号外添加use引入
多层闭包需要多层引用

```
$key='杰记';
$goods_id=10;
$price=50;

$result=Db::table('ecm_goods')
	->where(function($query) use($goods_id,$price){
	$query->where(function($q) ues($goods_id)P{
	$q-where('goods_id','>',$goods_id)
	->where('goods_id','<',80);
	})
	->whereOr('price','<',$price);	
	})
	->where('goods_name','like','%'.$key.'%')->select();
```









