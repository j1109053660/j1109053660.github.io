---
layout: post
title:  "ThinkPHP-day10"
categories: PHP
author: 滑稽兔啊
tags:  ThinkPHP
date:  2020-1-07 13:50:10
---

# 第九天，分页









* content
{:toc}
> $list=$db->paginate('每页显示条数'，true/false,['type'=>'bootstrap','var_page'=>'page','list_rows'=>15,]);



### 一，原生分页

1. 求总数

2. 总数÷每页条数，得到一个值向上取整，得出总数
3. limit 方法算一个起始结束位置
4. 计算分页链接





### 二，分页实现

> `Db`类查询的时候调用`paginate`方法：

```
// 查询状态为1的用户数据 并且每页显示10条数据<br>
2.$list = Db::name('user')->where('status',1)->paginate(10);<br>
3.// 把分页数据赋值给模板变量list<br>
4.$this->assign('list', $list);<br>
5.// 渲染模板输出<br>
6.return $this->fetch();<br>
//---------------------------------------
//模板输出{$list->paginate();}
```

> 模型的分页查询代码

```
// 查询状态为1的用户数据 并且每页显示10条数据
$list = User::where('status',1)->paginate(10);
// 把分页数据赋值给模板变量
list$this->assign('list', $list);
// 渲染模板输出return $this->fetch();
//---------模板文件输出--------------------------
<div>
<ul>
{volist name='list' id='user'}
    <li> {$user.nickname}</li>
{/volist}
</ul>
</div>
{$list->render()}
```

>单独赋值分页输出
```
// 查询状态为1的用户数据 并且每页显示10条数据
$list = User::where('status',1)->paginate(10);
// 获取分页显示
$page = $list->render();
// 模板变量赋值
$this->assign('list', $list);
$this->assign('page', $page);
// 渲染模板输出
return $this->fetch();
//----------模板文件分页输出---------------
<div>
<ul>
{volist name='list' id='user'}
    <li> {$user.nickname}</li>
{/volist}
</ul>
</div>
{$page}
```





### 三，分页参数

list_rows-每页数量 <br>

page-当前页<br>

path-url路径<br>

query-url额外参数<br>

fragment-url锚点<br>

var_page-分页变量<br>

type-分页类名<br>



### 四，分页循环

> each(function($item,$key){xxxxx})


```
$list=$db->paginate(5,false,[
'type'=>'bootstrap',
'vat_page'=>'page',
'query'=>$request->get(),
])->each(function($item,$key){
$item['goods_name']='【'.$item['cate_name'].'】'.$item['goods_name'];
});

```

