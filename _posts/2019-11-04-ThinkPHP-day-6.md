---
layout: post
title:  "ThinkPHP-day6"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-11-04 11:10:40
---

# 第六天，数据库连接-1









* content
{:toc}
## 什么是端口？

> 所谓的端口，就好像是门牌号一样，客户端可以通过ip地址找到对应的服务器端，但是服务器端是有很多端口的，每个应用程序对应一个端口号，通过类似门牌号的端口号，客户端才能真正的访问到该服务器。 



## 常用的端口有哪些？

HTTP：80(www服务)<br>
DHCP：服务器端口67，客户机端口68<br>
POP3：25<br>
SMTP：23<br>
FTP：20(数据传输),23(控制信令的传输、控制信息和数据能够同时传输)|FTP采用的是TCP连接<br>
DNS：53<br>
mysql:3306<br>
Apache:2268<br>
QQ：8000(服务端)和4000端口(客户端)<br>
远程桌面：3389<br>

## 查看端口号的两种方式：

1任务管理器<br>
2.cmd>netstat -ano



## 数据库操作
一.查询的类<br>
	1. DB类-数据库基本的类|特殊方法：query，execute(执行原生的查询方法) <br>
	2. 模型类 <br>
二.查询构造器 <br>
	1. 链式操作-解决SQL语句如何拼接的问题 <br>
	2. 查询语音-解决where条件怎么写的问题 <br>
三.CURL方法 <br>
	1. C-数据创建|create <br>
	2. U-数据更新|update <br>
	3. R-读取|find,select <br>
	4. D-删除|delete <br>

## 基础的sql语句

```
public function db(){
//基本的sql语句
$sql = "select * from 表名";
$result = \think\Db::query($sql);
}
```

配置了数据库链接信息后可以直接使用数据运行原生SQL操作，<br>
支持 ```query``` (查询操作) 和 ```execute``` （写入操作）支持参数绑定

**参数绑定**

```
Db::query('select * from think_user where id=?',[8]);
Db::execute('insert into think_user (id, name) values (?, ?)',[8,'thinkphp']);
```
**命名占位符绑定**

```
Db::query('select * from think_user where id=:id',['id'=>8]);
Db::execute('insert into think_user (id, name) values (:id, :name)',['id'=>8,'name'=>'thinkphp']);
```

**多个数据库连接**

```
Db::connect($config)->query('select * from think_user where id=:id',['id'=>8]);
```


## 查询构造器

- 链式操作作用是生成标准的严谨sql语句
- 所有的连贯操作都返回当前的模型实例对象（this）其中带*标识的表示支持多次调用

```
        $result =Db::table('ecm_user')
            ->field('id')
            ->field('uname')
            ->field('upwd')
            ->where('id','=',18)
            ->order('id,desc')
            ->select();
```

【链式操作1】table，指定查询的表，直接写完整的表明：如果需要别名一般陪着alias来使用或者直接空格+别名。

```
$result=Db::table('ecm_users')->select();
$result=Db::table('ecm_users a')->select();//起别名
$result=Db::table('ecm_users')->alias('a')->select();
$result=Db::table('__USERS__')->select();//表前缀与系统默认的相同时：去掉表前缀，所有字母都大写。
```



【链式操作2】field*，可以重复使用，指定要查询的字段

>	1. 逗号分隔的字符串：'字段名1,字段名2,字段名3,...'<br>
>	2. 字段名的索引数组：['字段名1','字段名2','字段名3'...]<br>
>	3. 可以对字段夹别名：逗号分隔的字符串'uname as 别名'|'uname 别名'|['uname'=>'别名']<br>
>	4. 多次field方法查询多个字段<br>
>	5. field(true),显示查询全部字段，默认查询全部字段的内容，默认把全部字段都列出来<br>
>	    隐式查询可以不写field，直接为星号，这种方式查询在高仿问量的系统中效率极低，<br>
>	    一般我们要进行显示查询，指定相关字段查询，这样效率高，即使查询全部字段这种方式也高<br>
>	6. 排除默认写占用资源高的字段或者根据要求显示一部分字段但不显示的占少数，可以考虑使用field('排除的字段',true)<br>
>	7.字段上可以使用SQL函数<br>

```
$result=Db::table('ecm_users')->field('id,uname,email')->select();
$result=Db::table('ecm_users')->field('id','uname','tel')->select();
$result=Db::table('ecm_users')->field(true)->select();
$result=Db::table('ecm_goods')
	->field('goods_id,left(goods_name,3) as goods_info')
	->field('FROM_UNIXTIME(add_time, \'%Y-%m-%d %H:%i:%s') as add_times')
	->field('if(if_show,"上架","下架") as if_shows')
	->select();
```



## SQL中时间戳和本地时间互相转换

> select from_unixtime(1234567890,'%Y-%m-%d %H:%i:%s');

> select unix_Timestamp('2019-11-04 12:23:00');



## sql中的if判断

> if(exp1,exp2,exp3)//exp1是判断条件，exp2是条件true执行，exp3是条件false执行



## 实例化

> 详情[小豆丁博客]( https://www.cnblogs.com/xiaodouding/p/6801170.html )介绍

> 什么是实例化


## 实例化本身

```
public static function instance($options = [])
{
	if(is_null(self::$instance)){
		self::$instance = new static($options);
	}
	return self::$instance;
}
```
> static方法实例化本身

-----

## 实例化对象M()和D()的区别

> 参考

[ThinkPHP中实例化对象M()和D()的区别](https://www.cnblogs.com/geniusxjq/p/4137002.html)



------

![](https://f.sinaimg.cn/tech/transform/98/w640h258/20191104/13f8-ihuuxuu5583284.gif)