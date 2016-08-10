title: 使用React Native 构建app
date: 2015-09-24 20:32:05
categories:
- 学习
tags:
- Android
- iOS
- React Native
---
## React Native的优势和劣势（借鉴网络）：

* React Native的优势：

> 相对Hybird app或者Webapp：
> 1. 不用Webview，彻底摆脱了Webview让人不爽的交互和性能问题
> 2. 有较强的扩展性，这是因为Native端提供的是基本控件，JS可以自由组合使用
> 3. 可以直接使用Native原生的「牛逼」动画（在FB Group这个app里面，面板滑出带一点果冻弹动，面板基于某个点展开这种动画随处可见，这种动画用Native code来做小菜一碟，但是用Web来做就难上加难）。
> 相对于Native app：
> 可以通过更新远端JS，直接更新app，不过这快成为各家大型Native app的标配了…

* 劣势：

> 扩展性仍然远远不如web，也远远不如直接写Native code（这个不用废话解释了吧）
> 从Native到Web，要做很多概念转换，势必造成双方都要妥协。最终web要用一套CSS的阉割版，Native要费劲地把这个阉割版转换成native原生的表达方式（比如iOS的Constraint\origin\Center等属性），两边都会不爽。

<!--more-->

## 搭建环境
这个环境搭建很简单，网上有很多教程，这里就不多说了，官方的文档介绍主要需要安装nvm, Node.js 4.0, watchman, flow。
在mac环境下安装了Homebrew，这些东东是很容易安装的。

## 开始 Hello World

环境准备好了之后，在终端直接输入

~~~bash
$ react-native init Test
$ cd Test/
~~~
如果是运行iOS平台，使用Xcode打开iOS工程直接运行即可。
iOS运行结果如下：
![](http://120.24.60.216:4000/img/20150924094142.png)
如果出现```Unable to download JS bundle```即是没有启动server端，在Test的目录下执行
~~~bash
react-native start
~~~
至此，iOS的运行应该没问题了。
恭喜你，React Native安装成功！

如果只是iOS版本，总感觉少了什么，也体现不出React Native优势所在，React Native就是跨平台开发的，人家 React Native 的重点放在所有开发人员关心的平台的开发效率上——开发者只需学习一种语言就能轻易为任何平台高效地编写代码。
Facebook也很给力，2015年9月15号比预计提前发布了安卓版本，那么激动人心的安卓运行就要来了。

## Android 调试

首先请插入你的调试机器。之后在Test目录下运行
~~~bash
$ react-native run-android
~~~
激动了半天，结果居然是构建失败，此刻的心情就像是准备提枪上阵的时候，妹子居然穿衣服走人了一样。
泪水不能解决问题，查看失败的原因，原来是```> failed to find Build Tools revision 23.0.1```，即是Android sdk 没有23版本，操蛋啊，要更新这个鬼，天朝的局域网，呵呵。
一顿折腾之后，终于把该死的sdk更新了，这下，小妞你跑不了了吧！

再次执行
~~~bash
$ react-native run-android
~~~

app终于构建成功了，但是该死的，有出现了```Unable to download JS bundle```，检查server端已经开启了。
![](http://120.24.60.216:4000/img/20150924104521.png)

一番折腾，此处省略10000字国骂。。。。。。。。

明明按照步骤执行的，为啥就不行了呢？？？拿着我的烂三星，突然想到太妈的网络不一致啊，怎么可能加载得了js啊，你是猪吗？我想到了这句台词。

查找Facebook文档说真机调试要执行
~~~bash
$ adb reverse tcp:8081 tcp:8081
~~~

再次操蛋的是，我运行后居然打印
~~~bash
error: closed
error: closed
~~~
什么鬼，我就好欺负吗？？？为啥我的就不行？？？
好吧，我上Google再看看，原来是我的机器是Android4.4的，而上面的命令只适合Android5.0，此刻，心中一万个草泥马奔腾而过。
要解决上面的问题只能在手机上面输入server端ip。好吧，来吧。

* 晃动手机，在出现的菜单选择```Dev Settings```，之后选择```Debug server host for device```，在弹出的窗口中输入server端的ip，之后再```Reload JS```就可以愉快地玩啥了！！！

至此，两个平台的app都可以爽快的运行调试了。之后你想干嘛就干嘛啦，你懂的！


# 转发请标明出处，谢谢！