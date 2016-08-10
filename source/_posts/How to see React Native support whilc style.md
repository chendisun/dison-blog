title: React Native 如何知道该组件支持哪些样式呢
date: 2015-09-25 16:32:05
categories:
- 学习
tags:
- Android
- iOS
- React Native
---
在用React Native开发的时候，有些组件的样式我们会不知道，但是我们怎样才能知道组件支持什么样式呢？
查看文档是一个好方法，但是查看文档毕竟不够方便，下面我介绍一种比较实用的方法。

## 修改index.ios.js代码

~~~bash
'use strict';

var React = require('react-native');
var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Image,
} = React;

var HelloWorld = React.createClass({
  render: function() {
    return (
      <View>
          <View style={styles.style_1}>

          </View>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  style_1: {
    height:40,
    borderWidth: 1,
    borderColor: 'red',
    aaa: 's'
  },
});

AppRegistry.registerComponent('HelloWorld', () => HelloWorld);

~~~
<!--more-->

可以看到在styles里面的样式style_1里，我乱写了一个样式```aaa: 's'```，这时运行工程，就会看到如下的结果
![](http://120.24.60.216:4000/img/20150925162728.png)

这个时候我们就可以看到当前组件支持的样式了，是不是很简单？但是这个方法必须写到样式的创建中去，而不能写为内联样式。写成内联样式，你是看不到报错提示的。




# 转发请标明出处，谢谢！