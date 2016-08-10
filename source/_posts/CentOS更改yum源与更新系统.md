title: CentOS更改yum源与更新系统
date: 2016-06-07 19:31:13
categories:
- 学习
tags:
- Java
---

## 首先备份/etc/yum.repos.d/CentOS-Base.repo
```bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

<!--more-->

## 进入yum源配置文件所在文件夹
```bash
[root@localhost yum.repos.d]# cd /etc/yum.repos.d/
```
## 下载163的yum源配置文件，放入/etc/yum.repos.d/(操作前请做好相应备份)
```bash
[root@localhost yum.repos.d]# wget http://mirrors.163.com/.help/CentOS6-Base-163.repo
```
## 运行yum makecache生成缓存
```bash
[root@localhost yum.repos.d]# yum makecache
```
## 更新系统
```bash
[root@localhost yum.repos.d]# yum -y update
```
## 安装vim编辑器
```bash
[root@localhost ~]# yum -y install vim*
```










# 转发自[http://www.cnblogs.com/lightnear/archive/2012/10/03/2710952.html](http://www.cnblogs.com/lightnear/archive/2012/10/03/2710952.html)，谢谢！