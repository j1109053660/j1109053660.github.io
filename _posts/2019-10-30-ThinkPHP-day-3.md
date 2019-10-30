---
layout: post
title:  "ThinkPHP-day3"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2019-10-30 15:25:12
---



# 视图层













**渲染模板输出**

```html
return $this->fetch('str',['name'=>'thinkphp']);
```
------


**助手函数**

> 渲染模板输出的话，可以使用系统提供的助手函数view，完成相同的功能：
>
> return view('hello',['name'=>'thinkphp']);

-----
【渲染模板】模板文件的存在不需要对应的控制器和方法存在
参数1：模板文件
```html
①不写；默认的规则，渲染当前模块下的当前控制器的当前方法对应的模板；
> return $this->fetch();
②模板表达式或者模板渲染方式：[模块@][控制器/][操作],可以从左向右省略，控制器和方法名次采用小写+下划线的方法.
> return $this->fetch('admin@goods/index')
③相对路径：相对于入口文件为起始的相对路径
> return('..\\application\\index\\view\\index\\index.html');
```

参数2：模板变量(数组)，第一维一定是关联数组，相当于批量赋值的写法
```html+php
fetch('[模板文件]'[,'模板变量(数组)'])
// 第二个数值可以不写，逗号占位
> return $this->fetch('','people'->'PRC');
视图代码：<{$people}>
```

参数3：模板输出替换(数组) ['__IMG__'=>'/static/img']
```html+php
return $this->fetch('',[参数2],['__IMG__'=>'/static/img']);
```



-----

**查看Think的版本**

```html
视图代码：
<{$Think.Version}>
```



-----

**URL生成**在控制器或者php代码种尽量使用类的静态调用方式（速度快）

```html+php
参数①：地址表达式，[模块/][控制器/][操作]，作用是为了生成URL地址而存在，控制器和方法名遵循控制器和方法的起名原则(驼峰法)
> use think\Url; //导入url
> echo \think\Url::build('admin/Goods/showMsg');
//可以简写不用引用
> echo url();
参数②：参数，URL链接上的参数，采用关联数组方法定义
参数③：伪静态后缀，默认值(true)是输出html，如果不想要后缀可以使用false或者‘’;
> echo \think\Url::build('admin/Goods/showMsg',['id'=>11,'name'=>'zhuoxiang'],'true');
//最后的参数是后缀名，可以填jsp,true,false,'';
参数④：是否显示域名,默认为false不显示域名，显示当前域名可以写true，或者直接写域名
> echo Url::build('admin/Goods/showMsg',['id'=11,'name'=>'zhuoxiang'],true,'www.baidu.com');
//最后参数是自定指定的链接
```



-----

**使用管道符**

```html+php
①使用管道符|来表示函数，模板变量|函数名=参数。
函数只有一个参数或者单多个参数在第一位时，可以不写这个参数或者用###占位
函数支持嵌套执行，从左向右顺序执行
* <{$name|md5|strtoupper|substr=###,1,10}>
* <?php echo substr(strtoupper(md5($name)),1,10);?>
②使用冒号：形式输出函数(跟原生的PHP使用函数方式一致，只是在前面加了一个冒号)，:函数名(参数...)
```

> 视图代码 


![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191030152625.png)


> 控制代码


![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191030152646.png)


> 网页显示


![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191030152717.png)





-----

> > > > > > > > > > > > > > > > end 