---
layout: post
title:  "mysql更改root密码"
date:   2021-04-03 14:42:00 +0800
categories: mysql
author:  Zee-hash
tags:  ["password", "mysql", "linux"]
---
> 由于通过apt安装的mysql没有密码配置过程，故需手动配置

## 第一次登录  
在第一次登录前确保mysql服务已经启动
```shell
$ systemctl status mysql-service
```
如果没有启动
```shell
$ sudo service mysql start
```
查看默认密码
```shell
$ sudo cat /etc/mysql/debian.cnf
```
使用文件中的用户名和密码完成登录
```shell
$ mysql -u debian-sys-maint -p
# 输入密码
```
## 修改密码
账号信息存储在名为mysql的数据库中
```shell
mysql> use mysql;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed

mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你想使用的密码';
Query OK, 0 rows affected (0.01 sec)

mysql> exit
Bye
```
完成Bye!