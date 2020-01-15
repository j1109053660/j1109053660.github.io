---
layout: post
title:  "ThinkPHP-day12"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2020-1-14 12:00:10
---

# 第12天，CURD









* content
{:toc}
## CURD的三种写法

1.第一种：Db类

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20200115110503.png)

2.第二种：Model动态

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20200115110519.png)

3.第三种：Model静态

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20200115110557.png)

在写项目时,常用写法:

* 创建和更新使用Model动态方法save()

* 查一条和多条使用Model静态方法get(),all()

* 删除使用Model静态方法destroy()

模型类与Db类的区别:

模型类具有修改器,获取器,自动完成,类型转换等高级操作,而Db类没有;





## 异常Exception

use think\Exception;

获取异常try{}catch(\think\Exception $e){//catch可以写多次}

**常用的属性:**

$this->error=$e->getMessage();

//调用模型类的一个属性error,并将抛出的异常信息,赋值到error属性中

  getLastInsID()

//作用是获取最后一次添加记录的主键(id)

allowField(true)类似链式操作的一种写法

//作用是在进行增加方法时,在用户提交的信息中将与数据库字段吻合的数据添加

### 在异常中使用三种方法新增

```
//测试是在控制器中,普通写法应该是在Model;
try{
	$data=[
		'name'=>'admin',
		'pwd'=>md5(123),
		'email'=>'110901678@qq.com'
	]
	//1.使用Db类新增
	$rt=Db::table('表名')->field(true)->insert($data);
	echo Db::getLastInsID();
	//2.使用模型静态-不推荐
	$rt=\app\index\model\Users::create($data);
	//3.使用模型动态-推荐
	$rt->allowField(true)->save($data);
	
}catch(\think\Exception $e){
	echo $e->getMessage();
}

```



## 拓展:static与self在实例化的区别

面向对象中new static 与new self区别:

1.写在类的本身时没有区别

2.写在类的继承时(例如下栗子)

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20200115120913.png)

当红框中是`self`时,最后echo 的是'Text'.

当红框中是`static`时,最后echo 的是'Zx'.