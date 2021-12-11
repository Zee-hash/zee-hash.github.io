---
layout: post
title:  "在我的云服务器上跑jupyter notebook"
date:   2021-12-11 18:08:00 +0800
categories: markdown
author:  Zee-hash
tags:  ["Jupyter notebook", "remote server"]
---

> 随时随时修改查看我的笔记  

## 更改jupyter notebook的密码  
```bash
$ jupyter notebook password
```  

## 修改jupyter notebook的配置文件
### 该文件在各系统中的位置如下  
+ Windows: C:\Users\USERNAME\.jupyter\jupyter_notebook_config.py
+ OS X: /Users/USERNAME/.jupyter/jupyter_notebook_config.py
+ Linux: /home/USERNAME/.jupyter/jupyter_notebook_config.py  

### 如果上述文件夹或文件不存在，则执行以下命令  
```bash
$ jupyter notebook --generate-config
```  

### 在文件末尾增加如下内容  
```
# 服务器地址
c.NotebookApp.ip = 'localhost'
# 默认不打开浏览器
c.NotebookApp.open_browser = False
# 端口，用于客户端绑定
c.NotebookApp.port = <port>
```  

## 本地电脑设置ssh连接 
### 启动【非root用户不需要加方框内参数，直接启动即可】
```
$ jupyter notebook [--allow-root]
```  

### 远程连接服务器
```bash
ssh -i your_server.pem root@your_server_public_ip -L 127.0.0.1:<local_port>:127.0.0.1:<server_port>
```  

### 本地浏览器
访问`localhost:<lobal_port>`，输入之前设置的密码即可访问远程服务器中的notebook。