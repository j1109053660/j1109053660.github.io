---
layout: post
title:  "ThinkPHP-day4"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-10-31 16:03:40
---




# 视图层-2讲

* content
{:toc}












-----

-----

## 使用默认值

> 给变量提供默认值，例如：

```html
{$name|default="xxxx"}
```

>默认值和函数可以同时使用，例如：
```html
{$Think.get.name|getName|default="xxxx"}
```



-----

## 三元运算符

{$name? "yes":"no"}
在什么情况下执行三种false: ```未定义``` ， ```定义了没赋值``` ， ```空````

> 三种写法
>>{$status? '正常':'错误'}
>>{$info['status']? $info['msg']:$info['error']}
>>{$info.status?$info.msg:$info.error}


> 5.0还支持{$name.aa ?? 'xxxx'}




![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191223110030.png)




第一种情况：``` ？：```
```html+php
<{$status? '正常';'错误'}>
echo ！empty($sataus)?''正常;'错误'
```
简写:标准的三目判断 如果问号前面不写参数为输出判断的参数
```html+php
{$status?:'xxxx'}相当于{$status? $status:'xxxx'}
```

第二种情况: ``` ？？```
```html+php
{vaername.aa ?? 'xxxx'}
原生》echo isset($static) ?$status:'错误';
```

第三种情况 :``` ?=```   （只能输出判断表达式为真的情况）
```html+php
<{$status?='xxx'}>
原生》if(!empty($status)) echo 'xxxx';
```

第四种情况:  条件表达式 ``` ==,>=,<=``` 
```html+php
<{$a==$b ? 'yes':'no'}>
原生》 echo $a==$b?'yes':'no';
```



----
## tp的注释-literal
> html中的<!---->不适用tp，因为文档加载时优先加载tp代码。

{literal}  tp代码 {/literal}  
tp的内置标签，输出不用尖角号<{}>直接{}即可

<!---
多行注释 {/*       */}只能用于一个定界符内<{/*xxxxxxxx*/}>
模板单行注释<{//$sataus}>
-->

模板注释
1.只能注释同一个标签内
2.结束标记跟定界符之前可以有空格，但起始标记不能与定界符有任何空格
3.模板注释后在临时文件中是不显示的



-----

## 包含文件-include(内置标签）

{include file='模板文件1，模板文件2,.........' /}

参数1：模板表达式【模快@】【控制器/】【操作】

参数2：使用模板相对地址

模板包含:

1.模板表达式中对应的控制器，方法未必一定存在
2.如果模板文件中含有对应控制器赋值的变量，那么该变量需要在当前控制器中再次赋值；
3.包含文件中可以在使用include标签包含别的文件，但注意不要形成A包含A，或者A包含B而B又包含A这样的死循环。

## 三种接值方法

1.post接值

```
$post=$request->post();
$arr=$request->post('id/a');//接数组
```

2.get接值

```
$get=$request->get();
```

3.pathinfo接值

```
$id=$request->param('id/d');//接单值
```
> pathinfo不能接数组

-----

窝窝头。嘿嘿qwq

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1572519198973&di=08ecaf78c2ebd9f7d627f469c4fbe2d3&imgtype=0&src=http%3A%2F%2Fhiphotos.baidu.com%2Ffeed%2Fpic%2Fitem%2F472309f79052982240810c3fdbca7bcb0b46d49f.jpg)





