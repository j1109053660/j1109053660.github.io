---
layout: post
title:  "ThinkPHP-day9"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-11-08 16:08:10
---

# 第九天，数据库连接-4









* content
{:toc}
## 复习-查询构造器


查询构造器分为：链式操作，查询语言


![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191111090904.png)



## 【高级查询技巧】获取SQL语句

报错信息
![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191111090830.png)

解决办法：添加fetchSql(true)
> 返回的是sql语句（字符串）

```
方法1：链式操作之一
$result=Db::table('ecm_users')
	->where('ids','>',20)
	->fetchSql(true)
	->select();
方法2：数据库类的方法返回sql语句并在两端多了括号
$result=Db::table('ecm_users')
	->where('ids','>',20)
	->buildSql();
```





## 【高级查询技巧】*聚合查询

五个函数：sum,avg,count,min,max 	=>	limit 1
> 返回的是字符串

```
//参数可选的方式，不写参数为count(*)
$result=Db::table('ecm_goods')->field(true)->count();
// SELECT COUNT(*) AS tp_count FROM `ecm_goods` LIMIT
//参数可选的方法，写参数count(id)
$result=Db::table('ecm_goods')->field(true)->count('goods_id');
// SELECT COUNT(*) AS tp_count FROM `ecm_goods` LIMIT 1

//sum 和 avg
$result=Db::table('ecm_goods')->field(true)->sum('price');
// SELECT SUM(price) AS tp_sum FROM `ecm_goods` LIMIT 1
$result=Db::table('ecm_goods')->field(true)->avg('price');
// SELECT AVG(price) AS tp_sum FROM `ecm_goods` LIMIT 1
```

> count例子中field链接没有用，查询时可以省略





## 【高级查询技巧】*快捷查询-不同字段
不同字段的相同值的查询，多个字段之间用|分隔表示OR查询，用&分隔表示AND查询

```
$result=Db::table('ecm_goods')
	->field(true)
	->where('goods_id&if_show&recommended','=',1)
	//WHERE ('goods_id' = 1 AND 'if_show' = 1 AND 'recommended' = 1)
	->where('if_show|recommended','=',1)
	//WHERE('if_show' = 1 OR 'recommended','=',1)
	->select();
```





## 【高级查询技巧】*快捷查询-相同字段
相同字段的不相同值的查询

```
$result=Db::table('ecm_goods')
	->field(true)
	->where('goods_id',['>=',1],['<=','10'])
	->where('goods_name',['like','%杰记%'],['like','%海泉%'],['like','%0%'],'OR')
	->select();
// ( `goods_id` >= 1 AND `goods_id` <= 10 ) 
//( `goods_name` LIKE '%杰记%' OR `goods_name` LIKE '%海泉%' OR `goods_name` LIKE '%0%' ) 
```





## 【高级查询技巧】快捷表达式查询

```
$result=Db::table('ecm_goods')
	->field(true)
	//->where('goods_id','in',[1,2,3,4,5,6])
	->whereIn('goods_id',[1,2,3,4,5,6])
	->select();
```



|	方法	|	作用	|
|--|--|
|whereNull|查询字段是否为Null |
|whereNotNull| 查询字段是否不为Null|
|whereIn|字段IN查询 |
|whereNotIn|字段NOT IN查询 |
|whereBetween|字段BETWEEN查询|
|whereNotBetween|字段NOT BETWEEN查询 |
|whereLike|字段LIKE查询 |
|whereNotLike|字段NOT LIKE查询 |
|whereExists|EXISTS条件查询 |
|whereNotExists|NOT EXISTS条件查询 |
|whereExp|表达式查询|




## 【高级查询技巧】*快捷查询-时间表达式

whereTime('日期字段名'，‘日期表达式’)

```
$result=Db::table('ecm_goods')
	->field(true)
	->whereTime('add_time','>','2019-11-08')
	->whereItme('add_time','d')
	->select();
```


支持的日期表达式包括：

|today或d |今天 |
|-------|--|
|week或w |本周 |
|month或m| 本月|
|year或y |今年 |
|yesterday| 昨天 |
|last week |上周 |
|last month |上月 |
|last year |去年 |
|-2 hours |查询两个小时内|
|10 hours ago |10小时之前到先到|



## 【高级查询技巧】动态查询

查询方法不是链式操作，要做为每次查询的最后一次调用的方法来使用,查询条件都是值等“=”

|动态查询|描述|
|--|--|
| `getByFieldName` |(根据某个字段查询)|
| `getFieldByFieldName` |(根据某个字段获取某个值)|



- 根据字段的值查询记录（仅一条记录，默认排序规则的第一条），
- `-> getByFieldName(值)` 返回值为一维数组|NULL 相当于find方法


```
$result=Db::table('ecm_goods')
	->field('description',true)
	->getByGoodsId(1);
//WHERE 'goods_id' = 1 LIMIT 1
```


- 根据字段的值查询某个字段的值（仅一条记录，默认排序规则的第一条），
- `-> getFieldByFieldName(值,字段名)` 返回值为字符串|整型|NULL 相当于find方法

```
$result=Db::table('ecm_goods')
	->field('description',true)
	->getFieldByGoodsId(111,'goods_name');
//SELECT 'goods_name' FROM 'ecm_goods' WHERE 'goods_id' = 1 LIMIT 1
```





## 【高级查询技巧】*子查询

**1. 子查询作为新表进行查询**

```
$sql=Db::table('ecm_goods')
	->field(true)
	->where('goods_id','<',50)
	->buildSql();
$result=Db::table($sql.' a')
	->where('price','<',20)
	->select();
//该例子为简单方式教学，通常第一个查询是很复杂（三表或多表联查）
```



**2.子查询作为字段进行查询**

```
$sql=Db::table('ecm_gcategory')
	->alias('g')
	->field('cate_id')
	->where('c.cate_id=g.parent_id','exp','')
	->limit(1)
	->buildSql();
$result=Db::table('ecm_goods')
	->alias('c')
	->field('cate_id,cate_name,parent_id')
	->field('if('.$sql.',1,0) as has_next')
	//->field('if(select cate_id from ecm_gcategory g where c.cate_id=g.parent_id limit 1),1,0) as has_next')
	->where('c.parent_id',0)
	->select();

```



**3.子查询作为查询条件，只会多数用于whereIn的条件中**

```
$result=Db::table('ecm_goods')
	->field('goods_id,goods_name.price')
	->whereIn('goods_id',function($query){
		$query->table('ecm_users')
			->field('id')
			->where('uname','like','%a%')
	})
	->select();
```







-----

​										**>>END**

-----

![](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3896930462,1404021441&fm=26&gp=0.jpg)













