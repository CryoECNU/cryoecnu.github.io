---
layout: post
title: MacOS下编译NCAR的汇流模型mizuRoute
date: 2021-10-05
categories: blog
description: 
tags: [Software, Linux, MacOS, HTTPS]
header-img: img/top.png    #这篇文章标题背景图片
---

很多陆面过程模式或者分布式水文模型都是输出的栅格runoff结果，并不是通常测量的出口断面径流。

NCAR他们开发了一个独立的runoff routing工具，能够从栅格runoff到流域径流。这个工具可以通过河网的相关参数（包括坡度之类），计算出来任意位置上游控制区域产生的流量。

具体参数解释：https://mizuroute.readthedocs.io/en/master/
示例数据：https://mizuroute.readthedocs.io/en/master/testCase.html

后面慢慢再看如何制备这些input数据。先把它编译出来，用例子数据跑一下看看能不能出结果吧

已经用MACPORTS安装了netcdf库和gcc，这里就省了事了。直接设置路径就行了。

进入源码根目录下面的route/build，用文本编辑器打开Makefile。

```
FC = gnu

FC_EXE = gfortran-mp-11

EXE = runoff_route

F_MASTER = /Users/<username>/Documents/GitHub/mizuRoute/route/

NCDF_PATH = /opt/local/
```

然后在terminal里面make一下。

如果不报错，那么就会在源码根目录下面的route/bin下面生成runoff_route的可执行文件。

可以拷贝到案例数据文件夹下面的bin目录里

再运行：

./bin/runoff_route settings/v1.2/testCase_cameo_case3.control

<center>
<p><img src="/img/WX20211005-165939@2x.png" align="center"></p>
</center>

完了就会在output文件夹下面保存结果。