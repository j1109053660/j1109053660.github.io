---
layout: post
title:  "右键新增.md文件"
categories: win10
author: 滑稽兔啊
tags:  win10 Markdown Windows10 Typora
date:  2019-10-7 20:11:30
---
<h1>Windows下设置右键可新建.md文件</h1>
​      <span style="color:red">应用场景：Windows10，Typora(Markdown编辑器)</span>



> ​      因为习惯用Markdown来写文档, 所以常常需要新建.md文档,但由于Windows并不会自带把.md文档放入右键新建项中（像Word那样）
>

​      所以方便起见，自己手动设置，其实就是把它写进Windows的注册表。

* content
{:toc}








### 1.进入注册表编辑器win+r，输入regedit，回车。



选择第一项"HKEY_CLASSES_ROOT",点开。

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025191838.png)

### 2. 新建项



找到".md"项，此时该项应该是空的，“右键”，“新建”->“项”。
此时该“项”中会有一个默认的字符串值。



![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025191923.png)



### 3. 新建字符串值



选中刚才新建的项，“右键”，“新建”->“字符串值”

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025191947.png)



至此，设置完毕。关闭注册表编辑器。
在当前界面，“右键”->“新建”，可以看到"Markdown File" 选项了。

![](https://j1109053660.oss-cn-hangzhou.aliyuncs.com/img/20191025192041.png)