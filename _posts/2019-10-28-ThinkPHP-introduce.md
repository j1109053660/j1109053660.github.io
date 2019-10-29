---
layout: post
title:  "ThinkPHP介绍"
categories: PHP
author: 滑稽兔啊
tags:  web php ThinkPHP
date:  2019-10-28 21:16:57
---

[TOC]

## ThinkPHP V5.0













一、什么是ThinkPHP

ThinkPHP是一个免费开源的，快速、简单的面向对象的轻量级PHP开发框架

二、六大特性

	1. 规范：遵循PSR-2、PSR-4规范，Composer及单元测试支持；
 	2. 严谨：异常严谨的错误监测和安全机制、详细的日志信息，为你的开发保驾护航；
 	3. 灵活：减少核心依赖、拓展更灵活、方便、支持命令行指令拓展；
 	4. API友好：出色的性能和REST支持、远程调试、更好的支持API开发；
 	5. 高效：惰性加载及路由、配置和自动加载的缓存
 	6. PRM：重构的数据库、模型及关联， MongoDb 支持；

> Composer：
>
> >是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。


三、环境

1.window/unix/linux服务器环境
2.PHP>=5.4
3.开启PDO拓展
4.开启MBstring拓展
5.开启CURL拓展


四、入口文件

ThinkPHP位与```public/index.php```(实际部署的目录就是对外访问目录)
```php
// 定义应用目录
define('APP_PATH', __DIR__ . '/../application/');
// 加载框架引导文件
require DIR'//thinkphp/start.php
```

> ThinkPHP开发第一步代码默认即可不用改动.

五、命名规范
> ThinkPHP5.0 遵循 ```PSR-2``` 命名规范和 ```PSR-4``` 自动加载规范，并注意一下规范：

**目录和文件：**

目录使用小写+下划线；

类库、函数文件统一以 ```.php``` 为后缀；

类的文件名均以命名空间定义，并且命名空间的路径和类库文件所在的路径一致；

类文件采用大驼峰命名，其他文件采用小写+下划线

类名和文件名保持一致，通知采用大驼峰

**函数和类、属性命名**

类的命名采用大驼峰，例如UserType;

函数的命名使用小写字母和下划线(小写字母开头)，例如get_class;

方法的命名使用小驼峰，例如getUserName;

属性的命名使用小驼峰，例如tableName;

以双下划线 ‘__’  打头的函数或者方法作为魔术方法，例如__call；

**常量和配置**

常量以大写字母和下划线命名，例如APP_PATH；

配置参数以小写字母和下划线命名，例如url_route;



六、 下载地址

[ThinkPHP](http://www.thinkphp.cn/)
[5.0完全开发手册](https://www.kancloud.cn/manual/thinkphp5/118003)

