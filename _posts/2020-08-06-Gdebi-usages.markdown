---
layout: post
title:  "A simple tool to install deb files"
date:   2020-08-06 18:41:51 +0800
categories: linux
author:  Zee-hash
tags:  ["deb files' dependencies", "linux"]
---

> I stumbled upon this useful tool when I was installing a software named "nutstore".  

install via .deb and resolve dependence using gdebi
```bash
$ sudo gdebi  ***.deb
```

## Install Gdebi 
```shell
$ sudo apt install gdebi
```  

## Use Gdebi  
### Terminal
```shell
$ sudo gdebi <package_name>.deb
```  
### GUI  
+ Right-click the deb installation package and select "Open With Other Application".   
+ Select "GDebi Package Installer" in the list. 
+ Then you will see information about the package. You can also choose to install or uninstall this software in the interface.

![软件界面](/assets/images/post_images/20200806information-of-packages.png)  

![软件界面2](/assets/images/post_images/20200806information-of-packages-2.png)  