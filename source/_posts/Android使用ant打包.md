title: Android使用ant打包，集成到jenkins里面自动构建
date: 2015-09-16 20:32:05
categories:
- 学习
tags:
- Android
- Ant
---
## 先安装ant
以下安装教程是mac系统的，至于win系统的安装，相信配合Google也很简单，这里就不再介绍。
mac下安装ant很简单，就一条命令，前提是要安装了Homebrew，什么？你没安装Homebrew？？那不好意思，自己Google去。
> 首先更新一下
~~~bash
brew update
~~~
> 然后再执行
~~~bash
brew install ant
~~~
<!--more-->
这样就可以成功的安装了ant

## 测试ant

在终端直接输入
~~~bash
ant
~~~
如果输出
> Buildfile: build.xml does not exist!
> Build failed

那么恭喜你，ant安装成功！

## 在Android工程下面生成ant脚本

* 在sdk/tools目录下执行下面的命令，注意将命令里面的目录改成你的工程的目录，name后面的名字也改成你自己的工程名字
~~~bash
android update project --name dison --target  android-21 --path /Users/dison/Documents/workspace4.4/dison-ant-test
~~~

* 如果你的工程没问题，就会在目录下生成2个文件，build.xml和local.properties,打开local.properties，可看到其实是一个sdk环境配置

* 在工程目录新建ant.properties，将下面的配置信息添加到该文件中，注意将keystore的信息改成你的
> key.store=/home/android/xxxxxxx.releasekey
> key.alias=android
> key.store.password=password
> key.alias.password=password

* 修改工程里面的build.xml文件，因为build执行的target是help，这里我们要修改为release
  如下：
  
~~~bash
<target name="release"
       depends="clean, -set-release-mode, -release-obfuscation-check, -package, -post-package, -release-prompt-for-password, -release-nosign, -release-sign, -post-build"
       description="Builds the application in release mode.">
</target>

<import file="${sdk.dir}/tools/ant/build.xml" />
~~~

把文件头改为
~~~bash
	<project name="cxy" default="release">
~~~

* 打包，直接在eclipse执行，或者使用ant release命令

## 项目依赖处理
如果你的项目依赖了别的项目，只需要在依赖的项目中也生成build.xml和local.properties，因为在project.properties中已经能读取到依赖关系，build.xml会根据这个文件自动依赖并打入包中的。
依赖的项目不用修改build.xml文件

## 把打包集合到jenkins
* 系统配置修改，增加SSH Servers，即是打包编译后的系统的目标服务器，具体配置如图所示（只需要配置一次）
![](http://120.24.60.216:4000/img/20150918133023.png)
* 创建项目，点击jenkins主页左上角的新建
![](http://120.24.60.216:4000/img/20150916211326.png)
给项目起个名字，这里以车小丫为例，命名为cxy，之后选择自由风格创建项目
* 配置项目svn路径，web项目和app项目都要配置，依赖的项目也要配置进来，最好配置在web项目和app项目的之前，如图
![](http://120.24.60.216:4000/img/20150918142922.png)
* 配置“构建”点“增加构建步骤“按钮，选择invoke Ant(如果无此选项，说明你没有安装ant插件，请安装插件），配置完“invoke Ant”点“Send files or execute commands over SSH“配置ssh
具体配置如图
![](http://120.24.60.216:4000/img/20150918144733.png)

至此，Android使用ant打包，集成到jenkins里面自动构建就配置完成，其他项目也可以依样画葫芦自己实现了。

# 转发请标明出处，谢谢！