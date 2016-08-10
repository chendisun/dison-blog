title: 用命令行在iOS应用中集成Alamofire（网络请求框架）
date: 2015-12-23 11:43:35
categories:
- 学习
tags:
- Xcode iOS Alamofire
---

## 背景
iOS项目一般都要联网的，所以本教程是Swift工程集成Alamofire进行网络请求。

<!--more-->

## 安装 Cocoapods
在终端理直接输入下面的命令
~~~bash
gem install cocoapods
~~~

## 创建Podfile文件

在工程的目录下面创建Podfile文件
~~~bash
vi Podfile
~~~
在Podfile文件里面输入
~~~bash
source 'https://github.com/CocoaPods/Specs.git'
 
platform :ios, '8.0'
 
use_frameworks!
 
pod 'Alamofire', '~> 3.0'
~~~
保存退出Podfile，执行
~~~bash
pod install
~~~
当终端输出类似下面的内容的时候就成功了。
![](http://120.24.60.216:4000/img/20151223115020.png)
## 关闭当前的所以Xcode
关闭当前打开项目的Xcode，之后点击工程的XXXX.xcworkspace打开工程
## Alamofire的使用

下面的是Alamofire的GET和POST的使用方法

* GET方式
~~~bash
Alamofire.request(.GET, "urlStr") .responseJSON { response in // 1
      print(response.request)  // original URL request
      print(response.response) // URL response
      print(response.data)     // server data
      print(response.result)   // result of response serialization

      if let JSON = response.result.value {
         print("JSON: \(JSON)")
      }
}
~~~
* POST方式
~~~bash
	let parameters = [
            "parameter1": "aaa",
            "parameter2":  1
        ]


        Alamofire.request(.POST, "urlStr", parameters:parameters ).responseJSON {response in

//          debugPrint(response)
            switch response.result {
            case .Success:
                //把得到的JSON数据转为字典
                if let j = response.result.value as? NSDictionary{
                    //获取字典里面的key为数组
                    let Items = j.valueForKey("result")as! NSArray
                    //便利数组得到每一个字典模型
                    for dict in Items{

                        print(dict)
                    }

                }
            case .Failure(let error):

                print(error)
            }


        }
~~~

over！！！



# 转发请标明出处，谢谢！