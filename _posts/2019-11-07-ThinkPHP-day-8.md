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


## 数据库操作
![](C:\Users\o.o\Desktop\Snipaste_2019-12-31_09-11-55.png)

### 查询语言的2个方法，3个用法，8个要诀
**两个方法：**where,whereOr<br>
**三个用法：**表达式查询，数组查询，闭包查询<br>
**八个要诀：**<br>
•查询条件的调用次序就是生成SQL的条件顺序；<br>
•查询字段用&分割表示对多个字段使用AND查询；<br>
•查询字段用|分割表示对多个字段使用OR查询；<br>
•对同一个查询字段多次调用非等查询条件会合并查询；<br>
•闭包查询和EXP查询会在生成的查询语句两边加上括号；<br>
•用闭包查询替代3.2版本的组合查询；<br>
•除了EXP查询外，其它查询都会自动使用参数绑定；<br>
•如果查询条件来自用户输入，尽量使用表达式和闭包查询，数组条件查询务必使用官方推荐的方法获取变量；<br>





## 【查询构造器】查询语句：表达式查询

表达式查询，三个参数，其中如果是等于的条件，可以省略等于的条件直接写两个参数

```
$result=Db::table('ecm_goods')
	->field(true)
	//->whereOr('goods_name','like','%thinkphp%')
	//->where('goods_id','>',1)
    //->where('goods_id','<',10)
    //->where('goods_id','<>',10)
    //->where('goods_id','between',[1,5])
    // ->where('goods_id','in','1,2,3,4,5')
    // ->where('goods_id','in',[1,2,3,4,5])
    //->where('goods_id',null)
	->where('descriptopn','null','')//select * from 'ecm_goods' where 'descriptopn' is null
	->where('descriptopn','')// 'descriptopn' = ''
	//特殊表达式
	//->where("left(goods_name,2)='杰记'",'exp','')//expression  引号内可以写原生表达式 ，left是从左截取
	//exp-表达式查询。原生的sql可以写在前面的参数或者后面的参数，唯一不能做的就是拆开写。
	->select();
```

```
$result=Db:table('ecm_users')->where('add_time','> time',13570128000)->select();
$result=Db:table('ecm_users')->where('add_time','> time','2015/11/12')->select();
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





-----

​			>>END

![](https://n.sinaimg.cn/tech/transform/737/w400h337/20191106/0a22-ihyxcrp8739915.gif)





