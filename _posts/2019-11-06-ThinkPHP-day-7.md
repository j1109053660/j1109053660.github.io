---
layout: post
title:  "ThinkPHP-day7"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-11-06 12:08:10
---

# 第七天，数据库连接-2









* content
{:toc}

* Similar Posts
{:toc}
## SQL中联表的三种方式

> 内联，外联（左联-右联）

左联与右联的区别：<br>
左联方式：在左表为主的数据和右表的数据展示出来<br>
右联方式：以右边为主查询数据，左表和右表有关联的数据展示出来，相同字段起别名区分。<br>



## 【链式操作】join*

> Db::table(表名)->alias(别名)->field(查找的字段)->join(要联的表名，字符串方式定义，不带数据表前缀的表名)；

>参数1：要联的表名 <br>
>		①数组方式定义，[' ```ecm_goods'=>'g'``` ],【任何时候都没有BUG】<br>
>		②字符串方式定义，‘ ```ecm_goods g``` ’ ,【当默认的表前缀与当前要联的表不一致时会自动加前缀，造成BUG】<br>
>		③不带数据表前缀的表名，‘ ```__GCATEGORY__ c``` ’ <br>
>参数2：联表的条件，按照where的条件定义方式来写 <br>
>参数3：联表方式。LEFT、RIGHT、INNER(默认)，当数据不存在时填充null <br>


:arrow_down_small:
```
$field=['goods_id','goods_name','price','c.cate_id','cate_name','parent_id','g.if_show'];
$result=Db::table('ecm_goods')
		->alias('g')
		->field($fielf)
		->join(['ecm_gcategory'=>'c'],'g.cate_id=c.cate_id and c.if_show=1','LEFT')
		->select();
```

> 注意两个表相同的字段必须显示指明使用的哪个字段，如if_show 必须写成 ```g.if_show``` <br>
> 注意两个表相同的字段作为where的查询条件时，如 ```if_show = 1``` ，这个时候必须加别名或者表名指明是哪个表的字段 ```g.if_show = 1```



## 【链式操作】order*

参数：排序的规则，逗号分隔的字符串或者数组

```
$result=Db::table('ecm_goods')
	->field(true)
	->order('goods_id desc,add_time desc')
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	->order('goods_id'=>'desc','add_time'=>'desc')
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	//->order(['goods_id'=>'desc'])
	//->order('add_time')
	->orderRaw('rand()')//随机排序
	//->find();只渲染一条数据
	->select();
```



## 【链式操作】limit

```
$result=Db::table('ecm_goods')
	->field(true)
	->limit('0,10')
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	->limit(0,10)
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	->limit(10)
	->select();
```



## 【链式操作】page,一般用于分页查询

```
$result=Db::table('ecm_goods')
	->field(true)
	->page('2,10')
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	->page(2,10)
	->select();
$result=Db::table('ecm_goods')
	->field(true)
	->page(2)
	->limit(10)
	->select();
```



## 【链式操作】group,having

```
$result = Db::table('ecm_goods')
		->filed('goods_id,goods_name,cate_id,count(cate_id) as total')
		->where('goods_id','<=',50)
		->group('cate_id')
		->having('total>5')
		->select();
```


## 【查询构造器】查询语言

查询语言：2个方法（where,whereOr） 3个用法（表达式查询，数组查询，闭包查询）

```
$result = Db::table('ecm_goods')
		//->filed(true)
		->where('goods_id','>',1)
		->where('price','<',10)
		->select();
```

```
$result = Db::table('ecm_goods')
		//->filed(true)
		->where('goods_id','between','1,5')
		//->where('goods_id','between',[1,5])
		//->where('goods_id','in','[1,2,3,5]')
		->select();
```



# 链式方法注意事项

- 链式方法支持所有的CURD操作；<br>
- 链式方法本身只是返回查询对象，只有执行查询后才会返回结果，而且只能在查询方法之前被调用；<br>
- 不同链式方法的调用顺序不影响查询；<br>
- 相同链式方法的调用顺序可能会影响查询（至少会影响SQL语句）<br>
- 链式方法在完成查询后会自动失效；<br>
- 同一个链式方法在CURD操作中的作用可能不同；<br>
- 链式方法仅针对CURD方法，对原生查询无效；<br>


