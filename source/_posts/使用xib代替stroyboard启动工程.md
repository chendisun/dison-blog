title: 使用xib代替stroyboard启动程序
date: 2015-09-11 17:49:05
categories:
- 学习
tags:
- swift
- iOS
---
## 新建一个swift工程
应该都懂怎么建一个swift工程，这里不详细啰嗦

<!--more-->

## 删除文件：
> 删除ViewController.swift文件
> 删除Main.storyboard文件

## 设置工程的Main interface 为空

如图
![](http://120.24.60.216:4000/img/20150911175830.png)

## 新建一个命名为mian的UIViewController，勾选Also create XIB file

![](http://120.24.60.216:4000/img/20150911175850.png)

## 修改AppDelegate.swift文件的application方法

```bash
application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        // Override point for customization after application launch.
        var viewController = Main(nibName: "Main", bundle: nil)
        var navigationController = UINavigationController(rootViewController: viewController)
        
        self.window = UIWindow(frame: UIScreen.mainScreen().bounds)
        self.window?.rootViewController = navigationController
        self.window?.makeKeyAndVisible()
        
        return true
}
```

这样就可以用我们自定义的xib代替storyboard启动工程了
