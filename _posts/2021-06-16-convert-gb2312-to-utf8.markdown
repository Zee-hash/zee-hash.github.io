---
layout: post
title:  "Convert encoding of text files"
date:   2021-06-16 17:20:00 +0800
categories: linux
author:  Zee-hash
tags:  ["linux", "gb2312", "UTF-8"]
---
## Install enca
```bash
$ sudo apt install enca
```

## Detect encoding of text files
```bash
$ enca -L zh_CN 下载说明.txt
Simplified Chinese National Standard; GB2312
  Mixed line terminators
```

## Convert encoding of text files
```bash
$ enca -L zh_CN -x UTF-8 下载说明.txt
# detect encoding of text files again after conversion
$ enca -L zh_CN 下载说明.txt 
Universal transformation format 8 bits; UTF-8
  Mixed line terminators
```