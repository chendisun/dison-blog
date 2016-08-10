title: 百度语言在线集成到iOS应用中
date: 2016-03-11 11:04:02
categories:
- 学习
tags:
- iOS 百度语言在线合成
---

## 背景
因领导需要在iOS应用上面集成语言集成播放，所以安排我着手做着方面的集成研究。下面我就把集成的过程记录下来，做不时之需。

<!--more-->

## 下载百度的语言在线合成sdk
百度语言集成sdk下载的地址，[sdk地址界面](http://yuyin.baidu.com/tts/download "sdk下载")

请下载图示的sdk

![](http://120.24.60.216:4000/img/20160311111224.png)

## 把解压后的必须文件复制到工程下
复制工程后，在Xcode里面把文件add到工程，做完这步我这里是如下的样子
![](http://120.24.60.216:4000/img/20160311112427.png)

## 引入编译需要的 Framework
在Xcode工程中引入 AVFoundation.framework 、SystemConfiguration.framework 、 MobileCoreServices.framework 、 CoreGraphics.framework 、Security.framework
![](http://120.24.60.216:4000/img/20160311112943.png)

## 把Library Search Paths指定到*.a所在的路径
如图所示
![](http://120.24.60.216:4000/img/20160311113128.png)

## 因为百度语言目前只支持iOS4到iOS7，为了避免出现不必要的错误，可以把工程的开发目标改为iOS6
如图
![](http://120.24.60.216:4000/img/20160311113510.png)

## 支持http协议
可以参考我的以前文章，[支持http协议地址](http://blog.disonchen.com/2015/12/22/7.1%E4%B8%AD%E4%BD%BF%E7%94%A8Http%E8%AF%B7%E6%B1%82/#more "支持http协议地址")

## 修改写百度语言代码的类的type
百度原话是
> 注意：静态库中采用 Objective C++实现，因此需要保证工程中引用静态库头文件实现文件的扩展名必须为.mm。


我这里是下面的
![](http://120.24.60.216:4000/img/20160311114405.png)

## 以下就是代码的实现了

* 首先在实现类的头文件里加入如下的代码
![](http://120.24.60.216:4000/img/20160311140015.png)
* 实现类的修改
![](http://120.24.60.216:4000/img/20160311140235.png)

好了，百度语言集成成功了！


# 参考自百度官方教程