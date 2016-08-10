title: Android反编译
date: 2016-03-11 14:20:13
categories:
- 学习
tags:
- Android
---

## 背景
有时做一些研究性的工作，需要反编译Android的app学习别人的代码，所以下面记录一个我学习到的反编译教程。

<!--more-->
下文所有的工具都可以在我提供的工具包里面找到，[工具下载](http://120.24.60.216:4000/resources/安卓反编译工具.zip "下载工具")


## 使用apktool工具对安卓应用就行资源的反编译

apktool工具可以对APK进行反编译生成程序的源代码和图片、XML配置、语言资源等文件

~~~bash
java -jar apktool_2.0.3.jar d -f xxx.apk <反编译后的路径，可以不指定（默认当前目录）>
~~~

## 解压dex2jar-2.0.zip包，使用dex2jar把apk转换成jar包

~~~bash
# tar -zxvf dex2jar-2.0.zip
# cd dex2jar-2.0
# sh d2j-dex2jar.sh xxx.apk
~~~

执行完以上命令会在dex2jar-2.0目录下发现多了一个xxx-dex2jar.jar的文件

## 使用JD-GUI工具打开生成的jar文件，就可以到反编译后的代码

JD-GUI工具还可以把代码保存下来，之后把第一步反编译得到的资源文件和代码全部导入到一个新的安卓工程里面，这样就可以整合成一个安卓工程了。
到这里你想干嘛就可以干嘛了啦！！！




# 参考自百度资料，转发表明出现，谢谢！