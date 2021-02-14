---
layout: post
title: 标准EOF分析
date: 2021-02-14
categories: blog
description: 
tags: [Software, EOF, NCL]
header-img: img/top.png    #这篇文章标题背景图片
---

## 标准EOF分析（标准经验正交分析）

标准EOF（又称特征向量，主成分）分析产生一系列正交的模态和时间序列。

EOF分析在数学上是严格的，但是并不是基于物理学。物理意义取决于分析人员对相应的数学结果的解释。

对于EOF的结果，一定要把空间模态和时间序列联系起来进行解释。比如，EOF正相位，本身没什么意义，必须要综合考虑时间序列，如果时间序列处在正相位，则表明这个区域的正相位增强，如果是温度变量的话，则表示增温信号。反过来，如果EOF负相位，而时间序列也处于负相位的话，也是一样的含义。如果时间序列处于正相位就是另外一种解释了。

也就是说，本质上，符号反转并不改变结果的意义。所以从某种意义上讲，可以通过反转符号（当然，必须在空间模态和时间序列上同时反转），使分解出来的空间模态和时间序列看起来比较符合物理意义，比如正相位->增温。

比较简单的使用NCL，当然NCL已经要退出历史舞台了。

NCL脚本：[点击这里](https://www.ncl.ucar.edu/Applications/Scripts/eof_1.ncl)

数据文件：[点击这里](ftp://ftp.cdc.noaa.gov/Datasets/ncep.reanalysis.derived/surface/slp.mon.mean.nc)

NCL结果：

<center>
<p><img src="/img/eof_20210214.png" align="center"></p>
</center>

## 相关参考资料

[EOF in IDL](http://www.idlcoyote.com/code_tips/eof_analysis.html), 不光是解释如何用IDL做EOF分析，也很仔细地解释了计算过程。

Daniel Wilks 的 [Statistical Methods in the Atmospheric Sciences](https://www.elsevier.com/books/statistical-methods-in-the-atmospheric-sciences/wilks/978-0-12-815823-4)，最新版应该是2019年的第四版。

Daniel Wilks 的第三版有中文译本：[大气科学中的统计方法](https://item.jd.com/12403725.html).