title: linux下使用ffmpeg将amr转成mp3
date: 2016-02-25 14:59:20
categories:
- 学习
tags:
- linux ffmpeg
---

## 背景
项目有需求把amr格式的音频转换成mp3格式在浏览器播放，所以我们打算使用ffmpeg实现这部分的功能。

<!--more-->

## yasm：汇编器，新版本的ffmpeg增加了汇编代码

~~~bash
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar -xzvf yasm-1.3.0.tar.gz
cd yasm-1.3.0
./configure
make
make install
~~~

## lame：Mp3音频解码
~~~bash
wget http://jaist.dl.sourceforge.net/project/lame/lame/3.99/lame-3.99.5.tar.gz
tar -xzvf lame-3.99.5.tar.gz
cd lame-3.99.5
./configure
make
make install
~~~

## amr支持
~~~bash
wget http://downloads.sourceforge.net/project/opencore-amr/opencore-amr/opencore-amr-0.1.3.tar.gz
tar -xzvf opencore-amr-0.1.3.tar.gz
cd opencore-amr-0.1.3
./configure
make
make install
~~~

## amrnb支持
~~~bash
wget http://www.penguin.cz/~utx/ftp/amr/amrnb-11.0.0.0.tar.bz2
tar -xjvf amrnb-11.0.0.0.tar.bz2
cd amrnb-11.0.0.0
./configure
make
make install
~~~

## amrwb支持
~~~bash
wget http://www.penguin.cz/~utx/ftp/amr/amrwb-11.0.0.0.tar.bz2
tar -xjvf amrwb-11.0.0.0.tar.bz2
cd amrwb-11.0.0.0
./configure
make
make install
~~~

## ffmpeg
~~~bash
wget http://ffmpeg.org/releases/ffmpeg-2.5.3.tar.bz2
tar -xjvf ffmpeg-2.5.3.tar.bz2
cd ffmpeg-2.5.3
./configure --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-version3 --enable-shared
make
make install
~~~

[资源下载](http://120.24.60.216:4000/resources/ffmpeg安装文件和教程.tar.gz "资源下载")

# 转发自http://my.oschina.net/ethan09/blog/372435?fromerr=OjFebdNT