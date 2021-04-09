---
layout: post
title:  "C++中运算符的优先级"
date:   2021-04-09 20:56:00 +0800
categories: dev
author:  Zee-hash
tags:  ["C++", "opreator precedence"]
---

> C++中的运算符优先级

| 结合律 | 运算符 | 功能 | 用法 |  
| :---: | :---: |  :---: |  :---: |
| 左 | :: |全局作用域|::name|
| 左 | :: |类作用域|class::name|
| 左 | :: |类名空间作用域|namespace::name|

------

| 结合律 | 运算符 | 功能 | 用法 |  
| :---: | :---: |  :---: |  :---: |
|左|.|成员选择|object.member|
|左|->|成员选择|pointer->member|
|左|\[\]|下标|expr\[expr\]|
|左|()|函数调用|name(expr_list)|
|左|()|类型构造|type(expr_list)|

------

| 结合律 | 运算符 | 功能 | 用法 |  
| :---: | :---: |  :---: |  :---: |
|右|++|后置递增运算|lvalue++|
|右|--|后置递增运算|lvalue--|
|右|typeid|类型ID|typeid(type)|
|右|typeid|运行时类型ID|typeid(expr)|
|右|explicit cast|类型转换|case_name\<type\>(expr)|

------
