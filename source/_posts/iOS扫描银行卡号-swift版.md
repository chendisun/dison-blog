title: iOS实现信用卡号扫描-swift版
date: 2015-11-02 11:43:15
categories:
- 学习
tags:
- swift iOS 
---

## 下载第三方的组件CaidIO

* 实现信用卡号的扫描使用的是第三方的包，详细的简介可以到github上查看，在github搜索CardIO就行，这里提供百度网盘的下载地址：[CardIO](http://pan.baidu.com/s/1jGGWiCu "")
下载好之后解压，后续导入到我们的项目中。

<!--more-->

* 把链接目标Build Setting - Linking - Other Linker Flag : -lc++
   如图：![](http://120.24.60.216:4000/img/20151102113923.png)
* 导入相关的框架，详细如图
![](http://120.24.60.216:4000/img/20151102114045.png)

## 创建一个object-c的文件，桥接CardIO的头文件
只要输入一行代码，就可以把oc代码翻译成了swift的代码了
``` bash
#import "CardIO.h"
```

## 搭建简单的页面，在主界面里面直接拖一个按钮和一个label，按钮触发扫描的开始

button的IBAction方法添加下面的代码
``` bash
//构造controller
let cardIOPVC = CardIOPaymentViewController(paymentDelegate: self)
//设置样式
cardIOPVC.modalPresentationStyle = UIModalPresentationStyle.FormSheet
//启动扫描界面
presentViewController(cardIOPVC, animated: true, completion: nil)
```
## 主页面实现CardIOPaymentViewControllerDelegate协议

实现协议的方法
``` bash
func userDidCancelPaymentViewController(paymentViewController: CardIOPaymentViewController!) {
    result.text = "Cancel!!!"
    paymentViewController.dismissViewControllerAnimated(true, completion: nil)
}

func userDidProvideCreditCardInfo(cardInfo: CardIOCreditCardInfo!, inPaymentViewController paymentViewController: CardIOPaymentViewController!) {
    if let info = cardInfo {
         result.text = info.cardNumber
    }
        
    paymentViewController.dismissViewControllerAnimated(true, completion: nil)
}
```
## 到这里就可以实现信用卡的扫描并且返回结果了

[项目地址](https://github.com/chendisun/CardIOTest.git "")



# 转发请标明出处，谢谢！