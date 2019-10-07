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











### 1.进入注册表编辑器win+r，输入regedit，回车。



选择第一项"HKEY_CLASSES_ROOT",点开。

[![Snipaste_2019-10-07_15-39-589555e.png](https://miao.su/images/2019/10/07/Snipaste_2019-10-07_15-39-589555e.png)](https://miao.su/image/ik4xQ)

### 2. 新建项



找到".md"项，此时该项应该是空的，“右键”，“新建”->“项”。
此时该“项”中会有一个默认的字符串值。



[![Snipaste_2019-10-07_17-20-44ac2bf.png](https://miao.su/images/2019/10/07/Snipaste_2019-10-07_17-20-44ac2bf.png)](https://miao.su/image/ik9Bz)

### 3. 新建字符串值

选中刚才新建的项，“右键”，“新建”->“字符串值”
[![Snipaste_2019-10-07_17-21-01f2742.png](https://miao.su/images/2019/10/07/Snipaste_2019-10-07_17-21-01f2742.png)](https://miao.su/image/ikK2H)

至此，设置完毕。关闭注册表编辑器。
在当前界面，“右键”->“新建”，可以看到"Markdown File" 选项了。

[![Snipaste_2019-10-07_17-21-4950200.png](https://miao.su/images/2019/10/07/Snipaste_2019-10-07_17-21-4950200.png)](https://miao.su/image/ikrrb)