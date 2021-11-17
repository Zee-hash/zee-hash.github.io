---
layout: post
title:  "切换Ubuntu上Python3命令默认使用版本"
date:   2021-11-17 21:25:00 +0800
categories: markdown
author:  Zee-hash
tags:  ["python3.9", "Ubuntu", "version"]
---
> 由于需要编译一个使用Python3.9的软件，安装了后发现默认调用的Python3使用的是自带的python3.8版本，所以尝试修改。  

## 目前的情况  
```bash
$ ls /usr/bin/python* -l

lrwxrwxrwx 1 root root       9 Jul 31 15:13 /usr/bin/python3 -> python3.8
-rwxr-xr-x 1 root root 5490488 Sep 29 00:10 /usr/bin/python3.8
lrwxrwxrwx 1 root root      33 Sep 29 00:10 /usr/bin/python3.8-config -> x86_64-linux-gnu-python3.8-config
-rwxr-xr-x 1 root root 5803936 May 19 19:32 /usr/bin/python3.9
lrwxrwxrwx 1 root root      33 May 19 19:32 /usr/bin/python3.9-config -> x86_64-linux-gnu-python3.9-config
lrwxrwxrwx 1 root root      16 Mar 13  2020 /usr/bin/python3-config -> python3.8-config
```  
从中可以看到实际上Python3目前是链接到python3.8的，为了指向且不影响系统其它功能的正常使用，使用`update-alternatives`  

## 使用说明  
+ 查看python的可替换版本信息  
```bash
update-alternatives --list python3
```  

+ 如果python3的可替换版本尚未被update-alternatives识别到，则可以通过以下命令添加：  
```bash
$ 5
update-alternatives: using /usr/bin/python3.8 to provide /usr/bin/python3 (python3) in auto mode
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 2
$ update-alternatives --list python3
/usr/bin/python3.8
/usr/bin/python3.9
```
+ 使用
```bash
$ sudo update-alternatives --config python3
There are 2 choices for the alternative python3 (providing /usr/bin/python3).
  Selection    Path                Priority   Status
------------------------------------------------------------
* 0            /usr/bin/python3.9   5         auto mode
  1            /usr/bin/python3.8   5         manual mode
  2            /usr/bin/python3.9   2         manual mode
```
