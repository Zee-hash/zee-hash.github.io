---
layout: post
title:  "Markdown代码块缩进"
date:   2021-11-07 09:48:00 +0800
categories: markdown
author:  Zee-hash
tags:  ["markdown", "notes", "codeblock"]
---
## 目标缩进样式  
+ 第一级  
    + 第二级   

```python
print('hello world')
```  
+  我想继续接着出现第二级

## 利用更多的四个空格缩进  
> 问题的关键在于让代码能够在其所处的层级，而不是在其默认的第一级，可能相对来说麻烦的一点就是所有的代码需要需要多缩进四个空格，代码量大的情况下相对耗时。    
+ 第一级  
    + 第二级
    <!--首先，需要在这一行需要添加一个空行-->
            print('hello world')
    <!--在代码前需要增加空格，tab无法起到相同的效果-->
    + 第二级  
+ 第一级
