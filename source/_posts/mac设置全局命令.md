title: mac设置全局命令
date: 2016-06-12 14:51:13
categories:
- 学习
tags:
- 学习
---

在使用mac的时候，总有一些程序或者命令希望设为全局的，这里我用xx-net为例，详细记录配置的过程。

<!--more-->

## 先创建xx-net.sh文件，以我本地的为准，我是放在这个路径下的`/Users/dison/fastssh`

```bash
cd /Users/dison/fastssh
vi xx-net.sh
```

## 在xx-net文件里面写入

```bash 
#!/bin/bash

export XX_NET_HOME="/Users/dison/XX-Net"

#sh /Users/dison/XX-Net/start

sh $XX_NET_HOME/start
```

## 赋写的权限给`xx-net.sh文件`
```bash
chmod -x xx-net.sh
```

## 设置这个路径`/Users/dison/fastssh`为环境变量，修改本地的`.bash_profile`文件
```bash
export FASTSSH_HOME=/Users/dison/fastssh
export PATH=${PATH}:${FASTSSH_HOME}
```

## source一下`.bash_profile`
```bash
source .bash_profile 
```
之后就可以在终端里面任何的路径都可以直接运行xx-net.sh了。


# 转发标明出处，谢谢！！！