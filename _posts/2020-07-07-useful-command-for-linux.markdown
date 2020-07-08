---
layout: post
title:  "Useful linux command"
date:   2020-07-07 16:56:00 +0800
categories: linux
author:  Zee-hash
tags:  ["manual", "linux"]
---
## INDEX  
[whatis](#whatis)  
[which](#which)  
[echo](#echo)  
[screen](#screen)  

## whatis
> display one-line manual page descriptions.  

ex:
```bash
$ whatis rm
rm (1)               - remove files or directories
```  
## which  
> locate a command  

ex:
```bash
$ which python
/home/zee-hash/anaconda3/bin/python
```

## echo  
> display a line of text  

ex:
```bash
$ echo $SHELL
/bin/bash

$ echo "$SHELL"
/bin/bash

# 原样输出
$ echo '$SHELL'
$SHELL

# 执行``中的命令
$ echo `whatis echo`
echo (1) - display a line of text
```
## screen  
> screen manager with VT100/ANSI terminal emulation  

ex:
```bash
# 新建
$ screen -S name
# 查看所有
$ screen -ls
# 临时退出
Ctrl + A + D
# 恢复，仅有一个时可省略name
$ screen -r name

$ screen -ls
There is a screen on:
	3830.bomb	(07/06/2020 11:19:37 AM)	(Detached)
1 Socket in /run/screen/S-root.

$ screen -r 3830/bomb
```