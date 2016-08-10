title: 简化 Storyboard
date: 2015-11-03 11:01:15
categories:
- 学习
tags:
- swift iOS 
---

在学习iOS开发的过程中，平时的界面布局都是使用Storyboard的，突然想到这样布局有个不好的地方，假如界面复杂了，
管理起来很不方便，并且在团队开发的过程很操蛋，每个人都修改一下，在代码提交的时候那真的是要骂娘了。幸好，iOS9提供了Storyboard References这个概念！！！
这里简单记录一下我的学习过程。
<!--more-->

## 首先创建一个简单的项目，进行一些前驱的布局

完整的[项目地址](https://github.com/chendisun/Storyboard.git "")
下面是我先布局截图，有点模糊，将就看吧，详细可以看项目里面的Main1.Storyboard
![](http://120.24.60.216:4000/img/20151103110010.png)


## 开始简化
这里我使用了TabBarController作为初始的viewController。这个TabBarController拥有两个NvigationController，每个对应一个不同的根ViewController，
每个ViewController里面都一个按钮可以去到一个共同的ViewController。

> 这里的思路是先把todo的ViewController单独抽为一个Storyboard，选中这个ViewController（高亮为选中），点击Xcode的导航栏，选择``` Editor->Refactor to Storyboard ```
> 这里给Storyboard起名为Todo，创建后，新的Storyboard呈现打开的状态

![](http://120.24.60.216:4000/img/20151103160455.png)

这个时候Main1.Storyboard里面的那两个ViewController都是指定到一个外接Storyboard了

> 之后把TabBarController左边的流程抽取到一个新的Storyboard里，选择所要抽取的NvigationController和ViewController（高亮为选中），选择 Editor->Refactor to Storyboard
> 这里给Storyboard起名为One，创建后，新的Storyboard呈现也是打开的状态

![](http://120.24.60.216:4000/img/20151103161035.png)

> 同理把另一个流程也抽取了

![](http://120.24.60.216:4000/img/20151103161226.png)

> 这时Main.Storyboard剩余为

![](http://120.24.60.216:4000/img/20151103161333.png)

到这里这个重构让我们的Storyboard变的更加的简单化，模块化，组件化。可以帮助我们后面更好的开发这个应用

## 跳转到新建的Storyboard

上面的方式是抽取已有的Storyboard的，那么假如我们要新增一个Storyboard，再通过指定的按钮跳转，要怎么实现呢？

> 新建一个Three.Storyboard，里面什么都不用干，只是简单的一个ViewController和一个Label

![](http://120.24.60.216:4000/img/20151103170057.png)

> 回到Two.Storyboard，添加一个Bar Button，起名为Three，用来跳转的。拖建一个Storyboard Reference，Storyboard 属性选为“Three”，把 Referenced ID 属性设置为“ThreeViewCL”
> 选中“Three”的按钮，按住 Control 健和鼠标左键，拖拽到 storyboard reference上，创建了一个 segue。
> 选中Three.Storyboard，设置 Storyboard ID 为 “ThreeViewCL”，这样就可以实现了跳转。

![](http://120.24.60.216:4000/img/20151103171005.png)

# 转发请标明出处，谢谢！