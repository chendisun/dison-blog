title: iOS版React-Native使用NavigatorIOS
date: 2015-09-29 18:16:15
categories:
- 学习
tags:
- iOS
- React Native
---
用React-Native开发iOS应用的时候，大多数情况下我们要使用导航栏的，这里简单对导航栏做个使用记录

## 定义NavigatorIOS

~~~javascript
var {
  AppRegistry,
  StyleSheet,
  NavigatorIOS,
  View,
  Text,
} = React;

~~~
<!--more-->

可以看到在React里面我定义了一个NavigatorIOS，这样后面的代码就可以调用NavigatorIOS了。

## 使用NavigatorIOS

~~~javascript
var HelloWorld = React.createClass({
  render: function() {
    return (
      <NavigatorIOS
        style={styles.container}
        initialRoute={{
            title: '首页',
            component: aaa,
        }}
      />
    );
  }
});
~~~

这里NavigatorIOS里面需要使用aaa面板，所以要创建aaa类

~~~javascript
var aaa = React.createClass({
  render: function() {
    return (
      <View style={styles.aaa}><Text style={styles.bbb}>你妹</Text></View>
    );
  }
});
~~~

## styles修改

~~~javascript
var styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  aaa: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  bbb: {
    fontSize: 15,
    color: 'blue'
  }
});
~~~

## 运行结果如下
![](http://120.24.60.216:4000/img/20150929181355.png)





# 转发请标明出处，谢谢！