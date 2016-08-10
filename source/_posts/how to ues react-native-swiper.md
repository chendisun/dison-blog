title: React Native图片轮播实现
date: 2015-10-08 10:56:15
categories:
- 学习
tags:
- React Native iOS Android
---

## 下载第三方的组件react-native-swiper

* 这里的轮播实现我使用的是第三方的组件，详细的简介可以到github上查看，github地址是：[https://github.com/leecade/react-native-swiper](https://github.com/leecade/react-native-swiper "")
在项目的根目录执行如下命令安装模块：

~~~bash
$ npm install react-native-swiper --save
$ npm i react-timer-mixin --save
~~~

<!--more-->

* 需要关闭React packager命令行和模拟器，在xcode中重启项目

## 代码修改

* 首先使用require引入react-native-swiper
~~~javascript
var Swiper = require('react-native-swiper');
~~~

* 使用swiper,将轮播封装成单独的组件

~~~javascript
var Slider = React.createClass({
    render: function(){
    return (
      <Swiper showsButtons={true} autoplay={true} showsPagination={true}>
        <View style={{backgroundColor: 'red',flex: 1}}></View>
        <View style={{backgroundColor: 'blue',flex: 1}}></View>
        <View style={{backgroundColor: 'green',flex: 1}}></View>
      </Swiper>
    );
  }
});
~~~

* 这样可以直接在render的时候直接用：<Slider/>

~~~javascript
var aaa = React.createClass({
  render: function() {
    return (
      <View style={styles.aaa}>
        <Slider/>
      </View>
    );
  }
});
~~~

* 效果图
![](http://120.24.60.216:4000/img/20151008111535.png)





# 转发请标明出处，谢谢！