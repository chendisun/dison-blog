title: linux下vi操作文件Found a swap file by the name
date: 2015-09-12 19:25:05
categories:
- 学习
tags:
- linux
---
## 在linux下用vi打开Test.java文件时
~~~bash
vi Test.java
~~~

会出现Found a swap file by the name ".Test.java.swp" 

原因是我之前有一次使用vi 操作Test.java文件时出现了异常中断，所以在当前目录下产生了一个.Test.java.swp文件
但是我使用ls命令查看该目录下，却发现没有这个文件，后来使用ls -a命令查看才知道Test.java.swp是一个隐藏文件。

现在只要把.Test.java.swp文件删除就可以可以了，这样就不会再出现上面的提示

~~~bash
rm .Test.java.swp
~~~