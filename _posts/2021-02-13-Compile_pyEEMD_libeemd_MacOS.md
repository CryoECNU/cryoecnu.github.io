---
layout: post
title: 编译libeemd并安装pyeemd
date: 2021-02-13
categories: blog
description: 
tags: [Software, EEMD, MacOS, conda]
header-img: img/top.png    #这篇文章标题背景图片
---

1. **目标**：编译libeemd并安装pyeemd
2.  **操作系统**：MacOS 10.15
3.  **python环境**：conda，python 3.7+
4. **软件需求**：gsl，make，gcc, pkg-config

## libeemd编译步骤

- 下载libeemd：[Download](https://bitbucket.org/luukko/libeemd/downloads/)
- 解压缩，进入解压缩后的目录
- make
- 编译出来的文件：eemd.h, libeemd.a, libeemd.so, libeemd.so.1.4.1, libeemd.so.1.4.1.dSYM，这些是pyeemd需要调用的。

【已知问题】：

- 可能会找不到头文件，比如"*.h"之类的文件，则需要从下面的文件夹中拷贝：/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include，到目标文件夹：miniconda3安装目录下面的include文件夹。

## pyeemd安装步骤

- 下载pyeemd：[Download](https://bitbucket.org/luukko/pyeemd/downloads/)
- 解压缩，进入解压缩后的目录
- `./setup.py install`
- 把eemd.h, libeemd.a, libeemd.so, libeemd.so.1.4.1, libeemd.so.1.4.1.dSYM都拷贝到pyeemd在miniconda3的安装目录下，比如：miniconda3/lib/python3.7/site-packages/pyeemd-1.4-py3.7.egg/pyeemd

## 测试是否可以调用

`python -c "import pyeemd"`

没有报错就基本上可以了。
